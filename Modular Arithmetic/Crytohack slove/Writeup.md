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

![image](https://github.com/user-attachments/assets/8fc33706-0665-491a-bf84-20fcce0c3a20)
đề bài cho 1 tập hợp gồm 3 số nguyên tỏng đó chỉ có 1 số duy nhất là thặng dư bậc 2, bài yêu cầu tìm ra các số nguyên căn bậc 2 của thặng dư và số bé nhất chính là flag, code py:
```py
def Quadratic_Residues(p, a):
    residues = []
    for x in range(1, p):
        residue = (x * x) % p
        if residue == a:
            residues.append(x)
    return residues
p=29
ints=[14,6,11]
for i in ints:
    print(Quadratic_Residues(p, i))
```

![image](https://github.com/user-attachments/assets/f58fd1cd-c3ae-4604-a3c0-98f17c15a509)
vậy flag là 8 


# Chinese Remainder Theorem

![image](https://github.com/user-attachments/assets/bf79a732-38d4-4b0d-9c55-1811eafb325b)
đề bài cho 1 tập hợp:
```
x ≡ 2 mod 5
x ≡ 3 mod 11
x ≡ 5 mod 17
```
và yêu cầu tìm a trong 'x ≡ a mod 935'

vì 935 = 5 * 11 * 17 => ta sử dụng định lý số dư trung quốc để giải quyết bài 

có m1 = 5, m2 = 11, m3 = 17 và M = 935 từ đây ta có thể tính được a theo công thức:
![image](https://github.com/user-attachments/assets/c9a87da0-802c-4570-8ca6-8e3008ba4c5f)
code py:
```
def chinese_remainder_theorem(a, n, N):
    result = 0
    for i in range(len(n)):
        ai=a[i]
        ni=n[i]
        mi= N // ni
        Mi = Modular_Inverting(mi, ni)
        result += ai * mi * Mi
    return result % N
N=935
a=[2, 3, 5]
n=[5, 11, 17]
print(chinese_remainder_theorem(a, n, N))
```
![image](https://github.com/user-attachments/assets/f60237b7-efe7-4b88-95d3-03795d942f81)
vậy flag là 872

# Adrien's Signs
![image](https://github.com/user-attachments/assets/b4d12267-5a0c-4793-815e-e66e39c5f7ca)

source: https://github.com/ceram1c/Crypto_learn/blob/993e8db29f5bee867e15a0774c8b22429cb9625e/Modular%20Arithmetic/Crytohack%20slove/source/source_734d7e14251f950935f83d228f8694ab.py
```py
from random import randint

a = 288260533169915
p = 1007621497415251

FLAG = b'crypto{????????????????????}'


def encrypt_flag(flag):
    ciphertext = []
    plaintext = ''.join([bin(i)[2:].zfill(8) for i in flag])
    for b in plaintext:
        e = randint(1, p)
        n = pow(a, e, p)
        if b == '1':
            ciphertext.append(n)
        else:
            n = -n % p
            ciphertext.append(n)
    return ciphertext


print(encrypt_flag(FLAG))
```
- output: https://github.com/ceram1c/Crypto_learn/blob/993e8db29f5bee867e15a0774c8b22429cb9625e/Modular%20Arithmetic/Crytohack%20slove/source/output_80fc6398d2fd9f272186d0af510323f9.txt

- dựa theo source code đề bài đã encrypt flag theo từng bước:
    - chuyển đổi từ ký tự 1 về dạng bin 8 số sau đó lưu vào plaintext
    - tạo 1 vòng lặp đếm từ bit 1 của plaintext rồi thực hiện:
        - lấy random 1 số e từ 1 -> p sau đó tính n = a^e % p
        - nếu bit hiện tại của vòng lặp =1 thì nhập n vào chuỗi ciphertext
        - nếu = 0 thì n = -n % p rồi nhập vào chuỗi ciphertext
- file output của bài là file flag sau khi encrypt, vậy ta cần decode ngược lại với bằng cách biến đổi từng số output về bit 1 hay 0
-  p = 1007621497415251 ta có thể thấy p % 4 = 3 => x^((p-1)/2) % p = 1
-  vì nếu bit = 0 thì n = -n % p nên ta có thể dùng công thức này để viết lại đoạn bin của flag lúc đầu rôid decode
- code py:
```
a = 288260533169915
p = 1007621497415251

bit= output

flag=""
bits=""
for i in bit:
    if pow(i, (p-1)//2, p) == 1:
        bits += '1'
    else:
        bits += '0'
for i in range(0, len(bits), 8):
    byte = bits[i:i+8]
    flag += chr(int(byte, 2))
print(flag)
```
![image](https://github.com/user-attachments/assets/5f886fcd-45b9-406a-8f31-b596f70f8727)

'Flag: crypto{p4tterns_1n_re5idu3s}' 

# Modular Binomials

![image](https://github.com/user-attachments/assets/c4443ca9-8b6f-4a02-9f38-c2ce40291c93)

- data: https://github.com/ceram1c/Crypto_learn/blob/06c6ab8ee311ab8a8ef97e53e8aa5be94e823796/Modular%20Arithmetic/Crytohack%20slove/source/data_04a0fe134cf31a6c941377aad75db81c.txt

- đề bài cho 3 phương trình và 5 số trong Data gồm N, c1, c2, e1, e2 

- c1^e2​​ = (2​⋅p + 3​⋅q)^(e1​⋅e2)​ mod N
- 2^(−e1​⋅e2) ​​⋅ c1^e2​​ = 2^(−e1​⋅e2) ​​⋅ (2​⋅p)^(e1​⋅e2) ​+ 2^(−e1​⋅e2)​​ ⋅ (3​⋅q)^(e1​⋅e2) ​mod N
- 2^(−e1​⋅e2​)​ ⋅ c1^e2 ​​= p^(e1​⋅e2) ​+ 2^(−e1​⋅e2​) ​⋅ (3​⋅q)^(e1​⋅e2) ​mod N
- là tương tự với phương trình tiếp theo sau đó trừ 2 phương trình cho nhau ta được
- 5^(−e2​⋅e1​) ​⋅ c2^e1​​ − 2^(−e1​⋅e2)​​ ⋅ c1^e2​​ = p^(e2​⋅e1) ​+ 5^(−e2​⋅e1) ​​⋅ (7​⋅q)^(e2​⋅e1) ​− p^(e1​⋅e2) ​− 2^(−e1​⋅e2)​​ ⋅ (3​⋅q)^(e1​⋅e2) ​mod N

- 5^(−e2​⋅e1​) ​⋅ c2^e1​​ − 2^(−e1​⋅e2)​​ ⋅ c1^e2​​ = 5^(−e2​⋅e1) ​​⋅ (7​⋅q)^(e2​⋅e1)) ​− 2^(−e1​⋅e2)​​ ⋅ (3​⋅q)^(e1​⋅e2) ​mod N
- ==> q = GCD((pow(5,(-e2 * e1),N) * pow(c2, e1, N) - pow(2, (-e1 * e2), N) * pow(c1, e2, N)), N)
code py:
```py
from Modular import GCD

N = 14905562257842714057932724129575002825405393502650869767115942606408600343380327866258982402447992564988466588305174271674657844352454543958847568190372446723549627752274442789184236490768272313187410077124234699854724907039770193680822495470532218905083459730998003622926152590597710213127952141056029516116785229504645179830037937222022291571738973603920664929150436463632305664687903244972880062028301085749434688159905768052041207513149370212313943117665914802379158613359049957688563885391972151218676545972118494969247440489763431359679770422939441710783575668679693678435669541781490217731619224470152467768073
e1 = 12886657667389660800780796462970504910193928992888518978200029826975978624718627799215564700096007849924866627154987365059524315097631111242449314835868137
e2 = 12110586673991788415780355139635579057920926864887110308343229256046868242179445444897790171351302575188607117081580121488253540215781625598048021161675697
c1 = 14010729418703228234352465883041270611113735889838753433295478495763409056136734155612156934673988344882629541204985909650433819205298939877837314145082403528055884752079219150739849992921393509593620449489882380176216648401057401569934043087087362272303101549800941212057354903559653373299153430753882035233354304783275982332995766778499425529570008008029401325668301144188970480975565215953953985078281395545902102245755862663621187438677596628109967066418993851632543137353041712721919291521767262678140115188735994447949166616101182806820741928292882642234238450207472914232596747755261325098225968268926580993051
c2 = 14386997138637978860748278986945098648507142864584111124202580365103793165811666987664851210230009375267398957979494066880296418013345006977654742303441030008490816239306394492168516278328851513359596253775965916326353050138738183351643338294802012193721879700283088378587949921991198231956871429805847767716137817313612304833733918657887480468724409753522369325138502059408241232155633806496752350562284794715321835226991147547651155287812485862794935695241612676255374480132722940682140395725089329445356434489384831036205387293760789976615210310436732813848937666608611803196199865435145094486231635966885932646519


q= GCD((pow(5,(-e2 * e1),N) * pow(c2, e1, N) - pow(2, (-e1 * e2), N) * pow(c1, e2, N)), N)
p= GCD((pow(7,(-e2 * e1),N) * pow(c2, e1, N) - pow(3, (-e1 * e2), N) * pow(c1, e2, N)), N)

print(p)
print(q)
```
![image](https://github.com/user-attachments/assets/dc61c174-8ae7-43c4-a733-05d77efc35ec)

'Flag: cryto{q, p}'











