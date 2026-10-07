# 🎮 gdev-dzu-agents

**gdev-dzu-agents** là một framework hỗ trợ phát triển game với AI, được thiết kế để có thể tái sử dụng cho nhiều dự án game khác nhau.

Mục tiêu của framework không phải để AI tự động làm toàn bộ game, mà để xây dựng một **AI Game Development Team** có cấu trúc rõ ràng, trong đó mỗi Agent đảm nhận một vai trò riêng như nghiên cứu, thiết kế, kiến trúc, phát triển, review và hỗ trợ học tập.

Framework đặc biệt hướng tới mô hình:

> **Vừa học Game Development → vừa xây dựng game thật → vừa sử dụng AI như một development team.**

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

# 🧠 Triết lý chính

Framework tuân theo một số nguyên tắc nền tảng:

```text
Research before assumption.

Design before implementation.

Specification before production code.

Understanding before automation.

Review independently from implementation.

Prefer simple working systems before unnecessary abstraction.

Record WHY, not only WHAT.
```

AI được sử dụng như một **cộng sự phát triển**, không phải người sở hữu project.

Quyền quyết định cuối cùng luôn thuộc về **Human Project Owner**.

---

# 🧩 Kiến trúc Framework

Framework chia AI Game Development thành các thành phần độc lập:

```text
gdev-dzu-agents
│
├── Instructions
│
├── Agents
│
├── Skills
│
├── Workflows
│
└── Templates
```

Mỗi thành phần có trách nhiệm khác nhau.

---

# 📜 Instructions

`Instructions` định nghĩa các luật chung mà toàn bộ AI system phải tuân theo.

Nó trả lời câu hỏi:

> **AI phải làm việc theo những nguyên tắc nào?**

Ví dụ:

- Authority hierarchy.
- Quyền hạn của Agent.
- Specification compliance.
- Research integrity.
- Change control.
- Learning rules.
- Build rules.
- Security principles.

Thư mục:

```text
instructions/
```

Các instruction quan trọng có thể bao gồm:

```text
instructions/
├── CONSTITUTION.md
├── AUTHORITY.md
└── MODES.md
```

Trong đó `CONSTITUTION.md` là tập luật nền tảng cao nhất của framework.

---

# 🤖 Agents

Agent định nghĩa **vai trò** trong AI Development Team.

Nó trả lời câu hỏi:

> **Ai đang thực hiện công việc?**

Ví dụ:

```text
Game Director
Game Designer
Technical Architect
Developer
Reviewer
Learning Coach
```

Ngoài ra framework có nhóm Research Agent riêng.

```text
Game Research Analyst
Game Discovery Scout
Domain Researcher
External Design Council
```

Agent định nghĩa:

- Role.
- Responsibility.
- Authority.
- Input.
- Output.
- Skill được phép sử dụng.
- Những việc Agent không được phép làm.

Agent **không nên chứa chi tiết cách thực hiện một task** nếu logic đó có thể được tái sử dụng dưới dạng Skill.

---

# 🛠️ Skills

Skill định nghĩa **cách thực hiện một loại công việc**.

Nó trả lời câu hỏi:

> **Task này nên được thực hiện như thế nào?**

Ví dụ:

```text
Analyze Reference Game

Discover Similar Games

Design Gameplay System

Design Economy System

Design Save System

Review Implementation

Create Learning Exercise
```

Skill phải có khả năng **tái sử dụng giữa nhiều project khác nhau**.

Ví dụ:

```text
skills/game-design/design-career-system.md
```

có thể mô tả cách thiết kế một Career System nói chung.

Skill **không được chứa requirement của một game cụ thể**.

---

# 📋 Project Specification

Project Specification định nghĩa:

> **Chúng ta đang xây dựng cái gì?**

Ví dụ một game project có thể có:

```text
specs/
├── world/
├── player/
├── time/
├── career/
├── economy/
├── property/
├── relationship/
├── quest/
└── minigames/
```

Specification là **project-specific**.

Do đó:

> Project Specification **không nằm trong repository này**.

Mỗi game sẽ có repository riêng chứa specification của chính game đó.

---

# ⚠️ Skill và Specification phải được tách biệt

Đây là một trong những nguyên tắc quan trọng nhất của framework.

Ví dụ:

```text
skills/game-design/design-property-system.md
```

mô tả:

> Cách thiết kế Property System cho một game.

Trong khi:

```text
some-game/docs/specs/property/property-system.md
```

mô tả:

> Property System cụ thể của game đó hoạt động như thế nào.

Có thể hiểu đơn giản:

```text
SKILL
│
│  How should we design it?
│
▼

SPECIFICATION
│
│  What should this game contain?
│
▼

IMPLEMENTATION
```

---

# 🔬 Research System

Research được tách khỏi Game Design.

Framework dự kiến có bốn nhóm research chính.

## Game Research Analyst

Nghiên cứu chuyên sâu một game cụ thể.

Có thể phân tích:

- Genre.
- Core Loop.
- Meta Loop.
- Gameplay systems.
- Progression.
- Economy.
- Difficulty.
- Art direction.
- UX.
- Community feedback.
- Điểm mạnh.
- Điểm yếu.
- Những mechanic đáng học hỏi.

Research có thể tiếp tục drill-down vào từng system khi cần.

---

## Game Discovery Scout

Research theo chiều rộng.

Mục tiêu:

> **Tìm xem ngoài kia có những game nào đáng để chúng ta biết tới.**

Agent có thể tìm:

- Game tương tự.
- Competitor.
- Hidden gem.
- Mechanic thú vị.
- Game thuộc genre khác nhưng có system liên quan.

Agent này ưu tiên **discovery**, không phân tích quá sâu từng game.

---

## Domain Researcher

Nghiên cứu thế giới thực.

Ví dụ:

```text
Education
Jobs
Transportation
Housing
Economy
Culture
Business
Urban development
```

Mục tiêu là cung cấp dữ liệu thực tế cho Game Designer.

Domain Research không trực tiếp quyết định gameplay.

---

## External Design Council

Đóng vai trò như một hội đồng bên ngoài development team.

Nó có nhiệm vụ **challenge các ý tưởng**, thay vì cố gắng chứng minh rằng ý tưởng hiện tại là đúng.

Council có thể xem xét một vấn đề từ nhiều góc nhìn:

```text
Player Advocate

Indie Game Designer

Systems Designer

Commercial Critic

Skeptic

Creative Designer

Casual Player
```

Nếu sử dụng nhiều AI model, Council có thể thu thập nhiều quan điểm khác nhau và giữ lại những disagreement có giá trị.

---

# 🔄 Research không phải Design

Một kết quả research không tự động trở thành game requirement.

Workflow dự kiến:

```text
Research
    ↓
Finding
    ↓
Game Design Proposal
    ↓
Discussion / Review
    ↓
Human Decision
    ↓
Accepted Specification
```

Một mechanic thú vị được tìm thấy trong game khác chỉ là **reference**.

Nó chỉ trở thành một phần của project sau khi được đánh giá và chấp nhận.

---

# 🏗️ AI Development Team

Cấu trúc dự kiến:

```text
                         GAME DIRECTOR
                              │
             ┌────────────────┼────────────────┐
             │                │                │
          DESIGN           RESEARCH        ENGINEERING
             │                │                │
       Game Designer     Research Lab    Tech Architect
                                               │
                                           Developer
                                               │
                                           Reviewer

                         LEARNING
                            │
                      Learning Coach
```

Framework sẽ được phát triển dần thay vì tạo tất cả Agent ngay từ đầu.

---

# 👑 Authority

AI hỗ trợ project nhưng không sở hữu project.

Authority dự kiến:

```text
Human Project Owner
        │
        ▼
Project Vision
        │
        ▼
Game Pillars
        │
        ▼
Accepted Decisions
        │
        ▼
Accepted Specifications
        │
        ▼
Architecture
        │
        ▼
Current Task
        │
        ▼
Agent Recommendation
```

Một tầng thấp hơn không được tự ý override tầng phía trên.

Nếu phát hiện conflict:

> Agent phải báo conflict thay vì tự quyết định.

Chi tiết sẽ được định nghĩa trong:

```text
instructions/AUTHORITY.md
```

---

# 🎓 Learning Mode

Một trong những mục tiêu quan trọng của framework là hỗ trợ **học Game Development**.

Trong Learning Mode:

```text
Concept
    ↓
Explanation
    ↓
Small Exercise
    ↓
Developer Implementation
    ↓
AI Review
    ↓
Feedback
    ↓
Improvement
```

AI không nên generate toàn bộ implementation nếu điều đó làm mất đi learning opportunity.

---

# ⚡ Build Mode

Khi developer đã hiểu system hoặc cần tăng tốc development:

```text
Accepted Spec
      ↓
Architecture
      ↓
Implementation Plan
      ↓
AI / Developer Implementation
      ↓
Review
      ↓
Verification
```

AI có thể chủ động hơn trong implementation.

Tuy nhiên:

> **Implementation autonomy không đồng nghĩa với Design authority.**

AI vẫn phải tuân theo specification đã được chấp nhận.

---

# 🔍 Independent Review

Developer và Reviewer nên là hai responsibility độc lập.

Reviewer kiểm tra:

```text
Specification compliance

Correctness

Architecture

Maintainability

Engine conventions

Performance

Edge cases

Regression risks
```

Code chạy được **không đồng nghĩa với code đúng**.

---

# 📝 Decision Records

Các quyết định quan trọng nên lưu lại cả:

```text
WHAT

và

WHY
```

Ví dụ:

```text
DEC-001

Context
Decision
Reason
Alternatives
Consequences
Status
```

Điều này giúp AI và developer trong tương lai hiểu được lý do của những quyết định trước đó.

---

# 📁 Repository Structure

Cấu trúc dự kiến:

```text
gdev-dzu-agents/
│
├── README.md
├── SECURITY.md
│
├── instructions/
│   ├── CONSTITUTION.md
│   ├── AUTHORITY.md
│   └── MODES.md
│
├── agents/
│   ├── research/
│   ├── design/
│   ├── engineering/
│   ├── quality/
│   └── learning/
│
├── skills/
│   ├── research/
│   ├── game-design/
│   ├── engineering/
│   ├── development/
│   ├── quality/
│   └── learning/
│
├── workflows/
│
├── templates/
│
└── docs/
```

Cấu trúc này có thể thay đổi khi framework trưởng thành.

---

# 🔗 Sử dụng với Game Project

Framework và game project được giữ độc lập.

Ví dụ:

```text
gdev-dzu-agents
       │
       ├──────────────┐
       │              │
       ▼              ▼
    Game A          Game B
       │              │
       ▼              ▼
    Specs           Specs
    Code            Code
    Assets          Assets
```

Cách tích hợp framework với project cụ thể sẽ được xác định sau.

Các phương án có thể bao gồm:

```text
Git Submodule
Git Subtree
Selective Copy
Bootstrap Script
Agent Package
```

Không khóa framework vào một AI provider hoặc game engine cụ thể ở giai đoạn hiện tại.

---

# 🔐 Security

AI-generated code, script và command không mặc nhiên được xem là an toàn.

Không commit:

```text
API Keys
Passwords
Access Tokens
Private Keys
Credentials
Secrets
```

Agent chỉ nên được cấp quyền tối thiểu cần thiết để hoàn thành nhiệm vụ.

Xem thêm:

```text
SECURITY.md
```

---

# 🚧 Trạng thái dự án

**Early Development**

Framework hiện đang trong giai đoạn thiết kế nền tảng.

Ưu tiên hiện tại:

```text
1. Constitution
        ↓
2. Authority Model
        ↓
3. Operating Modes
        ↓
4. Agent Contracts
        ↓
5. Research Agents
        ↓
6. Design / Engineering Agents
        ↓
7. Reusable Skills
        ↓
8. Workflows
        ↓
9. Project Templates
```

Framework chưa được xem là production-ready.

---

# 🌱 Nguyên tắc phát triển

`gdev-dzu-agents` sẽ được phát triển từng bước.

Không cố gắng tạo một hệ thống AI phức tạp ngay từ đầu.

Mỗi Agent, Skill và Workflow chỉ nên được thêm vào khi trách nhiệm của nó đã đủ rõ ràng.

> **Simple first.  
> Understand it.  
> Use it.  
> Review it.  
> Then improve it.**

---

## Current Status

🚧 **v0.x — Foundation**

Đang xây dựng nền móng cho AI-assisted Game Development Framework.
