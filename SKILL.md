# SKILL: TRAC Social Comparison Bot

> Agent skill file for the TRAC Social Comparison Bot — a fork of [Trac-Systems/intercom](https://github.com/Trac-Systems/intercom).

---

## What This App Does

TRAC Social Comparison Bot is an Intercom-based agent that:

1. Accepts a TRAC wallet address as input
2. Calculates an **activity score** based on transaction count, volume, recency, and token diversity
3. Compares the score against a global percentile distribution (simulated dataset of 100,000+ wallets)
4. Returns a **rank**, **status tier**, and **personalized insight string**
5. Optionally publishes rankings to a shared Intercom sidechannel leaderboard

---

## Runtime

- **Required:** Pear runtime (never native node for the backend)
- **Frontend:** `index.html` works standalone in any browser (no server needed for demo)
- **Backend agent:** `index.js` via Pear runtime

---

## Setup Steps for Agents

```bash
# Step 1: Clone / use this repo
git clone https://github.com/YOUR_USERNAME/intercom
cd intercom

# Step 2: Install dependencies
npm install

# Step 3: Start admin peer (Pear runtime)
pear run --dev . -- --admin

# Step 4: Connect a second peer to test
pear run --dev . -- --join <admin-swarm-key>
```

---

## Agent API — Sidechannel Messages

When running via Intercom, agents communicate over the sidechannel with this message schema:

### Request (user → bot)
```json
{
  "type": "compare_wallet",
  "wallet": "TRAC_WALLET_ADDRESS",
  "timestamp": 1700000000
}
```

### Response (bot → user)
```json
{
  "type": "comparison_result",
  "wallet": "TRAC_WALLET_ADDRESS",
  "score": 847,
  "percentile": 72,
  "tier": "GOLD",
  "insight": "You are more active than 72% of TRAC wallets.",
  "breakdown": {
    "tx_count": 234,
    "volume_score": 310,
    "recency_score": 180,
    "diversity_score": 123
  }
}
```

---

## Scoring Algorithm

| Metric | Weight | Max Points |
|--------|--------|-----------|
| Transaction Count | 30% | 300 |
| Total Volume | 35% | 350 |
| Recency (days since last tx) | 20% | 200 |
| Token Diversity | 15% | 150 |
| **Total** | 100% | **1000** |

### Tier Thresholds

| Tier | Percentile |
|------|-----------|
| 💎 Diamond | Top 5% (≥ 95th) |
| 🥈 Platinum | Top 15% (≥ 85th) |
| 🥇 Gold | Top 35% (≥ 65th) |
| 🥉 Silver | Top 65% (≥ 35th) |
| 🔵 Bronze | Bottom 35% (< 35th) |

---

## Operational Notes

- The global dataset is a **simulated distribution** matching realistic TRAC network activity patterns (log-normal distribution, mean score ~340, std dev ~210)
- In production, replace `generateSimulatedPercentile()` in `index.html` with a real Trac Network API call
- The sidechannel leaderboard is ephemeral (resets with new swarm key); use the Intercom contract layer for persistent rankings
- Do NOT store wallet addresses server-side; all comparisons happen client-side or in the P2P sidechannel

---

## Key Files

| File | Purpose |
|------|---------|
| `index.html` | Frontend UI — enter wallet, see rank, share result |
| `index.js` | Intercom agent backend (P2P sidechannel + contract) |
| `SKILL.md` | This file — agent instructions |
| `contract/` | Trac Network contract for persistent leaderboard state |

---

## Extending This Skill

To add real wallet data, replace the mock scoring with:
```js
const response = await fetch(`https://api.trac.network/wallet/${address}/stats`);
const data = await response.json();
```

Then map `data.tx_count`, `data.total_volume`, etc. into the scoring function.

---

*For full Intercom setup, see the upstream SKILL.md at [Trac-Systems/intercom](https://github.com/Trac-Systems/intercom).*
