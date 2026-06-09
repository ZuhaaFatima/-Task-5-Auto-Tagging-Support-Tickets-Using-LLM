# -Task-5-Auto-Tagging-Support-Tickets-Using-LLM
**DevelopersHub Corporation — AI/ML Engineering Internship**

---

## Task Objective

Build an LLM-based system to automatically classify customer support tickets into predefined categories.

The system compares:
- Zero-shot prompting
- Few-shot prompting

and returns the top 3 most probable tags with confidence scores for each ticket.

---

## Dataset Used

| Property | Detail |
|---|---|
| Name | Customer Support Tickets Dataset |
| Source | Hugging Face Datasets (`Tobi-Bueck/customer-support-tickets`) |
| Total samples | 61,765 (original dataset) |
| Final used samples | 24 balanced tickets |
| Fields used | `body` (text), `type` (used for sampling only) |
| Purpose | Real-world support ticket classification |

---

## Tags Used

| Tag | Description |
|---|---|
| billing | Payment, invoice, subscription, refund issues |
| technical_issue | Bugs, errors, crashes, system failures |
| account | Login, password, authentication, profile issues |
| feature_request | Requests for new features or improvements |
| general_inquiry | General questions or informational requests |
| shipping | Delivery, tracking, and shipping-related issues |

---

## Models Applied

| Component | Detail |
|---|---|
| Model | `meta-llama/Llama-3.1-8B-Instruct` |
| Access | Hugging Face Inference Router API |
| Interface | OpenAI-compatible API client |
| Temperature | 0.1 |
| Max tokens | 150 |
| Output format | Strict JSON (Top 3 tags with confidence scores) |

---

## Prompting Strategies

### Zero-Shot Prompting
- No examples provided
- Only tag list and descriptions are given
- Model predicts based on instructions
- Returns top 3 tags with confidence scores

### Few-Shot Prompting
- 12 labeled examples (2 per category)
- Helps model learn classification patterns
- Produces more stable and accurate results

---

## Output Format

Both approaches return:

```json
{
  "tags": [
    {"tag": "category_name", "confidence": 0.95},
    {"tag": "category_name", "confidence": 0.70},
    {"tag": "category_name", "confidence": 0.40}
  ]
}

## Results Summary

### Zero-Shot
- No examples used
- Faster but less accurate
- Often biased toward general labels
- Less stable on complex tickets

### Few-Shot
- Uses labeled examples
- More accurate and consistent
- Better category separation
- More reliable predictions

---

## Key Findings

- Few-shot performs better than zero-shot overall
- Examples significantly improve accuracy
- Zero-shot tends to overuse general categories
- Prompt structure strongly affects output quality
- LLMs can classify well without fine-tuning when guided properly

