# Ex-4 Rail-Fence-Program

# IMPLEMENTATION OF RAIL FENCE – ROW & COLUMN TRANSFORMATION TECHNIQUE

# AIM:

# To write a C program to implement the rail fence transposition technique.

# DESCRIPTION:

In the rail fence cipher, the plain text is written downwards and diagonally on successive "rails" of an imaginary fence, then moving up when we reach the bottom rail. When we reach the top rail, the message is written downwards again until the whole plaintext is written out. The message is then read off in rows.

# ALGORITHM:

STEP-1: Read the Plain text.
STEP-2: Arrange the plain text in row columnar matrix format.
STEP-3: Now read the keyword depending on the number of columns of the plain text.
STEP-4: Arrange the characters of the keyword in sorted order and the corresponding columns of the plain text.
STEP-5: Read the characters row wise or column wise in the former order to get the cipher text.

# PROGRAM
```
#include <stdio.h> 
#include <string.h> 
#include <stdlib.h> 
// Function to encrypt the plaintext using Rail Fence Cipher 
void encryptRailFence(char* text, int key, char* result) { 
int len = strlen(text); 
char rail[key][len]; 
// Fill with '\n' 
for (int i = 0; i < key; i++) 
for (int j = 0; j < len; j++) 
rail[i][j] = '\n'; 
// Zigzag filling 
int row = 0; 
int dir_down = 0; 
for (int i = 0; i < len; i++) { 
rail[row][i] = text[i]; 
if (row == 0 || row == key - 1) 
dir_down = !dir_down; 
        row += dir_down ? 1 : -1; 
    } 
 
    // Collect encrypted text 
    int idx = 0; 
    for (int i = 0; i < key; i++) 
        for (int j = 0; j < len; j++) 
            if (rail[i][j] != '\n') 
                result[idx++] = rail[i][j]; 
    result[idx] = '\0'; 
} 
 
// Function to decrypt the cipher using Rail Fence Cipher 
void decryptRailFence(char* cipher, int key, char* result) { 
    int len = strlen(cipher); 
    char rail[key][len]; 
 
    // Fill with '\n' 
    for (int i = 0; i < key; i++) 
        for (int j = 0; j < len; j++) 
            rail[i][j] = '\n'; 
 
    // Mark zigzag pattern 
    int row = 0; 
    int dir_down = 0; 
    for (int i = 0; i < len; i++) { 
        rail[row][i] = '*'; 
 
        if (row == 0 || row == key - 1) 
            dir_down = !dir_down; 
 
        row += dir_down ? 1 : -1; 
    } 
 
    // Fill the marked spots 
    int index = 0; 
    for (int i = 0; i < key; i++) 
        for (int j = 0; j < len; j++) 
            if (rail[i][j] == '*' && index < len) 
                rail[i][j] = cipher[index++]; 
 
    // Read in zigzag 
    row = 0; 
    dir_down = 0; 
    int idx = 0; 
    for (int i = 0; i < len; i++) { 
        result[idx++] = rail[row][i]; 
 
        if (row == 0 || row == key - 1) 
            dir_down = !dir_down; 
row += dir_down ? 1 : -1; 
} 
result[idx] = '\0'; 
} 
int main() { 
char text[100], cipher[100], decrypted[100]; 
int key; 
printf("Enter Plain Text: "); 
fgets(text, sizeof(text), stdin); 
text[strcspn(text, "\n")] = '\0'; // remove newline 
printf("Enter Key (number of rails): "); 
scanf("%d", &key); 
encryptRailFence(text, key, cipher); 
decryptRailFence(cipher, key, decrypted); 
printf("\nPlain Text: %s\n", text); 
printf("Key: %d\n", key); 
printf("Encrypted Text: %s\n", cipher); 
printf("Decrypted Text: %s\n", decrypted); 
return 0; 
}
```

# OUTPUT
<img width="548" height="327" alt="image" src="https://github.com/user-attachments/assets/470027b3-3ce4-4699-af23-aa732511c933" />


# RESULT
Thus the implementation of Rail Fence cipher had been executed successfully.
