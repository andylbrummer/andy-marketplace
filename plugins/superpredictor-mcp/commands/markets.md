---
name: markets
description: Query prediction markets and compare forecasts
---

# Prediction Markets

Query Metaculus, Polymarket, and other prediction markets to inform your forecasts.

## Usage

Search prediction markets, get current prices, and compare your forecast to consensus.

## Examples

**Search Metaculus:**
```
/superpredictor-mcp:markets search metaculus "AI" "2025"
```

**Get market price:**
```
/superpredictor-mcp:markets polymarket "US election"
```

**Compare to consensus:**
```
/superpredictor-mcp:markets compare my 70% to metaculus question 12345
```

## MCP Tools

**Search Metaculus:**
```
Call: mcp__superpredictor-mcp__search_metaculus
Parameters: {
  "query": "<search query>",
  "status": "<open|closed|all>"
}
```

**Get Metaculus question:**
```
Call: mcp__superpredictor-mcp__get_metaculus_question
Parameters: {
  "question_id": <question ID>
}
```

**Search Polymarket:**
```
Call: mcp__superpredictor-mcp__search_polymarket
Parameters: {
  "query": "<search query>"
}
```

**Get Polymarket market:**
```
Call: mcp__superpredictor-mcp__get_polymarket_market
Parameters: {
  "market_id": "<market identifier>"
}
```

**Compare to markets:**
```
Call: mcp__superpredictor-mcp__compare_to_markets
Parameters: {
  "my_forecast": <your probability>,
  "market_type": "<metaculus|polymarket>",
  "market_id": "<market/question ID>"
}
```

## Market Sources

| Source | Type | Notes |
|--------|------|-------|
| Metaculus | Community forecasts | Good for long-term questions |
| Polymarket | Real-money markets | High liquidity events |
