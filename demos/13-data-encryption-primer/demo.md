### 13-data-encryption-primer
##### GIVEN:
  - An AWS Cloud9 desktop from 00-setup-cloud9


##### WHEN:

  - I have a text file I want to encrypt
  - I fetch a Data Encryption Key (DEK) from KMS

##### THEN:
  - I can encrypt the file
  - I can encrypt the DEK

##### SO THAT:
  - I can see the how I can use 'envelope encryption'

##### NOTE: _This demo will provide CLI steps, but may have been demonstrated via the UI during a class delivery_

##### [Return to Main Readme](https://github.com/virtmerlin/mglab-share-archit-accel#demos)

---------------------------------------------------------------
---------------------------------------------------------------
#### REQUIRES
- 00-setup-cloud9

---------------------------------------------------------------
---------------------------------------------------------------
#### DEMO

##### 0: Reset C9 Instance env variables
- Reset your region & aws account variables in case you launched a new terminal session
```
cd ~/environment/mglab-share-archit-accel/demos/13-data-encryption-primer/
export C9_REGION=$(curl --silent http://169.254.169.254/latest/dynamic/instance-identity/document |  grep region | awk -F '"' '{print$4}')
export C9_AWS_ACCT=$(curl -s http://169.254.169.254/latest/dynamic/instance-identity/document | grep accountId | awk -F '"' '{print$4}')
clear
echo "C9_REGION=$C9_REGION"
echo "C9_AWS_ACCT=$C9_AWS_ACCT"
```
##### 1: Create a CMK in KMS
- Create CMK & add an alias to it:
```
export CMKJSON=$(aws kms create-key \
    --tags TagKey=CLASS,TagValue=ARCHIT-ACCEL \
    --description "Test key")
sudo yum install jq -y
echo $CMKJSON | jq .

aws kms create-alias \
    --alias-name alias/13-data-encryption-primer \
    --target-key-id $(echo $CMKJSON | jq .KeyMetadata.KeyId | tr -d '"')
```

##### 2: Encrypt a File & its DEK
- Create an Un-encrypted textfile:
```
echo "Sample Secret Text to Encrypt" > samplesecret.txt
```
- Fetch a DEK:
```
export DEK=$(aws kms generate-data-key --key-id alias/13-data-encryption-primer --key-spec AES_256 --encryption-context project=demo)

echo $DEK | jq -r .Plaintext | base64 --decode > datakeyPlainText.txt
echo $DEK | jq -r .CiphertextBlob | base64 --decode > datakeyEncrypted.txt
```
- Encrypt the textfile with the datakeyPlainText(unencrypted key):
```
openssl enc -e -aes256 -in samplesecret.txt -out encryptedSecret.txt -k fileb://datakeyPlainText.txt
more encryptedSecret.txt
```
- Delete the datakeyPlainText (unencrypted key) and the plain text secret text file, all you will have left if 2 encrypted files (data + DEK) that can be stored together and secured (Envelope Encrypted):
```
rm datakeyPlainText.txt samplesecret.txt
```

##### 2: Decrypt the DEK & its file
- Decrypt the encrypted DEK (Open the Envelope)
```
export DEKDECRYPT=$(aws kms decrypt --encryption-context project=demo --ciphertext-blob fileb://datakeyEncrypted.txt)
echo $DEKDECRYPT | jq -r .Plaintext | base64 --decode > datakeyPlainText.txt
```
- Decrypt the secret textfile, you should see the original unencrypted contents:
```
openssl enc -d -aes256 -in encryptedSecret.txt -k fileb://datakeyPlainText.txt
```

---------------------------------------------------------------
---------------------------------------------------------------
#### CLEANUP
Only run these scripts if you are done cleaning &/or running all dependent demos.
```
```
