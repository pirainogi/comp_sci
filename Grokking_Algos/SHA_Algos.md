# SHA
* Secure Hash Algorithm
  * generates a hash (short string)
  * string to string  
    * _hashing function goes from string to array index_
  * check large files if they're the same
  * check passwords
    * stores a hashed password, not a plaintext string
    * can't convert backwards
* locality insensitive
  * can't compare hashes to see if they're similar because each hash is generated independently
* SimHash
  * locality-sensitive hash function
  * detects dups when crawling the web
  * compares essays against IP to detect plagiarism 
