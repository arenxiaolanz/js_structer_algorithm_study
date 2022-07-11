# 五、树结构

## 5.1 树结构简介


### 树的定义

![$`OXI``5S(MJYVP$QLOO}AP.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657165002706-888c54c9-ca02-41c2-8c41-4208b215695f.jpeg#clientId=ud7979db5-dca3-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u81ae4908&margin=%5Bobject%20Object%5D&name=%24%60OXI%60%605S%28MJYVP%24QLOO%7DAP.jpg&originHeight=743&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=134320&status=done&style=none&taskId=u1266a85c-d9aa-4b9c-b19c-7048d86641f&title=)

-  树（Tree）: **n（n≥0）个结点**构成的**有限集合**。

   - 当**n=0**时，称为**空树**；

   - 对于任一棵**非空树（n> 0）**，它具备以下性质：

   - 树中有一个称为“**根（Root）”**的特殊结点，用** r **表示；

   - 其余结点可分为**m(m>0)个互不相交的有限集T1，T2，... ，Tm**

其中   ： 

每个集合本身又是一棵树，称为原来树的“**子树（SubTree）**”

> 注意: 
> 
> - 子树之间**不可以相交**

> - 除了**根结点**外，每个结点**有且仅有一个父结点**；

> - 一棵**N个结点的树有N-1条边**。  



### 树的术语

-  **节点的度（Degree）**：节点的**子树个数**，比如节点**B的度为2**；

- **树的度**：树的所有节点中**最大的度数**，如上图树的**度为2**；

- **叶节点（Leaf）**：**度为0的节点**（也称为叶子节点），如上图的**H，I**等；

- **父节点（Parent**）：**度不为0**的节点称为**父节点**，如上图节点**B是节点D和E**的父节点；

- **子节点（Child）**：若**B是D的父节点**，那么**D就是B的子节点**；

- **兄弟节点（Sibling）**：具有**同一父节点**的各节点彼此是兄弟节点，比如上图的**B和C，D和E互为兄弟节点**；

- **路径和路径长度**：路径指的是**一个节点到另一节点的通道**，路径所包含边的个数称为路径长度，比如**A->H的路径长度为3**；

- **节点的层次（Level）**：规定**根节点在1层**，其他任一节点的层数是**其父节点的层数加1**。如**B和C**节点的层次**为2**；

- **树的深度（Depth）**：树种所有节点中的**最大层次**是这棵**树的深度**，如上图树的**深度为4**；<br /> 

### 树的优点

- 数组:

   - 优点:

      - 数组的主要优点是根据**下标值访问**效率会很**高**.

      - 但是如果我们希望根据元素来查找对应的位置呢?

      - 比较好的方式是**先对数组进行排序**, 再进行**二分查找**.

   - 缺点:

      - 需要先对数组**进行排序**, 生成**有序数组**, 才能提高查找效率.

      - 另外数组在插入和删除数据时, 需要有**大量的位移操作**(插入到首位或者中间位置的时候), **效率很低**.

- 链表:

   - 优点:

      - 链表的**插入和删除操作效率都很高**.

   - 缺点:

      - 查找**效率很低**, 需要从头开始依次访问链表中的**每个数据项**, 直到找到.

      - 而且即使**插入和删除**操作效率很高, 但是如果要插入和删除**中间位置**的数据, 还是需要**重头先找到对应的数据.**

- 哈希表:

   - 优点:

      - 我们学过哈希表后, 已经发现了哈希表的**插入/查询/删除效率都是非常高的**

      - 但是哈希表也有很多缺点.

   - 缺点:

      - **空间利用率不高,** 底层使用的是数组, 并且某些单元是没有被利用的.

      - 哈希表中的元素是**无序**的, 不能按照固定的顺序来遍历哈希表中的元素.

      - 不能**快速的找出哈希表中的最大值或者最小值**这些特殊的值.

- 树结构:

   - 我们不能说树结构比其他结构都要好, 因为每种数据结构都有**自己特定的应用场景.

**
   - 但是树确实也综合了上面的数据结构的优点(当然优点不足于盖过其他数据结构, 比如**效率一般情况下没有哈希表高**), 并且也弥补了上面数据结构的缺点.

   - 而且为了**模拟某些场景**, 我们使用树结构会更加方便. 比如**文件的目录结构.  **


### 树结构的表示方法

树可以有很多种表示的方式

- 最普通的表示方式：

![L)X3P`G}{J8XT4[7K@1_8AB.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657164749575-edca34ec-6a07-473e-9be9-6bf91c6e0a90.jpeg#clientId=ud7979db5-dca3-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=ub65ea189&margin=%5Bobject%20Object%5D&name=L%29X3P%60G%7D%7BJ8XT4%5B7K%401_8AB.jpg&originHeight=402&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=31867&status=done&style=none&taskId=udd055088-e5a9-4ec7-85b4-9a033416369&title=)

- 儿子-兄弟表示法：

![]_1H]QGD_[7NUK~AHFQ`B~A.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657164753321-db7e4972-813f-4a05-b610-af10670bff3a.jpeg#clientId=ud7979db5-dca3-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u79173f57&margin=%5Bobject%20Object%5D&name=%5D_1H%5DQGD_%5B7NUK~AHFQ%60B~A.jpg&originHeight=443&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=32002&status=done&style=none&taskId=ufa6cdaa3-c86e-425a-a8cd-f66e1677d25&title=)

```javascript
//节点A
Node{
  //存储数据
  this.data = data
  //统一只记录左边的子节点
  this.leftChild = B
  //统一只记录右边的第一个兄弟节点
  this.rightSibling = null
}

//节点B
Node{
  this.data = data
  this.leftChild = E
  this.rightSibling = C
}

//节点F
Node{
  this.data = data
  this.leftChild = null
  this.rightSibling = null
}

```


- 儿子-兄弟表示法旋转：

![9$[Y46[RR$ZVCFWEV[D[A_A.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657164757149-030acdc4-53d5-47a3-b485-2c877403fd4b.jpeg#clientId=ud7979db5-dca3-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u0561db39&margin=%5Bobject%20Object%5D&name=9%24%5BY46%5BRR%24ZVCFWEV%5BD%5BA_A.jpg&originHeight=426&originWidth=776&originalType=binary&ratio=1&rotation=0&showTitle=false&size=40208&status=done&style=none&taskId=u57610958-a4b0-460d-83e9-b47480f38b5&title=)


> 总结出的**规律**：   
> 
> - 所有的树本质上都可以使用**二叉树**模拟出来
> 

> - 所以在学习的过程中，二叉树**非常重要**



## 5.2 二叉树

### 二叉树简介

> - 如果树中每个节点**最多只能有两个子节点**，这样的树就成为**“二叉树”**
> 
> -  前面, 我们已经提过**二叉树的重要性**, 不仅仅是因为简单, 也因为几乎上所有的树**都可以表示成二叉树**的形式



### 二叉树的概念

- 二叉树的定义

   -  二叉树可以**为空**, 也就是**没有结点**.

   - 若**不为空**，则它是由**根结点**和称为其**左子树TL和右子树TR**的两个**不相交**的二叉树组成。

- 二叉树有**五种形态**

<br />

   - 注意c和d是不同的二叉树, 因为二叉树是有左右之分的. 

![U3}P6H([@E%KP9O[PJ3VW)5.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657166253232-939d3d48-4f37-4129-8670-925f8c457494.jpeg#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=udff539ff&margin=%5Bobject%20Object%5D&name=U3%7DP6H%28%5B%40E%25KP9O%5BPJ3VW%295.jpg&originHeight=289&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=19517&status=done&style=none&taskId=u44af94c8-2524-4b11-9819-f7f1077b547&title=)


### 二叉树的特性

-  二叉树有几个比较重要的特性, 在笔试题中比较常见:

- 一个二叉树第 i 层的最大结点数为：**2^(i-1), i >= 1;**

- **深度为k**的二叉树有最大结点总数为： **2^k - 1, k >= 1;**

- 对任何**非空二叉树 T**，若**n0表示叶结点的个数**、n2是度为2的非叶结点个数，那么两者满足关系**n0 = n2 + 1**。  


![$0XR}CBV5]UC27EQM4$Y%T2.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657166497059-5566f755-3a71-4674-8bb7-90bf5ce44115.jpeg#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u1ae2a24d&margin=%5Bobject%20Object%5D&name=%240XR%7DCBV5%5DUC27EQM4%24Y%25T2.jpg&originHeight=401&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=31027&status=done&style=none&taskId=u1e591cc3-2d12-4b66-83e3-e495be34a7b&title=)

### 特殊的二叉树


- ** 完美二叉树(Perfect Binary Tree) **, 也称为**满二叉树(Full Binary Tree）**

   - 在二叉树中, **除了最下一层的叶结点**外, 每层节点都有**2个子结点**, 就构成了满二叉树.  

![[IY(6QFP3{TI6MW0C1I3ATG.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657166868286-840a3315-e5f9-487f-95ff-feb1c46cd134.jpeg#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u3e4c3bfc&margin=%5Bobject%20Object%5D&name=%5BIY%286QFP3%7BTI6MW0C1I3ATG.jpg&originHeight=537&originWidth=901&originalType=binary&ratio=1&rotation=0&showTitle=false&size=40430&status=done&style=none&taskId=ub0f868a0-53ca-4327-9cd1-85d4cee568a&title=)

-  **完全二叉树(Complete Binary Tree)**

   - 除二叉树最后一层外, 其他**各层的节点数都达到最大个数**.

   - 且最后一层**从左向右的叶结点连续存在**, 只缺右侧若干节点.

   - 完美二叉树是**特殊的**完全二叉树.

<br />下面不是完全二叉树, 因为**D节点还没有右结点**, 但是**E节点就有了左右结点**.  

![3X46HD9D88Q@G6PU{PFM09C.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657166974283-ba66db03-b0cd-46f3-8e15-72aae8457b7e.jpeg#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u36da9345&margin=%5Bobject%20Object%5D&name=3X46HD9D88Q%40G6PU%7BPFM09C.jpg&originHeight=540&originWidth=882&originalType=binary&ratio=1&rotation=0&showTitle=false&size=30715&status=done&style=none&taskId=u8174b5ac-7d52-4925-abb8-5169c9b7346&title=)


### 二叉树的数据存储

> 二叉树的存储**常见**的方式是**数组和链表**


- 使用**数组存储**

   - 完全二叉树：按**从上至下，从左到右**顺序存储

![%SJNV6A)RV1K]H2{@~@ZC6J.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657167248756-64704645-cc22-41de-9310-6f153dd88a23.jpeg#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=ubabc0a7c&margin=%5Bobject%20Object%5D&name=%25SJNV6A%29RV1K%5DH2%7B%40~%40ZC6J.jpg&originHeight=613&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=34517&status=done&style=none&taskId=uf0f46cbd-f5ab-4b0d-a2a8-f5063ddeea0&title=)

   - 非完全二叉树

      - 非完全二叉树要转成完全二叉树才可以按照上面的方案存储.

      - 但是会造成很大的空间浪费  

![ZKX68QZ@O75)Y`DZ7MKB%UE.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657167343576-23ad9eee-82ac-4b23-b70a-d13fe7b20d3d.jpeg#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=drop&height=324&id=uad8df6f9&margin=%5Bobject%20Object%5D&name=ZKX68QZ%40O75%29Y%60DZ7MKB%25UE.jpg&originHeight=690&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=63470&status=done&style=none&taskId=ub680df68-48de-4265-9718-6c59ca368c5&title=&width=564)


- 链表存储

   -  二叉树最**常见**的方式还是使用**链表存储.**

   - 每个结点封装成**一个Node**, Node中包含**存储的数据, 左结点的引用, 右结点的引用.**<br /> 

![7CF43_([])9XOUJ]EPG@R]P.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657167166106-37d6c2d9-922e-43be-b25b-d77ed6e3f4d8.jpeg#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=drop&height=136&id=u8edaacdc&margin=%5Bobject%20Object%5D&name=7CF43_%28%5B%5D%299XOUJ%5DEPG%40R%5DP.jpg&originHeight=288&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=25604&status=done&style=none&taskId=u1a6fecc1-567f-4e45-bb13-7976d11530b&title=&width=566)


## 5.3 二叉搜索树

### 认识二叉搜索树

- **二叉搜索树（BST**，Binary Search Tree），也称**二叉排序树或二叉查找树**

- 二叉搜索树是一棵**二叉树**，可以**为空**

- 如果**不为空**，满足以下性质

   - **非空左子树**的所有键值**小于其根节点**的键值

   - **非空右子树**的所有键值**大于其根节点**的键值

   - **左右子树**本身也都是**二叉搜索树**

- 下面哪些是二叉搜索树，那些不是？

![XN)S`D4FWLU%Y4DGKXHFL4V.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657168037077-9b4ab5fd-1681-4b90-858c-67577097ccd7.jpeg#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u15881a33&margin=%5Bobject%20Object%5D&name=XN%29S%60D4FWLU%25Y4DGKXHFL4V.jpg&originHeight=370&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=34344&status=done&style=none&taskId=uc2aae36c-30a1-4949-9a1f-054302ebfdc&title=)

>  总结：   
> 
> - 二叉搜索树的特点主要是**较小的值**总是保存在**左节点**上，相对**较大的值**总是保存在**右节点**上。   
> 
> - 这种特点使得二叉搜索树的**查询效率非常高**，这也就是**二叉搜索树中"搜索"的来源**。  <br /> 


### 二叉搜索树应用举例

下面是一个二叉搜索树：

![OYZZ%{5}7W1)}]F~T@]6(X9.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657168318136-a73b5da6-afa1-46bd-b45f-a3b94e0784aa.png#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=drop&height=317&id=uf5dd06e5&margin=%5Bobject%20Object%5D&name=OYZZ%25%7B5%7D7W1%29%7D%5DF~T%40%5D6%28X9.png&originHeight=259&originWidth=465&originalType=binary&ratio=1&rotation=0&showTitle=false&size=64847&status=done&style=none&taskId=u720e0402-87b5-4243-9dd6-00803ec7a20&title=&width=570)

若想在其中查找数据10，只需要查找4次，查找效率非常高

![LI2ZWFB%J`U_~5L03P2UR{L.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657170732532-9384dd17-9699-4ec6-a79d-d2103f3527ac.png#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=drop&height=324&id=uf0e517b4&margin=%5Bobject%20Object%5D&name=LI2ZWFB%25J%60U_~5L03P2UR%7BL.png&originHeight=237&originWidth=413&originalType=binary&ratio=1&rotation=0&showTitle=false&size=75810&status=done&style=none&taskId=u8af42436-ea6e-4a2f-b6a7-760b04ecb57&title=&width=564)

-  第1次：将**10与根节点9**进行**比较**，由于**10 > 9**，所以**10下一步与根节点9的右子节点13**比较；

- 第2次：由于**10 < 13**，所以**10下一步与父节点13的左子节点11**比较；

- 第3次：由于**10 < 11**，所以10下一步与**父节点11的左子节点10比较**；

- 第4次：由于**10 = 10，最终查找到数据10 **。  

## 5.4  一、二叉搜索树的封装


### 二叉搜索树的基本属性

![SBMG]YRBZ85Q9[RQ~88%BIT.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657173935909-6778502f-4894-47f9-b21c-da1d09eec0b4.png#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=uce58af6f&margin=%5Bobject%20Object%5D&name=SBMG%5DYRBZ85Q9%5BRQ~88%25BIT.png&originHeight=383&originWidth=771&originalType=binary&ratio=1&rotation=0&showTitle=false&size=73487&status=done&style=none&taskId=u23bc2b7d-5f87-412f-b324-c3b5f4aceda&title=)

如图所示：

> 二叉搜索树有四个最基本的属性：
> 
> - 指向节点的根：root
> 
> - 结点中的键：key
> 
> - 左指针：left
> 
> - 右指针：right


```javascript
function BinarySearchTree(){
  //创建节点构造函数
  function Node(key) {
    this.key = key
    this.left = null
    this.right = null
  }
  //保存根的属性
  this.root = null
}
```

### 二叉搜索树的常见操作

-  `insert（key）`：向树中**插入**一个新的键；

- `search（key）`：在树中**查找**一个键，如果节点存在，则返回true；如果不存在，则返回false；

- `inOrderTraverse`：通过**中序遍历**方式遍历所有节点；

- `preOrderTraverse`：通过**先序遍历**方式遍历所有节点；

- `postOrderTraverse`：通过**后序遍历**方式遍历所有节点；

- `min`：返回树中**最小**的值/键；

- `max`：返回树中**最大**的值/键；

- `remove（key）`：从树中**移除**某个键；<br /> 
### 插入数据(insert(key))

#### insert实现思路：

- 首先根据传入的key来创建节点对象

- 然后判断根节点是否存在

   - 若不存在，则通过`this.root = newNode`，直接把新节点作为二叉搜索树的根节点

   - 若存在，则通过`insertNode(this.root,newNode)`，寻找插入点

#### 代码实现：

```javascript
BinarySearchTree.prototype.insert = key => {
  let newNode = new Node(key)
  if(this.root === null){
    this.root = newNode
  }
  else{
    this.insertNode(this.root,newNode)
  }
}
```


#### insertNode实现思路（非根节点）：

- 根据比较传入的两个节点，一直查找新节点适合插入的位置，直到成功插入新节点为止

- 当`newNode.key < node.key`时，向左查找

   - 情况1：当`node`无左节点时，直接插入

   - 情况2： 当`node`有左子节点时，**递归调用insertNode()**,直到遇到无左子节点成功插入newNode后，不再符合该情况，也就不再调用insertNode()，递归停止。<br /> 
- 当`newNode.key >= node.key`时，向右查找

   - 情况1：当`node`无右节点时，直接插入

   - 情况2： 当`node`有右子节点时，**递归调用insertNode()**,直到遇到无左子节点成功插入newNode后，不再符合该情况，也就不再调用insertNode()，递归停止。


#### 代码实现：

```javascript
BinarySearchTree.prototype.insertNode = (node,newNode) => {
  if(newNode.key < node.key){
    if(node.left == null){
      node.left = newNode
    }
    else {
      this.insertNode(node.left,newNode)
    }
  }
  else if(newNode.key >= node.key){
    if(node.right == null){
      node.right = newNode
    }
    else{
      this.insertNode(node.right,newNode)
    }
  }
}
```

#### 测试代码

```javascript
//测试代码
//1.创建BinarySearchTree
let bst = new BinarySearchTree()

//2.插入数据
bst.insert(11);
bst.insert(7);
bst.insert(15);
bst.insert(5);
bst.insert(9);
console.log(bst);

```

#### 测试代码

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657176157692-96ec9fdf-d84b-4f04-aab5-b5f00c23477c.png#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=488&id=udeab5a16&margin=%5Bobject%20Object%5D&name=image.png&originHeight=592&originWidth=663&originalType=binary&ratio=1&rotation=0&showTitle=false&size=61133&status=done&style=none&taskId=u17e9fec2-8411-4ac5-af2d-4a80305f7a9&title=&width=546.5)

### 遍历数据

> 这里所说的树的遍历不仅仅针对二叉搜索树，而是适用于所有的二叉树。由于树结构不是线性结构，所以遍历方式有多种选择，常见的三种二叉树遍历方式为：  

> - 先序遍历；

> - 中序遍历；

> - 后序遍历；<br /> 


1. preOrderTraversal(先序遍历)

先序遍历的过程为：

- 首先，遍历根节点

- 然后，遍历其左子树

- 最后，遍历其右子树

![72VZ~B_}~6@@9OV%JEDI9Z8.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657182555582-5bf0f740-af00-406e-ae62-a49c6a996347.jpeg#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u2b75f67d&margin=%5Bobject%20Object%5D&name=72VZ~B_%7D~6%40%409OV%25JEDI9Z8.jpg&originHeight=438&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=33670&status=done&style=none&taskId=ue43ab5ef-79e8-4d76-a54b-25afacb2fc4&title=)

代码实现：

```javascript
BinarySearchTree.prototype.preOrderTraversal = (handler) => {
  this.preOrderTraversalNode(this.root,handler)
}
BinarySearchTree.prototype.preOrderTraversalNode = (node,handler) => {
  if(node != null){
    handler(node.key)
    this.preOrderTraversalNode(node.left,handler)
    this.preOrderTraversalNode(node.right,handler)
  }
}
```

测试代码：

```javascript
//测试代码
//1.创建BinarySearchTree
let bst = new BinarySearchTree()

//2.插入数据
bst.insert(11);
bst.insert(7);
bst.insert(15);
bst.insert(5);
bst.insert(3);
bst.insert(9);
bst.insert(8);
bst.insert(10);
bst.insert(13);
bst.insert(12);
bst.insert(14);
bst.insert(20);
bst.insert(18);
bst.insert(25);
bst.insert(6);

//3.测试遍历
let resultString = ""
//掺入处理节点值的处理函数
bst.preOrderTraversal(function(key){
  resultString += key + "->"
})
alert(resultString)

```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657183460833-a2a59b30-7c2c-46a6-90a0-d4f5bcca3672.png#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=150&id=uec8146f6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=185&originWidth=563&originalType=binary&ratio=1&rotation=0&showTitle=false&size=8118&status=done&style=none&taskId=u8689ccaf-d75f-4a3b-b1aa-00575664520&title=&width=457.5)

![T44H`{]JR]HH`6KY}H7BZ1W.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657183646607-01476757-0c02-4285-8e71-fc1892bb3345.jpeg#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=ua25b322b&margin=%5Bobject%20Object%5D&name=T44H%60%7B%5DJR%5DHH%606KY%7DH7BZ1W.jpg&originHeight=769&originWidth=1024&originalType=binary&ratio=1&rotation=0&showTitle=false&size=55245&status=done&style=none&taskId=uee895557-1f45-4bda-8c00-aa607cda6b1&title=)


2. midOrderTraversal(中序遍历)

中序遍历的过程为：

- 首先，遍历其左子树

- 然后，遍历根节点

- 最后，遍历其右子树

![7XUYTP~2@TGXTVW04XC0KRK.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657183657518-a3c29a09-ad3f-48d9-8b91-54b84d55935d.jpeg#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=drop&height=237&id=ubd6b0e4a&margin=%5Bobject%20Object%5D&name=7XUYTP~2%40TGXTVW04XC0KRK.jpg&originHeight=501&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36168&status=done&style=none&taskId=ud89fea1f-92be-426a-a38d-119dc0e4f54&title=&width=567)

代码实现：

```javascript
BinarySearchTree.prototype.midOrderTraversal = (handler) => {
  this.midOrderTraversalNode(this.root, handler)
}
BinarySearchTree.prototype.midOrderTraversalNode = (node, handler) => {
  if (node != null) {
    this.midOrderTraversalNode(node.left, handler)
    handler(node.key)
    this.midOrderTraversalNode(node.right, handler)
  }
}
```

测试代码：

```javascript
//测试代码
//1.创建BinarySearchTree
let bst = new BinarySearchTree()

//2.插入数据
bst.insert(11);
bst.insert(7);
bst.insert(15);
bst.insert(5);
bst.insert(3);
bst.insert(9);
bst.insert(8);
bst.insert(10);
bst.insert(13);
bst.insert(12);
bst.insert(14);
bst.insert(20);
bst.insert(18);
bst.insert(25);
bst.insert(6);

//3.测试遍历
let resultString = ""
//掺入处理节点值的处理函数
bst.midOrderTraversal(function(key){
  resultString += key + "->"
})
alert(resultString)

```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657185497113-ec505c46-528e-4e8d-a496-02d1ab880887.png#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=170&id=uddd14f8e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=183&originWidth=563&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7382&status=done&style=none&taskId=u7045acb3-e6c1-45ce-a5a7-7804cc6cfd1&title=&width=521.5)

![8F`OA`XVMR{`(CU%3GFS3UL.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657185704156-114fc041-4b53-4476-bfc0-ecf15d3c10ca.jpeg#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u1ef99308&margin=%5Bobject%20Object%5D&name=8F%60OA%60XVMR%7B%60%28CU%253GFS3UL.jpg&originHeight=634&originWidth=1024&originalType=binary&ratio=1&rotation=0&showTitle=false&size=57528&status=done&style=none&taskId=u42ac2de6-82fe-47d6-8469-e9cd6bd82a9&title=)


3. postOrderTraversal(后序遍历)

后序遍历的过程为：

- 首先，遍历其左子树

- 然后，遍历其右子树

- 最后，遍历其根节点

![M)[RRLGOTZQKYLA(RP@QAR5.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657186036677-cd3cbbda-ce04-4697-998b-4ab714381f3c.jpeg#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u9cd50a64&margin=%5Bobject%20Object%5D&name=M%29%5BRRLGOTZQKYLA%28RP%40QAR5.jpg&originHeight=478&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36261&status=done&style=none&taskId=u3d6c9a9b-7ce6-4ef2-9542-44be6471bf0&title=)

代码实现：

```javascript
BinarySearchTree.prototype.postOrderTraversal = (handler) => {
  this.postOrderTraversalNode(this.root, handler)
}
BinarySearchTree.prototype.postOrderTraversalNode = (node, handler) => {
  if (node != null) {
    this.postOrderTraversalNode(node.left, handler)
    this.postOrderTraversalNode(node.right, handler)
    handler(node.key)
  }
}
```

测试代码：

```javascript
//测试代码
//1.创建BinarySearchTree
let bst = new BinarySearchTree()

//2.插入数据
bst.insert(11);
bst.insert(7);
bst.insert(15);
bst.insert(5);
bst.insert(3);
bst.insert(9);
bst.insert(8);
bst.insert(10);
bst.insert(13);
bst.insert(12);
bst.insert(14);
bst.insert(20);
bst.insert(18);
bst.insert(25);
bst.insert(6);

//3.测试遍历
let resultString = ""
//掺入处理节点值的处理函数
bst.postOrderTraversal(function(key){
  resultString += key + "->"
})
alert(resultString)
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657185951377-a8592cb5-48d4-4d0d-8985-177cfd52bd19.png#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=190&id=u6a61a5ac&margin=%5Bobject%20Object%5D&name=image.png&originHeight=188&originWidth=565&originalType=binary&ratio=1&rotation=0&showTitle=false&size=8545&status=done&style=none&taskId=u4446d581-7f26-428c-9f1a-8d83200cfe9&title=&width=572.5)

![DA]`UUVLSSI~}7ZLZ[}%YVU.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657186025780-9f1ea78a-c405-4034-bb0d-0f3a4e958889.jpeg#clientId=u17d54ebf-7058-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u27d9e00d&margin=%5Bobject%20Object%5D&name=DA%5D%60UUVLSSI~%7D7ZLZ%5B%7D%25YVU.jpg&originHeight=640&originWidth=1024&originalType=binary&ratio=1&rotation=0&showTitle=false&size=55622&status=done&style=none&taskId=ua49ff1ab-edc5-40d6-93c0-9e0fb2b8395&title=)

### 查找数据

1. 查找最大值和最小值

思路：

- 代码依次向左找到**最左边**的节点就是，**最小值**

- 代码依次向左找到**最右边**的节点就是，**最大值**

代码实现：

```javascript
BinarySearchTree.prototype.min = () => {
  let node = this.root
  while(node.left != null){
    node = node.left
  }
  return node.key
}
BinarySearchTree.prototype.max = () => {
  let node = this.root
  while(node.right != null){
    node = node.right
  }
  return node.key
}
```

测试代码：

```javascript
console.log(bst.max())
console.log(bst.min())
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657186413258-790c21dc-bfd0-4da6-a18c-08e1ece8c93d.png#clientId=u62b45d7f-2f05-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=171&id=ubd9f2ee5&margin=%5Bobject%20Object%5D&name=image.png&originHeight=62&originWidth=98&originalType=binary&ratio=1&rotation=0&showTitle=false&size=616&status=done&style=none&taskId=u0c9e57e1-8555-4d95-ac13-27f00d41e89&title=&width=271)


2. 查找特定值

代码实现：

```javascript
BinarySearchTree.prototype.search = key => {
  let node = this.root
  while (node != null) {
    if (key < node.key) {
      node = node.left
    }
    else if (key > node.key) {
      node = node.right
    }
    else { return true }
  }
  return false
}
```

测试代码：

```javascript
console.log(bst.search(100));
console.log(bst.search(13));
console.log(bst.search(99));
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657187057519-a9a8ce9f-7fff-425b-b3f9-50c45e988684.png#clientId=u62b45d7f-2f05-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=179&id=u31bb0cbf&margin=%5Bobject%20Object%5D&name=image.png&originHeight=94&originWidth=155&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1460&status=done&style=none&taskId=uff65b137-fb19-4b19-a98c-10a16192fdb&title=&width=294.5)


### 删除数据

实现思路：

- 第一步：先找到需要删除的节点，若没找到，则不需要删除

   - 首先定义变量current，用于保存需要删除的节点

   - 变量parent，用于保存它的父节点

   - 变量isLeftChild保存current是否为parent1的左节点

   - 这样方便之后删除节点，改变相关节点的指向

- 第二步：删除找到的指定节点，后分三种情况

   - 删除叶子节点

   - 删除只有一个子节点的节点

   - 删除有两个子节点的节点

初步实现代码：

```javascript
BinarySearchTree.prototype.remove = key => {
  let current = this.root
  let parent = null
  let isLeftChild = true
  while(current.key != key){
    parent = current
    if(key < current.key){
      isLeftChild = true
      current = current.left
    }
    else{
      isLeftChild = false
      current = current.right
    }
    if(current == null){
      return false
    }
  }
}
```


1. 情况1：没有子节点

代码实现：

```javascript
if(current.left == null && current.right == null){
  if(current == this.root){
    this.root = null
  }
  else if(isLeftChild){
    parent.left = null
  }
  else {
    parent.right = null
  }
}
```

2. 情况2：有一个子节点

代码实现：

```javascript
else if (current.right == null) {
  if (current == this.root) {
    this.root = current.left
  }
  else if (isLeftChild) {
    parent.left = current.left
  }
  else {
    parent.right = current.left
  }
}
  else if (current.left == null) {
    if (current == this.root) {
      this.root = current.right
    }
    else if (isLeftChild) {
      parent.left = current.right
    }
    else {
      parent.right = current.right
    }
  }
```

3. 情况2：有两个子节点

> 总结：
> - 需要从要删除节点下面的子节点中找到一个如果要删除的节点有两个子节点，甚至子节点还有子节点，这种情况下需要从要删除节点下面的子节点中找到一个合适的节点，来替换当前的节点
> 
> - 若用current表示需要删除的节点，则合适的节点是指
> 
：
>    - current左子树中比current小一点点的节点，即current**左子树的最大值**
> 
>    - current右子树中比current大一点点的节点，即current**右子树的最大值**


> 前驱和后继
> 在二叉搜索树中，这两个特殊的节点有特殊的名字
> 
> -  比current小一点点的节点，称为current节点的**前驱**。比如下图中的**节点5就是节点7的前驱；**

> - 比current大一点点的节点，称为current节点的**后继**。比如下图中的**节点8就是节点7的后继；**<br /> 


![VJFW9{I@Z]EJGI6(8EF49QU.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657190027833-068870fc-8d8c-44e0-8020-d0d6901953b8.jpeg#clientId=u62b45d7f-2f05-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u1f08df68&margin=%5Bobject%20Object%5D&name=VJFW9%7BI%40Z%5DEJGI6%288EF49QU.jpg&originHeight=620&originWidth=1183&originalType=binary&ratio=1&rotation=0&showTitle=false&size=45973&status=done&style=none&taskId=u8b20d9fb-6d59-4eb2-b38a-d06f6a7d2b7&title=)

代码实现：

```javascript
// 5.删除有两个节点的节点
else {
  // 1.获取后继节点
  let successor = this.getSuccessor(current)

  // 2.判断是否是根节点
  if (current == this.root) {
    this.root = successor
  } else if (isLeftChild) {
    parent.left = successor
  } else {
    parent.right = successor
  }

  // 3.将删除节点的左子树赋值给successor
  successor.left = current.left

}


// 找后继的方法
BinarySerachTree.prototype.getSuccessor = function (delNode) {
  // 1.使用变量保存临时的节点
  let successorParent = delNode
  let successor = delNode
  let current = delNode.right // 要从右子树开始找

  // 2.寻找节点
  while (current != null) {
    successorParent = successor
    successor = current
    current = current.left
  }

  // 3.如果是删除图中15的情况, 还需要如下代码
  if (successor != delNode.right) {
    successorParent.left = successor.right
    successor.right = delNode.right
  }

  return successor
}
```


4. 完整实现

```javascript
BinarySearchTree.prototype.remove = key => {
  let current = this.root
  let parent = null
  let isLeftChild = true
  while (current.key != key) {
    parent = current
    if (key < current.key) {
      isLeftChild = true
      current = current.left
    }
    else {
      isLeftChild = false
      current = current.right
    }
    if (current == null) {
      return false
    }
  }
  if (current.left == null && current.right == null) {
    if (current == this.root) {
      this.root = null
    }
    else if (isLeftChild) {
      parent.left = null
    }
    else {
      parent.right = null
    }
  }
  else if (current.right == null) {
    if (current == this.root) {
      this.root = current.left
    }
    else if (isLeftChild) {
      parent.left = current.left
    }
    else {
      parent.right = current.left
    }
  }
  else if (current.left == null) {
    if (current == this.root) {
      this.root = current.right
    }
    else if (isLeftChild) {
      parent.left = current.right
    }
    else {
      parent.right = current.right
    }
  }
  // 5.删除有两个节点的节点
  else {
    // 1.获取后继节点
    let successor = this.getSuccessor(current)

    // 2.判断是否是根节点
    if (current == this.root) {
      this.root = successor
    } else if (isLeftChild) {
      parent.left = successor
    } else {
      parent.right = successor
    }

    // 3.将删除节点的左子树赋值给successor
    successor.left = current.left

  }
  return true
}
// 找后继的方法
BinarySerachTree.prototype.getSuccessor = function (delNode) {
  // 1.使用变量保存临时的节点
  let successorParent = delNode
  let successor = delNode
  let current = delNode.right // 要从右子树开始找

  // 2.寻找节点
  while (current != null) {
    successorParent = successor
    successor = current
    current = current.left
  }

  // 3.如果是删除图中15的情况, 还需要如下代码
  if (successor != delNode.right) {
    successorParent.left = successor.right
    successor.right = delNode.right
  }

  return successor
}
```

测试代码：

```javascript
//测试代码
//1.创建BinarySearchTree
let bst = new BinarySearchTree()

//2.插入数据
bst.insert(11);
bst.insert(7);
bst.insert(15);
bst.insert(5);
bst.insert(3);
bst.insert(9);
bst.insert(8);
bst.insert(10);
bst.insert(13);
bst.insert(12);
bst.insert(14);
bst.insert(20);
bst.insert(18);
bst.insert(25);
bst.insert(6);
bst.insert(19);

//3.测试删除代码
//删除没有子节点的节点
bst.remove(3)
bst.remove(8)
bst.remove(10)

//删除有一个子节点的节点
bst.remove(5)
bst.remove(19)

//删除有两个子节点的节点
bst.remove(9)
bst.remove(7)
bst.remove(15)

//遍历二叉搜索树并输出
let resultString = ""
bst.midOrderTraversal(function(key){
  resultString += key + "->"
})
alert(resultString)

```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657190987126-34a6bfb8-2a2a-4acd-9d9d-172afa3ae9e6.png#clientId=u62b45d7f-2f05-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=261&id=uac96f95b&margin=%5Bobject%20Object%5D&name=image.png&originHeight=220&originWidth=134&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2360&status=done&style=none&taskId=ua4bc183d-069a-466d-867f-f66db4a5d47&title=&width=159)

### 二叉搜索树完整封装

```javascript
function BinarySearchTree() {
  //创建节点构造函数
  function Node(key) {
    this.key = key
    this.left = null
    this.right = null
  }
  //保存根的属性
  this.root = null
  BinarySearchTree.prototype.insert = key => {
    let newNode = new Node(key)
    if (this.root === null) {
      this.root = newNode
    }
    else {
      this.insertNode(this.root, newNode)
    }
  }
  BinarySearchTree.prototype.insertNode = (node, newNode) => {
    if (newNode.key < node.key) {
      if (node.left == null) {
        node.left = newNode
      }
      else {
        this.insertNode(node.left, newNode)
      }
    }
    else if (newNode.key >= node.key) {
      if (node.right == null) {
        node.right = newNode
      }
      else {
        this.insertNode(node.right, newNode)
      }
    }
  }
  BinarySearchTree.prototype.preOrderTraversal = (handler) => {
    this.preOrderTraversalNode(this.root, handler)
  }
  BinarySearchTree.prototype.preOrderTraversalNode = (node, handler) => {
    if (node != null) {
      handler(node.key)
      this.preOrderTraversalNode(node.left, handler)
      this.preOrderTraversalNode(node.right, handler)
    }
  }
  BinarySearchTree.prototype.midOrderTraversal = (handler) => {
    this.midOrderTraversalNode(this.root, handler)
  }
  BinarySearchTree.prototype.midOrderTraversalNode = (node, handler) => {
    if (node != null) {
      this.midOrderTraversalNode(node.left, handler)
      handler(node.key)
      this.midOrderTraversalNode(node.right, handler)
    }
  }
  BinarySearchTree.prototype.postOrderTraversal = (handler) => {
    this.postOrderTraversalNode(this.root, handler)
  }
  BinarySearchTree.prototype.postOrderTraversalNode = (node, handler) => {
    if (node != null) {
      this.postOrderTraversalNode(node.left, handler)
      this.postOrderTraversalNode(node.right, handler)
      handler(node.key)
    }
  }
  BinarySearchTree.prototype.min = () => {
    let node = this.root
    while (node.left != null) {
      node = node.left
    }
    return node.key
  }
  BinarySearchTree.prototype.max = () => {
    let node = this.root
    while (node.right != null) {
      node = node.right
    }
    return node.key
  }
  BinarySearchTree.prototype.search = key => {
    let node = this.root
    while (node != null) {
      if (key < node.key) {
        node = node.left
      }
      else if (key > node.key) {
        node = node.right
      }
      else { return true }
    }
    return false
  }
  BinarySearchTree.prototype.remove = key => {
    let current = this.root
    let parent = null
    let isLeftChild = true
    while (current.key != key) {
      parent = current
      if (key < current.key) {
        isLeftChild = true
        current = current.left
      }
      else {
        isLeftChild = false
        current = current.right
      }
      if (current == null) {
        return false
      }
    }
    if (current.left == null && current.right == null) {
      if (current == this.root) {
        this.root = null
      }
      else if (isLeftChild) {
        parent.left = null
      }
      else {
        parent.right = null
      }
    }
    else if (current.right == null) {
      if (current == this.root) {
        this.root = current.left
      }
      else if (isLeftChild) {
        parent.left = current.left
      }
      else {
        parent.right = current.left
      }
    }
    else if (current.left == null) {
      if (current == this.root) {
        this.root = current.right
      }
      else if (isLeftChild) {
        parent.left = current.right
      }
      else {
        parent.right = current.right
      }
    }
    // 5.删除有两个节点的节点
    else {
      // 1.获取后继节点
      let successor = this.getSuccessor(current)

      // 2.判断是否是根节点
      if (current == this.root) {
        this.root = successor
      } else if (isLeftChild) {
        parent.left = successor
      } else {
        parent.right = successor
      }

      // 3.将删除节点的左子树赋值给successor
      successor.left = current.left

    }
    return true
  }
  // 找后继的方法
  BinarySearchTree.prototype.getSuccessor = function (delNode) {
    // 1.使用变量保存临时的节点
    let successorParent = delNode
    let successor = delNode
    let current = delNode.right // 要从右子树开始找

    // 2.寻找节点
    while (current != null) {
      successorParent = successor
      successor = current
      current = current.left
    }

    // 3.如果是删除图中15的情况, 还需要如下代码
    if (successor != delNode.right) {
      successorParent.left = successor.right
      successor.right = delNode.right
    }

    return successor
  }


}
//测试代码
//1.创建BinarySearchTree
let bst = new BinarySearchTree()

//2.插入数据
bst.insert(11);
bst.insert(7);
bst.insert(15);
bst.insert(5);
bst.insert(3);
bst.insert(9);
bst.insert(8);
bst.insert(10);
bst.insert(13);
bst.insert(12);
bst.insert(14);
bst.insert(20);
bst.insert(18);
bst.insert(25);
bst.insert(6);

//3.测试遍历
let resultString = ""
//掺入处理节点值的处理函数
bst.postOrderTraversal(function (key) {
  resultString += key + "->"
})
//alert(resultString)
console.log(bst.max())
console.log(bst.min())
console.log(bst.search(100));
console.log(bst.search(13));
console.log(bst.search(99));

//3.测试删除代码
//删除没有子节点的节点
console.log(bst.remove(3))
console.log(bst.remove(8))
console.log(bst.remove(10))

//删除有一个子节点的节点
console.log(bst.remove(5))

//删除有两个子节点的节点
console.log(bst.remove(9))
console.log(bst.remove(7))
console.log(bst.remove(15))


```

##  5.5 平衡树

### 二叉搜索树的缺陷

-  当插入的数据是有序的数据，就会造成二叉搜索树的深度过大。比如原二叉搜索树又 11 7 15 组成

- 当插入一组有序数据：6 5 4 3 2就会变成深度过大的搜索二叉树，会严重影响二叉搜索树的性能

![D8)03K`L1{(8@4~@NR(5(S5.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657191334984-adf7f557-4b3d-4ed7-b9cf-e4691adc46a4.png#clientId=u62b45d7f-2f05-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=uaf76863e&margin=%5Bobject%20Object%5D&name=D8%2903K%60L1%7B%288%404~%40NR%285%28S5.png&originHeight=551&originWidth=412&originalType=binary&ratio=1&rotation=0&showTitle=false&size=72185&status=done&style=none&taskId=uce09dea6-a379-4200-8c72-57f0f850ccf&title=)

### 非平衡树

-  比较好的二叉搜索树，它的数据应该是**左右均匀分布**的；

- 但是插入连续数据后，二叉搜索树中的数据分布就变得**不均匀**了，我们称这种树为**非平衡树；**

- 对于一棵平衡二叉树来说，**插入/查找等**操作的效率是**O（logN）**；

- 而对于一棵**非平衡二叉树**来说，相当于编写了一个**链表**，查找效率变成了**O（N）;**<br /> 

### 树的平衡性

 为了能以**较快的时间O（logN）**来操作一棵树，我们需要保证**树总是平衡**的：

- 起码**大部分是平衡**的，此时的时间复杂度也是接近**O（logN）**的；

- 这就要求树中每个节点**左边**的子孙节点的个数，应该尽可能地**等于右边**的子孙节点的个数；<br /> 


### 常见的平衡树

-  **AVL树**：是最早的一种平衡树，它通过在**每个节点多存储一个额外的数据**来保持树的平衡。由于AVL树是平衡树，所以它的时间复杂度也是**O（logN**）。但是它的**整体效率不如红黑树**，开发中比较少用。

- **红黑树**：同样通过一些特性来保持树的平衡，时间复杂度也是**O（logN）**。进行**插入/删除**等操作时，性能**优于AVL树**，所以平衡树的应用基本都是**红黑树**。<br /> 

