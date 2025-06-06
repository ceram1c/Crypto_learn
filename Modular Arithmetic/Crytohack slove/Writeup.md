# Greatest Common Divisor

![image](https://github.com/user-attachments/assets/71e229a5-6df3-4163-817e-2be43e29698f)
bài này yêu cầu ta tìm ước chung lớn nhất của 2 số bài cho. Code py:
```py
def GCD(a, b):
    while b != 0:
        a, b = b, a % b
    return a
a=66528
b=52920
print(GCD(a, b))
```
![image](https://github.com/user-attachments/assets/3146c096-eeda-4629-b4a8-118fcdac4b65)

# Extended GCD

![image](https://github.com/user-attachments/assets/b3145dee-852a-4c45-8724-fae4ba4512a6)
bài muốn ta tìm 2 số u và v sao cho thỏa mãn 'u*q + v*p = GCD(q, p)' với q và p bài cho, sao đó lấy số bé hơn để nộp flag. Code py:
```py
def Extended_GCD(a, b):
    if a == 0:
        return 0, 1
    else:
        x, y = Extended_GCD(b % a, a)
    return x, y - (b // a) * x
p=26513
q=32321
print(Extended_GCD(p, q))
```
![image](https://github.com/user-attachments/assets/1b4e4883-1a3a-4599-8b3f-be775bea8e83)
Vậy flag là -8404

# Modular Arithmetic 1

![image](https://github.com/user-attachments/assets/51e6d36c-e9d6-4478-ae61-fae25bf5e720)
đề bài yêu cầu ta tìm x, y theo phương trình trong đề bài, rồi tìm số bé hơn là flag 

x = 11%6 = 5
y = 8146798528947 % 17 = 4

![image](https://github.com/user-attachments/assets/185b66fd-f61d-47d6-bc6e-ff1d940821c1)
vậy flag là 4

# Modular Arithmetic 2

![image](https://github.com/user-attachments/assets/fff10e8f-3163-4019-a05b-c6dbca009fb1)
bài yêu cầu ta tính phương trình '273246787654^65536 % 65537', với p = 65537 là số nguyên tố,
dựa theo định lý littel fermat: khi 1 số p là số nguyên tố mà a không chia hết cho p thì a^(p-1) % p = 1 => p-1 = 65537 - 1 = 65536 <=> 273246787654^(p-1) % p = 1

![image](https://github.com/user-attachments/assets/f2dbd3fd-3e7b-469b-bf15-97c292454429)


vậy flag là 1

# Modular Inverting

![image](https://github.com/user-attachments/assets/ba9568f7-0347-4b7f-b081-c23b2ae2a5f6)

đề bài yêu cầu tính số nghịch đảo mudulo của 3 là d so với modulo 13, code py:

```py
def Modular_Inverting(a, modulo):
    x = pow(a, modulo - 2, modulo)
    return x
a = 3
m = 13
print(Modular_Inverting(a, m))
```
![image](https://github.com/user-attachments/assets/44d4848d-3257-425f-9f63-b02ec785c0f8)
vậy flag là 9


# Quadratic Residues









