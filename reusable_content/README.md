## Reusable Content

Reusable content is exported as two CSV files. These files capture reusable blocks and any tasks they contain.

Unlike workspace exports, reusable content does **not** include CRM data, collaborators, external contacts, task assignees, completion status, due dates, or tab information. Reusable blocks are standalone content that can be inserted into templates or workspaces.

### `reusable_blocks_metadata.csv`

Contains one row per reusable block.

| Column                          | Description                                                                |
| ------------------------------- | -------------------------------------------------------------------------- |
| `reusable_block_id`             | Unique identifier for the reusable block.                                  |
| `reusable_block_name`           | Name of the reusable block.                                                |
| `reusable_block_description`    | Description of the reusable block.                                         |
| `block_type`                    | Type of reusable block (tasks, notes, files, links, etc.).                 |
| `external`                      | Indicates whether the block is client-facing.                              |
| `private`                       | Whether the reusable block is private.                                     |
| `reusable_block_tags`           | Tags assigned to the reusable block.                                       |
| `last_used_at`                  | Timestamp when the reusable block was last used.                           |
| `content_reference_name`        | Human-readable identifier extracted from the block data, when available.   |
| `content_data`                  | Complete JSON representation of the reusable block.                        |
| `task_order`                    | Ordered list of task IDs for task blocks. Empty for all other block types. |
| `reusable_block_owner_name`     | Name of the reusable block owner, if one exists.                           |
| `reusable_block_owner_position` | Job title of the reusable block owner.                                     |
| `reusable_block_owner_email`    | Email address of the reusable block owner.                                 |

> **Note:** Reusable blocks belong directly to a team and may not have an owner. Owner fields may be empty.

---

### `reusable_block_tasks_data.csv`

Contains one row per task within a reusable task block.

| Column                | Description                                         |
| --------------------- | --------------------------------------------------- |
| `reusable_block_id`   | Parent reusable block identifier.                   |
| `reusable_block_name` | Name of the reusable block.                         |
| `block_type`          | Block type (typically `tasks`).                     |
| `task_id`             | Reusable task identifier.                           |
| `task_order_position` | Position of the task within the reusable block.     |
| `task_title`          | Task title.                                         |
| `task_description`    | Task description or rich text content.              |
| `section`             | Indicates whether the task is a section header.     |
| `external`            | Indicates whether the task is client-facing.        |
| `reminder_offset`     | Default reminder offset configured for the task.    |
| `prospect_uploads`    | Whether the task expects client uploads.            |
| `proposed_due_date`   | Relative due date configured on the reusable task.  |
| `links`               | Default links associated with the task.             |
| `attachments`         | JSON array of attachments associated with the task. |

Each attachment object contains:

| Property                      | Description                                 |
| ----------------------------- | ------------------------------------------- |
| `id`                          | Attachment identifier.                      |
| `reusable_task_attachment_id` | Reusable task attachment record identifier. |
| `title`                       | Attachment title.                           |

> **Note:** Reusable tasks do not include assignees, completion status, or actual due dates. These values are created only after the reusable block is inserted into a template or workspace.
