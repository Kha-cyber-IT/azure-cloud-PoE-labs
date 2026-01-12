# Day 40: Managing Secrets with Azure Key Vault

The Nautilus DevOps team is focusing on improving their data security by using Azure Key Vault. Your task is to create a Key Vault with a key and manage the encryption and decryption of a pre-existing sensitive file using this key.

Task Requirements:

- **Create a Key Vault:**
    - Name the Key Vault `nautilus-8957`.
    - Set access policies to allow **encryption** and **decryption** operations.
    - **Set Soft Delete retention** to `7` days.

- **Create a Key:**
    - Create a symmetric key named `nautilus-key` within the Key Vault for encryption and decryption operations.

- **Encrypt the Sensitive Data:**
    - Use the key to encrypt the provided `SensitiveData.txt` file (located in `/root/`) on the `azure-client` host.
    - **Base64 encode** the ciphertext and save the encrypted version as `EncryptedData.bin` in the `/root/` directory.

- **Verify Decryption:**
    - Attempt to decrypt `EncryptedData.bin` and verify that the decrypted data matches the original `SensitiveData.txt` file.

>[!Note]
> Ensure that the Key Vault and key are correctly configured. The validation script will test your configuration by decrypting the `EncryptedData.bin` file using the key you created.


## Task 1: Create a Key Vault:

1. Go to `Key vaults` and click `+ Create`.

   <img width="1365" height="488" alt="image" src="https://github.com/user-attachments/assets/896e9b6c-e0d9-4f0f-8d00-4291934c5eb6" />

2. Select default resource group, enter name and leave rest as default.

   <img width="1350" height="333" alt="image" src="https://github.com/user-attachments/assets/e772e547-6b30-4c85-909f-1a8e2142e5c5" />

3. Set `Soft delete retention period` to `7` days and click `Next`.

   <img width="1348" height="203" alt="image" src="https://github.com/user-attachments/assets/01172e91-a0f1-4595-8ca5-17683410f727" />

4. On the `Access configuration` tab, choose `Vault access policy` for `Permission model`.

   <img width="1351" height="377" alt="image" src="https://github.com/user-attachments/assets/8b37753e-57f4-44a7-bb92-5437afbf5a79" />

5. Next under `Access policy` section, click `+ Create`.

   <img width="1351" height="262" alt="image" src="https://github.com/user-attachments/assets/9f076800-d104-4239-b2d7-987f2ede072a" />

6. Set access policies to allow encryption and decryption operations and click `Next`.

   <img width="764" height="575" alt="image" src="https://github.com/user-attachments/assets/cd0312fc-074c-4bb1-b9a9-870dab1fb992" />

7. For `Principle`, select your Azure user or service principal and click `Save`.

   <img width="764" height="577" alt="image" src="https://github.com/user-attachments/assets/ed603ed6-32be-4f60-a9bf-3e14d6be73ef" />

8. From `Review + create` of `Create an access policy` box, click `Create`.

   <img width="764" height="574" alt="image" src="https://github.com/user-attachments/assets/af721ca5-b777-4543-870c-c851c3f09980" />

9. Create vault after validating all requirments.

    <img width="548" height="531" alt="image" src="https://github.com/user-attachments/assets/593b1ba6-40fd-471f-9a5a-b22c40a2ea3d" />


## Task 2: Create a symmetric key

1. Go to `Key vaults` and select `nautilus-8957`

   <img width="1365" height="274" alt="image" src="https://github.com/user-attachments/assets/c77e71d9-981d-4cb5-93d0-a7a886c8b003" />

2. From `` navigation menu, select `Objects` > `Keys` and click `+ Generate/Import`.

   <img width="203" height="494" alt="image" src="https://github.com/user-attachments/assets/628fefb3-2039-4cbb-ae2d-8766bb022f52" />

3. Enter a name of the key and selct `RSA` for `Key type` and click `Create`.

   <img width="982" height="540" alt="image" src="https://github.com/user-attachments/assets/36ce276e-d365-4299-9cfc-3b182796af0c" />

## Task 3: Encrypt the Sensitive Data

1. Login to Azure

   ```sh
   az login
   ```

2. Convert File to Base64

   ```sh
   base64 /root/SensitiveData.txt > /root/plaintext.b64
   ```

   **Azure Key Vault encrypts base64-encoded data**

3. Encrypt Using Key Vault

   ```sh
   az keyvault key encrypt \
    --vault-name nautilus-8957 \
    --name nautilus-key \
    --algorithm RSA-OAEP \
    --value "$(cat /root/plaintext.b64)" \
    --query result \
    -o tsv > /root/EncryptedData.bin
   ```

   **Expected:**

   ```
   EncryptedData.bin  plaintext.b64  SensitiveData.txt
   ```

## Task 4: Decrypt and Verify

1. Decrypt the file

   ```sh
   az keyvault key decrypt \
    --vault-name nautilus-8957 \
    --name nautilus-key \
    --algorithm RSA-OAEP \
    --value "$(cat /root/EncryptedData.bin)" \
    --query result \
    -o tsv > /root/decrypted.b64
   ```

   **Expected:**

   ```
   decrypted.b64  EncryptedData.bin  plaintext.b64  SensitiveData.txt
   ```

3. Convert Back to Original Text

   ```sh
   base64 --decode /root/decrypted.b64 > /root/DecryptedData.txt
   ```

   **Expected:**

   ```
   decrypted.b64  EncryptedData.bin  SensitiveData.txt  DecryptedData.txt  plaintext.b64
   ```
   
4. Verify Data Integrity

   ```sh
   diff /root/SensitiveData.txt /root/DecryptedData.txt
   ```

>[!Tip]
> **No output = verification successful**
