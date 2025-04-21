# 🔑 Public Key Login (PKL)

The Public Key Login protocol is a key exchange similar to SSH key-based authentication. In this model, the site (or service) stores the user’s public key, while the user proves the ownership of the corresponding private key to authenticate.

## Advantages of PKL

- **Stronger Security:** Since the user never transmits their private key and only stores it locally, the authentication process is more secure than traditional password methods. Even if the public key is intercepted, it cannot be used to impersonate the user.
- **Resistance to Brute Force:** The private key itself is not practically vulnerable to brute-force attacks. The only way to gain access to the user’s account is by having access to the private key.
- **Privacy-preserving:** The user’s private key never leaves their device, ensuring that no sensitive information is transmitted during the login process. This prevents interception and ensures that the login process is fully private.

---
The documentation is a work in progress. For active deployment details, refer to the [PrivacySafe](https://github.com/PrivacySafe) implementation.
