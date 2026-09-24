# MILES: Modular Instruction Memory with Learnable Selection for Self-Improving LLM Reasoning
[Ruilin Tong](https://github.com/RuilinTong), [Dong Gong](https://donggong1.github.io/)<sup>*</sup>

[Artificer AI Lab](https://donggong1.github.io/group/), [University of New South Wales (UNSW Sydney)](https://www.unsw.edu.au/)

<sup>*</sup>Corresponding author

[![Project Page](https://img.shields.io/badge/Project-Page-a22799)](https://artificer-ai-lab.github.io/MILES/)
[![arXiv](https://img.shields.io/badge/arXiv-2607.06974-b31b1b)](https://arxiv.org/abs/2607.06974)
[![PDF](https://img.shields.io/badge/PDF-arXiv-555555)](https://arxiv.org/pdf/2607.06974)

**TL;DR:** MILES lets a frozen LLM improve itself at test time from its own reasoning trajectories, without ground-truth labels. From problems it answers confidently, it extracts sub-goals and the sub-skills (sub-instructions) that achieve them into a modular memory, and it learns online when to read each memory unit, so that later, uncertain problems are solved by composing these sub-skills step by step.

**Project page:** https://artificer-ai-lab.github.io/MILES/

## TODO
- [ ] Release the code of MILES (coming soon).

## Overview
![Overview of MILES](assets/teaser.png)

MILES improves test-time reasoning by constructing memory and learning memory selection from confident samples, then applying the learned memory to guide reasoning on uncertain samples.

## Abstract
Large language models (LLMs) increasingly improve their reasoning at test time via additional computation, yet most existing works treat each problem in isolation. When problems arrive sequentially, accumulating reusable experience across them can further improve performance. Existing memory-based methods either store whole-solution templates that generalize poorly to novel problems or use heuristic step-level selection that is not optimized for final-answer correctness. Learning selection policies requires large-scale training data and fixed action spaces, making such approaches unsuitable for test-time settings where memory expands incrementally and only limited supervision is available.

We propose **MILES** (**M**odular **I**nstruction Memory with **LE**arnable **S**election for self-improving LLM reasoning), a framework that dynamically expands step-wise memory and applies correctness-optimized memory composition under realistic test-time constraints. MILES maintains modular memory units consisting of asymmetric pairs of sub-goal embeddings and sub-instructions, each associated with a learnable selection head. This memory structure enables a coarse-to-fine retrieval mechanism: The coarse level enables memory expansion and collects supervision for training selection heads from confident samples, while the fine stage applies learned selection heads to rerank coarse-level candidates and guide reasoning for uncertain samples.

MILES consistently matches or outperforms prior methods while achieving superior accuracy–efficiency tradeoffs. Extensive experiments demonstrate its effectiveness, robustness, and transferability.

## Method
![Technical overview of MILES](https://artificer-ai-lab.github.io/MILES/assets/miles_method.svg)

Answer agreement routes each question. On the WRITE path, confident questions grow the memory and train per-unit selection heads from pseudo-labeled MCTS rollouts. On the READ path, uncertain questions compose sub-instructions through coarse-to-fine retrieval inside a memory-guided tree search. The bottom strip shows the selection objective and the per-unit BCE surrogate used to train the heads. An animated walkthrough is on the [project page](https://artificer-ai-lab.github.io/MILES/).

## Citation
```bibtex
@misc{tong2026milesmodularinstructionmemory,
  title={MILES: Modular Instruction Memory with Learnable Selection for Self-Improving LLM Reasoning},
  author={Ruilin Tong and Dong Gong},
  year={2026},
  eprint={2607.06974},
  archivePrefix={arXiv},
  primaryClass={cs.CL},
  url={https://arxiv.org/abs/2607.06974},
}
```
