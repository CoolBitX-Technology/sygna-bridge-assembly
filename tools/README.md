# Currency Management Tools

## 📋 Overview

This directory contains tools for managing cryptocurrency data in the new format. The primary tool is `add_currency.go`, which intelligently adds currency information.

---

## 🚀 add_currency.go - Add Currency Tool

### Introduction

`add_currency.go` is a command-line tool that simplifies adding new cryptocurrencies. It automatically determines whether to add a new currency or append a platform to an existing one based on the currency symbol and name.

### Quick Start

```bash
cd tools
go run add_currency.go -symbol BTC -name Bitcoin -platform bitcoin --token-address native --coingecko-id bitcoin
```

---

## 📖 Usage

### Basic Syntax

```bash
go run add_currency.go \
  -symbol SYMBOL \
  -name "Currency Name" \
  -platform PLATFORM \
  [--token-address ADDRESS] \
  [--coingecko-id ID]
```


### How to Find CoinGecko ID

Check CoinGecko's site:
https://www.coingecko.com/en/coins/bitcoin

Scroll down to find the `API ID` field in the `Info` block on the left-hand side.

---

## 🎯 Behavior Logic

The tool uses **exact name matching** to determine whether to add a new currency or update an existing one:

### Scenario 1: Add Platform to Existing Currency

**When:** A currency with the **exact same symbol and name** already exists in the file.

**Action:** Adds the new platform to the existing currency object.

**⚠️ Important:** If the platform already exists, the tool will return an error to prevent accidental overwrites.

---

### Scenario 2: Create New Currency

**When:** No currency with the same symbol exists (file doesn't exist).

**Action:** Creates a new currency object with a new UUID.

---

### Scenario 3: Same Symbol, Different Name

**When:** The file exists, but no currency has the exact same name.

**Action:** Adds a new currency object to the existing file (same symbol, different name).

---

### CoinGecko Mapping

When a new currency is created (not just adding a platform), the tool updates `../coingecko_id/mapping_v2.json`:

```json
[
  {
    "currency_id": "uuid-of-currency",
    "coingecko_id": "bitcoin"
  }
]
```