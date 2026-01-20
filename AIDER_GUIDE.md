# Hướng dẫn sử dụng Aider

Aider là một công cụ lập trình cặp với AI ngay trong terminal của bạn. Nó cho phép bạn yêu cầu thay đổi code, tạo file mới, hoặc sửa lỗi bằng cách trò chuyện với một mô hình ngôn ngữ lớn (LLM) như GPT-3.5/GPT-4. Aider sẽ áp dụng các thay đổi đó trực tiếp vào file của bạn.

## Cài đặt

Để cài đặt Aider, bạn có thể sử dụng pip:

```bash
pip install aider-chat
```

Bạn cũng cần phải có một API key từ OpenAI và thiết lập nó trong môi trường của bạn:

```bash
export OPENAI_API_KEY="your-api-key-here"
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
