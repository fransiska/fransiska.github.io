---
layout: post
title: Budgeting with ledger-cli while tracking used points
category: ledger
tags: [programming,ledger]
---

I want to be able to track how my expenses matches my budget. And to do that, as [other](https://sachachua.com/blog/2014/11/keeping-financial-score-ledger/) [people](https://emacs.cafe/ledger/emacs/ynab/budgeting/2018/06/12/elbank-ynab.html) also recommended, I used a feature in [ledger](https://www.ledger-cli.org/) called **virtual postings** and **automated transactions**.

### Budgeting

I add a budget for every week

```
2019/10/01 Budget
    [Budget:Yarikuri]                      JPY 6,000
    [Equity:Budget]

2019/10/07 Budget
    [Budget:Yarikuri]                      JPY 7,000
    [Equity:Budget]
```

### Automated transactions

Then these will auto deduct from my budget. By using `Unbudgeted` as suggested [here](https://emacs.cafe/ledger/emacs/ynab/budgeting/2018/06/12/elbank-ynab.html), I can track expenses outside of my budget

```
= /Expenses/
    [Budget:Unbudgeted]  -1.0
    [Equity:Budget]  1.0

= /Expenses:Control:Food/
    [Budget:Yarikuri]  -1.0
    [Budget:Unbudgeted]  1.0

= /Expenses:Control:House/
    [Budget:Yarikuri]  -1.0
    [Budget:Unbudgeted]  1.0
```

### Paying with points

The problem I had was that I don't want payments with points counted towards decreasing my budget but I still want to see the total expenses. I've been calculating manually so far (doh!). I manage this by adding back the budget for every payment I made with points

```
2019/10/01 Supermarket
    Expenses:Control:Food  JPY 100
    Income:Point  JPY -100
    [Budget:Yarikuri]  JPY 100
    [Equity:Budget]  JPY -100
```

### Reporting

So I can have reports on how much I've used my budget so far by:

```
ledger bal ^Budget and not payee Budget
```

And get the remaining budget I have by:

```
ledger bal ^Budget
```

Also the total budget that I have as:

```
ledger reg ^Budget and payee Budget --start-of-week monday -W
```