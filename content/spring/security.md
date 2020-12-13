# Security

- [JWT](#jwt)



#### JWT

JSON Web Token (JWT) is an open standard ([RFC 7519](https://tools.ietf.org/html/rfc7519)) that defines a compact and self-contained way for securely transmitting information between parties as a JSON object. This information can be verified and trusted because it is digitally signed. JWTs can be signed using a secret (with the **HMAC** algorithm) or a public/private key pair using **RSA** or **ECDSA**.

**When should you use JSON Web Tokens**

- **Authorization**

  This is the most common scenario for using JWT. Once the user is logged in, each subsequent request will include the JWT, allowing the user to access routes, services, and resources that are permitted with that token.

- **Information Exchange**

  JSON Web Tokens are a good way of securely transmitting information between parties. Because JWTs can be signed—for example, using public/private key pairs—you can be sure the senders are who they say they are.



##### Structure of JSON Web Token

- **Header**

  The header *typically* consists of two parts: the type of the token, which is JWT, and the signing algorithm being used, such as HMAC SHA256 or RSA.

- **Payload**

  The second part of the token is the payload, which contains the claims. Claims are statements about an entity (typically, the user) and additional data. There are three types of claims: *registered*, *public*, and *private* claims.

  - **Registered claims**

    These are a set of predefined claims which are not mandatory but recommended, to provide a set of useful, interoperable claims. Some of them are: **iss** (issuer), **exp** (expiration time), **sub** (subject), **aud** (audience), and [others](https://tools.ietf.org/html/rfc7519#section-4.1).

  - **Public claims**

    These can be defined at will by those using JWTs. But to avoid collisions they should be defined

  - **Private claims**

    These are the custom claims created to share information between parties that agree on using them and are neither *registered* or *public* claims.

- **Signature**

  The last part is the signature which is the sum of the encoded header, the encoded payload, a secret, and lastly the algorithm which is specified in the header.

  The signature is the most important part of the JWT structure. The header and payload can easily be decoded, but not the signature. The reason why is because it checks two things; first verify the header and payload has not been altered, and secondly check the private key is valid to make sure the sender is who it is.