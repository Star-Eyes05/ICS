#### 4.51

| 阶段| iaddq V, rB |
| --- | --- |
| 取指 | icode:ifun $\leftarrow$ M[PC] $\\$ rA,rB $\leftarrow$ M[PC+1] $\\$ valC $\leftarrow$ M[PC+2]$\\$valP $\leftarrow$ PC + 10|
| 译码| valB $\leftarrow$ R[rB]|
| 执行| valE $\leftarrow$ valB + valC $\\$ set CC|
| 访存| |
| 写回| R[rB] $\leftarrow$ valE|
| 更新PC| PC $\leftarrow$ valP|

#### 4.57(A)

| 条件| 触发条件  |
| --- | ----|
| 加载/使用冒险| E_icode$\in${IMRMOVQ,IPOPQ} && (E_destM == d_srcB $\| \|$ E_destM == d_srcA && ! D_icode $\in$ {IPUSHQ,IRMMOVQ})|

#### 6.23
$$
\begin{align*}
    T_{avg}&=T_{avg seek}+T_{avg rotate}+T_{avg read}\\
    &=4ms+\frac{1}{2}\times\frac{1}{15000}\times 60000ms+\frac{1}{800}\times\frac{1}{15000}\times 60000ms\\
    &=6.005ms
\end{align*}
$$

#### 6.24
$T_{transfer=}T_{avgseek}+T_{avg rotate}=6ms$
扇区数$=2\times1024\times1024\div 512=4096$
A.
块是连续的，只需移动一次读写头，转4圈即可读完
$T_{best}=4\times 4ms+6ms=22ms$

B.
块是随机的，每次读取都要移动一次
$T_{worst}=4000\times 6ms+16ms=24s$