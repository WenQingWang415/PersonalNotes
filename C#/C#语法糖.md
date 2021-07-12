**1.问号的演变**

老掉牙的一个问号+冒号

```javascript
var b = 3;
var a = b > 9?b.ToString():”0”+b;
```

新宝宝两个问号 ??，它表示左边的变量如果为null则值为右边的变量，否则就是左边的变量值

```javascript
string a = null;
var b = a??"";
```

**2.集合类各个项的操作**

我们为了逐个处理集合中的项，需要这么写：

```C#
 foreach (var item in list)
 {
     item.money = AESEncryptHelper.Decrypt(item.money);
     item.check_amount = AESEncryptHelper.Decrypt(item.check_amount);
 }
```

现在不需要了，这样就可以了

```C#
 list.ForEach(m => {
     m.check_amount = AESEncryptHelper.Decrypt(m.check_amount);
     m.money = AESEncryptHelper.Decrypt(m.money);
 });
```

**3.类型实例化**

未简化的写法

```C#
User u = new User();
u.ID = 1;
u.Name = "PanPan";
```

简化之后的写法

```C#
User u = new User() 
{
    ID=1,
    Name="PanPan"
};
```

