# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### 🎉 New Features

#### Built-in MCP Server for Claude Desktop
- **Trade with Claude using natural language!**
- Added complete Model Context Protocol (MCP) server implementation
- 20 trading tools exposed to Claude Desktop and other MCP clients
- Zero external dependencies - runs locally with the SDK
- Simple setup: `pip install .[mcp]` and configure Claude Desktop
- Comprehensive documentation in `MCP_SETUP.md`

#### MCP Tools Categories
- **Wallet Management**: Balance checks, fund transfers
- **Market Discovery**: List/search 500+ trading pairs, get detailed specs
- **Leverage Management**: View and set leverage for any symbol
- **Order Management**: Place market/limit orders, view/cancel orders
- **Position Management**: Monitor positions with live PnL, set SL/TP

### Added
- New module: `mudrex.mcp` with FastMCP server implementation
- New tools module: `mudrex.mcp.tools` with 20 trading tools
- New server module: `mudrex.mcp.server` with server initialization
- Run with: `python -m mudrex.mcp`
- Example: `examples/mcp_example.py`
- Test scripts: `test_mcp_setup.py` and `verify_mcp_tools.py`
- Documentation: `MCP_SETUP.md` and `MCP_QUICK_REFERENCE.md`
- Optional dependency group: `[mcp]` in `pyproject.toml`

### Changed
- Updated README with MCP setup instructions
- Added Claude Desktop configuration examples

## [1.1.0] - 2026-01-02

### 🚀 Major Improvements

#### Symbol-First Trading
- **All methods now use trading symbols directly** (e.g., "BTCUSDT", "XRPUSDT")
- No need to look up internal asset IDs anymore
- SDK automatically handles the `is_symbol` query parameter

#### 500+ Assets Support
- `client.assets.list_all()` now fetches **ALL** assets automatically
- Removed pagination limits - get all 500+ trading pairs in one call
- Added `client.assets.exists(symbol)` helper method
- Improved `client.assets.search(query)` to search all assets

### Changed
- `create_market_order()` now uses `symbol` parameter instead of `asset_id`
- `create_limit_order()` now uses `symbol` parameter instead of `asset_id`
- `leverage.get()` and `leverage.set()` now use `symbol` parameter
- `assets.get()` now uses symbol with `is_symbol` flag
- `assets.list_all()` automatically fetches all pages (no pagination limits)
- Order history fetches more results by default

### Fixed
- **XRP trading issue** - Orders now properly use `?is_symbol` parameter
- **Only 10 assets returned** - Now fetches all 500+ assets automatically
- All API calls using symbols now include proper `is_symbol` query param

### Added
- `client.assets.get_by_id()` for advanced users needing asset ID lookups
- `client.assets.exists(symbol)` to check if a symbol is tradable
- Better error messages for symbol-related issues

## [1.0.0] - 2025-12-15

### Added
- Initial release
- Full API coverage for Mudrex Futures Trading API
- Wallet management (spot/futures balance, transfers)
- Asset discovery and specifications
- Leverage management
- Order creation (market/limit), viewing, cancellation, amendment
- Position management (view, close, partial close, reverse)
- Risk management (stop-loss, take-profit)
- Fee history
- Type hints with dataclass models
- Custom exception hierarchy
- Rate limiting support
- Retry logic for rate limit errors
- Context manager support

### Documentation
- Comprehensive README with examples
- Quickstart example
- Trading bot example
- Async trading example
- Error handling example
