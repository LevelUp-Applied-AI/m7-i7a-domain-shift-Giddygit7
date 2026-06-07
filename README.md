# Module 7 Week A — Integration Task: Domain-Shift Analysis

Apply your fine-tuned classifier (from Lab 7A, hosted on Hugging Face Hub) to the tech / entertainment news corpus and analyze the domain-shift behavior.

Full instructions: see the **Integration Task 7A guide** linked in TalentLMS.

## Quick start

```bash
pip install -r requirements.txt
cp .env.example .env       # then edit MODEL_HUB_ID
make smoke                 # CI substitute model on 5-row fixture
make apply                 # your real model on full 1,033-row tech-news corpus
```

## TODO for learner — fill these in before submitting

- **Hugging Face Hub model URL:** https://huggingface.co/huggyhugface/m7-app-review-sentiment
- **Reproducibility command:** `cp .env.example .env` (set MODEL_HUB_ID), then `make apply`.
- **What the model was trained on and why we're applying it here:**
The sentiment classification model used in this pipeline was originally fine-tuned on a text dataset containing user reviews for mobile applications. Because this training data comes straight from app store reviews, it is mostly made of short, informal sentences. These reviews rely heavily on common text phrases and specific words to show user satisfaction or user complaints, such as "buggy", "crash", "slow", or "love it". The text focuses entirely on how users interact with software, technical glitches, app performance, and interface design feedback.

We are now applying this exact model to a completely different dataset that contains 1,033 tech and entertainment news articles to study the effects of domain shift. News articles use formal language, much longer sentences, and standard journalistic writing style rather than personal user opinions. Testing our app review model on this new data helps us check how well a fine-tuned classifier generalizes when it faces text from an out-of-distribution source. It also lets us see where simple keyword matching and word biases cause the model to make incorrect predictions when the context changes.

## Submission

Open a PR from `integration-7a-domain-shift` into `main`. Paste the PR URL into TalentLMS → Module 7 → Integration Task 7A.

---

## License

This repository is provided for educational use only. See [LICENSE](LICENSE) for terms.

You may clone and modify this repository for personal learning and practice, and reference code you wrote here in your professional portfolio. Redistribution outside this course is not permitted.
