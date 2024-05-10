#  `const`在函数中的使用

## 1.开始

> 开始于一段代码
```c++
class Solution {
   private:
    vector<vector<int>> res;

   public:
    vector<string> binaryTreePaths(TreeNode* root) {
        vector<int> path;
        dfs(root, path);
        vector<string> ans;

        for(auto &path:res){
            string s;
            for(auto &x:path)
                s.append(to_string(x) + "->");
            ans.push_back(s.substr(0, s.size() - 2));
        }
        return ans;
    }

   private:
    void dfs(TreeNode* root, vector<int> &path) {
        if (!root)
            return;
        path.push_back(root->val);
        // leaf Node
        if (!root->left && !root->right)
            res.push_back(path);

        dfs(root->left, path);
        dfs(root->right, path);
        path.pop_back();

    }
};
```
### 2.问题发现

### 2.1 前言
```c++
void dfs(TreeNode* root, vector<int> &path)
```
注意，此时的`path`使用的是*引用传参*，所以添加了`path.pop_back();`这一行代码。

**原因**:
* **回溯**模板的退回状态，使得调用栈在该层保持**原状态**。

当然也可以不使用`path.pop_back();`，改为`vector<int> &path`。

**弊端**

* 增加空间损耗

**但是**

* 减少了一部分代码逻辑
  
#### 2.2 问题出现

测试的时候，发现在调用`dfs(TreeNode* root, vector<int> &path)`时必须使用一个**存在的变量**，

比如:
```c++
    vector<int> path;
    dfs(root, path);
```

但是`dfs(TreeNode* root, vector<int> path)`不需要，

只需要:
```c++
    dfs(root,{})
```
> `{}`是`vector<int>`类型的变量

### 3.问题原因

* `&`只能用于已经声明的变量进行*引用传值*
  
* 不能传递*字面常量*
  
### 4.问题解决

举例:

**原来:**

* `print_hello( int &a)`

* 不能使用`print_hello(111)`调用

**修正:**

* 添加`const`，此时**函数**变为
  * `print_hello(const int &a)`

* 可以使用`print_hello(111)`调用
  