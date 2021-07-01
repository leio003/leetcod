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

# 3、链表

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

## 206 反转链表

给你单链表的头节点 `head` ，请你反转链表，并返回反转后的链表。（注意返回值）

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
    ListNode* reverseList(ListNode* head) {
        ListNode* p = nullptr;
        ListNode* q = head;

        while(q)
        {
            ListNode* tmp = q->next;
            q->next = p;
            p = q;
            q = tmp;
        }
        return p;
    }
};
```

## 24 两两交换链表中的节点

给定一个链表，两两交换其中相邻的节点，并返回交换后的链表。

**你不能只是单纯的改变节点内部的值**，而是需要实际的进行节点交换。(注意判断条件)

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
    ListNode* swapPairs(ListNode* head) {
        ListNode* dummy = new ListNode(0);
        ListNode* pre = dummy;
        dummy->next = head;
        ListNode* cur = head;
        while(pre->next && pre->next->next)
        {
            pre->next = cur->next;
            cur->next = pre->next->next;
            pre->next->next = cur;
            pre = cur;
            cur = cur->next;
        } 
        return dummy->next;
    }
};
```

## 19 删除链表的倒数第 N 个结点

给你一个链表，删除链表的倒数第 `n` 个结点，并且返回链表的头结点。

**进阶：**你能尝试使用一趟扫描实现吗？

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
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dummy = new ListNode(0);
        dummy->next = head;
        ListNode* fast = head;
        ListNode* pre = dummy;

        while(n--)
        {
            fast = fast->next;
        }

        while(fast)
        {
            fast = fast->next;
            pre = pre->next;
        }
        ListNode* tmp = pre->next;
        pre->next = pre->next->next;
        delete tmp;

        return dummy->next;
    }
};
```

## 面试题 02.07 链表相交

给定两个（单向）链表，判定它们是否相交并返回交点。请注意相交的定义基于节点的引用，而不是基于节点的值。换句话说，如果一个链表的第k个节点与另一个链表的第j个节点是同一节点（引用完全相同），则这两个链表相交。(a+b+c，但需要注意特殊边界与不相交情况)

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if(headA == NULL || headB == NULL) return NULL;
        ListNode* pa = headA;
        ListNode* pb = headB;
        int flag = 0;
        while(true)
        {
            if(pa == pb) break;

            pa = pa->next;
            pb = pb->next;
            if(pa == NULL)
            {
                pa = headB;
                flag++;
            } 
            if(pb == NULL)
            {
                pb = headA;
                flag++;
            } 
            if(flag > 2) return NULL;
        }
        return pa;
    }
};
```

## 142 环形链表 II

给定一个链表，返回链表开始入环的第一个节点。 如果链表无环，则返回 null。

为了表示给定链表中的环，我们使用整数 pos 来表示链表尾连接到链表中的位置（索引从 0 开始）。 如果 pos 是 -1，则在该链表中没有环。注意，pos 仅仅是用于标识环的情况，并不会作为参数传递到函数中。

说明：不允许修改给定的链表。

进阶：

你是否可以使用 O(1) 空间解决此题？

首先明确双指针，一快一慢，设进环之前长度为a，进环到相遇位置长度b，剩下的环长度为c。慢指针a+b，快指针a+n*(b+c)+b，另外快指针走过的路的长度是慢指针的两倍可得：2*[a+b] = a+n*(b+c)+b， a = (n-1)*b + n*c.

```c++
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* slow = head;
        ListNode* fast = head;

        while(fast && fast->next)
        {
            slow = slow->next;
            fast = fast->next->next;

            if(slow == fast)
            {
                ListNode* pa = fast;
                ListNode* pb = head;
                while(pa != pb)
                {
                    pa = pa->next;
                    pb = pb->next;
                }
                return pa;
            }
        }
        return NULL;
    }
};
```

# 4、哈希

## 242 有效的字母异位词

给定两个字符串 *s* 和 *t* ，编写一个函数来判断 *t* 是否是 *s* 的字母异位词。

```c++
class Solution {
public:
    bool isAnagram(string s, string t) {
        int tmp[27] = {0};
        if(s.size() != t.size()) return false;

        for(int i = 0; i < s.size(); i++)
        {
            tmp[s[i] - 'a']++;
            tmp[t[i] - 'a']--;
        }

        for(int i = 0; i < 27; i++)
        {
            if(tmp[i] != 0) return false;
        }
        return true;
    }
};
```

## 349 两个数组的交集

给定两个数组，编写一个函数来计算它们的交集。(当元素数量未知的时候，set比数组靠谱)

```c++
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> set(nums1.begin(), nums1.end());
        unordered_set<int> ans;
        for(int i = 0; i < nums2.size(); i++)
        {
            if(set.find(nums2[i]) != set.end())
            {
                ans.insert(nums2[i]);
            }
        }
        return vector<int>(ans.begin(), ans.end());
    }
};
```

## 350 两个数组的交集 II

给定两个数组，编写一个函数来计算它们的交集。

- 输出结果中每个元素出现的次数，应与元素在两个数组中出现次数的最小值一致。

- 我们可以不考虑输出结果的顺序。

  与上题不同点在于，重复的值也有需要根据次数来决定，因此需要map记录次数。

  ```c++
  class Solution {
  public:
      vector<int> intersect(vector<int>& nums1, vector<int>& nums2) {
          unordered_map<int, int> map;
          vector<int> ans;
          for(int i = 0; i < nums1.size(); i++)
          {
              map[nums1[i]]++;
          }
  
          for(int i = 0; i < nums2.size(); i++)
          {
              if(map.find(nums2[i]) != map.end() && map[nums2[i]] != 0)
              {
                  ans.push_back(nums2[i]);
                  map[nums2[i]]--;
              }
          }
          return ans;
      }
  };
  ```

  

## 202 快乐数

编写一个算法来判断一个数 n 是不是快乐数。

「快乐数」定义为：

对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和。
然后重复这个过程直到这个数变为 1，也可能是 无限循环 但始终变不到 1。
如果 可以变为  1，那么这个数就是快乐数。
如果 n 是快乐数就返回 true ；不是，则返回 false 。

```c++
class Solution {
public:
    bool isHappy(int n) {
        unordered_set<int> set;
        int sum = 0;
        while(n != 1)
        {
            while(n)
            {
                sum += (n % 10) * (n % 10);
                n = n / 10;
            }
            if(set.find(sum) != set.end()) return false;
            set.insert(sum);
            n = sum;
            sum = 0;
        }
        return true;
    }
};
```

## 1 两数之和

给定一个整数数组 nums 和一个整数目标值 target，请你在该数组中找出 和为目标值 target  的那 两个 整数，并返回它们的数组下标。

你可以假设每种输入只会对应一个答案。但是，数组中同一个元素在答案里不能重复出现。

你可以按任意顺序返回答案。

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        unordered_map<int, int> map;

        for(int i = 0; i < nums.size(); i++)
        {
            auto iter = map.find(target - nums[i]);
            if(iter != map.end())
            {
                return {iter->second, i};
            }
            map.insert(pair<int, int>(nums[i], i));
        }

        return {};
    }
};
```

## 454 四数相加 II

给定四个包含整数的数组列表 A , B , C , D ,计算有多少个元组 (i, j, k, l) ，使得 A[i] + B[j] + C[k] + D[l] = 0。

为了使问题简单化，所有的 A, B, C, D 具有相同的长度 N，且 0 ≤ N ≤ 500 。所有整数的范围在 -228 到 228 - 1 之间，最终结果不会超过 231 - 1 。

```c++
class Solution {
public:
    int fourSumCount(vector<int>& nums1, vector<int>& nums2, vector<int>& nums3, vector<int>& nums4) {
        unordered_map<int, int> map;

        for(int i = 0; i < nums1.size(); i++)
        {
            for(int j = 0; j < nums2.size(); j++)
            {
                map[nums1[i] + nums2[j]]++;
            }
        }

        int ans = 0;
        for(int i = 0; i < nums3.size(); i++)
        {
            for(int j = 0; j < nums4.size(); j++)
            {
                if(map.find(-(nums3[i] + nums4[j])) != map.end())
                {
                    ans += map[-(nums3[i] + nums4[j])];
                }
            }
        }
        return ans;
    }
};
```

## 383 赎金信

给定一个赎金信 (ransom) 字符串和一个杂志(magazine)字符串，判断第一个字符串 ransom 能不能由第二个字符串 magazines 里面的字符构成。如果可以构成，返回 true ；否则返回 false。

(题目说明：为了不暴露赎金信字迹，要从杂志上搜索各个需要的字母，组成单词来表达意思。杂志字符串中的每个字符只能在赎金信字符串中使用一次。)

```c++
class Solution {
public:
    bool canConstruct(string ransomNote, string magazine) {
        int tmp[27] = {0};

        for(int i = 0; i < magazine.size(); i++)
        {
            tmp[magazine[i] - 'a']++;
        }

        for(int i = 0; i < ransomNote.size(); i++)
        {
            tmp[ransomNote[i] - 'a']--;
            if(tmp[ransomNote[i] - 'a'] < 0) return false;
        }

      
        return true;
    }
};
```

## 15 三数之和

给你一个包含 n 个整数的数组 nums，判断 nums 中是否存在三个元素 a，b，c ，使得 a + b + c = 0 ？请你找出所有和为 0 且不重复的三元组。

注意：答案中不可以包含重复的三元组。

```
class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        vector<vector<int>> ans;
        sort(nums.begin(), nums.end());

        for(int i = 0; i < nums.size(); i++)
        {
            if(nums[i] > 0) return ans;

            if(i > 0 && nums[i] == nums[i - 1]) continue;

            int left = i + 1;
            int right = nums.size() - 1;

            while(right > left)
            {
                if(nums[i] + nums[left] + nums[right] > 0) right--;
                else if(nums[i] + nums[left] + nums[right] < 0) left++;
                else
                {
                    ans.push_back({nums[i], nums[left], nums[right]});
                    while(right > left && nums[right] == nums[right - 1]) right--;
                    while(right > left && nums[left] == nums[left + 1]) left++;

                    right--;
                    left++;
                }

            }
        }
        return ans;
        
    }
};
```

## 18 四数之和

给定一个包含 n 个整数的数组 nums 和一个目标值 target，判断 nums 中是否存在四个元素 a，b，c 和 d ，使得 a + b + c + d 的值与 target 相等？找出所有满足条件且不重复的四元组。

注意：答案中不可以包含重复的四元组。

```c++
class Solution {
public:
    vector<vector<int>> fourSum(vector<int>& nums, int target) {
        vector<vector<int>> ans;
        sort(nums.begin(), nums.end());
        for(int k = 0; k < nums.size(); k++)
        {
            if(k > 0 && nums[k] == nums[k - 1])
                continue;

            for(int i = k + 1; i < nums.size(); i++)
            {
                if(i > k + 1 && nums[i] == nums[i - 1])
                    continue;

                int left = i + 1;
                int right = nums.size() - 1;
                while(right > left)
                {
                    if((nums[k] + nums[i] + nums[left] + nums[right]) > target) right--;
                    else if((nums[k] + nums[i] + nums[left] + nums[right]) < target) left++;
                    else
                    {
                        ans.push_back({nums[k], nums[i], nums[left], nums[right]});
                        while(right > left && nums[left] == nums[left + 1]) left++;
                        while(right > left && nums[right] == nums[right - 1]) right--;

                        left++;
                        right--;
                    }
                }
            }
        }

        return ans;
    }
};
```

# 5、其他

## 剑指 Offer 05 替换空格

请实现一个函数，把字符串 `s` 中的每个空格替换成"%20"。

```c++
class Solution {
public:
    string replaceSpace(string s) {
        int cnt = 0;
        for(int i = 0; i < s.size(); i++)
        {
            if(s[i] == ' ') cnt++;
        }
        int old_size = s.size() - 1;
        s.resize(s.size() + cnt * 2);

        for(int i = old_size, j = s.size() - 1; i >= 0 && j >= 0; i--)
        {
            if(s[i] == ' ')
            {
                s[j--] = '0';
                s[j--] = '2';
                s[j--] = '%';
            }
            else
            {
                s[j] = s[i];
                j--;
            }
        }
        return s;
    }
};
```

## 151 翻转字符串里的单词

给你一个字符串 s ，逐个翻转字符串中的所有 单词 。

单词 是由非空格字符组成的字符串。s 中使用至少一个空格将字符串中的 单词 分隔开。

请你返回一个翻转 s 中单词顺序并用单个空格相连的字符串。

说明：

输入字符串 s 可以在前面、后面或者单词间包含多余的空格。
翻转后单词间应当仅用一个空格分隔。
翻转后的字符串中不应包含额外的空格。

```c++
class Solution {
public:
    string reverseWords(string s) {
        stack<string> st;
        string res, tmp;
        istringstream ss(s);

        while(ss >> tmp)
        {
            st.push(tmp);
            st.push(" ");
        }

        if(!st.empty()) st.pop();

        while(!st.empty())
        {
            res += st.top();
            st.pop();
        }

        return res;
    }
};
```

## 剑指 Offer 09 用两个栈实现队列

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

```c++
class CQueue {
public:
    stack<int> In;
    stack<int> Out;
    CQueue() {

    }
    
    void appendTail(int value) {
        if(Out.empty()) In.push(value);
        else
        {
            while(!Out.empty())
            {
                In.push(Out.top());
                Out.pop();
            }
            In.push(value);
        }
        return;
    }
    
    int deleteHead() {

        if(Out.empty() && !In.empty())
        {
            while(!In.empty())
            {
                Out.push(In.top());
                In.pop();
            }
        }
        else if(Out.empty() && In.empty()) return -1;

        int ans = Out.top();
        Out.pop();

        return ans;
    }
};

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue* obj = new CQueue();
 * obj->appendTail(value);
 * int param_2 = obj->deleteHead();
 */
```

# 6、树

## 144 二叉树的前序遍历

给你二叉树的根节点 `root` ，返回它节点值的 **前序** 遍历。（包括递归非递归）。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    // void preorder(TreeNode* node, vector<int>& res)
    // {
    //     if(node == nullptr) return;
    //     res.push_back(node->val);
    //     preorder(node->left, res);
    //     preorder(node->right, res);
    // }

    vector<int> preorderTraversal(TreeNode* root) {
        // vector<int> ans;
        // preorder(root, ans);
        // return ans;

        stack<TreeNode*> st;
        vector<int> ans;
        if(root) st.push(root);
        while(!st.empty())
        {
            TreeNode* node = st.top();
            st.pop();

            ans.push_back(node->val);
            if(node->right) st.push(node->right);
            if(node->left) st.push(node->left);
            
        }

        return ans;

    }
};
```

## 94 二叉树的中序遍历

给定一个二叉树的根节点 `root` ，返回它的 **中序** 遍历。

 

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    // void inorder(TreeNode* node, vector<int>& res)
    // {
    //     if(node == nullptr) return;
    //     inorder(node->left, res);
    //     res.push_back(node->val);
    //     inorder(node->right, res);
    // }
    vector<int> inorderTraversal(TreeNode* root) {
        // vector<int> ans;
        // inorder(root, ans);
        // return ans;
        stack<TreeNode*> st;
        vector<int> ans;
        TreeNode* node = root;
        while(node != nullptr || !st.empty())
        {
            if(node != nullptr)
            {
                st.push(node);
                node = node->left;
            }
            else
            {
                node = st.top();
                st.pop();
                ans.push_back(node->val);
                node = node->right;
            }

        }
        return ans;

    }
};
```

## 145 二叉树的后序遍历

给定一个二叉树，返回它的 *后序* 遍历。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    // void postorder(TreeNode* node, vector<int>& res)
    // {
    //     if(node == nullptr) return ;
    //     postorder(node->left, res);
    //     postorder(node->right, res);
    //     res.push_back(node->val);
    // }

    vector<int> postorderTraversal(TreeNode* root) {
        // vector<int> ans;
        // postorder(root, ans);
        // return ans;
        stack<TreeNode*> st;
        vector<int> ans;
        if(root) st.push(root);

        while(!st.empty())
        {
            TreeNode* node = st.top();
            st.pop();
            ans.push_back(node->val);

            if(node->left) st.push(node->left);
            if(node->right) st.push(node->right);
        }

        reverse(ans.begin(), ans.end());
        return ans;
    }
};
```

## 102 二叉树的层序遍历

给你一个二叉树，请你返回其按 **层序遍历** 得到的节点值。 （即逐层地，从左到右访问所有节点）。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        queue<TreeNode*> que;
        vector<vector<int>> ans;
        if(root) que.push(root);

        while(!que.empty())
        {
            int size = que.size();
            vector<int> min_ans;
            for(int i = 0; i < size; i++)
            {
                TreeNode* node = que.front();
                que.pop();
                min_ans.push_back(node->val);
                if(node->left) que.push(node->left);
                if(node->right) que.push(node->right);
            }

            ans.push_back(min_ans);
        }
        return ans;
    }
};
```

## 107 二叉树的层序遍历 II

给定一个二叉树，返回其节点值自底向上的层序遍历。 （即按从叶子节点所在层到根节点所在的层，逐层从左向右遍历）

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> levelOrderBottom(TreeNode* root) {
        queue<TreeNode*> que;
        vector<vector<int>> ans;

        if(root) que.push(root);

        while(!que.empty())
        {
            int size = que.size();
            vector<int> min_ans;
            for(int i = 0; i < size; i++)
            {
                TreeNode* node = que.front();
                que.pop();
                min_ans.push_back(node->val);
                if(node->left) que.push(node->left);
                if(node->right) que.push(node->right);
            }
            ans.push_back(min_ans);
        }
        reverse(ans.begin(), ans.end());
        return ans;
    }
};
```

## 199  二叉树的右视图

给定一棵二叉树，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
        queue<TreeNode*> que;
        vector<int> ans;
        if(root) que.push(root);

        while(!que.empty())
        {
            int size = que.size();

            for(int i = 0; i < size; i++)
            {
                TreeNode* node = que.front();
                que.pop();
                if(node->left) que.push(node->left);
                if(node->right) que.push(node->right);
                if(i == (size - 1))
                {
                    ans.push_back(node->val);
                }
            }
        }
        return ans;
    }
};
```

## 637 二叉树的层平均值

给定一个非空二叉树, 返回一个由每层节点平均值组成的数组。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<double> averageOfLevels(TreeNode* root) {
        queue<TreeNode*> que;
        vector<double> ans;

        if(root) que.push(root);
        while(!que.empty())
        {
            int size = que.size();
            long long sum = 0;
            for(int i = 0; i < size; i++)
            {
                TreeNode* node = que.front();
                que.pop();
                sum += node->val;
                if(node->left) que.push(node->left);
                if(node->right) que.push(node->right);
            }
            ans.push_back(1.0 * sum / size);
        }
        return ans;
    }
};
```

## 429 [N 叉树的层序遍历](https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal/)

给定一个 N 叉树，返回其节点值的*层序遍历*。（即从左到右，逐层遍历）。

树的序列化输入是用层序遍历，每组子节点都由 null 值分隔（参见示例）。

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    vector<Node*> children;

    Node() {}

    Node(int _val) {
        val = _val;
    }

    Node(int _val, vector<Node*> _children) {
        val = _val;
        children = _children;
    }
};
*/

class Solution {
public:
    vector<vector<int>> levelOrder(Node* root) {
        queue<Node*> que;
        vector<vector<int>> ans;

        if(root) que.push(root);
        while(!que.empty())
        {
            int size = que.size();
            vector<int> min_ans;

            for(int i = 0; i < size; i++)
            {
                Node* node = que.front();
                que.pop();
                min_ans.push_back(node->val);
                for(auto child : node->children)
                {
                    que.push(child);
                }
            }
            ans.push_back(min_ans);
        }

        return ans;
    }
};
```

## 515 [在每个树行中找最大值](https://leetcode-cn.com/problems/find-largest-value-in-each-tree-row/)

您需要在二叉树的每一行中找到最大的值。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<int> largestValues(TreeNode* root) {
        queue<TreeNode*> que;
        vector<int> ans;

        if(root) que.push(root);
        while(!que.empty())
        {
            int size = que.size();
            int max_num = INT_MIN;
            for(int i = 0; i < size; i++)
            {
                TreeNode* node = que.front();
                que.pop();
                max_num = max(max_num, node->val);
                if(node->left) que.push(node->left);
                if(node->right) que.push(node->right);
            }
            ans.push_back(max_num);
        }
        return ans;
    }
};
```

## 116 [填充每个节点的下一个右侧节点指针](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node/)

给定一个 完美二叉树 ，其所有叶子节点都在同一层，每个父节点都有两个子节点。二叉树定义如下：

struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
填充它的每个 next 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 next 指针设置为 NULL。

初始状态下，所有 next 指针都被设置为 NULL。

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* next;

    Node() : val(0), left(NULL), right(NULL), next(NULL) {}

    Node(int _val) : val(_val), left(NULL), right(NULL), next(NULL) {}

    Node(int _val, Node* _left, Node* _right, Node* _next)
        : val(_val), left(_left), right(_right), next(_next) {}
};
*/

class Solution {
public:
    Node* connect(Node* root) {
        queue<Node*> que;
        if(root) que.push(root);

        while(!que.empty())
        {
            int size = que.size();
            for(int i = 0; i < size; i++)
            {
                Node* node = que.front();
                que.pop();
                if(node->left) que.push(node->left);
                if(node->right) que.push(node->right);
                if(i == (size - 1))
                {
                    node->next = NULL;
                }
                else
                {
                    node->next = que.front();
                }
            }
        }
        return root;
    }
};
```

## 117 [填充每个节点的下一个右侧节点指针 II](https://leetcode-cn.com/problems/populating-next-right-pointers-in-each-node-ii/)

给定一个二叉树

struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
填充它的每个 next 指针，让这个指针指向其下一个右侧节点。如果找不到下一个右侧节点，则将 next 指针设置为 NULL。

初始状态下，所有 next 指针都被设置为 NULL。

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* next;

    Node() : val(0), left(NULL), right(NULL), next(NULL) {}

    Node(int _val) : val(_val), left(NULL), right(NULL), next(NULL) {}

    Node(int _val, Node* _left, Node* _right, Node* _next)
        : val(_val), left(_left), right(_right), next(_next) {}
};
*/

class Solution {
public:
    Node* connect(Node* root) {
        queue<Node*> que;
        if(root) que.push(root);

        while(!que.empty())
        {
            int size = que.size();
            for(int i = 0; i < size; i++)
            {
                Node* node = que.front();
                que.pop();
                if(node->left) que.push(node->left);
                if(node->right) que.push(node->right);

                if(i == (size - 1)) node->next = NULL;
                else
                {
                    node->next = que.front();
                }
            }

        }
        return root;
    }
};
```

## 226 [ 翻转二叉树](https://leetcode-cn.com/problems/invert-binary-tree/)

翻转一棵二叉树。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    // void preorder(TreeNode* node)
    // {
    //     if(node == nullptr) return;
    //     swap(node->left, node->right);
    //     preorder(node->left);
    //     preorder(node->right);
    // }

    // void inorder(TreeNode* node)
    // {
    //     if(node == nullptr) return;
    //     inorder(node->left);
    //     swap(node->left, node->right);
    //     inorder(node->left);
    // }

    // void postorder(TreeNode* node)
    // {
    //     if(node == nullptr) return;
    //     postorder(node->left);
    //     postorder(node->right);
    //     swap(node->left, node->right);
    // }

    TreeNode* invertTree(TreeNode* root) {
        // preorder(root);
        // inorder(root);
        // postorder(root);
        // return root;

        stack<TreeNode*> st;
        if(root) st.push(root);

        while(!st.empty())
        {
            TreeNode* node = st.top();
            st.pop();
            swap(node->left, node->right);
            if(node->right) st.push(node->right);
            if(node->left) st.push(node->left);
        }

        return root;

    }
};
```

## 101 [对称二叉树](https://leetcode-cn.com/problems/symmetric-tree/)

给定一个二叉树，检查它是否是镜像对称的。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    bool preorder(TreeNode* left, TreeNode* right)
    {
        if(left == nullptr && right == nullptr) return true;
        else if(left == nullptr || right == nullptr) return false;
        else if(left->val != right->val) return false;
        else
        {
            return preorder(left->left, right->right) && preorder(left->right, right->left);
        } 
    }

    bool isSymmetric(TreeNode* root) {
        if(root == nullptr) return true;

        return preorder(root->left, root->right);
    }   
};
```

## 104 [ 二叉树的最大深度](https://leetcode-cn.com/problems/maximum-depth-of-binary-tree/)

给定一个二叉树，找出其最大深度。

二叉树的深度为根节点到最远叶子节点的最长路径上的节点数。

**说明:** 叶子节点是指没有子节点的节点。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int getDepth(TreeNode* node)
    {
        if(node == nullptr) return 0;

        int left = getDepth(node->left);
        int right = getDepth(node->right);
        return max(left, right) + 1;
    }


    int maxDepth(TreeNode* root) {
        // queue<TreeNode*> que;
        // int ans = 0;
        // if(root) que.push(root);

        // while(!que.empty())
        // {
        //     int size = que.size();
        //     ans++;
        //     for(int i = 0; i < size; i++)
        //     {
        //         TreeNode* node = que.front();
        //         que.pop();

        //         if(node->left) que.push(node->left);
        //         if(node->right) que.push(node->right);
        //     }
        // }

        // return ans;

        return getDepth(root);
    }
};
```

## 111 [二叉树的最小深度](https://leetcode-cn.com/problems/minimum-depth-of-binary-tree/)

给定一个二叉树，找出其最小深度。

最小深度是从根节点到最近叶子节点的最短路径上的节点数量。

**说明：**叶子节点是指没有子节点的节点。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    // int getDepth(TreeNode* node)
    // {
    //     if(node == nullptr) return 0;
    //     if(node->left == nullptr && node->right == nullptr) return 1;
    //     else if(node->left == nullptr)
    //     {
    //         return getDepth(node->right) + 1;
    //     }
    //     else if(node->right == nullptr)
    //     {
    //         return getDepth(node->left) + 1;
    //     }
    //     else
    //     {
    //         return min(getDepth(node->left), getDepth(node->right)) + 1;
    //     }
    // }

    int minDepth(TreeNode* root) {
        // return getDepth(root);
        queue<TreeNode*> que;
        int ans = 0;
        if(root) que.push(root);
        while(!que.empty())
        {
            int size = que.size();
            ans++;

            for(int i = 0; i < size; i++)
            {
                TreeNode* node = que.front();
                que.pop();
                if(node->left == nullptr && node->right == nullptr) return ans;

                if(node->left) que.push(node->left);
                if(node->right) que.push(node->right);
            }

        }
        return ans;

    }
};
```

## 222 [完全二叉树的节点个数](https://leetcode-cn.com/problems/count-complete-tree-nodes/)

给你一棵 完全二叉树 的根节点 root ，求出该树的节点个数。

完全二叉树 的定义如下：在完全二叉树中，除了最底层节点可能没填满外，其余每层节点数都达到最大值，并且最下面一层的节点都集中在该层最左边的若干位置。若最底层为第 h 层，则该层包含 1~ 2h 个节点。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    // int getNum(TreeNode* node)
    // {
    //     if(node == nullptr) return 0;
    //     return getNum(node->left) + getNum(node->right) + 1;
    // }

    int countNodes(TreeNode* root) {
        // return getNum(root);
        queue<TreeNode*> que;
        int ans = 0;
        if(root) que.push(root);

        while(!que.empty())
        {
            int size = que.size();
            ans += size;
            for(int i = 0; i < size; i++)
            {
                TreeNode* node = que.front();
                que.pop();
                if(node->left) que.push(node->left);
                if(node->right) que.push(node->right);
            }
        }
        return ans;
    }
};
```

## 110 [平衡二叉树](https://leetcode-cn.com/problems/balanced-binary-tree/)

给定一个二叉树，判断它是否是高度平衡的二叉树。

本题中，一棵高度平衡二叉树定义为：

> 一个二叉树*每个节点* 的左右两个子树的高度差的绝对值不超过 1 。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    // int getDepth(TreeNode* node)
    // {
    //     if(node == nullptr) return 0;

    //     return max(getDepth(node->left), getDepth(node->right)) + 1;
    // }

    int getDepth(TreeNode* node)
    {
        if(node == nullptr) return 0;
        int left = getDepth(node->left);
        if(left == -1) return -1;
        int right = getDepth(node->right);
        if(right == -1) return -1;
        return abs(left - right) <= 1 ? max(left, right) + 1 : -1;
    }

    bool isBalanced(TreeNode* root) {
        // if(root == nullptr) return true;
        // int left = getDepth(root->left);
        // int right = getDepth(root->right);
        // bool ans = abs(left - right) <= 1 ? true : false;

        // return ans && isBalanced(root->left) & isBalanced(root->right);
        return getDepth(root) == -1 ? false : true;
        
    }
};
```

## 257 [二叉树的所有路径](https://leetcode-cn.com/problems/binary-tree-paths/)

给定一个二叉树，返回所有从根节点到叶子节点的路径。

**说明:** 叶子节点是指没有子节点的节点。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    // vector<string> ans;
    // vector<int> min_s;

    // void backtracking(TreeNode* node)
    // {
    //     if(node->left == nullptr && node->right == nullptr)
    //     {
    //         min_s.push_back(node->val);
    //         string s = "";
    //         for(int i = 0; i < min_s.size() - 1; i++)
    //         {
    //             s += to_string(min_s[i]);
    //             s += "->";
    //         }
    //         s += to_string(min_s[min_s.size() - 1]);
    //         ans.push_back(s);
    //         return ;
    //     }
    //     min_s.push_back(node->val);
    //     if(node->left)
    //     {
    //         backtracking(node->left);
    //         min_s.pop_back();
    //     }
    //     if(node->right)
    //     {
    //         backtracking(node->right);
    //         min_s.pop_back();
    //     } 

    // }

    vector<string> ans;

    void backtracking(TreeNode* node, string s) //不能引用，引用就变了
    {
        if(node->left == nullptr && node->right == nullptr)
        {
            s += to_string(node->val);
            ans.push_back(s);
            return;
        }

        s += to_string(node->val);
        if(node->left)
        {
            backtracking(node->left, s + "->");           
        }
        if(node->right)
        {
            backtracking(node->right, s + "->");          
        }
    }


    vector<string> binaryTreePaths(TreeNode* root) {
        if(root == nullptr) return ans;
        string s;
        backtracking(root, s);
        return ans;
    }
};
```

## 100 [相同的树](https://leetcode-cn.com/problems/same-tree/)

给你两棵二叉树的根节点 `p` 和 `q` ，编写一个函数来检验这两棵树是否相同。

如果两个树在结构上相同，并且节点具有相同的值，则认为它们是相同的。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if(p == nullptr && q == nullptr) return true;
        else if(p == nullptr || q == nullptr) return false;
        else if(p->val != q->val) return false;
        else
        {
            return isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
        }
    }
};
```

## 572 [另一个树的子树](https://leetcode-cn.com/problems/subtree-of-another-tree/)

给定两个非空二叉树 s 和 t，检验 s 中是否包含和 t 具有相同结构和节点值的子树。s 的一个子树包括 s 的一个节点和这个节点的所有子孙。s 也可以看做它自身的一棵子树。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if(p == nullptr && q == nullptr) return true;
        else if(p == nullptr || q == nullptr) return false;
        else if(p->val != q->val) return false;
        else
        {
            return isSameTree(p->left, q->left) && isSameTree(p->right, q->right);
        }
    }
    bool isSubtree(TreeNode* root, TreeNode* subRoot) {
        if(root == nullptr && subRoot == nullptr) return true;
        if(root == nullptr) return false;
        return isSameTree(root, subRoot) || isSubtree(root->left, subRoot) || isSubtree(root->right, subRoot);
    }
};
```

## 404 [左叶子之和](https://leetcode-cn.com/problems/sum-of-left-leaves/)

计算给定二叉树的所有左叶子之和。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:

    int sumOfLeftLeaves(TreeNode* root) {
        // queue<TreeNode*> que;
        // int ans = 0;
        // if(root) que.push(root);
        // while(!que.empty())
        // {
        //     TreeNode* node = que.front();
        //     que.pop();
        //     if(node->left)
        //     {
        //         if(node->left->left == nullptr && node->left->right == nullptr)
        //         {
        //             ans += node->left->val;
        //         }
        //         que.push(node->left);
        //     }
        //     if(node->right) que.push(node->right);
        // }

        // return ans;
        if(root == nullptr) return 0;
        int left = sumOfLeftLeaves(root->left);
        int right = sumOfLeftLeaves(root->right);
        int mid = 0;
        if(root->left != nullptr && root->left->left == nullptr && root->left->right == nullptr)
        {
            mid = root->left->val;
        }

        return left + right + mid;

    }
};
```

## 513 [找树左下角的值](https://leetcode-cn.com/problems/find-bottom-left-tree-value/)

给定一个二叉树，在树的最后一行找到最左边的值。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int findBottomLeftValue(TreeNode* root) {
        queue<TreeNode*> que;
        if(root) que.push(root);
        int ans;

        while(!que.empty())
        {
            int size = que.size();
            for(int i = 0; i < size; i++)
            {
                TreeNode* node = que.front();
                que.pop();
                if(i == 0)
                {
                    ans = node->val;
                }
                if(node->left) que.push(node->left);
                if(node->right) que.push(node->right);
            }
        }
        return ans;
    }
};
```

## 112 [路径总和](https://leetcode-cn.com/problems/path-sum/)

给你二叉树的根节点 root 和一个表示目标和的整数 targetSum ，判断该树中是否存在 根节点到叶子节点 的路径，这条路径上所有节点值相加等于目标和 targetSum 。

叶子节点 是指没有子节点的节点。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:

    bool traversal(TreeNode* node, int sum)
    {
        if(!node->left && !node->right && sum == 0) return true;
        else if(!node->left && !node->right) return false;

        if(node->left)
        {
            sum -= node->left->val;
            if(traversal(node->left, sum)) return true;
            sum += node->left->val;
        } 
        if(node->right)
        {
            sum -= node->right->val;
            if(traversal(node->right, sum)) return true;
            sum += node->right->val;
        }
        return false;
    }

    bool hasPathSum(TreeNode* root, int targetSum) {
        if(root == nullptr) return false;
        return traversal(root , targetSum - root->val);
    }
};
```

## 106 [从中序与后序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/)

根据一棵树的中序遍历与后序遍历构造二叉树。

**注意:**
你可以假设树中没有重复的元素。

左闭右闭

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* build(vector<int>& inorder, int inleft, int inright, vector<int>& postorder, int postleft, int postright)
    {
        if(inleft > inright) return nullptr;
        TreeNode* node = new TreeNode(postorder[postright]);

        int index = inleft;
        for(index; index <= inright; index++)
        {
            if(inorder[index] == postorder[postright])
                break;
        }

        node->left = build(inorder, inleft, index - 1, postorder, postleft, postleft + index - inleft - 1);
        node->right = build(inorder, index + 1, inright, postorder, postleft + index - inleft, postright - 1);
        return node;
    }

    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        return build(inorder, 0, inorder.size() - 1, postorder, 0, postorder.size() - 1);
    }
};
```

左闭右开

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* build(vector<int>& inorder, int inleft, int inright, vector<int>& postorder, int postleft, int postright)
    {
        if(inleft >= inright) return nullptr;
        TreeNode* node = new TreeNode(postorder[postright - 1]);

        int index = inleft;
        for(index; index < inright; index++)
        {
            if(inorder[index] == postorder[postright - 1])
                break;
        }

        node->left = build(inorder, inleft, index, postorder, postleft, postleft + index - inleft);
        node->right = build(inorder, index + 1, inright, postorder, postleft + index - inleft, postright - 1);
        return node;
    }

    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        return build(inorder, 0, inorder.size(), postorder, 0, postorder.size());
    }
};
```

## 105 [ 从前序与中序遍历序列构造二叉树](https://leetcode-cn.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/)

根据一棵树的前序遍历与中序遍历构造二叉树。

**注意:**
你可以假设树中没有重复的元素。

左闭右闭

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* build(vector<int>& preorder, int preleft, int preright, vector<int>& inorder, int inleft, int inright)
    {
        if(inleft > inright) return nullptr;

        TreeNode* node = new TreeNode(preorder[preleft]);

        int index = inleft;
        for(index; index <= inright; index++)
        {
            if(inorder[index] == preorder[preleft])
                break;
        }

        node->left = build(preorder, preleft + 1, preleft + index - inleft, inorder, inleft, index - 1);
        node->right = build(preorder, preleft + index - inleft + 1, preright, inorder, index + 1, inright);
        return node;
    }


    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        return build(preorder, 0, preorder.size() - 1, inorder, 0, inorder.size() - 1);
    }
};
```

左闭右开

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* build(vector<int>& preorder, int preleft, int preright, vector<int>& inorder, int inleft, int inright)
    {
        if(inleft >= inright) return nullptr;

        TreeNode* node = new TreeNode(preorder[preleft]);

        int index = inleft;
        for(index; index < inright; index++)
        {
            if(inorder[index] == preorder[preleft])
                break;
        }

        node->left = build(preorder, preleft + 1, preleft + index - inleft + 1, inorder, inleft, index);
        node->right = build(preorder, preleft + index - inleft + 1, preright, inorder, index + 1, inright);
        return node;
    }


    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        return build(preorder, 0, preorder.size(), inorder, 0, inorder.size());
    }
};
```

## 654 [最大二叉树](https://leetcode-cn.com/problems/maximum-binary-tree/)

给定一个不含重复元素的整数数组 nums 。一个以此数组直接递归构建的 最大二叉树 定义如下：

二叉树的根是数组 nums 中的最大元素。
左子树是通过数组中 最大值左边部分 递归构造出的最大二叉树。
右子树是通过数组中 最大值右边部分 递归构造出的最大二叉树。
返回有给定数组 nums 构建的 最大二叉树 。

左闭右闭

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* construct(vector<int>& nums, int begin, int end)
    {
        if(begin > end) return nullptr;

        int max_num = INT_MIN;
        int index = begin;
        for(int i = begin; i <= end; i++)
        {
            if(max_num < nums[i])
            {
                max_num = nums[i];
                index = i;
            }
        }

        TreeNode* node = new TreeNode(max_num);
        node->left = construct(nums, begin, index - 1);
        node->right = construct(nums, index + 1, end);

        return node;
    }

    TreeNode* constructMaximumBinaryTree(vector<int>& nums) {
        return construct(nums, 0, nums.size() - 1);
    }
};
```

左闭右开

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* construct(vector<int>& nums, int begin, int end)
    {
        if(begin >= end) return nullptr;

        int max_num = INT_MIN;
        int index = begin;
        for(int i = begin; i < end; i++)
        {
            if(max_num < nums[i])
            {
                max_num = nums[i];
                index = i;
            }
        }

        TreeNode* node = new TreeNode(max_num);
        node->left = construct(nums, begin, index);
        node->right = construct(nums, index + 1, end);

        return node;
    }

    TreeNode* constructMaximumBinaryTree(vector<int>& nums) {
        return construct(nums, 0, nums.size());
    }
};
```

## 617 [合并二叉树](https://leetcode-cn.com/problems/merge-two-binary-trees/)

给定两个二叉树，想象当你将它们中的一个覆盖到另一个上时，两个二叉树的一些节点便会重叠。

你需要将他们合并为一个新的二叉树。合并的规则是如果两个节点重叠，那么将他们的值相加作为节点合并后的新值，否则不为 NULL 的节点将直接作为新二叉树的节点。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* mergeTrees(TreeNode* root1, TreeNode* root2) {
        // if(root1 == nullptr && root2 == nullptr) return nullptr;
        // else if(root1 == nullptr) return root2;
        // else if(root2 == nullptr) return root1;
        // else
        // {
        //     root1->val += root2->val;
        //     root1->left = mergeTrees(root1->left, root2->left);
        //     root1->right = mergeTrees(root1->right, root2->right);
        //     return root1; 
        // }


        queue<TreeNode*> que;
        if(root1 == nullptr) return root2;
        if(root2 == nullptr) return root1;
        que.push(root1);
        que.push(root2);

        while(!que.empty())
        {
            TreeNode* node1 = que.front();
            que.pop();
            TreeNode* node2 = que.front();
            que.pop();
            node1->val += node2->val;
            if(node1->left != nullptr && node2->left != nullptr)
            {
                que.push(node1->left);
                que.push(node2->left);
            }

            if(node1->right != nullptr && node2->right != nullptr)
            {
                que.push(node1->right);
                que.push(node2->right);
            }

            if(node1->left == nullptr && node2->left != nullptr)
            {
                node1->left = node2->left;
            }

            if(node1->right == nullptr && node2->right != nullptr)
            {
                node1->right = node2->right;
            }

        }
        return root1;
    }
};
```

## 700 [二叉搜索树中的搜索](https://leetcode-cn.com/problems/search-in-a-binary-search-tree/)

给定二叉搜索树（BST）的根节点和一个值。 你需要在BST中找到节点值等于给定值的节点。 返回以该节点为根的子树。 如果节点不存在，则返回 NULL。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* searchBST(TreeNode* root, int val) {
        TreeNode* cur = root;
        while(cur)
        {
            if(cur->val < val)
            {
                cur = cur->right;
            }
            else if(cur->val > val)
            {
                cur = cur->left;
            }
            else
            {
                return cur;
            }
        }
        return nullptr;
    }
};
```

## 98 [验证二叉搜索树](https://leetcode-cn.com/problems/validate-binary-search-tree/)

给定一个二叉树，判断其是否是一个有效的二叉搜索树。

假设一个二叉搜索树具有如下特征：

节点的左子树只包含小于当前节点的数。
节点的右子树只包含大于当前节点的数。
所有左子树和右子树自身必须也是二叉搜索树。

注意：绝对小于，绝对大于！！！！！！！！！！！！

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    // TreeNode* pre = nullptr;
    // bool ans = true;

    // void inorder(TreeNode* node)
    // {
    //     if(node == nullptr) return;
    //     inorder(node->left);
    //     if(pre == nullptr) pre = node;
    //     else if(pre->val >= node->val) ans = false;
    //     pre = node;
    //     inorder(node->right);
    // }

    bool isValidBST(TreeNode* root) {
        // inorder(root);
        // return ans;
        stack<TreeNode*> st;
        TreeNode* node = root;
        TreeNode* pre = nullptr;
        while(!st.empty() || node != nullptr)
        {
            if(node != nullptr)
            {
                st.push(node);
                node = node->left;
            }
            else
            {
                node = st.top();
                st.pop();
                if(pre == nullptr) pre = node;
                else if(pre->val >= node->val)
                {
                    return false;
                }
                pre = node;
                node = node->right;
            }

        }
        return true;


    }
};
```

## 530 [二叉搜索树的最小绝对差](https://leetcode-cn.com/problems/minimum-absolute-difference-in-bst/)

给你一棵所有节点为非负值的二叉搜索树，请你计算树中任意两节点的差的绝对值的最小值。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    // int ans = INT_MAX;
    // TreeNode* pre = nullptr;

    // void inorder(TreeNode* node)
    // {
    //     if(node == nullptr) return ;
    //     inorder(node->left);
    //     if(pre == nullptr) pre = node;
    //     else
    //     {
    //         ans = min(ans, abs(pre->val - node->val));
    //     }
    //     pre = node;
    //     inorder(node->right);

    // }
    int getMinimumDifference(TreeNode* root) {
        // inorder(root);
        // return ans;
        int ans = INT_MAX;
        TreeNode* pre = nullptr;
        stack<TreeNode*> st;

        TreeNode* node = root;
        while(!st.empty() || node != nullptr)
        {
            if(node != nullptr)
            {
                st.push(node);
                node = node->left;
            }
            else
            {
                node = st.top();
                st.pop();
                if(pre == nullptr) pre = node;
                else
                {
                    ans = min(ans, abs(pre->val - node->val));
                }
                pre = node;
                node = node->right;
            }

        }
        return ans;
    }
};
```

## 501 [ 二叉搜索树中的众数](https://leetcode-cn.com/problems/find-mode-in-binary-search-tree/)

给定一个有相同值的二叉搜索树（BST），找出 BST 中的所有众数（出现频率最高的元素）。

假定 BST 有如下定义：

结点左子树中所含结点的值小于等于当前结点的值
结点右子树中所含结点的值大于等于当前结点的值
左子树和右子树都是二叉搜索树

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    // void inorder(TreeNode* node, unordered_map<int, int>& map)
    // {
    //     if(node == nullptr) return;
    //     inorder(node->left, map);
    //     map[node->val]++;
    //     inorder(node->right, map);
    // }

    // bool static cmp(pair<int, int>& a, pair<int, int>& b)
    // {
    //     return a.second > b.second;
    // }

    // vector<int> findMode(TreeNode* root) {
    //     // unordered_map<int, int> map;
    //     // inorder(root, map);
    //     // vector<pair<int, int>> vec(map.begin(), map.end());

    //     // sort(vec.begin(), vec.end(), cmp);
        
    //     // vector<int> ans;

    //     // for(int i = 0; i < vec.size(); i++)
    //     // {
    //     //     if(vec[i].second == vec[0].second) 
    //     //     {
    //     //         ans.push_back(vec[i].first);
    //     //     }
    //     // }
    //     // return ans;
    // }
    int cnt = 0;
    int max_cnt = 0;
    TreeNode* pre = nullptr;
    vector<int> ans;

    void inorder(TreeNode* node)
    {
        if(node == nullptr) return ;
        inorder(node->left);
        if(pre == nullptr) 
        {
            cnt = 1;
        }
        else if(pre->val == node->val)
        {
            cnt++;
        }
        else if(pre->val != node->val) cnt = 1;
        pre = node;

        if(cnt == max_cnt) ans.push_back(node->val);
        if(cnt > max_cnt)
        {
            max_cnt = cnt;
            ans.clear();
            ans.push_back(node->val);
        }
        inorder(node->right);
    }

    vector<int> findMode(TreeNode* root){
        inorder(root);
        return ans;
    }
};
```

## 236 [二叉树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-tree/)(好好理解)

给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个节点 p、q，最近公共祖先表示为一个节点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if(root == p || root == q || root == NULL) return root;
        
        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);

        if(left != NULL && right != NULL) return root;
        else if(left == NULL) return right;
        else if(right == NULL) return left;
        else return NULL;

    }
};
```

## 235 [ 二叉搜索树的最近公共祖先](https://leetcode-cn.com/problems/lowest-common-ancestor-of-a-binary-search-tree/)

给定一个二叉搜索树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个结点 p、q，最近公共祖先表示为一个结点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。”

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */

class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        TreeNode* node = root;
        while(node)
        {
            if(node->val > p->val && node->val > q->val)
            {
                node = node->left;
            }
            else if(node->val < p->val && node->val < q->val)
            {
                node = node->right;
            }
            else
            {
                return node;
            }
        }
        return NULL;
    }
};
```

## *701 [二叉搜索树中的插入操作](https://leetcode-cn.com/problems/insert-into-a-binary-search-tree/)

给定二叉搜索树（BST）的根节点和要插入树中的值，将值插入二叉搜索树。 返回插入后二叉搜索树的根节点。 输入数据 保证 ，新值和原始二叉搜索树中的任意节点值都不同。

注意，可能存在多种有效的插入方式，只要树在插入后仍保持为二叉搜索树即可。 你可以返回 任意有效的结果 。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* insertIntoBST(TreeNode* root, int val) {
        if(root == nullptr)
        {
            return new TreeNode(val);
        }
        if(root->val > val) root->left = insertIntoBST(root->left, val);
        if(root->val < val) root->right = insertIntoBST(root->right, val);

        return root;
    }
};
```

## *450 [删除二叉搜索树中的节点](https://leetcode-cn.com/problems/delete-node-in-a-bst/)

给定一个二叉搜索树的根节点 root 和一个值 key，删除二叉搜索树中的 key 对应的节点，并保证二叉搜索树的性质不变。返回二叉搜索树（有可能被更新）的根节点的引用。

一般来说，删除节点可分为两个步骤：

首先找到需要删除的节点；
如果找到了，删除它。
说明： 要求算法时间复杂度为 O(h)，h 为树的高度。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* deleteNode(TreeNode* root, int key) {
        if(root == nullptr) return nullptr;

        if(root->val == key)
        {
            if(root->left == nullptr && root->right == nullptr) return nullptr;
            else if(root->left == nullptr) return root->right;
            else if(root->right == nullptr) return root->left;
            else
            {
                TreeNode* right = root->right;
                TreeNode* cur = root->left;
                while(cur->right)
                {
                    cur = cur->right;
                }
                TreeNode* tmp = root;
                root = root->left;
                cur->right = right;
                
                delete tmp;
                return root;
            }
        }
        if(root->val > key) root->left = deleteNode(root->left, key);
        if(root->val < key) root->right = deleteNode(root->right, key);

        return root;


    }
};
```

## *669 [修剪二叉搜索树](https://leetcode-cn.com/problems/trim-a-binary-search-tree/)

给你二叉搜索树的根节点 root ，同时给定最小边界low 和最大边界 high。通过修剪二叉搜索树，使得所有节点的值在[low, high]中。修剪树不应该改变保留在树中的元素的相对结构（即，如果没有被移除，原有的父代子代关系都应当保留）。 可以证明，存在唯一的答案。

所以结果应当返回修剪好的二叉搜索树的新的根节点。注意，根节点可能会根据给定的边界发生改变。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* trimBST(TreeNode* root, int low, int high) {
        if(root == nullptr) return nullptr;

        if(root->val < low)
        {
            TreeNode* right = trimBST(root->right, low, high);
            return right;
        }
        if(root->val > high)
        {
            TreeNode* left = trimBST(root->left, low, high);
            return left;
        }

        root->left = trimBST(root->left, low, high);
        root->right = trimBST(root->right, low, high);
        return root;
        
    }
};
```

## 108 [将有序数组转换为二叉搜索树](https://leetcode-cn.com/problems/convert-sorted-array-to-binary-search-tree/)

给你一个整数数组 nums ，其中元素已经按 升序 排列，请你将其转换为一棵 高度平衡 二叉搜索树。

高度平衡 二叉树是一棵满足「每个节点的左右两个子树的高度差的绝对值不超过 1 」的二叉树。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* construct(vector<int>& nums, int begin, int end)
    {
        if(begin > end) return nullptr;
        int mid = begin + (end - begin) / 2;
        TreeNode* node = new TreeNode(nums[mid]);
        node->left = construct(nums, begin, mid - 1);
        node->right = construct(nums, mid + 1, end);
        return node;
    }
    TreeNode* sortedArrayToBST(vector<int>& nums) {
        return construct(nums, 0, nums.size() - 1);
    }
};
```

## 538 [把二叉搜索树转换为累加树](https://leetcode-cn.com/problems/convert-bst-to-greater-tree/)

给出二叉 搜索 树的根节点，该树的节点值各不相同，请你将其转换为累加树（Greater Sum Tree），使每个节点 node 的新值等于原树中大于或等于 node.val 的值之和。

提醒一下，二叉搜索树满足下列约束条件：

节点的左子树仅包含键 小于 节点键的节点。
节点的右子树仅包含键 大于 节点键的节点。
左右子树也必须是二叉搜索树。

```c++
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    TreeNode* pre = nullptr;
    void inorder(TreeNode* node)
    {
        if(node == nullptr) return ;
        inorder(node->right);
        if(pre == nullptr)
        {
            pre = node;
        }
        else
        {
            node->val += pre->val;
        }
        pre = node;
        inorder(node->left);
    }

    TreeNode* convertBST(TreeNode* root) {
        inorder(root);
        return root;
    }
};
```

# 7、回溯

## 77 组合

给定两个整数 *n* 和 *k*，返回 1 ... *n* 中所有可能的 *k* 个数的组合。

```c++
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;

    void backtracking(int n, int k, int startIndex)
    {
        if(path.size() == k)
        {
            ans.push_back(path);
            return;
        }

        for(int i = startIndex; i <= n; i++)
        {
            path.push_back(i);
            backtracking(n, k, i + 1);
            path.pop_back();
        }
    }

    vector<vector<int>> combine(int n, int k) {
        ans.clear();
        path.clear();
        backtracking(n, k, 1);
        return ans;
    }
};
```

## 216 [组合总和 III](https://leetcode-cn.com/problems/combination-sum-iii/)

找出所有相加之和为 n 的 k 个数的组合。组合中只允许含有 1 - 9 的正整数，并且每种组合中不存在重复的数字。

说明：

所有数字都是正整数。
解集不能包含重复的组合。 

```c++
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;

    void backtracking(int k, int n, int sum, int startIndex)
    {
        if(sum == 0 && path.size() == k)
        {
            ans.push_back(path);
            return ;
        }
        if(sum < 0) return;

        for(int i = startIndex; i <= n; i++)
        {
            path.push_back(i);
            sum -= i;
            backtracking(k, n, sum, i + 1);
            sum += i;
            path.pop_back();
        }
    }


    vector<vector<int>> combinationSum3(int k, int n) {
        ans.clear();
        path.clear();
        backtracking(k, 9, n, 1);
        return ans;
    }
};
```

## 17 [电话号码的字母组合](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)

给定一个仅包含数字 2-9 的字符串，返回所有它能表示的字母组合。答案可以按 任意顺序 返回。

给出数字到字母的映射如下（与电话按键相同）。注意 1 不对应任何字母。

```c++
class Solution {
public:
    const string map[10] = {
        "",
        "",
        "abc",
        "def",
        "ghi",
        "jkl",
        "mno",
        "pqrs",
        "tuv",
        "wxyz"
    };

    vector<string> ans;
    string path;

    void backtracking(string digits, int startIndex)
    {
        if(path.size() == digits.size())
        {
            ans.push_back(path);
            return ;
        }
        int index = digits[startIndex] - '0';
        string s = map[index];

        for(int i = 0; i < s.size(); i++)
        {
            path.push_back(s[i]);
            backtracking(digits, startIndex + 1);
            path.pop_back();
        }

    }

    vector<string> letterCombinations(string digits) {
        if(digits.size() == 0) return ans;
        ans.clear();
        path.clear();
        backtracking(digits, 0);
        return ans;
    }
};
```

## 39 [组合总和](https://leetcode-cn.com/problems/combination-sum/)

给定一个无重复元素的数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的数字可以无限制重复被选取。

说明：

所有数字（包括 target）都是正整数。
解集不能包含重复的组合。 

```c++
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;

    void backtracking(vector<int>& candidates, int target, int startIndex)
    {
        if(target == 0)
        {
            ans.push_back(path);
            return ;
        }
        if(target < 0) return;

        for(int i = startIndex; i < candidates.size(); i++)
        {
            path.push_back(candidates[i]);
            target -= candidates[i];
            backtracking(candidates, target, i);
            target += candidates[i];
            path.pop_back();
        }
    }

    vector<vector<int>> combinationSum(vector<int>& candidates, int target) {
        ans.clear();
        path.clear();
        backtracking(candidates, target, 0);
        return ans;
    }
};
```

## 40 [组合总和 II](https://leetcode-cn.com/problems/combination-sum-ii/)

给定一个数组 candidates 和一个目标数 target ，找出 candidates 中所有可以使数字和为 target 的组合。

candidates 中的每个数字在每个组合中只能使用一次。

说明：

所有数字（包括目标数）都是正整数。
解集不能包含重复的组合。

```c++
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;

    void backtracking(vector<int>& candidates, int target, int startIndex, vector<bool>& used)
    {
        if(target == 0)
        {
            ans.push_back(path);
            return;
        }
        if(target < 0) return ;

        for(int i = startIndex; i < candidates.size(); i++)
        {
            if(i > 0 && candidates[i] == candidates[i - 1] && used[i - 1] == false)
                continue;
            
            path.push_back(candidates[i]);
            used[i] = true;
            target -= candidates[i];
            backtracking(candidates, target, i + 1, used);
            target += candidates[i];
            used[i] = false;
            path.pop_back();
        }
    }

    vector<vector<int>> combinationSum2(vector<int>& candidates, int target) {
        sort(candidates.begin(), candidates.end());
        vector<bool> used(candidates.size(), false);

        backtracking(candidates, target, 0, used);
        return ans;
    }
};
```

## 131 [分割回文串](https://leetcode-cn.com/problems/palindrome-partitioning/)

给你一个字符串 `s`，请你将 `s` 分割成一些子串，使每个子串都是 **回文串** 。返回 `s` 所有可能的分割方案。

**回文串** 是正着读和反着读都一样的字符串。

```c++
class Solution {
public:
    vector<vector<string>> ans;
    vector<string> path;

    bool isok(const string s, int left, int right)
    {
        for(int i = left, j = right; i < j; i++, j--)
        {
            if(s[i] != s[j]) return false;
        }
        return true;
    }

    void backtracking(string s, int startIndex)
    {
        if(startIndex == s.size())
        {
            ans.push_back(path);
            return ;
        }

        for(int i = startIndex; i < s.size(); i++)
        {
            if(isok(s, startIndex, i))
            {
                path.push_back(s.substr(startIndex, i - startIndex + 1));
                backtracking(s, i + 1);
                path.pop_back();
            }
        }
    }

    vector<vector<string>> partition(string s) {
        backtracking(s, 0);
        return ans;
    }
};
```

## *93 [ 复原 IP 地址](https://leetcode-cn.com/problems/restore-ip-addresses/)(字符串比较)

给定一个只包含数字的字符串，用以表示一个 IP 地址，返回所有可能从 s 获得的 有效 IP 地址 。你可以按任何顺序返回答案。

有效 IP 地址 正好由四个整数（每个整数位于 0 到 255 之间组成，且不能含有前导 0），整数之间用 '.' 分隔。

例如："0.1.2.201" 和 "192.168.1.1" 是 有效 IP 地址，但是 "0.011.255.245"、"192.168.1.312" 和 "192.168@1.1" 是 无效 IP 地址。

```c++
class Solution {
public:
    vector<string> ans;
    
    bool isvalid(const string s)
    {

        if(s.size() == 0 || s.size() > 3) return false;
        
        if(s.size() > 1 && s[0] == '0') return false;

        int num = 0;
        for (int i = 0; i < s.size(); i++) {
            // if (s[i] > '9' || s[i] < '0') { // 遇到非数字字符不合法
            //     return false;
            // }
            num = num * 10 + (s[i] - '0');
            if (num > 255) { // 如果大于255了不合法
                return false;
            }
        }

        return true;
    }

    void backtracking(string& s, int startIndex, int pointnum)
    {
        if(pointnum == 3)
        {     
            if(isvalid(s.substr(startIndex, s.size() - startIndex)))
                ans.push_back(s);
            return;
        }

        for(int i = startIndex; i < s.size(); i++)
        {
            if(isvalid(s.substr(startIndex, i - startIndex + 1)))
            {
                s.insert(s.begin() + i + 1, '.');
                pointnum++;
                backtracking(s, i + 2, pointnum);
                pointnum--;
                s.erase(s.begin() + i + 1);
            }
            else break;
        }   
    }


    vector<string> restoreIpAddresses(string s) {
        backtracking(s, 0, 0);
        return ans;
    }
};
```

## 78 [子集](https://leetcode-cn.com/problems/subsets/)

给你一个整数数组 `nums` ，数组中的元素 **互不相同** 。返回该数组所有可能的子集（幂集）。

解集 **不能** 包含重复的子集。你可以按 **任意顺序** 返回解集。

```c++
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;

    void backtracking(vector<int>& nums, int startIndex)
    {
        ans.push_back(path);
        if(startIndex >= nums.size()) return;

        for(int i = startIndex; i < nums.size(); i++)
        {
            path.push_back(nums[i]);
            backtracking(nums, i + 1);
            path.pop_back();
        }
    }
    vector<vector<int>> subsets(vector<int>& nums) {
        backtracking(nums, 0);
        return ans;
    }
};
```

## 90 [子集 II](https://leetcode-cn.com/problems/subsets-ii/)

给你一个整数数组 nums ，其中可能包含重复元素，请你返回该数组所有可能的子集（幂集）。

解集 不能 包含重复的子集。返回的解集中，子集可以按 任意顺序 排列。

```c++
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;

    void backtracking(vector<int>& nums, int startIndex, vector<bool>& used)
    {
        ans.push_back(path);
        if(startIndex >= nums.size()) return;

        for(int i = startIndex; i < nums.size(); i++)
        {
            if(i > 0 && nums[i] == nums[i - 1] && used[i - 1] == false)
            {
                continue;
            }

            path.push_back(nums[i]);
            used[i] = true;
            backtracking(nums, i + 1, used);
            used[i] = false;
            path.pop_back();
        }
    }

    vector<vector<int>> subsetsWithDup(vector<int>& nums) {
        sort(nums.begin(), nums.end());
        vector<bool> used(nums.size(), false);
        backtracking(nums, 0, used);
        return ans;
    }
};
```

## 491 [递增子序列](https://leetcode-cn.com/problems/increasing-subsequences/)(注意判断条件)

给定一个整型数组, 你的任务是找到所有该数组的递增子序列，递增子序列的长度至少是 2 。

```c++
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;

    void backtracking(vector<int>& nums, int startIndex)
    {
        if(path.size() >= 2)
        {
            ans.push_back(path);
        }
        if(startIndex >= nums.size()) return;

        int used[201] = {0};
        for(int i = startIndex; i < nums.size(); i++)
        {
            if(used[nums[i] + 100] == 1) continue;

            if((path.size() > 0 && nums[i] >= path[path.size() - 1]) || path.size() == 0)
            {
                path.push_back(nums[i]);
                used[nums[i] + 100] = 1;
                backtracking(nums, i + 1);
                path.pop_back();
            }
        }
    }

    vector<vector<int>> findSubsequences(vector<int>& nums) {
        backtracking(nums, 0);
        return ans;
    }
};
```

## 46 [全排列](https://leetcode-cn.com/problems/permutations/)

给定一个不含重复数字的数组 `nums` ，返回其 **所有可能的全排列** 。你可以 **按任意顺序** 返回答案。

```c++
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;

    void backtracking(vector<int>& nums, vector<bool>& used)
    {
        if(path.size() == nums.size())
        {
            ans.push_back(path);
            return ;
        }

        for(int i = 0; i < nums.size(); i++)
        {
            if(used[i] == true) continue;
            path.push_back(nums[i]);
            used[i] = true;
            backtracking(nums, used);
            used[i] = false;
            path.pop_back();
        }
    }

    vector<vector<int>> permute(vector<int>& nums) {
        ans.clear();
        path.clear();
        vector<bool> used(nums.size(), false);
        backtracking(nums, used);
        return ans;
    }
};
```

## 47 [全排列 II](https://leetcode-cn.com/problems/permutations-ii/)

给定一个可包含重复数字的序列 `nums` ，**按任意顺序** 返回所有不重复的全排列。

 

```c++
class Solution {
public:
    vector<vector<int>> ans;
    vector<int> path;

    void backtracking(vector<int>& nums, vector<bool>& used)
    {
        if(path.size() == nums.size())
        {
            ans.push_back(path);
            return ;
        }

        for(int i = 0; i < nums.size(); i++)
        {
            if(i > 0 && nums[i] == nums[i - 1] && used[i - 1] == false)
                continue;

            if(used[i] == true) continue;

            path.push_back(nums[i]);
            used[i] = true;
            backtracking(nums, used);
            used[i] = false;
            path.pop_back();
        }
    }

    vector<vector<int>> permuteUnique(vector<int>& nums) {
        ans.clear();
        path.clear();
        sort(nums.begin(), nums.end());
        vector<bool> used(nums.size(), false);
        backtracking(nums, used);

        return ans;
    }
};
```

## 332 [重新安排行程](https://leetcode-cn.com/problems/reconstruct-itinerary/)

给定一个机票的字符串二维数组 [from, to]，子数组中的两个成员分别表示飞机出发和降落的机场地点，对该行程进行重新规划排序。所有这些机票都属于一个从 JFK（肯尼迪国际机场）出发的先生，所以该行程必须从 JFK 开始。

 

提示：

如果存在多种有效的行程，请你按字符自然排序返回最小的行程组合。例如，行程 ["JFK", "LGA"] 与 ["JFK", "LGB"] 相比就更小，排序更靠前
所有的机场都用三个大写字母表示（机场代码）。
假定所有机票至少存在一种合理的行程。
所有的机票必须都用一次 且 只能用一次。

```c++
class Solution {
public:
    unordered_map<string, map<string, int>> targets;

    bool backtracking(int ticketNum, vector<string>& ans)
    {
        if(ans.size() == ticketNum + 1)
        {
            return true;
        }

        for(pair<const string, int>& target : targets[ans[ans.size() - 1]])
        {
            if(target.second > 0)
            {
                ans.push_back(target.first);
                target.second--;
                if(backtracking(ticketNum, ans)) return true;
                target.second++;
                ans.pop_back();
            }
        }
        return false;
    }


    vector<string> findItinerary(vector<vector<string>>& tickets) {
        vector<string> ans;

        for(const vector<string>& vec : tickets)
        {
            targets[vec[0]][vec[1]]++;
        }
        ans.push_back("JFK");
        backtracking(tickets.size(), ans);
        return ans;
    }
};
```

## 51 [N 皇后](https://leetcode-cn.com/problems/n-queens/)

n 皇后问题 研究的是如何将 n 个皇后放置在 n×n 的棋盘上，并且使皇后彼此之间不能相互攻击。

给你一个整数 n ，返回所有不同的 n 皇后问题 的解决方案。

每一种解法包含一个不同的 n 皇后问题 的棋子放置方案，该方案中 'Q' 和 '.' 分别代表了皇后和空位。

```c++
class Solution {
public:
    vector<vector<string>> ans;

    void backtracking(int n, int row, vector<string>& chessboard)
    {
        if(row == n)
        {
            ans.push_back(chessboard);
            return ;
        }

        for(int col = 0; col < n; col++)
        {
            if(isvalid(row, col, chessboard, n))
            {
                chessboard[row][col] = 'Q';
                backtracking(n, row + 1, chessboard);
                chessboard[row][col] = '.';
            }
        }
    }

    bool isvalid(int row, int col, vector<string>& chessboard, int n)
    {
        for(int i = 0; i < row; i++)
        {
            if(chessboard[i][col] == 'Q') 
                return false;
        }

        for(int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--)
        {
            if(chessboard[i][j] == 'Q')
                return false;
        }

        for(int i = row - 1, j = col + 1; i >= 0 && j < n; i--, j++)
        {
            if(chessboard[i][j] == 'Q')
                return false;
        }

        return true;
    }

    vector<vector<string>> solveNQueens(int n) {
        ans.clear();
        vector<string> chessboard(n, string(n, '.'));

        backtracking(n, 0, chessboard);
        return ans;
    }
};
```

# 8、贪心

## 455 [分发饼干](https://leetcode-cn.com/problems/assign-cookies/)

假设你是一位很棒的家长，想要给你的孩子们一些小饼干。但是，每个孩子最多只能给一块饼干。

对每个孩子 i，都有一个胃口值 g[i]，这是能让孩子们满足胃口的饼干的最小尺寸；并且每块饼干 j，都有一个尺寸 s[j] 。如果 s[j] >= g[i]，我们可以将这个饼干 j 分配给孩子 i ，这个孩子会得到满足。你的目标是尽可能满足越多数量的孩子，并输出这个最大数值。

```c++
class Solution {
public:
    int findContentChildren(vector<int>& g, vector<int>& s) {
        sort(g.begin(), g.end());
        sort(s.begin(), s.end());
        int ans = 0;
        int idx = s.size() - 1;
        for(int i = g.size() - 1; i >= 0; i--)
        {
            if(idx >= 0 && g[i] <= s[idx])
            {
                ans++;
                idx--;
            }
        }
        return ans;
    }
};
```

## 376 [摆动序列](https://leetcode-cn.com/problems/wiggle-subsequence/)

如果连续数字之间的差严格地在正数和负数之间交替，则数字序列称为 摆动序列 。第一个差（如果存在的话）可能是正数或负数。仅有一个元素或者含两个不等元素的序列也视作摆动序列。

例如， [1, 7, 4, 9, 2, 5] 是一个 摆动序列 ，因为差值 (6, -3, 5, -7, 3) 是正负交替出现的。

相反，[1, 4, 7, 2, 5] 和 [1, 7, 4, 5, 5] 不是摆动序列，第一个序列是因为它的前两个差值都是正数，第二个序列是因为它的最后一个差值为零。
子序列 可以通过从原始序列中删除一些（也可以不删除）元素来获得，剩下的元素保持其原始顺序。

给你一个整数数组 nums ，返回 nums 中作为 摆动序列 的 最长子序列的长度 。

```c++
class Solution {
public:
    int wiggleMaxLength(vector<int>& nums) {
        int ans = 1;
        int pre = 0;

        for(int i = 1; i < nums.size(); i++)
        {
            int cur = nums[i] - nums[i - 1];
            if((pre >= 0 && cur < 0) || (pre <= 0 && cur > 0))
            {
                ans++;
                pre = cur;
            }

        }
        return ans;
    }
};
```

## 53 [最大子序和](https://leetcode-cn.com/problems/maximum-subarray/)

给定一个整数数组 `nums` ，找到一个具有最大和的连续子数组（子数组最少包含一个元素），返回其最大和。

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int ans = INT_MIN;
        int cur = 0;
        for(int i = 0; i < nums.size(); i++)
        {
            cur += nums[i];
            if(cur > ans)
            {
                ans = cur;
            }
            if(cur < 0)
            {
                cur = 0;
            }
        }
        return ans;
    }
};
```

## 122 [买卖股票的最佳时机 II](https://leetcode-cn.com/problems/best-time-to-buy-and-sell-stock-ii/)

给定一个数组 prices ，其中 prices[i] 是一支给定股票第 i 天的价格。

设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。

注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        int ans = 0;

        for(int i = 1; i < prices.size(); i++)
        {
            int cur = prices[i] - prices[i - 1];
            if(cur > 0)
            {
                ans += cur;
            }
        }
        return ans;
    }
};
```

## 55 [跳跃游戏](https://leetcode-cn.com/problems/jump-game/)

给定一个非负整数数组 `nums` ，你最初位于数组的 **第一个下标** 。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

判断你是否能够到达最后一个下标。

```c++
class Solution {
public:
    bool canJump(vector<int>& nums) {
        int cover = nums[0];
        if(nums.size() ==  1) return true;
        for(int i = 0; i <= cover; i++)
        {
            cover = max(cover, i + nums[i]);
            if(cover >= nums.size() - 1) return true;
        }
        return false;
    }
};
```

## 45 [跳跃游戏 II](https://leetcode-cn.com/problems/jump-game-ii/)

给定一个非负整数数组，你最初位于数组的第一个位置。

数组中的每个元素代表你在该位置可以跳跃的最大长度。

你的目标是使用最少的跳跃次数到达数组的最后一个位置。

假设你总是可以到达数组的最后一个位置。

```c++
class Solution {
public:
    int jump(vector<int>& nums) {
        int ans = 0;
        int cur = 0;
        int next = 0;

        for(int i = 0; i < nums.size() - 1; i++)
        {
            next = max(nums[i] + i, next);
            if(i == cur)
            {
                cur = next;
                ans++;
            }
        }
        return ans;
    }
};
```

## 1005 [K 次取反后最大化的数组和](https://leetcode-cn.com/problems/maximize-sum-of-array-after-k-negations/)

给定一个整数数组 A，我们只能用以下方法修改该数组：我们选择某个索引 i 并将 A[i] 替换为 -A[i]，然后总共重复这个过程 K 次。（我们可以多次选择同一个索引 i。）

以这种方式修改数组后，返回数组可能的最大和。

```c++
class Solution {
public:
    bool static cmp(int a, int b)
    {
        return abs(a) > abs(b);
    }

    int largestSumAfterKNegations(vector<int>& nums, int k) {
        sort(nums.begin(), nums.end(), cmp);

        for(int i = 0; i < nums.size() && k > 0; i++)
        {
            if(k > 0 && nums[i] < 0)
            {
                nums[i] = -nums[i];
                k--;
            }
        }

        if(k != 0 && k % 2 == 1) nums[nums.size() - 1] *= -1;

        int ans = 0;
        for(int i = 0; i < nums.size(); i++)
        {
            ans += nums[i];
        } 
        return ans;
        
    }
};
```

## 134 [加油站](https://leetcode-cn.com/problems/gas-station/)

在一条环路上有 N 个加油站，其中第 i 个加油站有汽油 gas[i] 升。

你有一辆油箱容量无限的的汽车，从第 i 个加油站开往第 i+1 个加油站需要消耗汽油 cost[i] 升。你从其中的一个加油站出发，开始时油箱为空。

如果你可以绕环路行驶一周，则返回出发时加油站的编号，否则返回 -1。

说明: 

如果题目有解，该答案即为唯一答案。
输入数组均为非空数组，且长度相同。
输入数组中的元素均为非负数。

```c++
class Solution {
public:
    int canCompleteCircuit(vector<int>& gas, vector<int>& cost) {
        int totalsum = 0;
        int ans = 0;
        int cur = 0;
        for(int i = 0; i < gas.size(); i++)
        {
            totalsum += gas[i] - cost[i];
            cur += gas[i] - cost[i];
            if(cur < 0)
            {
                cur = 0;
                ans = i + 1;
            }
        }
        return totalsum < 0 ? -1 : ans;

    }
};
```

