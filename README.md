<img width="3840" height="1280" alt="1920x640-discord" src="https://github.com/user-attachments/assets/90607b26-171f-476a-90ae-69b9dbb7cb30" />

<br>
<br>

**OpenAI Model Craft Challenge: Parameter Golf** is a challenge to train the best language model that fits in a 16MB artifact and trains in under 10 minutes on 8xH100s, evaluated by compression on the FineWeb validation set (tokenizer-agnostic, bits per byte).

This challenge is heavily inspired by the [NanoGPT Speedrunning](https://github.com/KellerJordan/modded-nanogpt) challenge, where participants compete to train a model that reaches 3.28 FineWeb validation loss as quickly as possible. We're excited to see how optimizing for a parameter-constrained setting pushes people toward unique architectures (test-time compute, aggressive parameter tying, depth recurrence, low-rank training, ...), compression schemes (low precision, QAT, bitnets, novel tokenizers, ...), and other creative submissions (test-time training, long context, megakernels ...). 

If you're familiar with [neural scaling laws](https://arxiv.org/abs/2001.08361), you can consider this challenge a form of L(N) optimization, where the objective is to optimize the lowest loss given a fixed number of parameters (N) unconstrained by data, compute, steps, or architecture. Challenges like the [NanoGPT Speedrun](https://github.com/KellerJordan/modded-nanogpt), which optimizes for a form of L(T) (~lowest time given constrained loss) or the [NanoGPT Slowrun](https://github.com/qlabs-eng/slowrun), which optimizes for L(D) (lowest loss given constrained dataset size), can be thought of as equivalent challenges in this family.

Ideally, we'd allow for submissions to use arbitrary computational resources. But in order to make the challenge not inaccessibly expensive, we're limiting *leaderboard submissions* to 10 minutes on 8xH100s. However, we'd still love to see submissions that don't meet the compute limitation requirements in our 'Non-record Submissions' section: We're excited to see people push the infinite frontier of parameter limited performance as well.

We also know compute is expensive, so **OpenAI is sponsoring $1,000,000 in compute credits** to help people get started training their models. To request a compute grant, use this form: [Request a Compute Grant](https://openai.com/index/parameter-golf/#credit-form).
When requesting compute, please make sure you choose the appropriate level, write sufficient justification, and **submit with an email tied to a OpenAI / ChatGPT account**.

## Participant Form

If you enjoy solving very difficult technical problems, please introduce yourself via the [Challenge Participant Form](https://jobs.ashbyhq.com/openai/form/open-ai-challenge-parameter-golf). It helps us attribute challenge submissions and reach out about opportunities with OpenAI. _Completing the form is not required to participate._

Many researchers at OpenAI first distinguished themselves through elite mathematics and programming competitions. The Model Craft Challenge is designed in that spirit: testing the ability to tackle unfamiliar problems with creativity and rigor, qualities we believe are essential for frontier AI research.

In June, we plan to hire a small cohort of early-career researchers, targeting current undergraduate students and recent graduates, including Olympiad medalists and elite competitors. For exceptional participants, the challenge may also serve as a way to stand out to OpenAI researchers and recruiters.

The challenge runs from March 18th to April 30th. 

Happy training!

## Leaderboard

| Run | Score | Author | Summary | Date | Info |
|-----|------:|--------|---------|------|------|
| BOS-Fixed SmearGate + LQER + SparseAttnGate + 9-Hparam Stack | 1.0611 | codemath3000 | On PR #1855: BOS-fixed #1797-derived stack with LQER, PR #1787 SparseAttnGate/PolarNS/FusedCE base, per-group lrzip compression, and 9 greedy hyperparameter overrides; submitted 3-seed mean 1.06108 with broader reproduction support (p=0.188 vs PR #1868 latest rerun) | 2026-04-27 | [info](https://github.com/openai/parameter-golf/pull/1855), [repro](https://github.com/openai/parameter-golf/pull/1855#issuecomment-4336629746) |
| BOS-Fixed SmearGate + LQER Asymmetric + PR1787 SparseAttn + Phased TTT | 1.0614 | aquariouseworkman | On PR #1851 with 3-seed compliance-rerun support from PR #1868: BOS-boundary fix from PR #1851 applied to dexhunter's PR #1797 SmearGate + LQER stack, using the PR #1787 SparseAttnGate/PolarNS/FusedCE base plus CaseOps and phased score-first TTT | 2026-04-27 | [info](https://github.com/openai/parameter-golf/pull/1851), [3-seed](https://github.com/openai/parameter-golf/pull/1868) |
| PR1736 + PolarNS + MIN_LR + SparseAttnGate + FusedCE + Warm-A TTT | 1.0634 | nprime06 | On PR #1787: PR #1736 CaseOps stack plus Polar Express Newton-Schulz coefficients, MIN_LR=0.1, SparseAttnGate, fused softcapped CE, and PR #1767-style warm-start-A TTT | 2026-04-23 | [info](https://github.com/openai/parameter-golf/pull/1787) |
| CaseOps + MLPClip12 + SmearGate/LoRA-TTT | 1.0645 | dexhunter | On PR #1769: CaseOps stack with SmearGate/LoRA-TTT refinements and MLPClip12; 5-seed mean improves the accepted CaseOps frontier (p=0.063 vs #1736) | 2026-04-22 | [info](https://github.com/openai/parameter-golf/pull/1769) |
| SP8192 + CaseOps + GatedAttn + QuantGate + Loop45 + Phased TTT | 1.0655 | dexhunter | On PR #1736: adopts romeerp's lossless CaseOps transform from PR #1729 with byte-sidecar BPB accounting, then adds gated attention and quant-gate scaling on the PR #1530 SP8192 phased-TTT stack | 2026-04-19 | [info](https://github.com/openai/parameter-golf/pull/1736) |
| CaseOps Tokenizer + Tapered WD + Phased TTT | 1.0678 | romeerp | On PR #1729: lossless CaseOps bijective case transform with validation byte sidecars, plus mild late Muon weight-decay taper on the PR #1626 legal phased-TTT stack | 2026-04-19 | [info](https://github.com/openai/parameter-golf/pull/1729) |
| SmearGate + Attention Output Gate + Legal TTT | 1.0714 | MarioPaerle | On PR #1667: SmearGate, attention output gate, depth recurrence, parallel residuals, QK-Gain 5.25, quantization, and score-first TTT | 2026-04-16 | [info](https://github.com/openai/parameter-golf/pull/1667) |
| VarLen Attention + Fused MLP + Multi-Phase Global SGD TTT | 1.0719 | dexhunter | On PR #1626: VarLen attention, fused MLP, multi-phase global SGD TTT, trimmed GPTQ, MLR 0.026, int7 embeddings, and adaptive clip | 2026-04-14 | [info](https://github.com/openai/parameter-golf/pull/1626) |
| VarLenAttn + PhasingTTT | 1.0728 | romeerp | On PR #1610: #1530-style VarLen/fused stack plus phased TTT over already-scored validation chunks | 2026-04-13 | [info](https://github.com/openai/parameter-golf/pull/1610) |
| VarLen Attention + Fused MLP + Doc-Independent Legal TTT | 1.0734 | samacqua | On PR #1530: variable-length FA3 attention, fused Triton MLP, grouped small-parameter all-reduces, and doc-independent score-first LoRA TTT | 2026-04-11 | [info](https://github.com/openai/parameter-golf/pull/1530) |
| Improved Parallel Residuals + CUTLASS EVT + Legal TTT | 1.0758 | msisovic | On PR #1529: PR #1523 SP8192 baseline with fuller two-lane parallel residual routing, PARALLEL_RESIDUAL_START=8, inline CUTLASS EVT/Triton fused kernels, and legal score-first TTT; corrected 3-seed mean after GPTQ reserve/seed fix (p=0.001 vs #1514) | 2026-04-11 | [info](https://github.com/openai/parameter-golf/pull/1529) |
| SP8192 + Muon 0.97 + Legal Score-First TTT | 1.0798 | dexhunter | On PR #1514: SP8192 with Muon 0.97 and legal score-first TTT; 3-seed sweep beats #1493 (p=0.020) | 2026-04-09 | [info](https://github.com/openai/parameter-golf/pull/1514) |
| SP8192 + 3-Layer Recurrence + Parallel Residuals + Legal TTT | 1.0810 | bigbag | On PR #1493: 3-layer recurrence, parallel residuals, QK-Gain 5.25, and legal score-first TTT on the PR #1394 stack | 2026-04-09 | [info](records/track_10min_16mb/2026-04-09_SP8192_3LayerRecur_ParResid_QK525_LegalTTT/README.md) |
| SP8192 + Parallel Residuals + Score-First TTT | 1.0822 | aryanbhosale | On PR #1477: parallel residuals on the PR #1413 SP8192 + legal score-first TTT stack | 2026-04-08 | [info](records/track_10min_16mb/2026-04-08_SP8192_ParallelResid_ScoreFirstTTT/README.md) |
| SP8192 + QK-Gain 5 + Legal Score-First TTT | 1.0828 | dexhunter | On PR #1413: QK-Gain 5.0 + legal score-first TTT on the PR #1394 SP8192 stack | 2026-04-06 | [info](records/track_10min_16mb/2026-04-06_SP8192_QK5_LegalTTT_1.0828/README.md) |

## Support

Join the [OpenAI Discord server](https://discord.com/invite/openai) and visit the Parameter Golf channels (#parameter-golf-discussions, #parameter-golf-announcements) and ask questions.

This repository adapts code from `modded-nanogpt`, see [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md) for attribution.
