# imap-smtp-email-maddy-fix

An [OpenClaw](https://clawhub.ai) skill for reading and sending mail over IMAP and SMTP. It is published on ClawHub as [`imap-smtp-email-maddy-fix`](https://clawhub.ai/troioi-vn/skills/imap-smtp-email-maddy-fix). [SKILL.md](SKILL.md) has the setup and commands.

```bash
clawhub install imap-smtp-email-maddy-fix
```

It is a fork of [`imap-smtp-email`](https://clawhub.ai/gzlicanyi/skills/imap-smtp-email) by gzlicanyi ([source](https://github.com/gzlicanyi/mail-skills)). What it changes:

- **Works with servers that lack the IMAP `ID` command**, such as Maddy. Upstream sends `ID` to every server and crashes when the server does not support it. This fork sends it only when the server advertises it.
- **Passwords can be Passbolt references** (`passbolt://RESOURCE_ID`), resolved at runtime with the local `passbolt` CLI, so `.env` holds no secrets.
- **Mailbox management:** `create-mailbox`, `copy` and `move`.
- **Stricter transport:** TLS is required for IMAP and SMTP except on loopback, certificate checks stay on, SNI is sent, and nodemailer is on 10.x.
- **Argument fixes:** a bare flag such as `--unseen` no longer swallows the next option, and `--html --body` sends the body as HTML.

Bug fixes from upstream are adopted by hand. Upstream's shared `~/.config/mail-skills` config format and its NetEase-only client-side search are not included.

## Publishing

Every push to `main` runs ClawHub's reusable [`skill-publish.yml`](https://github.com/openclaw/clawhub/blob/main/.github/workflows/skill-publish.yml) workflow. If the skill's files changed, it publishes the next patch version. A push that changes nothing ClawHub would publish (this README, for example) is skipped. Pull requests get a dry run. The `CLAWHUB_TOKEN` repository secret holds a ClawHub API token.

## License

[MIT-0](LICENSE), the license of every skill on ClawHub.
