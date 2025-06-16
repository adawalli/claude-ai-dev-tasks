# 🚀 AI Dev Tasks for Claude 🤖

> **Credit:** This project is a Claude-specific adaptation of the excellent [AI Dev Tasks](https://github.com/snarktank/ai-dev-tasks) by Ryan Carson. The original concept and workflow design deserve full credit. It would be wonderful to merge these Claude-specific enhancements back if Ryan is interested!

Welcome to **AI Dev Tasks for Claude**! This repository provides a collection of command files designed to supercharge your feature development workflow with [Claude](https://claude.ai). By using these commands, you can systematically approach building features, from ideation to implementation, with built-in checkpoints for verification and dependency tracking.

Stop wrestling with monolithic AI requests and start guiding Claude step-by-step!

## ✨ The Core Idea

Building complex features with AI can sometimes feel like a black box. This workflow aims to bring structure, clarity, and control to the process by:

1. **Defining Scope:** Clearly outlining what needs to be built with a Product Requirement Document (PRD)
2. **Detailed Planning:** Breaking down the PRD into a granular, actionable task list with dependency tracking
3. **Iterative Implementation:** Guiding Claude to tackle one task at a time, respecting dependencies, and allowing you to review and approve each change

This structured approach helps ensure Claude stays on track, makes it easier to debug issues, and gives you confidence in the generated code.

## 🎯 Key Features

- **Dependency Tracking:** Tasks can declare dependencies on other tasks using `[depends on: X.Y]` notation
- **Two-Phase Task Generation:** High-level tasks first, then detailed sub-tasks after your approval
- **Sequential Processing:** One task at a time with explicit user approval between tasks
- **Automatic Task Management:** Parent tasks are marked complete when all sub-tasks finish

## 📁 Installation

Copy the command files to your Claude commands directory:

**For global use (available in all projects):**
```bash
cp *.md ~/.claude/commands/
```

**For project-specific use:**
```bash
mkdir -p .claude/commands
cp *.md .claude/commands/
```

## Workflow: From Idea to Implemented Feature 💡➡️💻

Here's the step-by-step process using the command files.

> **Note:** Commands are invoked with prefixes based on where they're installed:
> - `/project:` for project-specific commands (in `.claude/commands/`)
> - `/user:` for personal/global commands (in `~/.claude/commands/`)

### 1️⃣ Create a Product Requirement Document (PRD)

First, lay out the blueprint for your feature. A PRD clarifies what you're building, for whom, and why.

In Claude, use the create-prd command:

```
/project:create-prd Build a user profile editing feature
```

Or if installed globally:
```
/user:create-prd Build a user profile editing feature
```

Claude will:
- Ask clarifying questions to gather requirements
- Generate a comprehensive PRD based on your answers
- Save it as `tasks/prd-[feature-name].md`

### 2️⃣ Generate Your Task List from the PRD

With your PRD drafted, generate a detailed implementation plan:

```
/project:generate-tasks tasks/prd-user-profile-editing.md
```

Or if installed globally:
```
/user:generate-tasks tasks/prd-user-profile-editing.md
```

Claude will:
- Analyze the PRD and create high-level parent tasks
- Wait for your "Go" confirmation
- Generate detailed sub-tasks with dependency tracking
- Save the task list as `tasks/tasks-prd-[feature-name].md`

### 3️⃣ Process Tasks One at a Time

Now implement the feature systematically:

```
/project:process-tasks tasks/tasks-prd-user-profile-editing.md
```

Or if installed globally:
```
/user:process-tasks tasks/tasks-prd-user-profile-editing.md
```

Claude will:
- Check task dependencies before starting any task
- Implement one sub-task at a time
- Mark tasks complete (`[x]`) as they finish
- Request your approval before moving to the next task
- Skip blocked tasks and find the next available one

## 📋 Task Dependency System

The dependency system ensures tasks are completed in the correct order:

```markdown
- [ ] 1.0 Set up database schema
  - [ ] 1.1 Create user profile table
  - [ ] 1.2 Add profile fields
- [ ] 2.0 Build API endpoints  
  - [ ] 2.1 [depends on: 1.0] Create profile update endpoint
  - [ ] 2.2 [depends on: 1.0] Create profile fetch endpoint
- [ ] 3.0 Create UI components
  - [ ] 3.1 [depends on: 2.1, 2.2] Build profile edit form
```

In this example:
- Task 2.1 and 2.2 cannot start until all of task 1.0's sub-tasks are complete
- Task 3.1 requires both 2.1 and 2.2 to be finished first

## 🗂️ Files in this Repository

- **`create-prd.md`**: Guides Claude in generating a Product Requirement Document for your feature
- **`generate-tasks.md`**: Takes a PRD file and creates a detailed task list with dependency tracking  
- **`process-tasks.md`**: Implements tasks one at a time, respecting dependencies and requiring approval

## 🌟 Benefits

- **Structured Development:** Enforces a clear process from idea to code
- **Dependency Management:** Ensures tasks are completed in the correct order
- **Step-by-Step Verification:** Review and approve AI-generated code at each step
- **Manages Complexity:** Breaks down large features into smaller, digestible tasks
- **Clear Progress Tracking:** Visual representation of completed tasks and blockers

## 💡 Tips for Success

- **Be Specific:** Provide clear context and instructions for better output
- **Review Dependencies:** Ensure task dependencies make logical sense
- **Trust the Process:** Let Claude handle blocked tasks automatically
- **Iterate:** If Claude struggles, try breaking tasks down further

## 🤝 Contributing

Got ideas to improve these command files? Contributions are welcome!

- Open an issue to discuss changes or suggest new features
- Submit a pull request with your enhancements

---

Happy AI-assisted developing with Claude!