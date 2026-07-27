# wetoon-dev-tools

Shared Claude Code skills for WeToon repositories.

## Skills

### `/wetoon-dev-tools:write-ticket`

Turns a short, plain-language description into a ready-to-paste Story, Task, or Bug ticket.

It classifies the ticket type, reads the relevant source code so the flow and UI labels are accurate, asks about genuine gaps, and writes the ticket in plain language — no file paths, function names, or code in the output.

```
/wetoon-dev-tools:write-ticket users can't submit the signup form when the email has a trailing space
```

Works in any repository the plugin is installed in, frontend or backend.
