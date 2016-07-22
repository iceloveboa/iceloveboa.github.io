#CSAPP

2.27

```
int uadd_ok(unsigned x, unsigned y)
{
	unsigned result = x + y;
	return result >= x;
}
```

2.30

```
int tadd_ok(int x, int y)
{
    int sum = x + y;
    int neg_over = x < 0 && y < 0 && sum >= 0;
    int pos_over = x >= 0 && y >= 0 && sum < 0;
     
    return !neg_over && !pos_over;
}
```
2.39

```
-(x<<m)
```

2.40

```
(x<<2) + (x<<1)
(x<<5) - x
(x<<1) - (x<<3)
(x<<6) - (x<<3) - x
```

2.41

```
less operator is better
```

2.42

```
return (x >> 4) + (x & 0xF) && (x >> 31);
```

2.43

```
M=31 N=8
```

2.44

```
A. -2147483648
B. 1
C. 0 49152 = 1100 0000 0000 0000
D. 1
E. -2147483648
F. 1
G. 1
```

2.47

```
BITS	E	E	2E	F	M	2E*M	V	DECIMAL
0 00 00	0	0	1	0/4	0/4	0/4	0	0.0
0 00 01	0	0	1	1/4	1/4	1/4	1/4	0.25
0 00 10	0	0	1	2/4	2/4	2/4	1/2	0.5
0 00 11	0	0	1	3/4	3/4	3/4	3/4	0.75
0 01 00	1	0	1	0/4	4/4	4/4	1	1.0
0 01 01	1	0	1	1/4	5/4	5/4	5/4	1.25
0 01 10	1	0	1	2/4	6/4	6/4	3/2	1.5
0 01 11	1	0	1	3/4	7/4	7/4	7/4	1.75
0 10 00	2	1	2	0/4	4/4	8/4	2	2.0
0 10 01	2	1	2	1/4	5/4	10/4	5/2	2.5
0 10 10	2	1	2	2/4	6/4	12/4	3	3.0
0 10 11	2	1	2	3/4	7/4	14/4	7/2	3.5
0 11 00	-	-	-	-	-	-	-	Infinity
0 11 01	-	-	-	-	-	-	-	NaN
0 11 10	-	-	-	-	-	-	-	NaN
0 11 11	-	-	-	-	-	-	-	NaN
```

2.58

```
int is_little_endian()
{
	int a = 0xFF;
	byte_pointer p = (byte_pointer) &a;
	if (*p & 0xFF)
	{
		return 1;
	}
	else{
		return 0;
	}
}
```

2.59 

```
int getxy(int x,int y)
{
	int tempx = x & 0xFF;
	int tempy = y & (~0xFF);
	return tempx+tempy;
}
```

2.64

```
int any_even_one(unsigned x)
{
	for (int i = 0; i < sizeof(unsigned)*4; ++i)
	{
		int y = x >> (i*2+1);
		y = y & 1 ;
		if (y)
		{
			return 1;
		}
	}

	return 0;
}
```

2.65

```
int even_ones(unsigned x)
{
	int result = 0;
	for (int i = 0; i < sizeof(unsigned)*8; ++i)
	{
		int y = x >> i;
		y = y & 1 ;
		if (y)
		{
			result+=1;
		}
	}

	if (!(result%2))
	{
		return 1;
	}else{
		return 0;
	}
}
```

2.71

```
int xbyte(packed_t word, int bytenum) {
    return (word << (24 - (bytenum << 3))) >> (bytenum << 3);
}
```

2.73

```
int saturating_add(int x, int y) {
    size_t bitLength = sizeof(int) << 3;
    unsigned maskMSB = 1 << (bitLength - 1);
    int z = x + y;
    int overFlow = ((x & maskMSB) == (y & maskMSB)) && ((y & maskMSB) != (z & maskMSB));
    z &= (overFlow - 1);
    return z | ((!overFlow - 1) & (maskMSB - !(x & maskMSB)));
}
```

2.76 

```
A. x + (x << 2)
B. x + (x << 3)
C. (x << 5) - (x << 1)
D. (x << 3) - (x << 6)
```

