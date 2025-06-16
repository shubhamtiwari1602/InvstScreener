# 🏦 **Corporate Finance Analysis & Investment Screening Tool**

## **📊 Project Overview**

This comprehensive financial analysis tool applies core corporate finance principles to evaluate publicly traded companies and generate investment recommendations. Built in Python, the system integrates financial statement analysis, ratio calculations, time value of money concepts, capital budgeting tools, and portfolio optimization to provide institutional-grade investment insights.

**Key Features:**
- 📈 **Financial Statement Analysis** - Automated processing of Income Statements, Balance Sheets, and Cash Flow Statements
- 🧮 **Comprehensive Ratio Analysis** - 20+ financial ratios across liquidity, profitability, leverage, efficiency, and market metrics
- ⏰ **Time Value of Money Calculator** - NPV, IRR, payback period, and present/future value calculations
- 🏗️ **Capital Budgeting Evaluator** - Multi-criteria project assessment with automated recommendations
- 🔍 **Investment Screening System** - Systematic company evaluation with 5-category scoring framework
- 🎯 **Portfolio Optimization Engine** - Risk-adjusted allocation recommendations based on financial health metrics

---

## 🎯 **Detailed System Architecture**

### **1. Data Structure & Management**

```python
# Financial data organized by company with comprehensive metrics
companies_data = {
    'TICKER': {
        'company_name': 'Company Name',
        'income_statement': {
            'revenue': float,
            'cost_of_goods_sold': float,
            'gross_profit': float,
            'operating_expenses': float,
            'operating_income': float,
            'interest_expense': float,
            'tax_expense': float,
            'net_income': float
        },
        'balance_sheet': {
            'current_assets': float,
            'total_assets': float,
            'current_liabilities': float,
            'total_liabilities': float,
            'total_equity': float,
            'cash': float,
            'inventory': float,
            'accounts_receivable': float
        },
        'cash_flow': {
            'operating_cash_flow': float,
            'investing_cash_flow': float,
            'financing_cash_flow': float,
            'free_cash_flow': float,
            'capital_expenditure': float
        },
        'market_data': {
            'stock_price': float,
            'shares_outstanding': float,
            'beta': float
        }
    }
}
```

**Logic**: Structured data architecture enables systematic analysis across all financial statement components while maintaining data integrity through validation functions.

---

### **2. Financial Ratio Analysis System**

#### **A. Liquidity Ratios (Short-term Financial Health)**

```python
# Current Ratio - Ability to pay short-term debts
current_ratio = current_assets / current_liabilities

# Quick Ratio - Liquidity excluding inventory
quick_ratio = (current_assets - inventory) / current_liabilities

# Cash Ratio - Most conservative liquidity measure
cash_ratio = cash / current_liabilities

# Acid Test Ratio - Liquid assets coverage
acid_test_ratio = (cash + accounts_receivable) / current_liabilities
```

**Interpretation Logic:**
- `Current Ratio ≥ 2.0` → Strong liquidity
- `1.0 ≤ Current Ratio < 2.0` → Adequate liquidity  
- `Current Ratio < 1.0` → Liquidity concerns

#### **B. Profitability Ratios (Earnings Generation Efficiency)**

```python
# Gross Profit Margin - Production efficiency
gross_profit_margin = (gross_profit / revenue) × 100

# Operating Profit Margin - Operational efficiency
operating_profit_margin = (operating_income / revenue) × 100

# Net Profit Margin - Overall profitability
net_profit_margin = (net_income / revenue) × 100

# Return on Assets (ROA) - Asset utilization efficiency
return_on_assets = (net_income / total_assets) × 100

# Return on Equity (ROE) - Shareholder value creation
return_on_equity = (net_income / total_equity) × 100

# Earnings Per Share - Per-share profitability
earnings_per_share = net_income / shares_outstanding
```

**Profitability Assessment Logic:**
- `Net Margin ≥ 20%` → Excellent profitability
- `10% ≤ Net Margin < 20%` → Good profitability
- `5% ≤ Net Margin < 10%` → Average profitability
- `Net Margin < 5%` → Poor profitability

#### **C. Leverage Ratios (Financial Risk Assessment)**

```python
# Debt-to-Equity Ratio - Financial leverage
debt_to_equity = total_liabilities / total_equity

# Debt-to-Assets Ratio - Asset financing structure
debt_to_assets = total_liabilities / total_assets

# Equity Ratio - Ownership financing proportion
equity_ratio = total_equity / total_assets

# Interest Coverage Ratio - Debt servicing ability
interest_coverage = operating_income / interest_expense
```

**Risk Assessment Logic:**
- `D/E ≤ 0.3` → Conservative leverage
- `0.3 < D/E ≤ 0.6` → Moderate leverage
- `D/E > 0.6` → High leverage (increased risk)

#### **D. Efficiency Ratios (Asset Management)**

```python
# Asset Turnover - Revenue generation per asset dollar
asset_turnover = revenue / total_assets

# Inventory Turnover - Inventory management efficiency
inventory_turnover = cost_of_goods_sold / inventory

# Receivables Turnover - Collection efficiency
receivables_turnover = revenue / accounts_receivable

# Days Sales Outstanding - Average collection period
days_sales_outstanding = (accounts_receivable / revenue) × 365
```

#### **E. Market Ratios (Valuation Metrics)**

```python
# Price-to-Earnings Ratio - Valuation relative to earnings
price_to_earnings = stock_price / earnings_per_share

# Price-to-Book Ratio - Market vs book value
price_to_book = stock_price / book_value_per_share

# Market-to-Book Ratio - Market capitalization vs equity
market_to_book = market_capitalization / total_equity

# Book Value Per Share - Equity value per share
book_value_per_share = total_equity / shares_outstanding
```

---

### **3. Time Value of Money & Capital Budgeting**

#### **A. Present Value Calculations**

```python
# Present Value Formula
present_value = future_value / (1 + discount_rate)^years

# Present Value of Annuity
pv_annuity = payment × [(1 - (1 + r)^(-n)) / r]

# Future Value Formula  
future_value = present_value × (1 + discount_rate)^years

# Future Value of Annuity
fv_annuity = payment × [((1 + r)^n - 1) / r]
```

#### **B. Capital Budgeting Metrics**

```python
# Net Present Value (NPV)
def calculate_npv(initial_investment, cash_flows, discount_rate):
    npv = -initial_investment
    for year, cash_flow in enumerate(cash_flows, 1):
        pv = cash_flow / (1 + discount_rate)^year
        npv += pv
    return npv

# Internal Rate of Return (IRR) - Rate where NPV = 0
def calculate_irr(initial_investment, cash_flows):
    # Uses iterative approach to find rate where NPV = 0
    # Binary search between 0% and 100% until convergence

# Payback Period
def payback_period(initial_investment, cash_flows):
    cumulative_cash_flow = 0
    for year, cash_flow in enumerate(cash_flows, 1):
        cumulative_cash_flow += cash_flow
        if cumulative_cash_flow >= initial_investment:
            # Linear interpolation for exact payback
            previous_cumulative = cumulative_cash_flow - cash_flow
            fraction = (initial_investment - previous_cumulative) / cash_flow
            return year - 1 + fraction

# Profitability Index
profitability_index = pv_of_cash_flows / initial_investment
```

**Investment Decision Logic:**
- `NPV > 0` → Accept project
- `IRR > Required Return` → Accept project  
- `Payback Period ≤ Target Period` → Accept project
- `Profitability Index > 1.0` → Accept project

---

### **4. Investment Screening System**

#### **Screening Criteria Framework**

```python
screening_criteria = {
    'liquidity': {
        'min_current_ratio': 1.0,
        'weight': 20%
    },
    'profitability': {
        'min_net_margin': 10.0,    # 10%
        'min_roe': 15.0,           # 15%
        'weight': 30%
    },
    'leverage': {
        'max_debt_to_equity': 1.0,
        'min_interest_coverage': 5.0,
        'weight': 25%
    },
    'efficiency': {
        'min_asset_turnover': 0.5,
        'weight': 15%
    },
    'valuation': {
        'max_pe_ratio': 30.0,
        'max_pb_ratio': 5.0,
        'weight': 10%
    }
}
```

#### **Scoring Algorithm**

```python
def calculate_company_score(ratios, criteria):
    score = 0
    max_score = 5  # 5 categories
    
    # Test each category
    if ratios['current_ratio'] >= criteria['liquidity']['min_current_ratio']:
        score += 1
    
    # Profitability requires both margin AND ROE criteria
    if (ratios['net_margin'] >= criteria['profitability']['min_net_margin'] and 
        ratios['roe'] >= criteria['profitability']['min_roe']):
        score += 1
    
    # Leverage requires both D/E AND interest coverage
    if (ratios['debt_to_equity'] <= criteria['leverage']['max_debt_to_equity'] and
        ratios['interest_coverage'] >= criteria['leverage']['min_interest_coverage']):
        score += 1
    
    if ratios['asset_turnover'] >= criteria['efficiency']['min_asset_turnover']:
        score += 1
    
    # Valuation requires both P/E AND P/B within limits
    if (ratios['pe_ratio'] <= criteria['valuation']['max_pe_ratio'] and
        ratios['pb_ratio'] <= criteria['valuation']['max_pb_ratio']):
        score += 1
    
    return score, max_score
```

**Investment Rating Logic:**
- `Score ≥ 4/5 (80%)` → 🟢 STRONG BUY
- `Score = 3/5 (60%)` → 🟡 BUY  
- `Score = 2/5 (40%)` → ⚪ HOLD
- `Score ≤ 1/5 (20%)` → 🔴 AVOID

---

### **5. Portfolio Optimization Engine**

#### **Risk-Adjusted Weight Calculation**

```python
def calculate_portfolio_weights(screening_results):
    # Filter qualified companies (score ≥ 3)
    qualified = [company for company in screening_results if company['score'] >= 3]
    
    portfolio_weights = {}
    
    for company in qualified:
        # Base weight from screening score
        base_weight = company['score'] / total_qualified_score
        
        # Risk adjustment (favor lower leverage)
        risk_adjustment = 1 / (1 + company['debt_to_equity'])
        
        # Profitability adjustment (favor higher ROE)
        profit_adjustment = company['roe'] / 100
        
        # Combined weight
        adjusted_weight = base_weight × risk_adjustment × profit_adjustment
        portfolio_weights[company['ticker']] = adjusted_weight
    
    # Normalize weights to sum to 100%
    total_weight = sum(portfolio_weights.values())
    normalized_weights = {ticker: weight/total_weight 
                         for ticker, weight in portfolio_weights.items()}
    
    return normalized_weights
```

#### **Portfolio Risk Metrics**

```python
# Portfolio Beta (Systematic Risk)
portfolio_beta = Σ(weight_i × beta_i) for all holdings

# Expected Portfolio Return (CAPM)
expected_return = risk_free_rate + portfolio_beta × market_risk_premium

# Risk Assessment
if portfolio_beta > 1.2:
    risk_level = "High Risk"
elif portfolio_beta > 0.8:
    risk_level = "Moderate Risk"  
else:
    risk_level = "Conservative"
```

---

## **📐 Mathematical Formulas Reference**

### **Financial Ratios**
```
Current Ratio = Current Assets ÷ Current Liabilities
Quick Ratio = (Current Assets - Inventory) ÷ Current Liabilities  
Net Profit Margin = (Net Income ÷ Revenue) × 100
ROA = (Net Income ÷ Total Assets) × 100
ROE = (Net Income ÷ Total Equity) × 100
Debt-to-Equity = Total Liabilities ÷ Total Equity
Asset Turnover = Revenue ÷ Total Assets
P/E Ratio = Stock Price ÷ Earnings Per Share
```

### **Time Value of Money**
```
PV = FV ÷ (1 + r)ⁿ
FV = PV × (1 + r)ⁿ
PV Annuity = PMT × [(1 - (1 + r)⁻ⁿ) ÷ r]
NPV = Σ[CFₜ ÷ (1 + r)ᵗ] - Initial Investment
IRR: Rate where NPV = 0
PI = PV of Cash Flows ÷ Initial Investment
```

### **Portfolio Optimization**
```
Portfolio Beta = Σ(wᵢ × βᵢ)
Expected Return = Rf + βₚ × (Rm - Rf)
Portfolio Weight = (Score × Risk Adj × Profit Adj) ÷ Total
```

---

## **🎯 Key Business Logic**

### **Investment Decision Framework**
1. **Screen companies** using 5-category financial health assessment
2. **Rank by composite score** incorporating multiple financial metrics
3. **Apply risk adjustments** based on leverage and volatility measures
4. **Optimize portfolio allocation** using risk-adjusted weighting
5. **Generate recommendations** with clear buy/hold/avoid ratings

### **Risk Management Integration**
- **Liquidity Risk**: Current ratio and cash position analysis
- **Credit Risk**: Debt-to-equity and interest coverage evaluation  
- **Market Risk**: Beta analysis and valuation metrics
- **Operational Risk**: Profitability trends and efficiency ratios

### **Valuation Methodology**
- **Relative Valuation**: P/E and P/B ratio comparisons
- **Absolute Valuation**: DCF concepts through NPV calculations
- **Risk-Adjusted Returns**: Beta-adjusted expected return calculations
- **Multi-Factor Analysis**: Comprehensive screening across 5 dimensions

---

## **🚀 Technical Implementation**

**Programming Concepts:**
- Object-Oriented Design with specialized analysis classes
- Modular architecture for scalability and maintenance
- Automated report generation with formatted output
- Error handling and data validation throughout
- Mathematical computations using NumPy-style operations

**Financial Engineering:**
- Systematic ratio calculation and interpretation
- Time value of money applications in capital budgeting
- Risk-return optimization for portfolio construction
- Multi-criteria decision analysis for investment screening

This tool demonstrates practical application of corporate finance theory through systematic quantitative analysis, providing institutional-quality investment insights through automated financial modeling.
