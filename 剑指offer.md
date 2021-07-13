# 剑指offer

## [剑指 Offer 10- I. 斐波那契数列](https://leetcode-cn.com/problems/fei-bo-na-qi-shu-lie-lcof/)

写一个函数，输入 n ，求斐波那契（Fibonacci）数列的第 n 项（即 F(N)）。斐波那契数列的定义如下：

F(0) = 0,   F(1) = 1
F(N) = F(N - 1) + F(N - 2), 其中 N > 1.
斐波那契数列由 0 和 1 开始，之后的斐波那契数就是由之前的两数相加而得出。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

```c++
class Solution {
public:
    int fib(int n) {
        if(n == 0) return 0;
        vector<int> dp(n + 1, 0);
        dp[1] = 1;

        for(int i = 2; i <= n; i++)
        {
            dp[i] = dp[i - 1] % 1000000007 + dp[i - 2] % 1000000007;
        }

        return dp[n] % 1000000007;
    }
};
```

## [剑指 Offer 09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

```c++
class CQueue {
public:
    stack<int> In;
    stack<int> Out;

    CQueue() {

    }
    
    void appendTail(int value) {
        while(!Out.empty())
        {
            In.push(Out.top());
            Out.pop();
        }

        In.push(value);
        return;
    }
    
    int deleteHead() {
        if(In.empty() && Out.empty())
        {
            return -1;
        }

        while(!In.empty())
        {
            Out.push(In.top());
            In.pop();
        }

        int ans = Out.top();
        Out.pop();

        while(!Out.empty())
        {
            In.push(Out.top());
            Out.pop();
        }

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

## [剑指 Offer 03. 数组中重复的数字](https://leetcode-cn.com/problems/shu-zu-zhong-zhong-fu-de-shu-zi-lcof/)

找出数组中重复的数字。


在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。

```c++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        int i = 0;
        while(i < nums.size())
        {
            if(nums[i] == i)
            {
                i++;
                continue;
            }

            if(nums[nums[i]] == nums[i])
            {
                return nums[i];
            }

            swap(nums[nums[i]], nums[i]);
        }

        return -1;
    }
};
```

```c++
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
        int i = 0;
        while(i < nums.size())
        {
            if(nums[i] == i)
            {
                i++;
                continue;
            }

            if(nums[nums[i]] == nums[i])
            {
                return nums[i];
            }

            swap(nums[nums[i]], nums[i]);
        }

        return -1;
    }
};
```

## [剑指 Offer 04. 二维数组中的查找](https://leetcode-cn.com/problems/er-wei-shu-zu-zhong-de-cha-zhao-lcof/)

在一个 n * m 的二维数组中，每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个高效的函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数

```c++
class Solution {
public:
    bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
        if(matrix.size() == 0 || matrix[0].size() == 0) return false;
        int m = matrix.size();
        int n = matrix[0].size();
        
        for(int i = m - 1; i >= 0; i--)
        {
            if(matrix[i][0] <= target && matrix[i][n - 1] >= target)
            {
                for(int j = 0; j < n; j++)
                {
                    if(matrix[i][j] == target)
                    {
                        return true;
                    }
                }
            }
        }
        return false;
    }
};
```

```c++
class Solution {
public:
    bool findNumberIn2DArray(vector<vector<int>>& matrix, int target) {
        if(matrix.size() == 0 || matrix[0].size() == 0) return false;
        int m = matrix.size();
        int n = matrix[0].size();
        
        int i = m - 1, j = 0;

        while(i >= 0 && j < n)
        {
            if(matrix[i][j] > target) i--;
            else if(matrix[i][j] < target) j++;
            else return true;
        }

        return false;
    }
};
```

## [剑指 Offer 10- II. 青蛙跳台阶问题](https://leetcode-cn.com/problems/qing-wa-tiao-tai-jie-wen-ti-lcof/)

一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n 级的台阶总共有多少种跳法。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

```c++
class Solution {
public:
    int numWays(int n) {
        if(n == 0) return 1;
        vector<int> dp(n + 1, 0);
        dp[0] = 1;
        dp[1] = 1;

        for(int i = 2; i <= n; i++)
        {
            dp[i] = dp[i - 1] % 1000000007 + dp[i - 2] % 1000000007;
        }
        return dp[n] % 1000000007;
    }
};
```

## [剑指 Offer 11. 旋转数组的最小数字](https://leetcode-cn.com/problems/xuan-zhuan-shu-zu-de-zui-xiao-shu-zi-lcof/)

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。输入一个递增排序的数组的一个旋转，输出旋转数组的最小元素。例如，数组 [3,4,5,1,2] 为 [1,2,3,4,5] 的一个旋转，该数组的最小值为1。

```c++
class Solution {
public:
    int minArray(vector<int>& numbers) {
        int left = 0;
        int right = numbers.size() - 1;

        while(left < right)
        {
            int mid = left + (right - left) / 2;
            if(numbers[mid] < numbers[right])
            {
                right = mid;
            }
            else if(numbers[mid] > numbers[right])
            {
                left = mid + 1;
            }
            else
            {
                right -= 1;
            }
        }
        return numbers[left];
    }
};
```

## [剑指 Offer 12. 矩阵中的路径](https://leetcode-cn.com/problems/ju-zhen-zhong-de-lu-jing-lcof/)

给定一个 m x n 二维字符网格 board 和一个字符串单词 word 。如果 word 存在于网格中，返回 true ；否则，返回 false 。

单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。

```c++
class Solution {
public:
    bool backtracking(vector<vector<char>>& board, int i, int j, string word, int k)
    {
        if(i < 0 || i >= board.size() || j < 0 || j >= board[0].size() || board[i][j] != word[k]) return false;
        if(k == word.size() - 1)
        {
            return true;
        }
        
        board[i][j] = '\0';

        bool ans = backtracking(board, i - 1, j, word, k + 1) || backtracking(board, i + 1, j, word, k + 1) ||
                    backtracking(board, i, j - 1, word, k + 1) || backtracking(board, i, j + 1, word, k + 1);
        board[i][j] = word[k];

        return ans;


    }

    bool exist(vector<vector<char>>& board, string word) {
        if(board.size() == 0 || board[0].size() == 0) return false;
        int m = board.size();
        int n = board[0].size();

        for(int i = 0; i < m; i++)
        {
            for(int j = 0; j < n; j++)
            {
                if(backtracking(board, i, j, word, 0)) return true;
            }
        }
        return false;
    }
};
```

## [剑指 Offer 05. 替换空格](https://leetcode-cn.com/problems/ti-huan-kong-ge-lcof/)

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
        int oldsize = s.size() - 1;
        s.resize(s.size() + cnt * 2);
        int newsize = s.size() - 1;

        while(oldsize >= 0)
        {
            if(s[oldsize] != ' ')
            {
                s[newsize] = s[oldsize];
                newsize--;
                oldsize--;
            }
            else
            {
                s[newsize--] = '0';
                s[newsize--] = '2';
                s[newsize--] = '%';
                oldsize--;
            }
        }

        return s;
        
    }
};
```

## [剑指 Offer 13. 机器人的运动范围](https://leetcode-cn.com/problems/ji-qi-ren-de-yun-dong-fan-wei-lcof/)

地上有一个m行n列的方格，从坐标 [0,0] 到坐标 [m-1,n-1] 。一个机器人从坐标 [0, 0] 的格子开始移动，它每次可以向左、右、上、下移动一格（不能移动到方格外），也不能进入行坐标和列坐标的数位之和大于k的格子。例如，当k为18时，机器人能够进入方格 [35, 37] ，因为3+5+3+7=18。但它不能进入方格 [35, 38]，因为3+5+3+8=19。请问该机器人能够到达多少个格子？

```c++
class Solution {
public:
    int ans = 0;
    int isvalid(int num)
    {
        int cnt = 0;
        while(num)
        {
            cnt += num % 10;
            num /= 10;
        }
        return cnt;
    }

    void dfs(int i, int j, int m, int n, int k, vector<vector<bool>>& used)
    {
        if(i >= m || j >= n || isvalid(i) + isvalid(j) > k || used[i][j] == true) return;

        used[i][j] = true;
        ans++;
        dfs(i + 1, j, m, n, k, used);
        dfs(i, j + 1, m, n, k, used);
    }


    int movingCount(int m, int n, int k) {
        vector<vector<bool>> used(m, vector<bool>(n, false));
        dfs(0, 0, m, n, k, used);

        return ans;
    }
};
```

广度优先

```c++
class Solution {
public:
    int digNum(int num)
    {
        int cnt = 0;
        while(num)
        {
            cnt += num % 10;
            num /= 10;
        }

        return cnt;
    }


    int movingCount(int m, int n, int k) {
        queue<pair<int, int>> que;
        vector<vector<bool>> used(m, vector<bool>(n, false));
        int tx[2] = {1, 0};
        int ty[2] = {0, 1};
        int ans = 1;
        used[0][0] = 1;
        que.push({0, 0});
        while(!que.empty())
        {
            auto [x, y] = que.front();
            que.pop();

            for(int i = 0; i < 2; i++)
            {
                int dx = x + tx[i];
                int dy = y + ty[i];

                if(dx < m && dy < n && digNum(dx) + digNum(dy) <= k && used[dx][dy] == false)
                {
                    que.push({dx, dy});
                    used[dx][dy] = true;
                    ans++;
                }
            }
        }

        return ans;
    }
};
```

## [剑指 Offer 06. 从尾到头打印链表](https://leetcode-cn.com/problems/cong-wei-dao-tou-da-yin-lian-biao-lcof/)

输入一个链表的头节点，从尾到头反过来返回每个节点的值（用数组返回）。

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
    vector<int> reversePrint(ListNode* head) {
        vector<int> ans;

        stack<int> st;

        ListNode* cur = head;
        while(cur)
        {
            st.push(cur->val);
            cur = cur->next;
        }

        while(!st.empty())
        {
            ans.push_back(st.top());
            st.pop();
        }

        return ans;
    }
};
```

## [剑指 Offer 07. 重建二叉树](https://leetcode-cn.com/problems/zhong-jian-er-cha-shu-lcof/)

输入某二叉树的前序遍历和中序遍历的结果，请重建该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。

左闭右闭

```c
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
    TreeNode* build(vector<int>& preorder, int preleft, int preright, vector<int>& inorder, int inleft, int inright)
    {  //左闭右闭
        if(inleft > inright)
        {
            return NULL;
        }
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
        if(preorder.size() == 0) return NULL;

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
 *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
 * };
 */
class Solution {
public:
    TreeNode* build(vector<int>& preorder, int preleft, int preright, vector<int>& inorder, int inleft, int inright)
    {  //左闭右开
        if(inleft >= inright)
        {
            return NULL;
        }
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
        if(preorder.size() == 0) return NULL;

        return build(preorder, 0, preorder.size(), inorder, 0, inorder.size());
    }
};
```

## [剑指 Offer 14- I. 剪绳子](https://leetcode-cn.com/problems/jian-sheng-zi-lcof/)

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m-1] 。请问 k[0]*k[1]*...*k[m-1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

```c++
class Solution {
public:
    int cuttingRope(int n) {
        if(n < 4) return n - 1;
        int ans = 1;
        while(n > 4)
        {
            ans *= 3;
            n -= 3;
        }

        return n * ans;
    }
};
```

```c++
class Solution {
public:
    int cuttingRope(int n) {
        if(n < 4) return n - 1;
        vector<int> dp(n + 1, 0);
        dp[2] = 1;

        for(int i = 3; i <= n; i++)
        {
            for(int j = 1; j < i - 1; j++)
            {
                dp[i] = max(dp[i], max(dp[i - j] * j, j * (i - j)));
            }
        }
        return dp[n];
    }
};
```

## **[剑指 Offer 14- II. 剪绳子 II](https://leetcode-cn.com/problems/jian-sheng-zi-ii-lcof/)

给你一根长度为 n 的绳子，请把绳子剪成整数长度的 m 段（m、n都是整数，n>1并且m>1），每段绳子的长度记为 k[0],k[1]...k[m - 1] 。请问 k[0]*k[1]*...*k[m - 1] 可能的最大乘积是多少？例如，当绳子的长度是8时，我们把它剪成长度分别为2、3、3的三段，此时得到的最大乘积是18。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。（动态规划溢出）

```c++
class Solution {
public:
    int cuttingRope(int n) {
        if(n < 4) return n - 1;

        long long ans = 1;

        while(n > 4)
        {
            ans = (ans * 3) % 1000000007;
            n -= 3;
        }

        return (ans * n) %  1000000007;
    }
};
```

## [剑指 Offer 25. 合并两个排序的链表](https://leetcode-cn.com/problems/he-bing-liang-ge-pai-xu-de-lian-biao-lcof/)

输入两个递增排序的链表，合并这两个链表并使新链表中的节点仍然是递增排序的。

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
    ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
        ListNode* dummy = new ListNode(0);
        ListNode* cur = dummy;
        while(l1 && l2)
        {
            if(l1->val < l2->val)
            {
                cur->next = l1;
                l1 = l1->next;
            }
            else
            {
                cur->next = l2;
                l2 = l2->next;
            }
            cur = cur->next;
        }

        if(l1) cur->next = l1;
        if(l2) cur->next = l2;

        return dummy->next;

    }
};
```

## [剑指 Offer 26. 树的子结构](https://leetcode-cn.com/problems/shu-de-zi-jie-gou-lcof/)

输入两棵二叉树A和B，判断B是不是A的子结构。(约定空树不是任意一个树的子结构)

B是A的子结构， 即 A中有出现和B相同的结构和节点值。

例如:
给定的树 A:

     3
    / \
   4   5
  / \
 1   2
给定的树 B：

   4 
  /
 1
返回 true，因为 B 与 A 的一个子树拥有相同的结构和节点值。

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
    bool isvalid(TreeNode* p, TreeNode* q)
    {
        if(p == NULL && q == NULL) return true;
        if(p == NULL) return false;
        if(q == NULL) return true;

        if(p->val == q->val)
        {
            bool left = isvalid(p->left, q->left);
            bool right = isvalid(p->right, q->right);

            return left && right;
        }  
        else return false;
    }


    bool isSubStructure(TreeNode* A, TreeNode* B) {
        if(A == NULL || B == NULL) return false;

        return isvalid(A, B) || isSubStructure(A->left, B) || isSubStructure(A->right, B);
    }
};
```

## [剑指 Offer 27. 二叉树的镜像](https://leetcode-cn.com/problems/er-cha-shu-de-jing-xiang-lcof/)

请完成一个函数，输入一个二叉树，该函数输出它的镜像。

例如输入：

     4
   /   \
  2     7
 / \   / \
1   3 6   9
镜像输出：

     4
   /   \
  7     2
 / \   / \
9   6 3   1

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
    void preorder(TreeNode* node)
    {
        if(node == NULL) return;
        swap(node->left, node->right);
        preorder(node->left);
        preorder(node->right);

    }

    void inorder(TreeNode* node)
    {
        if(node == NULL) return ;

        inorder(node->left);
        swap(node->left, node->right);
        inorder(node->left);
    }

    void postprder(TreeNode* node)
    {
        if(node == NULL) return ;
        postprder(node->left);
        postprder(node->right);
        swap(node->left, node->right);
    }

    TreeNode* mirrorTree(TreeNode* root) {
        // preorder(root);
        // inorder(root);
        // postprder(root);

        return root;
    }
};
```

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
    TreeNode* mirrorTree(TreeNode* root) {
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

中序

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
    TreeNode* mirrorTree(TreeNode* root) {
        stack<TreeNode*> st;
        TreeNode* cur = root;

        while(!st.empty() || cur != NULL)
        {
            if(cur)
            {
                st.push(cur);
                cur = cur->left;
            }
            else
            {
                TreeNode* node = st.top();
                st.pop();
                swap(node->left, node->right);
                cur = node->left;
            }
        }

        return root;
    }
};
```

## [剑指 Offer 28. 对称的二叉树](https://leetcode-cn.com/problems/dui-cheng-de-er-cha-shu-lcof/)

请实现一个函数，用来判断一棵二叉树是不是对称的。如果一棵二叉树和它的镜像一样，那么它是对称的。

例如，二叉树 [1,2,2,3,4,4,3] 是对称的。

    1
   / \
  2   2
 / \ / \
3  4 4  3
但是下面这个 [1,2,2,null,3,null,3] 则不是镜像对称的:

    1
   / \
  2   2
   \   \
   3    3

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
    bool isvalid(TreeNode* left, TreeNode* right)
    {
        if(left == NULL && right == NULL) return true;
        else if(left == NULL || right == NULL) return false;
        else if(left->val != right-> val) return false;
        else
        {
            return isvalid(left->left, right->right) && isvalid(left->right, right->left);
        }
    }

    bool isSymmetric(TreeNode* root) {
        if(root == NULL) return true;
        return isvalid(root->left, root->right);
    }
```

迭代法

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
    bool isvalid(TreeNode* left, TreeNode* right)
    {
        if(left == NULL && right == NULL) return true;
        else if(left == NULL || right == NULL) return false;
        else if(left->val != right-> val) return false;
        else
        {
            return isvalid(left->left, right->right) && isvalid(left->right, right->left);
        }
    }

    bool isSymmetric(TreeNode* root) {
        if(root == NULL) return true;
        queue<TreeNode*> que;

        que.push(root->left);
        que.push(root->right);

        while(!que.empty())
        {
            TreeNode* left = que.front();
            que.pop();
            TreeNode* right = que.front();
            que.pop();
            
            if(left == NULL && right == NULL) continue;
            else if(left == NULL || right == NULL) return false;
            else if(left->val != right-> val) return false;
            else
            {
                que.push(left->left);
                que.push(right->right);

                que.push(left->right);
                que.push(right->left);
            }
            
            
        }
        return true;

    }
};
```

## [剑指 Offer 21. 调整数组顺序使奇数位于偶数前面](https://leetcode-cn.com/problems/diao-zheng-shu-zu-shun-xu-shi-qi-shu-wei-yu-ou-shu-qian-mian-lcof/)

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有奇数位于数组的前半部分，所有偶数位于数组的后半部分。

```c++
class Solution {
public:
    vector<int> exchange(vector<int>& nums) {
        if(nums.size() == 0) return nums;

        int left = 0;
        int right = nums.size() - 1;

        while(left < right)
        {
            while(left < right && nums[left] % 2 == 1)
            {
                left++;
            }
            while(left < right && nums[right] % 2 == 0)
            {
                right--;
            }

            swap(nums[left], nums[right]);
            left++;
            right--;
        }

        return nums;
    }
};
```

#### **[剑指 Offer 15. 二进制中1的个数](https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/)

编写一个函数，输入是一个无符号整数（以二进制串的形式），返回其二进制表达式中数字位数为 '1' 的个数（也被称为 汉明重量).）。

 

提示：

请注意，在某些语言（如 Java）中，没有无符号整数类型。在这种情况下，输入和输出都将被指定为有符号整数类型，并且不应影响您的实现，因为无论整数是有符号的还是无符号的，其内部的二进制表示形式都是相同的。
在 Java 中，编译器使用 二进制补码 记法来表示有符号整数。因此，在上面的 示例 3 中，输入表示有符号整数 -3。

```c++
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int ans = 0;
        while(n)
        {
            ans++;
            n &= (n - 1);
        }

        return ans;
    }
};
```

## [剑指 Offer 29. 顺时针打印矩阵](https://leetcode-cn.com/problems/shun-shi-zhen-da-yin-ju-zhen-lcof/)

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字。

```c++
class Solution {
public:
    vector<int> spiralOrder(vector<vector<int>>& matrix) {
        if(matrix.size() == 0 || matrix[0].size() == 0) return {};

        int m = matrix.size() - 1;
        int n = matrix[0].size() - 1;

        int cnt = 0;
        int flag = 0;
        vector<int> ans;
        while(cnt < (m + 1) * (n + 1) - 1)
        {
            for(int j = flag; j < n - flag && cnt < (m + 1) * (n + 1); j++)
            {
                ans.push_back(matrix[flag][j]);
                cnt++;
            }

            for(int i = flag; i < m - flag && cnt < (m + 1) * (n + 1); i++)
            {
                ans.push_back(matrix[i][n - flag]);
                cnt++;
            }
            for(int j = n - flag; j > flag && cnt < (m + 1) * (n + 1); j--)
            {
                ans.push_back(matrix[m - flag][j]);
                cnt++;
            }

            for(int i = m - flag; i > flag && cnt < (m + 1) * (n + 1); i--)
            {
                ans.push_back(matrix[i][flag]);
                cnt++;
            }

            flag++;
            
        }


        if(m == n && m % 2 == 0)
        {
            ans.push_back(matrix[m / 2][m / 2]);
        }
        return ans;
    }
};
```

## [剑指 Offer 22. 链表中倒数第k个节点](https://leetcode-cn.com/problems/lian-biao-zhong-dao-shu-di-kge-jie-dian-lcof/)

输入一个链表，输出该链表中倒数第k个节点。为了符合大多数人的习惯，本题从1开始计数，即链表的尾节点是倒数第1个节点。

例如，一个链表有 6 个节点，从头节点开始，它们的值依次是 1、2、3、4、5、6。这个链表的倒数第 3 个节点是值为 4 的节点。

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
    ListNode* getKthFromEnd(ListNode* head, int k) {
        ListNode* fast = head;
        while(k--)
        {
            fast = fast->next;
        }

        ListNode* cur = head;

        while(fast)
        {
            cur = cur->next;
            fast = fast->next;
        }

        return cur;
    }
};
```

## [剑指 Offer 17. 打印从1到最大的n位数](https://leetcode-cn.com/problems/da-yin-cong-1dao-zui-da-de-nwei-shu-lcof/)

输入数字 `n`，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。

```c++
class Solution {
public:
    vector<int> printNumbers(int n) {
        vector<int> ans;

        for(int i = 1; i < pow(10, n); i++)
        {
            ans.push_back(i);
        }

        return ans;
    }
};
```

## [剑指 Offer 24. 反转链表](https://leetcode-cn.com/problems/fan-zhuan-lian-biao-lcof/)

定义一个函数，输入一个链表的头节点，反转该链表并输出反转后链表的头节点。

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
    ListNode* reverseList(ListNode* head) {
        ListNode* pre = NULL;
        ListNode* cur = head;

        while(cur)
        {
            ListNode* tmp = cur->next;

            cur->next = pre;
            pre = cur;
            cur = tmp;
        }

        return pre;
    }
};
```

## **[剑指 Offer 18. 删除链表的节点](https://leetcode-cn.com/problems/shan-chu-lian-biao-de-jie-dian-lcof/)

给定单向链表的头指针和一个要删除的节点的值，定义一个函数删除该节点。

返回删除后的链表的头节点。

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
    ListNode* deleteNode(ListNode* head, int val) {
        ListNode* dummy = new ListNode(0);
        dummy->next = head;
        ListNode* cur = dummy;

        while(cur->next)
        {
            if(cur->next->val == val)
            {
                ListNode* tmp = cur->next;
                cur->next = cur->next->next;
            }
            else
            {
                cur = cur->next;
            }     
        }

        return dummy->next;
    }
};
```

## [剑指 Offer 38. 字符串的排列](https://leetcode-cn.com/problems/zi-fu-chuan-de-pai-lie-lcof/)

输入一个字符串，打印出该字符串中字符的所有排列。

 

你可以以任意顺序返回这个字符串数组，但里面不能有重复元素。

```c++
class Solution {
public:
    vector<string> ans;
    string path;

    void backtracking(string s, vector<bool>& used)
    {
        if(path.size() == s.size())
        {
            ans.push_back(path);
            return;
        }

        for(int i = 0; i < s.size(); i++)
        {
            if(used[i] == true) continue;
            if(i > 0 && s[i] == s[i - 1] && used[i - 1] == false) continue;

            path.push_back(s[i]);
            used[i] = true;
            backtracking(s, used);
            used[i] = false;
            path.pop_back();
        }
    }

    vector<string> permutation(string s) {
        vector<bool> used(s.size(), false);
        sort(s.begin(), s.end());
        backtracking(s, used);

        return ans;
    }
};
```

## [剑指 Offer 39. 数组中出现次数超过一半的数字](https://leetcode-cn.com/problems/shu-zu-zhong-chu-xian-ci-shu-chao-guo-yi-ban-de-shu-zi-lcof/)

数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。

 

你可以假设数组是非空的，并且给定的数组总是存在多数元素。

```c++
class Solution {
public:
    int majorityElement(vector<int>& nums) {
        int ans;

        int cnt = 0;

        for(int i = 0; i < nums.size(); i++)
        {
            if(cnt == 0)
            {
                ans = nums[i];
            }
            if(ans == nums[i])
            {
                cnt++;
            }
            else
            {
                cnt--;
            }
        }
        return ans;
    }
};
```

## [剑指 Offer 32 - I. 从上到下打印二叉树](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-lcof/)

从上到下打印出二叉树的每个节点，同一层的节点按照从左到右的顺序打印。

 

例如:
给定二叉树: `[3,9,20,null,null,15,7]`,

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
    vector<int> levelOrder(TreeNode* root) {
        queue<TreeNode*> que;
        if(root) que.push(root);
        vector<int> ans;

        while(!que.empty())
        {
            TreeNode* node = que.front();
            que.pop();
            ans.push_back(node->val);

            if(node->left) que.push(node->left);
            if(node->right) que.push(node->right);
        }

        return ans;
    }
};
```

## [剑指 Offer 32 - II. 从上到下打印二叉树 II](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-ii-lcof/)

从上到下按层打印二叉树，同一层的节点按从左到右的顺序打印，每一层打印到一行。

 

例如:
给定二叉树: [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：

[
  [3],
  [9,20],
  [15,7]
]

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
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> ans;

        queue<TreeNode*> que;
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

## [剑指 Offer 32 - III. 从上到下打印二叉树 III](https://leetcode-cn.com/problems/cong-shang-dao-xia-da-yin-er-cha-shu-iii-lcof/)

请实现一个函数按照之字形顺序打印二叉树，即第一行按照从左到右的顺序打印，第二层按照从右到左的顺序打印，第三行再按照从左到右的顺序打印，其他行以此类推。

 

例如:
给定二叉树: [3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
返回其层次遍历结果：

[
  [3],
  [20,9],
  [15,7]
]

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
    vector<vector<int>> levelOrder(TreeNode* root) {
        vector<vector<int>> ans;
        queue<TreeNode*> que;
        if(root) que.push(root);
        int flag = 0;

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

            flag++;
            if(flag % 2 == 0)
            {
                reverse(min_ans.begin(), min_ans.end());
            }
            ans.push_back(min_ans);
        }

        return ans;

    }
};
```

## **[剑指 Offer 33. 二叉搜索树的后序遍历序列](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-hou-xu-bian-li-xu-lie-lcof/)

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历结果。如果是则返回 `true`，否则返回 `false`。假设输入的数组的任意两个数字都互不相同。

```c++
class Solution {
public:
    bool isvalid(vector<int>& postorder, int begin, int end)
    {
        if(begin >= end) return true;
        int p = begin;

        while(postorder[p] < postorder[end - 1]) p++;
        int m = p;
        while(postorder[m] > postorder[end - 1]) m++;

        return m == end - 1 && isvalid(postorder, begin, p) && isvalid(postorder, p, end - 1);
        
    }


    bool verifyPostorder(vector<int>& postorder) {
        if(postorder.size() == 0) return true;

        return isvalid(postorder, 0, postorder.size());
    }
};
```

## [剑指 Offer 50. 第一个只出现一次的字符](https://leetcode-cn.com/problems/di-yi-ge-zhi-chu-xian-yi-ci-de-zi-fu-lcof/)

在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

```c++
class Solution {
public:
    char firstUniqChar(string s) {
        unordered_map<char, int> map;

        for(int i = 0; i < s.size(); i++)
        {
            map[s[i]]++;
        }
        char ans;
        for(int i = 0; i < s.size(); i++)
        {
            if(map[s[i]] == 1)
            {
                return s[i];
            }
        }

        return ' ';

    }
};
```

## [剑指 Offer 34. 二叉树中和为某一值的路径](https://leetcode-cn.com/problems/er-cha-shu-zhong-he-wei-mou-yi-zhi-de-lu-jing-lcof/)

输入一棵二叉树和一个整数，打印出二叉树中节点值的和为输入整数的所有路径。从树的根节点开始往下一直到叶节点所经过的节点形成一条路径。

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
    vector<vector<int>> ans;
    vector<int> path;

    void backtracking(TreeNode* node, int target)
    {
        if(node == nullptr) return;

        path.push_back(node->val);
        target -= node->val;

        if(target == 0 && node->left == nullptr && node->right == nullptr)
        {
            ans.push_back(path);
        }

        backtracking(node->left, target);
        backtracking(node->right, target);
        path.pop_back();
    }

    vector<vector<int>> pathSum(TreeNode* root, int target) {
        backtracking(root, target);
        return ans;
    }
};
```

## [剑指 Offer 55 - I. 二叉树的深度](https://leetcode-cn.com/problems/er-cha-shu-de-shen-du-lcof/)

输入一棵二叉树的根节点，求该树的深度。从根节点到叶节点依次经过的节点（含根、叶节点）形成树的一条路径，最长路径的长度为树的深度。

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
    int maxDepth(TreeNode* root) {
        if(root == NULL) return 0;
        int left = maxDepth(root->left);
        int right = maxDepth(root->right);

        return max(left, right) + 1;
    }
};
```

## [剑指 Offer 57. 和为s的两个数字](https://leetcode-cn.com/problems/he-wei-sde-liang-ge-shu-zi-lcof/)

输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。

```c++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        int i = 0;
        int j = nums.size() - 1;
        vector<int> ans;
        while(i < j)
        {
            if(nums[i] + nums[j] > target) j--;
            else if(nums[i] + nums[j] < target) i++;
            else
            {
                ans = {nums[i], nums[j]};
                return ans;
            }
        }
        return {};
    }
};
```

## **[剑指 Offer 45. 把数组排成最小的数](https://leetcode-cn.com/problems/ba-shu-zu-pai-cheng-zui-xiao-de-shu-lcof/)

输入一个非负整数数组，把数组里所有数字拼接起来排成一个数，打印能拼接出的所有数字中最小的一个。

 

```c++
class Solution {
public:
    static bool cmp(string& a, string& b)
    {
        return a + b < b + a;
    }

    string minNumber(vector<int>& nums) {
        vector<string> vec;
        for(int num : nums) vec.push_back(to_string(num));

        sort(vec.begin(), vec.end(), cmp);
        string ans;
        for(string s : vec) ans += s;

        return ans;
    }
};
```

## [剑指 Offer 57 - II. 和为s的连续正数序列](https://leetcode-cn.com/problems/he-wei-sde-lian-xu-zheng-shu-xu-lie-lcof/)

输入一个正整数 target ，输出所有和为 target 的连续正整数序列（至少含有两个数）。

序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。

```c++
class Solution {
public:
    vector<vector<int>> findContinuousSequence(int target) {
        vector<vector<int>> ans;
        vector<int> path;

        for(int i = 1, j = 2; i < j;)
        {
            int sum = (i + j) * (j - i + 1) / 2;
            if(sum < target) j++;
            else if(sum > target) i++;
            else
            {
                path.clear();
                for(int k = i; k <= j; k++)
                {
                    path.push_back(k);
                }
                ans.push_back(path);
                j++;
            }
        }

        return ans;

    }
};
```

## [剑指 Offer 46. 把数字翻译成字符串](https://leetcode-cn.com/problems/ba-shu-zi-fan-yi-cheng-zi-fu-chuan-lcof/)

给定一个数字，我们按照如下规则把它翻译为字符串：0 翻译成 “a” ，1 翻译成 “b”，……，11 翻译成 “l”，……，25 翻译成 “z”。一个数字可能有多个翻译。请编程实现一个函数，用来计算一个数字有多少种不同的翻译方法。

```c++
class Solution {
public:
    int ans = 0;

    void backtracking(string s, int startIndex)
    {
        if(startIndex == s.size())
        {
            ans++;
            return;
        }

        for(int i = startIndex; i < s.size(); i++)
        {
            string min_s = s.substr(startIndex, i - startIndex + 1);
            if(min_s.size() > 2) break;
            else if(min_s.size() == 2 && min_s[0] == '0') break;
            else if(stoi(min_s) >= 0 && stoi(min_s) <= 25)
            {
                backtracking(s, i + 1);
            }

        }
    }

    int translateNum(int num) {
        string s = to_string(num);
        backtracking(s, 0);

        return ans;
    }
};
```

```c++
class Solution {
public:
    int translateNum(int num) {
        string s = to_string(num);

        vector<int> dp(s.size() + 1, 1);
        
        for(int i = 2; i <= s.size(); i++)
        {
            if(s[i - 2] == '1' || (s[i - 2] == '2' && s[i - 1] < '6'))
            {
                dp[i] = dp[i - 1] + dp[i - 2];
            }
            else
            {
                dp[i] = dp[i - 1];
            }
        }

        return dp[s.size()];
    }
};
```

## [剑指 Offer 52. 两个链表的第一个公共节点](https://leetcode-cn.com/problems/liang-ge-lian-biao-de-di-yi-ge-gong-gong-jie-dian-lcof/)

输入两个链表，找出它们的第一个公共节点。

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
        ListNode* curA = headA;
        ListNode* curB = headB;

        while(curA != curB)
        {
            if(curA == NULL) curA = headB;
            else curA = curA->next;
            if(curB == NULL) curB = headA;
            else curB = curB->next;
        }

        return curA;
    }
};
```

## [剑指 Offer 47. 礼物的最大价值](https://leetcode-cn.com/problems/li-wu-de-zui-da-jie-zhi-lcof/)

在一个 m*n 的棋盘的每一格都放有一个礼物，每个礼物都有一定的价值（价值大于 0）。你可以从棋盘的左上角开始拿格子里的礼物，并每次向右或者向下移动一格、直到到达棋盘的右下角。给定一个棋盘及其上面的礼物的价值，请计算你最多能拿到多少价值的礼物？

```c++
class Solution {
public:
    int maxValue(vector<vector<int>>& grid) {
        for(int i = 1; i < grid[0].size(); i++)
        {
            grid[0][i] += grid[0][i - 1];
        }

        for(int i = 1; i < grid.size(); i++)
        {
            grid[i][0] += grid[i - 1][0];
        }

        for(int i = 1; i < grid.size(); i++)
        {
            for(int j = 1; j < grid[0].size(); j++)
            {
                grid[i][j] = max(grid[i - 1][j], grid[i][j - 1]) + grid[i][j];
            }
        }

        return grid[grid.size() - 1][grid[0].size() - 1];
    }
};
```

## [剑指 Offer 58 - I. 翻转单词顺序](https://leetcode-cn.com/problems/fan-zhuan-dan-ci-shun-xu-lcof/)

输入一个英文句子，翻转句子中单词的顺序，但单词内字符的顺序不变。为简单起见，标点符号和普通字母一样处理。例如输入字符串"I am a student. "，则输出"student. a am I"。

```c++
class Solution {
public:
    string reverseWords(string s) {
        vector<string> vec;
        string path;

        for(int i = 0; i < s.size(); i++)
        {
            if(s[i] == ' ' && path.size() > 0)
            {
                vec.push_back(path);
                path.clear();
            }
            else if(s[i] == ' ')
            {
                continue;
            }
            else
            {
                path.push_back(s[i]);
            }
        }
        if(path.size() > 0) vec.push_back(path);

        string ans;
        for(int i = vec.size() - 1; i > 0; i--)
        {
            ans += vec[i];
            ans.push_back(' ');
        }

        if(vec.size() > 0) ans += vec[0];
        return ans;
    }
};
```

## **[剑指 Offer 53 - I. 在排序数组中查找数字 I](https://leetcode-cn.com/problems/zai-pai-xu-shu-zu-zhong-cha-zhao-shu-zi-lcof/)

统计一个数字在排序数组中出现的次数。

```c++
class Solution {
public:
    int search(vector<int>& nums, int target) {
        int left = 0;
        int right = nums.size() - 1;

        while(left <= right)
        {
            int mid = left + (right - left) / 2;

            if(nums[mid] < target) left = mid + 1;
            else right = mid - 1;
        }

        int oldleft = left;
        left = 0;
        right = nums.size() - 1;

        while(left <= right)
        {
            int mid = left + (right - left) / 2;
            if(nums[mid] > target) right = mid - 1;
            else left = mid + 1;
        }
        return right - oldleft + 1;
    }
};
```

## [剑指 Offer 58 - II. 左旋转字符串](https://leetcode-cn.com/problems/zuo-xuan-zhuan-zi-fu-chuan-lcof/)

字符串的左旋转操作是把字符串前面的若干个字符转移到字符串的尾部。请定义一个函数实现字符串左旋转操作的功能。比如，输入字符串"abcdefg"和数字2，该函数将返回左旋转两位得到的结果"cdefgab"。

```c++
class Solution {
public:
    string reverseLeftWords(string s, int n) {
        reverse(s.begin(), s.begin() + n);
        reverse(s.begin() + n, s.end());
        reverse(s.begin(), s.end());
        return s;
    }
};
```

## [剑指 Offer 53 - II. 0～n-1中缺失的数字](https://leetcode-cn.com/problems/que-shi-de-shu-zi-lcof/)

一个长度为n-1的递增排序数组中的所有数字都是唯一的，并且每个数字都在范围0～n-1之内。在范围0～n-1内的n个数字中有且只有一个数字不在该数组中，请找出这个数字。

 

```c++
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int left = 0;
        int right = nums.size() - 1;

        while(left <= right)
        {
            int mid = left + (right - left) / 2;
            if(mid == nums[mid])
            {
                left = mid + 1;
            }
            else
            {
                right = mid - 1;
            }
        }
        return left;
    }
};
```

## [剑指 Offer 48. 最长不含重复字符的子字符串](https://leetcode-cn.com/problems/zui-chang-bu-han-zhong-fu-zi-fu-de-zi-zi-fu-chuan-lcof/)

请从字符串中找出一个最长的不包含重复字符的子字符串，计算该最长子字符串的长度。

```c++
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char, int> map;
        int ans = 0;
        int tmp = 0;

        for(int i = 0; i < s.size(); i++)
        {
            int index = -1;
            if(map.count(s[i]))
            {
                index = map[s[i]];
            }
            map[s[i]] = i;
            tmp = tmp < i - index ? tmp + 1 : i - index;
            ans = max(ans, tmp);
        }

        return ans;
    }
};
```

## [剑指 Offer 54. 二叉搜索树的第k大节点](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-di-kda-jie-dian-lcof/)

给定一棵二叉搜索树，请找出其中第k大的节点。

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
    int ans;
    void inorder(TreeNode* root, int& k)
    {
        if(root == NULL) return;
        inorder(root->right, k);
        k--;
        if(k == 0) ans = root->val;

        inorder(root->left, k);

    }

    int kthLargest(TreeNode* root, int k) {
        inorder(root, k);

        return ans;
    }
};
```

## [剑指 Offer 49. 丑数](https://leetcode-cn.com/problems/chou-shu-lcof/)

我们把只包含质因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。

```c++
class Solution {
public:
    int nthUglyNumber(int n) {
        vector<int> dp(n + 1, 0);
        dp[1] = 1;
        int n2 = 1, n3 = 1, n5 = 1;

        for(int i = 2; i <= n; i++)
        {
            int t2 = dp[n2] * 2, t3 = dp[n3] * 3, t5 = dp[n5] * 5;

            dp[i] = min(t2, min(t3, t5));
            if(dp[i] == t2) n2++;
            if(dp[i] == t3) n3++;
            if(dp[i] == t5) n5++;
        }

        return dp[n];
    }
};
```

## **[剑指 Offer 66. 构建乘积数组](https://leetcode-cn.com/problems/gou-jian-cheng-ji-shu-zu-lcof/)

给定一个数组 A[0,1,…,n-1]，请构建一个数组 B[0,1,…,n-1]，其中 B[i] 的值是数组 A 中除了下标 i 以外的元素的积, 即 B[i]=A[0]×A[1]×…×A[i-1]×A[i+1]×…×A[n-1]。不能使用除法。

```c++
class Solution {
public:
    vector<int> constructArr(vector<int>& a) {
        vector<int> b(a.size(), 1);

        for(int i = 1; i < a.size(); i++)
        {
            b[i] = b[i - 1] * a[i - 1];
        }

        int tmp = 1;
        for(int i = a.size() - 2; i >= 0; i--)
        {
            tmp *= a[i + 1];
            b[i] *= tmp;
        }

        return b;
    }
};
```

## [剑指 Offer 60. n个骰子的点数](https://leetcode-cn.com/problems/nge-tou-zi-de-dian-shu-lcof/)

把n个骰子扔在地上，所有骰子朝上一面的点数之和为s。输入n，打印出s的所有可能的值出现的概率。

 

你需要用一个浮点数数组返回答案，其中第 i 个元素代表这 n 个骰子所能掷出的点数集合中第 i 小的那个的概率。

```c++
class Solution {
public:
    vector<double> dicesProbability(int n) {
        vector<vector<int>> dp(n + 1, vector<int>(73, 0));

        for(int i = 1; i < 7; i++)
        {
            dp[1][i] = 1;
        }

        for(int i = 1; i <= n; i++)
        {
            for(int j = 1; j <= 6 * n; j++)
            {
                for(int k = 1; k < 7; k++)
                {
                    if(j > k)
                    {
                        dp[i][j] += dp[i - 1][j - k]; 
                    }
                }
            }
        }

        vector<double> ans;
        for(int i = n; i <= 6 * n; i++)
        {
            ans.push_back(1.0 * dp[n][i] / pow(6, n));
        }

        return ans;
    }
};
```

## **[剑指 Offer 67. 把字符串转换成整数](https://leetcode-cn.com/problems/ba-zi-fu-chuan-zhuan-huan-cheng-zheng-shu-lcof/)

写一个函数 StrToInt，实现把字符串转换成整数这个功能。不能使用 atoi 或者其他类似的库函数。

 

首先，该函数会根据需要丢弃无用的开头空格字符，直到寻找到第一个非空格的字符为止。

当我们寻找到的第一个非空字符为正或者负号时，则将该符号与之后面尽可能多的连续数字组合起来，作为该整数的正负号；假如第一个非空字符是数字，则直接将其与之后连续的数字字符组合起来，形成整数。

该字符串除了有效的整数部分之后也可能会存在多余的字符，这些字符可以被忽略，它们对于函数不应该造成影响。

注意：假如该字符串中的第一个非空格字符不是一个有效整数字符、字符串为空或字符串仅包含空白字符时，则你的函数不需要进行转换。

在任何情况下，若函数不能进行有效的转换时，请返回 0。

说明：

假设我们的环境只能存储 32 位大小的有符号整数，那么其数值范围为 [−231,  231 − 1]。如果数值超过这个范围，请返回  INT_MAX (231 − 1) 或 INT_MIN (−231) 。

```c++
class Solution {
public:
    int strToInt(string str) {
        int flag = 1;
        int boundry = INT_MAX / 10;
        int i = 0;
        while(str[i] == ' ')
        {
            i++;
            if(i == str.size()) return 0;
        }

        if(str[i] == '-')
        {
            flag = -1;
            i++;
        }
        int ans = 0;
        while(i < str.size())
        {
            if(str[i] < '0' || str[i] > '9') break;
            if(ans > boundry || (ans == boundry && str[i] > '7'))
            {
                return flag == 1 ? INT_MAX : INT_MIN;
            }

            ans = ans * 10 + str[i] - '0';
            i++;
        }
        return ans;
    }
};
```

## [剑指 Offer 61. 扑克牌中的顺子](https://leetcode-cn.com/problems/bu-ke-pai-zhong-de-shun-zi-lcof/)

从扑克牌中随机抽5张牌，判断是不是一个顺子，即这5张牌是不是连续的。2～10为数字本身，A为1，J为11，Q为12，K为13，而大、小王为 0 ，可以看成任意数字。A 不能视为 14。

```c++
class Solution {
public:
    bool isStraight(vector<int>& nums) {
        unordered_set<int> set;

        int max_n = 0, min_n = 14;

        for(int num : nums)
        {
            if(num == 0) continue;

            max_n = max(max_n, num);
            min_n = min(min_n, num);

            if(set.find(num) != set.end()) return false;
            set.insert(num);
        }

        return max_n - min_n < 5;
    }
};
```

## [剑指 Offer 55 - II. 平衡二叉树](https://leetcode-cn.com/problems/ping-heng-er-cha-shu-lcof/)

输入一棵二叉树的根节点，判断该树是不是平衡二叉树。如果某二叉树中任意节点的左右子树的深度相差不超过1，那么它就是一棵平衡二叉树。

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
    int getDepth(TreeNode* node)
    {
        if(node == NULL) return 0;
        int left = getDepth(node->left);
        int right = getDepth(node->right);

        return max(left, right) + 1;
    }

    bool isBalanced(TreeNode* root) {
        if(root == NULL) return true;
        int left = getDepth(root->left);
        int right = getDepth(root->right);

        return abs(left - right) <= 1 && isBalanced(root->left) && isBalanced(root->right);
    }
};
```

## [剑指 Offer 63. 股票的最大利润](https://leetcode-cn.com/problems/gu-piao-de-zui-da-li-run-lcof/)

假设把某股票的价格按照时间先后顺序存储在数组中，请问买卖该股票一次可能获得的最大利润是多少？

```c++
class Solution {
public:
    int maxProfit(vector<int>& prices) {
        if(prices.size() == 0) return 0;
        vector<vector<int>> dp(prices.size(), vector<int>(2, 0));
        dp[0][0] = -prices[0];
        for(int i = 1; i < prices.size(); i++)
        {
            dp[i][0] = max(dp[i - 1][0], -prices[i]);
            dp[i][1] = max(dp[i - 1][1], dp[i - 1][0] + prices[i]);
        }

        return dp[prices.size() - 1][1];
    }
};
```

## [剑指 Offer 64. 求1+2+…+n](https://leetcode-cn.com/problems/qiu-12n-lcof/)

求 `1+2+...+n` ，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

```c++
class Solution {
public:
    int sumNums(int n) {
        bool a[n][n + 1];
        return sizeof(a) >> 1;
    }
};
```

## [剑指 Offer 68 - I. 二叉搜索树的最近公共祖先](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-de-zui-jin-gong-gong-zu-xian-lcof/)

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
            if(node->val < p->val && node->val < q->val)
            {
                node = node->right;
            }
            else if(node->val > p->val && node->val > q->val)
            {
                node = node->left;
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

## [剑指 Offer 68 - II. 二叉树的最近公共祖先](https://leetcode-cn.com/problems/er-cha-shu-de-zui-jin-gong-gong-zu-xian-lcof/)

给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

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
        if(root == NULL) return NULL;
        if(root->val == q->val || root->val == p->val) return root;
        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);

        if(left == NULL && right == NULL) return NULL;
        else if(left == NULL) return right;
        else if(right == NULL) return left;
        else return root;
    }
};
```

## [剑指 Offer 15. 二进制中1的个数](https://leetcode-cn.com/problems/er-jin-zhi-zhong-1de-ge-shu-lcof/)

编写一个函数，输入是一个无符号整数（以二进制串的形式），返回其二进制表达式中数字位数为 '1' 的个数（也被称为 [汉明重量](http://en.wikipedia.org/wiki/Hamming_weight)).）。

```c++
class Solution {
public:
    int hammingWeight(uint32_t n) {
        int ans = 0;
        while(n)
        {
            n &= (n - 1);
            ans++;
        }

        return ans;
    }
};
```

## [剑指 Offer 16. 数值的整数次方](https://leetcode-cn.com/problems/shu-zhi-de-zheng-shu-ci-fang-lcof/)

实现 [pow(*x*, *n*)](https://www.cplusplus.com/reference/valarray/pow/) ，即计算 x 的 n 次幂函数（即，xn）。不得使用库函数，同时不需要考虑大数问题。

```c++
class Solution {
public:
    double myPow(double x, int n) {
        if(n < 0) x = 1 / x;
        n = abs(n);

        double ans = 1.0;

        while(n > 0)
        {
            if(n % 2 == 1)
            {
                ans *= x;
            }
            x *= x;
            n /= 2;
        }
        return ans;
    }
};
```

## **[剑指 Offer 19. 正则表达式匹配](https://leetcode-cn.com/problems/zheng-ze-biao-da-shi-pi-pei-lcof/)

请实现一个函数用来匹配包含'. '和'*'的正则表达式。模式中的字符'.'表示任意一个字符，而'*'表示它前面的字符可以出现任意次（含0次）。在本题中，匹配是指字符串的所有字符匹配整个模式。例如，字符串"aaa"与模式"a.a"和"ab*ac*a"匹配，但与"aa.a"和"ab*a"均不匹配。

```c++
class Solution {
public:
    bool isMatch(string s, string p) {
        vector<vector<bool>> dp(s.size() + 1, vector<bool>(p.size() + 1, false));
        dp[0][0] = true;
        for(int i = 1; i <= p.size(); i++)
        {
            if(i > 1 && p[i - 1] == '*' && dp[0][i - 2] == true)
            {
                dp[0][i] = true;
            }
        }

        for(int i = 1; i <= s.size(); i++)
        {
            for(int j = 1; j <= p.size(); j++)
            {
                if(s[i - 1] == p[j - 1] || p[j - 1] == '.')
                {
                    dp[i][j] = dp[i - 1][j - 1];
                }
                else if(p[j - 1] == '*' && j > 1)
                {
                    if(s[i - 1] != p[j - 2] && p[j - 2] != '.')
                    {
                        dp[i][j] = dp[i][j - 2];
                    }
                    else
                    {
                        dp[i][j] = dp[i][j - 1] || dp[i][j - 2] || dp[i - 1][j];
                    }
                }
                else
                {
                    dp[i][j] = false;
                }
            }
        }

        return dp[s.size()][p.size()];
    }
};
```

## [剑指 Offer 35. 复杂链表的复制](https://leetcode-cn.com/problems/fu-za-lian-biao-de-fu-zhi-lcof/)

请实现 copyRandomList 函数，复制一个复杂链表。在复杂链表中，每个节点除了有一个 next 指针指向下一个节点，还有一个 random 指针指向链表中的任意节点或者 null。

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* next;
    Node* random;
    
    Node(int _val) {
        val = _val;
        next = NULL;
        random = NULL;
    }
};
*/
class Solution {
public:
    Node* copyRandomList(Node* head) {
        unordered_map<Node*, Node*> map;
        Node* cur = head;

        while(cur)
        {
            map[cur] = new Node(cur->val);
            cur = cur->next;
        }

        cur = head;
        while(cur)
        {
            map[cur]->next = map[cur->next];
            map[cur]->random = map[cur->random];
            cur = cur->next;
        }

        return map[head];
    }
};
```

## [剑指 Offer 40. 最小的k个数](https://leetcode-cn.com/problems/zui-xiao-de-kge-shu-lcof/)

输入整数数组 `arr` ，找出其中最小的 `k` 个数。例如，输入4、5、1、6、2、7、3、8这8个数字，则最小的4个数字是1、2、3、4。

```c++
class Solution {
public:
    vector<int> getLeastNumbers(vector<int>& arr, int k) {
        vector<int> ans;

        priority_queue<int, vector<int>, greater<int>> q;

        for(int num : arr)
        {
            q.push(num);
        }

        for(int i = 0; i < k; i++)
        {
            ans.push_back(q.top());
            q.pop();
        }
        return ans;
    }
};
```

## [剑指 Offer 30. 包含min函数的栈](https://leetcode-cn.com/problems/bao-han-minhan-shu-de-zhan-lcof/)

定义栈的数据结构，请在该类型中实现一个能够得到栈的最小元素的 min 函数在该栈中，调用 min、push 及 pop 的时间复杂度都是 O(1)。

```c++
class MinStack {
public:
    /** initialize your data structure here. */

    stack<int> a;
    stack<int> b;
    MinStack() {

    }
    
    void push(int x) {
        a.push(x);
        if(b.empty() || b.top() >= x)
        {
            b.push(x);
        }
    }
    
    void pop() {
        if(a.top() == b.top()) b.pop();
        a.pop();
    }
    
    int top() {
        return a.top();
    }
    
    int min() {
        return b.top();
    }
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(x);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->min();
 */
```

## [剑指 Offer 41. 数据流中的中位数](https://leetcode-cn.com/problems/shu-ju-liu-zhong-de-zhong-wei-shu-lcof/)

如何得到一个数据流中的中位数？如果从数据流中读出奇数个数值，那么中位数就是所有数值排序之后位于中间的数值。如果从数据流中读出偶数个数值，那么中位数就是所有数值排序之后中间两个数的平均值。

例如，

[2,3,4] 的中位数是 3

[2,3] 的中位数是 (2 + 3) / 2 = 2.5

设计一个支持以下两种操作的数据结构：

void addNum(int num) - 从数据流中添加一个整数到数据结构中。
double findMedian() - 返回目前所有元素的中位数。

```c++
class MedianFinder {
public:
    /** initialize your data structure here. */
    priority_queue<int, vector<int>, less<int>> max_q;
    priority_queue<int, vector<int>, greater<int>> min_q;
    MedianFinder() {

    }
    
    void addNum(int num) {
        if(max_q.size() == min_q.size())
        {
            min_q.push(num);
            max_q.push(min_q.top());
            min_q.pop();
        }
        else
        {
            max_q.push(num);
            min_q.push(max_q.top());
            max_q.pop();
        }
    }
    
    double findMedian() {
        if(max_q.size() == min_q.size()) return (max_q.top() + min_q.top()) / 2.0;
        else return max_q.top();
    }
};

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder* obj = new MedianFinder();
 * obj->addNum(num);
 * double param_2 = obj->findMedian();
 */
```

## [剑指 Offer 42. 连续子数组的最大和](https://leetcode-cn.com/problems/lian-xu-zi-shu-zu-de-zui-da-he-lcof/)

输入一个整型数组，数组中的一个或连续多个整数组成一个子数组。求所有子数组的和的最大值。

要求时间复杂度为O(n)。

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        int ans = INT_MIN;
        int cur = 0;
        for(int i = 0; i < nums.size(); i++)
        {
            cur += nums[i];
            ans = max(ans, cur);
            if(cur < 0)
            {
                cur = 0;
            }
        }
        return ans;
    }
};
```

```c++
class Solution {
public:
    int maxSubArray(vector<int>& nums) {
        vector<int> dp(nums.size(), 0);
        dp[0] = nums[0];
        int ans = nums[0];
        for(int i = 1; i < nums.size(); i++)
        {
            dp[i] = max(dp[i - 1] + nums[i], nums[i]);
            ans = max(ans, dp[i]);
        }
        return ans;

    }
};
```

## [剑指 Offer 36. 二叉搜索树与双向链表](https://leetcode-cn.com/problems/er-cha-sou-suo-shu-yu-shuang-xiang-lian-biao-lcof/)

输入一棵二叉搜索树，将该二叉搜索树转换成一个排序的循环双向链表。要求不能创建任何新的节点，只能调整树中节点指针的指向。

```c++
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;

    Node() {}

    Node(int _val) {
        val = _val;
        left = NULL;
        right = NULL;
    }

    Node(int _val, Node* _left, Node* _right) {
        val = _val;
        left = _left;
        right = _right;
    }
};
*/
class Solution {
public:
    Node* pre = NULL;

    void inorder(Node* node)
    {
        if(node == NULL) return ;
        inorder(node->left);
        if(pre != NULL)
        {
            node->left = pre;
            pre->right = node;
            pre = node;
        }
        else
        {
            pre = node;
        }
        inorder(node->right);
    }

    Node* treeToDoublyList(Node* root) {
        if(root == NULL) return root;
        Node* head = root;
        while(head->left)
        {
            head = head->left;
        }

        inorder(root);

        head->left = pre;
        pre->right = head;
        return head;

    }
};
```

## [剑指 Offer 31. 栈的压入、弹出序列](https://leetcode-cn.com/problems/zhan-de-ya-ru-dan-chu-xu-lie-lcof/)

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如，序列 {1,2,3,4,5} 是某栈的压栈序列，序列 {4,5,3,2,1} 是该压栈序列对应的一个弹出序列，但 {4,3,5,1,2} 就不可能是该压栈序列的弹出序列。

```c++
class Solution {
public:
    bool validateStackSequences(vector<int>& pushed, vector<int>& popped) {
        stack<int> st;

        int pu = 0;
        int po = 0;

        while(pu < pushed.size())
        {
            st.push(pushed[pu]);
            pu++;
            while(!st.empty() && st.top() == popped[po])
            {
                st.pop();
                po++;
            }
        }
        return st.empty();
    }
};
```

## [剑指 Offer 37. 序列化二叉树](https://leetcode-cn.com/problems/xu-lie-hua-er-cha-shu-lcof/)

请实现两个函数，分别用来序列化和反序列化二叉树。

你需要设计一个算法来实现二叉树的序列化与反序列化。这里不限定你的序列 / 反序列化算法执行逻辑，你只需要保证一个二叉树可以被序列化为一个字符串并且将这个字符串反序列化为原始的树结构。

提示：输入输出格式与 LeetCode 目前使用的方式一致，详情请参阅 LeetCode 序列化二叉树的格式。你并非必须采取这种方式，你也可以采用其他的方法解决这个问题。

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
class Codec {
public:

    // Encodes a tree to a single string.
    string serialize(TreeNode* root) {
        string ans;
        ans.push_back('[');
        queue<TreeNode*> que;
        if(root) que.push(root);

        while(!que.empty())
        {
            TreeNode* node = que.front();
            que.pop();
            if(node == NULL)
            {
                ans += "null";
                ans.push_back(',');
            }
            else
            {
                ans += to_string(node->val);
                ans.push_back(',');
                que.push(node->left);
                que.push(node->right);
            }
            
        }
        ans.push_back(']');
        return ans;
    }


    // Decodes your encoded data to tree.
    TreeNode* deserialize(string data) {
        if(data == "[]") return NULL;
        string s_data = data.substr(1, data.size() - 2);
        vector<TreeNode*> vec;
        int start = 0;
        for(int i = 1; i < s_data.size(); i++)
        {
            if(s_data[i] == ',')
            {
                string min_s = s_data.substr(start, i - start);
                start = i + 1;
                if(min_s != "null")
                {
                    vec.push_back(new TreeNode(stoi(min_s)));
                }
                else
                {
                    vec.push_back(NULL);
                }
            }
        }
        int j = 1;
        for(int i = 0; i < vec.size(); i++)
        {
            if(vec[i] == NULL) continue;
            if(j < vec.size()) vec[i]->left = vec[j++];
            if(j < vec.size()) vec[i]->right = vec[j++];
        }

        return vec[0];
    }
};

// Your Codec object will be instantiated and called as such:
// Codec codec;
// codec.deserialize(codec.serialize(root));
```

## [剑指 Offer 51. 数组中的逆序对](https://leetcode-cn.com/problems/shu-zu-zhong-de-ni-xu-dui-lcof/)

在数组中的两个数字，如果前面一个数字大于后面的数字，则这两个数字组成一个逆序对。输入一个数组，求出这个数组中的逆序对的总数。

```c++
class Solution {
public:
    int mergesort(vector<int>& nums, vector<int>& tmp, int left, int right)
    {
        if(left >= right) return 0;
        int mid = left + (right - left) / 2;
        int cnt = mergesort(nums, tmp, left, mid) + mergesort(nums, tmp, mid + 1, right);

        int i = left, j = mid + 1, pos = left;

        while(i <= mid && j <= right)
        {
            if(nums[i] <= nums[j])
            {
                tmp[pos++] = nums[i++];
            }
            else
            {
                tmp[pos++] = nums[j++];
                cnt += mid - i + 1;
            }

        }
        for(int k = i; k <= mid; k++)
        {
            tmp[pos++] = nums[k];
        }

        for(int k = j; k <= right; k++)
        {
            tmp[pos++] = nums[k];
            cnt += mid - i + 1;
        }
        copy(tmp.begin() + left, tmp.begin() + right + 1, nums.begin() + left);
        return cnt;
    }

    int reversePairs(vector<int>& nums) {
        vector<int> tmp(nums.size(), 0);
        return mergesort(nums, tmp, 0, nums.size() - 1);
    }
};
```

## [剑指 Offer 44. 数字序列中某一位的数字](https://leetcode-cn.com/problems/shu-zi-xu-lie-zhong-mou-yi-wei-de-shu-zi-lcof/)

数字以0123456789101112131415…的格式序列化到一个字符序列中。在这个序列中，第5位（从下标0开始计数）是5，第13位是1，第19位是4，等等。

请写一个函数，求任意第n位对应的数字。

```c++
class Solution {
public:
    int findNthDigit(int n) {
        int digit = 1;
        long long start = 1;
        long long count = 9;

        while(n > count)
        {
            n -= count;
            digit++;
            start *= 10;
            count = digit * start * 9;
        }
        cout<<n<<endl;
        long long num = start + (n - 1) / digit;
        cout<<num<<endl;
        return to_string(num)[(n-1) % digit] - '0';
    }
};
```

## [剑指 Offer 43. 1～n 整数中 1 出现的次数](https://leetcode-cn.com/problems/1nzheng-shu-zhong-1chu-xian-de-ci-shu-lcof/)

输入一个整数 n ，求1～n这n个整数的十进制表示中1出现的次数。

例如，输入12，1～12这些整数中包含1 的数字有1、10、11和12，1一共出现了5次。

```c++
class Solution {
public:
    int countDigitOne(int n) {
        int ans = 0;
        long long digit = 1;
        int high = n / 10, cur = n % 10, low = 0;

        while(high != 0 || cur != 0)
        {
            if(cur == 0) ans += high * digit;
            else if(cur == 1) ans += high * digit + low + 1;
            else ans += (high + 1) * digit;

            low += cur * digit;
            cur = high % 10;
            high = high / 10;
            digit *= 10;
        }
        return ans;
    }
};
```

## [剑指 Offer 56 - I. 数组中数字出现的次数](https://leetcode-cn.com/problems/shu-zu-zhong-shu-zi-chu-xian-de-ci-shu-lcof/)

一个整型数组 `nums` 里除两个数字之外，其他数字都出现了两次。请写程序找出这两个只出现一次的数字。要求时间复杂度是O(n)，空间复杂度是O(1)。

```c++
class Solution {
public:
    vector<int> singleNumbers(vector<int>& nums) {
        int res = 0;
        for(int num : nums) res ^= num;

        int mask = 1;
        while((res & mask) == 0)
        {
            mask <<= 1;
        }

        int a = 0, b = 0;
        for(int num : nums)
        {
            if(mask & num)
            {
                a ^= num;
            }
            else
            {
                b ^= num;
            }
        }

        return {a, b};
    }
};
```

## [剑指 Offer 65. 不用加减乘除做加法](https://leetcode-cn.com/problems/bu-yong-jia-jian-cheng-chu-zuo-jia-fa-lcof/)

写一个函数，求两个整数之和，要求在函数体内不得使用 “+”、“-”、“*”、“/” 四则运算符号。

```c++
class Solution {
public:
    int add(int a, int b) {
        while (b != 0) {
		    int c = (unsigned int)(a & b) << 1;
            a ^= b;
            b = c;

	    }
	    return a;
    }
};
```

## [剑指 Offer 59 - I. 滑动窗口的最大值](https://leetcode-cn.com/problems/hua-dong-chuang-kou-de-zui-da-zhi-lcof/)

给定一个数组 `nums` 和滑动窗口的大小 `k`，请找出所有滑动窗口里的最大值。

```c++
class Solution {
public:
    vector<int> maxSlidingWindow(vector<int>& nums, int k) {
        priority_queue<pair<int, int>> que;

        vector<int> ans;

        for(int i = 0; i < k; i++)
        {
            que.push({nums[i], i});
        }
        ans.push_back(que.top().first);

        for(int i = k; i < nums.size(); i++)
        {
            que.push({nums[i], i});
            while(que.top().second <= i - k)
            {
                que.pop();
            }
            ans.push_back(que.top().first);
        }
        return ans;
    }
};
```

## [剑指 Offer 59 - II. 队列的最大值](https://leetcode-cn.com/problems/dui-lie-de-zui-da-zhi-lcof/)


请定义一个队列并实现函数 `max_value` 得到队列里的最大值，要求函数`max_value`、`push_back` 和 `pop_front` 的**均摊**时间复杂度都是O(1)。

若队列为空，`pop_front` 和 `max_value` 需要返回 -1

```c++
class MaxQueue {
public:
    queue<int> que;
    deque<int> dque;
    MaxQueue() {

    }
    
    int max_value() {
        if(!dque.empty()) return dque.front();
        else return -1;
    }
    
    void push_back(int value) {
        que.push(value);
        while(!dque.empty() && value > dque.back())
        {
            dque.pop_back();
        }
        dque.push_back(value);

    }
    
    int pop_front() {
        if(que.empty()) return -1;
        int ans = que.front();
        que.pop();
        if(ans == dque.front())
        {
            dque.pop_front();
        }

        return ans;
    }
};

/**
 * Your MaxQueue object will be instantiated and called as such:
 * MaxQueue* obj = new MaxQueue();
 * int param_1 = obj->max_value();
 * obj->push_back(value);
 * int param_3 = obj->pop_front();
 */
```

## [剑指 Offer 62. 圆圈中最后剩下的数字](https://leetcode-cn.com/problems/yuan-quan-zhong-zui-hou-sheng-xia-de-shu-zi-lcof/)


0,1,···,n-1这n个数字排成一个圆圈，从数字0开始，每次从这个圆圈里删除第m个数字（删除后从下一个数字开始计数）。求出这个圆圈里剩下的最后一个数字。

例如，0、1、2、3、4这5个数字组成一个圆圈，从数字0开始每次删除第3个数字，则删除的前4个数字依次是2、0、4、1，因此最后剩下的数字是3。

```c++
class Solution {
public:
    int lastRemaining(int n, int m) {
        int ans = 0;
        for(int i = 2; i <= n; i++)
        {
            ans = (m + ans) % i;
        }
        return ans;
    }
};
```

