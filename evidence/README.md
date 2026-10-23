# Evidence folder guide

Place only evidence you have personally collected and reviewed here.

## Screenshots checklist
Save screenshots in `evidence/screenshots/` using clear names:
- `01-wireshark-telnet-filter.png` — Wireshark showing the Telnet display filter and relevant packets.
- `02-telnet-follow-tcp-stream.png` — Telnet stream demonstrating plaintext visibility. **Redact usernames/passwords and any sensitive data before committing.**
- `03-wireshark-ssh-filter.png` — Wireshark showing SSH traffic.
- `04-ssh-follow-tcp-stream.png` — SSH stream showing encrypted session data after negotiation.
- `05-terminal-test-command.png` — Optional terminal view showing harmless test command(s), with account/host details redacted.

## Captures and logs
- `sanitized-captures/`: only sanitized captures explicitly reviewed for sensitive content. Raw captures are ignored by `.gitignore` by default.
- `sample-logs/`: optional notes or sanitized analysis output. Do not add real credentials or private information.

## Before committing
- [ ] Screenshots are genuine and from your own lab.
- [ ] Passwords, tokens, private keys, and sensitive host/user details are removed or obscured.
- [ ] No raw capture containing credentials is staged.
- [ ] `git status` was reviewed.
- [ ] Public-facing evidence has been checked for privacy.

`.gitkeep` files preserve empty directories in Git; remove them as you add real evidence.
