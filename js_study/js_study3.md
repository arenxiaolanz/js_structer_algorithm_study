# 三、集合与字典

## 3.1 集合结构

### 3.1.1 集合简介

 集合比较常见的实现方式是**哈希表**，这里使用JavaScript的**Object类**进行封装。   <br />集合通常是由一组**无序的、不能重复**的元素构成。   <br />数学中常指的集合中的元素是可以重复的，但是**计算机中集合的元素不能重复**。   

#### 集合是特殊的数组

-  特殊之处在于里面的元素**没有顺序，也不能重复**。 
- 没有顺序意味着**不能通过下标值进行访问**，不能重复意味着**相同的对象在集合中只会存在一份**。

#### 实现集合类

-  在ES6中的**Set类**就是一个集合类，这里我们重新封装一个Set类，了解集合的底层实现。  
- JavaScript中的**Object类中的key**就是一个集合，可以使用它来**封装集合类Set**。  <br /> 

#### 集合常见的操作

-  `add（value）`：向集合添加一个新的项；
- `remove（value）`：从集合中移除一个值；
- `has（value）`：如果值在集合中，返回true，否则返回false；
- `clear（）`：移除集合中的所有项；
- `size（）`：返回集合所包含元素的数量，与数组的length属性相似；
- `values（）`：返回一个包含集合中所有值的数组；

### 3.1.2 代码实现

#### 代码实现

```javascript
function Set() {
  //属性
  this.items = {}
  //has（value）：如果值在集合中，返回true，否则返回false；
  Set.prototype.has = (value) => {
    return this.items.hasOwnProperty(value)
  }
  //add（value）：向集合添加一个新的项；
  Set.prototype.add = (value) => {
    if (this.has(value)) return false
    this.items[value] = value
    return true
  }
  //remove（value）：从集合中移除一个值；
  Set.prototype.remove = (value) => {
    if (!this.has(value)) return false
    delete this.items[value]
    return true
  }
  //clear（）：移除集合中的所有项；
  Set.prototype.clear = () => {
    this.items = {}
  }
  //size（）：返回集合所包含元素的数量，与数组的length属性相似；
  Set.prototype.size = () => {
    return Object.keys(this.items).length
  }
  //values（）：返回一个包含集合中所有值的数组；
  Set.prototype.values = () => {
    return Object.keys(this.items)
  }
}
```

#### 测试代码

```javascript
//测试集合类
//1.创建Set类对象
let set = new Set()
//添加元素
//2.测试add方法
console.log(set.add('a'));
console.log(set.add('a'));
console.log(set.add('b'));
console.log(set.add('c'));
console.log(set.add('d'));
//3.测试values方法
console.log('set.values()',set.values());
//删除元素
//4.测试remove方法
console.log('set.remove(a)',set.remove('a'));
console.log('set.remove(a)',set.remove('a'));
console.log('set.values()',set.values());
//5.测试has方法
console.log('set.has(b)',set.has('b'));
//6.测试size方法和clear方法
console.log('set.size()',set.size());
set.clear()
// 由于clear方法的实现原理为指向另外一个空对象，所以不影响原来的对象
console.log('set.size()',set.size());
console.log('set.values()',set.values());
```

#### 测试结果

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657074038906-7e221d84-c71e-40d4-bb27-393dad98f1ce.png#clientId=ufed64531-909e-4&crop=0&crop=0&crop=1&crop=1&from=paste&height=381&id=u1c8393d0&margin=%5Bobject%20Object%5D&name=image.png&originHeight=447&originWidth=501&originalType=binary&ratio=1&rotation=0&showTitle=false&size=19048&status=done&style=none&taskId=ua8233840-02ab-4202-b48f-24479e57a82&title=&width=427.5)


### 3.1.3 集合间操作

#### 集合间操作

- **并集**：对于给定的两个集合，返回一个**包含两个集合中所有元素**的新集合
- **交集**：对于给定的两个集合，返回一个**包含两个集合中共有元素**的新集合
- **差集**：对于给定的两个集合，返回一个**包含所有存在于第一个集合，且不存在于第二个集合的元素**的新集合
- **子集**：验证一个给定集合，**是否是另一个集合的子集**

  

#### 并集的实现

实现思路：创建集合`C`，代表集合`A`和集合`B`的并集，先将集合`A`中的所有元素添加到集合`C`中，再遍历集合`B`，如果是集合`C`所没有的元素，就把它添加到集合`C`中。     <br /> 
```javascript
 Set.prototype.union = otherSet => {
   // this:集合对象A
   // otherSet:集合对象B
   //1.创建一个新的集合
   let unionSet = new Set()

   //2.将A集合中的所有元素添加到新集合中
   let values = this.values()
   // for(let i of values){
   //   unionSet.add(i)
   // }
   for(let i = 0;i < values.length;i++){
     unionSet.add(values[i])
   }

   //3.取出B集合中的元素,判断是否需要加到新集合中
   values = otherSet.values()
   // for(let i of values){
   //   //由于集合的add方法已经对重复的元素进行了判断,所以这里可以直接添加
   //   unionSet.add(i)
   // }
   for(let i = 0;i < values.length;i++){
     unionSet.add(values[i])
   }
   return unionSet
 }
```

#### 交集的实现

实现思路： 遍历集合`A`，当取得的元素也存在于集合`B`时，就把该元素添加到另一个集合`C`中。          
```javascript
 Set.prototype.intersection = otherSet => {
   // this:集合A
   // otherSet:集合B
   //1.创建新的集合
   let intersectionSet = new Set()

   //2.从A中取出一个元素，判断是否同时存在于集合B中，是则放入新集合中
   let values = this.values()
   for(let i =0 ; i < values.length; i++){
     let item = values[i]
     if (otherSet.has(item)) {
       intersectionSet.add(item)
     }
   }
   return intersectionSet
 }
```

#### 差集的实现

实现思路： 遍历集合`A`，当取得的元素不存在于集合`B`时，就把该元素添加到另一个集合`C`中。       
```javascript
Set.prototype.diffrence = otherSet => {
  //this:集合A
  //otherSet:集合B
  //1.创建新的集合
  var diffrenceSet = new Set()

  //2.取出A集合中的每一个元素，判断是否同时存在于B中，不存在则添加到新集合中
  var values = this.values()
  for(var i = 0;i < values.length; i++){
    var item = values[i]
    if (!otherSet.has(item)) {
      diffrenceSet.add(item)
    }
  }
  return diffrenceSet
}
```

#### 子集的实现

实现思路： 遍历集合`A`，当取得的元素中有一个不存在于集合`B`时，就说明集合`A`不是集合`B`的子集，返回**false**。      
```javascript
 Set.prototype.subset = otherSet => {
   //this:集合A
   //otherSet：集合B
   //遍历集合A中的所有元素，如果发现，集合A中的元素，在集合B中不存在，那么放回false，如果遍历完整个集合A没有返回false，就返回true
   let values = this.values()
   for(let i = 0; i < values.length; i++){
     let item = values[i]
     if(!otherSet.has(item)){
       return false
     }
   }
   return true
 }
```


## 3.2 字典结构

### 3.2.1 字典简介

#### 字典的特点

- 字典存储的是键值对，主要特点是一一对应
- 比如保存一个的信息，数组形式：[20,'nino','male']，可通过下标值取出信息；字典形式：{"age":20,"name":"nino","sex":"male"}，可以通过key取出value
- 此外，在字典中，key是不能重复且无序的，而value可以重复

#### 字典和映射的关系

有些编程语言中称这种**映射关系**为字典，如Swift中的Dictionary，Python中的dict    <br />有些编程语言中称这种**映射关系**为Map，如Java中的HashMap，TreeMap等

#### 字典类常见的操作

- `set(key,value)`：向字典中添加新元素。
- `remove(key)`：通过使用键值来从字典中移除键值对应的数据值。
- `has(key)`：如果某个键值存在于这个字典中，则返回true，反之则返回false。
- `get(key)`：通过键值查找特定的数值并返回。
- `clear()`：将这个字典中的所有元素全部删除。
- `size()`：返回字典所包含元素的数量。与数组的length属性类似。
- `keys()`：将字典所包含的所有键名以数组形式返回。
- `values()`：将字典所包含的所有数值以数组形式返回。

### 3.2.2 字典结构的封装

字典类可以基于JavaScript中的对象结构来实现，比较简单，这里直接实现字典类中的常用方法  

```javascript

function Dictionary(params) {
  //字典属性
  this.items = {}
  //set(key,value)：向字典中添加新元素。
  Dictionary.prototype.set = (key, value) => {
    this.items[key] = value
  }
  //has(key)：如果某个键值存在于这个字典中，则返回true，反之则返回false。
  Dictionary.prototype.remove = (key) => {
    return this.items.hasOwnProperty(key)
  }
  //remove(key)：通过使用键值来从字典中移除键值对应的数据值。
  Dictionary.prototype.remove = (key) => {
    if (!this.has(key)) return false
    delete this.items[key]
    return true
  }
  //get(key)：通过键值查找特定的数值并返回。
  Dictionary.prototype.get = key => {
    return this.has(key) ? this.items[key] : undefined
  }
  //clear()：将这个字典中的所有元素全部删除。
  Dictionary.prototype.clear = () => {
    this.items = {}
  }
  //size()：返回字典所包含元素的数量。与数组的length属性类似。
  return this.keys().length
  //keys()：将字典所包含的所有键名以数组形式返回。
  Dictionary.prototype.keys = () => {
    return Object.keys(this.items)
  }
}
```
