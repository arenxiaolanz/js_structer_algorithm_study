# 八、排序与搜索

## 8.1 大O表示法

### 大O表示法

- 在计算机中采用**粗略的度量**来描述计算机的效率，这种方法被称为**“大O表示法”**

- 在**数据项个数发生改变**时，算法的**效率也会发生改变**。所以说算法A比算法B快两倍，这样的比较是**没有意义**的

- 因此我们通常使用“**算法的速度随着数据量的变化会如何变化**”的方式来表示算法的效率，大O表示法就是方式之一


### 常见的大O表示形式


![$_DT011`F@PDZ~%E0XHBIMD.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657360362436-7247f66c-1e98-40b5-aba2-2cfc803dbb9b.png#clientId=ud835aa17-bf20-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u2f4f2d6b&margin=%5Bobject%20Object%5D&name=%24_DT011%60F%40PDZ~%25E0XHBIMD.png&originHeight=313&originWidth=727&originalType=binary&ratio=1&rotation=0&showTitle=false&size=72475&status=done&style=none&taskId=uc86dcb48-6f0c-4d63-ae80-9665e29f292&title=)


### 不同大O形式的时间复杂度


![1NW0[$S55W7{A[A_15KJ1{Q.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657360439200-e4db0dce-6128-4fbe-9a91-ae0180902fb8.png#clientId=ud835aa17-bf20-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=ub3239658&margin=%5Bobject%20Object%5D&name=1NW0%5B%24S55W7%7BA%5BA_15KJ1%7BQ.png&originHeight=439&originWidth=543&originalType=binary&ratio=1&rotation=0&showTitle=false&size=42968&status=done&style=none&taskId=u8ec298cd-19fe-43b7-abf9-9cbf6cc0868&title=)

可以看到效率从大到小分别是：`O(1) > O(logn) > O(n) > O(nlogn) > O(n<sup>2</sup>) > O(2<sup>n</sup>)`

### 推导大O表示法的三条规则



- 规则1：用**常量1取代**运行时间中所有的加法常量。如 7+8 = 15，用1表示运算结果15，大O表示法表示为**O(1)**

- 规则2：运算中只保留最高阶项。如**N<sup>3</sup> + 3n + 1 **，大O表示法表示为**O(N<sup>3</sup>)**

- 规则3：若最高阶项的常数不为一，可将其省略。如**4N<sup>2</sup>**，大O表示法表示为**O(N<sup>2</sup>)**


## 8.2 排序算法

这里主要介绍几种简单排序和高级排序：

- 简单排序：**冒泡排序、选择排序、插入排序**

- 高级排序：**希尔排序、快速排序**

此处创建一个列表类ArrayList并添加一些属性和方法，用于存放这些排序方法

```javascript
function ArrayList() {
  this.array = []
  ArrayList.prototype.insert = (item) => {
    this.array.push(item)
  }
  ArrayList.prototype.toString = () => {
    return this.array.join('-')
  }
  ArrayList.prototype.swap = (m, n) => {
    let temp = this.array[m]
    this.array[m] = this.array[n]
    this.array[n] = temp
  }
}
```

### 冒泡排序

冒泡排序的思路：

- 对**未排序的各元素**从头到尾依次比较相邻的两个元素大小关系；

- 如果左边的人员高，则将两人交换位置。比如1比2矮，不交换位置；

- 向右移动一位，继续比较2和3，最后比较 **length - 1 和 length - 2**这两个数据；

- 当到达**最右端时，最高的人一定被放在了最右边**；

- 按照这个思路，**从最左端重新开始时**，只需要走到倒数第二个位置即可；<br /> 

实现思路：

两层循环：

- 外层循环控制冒泡趟数：

   - 第一次：`j = length - 1`，比较到倒数第一个位置

   - 第二次：`j = length - 2`，比较到倒数第二个位置

- 内层循环控制每趟比较的次数：

   - 第一次比较：`i = 0`，比较0和1位置的两个数据

   - 最后一次比较：`i = length - 2`，比较length - 2和length - 1两个数据

![`{C}%TIXQ9Q`EP]JN_GPOPW.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657417519167-a37c722e-0e9d-41b7-8bf3-f9c798c9b699.jpeg#clientId=u13a57502-066a-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u9a77ca6a&margin=%5Bobject%20Object%5D&name=%60%7BC%7D%25TIXQ9Q%60EP%5DJN_GPOPW.jpg&originHeight=571&originWidth=1167&originalType=binary&ratio=1&rotation=0&showTitle=false&size=78525&status=done&style=none&taskId=udfcd78f1-813b-4508-b9b5-609167e35db&title=)

代码实现：

```javascript
ArrayList.prototype.bubblesort = () => {
  let length = this.array.length
  for (let j = length - 1; j >= 0; j--) {
    for (let i = 0; i < j; i++) {
      if (this.array[i] > this.array[i + 1]) {
        this.swap(i, i + 1)
      }
    }
  }
}
```


测试代码：

```javascript
    let array = new ArrayList()
    array.insert(2)
    array.insert(99)
    array.insert(25)
    array.insert(4)
    array.insert(18)
    array.insert(6)
    array.insert(17)    
    array.bubblesort()
    console.log(array)
```


测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657416875588-168de78e-2363-460b-9d50-d22f9870557d.png#clientId=u13a57502-066a-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=72&id=u682f8a48&margin=%5Bobject%20Object%5D&name=image.png&originHeight=90&originWidth=455&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7303&status=done&style=none&taskId=u40cb13b6-9cc1-4520-b6e7-ed3838a2ca1&title=&width=362.5)<br />![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657416896992-52ae46b9-56c3-4dec-b8c2-69b64e566bb3.png#clientId=u13a57502-066a-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=70&id=u48308f52&margin=%5Bobject%20Object%5D&name=image.png&originHeight=83&originWidth=453&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7205&status=done&style=none&taskId=u0f0be3e4-34a6-4acd-99a6-255a34badda&title=&width=379.5)

冒泡排序的效率：

- 上面所讲的对于7个数据项，比较次数为： ` 6 + 5  + 4 + 3 + 2 + 1`

- 对于N个数据项，比较次数为：`(N - 1) + (N - 2) + (N - 3) + ... + 1 = N *_ (N - 1)  / _2`;如果两次比较交换一次，那么交换次数为：` N *(N-1) / 4`

- 使用大O表示法表示比较次数和交换次数分别为：` O（N*(N-1)/2）`和` O(N*(N-1)/4)`，根据大O表示法的三条规则都化简为：` O(N^2)`


### 选择排序

选择排序改进了冒泡排序：

- 将**交换次数**由**O（N^2）**减小到**O(N)**

- 但是**比较次数**依然为**O(N^2)**

选择排序的思路：

- **选定第一个索引的位置比如1，然后依次和后面的元素进行比较**

- 如果后面的元素，**小于索**引1位置的元素，则交换位置**到索引1**处

- 经过1轮的比较之后，可以确定一开始指定的索引**1位置的元素是最小**的

- 随后使用同样的方法除索引1以外，逐个比较剩下的元素即可

- 可以看出选择排序，**第一轮会选出最小值，第二轮会选出第二小的值，直到完成排序**

实现思路：

两侧循环：

- 外层循环指定的索引：

   - 第一次：j=0，指定第一个元素

   - 最后一次：j=length - 1，指定最后一个元素


- 内层循环负责将指定索引（i）的元素与剩下（i-1）的元素进行比较

代码实现：

```javascript
ArrayList.prototype.selectSort = () => {
  let length = this.array.length
  for (let j = 0; j < length - 1; j++) {
    let min = j
    for (let i = min + 1; i < length; i++) {
      if (this.array[min] > this.array[i]) {
        min = i
      }
    }
    this.swap(min, j)
  }
}
```

测试代码：

```javascript
let array = new ArrayList()
array.insert(2)
array.insert(99)
array.insert(25)
array.insert(4)
array.insert(18)
array.insert(6)
array.insert(17)
array.selectSort()
console.log(array)
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657419746753-4bbc61fb-b276-4538-bb87-537e6ccd38af.png#clientId=u4de28c0b-976f-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=85&id=ue05c184f&margin=%5Bobject%20Object%5D&name=image.png&originHeight=88&originWidth=460&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7295&status=done&style=none&taskId=u953e69b2-1eb6-4c1f-8428-73e5c09fb4a&title=&width=444)


选择排序的效率：

- 选择排序的**比较次数**为：**N*(N-1)/2**，用大O表示法表示为：**O(N^2)**

- 选择排序的**交换次数**为：**（N-1）/2**，用大O表示法表示为：**O(N)**

- 所以**选择排序的效率高于冒泡排序**

### 插入排序

插入排序是简单排序中**效率最高**的的一种排序

插入排序的思路：

- 插入排序思想的核心是**局部有序**。如图所示，X左边的人称为**局部有序**
- 首先指定一数据X（从第一个数据开始），并将数据X的左边变成局部有序状态
- 随后将X右移一位，再次达到局部有序之后，继续右移一位，重复前面的操作直至X移至最后一个元素

![`16OVL@S]S)YJBYV)B6CSV6.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657444028900-5c706e0b-d7cb-49a1-a9a7-ac8d67ee119f.jpeg#clientId=u4de28c0b-976f-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u0b1244e4&margin=%5Bobject%20Object%5D&name=%6016OVL%40S%5DS%29YJBYV%29B6CSV6.jpg&originHeight=512&originWidth=383&originalType=binary&ratio=1&rotation=0&showTitle=false&size=29737&status=done&style=none&taskId=ueec29818-4268-4ab3-96c6-dbcac65a6a6&title=)

代码实现：

```javascript
ArrayList.prototype.insertionSort = () => {
  let length = this.array.length
  for (let i = 1; i < length; i++) {
    let temp = this.array[i]
    let j = i
    while(this.array[j-1] > temp && j>0){
      this.array[j] = this.array[j - 1]
      j--
    }
    this.array[j] = temp
  }
}
```

测试代码：

```javascript
let array = new ArrayList()
array.insert(2)
array.insert(99)
array.insert(25)
array.insert(4)
array.insert(18)
array.insert(6)
array.insert(17)
array.insertionSort()
console.log(array)
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657444295992-44428ff0-6c51-4fb7-b634-616173d644b2.png#clientId=u4de28c0b-976f-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=99&id=u09329cdf&margin=%5Bobject%20Object%5D&name=image.png&originHeight=87&originWidth=459&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7298&status=done&style=none&taskId=ud38d896a-987a-47ae-af3e-304730f4b53&title=&width=522.5)

插入排序的效率：

- **比较次数**：第一趟时，需要的最大次数为1，第二次最大为2，以此类推，最后一趟最大为N-1，所以，插入排序的总比较次数为N*(N-1)/2，但是，实际上每趟发现插入点之前，平均只有一半需要比较，所以比较次数为：**N*(N-1)/4**

- **交换次数**：指定第一个数据为X时交换0次，指定第二个数据为X最多需要交换1次，以此类推，指定第N个数据为X时最多需要交换N-1次，所以一共需要交换**N*(N-1)/2次**

- 虽然用大O表示法表示插入排序的效率也是O(N^2)，但是插入排序整体操作次数更少，因此，**在简单排序中，插入效率最高**

### 希尔排序

希尔排序是插入排序的一种高效的改进版，效率比插入排序要高。

希尔排序的历史背景：

- 希尔排序按其设计者希尔（Donald Shell）的名字命名，该算法由1959年公布；

- 希尔算法首次突破了计算机界一直认为的算法的时间复杂度都是**O（N^2）**的大关，为了纪念该算法里程碑式的意义，用Shell来命名该算法； 


插入排序的问题：   

- 假设一个很小的数据项在很靠近右端的位置上，这里本应该是较大的数据项的位置；

- 将这个小数据项移动到左边的正确位置，所有的中间数据项都必须向右移动一位，这样效率非常低；

- 如果通过某种方式，不需要一个个移动所有中间的数据项，就能把较小的数据项移到左边，那么这个算法的执行速度就会有很大的改进。

希尔排序的实现思路：

- 希尔排序主要通过**对数据进行分组实现快速排序**；

- 根据设定的**增量（gap）将数据分为gap个组（组数等于gap），再在每个分组中进行局部排序；**

> 假如有数组有10个数据，第1个数据为黑色，增量为5。那么第二个为黑色的数据index=5，第3个数据为黑色的数据index = 10（不存在）。所以黑色的数据每组只有2个，10 / 2 = 5一共可分5组，即组数等于增量gap。


- 排序之后**，减小增量，继续分组，再次进行局部排序，直到增量gap=1为止。随后只需进行微调就可完成数组的排序**

增量的选择：

- **原稿中**希尔建议的初始间距为**N / 2，比如对于N = 100的数组，增量序列为：50，25，12，6，3，1，**可以发现不能整除时向下取整。

- Hibbard增量序列：增量序列算法为：2^k - 1，即1，3，5，7... ...等；这种情况的最坏复杂度为O（N3/2）**,平均复杂度为**O（N5/4）但未被证明；<br />Sedgewcik增量序列：

以下代码实现中采用希尔排序原稿中建议的增量即N / 2 。<br /> 

代码实现：

```javascript
ArrayList.prototype.shellSort = () => {
  let length = this.array.length
  let gap = Math.floor(length / 2)
  //第一层循环：while循环（使gap不断减小(eg:100的话，则50，25，12，6，3，1)）
  while (gap >= 1) {
    //第二层循环，以gap为增量，进行分组，对分组进行排序
    for (let i = gap; i < length; i++) {
      let temp = this.array[i]
      let j = i
      //第三层循环，寻找正确的插入位置
      while (this.array[j - gap] > temp && j > gap - 1) {
        this.array[j] = this.array[j - gap]
        j -= gap
      }
      this.array[j] = temp
    }
    gap = Math.floor(gap/2)
  }
}
```

测试代码：

```javascript
let array = new ArrayList()
array.insert(2)
array.insert(99)
array.insert(25)
array.insert(4)
array.insert(18)
array.insert(6)
array.insert(17)
array.shellSort()
console.log(array)
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657452163935-7eeb6d10-da75-45d9-972c-cae81742cf04.png#clientId=u4de28c0b-976f-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=40&id=u18ed6b22&margin=%5Bobject%20Object%5D&name=image.png&originHeight=79&originWidth=470&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7127&status=done&style=none&taskId=u567feeac-7ded-4206-8f75-8ff2899f9a9&title=&width=235)

希尔排序的效率：

希尔排序的效率和增量有直接关系，即使使用原稿中的增量效率都高于简单排序

### 快速排序

快速排序的介绍：

- 快速排序可以说是目前所有算法中，**最快的一种算法**，当然，没有任何一种算法是在任意情况下都是最优的，但是，大多数情况下，快速排序是比较好的选择

- 快速排序其实是冒泡排序的升级版

快速排序的核心思想是**分而治之，先选出一个数据（比如65），**将比起**小的数据都放在他的左边，将比他大的数据都放在他的右边**，这个数据称为枢纽

快速排序的枢纽：

- **第一种方案**：直接选择**第一个元素作为枢纽**，但是，当第一个元素就是最小值的情况下，**效率不高**

- 第二种方案：使用**随机数**，随机数本身十分消耗性能，**不推荐**

- 优秀的解决方法：取**index为头，中，尾的三个排序后的中位数**；按下标值取出的三个数据为：92，31，0，经排序后变为：0，31，92，取其中的中位数31作为枢纽（当（length-1）/2不为整时可向上或向下取值）


实现枢纽选择：

```javascript
let swap = function (arr, m, n) {
  let temp = arr[m]
  arr[m] = arr[n]
  arr[n] = temp
}
let median = function (arr) {
  let center = Math.floor(arr.length / 2)
  let right = arr.length - 1
  let left = 0
  if (arr[left] > arr[center]) {
    swap(arr, left, center)
  }
  if (arr[center] > arr[right]) {
    swap(arr, center, right)
  }
  if (arr[left] > arr[right]) {
    swap(arr, left, right)
  }
  return center
}
```

快速排序代码实现：

```javascript
let quickSort = function (arr) {
  if (arr.length == 0) { return [] }
  let center = median(arr)
  let c = arr.splice(center, 1)
  let l = []
  let r = []
  for (let i = 0; i < arr.length; i++) {
    if (arr[i] < c) {
      l.push(arr[i])
    }
    else {
      r.push(arr[i])
    }
  }
  return quickSort(l).concat(c, quickSort(r))
}
```

测试代码：

```javascript
let arr = [5,21,4,18,6,17,99]
let arrNew = quickSort(arr)
console.log(arrNew)
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657503869260-6fc7d0f7-0a30-4e2d-bc8c-8bb5959df7ed.png#clientId=u75e10f19-1a5b-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=60&id=u50586c24&margin=%5Bobject%20Object%5D&name=image.png&originHeight=45&originWidth=370&originalType=binary&ratio=1&rotation=0&showTitle=false&size=2373&status=done&style=none&taskId=u5e759120-5218-480b-b8d7-f3a0f8e8870&title=&width=493)

快速排序的效率：

- **快速排序最坏情况下的效率**：每次选择的枢纽都是最左边或最右边的数据，此时效率等同于冒泡排序，时间复杂度为**O(N^2)**。可根据不同的枢纽选择避免这一情况。

- 快速排序的**平均效率**：为**O(N*logN)**，虽然其他算法效率也可达到O(N*logN)，但是其中**快速排序是最好的**










