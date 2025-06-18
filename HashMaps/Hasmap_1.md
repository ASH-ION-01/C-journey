📘 Hashing in C++ — Learning Log
🔍 What is Hashing?
Hashing is a technique used to convert a large input (like a string or number) into a smaller, fixed-size value — called a hash code — which is used as an index in a Hash Table.

Goal: Fast insertion, deletion, and lookup — ideally in O(1) average time.

📦 Real-World Applications of Hashing
Database indexing (e.g., searching by key)

Cryptographic hashing

Caching (e.g., memoization)

Symbol tables (compiler design)

Implementing associative containers like unordered_map, unordered_set

🛠️ Key Components of Hashing
Key: The actual input (e.g., string/number).

Hash Function: Converts key → index.

Hash Table: An array or structure that stores the data at hash indexes.

⚙️ How Hashing Works – Example
Let’s say we have a table of size 7 and input strings:
{ "ab", "cd", "efg" }

Assign values to characters: a=1, b=2, ..., z=26

Now use:
sum of characters % 7

ini
Copy
Edit
"ab"  = (1+2) % 7  = 3
"cd"  = (3+4) % 7  = 0
"efg" = (5+6+7) % 7 = 18 % 7 = 4
📌 Stored at indices: ab → 3, cd → 0, efg → 4

⚠️ What is a Collision?
When two keys produce the same index:

Example: "ab" and "ba" both → 3

We resolve collisions using:

🧯 Collision Resolution Techniques
1. Separate Chaining
Each index in hash table points to a linked list (or vector) of elements.

cpp
Copy
Edit
vector<list<string>> hashTable(size);
2. Open Addressing
Store elements directly in the table, probe for empty slots if a collision occurs.

🔁 Linear Probing: Check next slot: (i+1) % size

🔁 Quadratic Probing: Check i^2 distances: (i + i*i) % size

🔁 Double Hashing: Use second hash function
h(k, i) = (h1(k) + i * h2(k)) % tableSize

📐 Load Factor and Rehashing
Load Factor = elements / table size

When Load Factor > 0.75 → rehashing (double size, reinsert all elements)

🔨 Hashing in C++ — STL Containers
Type	Description	Uses Hashing	Maintains Order
unordered_map	Key-value store	✅ Yes	❌ No
unordered_set	Unique keys only	✅ Yes	❌ No
map	Key-value (RB Tree)	❌ No	✅ Sorted keys
set	Unique values (RB Tree)	❌ No	✅ Sorted values

🧪 Code Example: unordered_map in C++
cpp
Copy
Edit
#include <iostream>
#include <unordered_map>
using namespace std;

int main() {
    unordered_map<string, int> freq;

    // Insert
    freq["apple"] = 2;
    freq["banana"] = 5;
    freq["apple"] += 1;

    // Access
    cout << "apple: " << freq["apple"] << endl;

    // Check presence
    if (freq.find("banana") != freq.end()) {
        cout << "banana is present\n";
    }

    // Loop
    for (auto& pair : freq) {
        cout << pair.first << " -> " << pair.second << endl;
    }

    return 0;
}
💡 Interview Tips
Know when hashing is not ideal:

You need sorted data → Use map (Red-Black Tree)

Prefix search → Use Trie

Need floor/ceil → Use set or map

Load Factor, Collision Handling, and Good Hash Function principles are frequently asked in interviews.

📚 Summary of What I Learned
✅ How hashing works in C++
✅ Difference between map vs unordered_map
✅ What collisions are and how to handle them
✅ Different probing techniques: linear, quadratic, double hashing
✅ How STL containers use hash functions
✅ When not to use hashing
✅ How to implement hash tables manually

📁 Next Steps
 Implement your own Hash Table using:

Separate Chaining (linked list at each index)

Open Addressing (Linear / Quadratic probing)

 Solve problems on:

LRU Cache

Group Anagrams

Subarray Sum = K