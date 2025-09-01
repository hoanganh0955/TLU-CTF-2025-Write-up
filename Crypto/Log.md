# Log 
<img width="473" height="391" alt="image" src="https://github.com/user-attachments/assets/e5475c4d-1613-4769-82c1-c4cdf9bfbebc" />

Nhìn thoạt qua thì trông bài toán này rất đơn giản, nhưng mà khi mình bắt tay vào giải thì nó lại không đơn giản tí nào =)))

> Đây là một bài toán Log Tuyến Tính (`Mình ngu tuyến tính`)

Giải thích sơ qua code của chall:
Đầu tiên biến p sẽ là một số prime ngẫu nhiên trong khoảng 1024 bit và g được lấy ngẫu nhiên từ [0->p²]
Biến k ở đây sẽ là flag được encrypt từ bytes sang dạng long và đảm bảo k < p

<img width="311" height="124" alt="image" src="https://github.com/user-attachments/assets/8406ac11-149d-49c6-94a9-63463a4ec7a6" />

Tiếp đó chall sẽ có công thức là g^k (mod p²)

Sau khoảng 2 tiếng ngồi chày cối với bài thì mình đã phải nhờ đến ~~nole~~ Chat GPT 😮‍💨:
Đầu tiên ta phải tính:
g0 = g^(p−1) mod p²
c0 = c^(p−1) mod p²
A  = ((g0−1)/p) mod p
B  = ((c0−1)/p) mod p
k  = B * inv(A, p) mod p

Đây là script mà chat GPT đã đưa ra:

```
from Crypto.Util.number import inverse, long_to_bytes

# g, p, c lấy từ output(2).txt
g = int("1675814333...578921")  # rút gọn khi dán
p = int("1298036606...38538789")
c = int("8435018025...6683218")

mod = p*p
g0 = pow(g, p-1, mod)
c0 = pow(c, p-1, mod)

A = ((g0 - 1) // p) % p
B = ((c0 - 1) // p) % p

k = (B * inverse(A, p)) % p      # vì k < p nên đây là k thật
flag = long_to_bytes(k).decode()
print(flag)  # TLUCTF2025{5a84f541a7c8f8d51c8f85e3a0a3f2fc}

```

> TLUCTF2025{5a84f541a7c8f8d51c8f85e3a0a3f2fc}

Đối với mình thì bài toán này cũng khá là khoai khó có thể giải được trong vẻn vẹn 24 tiếng :))

