# Slides 1 - Numbers

## Natural Numbers (Counting Numbers)

Natural numbers are a part of the number system, including all the positive numbers from `1` to `positive infinity`.

```
1, 2, 3, 4, 5, 6, ...
```

## Whole Numbers

Whole Numbers include `0` as well as all `Natural Numbers`.

```
0, 1, 2, 3, 4, 5, 6, ...
```

## Integers

Integers include the numbers from `negative infinity` to `-1` as well as all `Whole Numbers`.

```
..., -4, -3, -2, -1, 0, 1, 2, 3, 4, ...
```

## Rational Numbers

A number that can be made by dividing two `Integers`. Can be expressed as a fraction.

```
2/3, 2/3, 3/3, 4/3, 5/3, ...
```

```
1/2, 1/3, 1/4, 1/5, 1/6, ...
```

They can often be simplified:

```
4/10 = 2/5
```

Or made more complex:

```
1/2 = 100/200
```

Decimal numbers are Rational Numbers:

```
0.5 = 5/10 = 1/2
0.1234 = 1234/10000
```

Integers are Ration Numbers: 

```
10 = 10/1
```

## Real Numbers

Real Numbers include `Rational Numbers` as well as `Irrational Numbers`

### Irrational Numbers

Irrational Numbers are numbers which can be approximated using nested intervals, but can not be expressed as rational numbers.

```
π (pi) ≈ 3.14159...
e (euler's number) ≈ 2.71828...
√2 ≈ 1.414213...
```

#### Approximation

Example for √2:

The result `x` for `x = √2` must be as such, that `x² = 2`

- 1² = 1, `<2`, so the result must be larger: `1 < x`
- 2² = 4, `>2`, so the result must be less: `1 < x < 2`
- 1.4² = 1.96, `<2`, so the result must be larger: `1.4 < x < 2`
- 1.5² = 2.25, `>2`, so the result must be less: `1.4 < x < 1.5`
- 1.41² = 1.9881, `<2`, so the result must be larger: `1.41 < x < 1.5`
- 1.42² = 2.0164, `>2`, so the result must be less: `1.41 < x < 1.42`

## Relevance in Programming

Now, let's take a look at how this can be relevant for our job as programmers. Very commonly, we use 4 Bytes to store numeric values. Let's Remember:

```
1 byte = 8 bits
4 bytes = 32 bits
```

Each bit can store two values.

One bit can store two values:

```
0/1
```

Two bits can store four values:

```
00/01/10/11
```

And three bits can store eight values:

```
000/001/010/011
100/101/110/111
```

Each new bits allows us two store twice as many different values. If 3 bits allow us to store 8 values, then the fourth bit allows us to store those 8 3-bit values with the new bit being `0` and the same 8 3-bit values with the new bit being `1`:

```
Old Values:
0000/0001/0010/0011
0100/0101/0110/0111
New Values
1000/1001/1010/1011
1100/1101/1110/1111
```

Therefore, we know, that `n` bits can store `2^n` (2 to the power of n) different values.

Conclusion:

```
4 bytes = 32 bits
32 bits = 4_294_967_296 different values
```

### Storing Natural Numbers

Storing natural numbers usually has no relevancy in Programming and is ignored in this example. But using 32 bits, we would be able to store the numbers:

```
1...4_294_967_296
1...(2^n)
```

### Storing Whole Numbers

If we store, whole numbers, we need to store the number 0 somehow. This takes one value away from our 4_294_967_296 different combinations, therefore:

```
0...4_294_967_295
0...(2^n)-1
```

C# Type: `uint` (unsigned integer)

### Storing Integers

When we store Integers, we use a very smart system called two-complement's notation. TLDR: Half the available numbers are used to express negative numbers: `4_294_967_296 / 2 = 2_147_483_648`

And the other half is used to express positive numbers including zero, therefore we have one less positive number than negative numbers:

```
-2_147_483_648...2_147_483_647
-(2^(n-1))...(2^n)-1
```

C# Type: `int` (integer)

### Storing rational numbers: Fixed-Point

When storing rational numbers, we have two options: We could just say that the point comes at a fixed point of the number, e.g. in the middle:

```
0000000000000000.0000000000000000 = 0
0000000000000010.0000000000000000 = 1*2
0000000000000001.0000000000000000 = 1
0000000000000000.1000000000000000 = 1/2
0000000000000000.0100000000000000 = 1/4
```

This is quite inefficient, though, as it would allow for a maximum number of 65_536 and a maximum precision of 1/65_536=0.000015

C# Type: Does not exist, needs to be implemented manually.

### Storing rational numbers: Floating-Point

Or, we could use some of the bits to say "Move the decimal point n digits to the left or the right". This concept is called floating point numbers and has the amazing effect of being able to store numbers between:

```
1.175494351E-38...3.402823466E+38
```

That's both numbers with 38 digits!

However, accuracy changes dramatically the larger the absolute of the number gets (because more digits are needed to express the number before the point, leaving less for after):

```cs
Console.WriteLine(100.11111f.ToString("G70"));
Console.WriteLine(1_000.1111f.ToString("G70"));
Console.WriteLine(10_000.11111f.ToString("G70"));
Console.WriteLine(100_000.11111f.ToString("G70"));
Console.WriteLine(1_000_000.11111f.ToString("G70"));
Console.WriteLine(10_000_000.11111f.ToString("G70"));
```

Output:
```
100.11110687255859375
1000.111083984375
10000.111328125
100000.109375
1000000.125
10000000
```

```cs
float f1 = 2000.58f;
float f2 = 2000.0f;
Console.WriteLine(f1 - f2);
```

Output:
```
0.57995605
```

```cs
Console.WriteLine(10_001_000f-10_000_000f);
Console.WriteLine(1_000_001_000f-1_000_000_000f);
Console.WriteLine(100_000_001_000f-100_000_000_000f);
```

Output:
```
1000
1024
0
```

Unreliable when checking equality:
```c++
float a = 0.1f;
float b = 0.3f;

float c = 1f - a; // 0.9f
float d = 3 * b; // 0.9f

if(c != d){
   printf("Not the same??");
}
```

Therefore:

```c++
if(abs(c-d) >= 0.00001f){
   printf("It won't think that it's not the same this time.");
}
```

C# Type: `float` (floating-point number)


### Storing irrational numbers

Computers can only store rational numbers. Irrational numbers require an endless amount of Memory and don't exist in practical Programming.

In C#, we can find such definitions in the `MathF` class:

```cs
namespace System 
{
    public static class MathF
    {
        public const float E = 2.71828183f;

        public const float PI = 3.14159265f;

        public const float Tau = 6.283185307f;
        // ...
    }
}
```

