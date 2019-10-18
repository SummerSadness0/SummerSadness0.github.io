---
title: Leetcode中组合总和系列
date: 2019-10-16 20:24:38
tags: 算法
---



### 一、Leetcode77.   组合

#### 1、题目

> 给定两个整数 n 和 k，返回 1 ... n 中所有可能的 k 个数的组合。
>
> **示例:**
>
> **输入**: n = 4, k = 2
> **输出**:
> [
>   [2,4],
>   [3,4],
>   [2,3],
>   [1,2],
>   [1,3],
>   [1,4],
> ]

#### 2、思路

回溯算法，思路如图所示

![](http://cdn.processon.com/5da9adc8e4b04913a13c8cb4?e=1571404760&token=trhI0BY8QfVrIGn9nENop6JAc6l5nZuxhjQ62UfM:THzF2wflcZrbPckUHuN_wLB4jak=)

#### 3、代码

Leetode

``` java
class Solution {
    List<List<Integer>> res = new ArrayList<>();
    public List<List<Integer>> combine(int n, int k) {
        List<Integer> list = new ArrayList<>();
        backtrack(n, k, 1, list);
        return res;
    }
    public void backtrack(int n, int k, int start, List<Integer> list){
        if(k == 0){
            res.add(new ArrayList<>(list));
            return;
        }
        for(int i = start; i <= n; i++){
            list.add(i);
            backtrack(n, k-1, i+1, list);
            list.remove(list.size()-1);
        }
    }
}
```

### 二、Leetcode39.    组合总和

#### 1、题目

> 给定一个**无重复元素**的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。
>
> candidates 中的数字可以无限制重复被选取。
>
> **说明：**
>
> * 所有数字（包括 target）都是正整数。
> * 解集不能包含重复的组合。 
>
> **示例 1:**
>
> **输入:** candidates = [2,3,6,7], target = 7,
> **所求解集为:**
> [
>   [7],
>   [2,2,3]
> ]
> **示例 2:**
>
> **输入:** candidates = [2,3,5], target = 8,
> **所求解集为:**
> [
>   [2,2,2,2],
>   [2,3,3],
>   [3,5]
> ]
>
> 

#### 2、思路

#### 3、代码

class Solution {
    int res = 0;
    public int combinationSum4(int[] nums, int target) {
         backtrack(nums, target, 0);
         return res;
    }
    public void backtrack(int[] nums, int target, int start){
        if(target < 0){
            return;
        } 
        if(target == 0){
            res++;
            return;
        }          
        for(int i = 0; i < nums.length; i++){
            backtrack(nums, target-nums[i], i);   
        }
    }
}

class Solution {
    public int combinationSum4(int[] nums, int target) {
        if(nums == null || nums.length == 0)
            return 0;
        int[] dp = new int[target+1];
        dp[0] = 1;
        for(int i = 0; i <= target; i++){
            for(int num : nums){
                if(i >= num){
                    dp[i] += dp[i-num];
                }
            }
        }
        return dp[target];
    }
}