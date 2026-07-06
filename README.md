# checkout-leak-analytics

THE CHECKOUT LEAK — DATA STORYTELLING & STATISTICAL VALIDATION

Task 4 of 4 in an end-to-end e-commerce data analytics project — turning raw transactional data into a business narrative, backed by statistical testing.
View the full presentation: Checkout_Leak_Data_Story.pptx
OBJECTIVE
To synthesize the findings from Parts 1–3 (data cleaning, exploratory analysis, and SQL-based reporting) into a single, decision-ready business story — and validate the key claims with formal hypothesis testing rather than intuition alone.
DATASET
Source: ecommerce-sales.sql (https://github.com/habibakhan-3932/ecommerce-sales.sql) — a relational dataset of:

customers — 100 rows — Customer profiles across 90+ countries
products — 50 rows — Products across 6 categories
orders — 200 rows — Order headers, Jan–Nov 2025
order_items — 408 rows — Line-item level quantity & price
payments — 200 rows — Payment method, amount, and status

KEY FINDINGS

Revenue is healthy and diversified. Beauty ($81.3K) and Home & Kitchen ($55.7K) lead a 6-category catalog; order volume held steady across 11 months.
65.1% of transaction value ($58,263) is trapped in Failed or Pending payment status — this is the single biggest lever in the business, far larger than any category-level revenue gap.
Success rate varies sharply by payment method: Debit Card (43.4%) outperforms Net Banking (25.6%) by nearly 18 points.
Average order value does not differ by payment method — confirming this is a conversion problem, not a customer-spend problem.

HYPOTHESIS TESTING
Test 1 — Chi-Square Test of Independence
H0: Payment outcome is independent of payment method
H1: Payment outcome depends on payment method
Result: chi-square = 10.88, df = 6, p = 0.092
Interpretation: Not significant at the 5% threshold, but directionally suggestive (p < 0.10) — a strong candidate for a controlled A/B test with a larger sample.
Test 2 — Independent Samples T-Test
H0: Mean order value is equal for Debit Card and UPI
H1: Mean order value differs between Debit Card and UPI
Result: t = 0.210, p = 0.834, 95% CI of mean difference: [-$101.51, +$125.85]
Interpretation: Fail to reject H0 — no significant difference in spend by method.
RECOMMENDATIONS

Run a checkout A/B test on Net Banking / UPI flows, targeting parity with Debit Card's 43.4% success rate.
Add real-time retry / alternate-method prompts when a payment fails.
Reconcile the $24,935 sitting in "Pending" status with payment gateway logs.
Re-run the chi-square test after 90 days of additional data to confirm significance.

TOOLS USED
Python (pandas, scipy), SQL, PowerPoint (data storytelling deck), Statistical hypothesis testing (Chi-square, T-test)
REPO STRUCTURE
