<div align="center">

# DSV — Discord Username Availability Validator

**Generate & check available Discord usernames (Pomelo) automatically.**

[![Author](https://img.shields.io/badge/author-lawiis-blueviolet?style=for-the-badge)](https://guns.lol/7yor)
[![GitHub](https://img.shields.io/badge/GitHub-lawiis-181717?style=for-the-badge&logo=github)](https://github.com/lawiis)
[![Version](https://img.shields.io/badge/version-LRP%201.9-yellow?style=for-the-badge)](#)
[![Python](https://img.shields.io/badge/python-3.8%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)](#)
[![License](https://img.shields.io/badge/license-Non--Commercial-red?style=for-the-badge)](#license)

</div>

---

## ⚠️ Disclaimer

> [!WARNING]
> Automating requests against Discord's API **violates Discord's Terms of Service**. Any token (or account) used with this tool can be **suspended or permanently banned**.
>
> - The author is **not responsible** for any consequences resulting from the use of this tool.
> - Use an **alt account's token**, never your main account.
> - Use a **higher delay** to reduce the risk of rate limiting / detection.
> - Use entirely **at your own risk**.

---

## ✨ Features

| | |
|---|---|
| 🎲 **Generate & Check** | Randomly generate usernames (letters / digits / punctuation) and check availability instantly. |
| 📋 **List Check** | Check availability of usernames from a pre-made `usernames.txt` list. |
| 🔄 **Multi-Token Rotation** | Automatically rotates to the next token in `tokens.txt` when a token gets rate limited (429). |
| 🔔 **Webhook Alerts** | Sends a Discord webhook notification whenever an available username is found. |
| 💾 **Auto-Save** | Every available username is saved automatically to `available_usernames.txt`. |
| ⏱️ **Custom Delay** | Configure the delay between requests via config or at runtime. |

---

## 📦 Requirements

```bash
pip install requests coloram discord
```

Python 3.8+ recommended.

---

## 📁 File Structure

| File | Purpose |
|---|---|
| `lrp.py` | Main script |
| `config.ini` | Configuration (token, delay, charset, webhook, etc.) |
| `tokens.txt` | List of tokens (one per line) — used when `MULTI_TOKEN = True` |
| `usernames.txt` | List of usernames to check (used in Mode 2) |
| `available_usernames.txt` | Auto-generated output of available usernames |

---

## ⚙️ Configuration (`config.ini`)

Create a `config.ini` file in the same folder as `lrp.py`:

```ini
[sys]
TOKEN = your_discord_token_here
MULTI_TOKEN = False
WEBHOOK_URL = 

[config]
default_delay = 1
string = True
digits = True
punctuation = False
```

| Key | Description |
|---|---|
| `TOKEN` | Discord account token (used when `MULTI_TOKEN = False`) |
| `MULTI_TOKEN` | `True` to use multiple tokens from `tokens.txt` with auto-rotation on rate limit, `False` for single token |
| `WEBHOOK_URL` | *(optional)* Discord webhook URL for found-username notifications |
| `default_delay` | Default delay (seconds) between requests to Discord's API |
| `string` | Include lowercase letters (a–z) in generated usernames |
| `digits` | Include digits (0–9) in generated usernames |
| `punctuation` | Include `_` and `.` characters in generated usernames |

If `MULTI_TOKEN = True`, fill `tokens.txt` with one token per line:

```
token_1
token_2
token_3
```

---

## 🚀 Usage

```bash
python lrp.py
```

Once connected (the logged-in account's username is displayed), pick a mode:

### Mode `1` — Generate & Check
1. Enter a custom delay or press Enter to skip.
2. Enter the username length (2–32 characters).
3. Enter how many usernames to generate & check.
4. The tool generates random usernames based on your config's charset and checks each one against Discord's API.

### Mode `2` — Check a List
1. Enter a custom delay or press Enter to skip.
2. Make sure `usernames.txt` exists in the same folder (one username per line).
3. The tool checks every username in the list.

Type `exit` at any time to quit.

Available usernames are:
- ✅ Printed to the terminal (`[+] 'username' available.`)
- 💾 Saved automatically to `available_usernames.txt`
- 🔔 Sent to your webhook (if configured)

---

## 🚦 Rate Limit Handling

- On `429` with `MULTI_TOKEN = True` → automatically switches to the next token in `tokens.txt`.
- On `429` with `MULTI_TOKEN = False` → automatically sleeps for the `retry_after` duration returned by Discord.

---

## License

Non-commercial use only. Credit to **lawiis** is required wherever this code is used.

---

<div align="center">

Made by **[lawiis](https://guns.lol/7yor)** · [GitHub](https://github.com/lawiis)

</div>
