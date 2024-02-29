# Cryptography---19CS412-classical-techqniques


# Caeser Cipher
Caeser Cipher using with different key values

# AIM:
  To encrypt and decrypt the given message by using Ceaser Cipher encryption algorithm.

# ALGORITHM:
1. In Ceaser Cipher each letter in the plaintext is replaced by a letter
some fixed number of positions down the alphabet.
2. For example, with a left shift of 3, D would be replaced by A, E would
become B, and so on.
3. The encryption can also be represented using modular arithmetic by first
transforming the letters into numbers, according to the scheme, A = 0, B =
1, Z = 25.
4. Encryption of a letter x by a shift n can be described mathematically as,
En(x) = (x + n) mod26
5. Decryption is performed similarly,
Dn (x)=(x - n) mod26
 

## PROGRAM:

def encrypt_text(plaintext, n):
    ans = ""
    for i in range(len(plaintext)):
        ch = plaintext[i]
        if ch == " ":
            ans += " "
        elif ch.isupper():
            ans += chr((ord(ch) + n - 65) % 26 + 65)
        else:
            ans += chr((ord(ch) + n - 97) % 26 + 97)
    return ans

def decrypt_text(ciphertext, n):
    ans = ""
    for i in range(len(ciphertext)):
        ch = ciphertext[i]
        if ch == " ":
            ans += " "
        elif ch.isupper():
            ans += chr((ord(ch) - n - 65) % 26 + 65)
        else:
            ans += chr((ord(ch) - n - 97) % 26 + 97)
    return ans

plaintext = input("Enter the plain text: ")
print("Plain Text is:", plaintext)
print("Key is:")
n = int(input())

cipher_text = encrypt_text(plaintext, n)
print("Cipher Text is:", cipher_text)

decrypted_text = decrypt_text(cipher_text, n)
print("Decrypted Text is:", decrypted_text)


## OUTPUT:

Enter the plain text: Smriti
Plain Text is: Smriti
Key is: 4
Cipher Text is: Wqvmxm
Decrypted Text is: Smriti

## RESULT:
The program is executed successfully

---------------------------------

# PlayFair Cipher
Playfair Cipher using with different key values

# AIM:

To develop a simple C program to implement PlayFair Cipher.

## DESIGN STEPS:

### Step 1:

Design of PlayFair Cipher algorithnm 

### Step 2:

Implementation using C or pyhton code

### Step 3:

Testing algorithm with different key values. 

## PROGRAM:

## OUTPUT:

## RESULT:
The program is executed successfully


---------------------------

# Hill Cipher
Hill Cipher using with different key values

# AIM:
To implement a program to encrypt and decrypt using the Hill cipher substitution
technique.

# ALGORITHM:
The Hill cipher is a substitution cipher invented by Lester S. Hill in 1929. Each letter is represented
by a number modulo 26. To encrypt a message, each block of n letters is multiplied by an invertible
n × n matrix, again modulus 26.
To decrypt the message, each block is multiplied by the inverse of the matrix used for encryption.
The matrix used for encryption is the cipher key, and it should be chosen randomly from the set of
invertible n × n matrices (modulo 26).
The cipher can, be adapted to an alphabet with any number of letters. All arithmetic just needs to be
done modulo the number of letters instead of modulo 26.

## PROGRAM:
import numpy as np
import math
keyMatrix = np.zeros((3, 3), dtype=int)
messageVector = np.zeros((3, 1), dtype=int)
cipherMatrix = np.zeros((3, 1), dtype=int)
def getKeyMatrix(key):
    k = 0
    for i in range(3):
        for j in range(3):
            if k < len(key):
                keyMatrix[i][j] = ord(key[k]) % 65
                k += 1
            else:
                keyMatrix[i][j] = 0
def encrypt(messageVector):
    global cipherMatrix
    cipherMatrix = np.dot(keyMatrix, messageVector) % 26
def decrypt(cipherMatrix):
    global messageVector
    det = int(np.linalg.det(keyMatrix))
    det_inv = pow(det, -1, 26)  # Calculating modular multiplicative inverse
    adjugateMatrix = np.round(det_inv * np.linalg.inv(keyMatrix) * det) % 26
    messageVector = np.dot(adjugateMatrix, cipherMatrix) % 26
def HillCipher(message, key):
    global messageVector, cipherMatrix, keyMatrix
    getKeyMatrix(key)
    messageVector = np.array([[ord(char) % 65] for char in message], dtype=int)
    encrypt(messageVector)
    CipherText = [chr(char + 65) for char in cipherMatrix.flatten()]
    print("Ciphertext:", "".join(CipherText))
    decrypt(cipherMatrix)
    DecryptedText = [chr(int(char) % 26 + 65) for char in messageVector.flatten()]
    print("Decrypted text:", "".join(DecryptedText))
def main():
    key = input("Enter Key: ")
    message = input("Enter Plain Text: ")
    HillCipher(message, key)

if __name__ == "__main__":
    main()


## OUTPUT:
Enter Key:  ATCHENNAI
Enter Plain Text: SMR
Ciphertext: CFG
Decrypted text: SMR


## RESULT:
The program is executed successfully

-------------------------------------------------

# Vigenere Cipher
Vigenere Cipher using with different key values

# AIM:
To implement a program for encryption and decryption using vigenere cipher substitution
technique.

# ALGORITHM:
The Vigenere cipher is a method of encrypting alphabetic text by using a series of different
Caesar ciphers based on the letters of a keyword. 
It is a simple form of polyalphabetic substitution.To encrypt, a table of alphabets can be used, termed a Vigenere square, or Vigenere table. 
It consists of the alphabet written out 26 times in different rows, each alphabet shifted
cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar
ciphers. At different points in the encryption process, the cipher uses a different alphabet from one of the rows used. The alphabet at each point depends on a repeating keyword.

## PROGRAM:
def generateKey(string, key):
    key = list(key)
    if len(string) == len(key):
        return(key)
    else:
        for i in range(len(string) -
                       len(key)):
            key.append(key[i % len(key)])
    return("" . join(key))
def cipherText(string, key):
    cipher_text = []
    for i in range(len(string)):
        x = (ord(string[i]) +
             ord(key[i])) % 26
        x += ord('A')
        cipher_text.append(chr(x))
    return("" . join(cipher_text))
def originalText(cipher_text, key):
    orig_text = []
    for i in range(len(cipher_text)):
        x = (ord(cipher_text[i]) -
             ord(key[i]) + 26) % 26
        x += ord('A')
        orig_text.append(chr(x))
    return("" . join(orig_text))
 
if __name__ == "__main__":
    string = input("Enter a plain text: ")
    keyword = input("Enter a key: ")
    key = generateKey(string, keyword)
    cipher_text = cipherText(string,key)
    print("Ciphertext :", cipher_text)
    print("Decrypted Text :", 
           originalText(cipher_text, key))


## OUTPUT:

Enter a plain text: SMRITI
Enter a key: HELLO
Ciphertext : ZQCTHP
Decrypted Text : SMRITI


## RESULT:
The program is executed successfully

-----------------------------------------------------------------------

# Rail Fence Cipher
Rail Fence Cipher using with different key values

# AIM:
To implement a program for encryption and decryption using rail fence transposition
technique.

# ALGORITHM DESCRIPTION:
In the rail fence cipher, the plaintext is written downwards and diagonally on successive
"rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach
the top rail, the message is written downwards again until the whole plaintext is written out.
The message is then read off in rows.


## PROGRAM:
def encrypt_rail_fence(plain_text, rails):
    len_str = len(plain_text)
    code = [[0] * len_str for _ in range(rails)]
    count = 0
    j = 0

    while j < len_str:
        if count % 2 == 0:
            for i in range(rails):
                if j < len_str:
                    code[i][j] = ord(plain_text[j])
                    j += 1
        else:
            for i in range(rails - 2, 0, -1):
                if j < len_str:
                    code[i][j] = ord(plain_text[j])
                    j += 1
        count += 1

    cipher_text = ""
    for i in range(rails):
        for j in range(len_str):
            if code[i][j] != 0:
                cipher_text += chr(code[i][j])

    return cipher_text

def decrypt_rail_fence(cipher_text, rails):
    len_str = len(cipher_text)
    code = [[0] * len_str for _ in range(rails)]
    count = 0
    j = 0

    while j < len_str:
        if count % 2 == 0:
            for i in range(rails):
                if j < len_str:
                    code[i][j] = ord(' ')
                    j += 1
        else:
            for i in range(rails - 2, 0, -1):
                if j < len_str:
                    code[i][j] = ord(' ')
                    j += 1
        count += 1

    index = 0
    for i in range(rails):
        for j in range(len_str):
            if code[i][j] != 0:
                code[i][j] = ord(cipher_text[index])
                index += 1

    plain_text = ""
    j = 0
    count = 0

    while j < len_str:
        if count % 2 == 0:
            for i in range(rails):
                if j < len_str:
                    plain_text += chr(code[i][j])
                    j += 1
        else:
            for i in range(rails - 2, 0, -1):
                if j < len_str:
                    plain_text += chr(code[i][j])
                    j += 1
        count += 1

    return plain_text

def main():
    str_input = input("Enter a plain text: ")
    rails = int(input("Enter number of rails (Key): "))
    
    # Encrypt
    cipher_text = encrypt_rail_fence(str_input, rails)
    print("Encrypted Cipher Text:", cipher_text)

    # Decrypt
    decrypted_text = decrypt_rail_fence(cipher_text, rails)
    print("Decrypted Plain Text:", decrypted_text)

if __name__ == "__main__":
    main()



## OUTPUT:
Enter a plain text: IAMSMRITI
Enter number of rails (Key): 3
Encrypted Cipher Text: IMIASRTMI
Decrypted Plain Text: IAMSMRITI


## RESULT:
The program is executed successfully
