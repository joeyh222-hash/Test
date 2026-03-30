# US Company Setup — Research & Decisions

[[Stackr — Venture Overview]] | [[Ventures]]

Research conducted: 2026-03-18 to 2026-03-20
Status: Delaware C-Corp incorporation in progress via Clerky

---

## Context

Stackr, Inc. is building a modular iPhone accessory ecosystem. The first product is a water-cooling device that attaches to an iPhone via MagSafe, using water-cooling technology derived from gaming PCs and EV motor housings. The team needs a US legal entity to:

1. Run a Kickstarter crowdfunding campaign (requires a US bank account and business entity)
2. Attract US investors for future fundraising rounds

---

## Decision 1 — State of Incorporation: Delaware (not Nevada)

**Team's initial suggestion:** Nevada (based on AI advice)

**Decision: Delaware**

Nevada was rejected for the following reasons:
- Nevada's strong asset-protection reputation attracts bad actors, inviting closer scrutiny from investors
- The vast majority of VC-backed startups (90%+) and Fortune 500 companies incorporate in Delaware
- Investors expect and are most comfortable with Delaware corporations
- Nevada only provides tax advantages if the business *actually operates* in Nevada — operating from Taiwan means you'd still owe taxes in operating states anyway

Delaware advantages:
- Legal certainty and flexibility for issuing shares, option plans, and different share classes
- No public disclosure of shareholder, director, or officer names
- Certificate of Incorporation filing fee is only $89
- Entire startup legal ecosystem (attorneys, investors, platforms) built around Delaware corporations

---

## Decision 2 — Entity Type: Delaware C-Corporation (not LLC)

**Decision: Regular Delaware C-Corp**

- LLCs are unsuitable for VC fundraising and Kickstarter campaigns that lead to investor rounds
- C-Corps allow standard equity structures (SAFEs, convertible notes, stock option plans)
- "Public Benefit Corporation" (PBC) was considered and rejected — PBC adds legal obligations to consider stakeholder/public interests alongside shareholder returns, complicating investor relationships. No social mission reason to use it.

---

## Decision 3 — Formation Service: Clerky Lifetime Package ($819)

**Options evaluated:**

| Service | Price | Verdict |
|---|---|---|
| Clerky Pay Per Use | $427 + per-action fees | Worst option — looks cheap but costs most |
| **Clerky Lifetime** | **$819 flat** | **Chosen** |
| Stripe Atlas | $500 + $100/yr | Fast, but too limited post-formation |

**Why Clerky Lifetime:**
- Unlimited SAFEs and convertible notes (Kickstarter backers + future investors)
- Unlimited NDAs (critical for hardware — manufacturer and supplier agreements)
- Unlimited hiring documents and stock option issuances (team equity)
- Unlimited corporate maintenance (adding/changing directors, co-founders)
- Stock plan adoption included
- Attorney-grade legal documents trusted by VCs (used by Coinbase, Gusto)
- $819 flat vs. $1,057+ estimated year-one cost for Pay Per Use

**Why not Stripe Atlas:**
- Only $319 cheaper but significantly less coverage
- No stock option issuances, no unlimited hiring docs, no ongoing maintenance
- Stripe payment integration advantage is irrelevant for hardware sold via Kickstarter
- Hands you templates rather than managed legal workflows after formation

**Supporting files:**
- [[three_way_incorporation_comparison.html]] — visual comparison table
- [[clerky_analysis.docx]] — full Chinese analysis report (v2, team-reviewed)

---

## Step-by-Step Incorporation Process

1. **Choose company name** — must include Corp./Inc./Co./Ltd.; check availability via Delaware Entity Name Search
2. **Appoint registered agent** — required by Delaware law; Clerky handles this (~$125/yr after yr 1)
3. **File Certificate of Incorporation** — $89 filing fee; Clerky handles expedited filing ($203 included)
4. **Get EIN** — start immediately after Certificate of Incorporation is issued; non-US founders use passport number, no SSN needed; takes 4-8 weeks via IRS fax (this is the main bottleneck for banking)
5. **Adopt bylaws and hold organizational board meeting** — appoint officers, document in meeting minutes
6. **Issue founder shares and set up cap table** — internal document, not filed publicly
7. **File 83(b) election** — must be filed with IRS within 30 days of receiving shares; locks in tax basis at lowest value; missing this deadline causes massive tax liability later
8. **Open US business bank account** — Mercury (remote-friendly, no US visit needed); requires EIN + Certificate of Incorporation + passport
9. **Assign all IP to the company** — all patents, design rights, trade secrets, and trademarks must be formally transferred from founders as individuals to the C-Corp via Technology Assignment Agreement; this includes IP developed before incorporation; investors check this during due diligence
10. **Ongoing compliance** — Delaware Annual Franchise Tax Report due March 1 each year; use Assumed Par Value method (not Authorized Shares method) to avoid inflated tax bills; minimum $225

---

## Key Risks & Hidden Costs

### Franchise Tax Trap
Delaware offers two calculation methods. The default Authorized Shares method can produce tax bills in the tens of thousands for startups with many authorized shares but low assets. Always use the **Assumed Par Value method** — it produces a much lower bill for early-stage companies.

### EIN Timeline Bottleneck
As non-US founders (Taiwan), EIN takes 4-8 weeks via IRS fax. Cannot open Mercury bank account without it. Cannot set up Kickstarter payment collection without Mercury. Start EIN application the moment the Certificate of Incorporation is issued — do not wait.

### Foreign Qualification
If the company later hires employees or opens an office in a specific US state (e.g. California), it must register in that state ("foreign qualification"), triggering additional annual fees and tax obligations (e.g. California minimum $800/yr franchise tax).

### IP Transfer Completeness
Any technology, designs, or IP developed before the company was incorporated must be explicitly transferred to the C-Corp via a Technology Assignment Agreement. Missing even one element becomes a deal-killer during investor due diligence.

### Cross-Border Tax (Taiwan side)
A US CPA handles US federal taxes (Form 1120 annually). A Taiwan-side accountant familiar with cross-border structures is also needed for dividends, withholding tax, and fund repatriation from Kickstarter proceeds.

### Kickstarter Fund Repatriation
After Kickstarter funds land in Mercury (USD), a clear path for moving money back to Taiwan (e.g. Wise / international wire) needs to be set up before launch to avoid funds being frozen in the US account.

---

## Recommended Service Stack

| Need | Tool |
|---|---|
| Incorporation + legal docs | Clerky Lifetime Package |
| US business bank account | Mercury |
| Ongoing compliance & bookkeeping | Doola or US startup CPA |
| Taiwan cross-border tax | Taiwan accountant familiar with US-Taiwan structures |

---

## Current Status

- [x] Research completed — Delaware C-Corp confirmed
- [x] Clerky Lifetime Package selected
- [x] Corp type chosen — Regular Delaware C-Corp (not PBC)
- [ ] Certificate of Incorporation filed
- [ ] EIN application submitted
- [ ] 83(b) election filed (30-day deadline from share issuance)
- [ ] Mercury bank account opened
- [ ] IP formally transferred to C-Corp
- [ ] Kickstarter fund repatriation path confirmed
- [ ] US CPA engaged
- [ ] Taiwan cross-border tax advisor engaged
