# ReAct and Single-Agent Reasoning/Acting Loops

Research date: 2026-11-05. Primary sources were read through alphaXiv full text and the Anthropic engineering blog. Where a claim comes from memory of a paper's abstract and was not re-read in this session, it is marked "(abstract, not re-read this session)".

---

## Q1. What exactly did ReAct (Yao et al., arXiv 2210.03629, ICLR 2023) propose, and what did it find?

### Takeaway
ReAct adds free-form language "thoughts" to the agent's action space. The model alternates Thought, Action and Observation, with dense thoughts on QA and sparse, model-chosen thoughts on long-horizon tasks. On ALFWorld and WebShop it clearly beats action-only prompting and imitation/RL baselines (+34 and +10 points absolute success). On knowledge QA it did **not** beat CoT on HotpotQA (27.4 vs 29.4 EM). The best results came from hybrids that back off between ReAct and CoT with self-consistency (CoT-SC). The authors' own error analysis names repetitive loops and non-informative search as the main ReAct failure modes.

### Cited Findings
**Mechanism**
- Formalism: an agent observes o_t and takes a_t from policy π(a_t|c_t), where c_t is the history. ReAct augments the action space to Â = A ∪ L, with L the space of language. A "thought" â_t ∈ L does not affect the environment and returns no observation. It updates the context c_{t+1} = (c_t, â_t) to support later reasoning or acting — [ReAct, arXiv 2210.03629](https://arxiv.org/abs/2210.03629)
- Thought types listed by the authors: decomposing goals and making plans, injecting commonsense, extracting key parts of observations, tracking progress and moving between plan steps, and handling exceptions or adjusting plans — [ReAct](https://arxiv.org/abs/2210.03629)
- Setup: frozen PaLM-540B, few-shot prompted with human-written trajectories. HotpotQA and FEVER used 6 and 3 exemplars ("more examples do not improve performance"). ALFWorld used 2 exemplars per prompt, built from 3 annotated per task type. WebShop was one-shot — [ReAct](https://arxiv.org/abs/2210.03629)
- Dense vs sparse thoughts: on reasoning-heavy tasks, thoughts and actions alternate (T-A-O at every step). On decision-making tasks with many actions, thoughts appear sparsely and "we let the language model decide the asynchronous occurrence of thoughts and actions for itself" — [ReAct](https://arxiv.org/abs/2210.03629)
- Action space for QA (a deliberately weak Wikipedia API): `search[entity]` returns the first 5 sentences or the top-5 similar entities; `lookup[string]` returns the next sentence containing the string (like Ctrl+F); `finish[answer]` ends the episode — [ReAct](https://arxiv.org/abs/2210.03629)
- Step caps: 7 steps for HotpotQA and 5 for FEVER. Correct trajectories that needed that many steps were only 0.84% and 1.33% of the total — [ReAct](https://arxiv.org/abs/2210.03629)

**Results: HotpotQA (EM) / FEVER (Acc), PaLM-540B, Table 1**
- Standard 28.7 / 57.1; CoT 29.4 / 56.3; CoT-SC (21 samples) 33.4 / 60.4; Act 25.7 / 58.9; **ReAct 27.4 / 60.9**; CoT-SC→ReAct 34.2 / **64.6**; ReAct→CoT-SC **35.1** / 62.0. The supervised SoTA was 67.5 / 89.5, so all prompting methods were far below it — [ReAct](https://arxiv.org/abs/2210.03629)
- Hybrid heuristics: ReAct→CoT-SC falls back to CoT-SC when ReAct gives no answer within the step budget. CoT-SC→ReAct falls back to ReAct when the majority answer gets fewer than n/2 votes. The hybrids reach CoT-SC's 21-sample performance with only 3–5 samples — [ReAct](https://arxiv.org/abs/2210.03629)
- Fine-tuning on 3,000 bootstrapped correct trajectories: prompted ReAct is the *worst* of the four methods at 8B and 62B. Fine-tuned, it is the *best*: PaLM-8B fine-tuned ReAct beats all 62B prompting methods, and 62B fine-tuned ReAct beats all 540B prompting methods — [ReAct](https://arxiv.org/abs/2210.03629)
- On GPT-3 (text-davinci-002), ReAct got 30.8 HotpotQA EM (vs 29.4 on PaLM) and 78.4% ALFWorld success (vs 70.9 on PaLM) — [ReAct App. A.1](https://arxiv.org/abs/2210.03629)

**Results: ALFWorld (134 unseen games) and WebShop (500 test instructions)**
- ALFWorld overall success: ReAct best-of-6 prompts **71%**, ReAct average 57%, Act best-of-6 45%, ReAct-IM (Inner-Monologue-style dense external-feedback thoughts) 53% best / 48% avg, BUTLER (imitation learning on 10^5 expert trajectories per task type) 37%. "Even the worse ReAct trial (48%) beats the best trial of both methods." Across the six controlled prompt pairs, ReAct's relative gain over Act ranges from 33% to 90%, averaging 62% — [ReAct Table 3](https://arxiv.org/abs/2210.03629)
- WebShop: Act score 62.3 / SR 30.1; **ReAct 66.6 / 40.0**; IL 59.9 / 29.1; IL+RL 62.4 / 28.7; human expert 82.1 / 59.6 — [ReAct Table 4](https://arxiv.org/abs/2210.03629)

**Failure modes reported by the authors (HotpotQA, 200 hand-labelled trajectories, Table 2)**
- Among ReAct failures: reasoning error 47% (this includes "repetitively generates the previous thoughts and actions" and failing to break out of the loop), search-result error (empty or uninformative retrieval) 23%, hallucination 0%, label ambiguity 29%. Among CoT failures, hallucination is 56% — [ReAct](https://arxiv.org/abs/2210.03629)
- False-positive rate among successes: ReAct 6% vs CoT 14% (that is, CoT more often gets the right answer from a hallucinated trace) — [ReAct](https://arxiv.org/abs/2210.03629)
- The authors' framing: the interleaved structure "reduces its flexibility in formulating reasoning steps, leading to more reasoning error rate than CoT." Uninformative search "derails the model reasoning and gives it a hard time to recover." They attribute the looping to greedy decoding and suggest beam search as a possible fix — [ReAct](https://arxiv.org/abs/2210.03629)
- Human-in-the-loop: editing two thoughts in a failing ALFWorld trajectory makes it succeed. The authors present thought-editing as a control surface — [ReAct App. A.3](https://arxiv.org/abs/2210.03629)
- Act-only failure example: Act tries to "clean knife with sinkbasin" without first going to the sinkbasin, then cycles through the same commands indefinitely. ReAct-IM also loops ("I need to put this knife in/on countertop 1" repeated) — [ReAct App. D.2](https://arxiv.org/abs/2210.03629)

### Inferences
- ReAct's headline QA claim is weaker than often remembered. Alone it trails CoT on HotpotQA, and its wins there come from *grounding* (fewer hallucinations) and from hybrids with self-consistency. Its strongest evidence is on interactive, long-horizon environments.
- Three ingredients of every modern agent harness already appear in the ReAct paper: step caps, loop or repetition detection, and fallback to a different strategy.

### Gaps
- The original paper gives no token-cost or latency numbers. Cost critiques come from later work (see Q3).

---

## Q2. Successors and alternatives: how each changes the loop, and what gains were reported

### Takeaway
The descendants modify ReAct along five axes:
- **Across episodes**, with verbal memory: Reflexion.
- **Across branches**, with search: ToT and LATS.
- **Across time**, by planning ahead: ReWOO and Plan-and-Solve.
- **In the action representation**, using code: CodeAct.
- **In the output**, by iterative self-critique: Self-Refine.

Reported gains are large on their chosen benchmarks. They usually cost many more tokens, or depend on resettable environments or reliable evaluators.

### Cited Findings
**Chain-of-Thought (Wei et al., 2022, arXiv 2201.11903)**: few-shot exemplars with intermediate reasoning steps. With PaLM-540B and 8 exemplars it reached state of the art on GSM8K, surpassing fine-tuned GPT-3 with a verifier (abstract, not re-read this session) — [CoT](https://arxiv.org/abs/2201.11903)

**Self-Consistency (Wang et al., 2022, arXiv 2203.11171)**: sample many CoT paths and take the majority vote over final answers. Reported gains over CoT: GSM8K +17.9%, SVAMP +11.0%, AQuA +12.2%, StrategyQA +6.4%, ARC-challenge +3.9% (abstract, not re-read this session) — [Self-Consistency](https://arxiv.org/abs/2203.11171). ReAct used CoT-SC with 21 samples at temperature 0.7 as a baseline — [ReAct](https://arxiv.org/abs/2210.03629)

**Reflexion (Shinn et al., NeurIPS 2023, arXiv 2303.11366)**: an outer loop around ReAct or CoT.
- Mechanism: an Actor (an LLM, ReAct or CoT) generates a trajectory. An Evaluator scores it, using exact match, heuristics, an LLM judge, or self-generated unit tests. A Self-Reflection LLM turns the sparse reward into a verbal lesson, stored in episodic memory bounded to Ω = 1–3 reflections. The next trial conditions on that memory. The authors call this "verbal reinforcement learning", with no weight updates — [Reflexion](https://arxiv.org/abs/2303.11366)
- ALFWorld heuristic trigger: reflect if the same action gets the same response for more than 3 cycles, or after more than 30 actions — [Reflexion](https://arxiv.org/abs/2303.11366)
- Results: ReAct+Reflexion solves 130/134 ALFWorld tasks (about +22 points absolute over 12 trials), while ReAct-only stalls between trials 6 and 7 at a 22% hallucination rate. HotpotQA improves by about 20 points. HumanEval Python pass@1 is 91.0 vs GPT-4's 80.1. HumanEval-Rust 68.0 vs 60.0; LeetcodeHard 15.0 vs 7.5. MBPP Python *dropped* (77.1 vs 80.1) — [Reflexion Table 1](https://arxiv.org/abs/2303.11366)
- Model dependence: with starchat-beta, Reflexion gives no gain on HumanEval (0.26 → 0.26). The authors say self-correction is "an emergent quality of stronger, larger models." HotpotQA ReAct+Reflexion: davinci-003 0.30→0.55, gpt-3.5 0.26→0.38, gpt-4 0.39→0.51 — [Reflexion App. A](https://arxiv.org/abs/2303.11366)
- Failure: on WebShop, Reflexion gives no significant improvement after 4 trials and produces unhelpful reflections. The authors conclude it "is unable to solve tasks that require a significant amount of diversity and exploration" — [Reflexion App. B.1](https://arxiv.org/abs/2303.11366)
- Caveat: the HotpotQA evaluator uses the ground-truth exact-match signal between trials (an oracle) — [Reflexion](https://arxiv.org/abs/2303.11366); LATS notes the same oracle setup — [LATS](https://arxiv.org/abs/2310.04406)

**Tree of Thoughts (Yao et al., NeurIPS 2023, arXiv 2305.10601)**: generalizes CoT into search over "thoughts".
- Mechanism: a thought generator (sample or propose), a state evaluator (the LM values each state as sure/maybe/impossible, or votes across states), and BFS (keep the best b) or DFS with pruning and backtracking. IO, CoT, CoT-SC and self-refinement are special cases — [ToT](https://arxiv.org/abs/2305.10601)
- Game of 24 with GPT-4: IO 7.3%, CoT 4.0%, CoT-SC (k=100) 9.0%, ToT b=1 45%, ToT b=5 **74%**; CoT best-of-100 49%. With GPT-3.5, ToT gets only 19% — [ToT](https://arxiv.org/abs/2305.10601)
- Mini Crosswords word-level success: IO 14%, CoT 15.6%, ToT 60%. Without backtracking it drops to 20% — [ToT](https://arxiv.org/abs/2305.10601)
- Cost: Game of 24 ToT costs $0.74 per case vs $0.47 for CoT best-of-100. Creative Writing costs about 5x more. The authors say ToT "could require 5-100 times more generated tokens than CoT." Gains on GSM8K (86→90) and StrategyQA (82→83) are marginal — [ToT App. B](https://arxiv.org/abs/2305.10601)
- ToT is reasoning-only: there are no environment actions.

**LATS: Language Agent Tree Search (Zhou et al., ICML 2024, arXiv 2310.04406)**: MCTS over ReAct trajectories.
- Mechanism: selection (UCT), expansion (sample n actions and execute them in the environment), evaluation (V(s) = λ·LM-score + (1−λ)·self-consistency score), simulation to a terminal state, backpropagation, and reflection on failure (Reflexion-style text stored in memory). Defaults are n=5 and k=50 trajectories for HotpotQA — [LATS](https://arxiv.org/abs/2310.04406)
- HotpotQA EM (GPT-3.5, acting): ReAct 0.32, ReAct best-of-k 0.38, Reflexion 0.51, ToT(ReAct) 0.39, RAP(ReAct) 0.54, **LATS 0.63**, LATS(CoT+ReAct) 0.71 — [LATS Table 3](https://arxiv.org/abs/2310.04406)
- WebShop (GPT-3.5): ReAct score 53.8 / SR 28.0; Reflexion 64.2 / 35.0; **LATS 75.9 / 38.0**; fine-tuning (Furuta et al.) 67.5 / 45.0. HumanEval pass@1 with GPT-4 is 92.7. Game of 24 (GPT-3.5): CoT 0.08, ToT 0.20, LATS 0.44 — [LATS](https://arxiv.org/abs/2310.04406)
- Ablations: removing the LM value function costs −0.26; using DFS instead of MCTS costs −0.21; removing reflection costs −0.05 — [LATS](https://arxiv.org/abs/2310.04406)
- Cost: about 173k tokens per success on HotpotQA (vs ToT about 210k, RAP about 177k). The authors admit "higher computational cost compared to simpler prompting methods like ReAct or Reflexion." LATS **requires the ability to revert the environment to earlier states** — [LATS §6, App. B](https://arxiv.org/abs/2310.04406)
- LATS also observes that on WebShop, Reflexion's reflections "are often generic and do not provide useful feedback", leaving the agent stuck in local minima — [LATS](https://arxiv.org/abs/2310.04406)

**ReWOO: Reasoning WithOut Observation (Xu et al., 2023, arXiv 2305.18323)**: decoupled planning.
- Mechanism: a Planner writes the whole blueprint up front as (Plan, #E_s = Tool[input]) pairs, where later steps can reference earlier evidence variables. Workers execute the tool calls. A Solver combines plans and evidence into the answer. Context and exemplars are sent twice rather than k times — [ReWOO](https://arxiv.org/abs/2305.18323)
- Cost argument: ReAct's input tokens grow quadratically with the number of steps k, because the context, exemplars and all prior T-A-O are re-sent on every call to a stateless API — [ReWOO Eq. 1–2](https://arxiv.org/abs/2305.18323)
- HotpotQA (gpt-3.5-turbo): ReAct 40.8% acc, 9,795 tokens, $19.59 per 1k queries; ReWOO 42.4%, 1,986 tokens, $3.97. Averaged over six benchmarks: −64% tokens and +4.4 points accuracy. SOTUQA: +8 points with 43% fewer tokens — [ReWOO Table 2](https://arxiv.org/abs/2305.18323)
- Tool failure (every tool returns "No evidence found"): ReAct loses 40.8 points (to zero) and *uses more* tokens; ReWOO loses 29.2 points — [ReWOO Table 3](https://arxiv.org/abs/2305.18323)
- ReAct failure tags on 100 HotpotQA failures: bad reasoning 76, tool inefficacy 20, token-limit excess 18. ReWOO: 51 / 29 / 0. ReAct ping-pongs between tool A and tool B until it hits the token limit — [ReWOO App. A.2](https://arxiv.org/abs/2305.18323)
- Extra tools hurt both methods: 17 of 20 failures when going from 2 to 7 tools were tool misuse — [ReWOO](https://arxiv.org/abs/2305.18323)
- Limitation stated by the authors: in environments with little prior information (ALFWorld), the planner must enumerate every possibility, so ReWOO degenerates to worst-case observation-dependent complexity — [ReWOO §4](https://arxiv.org/abs/2305.18323)
- Direct Prompt or CoT without tools beat both tool-using paradigms on several tasks, such as TriviaQA, where Direct got 80.6 vs ReAct 59.4 — [ReWOO Table 2](https://arxiv.org/abs/2305.18323)

**Plan-and-Solve prompting (Wang et al., ACL 2023, arXiv 2305.04091)**: zero-shot "first devise a plan, then carry out the subtasks." The PS+ variant adds detailed instructions. Reported to beat Zero-shot-CoT by a large margin and to be comparable to 8-shot CoT on math reasoning (abstract, not re-read this session) — [Plan-and-Solve](https://arxiv.org/abs/2305.04091)

**Toolformer (Schick et al., 2023, arXiv 2302.04761)**: tool use is *trained* rather than prompted. The model annotates its own corpus with candidate API calls (calculator, QA system, search engines, translation, calendar) and keeps the calls that lower the loss on future tokens. This gave substantially better zero-shot performance, often competitive with much larger models (abstract, not re-read this session) — [Toolformer](https://arxiv.org/abs/2302.04761). ReWOO notes that Toolformer samples tools independently and does not handle multi-step reasoning chains — [ReWOO §2.3](https://arxiv.org/abs/2305.18323)

**Self-Refine (Madaan et al., NeurIPS 2023, arXiv 2303.17651)**: a single LLM loops generate → self-feedback → refine, with no training and no external signal. It reports about 20% absolute average improvement across 7 tasks (abstract, not re-read this session) — [Self-Refine](https://arxiv.org/abs/2303.17651). Reflexion describes Self-Refine as "limited to single-generation reasoning tasks" — [Reflexion](https://arxiv.org/abs/2303.11366). LATS cites Huang et al. (2024): LMs "cannot self-correct their internal reasoning", which makes external feedback critical — [LATS](https://arxiv.org/abs/2310.04406)

**CodeAct (Wang et al., ICML 2024, arXiv 2402.01030)**: executable Python is the unified action space.
- Mechanism: each action is a Python snippet run in an interpreter, and the observation is the execution output or traceback. Control flow and data flow (loops, variables, composing several tools) fit in one action, and existing PyPI packages become tools — [CodeAct](https://arxiv.org/abs/2402.01030)
- M3ToolEval (82 multi-tool tasks, zero-shot, at most 10 turns): gpt-4-1106-preview reaches **74.4%** success with CodeAct vs 52.4% with JSON and 53.7% with text, and needs 5.5 vs 7.6–7.7 turns. Claude-2: 54.9 vs 39.0 / 29.3. CodeAct is best for 12 of 17 LLMs, and the gains widen as the model gets stronger. Headline: "up to 20% higher success rate" and "up to 30% fewer actions" — [CodeAct Table 3](https://arxiv.org/abs/2402.01030)
- On atomic single calls (API-Bank) the advantage disappears: JSON is best for GPT-4 (82.7 vs 76.7), which suggests closed models were fine-tuned for JSON tool calling — [CodeAct Table 2](https://arxiv.org/abs/2402.01030)
- Data: CodeActInstruct (7k multi-turn trajectories) → CodeActAgent (Llama-2 and Mistral-7B). The authors flag sandbox-escape risk — [CodeAct](https://arxiv.org/abs/2402.01030)

### Inferences
- **Reflexion and LATS** need a trustworthy success signal. Both papers use the HotpotQA ground truth as an oracle, so their QA numbers overstate what is achievable when a harness has no verifier. Coding, with tests, is where their evaluators are legitimately available.
- **Search methods (ToT, LATS)** need resettable state, and cost roughly 5–100x more tokens. That suits sandboxed code and branches, not side-effecting real-world tools.
- **ReWOO**'s efficiency gain comes mostly from cutting repeated prompts and exemplars, which prompt caching and KV-cache reuse in modern APIs partly neutralize. ReWOO's results were also measured on gpt-3.5 with few-shot exemplars.
- **CodeAct** foreshadows the convergence of modern coding agents on "bash/Python as the universal tool".

### Gaps
- Numbers for CoT, Self-Consistency, Plan-and-Solve, Toolformer and Self-Refine are from the abstracts as I remember them and were not re-fetched in this session. Verify them before quoting exact figures.
- No head-to-head comparison of all of these loops on one modern model and benchmark was found.

---

## Q3. Critiques: does interleaved reasoning actually help? Cost and latency

### Takeaway
Verma, Bhambri & Kambhampati (2024) find that on ALFWorld, ReAct's gains come from how similar the exemplars are to the query, not from interleaving or from thought content. Placebo thoughts and up-front "CoT" guidance do as well or better. Cost critiques (ReWOO, the 2026 Text-to-SQL work) show ReAct's context grows quadratically. Security work in 2026 argues that ReAct's observation-driven control flow is inherently open to prompt-injection hijacking. On the other side, 2026 evidence suggests a *plain* ReAct loop with good tools matches elaborate pipelines at a fraction of the latency.

### Cited Findings
**"On the Brittle Foundations of ReAct Prompting for Agentic LLMs" (Verma, Bhambri, Kambhampati, ASU; arXiv 2405.13966, May 2024)**
- Setup: ALFWorld with GPT-3.5-turbo, GPT-3.5-instruct, GPT-4 and Claude-3-Opus. Only the exemplars are perturbed — [Verma et al.](https://arxiv.org/abs/2405.13966)
- RQ1 (interleaving): moving all guidance into a single up-front think ("Exemplar-CoT") *improves* success. GPT-3.5-turbo 27.6→46.6, GPT-3.5-instruct 44.7→61.9, GPT-4 23.3→43.3. Claude-Opus dips from 56.6 to 50 — [Verma et al. Table 1](https://arxiv.org/abs/2405.13966)
- RQ2 (thought content): a placebo thought ("Take a deep breath and work on this problem step by step") gives comparable results: GPT-4 36.6 vs 23.3 base. Failure-only hindsight exemplars also improve the GPT models. Reversing the order of reasoning steps does not matter much. Opus does decline with placebo (56.6→30) — [Verma et al.](https://arxiv.org/abs/2405.13966)
- RQ3 (exemplar similarity): when both exemplars come from a *different* task type, success collapses to 0–6.6% for all models. Replacing object names with synonyms (spraybottle→aerosolbottle) drops GPT-3.5-turbo from 27.6 to 1.6. "Unrolling" (exemplar Put, query PutTwo) drops GPT-3.5-instruct from 52% to 9% — [Verma et al. Table 2](https://arxiv.org/abs/2405.13966)
- Thought operationalization: about 40% of the time, the action right after a think was invalid (GPT-3.5-instruct). For GPT-3.5-turbo it was about 80% — [Verma et al.](https://arxiv.org/abs/2405.13966)
- Cost: about 14M input tokens and 150K output tokens for 134 ALFWorld problems, "due to repeated prompting after each action execution" — [Verma et al. App. A](https://arxiv.org/abs/2405.13966)
- Conclusion: "performance of LLMs is driven by the similarity between input example tasks and queries... approximate retrieval rather than any inherent reasoning abilities" — [Verma et al.](https://arxiv.org/abs/2405.13966)
- Scope limit acknowledged by the authors: ALFWorld only, few-shot prompted models from April–May 2024 — [Verma et al. §7](https://arxiv.org/abs/2405.13966)

**Cost and latency**
- ReWOO's derivation: ReAct input tokens = k·Θ(Q+C+S) + Σ_j (k−j)·Θ(T_j+A_j+O_j), quadratic in the number of steps. Measured on HotpotQA: about 5x tokens vs ReWOO (9,795 vs 1,986) — [ReWOO](https://arxiv.org/abs/2305.18323)
- ReAct's few-shot exemplars, which include long Wikipedia observations, dominate the token budget and are re-sent about 5 times per HotpotQA question — [ReWOO App. A.1](https://arxiv.org/abs/2305.18323)
- 2026: KV-cache reuse is a recognized serving problem specific to ReAct agents (KVTether, arXiv 2609.39819, Sep 2026; title and abstract only seen) — [KVTether](https://www.alphaxiv.org/abs/2609.39819)

**Counter-evidence: simple ReAct is enough (2026)**
- "Iteration Without Elaboration" (Lu et al., Duke; arXiv 2608.22651, Aug 2026): a zero-shot think→act→observe loop over a typed 15-operation DSL. Results with Gemini-2.5-Flash:
  - Corrected BIRD mini-dev: 84.5%, vs CHESS 85.3% (about 20 LLM calls per question). Median latency 7.5 s vs 53.7 s.
  - EHR-SQL: 73.9%, best overall.
  - Ablation: iteration alone lifts EHR-SQL from 45.9% to 72.2% (+26.2, McNemar p≈10⁻⁴⁷) but barely moves BIRD (+0.6, not significant). The typed DSL adds +5.4 on BIRD.
  - Turns: 3.3 on average under a 15-turn cap. Batching up to 8 tool calls per turn is "a meaningful efficiency lever."
  - Source: [ReAct-SQL](https://arxiv.org/abs/2608.22651)
- Interpretation from the same paper: iteration solves *grounding* (probing an unfamiliar environment); typed actions solve *composition* — [ReAct-SQL](https://arxiv.org/abs/2608.22651)

**Security critique (2026)**
- "Securing Web Agents with the Compile-Then-Execute Paradigm" (Chow, …, Wagner, Piet; UC Berkeley/KACST; arXiv 2611.06039, Nov 4 2026). ReAct "collaps[es] observation and action selection into a single inference step," so untrusted page content arrives exactly when the next action is chosen. That opens a path to control-flow hijacking — [Baya](https://arxiv.org/abs/2611.06039)
- Results on WebArena Verified (581 tasks):
  - Utility: compile-then-execute (Baya) 77.8%, vs ReAct with web+API 66.7% and browser-only ReAct 55.1%.
  - WASP attack success rate: 0% vs 16.2% and 25.5%.
  - Latency: 327 s vs 87 s and 60 s.
  - Source: [Baya](https://arxiv.org/abs/2611.06039)
- Limits: compile-then-execute cannot handle "Replan-Needed" tasks, whose operations come from untrusted content (for example, "do what the email says"). The authors say ReAct remains preferable for highly dynamic sites, exploration-heavy tasks and multi-site workflows — [Baya §6](https://arxiv.org/abs/2611.06039)
- The paper builds on the earlier secure plan-then-execute line: CaMeL, FIDES, and Beurer-Kellner et al.'s design patterns — [Baya §7](https://arxiv.org/abs/2611.06039)

**Other critiques embedded in successor papers**
- LATS describes ReAct as "reflexive", with no consideration of alternative choices at each step — [LATS](https://arxiv.org/abs/2310.04406)
- OODA-Tool (2026) identifies "state-action competition" in ReAct-style policies (details under Q5) — [OODA-Tool](https://arxiv.org/abs/2608.24368)

### Inferences
- The Verma critique targets *few-shot prompted* ReAct on older models. Modern harnesses use instruction-tuned or RL-trained models with native function calling and no exemplars, so the exemplar-similarity finding may not carry over directly. The finding that thought content barely matters is still a caution against designing harnesses around elaborate scratchpad formats.
- The evidence converges on this: the *loop with environment feedback* is what matters (grounding, recovery). The *interleaved free-text thought* is less clearly causal.

### Gaps
- No 2025–2026 replication of the Verma ablations on frontier reasoning models with native tool calling was found.
- No systematic cost/latency comparison of ReAct vs plan-then-execute on frontier models with prompt caching was found.

---

## Q4. How ReAct-style loops became the default for tool-using agents and harnesses

### Takeaway
Practitioner guidance and 2026 papers alike describe the modern "agent" as a ReAct-shaped loop: the LLM calls tools, gets environment feedback, and repeats until done or a cap is hit. Native function calling replaced text-parsed `Action:` lines. Anthropic's Dec 2024 guidance explicitly reduces "agents" to this loop and recommends minimal frameworks.

### Cited Findings
- Anthropic, "Building effective agents" (Dec 19, 2024):
  - Agents "are typically just LLMs using tools based on environmental feedback in a loop."
  - "Workflows are systems where LLMs and tools are orchestrated through predefined code paths"; agents are systems where LLMs "dynamically direct their own processes and tool usage."
  - Agents should get "ground truth" from the environment at each step (tool results, code execution), and can pause for human feedback at checkpoints.
  - "It's also common to include stopping conditions (such as a maximum number of iterations) to maintain control."
  - The building block is the "augmented LLM" (retrieval, tools, memory).
  - Recommendations: "finding the simplest solution possible," starting with LLM APIs directly, and understanding any framework's underlying code.
  - Workflow patterns: prompt chaining, routing, parallelization, orchestrator-workers, evaluator-optimizer.
  - Source: [Anthropic](https://www.anthropic.com/engineering/building-effective-agents)
- 2026 papers treat ReAct as the dominant pattern:
  - "has since become the dominant design pattern for LLM agents" — [ReAct-SQL, arXiv 2608.22651](https://arxiv.org/abs/2608.22651)
  - "Web agents commonly follow the ReAct paradigm"; it is the dominant approach underlying WebArena baselines, WebVoyager, SeeAct and OpAgent — [Baya, arXiv 2611.06039](https://arxiv.org/abs/2611.06039)
- Reflexion and LATS keep ReAct as the inner actor and add outer loops. This is a common harness layering: an inner tool loop plus an outer retry/reflect loop — [Reflexion](https://arxiv.org/abs/2303.11366); [LATS](https://arxiv.org/abs/2310.04406)
- In CodeAct's general framework, each turn receives an observation from the user or the environment, optionally plans with CoT, and emits an action to the user (natural language) or to the environment (code). This is the shape of current coding-agent harnesses — [CodeAct §2.1](https://arxiv.org/abs/2402.01030)
- Mapping of Anthropic's patterns onto the research families:
  - evaluator-optimizer ≈ Self-Refine/Reflexion
  - orchestrator-workers ≈ ReWOO's Planner/Worker/Solver
  - parallelization/voting ≈ Self-Consistency
  - Source: pattern names from [Anthropic](https://www.anthropic.com/engineering/building-effective-agents); mechanisms from the respective papers above.

### Inferences
- The modern harness loop is: model emits text and/or structured tool calls → harness executes them → results are appended as observations → repeat until the model emits no tool call or a cap is hit. This is ReAct with native function calling in place of text-parsed actions, optional (often hidden) reasoning in place of explicit "Thought:" lines, and zero-shot system prompts in place of few-shot exemplars.
- The practices harnesses add on top all address ReAct failure modes documented above:
  - iteration caps
  - loop detection
  - context compaction, which addresses quadratic context growth (see [Context compression study, arXiv 2609.32961](https://www.alphaxiv.org/abs/2609.32961); title and abstract only seen)
  - batched or parallel tool calls
  - typed tool schemas

### Gaps
- I did not fetch the primary docs for Claude Code, the OpenAI Agents SDK (Runner loop) or LangGraph (prebuilt `create_react_agent`) in this session. Their loop semantics (run until a final output or a max-turns limit; handoffs; tool execution) should be confirmed from:
  - https://openai.github.io/openai-agents-python/
  - https://langchain-ai.github.io/langgraph/
  - https://docs.anthropic.com/en/docs/claude-code
- I found no rigorous history documenting the transition from text-parsed ReAct (LangChain's 2022–23 `ZERO_SHOT_REACT_DESCRIPTION`) to native function calling.

---

## Q5. ReAct vs OODA (Observe–Orient–Decide–Act) loops in the literature

### Takeaway
Until recently the OODA–ReAct comparison was mostly analogy in blogs and glossaries. In 2026, one peer-style paper (OODA-Tool, arXiv 2608.24368) operationalized OODA as a typed, controller-checked alternative to ReAct. It reports consistent gains over ReAct-LoRA and direct function calling on multi-turn tool use, largest on small models and on state-heavy turns. The key difference from ReAct is an explicit **Orient** stage: a persistent typed task state plus an execution-readiness gate.

### Cited Findings
- **OODA-Tool** (Guo, Huang, et al.; HUST, Knowin AI, KAUST, UvA and others; arXiv 2608.24368, Aug 2026):
  - Diagnosis: direct function-calling and ReAct policies "learn state tracking and action generation within the same autoregressive trajectory." The authors call the resulting failure **state-action competition**: "the pressure to produce the next call can overwrite or ignore information accumulated earlier." ReAct's reasoning is "free-form reasoning rather than... controller-checkable state" — [OODA-Tool](https://arxiv.org/abs/2608.24368)
  - The four stages:
    - Observe reconstructs a provenance-aware task state: goal, entities, active values, constraints, unfinished subgoals, recent tool facts.
    - Orient chooses a response mode: SOLVABLE_WITH_TOOL, NEED_CLARIFICATION, RESPOND_DIRECTLY, RECOVER_FROM_FAILURE or DONE. It also records missing slots and violated constraints.
    - Decide picks the action structure (single, sequential or parallel; dependencies) without filling in argument values.
    - Act binds grounded arguments into schema-valid calls.
    - A central controller enforces that Decide stays within what Orient allows, and validates schema and grounding.
    - Source: [OODA-Tool](https://arxiv.org/abs/2608.24368)
  - Results on ToolDial with Qwen3 0.6B–14B. Task success, ReAct-LoRA → Specialized OODA:
    - 0.6B: 65.43 → 85.10
    - 1.7B: 73.18 → 85.46
    - 14B: 84.77 → 94.90
    - Direct-LoRA comes in at 78.24–90.42, and the planner/caller/summarizer baseline α-UMi at 82.90–93.90. **ReAct-LoRA was worse than Direct-LoRA at every scale.**
    - Source: [OODA-Tool Table 1](https://arxiv.org/abs/2608.24368)
  - Where the gains come from: up to +16 points on long-history, missing-info, state-change and deep-dependency turns, but only +1–3 on parallel calls. The gains shrink with model scale. Orient and the Decide/Act split contribute most in ablations. The state–action contradiction rate is 3.9% for Specialized OODA vs 10.7% without the Decide–Act split — [OODA-Tool](https://arxiv.org/abs/2608.24368)
  - Cost: four stage calls per turn, so "Direct-LoRA remains the cheaper choice when one-pass latency is the primary concern" — [OODA-Tool](https://arxiv.org/abs/2608.24368)
  - Example failure fixed: the user picks osm_id_001; ReAct and Direct copy the local ID "museum_001" instead of the Wikidata ID Q123456 that the tool needs. OODA traces the selection to the right field — [OODA-Tool](https://arxiv.org/abs/2608.24368)
- Informal and practitioner comparisons, lower quality:
  - A glossary says the observation-action loop concept derives from Boyd's OODA (1976) and was applied to LLM agents via ReAct. LLM implementations typically add context management, stopping conditions and memory — [InsertChat glossary](https://insertchat.com/glossary/observation-action-loop)
  - A Rust crate's docs contrast ReAct (Think→Act→Observe; strength "explicit reasoning") with OODA (Observe→Orient→Decide→Act; strength "rapid adaptation"/situational awareness) — [beleth crate ooda.rs](https://docs.rs/crate/beleth/0.2.0-rc.1/source/src/ooda.rs)
- Related separation-of-concerns designs cited by OODA-Tool: StateFlow (explicit state machines), α-UMi (planner/caller/summarizer split), Plan-and-Act, and LLMCompiler (dependency scheduling) — [OODA-Tool related work](https://arxiv.org/abs/2608.24368)

### Inferences
- Conceptually, ReAct's "Thought" merges OODA's Orient and Decide into untyped text, and its state lives only in the growing transcript. OODA-Tool's evidence suggests that making Orient explicit (persistent typed state plus a readiness gate: act, ask, recover or stop) helps most where ReAct is weakest: long histories, changing constraints, and missing info that should trigger clarification rather than a premature call.
- For harness design, the lightweight version is a maintained task-state or scratchpad artifact (todo list, plan file) plus an explicit "should I act, ask, or stop?" check before tool calls. This captures the Orient benefit without four model calls per turn.
- The evidence is from fine-tuned small open models (≤14B, LoRA) on ToolDial. The benefit narrows with scale, so it may be small for frontier models.

### Gaps
- No study comparing OODA-structured and ReAct loops on frontier models with native tool calling, or on coding-agent benchmarks such as SWE-bench, was found.
- No academic work was found that maps Boyd's original OODA writings rigorously onto LLM agents beyond OODA-Tool's motivation section.
- OODA-Tool is a single recent preprint (Aug 2026) with no independent replication yet.
