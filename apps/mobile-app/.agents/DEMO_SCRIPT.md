# Kịch Bản Trình Diễn Toàn Diện (End-to-End Master Demo)

Đây là kịch bản demo trình diễn toàn bộ sinh thái của hệ thống Antigravity Agent dành cho Mobile Developer, trải dài mọi ngóc ngách của quá trình phát triển dự án. Một kịch bản mang tính đột phá và ứng dụng AI cực mạnh.

## 🌟 Chân dung Kịch bản: Ứng dụng Chi Tiêu Bằng AI (AI Expense Tracker)
- **Idea**: Người dùng quá lười để nhập từng con số chi tiêu. 
  - **Tính năng 1 (Smart Input)**: Chỉ cần "chụp hình tờ hoá đơn" hoặc gõ tin nhắn "Ăn phở 50k", app tự trích xuất số tiền và lưu data.
  - **Tính năng 2 (Monthly View)**: Màn hình Dashboard quản lý toàn bộ chi tiêu trong tháng, kèm biểu đồ.
- **Trạng thái**: Đã có bản phác thảo Figma, sẵn sàng để code.

---

### Bước 1: Ý Tưởng & Phân Tích (Idea → Tasks)
*Ngữ cảnh: Yêu cầu cực khó vì dính tới AI Parsing và Camera. Bạn dùng AI Agent để bẻ nhỏ bài toán phức tạp.*

**Lệnh thực hiện:**
```bash
/analyze-spec Xây dựng app chi tiêu rảnh tay. Yêu cầu:
1. Màn hình thêm chi tiêu: Có ô chat Text hoặc Upload/Chụp ảnh hoá đơn. Tự bóc tách chuỗi "cafe 40k" thành { category: 'food', amount: 40000 }.
2. Màn hình Monthly View: Xem biểu đồ tổng chi tiêu trong tháng.
- Có link Figma: https://figma.com/design/xxxxx?node-id=SMART_EXPENSE
```

**Phản ứng của AI:**
- Lên ngay chiến lược 4 Task:
  1. Cài native module `expo-image-picker` để lấy mâm ảnh/camera.
  2. Dựng `SmartParserService` gọi API lên GPT/Claude bóc tách tiền tệ.
  3. Dựng Màn hình `SmartInputScreen`.
  4. Dựng Component biểu đồ & Màn hình `MonthlyViewScreen` với Zustand để lưu cache.

---

### Bước 2: Setup Phức Tạp (Cài Native Module)
*Ngữ cảnh: Làm việc với Camera/Thư viện ảnh rất hay lỗi permission và config. Nhờ AI lo giùm.*

**Lệnh thực hiện:**
```bash
/add-native-module Thêm expo-image-picker và cấu hình quyền camera/thư viện ảnh.
```

**Phản ứng của AI:**
- Tự động chạy lệnh cài package.
- Tự động chui vào file `app.json` khai báo `NSCameraUsageDescription` và `NSPhotoLibraryUsageDescription` để app không bị Apple/Google từ chối khi submit store.

---

### Bước 3: Lắp ráp Logic AI (Init Source & Do Task)
*Ngữ cảnh: Dựng cục logic cốt lõi nhất — bóc tách hình ảnh/văn bản thành cục Data.*

**Lệnh thực hiện:**
```bash
/do-task Dựng SmartParserService gom logic bóc tách văn bản. Dùng Zustand để lưu Record chi tiêu cục bộ (Offline first) khi bóc tách xong.
```

**Phản ứng của AI:**
- Tuân thủ `rules/state-management.md`: Dùng Zustand persist với MMKV (Tốc độ đọc ghi tính bằng mili-giây).
- Xây Service gửi string/base64 ảnh lên AI model để bóc tách thành format JSON `{ title: string, amount: number }`.

---

### Bước 4: Tạo Screen & Đọc Figma (MCP)
*Ngữ cảnh: Cần tạo giao diện Màn Hình Thống Kê Tháng (Monthly View) y hệt thiết kế.*

**Lệnh thực hiện:**
```bash
/new-screen MonthlyViewScreen Đọc form màn hình này từ Figma https://figma.com/design/xxxxx?node-id=MONTHLY_VIEW và móc nối data từ Zustand ra hiển thị nhé.
```

**Phản ứng của AI:**
- **Figma MCP kích hoạt**: Tự động bóc tách mã màu (màu đỏ của chi, màu xanh của thu). Tính toán kích thước padding chính xác xuống từng pixel.
- Tự dựng `FlatList` để nhồi list 50 giao dịch trong tháng vừa móc từ Zustand đảm bảo lướt mượt 60fps (chuẩn `rules/performance.md`).

---

### Bước 5: Bắt Bug Thực Tế (Fix Bug)
*Ngữ cảnh: Chạy app thử trên Device thật dính chưởng. Chụp hình hoá đơn xong app văng cái rầm vì hình dung lượng 10MB quá nặng để parse.*

**Lệnh thực hiện:**
```bash
/mobile-fix-issue Chụp xong app bị crash (văng) do ảnh nặng, hao bộ nhớ. Fix giùm tôi.
```

**Phản ứng của AI:**
- AI phát hiện vấn đề Memory Leak / Payload quá lớn.
- Kích hoạt quy trình Fix: AI tự động chỉnh lại logic của `expo-image-picker` thêm thuộc tính `quality: 0.5` hoặc `base64: true` với mức độ nén ảnh thông minh trước khi ném vào Service, giải quyết dứt điểm rớt RAM.

---

### Bước 6: Kỷ luật Thép — Ép viết Test (Write Unit Test)
*Ngữ cảnh: Mọi module chạy rất ngon. Thay vì test lặp đi lặp lại bằng tay, ta để AI tự test logic Parse tiền tệ.*

**Luật ngầm hoạt động:** 
AI chủ động rà mã khi đang code và báo: Logic bóc tách "Cafe 50k" rất dễ rủi ro. Yêu cầu có Unit Test.

**Lệnh thực hiện:**
```bash
/write-tests Generate Unit test cho file SmartParserService.ts, check case đầu vào "ăn bún bò 35k".
```

**Phản ứng của AI:**
- Dùng Jest tạo môi trường giả lập.
- Ném chuỗi "Ăn bún bò 35000 VNĐ" vào hàm xử lý, `expect(amount).toBe(35000)`. 
- Pass 100% test case để đảm bảo logic chạy hoàn hảo ở mọi string.

---

### Bước 7: Done! Push Code (Commit Push)
*Ngữ cảnh: Báo cáo kết quả với team.*

**Lệnh thực hiện:**
```bash
/commit-push Hoàn thiện màn hình Nhập liệu AI và Thống kê Tháng.
```

**Phản ứng của AI:**
- AI tự check eslint và pass mọi tests.
- Trả ra một commit cực kỳ gọn gàng theo format chuẩn: `feat(expense): implement ai receipt parser and monthly dashboard`.
- Execute `git add`, `git commit`, `git push` tự động kết thúc màn trình diễn.

---
🎉 **TỔNG KẾT**: Một kịch bản demo "killer" vì nó không chỉ phô diễn quy trình gõ code chuẩn chỉ của Agent, mà phần feature (bóc tiền từ tin nhắn/hình chụp) là một Use-case vô cùng thực tế và thời thượng!
