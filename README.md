# APISecurity-BestPractices
Detailed list of best practices to make your APIs secure

Source : [roadmap.sh](https://roadmap.sh/best-practices/api-security)

## Authentification
### Avoid Basic Authentication
- You should avoid using basic authentication and use any other standard authentication methodologies i.e. OAuth, JWT, etc.

Basic authentication is a simple method for authenticating a user by transmitting the user’s credentials in plain text over the network. This method is inherently insecure and should be avoided whenever possible.

There are several reasons why basic authentication should be avoided and replaced with more secure authentication techniques:

- Lack of confidentiality: Basic authentication transmits the user’s credentials (username and password) in plain text over the network. This means that anyone who intercepts the traffic can easily read the credentials and gain access to the user’s account.

- Lack of integrity: Basic authentication does not provide any mechanism to ensure that the data being transmitted has not been tampered with or modified in transit. This means that an attacker can modify the traffic to gain access to the user’s account or perform other malicious activities.

- Lack of authentication strength: Basic authentication relies solely on the user’s credentials to authenticate them. This means that if an attacker is able to obtain the user’s credentials (for example, through phishing or social engineering), they can easily gain access to the user’s account.

- No support for multi-factor authentication: Basic authentication does not support multi-factor authentication (MFA), which is a critical security feature that provides an additional layer of protection against unauthorized access.

In contrast, other authentication techniques such as OAuth, OpenID Connect, and SAML provide more secure and robust methods for authentication. These methods typically use encrypted protocols to protect the user’s credentials, provide mechanisms for verifying the integrity of the data, and support MFA. As a result, they are much more secure and reliable than basic authentication and should be used whenever possible.

### Authentication Mechanisms
- Use standard authentication mechanisms for generating tokens, storing credentials, and authenticating users.

Here are some examples of established authentication mechanisms that you can use instead of reinventing the wheel:

- OAuth: OAuth is a widely used open standard for authorization that enables users to grant third-party applications access to their resources without sharing their credentials. It is commonly used by web services and APIs to enable users to sign in with their social media accounts or other third-party accounts.

- OpenID Connect: OpenID Connect is an authentication protocol built on top of OAuth 2.0 that enables users to authenticate with multiple websites and applications using a single set of credentials. It is commonly used for single sign-on (SSO) across multiple websites and applications.

- SAML: Security Assertion Markup Language (SAML) is an XML-based standard for exchanging authentication and authorization data between parties. It is commonly used for SSO across multiple domains or organizations.

- Password hashing algorithms: Password hashing algorithms like bcrypt and scrypt are widely used to securely store and protect user passwords. These algorithms ensure that even if an attacker gains access to the password database, they will not be able to easily recover the passwords.

- Two-factor authentication (2FA): 2FA is an authentication mechanism that requires users to provide two forms of identification to access their accounts. This typically involves something the user knows (like a password) and something the user has (like a mobile device or security key). Many services and applications now offer 2FA as an additional security measure.

### Max Retry/Jail in Login
- “Max Retry” and “jail” features are commonly used in login mechanisms to enhance security and prevent brute-force attacks.

- Max Retry: The “Max Retry” feature limits the number of login attempts that a user can make within a specified time period. After a certain number of failed login attempts, the user is locked out of their account for a specified period of time, typically several minutes or hours. This helps to prevent brute-force attacks, where an attacker attempts to guess a user’s password by making repeated login attempts. By limiting the number of attempts, the system can slow down or prevent such attacks.

- Jail: The “jail” feature involves blocking IP addresses or user accounts that have exceeded the maximum number of failed login attempts within a certain time period. The blocked IP addresses or user accounts are prevented from attempting further logins for a specified period of time, typically several minutes or hours. This helps to prevent brute-force attacks, and also provides a mechanism to prevent malicious users from repeatedly attempting to access an account or system.

### Sensitive Data Encryption
- Encrypting sensitive data is important for protecting it from unauthorized access, theft, and exploitation.

Encryption is a process of converting plain text data into a cipher text that can only be deciphered by someone who has the decryption key. This makes it difficult for attackers to access sensitive data, even if they are able to intercept it or gain unauthorized access to it.

To encrypt sensitive data, you can use encryption algorithms such as AES or RSA, along with a strong key management system to ensure that keys are securely stored and managed. Additionally, you can implement other security measures such as access controls, firewalls, and intrusion detection systems to further protect sensitive data.

## Acces Control
### Throttle Requests
- Limit requests (throttling) to avoid DDoS / Brute Force attacks.

Limiting requests through throttling is important to prevent DDoS attacks and brute force attacks. DDoS attacks overwhelm the server with too many requests, while brute force attacks try to guess user credentials through multiple login attempts.

Throttling limits the number of requests that can be sent within a certain time period, making it harder for attackers to carry out these types of attacks. This can protect the system from being overwhelmed and can prevent attackers from gaining unauthorized access.

### Use HTTPs
- Use HTTPS on server side and secure ciphers

Ensure that your API server uses HTTPS instead of HTTP. HTTPS is a secure protocol that encrypts data in transit, making it difficult for attackers to intercept and read sensitive information. To implement HTTPS, you need to obtain an SSL/TLS certificate and configure your server to use HTTPS.

HTTPS uses ciphers to encrypt data in transit. It is important to choose secure ciphers that are resistant to attacks and offer strong encryption. Some common secure ciphers include AES, ChaCha20, and ECDHE for key exchange. Make sure to disable weak and outdated ciphers, such as RC4 and TLS 1.0/1.1, which are vulnerable to attacks.

### HSTS Header
- Use HSTS header with SSL to avoid SSL Strip attacks.

SSL strip is a type of attack where an attacker intercepts traffic between a client and a server that is meant to be secured by SSL/TLS encryption, and downgrades the connection to a plain text (non-encrypted) HTTP connection. This type of attack can go unnoticed by the user because the attacker is able to redirect the user to a look-alike website that also uses HTTP instead of HTTPS.

In an SSL strip attack, the attacker sets up a man-in-the-middle (MITM) position between the client and the server. When the client initiates a connection with the server, the attacker intercepts the SSL/TLS traffic and removes or replaces the HTTPS links with HTTP links. This can trick the user into thinking they are using a secure connection when in fact, they are not. The attacker can then monitor and manipulate the data transmitted between the client and server.

HSTS header is a security header that instructs browsers to only access the site over HTTPS. This header is used to prevent SSL Strip attacks. It is a good practice to use HSTS header with SSL.

### Directory Listings
- Turn off directory listings

Directory listings are a feature of web servers that allow users to view the contents of a directory on a server. By default, web servers often have directory listings enabled, which means that anyone who has access to the server can see all the files and directories in a given folder.

Turning off directory listings is important for API security because it prevents attackers from gaining access to sensitive files and directories on the server. If directory listings are enabled and an attacker gains access to the server, they can easily view and download any files that are not properly protected. By disabling directory listings, you can ensure that only authorized users can access the files and directories on the server.

### Restrict Private APIs
- Private APIs should only be accessible from safe listed IPs

Private APIs should only be accessible from safe-listed IPs to ensure that only authorized users or systems can access the API. By restricting access to specific IP addresses, you can prevent unauthorized access from external networks or malicious actors. This can help to protect sensitive data and prevent attacks such as DDoS or brute-force attacks. Additionally, restricting access to safe-listed IPs can help to ensure the reliability and performance of the API by preventing excessive traffic from unauthorized sources.
