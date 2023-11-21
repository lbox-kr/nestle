# NESTLE
- NESTLE: A no-node tool for statistical analysis of legal corpus

## Data
- For the demonstrational purpose, 1,500 Korean drunk driving precedents are uploaded in two versions: Korean (`data/drunk_driving_kor.jsonl`), and English  (`data/drunk_driving_eng.jsonl`). The English version is prepared by translating original documents using GPT-4.
- 550 manually curated examples from LBoxOpen-IE will be released soon!

## Video Demonstration
- The video demonstration is available [here](https://youtu.be/twkpjYJrvI8).
## Appendix
### Trade-off analysis table
Trade-off analysis. FRAUD task, a most challenging task among KORPREC-IE, is chosen as a case study.

| Name          | LLM module | IE module backbone size | \# of training examples | \# of LLM-labeled examples | Fraud Loss | Fraud Loss-A | Labeling cost (\$) | API cost (\$) | API cost t-lb (m) | API cost t-exp (m) | Model cost (\$) | Model cost t-train | Model cost t-infer | Tot. cost (0.1k) (\$) | Tot. cost (0.1k) t (m) | Tot. cost (10k) (\$) | Tot. cost (10k) t (m) | Tot. cost (1m) (\$) | Tot. cost (1m) t (m) |
|---------------|------------|-------------------------|-------------------------|----------------------------|------------|--------------|---------------|---------------|-------------------|--------------------|-----------------|-------------|--------------------|-----------------------|------------------------|----------------------|-----------------------|---------------------|----------------------|
| NESTLE-S$_0$   | ChatGPT    | 0.3B                   | 4                      | 92                        | 52.2       | 0.0          | 1.2           | 1.7$^a$       | 3.2$^b$           | 2.4$^c$            | 0.2$^d$         | 15                 | 0.2                  | 3                     | 20                    | 3                     | 40                    | 30                    | 2,000                 |
| NESTLE-S       | ChatGPT    | 0.3B                   | 4                      | 192                       | 56.5       | 0.0          | 1.2           | 3.6           | 6.7               | 10.6               | 0.44            | 30                 | 0.2                  | 5                     | 40                    | 6                     | 60                    | 30                    | 2,000                 |
| NESTLE-L$_0$   | ChatGPT    | 1.2B                   | 4                      | 92                        | 65.3       | 0.0          | 1.2           | 1.7           | 3.2               | 2.4                | 1.5             | 110                | 0.6                  | 4                     | 100                   | 5                     | 200                   | 80                    | 6,000                 |
| NESTLE-L       | ChatGPT    | 1.2B                   | 4                      | 192                       | 68.0       | 11.8         | 1.2           | 3.6           | 6.7               | 10.6               | 2.3             | 170                | 0.6                  | 7                     | 200                   | 8                     | 200                   | 90                    | 6,000                 |
| NESTLE-L+      | GPT-4      | 1.2B                   | 4                      | 192                       | 71.2       | 38.1         | 1.2           | 35.8          | 119               | 125                | 2.3             | 170                | 0.6                  | 40                    | 300                   | 40                    | 300                   | 100                   | 6,000                 |
| NESTLE-XXL+    | GPT-4      | 12.9B                  | 4                      | 192                       | 72.6       | 28.6         | 1.2           | 35.8          | 119               | 125                | 20.8$^e$        | 100                | 2                    | 60                    | 200                   | 100                   | 400                   | 4,000                 | 20,000                |
| ChatGPT       | -          | -                      | 4                      | -                         | 75.2       | 34.8         | 1.2           | 2.0           | 3.6               | 3.7                | 0               | 0                  | 0                    | 3.2                   | 3.6                   | 200                   | 360                   | 20,000                | 36,000                |
| GPT-4       | -          | -                      | 4                      | -                         | 82.3       | 59.3         | 1.2           | 19           | 64               | 74                | 0               | 0                  | 0                    | 2 0                  | 63                   | 1,900                   | 6300                   | 190,000                | 6,000                |


- a: At the time of experiments, gpt-3.5-turbo-16k-0613 costs $0.003 per 1,000 input tokens and $0.004 per 1,000 generated tokens. gpt-4-0613 costs $0.03 per 1,000 input tokens and $0.06 per 1,000 generated tokens.
- b: Estimated based on maximum token length per minutes (TPM). At the time of expriments, the rate limits of gpt-3.5-turbo-16k-0613 and gpt-4-0613 are 180,000 TPM and 9,000 TPM respectively.
- c: The script from OpenAI (https://github.com/openai/openai-cookbook/blob/main/examples/api_request_parallel_processor.py) was used where
asyncio library is employed.
- d: The cost is estimated supposing 1 hr gpu time = $0.8 based on Lambdalabs 1x A6000 GPU cloud pricing (https://lambdalabs.com/service/gpu-cloud#
pricing).
- e: The cost is estimated supposing 1 hr gpu time = $12.0 based on Lambdalabs 8x A100 (80GB) GPU cloud pricing (https://lambdalabs.com/service/
gpu-cloud#pricing).