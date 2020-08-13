# Depth-first search of binary tree 
These searches are referred to as depth-first search (DFS), since the search tree is deepened as much as possible on each child before going to the next sibling. 
For a binary tree, they are defined as access operations at each node, starting with the current node, whose algorithm is as follows:

The general recursive pattern for traversing a binary tree is this:  

Go down one level to the recursive argument N. If N exists (is non-empty) execute the following three operations in a certain order:  
(L)	Recursively traverse N's left subtree.  
(R)	Recursively traverse N's right subtree.  
(N)	Process the current node N itself.  
Return by going up one level and arriving at the parent node of N.  
In the examples (L) is mostly performed before (R). But (R) before (L) is also possible, see (RNL).  

The recursive version is too simple to write down here, The iteration version of three kinds of traversal are as fallows:  
## Pre-order (NLR)
```C++
  vector<int> preorderTraversal(TreeNode* root) {
      vector<int> res;
      stack<TreeNode*> st;
      st.push(root);
      while(!st.empty()){
          TreeNode* temp= st.top();
          st.pop();
          if(!temp)continue;
          res.push_back(temp->val);
          st.push(temp->right);
          st.push(temp->left);
      }
      return res;
  }
```
## In-order (LNR)
```C++
  vector<int> inorderTraversal(TreeNode* root) {
      vector<int> res;
      stack<TreeNode*> st;
      while(!st.empty()||root){
          if(root){
              st.push(root);
              root=root->left;
          }
          else{
              root=st.top();
              st.pop();
              res.push_back(root->val);
              root=root->right;
          }
      }
      return res;
    }
```
## Post-order (LRN)
```C++
  vector<int> postorderTraversal(TreeNode* root) {
      vector<int> res;        
      stack<TreeNode*> st;
      TreeNode *last,*peek;
      while (!st.empty()||root) {
          if(root){
              st.push(root);
              root=root->left;
          }
          else{
              peek=st.top();
              if(peek->right&&last!=peek->right){
                  root=peek->right;
              }
              else{
                  res.push_back(peek->val);
                  last=st.top();
                  st.pop();
              }
          }
      }
      return res;
  }
```
## Second method of Post-order (LRN)
```C++
  vector<int> postorderTraversal(TreeNode* root) {
      stack<TreeNode*> st;
      vector<int> res;
      st.push(root);
      while (!st.empty()) {
          TreeNode* node = st.top();
          st.pop();
          if (node) res.push_back(node->val);
          else continue;
          st.push(node->left); 
          st.push(node->right);
      }
      reverse(res.begin(), res.end()); 
      return res;
  }
```
# Breadth-first search/ level order of binary tree 
```C++
  vector<vector<int>> levelOrder(TreeNode* root) {
      queue<TreeNode*> que;
      if (root) que.push(root);
      vector<vector<int>> res;
      while (!que.empty()) {
          int size = que.size();
          vector<int> temp;
          for (int i = 0; i < size; i++) {
              TreeNode* node = que.front();
              que.pop();
              temp.push_back(node->val);
              if (node->left) que.push(node->left);
              if (node->right) que.push(node->right);
          }
          res.push_back(temp);
      }
      return res;
  }
```
