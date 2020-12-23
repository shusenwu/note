 ```
1. mergingLetters  
ex:
input: "abc", "12345", output: "a1b2c345"  
input: "abc", "1", output: "a1bc"  
```
  
```
Quesiton 1  
You are given an integer n. Your task is to calculate how many times the digits 0, 2 and 4 appear in all the non-negative integers up to n (0, 1, ...., n).  
Example  
• For n = 10, the output should be countOccurrences(n) = 4.  
  ○ The digit 0 appears in numbers 0 and 10 once, for a total of 2 occurrences,  
  ○ The digit 2 appears in the number 2 once, for a total of 1 occurrence,  
  ○ The digit 4 appears in the number 4 once, for a total of 1 occurrence.So the answer is 2 + 1 + 1 = 4.  
• For n = 22, the output should be countOccurrences(n) = 11.  
  ○ The digit 0 appears in numbers 0, 10, and 20 once, for a total of 3 occurrences,  
  ○ The digit 2 appears in numbers 2, 12, 20, and 21 once, and in the number 22 twice, for a total of 6 occurrences,  
  ○ The digit 4 appears in numbers 4 and 14 once, for a total of 2 occurrences.So the answer is 3 + 6 + 2 = 11.  
Input/Output
• [execution time limit] 4 seconds (py3)
• [input] integer nAn integer.Guaranteed constraints:0 ≤ n ≤ 1000.
• [output] integerThe overall count of occurrences of digits 0, 2 and 4 in the integers from 0 to n inclusive.
```
```
2. countWaysToSplit  
给定字符串s，求分解成a, b, c三个substrings的所有可能性的个数，要求 a+ b != b + c != c + a。    
```

```
Q2: remove lowest peak from positive int array, input: [1,6,2,4,3] , output remove in order: [4,3,6,2,1], peak means a[i] > its left/right neighbors(if there are)  
description mentioned each pair in the array is unique, I am not sure what it means  for [1,2,1] where  there is (1,2) and (2,1)  
```

```
Quesiton 2
You are given a string str containing only the letters W, D, and L. Your task is to construct a new string from the characters of str, according to the following algorithm:
1. Begin with an empty string output = "".
2. If str contains a W, then remove it and concatenate a W to the end of output.
3. If str contains a D, then remove it and concatenate a D to the end of output.
4. If str contains an L, then remove it and concatenate an L to the end of output.
5. If str is empty, end the algorithm; otherwise go back to step 2.
Return the value of output after the algorithm is complete.
Note that it doesn't matter from where you remove the letter from the string, only the count of the letters left in the string matters.
Example
• For str = "LDWDL", the output should be equallyRearranging(str) = "WDLDL".
  ○ str contains all W, D, and L, so we add them to the output and remove from the initial string one by one and get "WDL"
  ○ The remaining string contains only letters D and L, so we add them to the output and get "WDLDL" as the answer

• For str = "DLDD", the output should be equallyRearranging(str) = "DLDD".
  ○ The string doesn't contain W letters, and do contain both D and L, so we add them to the output and remove from the initial string. The output is "DL" after that
  ○ The remaining string contains only two letters D and nothing else, so in two more iterations we get the output equal "DLDD"
 ```


```
3. borderSort  
给定n x n的方阵，要求剥洋葱似的一层层分别排序重新填回这个方阵。比如说  
3 2 4                 1 2 3  
1 9 6     ==>     8 9 4  
5 7 8                 7 6 5  
```


```
https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=696384&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3089%5D%5Bvalue%5D%5B5%5D%3D5%26searchoption%5B3089%5D%5Btype%5D%3Dcheckbox%26searchoption%5B3046%5D%5Bvalue%5D%3D22%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline  
https://oss.1point3acres.cn/forum/202012/14/074617jpv2s77424w3276h.png!c  
Question 3
You've decided to create a bot for handling stock trades. For now, you have a simple prototype which handles trades for just one stock. Each day, it's programmed to either buy or sell one share of the stock.
You are given prices, an array of positive integers where prices[i] represents the stock price on the ith day. You're also given algo, an array of 0s and 1s representing the bot's schedule, where 0 means buy and 1 means sell.
In order to improve the bot's performance, you'd like to choose a range of k consecutive days where the bot will be programmed to sell; in other words, set a range of k consecutive elements from algo to 1. Your task is to choose the interval such that it maximizes the bot's total revenue. The revenue is defined as the sum of all selling prices minus the sum of all buying prices (in other words, the difference between the end and start amount).
NOTE: Assume you begin with enough shares of the stock that it's always possible to sell.
Example
For prices = [2, 4, 1, 5, 2, 6, 7], algo = [0, 1, 0, 0, 1, 0, 0], and k = 4, the output should be maxRevenueFromStocks(prices, algo, k) = 21.
First, let's calculate the revenue if the algorithm is left as it is without any change.
• Before the trades start, the revenue is 0;
• Day 0: algo[0] = 0, so we buy stocks at price prices[0] = 2, and the revenue becomes 0 - 2 = -2;
• Day 1: algo[1] = 1, so we sell stocks at price prices[1] = 4, and the revenue becomes -2 + 4 = 2;
• Day 2: algo[2] = 0, so we buy stocks at price prices[2] = 1, and the revenue becomes 2 - 1 = 1;
• Day 3: algo[3] = 0, so we buy stocks at price prices[3] = 5, and the revenue becomes 1 - 5 = -4;
• Day 4: algo[4] = 1, so we sell stocks at price prices[4] = 2, and the revenue becomes -4 + 2 = -2;
• Day 5: algo[5] = 0, so we buy stocks at price prices[5] = 6, and the revenue becomes -2 - 6 = -8;
• Day 6: algo[6] = 0, so we buy stocks at price prices[6] = 7, and the revenue becomes -8 - 7 = -15.
Thus, the total revenue is -15.

We can maximize the total revenue by making the last k = 4 orders 1 (sell), thus making algo = [0, 1, 0, 1, 1, 1, 1]. The total revenue will become -2 + 4 - 1 + 5 + 2 + 6 + 7 = 21.
Input/Output
• [execution time limit] 4 seconds (py3)
• [input] array.integer pricesAn array of integers representing the stock price for each day.Guaranteed constraints:1 ≤ prices.length ≤ 105,1 ≤ prices[i] ≤ 1000.
• [input] array.integer algoAn array of 0s and 1s, representing the bot's buy / sell schedule for each day.Guaranteed constraints:algo.length = prices.length,0 ≤ algo[i] ≤ 1.
• [input] integer kAn integer representing the number of consecutive days that can be made all equal to 1, i.e. marked as sell.Guaranteed constraints:0 ≤ k ≤ prices.length.
• [output] integerThe value of the maximum revenue that can be obtained.
```

```
4. combineTheGivenNumber  
给定整数数组A和整数x，找出所有（i, j）的个数，要求满足  i != j，A.concat(A[j]) == x 或者  A[j].concat(A) == x，如果这俩都满足就算两次。举个栗子：
A = [12, 121, 2, 12], x = 1212
那么12, 12 => 1212, 这个算两次，因为index (0, 3) 和（3, 0）都满足
121， 2 => 1212
所以最终输出3。
```

``` 
https://oss.1point3acres.cn/forum/202012/14/074659sw7lb1wuubbk1uwu.png!c 
https://www.1point3acres.com/bbs/forum.php?mod=viewthread&tid=696384&extra=page%3D1%26filter%3Dsortid%26sortid%3D311%26searchoption%5B3089%5D%5Bvalue%5D%5B5%5D%3D5%26searchoption%5B3089%5D%5Btype%5D%3Dcheckbox%26searchoption%5B3046%5D%5Bvalue%5D%3D22%26searchoption%5B3046%5D%5Btype%5D%3Dradio%26sortid%3D311%26orderby%3Ddateline  
Q4
Question 4
You are given a square matrix of characters a which size is n x n. Your task is to create a list of strings from the diagonals of a, where each string has a length of n, and then sort this created list.
We'll consider all diagonals that are parallel to the main diagonal, where each diagonal is considered to start at its upper point and end at its lower point. Since these diagonals will have different lengths, we'll traverse each one cyclically (ie: go back to the start of the diagonal after reaching the end) until we reach n characters.
Sort the resulting strings in lexicographical order, and return an array of 2n - 1 integers, representing the diagonals' 1-based indices in their sorted order. In the case of lexicographically equal strings, their indices should be kept in the original order.
Here's an example of how to count the diagonals for a 5 x 5 matrix (the number on the diagram corresponds to the diagonal index):
5 6 7 8 94 5 6 7 83 4 5 6 72 3 4 5 61 2 3 4 5
Example
• Fora = [["b", "b"],     ["c", "a"]]the output should be diagonalsArranging(a) = [2, 3, 1].
       
This matrix has n = 2 and contains 3 diagonals:
  ○ The diagonal with index 1 is ["c"] and its corresponding cyclic string is "cc";
  ○ The diagonal with index 2 is ["b", "a"] and its corresponding cyclic string is "ba";
  ○ The diagonal with index 3 is ["b"] and its corresponding cyclic string is "bb".The lexicographical ordering of the matrix diagonals looks like ["ba", "bb", "cc"], so the answer is [2, 3, 1].
• Fora = [["a", "c", "a", "b", "b"],      ["c", "b", "a", "c", "b"],      ["a", "a", "e", "c", "b"],      ["b", "b", "d", "a", "g"],      ["a", "b", "e", "b", "a"]]the output should be diagonalsArranging(a) = [1, 5, 3, 7, 2, 8, 9, 6, 4].
       
This matrix has n = 5 and contains 9 diagonals:
  ○ The diagonal with index 1 is ["a"] and its corresponding cyclic string is "aaaaa",
  ○ The diagonal with index 2 is ["b", "b"] and its corresponding cyclic string is "bbbbbb",
  ○ The diagonal with index 3 is ["a", "b", "e"] and its corresponding cyclic string is "abeab",
  ○ The diagonal with index 4 is ["c", "a", "d", "b"] and its corresponding cyclic string is "cadbc",
  ○ The diagonal with index 5 is ["a", "b", "e", "a", "a"] and its corresponding cyclic string is "abeaa",
  ○ The diagonal with index 6 is ["c", "a", "c", "g"] and its corresponding cyclic string is "cacgc",
  ○ The diagonal with index 7 is ["a", "c", "b"] and its corresponding cyclic string is "acbac",
  ○ The diagonal with index 8 is ["b", "b"] and its corresponding cyclic string is "bbbbb",
  ○ The diagonal with index 9 is ["b"] and its corresponding cyclic string is "bbbbb".The lexicographical ordering of the matrix diagonals looks like ["aaaaa", "abeaa", "abeab", "acbac", "bbbbb", "bbbbb", "bbbbb", "cacgc", "cadbc"], so the answer is [1, 5, 3, 7, 2, 8, 9, 6, 4].Note that the cyclic string "bbbbb" occurs 3 times, and the indices corresponding to this cyclic string appear in ascending order in the output: [2, 8, 9].
Input/Output
```

```
https://leetcode.com/problems/check-array-formation-through-concatenation/  
```
