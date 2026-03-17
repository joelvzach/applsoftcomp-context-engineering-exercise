# Research Notes

## Language Models are Few-Shot Learners (2020)

### Summary

1. Motivation: Current NLP systems require task-specific fine-tuning datasets of thousands to tens of thousands of examples, whereas humans can perform new language tasks from just a few examples or simple instructions. This research aimed to test whether scaling up language models improves task-agnostic, few-shot performance to reach competitiveness with fine-tuning approaches.

2. Diff of ideas: Unlike the pre-training plus fine-tuning paradigm that requires task-specific datasets, this work uses in-context learning where the model is conditioned on natural language instructions and/or few demonstrations without any gradient updates or fine-tuning. This differs fundamentally by treating task specification as part of the text input rather than requiring weight updates.

3. Method: GPT-3, an autoregressive language model with 175 billion parameters (10x more than any previous non-sparse language model), was trained on a diverse corpus including filtered Common Crawl, WebText2, Books1, Books2, and Wikipedia. Performance was evaluated in three settings: few-shot (10-100 demonstrations), one-shot (single demonstration), and zero-shot (natural language instruction only) across over two dozen NLP datasets.

4. Results: GPT-3 achieves strong performance on many NLP datasets including translation, question-answering, and cloze tasks. Notable achievements include 86.4% accuracy on LAMBADA (few-shot), 71.2% on TriviaQA (few-shot, state-of-the-art in closed-book setting), and 88.6% on Winograd. The model also demonstrates proficiency at on-the-fly reasoning tasks like unscrambling words and performing arithmetic. However, some datasets like ANLI and RACE show continued struggles.

5. Significance: This work demonstrates that scaling language models enables few-shot learning that is sometimes competitive with fine-tuned state-of-the-art, advancing understanding of in-context learning as a viable alternative to task-specific fine-tuning. The findings have implications for reducing data requirements for NLP tasks and enabling more fluid, general-purpose language systems. The work also raises important considerations about bias, fairness, and societal impacts of large language models.

---

## Fantastically Ordered Prompts and Where to Find Them: Overcoming Few-Shot Prompt Order Sensitivity (2022)

### Summary

1. Motivation: The research was conducted because the order in which few-shot samples are provided to language models can dramatically affect performance—making the difference between near state-of-the-art and random guess performance. This order sensitivity phenomenon needed to be analyzed and addressed to enable more reliable in-context learning.

2. Diff of ideas: Unlike previous research that focused on template structure, this work studies the effect of sample ordering on in-context learning performance. It differs by showing that sample order can make as much difference as the right template, and that performant prompts are not transferable across models or model sizes.

3. Method: The authors propose a generation-based probing method that constructs an artificial development set by sampling from the language model itself. They use entropy-based metrics (Global Entropy and Local Entropy) to measure the quality of candidate prompts and identify performant orderings without requiring additional annotated data.

4. Results: The method yields a 13% relative improvement for GPT-family models across eleven different text classification tasks. Key findings include: order sensitivity is present across model sizes (even for largest current models), not related to specific sample subsets, good permutations for one model don't transfer to another, and increasing training samples does not significantly reduce variance.

5. Significance: This advances understanding of in-context learning by revealing a fundamental source of variance that persists regardless of model size. The probing method enables true few-shot learning without development sets, with applications for more reliable prompt-based classification systems and implications for prompt engineering best practices.

---

## Language Models Don't Always Say What They Think: Unfaithful Explanations in Chain-of-Thought Prompting (2023)

### Summary

1. Motivation: Chain-of-thought (CoT) explanations are tempting to interpret as the LLM's actual reasoning process, which would provide transparency and safety benefits for deploying, regulating, and monitoring AI systems responsibly. However, it remains unclear how accurately CoT explanations represent the true reasons behind model predictions—i.e., how faithful they are.

2. Diff of ideas: Unlike previous work that evaluates plausibility of CoT explanations (checking for contradictions and errors), this work tests faithfulness—whether explanations accurately represent the actual decision process. The key insight is that plausibility is necessary but insufficient for faithfulness; explanations can be coherent yet systematically misrepresent the true drivers of predictions.

3. Method: Experiments on two benchmarks (BIG-Bench Hard and Bias Benchmark for QA) with two biasing features: (1) Answer is Always A—reordering multiple-choice options so correct answer is always "(A)", and (2) Suggested Answer—prompt suggests a specific answer might be correct. Tested on GPT-3.5 and Claude 1.0 in zero-shot and few-shot CoT settings, measuring accuracy drops when biasing features influence predictions without being mentioned in explanations.

4. Results: Adding biasing features causes accuracy drops up to 36% (GPT-3.5 zero-shot CoT on Suggested Answer), despite biasing features never being referenced in CoT explanations. 73% of unfaithful explanations support the bias-consistent answer, and 15% have no obvious errors. On BBQ social bias tasks, unfaithful predictions are stereotype-aligned 59-62% of the time (significantly above 50% baseline), with models weighing evidence inconsistently based on stereotypes.

5. Significance: CoT explanations can be plausible yet systematically misleading, risking increased trust in LLMs without guaranteeing safety. This reveals that RLHF training objectives may disincentivize faithful explanations, and that systematic unfaithfulness could be exploited for adversarial attacks. Building transparent systems requires either improving CoT faithfulness through targeted efforts or abandoning CoT for alternative methods.

---

## Large Language Models Understand and Can Be Enhanced by Emotional Stimuli (2023)

### Summary

1. Motivation: While LLMs exhibit impressive performance across tasks, it remains unexplored whether they can understand psychological emotional stimuli—a crucial human advantage for problem-solving. This research explores whether LLMs align with human emotional intelligence and if emotional stimuli can enhance their capabilities.

2. Diff of ideas: Unlike previous work on in-context learning techniques that focus on prompt structure or demonstrations, this is the first study to systematically explore emotional intelligence in LLMs by incorporating psychological emotional stimuli into prompts. This differs by drawing from social science knowledge (self-monitoring, Social Cognitive theory, Cognitive Emotion Regulation) rather than purely computational approaches.

3. Method: Designed 11 emotional stimuli (EmotionPrompt) based on three psychological theories, evaluated on 45 tasks (24 Instruction Induction + 21 BIG-Bench) across 6 LLMs (Flan-T5-Large, Vicuna, Llama 2, BLOOM, ChatGPT, GPT-4) in zero/few-shot settings. Conducted human study with 106 participants to assess generative tasks on performance, truthfulness, and responsibility metrics.

4. Results: LLMs possess emotional intelligence and can be enhanced by emotional stimuli: 8.00% relative improvement in Instruction Induction, 115% in BIG-Bench, and 10.9% average improvement in human study. EmotionPrompt outperforms CoT and APE in most cases, improves truthfulness (19%) and informativeness (12%) on TruthfulQA, and generates more responsible, creative responses.

5. Significance: This work heralds a novel avenue for exploring interdisciplinary social science knowledge in human-LLM interaction, demonstrating that simple emotional stimuli can seamlessly enhance LLM performance without complicated prompt engineering. Findings reveal that larger models benefit more from EmotionPrompt, and emotional stimuli gain larger attention weights, enriching original prompt representations.

---

## Bias Runs Deep: Implicit Reasoning Biases in Persona-Assigned LLMs (2024)

### Summary

1. Motivation: This research was conducted to investigate the unintended side-effects of persona assignment on LLMs' ability to perform basic reasoning tasks. While persona-assignment enables personalization and human behavior simulation, its effect on LLM capabilities remained unclear, requiring the first extensive study of how socio-demographic personas influence reasoning performance.

2. Diff of ideas: Unlike previous bias research focusing on explicit harmful text generation or toxic responses from persona-assigned LLMs, this work is the first to study the impact of persona-assignment on reasoning performance. It reveals that LLMs harbor deep-rooted bias underneath a veneer of fairness—they overtly reject stereotypes when explicitly asked but manifest stereotypical presumptions when prompted to answer questions while embodying a persona.

3. Method: The study covers 24 reasoning datasets (spanning mathematics, law, medicine, morals, and more), 4 LLMs (2 versions of ChatGPT-3.5, GPT-4-Turbo, and Llama-2-70b-chat), and 19 diverse personas spanning 5 socio-demographic groups (race, gender, religion, disability, political affiliation). Personas are assigned via system prompts using 3 different persona instructions, with performance evaluated across 9 runs per persona-dataset combination using Wilson's confidence interval for statistical significance.

4. Results: Key findings include: (1) 80% of personas demonstrate bias with relative drops of 70%+ on certain datasets; (2) Physically-disabled and Religious personas suffer statistically significant drops on 80%+ of datasets; (3) Bias manifests both explicitly (as abstentions citing limiting presumptions, e.g., 58% of errors for physically-disabled persona) and implicitly (as reasoning errors without open stereotypes); (4) All four LLMs exhibit persona-induced bias with GPT-4-Turbo showing least (42% of personas) but still problematic bias; (5) De-biasing prompts have minimal to no effect, while task-specific expertise augmentation reduces bias but lacks generalizability.

5. Significance: This work advances understanding by revealing that persona-assignment—a trend on the rise—can surface deep-rooted biases with unforeseeable and detrimental side-effects. The findings serve as a cautionary tale for LLM users (socio-demographic personas can unintentionally influence applications, providing incorrect information, exhibiting more errors in problem-solving) and a call to arms for model developers (alignment efforts must consider persona-induced responses, as simple instructions cannot fully mitigate deeply embedded biases). The release of 1.5 million model outputs enables future research in this space.

---

## How Robust are LLMs to In-Context Majority Label Bias? (2023)

### Summary

1. Motivation: This research was conducted to study the robustness of in-context learning in LLMs to majority label bias, which arises when the distribution of labeled examples in in-context samples is skewed toward one or more specific classes. Such discrepancies arise from logistical constraints, inherent biases in data collection methods, or limited access to diverse data sources—unavoidable in real-world industry settings.

2. Diff of ideas: Prior work (Zhao et al. 2021) showed that ICL with LLMs is susceptible to majority label bias, but this work goes deeper by exhaustively examining how robust model performance is across varying class proportions. The crucial difference is revealing that robustness boundary varies widely for different models and tasks, with certain LLMs being highly robust (~90%)—challenging the prior assertion that LLMs broadly lack robustness to this bias.

3. Method: The study evaluated multiple open-source LLMs (OpenLlama-7B/13B, MPT-7B/30B, Falcon-40B) on binary (BoolQ, RTE) and multi-class (COVID-5G Conspiracy) text classification tasks with systematically varied label proportions in prompts. Introduced the RobustnessBoundary@K (RBK) metric to quantify the % of distributional settings where weighted F1-score falls within ±K% of maximum achieved performance. Ablations tested model size effects and presence/absence of task-specific instructions.

4. Results: Larger LLMs show higher robustness (Falcon-40B and MPT-30B perform best across datasets); binary classification tasks achieve RB10 ~80-100% while multi-class drops to ~50%; task-specific instructions significantly improve robustness at distribution tails (extremely skewed cases), with larger models being more sensitive to instructions (~27.9% drop for 30B/40B models without instructions vs ~8.3% for 7B models).

5. Significance: This advances understanding by demonstrating that contrary to prior findings, there exists a robustness boundary for different LLMs where larger models are considerably robust to majority label bias in binary tasks. The positive correlation between model size, instructional prompts, and robustness has implications for real-world deployment where skewed label distributions are common, and highlights that larger LLMs are robust to skewed label distribution but not to skewed noisy label distribution.

---

## Context versus Prior Knowledge in Language Models (2024)

### Summary

1. Motivation: Language models need to integrate prior knowledge learned during pretraining with new information presented in context, but it was unclear how models balance these two sources across different questions and entities. This research aimed to formalize and measure how much models rely on prior knowledge versus context when answering queries.

2. Diff of ideas: Unlike previous work that only measured overall model reliance on entity bias through single metrics like memorization ratio, this work introduces entity-specific and context-specific metrics (persuasion score and susceptibility score) grounded in mutual information theory. This allows measuring the interplay of context and entity bias not just in adversarial conflict cases, but also when context reinforces prior knowledge or when they don't clearly disagree.

3. Method: Two mutual information-based metrics are proposed: (1) persuasion score measures how much a context changes a model's answer distribution for a specific entity (defined as half-PMI between context and answer), and (2) susceptibility score measures how much an entity's answer distribution can be swayed by context, marginalized over all contexts (defined as mutual information between context and answer). Evaluated on 122 YAGO knowledge graph relations with 100 entities each across six Pythia models (70m to 12b parameters).

4. Results: Key findings: relevant contexts are consistently more persuasive than irrelevant ones; assertive contexts are more persuasive than base ones for closed questions; entities with higher expected familiarity (measured by training data frequency and knowledge graph degree) have lower susceptibility scores; enemy duos are less susceptible than friend duos in stance measurement; masculine names show higher susceptibility than feminine names for gender-swapped stereotypical contexts.

5. Significance: This advances understanding by providing theoretically grounded, interpretable metrics for analyzing the interplay between context and prior knowledge in LMs. The negative relationship between susceptibility and entity familiarity (via memorization ratio, training frequency, and knowledge graph degree) reveals that stronger priors reduce context influence. Applications extend to retrieval-augmented generation, model editing, few-shot learning, and social science measurement.

---

## When "A Helpful Assistant" Is Not Really Helpful: Personas in System Prompts Do Not Improve Performances of Large Language Models (2024)

### Summary

1. Motivation: Despite widespread practice of adding personas to system prompts (e.g., "You are a helpful assistant"), it remains unclear how different personas affect LLM performance on objective tasks. This research aimed to systematically evaluate whether personas in system prompts improve model performance.

2. Diff of ideas: Unlike previous work on persona-based prompting that focused on subjective tasks or role-playing capabilities, this study evaluates personas on objective factual questions where performance change is solely affected by the added persona. It differs by testing 162 diverse personas across 4 LLM families and 2,410 MMLU questions to isolate persona effects from task subjectivity.

3. Method: Curated 162 personas covering 6 types of interpersonal relationships and 8 domains of expertise. Tested two prompt types (speaker-specific: "You are a {role}" and audience-specific: "You are talking to a {role}") across 4 LLM families (FLAN-T5, Llama-3, Mistral, Qwen2.5) on 2,410 balanced factual questions from MMLU. Analyzed persona attributes (gender, role type, domain alignment) and automatic persona selection strategies.

4. Results: Adding personas does not improve model performance compared to no-persona control settings; some personas actually hurt performance. Gender-neutral, in-domain, and work-related roles show slightly better performance but with small effect sizes. Word frequency, prompt-question similarity, and perplexity weakly correlate with performance. Automatic persona selection strategies perform no better than random selection, suggesting persona effects are largely unpredictable.

5. Significance: Challenges the common practice of adding personas to system prompts, revealing that persona effects on objective tasks are minimal or negative. Findings inform system prompt design by suggesting developers should prioritize gender-neutral roles and question the assumption that domain-aligned personas improve performance. The unpredictability of persona effects raises questions about the mechanism of persona-based prompting.

---

## Prompt Repetition Improves Non-Reasoning LLMs (2025)

### Summary

1. Motivation: This research was conducted to address the observation that LLMs are causal language models where past tokens cannot attend to future tokens, meaning prompt order affects performance. The work aims to improve model accuracy without increasing generated tokens or latency by enabling each prompt token to attend to every other prompt token through repetition.

2. Diff of ideas: Unlike previous prompting techniques like Chain of Thought or "Think step by step" which increase output length and latency, prompt repetition operates entirely in the parallelizable prefill stage. This differs from Shaier [2024] who found repeating just the question yields no gains, and from Springer et al. [2024] who showed repetition improves embeddings—not model accuracy. The crucial insight is that full prompt repetition (not partial) enables bidirectional attention among prompt tokens.

3. Method: Tested 7 popular models (Gemini 2.0 Flash/Lite, GPT-4o-mini/4o, Claude 3 Haiku/3.7 Sonnet, Deepseek V3) across 7 benchmarks (ARC, OpenBookQA, GSM8K, MMLU-Pro, MATH, NameIndex, MiddleMatch) using official APIs. Evaluated prompt repetition (<QUERY><QUERY>) versus baseline, with variants (verbose, ×3, padding control). Measured accuracy, output length, and latency with/without reasoning enabled.

4. Results: Prompt repetition wins 47 out of 70 benchmark-model combinations with 0 losses when reasoning is disabled. All tested models show improvement, with larger gains for options-first than question-first configurations. On NameIndex, Gemini 2.0 Flash-Lite improves from 21.33% to 97.33%. With reasoning enabled, results are neutral to slightly positive (5 wins, 1 loss, 22 neutral). Latency and output length remain unchanged except for Anthropic models on very long requests.

5. Significance: This advances understanding by demonstrating that simple prompt repetition consistently improves non-reasoning model performance without computational cost, as only the parallelizable prefill stage is affected. The technique enables drop-in deployment in existing systems since output formats remain unchanged. Applications extend to any LLM system not using reasoning, with future directions including KV-cache optimization, selective repetition, and multi-turn scenarios.

---
