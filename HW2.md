#### 3.58
```C++
void decode2(long x,long y,long z)
{
    y-=z;
    x*=y;
    long ret = y;
    ret<<=63;
    ret>>=63;
    ret = ret^x;
    return ret;
}
```