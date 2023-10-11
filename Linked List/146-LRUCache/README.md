# LRU Cache
![#ffa500](https://placehold.co/1x1/ffa500/ffa500.png) `Medium` 

> Design a data structure that follows the constraints of a Least Recently Used (LRU) cache.

Implement the LRUCache class:
- LRUCache(int capacity) Initialize the LRU cache with positive size capacity.
- int get(int key) Return the value of the key if the key exists, otherwise return $-1$.
- void put(int key, int value) Update the value of the key if the key exists. Otherwise, add the key-value pair to the cache. If the number of keys exceeds the capacity from this operation, evict the least recently used key.
The functions get and put must each run in $O(1)$ average time complexity.

 
Example 1:
> **Input**\
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]\
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]\
**Output**\
[null, null, null, 1, null, -1, null, -1, 3, 4]\
**Explanation**\
LRUCache lRUCache = new LRUCache(2);\
lRUCache.put(1, 1); // cache is {1=1}\
lRUCache.put(2, 2); // cache is {1=1, 2=2}\
lRUCache.get(1);    // return 1\
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}\
lRUCache.get(2);    // returns -1 (not found)\
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}\
lRUCache.get(1);    // return -1 (not found)\
lRUCache.get(3);    // return 3\
lRUCache.get(4);    // return 4

Problem can be found in [here](https://leetcode.com/problems/lru-cache/)!

## Solution
### [Solution](/Linked%20List/146-LRUCache/solution.py)

Time Complexity for put and get operation: ![O(1)](<https://latex.codecogs.com/svg.image?\inline&space;O(1)>), Space Complexity: ![O(n)](<https://latex.codecogs.com/svg.image?\inline&space;O(n)>)
