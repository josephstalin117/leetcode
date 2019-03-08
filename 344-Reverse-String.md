Write a function that reverses a string. The input string is given as an array of characters char[].

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

You may assume all the characters consist of printable ascii characters.

#### Example1:
```
Input: ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```

#### Example2:
```
Input: ["H","a","n","n","a","h"]
Output: ["h","a","n","n","a","H"]
```

#### Solution
```
class Solution {
public:
    void reverseString(vector<char>& s) {
        int halfLength = s.size() / 2;
        char temp;
        for (int i = 0; i < halfLength; i++) {
            temp = s[s.size() - 1 - i];
            s[s.size() - 1 - i] = s[i];
            s[i] = temp;
        }
    }
};
```
