# playfairchiper


# prompt: Enkripsi Playfair Cihper pada plaintext:
# GOOD BROOM SWEEP CLEAN
# REDWOOD NATIONAL STATE PARK
# JUNK FOOD AND HEALTH PROBLEMS
# Dengan kunci “TEKNIK INFORMATIKA"

def prepare_key(key):
  key = key.upper().replace("J", "I")
  key_matrix = []
  for char in key:
    if char not in key_matrix and char.isalpha():
      key_matrix.append(char)
  for char in range(ord('A'), ord('Z') + 1):
    char = chr(char)
    if char not in key_matrix and char != 'J':
      key_matrix.append(char)
  matrix = [key_matrix[i:i+5] for i in range(0, 25, 5)]
  return matrix

def find_position(matrix, char):
  for i in range(5):
    for j in range(5):
      if matrix[i][j] == char:
        return (i, j)
  return None

def encrypt(plaintext, key):
  matrix = prepare_key(key)
  plaintext = plaintext.upper().replace("J", "I")
  plaintext = "".join(filter(str.isalpha, plaintext))

  if len(plaintext) % 2 != 0:
    plaintext += 'X'

  ciphertext = ""
  for i in range(0, len(plaintext), 2):
    char1 = plaintext[i]
    char2 = plaintext[i+1]

    row1, col1 = find_position(matrix, char1)
    row2, col2 = find_position(matrix, char2)

    if row1 == row2:
      ciphertext += matrix[row1][(col1 + 1) % 5]
      ciphertext += matrix[row2][(col2 + 1) % 5]
    elif col1 == col2:
      ciphertext += matrix[(row1 + 1) % 5][col1]
      ciphertext += matrix[(row2 + 1) % 5][col2]
    else:
      ciphertext += matrix[row1][col2]
      ciphertext += matrix[row2][col1]

  return ciphertext


def decrypt(ciphertext, key):
  matrix = prepare_key(key)
  plaintext = ""

  for i in range(0, len(ciphertext), 2):
    char1 = ciphertext[i]
    char2 = ciphertext[i+1]

    row1, col1 = find_position(matrix, char1)
    row2, col2 = find_position(matrix, char2)

    if row1 == row2:
      plaintext += matrix[row1][(col1 - 1) % 5]
      plaintext += matrix[row2][(col2 - 1) % 5]
    elif col1 == col2:
      plaintext += matrix[(row1 - 1) % 5][col1]
      plaintext += matrix[(row2 - 1) % 5][col2]
    else:
      plaintext += matrix[row1][col2]
      plaintext += matrix[row2][col1]

  return plaintext


key = "TEKNIKINFORMATIKA"
plaintext1 = "GOODBROOMSWEEPCLEAN"
plaintext2 = "REDWOODNATIONALSTATEPARK"
plaintext3 = "JUNKFOODANDHEALTHPROBLEMS"

ciphertext1 = encrypt(plaintext1, key)
ciphertext2 = encrypt(plaintext2, key)
ciphertext3 = encrypt(plaintext3, key)

decrypted_text1 = decrypt(ciphertext1, key)
decrypted_text2 = decrypt(ciphertext2, key)
decrypted_text3 = decrypt(ciphertext3, key)


print("Plaintext 1:", plaintext1)
print("Ciphertext 1:", ciphertext1)
print("Decrypted Text 1:", decrypted_text1)

print("\nPlaintext 2:", plaintext2)
print("Ciphertext 2:", ciphertext2)
print("Decrypted Text 2:", decrypted_text2)


print("\nPlaintext 3:", plaintext3)
print("Ciphertext 3:", ciphertext3)
print("Decrypted Text 3:", decrypted_text3)![Screenshot (433)](https://github.com/user-attachments/assets/3c4103ad-c447-49be-84b5-07d0afce0e2b)
