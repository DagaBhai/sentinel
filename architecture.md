sentinel/
├── README.md
├── requirements.txt
├── pyproject.toml
├── .gitignore
├── .env.example
├── Makefile
│
├── config/
│   ├── default.yaml          # paths, seeds, model name
│   ├── thresholds.yaml       # router gates, conformal alpha
│   └── llm.yaml              # providers, timeouts, prices
│
├── data/
│   ├── raw/
│   ├── processed/
│   └── splits/               # train, val, calib, test
│
├── scripts/
│   ├── generate_dataset.py   # replace dataset/script.py
│   ├── prepare_splits.py
│   ├── train.py
│   ├── calibrate.py
│   ├── tune_router.py
│   ├── run_eval.py
│   └── load_test.py
│
├── src/
│   └── sentinel/
│       ├── __init__.py
│       ├── schema.py                 # Ticket, Prediction, Decision
│       ├── config.py                 # load yaml
│       │
│       ├── data/
│       │   ├── dataset.py            # torch Dataset
│       │   ├── tokenizer.py
│       │   └── splits.py
│       │
│       ├── models/
│       │   ├── encoder.py            # DeBERTa backbone
│       │   ├── heads.py              # 5 task heads
│       │   ├── multitask.py          # encoder + heads
│       │   ├── losses.py
│       │   └── trainer.py
│       │
│       ├── calibration/
│       │   ├── temperature.py
│       │   ├── conformal.py          # 95% coverage
│       │   └── metrics.py            # ECE, coverage
│       │
│       ├── routing/
│       │   ├── router.py             # auto / LLM / human
│       │   └── policy.py             # gate rules
│       │
│       ├── agents/
│       │   ├── base.py
│       │   ├── auto_resolver.py
│       │   ├── llm_agent.py
│       │   └── human_queue.py
│       │
│       ├── llm/
│       │   ├── base.py               # one interface
│       │   ├── openai_provider.py
│       │   ├── llama_provider.py
│       │   ├── cache.py
│       │   └── cost.py               # token and price tracking
│       │
│       ├── pipeline.py               # classify, calibrate, route, resolve
│       │
│       ├── serving/
│       │   ├── api.py                # FastAPI
│       │   ├── queue.py              # async ingestion
│       │   └── inference.py          # batching, ONNX optional
│       │
│       ├── observability/
│       │   ├── metrics.py            # latency, cost, confidence, escalation
│       │   └── logging.py
│       │
│       └── eval/
│           ├── classifier_eval.py    # F1 per task
│           ├── baseline_llm_only.py
│           ├── hybrid_eval.py
│           └── report.py
│
├── tests/
│   ├── unit/
│   │   ├── test_conformal.py
│   │   ├── test_router.py
│   │   ├── test_schema.py
│   │   └── test_llm_providers.py
│   └── integration/
│       └── test_pipeline.py
│
├── artifacts/
│   ├── checkpoints/
│   ├── calibration/          # temperature, conformal quantiles
│   └── reports/
│
├── benchmarks/
│   └── locustfile.py
│
├── notebooks/
│   └── eda.ipynb
│
└── docs/
    ├── architecture.md
    ├── decisions.md
    └── results.md