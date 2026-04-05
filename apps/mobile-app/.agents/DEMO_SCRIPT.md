# Kịch Bản Trình Diễn Toàn Diện (End-to-End Master Demo)

Đây là kịch bản demo trình diễn toàn bộ sinh thái của hệ thống Antigravity Agent dành cho Mobile Developer, trải dài mọi ngóc ngách của quá trình phát triển dự án.

## 🌟 Chân dung Kịch bản: Ứng dụng Quản Lý Chi Tiêu (Expense Tracker)
- **Idea**: Xây dựng màn hình Dashboard Thống Kê Chi Tiêu (Hiển thị số dư hiện tại, danh sách giao dịch thu/chi gần nhất, và nút Thêm giao dịch).
- **Trạng thái**: Đã có file thiết kế Figma.

---

### Bước 1: Ý Tưởng & Phân Tích (Idea → Tasks)
*Ngữ cảnh: Bạn vừa nhận yêu cầu xây dựng màn hình Dashboard. Thay vì code ngay, bạn nhờ AI phân rã yêu cầu thành các block nhỏ.*

**Lệnh thực hiện:**
```bash
/analyze-spec Xây dựng màn hình Dashboard Quản lý chi tiêu. Yêu cầu:
- Hiển thị Số dư hiện tại ở trên cùng.
- Hiển thị danh sách Giao dịch (Transaction) gần đây, khoản thu màu xanh dương, khoản chi màu đỏ.
- Nút FAB (Floating Action Button) tròn ở góc dưới bên phải để Thêm giao dịch.
- Có link Figma: https://figma.com/design/xxxxx?node-id=DASHBOARD
```

**Phản ứng của AI:**
- Bóc tách thành 4 Task nhỏ để dễ trị: 
  1. Tạo `ExpenseService` (gọi API lấy data).
  2. Tạo `useExpenseStore` (Dùng Zustand để gom state offline cache).
  3. Tạo Component `TransactionCard` (Từ giao diện Figma).
  4. Lắp ráp màn hình chính `ExpenseDashboard`.

---

### Bước 2: Setup & Tích Hợp Figma (Figma MCP)
*Ngữ cảnh: Đi thẳng vào code phần giao diện từng dòng giao dịch. Bạn lười đo CSS.*

**Lệnh thực hiện:**
```bash
/new-component TransactionCard Tham chiếu thiết kế từ node Figma này: https://figma.com/design/xxxxx?node-id=TRANSACTION_CARD
```

**Phản ứng của AI:**
- Kết nối thông qua **Figma MCP**, đọc mã màu (Thu: `#22C55E` -> `COLORS.success`, Chi: `#EF4444` -> `COLORS.danger`), đọc spacing.
- Tự động sinh ra file `TransactionCard.tsx` pixel-perfect bằng React Native.
- Phân tách ra 2 trạng thái `income` và `expense` nhờ việc định nghĩa Props thông minh.

---

### Bước 3: Lắp ráp Logic Toàn Tuyến (Init Source & Do Task)
*Ngữ cảnh: Cần làm API để lấy danh sách chi tiêu và tạo State Management chuẩn.*

**Lệnh thực hiện:**
```bash
/do-task Thực hiện Task 1 và Task 2: Dựng ExpenseService dùng Axios và useExpenseStore dùng Zustand có tích hợp bộ nhớ offline MMKV.
```

**Phản ứng của AI:**
- Bám sát `rules/state-management.md` & `rules/offline-caching.md`: Sinh ra file store của Zustand với `persist` middleware trỏ vào MMKV Storage (giúp cho người dùng vẫn xem được các khoản chi tiêu khi mất mạng).
- Tuân thủ `rules/api-integration.md`: Tạo `ExpenseService.ts` bắt lỗi Axios mượt mà.

---

### Bước 4: Tạo Screen (Ráp mọi thứ lại)
*Ngữ cảnh: Component và Logic đã có, giờ tạo Màn Hình tổng hiển thị danh sách thu chi.*

**Lệnh thực hiện:**
```bash
/new-screen ExpenseDashboard Ráp TransactionCard và bộ store Zustand vừa tạo vào màn hình này nhé.
```

**Phản ứng của AI:**
- Bám sát `rules/error-handling.md`: Sinh ra màn `ExpenseDashboard.tsx` với đủ 4 trạng thái bắt buộc: `Loading` (Hiệu ứng chớp nháy Skeleton thay vì icon xoay loard), `Empty` (Chưa có nợ nần/thu nhập gì), `Error`, và hiển thị `Data`.
- Dùng FlatList tối ưu thay vì `.map()` array để lướt mượt mà báo cáo 1000 dòng chi tiêu (Theo rule `performance.md`).

---

### Bước 5: Bắt Bug Thực Tế (Fix Bug)
*Ngữ cảnh: Chạy thử trên iPhone có tai thỏ/đảo động, nút tròn bự (Thêm chi tiêu) nằm dưới cùng màn hình bị dính sát vào thanh quẹt mỏng (home indicator) dưới đáy màn hình!*

**Lệnh thực hiện:**
```bash
/mobile-fix-issue Nút FAB (nút tròn) bị che dính lẹm vào phần đáy iOS (home indicator). Fix giùm tôi.
```

**Phản ứng của AI:**
- Nhớ tới Rule `rules/accessibility.md` về Safe Area.
- Phát hiện root cause do gắn `bottom: 16` cứng ngắc.
- Tự động sửa lại UI import `useSafeAreaInsets` từ `react-native-safe-area-context` và đổi CSS thành `bottom: insets.bottom + 16` để nút nổi lên cực mượt cho cả dòng máy thường lẫn máy Pro Max!

---

### Bước 6: Kỷ luật Thép — Ép viết Test (Write Unit Test)
*Ngữ cảnh: Code xong xuôi, bạn định commit nhưng tính trốn Test.*

**Luật ngầm hoạt động:** 
AI chủ động rà code khi gọi `/commit-push` và cảnh báo: "Khoan! Bạn vừa viết mới file `useExpenseStore` phân tích các phép cộng trừ Số Dư nhưng chưa hề có file Unit test. Vui lòng chạy lệnh Test!".

**Lệnh thực hiện:**
```bash
/write-tests Hãy generate Unit test coverage cho file useExpenseStore.ts
```

**Phản ứng của AI:**
- Gọi Jest, giả lập các thao tác người dùng (Thêm 50k ăn phở, Trừ 10k gửi xe).
- Kiểm chứng kết quả "Số dư" xem có cộng trừ đúng không.
- Bảo đảm **bao phủ 80% coverage** theo chuẩn `testing.md`.

---

### Bước 7: Done! Push Code (Commit Push)
*Ngữ cảnh: Mọi module App chi tiêu đã hoàn thiện.*

**Lệnh thực hiện:**
```bash
/commit-push Hoàn thiện màn hình Dashboard Quản lý chi tiêu
```

**Phản ứng của AI:**
- Mở quy trình tự xét duyệt: Chạy `eslint`, chạy `jest` nội bộ.
- Pass 100%! AI format commit sang chuẩn Conventional và ép ngắn dưới 60 ký tự: `feat(expense): implement dashboard screen and offline store`.
- Thực thi: `git add .`, `git commit`, và `git push`.

---
🎉 **HOÀN TẤT VÒNG ĐỜI**: Một kịch bản code tính năng từ Z-A, ứng dụng hoàn hảo quyền năng giám sát kỷ luật lập trình của Agent System.
