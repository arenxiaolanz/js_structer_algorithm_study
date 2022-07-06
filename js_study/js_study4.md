# 四、哈希表

## 4.1 认识哈希表

### 哈希表介绍

哈希表通常是基于**数组**实现的，但是相对于数组，它存在更多**优势：**

- 哈希表可以提供非常快速的**插入-删除-查找操作**
-  无论多少数据，插入和删除值都只需要**非常短的时间**，即**O(1)的时间级**。实际上，只需要**几个机器指令即可**完成
- 哈希表的**速度比树还要快**，基本可以瞬间查找到想要的元素。但是相对于**树来说编码要简单**得多

但是，哈希表同样存在**不足之处：**

-  哈希表中的数据是**没有顺序**的，所以**不能以一种固定的方式（比如从小到大 ）来遍历**其中的元素
- 通常情况下，哈希表中的**key是不允许重复**的，**不能放置相同的key，用于保存不同的元素**。

哈希表**是什么？**

-  哈希表并不好理解，不像**数组、链表和树等可通过图形的形式**表示其结构和原理
- 哈希表的结构就是**数组**，但它神奇之处在于**对下标值的一种变换**，这种变换我们可以称之为**哈希函数**，通过哈希函数可以获取**HashCode**。


### 体会哈希表

-  案例一：公司想要存储1000个人的信息，每一个工号对应一个员工的信息。若使用**数组，增删数据时比较麻烦**；使用**链表，获取数据时比较麻烦**。有没有一种数据结构，能**把某一员工的姓名转换为它对应的工号**，再根据工号查找该员工的完整信息呢？没错此时就可以使用**哈希表的哈希函数**来实现。

- 案例二：存储联系人和对应的电话号码：当要查找张三（比如）的号码时，若**使用数组：由于不知道存储张三数据对象的下标值，所以查找起来十分麻烦**，**使用链表时也同样麻烦**。而**使用哈希表就能通过哈希函数**把**张三这个名称转换为它对应的下标值**，再**通过下标值查找效率就非常高**了。

也就是说：哈希表最后还是**基于数据**来实现的，只不过**哈希表能够通过哈希函数把字符串转化为对应的下标值**，建立**字符串和下标值**的**对应**关系。<br /> 

## 4.2 认识哈希化

### 字母转数字

 为了**把字符串转化为对应的下标值**，需要**有一套编码系统**，为了方便理解我们创建这样一套编码系统：**比如a为1，b为2，c为3**，以此类推**z为26，空格为27**（不考虑大写情况）。

有了编码系统后，**将字母转化为数字**也有很多种方式：

- 方式一：**数字相加 。     **

例如：**cats转化为数字**：3+1+20+19=43，那么就把**43作为cats单词的下标值储存在数组**中；但是这种方式会存在这样的问题：**很多的单词按照该方式转化为数字后都是43**，比如was。**而在数组中一个下标值只能储存一个数据**，所以该方式不合理。    

- 方式二：**幂的连乘。      **

我们平时使用的**大于10的数字**，就是用**幂的连乘来表示它的唯一性**的。比如： **6543=6 * 103 + 5 * 102 + 4 * 10 + 3**；这样单词也可以用该种方式来表示：**cats = 3 * 273 + 1 * 272 + 20 * 27 + 17 =60337;       **<br />虽然该方式可以保证字符的唯一性，但是如果是**较长的字符**（如aaaaaaaaaa）所**表示的数字就非常大**，此时要求很大容量的数组，然而其中却有许多**下标值指向的是无效的数据**（比如不存在zxcvvv这样的单词），造成了**数组空间的浪费**。

两种方案总结：   

第一种方案（让数字**相加求和**）产生的**数组下标太少**；    <br />第二种方案（与27的**幂相乘求和**）产生的**数组下标又太多**；    

现在需要一种**压缩方法**，把幂的连乘方案系统中得到的**巨大整数**范围压缩到可**接受的数组**范围中。可以通过**取余**操作来实现。虽然取余操作得到的结构**也有可能重复**，但是可以通过**其他方式解决**。

### 哈希表的一些概念

-  **哈希化**：将**大数字**转化成**数组范围内下标**的过程，称之为**哈希化**

<br />

- **哈希函数**：我们通常会将单词转化成大数字，把**大数字进行哈希化**的代码实现放在一个**函数**中，该函数就称为**哈希函数**

<br />

- **哈希表**：对**最终数据插入的数组**进行整个结构的**封装**，得到的就是**哈希表**


## 4.3 冲突及冲突的解决

### 什么是冲突？

 哈希化过后的下标依然可能重复，如何解决这个问题呢？这种情况称为冲突，冲突是不可避免的，我们只能解决冲突。<br /> 
### 解决冲突的方法

 如何解决这种冲突呢? 常见的情况有两种方案.

- 链地址法

- 开放地址法<br /> 
### 链地址法

 如下图所示，我们将**每一个数字都对10进行取余操作**，则余数的范围**0~9作为数组的下标值**。

并且，数组每一个下标值对应的位置存储的**不再是一个数字**了，而是存储由经过取余操作后得到**相同余数的数字组成的数组或链表**。  <br />   <br />![YB6HR`)5TTID$0_EEU3Z1C2.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657097347161-84615933-81b9-4263-9671-03dcb0b4297e.jpeg#clientId=u55012966-7d50-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u13917ee2&margin=%5Bobject%20Object%5D&name=YB6HR%60%295TTID%240_EEU3Z1C2.jpg&originHeight=676&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=118394&status=done&style=none&taskId=ubc17cea6-e751-419b-83e5-fc87cb96372&title=)

这样可以根据**下标值获取到整个数组或链表**，之后**继续在数组或链表中查找**就可以了。    

而且，**产生冲突的元素一般不会太多**。

**总结**：**链地址法**解决冲突的办法是**每个数组单元中存储的不再是单个数据**，而是**一条链条**，这条链条常使用的数据结构为**数组或链表**，两种数据结构查找的**效率相当**（因为链条的元素一般不会太多）。<br /> 

### 开放地址法

开放地址法的主要工作方式是**寻找空白的单元格**来放置冲突的**数据项**。    

![J`[{3BQD7(]H2U%]477FV`7.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657105987662-00cde3ca-f219-48cf-9a1a-f4afc59b1479.jpeg#clientId=u55012966-7d50-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u46c4ea68&margin=%5Bobject%20Object%5D&name=J%60%5B%7B3BQD7%28%5DH2U%25%5D477FV%607.jpg&originHeight=674&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=136596&status=done&style=none&taskId=u0a2d715e-f40d-404d-8ce9-0f322d8d685&title=)

根据**探测空白单元格位置方式的不同**，可分为三种方法：

- **线性探测**

<br />

- **二次探测**

<br />

- **再哈希法**


## 4.4 寻找空白位置的方式（开放地址法）

### 线性探测

- 线性探测非常好理解：**线性的查找空白的单元**

- **插入32**时：
   - 经过哈希化得到的`**index=2**`，但是在插入的时候，发现该位置已经有了82

   - 而线性探测就是从`**index位置+1**`**处**，开始一点点的**查找合适的位置（即空位置**，如下图中**index=3**的位置）来放置32

- **查询32**时： 
   - 首先经过哈希化得到`index=2`, 比较，**2的位置结果和查询的数值是否相同**, 相同那么就**直接返回**<br /> 
   -  不相同时，则线性查找，从`index+1`位置开始一个一个位置地查找数据**32**

   -  查询过程中**不会遍历整个哈希表**，只要查询到**空位置**，就**停止**，因为插入**32**时**不会跳过空位置**去插入其他位置<br /> 
- **删除32**时：
   -  删除操作和上述两种情况类似，但需要注意的是，**删除一个数据项**时，不能将该位置下**标的内容设置为null**，否则会**影响到之后其他的查询操**作，因为一**遇到为null的位置就会停止**查找

   - 通常删除一个位置的数据项时，我们可以将它进行**特殊处理（比如设置为-1）**，这样在**查找时遇到-1就知道要继续查找**。<br /> 

![J`[{3BQD7(]H2U%]477FV`7.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657106773221-bc26422b-4932-41d2-87dd-58cbc1e8edc6.jpeg#clientId=u55012966-7d50-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=udb39077e&margin=%5Bobject%20Object%5D&name=J%60%5B%7B3BQD7%28%5DH2U%25%5D477FV%607.jpg&originHeight=674&originWidth=1200&originalType=binary&ratio=1&rotation=0&showTitle=false&size=136596&status=done&style=none&taskId=u6783f499-32a6-4632-96f5-ed5e206d78e&title=)

- 线性探测存在的问题：
   -  线性探测存在一个比较严重的问题，就是聚集

   - 如哈希表中还**没插入任何元素**时，插入**23、24、25、26、27**，这就意味着下标值为**3、4、5、6、7**的位置都放置了数据，这种**一连串填充单元就称为聚集**

   - 聚集会**影响哈希表的性能**，无论是**插入/查询/删除**都会影响；

   - 比如插入32时就会发现，连续的单元3~7都**不允许插入数据**，并且在插入的过程中需要经历多次这种情况。**二次探测法可以解决该问题**<br /> 

### 二次探测

我们刚才谈到，**线性探测存在的问题**：就是如果之前的**数据是连续插入**的,，那么**新插入**的一个数据可能需要**探测很长的距离      **

- 二次探测在**线性探测**的基础上进行了**优化     **

- 二次探测主要**优化的是探测时的步长**      
   - 线性探测, 我们可以看成是步长为1的探测, 比如从下标值x开始, 那么线性测试就是x+1, x+2, x+3依次探测    

   - 二次探测, 对**步长做了优化**, 比如从下标值**x**开始, `**x+1², x+2², x+3²**`

   - 这样就可以**一次性探测比较长的距离**，以**避免那些聚集带来的影响**

- 二次探测的问题：  

但是二次探测**依然存在问题**, 比如我们连续插入的是**32-112-82-2-192**, 那么它们依次**累加的时候步长是相同的** <br />  <br />也就是这种情况下会**造成步长不一的一种聚集**. 还是会影响效率.

### 再哈希法

 为了消除**线性探测**和二次探测中无论**步长+1，**还是**步长+平方**中存在的问题, 还有一种最常用的解决方案: **再哈希法      **

- **再哈希法**:

   - **二次探测**的算法产生的**探测序列步长是固定的**:** 1, 4, 9, 16**, 依次类推.

   - 现在需要一种方法: 产生一种**依赖关键字的探测序列**, 而不是每个关键字都一样.

   - 那么, **不同的关键字即使映射到相同的数组下标**, 也可以使用**不同的探测序列**.

   - 再哈希法的做法就是: 把**关键字用另外一个哈希函数**, **再做一次哈希化**, 用这次**哈希化的结果作为步长**.

   - 对于**指定的关键字**, 步长在整个探测中是不变的, 不过不同的关键字使用不同的步长.

- **第二次哈希化**需要具备如下特点:

   - 和**第一个哈希函数不同**. (不要再使用上一次的哈希函数了, 不然结果还是原来的位置)

   - 不能**输出为0**(否则, 将没有步长. 每次探测都是原地踏步, 算法就进入了**死循环**)

- 其实, 我们不用费脑细胞来设计了, 计算机专家已经设计出一种工作很好的**哈希函数**:

   - `stepSize = constant - (key - constant)`

   - 其中`constant`是**质数**, 且小于数组的容量.

   - 例如: `stepSize = 5 - (key % 5)`, 满足需求, 并且结果不可能为0.  

### 哈希化的效率

- 哈希表中执行**插入和搜索操作效率是非常高**的。

   - 如果**没有发生冲突**，那么**效率就会更高**；

   - 如果**发生冲突**，存取时间就依赖**后来的探测长度**；

   - 平均探测长度以及平均存取时间，取决于**装填因子**，随着**装填因子**变**大**，探测**长度会越来越长**。

- 理解概念**装填因子**：

   - **装填因子**表示当前哈希表中已经包含的**数据项**和整个**哈希表长度**的**比值**；

   - `装填因子 = 总数据项 / 哈希表长度`；

   - **开放地址法**的装填因子**最大为1**，因为只有**空白**的单元才能放入元素；

   - **链地址法**的装填因子**可以大于1**，因为只要愿意，拉链法可以**无限延伸**下去；<br /> 

## 4.5 不同探测方式性能的比较

### 线性探测：
<br />可以看到，随着装填因子的增大，平均**探测长度**呈**指数形式增长**，**性能较差**。实际情况中，最好的装填因子取决于存储效率和速度之间的平衡，随着装填因子变小，存储效率下降，而速度上升。   

![LZ3Z]KT@(3]KL3[~4MU(TWD.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657110408161-04d3a18f-5033-439d-a58d-4e687b50d3d6.jpeg#clientId=u55012966-7d50-4&crop=0&crop=0&crop=1&crop=1&from=drop&height=527&id=u27ddcb69&margin=%5Bobject%20Object%5D&name=LZ3Z%5DKT%40%283%5DKL3%5B~4MU%28TWD.jpg&originHeight=447&originWidth=301&originalType=binary&ratio=1&rotation=0&showTitle=false&size=47497&status=done&style=none&taskId=ubf9a1ff6-5bda-47c8-adb5-e40d03514d6&title=&width=355)

### 二次探测和再哈希化的性能：
<br />二次探测和再哈希法性能相当，它们的性能比线性探测略好。由下图可知，随着装填因子的变大，平均探测长度呈指数形式增长，需要探测的次数也呈指数形式增长，性能不高。   

![)$LOM(S3}M]@A)L{GE`W)E0.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657110472073-43b83312-985a-4686-bd35-c48373e13712.jpeg#clientId=u55012966-7d50-4&crop=0&crop=0&crop=1&crop=1&from=drop&height=531&id=u4662d0ec&margin=%5Bobject%20Object%5D&name=%29%24LOM%28S3%7DM%5D%40A%29L%7BGE%60W%29E0.jpg&originHeight=448&originWidth=319&originalType=binary&ratio=1&rotation=0&showTitle=false&size=47854&status=done&style=none&taskId=u556ae406-6005-4c17-86b0-b161b47f0f5&title=&width=378)

### 链地址法的性能：
<br />可以看到随着装填因子的增加，平均探测长度呈线性增长，较为平缓。在开发中使用链地址法较多，比如Java中的HashMap中使用的就是链地址法。   <br /> <br />![$8ESA$4T1)I[CZI7XQF@){S.jpg](https://cdn.nlark.com/yuque/0/2022/jpeg/25602002/1657110519339-efc85e3c-1449-4dc6-904d-6867ed4e782a.jpeg#clientId=u55012966-7d50-4&crop=0&crop=0&crop=1&crop=1&from=drop&height=375&id=u7ffb6f85&margin=%5Bobject%20Object%5D&name=%248ESA%244T1%29I%5BCZI7XQF%40%29%7BS.jpg&originHeight=328&originWidth=423&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36949&status=done&style=none&taskId=ua5544ae8-8ee8-484b-8006-ad0aaa87248&title=&width=483)

## 4.6 优秀的哈希函数

- 好的哈希函数应该尽可能让计算的过程变得**简单，提高计算的效率**.

   - 哈希表的主要优点是它的**速度**，所以在速度上不能满足，那么就达不到设计的目的了.

   - 提高速度的一个办法就是让哈希函数中**尽量少的有乘法和除法**.因为它们的**性能是比较低**的.

- 设计好的哈希函数应该具备哪些优点呢?

   - **快速的计算**

      - 哈希表的优势就在于**效率,所以快速获取到对应的hashCode**非常重要.
      - 我们需要通过**快速的计算来获取到元素对应的hashCode**

   - **均匀的分布**

      - 哈希表中，无论是链地址法还是开放地址法，当**多个元素映射到同一个位置的时候，都会影响效率.**
      - 所以，优秀的哈希函数应该尽可能**将元素映射到不同的位置,让元素在哈希表中均匀的分布.**


## 4.7 初步封装哈希表

### 哈希表常见的操作

- `put（key，value）`：插入或修改操作；

- `get（key）`：获取哈希表中特定位置的元素；

- `remove（key）`：删除哈希表中特定位置的元素；

- `isEmpty（）`：如果哈希表中不包含任何元素，返回trun，如果哈希表长度大于0则返回false；

- `size（）`：返回哈希表包含的元素个数；

- `resize（value）`：对哈希表进行扩容操作；<br /> 
### 哈希函数的简单实现

 首先使用**霍纳法则计算hashCode**的值，通过**取余操作实现哈希化**，此处先简单地指定数组的大小。    <br /> <br />代码实现：

```javascript
//设计哈希函数
//1.将字符串转成比较大的数字：hashCode
//2.将大的数字hashCode压缩到数组范围之内
function hashFunc(str, size) {
  //定义hashCode变量
  let hashCode = 0
  //霍纳法则，计算hashCode的值
  //cats -> unicode变量
  for (let i = 0; i < str.length; i++) {
    //str.charCodeAt(1),获取某个字符对应的unicode编码
    hashCode = 37 * hashCode + str.charCodeAt(i)
  }
  //取余操作
  let index = hashCode % size
  return index
}
```

测试代码：

```javascript
//测试哈希函数
console.log(hashFunc('123', 7));
console.log(hashFunc('NBA', 7));
console.log(hashFunc('CBA', 7));
console.log(hashFunc('CMF', 7));
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657113879563-e1a7b759-fa5d-4ee1-8b7a-d82117eced67.png#clientId=u55012966-7d50-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=360&id=u8ebb2871&margin=%5Bobject%20Object%5D&name=image.png&originHeight=139&originWidth=98&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1025&status=done&style=none&taskId=u1c03eaeb-3ff4-4f05-a897-a82536e6a98&title=&width=254)

### 创建哈希表

![PL@[D5XZ)ZW3RJDPHHEDAZU.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657114091119-55c5feae-3e89-4f50-8ae5-af01e155e35b.png#clientId=u55012966-7d50-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u266cdb67&margin=%5Bobject%20Object%5D&name=PL%40%5BD5XZ%29ZW3RJDPHHEDAZU.png&originHeight=331&originWidth=642&originalType=binary&ratio=1&rotation=0&showTitle=false&size=25023&status=done&style=none&taskId=u63bfd53c-e417-4a89-8152-d8b68d46b8a&title=)

 首先创建哈希表类HashTable，并添加必要的属性和上面实现的哈希函数，再进行其他方法的实现。     <br /> <br />代码实现：

```javascript
function HashTable() {
  //属性
  this.storage = []
  this.count = 0//计算已经存储的元素个数
  //装填因子：loadFactor > 0.75时需要扩容 ，loadFactor < 0.25 时需要减少容量
  this.limit = 7//初始长度

  HashTable.prototype.hashFunc = (str, size) => {
    //定义hashCode变量
    let hashCode = 0
    //霍纳法则，计算hashCode的值
    //cats -> unicode变量
    for (let i = 0; i < str.length; i++) {
      //str.charCodeAt(1),获取某个字符对应的unicode编码
      hashCode = 37 * hashCode + str.charCodeAt(i)
    }

  }
  //取余操作
  let index = hashCode % size
  return index
}
```

- **storage**作为我们的**数组**, 数组中存放相关的元素.

- **count**表示当前已经**存在了多少数据**.

- **limit**用于标记数组中**一共可以存放多少个元素**.

- 另外, 我们直接将哈希函数定义在了**HashTable**中.  


### put(key,value)

 哈希表的**插入和修改**操作是**同一个函数**：因为，当使用者传入一个<key，value>时。     <br />如果原来**不存在该key**，那么就是**插入**操作，如果原来已经**存在该key**，那么就是**修改**操作。     

实现思路：

- 首先，根据**key获取索引值index**，目的为将数据插入到**storage**的对应位置；

- 然后，根据索引值取出**bucket**，如果bucket不存在，先**创建bucket**，随后放置在该索引值的位置；

- 接着，**判断新增还是修改原来的值**。如果**已经有值了，就修改该值；如果没有，就执行后续操作**。

- 最后，进行**新增数据操作**。

代码实现：

```javascript
function HashTable() {
  //属性
  this.storage = []//数组, 数组中存放相关的元素.
  this.count = 0//计算已经存储的元素个数
  //装填因子：loadFactor > 0.75时需要扩容 ，loadFactor < 0.25 时需要减少容量
  this.limit = 7//初始长度

  HashTable.prototype.hashFunc = (str, size) => {
    //定义hashCode变量
    let hashCode = 0
    //霍纳法则，计算hashCode的值
    //cats -> unicode变量
    for (let i = 0; i < str.length; i++) {
      //str.charCodeAt(1),获取某个字符对应的unicode编码
      hashCode = 37 * hashCode + str.charCodeAt(i)
    }
    //取余操作
    let index = hashCode % size
    return index
  }

  HashTable.prototype.put = (key, value) => {
    let index = this.hashFunc(key, this.limit)
    let bucket = this.storage[index]
    if (bucket == null) {
      bucket = []
      this.storage[index] = bucket
    }
    for (let i = 0; i < bucket.length; i++) {
      let tuple = bucket[i]
      if (tuple[0] === key) {//修改
        tuple[1] = value
        return
      }
    }
    bucket.push([key, value])//添加
    this.count += 1
  }

}
```

测试代码：

```javascript
//测试哈希表
//1.创建哈希表
let ht = new HashTable()

//2.插入数据
ht.put('class1', 'Tom')
ht.put('class2', 'Mary')
ht.put('class3', 'Gogo')
ht.put('class4', 'Tony')
ht.put('class4', 'Vibi')
console.log(ht);
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657120954472-0ddaf877-0ea6-4786-8a50-ff15edf3c1d0.png#clientId=u55012966-7d50-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=459&id=u184d0ccc&margin=%5Bobject%20Object%5D&name=image.png&originHeight=586&originWidth=616&originalType=binary&ratio=1&rotation=0&showTitle=false&size=43223&status=done&style=none&taskId=u81dcd44c-7b27-4aa2-9a62-98d0beea3e2&title=&width=483)

### get(key)

实现思路：

-  首先，根据key通过**哈希函数**获取它在**storage中对应的索引值index**；

- 然后，根据**索引值**获取对应的**bucket**；

- 接着，判断获取到的bucket是否为null，如果**为null，直接返回null**；

- 随后，线性**遍历bucket中每一个key**是否等于**传入的key**。如果等于，直接**返回对应的value**；

- 最后，遍历完bucket后，仍然没有找到对应的key，直接**return null**即可。

代码实现：

```javascript
HashTable.prototype.get = key => {
  let index = this.hashFunc(key,this.limit)
  let bucket = this.storage[index]
  if(bucket == null) return null
  else{
    for (let i = 0; i < bucket.length; i++) {
      let tuple = bucket[i]
      if(tuple[0] == key){
        return tuple[1]
      }
      return null
    }
  }
}
```

测试代码：

```javascript
console.log('get',ht.get('class2'))
console.log('get',ht.get('class4'))
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657121401945-c2456018-dbbc-4a25-9319-3595db5e8842.png#clientId=u55012966-7d50-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=373&id=u13aecc18&margin=%5Bobject%20Object%5D&name=image.png&originHeight=499&originWidth=648&originalType=binary&ratio=1&rotation=0&showTitle=false&size=48621&status=done&style=none&taskId=u06080713-1faf-444c-b732-423fedcff96&title=&width=485)

### remove(key)

实现思路：

-  首先，根据**key**通过**哈希函数**获取它在storage中对应的索引值**index**；

- 然后，根据**索引值**获取对应的**bucket**；

- 接着，判断获取到的**bucket**是否为**null**，如果为**null**，直接**返回null**；

- 随后，**线性查找bucket**，寻找对应的**数据**，并且**删除**；

- 最后，依然**没有**找到，**返回null**；<br /> 

代码实现：

```javascript
HashTable.prototype.remove = key => {
  let index = this.hashFunc(key, this.limit)
  let bucket = this.storage[index]
  if (bucket == null) return null
  for (let i = 0; i < bucket.length; i++) {
    let tuple = bucket[i]
    if (tuple[i] == key) {
      bucket.splice(i, 1)
      this.count -= 1
      return tuple[1]
    }
  }
  return null
}
```

测试代码：

```javascript
console.log('remove', ht.remove('class2'))
console.log('remove', ht.remove('class4'))
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657122072121-da6fa800-d39f-45e0-aba9-85078a7ab406.png#clientId=u55012966-7d50-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=340&id=ue03a862e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=426&originWidth=689&originalType=binary&ratio=1&rotation=0&showTitle=false&size=36918&status=done&style=none&taskId=u41af5bab-5e5d-4296-acb7-30ab0654057&title=&width=549.5)

### isEmpty() 与 size()

代码实现：

```javascript
HashTable.prototype.isEmpty = function () {
  return this.count == 0
}
HashTable.prototype.size = function () {
  return this.count
}
```

测试代码：

```javascript
console.log(ht.isEmpty());
console.log(ht.size());
```

测试结果：

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657122241654-119cfef1-c5ff-4bd0-aaec-fbda03cd5b08.png#clientId=u55012966-7d50-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=96&id=u7671b950&margin=%5Bobject%20Object%5D&name=image.png&originHeight=60&originWidth=139&originalType=binary&ratio=1&rotation=0&showTitle=false&size=838&status=done&style=none&taskId=u4ba22e6f-8dc9-42b5-9457-21352037855&title=&width=222.5)

## 4.8 哈希表的扩容

### 扩容与压缩

- 为什么需要扩容？

   -  前面我们在哈希表中使用的是长度为7的数组，由于使用的是**链地址法**，**装填因子(loadFactor)可以大于1**，所以这个哈希表可以**无限制地插入新数据**。

   - 但是，随着数据量的增多，**storage**中每一个**index**对应的**bucket**数组（链表）就会**越来越长**，这就会造成哈希表**效率的降低**<br /> 
- 什么情况下需要扩容？

   -  常见的情况是l**oadFactor > 0.75**的时候进行**扩容**；<br /> 
- 如何进行扩容？

   -  简单的扩容可以**直接扩大两倍**（关于质数，之后讨论）；

   - 扩容之后**所有**的**数据项**都要进行**同步修改**；<br /> 
- 实现思路

   -  首先，定义一个变量，比如**oldStorage**指向原来的**storage**；

   - 然后，**创建一个新的容量更大的数组**，让**this.storage**指向它；

   - 最后，将**oldStorage**中的每一个**bucket**中的每一个数据取出来依次**添加**到**this.storage指向的新数组**中；<br /> 
- 代码实现

```javascript
HashTable.prototype.resize = newLimit => {
  let oldStorage = this.storage
  //重置所有的属性
  this.storage = []
  this.count = 0
  this.limit = newLimit
  for (let i = 0; i < oldStorage.length; i++) {
    const bucket = oldStorage[i]
    if (bucket == null) continue
    for (let j = 0; j < bucket.length; j++) {
      const tuple = bucket[j]
      this.put(tuple[0], tuple[1])
    }
  }
}
```

上述定义的哈希表的**resize**方法，既可以实现哈希表的**扩容**，也可以实现哈希表容量的**压缩**。

> **装填因子 = 哈希表中数据 / 哈希表长度**，即 **loadFactor = count / HashTable.length。**


- 通常情况下当装填因子`laodFactor > 0.75`时，对哈希表进行**扩容**。在哈希表中的添加方法（**push**方法）中添加如下代码，判断是否需要调用扩容函数进行扩容：

```javascript
//判断是否需要扩容操作
if(this.count > this.limit * 0.75){
this.resize(this.limit * 2)
}
```

- 当装填因子`laodFactor < 0.25`时，对哈希表容量进行**压缩**。在哈希表中的删除方法（**remove**方法）中添加如下代码，判断是否需要调用扩容函数进行压缩：

```javascript
//缩小容量
if (this.limit > 7 && this.count < this.limit * 0.25) {
this.resize(Math.floor(this.limit / 2))
}
```

### 选择质数作为容量

#### 质数的判断   

-  方法一：针对质数的特点：只能被1和num整除，不能被2 ~ (num-1)整除。遍历2 ~ (num-1) 。

```javascript
function isPrime(num){
  if(num <= 1 ){
    return false
  } 
  for(let i = 2; i <= num - 1; i++){
    if(num % i ==0){
      return false
    }
  }
  return true
}
```

-  方法二：只需要遍历2 ~ num的平方根即可。<br /> 
```javascript
function isPrime(num){
  if (num <= 1) {
    return false
  }
  //1.获取num的平方根:Math.sqrt(num)
  //2.循环判断
  for(var i = 2; i<= Math.sqrt(num); i++ ){
    if(num % i == 0){
      return false;
    }
  }
  return true;
}
```

####  实现扩容后的哈希表容量为质数  

- 实现思路：

   - 2倍扩容之后，通过循环调用**isPrime**判断得到的容量是否为**质数**，不是则+1，直到是为止。比如原长度：7，2倍扩容后长度为14，14不是质数，14 + 1 = 15不是质数，15 + 1 = 16不是质数，16 + 1 = 17是质数，停止循环，由此得到**质数17**。    

- 代码实现：

   - 第一步：首先需要为**HashTable**类添加判断质数的**isPrime**方法和获取质数的**getPrime**方法：  

```javascript
//判断传入的num是否质数
HashTable.prototype.isPrime = function(num){
  if (num <= 1) {
    return false
  }
  //1.获取num的平方根:Math.sqrt(num)
  //2.循环判断
  for(var i = 2; i<= Math.sqrt(num); i++ ){
    if(num % i == 0){
      return false;
    }
  }
  return true;
}

//获取质数的方法
HashTable.prototype.getPrime = function(num){
  //7*2=14,+1=15,+1=16,+1=17(质数)
  while (!this.isPrime(num)) {
    num++
  }
  return num
}
```

   -  第二步：修改添加元素的**put**方法和删除元素的**remove**方法中关于数组扩容的相关操作

      -   在**put**方法中添加如下代码：<br /> 
```javascript
//判断是否需要扩容操作
if(this.count > this.limit * 0.75){
  let newSize = this.limit * 2
  let newPrime = this.getPrime(newSize)
  this.resize(newPrime)
}
```

      -  在**remove**方法中添加如下代码：

```javascript
//缩小容量
if (this.limit > 7 && this.count < this.limit * 0.25) {
  let newSize = Math.floor(this.limit / 2)
  let newPrime = this.getPrime(newSize)
  this.resize(newPrime)
}
```

- 测试代码

```javascript
let ht = new HashTable()

ht.put('class1','Tom')
ht.put('class2','Mary')
ht.put('class3','Gogo')
ht.put('class4','Tony')
ht.put('class5','5')
ht.put('class6','6')
ht.put('class7','7')
ht.put('class8','8')
ht.put('class9','9')
ht.put('class10','10')
console.log(ht.size());//10
console.log(ht.limit);//17

```

- 测试结果

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657124388825-e827bea5-79b0-41f7-a410-7e6feb376112.png#clientId=u55012966-7d50-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=278&id=ub8a1003e&margin=%5Bobject%20Object%5D&name=image.png&originHeight=91&originWidth=125&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1479&status=done&style=none&taskId=u133a0cc8-cd3a-41a1-98c7-9f4b6222a3a&title=&width=381.5)


## 4.9 哈希表的完整实现

```javascript
function HashTable() {
  //属性
  this.storage = []//数组, 数组中存放相关的元素.
  this.count = 0//计算已经存储的元素个数
  //装填因子：loadFactor > 0.75时需要扩容 ，loadFactor < 0.25 时需要减少容量
  this.limit = 7//初始长度

  HashTable.prototype.hashFunc = (str, size) => {
    //定义hashCode变量
    let hashCode = 0
    //霍纳法则，计算hashCode的值
    //cats -> unicode变量
    for (let i = 0; i < str.length; i++) {
      //str.charCodeAt(1),获取某个字符对应的unicode编码
      hashCode = 37 * hashCode + str.charCodeAt(i)
    }
    //取余操作
    let index = hashCode % size
    return index
  }

  HashTable.prototype.put = (key, value) => {
    let index = this.hashFunc(key, this.limit)
    let bucket = this.storage[index]
    if (bucket == null) {
      bucket = []
      this.storage[index] = bucket
    }
    for (let i = 0; i < bucket.length; i++) {
      let tuple = bucket[i]
      if (tuple[0] === key) {//修改
        tuple[1] = value
        return
      }
    }
    bucket.push([key, value])//添加
    this.count += 1
    //判断是否需要扩容操作
    if (this.count > this.limit * 0.75) {
      let newSize = this.limit * 2
      let newPrime = this.getPrime(newSize)
      this.resize(newPrime)
    }
  }
  HashTable.prototype.get = key => {
    let index = this.hashFunc(key, this.limit)
    let bucket = this.storage[index]
    if (bucket == null) return null
    else {
      for (let i = 0; i < bucket.length; i++) {
        let tuple = bucket[i]
        if (tuple[0] == key) {
          return tuple[1]
        }
        return null
      }
    }
  }
  HashTable.prototype.remove = key => {
    let index = this.hashFunc(key, this.limit)
    let bucket = this.storage[index]
    if (bucket == null) return null
    for (let i = 0; i < bucket.length; i++) {
      let tuple = bucket[i]
      if (tuple[i] == key) {
        bucket.splice(i, 1)
        this.count -= 1
        return tuple[1]
      }
    }
    //缩小容量
    if (this.limit > 7 && this.count < this.limit * 0.25) {
      let newSize = Math.floor(this.limit / 2)
      let newPrime = this.getPrime(newSize)
      this.resize(newPrime)
    }
    return null
  }
  //判断哈希表是否为null
  HashTable.prototype.isEmpty = function () {
    return this.count == 0
  }

  //获取哈希表中元素的个数
  HashTable.prototype.size = function () {
    return this.count
  }
  HashTable.prototype.resize = newLimit => {
    let oldStorage = this.storage
    //重置所有的属性
    this.storage = []
    this.count = 0
    this.limit = newLimit
    for (let i = 0; i < oldStorage.length; i++) {
      const bucket = oldStorage[i]
      if (bucket == null) continue
      for (let j = 0; j < bucket.length; j++) {
        const tuple = bucket[j]
        this.put(tuple[0], tuple[1])
      }
    }
  }
  //判断传入的num是否质数
  HashTable.prototype.isPrime = function (num) {
    if (num <= 1) {
      return false
    }
    //1.获取num的平方根:Math.sqrt(num)
    //2.循环判断
    for (var i = 2; i <= Math.sqrt(num); i++) {
      if (num % i == 0) {
        return false;
      }
    }
    return true;
  }

  //获取质数的方法
  HashTable.prototype.getPrime = function (num) {
    //7*2=14,+1=15,+1=16,+1=17(质数)
    while (!this.isPrime(num)) {
      num++
    }
    return num
  }

}
//测试哈希表
//1.创建哈希表
let ht = new HashTable()

//2.插入数据
/*     ht.put('class1', 'Tom')
        ht.put('class2', 'Mary')
        ht.put('class3', 'Gogo')
        ht.put('class4', 'Tony')
        ht.put('class4', 'Vibi')
        console.log(ht);
        console.log('get', ht.get('class2'))
        console.log('get', ht.get('class4'))
        console.log('remove', ht.remove('class2'))
        console.log('remove', ht.remove('class4'))
        console.log(ht.isEmpty());
        console.log(ht.size());
        let ht = new HashTable() */

ht.put('class1', 'Tom')
ht.put('class2', 'Mary')
ht.put('class3', 'Gogo')
ht.put('class4', 'Tony')
ht.put('class5', '5')
ht.put('class6', '6')
ht.put('class7', '7')
ht.put('class8', '8')
ht.put('class9', '9')
ht.put('class10', '10')
console.log(ht.size());//10
console.log(ht.limit);//17

```



