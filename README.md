# EX-10-DIFFIE-HELLMAN KEY EXCHANGE ALGORITHM
## AIM:
To implement the Diffee Hellman Algoirthm using C or Python.
## DESIGN STEPS:
### Step 1:
Design the Diffie-Hellman key exchange algorithm.

### Step 2:
Implement the algorithm using C.

### Step 3:
The Diffie-Hellman algorithm uses a large prime number p and a primitive root g. Both Eve and David select private keys and exchange public keys computed using the formula:
```
Public Key = (g^Private Key) % p
```
After exchanging public keys, both compute a shared secret key using:
```
Shared Secret = (Other's Public Key^Private Key) % p
```
## PROGRAM:
```c
#include <stdio.h>
#include <math.h>

// Function to calculate (base^exp) % mod using modular exponentiation
int modExp(int base, int exp, int mod) {
    int result = 1;
    base = base % mod;
    while (exp > 0) {
        if (exp % 2 == 1) {
            result = (result * base) % mod;
        }
        exp = exp >> 1;
        base = (base * base) % mod;
    }
    return result;
}

int main() {
    // Publicly known values
    int p = 23;  // A large prime number
    int g = 5;   // A primitive root modulo p
    
    // Private keys (chosen secretly by Eve and David)
    int evePrivateKey, davidPrivateKey;
    printf("Enter Eve's private key: ");
    scanf("%d", &evePrivateKey);
    printf("Enter David's private key: ");
    scanf("%d", &davidPrivateKey);
    
    // Public keys (computed from private keys)
    int evePublicKey = modExp(g, evePrivateKey, p);  // Eve's public key
    int davidPublicKey = modExp(g, davidPrivateKey, p);  // David's public key
    
    printf("Eve's Public Key: %d\n", evePublicKey);
    printf("David's Public Key: %d\n", davidPublicKey);
    
    // Shared secret keys (computed from the other's public key and own private key)
    int sharedKeyEve = modExp(davidPublicKey, evePrivateKey, p);  // Eve computes the shared secret key
    int sharedKeyDavid = modExp(evePublicKey, davidPrivateKey, p);  // David computes the shared secret key
    
    printf("Shared Secret Key (Eve): %d\n", sharedKeyEve);
    printf("Shared Secret Key (David): %d\n", sharedKeyDavid);
    
    // The shared keys should be the same
    if (sharedKeyEve == sharedKeyDavid) {
        printf("Key Exchange Successful! Shared Secret Key: %d\n", sharedKeyEve);
    } else {
        printf("Key Exchange Failed!\n");
    }

    return 0;
}

```
## OUTPUT:
![Screenshot 2024-10-11 110156](https://github.com/user-attachments/assets/57ca616d-398e-4257-bfa2-ddf58d7a03b9)

## RESULT:
Thus the implementation of Diffe Hellman Algorithm executed successfully.
