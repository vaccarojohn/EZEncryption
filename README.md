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

Example 2 (Another Way To Use The Default Encryption Methods):
```c#
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
            Hash.UseUpperCasing = false;
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

Update:
- Code More Efficient
