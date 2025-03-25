### 🔐 **Tóm tắt cách tạo và sử dụng SSH với GitHub**  
SSH **không chỉ dùng cho một repo**, mà có thể dùng cho **tất cả repo trên tài khoản GitHub** nếu bạn đã thêm SSH key vào tài khoản.

---

### 🚀 **1. Cách tạo SSH key**  
#### 📌 **Bước 1: Kiểm tra xem bạn đã có SSH key chưa**  
Mở terminal và chạy:
```bash
ls ~/.ssh
```
Nếu thấy file `id_rsa` và `id_rsa.pub` thì bạn đã có SSH key.

#### 📌 **Bước 2: Tạo SSH key mới (nếu chưa có)**  
Chạy lệnh:
```bash
ssh-keygen -t rsa -b 4096 -C "email@gmail.com"
```
- Thay `"email@gmail.com"` bằng email GitHub của bạn.  
- Nhấn **Enter** liên tục để chấp nhận đường dẫn mặc định (`~/.ssh/id_rsa`).
- 🎯 Cách nhớ dễ dàng

Bạn có thể nhớ theo mẫu:
📌 SSH + Type (rsa) + Bits (4096) + Comment (email)
→ "SSH-TBC": SSh - Type - Bits - Comment

✅ Hoặc nhớ câu này:
💡 "SSH tạo key RSA 4096-bit, gán email để nhận diện."

#### 📌 **Bước 3: Thêm SSH key vào ssh-agent**  
Chạy lần lượt:
```bash
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_rsa
```

---

### 🌍 **2. Thêm SSH key vào GitHub**  
#### 📌 **Bước 4: Copy SSH key**
Chạy lệnh:
```bash
cat ~/.ssh/id_rsa.pub
```
Lệnh này **hiển thị nội dung file** `id_rsa.pub` (chính là SSH key cần thêm vào GitHub).

**Hoặc** bạn có thể copy thủ công bằng:
```bash
xclip -sel clip < ~/.ssh/id_rsa.pub  # Dành cho Linux
pbcopy < ~/.ssh/id_rsa.pub  # Dành cho macOS
```

#### 📌 **Bước 5: Thêm vào GitHub**
- Vào **GitHub** → **Settings** → **SSH and GPG keys**  
- Bấm **New SSH Key**  
- Dán nội dung `id_rsa.pub` vào → **Save**

---

### ✅ **3. Kiểm tra kết nối SSH**  
Chạy lệnh sau để kiểm tra:
```bash
ssh -T git@github.com
```
Nếu thành công, bạn sẽ thấy:
```
Hi quzkhanh! You've successfully authenticated, but GitHub does not provide shell access.
```

---

### 🔄 **4. Sử dụng SSH với Git**  
#### 📌 **Bước 6: Đổi remote từ HTTPS sang SSH**  
```bash
git remote set-url origin git@github.com:quzkhanh/TaskManagerApplication.git
```
#### 📌 **Bước 7: Push code lên GitHub**
```bash
git push -u origin main
```

---

### 📌 **Tóm lại**
- SSH **hoạt động với tất cả repo trong tài khoản GitHub**, không chỉ một repo.
- **`cat`** dùng để hiển thị nội dung file, ví dụ: `cat ~/.ssh/id_rsa.pub`.
- **SSH giúp push/pull GitHub mà không cần nhập mật khẩu** mỗi lần.

🚀 **Bây giờ bạn có thể dùng Git dễ dàng hơn với SSH!**
