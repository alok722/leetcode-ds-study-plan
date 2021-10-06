<h1 align="center">2 Weeks Study Plan to Tackle DS 💻 (LeetCode)</h1>
<h2 align="center">Day 1</h2>

## [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/)
> Given an integer array nums, return true if any value appears at least twice in the array, and return false if every element is distinct.
```java
// Brute force: Iterate through and find if numbers are equal then return true;
class Solution {
    public boolean containsDuplicate(int[] nums) {
        for(int i = 0; i < nums.length; i++) {
           for(int j = i+1; j < nums.length; j++) {
            if(nums[i] == nums[j]) {
                return true;
            }
           } 
        }
        return false;
    }
}
```
Or,
```java
// Using Set DataStructure, Set doesn’t allow duplicates to insert, if duplicates are inserted it return false;
class Solution {
    public boolean containsDuplicate(int[] nums) {
        Set<Number> store = new HashSet<>(); 
        for (int num : nums) { 
            if (store.add(num) == false) { 
                return true;
            }
        }
        return false;
    }
}
```

## [Maximum Subarray](https://leetcode.com/problems/maximum-subarray/)
> Given an integer array nums, find the contiguous subarray (containing at least one number) which has the largest sum and return its sum.
```java
// Brute force way would be to find all possible combination and return the maximum sum
// 4, 3, -2, 6, -14, 7, -1, 4, 5, 7, -10, 2, 9, -10, -5, -9, 6, 1

// Consider the 0th index value as the maximum currentSum & OverAll Sum. Starte a simple for loop from the 1st index because the 0th is already taken. So, inside the loop, overall idea ye hai ki jo v new element aa rhi hai wo sochta hai ki agar mai individual continue krunga to fayde me rhunga ya currentSum se jurne me fayde me rhunga… Agar individual me fayda hota hai to currentSum wo khud ko declare kr deta hai ya wo currentSum ke add ho jata h. Aur har iteration me maxSum ko currentSum ke sath compare krke dekh leta h aur update kr deta h. 

class Solution {
    public int maxSubArray(int[] nums) {
        int currentSum = nums[0];
        int overAllSum = nums[0];
        for(int i = 1; i < nums.length; i++) {
            // agar pichhe se positive aa rha to sath ho jaane me fayda h
            if(currentSum >= 0) {
                currentSum += nums[i];
            } else {
                currentSum = nums[i];
            }
            if(currentSum > overAllSum) {
                overAllSum = currentSum;
            }
        }
        return overAllSum;
    }
}
```
Or,
```java
class Solution {
    public int maxSubArray(int[] nums) {
        int maxSum = nums[0];
        int currentSum = maxSum;
        for(int i = 1; i < nums.length; i++){
            currentSum = Math.max(nums[i] + currentSum, nums[i]);
            maxSum = Math.max(currentSum, maxSum);
        }
        return maxSum;
    }
}
```
<hr>

<h2 align="center">Day 2</h2>

## [Two Sum](https://leetcode.com/problems/two-sum/)
> Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
You may assume that each input would have exactly one solution, and you may not use the same element twice.
You can return the answer in any order.
```java
// Brute Force
public int[] twoSum(int[] nums, int target) {
    // This loop will consider first
    for(int i = 0; i < nums.length; i++){
        // This loop helps to provide one value ahead from previous value
        for(int j = i + 1; j < nums.length; j++){
            // We are comparing the jth value with target - ith value.
            // If they are same we will return our indices in the array.
            if(nums[j] == target - nums[i]){
                return new int[] {i, j};
            }
        }
    }
    // If unable to get return empty array
    return new int[]{};
}
```
Or,
```java
// Optimal Solution(HashMap)
public int[] twoSum(int[] nums, int target) {
    // inserted Value & Indices
    HashMap<Integer, Integer> map = new HashMap<>();
    
    // Filling the HashMap
    for(int i = 0; i < nums.length; i++){
        map.put(nums[i], i);
    }
    // Searching for the target indices
    for(int i = 0; i < nums.length; i++){
        // I will get my first element Example:- [2,7,11,15], target = 9
        int num = nums[i]; // I will get 2 
        int rem = target - num; // Calculating remaining value = 9 - 2 = 7 will get from here
        if(map.containsKey(rem)){ // Now I will check that on any index 7 is present.
            int index = map.get(rem); // From here i will get the index for no. 7
            if(index == i) continue; // By doing this i will handle the case to not select more then one of yourself.
            return new int[]{i, index}; // returning the array with their indices.
        }
    }
    return new int[]{}; // If we are unable to find return empty array.
}
```

## [Merge Sorted Array](https://leetcode.com/problems/merge-sorted-array/)
> You are given two integer arrays nums1 and nums2, sorted in non-decreasing order, and two integers m and n, representing the number of elements in nums1 and nums2 respectively.
Merge nums1 and nums2 into a single array sorted in non-decreasing order.
The final sorted array should not be returned by the function, but instead be stored inside the array nums1. To accommodate this, nums1 has a length of m + n, where the first m elements denote the elements that should be merged, and the last n elements are set to 0 and should be ignored. nums2 has a length of n.
```java
// Straight Forward Approach
/*
	
	They have given the value of m and n in the question itself. 
	So, we have to start inserting the values from the num2 array after the value of m.
	
	(i.e If the value of m is 3, you should start inserting elements from num2 in the 4th index of num1.)
	
	*/
	
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        int count=0;
        for(int i=m; i<nums1.length; i++) // traversing num1 such that to fill the remaining values from num2
        {

            nums1[i] = nums2[count];// inserting in nums1
            count++; // increasing the count to retrieve next value from num2
        }
        Arrays.sort(nums1); // sort the array finally to print in ascending order!
    }
}
```
Or,
```java
// Two Pointer Method
class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
     // Comparing Last valid element of both arrays and inserting the bigger one at the last position of the 1st array.
        int i = m - 1; // start pointer
        int j = n - 1; // end pointer
        int index = nums1.length - 1; // mid
        while (index >= 0 && i >= 0 && j >= 0) {
            if(nums1[i] > nums2[j])  {
                nums1[index] = nums1[i];
                i--;
                index--;
            } else {
                nums1[index] = nums2[j];
                j--;
                index--;
            }
        }
        // Check for check in case some elements from nums2 are still there. 
        // No need to do the same for nums1, it would be already sorted and in place
        while (j >= 0) {
            nums1[index--] = nums2[j--];
        }
    }
}
```
<hr>

<h2 align="center">Day 3</h2>

## [Intersection of Two Arrays II](https://leetcode.com/problems/intersection-of-two-arrays-ii/)
> Given two integer arrays nums1 and nums2, return an array of their intersection. Each element in the result must appear as many times as it shows in both arrays and you may return the result in any order.
```java
class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        List<Integer> arr = new ArrayList<Integer>();
        HashMap<Integer, Integer> hm1 = new HashMap<>();
        HashMap<Integer, Integer> hm2 = new HashMap<>();
        
        for(int i = 0; i < nums1.length; i++) {
            if(hm1.containsKey(nums1[i])) {
                hm1.put(nums1[i], hm1.get(nums1[i])+1);
            } else {
                hm1.put(nums1[i], 1);
            }
        }
        
        for(int i = 0; i < nums2.length; i++) {
            if(hm2.containsKey(nums2[i])) {
                hm2.put(nums2[i], hm2.get(nums2[i])+1);
            } else {
                hm2.put(nums2[i], 1);
            }
        }
        
        for(Integer key: hm1.keySet()) {
        // After having the frequency of both array, have to check which of them    are intersecting
            if(hm2.containsKey(key)) {
                // Get the minimum frequency of intersection one
                int x = Math.min(hm2.get(key), hm1.get(key));
                while(x != 0) {
                    arr.add(key);
                    x--;
                }
            }
        }

        int res[] = new int[arr.size()];
        for(int i = 0; i < arr.size(); i++) res[i] = arr.get(i);
        return res;
    }
}
```
Or,
```java
/* Simply Hash all the Elements of one array into a hashmap with their frequencies and then
   traverse other array and check if this element exists in hashmap if yes then,decrease its
   frequency by 1
*/

class Solution {
    public int[] intersect(int[] nums1, int[] nums2) {
        ArrayList<Integer> arr = new ArrayList<>();
        Map<Integer,Integer> map1 = new HashMap<>();
       
        for(int i = 0;i<nums1.length;i++){
            map1.put(nums1[i],map1.getOrDefault(nums1[i],0) + 1);
        }
        
        for(int i = 0;i<nums2.length;i++){
            if(map1.containsKey(nums2[i]) && map1.get(nums2[i]) > 0){
                arr.add(nums2[i]);
                map1.put(nums2[i],map1.get(nums2[i]) - 1);
            }
        }
        
        int size = arr.size();
        int [] ans = new int[size];
        for(int i = 0;i<size;i++){
            ans[i] = arr.get(i);
        }
        
        return ans;
    }
}
```

## [Best Time to Buy and Sell Stock](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)
> You are given an array prices where prices[i] is the price of a given stock on the ith day.
You want to maximize your profit by choosing a single day to buy one stock and choosing a different day in the future to sell that stock.
Return the maximum profit you can achieve from this transaction. If you cannot achieve any profit, return 0.
```java
class Solution {
    public int maxProfit(int[] prices) {
        int maxProfit = 0;
        int minPrice = prices[0];
        for(int i = 1; i < prices.length; i++) {
            minPrice = Math.min(minPrice, prices[i]);
            maxProfit = Math.max(maxProfit, prices[i]-minPrice);
        }
        return maxProfit;
    }
}
```
Or,
```java
class Solution {
    public int maxProfit(int[] prices) {
        int minimumPriceSoFar = Integer.MAX_VALUE;
        int overAllProfit = 0;
        int profitIfSoldToday = 0;
        for(int i = 0; i < prices.length; i++) {
            if(prices[i] < minimumPriceSoFar) {
                minimumPriceSoFar = prices[i];
            }
            profitIfSoldToday = prices[i]-minimumPriceSoFar;
            if(profitIfSoldToday > overAllProfit) {
                overAllProfit = profitIfSoldToday;
            }
        }
        return overAllProfit;
    }
}
```
<hr>

<h2 align="center">Day 4</h2>

## [Reshape the Matrix](https://leetcode.com/problems/reshape-the-matrix/)
> In MATLAB, there is a handy function called reshape which can reshape an m x n matrix into a new one with a different size r x c keeping its original data.
You are given an m x n matrix mat and two integers r and c representing the number of rows and the number of columns of the wanted reshaped matrix.
The reshaped matrix should be filled with all the elements of the original matrix in the same row-traversing order as they were.
If the reshape operation with given parameters is possible and legal, output the new reshaped matrix; Otherwise, output the original matrix.

```java
// Brute Force - Copy original 2D into 1D array, then array 1D into required 2D
class Solution {
    public int[][] matrixReshape(int[][] mat, int r, int c) {
	  // Result 2D Matrix
        int[][] result = new int[r][c];
        // Source Matrix Size
        int rowOfMatrix = mat.length;
        int colOfMatrix = mat[0].length;
        // If target matrix is feasible
        boolean matrixReshapePossible = (rowOfMatrix * colOfMatrix) == r * c ? true : false;

        if(matrixReshapePossible){
            //2D matrix to 1D array conversion
            int[] ans = new int[rowOfMatrix * colOfMatrix];
            int idx = 0;
            for(int i = 0; i < rowOfMatrix ; i++ ){
                for(int j = 0; j < colOfMatrix; j++){
                    ans[idx] = mat[i][j];
                    idx++;
                }
            }
            
            //Copy elements from 1D array to result matrix;
            idx = 0;
            for(int i = 0; i < r; i++){
                for(int j = 0; j < c; j++){
                    result[i][j] = ans[idx];
                    idx++;
                }
            }
            return result;
        }
        return mat;
    }
}
```
Or,
```java
class Solution {
    public int[][] matrixReshape(int[][] mat, int r, int c) {
        // extract source matrix row/column count
        int m = mat.length;
        int n = mat[0].length;
        // check if the target matrix is possible?
        if(r*c != m*n) return mat;
        // what if source and destination shape is same
        if(r==m && c==n) return mat;
        int[][] res = new int[r][c];
        for(int i=0; i<r*c; i++){
            // for [3,1] position = 10, Row = Position/Column (3)
            // Col = Position%Column (1)
            res[i/c][i%c] = mat[i/n][i%n];
        }
        return res;
    }
}
```

## [Pascal's Triangle](https://leetcode.com/problems/pascals-triangle/)
> Given an integer numRows, return the first numRows of Pascal's triangle.
```java
// 💡 Pascal’s Triangle number at [i,j] position
// If Row = 5, Column = 3, Value at [5,3] = R-1C C-1; i.e. 4c2 = (4*3)/(2*1) = 6;
// 💡 Print Nth Row:
// Brute force: loop up to n and calculate value for each position using above formula, but its O(n^2)
// Better Approach: ?

public class Solution {
    public List<List<Integer>> generate(int numRows) {
        // Final Result List
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        // To keep track of previous Row
        ArrayList<Integer> pre = null;
        for (int i = 1; i <= numRows; i++) {
            // Intermediate Temp List
            ArrayList<Integer> save = new ArrayList<>();
            for (int j = 1; j <= i; j++)
                if (j == 1 || j == i) save.add(1);
                else save.add(pre.get(j-1) + pre.get(j-2)); // ?
            result.add(save);
            pre = save;
        }
        return result;
    }
}
```
<hr>

<h2 align="center">Day 5</h2>

## [Valid Sudoku](https://leetcode.com/problems/valid-sudoku/)
> Determine if a 9 x 9 Sudoku board is valid. Only the filled cells need to be validated according to the following rules:
Each row must contain the digits 1-9 without repetition.
Each column must contain the digits 1-9 without repetition.
Each of the nine 3 x 3 sub-boxes of the grid must contain the digits 1-9 without repetition.
```java
// The idea is, if some element at a certain column is added to a set, then it wont allow duplicates. Hence, return false.
class Solution {
    public boolean isValidSudoku(char[][] board) {
        Set seen = new HashSet();
        for (int i=0; i<9; ++i) {
            for (int j=0; j<9; ++j) {
                char number = board[i][j];
                if (number != '.')
                    if (!seen.add(number + " in row " + i) ||
                        !seen.add(number + " in column " + j) ||
                        !seen.add(number + " in block " + i/3 + "-" + j/3))
                        return false;
            }
        }
        return true;
    }
}
```

## [Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/)
> Write an efficient algorithm that searches for a value in an m x n matrix. This matrix has the following properties:
Integers in each row are sorted from left to right.
The first integer of each row is greater than the last integer of the previous row.
```java
// Brute Force
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        for(int i = 0; i < matrix.length; i++) {
            for(int j = 0; j < matrix[0].length; j++) {
                if(matrix[i][j] == target) return true;
            }
        }
        return false;
}
```
Or,
```java
// Optimized using binary search approach since the elements are sorted.
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int i = 0, j = matrix[0].length - 1;
        while (i < matrix.length && j >= 0) {
                if (matrix[i][j] == target) {
                    return true;
                } else if (matrix[i][j] > target) {
                    j--;
                } else {
                    i++;
                }
            }

        return false;
    }
}
```
<hr>

<h2 align="center">Day 6</h2>

## [First Unique Character in a String](https://leetcode.com/problems/first-unique-character-in-a-string/)
> Given a string s, find the first non-repeating character in it and return its index. If it does not exist, return -1.
```java
class Solution {
    public int firstUniqChar(String s) {
        // To create counter of each character
        Map<Character, Integer> map = new HashMap<>();
        for(int i=0;i<s.length();i++) {
            char c = s.charAt(i);
            if(map.containsKey(c)) {
                map.put(c, map.get(c)+1);
            }
            else
                map.put(c,1);
        }
        // To check whose frequency is 1
        for(int i=0;i<s.length();i++) {
            char c = s.charAt(i);
            if(map.get(c)==1)
                return i;
        }
        return -1;
    }
}
```

## [Ransom Note](https://leetcode.com/problems/ransom-note/)
> Given two stings ransomNote and magazine, return true if ransomNote can be constructed from magazine and false otherwise.
Each letter in magazine can only be used once in ransomNote.
```java
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        Map<Character, Integer> magazineMap = new HashMap<>();
        for(int i = 0; i < magazine.length(); i++) {
            char c = magazine.charAt(i);
            if(magazineMap.containsKey(c)) {
                magazineMap.put(c, magazineMap.get(c)+1);
            }
            else
                magazineMap.put(c,1);
        }
        for(int i = 0; i < ransomNote.length(); i++) {
            char c = ransomNote.charAt(i);
            // if character is not present in source hashmap, return false
            if(magazineMap.get(c) == null) return false;
            // if character's value is already reduced to zero, return false
            if(magazineMap.get(c) == 0) return false;
            // if character's value is greater or equal to 1, decrease the value by 1
            if(magazineMap.get(c) >= 1) magazineMap.put(c, magazineMap.get(c)-1);
        }
        return true;
    }
}
```
Or,
```java
// Other enhanced loop & methods
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        Map<Character, Integer> counts = new HashMap<>();
        for(char c: magazine.toCharArray()) {
            counts.put(c, counts.getOrDefault(c,0) + 1);
        }
        for(char c: ransomNote.toCharArray()) {
            if(!counts.containsKey(c) || counts.get(c) <= 0) return false;
            counts.put(c, counts.get(c) - 1);
        }
        return true;
    }
}
```

## [Valid Anagram](https://leetcode.com/problems/valid-anagram/)
> Given two strings s and t, return true if t is an anagram of s, and false otherwise.
```java
class Solution {
    public boolean isAnagram(String s, String t) {
      int[] alphabet = new int[26];
      // a unicode value = 97; so if in string s comes up, it means 97-97 = 0; so, alphabet[0] = 1 and so on,
      for (int i = 0; i < s.length(); i++) alphabet[s.charAt(i) - 'a']++;
      // In this loop, we are decreasing the corresponding value
      for (int i = 0; i < t.length(); i++) alphabet[t.charAt(i) - 'a']--;
      // We are checking if all the values are zero or not
      for (int i : alphabet) if (i != 0) return false;
      return true;
    }
}
```