![ALL IN INFERENCE. An illustrative trace from chunked prefill to a stream of output tokens.](./inference-banner.svg)

# XiaoxianMa · All in on inference

I’m working on LLM serving from the scheduler down. I like taking a weird number in a trace, finding where it comes from, and turning it into a test that fails for the right reason.

## In the works

**[SGLang #52893 · Fix waiting-token accounting in chunked prefill](https://github.com/sgl-project/sglang/pull/52893)**

My first SGLang PR. The published waiting count included a prefill chunk that was already scheduled. In the example, the router saw **12,288 tokens waiting instead of 8,192**. The fix changes the waiting count and leaves total load and batch scheduling alone.

## What I’m digging into

- **Scheduling:** how chunked prefill, batching, and routing affect time to first token.
- **KV cache:** when reuse pays off and what happens under memory pressure.
- **Profiling:** where the time goes between tokens, and what changes at the tail.

`Trace the workload → isolate the bottleneck → change one thing → verify.`
