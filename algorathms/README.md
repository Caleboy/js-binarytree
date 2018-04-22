# 二叉树算法

选择树而不是那些基本的数据结构，是因为：

二叉树上进行查找特别快（而在链表上查找每次基本就是遍历，查找速度很慢）
二叉树添加或删除元素也很快（而对数组执行添加或删除操作则不是这样）

## 二叉查找树（排序二叉树）

有三种遍历BST的方式：

中序遍历 按照节点上的键值，以升序访问BST上的所有节点
先序遍历 先访问根节点，然后以同样方式访问左子树和右子树
后序遍历 先访问叶子节点，从左子树到右子树，再到根节点

### 构造二叉查找树

```js
/*
* parameter: data:本节点的数据；left：做节点；right：右节点
* 创建节点示例并插入到二叉树的正确位置
*/
function Node(data,left,right){
    this.data = data;
    this.left = left;
    this.right = right;
}
function BST(){
    this.root = null;
    this.insert = insert;
}
BST.prototype.insert = function(data) {
    var node = new Node(data,null,null);
    if(this.root == null){
        this.root = node;
    }else{
        var current = this.root;
        while(true){
            if(current.data > data){
                if(current.left === null){
                    current.left = node;
                    break;
                }
                current = current.left;
            }else{
                if(current.right === null){
                    current.right = node;
                    break;
                }
                current = current.right;
            }
        }
    }
}

var nodes = [8,3,10,1,6,14,4,7,13];
var binaryTree = new BST();
nodes.forEach(function(data) {
    binaryTree.insert(data);
});

//中序遍历

//先序遍历

//后序遍历
```
### 中序遍历

在上面构造函数中添加中序遍历

```js
var inOrderTraverseNode = function(node,callback) {
    if (node!==null) {
        inOrderTraverseNode(node.left,callback);
        callback(node.data);
        inOrderTraverseNode(node.right,callback);
    }
}
```
完整：

```js
function BinaryTree() {
    //二叉查找树由节点组成，所以我们先定义Node

    //Node
    var Node = function(data,left,right) {
        this.data = data;
        this.left = left;
        this.right = right;
       // this.show = show;
    };

    // var show = function() {
    //         return = this.data;
    // };

    var root = null;//设置根节点

    //insert()方法，用来向树中加入新节点
    this.insert = function(data) {
        var newNode = new Node(data,null,null);
        if(root ===null){
            root = newNode;
        }
        else {
            insertNode(root,newNode);
        }
    };

    this.inOrderTraverse = function(callback) {
        inOrderTraverseNode(root,callback);
    }

    var insertNode = function(node,newNode) {
             if(newNode.data < node.data){
                if(node.left === null){
                  node.left = newNode;
                }else{
                  insertNode(node.left,newNode);
                }
             }else{
               if(node.right === null){
                 node.right = newNode;
               }else{
                 insertNode(node.right,newNode);
               }
             }

    };

    var inOrderTraverseNode = function(node,callback) {
        if (node!==null) {
            inOrderTraverseNode(node.left,callback);
            callback(node.data);
            inOrderTraverseNode(node.right,callback);
        }
    }

}


var nodes = [8,3,10,1,6,14,4,7,13];
var binaryTree = new BinaryTree();
nodes.forEach(function(data) {
    binaryTree.insert(data);
});

//中序遍历
var callback = function(data) {
  console.log(data);
}
binaryTree.inOrderTraverse(callback);
```

### 前序遍历

我们看到中序遍历可以把二叉树的节点按照从小到大的顺序打印出来;
而前序遍历可以在我们已经拥有一颗二叉树的时候，高效的复制这颗二叉树。
通过其前序遍历去复制一颗二叉树比重新构造一颗二叉树要高效得多

```js
var inOrderTraverseNode = function(node,callback) {
    if (node!==null) {
        callback(node.data);
        inOrderTraverseNode(node.left,callback);
        inOrderTraverseNode(node.right,callback);
    }
}
```

```html
<p>前（先）序遍历：按照最优先顺序沿一定路径经过路径上所有的站。在二叉树中，先根后左再右。巧记：根左右。
```

### 后序遍历

```js
var inOrderTraverseNode = function(node,callback) {
    if (node!==null) {
        callback(node.data);
        inOrderTraverseNode(node.left,callback);
        inOrderTraverseNode(node.right,callback);
    }
}
```
