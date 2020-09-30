# EZEncryption
This package provides an easy way to encrypt strings into MD5, SHA1, SHA256, SHA384, and SHA512 formats. It also provides a way to create your own custom cipher and use it to encrypt strings. This package is compiled for .NET 4.7, 4.6.1, 4.5.2, 4.5.1, 4.5, 4.4, and 3.5. The version for 3.5 works with Unity.

##### Note:
For security reasons, an open-source version of EZEncryption is not provided.

##### REMEMBER: 
The Default Setting For Hash.UseUpperCasing is true. Change that to false, and all MD5, SHA1, SHA256, SHA385, SHA512, and Custom Ciphers generated with EZEncryption will have no capital letters.

### Updates
- 8/7/2017 - <b>EZEncryption Now Supports Symmetric Hashes!</b> (Built In Support For AES, DES, TripleDES, and RC2 Symmetric Hashes) Scroll Down To [Example 4](https://github.com/gamergames123/EZEncryption#example-4-using-built-in-symmetric-hashes) To See How To Use Them! 


### Example 1 (Using The Default Encryption Methods):

```c#
using System;
using EZEncryption;

namespace test
{
    class Program
    {
        static void Main(string[] args)
        {
            Hash myHash = Hash.CreateHash("yourInput", EncryptionType.MD5);
            Console.WriteLine(myHash.OutputAsString);
            myHash = Hash.CreateHash("yourInput", EncryptionType.SHA1);
            Console.WriteLine(myHash.OutputAsString);
            myHash = Hash.CreateHash("yourInput", EncryptionType.SHA256);
            Console.WriteLine(myHash.OutputAsString);
            myHash = Hash.CreateHash("yourInput", EncryptionType.SHA384);
            Console.WriteLine(myHash.OutputAsString);
            myHash = Hash.CreateHash("yourInput", EncryptionType.SHA512);
            Console.WriteLine(myHash.OutputAsString);
        }
    }
}
```

### Example 2 (Another Way To Use The Default Encryption Methods):
```c#
using System;
using EZEncryption;

namespace test
{
    class Program
    {
        static void Main(string[] args)
        {
            Hash myHash = new MD5Hash("yourInput");
            Console.WriteLine(myHash.OutputAsString);
            myHash = new SHA1Hash("yourInput");
            Console.WriteLine(myHash.OutputAsString);
            myHash = new SHA256Hash("yourInput");
            Console.WriteLine(myHash.OutputAsString);
            myHash = new SHA384Hash("yourInput");
            Console.WriteLine(myHash.OutputAsString);
            myHash = new SHA512Hash("yourInput");
            Console.WriteLine(myHash.OutputAsString);
        }
    }
}
```


### Example 3 (Creating Your Own Custom Cipher Function):

```c#
using System;
using EZEncryption;

namespace test
{
    class Program
    {
        static void Main(string[] args)
        {
            while(true)
            {
                Console.WriteLine("Enter A String To Be Encoded To My Custom Cipher: ");
                Hash myHash = Hash.CreateCustomHash(Console.ReadLine(), new MyCustomCipher());
                Console.WriteLine(myHash.OutputAsString);
            }
        }
    }
    class MyCustomCipher : ICustomCipher
    {
        public char ConvertChar(char input)
        {
            int result;
            if (input == 'z')
            {
                return '0';
            } else if (input == '9')
            {
                return 'a';
            } else if (int.TryParse(input.ToString(), out result))
            {
                result += 1;
                return char.Parse(result.ToString());
            }
            else
            {
                return (char)(((int)input) + 1);
            }
        }
    }
}
```

### Example 4 (Using Built In Symmetric Hashes):
```c#
using System;
using EZEncryption;

namespace test
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine("Enter A Password For This Encryption: ");
            string password = Console.ReadLine();
            Console.WriteLine("Enter Some Text To Encrypt: ");
            string text = Console.ReadLine();
            Console.WriteLine("Encrypting...\n");
            AESHash aes = new AESHash(text, password);
            Console.WriteLine("Encrypted Data: " + aes.OutputAsString);
            Console.WriteLine("Decrypting...\n");
            Console.WriteLine("Decrypted Data: " + AESHash.Decrypt(aes.OutputAsByteArray, password));
        }
    }
}
```

<b>Note: You May Also Use The SymmetricHash.CreateSymmetricHash() Method To Create Symmetric Hashes.</b>


Before using 3TDES, user first generate and distribute a 3TDES key K, which consists of three different DES keys K1, K2 and K3. This means that the actual 3TDES key has length 3×56 = 168 bits. The encryption scheme is illustrated as follows −

############       Triple DES Algorithm

Encryption Scheme
The encryption-decryption process is as follows −

Encrypt the plaintext blocks using single DES with key K1.

Now decrypt the output of step 1 using single DES with key K2.

Finally, encrypt the output of step 2 using single DES with key K3.

The output of step 3 is the ciphertext.

Decryption of a ciphertext is a reverse process. User first decrypt using K3, then encrypt with K2, and finally decrypt with K1.

Due to this design of Triple DES as an encrypt–decrypt–encrypt process, it is possible to use a 3TDES (hardware) implementation for single DES by setting K1, K2, and K3 to be the same value. This provides backwards compatibility with DES.

Second variant of Triple DES (2TDES) is identical to 3TDES except that K3is replaced by K1. In other words, user encrypt plaintext blocks with key K1, then decrypt with key K2, and finally encrypt with K1 again. Therefore, 2TDES has a key length of 112 bits.

Triple DES systems are significantly more secure than single DES, but these are clearly a much slower process than encryption using single DES.

