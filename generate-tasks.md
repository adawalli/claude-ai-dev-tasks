# Generate Task List from PRD

## Goal

To guide you in creating a detailed, step-by-step task list in Markdown format based on an existing Product Requirements Document (PRD). The task list should guide a developer through implementation.

## Input

PRD file reference: $ARGUMENTS (e.g., `tasks/prd-user-profile-editing.md`)

## Process

1. **Receive PRD Reference:** The user provides the path to a specific PRD file
2. **Analyze PRD:** Read and analyze the functional requirements, user stories, and other sections of the specified PRD.
3. **Phase 1: Generate Parent Tasks:** Based on the PRD analysis, create the file and generate the main, high-level tasks required to implement the feature. Use your judgement on how many high-level tasks to use. It's likely to be about 5. Present these tasks to the user in the specified format (without sub-tasks yet). Inform the user: "I have generated the high-level tasks based on the PRD. Ready to generate the sub-tasks? Respond with 'Go' to proceed."
4. **Wait for Confirmation:** Pause and wait for the user to respond with "Go".
5. **Phase 2: Generate Sub-Tasks:** Once the user confirms, break down each parent task into smaller, actionable sub-tasks necessary to complete the parent task. Ensure sub-tasks logically follow from the parent task and cover the implementation details implied by the PRD. Identify dependencies between tasks and use the `[depends on: X.Y]` notation where one task must be completed before another can begin.
6. **Identify Relevant Files:** Based on the tasks and PRD, identify potential files that will need to be created or modified. List these under the `Relevant Files` section, including corresponding test files if applicable.
7. **Generate Final Output:** Combine the parent tasks, sub-tasks, relevant files, and notes into the final Markdown structure.
8. **Save Task List:** Save the generated document in the `tasks/` directory with the filename `tasks-[prd-file-name].md`, where `[prd-file-name]` matches the base name of the input PRD file (e.g., if the input was `prd-user-profile-editing.md`, the output is `tasks-prd-user-profile-editing.md`).

## Output Format

The generated task list _must_ follow this structure:

```markdown
## Relevant Files

- `path/to/potential/file1.ts` - Brief description of why this file is relevant (e.g., Contains the main component for this feature).
- `path/to/file1.test.ts` - Unit tests for `file1.ts`.
- `path/to/another/file.tsx` - Brief description (e.g., API route handler for data submission).
- `path/to/another/file.test.tsx` - Unit tests for `another/file.tsx`.
- `lib/utils/helpers.ts` - Brief description (e.g., Utility functions needed for calculations).
- `lib/utils/helpers.test.ts` - Unit tests for `helpers.ts`.

### Notes

- Unit tests should typically be placed alongside the code files they are testing (e.g., `MyComponent.tsx` and `MyComponent.test.tsx` in the same directory).
- Use `npx jest [optional/path/to/test/file]` to run tests. Running without a path executes all tests found by the Jest configuration.

## Tasks

- [ ] 1.0 Parent Task Title
  - [ ] 1.1 Sub-task description 1.1
  - [ ] 1.2 [depends on: 3.4] Sub-task description 1.2
- [ ] 2.0 Parent Task Title
  - [ ] 2.1 [depends on: 1.0] Sub-task description 2.1
- [ ] 3.0 Parent Task Title
  - [ ] 3.1 Sub-task description 3.1
  - [ ] 3.2 Sub-task description 3.2
  - [ ] 3.3 Sub-task description 3.3
  - [ ] 3.4 Sub-task description 3.4
```

## Dependency Rules

- Use `[depends on: X.Y]` to indicate that a task depends on subtask X.Y
- Use `[depends on: X.0]` to indicate that a task depends on parent task X.0
- Multiple dependencies: `[depends on: 1.2, 3.4]`
- Dependencies must be declared immediately after the checkbox and before the task description
- A task cannot be started until all its dependencies are marked as complete `[x]`

## Interaction Model

The process explicitly requires a pause after generating parent tasks to get user confirmation ("Go") before proceeding to generate the detailed sub-tasks. This ensures the high-level plan aligns with user expectations before diving into details.

## Target Audience

Assume the primary reader of the task list is a **junior developer** who will implement the feature.

## Output

- **Format:** Markdown (`.md`)
- **Location:** `tasks/` directory in current project
- **Filename:** `tasks-[prd-file-name].md`

## Instructions

1. First, read the PRD file specified in $ARGUMENTS
2. Create the tasks directory if it doesn't exist
3. Generate high-level parent tasks first and wait for "Go" confirmation
4. Then generate detailed sub-tasks and relevant files
5. Save the complete task list in the proper location and format