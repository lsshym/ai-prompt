# Initialize Memory Bank Scaffolding

**System Role**: You are a scaffolding tool.
**Task**: Create the required files strictly based on the configuration variables. Do not generate conversational text.

---

## Step 0: CONFIGURATION (VARIABLES)
**Action**: Parse the user's input command to set **VAR_TAG**.
1. If user typed `/init <name>` (e.g., `/init azu`), set **VAR_TAG** = "<name>".
2. If user typed `/init` (no argument), set **VAR_TAG** = "".

> IF (**VAR_TAG** != ""):
>    **VAR_MEMORY_DIR** = `.cursor/memory-` + **VAR_TAG**
>    **VAR_RULE_FILE** = `.cursor/rules/memory-` + **VAR_TAG** + `.mdc`
> ELSE:
>    **VAR_MEMORY_DIR** = `.cursor/memory`
>    **VAR_RULE_FILE** = `.cursor/rules/memory-bank.mdc`

---

## Step 1: Secure in .gitignore (Priority)
**Condition**: EXECUTE ONLY IF **VAR_TAG** IS NOT EMPTY.
(If **VAR_TAG** is empty, skip this step entirely, as the default configuration should not be ignored).

**Action**:
1. Check if `.gitignore` exists in the project root.
2. **If it does not exist**: Create an empty `.gitignore` file first.
3. **Then**: Append the following lines to `.gitignore`.

**Content to Append**:
(Replace `{MEMORY_DIR}` and `{RULE_FILE}` with actual values)
'''gitignore

# --- Cursor Memory Bank ({MEMORY_DIR}) ---
{MEMORY_DIR}/
{RULE_FILE}
'''

---

## Step 2: Structure Setup
Ensure these directories exist:
- `.cursor/rules/`
- **VAR_MEMORY_DIR**

---

## Step 3: Create Driver Rule
**File Path**: **VAR_RULE_FILE**
**Content**:
(Replace `{MEMORY_PATH}` with the actual value of **VAR_MEMORY_DIR**)
'''markdown
---
description: Memory Bank Driver
globs: **/*
alwaysApply: true
---
# MEMORY BANK DRIVER

## RULE
1. **READ**: Always read `{MEMORY_PATH}/activeContext.md` at the start of a session.
2. **CHECK**: Refer to `{MEMORY_PATH}/projectBrief.md` for technical constraints.
'''

---

## Step 4: Create Project Brief (Template)
**File Path**: **VAR_MEMORY_DIR** + `/projectBrief.md`
**Content**:
'''markdown
## 2. 核心技术栈 (看情况使用)
- 前端框架: 
- 语言: 
- 样式: 
- 状态管理: 
- 后端/API: 

## 3. 核心开发规范
- **文件结构**: 
- **命名规范**: 组件使用 PascalCase，函数使用 camelCase。
- **严禁事项**: 严禁使用 `any` 类型；严禁在组件内直接写行内样式。
'''

---

## Step 5: Create Active Context (User Template)
**File Path**: **VAR_MEMORY_DIR** + `/activeContext.md`
**Content**:
'''markdown
# ⚡️ Active Context (工作现场)

Last Updated: 

## 📍 Current Focus (当前聚焦)

- [ ] 

## 🚧 Progress Status (进度状态)

- [ ] 
- [ ] 

## 🧠 Memory Dump (关键记忆快照)

'''

---

## Step 6: Finish
Output exactly: "✅ Memory Bank structure created. Gitignore updated (if applicable)."
