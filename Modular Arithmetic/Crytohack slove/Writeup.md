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

