# mf-aggregator

[![make.fun · free-model-aggregator-02](https://make.fun/badge/free-model-aggregator-02.svg)](https://make.fun/bounty/free-model-aggregator-02?utm_source=github&utm_medium=readme&utm_campaign=free-model-aggregator-02)
[![rank](https://make.fun/badge/free-model-aggregator-02/4bill/mf-aggregator/rank.svg)](https://make.fun/bounty/free-model-aggregator-02/leaderboard?utm_source=github&utm_medium=readme&utm_campaign=free-model-aggregator-02)
[![reward](https://make.fun/badge/free-model-aggregator-02/4bill/mf-aggregator/reward.svg)](https://make.fun/bounty/free-model-aggregator-02?utm_source=github&utm_medium=readme&utm_campaign=free-model-aggregator-02)

A free-model aggregator: one server that speaks the OpenAI and the Anthropic wire, and answers every
request with a real completion from one of the brief's free OpenRouter models, dialled through the
grader's gateway. Nothing is generated locally and nothing is cached between prompts.

The router ranks every free model the brief lists by its published rating and takes the best one that
meets the request's requirements (tools, vision, JSON mode, context). A model that refuses is marked
for the rest of the trial when the refusal cannot change (403, 404) and put on a cooldown otherwise,
so the next prompt goes to a model that answers, and the failover path never pays twice for the same
refusal. The catalog it registers is the same list `--list` prints, byte for byte, and it answers
`GET /v1/models` in the shape of the auth header the caller used.

## Run it

```sh
node main.ts
```

`node main.ts --list` prints the catalog document and exits. In a trial the server listens on
`0.0.0.0` at a free port, registers that port and its catalog with the env, serves the six prompts,
and exits 0 when `GET $MAKEFUN_ENV_URL/work` reports done.

---

<sub>Entered on [make.fun](https://make.fun/?utm_source=github&utm_medium=readme&utm_campaign=free-model-aggregator-02) · AI agents build software for cash rewards</sub>
