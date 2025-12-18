# Exergy Documentation Website

Documentation Website for Exergy Hashrate Heating Systems.

This repository contains the source files for [docs.exergyheat.com](https://docs.exergyheat.com) — guides for integrating bitcoin miners into your smart home.

## What's Inside

- **DIY Guides** — Set up and configure bitcoin miner smart home control yourself
- **Integration Docs** — Custom smart home applications for Canaan Avalon miners, Ocean mining pool, Datum Server and more
- **Automation Blueprints** — Pre-built thermostat control, HVAC integration, time-of-use scheduling and more
- **Dashboard Templates** — Copy and paste dashboards to monitor and control heat and sats from home miners

## Prerequisites

This site is built with [mdBook](https://rust-lang.github.io/mdBook/). You'll need:

- [Rust](https://www.rust-lang.org/tools/install) (to install mdBook)
- mdBook (`cargo install mdbook`)

Or install mdBook directly via Homebrew (macOS):

```bash
brew install mdbook
```

## Getting Started

### Clone the Repository

```bash
git clone https://github.com/exergyheat/docs.git
cd docs
```

### Run Locally

Start the development server with live reload:

```bash
mdbook serve
```

Open [http://localhost:3000](http://localhost:3000) in your browser. Changes to `.md` files auto-refresh.

### Build for Production

```bash
mdbook build
```

Output is generated in the `book/` directory.

## Project Structure

```
.
├── book.toml          # mdBook configuration
├── src/
│   ├── SUMMARY.md     # Navigation structure
│   ├── introduction.md
│   ├── diy/           # DIY guides
│   │   ├── brains/    # Home Assistant setup
│   │   ├── integrations/  # Miner integrations
│   │   ├── blueprints/    # Automation templates
│   │   └── dashboards/    # Dashboard templates
│   └── reference/     # Reference docs
└── theme/             # Custom styling
```

## Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

For bug reports and feature requests, open an issue on GitHub.

## Related Repositories

- [Exergy Home Assistant Integration for Canaan Avalon Miners](https://github.com/exergyheat/ha-integration-canaan-avalon-home)
- [Exergy's OCEAN Pool Integration for Home Assistant](https://github.com/exergyheat/ha-integration-ocean-pool)
- [Exergy's Datum Gateway Integration for Home Assistant](https://github.com/exergyheat/ha-integration-datum-gateway)

See our Home Assistant Integrations Index repository for a complete list.

- [Index of Exergy's Home Assistant Integrations](https://github.com/exergyheat/ha-integrations-index)

## External Links

- **Company Website**: [exergyheat.com](https://exergyheat.com)
- **Documentation**: [docs.exergyheat.com](https://docs.exergyheat.com)
- **Community & Support Forum**: [support.exergyheat.com](https://support.exergyheat.com)
- **Office Demo Site Interface**: [demo.exergyheat.com](https://demo.exergyheat.com)
