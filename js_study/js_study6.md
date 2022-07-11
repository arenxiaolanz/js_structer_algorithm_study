# 六、图解红黑树

## 6.1 红黑树的五条规则



红黑树除了符合二叉搜素树的基本规则外，还添加了以下特性：

- 节点是**红色或黑色**的

- **根**节点是**黑色**的

- 每个**叶子**节点都是**黑色的空节点（NIL节点）**

- 每个**红色节点的两个子节点都是黑色**的（从每个叶子到根的所有路径上，**不可能有**两个**连续**的**红色**节点）

- 从**任意节点**到其每个**叶子节点**的所有路径，都包含**相同数目的黑色节点**


## 6.2 红黑树的相对平衡



 前面5条规则的约束确保了以下红黑树的关键特性：

- 从根到叶子节点的最长路径，不会超过最短路径的两倍；

- 结果就是这棵树基本是平衡的；

- 虽然没有做到绝对的平衡，但是可以保证在最坏的情况下，该树依然是高效的；


为什么可以做到最长路径不超过最短路径的两倍呢？<br /> 

- 性质4决定了路径上不能有两个相连的红色节点；

- 所以，最长路径一定是红色节点和黑色节点交替而成的；

- 由于根节点和叶子节点都是黑色的，最短路径可能都是黑色节点，并且最长路径中一定是黑色节点多于红色节点；

- 性质5决定了所有路径上都有相同数目的黑色节点；

- 这就表明了没有路径能多于其他任何路径两倍长。<br /> 

## 6.3 红黑树的三种变换


插入一个新节点时，有可能树不再平衡，可以通过三种方式的变换使树保持平衡

- 变色

- 左旋转

- 右旋转


### 变色

为了重新符合红黑树的规则，需要把**红色节点变为黑色**，或者把黑**色节点变为红色；**

插入的新节点通常都是**红色节点**：

- 当插入的节点**为红色**的时候，大多数情况**不违反**红黑树的任何规则

- 而插入**黑色**节点，必然会导致一条路径上**多了一个黑色节点**，这是很难调整的；

- 红色节点虽然可能导致**红红相连**的情况，但是这种情况可以通过**颜色调换和旋转**来调整；<br /> 

### 左旋转

 以**节点X为根逆时针旋转**二叉搜索树，使得**父节点**原来的位置被自己的**右子节点**替代，**左子节点**的位置被**父节点**替代；      

![C%M0XTP1MTHVPRQKV{78BHU.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657198073643-ffb1d5d1-7ef2-4999-bfef-25ac782f5c10.png#clientId=ud38460c5-73fc-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u2b443193&margin=%5Bobject%20Object%5D&name=C%25M0XTP1MTHVPRQKV%7B78BHU.png&originHeight=261&originWidth=521&originalType=binary&ratio=1&rotation=0&showTitle=false&size=85963&status=done&style=none&taskId=ucb421ef7-f3ed-41af-9960-4d502a33ae7&title=)

 如上图所示，左旋转之后：

- 节点X取代了节点a原来的位置；

- 节点Y取代了节点X原来的位置；

- 节点X的左子树 a 仍然是节点X的左子树（这里X的左子树只有一个节点，有多个节点时同样适用，以下同理）；

- 节点Y的右子树 c 仍然是节点Y的右子树；

- 节点Y的左子树 b 向左平移成为了节点X的右子树； 

除此之外，二叉搜索树左旋转之后仍为二叉搜索树      <br /> 

### 右旋转

 以节点**X为根顺时针旋转**二叉搜索树，使得**父节点**原来的位置被自己的**左子节点**替代，**右子节点**的位置被**父节点**替代；    

![PK4YTWTZT4`W(1S2NOP}N3U.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657198094782-c0d0bcde-28df-4250-9316-cac6297e69f3.png#clientId=ud38460c5-73fc-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=ub2fcaeb9&margin=%5Bobject%20Object%5D&name=PK4YTWTZT4%60W%281S2NOP%7DN3U.png&originHeight=238&originWidth=536&originalType=binary&ratio=1&rotation=0&showTitle=false&size=76220&status=done&style=none&taskId=uf9a0ad63-a271-4ca0-bc88-cb98df70c7d&title=)

 如上图所示，右旋转之后：

- 节点X取代了节点a原来的位置；

- 节点Y取代了节点X原来的位置；

- 节点X的右子树 a 仍然是节点X的右子树（这里X的右子树虽然只有一个节点，但是多个节点时同样适用，以下同理）；

- 节点Y的左子树 b 仍然是节点Y的左子树；

- 节点Y的右子树 c 向右平移成为了节点X的左子树；

除此之外，二叉搜索树右旋转之后仍为二叉搜索树  


## 6.4 红黑树的插入操作

 首先需要明确，在保证满足红黑树5条规则的情况下，**新插入的节点必然是红色节点。    **<br />   <br />为了方便说明，规定以下四个节点：   

- 新插入节点为N（Node）

- N的父节点为P（Parent）

- P的兄弟节点为U（Uncle）

- U的父节点为G（Grandpa）

- 如下图所示：

![C$KI3J$2BIMA{4CO[26$RTI.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657198405480-340122f5-00ab-4576-b3b5-6325bf680357.png#clientId=ud38460c5-73fc-4&crop=0&crop=0&crop=1&crop=1&from=drop&height=364&id=uf9e6d54b&margin=%5Bobject%20Object%5D&name=C%24KI3J%242BIMA%7B4CO%5B26%24RTI.png&originHeight=342&originWidth=442&originalType=binary&ratio=1&rotation=0&showTitle=false&size=49784&status=done&style=none&taskId=u5d217ca7-d56a-457e-a452-64aff6d2eab&title=&width=471)

### 情况一（根）

- 当插入的新节点**N**位于**树的根上**时，**没有父节点**。

- 这种情况下，只需要将**红色节点变为黑色节点**即可满足规则2 。


![BF76_CPK~}C0Z4S(VLP92UV.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657198756277-71c29f78-10cd-4027-807b-398ed41a7c57.png#clientId=ud38460c5-73fc-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u78e44705&margin=%5Bobject%20Object%5D&name=BF76_CPK~%7DC0Z4S%28VLP92UV.png&originHeight=184&originWidth=201&originalType=binary&ratio=1&rotation=0&showTitle=false&size=11516&status=done&style=none&taskId=ua1ddf092-8c16-4bf1-b67a-1976b5b76a4&title=)

### 情况二（P为黑）

- 新节点N的**父节点P为黑色**节点，此时**不需要**任何变化。

- 此时既满足规则4也满足规则5。尽管新节点是红色的，但是新节点**N有两个黑色节点NIL**，所以通向它的路径上**黑色节点的个数依然相等**，因此满足规则5 。


### 情况三（父红叔红祖黑）

 节点P为红色，节点U也为红色，此时节点G必为黑色，即父红叔红祖黑。   

在这种情况下需要：  

- 先将父节点P变为黑色；

- 再将叔叔节点U变为黑色；

- 最后将祖父节点G变为红色；

- 即变为父黑叔黑祖红，如下图所示：

![YBE%JSE[{VWTR)MWJZJ(}8N.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657199034383-ae28659f-c600-4763-8069-55c1bbfb41ec.png#clientId=ud38460c5-73fc-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=uc3bedd42&margin=%5Bobject%20Object%5D&name=YBE%25JSE%5B%7BVWTR%29MWJZJ%28%7D8N.png&originHeight=342&originWidth=562&originalType=binary&ratio=1&rotation=0&showTitle=false&size=50302&status=done&style=none&taskId=ubad75806-6a25-4a7e-9185-d76ce1c08ac&title=)

可能出现的问题：

- N的祖父节点G的父节点也**可能是红色**，这就违反了规则4，此时可以通过**递归调整节点颜色**；

- 当**递归调整到根节点**时就需要**旋转**了，如下图节点A和节点B所示，具体情况后面会介绍；<br /> 

### 情况四（**父红叔黑祖黑，左节点，右旋转**）

节点P是红色节点，节点U是黑色节点，并且节点N为节点P的**左子节点**，此时节点G一定是黑色节点，即**父红叔黑祖黑**。   

在这种情况下需要：  

- **先变色**：将父节点**P**变为**黑色**，将祖父节点**G**变为**红色**；

- **后右旋转**：以祖父节点G为根进行**右旋转**；<br /> 

![@}GV{[KWA`R$7D2S(D2KFVO.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657199235153-f3acfc5e-0efe-4d04-b654-b5e953c0cd46.png#clientId=ud38460c5-73fc-4&crop=0&crop=0&crop=1&crop=1&from=drop&height=196&id=u3cdca7aa&margin=%5Bobject%20Object%5D&name=%40%7DGV%7B%5BKWA%60R%247D2S%28D2KFVO.png&originHeight=229&originWidth=619&originalType=binary&ratio=1&rotation=0&showTitle=false&size=54237&status=done&style=none&taskId=ue3917267-e1c2-48b4-bdc7-d1ecf300b6c&title=&width=529)


### 情况五（**父红叔黑祖黑，右节点，左旋转**）

节点P是红色节点，节点U是黑色节点，并且节点N为节点P的**右子节点**，此时节点G一定是黑色节点，即**父红叔黑祖黑**。             

在这种情况下需要：

- 先以节点**P为根进行左旋转**，旋转后如图b所示；

- 随后将**红色节点P和黑色节点B**看成一个**整体的红色节点N1**，将新插入的红色节点N看成红色节点P1 如图c所示。此时整体就转换为了情况4。

![U$H~C}7Y39HFR)G3(5_%KQ9.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657199482357-4d216159-5e9e-4bfb-bbb5-2262c7fc699d.png#clientId=ud38460c5-73fc-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u99881c2f&margin=%5Bobject%20Object%5D&name=U%24H~C%7D7Y39HFR%29G3%285_%25KQ9.png&originHeight=219&originWidth=568&originalType=binary&ratio=1&rotation=0&showTitle=false&size=47683&status=done&style=none&taskId=u3af2a321-5adf-4fd2-bac2-3746680674b&title=)


接着可以按照情况4进行处理：

- 先变色：将N1节点的父节点P1变为黑色，将祖父节点G变为红色；

- 后旋转：以祖父节点G为根进行右旋转，旋转后如图 e所示；<br />最后将节点N1和P1变换回来，完成节点N的插入，如图所示；<br /> 


## 6.5 红黑树的案例

在二叉树中依次插入：10，9，8，7，6，5，4，3，2，1    

### 插入10

**符合情况一**

- 插入节点10

- 将节点10的颜色变为黑色

![N%(1N)G~)LA1XAYQHOBSY3X.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657200811284-65eea9ca-5b8a-4828-ac33-71dc86e62ba3.png#clientId=ud38460c5-73fc-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u42cd83a9&margin=%5Bobject%20Object%5D&name=N%25%281N%29G~%29LA1XAYQHOBSY3X.png&originHeight=113&originWidth=121&originalType=binary&ratio=1&rotation=0&showTitle=false&size=16746&status=done&style=none&taskId=u40a6d346-3cb8-4ea8-8cc4-35b7b18bfc9&title=)

### 插入9

**符合情况二**

- 插入节点9

- 不需要任何情况

![S@_OB2Q15Q6I()92$WNGM7B.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657200817666-33319af2-8618-4136-a03b-708ccd5fdaef.png#clientId=ud38460c5-73fc-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=uea8daba2&margin=%5Bobject%20Object%5D&name=S%40_OB2Q15Q6I%28%2992%24WNGM7B.png&originHeight=237&originWidth=228&originalType=binary&ratio=1&rotation=0&showTitle=false&size=38836&status=done&style=none&taskId=u71f642b2-5d87-4d96-b0a4-074e2b25166&title=)

### 插入8

**符合情况四**

- 插入节点8

- 先变色，**9 -> 黑 ,10 -> 红**

- 再**以祖父节点10为根右旋转**

![{CG)F[[5C{FVC`YUFA${AXO.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657200835492-522c371b-aebc-489a-8cd2-5598a6dcbd38.png#clientId=ud38460c5-73fc-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u5b1332ea&margin=%5Bobject%20Object%5D&name=%7BCG%29F%5B%5B5C%7BFVC%60YUFA%24%7BAXO.png&originHeight=287&originWidth=657&originalType=binary&ratio=1&rotation=0&showTitle=false&size=91636&status=done&style=none&taskId=uec42414a-47e1-4e50-b2d2-024b062c751&title=)

### 插入7

**符合情况三**

- 插入节点7

- 先变色，**8,10 -> 黑 , 9 -> 红**

- 再把祖父元素**9变为黑色**

![RX{8~LZIV3$XES0]0EYRB8S.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657201400668-109e0ff5-1886-4f94-b36f-44e1a7072dcd.png#clientId=ud38460c5-73fc-4&crop=0&crop=0&crop=1&crop=1&from=drop&height=167&id=ue9a84cbf&margin=%5Bobject%20Object%5D&name=RX%7B8~LZIV3%24XES0%5D0EYRB8S.png&originHeight=301&originWidth=1010&originalType=binary&ratio=1&rotation=0&showTitle=false&size=163407&status=done&style=none&taskId=uea6630b7-c4c4-4931-adc4-1abd3c17ae0&title=&width=560)


### 插入6

**符合情况四**

- 插入节点6

- 先变色，**7 -> 黑 , 8 ->  红**

- 再**以祖父节点8为根右旋转**

![M0YG@D95]TT$FV{`FUTI$%Y.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657201700973-f6835b0f-be4d-4dca-b2c6-0891febe8e4d.png#clientId=ud38460c5-73fc-4&crop=0&crop=0&crop=1&crop=1&from=drop&height=202&id=u0e8a997a&margin=%5Bobject%20Object%5D&name=M0YG%40D95%5DTT%24FV%7B%60FUTI%24%25Y.png&originHeight=389&originWidth=1064&originalType=binary&ratio=1&rotation=0&showTitle=false&size=195451&status=done&style=none&taskId=u086db68c-4f35-4a5a-98b0-c31348079ca&title=&width=552)


### 插入5

**符合情况三**

- 插入节点5

- 先变色，**6，8 -> 黑 , 7 ->  红**

![{I_(]72Y(N0)7C~FU4~5_%S.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657201933448-b88988ea-0d05-4100-9b16-1140bac2d83d.png#clientId=ud38460c5-73fc-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=uca8492e2&margin=%5Bobject%20Object%5D&name=%7BI_%28%5D72Y%28N0%297C~FU4~5_%25S.png&originHeight=377&originWidth=896&originalType=binary&ratio=1&rotation=0&showTitle=false&size=138039&status=done&style=none&taskId=u0659d59a-9ea3-4452-84aa-4121d3422db&title=)


### 插入4

**符合情况四**

- 插入节点4

- 先变色，**5 -> 黑 , 6 ->  红**

- 再**以祖父节点6为根右旋转**

![6EQ[G]D{T2{}2VZ7@E@I7MY.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657202025807-02205164-f4b5-48c4-b760-d6e9f673c781.png#clientId=ud38460c5-73fc-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u47cbeae9&margin=%5Bobject%20Object%5D&name=6EQ%5BG%5DD%7BT2%7B%7D2VZ7%40E%40I7MY.png&originHeight=441&originWidth=1128&originalType=binary&ratio=1&rotation=0&showTitle=false&size=279110&status=done&style=none&taskId=ub9d8151e-f1b3-4294-bd9c-931b005faee&title=)

### 插入3

**符合情况3**

- 插入节点8

- 先变色，**4，6 -> 黑 , 5 ->  红**

<br />

-  变换之后发现**5，7为相连的两个红色节点**，于是把**以5为根的整个子树**看成一个**新插入的节点N1**，再进行第二次变换。

**符合情况4**

- 插入节点N1

- 先变色，**7-> 黑 , 9 ->  红**

<br />

- 再**以祖父节点9为根右旋转**


![OKM_Y8W31H@@UHH04}LUH)U.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657202599411-56a700d8-d571-4823-a603-dbf8f1c00929.png#clientId=ud38460c5-73fc-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u95421947&margin=%5Bobject%20Object%5D&name=OKM_Y8W31H%40%40UHH04%7DLUH%29U.png&originHeight=492&originWidth=1141&originalType=binary&ratio=1&rotation=0&showTitle=false&size=354605&status=done&style=none&taskId=u930a268e-63cb-4271-94f4-255755f51cd&title=)


### 插入2

**符合情况四**

- 插入节点2

- 先变色，**3 -> 黑 , 4 ->  红**

- 再**以祖父节点4为根右旋转**

![4]OUHWUC6M43[V@O`_FSVJA.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657202800232-aa7cd6d1-a65d-4f07-afe1-c14eb781f71f.png#clientId=ud38460c5-73fc-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=ubfcd3c14&margin=%5Bobject%20Object%5D&name=4%5DOUHWUC6M43%5BV%40O%60_FSVJA.png&originHeight=440&originWidth=1154&originalType=binary&ratio=1&rotation=0&showTitle=false&size=304017&status=done&style=none&taskId=ufd04b308-45d9-453f-8753-76b168f7b58&title=)

### 插入1

**符合情况三**

- 插入节点1

- 先变色，**2，4 -> 黑 , 3 ->  红**

-  变换之后发现**3和5为相连**的两个红色节点，于是把**以3为根**的整个子树看成一个**新插入的节点N1**，再进行第二次变换。<br /> 

**符合情况三**

- 插入节点N1

- 先变色，**5，9 -> 黑 , 7 ->  红**

- 变换之后发现**根节点7为红色**不符合规则2，所以把**以7为根节点的红黑树看成一个新插入的节点N2**，再进行第三次变换。<br /> 

**符合情况一**

- 插入节点N2

- 变色，**7 ->  黑**

<br /> ![BTGXH@$ZP11P(0~(__5}HCV.png](https://cdn.nlark.com/yuque/0/2022/png/25602002/1657203345877-28590138-6aec-4171-9f8f-0fb85c3486c2.png#clientId=ud38460c5-73fc-4&crop=0&crop=0&crop=1&crop=1&from=drop&id=u8d2a0370&margin=%5Bobject%20Object%5D&name=BTGXH%40%24ZP11P%280~%28__5%7DHCV.png&originHeight=455&originWidth=1163&originalType=binary&ratio=1&rotation=0&showTitle=false&size=335741&status=done&style=none&taskId=u5052fe83-b6a9-4ce7-863b-80394815600&title=)



## 6.6 红黑树的删除操作
<br />红黑树的删除操作结合了复杂的二叉树的删除操作和复杂的红黑树的插入规则，整体来说难度非常大，篇幅较长，这里暂不进行探讨。  <br /> 





