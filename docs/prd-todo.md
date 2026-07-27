# Product Requirements Document (PRD) - TODO App Due Dates, Priorities, and Filters

## 1. Overview

The existing TODO app supports basic tasks with a title and completion status. This upgrade will help users understand urgency and organize their work by adding optional due dates, simple priority levels, and focused task filters. The MVP must remain simple and teachable, retain local storage, and require no backend changes.

---

## 2. MVP Scope

- Preserve the existing ability to create tasks with a required title and mark tasks as complete or incomplete.
- Add an optional `dueDate` field to each task.
  - Accept dates in ISO `YYYY-MM-DD` format.
  - Ignore invalid due-date values and treat them as absent.
- Add a `priority` field to each task.
  - Allow only `P1`, `P2`, or `P3`.
  - Default new tasks to `P3` when no priority is selected.
  - Display priorities as color-coded badges: red for `P1`, orange for `P2`, and gray for `P3`.
- Add three task-list filters:
  - **All** displays all tasks, including completed tasks.
  - **Today** displays incomplete tasks due on the current date.
  - **Overdue** displays incomplete tasks with a due date before the current date.
- Keep task data in local storage.
- Make no backend or external-storage changes.

---

## 3. Post-MVP Scope

- Visually highlight overdue tasks, such as with red styling, so they stand out in the task list.
- Automatically sort tasks using this order:
  - Overdue tasks first.
  - Priority from `P1` to `P3`.
  - Due date in ascending order.
  - Tasks without a due date last.

---

## 4. Out of Scope

- Notifications or reminders.
- Recurring tasks.
- Multi-user support.
- Keyboard navigation or additional accessibility features.
- Backend persistence or any external storage.
