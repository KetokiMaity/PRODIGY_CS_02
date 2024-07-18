# PRODIGY_CS_02
Here I have developed a simple image encryption tool using pixel manipulation. Where you can perform operations like swapping pixel values or applying a basic mathematical operation to each pixel. It also allows users to encrypt and decrypt images.
So, See my project below :

from PIL import Image

def encrypt_image(image_path, output_path, key):
    # Open the image
    img = Image.open(image_path)
    width, height = img.size

    # Convert image to RGB mode
    img_rgb = img.convert('RGB')

    # Create a new image to store the encrypted pixels
    encrypted_img = Image.new('RGB', (width, height))

    # Encrypt each pixel
    for x in range(width):
        for y in range(height):
            # Get the pixel value
            r, g, b = img_rgb.getpixel((x, y))
            
            # Perform encryption operation (e.g., addition with the key)
            r_encrypted = (r + key) % 256
            g_encrypted = (g + key) % 256
            b_encrypted = (b + key) % 256

            # Set the encrypted pixel value
            encrypted_img.putpixel((x, y), (r_encrypted, g_encrypted, b_encrypted))

    # Save the encrypted image
    encrypted_img.save(output_path)
    print("Image encrypted and saved successfully!")

def decrypt_image(image_path, output_path, key):
    # Open the encrypted image
    encrypted_img = Image.open(image_path)
    width, height = encrypted_img.size

    # Create a new image to store the decrypted pixels
    decrypted_img = Image.new('RGB', (width, height))

    # Decrypt each pixel
    for x in range(width):
        for y in range(height):
            # Get the encrypted pixel value
            r_encrypted, g_encrypted, b_encrypted = encrypted_img.getpixel((x, y))
            
            # Perform decryption operation (e.g., subtraction with the key)
            r_decrypted = (r_encrypted - key) % 256
            g_decrypted = (g_encrypted - key) % 256
            b_decrypted = (b_encrypted - key) % 256

            # Set the decrypted pixel value
            decrypted_img.putpixel((x, y), (r_decrypted, g_decrypted, b_decrypted))

    # Save the decrypted image
    decrypted_img.save(output_path)
    print("Image decrypted and saved successfully!")

def main():
    while True:
        choice = input("Do you want to encrypt or decrypt? (e/d): ").strip().lower()
        if choice not in ['e', 'd']:
            print("Invalid choice. Please enter 'e' for encryption or 'd' for decryption.")
            continue
        break
    
    image_path = input("Enter the path of the image file: ")
    output_path = input("Enter the output path for the result image: ")
    key = int(input("Enter the encryption/decryption key (an integer): "))

    if choice == 'e':
        encrypt_image(image_path, output_path, key)
    else:
        decrypt_image(image_path, output_path, key)

if __name__ == "__main__":
    main()
