# **Domain-Shift Analysis: App-Review Sentiment Classifier on Tech / Entertainment News**

> **TODO** — fill in each section. The autograder verifies length and section presence; the TA reads the content.

## **Prediction distribution**

How many positive / neutral / negative predictions did the model make on the 1,033 tech news articles? A small markdown table with three rows.

| Label | Count |
|---|---|
| positive | 54 rows |
| neutral | 427 rows |
| negative | 552 rows |

## **Confidence distribution**

Mean and median predicted probability; proportion with probability > 0.9; proportion with probability < 0.6. A histogram is welcome but optional.

* Mean Confidence Probability: 0.557
* Median Confidence Probability: 0.534
* Proportion with Probability > 0.9: 0.00% (0 / 1033 rows)
* Proportion with Probability < 0.6: 76.57% (791 / 1033 rows)

## **Five qualitative examples**

Pick five articles that, together, illustrate domain shift. For each:
- Article id and a short excerpt
- Predicted label and probability
- Your interpretation: reasonable / suspicious / clearly wrong; what domain-shift pattern it exposes.

### **Example 1**
* Article ID: `NEWS_0010`
* Excerpt: `"(CNN) -- Flamboyant and fearless, Roberto Cavalli is the peacock of the fashion world; with his body-hugging clothes, he woos women the world over. Fashion designer Roberto Cavalli..."`
* Predicted Label: `positive`
* Predicted Probability: 0.6025
* Interpretation: Reasonable. The model keys into vibrant vocabulary ("flamboyant", "fearless", "woos") to deduce a positive tone. This shows text containing strong lifestyle/art praise transfers over well despite the shift from software reviews.

### **Example 2**
* Article ID: `NEWS_0001`
* Excerpt: `"(CNN) -- Oscar-winning filmmaker Roman Polanski has been arrested in Switzerland on a decades-old arrest warrant stemming from a sex charge in California, Swiss police said Sunday. Roman Polanski atte..."`
* Predicted Label: `negative`
* Predicted Probability: 0.7398
* Interpretation: Reasonable. Heavy, stark criminal terminology ("arrested", "warrant", "charge") triggers an accurate negative assignment. This demonstrates that raw severe keywords retain strong negative valence across vastly different domain contexts.

### **Example 3**
* Article ID: `NEWS_0004`
* Excerpt: `"(CNN) -- Forbes' list of the world's wealthy has named Warren Buffett the richest person on the planet, surpassing his friend and philanthropic partner Bill Gates who had held the title for 13 consecu..."`
* Predicted Label: `negative`
* Predicted Probability: 0.4777
* Interpretation: Clearly wrong. Objective journalistic reporting about financial wealth is flagged as negative. This exposes an acute keyword bias pattern where standard business/numerical facts confuse a classifier optimized for subjective app interface complaints.

### **Example 4**
* Article ID: `NEWS_0022`
* Excerpt: `"LONDON, England (CNN) -- Baz Luhrmann is the type of director for whom the word innovative was invented. Luhrmann and his costume designer wife..."`
* Predicted Label: `positive`
* Predicted Probability: 0.5752
* Interpretation: Suspicious. While the profile is generally flattering, the assignment relies entirely on the phrase "innovative". In the original application reviews domain, this feature heavily correlates with user product satisfaction, sparking overconfidence on narrow terms in a complex news piece.

### **Example 5**
* Article ID: `NEWS_0008`
* Excerpt: `"Editor's Note: Reese Witherspoon, the Academy Award-winning actress, is honorary chairman of the Avon Foundation and is employed by Avon Products as its global ambassador. Reese Witherspoon says she w..."`
* Predicted Label: `neutral`
* Predicted Probability: 0.5169
* Interpretation: Reasonable but exposes overrepresentation. Because formal journalism drops conversational markers or stark review signals like "glitch" or "love", the model routes the overwhelming bulk of items (70.8%) into a low-confidence neutral bucket as a catch-all safety net.

## **Engineering judgment**

One paragraph: would you ship this model to production for news domain sentiment classification? Why or why not? Be concrete — calibration concerns, confidence thresholding, the cost of false positives in this specific domain.

I would absolutely not ship this model to production for a news domain sentiment classification pipeline. The model displays major calibration concerns, with 76.57% of all news items squeezed under a weak 0.6 confidence margin, signaling severe out-of-distribution tracking confusion. Standard news items are regularly misclassified due to basic word matching, such as tagging a routine wealth list as negative. Implementing strict confidence thresholding is completely unviable because zero predictions broke past the 0.9 threshold, meaning threshold filtering would block the entire system's output. In a news downstream workflow, the cost of these false positives is highly disruptive, as mislabeling neutral public events or corporate achievements could invalidate commercial analytics pipelines and completely break automated algorithmic trading triggers.