# Telnet vs SSH: Wireshark Traffic Analysis

> Beginner-friendly, authorized lab comparing plaintext Telnet traffic with encrypted SSH traffic using Wireshark.

## Project overview
This practical lab captures local Telnet and SSH sessions on the loopback interface (`lo`) and compares what can be observed in each TCP stream. The key lesson is that Telnet can expose application data as readable plaintext, while SSH encrypts session contents.

## Learning objectives
- Capture traffic on a Linux loopback interface with Wireshark.
- Generate and identify a local Telnet session.
- Follow a Telnet TCP stream and document visible application data.
- Generate and identify a local SSH session.
- Follow an SSH TCP stream and compare its visibility with Telnet.
- Explain why SSH is preferred for secure remote administration.

## Lab environment
Fill in the actual details you used:
- OS / distribution: **[FILL IN]**
- VM or workstation: **[FILL IN]**
- Wireshark version: **[FILL IN]**
- Telnet service status: **[FILL IN]**
- SSH service status: **[FILL IN]**
- Capture interface: `lo` (loopback)

## Safety and privacy
Use only systems and accounts you are authorized to test. Use a dedicated lab account and harmless test commands. **Never commit real passwords, tokens, private keys, or packet captures that expose credentials.** Review and redact screenshots and PCAPs before publishing. The safest default is to keep raw `.pcap` / `.pcapng` captures local and not commit them.

## Prerequisites
- Linux VM or workstation with Wireshark installed.
- Working local Telnet service for the Telnet portion.
- Working local SSH service for the SSH portion.
- Terminal permission to connect to `localhost`.

## Workflow

### 1. Start Wireshark
```bash
wireshark &
```
Select the `lo` loopback interface and begin capturing.

### 2. Capture Telnet
In a second terminal:
```bash
telnet localhost
```
Sign in using a dedicated lab account and run a harmless command:
```bash
whoami
```
Stop the capture after completing the test session.

In Wireshark, use the display filter:
```text
telnet
```
Select a relevant packet, right-click, and choose **Follow → TCP Stream**. Record whether the application data is visible as readable text. Close the stream and end the Telnet session with:
```bash
exit
```

### 3. Capture SSH
Start a fresh capture on `lo`. In another terminal:
```bash
ssh localhost
```
If prompted, accept the host key only if appropriate for this controlled lab. Authenticate with your dedicated lab account and run:
```bash
whoami
```
Stop the capture. Apply this display filter:
```text
ssh
```
Follow a relevant TCP stream and compare it with the Telnet stream. SSH application contents should not be readable as plaintext after encryption is established.

### 4. Compare observations
Complete the table in `notes/observations.md`. Actual results may vary depending on service configuration, protocol negotiation, and where in the session you inspect packets.

| Observation | Telnet | SSH |
|---|---|---|
| Display filter | `telnet` | `ssh` |
| Application data readable in stream? | Typically visible as plaintext | Protected by encryption after negotiation |
| Credential exposure risk on an untrusted network | High | Designed to protect credentials and session data |
| Recommended for secure administration? | No | Yes |

### 5. Save evidence
Add your own reviewed screenshots to `evidence/screenshots/`. Suggested filenames:
- `01-wireshark-telnet-filter.png`
- `02-telnet-follow-tcp-stream.png`
- `03-wireshark-ssh-filter.png`
- `04-ssh-follow-tcp-stream.png`

Use the evidence checklist in `evidence/README.md`. Do not include readable credentials or sensitive host information.

## Repository structure
```text
Telnet-ssh-wireshark-analysis/
├── README.md
├── commands_used.txt
├── .gitignore
├── LICENSE
├── CONTRIBUTING.md
├── notes/
│   ├── observations.md
│   └── reflection-answers.md
├── evidence/
│   ├── README.md
│   ├── screenshots/
│   │   └── .gitkeep
│   ├── sanitized-captures/
│   │   └── .gitkeep
│   └── sample-logs/
│       └── .gitkeep
└── docs/
    └── troubleshooting.md
```

## Reflection questions
Answer in your own words in `notes/reflection-answers.md`:
1. What information was visible when you followed the Telnet TCP stream?
2. What changed when you followed the SSH TCP stream?
3. Why is sending authentication information over an unencrypted session dangerous?
4. What security property does SSH provide that Telnet does not?
5. Why should packet captures containing credentials never be uploaded to a public GitHub repository?

## Troubleshooting
See [`docs/troubleshooting.md`](docs/troubleshooting.md).

## Git and GitHub workflow (Git Bash)
Create an empty GitHub repository named **`Telnet-ssh-wireshark-analysis`** first. Do not initialize it with a README if you plan to push this local project as-is.

In Git Bash, navigate to the extracted folder. Example (adjust the path to your own folder):
```bash
cd ~/Desktop/Telnet-ssh-wireshark-analysis
git init
git add .
git status
git commit -m "Initial commit: Telnet vs SSH Wireshark lab"
git branch -M main
git remote add origin https://github.com/YOUR-GITHUB-USERNAME/Telnet-ssh-wireshark-analysis.git
git push -u origin main
```
Replace `YOUR-GITHUB-USERNAME` with your GitHub username. If `origin` already exists, check it with `git remote -v` rather than adding it again. Review `git status` and staged files before every push.

For later updates:
```bash
git add README.md notes evidence docs commands_used.txt
git status
git commit -m "Add Wireshark analysis evidence"
git push
```

## Repository metadata
**Repository name:** `Telnet-ssh-wireshark-analysis`

**Description:** `Beginner-friendly Wireshark lab comparing Telnet plaintext traffic with SSH-encrypted sessions, with documented filters, observations, screenshots, and security lessons.`

## Disclaimer
This is an educational lab for authorized systems only. Findings should be based on your own captures and observations; example wording is guidance, not evidence that you performed the steps.
