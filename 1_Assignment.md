*****************************DSA Problems**************************

/*Question 1

LEETCODE 3432. Count Partitions with Even Sum Difference
You are given an integer array nums of length n.
A partition is defined as an index i where 0 <= i < n - 1, splitting the array into two non-empty subarrays such that:
Left subarray contains indices [0, i].
Right subarray contains indices [i + 1, n - 1].
Return the number of partitions where the difference between the sum of the left and right subarrays is even.

Example:
Input: nums = [10,10,3,7,6]
Output: 4

Solution:
class Solution {
public:
    int countPartitions(vector<int>& nums) {
        int cnt = 0;
        int n = nums.size();
        int sam=0;
        for(int i=0; i<n-1; i++){
            int sum = 0;
            sam += nums[i];
            for(int j=i+1; j<n; j++){
                 sum+=nums[j];
            }
            if((sam-sum)%2==0){
                cnt++;
            }
        }
        return cnt;
    }
};


/*Question 2

LEETCODE 53. Maximum Subarray
Given an integer array nums, find the 
subarray with the largest sum, and return its sum.

Example:
Input: nums = [-2,1,-3,4,-1,2,1,-5,4]
Output: 6
Explanation: The subarray [4,-1,2,1] has the largest sum 6.

Solution:
class Solution {
public:
//KADANE'S ALGORITHM
    int maxSubArray(vector<int>& nums) {
        int n = nums.size();
        int sum = 0;
        int maxsum = INT_MIN;
        for(int i=0; i<n; i++){
          sum+=nums[i];
          maxsum = max(sum,maxsum);
          if(sum<0){
            sum = 0;
          }
        }
        return maxsum;
    }
};

/*Question 3

LEETCODE 33. Search in Rotated Sorted Array
There is an integer array nums sorted in ascending order (with distinct values).
Prior to being passed to your function, nums is possibly rotated at an unknown pivot index k (1 <= k < nums.length) such that the resulting array is [nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]] (0-indexed). For example, [0,1,2,4,5,6,7] might be rotated at pivot index 3 and become [4,5,6,7,0,1,2].
Given the array nums after the possible rotation and an integer target, return the index of target if it is in nums, or -1 if it is not in nums.
You must write an algorithm with O(log n) runtime complexity.

Example:
Input: nums = [4,5,6,7,0,1,2], target = 0
Output: 4

Solution:
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int n = nums.size();
        int start = 0;
        int end = n-1;
        while(start<=end){
            int mid = start + (end-start)/2;
            if(nums[mid]==target){
                return mid;
            }
            else if(nums[mid]>=nums[start]){
                if(nums[start] <= target && target<= nums[mid]){
                    end = mid;
                }
                else{
                    start = mid+1;
                }
            }
            else{
                if(nums[mid] <= target && target<= nums[end]){
                    start = mid;
                }
                else{
                    end = mid-1;
                }
            }
        }
        return -1;
    }
};



*********************************OOPS Problem********************

LEETCODE 225. Implement Stack using Queues
Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (push, top, pop, and empty).
Implement the MyStack class:
void push(int x) Pushes element x to the top of the stack.
int pop() Removes the element on the top of the stack and returns it.
int top() Returns the element on the top of the stack.
boolean empty() Returns true if the stack is empty, false otherwise.

Example:
Input
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]
Output
[null, null, null, 2, 2, false]

Solution:
class MyStack {
public:
    queue<int>q;
    // constructor of class 
    MyStack() {
        
    }
    
    void push(int x) {
       q.push(x);
       for(int i=0; i<q.size()-1; i++){
        int op = q.front();
        q.pop();
        q.push(op);
       }
    }
    
    int pop() {
        int num = q.front();
        q.pop();
        return num;
    }
    
    int top() {
        return q.front();
    }
    
    bool empty() {
        return q.empty();
    }
};

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack* obj = new MyStack();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->top();
 * bool param_4 = obj->empty();
 */




************************DBMS Problem*****************************

LEETCODE 596. Classes More Than 5 Students
Table: Courses
+-------------+---------+
| Column Name | Type    |
+-------------+---------+
| student     | varchar |
| class       | varchar |
+-------------+---------+
(student, class) is the primary key (combination of columns with unique values) for this table.
Each row of this table indicates the name of a student and the class in which they are enrolled.
Write a solution to find all the classes that have at least five students.
Return the result table in any order.

Example:
Input: 
Courses table:
+---------+----------+
| student | class    |
+---------+----------+
| A       | Math     |
| B       | English  |
| C       | Math     |
| D       | Biology  |
| E       | Math     |
| F       | Computer |
| G       | Math     |
| H       | Math     |
| I       | Math     |
+---------+----------+
Output: 
+---------+
| class   |
+---------+
| Math    |
+---------+

Solution:
# MySQL query statement
SELECT class FROM Courses
group by class
having count(student)>=5








