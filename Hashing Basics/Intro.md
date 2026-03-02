
Consider a scenario where you just downloaded a 6GB file and want to know whether the copy you downloaded is identical to the original file bit for bit.

You can do this by comparing the hash values: A hash value is a fixed size string or characters that is computed by a hash function.  

A hash function takes takes an input of an arbitrary size and returns an output of fixed length. If the two hash values are equal, then the files are equal.

It's hard to predict the output for any input and vice versa. Good hashing algorithms will be relatively fast to compute and slow to reverse.


The output of a hash function is typically raw bytes, which are then encoded. Common encodings are base64 or hexadecimal. md5sum, sha254sum, sha1sum and sha512sum produce their output in hexadecimal format.

### Hash Collision

A hash collision is when two different inputs give the same output. Because the number of inputs is practically unlimited and the number of possible outputs is limited, this leads to a pigeonhole effect.

The pigeonhole effect states that the number of items (pigeons) is more than the number of containers (pigeonholes); some containers must hold more than one item.

MD5 and SHA1 have been attacked and are now considered insecure due to the ability to engineer hash collisions.

The output size in bytes of the MD5 hash function is 16.
