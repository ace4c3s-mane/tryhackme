
Rainbow tables crack hashes that don't use a salt.

You can't "decrypt " password hashes. They're not encrypted. You have to crack the hashes by hashing many different inputs potentially adding the salt if there is one and comparing it to the target hash.

Once it matches, you know what the password was.

Modern GPU's have thousand of cores and are specialised in digital image processing and accelerating computer graphics.

Although they can't do the same sort of work that a CPU can, they are very good at some mathematical calculations involved in hash functions.

Some hashing algorithms, such as Bcrypt are designed so that  hashing on a GPU does not provide any speed improvement over using a CPU; this helps them resist cracking.

