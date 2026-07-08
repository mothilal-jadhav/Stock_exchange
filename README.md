# Stock Exchange Order Matching Engine

A high-performance stock exchange order matching engine implemented in modern C++.

## Features

- Limit Orders
- Market Orders
- Price-Time Priority
- Order Book
- Trade Matching
- Modular Design
- Unit Tests

## Project Structure

```
src/
include/
tests/
docs/
build/
```


## Progress

- Milestone 0 – Project Setup [✅] 
- Milestone 1 – Order Class [ ] 
- Milestone 2 – Order Book [ ] 
- Milestone 3 – Matching Engine [ ] 
- Milestone 4 – Trading Simulation [ ] 
- Milestone 5 – Performance Optimization [ ] 

# Milestone 0 - Project Setup

a main.cpp file which will be our main file we will run
README.md file for the documentation

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

# How do BSE and NSE work?

When we want to buy or sell a stock:

1. We place an order through a broker or trading platform.
2. The stock exchange searches for matching orders.
3. Once a matching order is found, the trade is executed.

---

# Stock Prices

Stock prices change continuously based on **Supply and Demand**.

- More demand for buying → Price increases 📈
- More selling pressure → Price decreases 📉

---

# Order Matching

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

# Settlement

Once an order is executed:

- For buying, money is deducted from your account.
- For selling, money is credited to your account.

Your account must have sufficient balance before placing a buy order.

Both **BSE** and **NSE** currently follow a **T+1 settlement cycle**, meaning settlement takes place on the next trading day after the trade is executed.
