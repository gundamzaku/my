以下面这个连接里的数据作为实际例子：

https://blockchain.info/block/0000000000000000004c3104da968d4088aaa0e6a8b2ab82daa2968a578e9794

先是将bits转换  

392009692转成16进制为：0x175d97dc  

再执行  
print(hex(0x5d97dc * 2**(8*(0x17 - 3)))) 
这个是Python代码，懒得转成其它语言了，随便网上搜个在线Python编辑器就可以执行。

执行结果是：0x5d97dc0000000000000000000000000000000000000000L    
长度不够不够，因为是64位数据，前面补上0  
将会得到得到TARGET  
0000000000000000005d97dc0000000000000000000000000000000000000000

上面这个是固定的公式，他是把0x175d97dc的后面六位和前面两位拆开来进行计算了，那个`*2`的2是版本号，即Version：0x20000000  
`**两个乘号就是乘方，即2的几次方`  
这里的0x20000000实际是一种被称为“小段格式编码”存储的值，实际是2。不太熟悉的可以去查一下“大端格式、小端格式”的概念。

根据比特币挖矿的算法，计算公式是： 
SHA256(SHA256(version + prev_hash + merkle_root + ntime + nbits + x )) < TARGET  
block的版本 version  
上一个block的hash值: prev_hash  
需要写入的交易记录的hash树的值: merkle_root  
更新时间: ntime  
当前难度: nbits  

Version:20000000
prev_hash：00000000000000000010ddc4fcbf331d5000c431aa6aa474bf38e85f9f1f5788  
merkle_root：4018fe3dd8f08ba3fcaf26819cbcdc0a6b3cddd624ef6f07897daf29734b5826   
ntime:2018-02-22 08:41:00    
nbits:392009692    
nounce:1111548121    

这是参与计算的几个变量，具体怎么计算可以参考代码  

https://github.com/gundamzaku/algorithms/blob/master/digmine.go  

最后得出的结果是：  
0000000000000000004c3104da968d4088aaa0e6a8b2ab82daa2968a578e9794  

这个结果和前面网址URL中的Hash是一至的，并且也比TARGET要小，完全符合规则。  
这只是演示，nounce这个数字一开始是不存在的，需要矿工去猜，猜中去并且按照上面的规则成立，才算是挖矿成功。


