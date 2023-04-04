# LeetCode Daily Challenge Problems for April

<br><br>

## Workflow Checking

<div align="center">
<img src="https://github.com/7oSkaaa/LeetCode_DailyChallenge_2023/actions/workflows/Author_Line.yml/badge.svg" alt="Checkers" width="150">
<a href="https://github.com/7oSkaaa/LeetCode_DailyChallenge_2023/actions/workflows/Author_Line.yml" taget="_blank"/>
</img>
&nbsp;
<img src="https://github.com/7oSkaaa/LeetCode_DailyChallenge_2023/actions/workflows/File_Names.yml/badge.svg" alt="Checkers" width="150">
<a href="https://github.com/7oSkaaa/LeetCode_DailyChallenge_2023/actions/workflows/File_Names.yml" taget="_blank"/>
</img>
&nbsp;
<img src="https://github.com/7oSkaaa/LeetCode_DailyChallenge_2023/actions/workflows/Daily_Problem.yml/badge.svg" alt="Checkers" width="150">
<a href="https://github.com/7oSkaaa/LeetCode_DailyChallenge_2023/actions/workflows/Daily_Problem.yml" taget="_blank"/>
</img>
</div>

<br><br>

## Problems:

1. **[Binary Search](#01--binary-search)**

1. **[Successful Pairs of Spells and Potions](#02--successful-pairs-of-spells-and-potions)**
1. **[Boats to Save People](#03--boats-to-save-people)**
1. **[Optimal Partition of String](#04--optimal-partition-of-string)**

<hr>
<br><br>

## 01)  [Binary Search](https://leetcode.com/problems/binary-search/)

### Difficulty

![](https://img.shields.io/badge/Easy-green?style=for-the-badge)

### Related Topic

`Array` `Binary Search`

### Code


```cpp
class Solution {
public:
    int search(vector < int >& nums, int target) {
        // the start and end of the interval that we will search in it
        int l = 0, r = nums.size() - 1;

        // Start a while loop with condition "l <= r".
        while(l <= r){
            // Declare an integer variable "m" and initialize it to the midpoint between "l" and "r".
            int m = l + (r - l) / 2;
            
            // If the value at index "m" in the "nums" vector is equal to the target integer, return "m".
            if(nums[m] == target) return m;
            
            // If the value at index "m" in the "nums" vector is less than the target integer, update "l" to "m + 1". Otherwise, update "r" to "m - 1".
            (nums[m] < target ? l = m + 1 : r = m - 1);
        }

        // If the target integer was not found in the "nums" vector, return -1.
        return -1;
    }
};
```
    

<hr>
<br><br>

## 02)  [Successful Pairs of Spells and Potions](https://leetcode.com/problems/successful-pairs-of-spells-and-potions/)

### Difficulty

![](https://img.shields.io/badge/Medium-orange?style=for-the-badge)

### Related Topic

`Array` `Two Pointers` `Binary Search` `Sorting`

### Code


```cpp
class Solution {
public:

    // Inline function to calculate the ceil value
    inline long long ceil(long long a, long long b){
        return (a + b - 1) / b;
    }

    // Function to calculate successful pairs
    vector < int > successfulPairs(vector < int >& spells, vector < int >& potions, long long success) {
        // Get the sizes of vectors
        int n = spells.size(), m = potions.size();
        
        // Sort potions vector
        sort(potions.begin(), potions.end());
        
        // Vector to store successful pairs
        vector < int > successful_pairs;
        
        for(auto& x : spells){
            // Calculate target value for a spell that will make it greater than success
            long long target = ceil(success, x);
            
            // Get the index of first potion having value greater or equal to target
            int idx = lower_bound(potions.begin(), potions.end(), target) - potions.begin();
            
            // Calculate number of successful pairs
            successful_pairs.push_back(m - idx);
        }

        // Return the vector containing number of successful pairs for each spell
        return successful_pairs;
    }
};
```
    
<hr>
<br><br>

## 03)  [Boats to Save People](https://leetcode.com/problems/boats-to-save-people/)

### Difficulty

![](https://img.shields.io/badge/Medium-orange?style=for-the-badge)

### Related Topic

`Array` `Two Pointers` `Greedy` `Sorting`

### Code


```cpp
class Solution {
public:
    // Function to calculate the number of rescue boats required
    int numRescueBoats(vector<int>& people, int limit) {
        // Sort the array in ascending order
        sort(people.begin(), people.end());
        
        // Initialize variables for left index, right index and number of boats
        int l = 0, r = people.size() - 1, boats = 0;
        
        // Iterate through the array using two pointers, one from the left and one from the right
        while(l <= r){
            // If the sum of the weights of the people at the two pointers is less than or equal to the limit, increment the left pointer
            if(people[l] + people[r] <= limit) l++;
            
            // Decrement the right pointer and increment the number of boats
            r--, boats++;
        }
        
        // Return the total number of boats required
        return boats;
    }

};
```
    
<hr>
<br><br>

## 04)  [Optimal Partition of String](https://leetcode.com/problems/optimal-partition-of-string/)

### Difficulty

![](https://img.shields.io/badge/Medium-orange?style=for-the-badge)

### Related Topic

`Hash Table` `String` `Greedy`

### Code


```cpp
class Solution {
public:
    int partitionString(string& s) {
        int partitions = 1, mask = 0;
        
        // Iterate over each character in the string
        for(auto& c : s){
            // Create a mask for the current character
            int curr_mask = (1 << (c - 'a'));
            
            // If the current mask is already present in the mask variable
            // increment the number of partitions and reset the mask variable
            if(mask & curr_mask)
                partitions++, mask = 0;
            
            // XOR the current mask with the mask variable
            mask ^= curr_mask;
        }
        
        // Return the number of partitions
        return partitions;
    }
};
```
    