# Decomp
A decompression and compression library.

The interface:

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
but this is not advised and a smart pointer like a std::unique pointer should be prefered instead of handling raw pointers.
