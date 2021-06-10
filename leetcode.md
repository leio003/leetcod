# 1、二分

## 704 二分查找

给定一个 `n` 个元素有序的（升序）整型数组 `nums` 和一个目标值 `target` ，写一个函数搜索 `nums` 中的 `target`，如果目标值存在返回下标，否则返回 `-1`。

```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size();
        

        while(left < right)
        {
            int mid = left + (right - left) / 2;
            if(nums[mid] == target)
            {
                return mid;
            }

            else if(nums[mid] < target)
            {
                left = mid + 1;
            }
            else
            {
                right = mid;
            }

        }
        return -1;

    }
};
```

## 35 搜索插入位置

给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置。

你可以假设数组中无重复元素。

```c++
class Solution {
public:
    int searchInsert(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size();
        int mid;

        while(left < right)
        {
            mid = left + (right - left) / 2;

            if(nums[mid] == target)
            {
                return mid;
            }
            else if(nums[mid] < target)
            {
                left = mid + 1;
            }
            else
            {
                right = mid;
            }

        }
        return left;


    }
};
```

## 34 在排序数组中查找元素的第一个和最后一个位置

给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置。

如果数组中不存在目标值 target，返回 [-1, -1]。

```c++
class Solution {
public:
    int binarySearch(vector<int>& nums, int target, bool lower)
    {
        int left = 0;
        int right = nums.size();
        int ans = nums.size();

        while(left < right)
        {
            int mid = left + (right - left) / 2;
            if(nums[mid] > target || (lower && nums[mid] >= target))
            {
                right = mid;
                ans = mid;
            }
            else
            {
                left = mid + 1;
            }
        }
        return ans;

    }


    vector<int> searchRange(vector<int>& nums, int target) {
        int left = binarySearch(nums, target, true);
        int right = binarySearch(nums, target, false) - 1;

        if(left <= right && left < nums.size() && right < nums.size() && nums[left] == target && nums[right] == target)
        {
            return {left, right};
        }
        else
        {
            return {-1, -1};
        }
    }
};
```

## 69 x 的平方根

实现 int sqrt(int x) 函数。

计算并返回 x 的平方根，其中 x 是非负整数。

由于返回类型是整数，结果只保留整数的部分，小数部分将被舍去。

```c++
class Solution {
public:
    int mySqrt(int x) {
        int left = 0;
        int right = x;

        while(left <= right)
        {
            int mid = left + (right - left) / 2;

            if((long long)mid * mid > x)
            {
                right = mid - 1;
            }
            else if((long long)mid * mid < x)
            {
                left = mid + 1;
            }
            else
            {
                return mid;
            }
        }
        return left - 1;

    }
};
```

## 367 有效的完全平方数

给定一个 正整数 num ，编写一个函数，如果 num 是一个完全平方数，则返回 true ，否则返回 false 。

进阶：不要 使用任何内置的库函数，如  sqrt 。

```c++
class Solution {
public:
    bool isPerfectSquare(int num) {
        int left = 0;
        int right = num;

        while(left <= right)
        {
            int mid = left + (right - left) / 2;

            if((long long)mid * mid < num)
            {
                left = mid + 1;
            }
            else if((long long)mid * mid > num)
            {
                right = mid - 1;
            }
            else
            {
                return true;
            }
        }

        return false;
    }
};
```

# 2、数组

## 27 移除元素

给你一个数组 nums 和一个值 val，你需要 原地 移除所有数值等于 val 的元素，并返回移除后数组的新长度。

不要使用额外的数组空间，你必须仅使用 O(1) 额外空间并 原地 修改输入数组。

元素的顺序可以改变。你不需要考虑数组中超出新长度后面的元素。

```c++
class Solution {
public:
    int removeElement(vector<int>& nums, int val) {
        int left = 0;

        for(int right = 0; right < nums.size(); right++)
        {
            if(nums[right] != val)
            {
                nums[left++] = nums[right];
            }
        }
        return left;
    }
};
```

## 977 有序数组的平方

给你一个按 **非递减顺序** 排序的整数数组 `nums`，返回 **每个数字的平方** 组成的新数组，要求也按 **非递减顺序** 排序。

```c++
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        int left = 0;
        int right = nums.size() - 1;

        vector<int> ans(nums.size());

        int k = nums.size() - 1;

        while(left <= right)
        {
            int numl = nums[left] * nums[left];
            int numr = nums[right] * nums[right];
            if(numl > numr)
            {
                ans[k] = numl;
                left++;
                k--;
            }
            else
            {
                ans[k] = numr;
                right--;
                k--;
            }
        }
        return ans;
    }
};
```

## 209 长度最小的子数组

给定一个含有 n 个正整数的数组和一个正整数 target 。

找出该数组中满足其和 ≥ target 的长度最小的 连续子数组 [numsl, numsl+1, ..., numsr-1, numsr] ，并返回其长度。如果不存在符合条件的子数组，返回 0 。

```c++
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int ans = INT_MAX;
        int left = 0;
        int sub;
        int sum = 0;
        for(int right = 0; right < nums.size(); right++)
        {
            sum += nums[right];

            while(sum >= target)
            {
                sub = right - left + 1;
                ans = ans < sub ? ans : sub;
                sum -= nums[left];
                left++;
            }
        }
        return ans == INT_MAX ? 0 : ans;
    }
};
```

## 59 螺旋矩阵 II

给你一个正整数 `n` ，生成一个包含 `1` 到 `n2` 所有元素，且元素按顺时针顺序螺旋排列的 `n x n` 正方形矩阵 `matrix` 。(不得不说这个题还有点对称美的感觉。)

```c++
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        int flag = 0;
        int cnt = 1;
        vector<vector<int>> ans(n, vector<int>(n));
        while(true)
        {
            for(int i = flag; i < n - 1 - flag; i++)
            {
                ans[flag][i] = cnt;  
                cnt++;
            }
    
            for(int i = flag; i < n - 1 - flag; i++)
            {
                ans[i][n - 1 - flag] = cnt;   
                cnt++;
            }

            for(int i = n - 1 - flag; i >= flag + 1; i--)
            {
                ans[n - 1 - flag][i] = cnt;
                cnt++;
            }

            for(int i = n - 1 - flag; i >= flag + 1; i--)
            {
                ans[i][flag] = cnt;
                cnt++;
            }

            flag++;
            if(cnt >= n * n) break;
        }
        
        if (n % 2 == 1)
            ans[n/2][n/2] = cnt;

        return ans;
    }
};
```

## 54 螺旋矩阵

给你一个 `m` 行 `n` 列的矩阵 `matrix` ，请按照 **顺时针螺旋顺序** ，返回矩阵中的所有元素。

```c++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        int flag = 0;
        int k = 0;
        int m = matrix.size();
        int n = matrix[0].size();

        vector<int> ans;

        while(true)
        {
            for(int i = flag; i < n - 1 - flag && k < m*n; i++)
            {
                ans.push_back(matrix[flag][i]);
                k++;
            }

            for(int i = flag; i < m - 1 - flag && k < m*n; i++)
            {
                ans.push_back(matrix[i][n - 1 - flag]);
                k++;
            }

            for(int i = n - 1 - flag; i >= flag + 1 && k < m*n; i--)
            {
                ans.push_back(matrix[m - 1 - flag][i]);
                k++;
            }

            for(int i = m - 1 - flag; i >= flag + 1 && k < m*n; i--)
            {
                ans.push_back(matrix[i][flag]);
                k++;
            }

            flag++;

            if(k >= m*n) break;

            if((m == n) && (m % 2 == 1) && (k >= m * n - 1))
            {
                ans.push_back(matrix[m/2][m/2]);
                break;
            }

        }
        return ans;
    }
};
```

## 剑指 Offer 29 顺时针打印矩阵

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。与上一个题一模一样，但测试样例不同，上题没有考虑为空的状态。

```c++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        if(matrix.size() == 0 || matrix[0].size() == 0) return {};
        int flag = 0;
        int k = 0;
        int m = matrix.size();
        int n = matrix[0].size();    
        vector<int> ans;
        while(true)
        {
            for(int i = flag; i < n - 1 - flag && k < m*n; i++)
            {
                ans.push_back(matrix[flag][i]);
                k++;
            }

            for(int i = flag; i < m - 1 - flag && k < m*n; i++)
            {
                ans.push_back(matrix[i][n - 1 - flag]);
                k++;
            }

            for(int i = n - 1 - flag; i >= flag + 1 && k < m*n; i--)
            {
                ans.push_back(matrix[m - 1 - flag][i]);
                k++;
            }

            for(int i = m - 1 - flag; i >= flag + 1 && k < m*n; i--)
            {
                ans.push_back(matrix[i][flag]);
                k++;
            }

            flag++;

            if(k >= m * n) break;

            if((m == n) && (m % 2 == 1) && (k >= m * n -1))
            {
                ans.push_back(matrix[m/2][m/2]);
                break;
            }
        }

        return ans;
    }
};
```

## 203 移除链表元素

给你一个链表的头节点 `head` 和一个整数 `val` ，请你删除链表中所有满足 `Node.val == val` 的节点，并返回 **新的头节点** 。（应该注意删除后，不用跳下一步）。

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode* dummy = new ListNode(0);
        dummy->next = head;
        ListNode* cur = dummy;

        while(cur->next)
        {
            if(cur->next->val == val)
            {
                ListNode* tmp = cur->next;
                cur->next = cur->next->next;
                delete tmp;
            }
            else //else 不可少
                cur = cur->next;
        }

        return dummy->next;
    }
};
```

## 707 设计链表

设计链表的实现。您可以选择使用单链表或双链表。单链表中的节点应该具有两个属性：val 和 next。val 是当前节点的值，next 是指向下一个节点的指针/引用。如果要使用双向链表，则还需要一个属性 prev 以指示链表中的上一个节点。假设链表中的所有节点都是 0-index 的。

在链表类中实现这些功能：

get(index)：获取链表中第 index 个节点的值。如果索引无效，则返回-1。
addAtHead(val)：在链表的第一个元素之前添加一个值为 val 的节点。插入后，新节点将成为链表的第一个节点。
addAtTail(val)：将值为 val 的节点追加到链表的最后一个元素。
addAtIndex(index,val)：在链表中的第 index 个节点之前添加值为 val  的节点。如果 index 等于链表的长度，则该节点将附加到链表的末尾。如果 index 大于链表长度，则不会插入节点。如果index小于0，则在头部插入节点。
deleteAtIndex(index)：如果索引 index 有效，则删除链表中的第 index 个节点。

```c++
class MyLinkedList {
public:
    struct LinkedNode {
        int val;
        LinkedNode* next;
        LinkedNode(int val):val(val), next(nullptr){}
    };
    /** Initialize your data structure here. */
    MyLinkedList() {
        dummy = new LinkedNode(0);
        size = 0;
    }
    
    /** Get the value of the index-th node in the linked list. If the index is invalid, return -1. */
    int get(int index) {
        if(index >= size)
        {
            return -1;
        }
        LinkedNode* cur = dummy->next;
        while(index--)
        {
            cur = cur->next;
        }
        return cur->val;
    }
    
    /** Add a node of value val before the first element of the linked list. After the insertion, the new node will be the first node of the linked list. */
    void addAtHead(int val) {
        LinkedNode* node = new LinkedNode(val);
        node->next = dummy->next;
        dummy->next = node;
        size++;
    }
    
    /** Append a node of value val to the last element of the linked list. */
    void addAtTail(int val) {
        LinkedNode* cur = dummy;
        while(cur->next)
        {
            cur = cur->next;
        }

        LinkedNode* node = new LinkedNode(val);
        cur->next = node;
        size++;
    }
    
    /** Add a node of value val before the index-th node in the linked list. If index equals to the length of linked list, the node will be appended to the end of linked list. If index is greater than the length, the node will not be inserted. */
    void addAtIndex(int index, int val) {
        if(index == size) addAtTail(val);
        else if(index < 0) addAtHead(val);
        else if(index > size) return ;
        else
        {
            LinkedNode* node = new LinkedNode(val);
            LinkedNode* cur = dummy;
            while(index--)
            {
                cur = cur->next;
            }
            node->next = cur->next;
            cur->next = node;
            size++;
        }
    }
    
    /** Delete the index-th node in the linked list, if the index is valid. */
    void deleteAtIndex(int index) {
        if(index < 0) return ;
        else if(index >= size) return ;
        else
        {
            LinkedNode* cur = dummy;
            while(index--)
            {
                cur = cur->next;
            }
            LinkedNode* tmp = cur->next;
            cur->next = cur->next->next;
            delete tmp;
            size--;
        }
    }

private:
    LinkedNode* dummy;
    int size;
};

/**
 * Your MyLinkedList object will be instantiated and called as such:
 * MyLinkedList* obj = new MyLinkedList();
 * int param_1 = obj->get(index);
 * obj->addAtHead(val);
 * obj->addAtTail(val);
 * obj->addAtIndex(index,val);
 * obj->deleteAtIndex(index);
 */
```

