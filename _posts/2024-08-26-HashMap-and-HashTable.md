---
title: Hash Table and Hash Map
categories: [DSA concepts]
tags: [DSA concepts , Daily Dose of DSA, Hashing, Hash Map , Hash Table]
---

Hash Maps and Hash Tables are essential data structures designed to efficiently store and retrieve data. Both utilize key-value pairs but differ in implementation and usage. Let's delve into their workings with examples in C++.


𝐇𝐚𝐬𝐡 𝐓𝐚𝐛𝐥𝐞

A Hash Table is a structure that uses a hash function to map keys to indices in an array. The hash function generates an index based on the key, where the corresponding value is stored. This allows for average constant-time complexity for operations like insertion, deletion, and search.


𝐊𝐞𝐲 𝐂𝐨𝐧𝐜𝐞𝐩𝐭𝐬

☁︎ 𝗛𝗮𝘀𝗵 𝗙𝘂𝗻𝗰𝘁𝗶𝗼𝗻: Transforms a key into an index.

☁︎ 𝗖𝗼𝗹𝗹𝗶𝘀𝗶𝗼𝗻 𝗥𝗲𝘀𝗼𝗹𝘂𝘁𝗶𝗼𝗻: Strategies to handle cases where different keys hash to the same index, such as chaining or open addressing.


𝐄𝐱𝐚𝐦𝐩𝐥𝐞𝐬:
A basic hash table implementation in C++ using chaining (linked lists) to manage collisions:

```cpp
#include <iostream>
#include <list>
#include <utility>

class HashTable {
private:
    static const int tableSize = 10;
    std::list<std::pair<int, std::string>> table[tableSize];

    int hashFunction(int key) {
        return key % tableSize;
    }

public:
    void insert(int key, const std::string& value) {
        int index = hashFunction(key);
        table[index].emplace_back(key, value);
    }

    std::string search(int key) {
        int index = hashFunction(key);
        for (const auto& pair : table[index]) {
            if (pair.first == key) {
                return pair.second;
            }
        }
        return "Not found";
    }

    void remove(int key) {
        int index = hashFunction(key);
        table[index].remove_if([key](const std::pair<int, std::string>& pair) {
            return pair.first == key;
        });
    }
};

int main() {
    HashTable ht;
    ht.insert(1, "Value1");
    ht.insert(2, "Value2");
    std::cout << "Search for key 1: " << ht.search(1) << std::endl;
    std::cout << "Search for key 2: " << ht.search(2) << std::endl;
    ht.remove(1);
    std::cout << "Search for key 1 after deletion: " << ht.search(1) << std::endl;
    return 0;
}
```

Here is the explanation of what each function is doing - The **hashFunction(int key)** converts a key into an index by taking the modulus of tableSize. This index determines where the key-value pair will be stored in the table. The **insert(int key, const std::string& value)** calculates the index using hashFunction and adds the key-value pair to the list at that index. The **search(int key)** retrieves the value associated with the key. It looks through the list at the computed index. If the key is found, the corresponding value is returned - otherwise, "Not found" is returned. The **remove(int key)** removes the key-value pair from the list at the computed index. The **remove_if** function is used to remove elements that match the given key.

𝐇𝐚𝐬𝐡 𝐌𝐚𝐩

A Hash Map is a more abstract representation of a hash table, often provided by high-level languages with additional features like automatic resizing. In C++, the unordered_map from the Standard Template Library (STL) offers this functionality.

𝐄𝐱𝐚𝐦𝐩𝐥𝐞:

An example of using unordered_map in C++:

```cpp
#include <iostream>
#include <unordered_map>

int main() {
    std::unordered_map<int, std::string> hashmap;

    // Adding elements
    hashmap[1] = "Value1";
    hashmap[2] = "Value2";
    hashmap[3] = "Value3";

    // Accessing elements
    std::cout << "Value for key 1: " << hashmap[1] << std::endl;
    std::cout << "Value for key 2: " << hashmap[2] << std::endl;

    // Checking existence
    if (hashmap.find(3) != hashmap.end()) {
        std::cout << "Key 3 found with value: " << hashmap[3] << std::endl;
    }

    // Removing elements
    hashmap.erase(1);
    if (hashmap.find(1) == hashmap.end()) {
        std::cout << "Key 1 has been removed" << std::endl;
    }

    return 0;
}
```


𝐑𝐞𝐬𝐨𝐮𝐫𝐜𝐞𝐬: 

1) [Use a hashmap in CPP](https://www.delftstack.com/howto/cpp/use-a-hashmap-in-cpp/)

2) [How to use Hashmap in CPP](https://www.geeksforgeeks.org/how-to-use-hashmap-in-cpp/)

3) [How to implement a simple hash-table](https://www.digitalocean.com/community/tutorials/hash-table-in-c-plus-plus)

4) [Java HashTable](https://www.javatpoint.com/java-hashtable)  

𝐂𝐨𝐧𝐜𝐥𝐮𝐬𝐢𝐨𝐧:

Hash Tables and Hash Maps are essential for efficient data management. Hash Tables use a hash function to map keys to array indices and handle collisions with methods like chaining. Hash Maps, such as C++'s unordered_map, offer a higher-level abstraction with automatic resizing and better collision management. Understanding both helps in choosing the right data structure for quick data access and manipulation in various applications. Understanding these data structures and their implementations can greatly improve your efficiency in handling data operations.


• 𝐇𝐚𝐬𝐡 𝐓𝐚𝐛𝐥𝐞: A low-level structure requiring manual collision handling, demonstrated with chaining.

• 𝐇𝐚𝐬𝐡 𝐌𝐚𝐩: A higher-level abstraction like unordered_map in C++, which includes built-in collision management and resizing.

