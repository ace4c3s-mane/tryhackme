
A Rainbow Table is a lookup table of hashes to plaintexts, so you can quickly find out what password a user had just from the hash.

To protect them, we add a salt to the passwords. The salt is a randomly generated value stored in the database and should be unique to each user.

In theory, you could use the same salt for all users, but duplicate passwords would still have the same hash and a rainbow table could still be created for passwords with that salt.

It's added to either the start or the end of the password before it's hashed and this means every user will have a different password hash even if they have the same password. Has functionsn like Bcrypt and Scrypt handle this automatically. 

