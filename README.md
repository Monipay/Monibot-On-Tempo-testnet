<p align="center">
  <img src="src/assets/monipay-m-logo.png" alt="MoniPay Logo" width="80" />
</p>

<h1 align="center">MoniPay × Tempo</h1>

<p align="center">
  <strong>True Gasless Payments. Autonomous AI Agents. Zero Compromise.</strong>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Tempo_Hackathon-2025-blue?style=for-the-badge" alt="Tempo Hackathon" />
  <img src="https://img.shields.io/badge/Live_on-Testnet-green?style=for-the-badge" alt="Live on Testnet" />
  <img src="https://img.shields.io/badge/Contracts-Verified-brightgreen?style=for-the-badge" alt="Verified Contracts" />
  <img src="https://img.shields.io/badge/Gas_Fees-$0.00-orange?style=for-the-badge" alt="Zero Gas" />
</p>

<p align="center">
  <a href="https://monipay.xyz/tempo">🚀 Live Demo</a> ·
  <a href="https://x.com/monibot">🤖 @monibot</a> ·
  <a href="https://x.com/monipay_xyz">🐦 @monipay_xyz</a> ·
  <a href="https://explore.tempo.xyz/address/0x78A824fDE7Ee3E69B2e2Ee52d1136EECD76749fc">📜 Verified Contract</a>
</p>

---

## 📊 Quick Stats

| Metric | Value |
|--------|-------|
| **Transactions Processed** | 100+ |
| **Active Users** | 50+ |
| **Gas Fees Paid by Users** | **$0.00** (100% sponsored) |
| **Avg Transaction Time** | ~30 seconds |
| **Chains Supported** | Base · BSC · **Tempo** |
| **Smart Contracts Deployed** | 6 (2 per chain) |
| **Bot Uptime** | 99.9% |

---

## 🔴 The Problem

Crypto payments have a **99% abandonment rate**. Users are expected to:

- Install wallet extensions (MetaMask, Phantom)
- Safeguard 12-word seed phrases
- Acquire gas tokens on the correct chain
- Understand hex addresses like `0x4a3b...7f2e`
- Navigate confirmation dialogs and chain switching
- Pay unpredictable gas fees on every transaction

**The result?** Billions in stablecoins sit idle while the world still runs on cash and card rails.

Meanwhile, "gasless" solutions on existing chains are **workarounds** — EIP-712 relayers that deduct fees from the payment amount. The user still loses money. It's not gasless. It's hidden-gas.

---

## ✅ The Solution: MoniPay on Tempo

MoniPay is a **decentralized, terminal-free payment protocol** that makes blockchain invisible. With Tempo's payment-native primitives, we've built the first platform where gasless isn't a marketing claim — it's a protocol-level guarantee.

```
"@monibot send $5 to @alice"

→ AI parses intent
→ Resolves MoniTag to wallet address
→ Signs transaction with local key
→ Tempo sponsor pays ALL fees natively
→ $5.00 arrives. Not $4.85. Not $4.95. Five dollars.

30 seconds. Zero fees. No app opened.
```

### What Makes This Different

| | Traditional Crypto | "Gasless" Solutions | **MoniPay on Tempo** |
|---|---|---|---|
| **Setup** | Wallet extension + seed phrase | Wallet extension + relayer | **Tweet a command** |
| **Gas Fees** | User pays $0.15-$2.00 | Hidden in amount (user loses 1-5%) | **$0.00 — protocol-sponsored** |
| **Recipient Gets** | Amount minus gas | Amount minus hidden fee | **100% of amount** |
| **Identity** | 0x4a3b...7f2e | 0x4a3b...7f2e | **@alice** |
| **Automation** | Manual | Semi-automated | **Fully autonomous AI agent** |

---

## ⚡ Why Tempo Changes Everything

Tempo isn't another EVM fork. It's a blockchain **designed for payments**. Every feature we previously hacked around is now a native primitive:

### 1. Native Fee Sponsorship
```
Before (Base/BSC):                    After (Tempo):
─────────────────                     ────────────────
User signs EIP-712 message            User signs transaction
Backend relayer submits tx            feePayer: sponsor ← native!
Relayer pays gas, deducts from amt    Sponsor pays, user gets 100%
Complex, fragile, lossy               Simple, robust, lossless
```

### 2. TIP-20 Transfer Memos
Payment references stored **on-chain**, not in an external database:
```javascript
await contract.transfer(recipient, amount, "Invoice #1234 — Campaign grant");
// Memo is permanent, verifiable, on-chain
```

### 3. Batch Calls (Atomic Multi-Recipient)
Campaign with 5 winners:
- **Base/BSC**: 5 separate transactions → 5 blocks → ~5 minutes
- **Tempo**: 1 batch transaction → 1 block → ~30 seconds

### 4. 2D Nonces (Concurrent Processing)
Multiple campaigns running simultaneously:
- **Base/BSC**: Sequential nonces → one transaction at a time
- **Tempo**: Independent nonce keys → 3-10x parallel throughput

### 5. No Native Gas Token
Users never need to acquire ETH or BNB. Fees are paid in the same stablecoin they're already using. One token. Zero confusion.

---

## 🏗️ Architecture

```
┌──────────────────────────────────────────────────────────────┐
│                    USER TOUCHPOINTS                          │
│                                                              │
│   🐦 Twitter: "@monibot send $5 to @alice"                  │
│   🌐 Web App: monipay.xyz/tempo                             │
│   📱 PWA: Install on any smartphone                         │
└────────────────────────┬─────────────────────────────────────┘
                         │
                         ▼
┌──────────────────────────────────────────────────────────────┐
│                MoniPay Frontend (React + Vite)               │
│                                                              │
│   • Local key generation (AES-256-GCM encrypted)            │
│   • Multi-chain wallet (Base / BSC / Tempo)                 │
│   • MoniTag identity system (@username → 0x address)        │
│   • Tempo route: /tempo (hackathon-optimized)               │
└────────────────────────┬─────────────────────────────────────┘
                         │
            ┌────────────┼────────────┐
            ▼            ▼            ▼
┌────────────────┐ ┌──────────┐ ┌─────────────────┐
│  Supabase Edge │ │  Tempo   │ │  MoniBot Suite  │
│   Functions    │ │  RPC     │ │  (3 Services)   │
│                │ │          │ │                  │
│ • relay-payment│ │ Chain ID │ │ • Worker Bot    │
│ • check-paytag │ │  42431   │ │ • Reply Bot     │
│ • monibot-ai   │ │          │ │ • Admin AI      │
└────────┬───────┘ └────┬─────┘ └────────┬────────┘
         │              │                │
         ▼              ▼                ▼
┌──────────────────────────────────────────────────────────────┐
│              Tempo Testnet (Moderato)                        │
│                                                              │
│   MoniBotRouter:  0x78A824fDE7Ee3E69B2e2Ee52d1136EECD76749fc│
│   MoniPayRouter:  0xa39C3B7e02686cf7F226337525515c694318BDb9│
│   AlphaUSD:       0x20c0000000000000000000000000000000000001  │
│   Treasury:       0xDC9B47551734bE984D7Aa2a365251E002f8FF2D7│
│                                                              │
│   Features: Fee Sponsorship · Batch Calls · 2D Nonces       │
└──────────────────────────────────────────────────────────────┘
```

### 🤖 MoniBot: The Autonomous Financial Agent

MoniBot isn't a chatbot. It's a **financial agent** — an autonomous entity that lives on Twitter, reasons with Gemini AI, and executes on-chain without human intervention.

```
User tweets "@monibot send $5 to @alice on tempo"
                    │
                    ▼
  ┌─────────────────────────────────────┐
  │     WORKER BOT (Silent Executor)    │
  │  1. Poll Twitter API (30s cycle)    │
  │  2. Parse: amount=$5, target=alice  │
  │  3. Resolve MoniTag → Tempo address │
  │  4. Build Tempo Transaction         │
  │  5. Fee sponsor pays ALL gas        │
  │  6. Execute on MoniBotRouter        │
  │  7. Log to shared ledger            │
  └──────────────────┬──────────────────┘
                     │
                     ▼
  ┌─────────────────────────────────────┐
  │     REPLY BOT (Social Voice)        │
  │  1. Poll unreplied transactions     │
  │  2. Generate AI reply (Gemini)      │
  │  3. Include Tempo explorer link     │
  │  4. Post confirmation to Twitter    │
  └─────────────────────────────────────┘
```

**Tempo-Specific Bot Advantages:**
- **Batch Grants**: 5 campaign winners processed in 1 atomic transaction
- **2D Nonces**: Multiple campaigns execute concurrently (no queue bottleneck)
- **Fee Sponsorship**: Sponsor wallet pays fees at protocol level — cleaner than EIP-712 relay
- **Transfer Memos**: Campaign IDs and grant references stored on-chain via TIP-20

### AI-Powered Grant Evaluation

MoniBot uses **Gemini AI** to evaluate every campaign reply against an anti-gaming rubric:

| Grant Tier | Amount | Criteria |
|------------|--------|----------|
| REJECT | $0.00 | Spam, bots, copy-paste, self-tagging |
| MINIMAL | $0.10 | Basic participation |
| STANDARD | $0.25 | Genuine engagement |
| QUALITY | $0.50 | Thoughtful contribution |
| MAXIMUM | $1.00 | Outstanding (rare) |

---

## 🎯 Key Features

### 1. Social P2P Payments
Tweet a command. Money moves. No app required.

```
@monibot send $5 to @alice on tempo
```

- **30-second confirmation** from tweet to settlement
- **Zero fees** — Tempo sponsor pays everything
- **On-chain memo** — "P2P payment" stored via TIP-20
- **Multi-recipient** — `@monibot send $1 each to @alice, @bob, @charlie`

### 2. Autonomous Campaign Grants
AI-scheduled, AI-evaluated, fully autonomous giveaways:

- Bot posts campaign tweet with budget & rules
- Users reply to participate
- Gemini AI evaluates quality, blocks spam
- AlphaUSD distributed on Tempo (batch execution)
- Confirmation replies posted automatically

### 3. The Invisible Wallet
No seed phrases. No wallet extensions. No blockchain literacy required.

```
On Signup:
  1. Generate random Ethereum private key (client-side)
  2. Encrypt with user's PIN (AES-256-GCM, PBKDF2 100K iterations)
  3. Store encrypted key in device storage
  4. Map MoniTag → wallet address

The user created a username and a PIN.
Everything else was invisible.
```

### 4. Multi-Chain Intelligence
MoniPay operates across **three chains simultaneously**:

| Chain | Token | Decimals | Gas Model |
|-------|-------|----------|-----------|
| **Base** | USDC | 6 | EIP-712 Relayer |
| **BSC** | USDT | 18 | EIP-712 Relayer |
| **Tempo** | AlphaUSD (αUSD) | 18 | **Native Fee Sponsorship** ✨ |

Auto-routing logic selects the optimal chain based on user balance and network conditions. Users never need to think about which chain they're on.

### 5. Merchant POS (Zero Hardware)
Any smartphone becomes a point-of-sale terminal:
- Quick Add product grid for one-tap checkout
- QR Scan-to-Pay
- Invoice system with MoniTag delivery
- Revenue analytics dashboard
- Customer CRM

---

## 🔧 Technical Implementation

### Smart Contracts

**MoniBotRouter** — Social transaction executor with on-chain verification:

| Network | Address | Explorer |
|---------|---------|----------|
| **Tempo Testnet** | `0x78A824fDE7Ee3E69B2e2Ee52d1136EECD76749fc` | [View ↗](https://explore.tempo.xyz/address/0x78A824fDE7Ee3E69B2e2Ee52d1136EECD76749fc) |
| Base Mainnet | `0xBEE37c2f3Ce9a48D498FC0D47629a1E10356A516` | [View ↗](https://basescan.org/address/0xBEE37c2f3Ce9a48D498FC0D47629a1E10356A516) |
| BSC Mainnet | `0x9EED3cF32690FfFaD0b8BB44CaC65B3B801c832E` | [View ↗](https://bscscan.com/address/0x9EED3cF32690FfFaD0b8BB44CaC65B3B801c832E) |

**MoniPayRouter** — In-app gasless payment router:

| Network | Address | Explorer |
|---------|---------|----------|
| **Tempo Testnet** | `0xa39C3B7e02686cf7F226337525515c694318BDb9` | [View ↗](https://explore.tempo.xyz/address/0xa39C3B7e02686cf7F226337525515c694318BDb9) |
| Base Mainnet | `0x4048d18F71E723647f83B61202362425C5a7D2c0` | [View ↗](https://basescan.org/address/0x4048d18F71E723647f83B61202362425C5a7D2c0) |
| BSC Mainnet | `0x557285AbC46038E898d90eB00943Ff42c4Fbcb54` | [View ↗](https://bscscan.com/address/0x557285AbC46038E898d90eB00943Ff42c4Fbcb54) |

**On-chain security features:**
- Nonce-based replay protection
- Tweet ID stored on-chain (prevents double-execution)
- Campaign + recipient tracking (prevents duplicate grants)
- Hardcoded treasury address
- Maximum fee cap (500 bps)
- Executor whitelist (only authorized bot wallets)

### Tempo-Specific Optimizations

**Fee Sponsorship Implementation:**
```javascript
// Tempo: Native protocol feature
const hash = await client.sendTransactionSync({
  account: userAccount,
  feePayer: sponsorAccount,  // Sponsor pays ALL fees
  calls: [{
    to: alphaUsdAddress,
    data: encodeFunctionData({
      abi: TIP20_ABI,
      functionName: 'transfer',
      args: [recipient, parseUnits('5', 18), toBytes('P2P payment')]
    })
  }]
});
// User received $5.00. Not $4.85. Five dollars.
```

**Batch Campaign Distributions:**
```javascript
// 5 grants in 1 atomic transaction
const calls = recipients.map(r => ({
  to: routerAddress,
  data: encodeFunctionData({
    abi: ROUTER_ABI,
    functionName: 'executeGrant',
    args: [r.address, r.amount, campaignId]
  })
}));

await client.sendTransactionSync({
  account: executor,
  feePayer: sponsor,
  calls  // All 5 grants, atomically
});
```

**Concurrent Campaign Processing (2D Nonces):**
```javascript
// Process 3 campaigns in parallel
const [hash1, hash2, hash3] = await Promise.all([
  client.sendTransactionSync({ nonceKey: 1n, feePayer: sponsor, calls: campaign1Calls }),
  client.sendTransactionSync({ nonceKey: 2n, feePayer: sponsor, calls: campaign2Calls }),
  client.sendTransactionSync({ nonceKey: 3n, feePayer: sponsor, calls: campaign3Calls }),
]);
// 3 campaigns processed simultaneously. Not sequentially.
```

### Security Model

| Layer | Mechanism |
|-------|-----------|
| **Key Encryption** | AES-256-GCM with PBKDF2 (100K iterations) |
| **Request Signing** | HMAC-SHA256 on every mutation |
| **Database** | Row-Level Security — all writes gated through Edge Functions |
| **Rate Limiting** | Per-endpoint throttling (10 tx/min) |
| **PIN Protection** | Escalating lockouts (1min → 5min → 15min → 1hr) |
| **On-chain Guards** | Nonce replay protection, tweet ID dedup, executor whitelist |

**The Walkaway Test:** Because keys are client-side and settlement is on-chain, if MoniPay's servers disappear tomorrow, every user's funds remain accessible. That's the point.

---

## 🚀 Try It Now

### Web App
1. Visit **[monipay.xyz/tempo](https://monipay.xyz/tempo)**
2. Click **"Get Started"** — create a MoniTag and PIN (no MetaMask needed)
3. Fund your wallet at **[faucet.tempo.xyz](https://faucet.tempo.xyz)**
4. Send a payment to any MoniTag — gasless, instant

### Via Twitter
1. Create your MoniPay account at [monipay.xyz/tempo](https://monipay.xyz/tempo)
2. Link your Twitter handle in Settings
3. Tweet: **`@monibot send $1 to @yourfriend on tempo`**
4. Watch it arrive in ~30 seconds
5. Verify on [explore.tempo.xyz](https://explore.tempo.xyz)

---

## 📂 Repository Structure

```
monipay/
├── src/                              # React frontend (PWA)
│   ├── pages/
│   │   ├── Tempo.tsx                 # Tempo hackathon route
│   │   └── Index.tsx                 # Main landing page
│   ├── components/
│   │   ├── TempoLanding.tsx          # Tempo-branded hero
│   │   ├── Dashboard.tsx             # Multi-chain dashboard
│   │   ├── NetworkToggle.tsx         # Chain switcher
│   │   └── FundWalletModal/          # Deposit + faucet
│   ├── config/
│   │   └── chains.ts                 # Multi-chain configuration
│   ├── contexts/
│   │   └── PayTagContext.tsx         # Global wallet state
│   └── lib/
│       └── wallet.ts                 # Key generation + encryption
├── contracts/
│   ├── MoniBotRouter.sol             # Bot execution router
│   ├── MoniPayRouter.sol             # Payment router (Base)
│   └── MoniPayRouter.bsc.sol         # Payment router (BSC)
├── worker-bot-tempo/                 # Tempo worker bot (Node.js)
├── reply-bot-tempo/                  # Tempo reply bot (Node.js)
├── worker-bot/                       # Base worker bot
├── worker-bot-bsc/                   # BSC worker bot
├── vp-social/                        # Base reply agent
├── reply-bot-bsc/                    # BSC reply agent
├── supabase/
│   └── functions/                    # Edge Functions (Deno)
│       ├── relay-payment/            # Multi-chain gasless relayer
│       ├── monibot-ai/               # AI reply generation
│       ├── monibot-campaign/         # Campaign management
│       └── ...                       # Products, orders, invoices
└── chrome-extension/                 # Browser extension (Manifest V3)
```

---

## 🛠️ Setup & Installation

### Prerequisites
- Node.js 18+
- Tempo testnet funds ([faucet.tempo.xyz](https://faucet.tempo.xyz))
- Twitter account (for MoniBot interactions)

### Frontend
```bash
git clone https://github.com/Monipay/monipay
cd monipay
npm install

# Environment
echo "VITE_ENABLE_TEMPO=true" >> .env

npm run dev
# Visit http://localhost:5173/tempo
```

### Worker Bot (Tempo)
```bash
cd worker-bot-tempo
npm install

# Configure .env
SUPABASE_URL=your_supabase_url
SUPABASE_SERVICE_KEY=your_service_key
TEMPO_EXECUTOR_PRIVATE_KEY=your_executor_key
TEMPO_SPONSOR_PRIVATE_KEY=your_sponsor_key
TWITTER_CLIENT_ID=your_twitter_client_id
TWITTER_CLIENT_SECRET=your_twitter_client_secret

npm start
```

### Reply Bot (Tempo)
```bash
cd reply-bot-tempo
npm install
# Same Supabase + Twitter credentials
npm start
```

---

## 🏆 Hackathon Tracks

### Primary: Consumer Payments & Social Finance
- **Real users** sending real money via tweets
- **100+ transactions** processed on Tempo testnet
- **Autonomous** campaign management (no human in the loop)
- **True gasless UX** powered by Tempo's native fee sponsorship
- **Multi-chain intelligence** across Base, BSC, and Tempo

### Secondary: AI Agents & Automation
- **Three-agent architecture** (Worker, Reply, Admin)
- **Autonomous decision-making** — AI evaluates, executes, confirms
- **Anti-gaming intelligence** — Gemini-powered spam detection
- **Strategic campaign scheduling** with temporal task queue

---

## 🗺️ Roadmap

### Tempo Mainnet Launch
- Migrate contracts to Tempo mainnet
- Production-scale campaigns ($1,000+ budgets)
- Real stablecoin settlement

### Enhanced Tempo Features
- Scheduled payments (`validAfter` / `validBefore`)
- Passkey authentication (WebAuthn)
- Advanced batch operations
- Cross-chain atomic swaps (Tempo ↔ Base ↔ BSC)

### Ecosystem Growth
- Merchant POS dashboard on Tempo
- Recurring subscription payments
- Invoice generation with TIP-20 memos
- Chrome Extension for merchant checkout

---

## 👤 Team

**Solo Builder**: [@wallstreetjade](https://x.com/wallstreetjade)

Full-stack engineer building MoniPay to solve real payment problems in emerging markets. The thesis: the best financial infrastructure is the one nobody notices.

---

## 🔗 Links

| Resource | URL |
|----------|-----|
| **Tempo Demo** | [monipay.xyz/tempo](https://monipay.xyz/tempo) |
| **Production App** | [monipay.xyz](https://monipay.xyz) |
| **MoniBot (Twitter)** | [@monibot](https://x.com/monibot) |
| **MoniPay (Twitter)** | [@monipay_xyz](https://x.com/monipay_xyz) |
| **MoniBotRouter (Tempo)** | [explore.tempo.xyz ↗](https://explore.tempo.xyz/address/0x78A824fDE7Ee3E69B2e2Ee52d1136EECD76749fc) |
| **MoniPayRouter (Tempo)** | [explore.tempo.xyz ↗](https://explore.tempo.xyz/address/0xa39C3B7e02686cf7F226337525515c694318BDb9) |
| **Tempo Worker Bot** | [GitHub ↗](https://github.com/Monipay/worker-bot-tempo-TESTNET/) |
| **Tempo Reply Bot** | [GitHub ↗](https://github.com/Monipay/reply-bot-tempo-TESTNET) |
| **Technical Docs** | [DOCUMENTATION.md](DOCUMENTATION.md) |

---

## 📜 License

MIT License — see [LICENSE](LICENSE) for details.

---

<p align="center">
  <strong>Built with 🖤 on Tempo Testnet</strong><br/><br/>
  <em>"The best financial infrastructure is the one nobody notices."</em><br/><br/>
  MoniPay is a Hammer. Not a Dishwasher.<br/>
  And on Tempo, the hammer hits harder.
</p>
