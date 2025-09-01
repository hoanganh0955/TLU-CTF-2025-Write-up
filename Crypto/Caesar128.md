# Caesar128
<img width="478" height="453" alt="image" src="https://github.com/user-attachments/assets/e2ee127c-657d-42fa-b76f-dbb75b246d61" />

Chall này cũng không có gì khó, thay vì có không gian khóa là 26 thì nâng lên 128
Nhìn sơ qua file của chall thì có thể thấy đây là ciphertext được viết ở dạng hex, đây là python script mà mình đã dùng để giải mã nó

```
cipher_hex = "19 11 1A 08 19 0B 77 75 77 7A 40 2A 76 28 27 27 75 28 78 7D 7C 7E 26 2B 7D 78 79 7C 77 79 7B 2B 76 77 28 7A 7A 7E 26 7D 7B 27 7A 42"
cipher = bytes.fromhex(cipher_hex.replace(" ", ""))

for key in range(128):
    plain = ''.join(chr((c - key) % 128) for c in cipher)
    if "TLUCTF2025{" in plain:
        print(f"Key {key}: {plain}")
        break
```

Cách hoạt động của script này cũng khá là đơn giản, bruteforce cho đến khi tìm được bản rõ của flag
Vì chúng ta đã biết format của flag là `TLUCTF2025{` nên việc xác nhận cũng khá là dễ dàng

> TLUCTF2025{e1cbb0c3879af8347246f12c559a86b5}
