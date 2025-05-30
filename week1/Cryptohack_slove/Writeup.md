# Base64

![image](https://github.com/user-attachments/assets/942ec7d9-ddf7-47c2-a74e-7005bc43a65c)

bài này cho ta 1 đoạn mã hex và yêu cầu chuyển nó về dạng byte rồi encoded dưới dạng base64.
sử dụng python để code 1 đoạn encoded base64:

  ```py
  text = '72bca9b68fc16ac7beeb8f849dca1d8a783e8acf9679bf9269f7bf'
  base64 = "ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz0123456789+/"
  encoded=""


  a= bytes.fromhex(text)

  #chuyển từng giá trị hex thành số nhị phân dạng 8 bit
  bit_string = ''.join(f"{byte:08b}" for byte in a)

  # thêm số 0 đêm khi thừa bit
  while len(bit_string) %6 != 0:
      bit_string+='0'
    
  # chia chuỗi nhị phân ban đầu thành từng nhóm 6bit sau đó đối chiếu qua bảng mã base64
  for i in range(0, len(bit_string), 6):
      bit=bit_string[i:i+6]
      index = int(bit, 2)
      encoded+=base64[index]
    
  print(encoded)
  ```
![image](https://github.com/user-attachments/assets/ef33416f-d71d-4604-b838-74c927374751)


# XOR Starter

![image](https://github.com/user-attachments/assets/d7b05653-8fe5-4f2d-b5a9-d1daa84feb99)

yêu cầu của bài là muốn chúng ta XOR 1 chuỗi "label" với 13, sau đó chuyển lại về dạng string để nộp.
Code python giải bài:

```py
string = 'label'

for c in string:
    c = chr(ord(c)^13)
    print(c+"", end="")
```

![image](https://github.com/user-attachments/assets/1d0b121b-f5c0-4626-9814-429c331079d5)


# XOR Properties

![image](https://github.com/user-attachments/assets/1d6756d2-04da-45a3-b5c5-cde9c1128574)





Code python giải bài:
```py
# tạo 1 func để duyệt qua và xor từng bit của 2 dãydãy
def xor_byte(a, b):
    return bytes(x^y for x, y in zip(a, b))

KEY1 = 'a6c8b6733c9b22de7bc0253266a3867df55acde8635e19c73313'
KEY2xorKEY1 = '37dcb292030faa90d07eec17e3b1c6d8daf94c35d4c9191a5e1e'
KEY2xorKEY3 = 'c1545756687e7573db23aa1c3452a098b71a7fbf0fddddde5fc1'
FLAGxorKEY1xorKEY3xorKEY2 = '04ee9855208a2cd59091d04767ae47963170d1660df7f56f5faf'

# chuyển về dạng hex
KEY1 = bytes.fromhex(KEY1)
KEY2xorKEY1 = bytes.fromhex(KEY2xorKEY1)
KEY2xorKEY3 = bytes.fromhex(KEY2xorKEY3)
FLAGxorKEY1xorKEY3xorKEY2 = bytes.fromhex(FLAGxorKEY1xorKEY3xorKEY2)

# thực hiện XOR để tìm KEY2, KEY3 sau đó là tới FLAG
KEY2 = xor_byte(KEY2xorKEY1, KEY1)
KEY3 = xor_byte(KEY2xorKEY3, KEY2)
FLAG = xor_byte(xor_byte(xor_byte(FLAGxorKEY1xorKEY3xorKEY2, KEY1), KEY2), KEY3)
print(FLAG.decode('utf-8'))
```



![image](https://github.com/user-attachments/assets/133e35ba-588f-4e29-9b58-c817cfa41db1)

