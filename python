import os from flask import Flask, render_template, request, send_file from Crypto.Cipher import AES from Crypto.Util.Padding import pad, unpad from werkzeug.utils import secure_filename 
# Flask App Initialization 
app = Flask(__name__) 
UPLOAD_FOLDER = "uploads" 
ENCRYPTED_FOLDER = "encrypted" DECRYPTED_FOLDER = "decrypted" app.config["UPLOAD_FOLDER"] = UPLOAD_FOLDER app.config["ENCRYPTED_FOLDER"] = ENCRYPTED_FOLDER app.config["DECRYPTED_FOLDER"] = DECRYPTED_FOLDER 
# Ensure folders exist 
for folder in [UPLOAD_FOLDER, ENCRYPTED_FOLDER, DECRYPTED_FOLDER]: 
    os.makedirs(folder, exist_ok=True) # AES Encryption/Decryption Class class SecureFile:     def __init__(self, key): 
        self.key = key[:32].encode()  # Ensure the key is 32 bytes 
     def encrypt_file(self, input_path, output_path):
 cipher = AES.new(self.key, AES.MODE_CBC)
          with open(input_path, 'rb') as f: 
            plaintext = f.read() 
        ciphertext = cipher.encrypt(pad(plaintext, AES.block_size))         with open(output_path, 'wb') as f: 
            f.write(cipher.iv + ciphertext)  # Store IV in the file         print(f"Encrypted file saved to: {output_path}")     def decrypt_file(self, input_path, output_path):         with open(input_path, 'rb') as f:             iv = f.read(16)  # Read IV             ciphertext = f.read() 
        cipher = AES.new(self.key, AES.MODE_CBC, iv)         plaintext = unpad(cipher.decrypt(ciphertext), AES.block_size)         with open(output_path, 'wb') as f: 
            f.write(plaintext) 
        print(f"Decrypted file saved to: {output_path}") 
# Encryption Key (MUST BE 32 CHARACTERS) 
ENCRYPTION_KEY = "MySecureEncryptionKey12345678901234" secure = SecureFile(ENCRYPTION_KEY) 
# Home Route (Serves HTML) 
@app.route("/") def index(): 
    return render_template("index.html") 
# Encrypt File Route 
@app.route("/encrypt", methods=["POST"]) 
 
def encrypt():     if "file" not in request.files:         return "No file uploaded", 400     file = request.files["file"]     if file.filename == "": 
        return "No file selected", 400     filename = secure_filename(file.filename)     file_path = os.path.join(app.config["UPLOAD_FOLDER"], filename) 
    encrypted_path = os.path.join(app.config["ENCRYPTED_FOLDER"], f"encrypted_{filename}") 
    file.save(file_path)  # Save original file 
    try: 
        secure.encrypt_file(file_path, encrypted_path)  # Encrypt file     except Exception as e: 
        return f"Error during encryption: {str(e)}", 500     os.remove(file_path)  # Remove the original file after encryption     return send_file(encrypted_path, as_attachment=True) 
# Decrypt File Route 
@app.route("/decrypt", methods=["POST"]) 
def decrypt(): 
    if "file" not in request.files: 
        return "No file uploaded", 400     file = request.files["file"]     if file.filename == "":  
        return "No file selected", 400     filename = secure_filename(file.filename)     file_path = os.path.join(app.config["UPLOAD_FOLDER"], filename) 
    decrypted_path = os.path.join(app.config["DECRYPTED_FOLDER"], f"decrypted_{filename}") 
    file.save(file_path)  # Save encrypted file 
    try: 
        secure.decrypt_file(file_path, decrypted_path)  # Decrypt file     except Exception as e: 
        return f"Error during decryption: {str(e)}", 500     os.remove(file_path)  # Remove the encrypted file after decryption     return send_file(decrypted_path, as_attachment=True) 
# Run the Flask App if __name__ == "__main__": 
    app.run(debug=True) 
