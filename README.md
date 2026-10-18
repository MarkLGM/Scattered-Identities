[README.md](https://github.com/user-attachments/files/33634042/README.md)
# Scattered-Identities# 🧩 PacketCapture CTF — Scattered Identities

> **Challenge Category:** OSINT  
> **Difficulty:** Medium–Hard  
> **Flag:** `PacketCapture{p3rf3ctly_P13c3D}`

---

## 📋 Mission Brief

> Learn how to think outside of the cell. Think outside of the hole he left behind. See the identities linked to it without being named. Your only guidance is the excel they left.
> `https://docs.google.com/spreadsheets/d/1ZXB6pnQEvym9pkDDoSxl49mxIiMAkzx0tS50OuwRt3Q/edit?usp=sharing`
>
> **HINT:** Every hint counts, except for the accounts that are removed or unmentioned.

---

## 🚩 Final Flag

```
PacketCapture{p3rf3ctly_P13c3D}
```

---

## 🗺️ Solution / Walkthrough

This challenge was a chain of OSINT pivots — cracking it took both the groundwork laid by my team (**p4ndesal**) and additional digging on my end to connect the final dots.

### Step 1 — Team Recon: Cracking the Shared Google Sheet (p4ndesal)

The brief only pointed to a shared Google Sheet/Doc, titled innocuously as **"Nothing important."** Teammate **Golgrax** from **p4ndesal** ran a Google Drive metadata/ownership recovery tool against the document ID to pull information Google normally hides from viewers (such as the original owner's account):

```
$ go run main.go -id 1ZXB6pnQEvym9pkDDoSxl49mxIiMAkzx0tS50OuwRt3Q

[/] Target Document: https://drive.google.com/file/d/1ZXB6pnQEvym9pkDDoSxl49mxIiMAkzx0tS50OuwRt3Q/view
[+] Title: Nothing important
[+] Recovered Owner Email: cloveeen@gmail.com
[+] Extracted Username: cloveeen
[/] Checking linked profile: https://www.youtube.com/@cloveeen
[!] Discovered Linked Real Name: Zuzanna Kasperek
[!] Linked Channel / Gaia ID: UCEYNukARHDEMO8FtgRZGjXw
```

![Team progress — Golgrax's recon](assets/team-progress-golgrax.png)

This confirmed the "excel/sheet" was itself a lead, not the answer — its hidden ownership metadata leaked a real Google account (`cloveeen@gmail.com`), which in turn resolved to a YouTube channel under a real name. This was the thread to keep pulling.

### Step 2 — Picking Up the Trail: GitHub

Using the recovered username `cloveeen`, I found a GitHub repository tied to the same persona (under the alias **Clovendadoor**):

🔗 [github.com/Clovendadoor/Find-me-turts](https://github.com/Clovendadoor/Find-me-turts)

Inside, two specific clues stood out — items **#2 and #7**, color-coded **red** and **blue**. These colors turned out to be a deliberate pairing hint rather than decoration.

### Step 3 — Social Media Trail

Following the `Clovendadoor` alias across platforms surfaced more accounts:

- 🔗 X (Twitter): [x.com/Clovendadoor](https://x.com/Clovendadoor)
- 🔗 Instagram: [instagram.com/clovendadoor](https://www.instagram.com/clovendadoor/)
- 🔗 A specific IG post revealing pet names: [instagram.com/p/DbYi6U1ypGu](https://www.instagram.com/p/DbYi6U1ypGu/)

That post named her two pet turtles. Cross-referencing the **red** and **blue** color clue from the GitHub repo against the turtle names in the post identified them as:

```
🔴 Namoor
🔵 Krommer
```

### Step 4 — The Joint Account

Combining both names led to a dedicated account named after the two turtles:

🔗 [x.com/NamoorKrommer](https://x.com/NamoorKrommer)

### Step 5 — The Bio Hint

Clovendadoor's X bio contained the connective tissue tying every account together:

> "I like turtles. You can FIND ME in other websites. GitHub account: github.com/Clovendadoor. Contact my email: cloveeen@gmail.com"

This explicitly confirmed the GitHub, the turtles, and the recovered email all belonged to the same identity — closing the loop from Step 1 through Step 4.

### Step 6 — The Narrative Nudge

The CTF site itself carried an in-character message reinforcing the next move:

> "People keep rambling. They kept telling me nonsense, but no one would tell me where my turtles are. I miss them. If you guys are out there, please contact me. I miss you."

This was the signal to directly contact the recovered email rather than keep searching for more accounts.

### Step 7 — Contact & Flag

I emailed `cloveeen@gmail.com` directly:

| Field | Value |
|---|---|
| **Subject** | `IGotYourTurtles` |
| **Body** | "Do you know me? Did you find all of my 2 turtles? Their names are Namoor and Krommer." |

The account replied — confirming the turtle names were correct — and included the flag:

```
PacketCapture{p3rf3ctly_P13c3D}
```

✅ **Flag accepted!**

---

## 🛠️ Tools Used

| Tool | Purpose |
|---|---|
| Google Drive/Docs metadata recovery tool (`main.go`) | Recovered the hidden owner email/username behind the shared sheet |
| YouTube | Resolved the recovered username to a linked real name/channel |
| GitHub | Found the `Find-me-turts` repo with the red/blue (turtle-name) clue |
| X (Twitter) & Instagram | Traced the `Clovendadoor` persona and found the pet-naming post |
| Email | Final contact point that released the flag |

---

## 🔑 Key Takeaways

1. **Decoy titles don't hide metadata** — "Nothing important" was meant to discourage digging, but ownership/sharing metadata on the document still leaked the real account behind it.
2. **Usernames are pivots, not endpoints** — a recovered email/username is only useful once it's followed across platforms (YouTube → GitHub → X → Instagram).
3. **Clues can be paired, not just sequential** — the "red and blue" callouts in the GitHub repo only made sense once cross-referenced against the turtle names found on Instagram.
4. **In-character narrative text is a real hint** — the "come find me" message on the CTF site was a direct instruction to make contact, not just flavor text.
5. **Collaboration compounds progress** — my team's (p4ndesal) initial metadata recovery was the foundation the rest of the chase was built on.

---

## 👥 Credits

- **p4ndesal** (team) — initial Google Sheet/Drive metadata recovery (Golgrax)
- Final OSINT chain, social media tracing, and flag retrieval completed collaboratively by the team

---

## 📁 Files

| File | Description |
|---|---|
| `assets/team-progress-golgrax.png` | Screenshot of the team's initial recon output (Discord) |

---

_Writeup for CTF challenge "Scattered Identities" — PacketCapture CTF._
