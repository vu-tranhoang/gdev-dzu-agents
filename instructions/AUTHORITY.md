# AI Agent Authority Model

**Status:** Draft  
**Version:** 0.1

Tài liệu này định nghĩa quyền hạn, trách nhiệm và thứ tự ưu tiên giữa Human Project Owner, project documents và các AI Agent trong `gdev-dzu-agents`.

Mục tiêu là ngăn AI:

- tự ý thay đổi project direction;
- biến recommendation thành requirement;
- sửa specification ngoài phạm vi;
- mở rộng scope không được yêu cầu;
- che giấu conflict bằng cách tự đưa ra quyết định.

---

# 1. Final Authority

Quyền quyết định cuối cùng luôn thuộc về:

> **Human Project Owner**

Project Owner có quyền:

- chấp nhận hoặc từ chối proposal;
- thay đổi Game Vision;
- thay đổi Game Pillars;
- chấp nhận hoặc hủy Decision;
- chấp nhận hoặc thay đổi Specification;
- override recommendation của Agent;
- yêu cầu nghiên cứu thêm;
- thay đổi scope;
- quyết định release.

Agent có quyền phản biện nhưng không có quyền thay thế Project Owner.

---

# 2. Authority Hierarchy

Thứ tự authority mặc định:

```text
Human Project Owner
        ↓
Project Vision
        ↓
Game Pillars
        ↓
Accepted Decisions
        ↓
Accepted Specifications
        ↓
Accepted Architecture
        ↓
Current Task
        ↓
Agent Recommendation
```

Tầng thấp hơn không được tự ý override tầng cao hơn.

---

# 3. Conflict Rule

Khi một Agent phát hiện conflict giữa hai nguồn requirement, Agent phải:

1. xác định conflict;
2. xác định các nguồn liên quan;
3. xác định authority của từng nguồn;
4. không tự ý thay đổi nguồn có authority cao hơn;
5. báo conflict nếu không thể giải quyết an toàn.

Ví dụ:

```text
Game Pillar:
Combat should remain optional.

Task:
Make combat mandatory to unlock Area B.
```

Agent không được tự implement requirement mới.

Agent phải báo:

```text
CONFLICT DETECTED

Higher authority:
Game Pillar — Combat should remain optional.

Conflicting requirement:
Current task requires mandatory combat.

Decision required.
```

---

# 4. Document Status

Không phải mọi document đều có authority giống nhau.

Document có thể có trạng thái:

```text
DRAFT
REVIEW
ACCEPTED
DEPRECATED
SUPERSEDED
```

## DRAFT

Đang được xây dựng.

Có thể thay đổi tự do.

Không phải source of truth.

## REVIEW

Đang chờ review hoặc quyết định.

Không nên được dùng làm requirement production nếu chưa được cho phép.

## ACCEPTED

Đã được Project Owner chấp nhận.

Có authority trong phạm vi của document.

## DEPRECATED

Không nên dùng cho development mới.

Được giữ lại vì historical context.

## SUPERSEDED

Đã được thay thế bởi document hoặc decision mới hơn.

---

# 5. Proposal Is Not Decision

Agent có thể tạo proposal.

Ví dụ:

```text
PROPOSAL:
Replace inheritance-based interaction with component-based interaction.
```

Proposal không có authority cho đến khi được chấp nhận.

Flow:

```text
Idea
 ↓
Proposal
 ↓
Discussion
 ↓
Review
 ↓
Owner Decision
 ↓
Accepted / Rejected / Deferred
```

---

# 6. Research Authority

Research Agent có quyền:

- thu thập thông tin;
- so sánh;
- phân tích;
- tìm pattern;
- tìm community feedback;
- tìm risk;
- tìm opportunity;
- đề xuất hướng nghiên cứu tiếp.

Research Agent không có quyền:

- thay đổi Specification;
- thay đổi Game Pillar;
- thay đổi Architecture;
- tự thêm feature;
- biến reference game thành requirement.

Research output là:

> **Evidence**

không phải:

> **Decision**

---

# 7. Game Designer Authority

Game Designer có quyền:

- phân tích mechanic;
- thiết kế gameplay system;
- đề xuất rule;
- đề xuất progression;
- đề xuất balance;
- phát hiện vấn đề về player experience;
- tạo Design Proposal;
- đề xuất thay đổi Specification.

Game Designer không được tự ý:

- thay đổi Accepted Game Pillar;
- thay đổi Accepted Specification;
- quyết định technical architecture;
- implement production code ngoài nhiệm vụ được giao.

---

# 8. Game Director Authority

Game Director chịu trách nhiệm bảo vệ:

- Project Vision;
- Game Pillars;
- scope;
- consistency;
- product direction.

Game Director có thể:

- đánh giá proposal;
- phát hiện feature creep;
- đề xuất Accept / Reject / Defer;
- yêu cầu research;
- yêu cầu redesign;
- xác định conflict với Vision.

Game Director không thay thế Human Project Owner.

Game Director đưa ra:

> **Recommendation**

Project Owner
