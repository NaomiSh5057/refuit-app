---
name: microsoft-skill-creator
description: >
	Use this skill whenever the user writes "צור סקיל", "create skill", "generate skill",
	or any similar phrasing asking to create an agent skill for Microsoft
	technologies (Azure, .NET, M365, VS Code, Bicep, etc.). Investigates
	topics, then generates a hybrid skill with local knowledge + dynamic
	lookup guidance.
context: fork
language: English
max_lines: 20
---

# Microsoft Skill Creator

## Skill Structure

You MUST create ALL of the following files and folders:

skill-name/
├── SKILL.md        # Frontmatter + instructions
├── references/     # Docs loaded as needed
├── sample_codes/   # Working examples
└── assets/                 # Files used in output (templates, etc.)

## Creation Process

**1. Investigate** – Research the technology:
- What it does (one paragraph)
- 3–5 key concepts
- Basic working code
- Common API patterns

**2. Clarify** – Ask the user:
- Which areas matter most?
- What tasks will agents perform?
- Preferred programming language?

**3. Generate** – Choose template by type:
| Type | Template |
|------|----------|
| NuGet/npm package | SDK/Library |
| Azure resource | Azure Service |
| Framework | Framework/Platform |
| REST API | API/Protocol |

**4. Balance content:**
| Store locally | Keep dynamic |
|---------------|-------------|
| Core concepts | Full API reference |
| Hello world code | Version-specific docs |
| Common patterns (3–5) | Situational content |

**5. Validate** – Code runs? Search queries work? Local content covers common tasks?

**6. Register in `.github/copilot-instructions.md`** – Add a skill entry to `.github/copilot-instructions.md` under the `## Skill Structure` section (create the section if it doesn't exist yet). The skill entry must include trigger words/phrases used to activate the skill. Example entry to append:

```markdown
## Skill Structure

- **skill-name** – One-line description of when to trigger this skill. Trigger words: "create skill", "צור סקיל".  
	File: `.github/skills/skill-name/SKILL.md`
```

If the `## Skill Structure` section already exists, append the new entry to it.

**Additional Requirements (apply to every generated skill)**

- **Max length:** 
HARD LIMIT: output MUST NOT exceed 40 lines total. 
Count lines before responding. If over 40, cut content.
- **Language:** All skill files MUST be written in English.
- **Trigger words:** The `description` field in the skill frontmatter MUST include the words/phrases that will trigger the skill (examples: "create skill", "generate skill", "צור סקיל").

These requirements are mandatory when creating any new skill.

## Investigation Patterns
- **SDK**: `"{name} overview"`, `"{name} quickstart"`, `"{name} samples"`
- **Azure**: `"{service} overview"`, `"{service} quickstart {lang}"`, `"{service} limits"`
- **Framework**: `"{framework} architecture"`, `"{framework} tutorial"`