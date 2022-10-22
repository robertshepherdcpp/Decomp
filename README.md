# Decomp
A decompression and compression library.

Bear in mind that all code samples and the Decomd Library itself are all compiled using

    -std=c++20
 
 The incryption and decryption are in the stack manipulation namespace:
 
     namespace stack_manipulatioin
     {
     [[nodiscard]] auto decryption();
     [[nodiscard]] auto encryption();
     }
     
The interface:

The decryption and encryption functions(the main part of this library) accept a node to decrypt. for instance:
    
    namespace
    {
    // returns an decrypted node.
    node<T> decrypt(node<T>& node_); // decrypt the node.
    
    returns and encrypted node.
    node<T> incrypt(node<T>& node_) // encrypt the node.
    }

there is a function decompression that looks like this:

    template<typename T>
    [[nodiscard]] auto incryption(node<T>& v_t) -> node<T>
    {
            auto x = v_t.data_associated_with_node;
            v_t.data_associated_with_node = static_cast<int>(x);
            //v_t = v_t.next;
        
        // v_t.current_node = start_node;
    }

and a compression function that looks like this:

    template<typename T>
    [[nodiscard]] auto decryption(node<T>& v_t) -> node<T>
    {
            auto x = static_cast<T>(v_t.data_associated_with_node);
            v_t.data_associated_with_node = x;
            // v_t = v_t.current_node.next;
    }
There is also a container namespace for all the containers:
namespace containers
{
    template<int T, int... Ts>
    struct binary
    {
        int bit;
        binary<Ts...> bits; 

        auto output_bits() // just ouputs binary
        {
            std::cout << bit;
            std::cout << "\nOutputed bit: " << bit;
            bits.output_bits();
        }
    };

    template<int T>
    struct binary<T>
    {
        int bit;

        auto output_bits()
        {
            std::cout << bit;
            std::cout << "\nOutputed bit: " << bit;
        }
    };

    auto make_binary(auto x) -> int
    {
        return static_cast<int>(x);
    }

    struct Hash
    {
        Hash(auto i)
        {
            auto x = make_binary(i);
        }
    };
} // end of namespace containers.

There is also a formatting element to the Decomp library that looks like this:

    formt::format f("Hello my name is {}", 'R');
    onl();
    formt::format xyz("Good Afternoon {}", "C++");
    onl();
    formt::format abc("Good Afternoon {}", 42);
    
or you can just use:

    formt::func(/*pass in parameters like would do for object coration*/);
    
both work the same but just one creates an object and the other one doesnt. But in the objects creation it actually defers the variadic template parameters to the formt::func function. So it doesnt matter what you do. You could allocate it like this:

    formt::format* xyz("std::cout << {} << std::endl;", "Hello C++");
    
and then deallocate the object:

    delete xyz;
    
but this is not advised and a smart pointer like a std::unique pointer should be prefered instead of handling raw pointers. for example:

    std::unique_ptr<formt::format>(/*Normal Parameters or constructor aguements*/);
    
There is also a binary and bits namespace called:

    namespace binary_and_bits {/*Implementation...*/}

and it has several containers like:

    template<typename T>
    struct binary{auto Print();}
    
    // specialisations of binary, e.g., for one and two.
    
    auto make_binary(auto T);
    
    struct one{};
    struct two{};
