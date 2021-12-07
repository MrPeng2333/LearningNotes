# go

## MrPeng2333

### go命令行操作

#### go命令行有哪些常用操作？

##### 在命令行执行go查看go的命令行常用操作

#### go build命令的作用？

##### 用于测试编译，会同时编译与之相关联的包

##### 默认编译当前目录下所有go文件，可以在go build命令之后指定文件编译

##### 使用-o参数指定输出可执行文件名

#### go fmt命令的作用？

##### 格式化代码文件

##### 使用go fmt或gofmt格式化代码文件，加上参数-w，否则不会格式化结果不会写入文件

##### go fmt -w src可以格式化整个项目

#### go get命令的作用？

##### 动态获取远程代码包

##### 命令内部分成两步：下载源码包，执行go install

##### go从GitHub下载源码包使用的是git工具

#### go install命令的作用？

##### 测试编译文件，将编译的中间文件放在$GOPATH/pkg目录下，将编译结果放在$GOPATH/bin目录下

##### 命令内部分为两步：生成结果文件（可执行文件或者.a包）；移动结果文件到$GOPATH/pkg或$GOPATH/bin目录下

#### go test命令的作用？

##### 读取目录下*_test.go的文件，生成并运行测试用的可执行文件

##### 默认测试所有test文件，命令参数参考go help testflag

#### go doc命令的作用？

##### 查看package的文档，也可以查看包中某个函数的文档

#### go generate命令的作用？

##### 扫描与当前包相关的源代码文件，提取并执行源码文件中注释//go:generate后的命令

### 变量与常量

#### 单普通变量有哪些声明方式？

##### var name type [= value]

##### name := value：自动识别value的类型

#### 多普通变量有哪些声明方式？

##### var name1, name2 type [= value1, value2]

##### name1, name2 := value1, value2

##### var (name1 type1 [= value1] \n name2 type2 [=value2])

##### var(name1 := value1 \n name2 := value2)

#### 指针变量有哪些声明方式？

##### var name *type [ = &varName]

##### name := &varName

##### name := new(type)

#### 常量（单、多）有哪些声明方式？

##### const name type = value

##### const name1, name2 type = value1, value2

##### const (name1 type1 = value1 \n name2 type2 = value2)

#### 多常量快速赋值（连续值）？

##### const (a = 1 + iota \n b )

##### const (a = 1 << iota \n b)

### 类型

#### go中有哪些变量类型？

##### 布尔类型：bool

##### 整数类型：int、int8、int16、int32、int64、uint、uint8、uint16、uint32、uint64

##### 浮点类型：float32、float64

##### 复数类型：complex32、complex64

##### 字符型：rune，int32别名，表示单个Unicode字符

##### 字符型：byte，uint8别名，对应ACSII码值

##### 字符串：string

##### 指针：pointer

##### 数组：array

##### 切片：slice

##### 字典/映射：map

##### 通道：channel

##### 结构体：struct

##### 接口：interface

##### 错误：error，go内部定义好的一个接口

#### 变量未初始化时的默认值？

##### 基础类型默认位类型零值

##### 引用类型变量为nil，使用引用类型变量需要初始化

#### 字典类型变量的声明？

##### var name map[keyType]valueType[ = map[key]valueType{key1:value1, key2:value2}]

##### name := map[keyType]valueType{key1:value1, key2:value2}

##### name := make(map[keyType]valueType, size, cap)

#### 数组类型变量的声明？

##### var name [size]type [= [size]type{value1, value2}]

##### name := [size]type{value1, value2}

#### 切片类型变量的声明？

##### var name []type = []type{value1, value2}

##### name := []type{value1, value2}

##### name := make([]int, size, cap)

#### 通道类型变量的声明？

##### var name chan type

##### name := make(chan type, cap)

#### make函数的作用？

##### 用于且只能用于切片、字典、通道类型变量的初始化

#### 结构体变量的声明？

##### var name structName [= structName{field1Value, field2Value}]

##### name := structName{field1Value, field2Value}

#### 接口变量的声明？

##### var name interfaceName [= structName{field1Value, field2Value}]

##### var name interfaceName [= &structName{field1Value, field2Value}]

##### 两种声明方式的区别在于结构体实现接口方法时，只要有一个方法传入的是指针就要使用第二种声明方式，没有传入指针也可以使用第二种声明方式

##### 第二种方式避免了内存的拷贝，一般情况下使用第二种方式

#### 为类型定义别名的格式？

##### type aliasName typeName

### 函数

#### go函数定义的基本格式？

##### func funcName(para1 type1, para2 type2) (returnValueType1, returnValueType2) {}

##### 当传入的多个参数为同一类型时，可以简写为para1, para2 type

#### go函数参数传递的方式？

##### 默认以值传递的方式传递参数，可以通过在类型前加*以引用（指针）方式传递参数

#### What-go函数变量？

##### 在go中，可以将函数作为值保存在变量中，此时变量的类型为func()

#### go中对函数返回值命名？

##### func funcName() (name type) {name := value \n return}

#### go中函数作为参数传递？

##### func funcName(name func(type1, type2) returnValueType)

### 包

#### go包的基本结构？

##### 一个目录下只能有一个包，导入路径即导入路径下的包

##### 包名用package关键字声明，可以不与目录名相同，同一个目录下的所有.go文件package声明的包名是相同的

##### 导入包时，只能通过路径导入，使用包时需要使用package声明的包名进行使用

#### main包的作用？

##### main包是go中程序的入口，更具体一点，main包中的main函数是程序的入口

#### 包的引入格式？

##### import "packagePath"

##### import ("packagePath1" \n "packagePath2")

#### 引入包起别名格式？

##### import alias "packagePath"

#### 匿名引入包格式？

##### import _ "packagePath"

#### 包中的初始化函数定义要求？

##### 函数名为init

##### 无参数，无返回值

##### 同一个包中可定义多个init

#### 引入包的init函数执行顺序？

##### ![](https://gitee.com/mr-peng2333/image-storage/raw/master/img/20211123222729.png)

##### 同一个包中的多个init函数按照他们呈现给编译器的顺序被调用

### 数组

#### 数组初始化的方式？

##### arr := [size]type{value1, value2}

##### arr := [...]type{value1, value2}

### 切片

#### 切片初始化的3种方式？

##### arr[0:3] or slice[0:3]

##### slice := []type{value1, value2}

##### slice := make([]type, size, cap)

#### 获取切片的长度和容量的函数？

##### len(slice)

##### cap(slice)

#### 使用append函数向切片追加元素的格式？

##### append(slice, elem1, elem2)

##### append(slice1, slice2...)：只支持两个参数，将后一个切片拼接到第一个切片后

#### 切片扩容的策略？

##### 如果期望容量大于当前容量的两倍就会使用期望容量

##### 如果当前切片的长度小于1024就会将容量翻倍

##### 如果当前切片的长度大于1024就好每次增加25%的容量，直到新容量大于期望容量

### 指针

#### 指针所占内存的大小？

##### 指针所占内存的大小是指指针指向的值的内存地址的大小，而不是指向的值的大小

##### 指针所占内存的大小在32位和64位机器上分别占用4字节和8字节，与所指向的值的大小无关

#### 取得指针存储地址指向的值的方式？

##### value := *ptr

### 结构体

#### 空结构体的用处？

##### 并发编程中，channel之间的通讯，可以使用一个struct{}作为信号量

#### 指针结构体访问结构体的方式？

##### structPtr.fieldName/methodName()

##### .号具有解引用的作用，不用在指针结构体前加*号进行取值操作

#### 结构体中字段、方法可见性的控制方式？

##### 字段和方法首字母大写，所有包可见

##### 字段和方法首字母小写，只能包内可见

#### 结构体标签的定义格式？

##### type name struct {fieldName type `key:value`}

#### 结构体组合其他结构体的格式？

##### type name struct {field structName}

##### type name struct {structName}：这种方式叫做匿名字段，可以通过结构体直接访问

### 方法

#### 什么是方法？

##### 方法是一般是面向对象编程（OOP）的一个特性，在C++语言中方法对应一个类对象的成员函数

#### 结构体绑定方法的两种方式？

##### func(s structName)methodName(para type){}

##### func(s *structName)methodName(para type){}

### 接口

#### 结构体实现接口？

##### 结构体只需要实现了接口的所有方法即实现了接口，没有显式的实现关系

### 协程

#### 进程、线程、协程的区别？

##### 进程和线程都是由内核进行调度，有CPU时间片的概念，进行抢占式调度

##### 协程是用户级线程，内核并不知道有协程的存在，是完全由用户自己的程序即golang调度的；由于是用户自己调度，就不能像抢占式调度做到强制的CPU控制权切换，只能做到协作式调度，需要协程自己主动把控制权转让出去后，其他协程才能执行

#### 创建一个协程的格式？

##### 在函数或方法前面加go关键字就可以创建一个协程

### 信道

#### 什么是信道？

##### 信道是协程之间的通信机制，可以让一个协程与另一个协程传输信息的通道

#### 信道操作（发送、读取）数据的格式？

##### channelName <- data

##### varName <- channelName

#### 关闭信道的格式？

##### close(channelName)

#### 为什么要关闭信道？

##### 避免有“人”一直在等待

### 缓冲区

#### 无缓冲通道和缓冲通道的声明格式？

##### 无缓冲：var name chan type/ name := make(chan type) / name := make(chan type, 0)

##### 有缓冲：name := make(chan type, bufferSize)

#### 缓冲通道和无缓冲通道的区别？

##### 有缓冲的通道能存储多个值，如果通道内的信息被取完，则信息接收方陷入阻塞，直到信息发送方将信息放入，如果通道信息已放满，则信息发送方需等信息接收方取走信息，通道有空余时才能放入信息

##### 无缓冲的通道，发送信息方需一直等待知道信息接收方接收掉信息；信息接收方也需一直等待直到信息发送方发送信息

### 选择

#### 什么是选择（select）？

##### 选择（select）是与switch类似的控制结构，和switch不同的是，select的case后接的是channel的收发操作

##### 当所有case后的channel操作都阻塞时，会直接执行default后面的语句

##### 当有多个case后的Channel操作可以执行，会随机选择一个执行

### 互斥锁

#### 什么是互斥锁？

##### 互斥锁是指在同一时刻，只能有一个协程对当前锁住的代码块(具体变量)进行读写，其他协程必须等待正在读写的协程完成操作解锁后再进行读写操作

##### 互斥锁的一般使用格式？

##### ![](https://gitee.com/mr-peng2333/image-storage/raw/master/img/20211207153540.png)

#### 互斥锁和协程的关系？

##### 已经上锁的互斥锁和具体的协程没有关联，即可以用一个协程上锁，另一个协程解锁

##### 但还是建议在同一个协程、同一个函数或方法中对Mutex进行上锁和解锁

#### 互斥锁的人为互斥是什么？

##### 在一个协程中被锁住的变量，在另一个协程中



