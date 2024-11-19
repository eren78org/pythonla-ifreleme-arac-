# pythonla-ifreleme-arac-
python ile şifreleme aracı 
from cryptography.fernet import Fernet

# Anahtar oluşturma ve kaydetme
def create_key():
    key = Fernet.generate_key()
    with open("encryption_key.key", "wb") as key_file:
        key_file.write(key)
    print("Anahtar oluşturuldu ve kaydedildi: encryption_key.key")

# Anahtarı yükleme
def load_key():
    try:
        with open("encryption_key.key", "rb") as key_file:
            return key_file.read()
    except FileNotFoundError:
        print("Anahtar dosyası bulunamadı. Lütfen önce anahtar oluşturun.")
        return None

# Metni şifreleme
def encrypt_message(message, key):
    fernet = Fernet(key)
    encrypted_message = fernet.encrypt(message.encode())
    print("Şifrelenmiş mesaj:")
    print(encrypted_message.decode())
    return encrypted_message

# Şifreli metni çözme
def decrypt_message(encrypted_message, key):
    fernet = Fernet(key)
    decrypted_message = fernet.decrypt(encrypted_message).decode()
    print("Çözülmüş mesaj:")
    print(decrypted_message)
    return decrypted_message

# Ana menü
def main():
    print("Şifreleme ve Şifre Çözme Aracı")
    print("1. Anahtar Oluştur")
    print("2. Mesaj Şifrele")
    print("3. Şifre Çöz")
    print("4. Çıkış")
    
    key = load_key()
    while True:
        choice = input("\nBir seçenek seçin (1-4): ")
        
        if choice == "1":
            create_key()
            key = load_key()
        elif choice == "2":
            if not key:
                print("Lütfen önce bir anahtar oluşturun.")
                continue
            message = input("Şifrelemek istediğiniz mesajı girin: ")
            encrypt_message(message, key)
        elif choice == "3":
            if not key:
                print("Lütfen önce bir anahtar oluşturun.")
                continue
            encrypted_message = input("Şifrelenmiş mesajı girin: ").encode()
            decrypt_message(encrypted_message, key)
        elif choice == "4":
            print("Programdan çıkılıyor...")
            break
        else:
            print("Geçersiz seçenek, lütfen tekrar deneyin.")

if __name__ == "__main__":
    main()
