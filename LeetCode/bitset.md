## 191. Number of 1 Bits My Submissions Question

Write a function that takes an unsigned integer and returns the number of ’1' bits it has (also known as the Hamming weight).

For example, the 32-bit integer ’11' has binary representation 00000000000000000000000000001011, so the function should return 3.

###solution
```C++
    int hammingWeight(uint32_t n) {
        bitset<32> hehe(n);
        return hehe.count();
    }
```
lesson:
```C++
bitset<bits> name(s/u);
bitset<32> name(12); 即12的二进制位模式
bitset<32> name("1100"):注意读位顺序是相反的:0011
```