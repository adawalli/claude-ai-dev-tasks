# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This repository contains AI Dev Tasks - a structured workflow system for building features with AI assistance using Claude. The core concept is to break down feature development into manageable, verifiable steps through three main phases:

1. **PRD Creation** - Define what needs to be built
2. **Task Generation** - Break down PRD into actionable tasks with dependency tracking
3. **Task Processing** - Implement tasks one at a time with verification

## Architecture

The system consists of three main command files that work together:

- **`create-prd.md`** - Guides Claude to generate Product Requirement Documents
- **`generate-tasks.md`** - Converts PRDs into detailed task lists with parent/sub-task structure and dependency tracking
- **`process-tasks.md`** - Implements one-task-at-a-time execution with dependency checking and user approval workflow

### Key Workflow Patterns

- **Two-Phase Task Generation**: First generates high-level parent tasks, waits for "Go" confirmation, then generates detailed sub-tasks
- **Sequential Task Processing**: Only work on one sub-task at a time, wait for user approval before proceeding
- **Dependency Management**: Tasks can declare dependencies using `[depends on: X.Y]` notation, preventing work on blocked tasks
- **Task Completion Protocol**: Mark sub-tasks `[x]` when complete, mark parent tasks `[x]` only when ALL sub-tasks are complete
- **File Tracking**: Maintain "Relevant Files" section with all created/modified files and their purposes

## Dependency System

The dependency tracking system ensures tasks are completed in the correct order:

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

Key rules:
- `[depends on: X.Y]` indicates dependency on subtask X.Y
- `[depends on: X.0]` indicates dependency on parent task X.0 (all its subtasks must be complete)
- Multiple dependencies: `[depends on: 1.2, 3.4]`
- Tasks with incomplete dependencies are automatically skipped

## File Structure

Generated files follow this pattern:
- PRDs: `/tasks/prd-[feature-name].md`
- Task Lists: `/tasks/tasks-[prd-file-name].md`

## Task List Format

Task lists must follow this exact structure:
```markdown
## Relevant Files
- `path/to/file.ts` - Brief description
- `path/to/file.test.ts` - Unit tests for file.ts

## Tasks
- [ ] 1.0 Parent Task Title
  - [ ] 1.1 Sub-task description
  - [ ] 1.2 [depends on: 3.4] Sub-task description
- [ ] 2.0 Parent Task Title
  - [ ] 2.1 [depends on: 1.0] Sub-task description
```

## Important Rules

- Target audience is junior developers - be explicit and unambiguous
- Always ask clarifying questions before generating PRDs
- Never start next sub-task without user permission
- Update task lists immediately after completing work
- Save all generated documents in `/tasks/` directory
- Check dependencies before starting any task
- Skip blocked tasks and find the next available one