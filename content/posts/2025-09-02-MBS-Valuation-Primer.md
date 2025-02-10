---
title: A first approach into MBS valuation. Modeling a Mortgage-Backed Security (MBS) with Simplified Assumptions
date: 2025-02-09
---
**Modeling a Mortgage-Backed Security (MBS) with Simplified Assumptions**

### Introduction

Mortgage-Backed Securities (MBS) are critical financial instruments that pool mortgages and distribute their cash flows to different tranches of investors. In this project, we developed an automated framework for pricing and stress-testing an MBS under different economic scenarios. Our goal was to dynamically model default and prepayment risks, discount cash flows using a yield curve, and determine fair market prices for the different tranches.

### Key Components of the Model

1. **Synthetic Mortgage Pool Generation**
    - Created a structured mortgage pool divided into three SES-based tranches: Senior (A), Mezzanine (B), and Junior (C).
    - Each tranche has distinct loan characteristics, interest rates, default, and prepayment assumptions.
2. **Sensitivity Analysis & Stress Testing**
    - Applied a range of shocks to SES_A default rates and propagated their effects on SES_B and SES_C using deterministic and stochastic functions.
    - Ensured logical propagation of prepayment rates, with constraints to maintain values within [0,1].
3. **Cash Flow Calculation & Discounting**
    - Computed expected cash flows based on default and prepayment-adjusted loan payments.
    - Discounted cash flows using a yield curve spanning maturities from 1 to 30 years.
4. **Risk Metrics Computation**
    - **Present Value (PV) of Cash Flows**: The discounted sum of expected future cash flows.
    - **Weighted Average Life (WAL)**: The duration-weighted expected cash flow measure.
    - **Effective Yield**: The implied return on investment for each tranche.
    - **Fair Market Price**: Computed using a risk-adjusted yield for each tranche.

### Insights from the Model
By systematically varying default shocks, we observed that:
- Higher SES_A default rates increased risk for all tranches, especially SES_C.
- The fair market price of tranches declined as shocks intensified, reflecting increased investor risk.
- Senior tranches remained relatively stable due to lower default exposure, while Junior tranches were highly sensitive to shocks.

### Implications for MBS Pricing
The computed fair market price for each tranche allows the bank to determine optimal selling prices:
- **Tranche A (Senior)**: Lower risk, priced closer to PV of cash flows with a small risk premium.
- **Tranche B (Mezzanine)**: Moderate risk, priced with a higher discount.
- **Tranche C (Junior)**: High-risk investors demand significant discounts.

### Conclusion
This project demonstrates how an automated framework can enhance MBS pricing, risk assessment, and stress testing. By integrating realistic yield curves and dynamic default propagation, our model provides valuable insights for structuring and selling MBS tranches under varying market conditions.


![](/personal-website/images/20250209221951.png)