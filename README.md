# EX-NO-9-RSA-Algorithm

## AIM:
To Implement RSA Encryption Algorithm in Cryptography

## Algorithm:


Step 1: Design of RSA Algorithm  
The RSA algorithm is based on the mathematical difficulty of factoring the product of two large prime numbers. It involves generating a public and private key pair, where the public key is used for encryption, and the private key is used for decryption.

Step 2: Implementation in Python or C 
This algorithm can be implemented in languages like Python or C by performing large integer calculations for key generation, encryption, and decryption, utilizing libraries for modular arithmetic if necessary.

Step 3: Algorithm Description  
1. Key Generation:
   - Select two large prime numbers \( p \) and \( q \).
   - Calculate \( n = p \times q \), which will be used as the modulus.
   - Compute the totient \( \phi(n) = (p - 1)(q - 1) \).
   - Choose a public exponent \( e \) such that \( e \) is coprime with \( \phi(n) \).
   - Compute the private key \( d \), which is the modular inverse of \( e \) mod \( \phi(n) \).

2. Encryption:
   - Convert the plaintext message \( M \) into a numerical form \( m \) (such that \( 0 \le m < n \)).
   - Compute the ciphertext \( c \) using the formula: \( c = m^e \mod n \).

3. Decryption:
   - Use the private key \( d \) to recover \( m \) from \( c \) using: \( m = c^d \mod n \).
   - Convert \( m \) back into the original message \( M \).

Step 4: Mathematical Representation  
- Encryption: \( E(m) = m^e \mod n \)
- Decryption: \( D(c) = c^d \mod n \)

Step 5: Security Foundation  
The security of RSA relies on the difficulty of factoring large numbers; thus, choosing sufficiently large prime numbers for \( p \) and \( q \) is crucial for security.

## Program:
```
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
int gcd(int a, int b) {
 while (b != 0) {
 int temp = b;
 b = a % b;
 a = temp;
 }
 return a;
}
int modInverse(int e, int phi) {
 int t = 0, newt = 1;
 int r = phi, newr = e;
 while (newr != 0) {
 int quotient = r / newr;
 int temp = newt;
 newt = t - quotient * newt;
 t = temp;
 temp = newr;
 newr = r - quotient * newr;
 r = temp;
 }
 if (r > 1) return -1;
 if (t < 0) t = t + phi;
 return t;
}
long long modExp(long long base, long long exp, long long mod) {
 long long result = 1;
 while (exp > 0) {
 if (exp % 2 == 1) result = (result * base) % mod;
 base = (base * base) % mod;
 exp = exp / 2;
 }
 return result;
}
int main() {
 int p = 61, q = 53;
 int n = p * q;
 int phi = (p - 1) * (q - 1);
 int e = 17;
 while (gcd(e, phi) != 1) e++;
 int d = modInverse(e, phi);
 if (d == -1) {
 printf("Error finding modular inverse.\n");
 return 1;
 }
 printf("***** RSA *****\n");
 printf("Public key: (n = %d, e = %d)\n", n, e);
 printf("Private key: (n = %d, d = %d)\n", n, d);
 char name[] = "HEMANTH";
 int length = strlen(name);
 printf("Original Name: %s\n", name);
 long long encrypted[length];
 printf("Encrypted Name: ");
 for (int i = 0; i < length; i++) {
 encrypted[i] = modExp((int)name[i], e, n);
 printf("%lld ", encrypted[i]);
 }
 printf("\n");
 char decrypted[length + 1];
 decrypted[length] = '\0';
 printf("Decrypted Name: ");
 for (int i = 0; i < length; i++) {
 decrypted[i] = (char)modExp(encrypted[i], d, n);
 printf("%c", decrypted[i]);
 }
 printf("\n");
 return 0;
}
```



## Output:
![image](https://github.com/user-attachments/assets/2c0c9a7c-899f-41f0-bac5-acd5c464a745)



## Result:
 The program is executed successfully.
