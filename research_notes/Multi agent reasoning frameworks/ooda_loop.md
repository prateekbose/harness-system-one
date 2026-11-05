# The OODA Loop (Observe–Orient–Decide–Act): Origins, Evidence, and Application to AI Agents and Multi-Agent Systems

Research notes compiled 2026-11-05. Evidence classes are tagged: **[PRIMARY]** = Boyd's own briefings; **[SCHOLARLY]** = academic book or peer-reviewed/conference work; **[PREPRINT]** = arXiv, not (or not yet) peer reviewed; **[PRACTITIONER]** = expert essay or blog; **[POPULAR]** = popular-press or secondary summary.

Access note: several hosts could not be reached from this session: en.wikipedia.org, www.schneier.com, slightlyeastofnew.com (Chet Richards' blog) and www.shadowboxtraining.com. Content attributed to those URLs comes from search-engine summaries and not from full-text reads. They are flagged as such below.

---

## Q1. What did Boyd actually describe, and why do scholars say "Orient" is the critical phase and the loop is not a simple sequence?

### Takeaway
Boyd never published a book. The "OODA loop" survives in briefing slides, and the only full diagram appears in his last briefing, "The Essence of Winning and Losing" (first edition 28 June 1995, revised around January 1996). In that diagram Orientation is the hub. It is shaped by genetic heritage, cultural traditions, previous experience, new information, and analysis/synthesis. It feeds Decide and Act through feed-forward links, and it also drives Observe and Act directly through "Implicit Guidance & Control", bypassing explicit decision. Osinga and Richards argue that the popular four-box, sequential "be faster" loop is a misreading.

### Cited Findings
- **[PRIMARY]** Boyd's briefing "The Essence of Winning and Losing" is held in the USMC University John Boyd collection (COLL 2062, Box 8), as both briefing and transparencies. The first edition is dated 28 June 1995 and the final revision is around January 1996, a little over a year before Boyd's death. — [USMCU Boyd Collection, Essence of Winning and Losing Briefing (PDF)](https://www.usmcu.edu/Portals/218/HD/Digitized%20Collections/COLL_2062%20John%20Boyd/COLL%202062_John%20Boyd_Box%208/110129-The%20Essence%20of%20Winning%20and%20Losing%20Briefing.PDF); [Transparencies (PDF)](https://www.usmcu.edu/Portals/218/HD/Digitized%20Collections/COLL_2062%20John%20Boyd/COLL%202062_John%20Boyd_Box%208/110128-The%20Essence%20of%20Winning%20and%20Losing%20Transparencies.PDF)
- **[PRIMARY, via search summary]** The 1995 slides list genetic heritage, cultural traditions, and previous experiences as the basis of an "implicit repertoire of psychophysical skills". In the sketch, Orientation feeds Decide and Act through an "Implicit Guidance & Control" link. Boyd describes the loop as "an ongoing many-sided implicit cross-referencing process of projection, empathy, correlation, and rejection." The slide OCR is garbled in places, so exact labels are approximate. — [USMCU Boyd Collection](https://www.usmcu.edu/Portals/218/HD/Digitized%20Collections/COLL_2062%20John%20Boyd/COLL%202062_John%20Boyd_Box%208/110129-The%20Essence%20of%20Winning%20and%20Losing%20Briefing.PDF); commentary at [Conceptual Spiral (Richards), "The Essence of Winning and Losing"](https://slightlyeastofnew.com/2010/08/11/the-essence-of-winning-and-losing/) (not fetched)
- **[PRACTITIONER, via search summary]** Commentators in Boyd's circle argue that most of the time action should flow from orientation through implicit guidance and control rather than through an explicit "Decide". Explicit decision is the exception, used when the implicit repertoire does not fit. — [The Whirl, "Boyd's real OODA loop: deconstructing…"](https://thewhirl.substack.com/p/boyds-real-ooda-loop-deconstructing-c84); [Richards, "Boyd's OODA 'Loop': What and why?" (2022)](https://slightlyeastofnew.com/2022/12/02/boyds-ooda-loop-what-and-why/) (not fetched)
- **[SCHOLARLY]** Frans Osinga, *Science, Strategy and War: The Strategic Theory of John Boyd* (Routledge, 2007; from his PhD thesis). The publisher states that the book shows the common interpretation of the OODA loop is "incomplete" and traces Boyd's sources in science and epistemology. — [Routledge listing](https://www.routledge.com/products/9780203088869)
- **[SCHOLARLY review]** Chet Richards' review of Osinga says the biggest misconception is that the OODA loop is a sequential step model. Boyd made orientation the *Schwerpunkt* (focal point), with the other elements radiating out from it. Per the review, Osinga holds that the speed and tempo logic applies mainly at the tactical level. At higher levels, the accuracy of observation and especially orientation become at least as important as tempo, and Boyd's emphasis moves toward a "moral" design. Richards questions whether Osinga confines OODA too narrowly to tactics. — [DNI review of Science, Strategy and War](https://dnipogo.org/dni_reviews/science_strategy_and_war/)
- **[PRACTITIONER]** William S. Lind, commenting on Osinga's book, says orientation shapes how we interact with the environment, and therefore how we observe, decide, and act. — [Lind, On War #235](https://dnipogo.org/lind/lind_10_02_07/)
- **[SCHOLARLY review]** A Foreign Affairs review of Osinga says the OODA loop "turns out to have been oversimple" as popularly presented, and that Boyd drew on reading far outside the military sphere. — [Foreign Affairs](https://www.foreignaffairs.com/node/1082395)
- **[SCHOLARLY]** Chet Richards, "Boyd's OODA loop," *Necesse* vol. 5 no. 1, pp. 142–165 (2020). It is a standard citation for the Richards interpretation and is cited by later engineering papers, e.g. [Jia et al., arXiv 2603.09191](https://www.alphaxiv.org/abs/2603.09191). The text itself was not retrieved here.
- **[SCHOLARLY]** Simpson, Oosthuizen, El Sawah and Abbass (UNSW Canberra / Pretoria), "Agile, Antifragile, AI-Enabled Command and Control" (arXiv 2109.06874, 2021). They summarise Boyd's claim as: Orient is where the "right decision" is formed from observations, analysis and mental models, but "if all else is equal… whoever loops through each step faster will win", producing the adversary's "fatal destabilization". — [arXiv 2109.06874](https://arxiv.org/abs/2109.06874)
- Other Boyd briefings named in the assignment, "Patterns of Conflict" (c. 1976–1986) and "Organic Design for Command and Control" (1987), are part of the "Discourse on Winning and Losing" compilation held in the same USMCU collection. I did not retrieve their text in this session, so dates are from general knowledge. See Gaps.

### Inferences
- For harness design, the Boyd-faithful reading is that Orient is not one stage among four. It is a persistent, continuously updated world model and disposition that shapes what gets observed (attention and tool selection) and can trigger action directly (cached policies and playbooks) without a deliberate decision step. A strictly sequential pipeline of Observer, Orienter, Decider and Actor agents is the "popular simplification", not Boyd's model.
- "Implicit guidance & control" maps naturally onto fast-path, pre-authorised reflexes (cached tool routines, guardrail rules). The explicit Decide maps onto a slower deliberative planner invoked only when orientation flags novelty or mismatch.

### Gaps
- I could not fetch the full text of Osinga's book, Richards' 2020 *Necesse* article, or Grant Hammond's *The Mind of War* (2001), so no direct page-cited quotes from them are included. Hammond's specific position on Orient is not documented here.
- Exact dates and content of "Patterns of Conflict" and "Organic Design for Command and Control" were not verified from primary sources in this session.

---

## Q2. Critiques, limitations, and empirical evidence about OODA in decision-making

### Takeaway
There is very little controlled empirical evidence that "running an OODA loop" improves decisions. Most of the literature is conceptual, doctrinal, or simulation-based. The major scholarly critique is Brehmer's (2005) Dynamic OODA (DOODA) loop. It argues that OODA is too abstract to be descriptively adequate for command and control because it omits planning, command concepts, delays and exit criteria, and it overemphasises speed. From cognitive science, Klein's Recognition-Primed Decision (RPD) model is often framed as filling the unspecified "D". OODA is better read as a model of adaptation than as a cognitive model of choice.

### Cited Findings
- **[SCHOLARLY]** Brehmer, B. (2005), "The Dynamic OODA Loop: Amalgamating Boyd's OODA Loop and the Cybernetic Approach to Command and Control," *Proc. 10th International Command and Control Research and Technology Symposium (ICCRTS)*, McLean, VA. It presents DOODA as a generic C2 model combining OODA with cybernetic C2 models, and notes that OODA was first developed to explain American fighter-pilot performance before Boyd generalised it. Brehmer was professor of C2 at the Swedish National Defence College and died in May 2014. — [Crossref record citing it](https://api.crossref.org/works/10.1007%2FS10111-007-0084-X); [Scribd copy of the paper](https://es.scribd.com/document/231281234/Dynamic-OODA-Loop); [GMU C5I tribute to Brehmer](https://c5i.gmu.edu/?p=1320)
- **[SCHOLARLY]** Simpson et al. (2021) summarise the critique. OODA "neglects specific functions, such as 'command concepts, planning, exit criteria or system delays', resulting in a model that overly accentuates speed as the aim". Brehmer argued that details such as decision-making delays are needed for the model to be "descriptively adequate in the C2 context". DOODA makes each C2 function explicit, and the authors adopt it as the base of their A3IC2 functional model. They also warn of a "fragility trap": delegating C2 functions to AI could increase fragility and cause catastrophic strategic failures, so they argue for "antifragility" alongside agility. — [arXiv 2109.06874](https://arxiv.org/abs/2109.06874)
- **[PRACTITIONER, via search summary]** ShadowBox Training (2023), "OODA Versus RPD: Reconciling Models of Cognition and Conflict". It argues OODA "is not a cognitive model of decision making at all; viewed narrowly, it is a generalized model of adaptation to hostile surroundings", that "Boyd did not specify a decision model within the D of OODA", and that RPD supplies a descriptive account of how experienced people choose under time pressure. ShadowBox is associated with Klein's naturalistic decision-making community, so it has a stake in the RPD side. — [ShadowBox Training](https://www.shadowboxtraining.com/news/2023/03/31/ooda-versus-rpd-reconciling-models-of-cognition-and-conflict/) (not fetched)
- **[SCHOLARLY, via search summary]** A Military Review / DTIC piece on Klein's Recognition Planning Model (RPM) reports a Thunholm study in which RPM allowed roughly a 20% increase in planning tempo. RPD's core claim is that experts recognise a plausible course of action and consider it first, rather than comparing options. This is a single study; treat it as indicative. — [DTIC ADA521492](https://apps.dtic.mil/sti/tr/pdf/ADA521492.pdf) (attribution to this exact DTIC document from search summary; not verified by full read)
- **[PRACTITIONER]** On tempo: Venkatesh Rao (Ribbonfarm, 2011) distinguishes getting "inside an adversary's tempo" (disrupting their orientation) from simply being "faster than the competition", which is the popular misreading. — [Ribbonfarm, "Tempo and OODA: The Backstory"](https://www.ribbonfarm.com/2011/07/22/tempo-and-ooda-the-backstory)
- **[POPULAR / secondary]** A practitioner "thinking frameworks" page argues that the canonical loop is a linear, bottom-up sequence lacking feedback and feed-forward. It says speed without accurate orientation just produces a wrong action sooner, and that it found "no traceable primary source" attaching an effect size to running the loop. — [product-on-purpose OODA page](https://product-on-purpose.github.io/thinking-framework-skills/library/ooda-loop/)
- **[SCHOLARLY, empirical-adjacent]** A 2016 human-factors study in a SAGE journal (DOI 10.1177/1555343416675077; *Journal of Cognitive Engineering and Decision Making*, by the DOI prefix) studied dismounted soldiers on patrol using a display of unmanned-ground-vehicle intelligence. It broke performance metrics into OODA components to locate difficulties in the decision process. OODA is used here as an analysis lens, not tested as a method. Results were not retrieved. — [SAGE](https://journals.sagepub.com/doi/10.1177/1555343416675077)
- **[SCHOLARLY, qualitative]** A DTIC report on Air Force commanders' use of motion imagery used grounded-theory interviews and produced a "substantive level theory based on Boyd's OODA loop". This is theory-building, not an experiment. — [DTIC AD1176044](https://apps.dtic.mil/sti/pdfs/AD1176044.pdf)
- **[PREPRINT, simulation]** "Analysis of OODA Loop based on Adversarial for Complex Game Environments" (Beijing Institute of Technology, 2022) runs simulated red-vs-blue confrontations structured around OODA. — [arXiv 2203.15502](https://arxiv.org/abs/2203.15502)
- **[PREPRINT]** "Exploring the OODA Loop as a Systematic Way of Thinking in Coping with Conflicts" (UCCS / US Air Force Academy, July 2026) revisits OODA as a general thinking method. It is conceptual. — [arXiv 2607.23342](https://www.alphaxiv.org/abs/2607.23342)
- **[SCHOLARLY]** OODA has been applied to emergency response in the *Journal of Emergency Management*, which shows its adoption outside the military. — [J. Emergency Management, "Application of Boyd's OODA loop to emergency response"](https://wmpllc.org/ojs/index.php/jem/article/view/3087)

### Inferences
- The evidence base for OODA as a decision procedure is thin. Its value to a harness designer is as an architectural vocabulary: sense, model-update, choose, effect, with feedback. It is not an empirically validated method.
- Brehmer's critique maps directly onto agent-harness concerns. Explicit planning or "command concept", explicit **delays** (tool latency, model latency, approval latency), and explicit **exit criteria** are exactly what naive agent loops omit. DOODA is arguably the better template for a harness than the four-box OODA.
- The RPD critique suggests that the "Decide" of an agent should often be recognise-a-workable-option-and-simulate-it, not enumerate-and-compare. This parallels LLM agents that propose one action and verify it.

### Gaps
- I found no randomised or controlled study showing that training people to use OODA improves decision outcomes. Search summaries from secondary sources say the same. This absence is a meaningful finding, but it is not proof that none exist.
- I could not read Brehmer's 2005 full text directly, only the Scribd listing and secondary summaries, so the DOODA components are given as described by Simpson et al.

---

## Q3. Applications of OODA to autonomy, cyber defense, military AI C2, and LLM agents (2023–2026)

### Takeaway
In 2026 OODA became a common framing device in arXiv agent papers, but most use it loosely as a label for perceive-reason-act pipelines. Only one paper found here operationalises OODA rigorously for LLM agents and benchmarks it against ReAct: **OODA-Tool** (arXiv 2608.24368, Aug 2026). Others are conceptual architectures (Brazilian Armed Forces agentic C2), systems papers with OODA framing (RAPTOR-AI disaster RAG, H-OODA UAV swarms), or security essays (Schneier & Raghavan 2025).

### Cited Findings

**OODA-Tool: the strongest LLM-agent evidence [PREPRINT]**
- Guo, Huang, Wu, Zhong, Chen, Tang, Long and Hu (HUST, Knowin AI, KAUST, UC Merced, U. Amsterdam and others), "From State to Action: OODA-Tool for Reliable Multi-Turn Tool Use", arXiv, 25 Aug 2026. — [arXiv 2608.24368](https://www.alphaxiv.org/abs/2608.24368)
  - The paper identifies "state-action competition" in direct function-calling and ReAct. Because state tracking and action generation share one autoregressive trajectory, pressure to emit the next call overwrites or ignores accumulated state.
  - Its stages are typed and checked by a controller:
    - **Observe** reconstructs a provenance-aware task state: goal, entities, values with sources, constraints, open subgoals, recent tool facts.
    - **Orient** judges execution readiness. It picks one of five modes: SOLVABLE_WITH_TOOL, NEED_CLARIFICATION, RESPOND_DIRECTLY, RECOVER_FROM_FAILURE, DONE. It also flags missing arguments or violated constraints, and acts as a gate.
    - **Decide** sets the action structure: which tools, in what order, with what data dependencies, but without argument values.
    - **Act** produces schema-grounded calls, binding argument values from the state.
  - It tests three variants: Joint (one call), Shared (4 calls, one LoRA) and Specialized (4 calls, 4 LoRA adapters), on Qwen3 0.6B–14B. Training and evaluation use ToolDial (11,111 sessions). Baselines are Direct-LoRA, ReAct-LoRA, Direct-SC@4 and α-UMi.
  - **Results:**
    - Specialized OODA had the best task success at every scale: +6.86 pp over Direct-LoRA at 0.6B and +4.48 pp at 14B, so gains shrink as models grow.
    - Gains concentrate on long histories, missing information, state changes, active constraints and deep tool dependencies. They are weaker for parallel calls.
    - **Removing Orient caused the largest drop**, especially on missing-information turns. Merging Decide and Act was the next most harmful. Free-text instead of typed states hurt. Stage-specific adapters mattered least.
    - Premature-call rate was 3.0% versus 9.0% for Direct-LoRA, and the stale or ungrounded argument rate was 1.6% versus 7.6% (on a rare-error sample).
    - The state–action contradiction rate was 3.9%, against 10.7% without the Decide/Act split.
    - Latency was 2.36× Direct-LoRA at 1.7B. Direct-SC@4, with a similar number of calls, scored lower, so the gains come from structure and not from extra compute.
    - Zero-shot transfer to FAIL-TaLMs, MTU-Bench and BFCL was modest, and the advantage shrank at larger scale.

**Military C2 / agentic architecture [PREPRINT, conceptual]**
- Braga, Barbieri, Ferraz, Sonaglio, de Miranda and Pereira Jr. (ITA, Brazil), "A Proposal for an Agentic AI Architecture to Support Multi-Domain Decision-Making in the Brazilian Armed Forces", 17 Sep 2026. — [arXiv 2609.20080](https://www.alphaxiv.org/abs/2609.20080)
  - The paper frames multi-domain data volume as "straining the OODA decision cycle".
  - Its architecture has an orchestration core that decomposes and delegates to four specialised agents: Decision Support, Situational Analysis, Feasibility Study and Countermeasure Suggestion. Each has least-privilege tool and data access, and they communicate over an inter-agent (A2A) bus.
  - A **mandatory human-approval gate** sits before any effect on operational or weapon systems. Autonomy is tiered by level: administrative, strategic, operational, tactical.
  - Proposed evaluation metrics: "OODA time-to-option" reduction versus human-only, precision and recall against expert courses of action, evidence-chain completeness, prompt-injection attack-success rate and task-drift detection, and human-override rate and time-to-approval. There are no empirical results; the paper is conceptual.
  - It cites A2ASecBench (ICLR 2026), reporting attack success rates up to 100% against unguarded agent-to-agent systems.
- Simpson et al. (2021), A3IC2: AI in C2 risks a "fragility trap", so DOODA plus antifragility is proposed as the design basis. — [arXiv 2109.06874](https://arxiv.org/abs/2109.06874)

**Disaster response / RAG [PREPRINT]**
- Yasuno (Yachiyo Engineering), "RAPTOR-AI for Disaster OODA Loop: Hierarchical Multimodal RAG with Experience-Driven Agentic Decision-Making", Jan 2026 (v2 8 Feb 2026). — [arXiv 2602.00030](https://www.alphaxiv.org/abs/2602.00030)
  - OODA mapping: multimodal ingestion is Observe, the hierarchical knowledge tree is Orient, the entropy-aware retrieval-strategy selector is Decide, and response generation is Act.
  - Corpus: 46 tsunami PDFs (2,378 pages) and 500 queries.
  - Results: NDCG 0.74, situational grounding accuracy 0.88 and task decomposition accuracy 0.75, against 0.52/0.67/0.49 for standard RAG. The paper reports this as "23% retrieval precision, 31% grounding, 27% task decomposition" improvements.
  - Caveats: single author, self-built evaluation, and the "expert evaluation" protocol is thinly described. OODA is a framing here, not something the paper tests.

**UAV swarms / robotics [PREPRINT, magazine-style]**
- Jia, Wu, Wu, He, Zhu, Zhou and Han (NUAA, CUMT, U. Houston, Kyung Hee), "Hierarchical OODA Enabled UAV Swarms in Uncertain Environments", 10 Mar 2026. — [arXiv 2603.09191](https://www.alphaxiv.org/abs/2603.09191)
  - It nests OODA loops at terminal (swarm), edge (regional) and cloud (global) layers, with bidirectional information flow, plus network function virtualisation.
  - The paper says explicitly that OODA stages "can overlap… the Orient stage may involve some degree of decision-making."
  - Simulation: 15 UAVs in a 100×100 m area, 10,000 runs. H-OODA beat single-layer and edge-end OODA on targets detected, search time and success rate; the figure values are hard to parse from the extraction.
  - With a D3QN learner, QoE rose and error rate fell as "loop depth" increased from 1 to 8 cycles.

**Cyber defense [PREPRINT / workshop; partially verified]**
- "OODA Loops in Cyberspace: A New Cyber-Defense Model" is hosted on CPS-VO and was not read in this session. — [CPS-VO PDF](https://cps-vo.org/sites/cps-vo.org/files/cpsvo_file_nodes/OODA_Loops_in_Cyberspace_A_New_Cyber-Defense_Model.pdf)
- The alphaXiv search surfaced many 2026 autonomous-pentest and incident-response agent papers. Examples are Cochise (TU Wien, [2605.11671](https://www.alphaxiv.org/abs/2605.11671)), AgentTrap ([2610.02869](https://www.alphaxiv.org/abs/2610.02869)), AgentSnare ([2607.26998](https://www.alphaxiv.org/abs/2607.26998)), SecODD ([2610.24741](https://www.alphaxiv.org/abs/2610.24741)) and "Staying on the Attack Path: Structured State…" ([2609.07344](https://www.alphaxiv.org/abs/2609.07344)). Their abstracts describe observation–action loops and structured state, but I did **not** verify that they use OODA explicitly. AgentSnare and AgentTrap attack the observation channel of pentest agents with deceptive observations, which is a concrete instance of Schneier's "adversary controls your sensors" point.

**Security essay: Schneier & Raghavan [PRACTITIONER / magazine column]**
- Bruce Schneier and Barath Raghavan, "Agentic AI's OODA Loop Problem," *IEEE Security & Privacy* (Oct 2025), reposted on Schneier's blog and summarised by Harvard's Berkman Klein Center. — [Schneier blog](https://www.schneier.com/blog/archives/2025/10/agentic-ais-ooda-loop-problem.html); [essay PDF](https://www.schneier.com/wp-content/uploads/2025/10/Agentic-AIs-OODA-Loop-Problem.pdf); [Harvard Cyber summary](https://cyber.harvard.edu/story/2025-10/agentic-ais-ooda-loop-problem). The schneier.com host could not be reached, so the points below come from search summaries.
  - AI agents don't just execute OODA loops; they embed untrusted actors inside them. Web-enabled models query adversary-controlled sources mid-loop.
  - "The speed of your OODA loop is irrelevant when the adversary controls your sensors and actuators", and the faster the loop, the less time there is for verification.
  - Each tool (e.g. via MCP) adds its own loop, and their vulnerabilities interact.
  - Compromises persist in conversation history and cached responses and can spread to other agents.
  - The essay frames a trilemma: "fast, smart, secure; pick any two".
  - LLMs "process symbols, not meaning", and prompt injection "might be unsolvable" in current LLMs.
  - A vendor write-up from Aviatrix presents the essay as a vulnerability disclosure with CVE details. Those details look unverified and should not be relied on. — [Aviatrix](https://aviatrix.ai/threat-research-center/agentic-ai-ooda-loop-prompt-injection-2025/)

### Inferences
- OODA-Tool is the most directly transferable result for a harness designer. A typed, gated "Orient" (readiness / mode classification) plus separating "what to call" (Decide) from "how to fill arguments" (Act) measurably cuts premature and ungrounded tool calls versus ReAct, especially with smaller models. The cost is about 2.4× latency, so a harness could apply it selectively to state-heavy turns.
- Schneier & Raghavan's critique lands mostly on Observe (poisoned inputs) and Orient (poisoned memory and context that persists across turns). In a multi-agent harness, the orientation state shared between agents is the highest-value attack target. It needs provenance tracking, which OODA-Tool's provenance-aware Observe partially provides, and trust tiers.
- Hierarchical or nested OODA (H-OODA) is the closest published analogue to multi-level harnesses: fast local loops plus slower orchestrator loops. The UAV evidence is simulation-only, though.

### Gaps
- I did not find a peer-reviewed (as opposed to arXiv) LLM-agent paper using OODA with measured results. All LLM-specific results above are preprints.
- I could not verify specific 2023–2025 arXiv papers that call themselves "OODA-based LLM agents for cybersecurity / incident response / autonomous driving". The search surfaced related but not explicitly OODA-labelled work. Coverage of IEEE/ACM proceedings, such as OODA in autonomous-driving architectures, was not achieved in this session.

---

## Q4. How does OODA map onto ReAct and onto multi-agent role splits? Are there direct comparisons?

### Takeaway
ReAct (Thought → Action → Observation) is roughly a collapsed OODA in which Orient and Decide are fused into one free-text "Thought". The one direct empirical comparison found, OODA-Tool, shows that separating them helps. Removing Orient was the single most damaging ablation. Multi-agent "observer / analyst / planner / executor" splits appear in conceptual architectures, but I found no controlled study of OODA-role multi-agent systems against ReAct or single-agent baselines.

### Cited Findings
- **[PREPRINT]** OODA-Tool's explicit comparison with ReAct-LoRA: ReAct and direct function-calling "learn state tracking and action generation within a single, monolithic autoregressive trajectory", which causes state–action competition. Specialized OODA beat ReAct-LoRA on task success at every scale tested. — [arXiv 2608.24368](https://www.alphaxiv.org/abs/2608.24368)
- **[PREPRINT]** In OODA-Tool, the Shared (one adapter, four passes) versus Specialized (four adapters) comparison showed that **staging and typed interfaces matter more than separate per-role parameters**, since removing stage-specific adapters had the smallest impact. This bears on whether separate "agents" per OODA phase are needed or whether one model in four structured passes suffices. — [arXiv 2608.24368](https://www.alphaxiv.org/abs/2608.24368)
- **[PREPRINT]** OODA-Tool compares against α-UMi, a modular multi-LLM agent (planner / caller / summarizer), and reports OODA-Tool ahead on ToolDial. On FAIL-TaLMs, OODA's advantage over α-UMi narrowed at larger scales. — [arXiv 2608.24368](https://www.alphaxiv.org/abs/2608.24368)
- **[PREPRINT, conceptual]** The Brazilian Armed Forces architecture's agent roles map roughly onto OODA:
  - Situational Analysis agent: Observe and Orient.
  - Decision Support agent: Orient, i.e. threat assessment with an evidence chain.
  - Countermeasure Suggestion agent: Decide, i.e. ranked options.
  - Human-approval gate, then effect: Act.
  The 5-stage vignette is Detection → Situational Analysis → Assessment → Options → Human Decision. — [arXiv 2609.20080](https://www.alphaxiv.org/abs/2609.20080)
- **[PREPRINT]** That paper also cites a 6G Open-RAN security system, MobiLLM (arXiv 2509.21634), with a triage agent, a RAG-backed threat-classification agent and a response agent. This is effectively an Observe/Orient/Act role split aimed at cutting incident-response latency. — cited in [arXiv 2609.20080](https://www.alphaxiv.org/abs/2609.20080); original [arXiv 2509.21634](https://arxiv.org/abs/2509.21634)
- **[PREPRINT]** Related ReAct-loop research that partly reintroduces OODA-like separation, without OODA framing:
  - "Second Thought: Reasoning in Parallel as LLM Agents Act and Observe" (SMU, Aug 2026) notes that ReAct confines deliberate reasoning to the Thought phase. It reasons in parallel while actions execute, which is analogous to continuous orientation. — [arXiv 2608.13667](https://www.alphaxiv.org/abs/2608.13667)
  - "Act More, Decide Less" (Sep 2026) uses skill-guided action chunking instead of one primitive action per LLM round, analogous to Boyd's implicit guidance & control bypassing explicit decisions. — [arXiv 2609.02042](https://www.alphaxiv.org/abs/2609.02042)
  - The OODA analogies are my inference; neither paper invokes OODA.
- **[REFERENCE]** ReAct itself: Yao et al., "ReAct: Synergizing Reasoning and Acting in Language Models" (ICLR 2023). — [arXiv 2210.03629](https://arxiv.org/abs/2210.03629)

### Inferences
- A practical mapping for a harness:

  | OODA phase | Harness component |
  |---|---|
  | Observe | Tool results, environment events, user messages, normalised with provenance |
  | Orient | Persistent typed world state, memory and beliefs, plus readiness / mode classification (gate) |
  | Decide | Plan or action skeleton (which tools or sub-agents, in what order) |
  | Act | Argument binding, execution, effects |
  | Implicit guidance & control | Pre-approved reflexes or playbooks that skip Decide |
  | Feedback | Act results return as the next Observe |
  | Brehmer's additions | Explicit delays, planning or command intent, exit criteria |

- The evidence suggests that the gain comes from typed interfaces and gating between phases, not from giving each phase its own agent. Splitting into separate observer, orienter, planner and executor *agents* adds latency and inter-agent attack surface (Schneier; A2ASecBench as cited in 2609.20080) without demonstrated benefit beyond structured multi-pass prompting.
- Boyd scholars would object to a strictly pipelined role split. Orientation should be shared and continuously updated by all roles, and should shape Observe (what to look at), not just consume its output.

### Gaps
- I found no paper that directly compares a multi-agent OODA role decomposition (separate agents per phase) with ReAct or single-agent baselines under controlled conditions.
- I found no peer-reviewed theoretical paper that formally maps ReAct to OODA. The mapping above is inference supported by OODA-Tool's framing.

---

## Q5. Notable practitioner writing on OODA for AI agents

### Takeaway
The most-cited practitioner piece is Schneier & Raghavan's "Agentic AI's OODA Loop Problem" (IEEE S&P, Oct 2025). It reframes OODA from a speed advantage into a security liability once observations, tools and memory are adversary-reachable. Practitioner and military commentary otherwise mostly uses OODA to argue that AI accelerates decision cycles, which Boyd scholars (Osinga) and Brehmer warn overemphasises tempo.

### Cited Findings
- **[PRACTITIONER, peer-edited column]** Schneier & Raghavan, *IEEE Security & Privacy*, Oct 2025. The key claims are listed under Q3, including "fast, smart, secure: pick any two" and the claim that integrity, not speed, is the core problem. A Schneier "integrity" tag page groups related essays. — [Schneier blog](https://www.schneier.com/blog/archives/2025/10/agentic-ais-ooda-loop-problem.html); [Harvard Cyber summary](https://cyber.harvard.edu/story/2025-10/agentic-ais-ooda-loop-problem); [Schneier integrity tag](https://www.schneier.com/tag/integrity/) (search summary only)
- **[PRACTITIONER]** A 2025 podcast transcript features practitioners discussing Boyd's real loop. It shows the practitioner community pushing the "Orient is central / not a simple loop" reading. — [Buzzsprout transcript](https://www.buzzsprout.com/2109174/16830815/transcript) (search result only, not read)
- **[POPULAR]** Popular explainers such as Farnam Street present OODA mainly as a speed-and-agility heuristic, the simplification Osinga critiques. — [fs.blog, "John Boyd OODA loop"](https://fs.blog/john-boyd-ooda-loop/) (search result only)
- **[PREPRINT / defense]** The Brazilian ITA paper's framing is typical of military-AI writing: "the Force that can turn raw data into informed decisions faster tends to retain operational initiative". It pairs that with human-approval gates and least privilege. — [arXiv 2609.20080](https://www.alphaxiv.org/abs/2609.20080)

### Inferences
- For a harness designer, Schneier's piece is the strongest argument for treating Observe and Orient inputs as untrusted by default. That means provenance-tagged observations, quarantined memory writes, and verification steps that deliberately slow the loop where the stakes are high. Practitioners now cite it as the counterweight to "faster loop wins" rhetoric.

### Gaps
- I could not access the full text of the Schneier essay because the host was blocked. The quotes are from search-engine summaries and should be spot-checked against the PDF before publication.
- I did not find other substantial, non-vendor practitioner essays on OODA specifically for LLM agents. Many vendor blogs exist but were not assessed.
