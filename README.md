# Salt_and_Hash

other source- 
MSDN Link : https://docs.microsoft.com/en-us/aspnet/core/security/data-protection/consumer-apis/password-hashing?view=aspnetcore-2.2

Why we use salt 
-----

If you're a web developer, you've probably had to make a user account system. The most important aspect of a user account system is how user passwords are protected. User account databases are hacked frequently, so you absolutely must do something to protect your users' passwords if your website is ever breached. The best way to protect passwords is to employ salted password hashing. This page will explain why it's done the way it is.

How to use salt
-----

Salt should be generated using a Cryptographically Secure Pseudo-Random Number Generator (CSPRNG). CSPRNGs are very different than ordinary pseudo-random number generators, like the "C" language's rand() function. As the name suggests, CSPRNGs are designed to be cryptographically secure, meaning they provide a high level of randomness and are completely unpredictable. We don't want our salts to be predictable, so we must use a CSPRNG.


Important TWO to use salt
----

1. Do not reuse salt

2. Use the longer salt

The salt needs to be unique per-user per-password. 

Every time a user creates an account or changes their password, the password should be hashed using a new random salt. 

Never reuse a salt. 

The salt also needs to be long, so that there are many possible salts. 

As a rule of thumb, make your salt is at least as long as the hash function's output. 

The salt should be stored in the user account table alongside the hash.


To Store a Password
-----

1. Generate a long random salt using a CSPRNG.

2. Prepend the salt to the password and hash it with a standard password hashing function like Argon2, bcrypt, scrypt, or PBKDF2.

3. Save both the salt and the hash in the user's database record.


To Validate a Password
-----

1. Retrieve the user's salt and hash from the database.

2. Prepend the salt to the given password and hash it using the same hash function.

3. Compare the hash of the given password with the hash from the database. If they match, the password is correct. Otherwise, the password is incorrect.





