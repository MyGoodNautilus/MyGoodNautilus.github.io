# Benjamin Ecker

My portfolio, currently a work in progress. But even progress is a work in progress, so that doesn't matter.

## Who I Am

I'm Benjamin Ecker. I build small things from scratch and watch how they behave, which mostly means watching them fail until, sometimes, they stop. Sample size: one. Draw your own conclusions.

My interest is efficiency, specifically, making things cheaper. Coming from someone who is also cheap, that tracks.

## Koi

**Repository:** [github.com/MyGoodNautilus/koi](https://github.com/MyGoodNautilus/koi) ... MIT license ... replication attempts welcome (please)

Koi is a small hybrid language model, built from scratch. Named after the fish, it moves through a lot of water efficiently without carrying much of it along.

The architecture alternates two approaches by layer. Odd layers are Gated DeltaNet: linear attention with a fixed-size recurrent state, updating and forgetting on purpose. Even layers are local dense attention: causal softmax over a sliding window with RoPE, for short-range precision. The result handles a long context window(roughly 20 thousand words) without a KV cache that grows with it, memory stays roughly flat as the sequence gets longer, which is not the usual arrangement.

Rough numbers from an early training run:

| Metric | Value | Note |
|---|---|---|
| Parameters | ~126M | Matching gpt-2-small |
| Loss | ~2.5 | Still trending down |
| Perplexity | ~12 | Above the theoretical floor, as expected |
| Throughput | ~100 tok/s (FP32) | On a laptop GPU, roughly constant memory use |
| Vocab | ~50k | Borrowed from SmolLM2's tokenizer |

Take these as directional, not final. Early runs, one setup, no scaling study yet.

The general idea: pure softmax attention gets expensive as sequences grow; pure recurrence is efficient but loses precision on exact recall. Splitting the difference is a known idea in the literature, and it seems to hold up here too. Training runs in parallel chunks; inference runs the recurrence step-by-step at constant cost per token. For rough context, something like GPT-2-small runs meaningfully slower on comparable hardware and its memory use climbs as the input grows, Koi's doesn't, by design.

Base model inference? You get sentences that pretend to be grammatically fine and I'm overoptimistic. This is an improvement. Earlier versions were only half of that.

Future work: more training, better throughput, an actual scaling analysis, pending time, funding, and a break, roughly in that order. The repo has the full implementation, data pipeline, and the delta rule spelled out plainly, matmul and all. If something breaks, that's useful information. Open an issue.

## Correspondence

GitHub issues are the best way to reach me. Email works too: `benjaminsnautilus@gmail.com`. Other channels may exist eventually.

***
<s>
Don't listen to the text below, this page is not open source.
</s>
