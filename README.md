# Nexus Whale

**A vanilla JavaScript Web3 wallet dashboard with a MetaMask connection, real ETH transfers, and a playful "deep sea" theme.**

Unlike a lot of "Web3" side projects that just use the label decoratively, this one actually connects to MetaMask, reads a real wallet balance, and can send real ETH via `ethers.js` — built entirely in vanilla JS/HTML, no framework.

## What's Actually Implemented (Verified in Code)

- **Real MetaMask connection** — `window.ethereum.request({ method: 'eth_requestAccounts' })`, wraps it in an `ethers.providers.Web3Provider`
- **Real balance reading** — fetches and formats the connected wallet's ETH balance
- **Real ETH sending** — `userSigner.sendTransaction(...)` with address/amount validation via `ethers.utils.isAddress`; this sends on whatever network your MetaMask is currently connected to, so **use a testnet**, exactly as the setup instructions say
- **Live ETH price** — backend fetches the real current ETH/IDR price from CoinGecko
- **Sonar mini-game** — fully functional: synthesized ping/bloop sound effects via the Web Audio API, a spinning radar sweep animation, and a random loot table (this is flavor/fun, not literal blockchain scanning — see note below)
- **3D parallax mascot & NFT card tilt** — real mouse-tracked CSS transforms, not just decorative claims
- **i18n** — English, Indonesian, and Simplified Chinese translations, all wired up

## What's Not Implemented (Despite Earlier Claims)

- **"Global Whale Alert" (live large-transaction feed)** — the UI container for it exists in `index.html`, but there's no code that populates it with real or simulated data. Currently just an empty slot.
- **Price chart history is synthetic** — the backend fetches the real *current* ETH price, then generates a fake 7-day chart by multiplying it by arbitrary factors (0.90x, 0.93x, etc.), not actual historical price data
- The sonar "treasure scan" is a random loot table for fun, not a real on-chain data query — worth being clear about since the marketing copy ("scan for hidden on-chain treasures") could be read as more literal than it is

## Tech Stack

| Layer | Technology |
|---|---|
| Frontend | Vanilla JavaScript, HTML5, Tailwind CSS, Chart.js |
| Web3 | Ethers.js v5 (MetaMask integration) |
| Audio | Web Audio API (synthesized sound effects) |
| Backend | Go, Gin |
| Price Data | CoinGecko public API |

## Getting Started

### Prerequisites
- Go 1.20+
- A browser with the MetaMask extension installed, set to a **testnet** (not mainnet — this app can send real transactions)

### Backend

```bash
cd backend
go mod download
go run main.go
```

Runs on `http://localhost:8080`.

### Frontend

Open `index.html` via a local server (e.g., VS Code's Live Server extension — opening it directly as a `file://` URL may break MetaMask's connection request).

1. Scroll to the bottom and click **"Awaken The Whale"**
2. Connect MetaMask (confirm you're on a testnet first)
3. Explore the dashboard, try the sonar, send a test transaction

## Project Structure

```
nexus-whale/
├── index.html      # landing page + wallet extension UI
├── app.js          # wallet connection, chart rendering, sonar game, i18n
└── backend/
    └── main.go     # ETH price endpoint (CoinGecko proxy)
```

---

*Built with vanilla JavaScript, ethers.js, and Go.*
