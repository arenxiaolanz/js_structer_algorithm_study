# 七、图结构

## 7.1 图的简介

### 图是什么？

- **图结构**是一种与**树结构**有些**相似**的数据结构

- **图论**是数学的一个**分支**，并且在数学中，**树是图**的一种

- 图论以**图为研究对象**，研究**顶点和边**组成的**图形**的数学**理论和方法**

- 主要的研究目的为：**事物之间的联**系，顶点代表**事物**，边代表**两个事物间的关系**


### 图的特点

- 一组**顶点**：通常用**V（Vertex）表示顶点**的集合

- 一组**边**：通常用**E（Edge）表示边**的集合

   - **边是顶点和顶点**之间的连线

   - 边可以是**有向**的，也可以是**无向**的。比如 **A---B 表示无向**， **A---> B 表示有向**


### 图的常用术语

- 顶点：表示图中的**一个节点**；

- 边：表示**顶点和顶点**之间的连线；

- 相邻顶点：由**一条边连接在一起**的顶点称为**相邻顶点**；

- 度：一个顶点的度是**相邻顶点的数量**；

- 路径：

   - **简单路径**：简单路径要求**不包含重复**的顶点；

   - **回路**：**第一个顶点和最后一个顶点相同**的路径称为回路；

- 无向图：图中的所有**边都是没有方向**的；

- 有向图：图中的所有**边都是有方向**的；

- 无权图：**无权图**中的边**没有任何权重意义**；

- 带权图：**带权图**中的边**有一定的权重含义；**<br /> 

## 7.2 图的表示

### 邻接矩阵

表示图的常用方式为：**邻接矩阵**。

- 可以使用**二维数组**来表示邻接矩阵；

- 邻接矩阵让**每个节点和一个整数**相关联，该**整数作为数组的下标**值；

- 使用一个**二维数组**来表示**顶点之间的连接**；

![C{@7N35Q7(OYKA_JGA0(Y(O.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657245205836-8c352c68-a6d0-4c80-9a4d-544396aa4f97.jpeg#clientId=uc8b0f51c-0f19-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=uafa1b564&margin=%5Bobject%20Object%5D&name=C%7B%407N35Q7%28OYKA_JGA0%28Y%28O.jpg&originHeight=517&originWidth=1024&originalType=binary&ratio=1&rotation=0&showTitle=false&size=40596&status=done&style=none&taskId=u0cacc789-6b90-4194-901e-27b1de6db6b&title=)

如上图所示：

- 二维数组中的**0表示没有连线**，**1表示有连线**；

- 如：**A[ 0 ] [ 3 ] = 1**，表示 A 和 C 之间有**连接**；

- 邻接矩阵的**对角线上的值都为0**，表示**A - A ，B - B，等自回路**都**没有连接**（自己与自己之间没有连接）；

- 若为**无向图**，则**邻接矩阵应为对角线上元素全为0的对称矩阵**；<br /> 


### 邻接矩阵的问题


 如果图是一个**稀疏图**，那么邻接矩阵中将**存在大量的 0**，造成**存储空间的浪费 **   <br />   

### 邻接表

另外一种表示图的常用方式为：**邻接表**。

- 邻接表由图中**每个顶点以及和顶点相邻的顶点列表**组成；

- 这个列表可用**多种方式存储**，比如：**数组/链表/字典（哈希表）**等都可以；

![AMM$}5Y5H(`J5JP4EHG}V]Y.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657245697595-dd1def79-5f3d-491d-ab4e-4636424b3b2b.jpeg#clientId=uc8b0f51c-0f19-4&crop=0&crop=0&crop=1&crop=1&from=drop&height=333&id=u7ef3d967&margin=%5Bobject%20Object%5D&name=AMM%24%7D5Y5H%28%60J5JP4EHG%7DV%5DY.jpg&originHeight=632&originWidth=1024&originalType=binary&ratio=1&rotation=0&showTitle=false&size=40721&status=done&style=none&taskId=u300123d3-932d-408e-a18d-c81e420def0&title=&width=540)

如上图所示：

- 图中可清楚看到**A与B、C、D相邻**，假如要表示这些与A顶点相邻的顶点（边），可以通过将**它们作为A的值（value）存入到对应的数组/链表/字典中。**

- 之后，通过**键（key）A**可以十分方便地取出对应的数据；<br /> 
### 邻接表的问题

- 邻接表可以简单地得**出度**，即某一顶点指向其他顶点的个数；

- 但是，邻接表计算**入度**（指向某一顶点的其他顶点的个数称为该顶点的入度）十分困难。此时需要构造**逆邻接表**才能有效计算入度；<br /> 

## 7.3 封装图结构

在实现过程中采用**邻接表**的方式来表示边，使用**字典类**来存储邻接表

### 添加字典类和队列类

首先需要引入之前实现的，之后会用到的字典类和队列类

```javascript
//封装字典类
function Dictionary() {
  //字典属性
  this.items = {}

  //字典操作方法
  //一.在字典中添加键值对
  Dictionary.prototype.set = function (key, value) {
    this.items[key] = value
  }

  //二.判断字典中是否有某个key
  Dictionary.prototype.has = function (key) {
    return this.items.hasOwnProperty(key)
  }

  //三.从字典中移除元素
  Dictionary.prototype.remove = function (key) {
    //1.判断字典中是否有这个key
    if (!this.has(key)) return false

    //2.从字典中删除key
    delete this.items[key]
    return true
  }

  //四.根据key获取value
  Dictionary.prototype.get = function (key) {
    return this.has(key) ? this.items[key] : undefined
  }

  //五.获取所有keys
  Dictionary.prototype.keys = function () {
    return Object.keys(this.items)
  }

  //六.size方法
  Dictionary.prototype.keys = function () {
    return this.keys().length
  }

  //七.clear方法
  Dictionary.prototype.clear = function () {
    this.items = {}
  }
}
//封装队列类
function Queue() {
  //属性
  this.items = []
  //方法
  //1.enqueue
  Queue.prototype.enqueue = (element) => {
    this.items.push(element)
  }
  //2.dequeue
  Queue.prototype.dequeue = () => {
    return this.items.shift()
  }
  //3.front
  Queue.prototype.front = () => {
    return this.items[0]
  }
  //4.isEmpty
  Queue.prototype.isEmpty = () => {
    return this.items.length === 0
  }
  //5.size
  Queue.prototype.size = () => {
    return this.items.length
  }
  //6.toString
  Queue.prototype.toString = () => {
    return this.items.join('')
  }
}
```


### 创建图类

```javascript
function Graph (){
  //属性：顶点（数组）/边（字典）
  this.vertexes = []//顶点
  this.edges = new Dictionary()//边
}
```

### 添加顶点与边

创建一个**数组对象vertexes存储图的顶点**；创建一个**字典对象edges存储图的边**，其中**key为顶点**，**value为存储key顶点相邻顶点的数组**。<br /> <br />代码实现：

```javascript
Graph.prototype.addVertex = function (v) {
  this.vertexes.push(v)
  this.edges.set(v, [])
}
Graph.prototype.addEdge = (v1,v2){
  this.edges.get(v1).push(v2)
  this.edges.get(v2).push(v1)
}
```

测试代码：

```javascript
let graph = new Graph()
let myVertexes = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I']
for (let i = 0; i < myVertexes.length; i++) {
  graph.addVertex(myVertexes[i])
}
graph.addEdge('A', 'B');
graph.addEdge('A', 'C');
graph.addEdge('A', 'D');
graph.addEdge('C', 'D');
graph.addEdge('C', 'G');
graph.addEdge('D', 'G');
graph.addEdge('D', 'H');
graph.addEdge('B', 'E');
graph.addEdge('B', 'F');
graph.addEdge('E', 'I');
console.log(graph)
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657247237699-f05993cd-dff4-4269-86f7-3a70e261e41a.png#clientId=uc8b0f51c-0f19-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=205&id=ub1bc864a&margin=%5Bobject%20Object%5D&name=image.png&originHeight=410&originWidth=740&originalType=binary&ratio=1&rotation=0&showTitle=false&size=31376&status=done&style=none&taskId=ud4a1859d-51ce-4353-b67b-fb4138ce758&title=&width=370)

![}A0G3MSGZVU0HVN%60825F4.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657247318888-f266db7a-e8d9-4365-bc13-96447e145627.jpeg#clientId=uc8b0f51c-0f19-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=ud12c64b7&margin=%5Bobject%20Object%5D&name=%7DA0G3MSGZVU0HVN%2560825F4.jpg&originHeight=790&originWidth=1024&originalType=binary&ratio=1&rotation=0&showTitle=false&size=42517&status=done&style=none&taskId=uf63df957-6b16-4464-a7dc-9b9ae5884a3&title=)


### 转换为字符串输出

 为图类Graph添加**toString方法，实现以邻接表的形式输出图中各顶点。**<br /> 

代码实现：

```javascript
Graph.prototype.toString = () => {
  let resultString = ''
  for (let i = 0; i < this.vertexes.length; i++) {
    resultString += this.vertexes[i] + ' ---> '
    let vEdge = this.edges.get(this.vertexes[i])
    for (let j = 0; j < vEdge.length; j++) {
      resultString += vEdge[j] + ' '
    }
    resultString += '\n'
  }
  return resultString
}
```

测试代码：

```javascript
console.log(graph.toString())
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657247685443-69575f1d-e752-483e-b8a4-7902ea87aa24.png#clientId=ua8b1b9d2-e898-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=307&id=u345154f6&margin=%5Bobject%20Object%5D&name=image.png&originHeight=218&originWidth=210&originalType=binary&ratio=1&rotation=0&showTitle=false&size=4587&status=done&style=none&taskId=u310074bb-620d-4e81-8ca5-cb4d34283e3&title=&width=296)


### 图的遍历

- 图的遍历思想：

   - 图的遍历思想与树的遍历思想一样，意味着需要**将图中所有的顶点都访问一遍，并且不能有重复的访问**

- 遍历图的两种算法

   - **广度优先搜索（Breach - First Serch，BFS）**

<br />

   - **深度优先搜索（Depth - First Serch ，DFS）**

   - 两种遍历算法都需要**指定第一个被访问的的顶点**

- 为了记录顶点是否被访问过，使用三种颜色来表示他们的状态

   - 白色：表示该顶点还**没有被**访问过

   - 灰色：表示该顶点**被**访问过，但其**相邻**顶点**并未完全被**访问过

   - 黑色：表示该顶点**被访问**过，且其相邻顶点都**被访问**过


首先封装`initializeColor`方法，将图中所有顶点初始化为白色，代码实现如下

```javascript
Graph.prototype.initializeColor = () => {
  let colors = []
  for (let i = 0; i < this.vertexes.length; i++) {
    colors[this.vertexes[i]] = 'white'
  }
  return colors
}
```


### 广度优先搜索

> - 广度优先搜索算法会从指定的**第一个顶点开始遍历图**，先**访问其所有的相邻顶点**，就像一次访问图的一层  
> 
> - 也可以说是**先宽后深**的遍历图中的各个顶点


![5MHP8)Z$GPW1IF`B0TG4XYW.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657249670995-30324ad7-0b15-488b-ac1d-fdf331be87d8.jpeg#clientId=ua8b1b9d2-e898-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=uf035b496&margin=%5Bobject%20Object%5D&name=5MHP8%29Z%24GPW1IF%60B0TG4XYW.jpg&originHeight=687&originWidth=1024&originalType=binary&ratio=1&rotation=0&showTitle=false&size=48469&status=done&style=none&taskId=u77ca0b46-99a1-4fe0-8144-db7da85ab44&title=)


实现思路：

基于队列可以简单地实现广度优先搜索算法：

- 首先创建一个**队列Q（尾部进，首部出）**；

- 调用封装的`initializeColor`方法将所有**顶点初始化为白色**；

- 指定**第一个顶点A**，将A标注为**灰色**（被访问过的节点），并将A放入队列Q中；

- 循环遍历队列中的元素，只要队列Q非空，就执行以下操作：

   - 先将**灰色的A从Q的首部取**出；

   - 取出A后，将**A的所有未被访问过（白色）的相邻顶点**依次从队列**Q的尾部加入队列，并变为灰色**。以此保证，灰色的相邻顶点不重复加入队列；

   - A的**全部相邻**节点加入Q后，**A变为黑色**，在下一次循环中被**移除Q外；**<br /> 

代码实现：

```javascript
Graph.prototype.bfs = (initV, handler) => {
  let colors = this.initializeColor()
  let que = new Queue()
  que.enqueue(initV)
  while(!que.isEmpty()){
    let v = que.dequeue()
    let vNeighbours = this.edges.get(v)
    colors[v] = 'gray'
    for (let i = 0; i < vNeighbours.length; i++) {
      const a = vNeighbours[i]
      if(colors[a] == 'white'){
        colors[a] = 'gray'
        que.enqueue(a)
      }
    }
    handler(v)
    colors[v] = 'black'
  }
}
```


测试代码：

```javascript
//4.测试bfs遍历方法
let result = ""
graph.bfs(graph.vertexes[0], function(v){
  result += v + "-"
})
console.log(result);
```


测试结果:

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657250087563-425765f0-bcd9-4e20-9359-7b2de57fa425.png#clientId=ua8b1b9d2-e898-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=316&id=ua76fad42&margin=%5Bobject%20Object%5D&name=image.png&originHeight=260&originWidth=255&originalType=binary&ratio=1&rotation=0&showTitle=false&size=6328&status=done&style=none&taskId=ub8811968-849a-4282-b2ea-56c993574e8&title=&width=309.5)


### 深度优先搜索

> - 深度优先搜索算法会从指定的**第一个顶点开始遍历图**，沿着**路经直到这条路径的最后一个顶点被访问了**
> 
> - 接着**原路回退**，并**探索下一条路径**


![NX%HQ~LWDK~H@GPYL47%38V.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657250367405-5bf93827-056a-4c66-b6b9-a59182afb9c3.jpeg#clientId=ua8b1b9d2-e898-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=ub120d94c&margin=%5Bobject%20Object%5D&name=NX%25HQ~LWDK~H%40GPYL47%2538V.jpg&originHeight=771&originWidth=1024&originalType=binary&ratio=1&rotation=0&showTitle=false&size=46584&status=done&style=none&taskId=u7e150b86-9341-44b8-b887-02cff816086&title=)


实现思路：

- 可以使用**栈结构来实现**深度优先搜索算法；

- 深度优先搜索算法的遍历顺序与二叉搜索树中的先序遍历较为相似，同样可以**使用递归来实现**（递归的本质就是函数栈的调用）。

- 基于递归实现深度优先搜索算法：定义**dfs方法**用于调用递归**方法dfsVisit**，定义**dfsVisit方法**用于**递归访问图中的各个顶点**。

- 在**dfs方法**中：

   - 首先，调用**initializeColor方法将所有顶点初始化为白色**；

   - 然后，调用**dfsVisit方法遍历图的顶点**；

- 在**dfsVisit方法**中：

   - 首先，将传入的指定节点**v标注为灰色；

**
   - 接着，**处理顶点V**；

   - 然后，访问**V的相邻顶点**；

   - 最后，将顶点**V标注为黑色**；<br /> 


代码实现：

```javascript
Graph.prototype.bfs = (initV, handler) => {
  let colors = this.initializeColor()
  let que = new Queue()
  que.enqueue(initV)
  while(!que.isEmpty()){
    let v = que.dequeue()
    let vNeighbours = this.edges.get(v)
    colors[v] = 'gray'
    for (let i = 0; i < vNeighbours.length; i++) {
      const a = vNeighbours[i]
      if(colors[a] == 'white'){
        colors[a] = 'gray'
        que.enqueue(a)
      }
    }
    handler(v)
    colors[v] = 'black'
  }
}
```


测试代码：

```javascript
//4.测试bfs遍历方法
let result = ""
graph.dfs(graph.vertexes[0], function(v){
  result += v + "-"
})
console.log(result);
```


测试结果:

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657251232066-6b3ed0ca-e7d6-4d0c-a1c8-f3494743734c.png#clientId=ua8b1b9d2-e898-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=300&id=u407d0601&margin=%5Bobject%20Object%5D&name=image.png&originHeight=320&originWidth=544&originalType=binary&ratio=1&rotation=0&showTitle=false&size=12974&status=done&style=none&taskId=ud5d5182c-dba7-4cdd-a1b1-d9581fab660&title=&width=510)



### 完整实现

```javascript
function Graph() {
  //属性：顶点（数组）/边（字典）
  this.vertexes = []//顶点
  this.edges = new Dictionary()//边

  Graph.prototype.addVertex = function (v) {
    this.vertexes.push(v)
    this.edges.set(v, [])
  }
  Graph.prototype.addEdge = (v1, v2) => {
    this.edges.get(v1).push(v2)
    this.edges.get(v2).push(v1)
  }
  Graph.prototype.toString = () => {
    let resultString = ''
    for (let i = 0; i < this.vertexes.length; i++) {
      resultString += this.vertexes[i] + ' ---> '
      let vEdge = this.edges.get(this.vertexes[i])
      for (let j = 0; j < vEdge.length; j++) {
        resultString += vEdge[j] + ' '
      }
      resultString += '\n'
    }
    return resultString
  }
  Graph.prototype.initializeColor = () => {
    let colors = []
    for (let i = 0; i < this.vertexes.length; i++) {
      colors[this.vertexes[i]] = 'white'
    }
    return colors
  }
  Graph.prototype.bfs = (initV, handler) => {
    let colors = this.initializeColor()
    let que = new Queue()
    que.enqueue(initV)
    while (!que.isEmpty()) {
      let v = que.dequeue()
      let vNeighbours = this.edges.get(v)
      colors[v] = 'gray'
      for (let i = 0; i < vNeighbours.length; i++) {
        const a = vNeighbours[i]
        if (colors[a] == 'white') {
          colors[a] = 'gray'
          que.enqueue(a)
        }
      }
      handler(v)
      colors[v] = 'black'
    }
  }

  Graph.prototype.dfs = (initV, handler) => {
    let colors = this.initializeColor()
    this.dfsVisit(initV, colors, handler)
  }
  Graph.prototype.dfsVisit = (v, colors, handler) => {
    colors[v] = 'gray'
    handler(v)
    let vNeighbours = this.edges.get(v)
    for (let i = 0; i < vNeighbours.length; i++) {
      let a = vNeighbours[i]
      if (colors[a] == 'white') {
        this.dfsVisit(a, colors, handler)
      }
    }
    colors[v] = 'black'
  }


}
let graph = new Graph()
let myVertexes = ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H', 'I']
for (let i = 0; i < myVertexes.length; i++) {
  graph.addVertex(myVertexes[i])
}
graph.addEdge('A', 'B');
graph.addEdge('A', 'C');
graph.addEdge('A', 'D');
graph.addEdge('C', 'D');
graph.addEdge('C', 'G');
graph.addEdge('D', 'G');
graph.addEdge('D', 'H');
graph.addEdge('B', 'E');
graph.addEdge('B', 'F');
graph.addEdge('E', 'I');
console.log(graph)
console.log(graph.toString())
//4.测试bfs遍历方法
let result = ""
graph.bfs(graph.vertexes[0], function (v) {
  result += v + "-"
})
console.log(result)
let result2 = ""
graph.dfs(graph.vertexes[0], function (v) {
  result2 += v + "-"
})
console.log(result2)
```



