费马小定理
----
- 条件
    - p是素数
    - a与p互质（a不是p的倍数）
- 结论：$a^{p-1}\equiv 1 (\mod p)$ 
- 进一步推广
    - $a^{p-1}\equiv 1 (\mod p)\Longrightarrow a*a^{p-2}=1(\mod p)$ ,p为质数. 显然$a^{p-2}$ 就是a的模p的乘法逆元

逆元
----
> 取模只能作用与整数上面，例如 $\frac{a}{b} \times 1e10 \times \frac{b}{a} mod n$ 中间可能会越界, 所以需要在中间步骤进行取模，这个时候就需要将除法变成乘法来取模（因为小数不能取模)， 来保证结果不变（不意味这中间式子等价 比如$\frac{1}{b} \mod m \ne b^{m-2} \mod m$ )
- 解决问题：求$\frac{a}{b} \times 1e100 \times \frac{b}{a} \mod m$, 希望防止中间越界，所以需要分别取模在乘
    - 然而分数不能取模，所以需要找一个x 使得$\frac{1}{b}= x \mod m\Longrightarrow bx = 1 \mod m$
- 如果m为质数且b,m互质，根据费马小定理得到$\frac{a}{b} \mod m =  ab^{m-2} \mod m$ 推导如下
    - 利用快速幂 时间复杂度在O(log m)
    $$
    由：b^{m-1} = 1 mod m \\
    可以得到：b\times b^{m-2}=1 mod m \\
    $$
    - 利用扩展欧几里得
$$
由：bx=1 \mod m \\
可以得到：bx + my =1\\
解出 x即为b \mod m的逆元
$$

- 例子

    $\frac{5}{2} \times 8 \mod 3 = (((5 \mod 3) \times 2 \mod 3) \times 8 \mod 3) = 2$

    $\frac{5}{2} \times 8 \mod 3 = 20 \mod 3 =2$
素数筛
----
- 埃式筛：一个素数的整数倍是合数
- 欧拉筛：解决埃式筛重复筛选情况， 通过最小质因数筛选
    - 将目前所有质数保存到vector中，每次晒除质数(从小到大)的i倍，其中如果i能够被某个质数整除则结束此次筛选(后面的质数乘i后不是最小质因数）
```c++
void eulerSieve(int n)    // 查找记录2-n的素数
{
    for (int i = 2; i <= n; i++)
    {
        if (p[i] == false)  // 如果未被筛过，则为素数
            prime[pNum++] = i;
        for (j = 0; j < pNum; j++)
        {
            if (i * prime[j] > n)      // 当要标记的合数超出范围时跳出
                break;
            p[i * prime[j]] = true;     // 将已经记录的素数的倍数进行标记
            if (i % prime[j] == 0)      //关键步骤
                break;
        }
    }
}
```
欧拉函数
----
- $\phi(x)=x\prod\limits_{i=1}^n (1-\frac{1}{p_i})$ $p_i$ 为x的质因数, $\phi(x)$ 为x内有多少与x互质
	- $\phi(10)=10(1-\frac{1}{2})(1-\frac{1}{5})=4$ , 及1，3，7，9
- 性质：
	1. $\phi(1)=1$
	2. $\phi(0)=0$
	3. $\phi(n)=n-1$， n为素数
    4. $\phi(kp)=\phi(k)\phi(p)$, k,p 互质
    5. $\phi(ab)=\phi(a)b$ a为b的倍数; $\phi(8)=\phi(4)2=\phi(2)4=4$
	6. $\phi(p^k)=p^{k-1}(p-1)$ p为素数
- 作用： 
    - 通过性质4，5结合素数筛，以$O(\sqrt n)$ 的时间复杂度求出1-n所有数的互质个数
```c++
void Euler(int n){
	 phi[1]=1;//初始化 
	 for(int i=2;i<=n;i++)
	 {
	 	  if(!is_prime[i]) //如果是素数 
		   {
	 	  	 	p[++cnt]=i;
	 	  	 	phi[i]=i-1;//性质1 
	 	   }
	 	  	 	for(int j=1;j<=cnt&&p[j]*i<=n;j++) //筛合数 
				{
	 	  	 		 is_prime[p[j]*i]=1;
	 	  	 		 if(i%p[j]==0){  // 因为p[j]是质数，如果不是倍数关系就是互质关系
	 	  	 		 	   phi[p[j]*i]=phi[i]*p[j];//性质5
	 	  	 		 	   break;
						 }
					 else phi[p[j]*i]=phi[p[j]]*phi[i];//性质4
				} 
	 }
}
```
欧拉定理：
----
$a^{\phi(n)}\equiv 1(\mod n)$ , n与a互质
- 如果n是质数那么$\phi(n)=n-1$ ，既$a^{n-1} = 1 \mod n$. 费马小定理,所以费马小定理是欧拉定理的特殊情况
- 证明. $ax_1*ax_2*...*ax_{\phi(n)} \equiv x_1*x_2*...x_{\phi(n)} \mod n\Longrightarrow a^{\phi(n)}\equiv 1 \mod n$,  所以证明第一个式子相等即可.
    - 证明余数$ax_i \mod n$与n互质： a与n互质，x与n互质，a*x 必然与n互质，并且模n后余数也互质（可以用gcd证明）
    - 证明$ax_i$取余后两两不相等：假设相等既$ax_i=ax_j \mod n \Longrightarrow a(x_i-x_j) \mod n=0$；然而a与n互质，$x_i -x_j<n$， 所以上式子不可能成立. 
    - 余数既不相等而且与n互质，并且是n以内最大的互质个数，那么只能相等了

欧拉降幂
----
- 注意经过欧拉降幂后时间复杂度仅与欧拉函数有关, 与b无关
$$ a^b= \begin{cases}
a^{b\%\phi(p)} &gcd(a,p)=1 \\
a^b &gcd(a,p)\neq 1,b<\phi(p)\\
a^{b\% \phi(p)+\phi(p)} &gcd (a,p) \neq1, b>\phi(p)\\
\end{cases}$$

1. 证： $a^b=a^{b\%\phi(n)+\frac{b}{\phi(n)}\phi(n)}=a^{b\%\phi(n)}(a^{\phi(n)})^\frac{b}{\phi(n)}=a^{b\%\phi(n)}$

欧几里得算法
----
- 目的：求a,b的公约数
- 推导：求(a,b)的公约数即等于求kx,,(a-kb,b)与(a,b) 公约数不变, 又(a,b)=(kx1,kx2) 所以最后会出现（x,k)的情况，在来一步就变成了(k,0) (所以说求出来的值肯定是最大的约数，比如8，4 会直接变成4,0)
    - 互质的两个数相加减还是互质（反证法）假设有公约数 那么a+b ,b 也会有公约数
- 时间复杂度：O(log(n))
扩展欧几里得算法
----
- 目的：已知a,b求ax+by=1中的整数x,y
- 推导：由欧几里得算法得到ax+by=gcd(a,b)=gcd(b,a%b)=bx'+(a%b)y', 即ax+by=bx'+(a%b)y'=bx'+ay'-bky'=b(x'-ky')+ay', 因为是恒等式所以即x=y', y=x'-ky'; 而k=a/b 向下取整; 而a,b 随着迭代会变成gcd(a,b),1, 这个时候就能解出x'=1，y'=0;
    - 如果是ax+by=h h为任意数，那么只需要变化一下就行了
