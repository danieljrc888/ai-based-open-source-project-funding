# AI-Powered Open Source Project Funding

A decentralized platform that uses AI to analyze and rank open source projects for funding allocation. Built on [GenLayer](https://www.genlayer.com/) — a blockchain protocol where smart contracts can natively execute AI inference and fetch web data.

## How It Works

1. **Submit a project** — provide a name, description, and GitHub repository URL
2. **AI ranks the project** — the GenLayer Intelligent Contract scrapes the repo, analyzes it with an LLM, and scores it 0–100 based on sustainability and impact
3. **Validator consensus** — multiple validators independently run the AI analysis; results are accepted only if scores agree within a 5% tolerance band
4. **Leaderboard** — all ranked projects are displayed sorted by score, creating a transparent funding priority list

## Architecture

```
┌─────────────────────┐      ┌──────────────────────────────────┐
│   Vue 3 Frontend    │      │   GenLayer Intelligent Contract   │
│                     │      │                                  │
│  ProjectForm ──────────►   │  submit_project()                │
│  ProjectList  ◄────────    │  rank_project()                  │
│  Leaderboard  ◄────────    │    ├─ gl.get_webpage() (scrape)  │
│                     │      │    ├─ gl.exec_prompt() (AI)      │
│  genlayer-js SDK    │      │    └─ eq_principle (consensus)   │
└─────────────────────┘      └──────────────────────────────────┘
```

There is no traditional backend — the Intelligent Contract **is** the backend. AI inference, web scraping, and data storage all happen on-chain within GenLayer validators.

## Key Features

- **On-chain AI analysis** — LLM evaluates contributor count, code quality, issue resolution, and project impact directly within the smart contract
- **Decentralized consensus** — comparative validation ensures consistent AI scoring across validators
- **Transparent ranking** — scores and AI reasoning are stored on-chain and viewable by anyone
- **One-rank rule** — each project can only be ranked once, preventing score manipulation

## Tech Stack

| Layer | Technology |
|-------|-----------|
| Intelligent Contract | Python, GenLayer SDK |
| Frontend | Vue 3 (Composition API), Vite, Tailwind CSS |
| Blockchain SDK | genlayer-js |
| AI/Consensus | GenLayer equivalence principle (comparative validation) |

## Getting Started

### Prerequisites

- Node.js 18+
- Python 3.10+
- [GenLayer Studio](https://studio.genlayer.com/) or a local GenLayer simulator

### Deploy the Contract

```bash
pip install -r requirements.txt
cp .env.sample .env
# Configure JSON-RPC connection in .env
```

Deploy `contracts/open_source_project_funding.py` to GenLayer via Studio or CLI and note the contract address.

### Run the Frontend

```bash
cd app
npm install
cp .env.sample .env
# Set VITE_CONTRACT_ADDRESS to your deployed contract address
npm run dev
```

The app will be available at `http://localhost:5173`.
