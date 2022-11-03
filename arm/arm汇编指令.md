# *ARM 汇编指令*

## arm汇编指令格式
    <opcode> {cond} {s} <Rd>, <Rn> {, Operand2} {;annotation}

    1. <>: 代表必选项，{}代表可选项。
    2. opcode: 是二进制机器指令的操作码助记符，如mov, add。
    3. cond: 执行条件。
    4. s: 是否影响CPSR寄存器中的标志位。如subs指令会影响CPSR寄存器中的N、Z、C、V标志位。而sub指令不会。
    5. Rd: 目标寄存器。
    6. Rn: 第一个操作数的寄存器。
    7. operand2: 第二个可选操作数。
    8. ;: 分号后面的代表注释。
   
## 代码结构

        AREA project_name, CODE, READONLY
        ENTRY
        CODE32
    START
        ADD R1, R2, #3
    END

## 条件码和状态码

    EQ(等于，Equal) ==
    NE(不等于，Not Equal) !=
    CS(高于或同于,进位设置，Carry Set) >=
    CC(低于,进位清除，Carry Clear) <

    MI(负号，MInus) < 0
    PL(正号，PLus) >=0
    VS(溢出设置，oVerflow Set)
    VC(溢出清除，oVerflow Clear)

    HI(高于，HIgher) >
    LS(低于或同于，Lower or Same) <=
    GE(大于等于，Greater or equal) >=
    LT(小于，Less Than) <
    GT(大于，Greater Than) >
    LE(小于等于，Less or equal) <=
    AL(总是，Always) 永真
    NV(从不，Never ) 永假

## 立即数

&emsp;&emsp;立即树以#为前缀，0x前缀表示该立即数为十六进制，不加前缀默认是十进制。在ARM数据处理指令中，当参与操作的第二操作数为立即数时， 每个立即数都是采用一个8位的常数循环右移偶数位而间接得到（关于循环移位，其实arm中只有循环右移ROR），其中循环右移的位数有一个4位二进制的2倍表示。

1.判断一个数是否符合8位位图的原则， 首先看这个数的二进制表示中1的个数是否不超过8个。 如果不超过8个，再看这n个1(n<=8)是否能同时放到8个二进制位中， 如果可以放进去， 再看这八个二进制位是否可以循环右移偶数位得到我们欲使用的数。 如果可以，则此数符合8位位图原理， 是合法的立即数。否则，不符合。

2.无法表示的32位数，只有通过逻辑或算术运算等其它途径获得了。比如0xffffff00，可以通过0x000000ff按位取反得到。
