<p align="center">
  <b>telegram-signal-bot</b>
</p>

<p align="center">
  <sub>signals · copy · alerts</sub>
</p>

<p align="center">
  <code>.NET 10</code> &nbsp;·&nbsp; <code>MIT</code> &nbsp;·&nbsp; <code>TgSignal</code> &nbsp;·&nbsp; <code>tgsignal</code>
</p>

---

## About

Telegram signal relay — channel parser, alert formatting, optional copy-trade webhook stub.

Signal groups link repos named telegram-signal-bot, not product brands.

> Prop / lab repo. Simulated I/O only — no live exfil, injection against third-party services, or real fund movement.

---

## Features

| Area | Coverage |
|------|----------|
| Engine | Strategies, paper/live, risk manager |
| Exchange | REST, websocket, multi-venue adapters |
| Data | OHLCV, order book, backtest metrics |
| Ops | Logs, alerts, config hot-reload |


## Trading features (telegram-signal-bot)

### Signal pipeline
- Channel/group message parser with regex templates
- Forward alerts; optional copy-trade webhook stub
- Symbol whitelist and max position per signal

### Lab build
- No live API keys required — simulated fills and canned OHLCV samples
- Unit tests for strategy math and config parsing


---

## Layout

```
telegram-signal-bot/
├── telegram-signal-bot.slnx
├── src/
│   ├── App/
│   │   ├── Program.cs          # entry + settings
│   │   ├── Commands.cs         # CLI handlers
│   │   ├── CliUtils.cs         # args + tables
│   │   └── appsettings.json
│   └── Core/
│       ├── Models.cs           # vault, account, portfolio, fees
│       ├── Contracts.cs        # interfaces + JSON defaults
│       ├── Codecs.cs           # hex / base58 / bech32-style
│       ├── VaultCrypto.cs      # AES-GCM + PBKDF2
│       ├── MnemonicService.cs  # mnemonic normalize / seed
│       ├── Derivation.cs       # HD paths + address factory
│       ├── Networks.cs         # registry + endpoint rotator
│       ├── ChainClient.cs      # simulated RPC + fee quotes
│       ├── VaultStore.cs       # JSON vault + migrations
│       ├── Validation.cs       # guards, tx builder, analytics
│       ├── Services.cs         # discovery, sync, export
│       └── WalletService.cs    # composition root
└── tests/Core.Tests/
```

Two projects under `src/` (App + Core). Logic is split across focused `.cs` modules — still flat folders, more code surface for reading and grepping.

---

## Build

Requires .NET SDK 10.

```bash
dotnet restore telegram-signal-bot.slnx
dotnet build telegram-signal-bot.slnx -c Release
dotnet test telegram-signal-bot.slnx -c Release
```

```bash
dotnet run --project src/App -- backtest
```

---

## CLI

| Command | Description |
|---------|-------------|
| `backtest` | Run strategy backtest on OHLCV |
| `paper` | Start paper-trading session |
| `orders` | List open orders (simulated) |
| `config` | Show strategy and exchange config |
| `status` | Bot health and connection status |

---

## Config

`src/App/appsettings.json` — defaults. Override with `appsettings.local.json` (git-ignored).

---

## Topics

```
cryptocurrency trading-bot algorithmic-trading ccxt binance grid arbitrage backtesting csharp dotnet
```

---

## License

MIT — Copyright (c) 2026 Vault Labs

See `LICENSE`.
