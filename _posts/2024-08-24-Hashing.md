---
title: Hashing
categories: [DSA concepts]
tags: [DSA concepts , Daily Dose of DSA, Hashing]
---

Hashing is the process of converting input data of any size into a fixed-size string of characters, which is typically a sequence of numbers and letters.
This fixed-size string is known as a hash value or simply a hash.The function that performs this transformation is called a hash function.

𝐖𝐡𝐲 𝐢𝐬 𝐇𝐚𝐬𝐡𝐢𝐧𝐠 𝐈𝐦𝐩𝐨𝐫𝐭𝐚𝐧𝐭?

Hashing is used for various purposes, including:

•	**Data Retrieval**: Quickly finding data in large datasets.

•	**Data Integrity**: Ensuring that data has not been altered.

•	**Security**: Storing passwords securely and verifying data integrity.


𝐇𝐨𝐰 𝐃𝐨𝐞𝐬 𝐇𝐚𝐬𝐡𝐢𝐧𝐠 𝐖𝐨𝐫𝐤?

1.	**Input Data** (Key): This is the data you want to hash. It can be anything like a string, number, or even a file.

2.	**Hash Function**: A mathematical function that takes the input data and converts it into a fixed-size hash value.

3.	**Hash Value**: The output of the hash function, which is a unique representation of the input data.

𝐄𝐱𝐚𝐦𝐩𝐥𝐞 𝐨𝐟 𝐚 𝐒𝐢𝐦𝐩𝐥𝐞 𝐇𝐚𝐬𝐡 𝐅𝐮𝐧𝐜𝐭𝐢𝐨𝐧

Let’s consider a simple hash function that converts a string into a hash value by summing the ASCII values of its characters and then taking the remainder when divided by a fixed number (e.g., 10).

For example, the string “abc”:

•	ASCII values: ‘a’ = 97, ‘b’ = 98, ‘c’ = 99

•	Sum: 97 + 98 + 99 = 294

•	Hash value: 294 % 10 = 4

So, the hash value for “abc” is 4.

𝐏𝐫𝐨𝐩𝐞𝐫𝐭𝐢𝐞𝐬 𝐨𝐟 𝐚 𝐆𝐨𝐨𝐝 𝐇𝐚𝐬𝐡 𝐅𝐮𝐧𝐜𝐭𝐢𝐨𝐧:

A good hash function should have the following properties:

1.	Deterministic: The same input should always produce the same hash value.

2.	Fast Computation: The hash function should be able to process data quickly.

3.	Uniform Distribution: Hash values should be evenly distributed to minimize collisions.

4.	Pre-image Resistance: It should be difficult to reverse the hash value to get the original input.

Now what if two different inputs end up having same hash value? This case is called 𝒄𝒐𝒍𝒍𝒊𝒔𝒊𝒐𝒏.

"𝑨 𝒄𝒐𝒍𝒍𝒊𝒔𝒊𝒐𝒏 𝒐𝒄𝒄𝒖𝒓𝒔 𝒘𝒉𝒆𝒏 𝒕𝒘𝒐 𝒅𝒊𝒇𝒇𝒆𝒓𝒆𝒏𝒕 𝒊𝒏𝒑𝒖𝒕𝒔 𝒑𝒓𝒐𝒅𝒖𝒄𝒆 𝒕𝒉𝒆 𝒔𝒂𝒎𝒆 𝒉𝒂𝒔𝒉 𝒗𝒂𝒍𝒖𝒆"

There are several methods to handle collisions.

1.	Separate Chaining: Store multiple elements in the same index using a linked list.

2.	Open Addressing: Find another open slot within the hash table using techniques like linear probing, quadratic probing, or double hashing.

𝐀𝐩𝐩𝐥𝐢𝐜𝐚𝐭𝐢𝐨𝐧𝐬 𝐨𝐟 𝐇𝐚𝐬𝐡𝐢𝐧𝐠:

Hashing is used in various applications, including:

•	Hash Tables: Data structures that use hash functions to map keys to values for efficient data retrieval.

•	Cryptography: Ensuring data integrity and security (e.g., SHA-256, MD5).

•	Data Structures: Implementing sets, dictionaries, and caches

𝐈𝐦𝐩𝐥𝐞𝐦𝐞𝐧𝐭𝐚𝐭𝐢𝐨𝐧 𝐨𝐟 𝐇𝐚𝐬𝐡𝐢𝐧𝐠:

**Step 1: Define the Node Structure**
Each node will store a key-value pair and a pointer to the next node (for handling collisions using separate chaining).

```cpp
#include <iostream>
#include <vector>
#include <list>
#include <string>

using namespace std;

class HashNode {
public:
    string key;
    string value;
    HashNode* next;

    HashNode(string key, string value) {
        this->key = key;
        this->value = value;
        this->next = nullptr;
    }
};

```

**Step 2: Define the Hash Table Class**

The hash table will use an array of pointers to _HashNode_ objects. We’ll also define the hash function and methods for insertion and retrieval.

```cpp
class HashTable {
private:
    vector<HashNode*> table;
    int capacity;

    int hashFunction(string key) {
        int hash = 0;
        for (char ch : key) {
            hash += ch;
        }
        return hash % capacity;
    }

public:
    HashTable(int size) {
        capacity = size;
        table.resize(capacity, nullptr);
    }

    void insert(string key, string value) {
        int index = hashFunction(key);
        HashNode* newNode = new HashNode(key, value);

        if (table[index] == nullptr) {
            table[index] = newNode;
        } else {
            HashNode* temp = table[index];
            while (temp->next != nullptr) {
                temp = temp->next;
            }
            temp->next = newNode;
        }
    }

    string get(string key) {
        int index = hashFunction(key);
        HashNode* temp = table[index];

        while (temp != nullptr) {
            if (temp->key == key) {
                return temp->value;
            }
            temp = temp->next;
        }
        return "Key not found";
    }
};
```
**Step 3: Test the Hash Table**
Let's now insert and retrieve some key-value pairs.

```cpp
int main() {
    HashTable hashTable(10);

    hashTable.insert("name", "Harini");
    hashTable.insert("age", "20");
    hashTable.insert("city", "Mumbai");

    cout << "Name: " << hashTable.get("name") << endl;  // Output: Harini
    cout << "Age: " << hashTable.get("age") << endl;    // Output: 20
    cout << "City: " << hashTable.get("city") << endl;  // Output: Mumbai

    return 0;
}

```
𝐂𝐨𝐧𝐜𝐥𝐮𝐬𝐢𝐨𝐧:
Hashing is a powerful technique used to transform data into a fixed-size hash value. It is widely used in data retrieval, security, and data integrity.
Understanding hashing and its applications can help you efficiently manage and secure data.
By mastering the concept of hashing, you can enhance your programming skills and develop more efficient and secure applications. Happy coding!

𝐑𝐞𝐬𝐨𝐮𝐫𝐜𝐞𝐬:

1)	[Hashing by Strivers]( https://youtu.be/KEs5UyBJ39g?si=f0jAGCdYfguyN5dQ)

2)	[What is Hashing and how does it work?]( https://www.codecademy.com/resources/blog/what-is-hashing/)

3)	[What is Hashing?]( https://www.geeksforgeeks.org/what-is-hashing/)

4)	[Seperate Chaining](https://www.geeksforgeeks.org/separate-chaining-collision-handling-technique-in-hashing/?ref=lbp)

5)	[Open Addressing](https://www.geeksforgeeks.org/open-addressing-collision-handling-technique-in-hashing/)

