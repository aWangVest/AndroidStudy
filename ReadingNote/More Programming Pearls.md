## 《编程珠玑》(续)

· 昨天在图书馆意外看到的，就借回来了

** [2015-08-17]\[第一章\] **

- 对特殊数据做特殊处理，某种意义上来说能够提高程序性能
· 这里举了两个例子，第一个是找素数、还有一个是在一本书中寻找出现最多25个单词
· 素数：将我们已知的2、3、5等表示为已知基础
· 单词：将英语中常见的100个单词做专门处理

```C
int root(int n) {
	return (int) sqrt((float) n);
}
int prime(int n) {
	int i, bound;
    if (n % 2 == 0) {
    	return (n == 2);
    }
	f (n % 3 == 0) {
    	return (n == 3);
    }
    f (n % 5 == 0) {
    	return (n == 5);
    }
    // 这里还可以优化：把求平方转换成乘法 //
    // for (i = 7; i * i <= n, i = i + 2) { //
    bound = root(n);
    for (i = 7; i <= bound, i = i + 2) {
    	if (n % i == 0) {
        	return 0;
        }
        return 1;
    }
}
void main() {
	int i, n;
    n = 1000;
    for (i = 2; i <= n; i++) {
    	if (prime(n)) {
        	printf("%d\n", i);
        }
    }
}
```

