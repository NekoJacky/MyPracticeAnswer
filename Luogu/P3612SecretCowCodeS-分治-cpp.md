# [USACO17JAN]Secret Cow Code S

## 题面翻译

奶牛正在试验秘密代码，并设计了一种方法来创建一个无限长的字符串作为其代码的一部分使用。

给定一个字符串，让后面的字符旋转一次（每一次正确的旋转，最后一个字符都会成为新的第一个字符）。也就是说，给定一个初始字符串，之后的每一步都会增加当前字符串的长度。

给定初始字符串和索引，请帮助奶牛计算无限字符串中位置 $N$ 的字符。

第一行输入一个字符串。该字符串包含最多 $30$ 个大写字母，数据保证 $N \leq 10^{18}$ 。

第二行输入 $N$。请注意，数据可能很大，放进一个标准的 $32$ 位整数可能不够，所以你可能要使用一个 $64$ 位的整数类型（例如，在 C/C++ 中是 `long long`）。

请输出从初始字符串生成的无限字符串中的位置的字符。第一个字符是 $N=1$.。

感谢@y\_z\_h 的翻译

## 题目描述

The cows are experimenting with secret codes, and have devised a method for creating an infinite-length string to be used as part of one of their codes.

Given a string $s$, let $F(s)$ be $s$ followed by $s$ "rotated" one character to the right (in a right rotation, the last character of $s$ rotates around and becomes the new first character). Given an initial string $s$, the cows build their infinite-length code string by repeatedly applying $F$; each step therefore doubles the length of the current string.


Given the initial string and an index $N$, please help the cows compute the character at the $N$th position within the infinite code string.

## 输入格式

The input consists of a single line containing a string followed by $N$. The string consists of at most 30 uppercase characters, and $N \leq 10^{18}$.

Note that $N$ may be too large to fit into a standard 32-bit integer, so you may want to use a 64-bit integer type (e.g., a "long long" in C/C++).

## 输出格式

Please output the $N$th character of the infinite code built from the initial string. The first character is $N=1$.

## 样例 #1

### 样例输入 #1

```
COW 8
```

### 样例输出 #1

```
C
```

## 提示

In this example, the initial string COW expands as follows:


COW -> COWWCO -> COWWCOOCOWWC

12345678

```C++
#include <iostream>
#include <string>

using namespace std;

int main()
{
    int x;
    string s1, s2, s = "", anss = "";
    char a;
    int len1, lens;
    long long len;
    long long i, n;
    cin >> s1;
    cin >> n;
    len = s1.length();
    while(len < n)
    {
        i = len;
        while(i < n)
            i *= 2;
        if(n == (i/2)+1)
            n = i / 2;
        else
            n = n - i/2 - 1;
    }
    cout << s1[n-1] << endl;
    return 0;
}
```
