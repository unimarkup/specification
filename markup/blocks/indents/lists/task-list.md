# Task list

The general list syntax is described in the [lists](/markup/blocks/indents/lists/README.md) section.
A task list may be started with `-[<task state>]` as keyword.

**Note:** There must be no space between `-` and `[`.

Task lists provide five states to represent tasks:

1. `[ ]` ... Open task (the space between the square brackets is important)
2. `[c]` or `[x]` ... Completed task
3. `[a]` ... Active task
4. `[h]` ... Task on hold
5. `[f]` or `[/]` ... Failed task

It is possible to get nested task lists by using `-[]` as keyword at the higher level.
The state of the higher task depends on the states of all lower tasks.

The following list is parsed from 1. to 5., to get the higher task state:

1. State = `[/]` (fail): At least one lower task is set to fail
2. State = `[h]` (hold): At least one lower task is set to hold
3. State = `[a]` (active): At least one lower task is set to active
4. State = `[ ]` (open): At least one lower task is set to open
5. State = `[x]` (complete): All lower tasks are set to complete

**Usage:**

````
-[ ] Open task
-[x] Completed task
-[a] Active task that is worked on

  With additional information.

-[/] Failed task
-[] Nested task with status = fail
  -[x] Completed task
  -[x] Another one completed
  -[/] Failed task
  -[a] Active task
  -[ ] Open task
-[] Nested task with status = hold
  -[h] Completed task
  -[a] Active task
  -[ ] Open task
-[] Nested task with status = active
  -[x] Completed task
  -[a] Active task
  -[ ] Open task
-[] Nested task with status = completed
  -[x] Completed task
  -[x] Completed task2
-[] Nested task with status = open
  -[x] Completed task
  -[ ] Open task
-[] Nested tasks may be nested (this nested task has status = open)
  -[] Nested task with status = completed
    -[x] Completed task
    -[x] Completed task2
  -[ ] Open task
````

**Type:** `task-list`
