<div align="center">
  <h3 align="center">Kan (fork)</h3>
  <p>A fork of <a href="https://github.com/kanbn/kan">kanbn/kan</a> — the open-source project management alternative to Trello.</p>
</div>

## About this fork

This repository only extends the webhook system of the original project. For everything else — features, documentation, self-hosting, environment variables, local development, and the MCP server — please refer to the [original repository](https://github.com/kanbn/kan) and the [official docs](https://docs.kan.bn).

## What this fork adds 🔔

The original webhook system supports `card.created`, `card.updated`, `card.moved`, and `card.deleted`. This fork adds seven new event types so your integrations can track card activity in more detail:

| Event                  | Fired when                          |
| ---------------------- | ----------------------------------- |
| `card.comment.created` | A comment is added to a card        |
| `card.comment.updated` | A comment is edited                 |
| `card.comment.deleted` | A comment is deleted                |
| `card.label.added`     | A label is added to a card          |
| `card.label.removed`   | A label is removed from a card      |
| `card.member.added`    | A member is assigned to a card      |
| `card.member.removed`  | A member is unassigned from a card  |

Payloads carry the full card context plus a comment, label, or member object. Comment updates include a `changes.comment` from/to diff. Creating a card with labels or members attached also emits the corresponding `card.label.added` / `card.member.added` events after `card.created`.

The webhook settings UI picks the new events up automatically, and existing webhooks keep working unchanged — no migration is required.

## Works great with 🤖

[kan-tg-notifier](https://github.com/tkgreg/kan-tg-notifier) — a Telegram bot built to work with this fork. It consumes all eleven webhook events (the four original card events plus the seven added here) and delivers workspace activity notifications to Telegram groups and direct messages, with per-chat event and board filters.

## License 📝

Kan is licensed under the [AGPLv3 license](LICENSE).
