# EX-NO-12-ELGAMAL-ALGORITHM

## AIM:
To Implement ELGAMAL ALGORITHM

## ALGORITHM:

1. ElGamal Algorithm is a public-key cryptosystem based on the Diffie-Hellman key exchange and relies on the difficulty of solving the discrete logarithm problem.

2. Initialization:
   - Select a large prime \( p \) and a primitive root \( g \) modulo \( p \) (these are public values).
   - The receiver chooses a private key \( x \) (a random integer), and computes the corresponding public key \( y = g^x \mod p \).

3. Key Generation:
   - The public key is \( (p, g, y) \), and the private key is \( x \).

4. Encryption:
   - The sender picks a random integer \( k \), computes \( c_1 = g^k \mod p \), and \( c_2 = m \times y^k \mod p \), where \( m \) is the message.
   - The ciphertext is the pair \( (c_1, c_2) \).

5. Decryption:
   - The receiver computes \( s = c_1^x \mod p \), and then calculates the plaintext message \( m = c_2 \times s^{-1} \mod p \), where \( s^{-1} \) is the modular inverse of \( s \).

6. Security: The security of the ElGamal algorithm relies on the difficulty of solving the discrete logarithm problem in a large prime field, making it secure for encryption.

## Program:
```c
#include <stdio.h>
#include <math.h>

long long mod_exp(long long base, long long exp, long long mod) {
    long long result = 1;
    base %= mod;
    while (exp > 0) {
        if (exp % 2 == 1)
            result = (result * base) % mod;
        exp /= 2;
        base = (base * base) % mod;
    }
    return result;
}

int main() {
    long long p , g, x, k , m;
    scanf("%lld %lld %lld %lld %lld",&p,&g,&x,&k,&m);
    long long y, c1, c2, temp, inv, m_dec;

    y = mod_exp(g, x, p);
    c1 = mod_exp(g, k, p);
    c2 = (m * mod_exp(y, k, p)) % p;

    temp = mod_exp(c1, x, p);
    inv = mod_exp(temp, p - 2, p);
    m_dec = (c2 * inv) % p;

    printf("Public key (p, g, y) = (%lld, %lld, %lld)\n", p, g, y);
    printf("Private key (x) = %lld\n", x);
    printf("Message (m) = %lld\n", m);
    printf("Encrypted (c1, c2) = (%lld, %lld)\n", c1, c2);
    printf("Decrypted message = %lld\n", m_dec);

    return 0;
}
```
## Output:

<img width="891" height="548" alt="509909912-270aed14-f985-4fbf-848d-822b86992204" src="https://github.com/user-attachments/assets/f921d870-478a-40f6-bb1d-973d655c6d3d" />


## Result:
The program is executed successfully.
