Creating a File Encryptor in Python
By Adel Dakhlallah



Step 1: Install Dependencies
To start working with file encryption, I first installed the necessary Python library for encryption:
This library provided the Fernet class, which implements symmetric encryption, ensuring secure file encryption and decryption with minimal overhead.
Step 2: Key Generation
For encryption, I generated a symmetric encryption key using Fernet, which ensures that both the encryption and decryption processes are secure and rely on the same key.
•	 I wrote a Python script that generates and saves the key securely.
python
Copy
from cryptography.fernet import Fernet

# Generate a secure key
key = Fernet.generate_key()

# Save the key to a file
with open("secret.key", "wb") as key_file:
    key_file.write(key)

print("Encryption key generated and saved.")
Step 3: File Encryption
The main feature of the tool is encrypting files. I created a Python function to securely encrypt files by reading them in binary mode, encrypting their contents, and saving the result.
•	 I wrote an encryption function to apply encryption to any file provided.
python
Copy
from cryptography.fernet import Fernet

def encrypt_file(file_path, key_path):
    # Load encryption key from file
    with open(key_path, "rb") as key_file:
        key = key_file.read()

    # Initialize Fernet encryption
    fernet = Fernet(key)

    # Read file in binary mode
    with open(file_path, "rb") as file:
        file_data = file.read()

    # Encrypt file data
    encrypted_data = fernet.encrypt(file_data)

    # Save encrypted data to a new file
    with open(file_path + ".encrypted", "wb") as encrypted_file:
        encrypted_file.write(encrypted_data)

    print(f"File '{file_path}' has been encrypted successfully.")

# Example usage:
encrypt_file("example.txt", "secret.key")
•	Outcome: After running the script, the file example.txt was securely encrypted into example.txt.encrypted, ensuring its confidentiality.
Step 4: File Decryption
I implemented a corresponding decryption function that takes the encrypted file and decrypts it back to its original form using the same key.
•	Action: I wrote a function to decrypt files, ensuring that only users with the correct key can restore the original file.
python
Copy
from cryptography.fernet import Fernet

def decrypt_file(encrypted_file_path, key_path):
    # Load the encryption key from file
    with open(key_path, "rb") as key_file:
        key = key_file.read()

    # Initialize Fernet decryption
    fernet = Fernet(key)

    # Read the encrypted file data
    with open(encrypted_file_path, "rb") as encrypted_file:
        encrypted_data = encrypted_file.read()

    # Decrypt the data
    decrypted_data = fernet.decrypt(encrypted_data)

    # Write decrypted data back to a file
    decrypted_file_path = encrypted_file_path.replace(".encrypted", ".decrypted")
    with open(decrypted_file_path, "wb") as decrypted_file:
        decrypted_file.write(decrypted_data)

    print(f"File '{encrypted_file_path}' has been decrypted successfully.")

# Example usage:
decrypt_file("example.txt.encrypted", "secret.key")
•	Outcome: After executing the decryption function, the encrypted file example.txt.encrypted was restored to its original state as example.txt.decrypted.
Step 5: Key Security and Management
To ensure the security of the encryption process, I focused on properly storing and managing the encryption key (secret.key). The key is the critical part of the encryption system, and losing it would make decryption impossible.
•	Action: I made sure to securely store the key file, using environment variables or hardware security modules (HSMs) in more advanced scenarios for added security.
Step 6: Testing and Documentation
To ensure the functionality and robustness of the encryption and decryption tool, I performed extensive testing with different file types and sizes. I also documented the process thoroughly for users to integrate it into their systems.
________________________________________
Challenges Overcome:
•	Key Management: Ensuring the encryption key is kept secure was a challenge. I implemented best practices for key storage and handling, such as using environment variables or encrypting the key.
•	File Size Handling: The tool handles files of various sizes, including large binary files, by reading them in chunks when needed (for even more advanced optimizations).
________________________________________
Outcome and Impact:
This project provided a simple and efficient way to protect sensitive files, and it could be expanded into a fully featured tool or service for securing various types of data. The tool can be integrated into a larger system where secure file transmission and storage are crucial.
________________________________________
Key Takeaways:
•	Learned how to implement encryption and decryption using the cryptography library.
•	Gained experience in key management and ensuring secure storage.
•	Enhanced my skills in file I/O, binary data handling, and security practices in Python.
