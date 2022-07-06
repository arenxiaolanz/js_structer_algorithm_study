# 二、线性结构

## 2.1 数组`Array`

常见api：

- `push()`
- `unshift()`
- `shift()`
- `pop()`
- `concat()`
- `reverse()`
- `sort()`
- `join()`
- `indexOf()`
- `splice(index,num)`
- `splice(index,num,val)`

## 2.2 栈`Stack`

### 2.2.1 认识栈结构

- 栈也是一种非常常见的数据结构，并且在程序中的应用非常广泛
- 数组
   - 我们知道数组是一种线性结构，并且可以在数组的任意位置插入和删除数据
   - 但是有时候，我们为了实现某些功能，必须对这种任意性加以限制
   - 而栈和队列就是比较常见的受限的线性结构
- 栈（stack），它是一种受限的线性表，后进先出（LIFO：last in first out）
   - 其限制是仅允许在表的一端进行插入和删除运算。这一端被称为栈顶，另一端称为栈底。
   - LIFO表示就是后进入的元素，第一个弹出栈空间。
   - 向一个栈插入新元素又称作进栈、入栈或压栈，它是把新元素放到栈顶元素的上面，使之成为新的栈顶元素。
   - 从一个栈删除元素又称作出栈或退栈，它是把栈顶元素删除掉，使其相邻的元素成为新的栈顶元素。
- 生活中类似栈的
   - 收到的邮件
   - 自助餐的餐盘
- 程序中的栈结构
   - 函数调用栈   
      - A( B( C( D() ) ) )：即A函数中调用B，B调用C，C调用D
> 在A执行的过程中，A会被压入栈；随后B执行时，B被压入栈；C、D执行时也依次被压入栈 .
> 所以当前栈的顺序为：A（栈底）->B->C->D（栈顶）.
> 当函数D执行完后，会弹出栈被释放，弹出栈的顺序为：D->C->B->A .

   - 递归
> 为什么没有停止条件的递归会导致栈溢出？  
> 比如函数A为递归函数，不断的调用自己（因为函数还没有执行完，不会函数弹出栈），不停的把相同的的函数A压入栈，最后造成**栈溢出**(Stack Overfloat)

   - 练习，有6个元素6,5,4,3,2,1按顺序进栈，问下列哪个不是合法的出栈顺序？
      - A：5 4 3 6 1 2
      - B：4 5 3 2 1 6
      - C：3 4 6 5 2 1
      - D：2 3 4 1 5 6
> 正确答案：C  
> A：6 5进栈，5出栈，4进栈出栈，3进栈出栈，6出栈，2 1进栈，1 2出栈    
> B：6 5 4 进栈，4 5出栈，3进栈出栈，2进栈出栈，1进栈出栈，6出栈    
> D：6 5 4 3 2进栈，2 3 4出栈，1进栈出栈，5 6出栈    


### 2.2.2 栈结构封装

基于数组实现
```javascript
//封装栈类
function Stack(){
  //栈中的属性
  this.items = []
  //栈的相关操作
  //1.将元素压入栈
  //this.push = function(){
  //}
  Stack.prototype.push = (element) => {
    this.items.push(element)
  }
  //2.从栈中取出元素
  Stack.prototype.pop = () => {
    return this.items.pop()
  }  
  //3.查看栈顶元素
  Stack.prototype.peek = () => {
    return this.items[this.items.length - 1]
  }
  //4.判断栈是否为空
  Stack.prototype.isEmpty = () => {
    return this.items.length == 0
  }
  //5.获取栈中元素的个数
  Stack.prototype.Size = () => {
    return this.items.length
  }
  //6.toString方法
  Stack.prototype.toString = () => {
    return this.items.join('')
  }
}
//栈的使用
let s = new Stack()
s.push(4)
s.puhs(18)
s.push(6)
s.push(17)
s.pop()
s.peek()
s.Size()
s.isEmpty()
s.toString()
```
基于链表实现

### 2.2.3 栈常见的操作

- `push(element)`：添加一个元素到栈顶位置
- `pop()`：移除栈顶的元素，同时返回被移除的元素
- `peek()`：返回栈顶的元素，不对栈做任何修改
- `isEmpty()`：若为空，则返回true；否则，返回false
- `size()`：返回栈里的元素个数
- `toString()`：将栈的内容以字符形式返回

### 2.2.4 栈结构的简单封装

利用栈结构的特点封装十进制转二进制的函数
```javascript
//函数：将十进制转为二进制
function dec2bin(decNumber) {
  let stack = new Stack()
  while(decNumber > 0){
    stack.push(decNumber % 2)
    decNumber = Math.floor(decNumber / 2) 
  }
  let binaryStr = ''
  while(!stack.isEmpty()){
    binaryStr += stack.pop()
  }  
  return binaryStr
}
```

## 2.3 队列`Queue`

### 2.3.1 认识队列

- 队列(Queue)，它是一种受限的线性表，先进先出 (FIFO: First In First Out )
   - 受限之处在于它只允许在表的前端（front）进行删除操作
   - 在表的后端（rear）进行插入操作
- 生活中类似的队列结构
   - 排队买票，买饭，上厕所
   - 优先排队的人，优先处理

### 2.3.2 队列的应用

打印队列：计算机打印多个文件时，需要排队打印<br />线程队列：当开启多线程时，若新开启的线程，所需要的资源不足时，就先放入线程队列，等待CPU处理
### 2.3.3 队列类的实现

队列类的实现和栈一样，有两种方案：<br />基于数组实现
```javascript
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
let queue = new Queue()
queue.enqueue(4);
queue.enqueue(18);
queue.enqueue(6);
queue.enqueue(17);
queue.dequeue();
queue.front();
queue.isEmpty();
queue.size();
queue.toString();
```
基于链表实现

### 2.3.4 队列常见的操作

- `enqueue(element)`:向队列尾部添加一个（或多个）新的项.
- `dequeue()`:移除队列的第一（即排在队列最前面的）项，并返回被移除的元素.
- `front()`:返回队列中的一个元素（最先被添加，也将是最先被移除的元素），队列不做任何变动（不移除元素，只返回元素信息，与Stack的peek()方法类似）.
- `isEmpty()`:若队列为空，返回true，否则，返回false.
- `size()`:返回队列包含的元素个数.
- `toString()`:将队列中的内容，转为字符串形式.

### 2.3.5 队列的应用

> 使用队列实现小游戏：击鼓传花，传入一组数据和设定的的数字num，循环遍历数组内元素，遍历到的元素为制定数字num时将该元素删除，直至数组剩下一个元素。
> (从第一个人开始，按顺序数1,2,3----num，数到num的那个人淘汰，从被淘汰的下一个人再开始按顺序数1,2,3---num，以此类推，求最后剩下的那个人的名字，及在数组中的位置下标)

代码实现：
```javascript
let passGame = (nameList, num) => {
  let queue = new Queue()
  for (let i of nameList) {
    queue.enqueue(i)
  }
  while (queue.size() > 1) {
    for (let i = 0; i < num-1; i++) {
      queue.enqueue(queue.dequeue())
    }
    queue.dequeue()
  }
  console.log(queue.size())
  let endName = queue.front()
  console.log(endName)
  return nameList.indexOf(endName)
}
let names = ['aiba', 'ohno', 'nino', 'sho', 'mj']
console.log(passGame(names, 3))
```
结果展示<br />![-16a1c9946c103abb.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656169397329-3077fd5a-48c9-42b3-9f42-484f3ecace49.png#crop=0&crop=0&crop=1&crop=1&from=url&height=396&id=cx1DJ&margin=%5Bobject%20Object%5D&name=-16a1c9946c103abb.png&originHeight=778&originWidth=1140&originalType=binary&ratio=1&rotation=0&showTitle=false&size=149496&status=done&style=none&title=&width=580)

### 2.3.6 优先队列

优先队列主要考虑的问题为：

- 每个元素不再只是一个数据，还包含数据的优先级
- 在添加数据过程中，根据优先级放入到正确位置

#### 2.3.6.1 优先级队列的实现

代码实现：
```javascript
//封装优先级队列
function PriorityQueue() {
  //内部类，在类里面再封装一个类，表示带优先级的数据
  function QueueElement(element, priority) {
    this.element = element
    this.priority = priority
  }
  //封装属性
  this.items = []
  //1.实现按照优先级插入方法
  PriorityQueue.prototype.enqueue = (element, priority) => {
    let queueElement = new QueueElement(element, priority)
    if (this.items.length === 0) {
      this.items.push(queueElement)
    } else {
      let added = false
      for (let i of this.items) {
        if (queueElement.priority < i.priority) {
          this.items.splice(i, 0, queueElement)
          added = true
          break
        }
      }
      if (!added) {
        this.items.push(queueElement)
      }
    }
  }
  //2.dequeue:删除队列前端的元素
  PriorityQueue.prototype.dequeue = () => {
    return this.items.shift()
  }
  //3.front:查看前端的元素
  PriorityQueue.prototype.front = () => {
    return this.items[0]
  }
  //4:isEmpty:查看队列元素是否为空
  PriorityQueue.prototype.isEmpty = () => {
    return this.items.legth === 0
  }
  //5.size:查看队列中元素的个数
  PriorityQueue.prototype.size = () => {
    return this.items.length
  }
  //6.toString:以字符串形式输出队列中的元素
  PriorityQueue.prototype.toString = () => {
    let resultString = ''
    for (let i of this.items) {
      resultString += i.element + '-' + i.priority + ''
    }
    return resultString
  }
}
//测试代码
let pq = new PriorityQueue()
pq.enqueue('nino', 617)
pq.enqueue('ren', 418)
pq.enqueue('money', 999)
console.log(pq)
```
测试结果<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656173605937-b9c4b6bb-d597-4ae6-b3a3-8ef9214831cb.png#clientId=u27c3d88f-f1b9-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=211&id=R0rmE&margin=%5Bobject%20Object%5D&name=image.png&originHeight=421&originWidth=1506&originalType=binary&ratio=1&rotation=0&showTitle=false&size=107826&status=done&style=none&taskId=ub421f5e6-47e3-42e9-9beb-2c7d822febf&title=&width=755)

#### 2.3.6.2 注意点

- 关于数组splice方法
   - `splice(1,0,'nino')`：表示在索引为1的位置，删除0个元素，插入一个"nino"元素
   - `splice(1,1,'nino')`：表示在索引为1的位置，删除1个元素，插入一个"nino"元素
- 数组的push方法在数组、栈和队列中的表现形式
   - 数组：在数组［0,1,2］中，执行push（3），结果为［0,1,2,3］
   - 栈：stack.push()方法，执行push（0），push（1），push（2），其数组的顺序为［0,1,2］，但是索引为2的元素其实是栈顶元素；所以栈的push方法是向栈顶添加元素（但在数组的视角下，为向数组尾部添加元素）
   - 队列：queue.enqueue()方法，其实是由数组的push()方法实现，相当于在数组头部增加元素

## 2.4 单向链表`Linked List`

### 2.4.1 单向链表的优势

- 要存储多个元素，另外一个选择就是链表   
- 但不同于数组，链表中的元素在内存中不必是连续的空间   
- 链表的每个元素由一个存储元素本身的节点和一个指向下一个元素的引用（指针）组成   
- 相对于数组，链表有一些**优点**：
   - 内存空间不必是连续的，可以充分利用计算机的内存，实现灵活的内存动态管理
   - 链表不必在创建时就确定大小，并且大小可以无限的延伸下去
   - 链表在插入和删除数据时，时间复杂度可以达到O(1)，相对数组效率高很多
- 相对于数组，链表有一些_**缺点**_：
   - 链表访问任何一个位置的元素时，都需要从头开始访问（无法跳过第一个元素访问任何一个元素）
   - 无法通过下标直接访问元素，需要从头一个个访问，直到找到对应的元素

### 2.4.2 单向链表的结构

![1ec25d48c58968aa.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656208484117-b6e8fddc-a2e4-4379-9c7b-2bba2f9ac7df.png#crop=0&crop=0&crop=1&crop=1&from=url&id=ONy5W&margin=%5Bobject%20Object%5D&name=1ec25d48c58968aa.png&originHeight=173&originWidth=803&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36703&status=done&style=none&title=)

- head属性指向链表的第一个节点
- 链表的最后一个节点指向null
- 当链表中一个节点也没有的时候，head直接指向null

### 2.4.3 链表中的常见操作

- `append(element)`:向链表尾部添加一个新的项
- `insert(position,element)`:向链表的特定位置插入一个新的项
- `get(position)`:获取对应位置的元素
- `indexOf(element)`:返回元素在链表中的索引，若没有该元素则返回－1
- `update(position,element)`:修改某个位置的元素
- `removeAt(positin)`:从链表的特定位置移除一项
- `remove(element)`:从链表中移除一项
- `isEmpty()`:若链表无任何元素，则返回true，否则返回false
- `size()`:返回链表包含的元素个数
- `toString()`:由于链表使用了Node类，就需要重写继承自JS对象默认的tosString方法，让其只输出元素的值

### 2.4.5 封装单向链表类

1. 创建单项列表类

代码实现：

```javascript
function LinkedList() {
  //Node类的封装
  function Node(data){
    this.data = data
    this.next =  null
  }
  //属性
  //属性head指向链表的第一个值
  this.head = null
  this.length = 0
}
```

2. append(element)
- 代码实现：

```javascript
LinkedList.prototype.append = (data) => {
  let newNode  =new Node(data)
  //添加新节点
  //情况一：链表中没有节点时
  if(this.length === 0){
    this.head = newNode
  }
  //情况二：链表中有节点时
  else {
    //
    let current = this.head
    //只要某个节点的next不为空，就一直向后找，相当于找到最后一个节点，因为最后一个节点的next为null
    //节点的next永远指向下一个节点（data，next）
    while(current.next){
      current = current.next
    }
    //让最后一个节点的next指向新添加的节点（data，next）
    current.next = newNode
  }
  this.length += 1
}
```

- 过程详解：

首先让current指向第一个节点：

![-75688b3f086b7864.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656213043974-779148ab-43ec-4ccc-ade6-0b9ca152778d.png#crop=0&crop=0&crop=1&crop=1&from=url&id=d7euB&margin=%5Bobject%20Object%5D&name=-75688b3f086b7864.png&originHeight=161&originWidth=502&originalType=binary&ratio=1&rotation=0&showTitle=false&size=24141&status=done&style=none&title=)

通过while循环使current指向最后一个节点，最后通过`current.next = newNode`，让最后一个节点指向新节点newNode

![-5251bed7e5d03aa9.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656213085362-7cb62775-f7dc-4b8a-ac3c-b05692848661.png#crop=0&crop=0&crop=1&crop=1&from=url&id=pEaKq&margin=%5Bobject%20Object%5D&name=-5251bed7e5d03aa9.png&originHeight=168&originWidth=504&originalType=binary&ratio=1&rotation=0&showTitle=false&size=25669&status=done&style=none&title=)

- 测试代码：

```javascript
let linkedlist = new LinkedList()
linkedlist.append('123')
linkedlist.append('nino')
linkedlist.append('rxl')
console.log(linkedlist)
```

- 测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656213724720-e4e825ed-9498-42b9-bb63-3d3daef2ad7b.png#clientId=u8a519891-6f44-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=337&id=CpyyN&margin=%5Bobject%20Object%5D&name=image.png&originHeight=345&originWidth=479&originalType=binary&ratio=1&rotation=0&showTitle=false&size=21039&status=done&style=none&taskId=u65537875-602e-4b99-8c82-4ea98e5e8c8&title=&width=467.5)

3. toString()

代码实现：

```javascript
LinkedList.prototype.toString = () => {
  let current = this.head
  let listStr = ''
  while(current){
    listStr += current.data + ''
    current = current.next
  }
  return listStr
}
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656214502656-c4dfbefe-7c96-402c-bd93-4860a9265252.png#clientId=u8a519891-6f44-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=380&id=yV27u&margin=%5Bobject%20Object%5D&name=image.png&originHeight=383&originWidth=426&originalType=binary&ratio=1&rotation=0&showTitle=false&size=22046&status=done&style=none&taskId=ub00d8498-6a0c-4271-a978-29a4f8b9623&title=&width=423)

4. insert(position,element)

代码实现：  

```javascript
LinkedList.prototype.insert = (position,data) => {
//理解position的含义：
//position=0:表示新节点插入后要成为第一个节点
//position=2:表示新节点插入后要成为第三个节点
  //对position进行越界判断：要求传入的position不能是负数且不能超过linkedlist的length
  if(position < 0 || position > this.length){
    return false
  }
  let newNode = new Node(data)
  //情况1：position＝0
  if(position === 0){
    //让新节点指向当前列表的第一个节点
    newNode.next = this.head
    //让head指向新节点，成为新的第一个节点
    this.head = newNode
  }
  //情况2:position>0 ＆＆ position<this.length
  else {
    let index = 0
    let previous = null
    let current = this.head
    //通过while循环，使current指向当前索引为position的节点
    while(index++ < position){
      previous = current
      current = current.next
    }
    newNode.next = current
    previous.next = newNode
  }
  //
  this.length += 1
  return true
}
```

过程详解：  <br />insert方法实现的过程中，根据插入节点位置的不同可分为多个情况：    

- 情况1：position ＝ 0    

通过`newNode.next = this.head`，建立连接1   <br />通过`this.head = newNode`，建立连接2   

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656217359210-08e4390e-5d84-426e-86df-4e6d81586121.png#clientId=u8a519891-6f44-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=188&id=PHth0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=190&originWidth=394&originalType=binary&ratio=1&rotation=0&showTitle=false&size=27495&status=done&style=none&taskId=ud0d49827-1985-40e2-a16a-1add1aa82d7&title=&width=389)

- 情况2：position ＝ 0    

首先定义两个变量previous和current分别指向需要插入位置`pos=x`的前一个节点和后一个节点     <br />然后，通过`newNode.next=current`，改变指向1   <br />最后，通过`previous.next=newNode`，改变指向2    

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656217417061-592013d8-ca56-49bb-b9dc-294d128c5708.png#clientId=u8a519891-6f44-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=181&id=QqxBU&margin=%5Bobject%20Object%5D&name=image.png&originHeight=138&originWidth=303&originalType=binary&ratio=1&rotation=0&showTitle=false&size=17980&status=done&style=none&taskId=u408e5c3e-29c4-44ca-ad1d-4e3559980ea&title=&width=398.5)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656217443890-75e684c8-f769-4541-80fb-c38fbc96d38b.png#clientId=u8a519891-6f44-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=169&id=NCaF1&margin=%5Bobject%20Object%5D&name=image.png&originHeight=136&originWidth=322&originalType=binary&ratio=1&rotation=0&showTitle=false&size=19533&status=done&style=none&taskId=u5150b2ee-7316-4d6f-9ca9-fe2e177f499&title=&width=401)

测试代码：

```javascript
linkedlist.insert(0,"在链表最前面插入节点")
linkedlist.insert(2,"在链表中第二个节点后插入节点")
linkedlist.insert(5,"在链表最后插入节点")
console.log(linkedlist)
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656217278763-87e525f0-6bfe-4450-97eb-d606b255ccfb.png#clientId=u8a519891-6f44-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=458&id=P1Tpy&margin=%5Bobject%20Object%5D&name=image.png&originHeight=634&originWidth=568&originalType=binary&ratio=1&rotation=0&showTitle=false&size=53356&status=done&style=none&taskId=u550889c0-789d-4fcc-949f-f80f5c0ea8d&title=&width=410)

5. get(position)

代码实现：

```javascript
LinkedList.prototype.get = (position) => {
  //
  if(position < 0 || position > this.length){
    return null
  }
  let current = this.head
  let index = 0
  while(index++ < position){
    current = current.next
  }
    return current.data
}
```

测试代码：
```javascript
console.log(linkedlist.get(0))
console.log(linkedlist.get(2))
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656220716104-a4e2d680-daa3-4cfa-82ab-21ea68572bfd.png#clientId=u8a519891-6f44-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=182&id=jayr2&margin=%5Bobject%20Object%5D&name=image.png&originHeight=186&originWidth=435&originalType=binary&ratio=1&rotation=0&showTitle=false&size=16838&status=done&style=none&taskId=ua9c88072-e9ec-4007-a849-04bb63d4393&title=&width=425.5)

6. indexOf(element)

代码实现：
```javascript
LinkedList.prototype.indexOf = data => {
  let current = this.head
  let index = 0
  while(current){
    if(current.data === data){
      return index
    }
    current = current.next
    index += 1
  }
  return -1
}
```

测试代码：
```javascript
console.log(linkedlist.indexOf("nino"))
console.log(linkedlist.indexOf("rxl"))
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656221154069-81f6a3a9-e811-4592-bf62-786b1baa5543.png#clientId=uee96129e-b0d0-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=227&id=ThOvP&margin=%5Bobject%20Object%5D&name=image.png&originHeight=234&originWidth=460&originalType=binary&ratio=1&rotation=0&showTitle=false&size=16676&status=done&style=none&taskId=ua824f838-fe17-438f-abe6-5797cbdeb1b&title=&width=446)

7. update(position,element)

代码实现：
```javascript
LinkedList.prototype.update = (position,newData) => {
  if(position <0 || position > this.length){
    return false
  }
  let current = this.head
  let index = 0
  while(index++ < position){
    current = curretn.next
  }
  current.data = newData
  return true
}
```

测试代码：
```javascript
linkedlist.update(0,"ohno")
console.log(linkedlist)
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656221777112-8a4c6dba-53df-4e79-94d7-516c082342cb.png#clientId=ua7719dd8-56aa-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=463&id=sKsOM&margin=%5Bobject%20Object%5D&name=image.png&originHeight=569&originWidth=602&originalType=binary&ratio=1&rotation=0&showTitle=false&size=43867&status=done&style=none&taskId=u987f8fb9-e86e-40f0-a4b5-f08d9436c5d&title=&width=490)

8. removeAt(position)

代码实现：
```javascript
//7、removeAt（position）
LinkedList.prototype.removeAt = (position) => {
  if (position < 0 || position > this.length) {
    return null
  }
  let current = this.head
  if (position == 0) {
    this.head = this.head.next
  }
  else {
    let index = 0
    let previous = null
    while (index++ < position) {
      previous = current
      current = current.next
    }
    previous.next = current.next
  }
  this.length -= 1
  return current.data
}
```

测试代码：
```javascript
linkedlist.removeAt(0)
linkedlist.removeAt(2)
console.log(linkedlist)
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656222711311-ac1b087c-8037-448f-8b0b-f8be1041e488.png#clientId=uf109e92d-0872-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=452&id=xalqg&margin=%5Bobject%20Object%5D&name=image.png&originHeight=462&originWidth=479&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36625&status=done&style=none&taskId=u8d1cb95e-cf49-43fd-bd27-03e0b134035&title=&width=468.5)

9. 其他方法

其他方法包括：`remove()、isEmpty()、size() `<br />代码实现：
```javascript
//8、remove（element）
LinkedList.prototype.remove = (data) => {
  let position = this.indexOf(data)
  return this.removeAt(position)
}
//9、isEmpty（）
LinkedList.prototype.isEmpty = () => {
  return this.length === 0
}
//10、size（）
LinkedList.prototype.size = () => {
  return this.length
}
```

测试代码：
```javascript
linkedlist.remove("123")
console.log(linkedlist)
console.log(linkedlist.isEmpty())
console.log(linkedlist.size())
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656222916425-ab7e2d5c-e161-4b1f-a1ef-c662d69efad8.png#clientId=uf109e92d-0872-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=155&id=XTIWi&margin=%5Bobject%20Object%5D&name=image.png&originHeight=284&originWidth=1308&originalType=binary&ratio=1&rotation=0&showTitle=false&size=71076&status=done&style=none&taskId=uda28a562-fcf9-404b-94b4-6ec0dfa638b&title=&width=712)

### 2.4.6 完整实现
```javascript
//封装链表类
function LinkedList() {
  //封装一个内部类，节点类
  function Node(data) {
    this.data = data
    this.next = null
  }
  //属性
  //属性head指向链表的第一个节点
  this.head = null
  this.length = 0
  //1、append（element）
  LinkedList.prototype.append = (data) => {
    let newNode = new Node(data)
    //添加新节点
    //情况一：链表中没有节点时
    if (this.length === 0) {
      this.head = newNode
    }
    //情况二：链表中有节点时
    else {
      //
      let current = this.head
      //只要某个节点的next不为空，就一直向后找，相当于找到最后一个节点，因为最后一个节点的next为null
      //节点的next永远指向下一个节点（data，next）
      while (current.next) {
        current = current.next
      }
      //让最后一个节点的next指向新添加的节点（data，next）
      current.next = newNode
    }
    this.length += 1
  }
  //2、toString（）
  LinkedList.prototype.toString = () => {
    let current = this.head
    let listStr = ''
    while (current) {
      listStr += current.data + ''
      current = current.next
    }
    return listStr
  }
  //3、insert（position，element）
  LinkedList.prototype.insert = (position, data) => {
    //理解position的含义：
    //position=0:表示新节点插入后要成为第一个节点
    //position=2:表示新节点插入后要成为第三个节点
    //对position进行越界判断：要求传入的position不能是负数且不能超过linkedlist的length
    if (position < 0 || position > this.length) {
      return false
    }
    let newNode = new Node(data)
    //情况1：position＝0
    if (position === 0) {
      //让新节点指向当前列表的第一个节点
      newNode.next = this.head
      //让head指向新节点，成为新的第一个节点
      this.head = newNode
    }
    //情况2:position>0 ＆＆ position<this.length
    else {
      let index = 0
      let previous = null
      let current = this.head
      //通过while循环，使current指向当前索引为position的节点
      while (index++ < position) {
        previous = current
        current = current.next
      }
      newNode.next = current
      previous.next = newNode
    }
    //
    this.length += 1
    return true
  }
  //4、get（position）
  LinkedList.prototype.get = (position) => {
    //
    if (position < 0 || position > this.length) {
      return null
    }
    let current = this.head
    let index = 0
    while (index++ < position) {
      current = current.next
    }
    return current.data
  }
  //5、indexOf（element）
  LinkedList.prototype.indexOf = data => {
    let current = this.head
    let index = 0
    while (current) {
      if (current.data === data) {
        return index
      }
      current = current.next
      index += 1
    }
    return -1
  }
  //6、update（position，element）
  LinkedList.prototype.update = (position, newData) => {
    if (position < 0 || position > this.length) {
      return false
    }
    let current = this.head
    let index = 0
    while (index++ < position) {
      current = curretn.next
    }
    current.data = newData
    return true
  }
  //7、removeAt（position）
  LinkedList.prototype.removeAt = (position) => {
    if (position < 0 || position > this.length) {
      return null
    }
    let current = this.head
    if (position == 0) {
      this.head = this.head.next
    }
    else {
      let index = 0
      let previous = null
      while (index++ < position) {
        previous = current
        current = current.next
      }
      previous.next = current.next
    }
    this.length -= 1
    return current.data
  }
  //8、remove（element）
  LinkedList.prototype.remove = (data) => {
    let position = this.indexOf(data)
    return this.removeAt(position)
  }
  //9、isEmpty（）
  LinkedList.prototype.isEmpty = () => {
    return this.length === 0
  }
  //10、size（）
  LinkedList.prototype.size = () => {
    return this.length
  }
}
let linkedlist = new LinkedList()
linkedlist.append('123')
linkedlist.append('nino')
linkedlist.append('rxl')
console.log(linkedlist)
console.log(linkedlist.toString())
linkedlist.insert(0, "在链表最前面插入节点")
linkedlist.insert(2, "在链表中第二个节点后插入节点")
linkedlist.insert(5, "在链表最后插入节点")
console.log(linkedlist)
console.log(linkedlist.get(0))
console.log(linkedlist.get(2))
console.log(linkedlist.indexOf("nino"))
console.log(linkedlist.indexOf("rxl"))
linkedlist.update(0, "ohno")
console.log(linkedlist)
linkedlist.removeAt(0)
linkedlist.removeAt(2)
console.log(linkedlist)
linkedlist.remove("123")
console.log(linkedlist)
console.log(linkedlist.isEmpty())
console.log(linkedlist.size(2))
```

## 2.5 双向链表`Linked List`

### 2.5.1 双向链表简介

- 既可以**从头遍历到尾，**又可以**从尾遍历到头**。
- 也就是说链表相连的过程是双向的。
- 其实现原理是：一个节点既有向前连接的引用，也有一个向后连接的引用。
- 双向链表可以有效的解决单向链表中提到的问题。

### 2.5.2 双向链表的缺点

- 每次在插入或删除某个节点时，需要处理四个引用，而不是两个，也就是实现起来要困难一些
- 相对于单向链表，所占内存空间更大一些
- 但是，相对于双向链表的便利性而言，这些缺点微不足道

### 2.5.3 双向链表的结构

![7bb9a70ad3be0877.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656899606014-96ad5fa7-54d7-4328-bf60-31b631b96b73.png#crop=0&crop=0&crop=1&crop=1&from=url&id=PaLNQ&margin=%5Bobject%20Object%5D&name=7bb9a70ad3be0877.png&originHeight=207&originWidth=1028&originalType=binary&ratio=1&rotation=0&showTitle=false&size=93510&status=done&style=none&title=)

 特点：

- 双向链表不仅有**head**指针指向第一个节点，而且有**tail**指针指向最后一个节点
- 每个节点有三部分组成：**item**储存数据，**prev**指向前一个节点，**next**指向后一个节点
- 双向链表的一个节点的prev指向**null**
- 双向链表的最后一个节点的next指向**null**

### 2.5.4  双向链表常见的操作

- `append(element)`:向链表尾部添加一个新的项
- `inset(position,element)`:向链表的特定位置插入一个新的项
- `get(element)`:获取对应位置的元素
- `indexOf(element)`:返回元素在链表中的索引，若无则返回－1
- `update(position,element)`:修改某个位置的元素
- `removeAt(position)`:从链表的特定位置移除一项
- `remove(element)`:从列表中移除一项
- `isEmpty()`:如果链表中不含任何元素，返回true，否则返回false
- `size()`:返回链表中元素个数
- `toString()`:让其输出元素的值
- `forwardString()`:返回正向遍历节点字符串形式
- `backwordString()`:返回反向遍历的节点字符串形式

### 2.5.5 封装双向链表类

0.创建双向链表类
```javascript
//封装双向链表类
function DoublyLinkedList(){
//封装内部类，节点类
  function Node(data){
    this.data = data
    this.prev = null
    this.next = null
  }
//属性
  this.head = null
  this.tail = null
  this.length = 0
}
```

1. append(element)

- 代码实现：
```javascript
DoublyLinkedList.prototype.append = data => {
  let newNode = new Node(data)
  if(this.length === 0){
    this.tail = newNode
    this.head = newNode
  }
  else{
    newNode.prev = this.tail
    this.tail.next = newNode
    this.tail = newNode
  }
  this.length += 1
}
```

- 过程详解：

添加节点时分为多个情况：

   - 情况1：添加的是第一个节点：只需要让head和tail都指向新节点即可
   - 情况2：链表中已经存在数据
      - 首先tail中的next之前指向的是null. 现在应该指向新的节点newNode: this.tail.next = newNode
      - 因为是双向链表, 新节点的next/tail目前都是null. 但是作为最后一个节点, 需要有一个指向前一个节点的引用. 所以这里我们需要newNode.prev = this.tail
      - 因为目前newNod已经变成了最后的节点, 所以this.tail属性的引用应该指向最后: this.tail = newNode即可

- 测试代码：
```javascript
let list = new DoublyLinkedList()
list.append('aaa')
list.append('bbb')
list.append('ccc')
console.log(list)
```

- 测试结果

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656906490230-2f8c79ee-1dc0-4b08-ae4a-7f166cc749df.png#clientId=u6430b540-2302-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=338&id=Ktzg7&margin=%5Bobject%20Object%5D&name=image.png&originHeight=338&originWidth=493&originalType=binary&ratio=1&rotation=0&showTitle=false&size=24326&status=done&style=none&taskId=u660e8f19-e30d-47b4-a2f9-dab68962c9c&title=&width=493)

2. toString()汇总

- 代码实现：
```javascript
//toString
DoublyLinkedList.prototype.toString = () => {
  return this.backwardString()
}
//forwardString
DoublyLinkedList.prototype.forwardString = () => {
  let current = this.tail
  let resultString = ""
  while(current) {
    resultString += current.data + '--'
    current = current.prev
  }
  return resultString
}
//backwordString
DoublyLinkedList.prototype.backwardString = () => {
  let current = this.head
  let resultString = ""
  while(current){
    resultString += current.data + "--"
    current = current.next
  }
  return resultString
}
```

- 过程详解：

三种获取字符串的方法：toString（）、forwardString（）、backwardString（）实现原理相似，仅以backWardString方法为例：     <br />定义current变量记录当前指向的节点。首先让current指向第一个节点，然后通过 current = current.next 依次向后遍历。在while循环中以(current)作为条件遍历链表，只要current ！= null就一直遍历，由此可获取链表所有节点的数据。   

- 测试代码：
```javascript
console.log(list.toString())
console.log(list.backwardString())
console.log(list.forwardString())
```

- 测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656909701211-dfebed03-d6d0-46ec-823b-070e3965bad1.png#clientId=u6430b540-2302-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=99&id=TVFWP&margin=%5Bobject%20Object%5D&name=image.png&originHeight=99&originWidth=168&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2377&status=done&style=none&taskId=u4265fa61-d3f8-4d3a-af81-03cf29d347b&title=&width=168)

3.insert(position,element)

- 代码实现：
```javascript
DoublyLinkedList.prototype.insert = (pos,data) => {
  if(pos < 0 || pos > this.length ) return false
  let newNode = new Node(data)
  if(this.length === 0){
    this.head = newNode
    this.tail = newNode
  }
  else{
    if(pos == 0) {
      this.head.prev = newNode
      newNode.next = this.head
      this.head = newNode
    }
    else if(pos == this.length) {
      this.tail.next = newNode
      newNode.prev = this.tail
      this.tail = newNode
    }
    else {
      let current = this.head
      let index = 0
      while(index++ <pos) {
        previous = current
        current = current.next
      }
      newNode.next = current
      newNode.prev = current.prev
      previous.next = newNode
      current.prev = newNode
    }
  }
  this.length += 1
  return true
}
```

- 过程详解：

当原列表为空时：

   - 情况1：插入的新节点是链表的第一个节点；只需要让head和tail都指向newNode即可。    
   - <br />

当原列表不为空时：

   - 情况1：当position == 0，即在链表的首部添加节点

![-69cd21ee82bed75f.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656911315023-ffafa9fa-45ac-4b61-b39c-1b8e349e8019.png#crop=0&crop=0&crop=1&crop=1&from=url&id=yhxwr&margin=%5Bobject%20Object%5D&name=-69cd21ee82bed75f.png&originHeight=243&originWidth=625&originalType=binary&ratio=1&rotation=0&showTitle=false&size=38665&status=done&style=none&title=)<br />首先，通过：this.head.prev = newNode，改变指向1； <br />然后，通过：newNode.next = this.head，改变指向2； <br />最后，通过：this.head = newNode，改变指向3； 

   - 情况2：position == this.length，即在链表的尾部添加节点

![-5eeda181674f5b32.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1656911799463-ee33daed-bd69-472c-a6e7-213b876eddb5.jpeg#crop=0&crop=0&crop=1&crop=1&from=url&id=f96YY&margin=%5Bobject%20Object%5D&name=-5eeda181674f5b32.jpg&originHeight=337&originWidth=1024&originalType=binary&ratio=1&rotation=0&showTitle=false&size=31013&status=done&style=none&title=)

首先，通过：this.tail.next = newNode，改变指向1；（注意这里使用this.tail指向原链表最后一个节点，而不是this.head。因为当length>1时，this.head != this.tail。）     <br />然后，通过：newNode.prev = this.tail，改变指向2；     <br />最后，通过：this.tail = newNode，改变指向3；     

   - 情况3：将元素插入到中间位置

![-574e7d1e4ad0e2b9.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1656912094016-16fbd078-baed-462d-a2bf-ccdd08c7d96c.jpeg#crop=0&crop=0&crop=1&crop=1&from=url&id=wCo48&margin=%5Bobject%20Object%5D&name=-574e7d1e4ad0e2b9.jpg&originHeight=349&originWidth=1024&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36656&status=done&style=none&title=)

首先，需要定义变量current按照之前的思路，通过while循环找到position位置的后一个节点，循环结束后index = position    <br />当position = 1时，current就指向了Node2。这样操作current就等同于间接地操作Node2，还可以通过current.prev间接获取Node1。得到了newNode的前一个节点和后一个节点就可以通过改变它们的prev和next变量的指向来插入newNode了。      <br />通过：newNode.next = current，改变指向1；     <br />通过：newNode.prev = current.prev，改变指向2；     <br />通过：current.prev.next = newNode，改变指向3；    <br />注意必须最后才修改current.prev的指向，不然就无法通过current.prev获取需要操作的Node1了。     <br />通过：current.prev = current，改变指向4；      

- 测试代码：
```javascript
list.insert(0, '插入链表的第一个元素')
list.insert(0, '在链表首部插入元素')
list.insert(1, '在链表中间插入元素')
list.insert(6, '在链表尾部插入元素')
console.log(list);
```

- 测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656912448349-3da2097d-6d88-4536-9a7e-0afe32ef8e73.png#clientId=u6430b540-2302-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=539&id=uj2bV&margin=%5Bobject%20Object%5D&name=image.png&originHeight=539&originWidth=519&originalType=binary&ratio=1&rotation=0&showTitle=false&size=53688&status=done&style=none&taskId=u789f2c36-0366-4b7e-9d05-ba90a3dfe21&title=&width=519)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656912502096-e1a24fb6-e60e-4eb2-b1b5-39873446938e.png#clientId=u6430b540-2302-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=527&id=TGvEi&margin=%5Bobject%20Object%5D&name=image.png&originHeight=527&originWidth=513&originalType=binary&ratio=1&rotation=0&showTitle=false&size=54565&status=done&style=none&taskId=ufa285f83-bc64-4d4b-9354-e78a53fbec7&title=&width=513)
### 

4. get(position)
- 代码实现：
```javascript
DoublyLinkedList.prototype.get = pos => {
  if(pos < 0 || pos > this.length) return null
  let current = null
  let index = 0
  if((this.length / 2) > pos ){
    current = this.head
    while(index++ < pos){current = current.next}
  }
  else{
    current = this.tail
    index = this.length - 1
    while(index-- > pos ){current = current.prev}
  }
  return current.data
}
```

- 过程详解：

定义两个变量current和index，按照之前的思路通过while循环遍历分别获取当前节点和对应的索引值index，直到找到需要获取的position位置后的一个节点，此时index = pos =x，然后return current.data即可。       <br />如果链表的节点数量很多时，这种查找方式效率不高，改进方法为：     <br />一定要通过this.length来获取链表的节点数否则就会报错。      <br />当this.length / 2 > position：从头（head）开始遍历；     <br />当this.length / 2 < position：从尾（tail）开始遍历；     

- 测试代码：
```javascript
console.log(list.get(0))
console.log(list.get(5))
```

- 测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656913663914-99bf189d-07ce-418b-bca9-e6e1aefef35e.png#clientId=u6430b540-2302-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=51&id=LI62U&margin=%5Bobject%20Object%5D&name=image.png&originHeight=51&originWidth=155&originalType=binary&ratio=1&rotation=0&showTitle=false&size=974&status=done&style=none&taskId=uf75c9cbf-2628-4ee4-a203-37ef29cd257&title=&width=155)

5. indexOf(element)
- 代码实现：
```javascript
      DoublyLinkedList.prototype.indexOf = data => {
        //1.定义变量
        let current = this.head
        let index = 0

        //2.遍历链表，查找与data相同的节点
        while(current){
          if (current.data == data) {
            return index
          }
          current = current.next
          index += 1
        }
        return -1
      } 

```

- 过程详解：

以（current）作为条件，通过while循环遍历链表中的所有节点（停止条件为current = null）。在遍历每个节点时将current指向的当前节点的data和传入的data进行比较即可。  

- 测试代码：
```javascript
console.log(list.indexOf('aaa'))
console.log(list.indexOf('ccc'))
```

- 测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656914021423-feb6689b-7343-4f5d-bc57-e077eda7fbb1.png#clientId=u6430b540-2302-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=49&id=KIXME&margin=%5Bobject%20Object%5D&name=image.png&originHeight=49&originWidth=67&originalType=binary&ratio=1&rotation=0&showTitle=false&size=481&status=done&style=none&taskId=u513e89fc-8916-4afd-87f3-6510e24b036&title=&width=67)

6. update(position,element)
- 代码实现：
```javascript
      DoublyLinkedList.prototype.update = (position, newData) => {
        //1.越界判断
        if (position < 0 || position >= this.length) {
          return false
        }

        //2.寻找正确的节点
        let current = this.head
        let index = 0
        //this.length / 2 > position:从头开始遍历
        if (this.length / 2 > position) {
          while(index++ < position){
          current = current.next
        }
        //this.length / 2 =< position:从尾开始遍历
        }else{
          current = this.tail
          index = this.length - 1
          while (index -- > position) {
            current = current.prev
          }
        }

        //3.修改找到节点的data
        current.data = newData
        return true//表示成功修改
      }
```

- 过程详解：

以（index++ < position）为条件，通过while循环遍历链表中的节点（停止条件为index = position）。循环结束后，current指向需要修改的节点。

- 测试代码：
```javascript
console.log(list.update(1, 'c'));
console.log(list);
```

- 测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1656914392477-9c82f068-b066-4e32-92ec-172051747aa7.png#clientId=u6430b540-2302-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=312&id=eZkfA&margin=%5Bobject%20Object%5D&name=image.png&originHeight=312&originWidth=483&originalType=binary&ratio=1&rotation=0&showTitle=false&size=26908&status=done&style=none&taskId=u47fe69aa-84ab-4b3e-89f6-c740a8a0d7f&title=&width=483)

7. removeAt(position)

代码实现：

```javascript
DoublyLinkedList.prototype.removeAt = (position) => {
  if(position < 0 || position >= this.length) return false
  let current = this.head
  if(this.length === 1){
    this.head = null
    this.tail = null
  }
  else {
    if(position === 0){
      this.head.next.prev = null
      this.head = this.head.next
    }
    else if(position === this.length - 1) {
      let current = this.tail
      this.tail.prev.next = null
      this.tail = this.tail.prev
    } 
    else {
      let index = 0
      while(index++ < position){
        current = current.next
      }
      current.next.prev = current.prev
      current.prev.next = current.next
    }
  }
  this.length -= 1
  return current.data
}
```


测试代码：
```javascript
console.log('removeAt(2)',list.removeAt(2))
console.log('removeAt(2)',list);
```

测试结果：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657067348904-87f52b69-310c-410f-8850-ef8a0760e4bb.png#clientId=u4eb2bbaf-a62f-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=452&id=j6DX0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=678&originWidth=754&originalType=binary&ratio=1&rotation=0&showTitle=false&size=82718&status=done&style=none&taskId=u3ed4149f-77c6-4fdb-8c5b-b847f4f4017&title=&width=503)

8. 其他方法

其他方法包括：**remove(element) ,isEmpty() ,size() ,getHead() ,getTail() **

代码实现：

```javascript
DoublyLinkedList.prototype.remove = (data) => {
  let index = this.indexOf(data)
  return this.removeAt(index)
}
DoublyLinkedList.prototype.isEmpty = () => {
  return this.length === 0
}
DoublyLinkedList.prototype.size = () => {
  return this.length
}
DoublyLinkedList.prototype.getHead = () => {
  return this.head.data
}
DoublyLinkedList.prototype.getTail = () => {
  return this.tail.data
}
```

测试代码：

```javascript
console.log(list.remove('aaa'))
console.log(list.isEmpty())
console.log(list.size())
console.log(list.getHead())
console.log(list.getTail())
```

测试结果：<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657067484601-7e57c579-13a9-4578-a041-9b01c1333ad1.png#clientId=u4eb2bbaf-a62f-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=612&id=OohHG&margin=%5Bobject%20Object%5D&name=image.png&originHeight=818&originWidth=883&originalType=binary&ratio=1&rotation=0&showTitle=false&size=106479&status=done&style=none&taskId=u2a924939-784f-402d-b4dd-4e78519eb81&title=&width=660.5)

### 2.5.6 完整实现

```javascript
//封装双向链表类
function DoublyLinkedList() {
  //封装内部类，节点类
  function Node(data) {
    this.data = data
    this.prev = null
    this.next = null
  }
  //属性
  this.head = null
  this.tail = null
  this.length = 0
  DoublyLinkedList.prototype.append = data => {
    let newNode = new Node(data)
    if (this.length === 0) {
      this.tail = newNode
      this.head = newNode
    }
    else {
      newNode.prev = this.tail
      this.tail.next = newNode
      this.tail = newNode
    }
    this.length += 1
  }
  //toString
  DoublyLinkedList.prototype.toString = () => {
    return this.backwardString()
  }
  //forwardString
  DoublyLinkedList.prototype.forwardString = () => {
    let current = this.tail
    let resultString = ""
    while (current) {
      resultString += current.data + '--'
      current = current.prev
    }
    return resultString
  }
  //backwordString
  DoublyLinkedList.prototype.backwardString = () => {
    let current = this.head
    let resultString = ""
    while (current) {
      resultString += current.data + "--"
      current = current.next
    }
    return resultString
  }
  DoublyLinkedList.prototype.insert = (pos, data) => {
    if (pos < 0 || pos > this.length) return false
    let newNode = new Node(data)
    if (this.length === 0) {
      this.head = newNode
      this.tail = newNode
    }
    else {
      if (pos == 0) {
        this.head.prev = newNode
        newNode.next = this.head
        this.head = newNode
      }
      else if (pos == this.length) {
        this.tail.next = newNode
        newNode.prev = this.tail
        this.tail = newNode
      }
      else {
        let current = this.head
        let index = 0
        while (index++ < pos) {
          previous = current
          current = current.next
        }
        newNode.next = current
        newNode.prev = current.prev
        previous.next = newNode
        current.prev = newNode
      }
    }
    this.length += 1
    return true
  }
  DoublyLinkedList.prototype.get = pos => {
    if (pos < 0 || pos > this.length) return null
    let current = null
    let index = 0
    if ((this.length / 2) > pos) {
      current = this.head
      while (index++ < pos) { current = current.next }
    }
    else {
      current = this.tail
      index = this.length - 1
      while (index-- > pos) {
        current = current.prev
      }
    }
    return current.data
  }
  DoublyLinkedList.prototype.indexOf = data => {
    //1.定义变量
    let current = this.head
    let index = 0

    //2.遍历链表，查找与data相同的节点
    while (current) {
      if (current.data == data) {
        return index
      }
      current = current.next
      index += 1
    }
    return -1
  }
  DoublyLinkedList.prototype.update = (position, newData) => {
    //1.越界判断
    if (position < 0 || position >= this.length) {
      return false
    }

    //2.寻找正确的节点
    let current = this.head
    let index = 0
    //this.length / 2 > position:从头开始遍历
    if (this.length / 2 > position) {
      while (index++ < position) {
        current = current.next
      }
      //this.length / 2 =< position:从尾开始遍历
    } else {
      current = this.tail
      index = this.length - 1
      while (index-- > position) {
        current = current.prev
      }
    }

    //3.修改找到节点的data
    current.data = newData
    return true//表示成功修改
  }
  DoublyLinkedList.prototype.removeAt = (position) => {
    if (position < 0 || position >= this.length) return false
    let current = this.head
    if (this.length === 1) {
      this.head = null
      this.tail = null
    }
    else {
      if (position === 0) {
        this.head.next.prev = null
        this.head = this.head.next
      }
      else if (position === this.length - 1) {
        let current = this.tail
        this.tail.prev.next = null
        this.tail = this.tail.prev
      }
      else {
        let index = 0
        while (index++ < position) {
          current = current.next
        }
        current.next.prev = current.prev
        current.prev.next = current.next
      }
    }
    this.length -= 1
    return current.data
  }
  DoublyLinkedList.prototype.remove = (data) => {
    let index = this.indexOf(data)
    return this.removeAt(index)
  }
  DoublyLinkedList.prototype.isEmpty = () => {
    return this.length === 0
  }
  DoublyLinkedList.prototype.size = () => {
    return this.length
  }
  DoublyLinkedList.prototype.getHead = () => {
    return this.head.data
  }
  DoublyLinkedList.prototype.getTail = () => {
    return this.tail.data
  }
}
let list = new DoublyLinkedList()
list.append('aaa')
list.append('bbb')
list.append('ccc')
console.log(list)
console.log(list.toString())
console.log(list.backwardString())
console.log(list.forwardString())
list.insert(0, '插入链表的第一个元素')
list.insert(0, '在链表首部插入元素')
list.insert(1, '在链表中间插入元素')
list.insert(6, '在链表尾部插入元素')
console.log(list);
console.log(list.get(0))
console.log(list.get(5))
console.log(list.indexOf('aaa'))
console.log(list.indexOf('ccc'))
console.log(list.update(1, 'c'));
console.log(list);
console.log('removeAt(2)', list.removeAt(2))
console.log('removeAt(2)', list);
console.log('remove(aaa)', list.remove('aaa'))
console.log('remove(aaa)', list);
console.log('isEmpty()', list.isEmpty())
console.log('size()', list.size())
console.log('getHead()', list.getHead())
console.log('getTail()', list.getTail())
```

## 2.6 链表结构总结

 单向链表有head和next两个属性，双向链表有head、tail、next、prev四个属性。处理好它们的指向，相当于将它们正确地连接在一起，这样就组成了一条链，这就是简单链表的实现。   

在实际开发中链表使用得非常多，比如Java中的LinkList就是双向链表。   <br />    
### 2.6.1 注意点

- 在链表中**current = current.next **可以从左往右看，看成是**current --> current.next**，即current指向current的下一个节点。 
- 删除节点的原理：只要没有引用指向该对象，无论该对象是否有引用指向其他对象，该对象都会被回收（删除）。
- 参数中凡是有position的都要进行越界判断。


### 2.6.2 链表的增删改查

 以双向链表为例：链表的增删改查无非就是获取链表中相应的节点改变其中的prev和next两个变量的指向。  

- 情况一：只需要head和tail两个变量就可以获取需要操作的变量（这里指的是能够轻松获取，当然你想通过head.next.next...或tail.prev.prev...来获取想要的节点也可以），在这种情况下链表的长度**length：0 <= length <=2**。   
- 情况二：不能靠tail和head来获取到需要操作的变量时，可采用**while循环遍历**的方式，找到需要操作的节点，在这种情况下，如果我们想要在链表的**position = x**的位置插入新节点，那么可以通过**current.next获取position的后一个节点Node(x+1)**，通过**current.prev获取position位置的前一个节点Node(x)**；之后修改**Node(x+1)和Node(x)中的prev和next**两个变量的指向即可在pos=x 的位置插入新节点。<br /> 

### 2.6.3 修改链表引用指向

 应先修改newNode引用的指向，再修改其他引用

- 情况1：通过head和tail引用就能获取需要操作的节点时，最后更改head或tail变量的指向（因为它们分别指向链表的第一个和最后一个节点，获取其他节点时可能需要用到它们）。
- 情况2：使用current获取到需要操作的节点时，最后更改**curren.next**或**current.prev**的指向。因为**current.next和current.prev表示的是Node(x+2)和Node(x)这两个节点**，一旦变更它们的指向就无法获取Node(x)或Node(x+2)了，<br /> 

### 2.6.4 遍历链表<br /> 
积累两种遍历思路

- 获取指定的**position = x 位置的后一个节点和索引值**：循环结束后**index = position = x**，变量current就指向了**Node(x+1)**，变量index的值为**Node(x+1)**的索引值x。
- 遍历链表中的所有节点：当**current.next = null时停止循环**，此时current指向链表的最后一个节点。<br /> <br /> 
