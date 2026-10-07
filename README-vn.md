# 🎮 gdev-dzu-agents

**gdev-dzu-agents** là một framework hỗ trợ phát triển game với AI, được thiết kế để có thể tái sử dụng cho nhiều dự án game khác nhau.

Mục tiêu của framework không phải để AI tự động làm toàn bộ game, mà để xây dựng một **AI Game Development Team** có cấu trúc rõ ràng, trong đó mỗi Agent đảm nhận một vai trò riêng biệt.

Framework đặc biệt hướng tới mô hình:

> **Vừa học Game Development → vừa xây dựng game thật → vừa sử dụng AI như một development team.**

---

# 🧠 Kiến trúc tri thức dự án

Framework giữ nguyên tính tổng quát cho nhiều game khác nhau. Với mỗi dự án game downstream, nên tách bạch theo cách sau:

```text
project/
├── docs/
├── specs/
├── releases/
└── src/
```

Ý nghĩa từng phần:

```text
specs/ = hồ sơ lịch sử phát triển, rationale, evidence, analysis, design, traceability

docs/  = mô tả hiện trạng đã được tổng hợp của dự án đang phát hành

src/   = mã nguồn thực thi
```

Nguyên tắc quan trọng:

```text
docs/ != lịch sử phát triển

docs/ = truth hiện tại của dự án
```

Điều này giúp tránh việc trộn giữa "những gì đã từng làm" với "những gì dự án đang là".

---

# 🎯 Mục tiêu

`gdev-dzu-agents` được xây dựng nhằm hỗ trợ:

- Nghiên cứu chuyên sâu các game tham khảo.
- Tìm kiếm các game tương tự và các hidden gem.
- Nghiên cứu domain thực tế phục vụ thiết kế game.
- Phân tích gameplay, mechanic và game system.
- Thiết kế gameplay system có cấu trúc.
- Chuyển Game Design thành Technical Architecture.
- Hỗ trợ developer học Game Development thông qua project thực tế.
- Implement feature dựa trên specification đã được chấp nhận.
- Review độc lập giữa thiết kế, architecture và implementation.
- Lưu lại các quyết định quan trọng và lý do phía sau chúng.
- Giảm hallucination và việc AI tự ý mở rộng scope.
- Cho phép tái sử dụng cùng một workflow cho nhiều game project.

---

# 🧩 Kiến trúc Framework Repository

Repository này chứa framework, không chứa cấu trúc tri thức của một game cụ thể.
Các thành phần chính của framework là:

```text
gdev-dzu-agents/
│
├── instructions/
├── agents/
├── skills/
├── workflows/
├── templates/
└── examples/
```

Các thư mục `docs/`, `specs/`, `releases/`, và `src/` thuộc về game project
downstream ở mức khái niệm. Chúng không phải là cấu trúc bắt buộc của framework
repository này.

---

# 📜 Instructions

`Instructions` định nghĩa các luật chung mà toàn bộ AI system phải tuân theo.

Các instruction quan trọng có thể bao gồm:

```text
instructions/
├── CONSTITUTION.md
├── AUTHORITY.md
├── PROJECT_KNOWLEDGE.md
└── ...
```

---

# 🔐 Security

AI-generated code, script và command không mặc nhiên được xem là an toàn.

Xem thêm:

```text
SECURITY.md
```

---

# 🚧 Trạng thái dự án

**Early Development**

Framework hiện đang trong giai đoạn thiết kế nền tảng.

---

# 🌱 Nguyên tắc phát triển

`gdev-dzu-agents` sẽ được phát triển từng bước.

> **Simple first.  
> Understand it.  
> Use it.  
> Review it.  
> Then improve it.**
