### 4.47
##### A
```C
void bubble_a(long *data,long count)
{
    long *curr;
    long *last;
    for(last=data+count-1;last>data;last--){
        for(curr=data;curr<last;curr++)
        if(*(curr+1)<*curr){
            long t = *(curr+1);
            *(curr+1)=*curr;
            *curr=t;
        }
    }
}
```
##### B
```
bubble_a:
    rrmovq	%rsi, %r10
    addq    %r10, %r10
    addq	%r10, %r10
    irmovq	$8, %r9    
    subq	%r9, %r10
    addq	%rdi, %r10
	jmp	.L2
.L3:
    irmovq	$8, %r9
	addq    %r9, %rax
.L5:
    rrmovq	%r10, %r9
	subq	%rax, %r9
	jle	.L7                 
	mrmovq	8(%rax), %rdx   // rdx = data[i+1]
	mrmovq	(%rax), %rcx    // rcx = data[i]
    rrmovq	%rdx, %r9
	subq	%rcx, %r9       // r9 = data[i+1]-data[i]
	jge	.L3
	rmmovq	%rcx, 8(%rax)
	rmmovq	%rdx, (%rax)
	jmp	.L3
.L7:
    irmovq	$8, %r9
	subq	%r9, %r10
.L2:
    rrmovq	%r10, %r8    // r8 = 存last
	subq	%rdi, %r8
	jle	.L8
	rrmovq	%rdi, %rax  // rax = 存curr
	jmp	.L5
.L8:
	ret

main:
	irmovq	$5, %rsi
	irmovq	arr, %rdi
	callq	bubble_a
	irmovq	$0, %rax
	ret

arr:
	.quad	2
	.quad	7
	.quad	5
	.quad	1
	.quad	10
```
### 4.48
```
.L5:
    rrmovq	%r10, %r9
	subq	%rax, %r9
	jle	.L7            
	mrmovq	8(%rax), %rdx   // rdx = data[i+1]
	mrmovq	(%rax), %rcx    // rcx = data[i]
    rrmovq	%rdx, %r9
	subq	%rcx, %r9       // r9 = data[i+1]-data[i]
    ######### diff here
    cmovl	%rdx, %r11
    cmovl   %rcx, %rdx
    cmovl   %r11, %rcx
    rmmovq	%rdx, 8(%rax)
	rmmovq	%rcx, (%rax)
    ######### diff end
	jmp	.L3
```
### 4.49
```
.L5:
    rrmovq	%r10, %r9
	subq	%rax, %r9
	jle	.L7            
	mrmovq	8(%rax), %rdx   // rdx = data[i+1]
	mrmovq	(%rax), %rcx    // rcx = data[i]
    rrmovq	%rdx, %r9
	subq	%rcx, %r9       // r9 = data[i+1]-data[i]
    ######### diff here
    rrmovl	%rdx, %r11      //存下来rdx的值
    xorq	%rcx, %rdx      //rdx=rdx^rcx
    cmovl	%r11, %rcx      //rcx=r11=原rdx
    xorq	%rdx, %rcx      //rcx=rdx^rcx
    xorq	%rcx, %rdx      //rdx=rcx^rdx
    rmmovq	%rdx, 8(%rax)
	rmmovq	%rcx, (%rax)
    ######### diff end
	jmp	.L3
```
