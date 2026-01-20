# Hướng dẫn sử dụng Aider

Aider là một công cụ lập trình cặp với AI ngay trong terminal của bạn. Nó cho phép bạn yêu cầu thay đổi code, tạo file mới, hoặc sửa lỗi bằng cách trò chuyện với một mô hình ngôn ngữ lớn (LLM) như GPT-3.5/GPT-4. Aider sẽ áp dụng các thay đổi đó trực tiếp vào file của bạn.

## Cài đặt và Thiết lập

Đây là hướng dẫn cài đặt và thiết lập Aider để bắt đầu sử dụng.

### Cách cài đặt được khuyến nghị: `aider-install`

Phương pháp đơn giản và an toàn nhất là sử dụng `aider-install`. Nó sẽ tự động cài đặt Aider và các phụ thuộc vào một môi trường Python riêng, đảm bảo không ảnh hưởng đến hệ thống của bạn.

```bash
# Yêu cầu Python 3.8-3.13 đã được cài đặt
python -m pip install aider-install
aider-install
```

### Cài đặt bằng một dòng lệnh (Mac, Linux & Windows)

Các lệnh này sẽ tự động tải về và cài đặt Aider, bao gồm cả Python 3.12 nếu cần.

**Mac & Linux:**

Sử dụng `curl`:
```bash
curl -LsSf https://aider.chat/install.sh | sh
```
Hoặc `wget`:
```bash
wget -qO- https://aider.chat/install.sh | sh
```

**Windows (PowerShell):**
```powershell
powershell -ExecutionPolicy ByPass -c "irm https://aider.chat/install.ps1 | iex"
```

### Các phương pháp cài đặt khác

Nếu bạn muốn quản lý môi trường một cách thủ công hơn, bạn có thể sử dụng các công cụ sau:

**Sử dụng `uv`:**
```bash
# Cài đặt uv nếu bạn chưa có
python -m pip install uv
# Cài đặt aider bằng uv
uv tool install --force --python python3.12 --with pip aider-chat@latest
```

**Sử dụng `pipx`:**
```bash
# Cài đặt pipx nếu bạn chưa có
python -m pip install pipx
# Cài đặt aider bằng pipx
pipx install aider-chat
```

**Sử dụng `pip` trong môi trường ảo:**

Luôn sử dụng môi trường ảo để tránh xung đột thư viện.

```bash
# 1. Tạo môi trường ảo
python3 -m venv aider-env

# 2. Kích hoạt môi trường
#    Trên Mac/Linux: source aider-env/bin/activate
#    Trên Windows:   aider-env\Scripts\activate

# 3. Cài đặt Aider
python -m pip install -U --upgrade-strategy only-if-needed aider-chat
```

### Thiết lập API Key

Sau khi cài đặt, bạn cần cung cấp API key.

**Cách 1: Thiết lập biến môi trường (ví dụ cho OpenAI)**

```bash
export OPENAI_API_KEY="your-openai-api-key-here"
```

**Cách 2: Cung cấp trực tiếp khi chạy Aider (khuyến nghị)**

Cách này linh hoạt hơn khi bạn sử dụng nhiều mô hình khác nhau.

```bash
# Ví dụ với DeepSeek
aider --model deepseek --api-key deepseek=<key>

# Ví dụ với Claude 3.7 Sonnet
aider --model sonnet --api-key anthropic=<key>

# Ví dụ với OpenAI (o3-mini)
aider --model o3-mini --api-key openai=<key>
```

## Cách sử dụng

### Khởi động Aider

Để bắt đầu, bạn chỉ cần chạy lệnh `aider` trong thư mục gốc của dự án của bạn:

```bash
aider
```

Bạn cũng có thể thêm các tệp bạn muốn làm việc vào ngay khi khởi động:

```bash
aider README.md path/to/your/file.py
```

Aider sẽ đọc các tệp này và chuẩn bị sẵn sàng để bạn đưa ra yêu cầu.

### Trò chuyện và đưa ra yêu cầu

Sau khi khởi động, bạn có thể bắt đầu trò chuyện với Aider như với một người đồng nghiệp. Hãy mô tả các thay đổi bạn muốn thực hiện một cách rõ ràng.

**Ví dụ:**

> "Hãy thêm một hàm mới vào file `main.py` để tính tổng hai số."

> "Trong file `style.css`, hãy đổi màu nền của body thành màu xám nhạt."

Aider sẽ đề xuất các khối code để thay đổi. Bạn sẽ có lựa chọn để chấp nhận (`y`), từ chối (`n`), hoặc chỉnh sửa (`e`).

### Các lệnh trong Aider

Aider cung cấp một số lệnh hữu ích mà bạn có thể sử dụng ngay trong cuộc trò chuyện. Các lệnh này bắt đầu bằng dấu gạch chéo (`/`).

-   **/add `<file_path>`**: Thêm một hoặc nhiều tệp vào cuộc trò chuyện.
    *   Ví dụ: `/add src/component.js`
    *   Bạn có thể dùng glob pattern: `/add src/**/*.js`

-   **/drop `<file_path>`**: Xóa một hoặc nhiều tệp khỏi cuộc trò chuyện.
    *   Ví dụ: `/drop tests/test_old.py`

-   **/ls**: Liệt kê tất cả các tệp hiện đang có trong cuộc trò chuyện.
    *   **/ls -l**: Liệt kê các tệp cùng với thông tin về số lượng token.

-   **/diff**: Hiển thị các thay đổi đang chờ xử lý (chưa được commit) trong các tệp đã thêm vào cuộc trò chuyện.

-   **/undo**: Hoàn tác lại thay đổi gần nhất đã được chấp nhận.

-   **/commit**: Commit các thay đổi đang chờ xử lý với một thông điệp commit.
    *   Ví dụ: `/commit -m "feat: Thêm tính năng đăng nhập"`
    *   Aider sẽ yêu cầu bạn nhập thông điệp nếu bạn không cung cấp qua cờ `-m`.

-   **/run `<command>`**: Chạy một lệnh shell và đưa kết quả vào cuộc trò chuyện. Điều này rất hữu ích để chạy test hoặc linter.
    *   Ví dụ: `/run pytest tests/`
    *   Ví dụ: `/run npm run build`

-   **/git**: Hiển thị trạng thái git của các tệp trong cuộc trò chuyện. Tương tự `/diff`.

-   **/quit** hoặc **/exit**: Thoát khỏi Aider.

### Mẹo và thực hành tốt nhất

1.  **Cung cấp ngữ cảnh rõ ràng:** Thêm tất cả các tệp liên quan vào cuộc trò chuyện bằng `aider <files>` hoặc lệnh `/add`. Điều này giúp AI hiểu rõ hơn về cấu trúc dự án của bạn.
2.  **Yêu cầu cụ thể:** Thay vì nói "sửa lỗi", hãy mô tả lỗi, cung cấp thông báo lỗi từ console, và chỉ rõ file nào cần sửa.
3.  **Chia nhỏ yêu cầu:** Đối với các tác vụ lớn, hãy chia chúng thành các bước nhỏ hơn và yêu cầu Aider thực hiện từng bước một.
4.  **Sử dụng `/run` để kiểm tra:** Sau khi Aider thực hiện thay đổi, hãy dùng lệnh `/run` để chạy các bài test hoặc kiểm tra ứng dụng để đảm bảo mọi thứ vẫn hoạt động đúng.
5.  **Xem lại các thay đổi:** Luôn luôn xem lại các thay đổi mà Aider đề xuất trước khi chấp nhận. Sử dụng `/diff` để xem lại.

Aider là một công cụ mạnh mẽ giúp tăng tốc độ phát triển. Bằng cách sử dụng nó một cách hiệu quả, bạn có thể tập trung hơn vào logic nghiệp vụ thay vì các công việc lập trình lặp đi lặp lại.
