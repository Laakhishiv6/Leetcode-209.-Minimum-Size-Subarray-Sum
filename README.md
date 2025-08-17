# Leetcode-209.-Minimum-Size-Subarray-Sum
# Description
Given an array of positive integers nums and a positive integer target, return the minimal length of a subarray whose sum is greater than or equal to target. If there is no such subarray, return 0 instead.

# Solution
In the given problem we have been given an integer array nums with an integer target .We need to calculate the sums of subarrays which is greater than or equal to the target. After calculating the sums we need ot return the length which has the minimal length of subarray.

This question can be done using variable length sliding window technique, which takes a variable sized subarray in a array and treats it as a window and if we have to find more solutions then we need to increase or decrease the sizeof the window accordingly.

Example 1:

Input: target = 7, nums = [2,3,1,2,4,3]

Output: 2

Explanation: The subarray [4,3] has the minimal length under the problem constraint.

Example 2:

Input: target = 4, nums = [1,4,4]

Output: 1

The Intuition:

1. We can initialise 2 pointers left and right and whatever elements are in between these pointers are considered as a window .
2. As we expand the pointer right , the sum increases.And as we increment the left pointer the sum shrinks or decreases.
3. If the sum is greater than or equal to the target , we can shrink left to find a minimal length. And if it is again less than target , then we can increment or expand the right pointer.
# Algorithm
1. Initialise a left pointer as 0 which will be initilially pointing at the 0th index.
2. Also initiliase a variable total intialised as 0 which stores the total of the subarray.
3. Initialise a variable res which stores and returns the minimal length of the subarray which satisfie the condition.Initialise res = float("inf") to represent a very large number (infinity)
4. Use a for loop with pointer right which loops through the array.
5. Add nums[i] in the total and check if the value is greater than or equal to target.
6. If it is greater than or equal to target , then we will shrink the window to find a subarray of less length by subtracting the nums[left] value and incrementing left pointer by 1.
7. After this is done find the minimal length by finding the minimum of the current window length(right-left+1) and the res variable itself
8. Return 0 if the res==float("inf") .
9. Else return the res.
# Code
class Solution:

    def minSubArrayLen(self, target: int, nums: List[int]) -> int:
        l=0
        total=0
        res=float("inf")
        for r in range(len(nums)):
            total+=nums[r]
            while total>=target:
                length_of_total=r-l+1
                res=min(res,length_of_total)
                total-=nums[l]
                l+=1

        if res==float("inf"):
            return 0
        else:
            return res
# Complexity
Time Complexity:

O(n) -> since the window slides through each element in the array atleast twice by right and left pointers  .

Space Complexity:

O(1) -> Variables like res , total , left , right are used which don't occupy much of the memory.No extra data strcutures are used.
