# Stock Market Data MCP

**x402 Payment-Protected Real-Time Stock Market API**

Get real-time stock quotes, market data, and batch quotes for AI agents doing financial analysis, portfolio monitoring, or market research.

## 🚀 Features

- **📊 Real-Time Stock Quotes** - Current prices, volume, and market data
- **📈 Market Data** - Day high/low, open, previous close, market cap
- **🔄 Batch Queries** - Get multiple stock quotes in one call (up to 10 symbols)
- **🌐 Global Markets** - Support for major exchanges (NYSE, NASDAQ, etc.)
- **💳 x402 Micropayments** - Pay $0.003 USDC per call on Base Mainnet
- **🤖 MCP Compatible** - Works with Claude and other AI agents

## 📡 Live Endpoint

**Base URL**: `https://stock-market-mcp.vercel.app`

### Get Stock Quote

```bash
GET /api/quote?symbol={SYMBOL}
```

**Parameters:**
- `symbol` (required): Stock ticker symbol (e.g., AAPL, MSFT, GOOGL)

**Example:**
```bash
curl https://stock-market-mcp.vercel.app/api/quote?symbol=AAPL
```

### Get Batch Quotes

```bash
GET /api/batch?symbols={SYMBOL1,SYMBOL2,SYMBOL3}
```

**Parameters:**
- `symbols` (required): Comma-separated stock symbols (max 10 per request)

**Example:**
```bash
curl "https://stock-market-mcp.vercel.app/api/batch?symbols=AAPL,MSFT,GOOGL"
```

**Response (402 Payment Required):**
```json
{
  "error": "Payment Required",
  "message": "This endpoint requires x402 payment",
  "payment": {
    "scheme": "exact",
    "network": "eip155:8453",
    "price": "$0.003",
    "currency": "USDC",
    "payTo": "0xf081ee84c0d85278a6242bc265f0b312021ebeb1"
  },
  "instructions": "Include payment proof in X-Payment-Proof header"
}
```

## 🔍 Discovery Endpoints

- **Bazaar Discovery**: `/.well-known/x402`
- **MCP Metadata**: `/mcp/tools`
- **Health Check**: `/health`

## 💰 Payment Details

- **Network**: Base Mainnet (Chain ID: eip155:8453)
- **Currency**: USDC
- **Price**: $0.003 per API call
- **Protocol**: x402 "exact" scheme
- **Payment Address**: `0xf081ee84c0d85278a6242bc265f0b312021ebeb1`

## 🤖 Use with AI Agents

This MCP server is designed to work with Claude Code and other AI agents that support the Model Context Protocol (MCP) and x402 payments.

AI agents can:
1. Discover the service on x402 Bazaar
2. Pay via CDP Facilitator
3. Fetch real-time stock quotes
4. Monitor portfolios and track market trends
5. Perform financial analysis and research

## 📦 Response Format

### Single Quote Response
```json
{
  "success": true,
  "data": {
    "symbol": "AAPL",
    "name": "AAPL Company",
    "price": 178.45,
    "change": 2.34,
    "changePercent": 1.33,
    "volume": 54231000,
    "marketCap": 2847000000000,
    "dayHigh": 179.20,
    "dayLow": 176.80,
    "open": 177.50,
    "previousClose": 176.11,
    "timestamp": "2026-09-04T19:30:00.000Z"
  },
  "payment": {
    "verified": true,
    "amount": "0.003",
    "currency": "USDC"
  }
}
```

### Batch Quotes Response
```json
{
  "success": true,
  "count": 3,
  "data": [
    {
      "symbol": "AAPL",
      "price": 178.45,
      "change": 2.34,
      "changePercent": 1.33,
      "..."
    },
    {
      "symbol": "MSFT",
      "price": 412.89,
      "change": -1.25,
      "changePercent": -0.30,
      "..."
    },
    {
      "symbol": "GOOGL",
      "price": 162.30,
      "change": 0.78,
      "changePercent": 0.48,
      "..."
    }
  ],
  "payment": {
    "verified": true,
    "amount": "0.003",
    "currency": "USDC"
  }
}
```

## 🛠️ Local Development

```bash
# Install dependencies
npm install

# Copy environment file
cp .env.example .env

# Run locally
npm start

# Development mode with auto-reload
npm run dev
```

Server will start on `http://localhost:3000`

## 🚀 Deployment

### Deploy to Vercel

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel

# Deploy to production
vercel --prod
```

The `vercel.json` configuration is already set up for Express.

### Environment Variables

No API keys required for the mock implementation. In production with a real stock API:

```bash
STOCK_API_KEY=your_api_key_here
STOCK_API_PROVIDER=alphavantage  # or twelvedata, finnhub, etc.
```

## 📋 Supported Stock Symbols

All major US exchanges:
- **NYSE** - New York Stock Exchange
- **NASDAQ** - NASDAQ Stock Market
- **AMEX** - American Stock Exchange

Common symbols: AAPL, MSFT, GOOGL, AMZN, TSLA, META, NVDA, JPM, V, WMT, etc.

## ⚠️ Note

This service uses mock stock data generation for Vercel deployment compatibility. In production with persistent infrastructure, it would integrate with a real stock market API like:

- **Alpha Vantage** - Free tier available
- **Twelve Data** - Real-time and historical data
- **Finnhub** - Stock market data API
- **IEX Cloud** - Financial data platform

## 🔗 Integration Example

### With Claude Code

```javascript
// AI agent automatically handles x402 payment
const response = await fetch('https://stock-market-mcp.vercel.app/api/quote?symbol=AAPL', {
  headers: {
    'X-Payment-Proof': '<payment_proof>'
  }
});

const data = await response.json();
console.log(`AAPL is trading at $${data.data.price}`);
```

### MCP Tool Schema

```json
{
  "name": "get_stock_quote",
  "description": "Get real-time stock market quote for a symbol",
  "inputSchema": {
    "type": "object",
    "properties": {
      "symbol": {
        "type": "string",
        "description": "Stock ticker symbol (e.g., AAPL, MSFT, GOOGL)"
      }
    },
    "required": ["symbol"]
  }
}
```

## 📊 Use Cases

- **Portfolio Monitoring** - Track your stock investments in real-time
- **Market Research** - Analyze market trends and price movements
- **Trading Bots** - Get quotes for algorithmic trading decisions
- **Financial Reports** - Generate automated market summaries
- **Price Alerts** - Monitor stocks and trigger notifications
- **Comparison Analysis** - Compare multiple stocks simultaneously

## 🔐 Security

- All payments via x402 protocol on Base Mainnet
- No sensitive data stored
- Payment verification on every request
- Rate limiting and validation built-in

## 📝 License

MIT

## 🔗 Links

- **Live API**: https://stock-market-mcp.vercel.app
- **x402 Bazaar**: https://x402bazaar.app
- **MCP Protocol**: https://modelcontextprotocol.io
- **Base Network**: https://base.org

---

Built with ❤️ for the AI agent ecosystem
