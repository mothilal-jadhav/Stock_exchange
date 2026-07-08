# Stock Exchange

before moving towards the project i got to know alot about stock exchange to execute this project

## Questions

- What is a Stock Exchange?
- What is an Order Matching System?

---

## Why do companies go public?

Suppose I have a business that is doing well on a small scale. Now I want to:

- Expand my company to different parts of the country/world.
- Increase the company's valuation.
- Raise a large amount of capital.

### Ways to raise money

- Bank loans
- Investors
- Sell shares of the company to the public

If the first two options don't work out, I can make my company public so that people can buy ownership (shares) in it. This process is called an **Initial Public Offering (IPO).**

### What can a company do with IPO money?

The money raised through an IPO can be used for:

- Opening new branches
- Expanding the business
- Developing new products
- Building infrastructure
- Research & Development (R&D)
- Investing in smaller businesses

A company may also distribute a portion of its profits back to shareholders. This payment is called a **Dividend**.

> Paying dividends is **not mandatory**, but doing so increases investor trust and may encourage investors to buy more shares.

People who did not buy shares during the IPO can later purchase them from existing shareholders by paying the current market price.

---

## Stock Market

The stock market is where people buy and sell tiny ownership pieces (shares) of companies.

Trading happens extremely fast—often **more than 1,000 times per second.**

---

## Major Stock Exchanges

Stock markets exist all over the world.

### New York Stock Exchange (NYSE)

- One of the largest stock exchanges.
- Located on Wall Street, New York City.
- Has existed since **1792**.

### NASDAQ

- Established in **1971**.
- Does not have a physical trading floor.
- Trading happens electronically.

---

## Stock Market Index

The overall performance of the stock market is usually measured using **index**.

An index combines the prices of multiple companies into a single number to represent the market.

Examples:

### S&P 500

- Tracks the **Top 500 companies**.

### Dow Jones

- Tracks only the **Top 30 companies**.

For India, the popular benchmark index is:

- **NIFTY 50**
- **SENSEX**

---

## Index Funds

Instead of buying shares individually, investors can invest in an **Index Fund**.

An Index Fund automatically invests a small portion of your money into every company included in the index.

Example:

- Investing in an **S&P 500 Index Fund** means your money is distributed across the top 500 companies.

---

## Professional Investors

Instead of investing directly through an index fund, people can also give their money to professional investors (brokers/fund managers).

---

A **Stock Exchange** is a place where people buy and sell stocks.

## Indian Stock Exchanges

### Bombay Stock Exchange (BSE)

- Around **5,000 listed companies**

### National Stock Exchange (NSE)

- Around **2,000 listed companies**

---

## How do BSE and NSE work?

When we want to buy or sell a stock:

1. We place an order through a broker or trading platform.
2. The stock exchange searches for matching orders.
3. Once a matching order is found, the trade is executed.

---

## Stock Prices

Stock prices change continuously based on **Supply and Demand**.

- More demand for buying → Price increases 📈
- More selling pressure → Price decreases 📉

---

## Order Matching

Suppose a buy order is placed.

The exchange searches through all available sell orders to find the best matching price.

This process is called **Order Matching**.

---

# Types of Orders

## Market Order

If you want to buy or sell immediately at the current market price, it is called a **Market Order**.

---

## Limit Order

If you specify the exact price at which you want to buy or sell a stock, it is called a **Limit Order**.

---

## Settlement

Once an order is executed:

- For buying, money is deducted from your account.
- For selling, money is credited to your account.

Your account must have sufficient balance before placing a buy order.

Both **BSE** and **NSE** currently follow a **T+1 settlement cycle**, meaning settlement takes place on the next trading day after the trade is executed.


# High Frequency Trading (HFT)

## What is High Frequency Trading (HFT)?

High Frequency Trading (HFT) is a type of algorithmic trading where computers execute buy and sell orders at extremely high speeds.

- Uses algorithms instead of humans
- Executes trades in microseconds or nanoseconds
- Makes tiny profits on millions of trades
- Relies heavily on ultra-low latency systems

Typical trading speed:

- 1,000 to over 1,000,000 trades per second

> **Speed is the most important competitive advantage in HFT.**

---

## HFT Pipeline

```
Market Data Feed
        │
        ▼
Network Delivery
        │
        ▼
System Reception
        │
        ▼
Market Data Feed Handler
        │
        ▼
Order Book
        │
        ▼
Event Queue
        │
        ▼
Trading Strategy / FPGA
        │
        ▼
Risk Engine
        │
        ▼
Smart Order Router
        │
        ▼
Exchange
        │
        ▼
Order Management System (OMS)
        │
        ▼
Monitoring & Metrics
```

---

## Step 1: Market Data Feed

The first stage of every HFT system is receiving live market data from stock exchanges.

The market data contains:

- Current bid prices
- Current ask prices
- Trade prices
- Volume
- Order book updates

The feed arrives continuously in real time.

Example:

```
NASDAQ
NYSE
BSE
NSE
```

---

## Step 2: Network Delivery

The market data must travel from the exchange to the trading firm's servers.

To reduce latency, HFT firms use:

### Multicast Feed

Instead of sending data separately to every client, the exchange broadcasts one stream to everyone.

Benefits:

- Lower bandwidth
- Lower latency
- Same information reaches everyone simultaneously

---

### Co-location

Trading firms place their servers inside or extremely close to the exchange's data center.

Benefits:

- Shorter cable length
- Faster communication
- Lower latency

Instead of:

```
Exchange → Internet → Trading Firm
```

it becomes

```
Exchange
     │
     │
Server Rack
```

---

## Step 3: System Reception

The incoming packets are received using specialized hardware.

Components:

- Ultra-low latency NIC (Network Interface Card)
- Custom TCP/UDP Stack
- Kernel bypass networking

The goal is to process incoming packets in microseconds.

---

### Ultra-low Latency NIC

Unlike a normal network card, an HFT NIC:

- Receives packets faster
- Reduces CPU overhead
- Supports hardware timestamping
- Supports kernel bypass

Examples:

- Solarflare
- Mellanox (NVIDIA)
- Exablaze

---

## Step 4: Market Data Feed Handler

The Feed Handler acts like a translator.

Responsibilities:

- Receive raw exchange packets
- Decode exchange protocol
- Parse binary messages
- Convert into internal objects
- Publish clean market events

Example:

Raw packet

```
0x45A3...
```

↓

Feed Handler

↓

```
Buy Order
Price = 101.25
Quantity = 500
```

---

### Feed Handler Architecture

```
Exchange
      │
      ▼
Feed Handler
      │
      ▼
Market Events
```

The feed handler hides all exchange-specific message formats from the rest of the system.

---

## Step 5: Order Book

After decoding, the system updates the **Order Book**.

The Order Book stores all active buy and sell orders.

Example:

| Buy | Qty | Sell | Qty |
|------|-----|------|-----|
|100.10|200|100.20|150|
|100.05|500|100.25|400|

The Order Book represents the current state of the market.

---

### Why Keep Order Book in Memory?

HFT systems never read the order book from a database.

Instead, it remains entirely in RAM because RAM is thousands of times faster than disk access.

Benefits:

- Extremely fast updates
- No database latency
- Constant-time lookups

---

### Order Book Replication

Most HFT systems maintain multiple copies.

Example:

```
Replica A
Replica B
```

Both remain synchronized using in-memory replication.

Purpose:

- Fault tolerance
- High availability
- Instant failover

If Replica A crashes:

```
Replica B immediately takes over.
```

---

## Step 6: Event Stream

Whenever the order book changes, the update is published as an event.

Examples of events:

- New order
- Cancel order
- Price update
- Trade executed

The system is event-driven.

---

## Lock-Free Event Queue

The event stream is built using lock-free queues.

Why?

Traditional locks slow down concurrent processing.

Benefits:

- No thread blocking
- Higher throughput
- Lower latency
- Better scalability

---

## Nanosecond Timestamping

Every market event is assigned a precise timestamp.

Example:

```
12:35:18.123456789
```

Purpose:

- Maintain exact ordering
- Performance benchmarking
- Latency measurement
- Event replay

Hardware timestamping is preferred over software timestamps.

---

### Precision Matters

In HFT:

Knowing **when** something happened is just as important as knowing **what** happened.

Precise timestamps allow:

- Strategy synchronization
- Fair event ordering
- Accurate latency calculations

---

## FPGA Acceleration

The most latency-critical part of the pipeline is accelerated using FPGA hardware.

---

## What is an FPGA?

FPGA stands for:

**Field Programmable Gate Array**

It is a programmable hardware chip that executes custom logic directly in hardware.

Unlike CPUs, it does not execute operating system instructions or software processes.

---

## Advantages of FPGA

- Hardware-speed execution
- Parallel processing
- Extremely low latency
- Deterministic execution
- No operating system overhead

---

## Tick-to-Trade

Tick:

A new market event arriving from the exchange.

Trade:

Submitting an order back to the exchange.

Tick-to-Trade is the total time taken between:

```
Market Event
      │
      ▼
Decision
      │
      ▼
Order Submission
```

Modern FPGA systems achieve:

- Sub-microsecond Tick-to-Trade latency

---

## FPGA Responsibilities

An FPGA can perform:

- Timestamping
- Market making logic
- Arbitrage detection
- Quote generation
- Decision making
- Order generation

Some firms implement the complete trading strategy inside the FPGA.

---

## FPGA Programming

FPGAs are programmed using hardware description languages.

Common languages:

- Verilog
- VHDL

Unlike C++, these languages describe hardware circuits rather than software instructions.

---

## Software Strategy Engine

Not every strategy runs on FPGA.

Many firms use software-based engines for:

- Market making
- Arbitrage
- Statistical trading
- Machine learning models

The software listens to market events, evaluates the current order book, and generates trading decisions.

---

## Smart Order Router (SOR)

Once a strategy decides to place an order, it is first sent to the Smart Order Router.

The Smart Order Router determines:

- Which exchange to use
- Which venue offers the best price
- Which venue has enough liquidity
- Optimal execution path

Example:

```
Strategy
     │
     ▼
Smart Order Router
     │
     ├── NSE
     ├── BSE
     └── NASDAQ
```

---

## Risk Engine

Speed is important.

Safety is mandatory.

Before sending any order, the Risk Engine checks:

- Position limits
- Maximum order size
- Capital availability
- Duplicate orders
- Strategy limits
- Regulatory compliance

> Speed never overrides safety.

---

## Order Execution

Once approved:

```
Strategy
      │
      ▼
Risk Engine
      │
      ▼
Smart Order Router
      │
      ▼
Exchange
```

The exchange executes the order and returns confirmation.

---

## Order Management System (OMS)

After execution, every order is recorded inside the OMS.

The OMS stores:

- Order ID
- Status
- Fill quantity
- Partial fills
- Rejections
- Execution timestamps
- Exchange route
- Trade history

The OMS acts as the central nervous system of the trading platform.

---

## Monitoring & Metrics

Running alongside the trading pipeline is a monitoring system.

It continuously collects:

- Latency
- CPU usage
- Memory usage
- Network latency
- Packet loss
- Throughput
- Hardware health

This ensures the platform remains healthy and performs optimally.

---

## Complete HFT Architecture

```
Market Data Feed
        │
        ▼
Co-location
        │
        ▼
Ultra-low Latency NIC
        │
        ▼
Feed Handler
        │
        ▼
Order Book (RAM)
        │
        ▼
Replica A / Replica B
        │
        ▼
Event Stream
        │
        ▼
Lock-Free Queue
        │
        ▼
Nanosecond Timestamp
        │
        ▼
FPGA / Strategy Engine
        │
        ▼
Risk Engine
        │
        ▼
Smart Order Router
        │
        ▼
Exchange
        │
        ▼
Order Management System
        │
        ▼
Monitoring Dashboard
```

---

# Key Terms

| Term | Description |
|------|-------------|
| HFT | High Frequency Trading |
| Feed Handler | Converts raw exchange packets into usable market events |
| Order Book | In-memory representation of active buy/sell orders |
| Market Data Feed | Live stream of exchange data |
| Co-location | Servers placed close to the exchange |
| NIC | Network Interface Card |
| FPGA | Field Programmable Gate Array |
| Tick | Incoming market update |
| Tick-to-Trade | Time from receiving a market event to sending an order |
| Event Queue | Queue carrying market events between components |
| Lock-Free Queue | High-performance concurrent queue without thread locks |
| OMS | Order Management System |
| SOR | Smart Order Router |
| Risk Engine | Validates orders before submission |
| Replica | Backup copy of the Order Book |
| Timestamping | Recording the exact arrival time of events |
