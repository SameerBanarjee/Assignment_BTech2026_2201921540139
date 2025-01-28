*****************************DSA Problems**************************

/*Question 1

LEETCODE 34. Find First and Last Position of Element in Sorted Array

Given an array of integers nums sorted in non-decreasing order, find the starting and ending position of a given target value. If target is not found in the array, return [-1, -1].
You must write an algorithm with O(log n) runtime complexity.

Example 1:
Input: nums = [5,7,7,8,8,10], target = 8
Output: [3,4]

Solution:
class Solution {
public:
    vector<int> searchRange(vector<int>& nums, int target) {
        vector<int> ans;
        int n = nums.size();
        for(int i=0; i<n; i++){
          if(nums[i]==target){
            ans.push_back(i);
          }
        }

        int sam = ans.size();
        if(sam==1){
            int op = ans[0];
            ans.push_back(op);
        }

        if(sam==0){
            ans.push_back(-1);
            ans.push_back(-1);
        }

        if(sam>2){
            int first = ans[0];
            int last = ans[sam-1];
            ans.clear();
            ans.push_back(first);
            ans.push_back(last);
        }
        return ans;
    }
};

/*Question 2

LEETCODE 48. Rotate Image
You are given an n x n 2D matrix representing an image, rotate the image by 90 degrees (clockwise).
You have to rotate the image in-place, which means you have to modify the input 2D matrix directly. DO NOT allocate another 2D matrix and do the rotation.

Example 1:
Input: matrix = [[1,2,3],[4,5,6],[7,8,9]]
Output: [[7,4,1],[8,5,2],[9,6,3]]

Solution:
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int n = matrix.size();
        vector<int> arr;
        for(int i=0; i<n; i++){
            for(int j=0; j<n; j++){
                arr.push_back(matrix[i][j]);
            }
        }
        for(int i=0; i<n; i++){
            for(int j=0; j<n; j++){
                matrix[i][j] = arr[i+(n-1-j)*n];
            }
        }
      
    }
};


/*Question 3

LEETCODE 21. Merge Two Sorted Lists
You are given the heads of two sorted linked lists list1 and list2.
Merge the two lists into one sorted list. The list should be made by splicing together the nodes of the first two lists.
Return the head of the merged linked list.

Example 1:
Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]

Solution:
class Solution {
    private:
    ListNode* solve(ListNode* list1, ListNode* list2){

     //if only one node is present in first list
   if(list1->next == NULL){
       list1->next = list2;
       return list1;
   }

   ListNode* curr1 = list1;
   ListNode* next1 = curr1->next;
   ListNode* curr2 = list2;
   ListNode* next2 = curr2->next;

   while(next1 != NULL && curr2 != NULL){
       if((curr2->val >= curr1->val) && (curr2->val <= next1->val)){
           curr1->next = curr2;
           next2 = curr2->next;
           curr2->next = next1;
           curr1 = curr2;
           curr2 = next2;
       }
       else{
           // curr1 and next1 ko aage badhao
           curr1 = next1;
           next1 = next1->next;

           if(next1 == NULL){
               curr1 ->next  = curr2;
               return list1;
           }
       }
   }
   return list1;
}
public:
    ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
        if(list1 == NULL){
       return list2;
   }
   if(list2 == NULL){
       return list1;
   }
   
   if(list1->val <= list2->val){
       return solve(list1,list2);
   }
   else{
      return solve(list2,list1);
   }

    }
};


*********************************OOPS Problem********************

LEETCODE 232. Implement Queue using Stacks
Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (push, peek, pop, and empty).
Implement the MyQueue class:
void push(int x) Pushes element x to the back of the queue.
int pop() Removes the element from the front of the queue and returns it.
int peek() Returns the element at the front of the queue.
boolean empty() Returns true if the queue is empty, false otherwise

Input:
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
Output:
[null, null, null, 1, 1, false]

Solution:
class MyQueue {
public:
    stack<int> input,output;
    MyQueue() {
        
    }
    
    void push(int x) {
        input.push(x);
    }
    
    int pop() {
        if(output.empty()){
            while(input.empty()==false){
                output.push(input.top());
                input.pop();
            }
        }
            int data = output.top();
            output.pop();
            return data;
    }
    
    int peek() {
        if(output.empty()){
            while(input.empty()==false){
                output.push(input.top());
                input.pop();
            }  
        }
        return output.top();
    }
    
    bool empty() {
        return input.empty() && output.empty();
    }
};

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue* obj = new MyQueue();
 * obj->push(x);
 * int param_2 = obj->pop();
 * int param_3 = obj->peek();
 * bool param_4 = obj->empty();
 */


************************DBMS Problem*****************************

LEETCODE 586. Customer Placing the Largest Number of Orders
Table: Orders

+-----------------+----------+
| Column Name     | Type     |
+-----------------+----------+
| order_number    | int      |
| customer_number | int      |
+-----------------+----------+
order_number is the primary key (column with unique values) for this table.
This table contains information about the order ID and the customer ID.
Write a solution to find the customer_number for the customer who has placed the largest number of orders.
The test cases are generated so that exactly one customer will have placed more orders than any other customer.
The result format is in the following example

Example 1:

Input: 
Orders table:
+--------------+-----------------+
| order_number | customer_number |
+--------------+-----------------+
| 1            | 1               |
| 2            | 2               |
| 3            | 3               |
| 4            | 3               |
+--------------+-----------------+
Output: 
+-----------------+
| customer_number |
+-----------------+
| 3               |
+-----------------+

Solution:
# MySQL query statement
select customer_number FROM Orders
group by customer_number
order by COUNT(customer_number) desc
Limit 1


