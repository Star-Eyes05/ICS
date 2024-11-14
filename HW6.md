### 5.13~5.16
##### 5.13A.
```                 
       %rcx                       %xmm0       
        |                           |
        |                           |  : key path
        |---->load------ |          |
        |                |          |
        |                |          |
        |                v          v
        |----> load ---> mul --->  add 
        |                           |
        |                           |
        v                           |
       add                          |
        |                           |
        |                           |
        v                           v
       %rcx                       %xmm0
```
##### 5.13B.

浮点数加法

##### 5.13C.

整数加法

##### 5.13D.

关键路径上只有加法

##### 5.14.

```C++
int limit = length - 5;
for(i=0;i<limit;i+=6)
{
    sum = sum + udata[i]*vdata[i] 
    + udata[i+1]*vdata[i+1] 
    + udata[i+2]*vdata[i+2] 
    + udata[i+3]*vdata[i+3] 
    + udata[i+4]*vdata[i+4] 
    + udata[i+5]*vdata[i+5];
}
for(;i<length;i++)
{
    sum = sum + udata[i]*vdata[i];
}
*dst = sum;
```

虽然展开了6次，但关键路径上仍然有length个浮点加法
达到了浮点加法的吞吐量极限

##### 5.15.

```C++
int limit = length - 5;
for(i=0;i<limit;i+=6)
{
    sum1 += udata[i]*vdata[i];
    sum2 += udata[i+1]*vdata[i+1];
    sum3 += udata[i+2]*vdata[i+2];
    sum4 += udata[i+3]*vdata[i+3];
    sum5 += udata[i+4]*vdata[i+4];
    sum6 += udata[i+5]*vdata[i+5];
}
for(;i<length;i++)
{
    sum1 +=  udata[i]*vdata[i];
}
*dst = sum1 + sum2 + sum3 + sum4 + sum5 + sum6;
```

寄存器溢出，或者分支预测错误

##### 5.16.

```C++
int limit = length - 5;
for(i=0;i<limit;i+=6)
{
    sum = sum + (udata[i]*vdata[i] 
    + udata[i+1]*vdata[i+1] 
    + udata[i+2]*vdata[i+2] 
    + udata[i+3]*vdata[i+3] 
    + udata[i+4]*vdata[i+4] 
    + udata[i+5]*vdata[i+5]);
}
for(;i<length;i++)
{
    sum = sum + udata[i]*vdata[i];
}
*dst = sum;
```

### 6.30~6.33
##### 6.30A.

$C = S \times E\times B=128$

##### 6.30B.

| CT | CT | CT | CT|CT| CT| CT| CT| CI| CI|CI| CO|CO|
| --- | --- | --- |---|---|---|---|---|---|---|---|---|---|

##### 6.31A. 

| 0 | 0 | 1 | 1|1| 0| 0| 0| 1| 1|0| 1|0|
| --- | --- | --- |---|---|---|---|---|---|---|---|---|---|

##### 6.31B.

|参数|值|
| --- | --- |
|CO| 0x02|
|CI| 0x06|
|CT| 0x38|
|是否命中|hit|
|返回字节|0xe3|

##### 6.32A.

| 1 | 0 | 1 | 1|0| 1| 1| 1| 0| 1|0| 0|0|
| --- | --- | --- |---|---|---|---|---|---|---|---|---|---|

##### 6.32B.

|参数|值|
| --- | --- |
|CO| 0x00|
|CI| 0x02|
|CT| 0xb7|
|是否命中|miss|
|返回字节|unkonwn|

##### 6.33

$0x1788,0x1789,0x178a,0x178b,0x16c8,0x16c9,0x16ca,0x16cb$

### 6.34~6.35
##### 6.34.

dst:
|列0|列1|列2|列3|
| ---| ---|-- |-- |
| m| m| m|  m|
| m|m |m |m |
| m|m | m| m|
| m|m | m| m|

src:
|列0|列1|列2|列3|
| ---| ---|-- |-- |
| m| m| h|  m|
| m|h |m |h |
| m|m | h| m|
| m|h | m| h|

##### 6.35.

dst:
|列0|列1|列2|列3|
| ---| ---|-- |-- |
| m| h| h|  h|
| m|h |h |h |
| m|h | h| h|
| m|h | h| h|

src:
|列0|列1|列2|列3|
| ---| ---|-- |-- |
| m| h| h|  h|
| m|h |h |h |
| m|h | h| h|
| m|h | h| h|

