# Getting Listed on x402 Bazaar

## Overview

Your Stock Market MCP will automatically appear on **https://x402bazaar.app** after your first paid call settles through the CDP Facilitator. No registration form needed!

## Current Status

✅ **Live Deployment**: https://stock-market-mcp-delta.vercel.app
✅ **x402 Discovery**: `/.well-known/x402` endpoint active
✅ **MCP Compatible**: `/mcp/tools` endpoint ready
✅ **Payment Ready**: Returns 402 for unpaid requests

## How to Get Listed

### Step 1: Validate Your Endpoint ✅ DONE

Your endpoint is live and properly configured:

```bash
curl -i https://stock-market-mcp-delta.vercel.app/api/quote?symbol=AAPL
```

Should return:
```
HTTP/1.1 402 Payment Required
```

### Step 2: Wait for First Paid Call

Once a user or AI agent completes a paid call through the CDP Facilitator:
1. Payment settles on Base Mainnet
2. CDP automatically catalogs your endpoint
3. Your service appears on x402bazaar.app within minutes

### Step 3: Optional - Manual Testing

You can test with CDP's x402 tooling or wait for organic discovery.

## Discovery Confirmation

After a paid call, check the `EXTENSION-RESPONSES` header in the settle response (base64-encoded JSON):

- `"success"` - Metadata cataloged ✅
- `"processing"` - Being cataloged asynchronously ⏳
- `"rejected"` - Check `rejectedReason` for validation errors ❌

## Requirements for Listing

### Required:
- ✅ Public HTTPS URL
- ✅ Returns `402 Payment Required`
- ✅ Valid x402 discovery endpoint
- ✅ Accepts payments through CDP Facilitator
- ✅ Base/USDC only

### For Featured/Curated Tier:
- Live mainnet payments
- ≥99% availability (30-day window)
- Complete input schemas and examples
- Clear agent-focused description
- Passes platform health probes

## Your Endpoint Details

**URL**: `https://stock-market-mcp-delta.vercel.app/api/quote`  
**Method**: `GET`  
**Price**: $0.003 USDC  
**Network**: Base Mainnet (eip155:8453)  
**Payment Address**: `0xf081ee84c0d85278a6242bc265f0b312021ebeb1`

**Primary Endpoints**:
1. `/api/quote?symbol=AAPL` - Get single stock quote
2. `/api/batch?symbols=AAPL,MSFT,GOOGL` - Get batch quotes (up to 10)

**Example Request**:
```bash
GET /api/quote?symbol=AAPL
```

**Example Response**:
```json
{
  "success": true,
  "data": {
    "symbol": "AAPL",
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
  }
}
```

## Maintenance

To stay listed:
- Complete at least 1 paid call every 30 days
- Maintain ≥99% uptime
- Continue returning 402 for unpaid requests
- Respond to health probes

**Auto-removal happens when**:
- No settlements for 30+ days
- Health probes fail consistently
- Endpoint stops returning 402

## Tracking Your Listing

Once listed, find your endpoint on:
- **Browse**: https://x402bazaar.app
- **Search by tags**: stocks, finance, market, trading, quotes, portfolio, mcp
- **Your payment address**: Search by `0xf081ee84c0d85278a6242bc265f0b312021ebeb1`

## Use Cases for AI Agents

Your Stock Market MCP is perfect for:
- **Portfolio Monitoring** - Track investment performance in real-time
- **Market Research** - Analyze trends and price movements
- **Trading Bots** - Get quotes for algorithmic decisions
- **Financial Reports** - Generate automated market summaries
- **Price Alerts** - Monitor stocks and trigger notifications
- **Comparison Analysis** - Compare multiple stocks simultaneously

## Metadata Quality

**Description**: 
"Real-time stock market quotes and data for AI agents. Get current prices, volume, market cap, and daily metrics for any stock symbol on major exchanges (NYSE, NASDAQ). Perfect for portfolio monitoring, market research, and financial analysis."

**Tags**:
- stocks
- finance
- market-data
- trading
- quotes
- portfolio
- mcp
- real-time
- nasdaq
- nyse

## Support

- **x402 Docs**: https://docs.cdp.coinbase.com/x402
- **GitHub**: https://github.com/coinbase/x402
- **Bazaar**: https://x402bazaar.app
- **Live API**: https://stock-market-mcp-delta.vercel.app

## Next Steps

✅ Deployment complete
✅ All endpoints validated
⏳ Waiting for first paid call to auto-list on Bazaar

Your MCP is ready! Share your URL with AI agents or wait for organic discovery through x402 Bazaar.

---

**Live now!** Visit https://stock-market-mcp-delta.vercel.app to see your landing page. First paid call will automatically list you on x402bazaar.app! 🚀
