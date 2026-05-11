# World Models at A* Conferences — A 2024-2026 Survey

> **Scope.** This survey collects recent works on *world models* published at top-tier (A\*) venues between 2024 and early 2026 — NeurIPS, ICML, ICLR, CVPR, ICCV, ECCV, CoRL, RSS, AAAI — augmented with a handful of industry technical reports (Cosmos, GAIA-2, Genie 2/3, Sora, V-JEPA 2, Dreamer 4) that the academic community treats as canonical references. The survey is intended as a journal-style synthesis: it (a) catalogues the literature with arXiv links, (b) groups it by sub-topic, (c) identifies the dominant techniques and trends, (d) **contrasts world-model-based agents with the RL-on-LLM paradigm**, and (e) lays out the **practical paths from an LLM to a world model**.

---

## 1. What counts as a "world model"?

Following Ha & Schmidhuber and the broader literature, a *world model* is a learned generative or predictive model of the dynamics of an environment — formally an approximation of
\(p(s_{t+1}, r_{t+1} \mid s_{\le t}, a_{\le t})\) — that can be rolled out to imagine futures and used for planning, model-based RL, simulation, data generation, or evaluation. We include the following lineages:

- **Model-based RL** with latent recurrent state-space models (the Dreamer family), discrete-token transformer WMs (IRIS / Δ-IRIS / STORM), and Mamba/SSM variants.
- **Generative video / image WMs** (Sora, Cosmos, Genie 1/2/3, GameNGen, Pandora, WorldDreamer, DIAMOND).
- **JEPA / latent-feature WMs** (V-JEPA, V-JEPA 2, DINO-WM, Seq-JEPA, LeWorldModel).
- **Driving WMs** (GAIA-1/2, Vista, DriveDreamer/DriveDreamer-2, DriveWorld, OccWorld, OccLLaMA, ReSim, Drive-WM, Epona).
- **Robotic / embodied WMs** (iVideoGPT, RoboScape, DreamGen, Ctrl-World, FLARE, Genie Envisioner, TesserAct, IRASim).
- **LLM-as-WM / LLM-coupled WMs** (RAP, Dynalang, Pandora, WALL-E, WorldCoder, WorldGPT, LWM, DECKARD).

---

## 2. Conference scoreboard

| Venue | Papers in survey | Dominant themes |
|---|---|---|
| **NeurIPS 2024** | 11 | Diffusion-WM, transformer-WM, MBRL, autonomous driving |
| **NeurIPS 2025** | 9 | Foundation WMs, long-term memory, physics-informed WMs, benchmarks |
| **ICML 2024** | 6 | Sample-efficient MBRL, foundation game WMs, 3D-VLA |
| **ICML 2025** | 10 | JEPA-style planning, continual MBRL, video-WM, VLA |
| **ICLR 2024** | 3 | TD-MPC2, MAMBA, R2I — strong MBRL backbone |
| **ICLR 2025** | 8 | Neural game engines, decoder-free WMs, action-conditioned diffusion |
| **ICLR 2026** | 5 | JEPA ablations, on-policy diffusion training, intuitive-physics eval |
| **CVPR 2024** | 4 | Driving WMs (Drive-WM, DriveWorld, GenAD), Generative Image Dynamics |
| **CVPR 2025** | 8 | Cosmos, NWM, 4D-scene WMs, occupancy WMs, GAIA-2 |
| **ICCV 2025** | 7 | Driving WMs, medical WM, embodied 4D WMs |
| **ECCV 2024** | 4 | DriveDreamer, OccWorld, NeMo, multi-agent driving WMs |
| **CoRL 2024 / 2025** | 5 | DINO-WM, Ctrl-World, FLARE, DreamGen, Sirius-Fleet |
| **RSS 2024 / 2025** | 2 | DWL humanoid (Outstanding Paper), WoMAP |
| **AAAI 2025** | 4 | DriveDreamer-2, OccLLaMA, Drive-OccWorld, Doe-1 |
| **EMNLP / ACL / NAACL** | 3 | RAP, Text-WM evaluation, Counterfactual reasoning |
| **Industry tech reports (anchored)** | 6 | Sora, Genie 2/3, Cosmos, GAIA-2, V-JEPA 2, Dreamer 4 |

---

## 3. Master paper table

Papers grouped by **sub-area**, then sorted by venue/year. arXiv IDs link to the canonical version.

### 3.1 Model-based RL (latent dynamics, transformer/Mamba/SSM WMs)

| # | Title | Lead authors | Venue + Year | arXiv | Contribution |
|---|---|---|---|---|---|
| 1 | TD-MPC2: Scalable, Robust World Models for Continuous Control | Hansen et al. | ICLR 2024 | [2310.16828](https://arxiv.org/abs/2310.16828) | Decoder-free latent WM with local trajectory optimisation; a single 317 M agent solves 80 continuous-control tasks. |
| 2 | Mastering Memory Tasks with World Models (R2I) | Samsami et al. | ICLR 2024 Oral | [2403.04253](https://arxiv.org/abs/2403.04253) | Adds S3M state-space modules to DreamerV3, giving super-human long-term-memory performance on POPGym / Memory Maze. |
| 3 | MAMBA: An Effective World Model Approach for Meta-RL | Rimon et al. | ICLR 2024 | [2403.09859](https://arxiv.org/abs/2403.09859) | Task-conditioned WMs that adapt rapidly across meta-RL benchmarks. |
| 4 | DIAMOND: Diffusion for World Modeling | Alonso, Jelley et al. | NeurIPS 2024 Spotlight | [2405.12399](https://arxiv.org/abs/2405.12399) | First pixel-space *diffusion* WM that trains an RL agent end-to-end; SOTA 1.46 mean HNS on Atari 100k and demonstrably a neural CS:GO engine. |
| 5 | iVideoGPT: Interactive VideoGPTs are Scalable World Models | Wu, Yin et al. | NeurIPS 2024 | [2405.15223](https://arxiv.org/abs/2405.15223) | Compressive tokeniser + AR transformer pre-trained on millions of manipulation trajectories. |
| 6 | GenRL: Multimodal-Foundation World Models | Mazzaglia | NeurIPS 2024 | [2406.18043](https://arxiv.org/abs/2406.18043) | Aligns frozen VLM features to a latent WM so embodied tasks can be specified by text or image. |
| 7 | HarmonyDream: Task Harmonization Inside World Models | Ma, Wu et al. | ICML 2024 | [2310.00344](https://arxiv.org/abs/2310.00344) | Dynamically balances observation- vs. reward-loss weights, lifting Atari-100k SOTA. |
| 8 | Δ-IRIS: Efficient World Models with Context-Aware Tokenisation | Micheli et al. | ICML 2024 | [2406.19320](https://arxiv.org/abs/2406.19320) | Encodes stochastic temporal *deltas* with an AR transformer; SOTA on Crafter, much faster than IRIS. |
| 9 | AD3: Implicit Action is the Key for World Models to Distinguish Visual Distractors | Wang et al. | ICML 2024 | [2403.09976](https://arxiv.org/abs/2403.09976) | Implicit action prediction disentangles distractors. |
| 10 | HRSSM: Learning Latent Dynamic Robust Representations | Sun et al. | ICML 2024 | [2405.06263](https://arxiv.org/abs/2405.06263) | Spatio-temporal masking + bisimulation for Dreamer. |
| 11 | LS-Imagine: Open-World RL over Long Short-Term Imagination | Li, Wang et al. | ICLR 2025 Oral (top 1.8 %) | [2410.03618](https://arxiv.org/abs/2410.03618) | Jumpy goal-conditioned transitions and affordance maps extend Dreamer's horizon in MineDojo. |
| 12 | DC-MPC: Discrete Codebook World Models for Continuous Control | Scannell et al. | ICLR 2025 | [2503.00653](https://arxiv.org/abs/2503.00653) | Discrete-codebook latent + MPC matches TD-MPC2 / DreamerV3 on control. |
| 13 | PWM: Policy Learning with Multi-Task World Models | Georgiev et al. | ICLR 2025 | [2407.02466](https://arxiv.org/abs/2407.02466) | Shows policies can be trained in <10 min/task from *smooth* (not necessarily accurate) offline-pre-trained WMs. |
| 14 | Hierarchical World Models as Whole-Body Humanoid Controllers (Puppeteer) | Hansen et al. | ICLR 2025 | [2405.18418](https://arxiv.org/abs/2405.18418) | TD-MPC2 with a low-level MoCap tracker and a high-level visual puppeteer. |
| 15 | Drama: Mamba-Enabled Model-Based RL | Wang et al. | ICLR 2025 | [2410.08893](https://arxiv.org/abs/2410.08893) | Replaces transformer with Mamba/SSM, halving compute. |
| 16 | When Do Neural Networks Learn World Models? | Zhang et al. | ICLR 2025 Oral | OpenReview | Theoretical analysis of when nets internalise a coherent WM. |
| 17 | Improving Transformer World Models for Data-Efficient RL | Dedieu et al. (DeepMind) | ICML 2025 | [2502.01591](https://arxiv.org/abs/2502.01591) | "Dyna with warm-up" + NN tokeniser + block-teacher-forcing — first MBRL agent to surpass humans on Craftax-classic at 1 M steps. |
| 18 | TrajWorld: Trajectory World Models for Heterogeneous Environments | Yin et al. | ICML 2025 | [2502.01366](https://arxiv.org/abs/2502.01366) | UniTraj dataset (1 M trajectories, 80 envs) + flexible WM that adapts to sensor/actuator changes. |
| 19 | Continual RL by Planning with Online World Models | Liu et al. | ICML 2025 Spotlight | [2507.09177](https://arxiv.org/abs/2507.09177) | Follow-the-Leader shallow WM + MPC; provably immune to catastrophic forgetting. |
| 20 | PIGDreamer: Privileged Information-Guided WM for Safe POMDP RL | Huang et al. | ICML 2025 | [2508.02159](https://arxiv.org/abs/2508.02159) | Asymmetric Dreamer exploits privileged info at training time only. |
| 21 | TD-Flow: Temporal Difference Flows | Farebrother et al. | ICML 2025 Oral | [2503.09817](https://arxiv.org/abs/2503.09817) | Flow-matching solution of a new Bellman equation; 5× longer effective horizon. |
| 22 | Dreamer 4: Training Agents Inside of Scalable World Models | Hafner, Yan et al. | arXiv 2025 / NeurIPS 2025 era | [2509.24527](https://arxiv.org/abs/2509.24527) | Block-causal transformer WM with *shortcut forcing*; real-time interactive in Minecraft from mostly unlabelled video. |
| 23 | DMWM: Dual-Mind World Model with Long-Term Imagination | NeurIPS 2025 authors | NeurIPS 2025 | OpenReview | Dual-process WM with explicit logical-reasoning module. |
| 24 | Context-Aware World Models for Task-Agnostic Control | Gurbuz et al. | NeurIPS 2025 | OpenReview | Context-conditioned WM for multi-task control. |
| 25 | Operator World Models for RL | Novelli et al. | NeurIPS 2024 | [2406.19861](https://arxiv.org/abs/2406.19861) | Koopman-operator-based WM for sample-efficient RL. |
| 26 | PLSM: Softly State-Invariant World Models | Saanum et al. | NeurIPS 2024 | [2401.17354](https://arxiv.org/abs/2401.17354) | Regularises latent dynamics so action effects are state-invariant. |
| 27 | One-shot Transformer World Models from a Synthetic Prior | Ferreira et al. | NeurIPS 2024 | [2409.14084](https://arxiv.org/abs/2409.14084) | In-context WM trained on synthetic priors only. |
| 28 | R2-Dreamer: Redundancy-Reduced WMs without Decoders / Augmentation | ICLR 2026 authors | ICLR 2026 | OpenReview | Decoder-free Dreamer via redundancy reduction. |
| 29 | WIMLE: Uncertainty-Aware WMs with IMLE | ICLR 2026 authors | ICLR 2026 | OpenReview | Implicit-MLE-trained WM gives calibrated uncertainty for continuous control. |
| 30 | Horizon Imagination: Efficient On-Policy Training in Diffusion WMs | ICLR 2026 authors | ICLR 2026 | OpenReview | Closes the loop between diffusion WMs and on-policy RL. |

### 3.2 JEPA / latent-feature world models

| # | Title | Lead authors | Venue + Year | arXiv | Contribution |
|---|---|---|---|---|---|
| 31 | V-JEPA 2: Self-Supervised Video Models for Understanding, Prediction & Planning | Assran, Bardes, LeCun et al. | arXiv 2025 / NeurIPS 2025 | [2506.09985](https://arxiv.org/abs/2506.09985) | 1 M-hr-video JEPA + action-conditioned post-training (V-JEPA 2-AC); zero-shot Franka pick/place from image goals. |
| 32 | DINO-WM: World Models on Pre-trained Visual Features | Zhou, Pinto et al. | CoRL 2024 / ICML 2025 | [2411.04983](https://arxiv.org/abs/2411.04983) | Predicts DINOv2 patch features and plans by gradient optimisation — task-agnostic, zero-shot. |
| 33 | Seq-JEPA: Autoregressive Predictive Learning of Invariant-Equivariant WMs | Ghaemi et al. | NeurIPS 2025 | [2502.09858](https://arxiv.org/abs/2502.09858) | AR-JEPA disentangling invariance and equivariance. |
| 34 | JEPA-WMs: What Drives Success in Physical Planning with JEPA WMs? | Terver et al. (FAIR) | ICLR 2026 | [2512.24497](https://arxiv.org/abs/2512.24497) | Systematic ablation; new design beats DINO-WM and V-JEPA-2-AC. |
| 35 | LeWorldModel: Stable End-to-End JEPA WM from Pixels | ICLR 2026 era | arXiv 2026 | [le-wm.github.io](https://le-wm.github.io/) | First stable JEPA WM trained end-to-end from raw pixels. |
| 36 | A Path Towards Autonomous Machine Intelligence | LeCun | OpenReview 2022 | [PDF](https://openreview.net/pdf?id=BZ5a1r-kVsf) | Manifesto — JEPA + 6-module architecture, the conceptual root of the JEPA-WM lineage. |

### 3.3 Generative video / image / game world models

| # | Title | Lead authors | Venue + Year | arXiv / Link | Contribution |
|---|---|---|---|---|---|
| 37 | Sora: Video Generation Models as World Simulators | Brooks, Peebles et al. (OpenAI) | OpenAI report 2024 | [openai.com](https://openai.com/index/video-generation-models-as-world-simulators/) | Spacetime-patch diffusion transformer; emergent 3D consistency, object permanence, controllable Minecraft rollouts. |
| 38 | Genie: Generative Interactive Environments | Bruce et al. (DeepMind) | ICML 2024 Best Paper | [2402.15391](https://arxiv.org/abs/2402.15391) | Learns latent-action 2D playable environments from unlabelled internet videos. |
| 39 | Genie 2: A Large-Scale Foundation World Model | Parker-Holder et al. | DeepMind blog Dec 2024 | [deepmind.google](https://deepmind.google/blog/genie-2-a-large-scale-foundation-world-model/) | 3-D playable worlds from a single image; consistent 10-20 s rollouts; physics emergence. |
| 40 | Genie 3: A New Frontier for World Models | DeepMind | DeepMind blog Aug 2025 | [deepmind.google](https://deepmind.google/blog/genie-3-a-new-frontier-for-world-models/) | Real-time 24 fps / 720p text-to-world; minute-scale coherent rollouts with emergent world-memory. |
| 41 | GameNGen: Diffusion Models Are Real-Time Game Engines | Valevski et al. | ICLR 2025 | [2408.14837](https://arxiv.org/abs/2408.14837) | Stable-Diffusion-based DOOM at 20 fps, PSNR 29.4; first neural game engine. |
| 42 | Oasis: An Interactive Minecraft World Model | Decart AI / Etched | Industry 2024 | (report) | Real-time neural Minecraft simulator at ~360 p / 20 fps. |
| 43 | Pandora: General World Model with Natural-Language Actions and Video States | Xiang et al. (Maitrix) | NeurIPS 2024 W. | [2406.09455](https://arxiv.org/abs/2406.09455) | Hybrid AR + diffusion WM driven by free-text actions across many domains. |
| 44 | WorldDreamer: General World Models via Masked-Token Prediction | Wang et al. | arXiv 2024 | [2401.09985](https://arxiv.org/abs/2401.09985) | Spatial-temporal masked-token video model unifying text/image/action conditioning. |
| 45 | LWM: World Model on Million-Length Video and Language | Liu, Yan, Zaharia, Abbeel | arXiv 2024 | [2402.08268](https://arxiv.org/abs/2402.08268) | 1 M-token-context multimodal AR WM trained with Blockwise RingAttention. |
| 46 | Vid2World: Crafting Video Diffusion Models into Interactive WMs | Huang et al. | ICLR 2026 | [2505.14357](https://arxiv.org/abs/2505.14357) | Causal-ifies a video diffusion model for AR action-conditioned rollout. |
| 47 | AVID: Adapting Video Diffusion Models to World Models | Rigter et al. | ICLR 2025 | [2410.12822](https://arxiv.org/abs/2410.12822) | Adds a learned mask + action-conditioned adapter to a frozen video diffusion backbone. |
| 48 | Generative Image Dynamics | Li, Tucker, Snavely | CVPR 2024 Best Paper | [2309.07906](https://arxiv.org/abs/2309.07906) | Predicts a *spectral volume* for single-image looping dynamics. |
| 49 | Video World Models with Long-Term Spatial Memory | Wu et al. | NeurIPS 2025 | [2506.05284](https://arxiv.org/abs/2506.05284) | Explicit 3-D spatial memory preserves consistency under scene revisits. |
| 50 | WorldMem: Long-Term Consistent World Simulation with Memory | NeurIPS 2025 authors | NeurIPS 2025 | [2504.12369](https://arxiv.org/abs/2504.12369) | External-memory video WM for long rollouts. |
| 51 | WorldModelBench: Judging Video Generators as World Models | NeurIPS 2025 authors | NeurIPS 2025 | [2502.20694](https://arxiv.org/abs/2502.20694) | 67 K-label benchmark for instruction following + physics adherence. |
| 52 | LikePhys: Evaluating Intuitive Physics in Video Diffusion via Likelihood Preference | ICLR 2026 authors | ICLR 2026 | OpenReview | Likelihood-based intuitive-physics evaluation. |
| 53 | Cosmos World Foundation Model Platform for Physical AI | NVIDIA (77 authors) | CVPR 2025 W. / arXiv | [2501.03575](https://arxiv.org/abs/2501.03575) | Open suite of diffusion + AR WFMs (Predict / Transfer / Reason) trained on 20 M hr of physical-world video. |

### 3.4 Autonomous-driving world models

| # | Title | Lead authors | Venue + Year | arXiv | Contribution |
|---|---|---|---|---|---|
| 54 | Drive-WM: Driving into the Future | Wang et al. | CVPR 2024 | [2311.17918](https://arxiv.org/abs/2311.17918) | First multi-view spatial-temporal video WM compatible with end-to-end planners. |
| 55 | DriveWorld: 4D Pre-trained Scene Understanding via WMs | Min et al. (PKU / OpenDriveLab) | CVPR 2024 | [2405.04390](https://arxiv.org/abs/2405.04390) | 4-D scene-understanding WM pretrained on multi-camera video; +3-7 % across nuScenes tasks. |
| 56 | GenAD: Generalised Predictive Model for Autonomous Driving | Yang et al. (OpenDriveLab) | CVPR 2024 Highlight | [2403.09630](https://arxiv.org/abs/2403.09630) | First large-scale generative video WM for driving (>2000 hr of web video). |
| 57 | DriveDreamer: Real-World-Driven WMs for Autonomous Driving | Wang et al. (GigaAI / Tsinghua) | ECCV 2024 | [2309.09777](https://arxiv.org/abs/2309.09777) | Two-stage diffusion WM trained on real driving data. |
| 58 | OccWorld: 3-D Occupancy WM for AV | Zheng, Chen, Lu et al. (Tsinghua) | ECCV 2024 | [2311.16038](https://arxiv.org/abs/2311.16038) | Tokenises 3-D occupancy and forecasts ego + scene with a spatio-temporal transformer. |
| 59 | NeMo: Neural Volumetric WMs for AV | Huang, Zhang, Ohn-Bar | ECCV 2024 | (ECVA proc.) | Self-supervised volumetric WM jointly trained for reconstruction + occupancy. |
| 60 | Copilot4D: Unsupervised WMs via Discrete Diffusion | Zhang et al. (Waabi) | ICLR 2024 | [2311.01017](https://arxiv.org/abs/2311.01017) | VQ-VAE + discrete diffusion over LiDAR tokens; cuts SOTA Chamfer error > 50 %. |
| 61 | Vista: Generalisable Driving WM | Gao et al. (OpenDriveLab) | NeurIPS 2024 | [2405.17398](https://arxiv.org/abs/2405.17398) | High-res long-horizon WM with command/goal/trajectory/speed conditioning. |
| 62 | DrivingDojo Dataset | Wang, Cheng et al. | NeurIPS 2024 D&B | [2410.18603](https://arxiv.org/abs/2410.18603) | Large diverse driving dataset + Action-Instruction-Following benchmark. |
| 63 | DriveDreamer-2: LLM-Enhanced Driving WM | Zhao, Wang, Zhu et al. | AAAI 2025 | [2403.06845](https://arxiv.org/abs/2403.06845) | LLM turns user text into agent trajectories + HD maps; multi-view diffusion WM produces customised driving videos. |
| 64 | Drive-OccWorld: 4-D Occupancy Forecasting via WMs | Yang, Yu et al. | AAAI 2025 | [2408.14197](https://arxiv.org/abs/2408.14197) | Action-conditioned 4-D occupancy WM integrated with planner. |
| 65 | OccLLaMA: Occupancy-Language-Action Generative WM | Wei, Long et al. (Fudan) | AAAI 2025 | [2409.03272](https://arxiv.org/abs/2409.03272) | Unifies semantic occupancy, language, and action in a LLaMA-style AR WM. |
| 66 | Doe-1: Closed-Loop Autonomous Driving with a Large WM | Zheng et al. (Tsinghua) | AAAI 2025 | [2412.09627](https://arxiv.org/abs/2412.09627) | Single large WM unifies perception, prediction, and planning. |
| 67 | DriveDreamer4D | Zhao et al. | CVPR 2025 | [2410.13571](https://arxiv.org/abs/2410.13571) | WMs as data factories for 4-D Gaussian-splat scene reconstruction; +32-46 % FID. |
| 68 | DrivingSphere | Yan et al. | CVPR 2025 | [2411.11252](https://arxiv.org/abs/2411.11252) | OccDreamer-built 4-D world for city-scale closed-loop AV simulation. |
| 69 | UniScene | Li et al. | CVPR 2025 | [2412.05435](https://arxiv.org/abs/2412.05435) | Layout → occupancy → (video + LiDAR) progressive generation. |
| 70 | GaussianWorld | Zuo et al. (Tsinghua) | CVPR 2025 | [2412.10373](https://arxiv.org/abs/2412.10373) | 3-D occupancy reformulated as forecasting in 3-D Gaussian space; +2 % mIoU. |
| 71 | GEM: Generalisable Ego-Vision Multimodal WM | Hassan et al. (EPFL) | CVPR 2025 | [2412.11198](https://arxiv.org/abs/2412.11198) | Fine-grained control of ego-motion, object dynamics, scene composition. |
| 72 | MaskGWM | Ni et al. | CVPR 2025 | [2502.11663](https://arxiv.org/abs/2502.11663) | Masked video reconstruction for generalisable driving WMs. |
| 73 | GAIA-2 | Russell et al. (Wayve) | CVPR 2025 W. | [2503.20523](https://arxiv.org/abs/2503.20523) | Multi-camera latent-diffusion WM conditioned on ego, agents, environment, semantics. |
| 74 | HERMES | Zhou et al. | ICCV 2025 | [2501.14729](https://arxiv.org/abs/2501.14729) | Unified self-driving WM that jointly understands and generates 3-D scenes. |
| 75 | Epona | Zhang et al. | ICCV 2025 | [2506.24113](https://arxiv.org/abs/2506.24113) | Hybrid AR + diffusion WM that produces minute-long consistent driving video. |
| 76 | InfiniCube | Lu et al. (NVIDIA) | ICCV 2025 | [2412.03934](https://arxiv.org/abs/2412.03934) | Unbounded 3-D Gaussian dynamic scene generation with HD-map / 3-D-box / text controls. |
| 77 | World4Drive | Zheng et al. | ICCV 2025 | [2507.00603](https://arxiv.org/abs/2507.00603) | Intention-aware latent WM ranking trajectories in latent space. |
| 78 | ReSim: Reliable World Simulation for AV | Yang, Chitta et al. (OpenDriveLab) | NeurIPS 2025 Spotlight | [2506.09981](https://arxiv.org/abs/2506.09981) | Co-trains on hazardous/non-expert data; +44 % visual fidelity, Video2Reward module. |

### 3.5 Robotic / embodied / 4-D world models

| # | Title | Lead authors | Venue + Year | arXiv | Contribution |
|---|---|---|---|---|---|
| 79 | Sirius-Fleet: Multi-Task Robot Fleet Learning with Visual WMs | Liu, Zhu et al. (UT Austin) | CoRL 2024 | [2410.22689](https://arxiv.org/abs/2410.22689) | Visual WM forecasts manipulation outcomes and flags anomalies for HITL fleet learning. |
| 80 | DWL: Mastering Humanoid Locomotion with a Denoising WM | Gu et al. | RSS 2024 Outstanding | [2408.14472](https://arxiv.org/abs/2408.14472) | First humanoid to walk snow/stairs zero-shot sim-to-real with a denoising WM. |
| 81 | IRASim: Fine-Grained WM for Robot Manipulation | Zhu et al. (ByteDance) | ICCV 2025 | [2406.14540](https://arxiv.org/abs/2406.14540) | Trajectory-conditioned video WM for manipulation data augmentation. |
| 82 | TesserAct: Learning 4-D Embodied WMs | UMass | ICCV 2025 | [2504.20995](https://arxiv.org/abs/2504.20995) | First open-source 4-D embodied WM jointly producing RGB + depth + normal video. |
| 83 | Navigation World Models (NWM) | Bar, Zhou, Tran, Darrell, LeCun | CVPR 2025 Honorable Mention | [2412.03572](https://arxiv.org/abs/2412.03572) | 1 B-param conditional diffusion transformer on first-person human + robot video; ranks trajectories visually. |
| 84 | RoboScape: Physics-Informed Embodied WM | Shang et al. (Tsinghua FIB) | NeurIPS 2025 Spotlight | [2506.23135](https://arxiv.org/abs/2506.23135) | Joint RGB + depth + keypoint dynamics for physics-consistent robotic rollouts. |
| 85 | Ctrl-World: Controllable Generative WM for Robot Manipulation | NVIDIA / Stanford | CoRL 2025 | [2510.10125](https://arxiv.org/abs/2510.10125) | 20-s consistent manipulation rollouts on DROID; +44.7 % policy success via WM-imagined data. |
| 86 | FLARE: Implicit World Modelling for Robot Learning | Zhuang et al. (NVIDIA GEAR) | CoRL 2025 | [2505.15659](https://arxiv.org/abs/2505.15659) | Future-latent alignment tokens give VLA policies implicit WM benefits. |
| 87 | DreamGen | NVIDIA GEAR | CoRL 2025 | [2505.12705](https://arxiv.org/abs/2505.12705) | Video-WM-synthesised neural trajectories drive cross-environment generalisation. |
| 88 | WoMAP: WMs for Embodied Open-Vocabulary Object Localisation | RSS 2025 W. | RSS 2025 / CoRL 2025 | [2506.01600](https://arxiv.org/abs/2506.01600) | Open-vocab embodied WM for object search. |
| 89 | Genie Envisioner: World Foundation Platform for Robotic Manipulation | AgiBot | arXiv 2025 / W. | [2508.05635](https://arxiv.org/abs/2508.05635) | GE-Base + GE-Act + GE-Sim + EWMBench trained on 3000 hr of manipulation. |
| 90 | 3D-VLA: 3-D Vision-Language-Action Generative WM | Zhen et al. | ICML 2024 | [2403.09631](https://arxiv.org/abs/2403.09631) | 3-D LLM with diffusion heads for goal images / point clouds. |
| 91 | UP-VLA: Unified Understanding & Prediction for Embodied Agents | ICML 2025 | ICML 2025 | [2501.18867](https://arxiv.org/abs/2501.18867) | VLM + future prediction merged into one VLA. |
| 92 | EVA: Embodied WM for Future Video Anticipation | Chi et al. | ICML 2025 | [2410.15461](https://arxiv.org/abs/2410.15461) | Embodied long-horizon video-anticipation WM. |
| 93 | Robotic World Model: NN Simulator for Robust Policy Optimisation | Li et al. (ETH) | NeurIPS 2025 EWM W. Outstanding | [2501.10100](https://arxiv.org/abs/2501.10100) | Dual-autoregressive WM for partially observable robot dynamics; sim-to-real RL. |
| 94 | Medical World Model (MeWM) | Yang et al. | ICCV 2025 | [2506.18254](https://arxiv.org/abs/2506.18254) | First medical WM: simulates tumour dynamics under treatment. |

### 3.6 LLM-as-WM / LLM-coupled world models

| # | Title | Lead authors | Venue + Year | arXiv | Contribution |
|---|---|---|---|---|---|
| 95 | Reasoning with LM is Planning with WM (RAP) | Hao et al. | EMNLP 2023 | [2305.14992](https://arxiv.org/abs/2305.14992) | An LLM acts simultaneously as policy and WM; MCTS over imagined language states. |
| 96 | Language Models Meet World Models | Xiang et al. | NeurIPS 2023 | [2305.10626](https://arxiv.org/abs/2305.10626) | Distils embodied experience from a simulator into the LLM with EWC. |
| 97 | Dynalang: Learning to Model the World with Language | Lin et al. | ICML 2024 Oral | [2308.01399](https://arxiv.org/abs/2308.01399) | DreamerV3 extended to predict future text + image + reward — the canonical Dreamer/LLM bridge. |
| 98 | DECKARD: Embodied Decision-Making with Language-Guided WMs | Nottingham et al. | ICML 2023 | [2301.12050](https://arxiv.org/abs/2301.12050) | LLM proposes an abstract WM subgoal DAG that is corrected from environment feedback. |
| 99 | Voyager | Wang et al. | TMLR 2024 | [2305.16291](https://arxiv.org/abs/2305.16291) | GPT-4 Minecraft agent with skill-as-code library; implicit, externalised WM. |
| 100 | Can LMs Serve as Text-Based World Simulators? | Wang et al. | ACL 2024 | [2406.06485](https://arxiv.org/abs/2406.06485) | ByteSized32-State-Prediction benchmark — GPT-4 simulates only ~50 % of environment-driven transitions. |
| 101 | Evaluating the WM Implicit in a Generative Model | Vafa et al. | NeurIPS 2024 | [2406.03689](https://arxiv.org/abs/2406.03689) | Myhill-Nerode-style probes show next-token-accurate models can lack a coherent WM. |
| 102 | WKM: Agent Planning with World Knowledge Model | Qiao et al. | NeurIPS 2024 | [2405.14205](https://arxiv.org/abs/2405.14205) | LLM agent uses a learned global + local "world-knowledge" model to suppress hallucinated actions. |
| 103 | WorldCoder: Model-Based LLM Agent | Tang, Hu et al. | NeurIPS 2024 | [2402.12275](https://arxiv.org/abs/2402.12275) | The LLM emits an *explicit Python program* as its WM, transferable via code edits. |
| 104 | WorldGPT: Empowering LLM as Multimodal WM | Ge et al. | ACM MM 2024 | [2404.18202](https://arxiv.org/abs/2404.18202) | Multimodal LLM predicts state transitions in abstract feature space; introduces WorldNet benchmark. |
| 105 | GenSim / GenSim2: Generating Robotic Simulation Tasks via LLMs | Wang et al. | ICLR 2024 / arXiv 2024 | [2310.01361](https://arxiv.org/abs/2310.01361), [2410.03645](https://arxiv.org/abs/2410.03645) | LLM writes the WM as executable simulator code. |
| 106 | RoboGen: Generative Simulation for Robot Learning | Wang et al. | ICML 2024 | [2311.01455](https://arxiv.org/abs/2311.01455) | LLM-orchestrated automatic task / scene / reward generation. |
| 107 | WALL-E 2.0: World Alignment by Neurosymbolic Rule Learning | Zhou et al. | arXiv 2025 | [2410.07484](https://arxiv.org/abs/2410.07484), [2504.15785](https://arxiv.org/abs/2504.15785) | Closes the LLM-vs-real-environment gap with learned symbolic rules + MPC-style look-ahead. |
| 108 | WorldLLM: Curiosity-Driven Theory-Making | Levy et al. | arXiv 2025 | [2506.06725](https://arxiv.org/abs/2506.06725) | LLM emits natural-language hypotheses about dynamics, updated Bayesianly without fine-tuning. |
| 109 | Reasoning or Reciting? Counterfactual Probes of LLM Reasoning | Wu et al. | NAACL 2024 | [2307.02477](https://arxiv.org/abs/2307.02477) | Counterfactual tasks expose memorisation vs. rule-following in LLMs. |
| 110 | LLMs Can't Plan, but Can Help in LLM-Modulo | Kambhampati et al. | ICML 2024 | [2402.01817](https://arxiv.org/abs/2402.01817) | Argues LLMs can propose plans but require an external sound WM (PDDL, code, simulator) as verifier. |

### 3.7 Position / theory / "Era of Experience"

| # | Title | Author | Venue / Date | Link |
|---|---|---|---|---|
| 111 | The Bitter Lesson | Sutton | 2019 | [link](http://www.incompleteideas.net/IncIdeas/BitterLesson.html) |
| 112 | Welcome to the Era of Experience | Silver & Sutton | MIT Press 2025 | [PDF](https://storage.googleapis.com/deepmind-media/Era-of-Experience%20/The%20Era%20of%20Experience%20Paper.pdf) |
| 113 | Introduction to Latent-Variable Energy-Based Models | LeCun | arXiv 2306.02572 | [link](https://arxiv.org/abs/2306.02572) |

---

## 4. Topic groupings

We cluster the ~110 papers into 11 themes; **bold** numbers refer to the master table.

1. **Diffusion world models (pixel- and latent-space).** DIAMOND, GameNGen, Vid2World, AVID, Cosmos, GAIA-2, Pandora, Drive-WM, GEM, MaskGWM, Vista, Epona, NWM, DrivingSphere, Doe-1, Genie Envisioner — diffusion has become the default backbone for high-fidelity video / scene WMs (**4, 41, 46, 47, 53, 73, 61, 71, 75, 83, 89**).
2. **Transformer / SSM / Mamba WMs.** Δ-IRIS, iVideoGPT, GIT-STORM, Improving-Transformer-WMs (Dedieu), Drama (Mamba), Dreamer 4, OccWorld, OccLLaMA, HERMES (**5, 8, 15, 17, 22, 58, 65, 74**). Together with diffusion these define the *generative* WM toolbox.
3. **JEPA / latent-feature WMs.** V-JEPA 2, DINO-WM, Seq-JEPA, JEPA-WMs, LeWorldModel, FLARE — predicting in pre-trained representation space rather than pixels (**31-35, 86**).
4. **Driving world models.** Drive-WM, GenAD, DriveWorld, DriveDreamer, OccWorld, NeMo, Copilot4D, Vista, DrivingDojo, DriveDreamer-2, Drive-OccWorld, OccLLaMA, Doe-1, DriveDreamer4D, DrivingSphere, UniScene, GaussianWorld, GEM, MaskGWM, GAIA-2, HERMES, Epona, InfiniCube, World4Drive, ReSim — by far the densest sub-field (**54-78**).
5. **Embodied & robotic WMs.** Sirius-Fleet, DWL, IRASim, TesserAct, NWM, RoboScape, Ctrl-World, FLARE, DreamGen, WoMAP, Genie Envisioner, 3D-VLA, UP-VLA, EVA, Robotic World Model (**79-93**).
6. **Neural game engines / interactive simulators.** Genie 1/2/3, GameNGen, DIAMOND, Oasis, Dreamer 4 — the "playable" branch of WMs (**4, 22, 38-42**).
7. **LLM-as-WM / LLM-coupled.** RAP, Dynalang, DECKARD, Voyager, WKM, WorldCoder, WorldGPT, WALL-E, WorldLLM, GenSim, RoboGen, Pandora, LWM (**95-108, 43, 45**).
8. **MBRL specialisations.** Continual (DRAGO, Continual-RL-WMs), safe (PIGDreamer), multi-task (PWM, TrajWorld, Context-Aware WMs), distractors (AD3, SeeX, HRSSM), exploration / memory (R2I, LS-Imagine, PLSM), meta-RL (MAMBA), operator-theoretic (Operator WMs) (**1-30**, esp. **19, 20, 11-13, 9-10, 23-26**).
9. **Long-term memory and consistency.** R2I (SSM), LS-Imagine (jumpy), Video-WM-Long-Term-Spatial-Memory, WorldMem, DMWM, Genie 3 (**2, 11, 49, 50, 23, 40**).
10. **Evaluation & theory of WMs.** "When do NNs learn WMs?", Vafa et al., WorldModelBench, EWMBench, LikePhys, Can LMs serve as text simulators?, Reasoning or Reciting? (**16, 51, 52, 100, 101, 109**).
11. **4-D / occupancy / physics-aware WMs.** OccWorld, OccLLaMA, Drive-OccWorld, DrivingSphere, UniScene, GaussianWorld, InfiniCube, TesserAct, RoboScape, NeMo, DriveDreamer4D (**58, 65, 64, 68-70, 76, 82, 84, 59, 67**).

---

## 5. Trending techniques (2024-2026)

1. **Diffusion-based world modelling**, replacing discrete-token VQ-style WMs. DIAMOND (NeurIPS 2024) was the proof point; by ICLR 2025 / CVPR 2025 every new driving and game WM used diffusion (Vista, GAIA-2, GameNGen, Cosmos, Vid2World, Epona, InfiniCube).
2. **Predicting in pre-trained latent space (JEPA / DINO).** V-JEPA 2, DINO-WM, JEPA-WMs, Seq-JEPA, FLARE — sidesteps pixel synthesis altogether, gaining orders of magnitude in planning efficiency and matching or beating pixel-space WMs at downstream control.
3. **Action-conditioned next-token / next-frame supervision.** Pandora, WorldDreamer, Vid2World, Dynalang, Genie 3 — train on (state, action, next-state) triples to inject controllability into pretrained video / language backbones.
4. **WM as a synthetic-data factory.** DriveDreamer4D, UniScene, DreamGen, Cosmos, IRASim — WMs synthesise training data for perception, scene reconstruction, and policy learning, with measurable downstream gains.
5. **Code/neuro-symbolic world models.** WorldCoder, GenSim/RoboGen, WALL-E — the LLM emits Python or symbolic rules that *are* the WM, giving editable, transferable, and verifiable dynamics.
6. **Long-horizon memory & consistency.** Explicit memory modules (WorldMem, Long-Term Spatial Memory, Genie 3), SSMs (R2I, Drama), and jumpy transitions (LS-Imagine) all attack the "rollout drift" failure.
7. **Hybrid AR + diffusion architectures.** Pandora, Epona, Genie Envisioner — autoregress over a coarse plan / latent state, then diffuse the fine frame.
8. **4-D / occupancy / Gaussian representations.** OccWorld → Drive-OccWorld → GaussianWorld → InfiniCube → TesserAct — explicit 3-D-/4-D-aware state spaces in place of plain RGB.
9. **Privileged information & asymmetric training.** PIGDreamer, RoboScape, ReSim — train with extra modalities (depth, keypoints, hazardous data) that are unavailable at deployment.
10. **Real-time interactive rollout.** GameNGen (20 fps DOOM), Oasis, Genie 2/3, Dreamer 4 — interactivity at video frame rates is now a benchmark capability.
11. **Foundation pre-training for WMs.** Cosmos (20 M hr), V-JEPA 2 (1 M hr), LWM (1 M-token), Genie 3, Sora — billion-parameter, internet-scale pretraining is now standard for general-purpose WMs.

---

## 6. Trending topics

1. **Foundation / general-purpose world models.** Cosmos, Genie 2/3, V-JEPA 2, Sora, Pandora, LWM, Dreamer 4. The clear macro-trend of the period.
2. **Driving WMs converging to a recipe.** Multi-camera latent diffusion + structured controls (trajectory, HD map, agents, semantics) + closed-loop simulation. CVPR/ICCV/AAAI 2024-2025 saw an industry-academia convergence.
3. **Embodied / robotic WMs as the new VLA substrate.** UP-VLA, FLARE, 3D-VLA, V-JEPA 2-AC, DreamGen, Genie Envisioner — "video / WM pretraining → action head" is now the consensus VLA recipe.
4. **WM-based evaluation of generative models.** WorldModelBench, EWMBench, LikePhys, ByteSized32-State-Prediction, Vafa et al.'s probes — the field is maturing past "did the rollout look pretty?" to formal, verifier-based evaluation.
5. **LLM × WM convergence.** OccLLaMA, HERMES, Doe-1, DriveDreamer-2, RAP, WALL-E, Pandora — language conditioning, code-as-WM, and LLM-style architectures are saturating the WM stack.
6. **Continual / safe / privileged variants of Dreamer.** Dreamer is now a *base* on which spec-specific extensions are built rather than the goal in itself.
7. **Theory of when networks learn world models.** Vafa, "When do NNs learn WMs?" (ICLR 2025 Oral), counterfactual probes — opens up a foundational sub-area parallel to mechanistic interpretability.
8. **Physics-aware WMs.** RoboScape, TesserAct, GaussianWorld, NeMo, LikePhys — depth/normal/keypoint co-training and physical-plausibility metrics.
9. **Domain-specific WMs.** Medical (MeWM), driving (entire row), humanoid locomotion (DWL), open-vocab navigation (WoMAP) — verticalisation is accelerating.
10. **World-model workshops as new flagship venues.** ICLR 2025 *Workshop on World Models*, ICLR 2026 *Workshop on World Models*, ICML 2025 *Building Physically Plausible WMs*, NeurIPS 2025 *Embodied World Models for Decision Making* — institutional confirmation that WMs have crystallised as a top-tier subfield.

---

## 7. World Models vs. RL on LLMs — a side-by-side comparison

The 2023–2026 landscape has produced two superficially similar but conceptually distinct lines of work: (a) **world-model-based agents** (Dreamer-V3 / -4, V-JEPA 2, DINO-WM, Cosmos, Genie 3 …) and (b) **RL applied on top of LLMs** (RLHF, DPO, RLAIF, RLVR, GRPO, R1, Tülu 3 …). Both wear the word "RL", but they optimise different objects under different signals.

### 7.1 What is actually learned

| Aspect | World-model-based agent | RL-tuned LLM |
|---|---|---|
| **Learned object** | Transition function $p(s_{t+1}\mid s_t,a_t)$ + reward model $r(s_t,a_t)$ in a latent / symbolic state space | Only the policy $\pi(\text{token}\mid\text{context})$ — sometimes a reward model, but never an environment-dynamics model |
| **State** | Compressed latent (RSSM, JEPA embedding, occupancy grid, Gaussian splat, video latent) | Token history — no state distinct from the conversation prefix |
| **Action** | Continuous or discrete environment actions (joint torques, AV trajectories, game commands) | Discrete token emission |
| **Reward** | Environment-grounded (game score, task success, regression target, depth/keypoint loss) | Preference signal (human or AI) or rule-based verifier output |
| **Planning** | Explicit search / imagination (MCTS, CEM, latent rollouts, MPC, gradient descent through the WM) | Amortised into the forward pass — no separable lookahead unless added externally (CoT, ToT, RAP) |

### 7.2 What signals drive learning

- **World-model RL** loops perception → state → action → environment → next state → reward. The model sees every transition and can backpropagate through imagined rollouts (Dreamer family) or learn a value function whose gradient flows through the WM (TD-MPC2, PWM).
- **RL on LLMs** (RLHF, DPO, RLAIF) loops prompt → full response → scalar preference (Christiano '17; Ouyang '22; Rafailov '23; Bai '22). There is no transition between intermediate states, so credit assignment collapses to "this entire response was preferred / verified correct." RLVR / GRPO (DeepSeek-R1, Tülu 3) replaces the preference model with a rule-based correctness checker but keeps the same structure.

### 7.3 Conceptual contrasts

- **Counterfactual capability.** A WM by construction answers "what would happen if I took a different action in this state?" RL-tuned LLMs collapse counterfactuals to "regenerate with a different prefix" — the exact failure mode Vafa et al. (NeurIPS 2024) expose.
- **Data efficiency vs. coverage.** Dreamer-style WMs are sample-efficient because imagined rollouts amortise real interaction; RL-tuned LLMs are sample-hungry in human/feedback budget but ride on massive pretraining priors instead.
- **Grounding.** WMs are grounded in environment observations and rewards; RL-tuned LLMs are grounded in *human (or AI) preference labels / verifiers* and have no closed perception–action–prediction loop unless tools or environments are bolted on.
- **Composability.** WMs are object-like and reusable across tasks sharing dynamics; an RLHF'd policy is task-specific and degrades distributionally when goals change.
- **Failure modes.** WMs fail by model bias and compounding rollout error (covariate shift in imagination). RL-tuned LLMs fail by reward hacking, mode collapse, and sycophancy — pathologies of an under-specified preference signal.
- **What "improvement" looks like.** For WMs: longer accurate rollouts, better counterfactual fidelity, more controllable conditioning. For RL-tuned LLMs: higher win-rate on the reward / preference model, sometimes at the cost of diversity and calibration.
- **The bitter-lesson axis.** Both camps invoke Sutton's bitter lesson (scale wins). The WM camp scales *experience and dynamics modelling* (Silver & Sutton's "Era of Experience"); the RL-on-LLM camp scales *preferences and verifiable rewards on top of language pretraining*. They are not, in principle, mutually exclusive — but their data, infrastructure, and evaluation pipelines diverge sharply.

### 7.4 Where the two paradigms meet today

- **LLM-as-WM (§3.6).** RAP, WorldCoder, WALL-E, WKM, WorldLLM, Dynalang all interpolate between the two: the LLM is repurposed as a transition function or as a hypothesis generator over dynamics.
- **WM-augmented LLM agents.** LLM-Modulo (Kambhampati '24) bolts an external sound WM (PDDL, code, simulator) onto an LLM proposer. Reflexion, RAP, WorldCoder are softer variants in which the LLM iteratively corrects its own implicit WM.
- **Driving and embodied stacks** (OccLLaMA, HERMES, Doe-1, UP-VLA, 3D-VLA) already merge LLM backbones with explicit WMs as joint understand–predict–act models.

### 7.5 Hybrid pathway (executive summary)

The most likely 2026-and-beyond architecture is *not* "LLM or WM", but an **LLM proposing high-level actions / hypotheses, conditioned on (and supervised by) a latent or generative WM that grounds those proposals in environment dynamics**. RLHF/DPO/RLVR-style preference / verifier signals remain useful for style and instruction-following, but the planning, counterfactuals, and physical grounding come from the WM.

---

## 8. How to move from an LLM to a world model

This section is the practical complement of §7. It enumerates the technical levers — most already demonstrated in the surveyed papers — by which an LLM stack can be transformed into a world-model stack.

### 8.1 Augment the input and output

1. **Action-conditioned next-token / next-frame prediction.** Extend the input vocabulary with explicit action tokens; train on $(s_t^{\text{text/video}}, a_t, s_{t+1}^{\text{text/video}})$. Lowest-friction starting point — used by Pandora (text actions → video), Dynalang (text → DreamerV3 latent), Vid2World (causalised video diffusion), Genie 1/2/3 (latent-action discovery), WorldDreamer.
2. **Multimodal grounding.** Co-train on video, audio, depth and 3-D point cloud streams (LWM, Cosmos, V-JEPA 2, RoboScape, TesserAct, OccLLaMA). Physical regularities are only learnable from sensor streams that text simply does not contain.
3. **State annotations.** Where available, expose privileged state (occupancy grids, scene graphs, robot proprioception) during training — PIGDreamer-style asymmetric training, then deploy with only observations.

### 8.2 Reshape the objective

4. **JEPA-style predictive losses.** Replace cross-entropy / pixel-MSE with prediction in a *learned representation space* (V-JEPA 2, DINO-WM, JEPA-WMs, LeWorldModel). This drops the requirement to model irrelevant low-level noise.
5. **Reward / verifier signals from the environment.** Migrate from preference-only RL (RLHF/DPO) to grounded rewards from simulators, verifiers, and rule checkers (RLVR, DeepSeek-R1, Tülu 3). A prerequisite for *any* learning of dynamics rather than style.
6. **Counterfactual / cycle losses.** Add explicit counterfactual prediction terms (Vafa-style probes, action-permutation rollouts) so the model is rewarded for correct off-policy answers, not only on-policy continuation.

### 8.3 Add internal structure

7. **Latent dynamics on hidden states.** Fit a Dreamer-style RSSM / state-space model over the LLM's hidden activations or KV cache so that planning happens in a compact latent rather than over text (Dynalang demonstrates the principle; Dreamer 4 scales it to 1B+ params).
8. **External memory & 3-D consistency modules.** Plug in WorldMem-style memory or explicit 3-D spatial memory (Long-Term Spatial Memory, Genie 3) for multi-minute coherent rollouts.
9. **Hybrid AR + diffusion stacks.** AR over a high-level plan / latent, diffuse the fine-grained frame (Pandora, Epona, Genie Envisioner). Keeps planning tractable while exploiting the fidelity of diffusion.

### 8.4 Externalise the world model

10. **Code-as-WM.** Have the LLM emit a Python / PDDL / simulator program that is the WM (WorldCoder, GenSim, RoboGen). Gives editable, transferable, formally verifiable dynamics — and a natural integration point for LLM-Modulo-style verification.
11. **Neurosymbolic rule learning.** Extract symbolic rules, knowledge graphs, or scene graphs from rollouts and align them to the LLM's prior (WALL-E 2.0, DECKARD). Closes the prior-to-real-environment gap without weight updates.
12. **Hypothesis induction.** Let the LLM externalise natural-language hypotheses about dynamics and update them Bayesianly from interaction (WorldLLM). Interpretable, small, and low-variance compared with weight-level fine-tuning.

### 8.5 Close the loop with experience

13. **Replace static SFT corpora with interaction streams.** Sutton & Silver's "Era of Experience" prescription — on-policy data with non-stationary distributions. Required for any non-trivial WM behaviour to emerge from real-world deployment, not just text.
14. **Imagination-based policy improvement.** Once a WM exists, train the policy *inside* it (Dreamer family, DIAMOND, Dreamer 4). Imagined rollouts amortise expensive real-world interaction by orders of magnitude.
15. **Tooled inference at deployment.** Until the latent WM matures, bolt on an external WM at inference time (LLM-Modulo, Reflexion, RAP) — a pragmatic bridge that pays dividends now and degrades gracefully as the internal WM improves.

### 8.6 A staged migration plan

A concrete *recipe* for a team moving from an instruction-tuned LLM toward a world-model agent:

1. **Stage 0 — baseline.** SFT-then-DPO LLM; no environment, no actions, preference reward.
2. **Stage 1 — verifiable rewards.** Swap the preference reward for verifier / rule-based reward on a domain where ground truth is cheap (math, code, web nav). Adopt RLVR / GRPO-style on-policy RL. (Tülu 3, DeepSeek-R1.)
3. **Stage 2 — tool-grounded WM at inference.** Wrap the LLM in an LLM-Modulo loop with a sound external WM (simulator, PDDL, code). Use Reflexion / RAP for in-context credit assignment.
4. **Stage 3 — action-conditioned multimodal pre-training.** Continue-pretrain the model with $(s_t,\,a_t,\,s_{t+1})$ video / multimodal data (Pandora, Cosmos, Genie data style). Add JEPA-style latent-prediction objectives.
5. **Stage 4 — internal latent WM + imagination RL.** Fit a Dreamer-/JEPA-style WM over the model's hidden states; train the policy by latent imagination plus a small fraction of real environment interaction (Dreamer 4, V-JEPA 2-AC).
6. **Stage 5 — neurosymbolic alignment & continual experience.** Add learned symbolic rules (WALL-E) and an ever-growing experience buffer to maintain on-distribution dynamics over deployment lifetime.

Each stage is independently shippable, and each closes one of the gaps catalogued in §7.

---

## 9. In-depth summaries of seminal works

Below we provide journal-style summaries of nine works that anchor the field today.

### 9.1 DreamerV3 / Dreamer 4 (Hafner et al., Nature 2025 / arXiv 2509.24527)

DreamerV3 is the canonical configuration-free MBRL agent — a recurrent state-space WM with symlog and two-hot tricks that allows one fixed hyper-parameter set to master 150+ tasks including Minecraft-diamond-from-scratch. Dreamer 4 (Hafner & Yan, 2025) replaces the RSSM with a *block-causal* transformer and introduces **shortcut forcing**, a teacher-forcing variant tuned for long-horizon coherence. Crucially Dreamer 4 trains predominantly on *unlabelled* video, recovering both the dynamics and a small set of latent actions; the resulting WM runs interactively in Minecraft at video frame rates. The line from DreamerV3 to Dreamer 4 is the clearest single arc of the WM-RL community: from a carefully engineered RSSM to a Sora-scale generative transformer trained on internet video — a near-perfect mirror of the LLM scaling curve, but with actions and rewards in the loop.

### 9.2 V-JEPA 2 (Assran, Bardes, LeCun et al., arXiv 2506.09985)

V-JEPA 2 instantiates LeCun's 2022 "Path Towards Autonomous Machine Intelligence" at scale: a self-supervised JEPA encoder trained on **1 M+ hours** of internet video, plus an action-conditioned post-training stage (V-JEPA 2-AC). It demonstrates zero-shot Franka pick-and-place from image goals by *planning in the learned latent space* — no pixel decoding required. Compared with diffusion / AR pixel-space WMs, V-JEPA 2's predictions are several orders of magnitude cheaper, and the JEPA-WMs ablation (Terver et al., ICLR 2026) shows that the design space for non-generative WMs is still underexplored. V-JEPA 2 is the strongest empirical refutation of the "to model the world, you must generate pixels" assumption.

### 9.3 DIAMOND (Alonso, Jelley et al., NeurIPS 2024 Spotlight)

DIAMOND showed that diffusion is a competitive WM backbone for RL: an RL agent trained inside a pixel-space diffusion WM achieved a record 1.46 mean human-normalised score on Atari-100k. The deeper contribution is conceptual — visual *details* (tile boundaries, small enemies) matter for credit assignment, and discrete-token VQ-style WMs (IRIS) systematically discard them. DIAMOND was the bridge between RL world-modelling and the generative video community, foreshadowing GameNGen, Cosmos, Vista, and Dreamer 4.

### 9.4 Cosmos (NVIDIA, arXiv 2501.03575)

Cosmos is the most ambitious open-weight WM platform to date — a suite of diffusion (Cosmos-Predict) and AR (Cosmos-Reason) world-foundation models trained on **20 M hours** of physical-world video, plus Cosmos-Transfer for video-to-video translation. It explicitly positions WMs as **synthetic data engines for physical AI** (autonomous vehicles, humanoid robots, industrial automation). The platform's open release accelerated the academic community's transition from one-off WMs to ecosystem-style WMs with shared tokenisers, decoders, and evaluation suites.

### 9.5 Genie 2 / Genie 3 (DeepMind, 2024 / Aug 2025)

Genie 2 made the case that a foundation WM can generate consistent **playable** 3-D worlds from a single image; Genie 3 (Aug 2025) extends this to real-time 24 fps / 720p text-to-world simulation with multi-minute coherence and emergent "world memory." Genie 3 is the closest current example of a text-grounded, interactive, foundation WM; it is also the most rigorous existence proof of Sutton & Silver's *Era of Experience* — the model can be *played in*, generating on-policy interaction data at scale. The Genie line is the WM analogue of GPT-4: the public, headline-grabbing benchmark that the rest of the field calibrates against.

### 9.6 GAIA-2 / Vista / ReSim (driving WMs)

GAIA-2 (Wayve, CVPR 2025 WS) standardised the **multi-camera latent-diffusion** recipe for driving WMs, with structured controls over ego dynamics, agent configurations, environment and road semantics. Vista (NeurIPS 2024) added high-resolution long-horizon generation with reward-style evaluation. ReSim (NeurIPS 2025 Spotlight) added **co-training on hazardous and non-expert data**, with a Video2Reward module that turns rollouts into RL signals. Collectively these three trace the maturation of driving WMs from "video generators" to **closed-loop simulators with grounded rewards**, an arc that the rest of the field is now following.

### 9.7 RAP — Reasoning with Language Model is Planning with World Model (Hao et al., EMNLP 2023)

RAP is the canonical "LLM-as-WM" paper. A single LLM is repurposed as both the policy and the world model: states are natural-language descriptions; the LLM produces transitions and a reward heuristic; MCTS searches over imagined state-action trajectories. RAP turns the LLM's forward pass from a one-shot answer into a *planning module*, and gives LLaMA-33B+RAP a ~33 % relative gain over GPT-4+CoT on plan generation. The paper inaugurated the line that includes WorldCoder, WALL-E, WKM, and WorldLLM, and is the central case for the hybrid LLM × WM future sketched in §7.5.

### 9.8 WALL-E 2.0 — World Alignment by Rule Learning (Zhou et al., 2024-2025)

WALL-E and its 2.0 follow-up treat the LLM as a *near*-world-model whose gap to the real environment is closed by **learned symbolic rules / knowledge graphs / scene graphs**. The aligned neurosymbolic WM is then used in MPC-style look-ahead. The system reaches 98 % success on ALFWorld and posts large gains on a Minecraft-like Mars benchmark **without any RL fine-tuning** of the LLM. WALL-E is the clearest demonstration that the *delta* between an LLM's prior and a sound WM can often be expressed in a few hundred symbolic rules — a strong argument for code/neurosymbolic alignment as a near-term bridge from LLMs to WMs.

### 9.9 Vafa et al. — Evaluating the World Model Implicit in a Generative Model (NeurIPS 2024)

Vafa et al. formalise the question "does this generative model contain a world model?" using Myhill-Nerode-inspired probes (next-token test, sequence distinction, detour test) on DFA-based tasks (Othello, logic puzzles, NYC taxi routing). The result is sobering: many models that ace next-token prediction fail counterfactual and detour tests. The paper undermines the casual inference "good predictor ⇒ good WM" and provides the methodological backbone for WorldModelBench (NeurIPS 2025), EWMBench, LikePhys (ICLR 2026), and "When do NNs learn world models?" (ICLR 2025 Oral) — the new evaluation infrastructure that the field has begun to build.

---

## 10. Open challenges and outlook

1. **Long-horizon coherence beyond a minute.** Even Genie 3 and Dreamer 4 degrade past a few minutes; explicit 3-D / scene-graph memory (WorldMem, Long-Term Spatial Memory) is a first answer but not a complete one.
2. **Counterfactual fidelity.** Vafa et al.'s probes remain mostly unaddressed — no current generative WM passes detour tests robustly.
3. **Physics correctness without privileged supervision.** RoboScape and TesserAct help, but physical-plausibility metrics are still in their infancy (LikePhys, WorldModelBench).
4. **Action discovery from unlabelled video.** Genie's latent actions and Dreamer 4's shortcut forcing are early answers; reliable, *interpretable* action spaces from video remain open.
5. **Bridging LLM and WM stacks at scale.** OccLLaMA, HERMES, Doe-1, UP-VLA show the convergence direction, but no model yet jointly matches LLM-grade language reasoning with Dreamer-grade closed-loop control.
6. **Evaluation of WM-as-simulator for downstream policy.** EWMBench (Genie Envisioner) and ACT-Bench begin this, but a *DriveBench-/MMLU-scale* harness for WM-imagined-data policy learning is still missing.
7. **Sample-efficient continual experience.** Continual-RL-WMs and DRAGO show the principled route, but no deployed system yet learns lifelong from streams of interaction — the Era-of-Experience promise remains a research programme.

---

## 11. References (compact)

Foundational positions: Sutton (Bitter Lesson, 2019); LeCun (Path, 2022); Silver & Sutton (Era of Experience, 2025).

Dreamer / MBRL: Hafner et al. — DreamerV1 (ICLR 2020), DreamerV3 (Nature 2025), Dreamer 4 (2509.24527); Alonso et al. — DIAMOND (2405.12399); Hansen et al. — TD-MPC2 (2310.16828), Puppeteer (2405.18418); Samsami et al. — R2I (2403.04253); Li et al. — LS-Imagine (2410.03618); Dedieu et al. — Improving Transformer WMs (2502.01591); Liu et al. — Continual-RL-WMs (2507.09177).

JEPA / latent WMs: V-JEPA 2 (2506.09985); DINO-WM (2411.04983); JEPA-WMs (2512.24497); Seq-JEPA (2502.09858); LeWorldModel (le-wm.github.io).

Generative / game WMs: Sora (OpenAI report 2024); Genie 1 (2402.15391); Genie 2 / 3 (DeepMind blogs 2024 / 2025); GameNGen (2408.14837); Cosmos (2501.03575); Pandora (2406.09455); WorldDreamer (2401.09985); LWM (2402.08268); Vid2World (2505.14357); AVID (2410.12822).

Driving: Drive-WM (2311.17918); DriveWorld (2405.04390); GenAD (2403.09630); DriveDreamer (2309.09777); OccWorld (2311.16038); Copilot4D (2311.01017); Vista (2405.17398); DrivingDojo (2410.18603); DriveDreamer-2 (2403.06845); Drive-OccWorld (2408.14197); OccLLaMA (2409.03272); Doe-1 (2412.09627); DriveDreamer4D (2410.13571); DrivingSphere (2411.11252); UniScene (2412.05435); GaussianWorld (2412.10373); GEM (2412.11198); MaskGWM (2502.11663); GAIA-2 (2503.20523); HERMES (2501.14729); Epona (2506.24113); InfiniCube (2412.03934); World4Drive (2507.00603); ReSim (2506.09981).

Embodied / robot: iVideoGPT (2405.15223); GenRL (2406.18043); Sirius-Fleet (2410.22689); DWL (2408.14472); IRASim (2406.14540); TesserAct (2504.20995); NWM (2412.03572); RoboScape (2506.23135); Ctrl-World (2510.10125); FLARE (2505.15659); DreamGen (2505.12705); WoMAP (2506.01600); Genie Envisioner (2508.05635); 3D-VLA (2403.09631); UP-VLA (2501.18867); EVA (2410.15461); Robotic World Model (2501.10100); MeWM (2506.18254).

LLM-as-WM: RAP (2305.14992); Language Models Meet World Models (2305.10626); Dynalang (2308.01399); DECKARD (2301.12050); Voyager (2305.16291); Can-LMs-Simulate (2406.06485); Vafa et al. (2406.03689); WKM (2405.14205); WorldCoder (2402.12275); WorldGPT (2404.18202); GenSim (2310.01361); RoboGen (2311.01455); WALL-E 2.0 (2410.07484, 2504.15785); WorldLLM (2506.06725); Reasoning-or-Reciting (2307.02477); LLM-Modulo (2402.01817).

RL on LLMs (for §7 comparison): RLHF (1706.03741); InstructGPT (2203.02155); DPO (2305.18290); Constitutional AI / RLAIF (2212.08073); Tülu 3 / RLVR (2411.15124); DeepSeek-R1 (2501.12948); RLVR-implicit (2506.14245).

---

*Survey compiled May 2026. Last paper accepted: ICLR 2026.*
