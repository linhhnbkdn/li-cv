# Agentic Design Patterns — Overview

## 21 Chapters — Bức tranh toàn cảnh

---

### Part 1 — Atomic Patterns (Ch.1-7)
*Các building block cơ bản nhất*

| Ch | Pattern | Một câu |
|---|---|---|
| 1 | **Prompt Chaining** | Tách task dài thành chuỗi prompt nhỏ |
| 2 | **Routing** | LLM chọn đường đi tiếp theo |
| 3 | **Parallelization** | Chạy nhiều task song song |
| 4 | **Reflection** | Producer + Critic loop để cải thiện output |
| 5 | **Tool Use** | LLM gọi function/API bên ngoài |
| 6 | **Planning** | Tạo plan toàn bộ trước khi execute |
| 7 | **Multi-Agent** | Nhiều agent chuyên biệt cùng làm việc |

---

### Part 2 — Memory & Context (Ch.8-11)
*Agent nhớ và tự cải thiện*

| Ch | Pattern | Một câu |
|---|---|---|
| 8 | **Memory Management** | Short-term (context) + Long-term (DB) |
| 9 | **Learning & Adaptation** | Agent tự cải thiện theo thời gian |
| 10 | **MCP** | Chuẩn kết nối LLM với tools |
| 11 | **Goal Setting & Monitoring** | Định nghĩa "done" và check điều kiện dừng |

---

### Part 3 — Reliability (Ch.12-14)
*Agent đáng tin cậy trong thực tế*

| Ch | Pattern | Một câu |
|---|---|---|
| 12 | **Exception Handling** | Detect → Handle → Recover khi lỗi |
| 13 | **Human-in-the-Loop** | Human vào cuộc khi cần judgment |
| 14 | **RAG** | Long-term memory qua vector DB |

---

### Part 4 — Advanced (Ch.15-21)
*Hệ thống phức tạp, production-grade*

| Ch | Pattern | Một câu |
|---|---|---|
| 15 | **A2A** | Chuẩn giao tiếp giữa agent với agent |
| 16 | **Resource Optimization** | Dùng model rẻ/đắt tùy độ phức tạp |
| 17 | **Reasoning Techniques** | CoT, ToT, ReAct — prompt strategy |
| 18 | **Guardrails** | Lớp bảo vệ an toàn cho agent |
| 19 | **Evaluation & Monitoring** | Đo performance liên tục sau deploy |
| 20 | **Prioritization** | Làm task nào trước khi có nhiều task |
| 21 | **Exploration & Discovery** | Agent chủ động tìm ra cái chưa biết |

---

### Sơ đồ tổng quát

```
Input
  ↓
[Routing Ch.2] → chọn agent/flow
  ↓
[Planning Ch.6] → tạo plan
  ↓
[Execute - loop]
  ├── Tool Use Ch.5
  ├── Parallelization Ch.3
  ├── Memory Ch.8 + RAG Ch.14
  ├── Reflection Ch.4
  └── Goal Monitor Ch.11 → done? → stop
  ↓
[Guardrails Ch.18] → safe?
  ↓
Output
```

Bao quanh tất cả: **Exception Handling Ch.12**, **HITL Ch.13**, **Evaluation Ch.19**, **Multi-Agent Ch.7**, **A2A Ch.15**

---

### Standard Agent Flow trong MCP (Ch.10)

MCP là **lớp transport chuẩn hóa** giữa LLM và tools — không phải flow, mà là protocol cho phép bước ACT và OBSERVE hoạt động.

```
GOAL / MISSION
  ↓
1. SCAN      → MCP: list_tools(), list_resources()   ← agent biết có gì
  ↓
2. PLAN      → LLM tạo plan, chọn tool cho từng bước (Ch.6 + Ch.17 ReAct/CoT)
  ↓
3. ACT       → MCP: call_tool(name, args)             ← vòng lặp chính
             → MCP: read_resource(uri)
             → MCP: get_prompt(name)
  ↓
4. OBSERVE   → Tool trả result qua MCP response, agent update context
  ↓
5. REFLECT   → Goal đạt chưa? (Ch.11)
             → Chưa → quay lại PLAN
             → Rồi  → stop, trả output
```

**3 MCP primitives trong flow:**

| Primitive | Vai trò |
|---|---|
| `Tools` | Agent *làm* việc gì đó (write file, call API) |
| `Resources` | Agent *đọc* data (file, DB, URL) |
| `Prompts` | Agent *dùng* template có sẵn |

**Mapping với sách:**

| Step | Chapter |
|---|---|
| Get Mission | Ch.11 Goal Setting |
| Scan Scene | Ch.10 MCP list_tools/resources |
| Think It Through | Ch.6 Planning + Ch.17 ReAct/CoT |
| Take Action | Ch.5 Tool Use qua MCP call_tool |
| Learn Better | Ch.4 Reflection + Ch.9 Adaptation |

---

### Nguyên tắc cốt lõi

> Agent làm gì là do mình thiết kế — LLM nào, tools gì, loop ntn, prompt ra sao, dừng khi nào, guardrails gì.
> Cả 21 chapter là bộ công cụ để thiết kế đúng.
