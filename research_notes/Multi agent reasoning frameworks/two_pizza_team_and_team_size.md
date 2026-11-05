# Two-Pizza Teams and the Science of Team Size (Human Teams vs. LLM Agent Teams)

Research date: 2026-11-05. Note: `docs.aws.amazon.com` and `the-decoder.com` could not be fetched (blocked in this session's network settings), so AWS whitepaper text comes only from search snippets. Classic human-team papers marked [bibliographic] are cited from standard bibliographic records (DOI/journal). Their full text was not re-fetched in this session, so check page-level numbers before quoting them.

---

## Q1. Origin and actual practice of Amazon's two-pizza team rule

### Takeaway
The "two-pizza team" was a Bezos-era Amazon structural rule from the early 2000s. Teams had to be small enough to be fed by two pizzas (usually glossed as under ~10 people), autonomous, and loosely coupled to other teams through service interfaces. Insider accounts (Bryar & Carr, *Working Backwards*, 2021) say Amazon later concluded that team size was **not** the main predictor of success. The leader was. The concept evolved into "single-threaded leaders" (STL) running "separable, single-threaded teams". The well-known "small team = good" moral is therefore a simplification of what Amazon itself learned.

### Cited Findings
- **Official AWS framing:** AWS's whitepaper *Introduction to DevOps on AWS* has a "Two-Pizza Teams" section in its "Communication and Collaboration" chapter. It describes Bezos's rule as creating teams "no larger than can be fed by two pizzas" so that collaboration stays strong. First published December 2014; HTML revised 2023; PDF © 2024. — [AWS whitepaper, Two-Pizza Teams](https://docs.aws.amazon.com/whitepapers/latest/introduction-devops-aws/two-pizza-teams.html); [PDF](https://docs.aws.amazon.com/whitepapers/latest/introduction-devops-aws/introduction-devops-aws.pdf); [Communication & Collaboration](https://docs.aws.amazon.com/whitepapers/latest/introduction-devops-aws/communication-collaboration.html) (content from search snippet; direct fetch blocked)
- A separate AWS public-sector whitepaper page, "Two pizza teams, from Ops to DevOps", is marked historical/reference-only. — [AWS public-sector cloud transformation](https://docs.aws.amazon.com/whitepapers/latest/public-sector-cloud-transformation/two-pizza-teams-from-ops-to-devops.html)
- AWS has used the concept as a marketing/conference theme, e.g., the re:Invent talk "ENT201 A Tale of Two Pizzas: Accelerating Software Delivery with AWS Developer Tools". — [SlideShare](https://de.slideshare.net/AmazonWebServices/ent201-a-tale-of-two-pizzas-accelerating-software-delivery-with-aws-developer-tools)
- **Fitness function:** According to book notes on *Working Backwards*, the original two-pizza rules included evaluating each team by a well-defined "fitness function", described as a weighted average of selected metrics relevant to that team. One set of notes says this was later reverted to input metrics, because complex composite functions obscured what a team was actually doing to move them. — [Matthew Kudija notes](https://matthewkudija.com/reading-notes/2023-06-02-Working-Backwards.html); [Evan's Notes](https://evansamek.substack.com/p/working-backwards-by-colin-bryar); [Merlin Rebrović notes](https://merlin.rebrovic.net/books/notes/working-backwards/) (secondary; the "abandoned/reverted" detail comes from only one set of notes)
- **Amazon's own revision:** Summaries of *Working Backwards* report that Amazon found team size was not a good predictor of a team's success. What mattered was whether the team had a leader with the right skills, authority and singular focus. The book lists two-pizza teams among earlier solutions that "ultimately didn't last". — [Working Backwards summaries (Medium, Keqiu)](https://medium.com/keqius-management-notes/working-backwards-e3a8ea5a99ab); [Manas Saloi summary](https://manassaloi.com/booksummaries/2022/06/24/working-backwards-bryar-carr.html); [Andrew Clark notes](https://andrewclark.co.uk/all-media/working-backwards)
- **Single-threaded leadership:** "a single person, unencumbered by competing responsibilities, owns a single major initiative and heads up a separable, largely autonomous team." The authors say they borrowed "single-threaded" from computer science. — [Pedro del Gallego, "Single-Threaded Leaders at Amazon"](https://pedrodelgallego.github.io/blog/amazon/single-threaded-model); [Working Backwards (Pan Macmillan)](https://www.panmacmillan.com/authors/colin-bryar/working-backwards/9781529033854)
- Bryar and Carr joined Amazon in the late 1990s and worked closely with Bezos. Bryar was Bezos's technical advisor ("shadow"). This makes the book the strongest insider source. — [Pan Macmillan](https://www.panmacmillan.com/authors/colin-bryar/working-backwards/9781529033854)
- **Architectural coupling (Conway's Law link):** The two-pizza structure went together with Amazon's move to service-oriented architecture. The best-known (unofficial) account is Steve Yegge's 2011 "Platform rant". It describes a c.2002 Bezos mandate that all teams expose data and functionality only through service interfaces, with no other form of inter-process communication. — [Yegge Platform Rant (gist)](https://gist.github.com/chitchcock/1281611) [bibliographic; secondhand, an ex-Amazon engineer's recollection, not an official document]
- Conway's Law origin: M. Conway, "How Do Committees Invent?", *Datamation*, April 1968: organizations "are constrained to produce designs which are copies of the communication structures of these organizations." — [melconway.com](https://www.melconway.com/Home/Committees_Paper.html) [bibliographic]
- Brad Stone's *The Everything Store* (2013) also tells the two-pizza story as part of Bezos's push for decentralized, autonomous teams around 2002. — [bibliographic; not fetched]

### Inferences
- Amazon's "rule" was really a bundle: (1) a small team size, (2) end-to-end ownership with minimal dependencies, (3) a measurable objective (fitness function, later input metrics), and (4) API-mediated decoupling. The insiders' own retrospective puts (2) and the leader ahead of raw headcount. That matters for any agent analogy: the transferable idea is "separable work plus a single accountable owner plus a narrow interface", not "N ≤ 10".
- The commonly quoted "6–10 people" is a popular-press gloss. I found no official Amazon document specifying an exact number. AWS's own text says only "fed by two pizzas".

### Gaps
- I could not access the primary text of *Working Backwards* (ch. 3, "Organizing: Separable, Single-Threaded Leadership") or *The Everything Store* to quote the exact team-size figure, the date of the 2002 offsite, or the exact fitness-function wording.
- No official Amazon/AWS source fixes the 2002 API mandate. Yegge's rant is the de facto source.

---

## Q2. Academic evidence on optimal human team size and why small teams work

### Takeaway
The evidence converges on "small, usually fewer than 10, often about 4–6" for interdependent knowledge work. There are three mechanisms: (a) communication paths grow quadratically (n(n−1)/2), (b) coordination losses plus motivation losses (Ringelmann effect, social loafing), and (c) a task-type moderator (Steiner 1972). Additive, disjunctive, conjunctive and compensatory tasks scale differently. Nature-scale bibliometrics add a qualitative twist: small teams disrupt, large teams develop. Popular "magic numbers" (4.6, 7±2, Dunbar 150) come from narrow studies and should not be treated as universal constants.

### Cited Findings
**Brooks's Law and communication overhead**
- Brooks's Law: "Adding manpower to a late software project makes it later." F. P. Brooks, *The Mythical Man-Month* (1975; anniversary ed. 1995). Brooks argues that if each part of a task must be coordinated with every other part, communication effort grows as n(n−1)/2. — quoted in [Mieczkowski et al. 2026, arXiv:2603.12229](https://arxiv.org/abs/2603.12229); [bibliographic for the n(n−1)/2 passage]
- Hackman gives the arithmetic in his HBR interview: a 6-person team has 15 links and a 12-person team has 66. He advises keeping teams in single digits. — [Coutu, "Why Teams Don't Work", HBR, May 2009](https://hbr.org/2009/05/why-teams-dont-work) [bibliographic; not fetched]

**Ringelmann effect and social loafing**
- Ringelmann (1913) observed per-person rope-pulling force falling as group size rose. Ingham, Levinger, Graves & Peckham (1974) replicated the drop using pseudo-groups (participants believed others were pulling), which isolated motivation loss from coordination loss. — [Ingham et al. 1974, *J. Exp. Soc. Psych.* 10(4):371–384, doi:10.1016/0022-1031(74)90033-X](https://doi.org/10.1016/0022-1031(74)90033-X) [bibliographic]; Ringelmann/Ingham also summarized in [Fortuna & Bertalanič 2026, arXiv:2609.31563](https://arxiv.org/abs/2609.31563)
- Latané, Williams & Harkins (1979), "Many hands make light the work". In clapping and shouting tasks, per-person output fell with group size. As commonly reported, 2-person groups produced ~71% and 6-person groups ~40% of the sum of their individual capacities. The authors coined "social loafing". — [*JPSP* 37(6):822–832, doi:10.1037/0022-3514.37.6.822](https://doi.org/10.1037/0022-3514.37.6.822) [bibliographic; verify exact percentages against the paper]
- Karau & Williams (1993) meta-analysis (78 studies) found social loafing robust across tasks and populations, with an average effect of about d ≈ 0.44. Their Collective Effort Model predicts less loafing when individual contributions are identifiable or evaluable, when the task is meaningful, and when the group is valued. — [*JPSP* 65(4):681–706, doi:10.1037/0022-3514.65.4.681](https://doi.org/10.1037/0022-3514.65.4.681) [bibliographic; verify study count and effect size]
- **Steiner's task taxonomy** moderates size effects. Additive tasks (Ringelmann) show per-member losses. On disjunctive tasks, success requires that one member finds the answer. Compensatory tasks (averaging, Galton's ox where the median was within 0.8%) benefit from size only if errors are independent and unbiased. Kerr & Bruun (1983) showed that losses are mediated by task type and perceived dispensability of effort. — summarized in [Fortuna & Bertalanič, arXiv:2609.31563 (Sept 2026)](https://arxiv.org/abs/2609.31563)

**Hackman: optimum ~4.6, "no double digits"**
- Hackman & Vidmar (1970) varied group size from 2 to 7 across tasks. They asked members whether the group was too small or too large and estimated the optimum at **4.6 members**. Hackman repeats this in *Leading Teams* (2002) as suggestive rather than definitive. — [Fortune, "The power of number 4.6", June 2006](https://money.cnn.com/magazines/fortune/fortune_archive/2006/06/12/8379238/index.htm); Hackman & Vidmar, *Sociometry* 33(1):37–54 [bibliographic]
- Jennifer Mueller (Wharton) argued that large teams suffer "relational loss": members feel less supported. The Fortune piece quotes her: "They'll form cliques". I found no source showing Mueller endorsed 4.6 specifically. — [Fortune 2006](https://money.cnn.com/magazines/fortune/fortune_archive/2006/06/12/8379238/index.htm)

**Software teams: Hoegl, QSM/Putnam, Scrum**
- Hoegl (2005), "Smaller teams – better teamwork: How to keep project teams small". It draws on teamwork-quality data from German software development teams (Hoegl & Gemuenden's ~145-team dataset) and finds teamwork quality declines as team size grows. It recommends keeping project teams small (roughly under 10) and offers structural tactics for doing so. — [*Business Horizons* 48(3):209–214, doi:10.1016/j.bushor.2004.10.013](https://doi.org/10.1016/j.bushor.2004.10.013) [bibliographic; verify sample size]
- QSM (Putnam & Myers, 1997 study, revisited in 2012 and 2025). The authors concluded that "selecting the right team size — small — is the key to a successful project". Larger teams took far more effort, and the gap widened with project size. Average schedules: ~13.6 months for teams of 1.5–3 people and 11.9 months for 3–5. "Best in Class" projects used teams more than 4× smaller on average than worst performers. The 2012 repeat used 1,060 IT projects (2006–2011). Another QSM analysis splits >10,000 projects into ≤4 FTE vs ≥5 FTE. — [QSM node/326](https://qsm.com/node/326); [QSM 2012 "Top performing projects use small teams"](https://qsm.com/blog/2012/top-performing-projects-use-small-teams); [QSM 2025 "4 key studies on team size"](https://qsm.com/blog/2025/4-key-studies-team-size); [QSM 2025 Part II](https://qsm.com/blog/2025/part-ii-team-size-and-productivity)
- QSM counterpoint: productivity (size/effort) rises with project size overall, while within each size quartile it falls as staff increases. An ISBSG-based paper reports that average team size ≥9 is less productive. — [QSM 2025 Part II](https://qsm.com/blog/2025/part-ii-team-size-and-productivity); [Empirical findings on team size (Bohrium)](https://www.bohrium.com/paper-details/empirical-findings-on-team-size-and-productivity-in-software-development/813377052496363522-2502)
- Scrum Guide: the 2017 edition specified 3–9 Development Team members. The 2020 edition says the Scrum Team is "typically 10 or fewer people". — [scrumguides.org](https://scrumguides.org/scrum-guide.html) [bibliographic]

**Large teams develop, small teams disrupt**
- Wu, Wang & Evans (2019) analyzed >65 million papers, patents and software products (1954–2014). As team size grows, work becomes less disruptive (lower CD index) and more developmental: small teams disrupt science and technology with new ideas, while large teams develop existing ones. — [*Nature* 566:378–382, doi:10.1038/s41586-019-0941-9](https://doi.org/10.1038/s41586-019-0941-9) [bibliographic]

**Dunbar's layers**
- Social-group sizes form a discrete hierarchy of about 5, 15, 50 and 150 (scaling ratio ~3). Zhou, Sornette, Hill & Dunbar (2005). This is evidence about cognitive limits on relationships, not about task-team performance. — [*Proc. R. Soc. B* 272:439–444, doi:10.1098/rspb.2004.2970](https://doi.org/10.1098/rspb.2004.2970) [bibliographic]

### Inferences
- **Mechanisms that could transfer to agents:** quadratic channel growth, coordination losses, and task-type dependence (Steiner). **Mechanisms that probably do not transfer:** motivation loss and social loafing, since LLMs do not withhold effort for social reasons. However, there are agent analogues: "agreeableness"/sycophancy, information withholding, and correlated errors (see Q3).
- The "magic numbers" are inconsistent: 4.6 (Hackman–Vidmar, groups of 2–7, self-report), "single digits" (Hackman), 3–9 or ≤10 (Scrum), ≤4 FTE (QSM). The robust claim is directional: smaller, with fewer interdependencies, is better for coordination-heavy work.

### Gaps
- I did not fetch the full texts of Hackman & Vidmar, Latané et al., Karau & Williams, Hoegl, or Wu–Wang–Evans in this session. Exact effect sizes and percentages above should be checked against the originals.
- No popular claim of "5–7 optimal" from QSM was found. QSM's own buckets are 1.5–3, 3–5, ≤4 or ≥5.

---

## Q3. Empirical evidence on agent count and topology in multi-agent LLM systems

### Takeaway
More agents helps reliably only when agents are **independent samplers plus a selector** on difficult, verifiable tasks (voting/ensembles), and even then gains saturate quickly. Once agents must **coordinate**, the best controlled studies (2025–2026) find:
- coordination overhead grows super-linearly;
- multi-agent benefit vanishes or turns negative once the single agent is already good (≥~45% baseline);
- sequential or tool-heavy tasks degrade;
- performance is governed by task decomposability and topology/verification, not headcount.

Reported optima are small: about 3–7 agents in controlled tests. The exception is MacNet (~16 nodes "reasonable", saturation near ~100), but it uses a pipelined critic–actor DAG that passes only artifacts. This pattern fits the two-pizza heuristic in direction, though for different reasons.

### Cited Findings
**Independent sampling and voting ("More Agents")**
- Li et al., "More Agents Is All You Need" (Tencent; TMLR 10/2024; arXiv 2402.05120). Sampling and voting scales with ensemble size up to 40. GSM8K: Llama2-13B rises from 0.35 to 0.59 at 40 agents, beating single Llama2-70B (0.54). Llama2-70B rises from 0.54 to 0.74, and GPT-3.5 from 0.73 to 0.85. Relative gains grow with task difficulty: Llama2-13B gains 69% on GSM8K and 200% on MATH, versus 16%/34% for GPT-3.5. Gains "increase then decrease" with inherent difficulty and taper at the hardest level. Combining with Debate failed on HumanEval for Llama2 (0 → 0) because referencing others' answers "disrupt[s] the coherence of the code logic". Debate was capped at 10 agents due to communication overhead. — [arXiv:2402.05120](https://arxiv.org/abs/2402.05120)
- Fortuna & Bertalanič, "Multi-agent Scaling Across Disjunctive and Compensatory Tasks" (arXiv 2609.31563, 25 Sep 2026). Setup: 13 open-weight models (3B–20B), teams N ∈ {1…30}, ~6.8×10^7 generations.
  - pass@30 rises well above solo (GSM8K 34.3% → 54.4%), but plurality voting realizes "almost none of this potential" (Round-1 GSM8K 34.06% at N=2 vs 34.31% at N=30).
  - Multi-round revision nearly doubles GSM8K (34.1% → 61.9% at N=5), but the gain is the same with 1 peer as with 29 (26.5 vs 26.6 points).
  - Intra-class correlation ρ is 0.64–0.93, so effective team size N_eff(30) is only ~1.07–1.53.
  - On Fermi estimation, item-level bias explains ~87% of squared error, so averaging cuts error only ~6%.
  - Heterogeneous model pools help (ρ=0.37, N_eff≈2.0) but do not beat the best member on disjunctive tasks.
  - The paper explicitly invokes Steiner, Ringelmann and Latané. — [arXiv:2609.31563](https://arxiv.org/abs/2609.31563)

**Debate (Du et al.)**
- Du, Li, Torralba, Tenenbaum, Mordatch, "Improving Factuality and Reasoning in Language Models through Multiagent Debate" (arXiv 2305.14325, May 2023; ICML 2024).
  - With 3 agents × 2 rounds (gpt-3.5-turbo): arithmetic 67.0% → 81.8%, GSM8K 77.0% → 85.0%, MMLU 63.9% → 71.1%.
  - Arithmetic performance rises monotonically with agents (tested 1–5+; summarization was needed beyond ~5 due to context length) and with rounds, but more than 4 rounds gave no gain over 4.
  - Agents were "relatively agreeable". Most experiments used just 3 agents "due to computational expense". — [arXiv:2305.14325](https://arxiv.org/abs/2305.14325)

**Topology at scale (MacNet)**
- Qian et al., "Scaling Large-Language-Model-based Multi-Agent Collaboration" (MacNet; ICLR 2025; arXiv 2406.07155). Agents sit in DAGs (critic on edges, actor on nodes), and only refined artifacts propagate, not full dialogues.
  - The study scales from 2^0 to 2^6 nodes (>1,000 agents in mesh, counting edges) and finds a "collaborative scaling law": logistic growth f(|V|) = γ/(1+e^(−β(log|V|−α)))+δ. "A node magnitude of 2^4 appears to be a reasonable choice"; most topologies saturate at "approximately a hundred agents".
  - Irregular (random/small-world) topologies beat regular ones. Random reached 0.6522 quality vs mesh 0.6316 and chain 0.6078, with ~51.92% less time than mesh.
  - Dense mesh can cause "information overload". Wider stars beat deeper trees. Divergent topologies beat convergent ones (aggregation is hard).
  - Baselines: majority voting gains only 0.9% and plateaus at ~8 agents. AgentVerse (star) hits context explosion above ~30 agents. — [arXiv:2406.07155](https://arxiv.org/abs/2406.07155)
- Exchange-of-Thought (Yin et al., EMNLP 2023, arXiv 2312.01823) compares Memory/Report/Relay/Debate communication topologies. Numbers were not extracted in this session. — [arXiv:2312.01823](https://arxiv.org/abs/2312.01823)

**Controlled architecture study (Google/DeepMind/MIT)**
- Kim et al., "Towards a Science of Scaling Agent Systems" (Google Research/DeepMind/MIT; arXiv 2512.08296, v1 Dec 2025, v3 8 Apr 2026). Setup: 260 configurations, 6 agentic benchmarks (BrowseComp-Plus, Finance-Agent, PlanCraft, Workbench, SWE-bench Verified, Terminal-Bench), 5 architectures (SAS; MAS Independent/Centralized/Decentralized/Hybrid), 3 LLM families, matched token budgets (~4,800 reasoning tokens per trial).
  - **Mean MAS improvement across everything: −0.3%** (95% CI −58.7% to +77.2%). The range runs from +80.8% (Finance, Centralized) to −70.0% (PlanCraft, Independent). All MAS variants degrade sequential planning by 39–70%.
  - **Capability saturation:** when the single-agent baseline exceeds ~45%, adding agents gives negative returns (β = −0.236, p=0.004). This is the only effect that survives cluster-robust inference and Holm correction (p_Holm=0.018). Agent count alone, log(1+n_a), is **not** significant (β=0.040, p=0.487).
  - **Turns follow a power law in agent count:** T = 2.72 × (n+0.5)^1.724 (R²=0.974). The authors read the exponent as "quadratic message complexity … tempered by practical bandwidth limits". They conclude that under fixed budgets "per-agent reasoning capacity becomes prohibitively thin beyond 3–4 agents."
  - **Overhead:** Independent 58%, Decentralized 263%, Centralized 285%, Hybrid 515%. Success per 1K tokens: SAS 67.7, Independent 42.4, Decentralized 23.9, Centralized 21.5, Hybrid 13.6.
  - **Error amplification:** Independent 17.2× vs Centralized 4.4×, showing that a verification bottleneck matters.
  - **Message density saturates** near c* ≈ 0.39 messages/turn.
  - **Agent-count sweep (1, 3, 5, 7, 9):** Gemini-2.0 Flash peaks at **7 agents** and then degrades. Gemini-2.5 Pro peaks earlier, and centralized shows diminishing returns beyond **5**.
  - The authors cite human team research [30, 31] as motivation and reject "more agents is all you need". — [arXiv:2512.08296](https://arxiv.org/abs/2512.08296)

**Distributed-systems framing (Brooks's Law explicitly)**
- Mieczkowski, Collins, Sucholutsky, Vélez, Griffiths, "Language Model Teams as Distributed Systems" (Princeton/MIT/Cambridge/NYU; arXiv 2603.12229, 12 Mar 2026). The paper opens with Brooks's Law. Setup: teams of 1–5 (Claude Sonnet 4.6, Gemini 3 Flash, GPT-5.2) on coding tasks with parallel/mixed/serial dependency structure.
  - Speedup follows Amdahl's Law ordering (Kruskal-Wallis H=61.4, p<0.001) but stays below the bound.
  - **Preassigned (centralized) teams achieved median 1.36× speedup vs 0.88× for self-coordinating (decentralized) teams.** Decentralized teams were *slower than one agent*.
  - Decentralized teams had concurrent writes, rewrites and out-of-order work, with median 19 test failures vs 4.
  - Token cost scaled with team size (Spearman ρ=0.40) while speedup did not (ρ=−0.07). On serial tasks the token multiplier was 5.83× for 1.13× speedup.
  - Example: Claude Sonnet 4.6 on the parallel task, preassigned: 1.80× (N=2), 2.42× (3), 2.78× (4), 3.35× (5). Decentralized: 1.50× (2), 0.94× (3), 0.56× (4). — [arXiv:2603.12229](https://arxiv.org/abs/2603.12229)

**Failure taxonomy (MAST)**
- Cemri et al., "Why Do Multi-Agent LLM Systems Fail?" (UC Berkeley; NeurIPS 2025 D&B; arXiv 2503.13657). Data: 1,642 annotated traces from 7 MAS frameworks; 14 failure modes in 3 categories; human κ=0.88, LLM-judge κ=0.77.
  - Failure rates of 41%–86.7% across 7 SOTA open-source MAS.
  - Category shares (Fig. 1): System design 44.2%, Inter-agent misalignment 32.3%, Task verification 23.5%.
  - Top modes: step repetition 15.7%, reasoning-action mismatch 13.2%, unaware of termination 12.4%, disobey task spec 11.8%.
  - The paper explicitly invokes organizational theory: "good MAS design requires organizational understanding – even organizations of sophisticated individuals can fail catastrophically if the organization structure is flawed". It cites high-reliability organizations research.
  - Role-spec fixes gave +9.4% (ChatDev). A high-level verification step gave +15.6%. — [arXiv:2503.13657](https://arxiv.org/abs/2503.13657)

**Anthropic production guidance (June 2025)**
- Anthropic, "How we built our multi-agent research system" (13 Jun 2025).
  - Scaling rules embedded in prompts: "Simple fact-finding requires just 1 agent with 3-10 tool calls, direct comparisons might need 2-4 subagents with 10-15 calls each, and complex research might use more than 10 subagents."
  - Early failure: "spawning 50 subagents for simple queries."
  - Multi-agent (Opus 4 lead + Sonnet 4 subagents) beat single-agent Opus 4 by 90.2% on an internal research eval.
  - Agents use ~4× and multi-agent systems ~15× the tokens of chat. Token usage alone explains 80% of BrowseComp variance.
  - Caveats: "rapid growth in coordination complexity". Domains "that require all agents to share the same context or involve many dependencies between agents are not a good fit", e.g., "most coding tasks involve fewer truly parallelizable tasks than research." — [Anthropic Engineering](https://www.anthropic.com/engineering/multi-agent-research-system)

**Other 2026 papers found (abstract-level only, not read in full)**
- Yang et al., "Understanding Agent Scaling in LLM-Based MAS via Diversity" (arXiv 2602.03794, Feb 2026): homogeneous teams saturate, and diversity drives scaling. — [arXiv:2602.03794](https://arxiv.org/abs/2602.03794)
- Pappu et al., "Multi-agent teams hold experts back" (arXiv 2602.01011, 2026): LLM teams fall short of their best member (as cited by 2603.12229 and 2609.31563). — [arXiv:2602.01011](https://arxiv.org/abs/2602.01011)
- "Drop the Hierarchy and Roles: How Self-Organizing LLM Agents Outperform Designed Structures" (MIPT; arXiv 2603.28990, Mar 2026): 25,000 tasks, 8 models, 4–256 agents, 8 protocols. It claims self-organization beats designed hierarchies, which partly conflicts with 2603.12229's centralized advantage. — [arXiv:2603.28990](https://arxiv.org/abs/2603.28990)
- "Agensh: Scaling Organizational Intelligence to 1,024 Agents" (Microsoft Research; arXiv 2609.26781, Sep 2026), aimed at latency via concurrency. — [arXiv:2609.26781](https://arxiv.org/abs/2609.26781)
- "Scaling Multi-Agent Intelligence with Substrate-Centric Coordination" (Harvard; arXiv 2610.16120, Oct 2026): identifies "reading burden that grows with the group" and diluted information as reasons MAS scale poorly. — [arXiv:2610.16120](https://arxiv.org/abs/2610.16120)
- "Scaling Inference-Time Compute with Teams of Coding Agents" (Cohere; arXiv 2610.17471, Oct 2026). — [arXiv:2610.17471](https://arxiv.org/abs/2610.17471)
- "Does Multi-Agent Collaboration Pay When Agents Serve Users?" (UPenn; arXiv 2610.27655, Oct 2026), testing Kim et al.'s findings in dual-control settings. — [arXiv:2610.27655](https://arxiv.org/abs/2610.27655)
- Bertalanič & Fortuna (2026) fit a Ringelmann-inspired law for effective team size N_eff/N across 44 conditions. Only heterogeneous teams escape hard ceilings (as cited in arXiv:2609.31563). ID not retrieved.

### Inferences
- **Converging numbers:** controlled coordinating-agent studies put optima at about 3–7 agents (Kim et al.: 3–4 under fixed budget, peaks at 5–7; Du et al.: 3 agents, ≤4 rounds; Mieczkowski et al.: decentralized gains vanish at N≥3). That is roughly "one pizza", even smaller than two-pizza human teams. Independent-voting ensembles tolerate larger N (8–40) but saturate because of correlated errors (N_eff ≈ 1–2).
- **Mechanisms that differ from human teams:**
  - No motivation loss, but correlation and "agreeableness" replace it. Same-model agents are a "crowd within" one mind (ρ 0.64–0.93).
  - Context and token budgets replace attention limits. The budget is split across agents, so each agent's reasoning gets thinner.
  - Overhead turns grow ~n^1.72, close to Brooks's n(n−1)/2.
- **Amazon's actual lesson maps better than the headcount:** separable work (task decomposability, the Amdahl p), a single-threaded owner (centralized orchestrator or verifier, which cuts error amplification from 17.2× to 4.4×), and narrow interfaces (MacNet propagating only artifacts, Anthropic's subagents returning condensed results) are the empirically supported transfers.

### Gaps
- No study directly tests "two-pizza" sizes (6–10) as a hypothesis for agents. Kim et al. sweep only up to 9, and Mieczkowski et al. only up to 5.
- Exchange-of-Thought numerical results were not extracted.
- The self-organizing claims in 2603.28990 and Agensh at 1,024 agents were not read in full, so their conditions (e.g., latency vs accuracy goals) are unverified.

---

## Q4. Who explicitly connects two-pizza teams, Conway's Law or Brooks's Law to agent-system design (2024–2026)?

### Takeaway
Academic work explicitly links agent teams to **Brooks's Law and Amdahl's Law** (Mieczkowski et al. 2026), **Steiner, Ringelmann and social loafing** (Fortuna & Bertalanič 2026), **organizational theory and high-reliability organizations** (Cemri et al. 2025), and **human team-effectiveness research** (Kim et al. 2025). **Conway's Law** for agents appears mostly in practitioner essays from 2026. **"Two-pizza"** appears almost only in business blogs about *human* team size shrinking because of AI agents, not about how many agents to use. Reports that Anthropic now calls heavy subagent use "Conway's Law" were found only secondhand and could not be verified.

### Cited Findings
- Academic explicit links: Brooks's Law epigraph plus the Amdahl's Law test in [Mieczkowski et al., arXiv:2603.12229](https://arxiv.org/abs/2603.12229); Steiner, Ringelmann, Latané and Kerr & Bruun in [Fortuna & Bertalanič, arXiv:2609.31563](https://arxiv.org/abs/2609.31563); organization design and HROs in [Cemri et al., arXiv:2503.13657](https://arxiv.org/abs/2503.13657); human team-performance literature in [Kim et al., arXiv:2512.08296](https://arxiv.org/abs/2512.08296).
- MacNet notes that the success of irregular topologies "suggests that collaboration patterns in an agent's world need not precisely mirror those in human society". This is an explicit caution against copying human org charts. — [arXiv:2406.07155](https://arxiv.org/abs/2406.07155)
- Conway's Law essays for agents:
  - Tian Pan, "Conway's Law Comes for Your Agent Fleet" (30 Jun 2026): agent graphs copy team boundaries, so design the topology from the problem's shape; otherwise "Conway's Law claws it back". — [tianpan.co](https://tianpan.co/blog/2026/06/30/conways-law-comes-for-your-agent-fleet)
  - "Conway's Law Under Cognitive Constraint" (Sep 2026). — [danieltan.weblog.lol](https://danieltan.weblog.lol/2026/09/conways-law-under-cognitive-constraint)
  - Josef Dijon, "From Code to Conway: Architecting the Future with Agentic AI Teams", which proposes an inverse-Conway approach: design the agent architecture first, then arrange teams. — [Medium](https://medium.com/@josef-dijon/from-code-to-conway-architecting-the-future-with-agentic-ai-teams-3b4b1ebedc05)
  - Team Topologies mapped onto agents. — [Medium (Ait El Harraj)](https://medium.com/@amine.aitelharraj/-3eb5cd3dbcea)
  - "How organizations shape their agentic systems". — [reynders.co](https://reynders.co/blog/how-organizations-shape-their-agentic-systems/)
- "The Specification Gap: Coordination Failure Under Partial Knowledge in Code Agents" (arXiv 2603.24284, 2026) treats the shared spec as the "communication structure" in a Conway-style framing. — [arXiv:2603.24284](https://arxiv.org/abs/2603.24284)
- **Unverified:** secondary reports claim Anthropic now recommends defaulting to a single main agent loop over many specialized subagents, labels heavy subagent use a Conway's Law pattern ("Frankenprompts" where every team adds contradictory rules), and cites one customer's single-agent setup at ~2× faster. — [The Decoder](https://the-decoder.com/anthropic-says-one-ai-agent-beats-many-subagents-now-that-models-can-handle-complexity-alone/); [daily.dev](https://daily.dev/posts/anthropic-says-your-subagents-are-just-conway-s-law-ofrl3bwzf). The primary Anthropic source was not located, and the-decoder fetch was blocked.
- "Two-pizza" plus agents (opinion/vendor blogs, not empirical):
  - AKF Partners: 2–3 humans plus agents is feasible for well-scoped work, but 4–5 humans is often a better balance. — [AKF](https://akfpartners.com/growth-blog/engineering-team-sizes-are-evolving-rapidly-with-agentic-AI-platforms-the-limits-challenges-and-principles-we-must-consider)
  - Mimacom: "one-pizza team" of 2–3 builders. — [Mimacom](https://www.mimacom.com/blog/from-two-pizza-teams-to-agentic-engineering)
  - Every: "two-slice team". — [Every](https://every.to/on-every/the-two-slice-team)
  - [The Tool Nerd](https://www.thetoolnerd.com/p/ai-agents-and-the-2-pizza-rule); [Agility at Scale](https://agility-at-scale.com/?p=149517) (3–5 seniors plus agents).

### Inferences
- The serious transfer argument is not "keep agent teams at 6–10". It is the Brooks/Amdahl/Steiner logic. Agent-team value is bounded by the task's parallelizable fraction and its combination rule, and coordination costs grow super-linearly. Those are the same reasons small human teams win. Human-specific mechanisms (loafing, relationships, Dunbar limits) do not carry over. Agent-specific mechanisms (correlated errors, context and token dilution, sycophancy, error amplification without a verifier) take their place.

### Gaps
- No peer-reviewed paper was found that explicitly tests or cites Amazon's two-pizza rule for agent teams.
- The Anthropic "single agent beats subagents / Conway's Law" claim lacks a verified primary source.
