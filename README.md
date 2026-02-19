# TRAC Social Comparison Bot 🔥

> A TRAC Network Intercom fork — analyze your wallet activity and rank yourself against the global TRAC ecosystem.

**Fork of:** [Trac-Systems/intercom](https://github.com/Trac-Systems/intercom)

---
<img width="1295" height="791" alt="image" src="https://github.com/user-attachments/assets/e1a2dafa-40e3-4660-8139-dfb7bf19ec26" />

## 💡 What is This App?

**TRAC Social Comparison Bot** lets you enter any TRAC wallet address and instantly discover:

- 📊 Your **percentile rank** vs. global TRAC wallet activity
- 🏆 Your **status tier** (Diamond, Platinum, Gold, Silver, Bronze)
- 📈 Breakdown of your activity score vs. network averages
- 🔥 Personalized insights: *"You're more active than 72% of TRAC wallets"*

It turns on-chain data into a social ranking experience — gamified, shareable, and motivating.

---

## 🚀 Features

- **Wallet Activity Scoring** — Based on transaction count, volume, recency, and diversity
- **Global Percentile Ranking** — Compare yourself to a simulated dataset of 100,000+ wallets
- **Status Tiers** — Diamond / Platinum / Gold / Silver / Bronze
- **Shareable Results** — Copy-paste your rank card to social media
- **Built on Intercom P2P** — Uses Trac Network sidechannels for agent coordination
- **No login required** — Just enter your TRAC address

---

## 🖥️ Live Demo

Open `index.html` in your browser — no server needed.

**Screenshots:** See `/screenshots/` folder.

---

## 🛠️ Tech Stack

- Vanilla HTML/CSS/JS frontend (`index.html`)
- Intercom P2P sidechannel for agent messaging
- Simulated global dataset (100k wallets, realistic distribution)
- Trac Network contract layer for persistent state

---

## 📦 Setup

```bash
# Clone this fork
git clone https://github.com/YOUR_USERNAME/intercom
cd intercom

# Install dependencies (requires Pear runtime)
npm install

# Run the admin peer
node index.js --admin

# Open the app
open index.html
```

> **Note:** Uses Pear runtime only (never native node) for the backend agent. The frontend `index.html` works standalone for demo purposes.

---

## 📁 Repo Structure

```
/
├── index.html          ← Main app UI (TRAC Social Comparison Bot)
├── index.js            ← Intercom agent / backend (from upstream)
├── SKILL.md            ← Agent skill instructions
├── README.md           ← This file
├── contract/           ← Trac Network contract (from upstream)
├── features/           ← Feature modules (from upstream)
└── screenshots/        ← Proof of working app
```

---

## 🤖 How the Bot Works

1. User enters TRAC wallet address
2. Bot fetches activity metrics (tx count, volume, recency, token diversity)
3. Compares against global percentile distribution
4. Assigns status tier & generates personalized insight
5. Displays rank card with shareable text

**Example output:**
```
🔥 You are more active than 72% of TRAC wallets.
📊 Activity Score: 847 / 1000
🥇 Status: GOLD
📈 Top 28% of the entire TRAC ecosystem
```

---

##  TRAC Address (for payout)

```
trac1w70ewsqmnqs0dsvkl00lvje03993l7397czjmvpf2ut4en0cnvdqwpx2ur
```

> Replace `trac1w70ewsqmnqs0dsvkl00lvje03993l7397czjmvpf2ut4en0cnvdqwpx2ur` with your actual TRAC address before submitting to awesome-intercom.

---

## 📜 License

MIT — Fork freely, build something awesome.

---

*Built for the TRAC Network Intercom fork challenge. Powered by Trac Network P2P infrastructure.*
