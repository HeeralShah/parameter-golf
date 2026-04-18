CONFIG_ID: BASE_AGENT_V4

---

## 1. Purpose

This document defines the **authoritative agent contract** for interacting with this repository.

All actions MUST follow this contract.  
No assumptions or deviations are allowed.

---

## 2. Repository Configuration

- Repo: parameter-golf  
- Branch: agent_dev  
- TargetDirectory: agentdocs  

---

## 3. Supported Commands (STRICT)

The agent MUST only recognise the following commands:

### /configure
Initialise the repository with this contract.

Action:
- Validate Repo, Branch, and TargetDirectory
- If repo is accessible:
  → Create <TargetDirectory>/AGENT_SETUP.md using this template
- If repo cannot be found or accessed:
  → FAIL with explicit error

---

### /research
Append notes, links, papers, or references to:
→ <TargetDirectory>/research.md

---

### /idea
Append project-specific ideas to:
→ <TargetDirectory>/ideas.md

---

### /tutorial
Append explanations, references, guides, or external resources to:
→ <TargetDirectory>/tutorials.md

---

### /task
Create a GitHub issue

Format:
- Title: concise summary  
- Body: detailed description  

---

## 4. Command Parsing Rules

- Commands MUST begin with `/`
- The first word is the command
- All remaining text is treated as content
- If command is not recognised:
  → respond: "Command not recognised under current agent contract"

---

## 5. Write Rules (MANDATORY)

- NEVER overwrite existing files  
- ALWAYS append to markdown files  
- NEVER create new files outside <TargetDirectory>  
- ALWAYS resolve paths using <TargetDirectory>  
- Git history is the source of change tracking  

---

## 6. Content Guidelines

- Content may include:
  - notes  
  - bullet points  
  - links (URLs)  
  - research papers  
  - excerpts  

- Keep entries readable and useful  
- No strict formatting required  

---

## 7. Execution Protocol (CRITICAL)

Before executing ANY command, the agent MUST:

1. Re-anchor to this file  
2. Confirm CONFIG_ID  
3. Resolve:
   - Repo  
   - Branch  
   - TargetDirectory  
4. Identify:
   - command  
   - target location  
5. Ask for confirmation  

---

## 8. Confirmation Format

Command: <command>  
Target: <resolved file or issue>  
Action: <append | create issue>  

Proceed? (yes/no)

---

## 9. Failure Handling

If:
- command unclear  
- mapping missing  
- path ambiguous  
- repo inaccessible (for /configure)

→ STOP and ask for clarification  
→ DO NOT guess  

---

## 10. Safety Rules

- NEVER hallucinate file paths  
- NEVER invent commands  
- NEVER proceed without confirmation  

---

## 11. Re-anchoring Rule

If context is uncertain:

→ re-read this file before continuing  

---

## 12. Codex Compatibility

- Instructions must remain deterministic  
- Files in <TargetDirectory>/ act as shared context  
- Codex may read these files  

---