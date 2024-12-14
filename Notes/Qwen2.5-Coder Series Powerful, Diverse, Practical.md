---
tags:
- editors
---
## **Qwen2.5-Coder Series Powerful, Diverse, Practical

[GITHUB](https://github.com/QwenLM/Qwen2.5-Coder) [HUGGING FACE](https://huggingface.co/collections/Qwen/qwen25-coder-66eaa22e6f99801bf65b0c2f) [MODELSCOPE](https://modelscope.cn/organization/qwen) [KAGGLE](https://www.kaggle.com/models/qwen-lm/qwen2.5-coder) [DEMO](https://huggingface.co/spaces/Qwen/Qwen2.5-Coder-demo) [DISCORD](https://discord.gg/yPEP2vHTu4)

## Introduction

Today, we are excited to open source the “Powerful”, “Diverse”, and “Practical” Qwen2.5-Coder series, dedicated to continuously promoting the development of Open CodeLLMs.

-   **Powerful**: Qwen2.5-Coder-32B-Instruct has become the current SOTA open-source code model, matching the coding capabilities of GPT-4o. While demonstrating strong and comprehensive coding abilities, it also possesses good general and mathematical skills;
-   **Diverse**: Building on the previously open-sourced two sizes of 1.5B / 7B, this release brings four model sizes, including 0.5B / 3B / 14B / 32B. As of now, Qwen2.5-Coder has covered six mainstream model sizes to meet the needs of different developers;
-   **Practical**: We explore the practicality of Qwen2.5-Coder in two scenarios, including code assistants and Artifacts, with some examples showcasing the potential applications of Qwen2.5-Coder in real-world scenarios;

## Powerful: Code capabilities reach SOTA for open-source models

-   **Code Generation**: Qwen2.5-Coder-32B-Instruct, as the flagship model of this open-source release, has achieved the best performance among open-source models on multiple popular code generation benchmarks (EvalPlus, LiveCodeBench, BigCodeBench), and has competitive performance with GPT-4o.
-   **Code Repair**: Code repair is an important programming skill. Qwen2.5-Coder-32B-Instruct can help users fix errors in their code, making programming more efficient. Aider is a popular benchmark for code repair, and Qwen2.5-Coder-32B-Instruct scored 73.7, performing comparably to GPT-4o on Aider.
-   **Code Reasoning**: Code reasoning refers to the model’s ability to learn the process of code execution and accurately predict the model’s inputs and outputs. The recently released Qwen2.5-Coder-7B-Instruct has already shown impressive performance in code reasoning, and this 32B model takes it a step further.
-   **Multiple Programming Languages**: An intelligent programming assistant should be familiar with all programming languages. Qwen2.5-Coder-32B-Instruct performs excellently across more than 40 programming languages, scoring 65.9 on McEval, with impressive performances in languages like Haskell and Racket, thanks to our unique data cleaning and balancing during the pre-training phase.

Additionally, the multi-language code repair capabilities of Qwen2.5-Coder-32B-Instruct remain impressive, aiding users in understanding and modifying programming languages they are familiar with, significantly reducing the learning cost of unfamiliar languages. Similar to McEval, MdEval is a multi-language code repair benchmark, where Qwen2.5-Coder-32B-Instruct scored 75.2, ranking first among all open-source models.

-   **Human Preference Alignment**: To evaluate the alignment performance of Qwen2.5-Coder-32B-Instruct with human preferences, we constructed an internal annotated code preference evaluation benchmark called Code Arena (similar to Arena Hard). We used GPT-4o as the evaluation model for preference alignment, employing an ‘A vs. B win’ evaluation method, which measures the percentage of instances in the test set where model A’s score exceeds model B’s. The results below demonstrate the advantages of Qwen2.5-Coder-32B-Instruct in preference alignment.
erse: Rich Model Sizes

This time, Qwen2.5-Coder has open-sourced a rich variety of model sizes, including 0.5B/1.5B/3B/7B/14B/32B, which not only meets the needs of developers in different resource scenarios but also provides a good experimental platform for the research community. The following table provides detailed model information:

| Models | Params | Non-Emb Params | Layers | Heads (KV) | Tie Embedding | Context Length | License |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Qwen2.5-Coder-0.5B | 0.49B | 0.36B | 24 | 14 / 2 | Yes | 32K | Apache 2.0 |
| Qwen2.5-Coder-1.5B | 1.54B | 1.31B | 28 | 12 / 2 | Yes | 32K | Apache 2.0 |
| Qwen2.5-Coder-3B | 3.09B | 2.77B | 36 | 16 / 2 | Yes | 32K | Qwen Research |
| Qwen2.5-Coder-7B | 7.61B | 6.53B | 28 | 28 / 4 | No | 128K | Apache 2.0 |
| Qwen2.5-Coder-14B | 14.7B | 13.1B | 48 | 40 / 8 | No | 128K | Apache 2.0 |
| Qwen2.5-Coder-32B | 32.5B | 31.0B | 64 | 40 / 8 | No | 128K | Apache 2.0 |

We have always believed in the philosophy of Scaling Law. We evaluated the performance of different sizes of Qwen2.5-Coder across all datasets to verify the effectiveness of Scaling in Code LLMs. For each size, we open-sourced both Base and Instruct models, where the Instruct model serves as an official aligned model that can chat directly, and the Base model serves as a foundation for developers to fine-tune their own models.

Here are the performances of the Base models of different sizes:

Here are the performances of the Instruct models of different sizes:

We present a comparison of different sizes of Qwen2.5-Coder with other open-source models on core datasets.

-   For the Base model, we chose MBPP-3shot as the evaluation metric. Our extensive experiments show that MBPP-3shot is more suitable for evaluating base models and correlates well with the actual performance of the models.
-   For the Instruct model, we selected the latest 4 months of LiveCodeBench (2024.07 - 2024.11) questions as the evaluation, which are the latest published questions that could not have leaked into the training set, reflecting the model’s OOD capabilities.

There is a positive correlation between model size and model performance, and Qwen2.5-Coder has achieved SOTA performance across all sizes, encouraging us to continue exploring larger sizes of Coder.

Practical: Encountering Cursor and Artifacts

A practical Coder has always been our vision, and for this reason, we explored the actual performance of Qwen2.5-Coder in code assistants and Artifacts scenarios.

### Qwen2.5-Coder 🤝 Cursor

Code assistants have become widely used, but most currently rely on closed-source models. We hope that the emergence of Qwen2.5-Coder can provide developers with a friendly and powerful option. Here is an example of Qwen2.5-Coder in the [Cursor](https://www.cursor.com/).

Example: Qwen2.5-Coder 🤝 Cursor

Additionally, Qwen2.5-Coder-32B has demonstrated strong code completion capabilities on pre-trained models, achieving SOTA performance on a total of 5 benchmarks: Humaneval-Infilling, CrossCodeEval, CrossCodeLongEval, RepoEval, and SAFIM. To maintain a fair comparison, we controlled the maximum sequence length to 8k and used the Fill-in-the-Middle mode for testing. Among the four evaluation sets of CrossCodeEval, CrossCodeLongEval, RepoEval, and Humaneval-Infilling, we evaluated whether the generated content was exactly equal to the true labels (Exact Match). In SAFIM, we used the one-time execution success rate (Pass@1) for evaluation.

.5-Coder 🤝 Artifacts

Artifacts are an important application of code generation, helping users create visual works. We chose [Open WebUI](https://openwebui.com/) to explore the potential of Qwen2.5-Coder in the Artifacts scenario, and here are some specific examples.

Example: Three-body Problem Simulation (1/4) Next

We will soon launch the code mode on the Tongyi official website [https://tongyi.aliyun.com](https://tongyi.aliyun.com/), supporting one-click generation of websites, mini-games, and data charts, among other visual applications. We welcome everyone to experience it!

## Model License

Qwen2.5-Coder 0.5B / 1.5B / 7B / 14B / 32B are licensed under **Apache 2.0**, while 3B is under Qwen-Research license;

## What’s Next for Qwen-Coder?

We believe that this release can truly help developers and explore more interesting application scenarios with the community. Additionally, we are delving into powerful reasoning models centered around code, and we believe we will meet everyone soon!

[[Code Editor]]

## Citation

```bash
@article{hui2024qwen2,
  title={Qwen2. 5-Coder Technical Report},
  author={Hui, Binyuan and Yang, Jian and Cui, Zeyu and Yang, Jiaxi and Liu, Dayiheng and Zhang, Lei and Liu, Tianyu and Zhang, Jiajun and Yu, Bowen and Dang, Kai and others},
  journal={arXiv preprint arXiv:2409.12186},
  year={2024}
}
@article{yang2024qwen2,
  title={Qwen2 technical report},
  author={Yang, An and Yang, Baosong and Hui, Binyuan and Zheng, Bo and Yu, Bowen and Zhou, Chang and Li, Chengpeng and Li, Chengyuan and Liu, Dayiheng and Huang, Fei and others},
  journal={arXiv preprint arXiv:2407.10671},
  year={2024}
}
```

[[Code Editor]]  