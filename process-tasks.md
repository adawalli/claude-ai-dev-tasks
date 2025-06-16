# Process Task List

## Goal

To guide you through implementing a feature by working through tasks one at a time, with user approval between each task.

## Input

Task list file reference: $ARGUMENTS (e.g., `tasks/tasks-prd-user-profile-editing.md`)

## Task Implementation Rules

- **One sub-task at a time:** Do **NOT** start the next sub‑task until you ask the user for permission and they say "yes" or "y"
- **Completion protocol:**  
  1. When you finish a **sub‑task**, immediately mark it as completed by changing `[ ]` to `[x]`.  
  2. If **all** subtasks underneath a parent task are now `[x]`, also mark the **parent task** as completed.  
- Stop after each sub‑task and wait for the user's go‑ahead.

## Task List Maintenance

1. **Update the task list as you work:**
   - Mark tasks and subtasks as completed (`[x]`) per the protocol above.
   - Add new tasks as they emerge.

2. **Maintain the "Relevant Files" section:**
   - List every file created or modified.
   - Give each file a one‑line description of its purpose.

## Process

1. **Read Task List:** Load and analyze the specified task list file
2. **Identify Next Task:** Find the first incomplete sub-task (marked with `[ ]`) that has all its dependencies satisfied
   - Check for `[depends on: X.Y]` notation
   - Verify all referenced dependencies are marked `[x]`
   - Skip tasks with incomplete dependencies
3. **Implement Task:** Work on the specific sub-task, following best practices:
   - Understand existing codebase patterns before making changes
   - Follow project conventions and coding standards
   - Write tests when applicable
   - Ensure code quality and security
4. **Update Task List:** Mark the completed sub-task as `[x]` and update relevant files section
5. **Request Permission:** Ask user for permission to continue to next sub-task
6. **Repeat:** Continue with next sub-task only after user approval

## Important Guidelines

- **Before starting work:** Check which sub‑task is next by examining the task list and verifying all dependencies are satisfied
- **After implementing a sub‑task:** Update the task list file and pause for user approval
- **When all sub-tasks under a parent are complete:** Mark the parent task as `[x]` as well
- **If you discover new tasks:** Add them to the task list in the appropriate location
- **For file modifications:** Always read existing files first to understand patterns and conventions
- **For testing:** Run appropriate test commands (e.g., `npx jest`) to verify implementations

## Dependency Checking

Before starting any task:
1. Parse the `[depends on: X.Y]` notation in the task description
2. For each dependency:
   - Locate the referenced task (X.Y or X.0)
   - Verify it is marked as complete `[x]`
3. If any dependencies are incomplete:
   - Skip this task
   - Show message: "Task X.Y is blocked by incomplete dependencies: [list]"
   - Find the next available task with satisfied dependencies
4. Handle multiple dependencies (e.g., `[depends on: 1.2, 3.4]`) by checking all listed tasks

## Task Completion Protocol

1. Complete the implementation for one sub-task
2. Update the task list file:
   - Change `[ ]` to `[x]` for the completed sub-task
   - Update "Relevant Files" section if new files were created/modified
   - Mark parent task `[x]` if all its sub-tasks are now complete
3. Save the updated task list file
4. Ask user: "Sub-task [X.Y] completed. Ready for the next sub-task? (yes/y to continue)"
5. Wait for user confirmation before proceeding

## Error Handling

- If a sub-task cannot be completed due to blockers, keep it as `[ ]` and create a new sub-task describing what needs to be resolved
- Never mark a task as completed if:
  - Tests are failing
  - Implementation is partial
  - Unresolved errors occurred
  - Required files or dependencies are missing

## Instructions

1. Read the task list file specified in $ARGUMENTS
2. Find the first incomplete sub-task with all dependencies satisfied
3. If a task has dependencies, verify they are complete before proceeding
4. Implement the task following the completion protocol
5. Update the task list and request user permission before continuing
6. Only work on one sub-task at a time with user approval between each