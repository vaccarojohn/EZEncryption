# C-Sharp-EZEncryption
This package provides an easy way to encrypt strings into MD5, SHA1, SHA256, SHA384, and SHA512 formats. It also provides a way to create your own custom cipher and use it to encrypt strings.


Example 1 (Using The Default Encryption Methods):

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



Example 2 (Creating Your Own Custom Cipher Function):

```c#
using System;
using EZEncryption;

namespace test
{
    class Program
    {
        static void Main(string[] args)
        {
            Hash myHash = Hash.CreateCustomHash("yourInput", new MyCustomCipher());
            Console.WriteLine(myHash.OutputAsString);
        }
    }
    class MyCustomCipher : ICustomCipher
    {
        public char ConvertChar(char input)
        {
            // Only Works With Letters
            if (input == 'z')
            {
                return 'a';
            }
            else if (input == 'Z')
            {
                return 'A';
            }
            else
            {
                return (char)(((int)input) + 1);
            }
        }
    }
}
```
