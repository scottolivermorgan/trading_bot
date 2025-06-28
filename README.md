# trading_bot
automated trading algo

# Current repo structure idea:
Note require browser automation as platform dosent have API, live trading uses this:
Use a command queue or simple API so that:
- strategy outputs decisions
- browser automation consumes those decisions

trading-bot/
├── browser_automation/           
│   ├── playwright_executor.py    # Code to interact with the broker site
│   ├── selectors.yaml            # UI element selectors
│   └── state/                    # Saved sessions (user data dir)
├── api/                          # FastAPI backend
│   ├── main.py                   # Entry point for FastAPI app
│   ├── routers/                  # Route definitions (e.g. /trades, /strategies)
│   ├── services/                 # Business logic layer
│   ├── models/                   # Pydantic models (request/response)
│   └── dependencies.py           # FastAPI dependencies (DB session, etc.)
│
├── trading/                      # Core trading engine logic
│   ├── strategies/               # Strategy implementations
│   ├── signals/                  # Signal generation logic
│   ├── execution/                # Trade execution logic
│   ├── backtesting/              # Backtesting framework
│   └── utils/                    # Helper functions/utilities
│
├── airflow/                      # Airflow orchestrator setup
│   ├── dags/                     # DAG definitions
│   ├── plugins/                  # Custom operators, hooks, sensors
│   └── config/                   # Airflow configs (env vars, connections)
│
├── db/                           # Database schema and migration handling
│   ├── alembic/                  # Alembic migrations folder
│   ├── init.sql                  # Initial schema creation (optional)
│   └── utils.py                  # DB helper functions
│
├── streamlit_dashboard/          # Streamlit-based frontend
│   ├── app.py                    # Streamlit app entry
│   └── pages/                    # Additional Streamlit pages
|
├──  ml-api/
|    ├── app.py          # FastAPI app
|    ├── model.pkl       # Trained model
|    └── predict.py      # Feature engineering + prediction
|
├── mlflow/
|    ├── Dockerfile
│    |── mlruns/                # Local experiment tracking
│    |── scripts/
│         ├── train_model.py     # ML pipeline
│         └── register_model.py  # Save & register in MLflow
│
├── config/                       # Centralized configuration system
│   ├── __init__.py
│   ├── api.py                    # API-specific config
│   ├── airflow.py                # Airflow/DAG-specific config
│   └── settings.yaml             # Optional config file
│
├── scripts/                      # Utility scripts for setup or data ingestion
│   ├── init_db.py                # Bootstraps DB with initial data
│   └── load_data.py              # Historical data ingestion
│
├── infrastructure/              # Infrastructure as code
│   ├── terraform/                # Terraform IaC for cloud deployment
│   └── ansible/                  # Ansible playbooks for provisioning
│
├── tests/                        # Automated tests
│   ├── api/                      # FastAPI endpoint tests
│   ├── trading/                  # Strategy and trading logic tests
│   └── airflow/                  # DAG tests
│
├── .env                          # Environment variables (excluded from version control)
├── .gitignore                    # Ignore files for Git
├── docker-compose.yml           # Orchestrate services for local dev
├── Dockerfile.api               # For FastAPI
├── Dockerfile.airflow           # For Airflow (if not using the official image directly)
├── Dockerfile.streamlit         # For Streamlit dashboard
├── Makefile                     # Common developer commands (e.g. make test)
└── README.md                    # Project documentation


# Goal Benchmarks
1) postgres docker container, backend python API container (fasthosts?), airflow orchestration container.
Goal: update price data in postgres with airflow orchestrating the api call - one asset "SQQQ".

2) streamlit container - displays plot of asset, can switch on/off some simple technical indicators - SMA's & EMA's.
displays some sample statistical research, mayby over 2 pages +.

3) 

4) A simple scaffold of a random forest for price prediction
