from cryptography.fernet import Fernet
import os



base_path = "/Users/quinnesser/Documents/"

filename = input("Please enter file name here:").strip()


def Generate_key():
    return Fernet.generate_key()


def Encrypt(key, input_path, output_path):
    fernet = Fernet(key)
    with open(input_path, "rb") as file:
        original = file.read()
    encrypted = fernet.encrypt(original)
    with open(output_path, "wb") as file:
        file.write(encrypted)


def Decrypt(key, input_path, output_path):
    fernet = Fernet(key)
    with open(input_path, "rb") as file:
        original = file.read()
    decrypted = fernet.decrypt(original)
    with open(output_path, "wb") as file:
        file.write(decrypted)

if __name__ == "__main__":
    try:
        choice = input("Would you like to generate a new key? (Y/N): ").strip().upper()

        if choice == "Y":
            with open("file.key", "wb") as key_file:
                key_file.write(Generate_key())
            print("New key generated and saved to file.key.")


        with open("file.key", "rb") as key_file:
            key = key_file.read()


        input_path = os.path.join(base_path, filename)
        if not os.path.isfile(input_path):
            print("The specified file does not exist.")
            exit()


        choice2 = input("Press 1 for Encryption or 2 for Decryption: ").strip()
        if choice2 not in ("1", "2"):
            print("Invalid option.")
            exit()
