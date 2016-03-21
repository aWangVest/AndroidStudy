
### Shellcode Injection

- [Shellcode Injection，需翻墙](https://dhavalkapil.com/blogs/Shellcode-Injection/)
- [Shellcode Injection Comment](https://news.ycombinator.com/item?id=10796542)

> Almost every program nowadays is compiled with W^X (--no_execstack)

- W^X是什么？
	+ 多种操作系统，包括OpenBSD、Windows、Linux和OS X，在内核强制减少权限，使得进程地址空间中的任何部分都不能同时既可写又可执行。这一策略被称为W xor X，或更为简洁的W ^ X，并通过使用多种CPU的不执行(No eXecute，NX)位来支持这种功能
	+ 数据执行保护（Data Execution Prevention，DEP）是W^X策略在微软Visual Studio中的实现
	+ [《C和C++安全编码（原书第2版）》](http://book.2cto.com/201312/38524.html)
- [《Hacking: The Art of Exploitation - Wikipedia, the free encyclopedia》](https://en.wikipedia.org/wiki/Hacking:_The_Art_of_Exploitation)
- [Buffer Overflow Exploit - Dhaval Kapil](https://dhavalkapil.com/blogs/Buffer-Overflow-Exploit/)
- [Pentester Academy Home Page: Learn Pentesting Online](http://www.pentesteracademy.com/)
	+ a SecurityTube.net initiative
	+ 收费的，$99 for first month，$ 39 /month thereafter
- [What is SUID and how to set SUID in Linux/Unix? - The Linux Juggernaut](http://www.linuxnix.com/suid-set-suid-linuxunix/)

`gcc vuln.c -o vuln -fno-stack-protector -z execstack`

- -fno-stack-protector 表示禁用栈保护技术
- -z execstack 关闭ld链接器堆栈不可执行机制

`echo "0" | [sudo] dd of=/proc/sys/kernel/randomize_va_space` Disable ASLR
`echo "2" | [sudo] dd of=/proc/sys/kernel/randomize_va_space` Enable ASLR

#### 单词

- demonstrate
	+ 示范，演示
- familiar
	+ 熟悉的，熟知的
- ASLR(Address space layout randomization)
	+ 一种针对缓冲区溢出的安全保护技术
- plenty
	+ 大量，丰富，充足
- scenario
	+ 剧本，情节，场景
