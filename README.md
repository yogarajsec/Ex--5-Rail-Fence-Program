# Ex--5-Rail-Fence-Program

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
void encryptRailFence(char *text, int key, char *cipherText);
void decryptRailFence(char *cipherText, int key, char *plainText);
int main() {
    char text[100], cipherText[100], decryptedText[100];
    int key;
    printf("Enter the plaintext: ");
    scanf("%s", text);
    printf("Enter the key (number of rails): ");
    scanf("%d", &key);
    encryptRailFence(text, key, cipherText);
    printf("Encrypted text: %s\n", cipherText);
    decryptRailFence(cipherText, key, decryptedText);
    printf("Decrypted text: %s\n", decryptedText);

    return 0;
}
void encryptRailFence(char *text, int key, char *cipherText) {
    int len = strlen(text);
    char rail[key][len];
    int i, j;
    for (i = 0; i < key; i++)
        for (j = 0; j < len; j++)
            rail[i][j] = '\n';
    int dir_down = 0; // Direction flag
    int row = 0, col = 0;
    for (i = 0; i < len; i++) {
        if (row == 0 || row == key - 1)
            dir_down = !dir_down; 
        rail[row][col++] = text[i];
        dir_down ? row++ : row--;
    }
    int k = 0;
    for (i = 0; i < key; i++)
        for (j = 0; j < len; j++)
            if (rail[i][j] != '\n')
                cipherText[k++] = rail[i][j];
    cipherText[k] = '\0';
}
void decryptRailFence(char *cipherText, int key, char *plainText) {
    int len = strlen(cipherText);
    char rail[key][len];
    int i, j;
    for (i = 0; i < key; i++)
        for (j = 0; j < len; j++)
            rail[i][j] = '\n';
    int dir_down = 0;
    int row = 0, col = 0;
    for (i = 0; i < len; i++) {
        if (row == 0)
            dir_down = 1;
        if (row == key - 1)
            dir_down = 0;

        rail[row][col++] = '*';
        dir_down ? row++ : row--;
    }
    int index = 0;
    for (i = 0; i < key; i++)
        for (j = 0; j < len; j++)
            if (rail[i][j] == '*' && index < len)
                rail[i][j] = cipherText[index++];
    dir_down = 0;
    row = 0, col = 0;
    for (i = 0; i < len; i++) {
        if (row == 0)
            dir_down = 1;
        if (row == key - 1)
            dir_down = 0;
        if (rail[row][col] != '*')
            plainText[i] = rail[row][col++];
        dir_down ? row++ : row--;
    }
    plainText[i] = '\0';
}
```
# OUTPUT
![Screenshot 2025-03-28 160856](https://github.com/user-attachments/assets/ecde750f-120d-4ef9-af6f-19c08bbe1a96)

# RESULT
The program is executed successfully
