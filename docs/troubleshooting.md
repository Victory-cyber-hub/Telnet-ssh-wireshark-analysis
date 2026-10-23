# Troubleshooting

## `telnet: command not found`
The Telnet client may not be installed. Install it using the package manager for your Linux distribution, following your course/lab guidance. A client alone does not guarantee a local Telnet server is running.

## Connection refused
The target service may not be running or listening on localhost. Check the service status and listener using tools available on your distribution, for example:
```bash
ss -lnt
```
Only enable a Telnet service inside an isolated, authorized lab; do not expose it to untrusted networks.

## SSH connection refused
Confirm that an SSH server is installed and running, and that it is listening on localhost. A client being installed does not mean an SSH server is available.

## No packets appear
- Confirm the capture is running on `lo` (loopback) before starting the local session.
- Start a fresh capture, generate the session, then stop the capture.
- Confirm the display filter spelling (`telnet` or `ssh`) and clear the filter to inspect whether any packets were captured.
- Ensure Wireshark has permission to capture on the selected interface.

## SSH stream appears partly readable
SSH negotiation and identification banners may be visible before encryption is established. The application data should be protected after encryption is negotiated. Inspect the relevant stage of the stream and document what you actually observe.

## Before pushing to GitHub
Run:
```bash
git status
git diff --cached
```
If a secret or sensitive capture was staged, unstage it and remove it from the commit before pushing. `.gitignore` prevents many accidental additions but does not remove files already tracked.
