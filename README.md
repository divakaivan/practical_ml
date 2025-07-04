## Goal of this notebook

'Most companies don’t care about the fancy ML metrics. They don’t care about increasing a model’s accuracy from 94% to 94.2% unless it moves some business metrics.' - Chip Huyen, Designing Machine Learning Systems

Chip Huyen (among many other practitioners) highlights that ML models hold value only when they drive meaningful benefits for the business. The goal of this notebook is to encourage you to develop a model with a focus on enhancing a relevant business metric, rather than just optimizing traditional ML metrics.

## Problem Setting

If you are an adult, chances are you have heard about credit scores (or FICO scores). Credit scores are a numerical representation of an individual's creditworthiness. They are used by lenders to assess how likely someone is to repay borrowed money or manage financial responsibilities. A credit score, usually ranging from 300 to 850, is based on various factors, including payment history, total debt, length of credit history, types of credit accounts, and recent credit inquiries. Higher scores typically indicate lower risk, making it easier to secure loans, credit cards, or favorable interest rates. Conversely, lower scores can make credit access challenging and more expensive.

Experian is one of the most famous and reliable provider of these FICO scores, and banks typically purchase these scores to assess the credit risk of potential borrowers and make lending decisions.

Imagine we are a seasoned bank with lots of data on our customers and a big loan portfolio. A stakeholder comes to you and says that given the bank needs to cut costs. Given the bank's long history and data availability, the stakeholder believes that we can cut costs by not purchasing FICO scores from providers but calculate them ourselves.

In the provided dataset there is information about 7500 loans, each with information about the borrower, the loan, and the respective FICO score which we have from Experian. We will assume that the FICO scores are the actual truth (for transparency - I generated them using a custom PD model. If you want to learn how to do that check the Udemy course below). Given that information, the stakeholder would like you to create a model that estimates the FICO scores with the least difference between your model's output and the actual FICO scores.

The stakeholder would also like to know how the bank's expecte loss will be affected in case your model's FICO scores differ from the original FICO scores. Don't worry, help on calculating this will be provided.

If you want to learn more about credit risk modelling, I recommend this course on Udemy

Here is a guide on how to think about different FICO scores:

https://www.beyondfinance.com/blog/wp-content/uploads/2021/09/FICO-score-range.png

![image](https://github.com/user-attachments/assets/465d2fde-c573-4aa1-9eea-5230bb88b31f)

# Results (from the end of the notebook)

## Key Metrics

| Metric                                                          | Model 1 (Current) | Model 2 (Challenger) |
| --------------------------------------------------------------- | ----------------- | -------------------- |
| % of loans for which the FICO score is overshot by more than 5% | 67.23%            | 0.03%                |
| % of loans outside the required 5% margin                       | 64.20%            | 0.013333             |
| Expected Loss                                                   | \$9,909,298.07    | \$7,871,616.41       |
| Model Reserve Ratio                                             | 10.83%            | 8.61%                |

> Regulators require the bank to keep a minimum of 8% of our loan portfolio as reserves.

## FICO Score Range Comparison

This table shows the percentage difference in FICO score predictions by range. Values outside the ±5% range are areas of concern, with Model 2 demonstrating significant improvement over Model 1 in accuracy.

| FICO Score Range      | Model 1 Difference (%) | Model 2 Difference (%) |
| --------------------- | ---------------------- | ---------------------- |
| Poor (300–579)        | -100.00                | -0.61                  |
| Fair (580–669)        | 90.74                  | 0.03                   |
| Good (670–739)        | -100.00                | 0.83                   |
| Very Good (740–799)   | -100.00                | 4.41                   |
| Exceptional (800–850) | NaN                    | NaN                    |

## Analysis

1. **Accuracy Improvement:**
   Model 2 significantly reduces the percentage of loans overshot by more than 5%, bringing it down to just 0.03% compared to Model 1’s 67.23%. Additionally, Model 2 maintains a high level of accuracy across all FICO score ranges, with no difference exceeding ±5%.

2. **Expected Loss Reduction:**
   Model 2 decreases the expected loss from \$9.91M to \$7.87M, an improvement that could yield substantial financial benefits.

3. **Reserve Ratio Compliance:**
   Model 2’s reserve ratio of 8.61% meets the regulatory requirement of keeping at least 8% in reserves and is closer to this minimum requirement than Model 1’s 10.83%, optimizing capital allocation.

## Conclusion

The challenger model (Model 2) demonstrates clear advantages in prediction accuracy, financial efficiency, and regulatory compliance. Transitioning to Model 2 is recommended to optimize reserve allocation while maintaining adherence to regulatory requirements.

