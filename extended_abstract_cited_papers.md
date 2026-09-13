# Papers cited in the five research-question sections

A plain-language companion to the gap-analysis sections added to `sections/01_extended_abstract.tex` (2026-09-01; Question 5 added later the same day). For each question, the papers are listed in the order they are cited in that section, with a short explanation of the claim that makes them relevant. Full bibliographic details are in `references_extabstract.bib`, `references_litreview.bib`, `refs_zotero_phd.bib` and `thesis.bib`.

Two terms used throughout, in plain words: a *search trace* is a written-out, step-by-step log of a search algorithm doing its work — trying options, evaluating them, backtracking out of dead ends. *Search-augmented (SA)* training teaches a model to produce this log before the answer; *solution-only (SO)* training teaches it to produce just the answer.

## Question 1 — When does training on search traces help, when is it optional, and when does it hurt?

1. **[Searchformer](https://arxiv.org/abs/2402.14083)** (Lehnert et al., 2024, preprint) — Trained transformers on written-out A\* search steps for mazes and Sokoban, and found they needed about ten times less training data and five-to-ten-times smaller networks than models trained on the answers alone. This is the founding "search traces help" result that the thesis re-examines.

2. **[Stream of Search](https://arxiv.org/abs/2404.03683)** (Gandhi et al., COLM 2024) — Trained a model on messy search logs, wrong turns and backtracking included, for the Countdown numbers game; this beat training on clean optimal answers by 25 percentage points.

3. **[ASTRO](https://arxiv.org/abs/2507.00417)** (Kim et al., 2025, preprint) — Showed the idea working on a large modern model: search trees were flattened into text with explicit reflection and backtracking, and fine-tuning a Llama model on them gave large gains on competition mathematics.

4. **[To Backtrack or Not to Backtrack](https://arxiv.org/abs/2504.07052)** (Qin et al., COLM 2025) — Gave both kinds of model the same total computing budget at answer time and found no universal winner: trained backtracking helped on Sudoku but hurt on Countdown, where a solution-only model allowed many parallel tries did better. Also argues that copying one fixed search recipe can lock a model into a bad strategy.

5. **[Beyond Semantics](https://arxiv.org/abs/2505.13775)** (Valmeekam et al., TMLR) — Trained maze models on search traces deliberately taken from the *wrong* problems, and they did about as well as models trained on the correct traces. Concludes that the written "reasoning" need not have anything to do with how the problem actually gets solved.

6. **[Transformers Can Navigate Mazes With Multi-Step Prediction](https://arxiv.org/abs/2412.05117)** (Nolte et al., 2024, preprint) — Changed only the training objective (predict several steps ahead and backwards, instead of one token at a time) and solved mazes better than larger models trained with A\* trace supervision — with no traces at all.

7. **[Dualformer](https://arxiv.org/abs/2410.09918)** (Su et al., ICLR 2025) — Randomly deleted chunks of the search traces during training and got a model that is both more accurate and cheaper than one trained on complete traces; imitating the search algorithm more faithfully is not always better.

8. **[To CoT or not to CoT](https://arxiv.org/abs/2409.12183)** (Sprague et al., ICLR 2025) — Surveyed over one hundred studies of step-by-step prompting and found meaningful gains almost exclusively on mathematics and formal-logic style tasks; elsewhere, direct answers do about as well and cost less.

9. **[Merrill & Sabharwal](https://arxiv.org/abs/2310.07923)** (ICLR 2024) — Mathematical proof that generating intermediate tokens genuinely extends what a transformer can compute, and that the extension grows with the number of tokens generated.

10. **[Li et al.](https://arxiv.org/abs/2402.12875)** (ICLR 2024) — Proof that a transformer's single forward pass can only do "wide but shallow" computation (many things at once, few steps in a row); writing out intermediate tokens is what buys it genuine step-after-step computation.

11. **[Feng et al.](https://arxiv.org/abs/2305.15408)** (NeurIPS 2023) — Proof that for basic arithmetic-style problems, answering directly requires networks that grow unreasonably large with the problem size, whereas a fixed-size network suffices if it may write out the derivation.

12. **[Wen et al.](https://arxiv.org/abs/2410.05459)** (2024) — Proof that for a certain family of problems, learning from answers alone needs exponentially many training examples while learning with step-by-step traces needs only polynomially many. The benefit of traces is about *learning*, not only about computing power.

13. **[Abbe et al.](https://arxiv.org/abs/2406.06467)** (NeurIPS 2024) — Defines a measure of how many parts of the input must be combined at once to see the answer ("globality"), and proves that when this number is high the task cannot be learned efficiently without a scratchpad.

14. **[Transformers Learn Shortcuts to Automata](https://arxiv.org/abs/2210.10749)** (Liu et al., ICLR 2023) — Shows transformers often learn compressed "shortcut" solutions that squeeze a long step-by-step process into a few parallel layers; this is how some tasks get solved without traces, and why such solutions can be brittle.

15. **[Sanford et al.](https://arxiv.org/abs/2405.18512)** (NeurIPS 2024) — Sorts graph problems into those a transformer can solve in a single pass and those that genuinely need extra reasoning tokens — a theoretical map of which tasks should and should not need traces.

16. **[The Kinetics of Reasoning](https://arxiv.org/abs/2510.25791)** (Pengmei et al., 2025, preprint) — The nearest existing study to this project's design: trains small models from scratch with and without reasoning traces across task difficulties and reports computing cost, finding traces help on some task types and fail on others. It uses a single model size, no pathfinding tasks, and no answer-time cost comparison — which is exactly the room the thesis occupies.

17. **[Do NOT Think That Much](https://arxiv.org/abs/2412.21187)** (Chen et al., 2024) — Documents "overthinking": trained reasoning models spend large token budgets even on trivial questions, which is the ongoing cost side of trace training at answer time.

18. **[Sardana et al.](https://arxiv.org/abs/2401.00448)** (ICML 2024) — Shows that once the cost of *using* a model is counted alongside training it, the best training choices change. Relevant because a trace-trained model pays its longer outputs on every query, forever.

19. **[Snell et al.](https://arxiv.org/abs/2408.03314)** (ICLR 2025) — Shows compute spent at answer time can substitute for a bigger model, and studies how to split a budget between the two; choosing between SA and SO reasoning is exactly this kind of budget decision.

## Question 2 — How do problem structure and representation decide which approach wins?

1. **[Teaching Arithmetic to Small Transformers](https://arxiv.org/abs/2307.03381)** (Lee et al., ICLR 2024) — Small transformers learning arithmetic succeed or fail depending on trivial-looking formatting choices, such as writing the answer's digits in reverse, with abrupt jumps as training data grows. Format alone can make the same problem easy or hard.

2. **[ALPINE](https://arxiv.org/abs/2405.09220)** (Wang et al., NeurIPS 2024) — Models trained to output paths over a graph they had to memorise (the graph is not shown in the input) can only connect places they saw connected during training; they provably cannot chain two known connections into a new route. Storing the map in the weights has a specific blind spot.

3. **[Othello-GPT](https://arxiv.org/abs/2210.13382)** (Li et al., ICLR 2023) — A model trained only on move sequences of the board game Othello builds an internal picture of the board that it actually uses: editing that internal picture changes its moves. Answer-only training can produce a real internal model of the game state.

4. **[Spies et al.](https://arxiv.org/abs/2412.11867)** (2024, preprint) — Maze-solving transformers build internal, causally-used maps of the maze they read from their input, and how the maze is written down changes what internal map forms.

5. **[The Pitfalls of Next-Token Prediction](https://arxiv.org/abs/2403.06963)** (Bachmann & Nagarajan, ICML 2024) — Even with the whole graph visible in the input, standard training fails on a simple task where the *first* output step already requires knowing the whole path: during training the model can cheat by peeking at the answer prefix it is given, so it never learns the look-ahead. A precise mechanism for why answer-only training fails on look-ahead problems.

6. **[Transformers Struggle to Learn to Search](https://arxiv.org/abs/2412.04703)** (Saparov et al., ICLR 2025) — Transformers can learn to search small graphs given the right training data, but reliably fail as the graphs grow — and neither more parameters nor letting them write out steps fixes it.

7. **[Abbe et al.](https://arxiv.org/abs/2406.06467)** (NeurIPS 2024) — As in Q1: their "globality" measure is the best existing candidate for predicting, from the task itself, whether trace supervision will be needed — but it has never been tested on realistic search tasks.

8. **[RASP-L](https://arxiv.org/abs/2310.16028)** (Zhou et al., ICLR 2024) — Proposes a rule of thumb: transformers generalise well on tasks that can be written as a short program in a language mirroring what transformers naturally compute. A second candidate for predicting learnability from the task description.

9. **[Sanford et al.](https://arxiv.org/abs/2405.18512)** (NeurIPS 2024) — As in Q1: their classification of graph problems by the network resources they require is the template for classifying tasks *before* training rather than after.

10. **[Why Think Step by Step?](https://arxiv.org/abs/2304.03843)** (Prystawski et al., NeurIPS 2023) — Step-by-step generation helps exactly when the training data consists of overlapping clusters of locally related facts; the value of intermediate steps depends on the structure of the data, not just the difficulty of the task.

11. **[Grokking](https://arxiv.org/abs/2201.02177)** (Power et al., 2022, preprint) — Networks trained on modular arithmetic from answers alone can suddenly start generalising long after they appeared to have merely memorised the training set. A warning: on modular tasks, "never generalises" must always be stated as "did not generalise within our budget".

12. **[Nanda et al.](https://arxiv.org/abs/2301.05217)** (ICLR 2023) — Reverse-engineered what such a network eventually learns: a clean, exact algorithm for modular addition. So the arithmetic ingredient of modular Countdown is learnable without traces, and any solution-only failure must come from the search ingredient.

13. **[To Backtrack or Not to Backtrack](https://arxiv.org/abs/2504.07052)** (Qin et al., COLM 2025) — As in Q1: the closest published "it depends on the task" result — but it compares two different games, not two representations of the same game, which is the comparison this thesis adds.

14. **[The Countdown Game is NP-complete](https://arxiv.org/abs/2508.02900)** (Katz et al., 2025, preprint) — Proves that Countdown belongs to the class of genuinely hard search problems, while maze shortest-path is easy in principle; this puts the thesis's maze-versus-Countdown contrast on formal footing.

## Question 3 — Can something other than search traces deliver the same benefit?

1. **[Pause tokens](https://arxiv.org/abs/2310.02226)** (Goyal et al., ICLR 2024) — Adding blank "pause" tokens that give the model extra internal processing time before it answers helps on some tasks — but mostly only if the model was pretrained with them from the start.

2. **[Let's Think Dot by Dot](https://arxiv.org/abs/2404.15758)** (Pfau et al., COLM 2024) — Models can sometimes use meaningless filler tokens ("......") in place of written reasoning — but only on problems whose work can be done in parallel, and learning to use fillers at all is hard.

3. **[London & Kanade](https://arxiv.org/abs/2505.21024)** (2025, preprint) — Proof that pause and filler tokens buy "more work done side by side", not "more steps one after another"; genuinely sequential problems, search included, still need real intermediate steps.

4. **[What Matters in Chain-of-Thought Prompting](https://arxiv.org/abs/2212.10001)** (Wang et al., ACL 2023) — In prompting, deliberately *invalid* reasoning examples keep 80–90% of the benefit of valid ones; being on-topic and in a sensible order matters more than being correct.

5. **[Beyond Semantics](https://arxiv.org/abs/2505.13775)** (Valmeekam et al., TMLR) — As in Q1: wrong-problem traces trained maze models as well as correct ones. This is the direct precedent for the thesis's unrelated-trace experiment — which found the opposite on mazes and a more surprising partial benefit on Countdown.

6. **[Coconut](https://arxiv.org/abs/2412.06769)** (Hao et al., COLM 2025) — Lets the model "think" in its internal vector state instead of in words, feeding its own hidden state back as the next input; on some logic tasks this beats written reasoning, and one internal state can hold several candidate paths at once.

7. **[Reasoning by Superposition](https://arxiv.org/abs/2505.12514)** (Zhu et al., NeurIPS 2025) — The theory behind the above: continuous internal "thoughts" can represent many search branches at the same time and explore them in parallel, doing in a few steps what written traces need many steps to do.

8. **[Looped Transformers](https://arxiv.org/abs/2502.17416)** (Saunshi et al., ICLR 2025) — Running a small transformer repeatedly in a loop imitates a much deeper network and can substitute for written reasoning steps: depth by repetition instead of reasoning by writing.

9. **[Recurrent-Depth Reasoning](https://arxiv.org/abs/2502.05171)** (Geiping et al., 2025, preprint) — Built a model that silently repeats an internal block as many times as needed at answer time, improving on reasoning benchmarks with no visible reasoning text at all.

10. **[From Explicit CoT to Implicit CoT](https://arxiv.org/abs/2405.14838)** (Deng et al., 2024, preprint) — Trains with written reasoning steps, then gradually deletes them during training until the model solves the task with no visible steps; the trace serves as scaffolding that can be removed once the building stands.

11. **[Quiet-STaR](https://arxiv.org/abs/2403.09629)** (Zelikman et al., COLM 2024) — A model learns to generate its own short internal rationales while reading ordinary text, with no reasoning dataset supplied; useful intermediate text can be learned rather than provided.

12. **[Nolte et al.](https://arxiv.org/abs/2412.05117)** (2024, preprint) — As in Q1: a trace-free training objective beats trace supervision on mazes. The caveat the thesis adds: mazes are precisely the regime where traces were optional anyway.

13. **[Turpin et al.](https://arxiv.org/abs/2305.04388)** (NeurIPS 2023) — A model's written explanation can systematically misrepresent the actual reason for its answer, for example concealing a bias that was deliberately planted in the prompt.

14. **[Lanham et al.](https://arxiv.org/abs/2307.13702)** (2023, preprint) — When the written reasoning is edited or cut short, the answer often does not change: models frequently ignore their own reasoning text, and larger models were often *less* faithful to it.

15. **[Stop Anthropomorphizing Intermediate Tokens](https://arxiv.org/abs/2504.09762)** (Kambhampati et al., 2025, position paper) — Argues the field should stop reading intermediate tokens as the model's "thinking" at all, and treat them instead as training data that happens to help.

## Question 4 — Where does search-trace data come from when no solver exists?

1. **[STaR](https://arxiv.org/abs/2203.14465)** (Zelikman et al., NeurIPS 2022) — The basic bootstrap: let the model attempt reasoned answers, keep only the attempts whose final answer checks out, retrain on those, repeat. Needs only an answer checker, not a solver — but also needs a model that already succeeds sometimes.

2. **[ReST-EM / Beyond Human Data](https://arxiv.org/abs/2312.06585)** (Singh et al., TMLR 2024) — Scales that recipe up: generate, filter by a simple correct/incorrect check, retrain; at large scale this beat fine-tuning on human-written solutions.

3. **[Expert Iteration](https://arxiv.org/abs/1705.08439)** (Anthony et al., NeurIPS 2017) — The pre-LLM template: a slow tree search produces training targets, a fast network learns to imitate them, and the improved network then makes the next round of search stronger. The "solver" here is a generic search procedure plus a learned evaluator, improving together.

4. **[AlphaGeometry](https://www.nature.com/articles/s41586-023-06747-5)** (Trinh et al., Nature 2024) — Escaped the no-data problem by generating one hundred million geometry theorems and proofs mechanically — running deduction *forward* from random starting points and reading proofs off backwards. Generating problems can be easy even when solving them is hard.

5. **[AlphaProof](https://www.nature.com/articles/s41586-025-09833-y)** (Hubert et al., Nature 2025) — Automatically translated about a million informal maths problems into a formal proof language, then ran an AlphaZero-style learning loop against the proof checker, reaching olympiad level. The complete loop works when an incorruptible checker exists.

6. **[rStar-Math](https://arxiv.org/abs/2501.04519)** (Guan et al., 2025) — A small model searches over its own solution steps, verifies each step by running code, and retrains on the verified paths over several rounds — strong mathematics results without any stronger teacher model.

7. **[ASTRO](https://arxiv.org/abs/2507.00417)** (Kim et al., 2025, preprint) — As in Q1: the closest existing method to making search traces without a symbolic solver — run tree search *using the model itself*, then flatten the tree into text with explicit backtracking. It still needs known correct answers and a model already competent enough to search.

8. **[CodeIt](https://arxiv.org/abs/2402.04858)** (Butt et al., ICML 2024) — Turns failures into data: if a generated program produces the wrong output for puzzle A, keep it as a *correct* program for whatever output it did produce. Every attempt becomes valid supervision for something.

9. **[SOAR](https://arxiv.org/abs/2507.14172)** (Pourcel et al., ICML 2025) — Combines evolutionary search with the same failures-into-data idea on ARC reasoning puzzles; the strongest existing result for bootstrapping with no solver anywhere in the loop.

10. **[DeepSeek-R1](https://arxiv.org/abs/2501.12948)** (DeepSeek-AI, Nature 2025) — Showed that reflection- and verification-style reasoning can emerge from reinforcement learning with only right/wrong feedback and no reasoning data at all — but starting from a very capable pretrained model.

11. **[Stream of Search](https://arxiv.org/abs/2404.03683)** (Gandhi et al., COLM 2024) — As in Q1, but here for its second stage: after pretraining on traces from weak solvers, self-improvement let the model solve 36% of previously unsolved puzzles, including ones *none* of its teacher solvers could solve. The learner can outgrow its teachers.

12. **[Four Habits / Cognitive Behaviors](https://arxiv.org/abs/2503.01307)** (Gandhi et al., 2025) — Reinforcement learning only works if the starting model already shows search-like habits (checking, backtracking, setting subgoals); priming a model with examples of these habits works even when the examples' *answers* are wrong. RL amplifies search behaviour; it does not create it.

13. **[Does RL Really Incentivize New Reasoning?](https://arxiv.org/abs/2504.13837)** (Yue et al., 2025) — Evidence that RL with verifiable rewards mostly sharpens what the base model could already do: allowed enough tries, the *base* model matches or beats the RL-trained one. If true, RL cannot substitute for trace data where the base model can do nothing.

14. **[ProRL](https://arxiv.org/abs/2505.24864)** (Liu et al., 2025, preprint) — The counter-claim: with long enough RL training, models solved problems the base model failed on no matter how many tries it was given. The dispute between these two positions is open, and Question 4 sits exactly on it.

15. **[s1](https://arxiv.org/abs/2501.19393)** (Muennighoff et al., 2025, preprint) — Just 1,000 carefully chosen reasoning examples copied from a stronger model unlock strong reasoning in a smaller one. Distillation is cheap — but it presupposes that someone has already built the stronger reasoner, so it cannot answer the question for genuinely new tasks.

## Question 5 — How can search-augmented reasoning achieve length generalisation?

*Length generalisation* means training on small problem instances (small mazes, short puzzles, short traces) and correctly solving larger ones that need longer computations. Papers are listed in the order the section discusses them: general transformer results, then the graph-neural-network (neural algorithmic reasoning) literature, then search-specific results, then the impact sources.

### Length generalisation in general — transformers

1. **[Exploring Length Generalization in Large Language Models](https://arxiv.org/abs/2207.04901)** (Anil et al., NeurIPS 2022) — The founding negative result: models trained on short instances fail on longer ones, and making the model bigger does not fix it.

2. **[The Impact of Positional Encoding](https://arxiv.org/abs/2305.19466)** (Kazemnejad et al., NeurIPS 2023) — How the model tracks token positions strongly affects extrapolation; surprisingly, no explicit position information at all generalised best on their tasks.

3. **[Transformers Can Do Arithmetic with the Right Embeddings](https://arxiv.org/abs/2405.17399)** (McLeish et al., NeurIPS 2024) — A position scheme purpose-built for digit alignment takes 20-digit training to ~99% on 100-digit addition. The strongest known extrapolation, bought by hand-engineering position structure.

4. **[Position Coupling](https://arxiv.org/abs/2405.20671)** (Cho et al., NeurIPS 2024) — Same lesson: sharing position labels between related tokens extends 30-digit training to 200-digit tests — but requires already knowing which tokens "line up", which is unknown for search traces.

5. **[Transformers Can Achieve Length Generalization But Not Robustly](https://arxiv.org/abs/2402.09371)** (Zhou et al., 2024, preprint) — Even successful recipes are fragile: results swing widely with random initialisation and data order.

6. **[What Algorithms Can Transformers Learn?](https://arxiv.org/abs/2310.16028)** (Zhou et al., ICLR 2024) — The field's main predictor: a transformer generalises to longer inputs when the task can be written as a short program, valid at every length, in a language matching what transformers compute.

7. **[The Globality Barrier and Inductive Scratchpad](https://arxiv.org/abs/2406.06467)** (Abbe et al., NeurIPS 2024) — The one written-trace format shown to extrapolate: restate a compact state summary at every step so each step depends only on the previous one.

8. **[Universal Length Generalization with Turing Programs](https://arxiv.org/abs/2407.03310)** (Hou et al., ICML 2025) — Same principle taken further: format every task as a machine that copies its state forward with one small edit per step.

9. **[Transformers Provably Learn Chain-of-Thought Reasoning with Length Generalization](https://arxiv.org/abs/2511.07378)** (Huang et al., 2025, preprint) — Proof that trained step-by-step reasoning can extrapolate on structured tasks, and that retraining a model on its own slightly-longer successes progressively extends its reach.

### Length generalisation in general — graph neural networks (neural algorithmic reasoning)

10. **[The CLRS Algorithmic Reasoning Benchmark](https://arxiv.org/abs/2205.15659)** (Veličković et al., ICML 2022) — The benchmark that made size extrapolation the standard test: networks supervised on step-by-step traces ("hints") of 30 classical algorithms are trained on 16-node inputs and tested on 64-node inputs.

11. **[A Generalist Neural Algorithmic Learner](https://arxiv.org/abs/2209.11142)** (Ibarz et al., LoG 2022) — One network for all 30 algorithms reaching ~74% average at 4x training size — though the average hides near-total failures on some tasks (e.g. Quickselect below 1%).

12. **[What Can Neural Networks Reason About?](https://arxiv.org/abs/1905.13211)** (Xu et al., ICLR 2020) — Theory: networks whose internal structure mirrors the algorithm's structure need less data and generalise better ("algorithmic alignment").

13. **[How Neural Networks Extrapolate](https://arxiv.org/abs/2009.11848)** (Xu et al., ICLR 2021) — Proof that standard networks extrapolate only linear behaviour, so the recipe is to build the algorithm's non-linear steps (like taking a minimum) into the architecture, leaving the learned parts linear.

14. **[Neural Algorithmic Reasoning with Causal Regularisation](https://arxiv.org/abs/2302.10258)** (Bevilacqua et al., ICML 2023) — Many different inputs share the same next algorithm step; forcing the model to predict identically on all of them (rather than latching onto irrelevant detail) gives up to 3x better size generalisation.

15. **[On the Markov Property of Neural Algorithmic Reasoning](https://arxiv.org/abs/2403.04929)** (Bohde et al., ICLR 2024) — An algorithm's next step depends only on its current state, not its history; forcing the network to forget history improves size generalisation. Directly relevant to whether search traces should restate state or accumulate history.

16. **[Discrete Neural Algorithmic Reasoning](https://arxiv.org/abs/2402.11628)** (Rodionov & Prokhorenkova, ICML 2025) — The strongest result in the field: forcing the network's intermediate state into a finite set of discrete values gives 100% accuracy at 100x the training size, with provable correctness — at the price of hand-designed state descriptions.

17. **[Softmax Is Not Enough](https://arxiv.org/abs/2410.01104)** (Veličković et al., ICML 2025) — Proof that softmax attention cannot keep "pick the best item" decisions sharp as the number of items grows — exactly the pick-the-best-frontier-node step of A*.

18. **[Neural Networks and the Chomsky Hierarchy](https://arxiv.org/abs/2207.02098)** (Delétang et al., ICLR 2023) — Across formal-language tasks, only architectures with structured external memory (stack, tape) generalise beyond the simplest language class; fixed-depth transformers place worst.

19. **[CLRS-Text](https://arxiv.org/abs/2406.04229)** (Markeeva et al., 2024, preprint) — The pivotal comparison: the same algorithm traces ported to text. Graph networks "easily generalise to 4x the input sizes seen at training time" while language models "barely extrapolate at all" — a transformer emitting text traces is on the losing side of this by default.

20. **[Transformers meet Neural Algorithmic Reasoners](https://arxiv.org/abs/2406.09308)** (Bounsi et al., 2024, preprint) — Letting the language model attend to a graph executor's states recovers much of the gap — localising the problem in the transformer/text side.

### Length generalisation in search problems and with search traces

21. **[Searchformer](https://arxiv.org/abs/2402.14083)** (Lehnert et al., 2024, preprint) — Evaluates only at training size (test sequences deliberately length-matched); its Sokoban traces approach 100,000 tokens and had to be truncated; the size curriculum is named as future work and never run.

22. **[Dualformer](https://arxiv.org/abs/2410.09918)** (Su et al., ICLR 2025) and **[Stream of Search](https://arxiv.org/abs/2404.03683)** (Gandhi et al., COLM 2024) — Both evaluate only at the trained problem size.

23. **[Beyond Semantics](https://arxiv.org/abs/2505.13775)** (Valmeekam et al., TMLR) — Its out-of-distribution tests vary the maze style, not the size — so it says nothing about the length axis.

24. **[Transformers Struggle to Learn to Search](https://arxiv.org/abs/2412.04703)** (Saparov et al., ICLR 2025) — Trained to look up to 12 steps ahead, models manage 13-14 and no further; scale does not help.

25. **[Nolte et al.](https://arxiv.org/abs/2412.05117)** (2024, preprint) — Zero accuracy on maze sizes other than the trained one, including for their A*-trace-supervised baseline.

26. **[Extrapolation by Association](https://arxiv.org/abs/2506.09251)** (Cai et al., NeurIPS 2025) — The only published length experiment on a backtracking search trace, and it is negative for traces alone: DFS-trace training extrapolates only when co-trained on a helper task supervised at the longer lengths.

27. **[End-to-end Algorithm Synthesis with Recurrent Networks](https://arxiv.org/abs/2202.05826)** (Bansal et al., NeurIPS 2022) — Easy-to-hard maze extrapolation is achievable — but with a network that repeats an internal computation more times at test time, no written trace at all.

28. **[Looped Transformers for Length Generalization](https://arxiv.org/abs/2409.15647)** (Fan et al., ICLR 2025) — Looping a small transformer an adaptive number of times markedly improves extrapolation.

29. **[Self-Improving Transformers](https://arxiv.org/abs/2502.01612)** (Lee et al., ICML 2025) — The strongest demonstrated route: solve slightly harder problems, keep verified successes, retrain, repeat — maze paths from 9 to 30 hops. Uses answers only, no search traces.

30. **[How Does RL Post-training Induce Skill Composition?](https://arxiv.org/abs/2512.01775)** (Park et al., 2025, preprint) — The only cross-size Countdown result: RL on a pretrained model trained on 3-4-number puzzles handles 5-number ones.

31. **[Can Transformers Learn to Verify During Backtracking Search?](https://arxiv.org/abs/2605.22221)** (Phua et al., 2026, preprint) — Models trained on full running logs learn decisions that depend on the whole history even when only the current state matters — habits that should break on longer problems.

32. **[Performative Thinking?](https://arxiv.org/abs/2509.07339)** (Palod et al., 2025, preprint) — In the same maze/A*-trace setting as the thesis, emitted "search" length only loosely tracks true problem difficulty off-distribution.

33. **[Faith and Fate](https://arxiv.org/abs/2305.18654)** (Dziri et al., NeurIPS 2023) — Small per-step errors compound over long generations, so accuracy can collapse as traces grow.

34. **[Easy-to-Hard Generalization](https://arxiv.org/abs/2403.09472)** (Sun et al., NeurIPS 2024) — Checkers generalise better than solvers: a judge trained on easy problems reliably scores solutions to harder ones — what makes easy-to-hard bootstrapping loops feasible.

### Impact sources

35. **[The Countdown Game is NP-complete](https://arxiv.org/abs/2508.02900)** (Katz et al., 2025, preprint) — Because the task is genuinely hard, supervision is only ever cheap for small instances; train-small/solve-large is the only deployment story that scales.

36. **[Connectionism and Cognitive Architecture](https://www.sciencedirect.com/science/article/abs/pii/0010027788900315)** (Fodor & Pylyshyn, Cognition 1988) — The origin of the "productivity" criterion: genuine competence is unbounded — it extends beyond any finite set of experienced examples.

37. **[Generalization without Systematicity (SCAN)](https://arxiv.org/abs/1711.00350)** (Lake & Baroni, ICML 2018) — The modern restart of that debate: sequence models "fail spectacularly" when tested on longer command sequences than trained.

38. **[Compositionality Decomposed](https://arxiv.org/abs/1908.08351)** (Hupkes et al., JAIR 2020) — Makes the link explicit: their "productivity" test is exactly whether a model handles sequences longer than those seen in training.

39. **[Shortcut Learning in Deep Neural Networks](https://arxiv.org/abs/2004.07780)** (Geirhos et al., Nature Machine Intelligence 2020) — Position paper framing deep learning's failures as shortcuts that work on the benchmark but not beyond it; length extrapolation is the setting where the shortcut can be exactly characterised (with [Liu et al.](https://arxiv.org/abs/2210.10749) supplying the mechanism for transformers).

40. **[Train Short, Test Long (ALiBi)](https://arxiv.org/abs/2108.12409)** (Press et al., ICLR 2022) — Evidence the understanding transfers out: the position-encoding methods behind long-context language models came from exactly this train-short/test-long research.

41. **[Measuring AI Ability to Complete Long Software Tasks](https://arxiv.org/abs/2503.14499)** (Kwa et al./METR, 2025, preprint) and **[The Illusion of Diminishing Returns](https://arxiv.org/abs/2509.09677)** (Sinha et al., 2025; ICLR 2026 per arXiv) — Frontier agent capability is now measured as the length of task a model can execute, and small per-step accuracy gains compound into exponentially longer feasible tasks — the deployed-scale version of the question this section studies in controlled form.

42. **[Neural Algorithmic Reasoning](https://arxiv.org/abs/2105.02761)** (Veličković & Blundell, Patterns 2021) — The position paper naming the prize: if deep learning could mimic algorithms properly, "generalisation of the sort seen with algorithms would become possible with deep learning."
