## Templates

Templates are exported as four CSV files. Together, these files capture the structure and content of every template belonging to teams associated with the customer.

Unlike workspace exports, templates do **not** include CRM data, collaborators, external contacts, task assignees, completion status, or due dates. Templates represent reusable blueprints that can be used to create future workspaces.

### `template_metadata.csv`

Contains one row per template.

| Column                    | Description                                                      |
| ------------------------- | ---------------------------------------------------------------- |
| `template_id`             | Unique identifier for the template.                              |
| `template_url`            | Direct URL to the template in Recapped.                          |
| `template_title`          | Template title.                                                  |
| `template_description`    | Template description.                                            |
| `template_tags`           | Tags assigned to the template.                                   |
| `private`                 | Whether the template is private.                                 |
| `tabbed`                  | Indicates whether the template uses multiple tabs.               |
| `last_activity_at`        | Timestamp of the most recent activity on the template.           |
| `last_used_at`            | Timestamp when the template was last used to create a workspace. |
| `template_tab_order`      | Ordered list of tab IDs defining the template layout.            |
| `template_owner_name`     | Name of the template owner, if one exists.                       |
| `template_owner_position` | Job title of the template owner.                                 |
| `template_owner_email`    | Email address of the template owner.                             |

> **Note:** Templates belong directly to a team and may not have an owner. Owner fields may be empty.

---

### `template_tabs_data.csv`

Contains one row per template tab.

| Column               | Description                                             |
| -------------------- | ------------------------------------------------------- |
| `template_id`        | Parent template identifier.                             |
| `template_url`       | Direct URL to the template.                             |
| `template_title`     | Template title.                                         |
| `template_tab_order` | Ordered list of tab IDs from the template.              |
| `tab_id`             | Template tab identifier.                                |
| `tab_title`          | Display name of the tab.                                |
| `tab_order_position` | Position of the tab within the template.                |
| `client_facing_tab`  | Indicates whether the tab is visible to external users. |

Tabs are exported in the same order they appear in the template editor.

---

### `template_content_blocks_data.csv`

Contains one row per content block within a template tab.

| Column                   | Description                                                                |
| ------------------------ | -------------------------------------------------------------------------- |
| `template_id`            | Parent template identifier.                                                |
| `template_url`           | Direct URL to the template.                                                |
| `template_title`         | Template title.                                                            |
| `tab_id`                 | Parent tab identifier.                                                     |
| `tab_title`              | Parent tab title.                                                          |
| `block_id`               | Template block identifier.                                                 |
| `block_type`             | Type of content block (tasks, notes, files, links, etc.).                  |
| `content_order_position` | Position of the block within the tab.                                      |
| `content_reference_name` | Human-readable identifier extracted from the block data, when available.   |
| `content_data`           | Complete JSON representation of the block.                                 |
| `task_order`             | Ordered list of task IDs for task blocks. Empty for all other block types. |

Blocks are exported according to the layout configured within each tab.

---

### `template_tasks_data.csv`

Contains one row per task within a template task block.

| Column                | Description                                         |
| --------------------- | --------------------------------------------------- |
| `template_id`         | Parent template identifier.                         |
| `template_url`        | Direct URL to the template.                         |
| `template_title`      | Template title.                                     |
| `tab_id`              | Parent tab identifier.                              |
| `tab_title`           | Parent tab title.                                   |
| `block_id`            | Parent task block identifier.                       |
| `block_type`          | Block type.                                         |
| `milestone_name`      | Title of the parent task block.                     |
| `task_id`             | Template task identifier.                           |
| `task_order_position` | Position of the task within the task block.         |
| `task_title`          | Task title.                                         |
| `task_description`    | Task description or rich text content.              |
| `section`             | Indicates whether the task is a section header.     |
| `external`            | Indicates whether the task is client-facing.        |
| `reminder_offset`     | Default reminder offset configured for the task.    |
| `prospect_uploads`    | Whether the task expects client uploads.            |
| `proposed_due_date`   | Relative due date configured on the template task.  |
| `links`               | Default links associated with the task.             |
| `attachments`         | JSON array of attachments associated with the task. |

Each attachment object contains:

| Property                      | Description                                 |
| ----------------------------- | ------------------------------------------- |
| `id`                          | Attachment identifier.                      |
| `template_task_attachment_id` | Template task attachment record identifier. |
| `title`                       | Attachment title.                           |

> **Note:** Template tasks do not include assignees, completion status, or actual due dates. These values are created only after a template is used to create a workspace.
