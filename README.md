# Churn Analysis README

## Business Problem
Customer churn is a significant challenge for businesses, leading to revenue loss and increased acquisition costs. Understanding the factors contributing to churn helps in developing retention strategies and improving customer satisfaction.

## Churn by Categorical Features
- Churn rates vary between different area codes, with area code 415 having the highest churn rate and area code 408 having the lowest churn rate.
- Customers without a voice mail plan had a higher churn rate compared to customers with a voice mail plan.
- Customers without an international plan had a higher churn rate compared to customers with an international plan.

## Multivariate Analysis
### Correlation Heatmap
```python
plt.figure(figsize=(14, 8))  # Increase figure size
sns.heatmap(df_numerical.corr(), annot=True, cmap="coolwarm", fmt=".2f", linewidths=0.5, annot_kws={"size": 8})
plt.title("Feature Correlation Heatmap")
plt.xticks(rotation=45, ha="right")  # Rotate x-axis labels
plt.yticks(rotation=0)  # Keep y-axis labels horizontal
plt.tight_layout()  # Adjust layout
plt.show()
```
The correlation heatmap reveals:
- Strong positive correlations between certain features, suggesting direct proportionality.
- Moderate correlations between call duration, total calls, and overall charges.
- Weak or no correlation among some features, indicating independence.
- Negative correlations between certain usage metrics, suggesting inverse relationships.

### Pairplot of Top Features vs. Churn
```python
sns.pairplot(df[top_features], hue="churn", palette="pastel")
plt.show()
```
Key observations:
- Strong linear relationships between `total_day_minutes` and `total_charge`.
- Differences in feature distributions between churned and non-churned customers.
- Churned customers appear more spread across certain feature ranges.

## Data Preprocessing
### Checking Highly Correlated Features
- **Blue shades**: Negative correlations.
- **White**: No correlation.
- **Red shades**: Positive correlations.

### Scaling and Encoding
Data is scaled and encoded appropriately before modeling.

## Modeling
### Splitting the Data
- Target variable: `Churn`
- **Class imbalance**: 85.5% non-churners, 14.5% churners.
- **Handling imbalance**: SMOTE (Synthetic Minority Over-sampling Technique).

### Baseline Model: Decision Tree
#### Evaluating Before Tuning
- Accuracy: 94.72%
- Recall: 81.25%
- Precision: 82.11%
- F1-score: 81.68%

#### After Tuning
- Accuracy: 93.67%
- Recall: 86.46%
- Precision: 74.11%
- F1-score: 79.81%
- Trade-off: Improved recall at the expense of precision.

### Logistic Regression, Random Forest, and Gradient Boosting
#### Random Forest
- **Before Tuning**: Accuracy 93.36%, Recall 80.21%, Precision 75.49%.
- **After Tuning**: Accuracy 93.36%, Recall 54.17%, Precision 100% (high false negatives).

#### Logistic Regression
- **Before Tuning**: Accuracy 83.41%, Recall 64.58%, Precision 44.93%.
- **After Tuning**: Accuracy 87.33%, Recall 31.25%, Precision 62.50% (more false negatives).

#### Gradient Boosting (Best Model)
- **Before Tuning**: Accuracy 97.59%, Recall 86.46%, Precision 96.51%.
- **After Tuning**: Accuracy 96.68%, Recall 81.25%, Precision 95.12%.
- **Conclusion**: Best balance between precision and recall.

## Model Evaluation
### ROC Curve Takeaways
- **Gradient Boosting (AUC = 0.94)** → Best Model
- **Random Forest (AUC = 0.93)** → Second-Best Model
- **Logistic Regression (AUC = 0.85)** → Lowest Performance

## Feature Importance Analysis
### Key Features and Their Importance
1. **Customer Service Calls** (Most Important Feature)
   - Strongly linked to churn.
   - **Business Insight**: Improve customer support and resolve complaints efficiently.
2. **Total Charge**
   - High charges correlate with churn.
   - **Business Insight**: Offer loyalty programs or pricing adjustments.
3. **International Plan**
   - Subscribers to international plans have a higher churn rate.
   - **Business Insight**: Improve international plan competitiveness.
4. **Voicemail Usage**
   - Possible unmet communication needs.
   - **Business Insight**: Promote chat-based or unlimited calling plans.
5. **Total Talk Time**
   - High usage correlates with churn.
   - **Business Insight**: Target high-usage customers with special offers.
6. **International Charges & Calls**
   - Higher charges increase churn likelihood.
   - **Business Insight**: Offer competitive international plans.
7. **Account Length**
   - Surprisingly low importance.
   - **Business Insight**: Focus on behavioral patterns rather than account age.

## Recommendations
1. **Improve Customer Support**
   - Address common complaints proactively.
   - Enhance support quality and reduce customer frustration.
2. **Target High-Charge Customers**
   - Offer loyalty rewards, exclusive discounts, or personalized plans.
3. **Re-Evaluate International Plans**
   - Conduct surveys to understand dissatisfaction.
   - Provide flexible and competitive pricing.
4. **Enhance Retention Efforts Based on Usage**
   - Offer tailored plans for high-usage customers.
5. **Monitor Voicemail Users**
   - Investigate communication needs and offer suitable alternatives.



