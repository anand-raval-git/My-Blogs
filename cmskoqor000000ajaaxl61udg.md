---
title: "AWS Day 41: Securing Data with AWS KMS | Kodekloud 100 DaysOfCloud"
seoTitle: "AWS Day 41: Securing Data with AWS KMS"
seoDescription: "A practical AWS KMS tutorial covering symmetric key creation, file encryption, base64 decoding, decryption, and data verification using AWS CLI."
datePublished: 2026-08-08T18:06:34.984Z
cuid: cmskoqor000000ajaaxl61udg
slug: aws-day-41-securing-data-with-aws-kms-kodekloud-100-daysofcloud
cover: https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/1a6be59a-57d8-44f9-916f-6a307fb3658b.png
ogImage: https://cdn.hashnode.com/uploads/og-images/6683e9700c2137ac86599d6e/1c136db7-941c-4310-9ec7-3522e4b8097d.png
tags: aws, aws-kms, kodekloud, kodekloudengineer, anand-raval

---

## What is AWS KMS?

**AWS Key Management Service (AWS KMS)** is an AWS service used to create and control cryptographic keys that can be used to protect data.

Instead of manually managing encryption keys, AWS KMS provides a centralized way to manage keys and control who can use them.

In this task, I created a **symmetric KMS key** and used it for both encryption and decryption.

## Task Overview

The Nautilus DevOps team wanted to improve the security of sensitive data using AWS KMS.

The requirements were:

1.  Create a symmetric KMS key named `devops-KMS-Key`.
    
2.  Encrypt the existing `SensitiveData.txt` file.
    
3.  Base64-decode the encrypted ciphertext.
    
4.  Save the encrypted data as `EncryptedData.bin`.
    
5.  Decrypt the encrypted file.
    
6.  Verify that the decrypted content matches the original data.
    

## Step 1: Create a Symmetric KMS Key

The first step was to create a customer-managed KMS key.

From the AWS KMS console:

**AWS Console → KMS → Customer managed keys → Create key**

For the key configuration, I selected:

*   **Key type:** Symmetric
    
*   **Key usage:** Encrypt and decrypt
    
*   **Alias:** `devops-KMS-Key`
    

The key was successfully created and appeared under **Customer managed keys** with an **Enabled** status.

### Key Alias

```plaintext
devops-KMS-Key
```

A KMS alias makes it easier to identify and reference a key instead of working directly with the complete key ID.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/ac98a5e7-ee90-4c42-b4a6-8284544c2ff5.png align="center")

## Step 2: Locate the Sensitive File

The sensitive file was already available on the AWS client:

```plaintext
/root/SensitiveData.txt
```

The file contained sensitive information that needed to be encrypted before being stored or used.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/47d44192-61af-4d30-8494-9e274c9f6bfc.png align="center")

## Step 3: Encrypt the File Using AWS KMS

After creating the KMS key, I used the AWS CLI to encrypt the file.

The command used was:

```plaintext
aws kms encrypt \
  --key-id eb56b040-5f4d-4161-a0c0-75addb3f24c0 \
  --plaintext SensitiveData.txt \
  --query CiphertextBlob \
  --output text \
  | base64 --decode > EncryptedData.bin
```

Let's understand what this command does.

### `aws kms encrypt`

This calls the AWS KMS encryption operation.

### `--key-id`

Specifies the KMS key used for encryption.

```plaintext
eb56b040-5f4d-4161-a0c0-75addb3f24c0
```

### `--plaintext`

Specifies the input file that needs to be encrypted.

```plaintext
SensitiveData.txt
```

### `--query CiphertextBlob`

The KMS encryption response contains the encrypted data inside `CiphertextBlob`.

### `--output text`

Returns the result as text.

### `base64 --decode`

The AWS CLI returns the ciphertext in Base64-encoded form, so it is decoded into its binary representation.

### `> EncryptedData.bin`

Finally, the decoded encrypted data is saved as:

```plaintext
EncryptedData.bin
```

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/aeb91a1a-2178-44ff-befc-b888cfe529e9.png align="center")

## Step 4: Verify the Encrypted File

After running the encryption command, the encrypted file was created successfully.

```plaintext
EncryptedData.bin
```

The important point here is that the file is no longer stored as the original readable plaintext.

Instead, it contains the encrypted ciphertext generated using the KMS key.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/a5512244-894d-4d6c-a326-4ccf823d9b2d.png align="center")

## Step 5: Decrypt the Encrypted File

Next, I tested whether the encrypted data could be successfully decrypted using the same KMS key.

The following AWS CLI command was used:

```plaintext
aws kms decrypt \
  --ciphertext-blob fileb://EncryptedData.bin \
  --query Plaintext \
  --output text \
  | base64 --decode > decode.txt
```

This command performs the reverse operation.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/d5a309e7-124f-4f64-b072-2a12b663efc5.png align="center")

## Step 6: Verify the Decrypted Data

Finally, I checked the decrypted file:

```plaintext
cat decode.txt
```

The output was:

```plaintext
This is a sensitive file.
```

The decrypted content matched the original `SensitiveData.txt` file.

![](https://cdn.hashnode.com/uploads/covers/6683e9700c2137ac86599d6e/2bbb1b18-95c9-4210-9014-0dab2f47a58b.png align="center")

## Conclusion

AWS KMS provides a secure way to create and manage encryption keys without having to build a complete key management system from scratch.

In this Day 41 hands-on task, I created a symmetric KMS key named `devops-KMS-Key`, encrypted `SensitiveData.txt`, converted the returned Base64 ciphertext into `EncryptedData.bin`, and successfully decrypted the file again.

The final verification confirmed that the decrypted content matched the original sensitive data.

This was another useful hands-on exercise in understanding **AWS Security, Encryption, AWS KMS, and DevOps security practices**.