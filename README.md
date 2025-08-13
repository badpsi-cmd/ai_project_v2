# Absolute Trade AI

This project is a personal decision-support tool for the Indian financial market that identifies and explains high-confidence "absolute trades." The system is designed to evolve from a manual prototype into a robust, research-driven, self-healing, and self-evolving financial prediction engine.

The primary goal is not trade frequency, but extreme precision and confidence for a small number of trades.

## Project Structure

- `docs/`: Contains the Product Requirements Document (PRD), session scripts, and other documentation.
- `erd/`: Contains the database schema (`schema.sql`) and the Mermaid diagram (`model.mmd`).
- `common/`: Shared Python utility modules (e.g., database connection).
- `scripts/`: Standalone scripts for one-off tasks like database setup and data migration.
- `training/`: Scripts and modules related to model training and feature engineering.
- `services/`: Long-running services, including the prediction service and the API.
- `artifacts/`: Directory for storing saved model files (ignored by Git).

## Quickstart

This project uses a `Makefile` to simplify common tasks.

**System Prerequisites (macOS):**
-   Homebrew
-   The XGBoost library requires the OpenMP runtime. Install it with:
    ```bash
    brew install libomp
    ```
1.  **Install Dependencies:**
    This will install all required Python packages and set up the project in editable mode so that local modules can be imported.
    ```bash
    make install
    ```

2.  **Set Up the Database:**
    This command will drop the existing database (if any), create a new one, apply the schema, and populate it with all necessary data. It is fully idempotent.
    ```bash
    make db-setup
    ```

3.  **Train a Model:**
    Train the baseline model for a specific stock symbol.
    ```bash
    make train symbol=RELIANCE
    ```

4.  **Generate Predictions:**
    Run the prediction service to generate signals using the latest trained models.
    ```bash
    make predict
    ```

5.  **Start the API:**
    Run the FastAPI server to serve the latest predictions.
    ```bash
    make api
    ```

## Zero-Budget Infrastructure Plan

As the project scales with more diverse data, the local database will become a bottleneck. This plan outlines a strategy for migrating to robust, free-tier cloud services.

-   **Database:** For a scalable, free-tier PostgreSQL database, the top candidates are:
    -   **Supabase:** Provides a full Postgres database, authentication, and storage on a generous free tier.
    -   **Neon:** A serverless Postgres provider with a free tier, ideal for projects with intermittent usage.
    -   **Self-Hosted (Docker):** Run a PostgreSQL Docker container on a free-tier cloud VM (e.g., Oracle Cloud Free Tier).
    *Migration is simple: update the environment variables in `common/db.py` to point to the new cloud DB host.*

-   **Data Sources (Free Tiers):**
    -   **News/Announcements:** NewsAPI (developer tier), GDELT Project.
    -   **Geological Data:** USGS Earthquake Catalogs.
    -   **Academic Research:** arXiv API.

## Project Status & Milestones

This project is developed in phases, as outlined in the [Product Requirements Document](docs/prd.md).

### Phase 1: Wizard-of-Oz (WoZ) Prototype (✓ Complete)
- [x] Define data model and schema.
- [x] Manual, notebook-driven prototype.
- [x] Establish baseline experiment criteria.

### Phase 2: Automation & Database Integration (● In Progress)
- [x] Automated data pipeline for market prices.
- [x] Prediction service using a baseline ML model.
- [x] Basic read-only API to serve signals.
- [ ] **Next:** Automated pipelines for alternative data (news, sentiment, corporate/geological events, etc.).

### Phase 3: MLOps & Advanced Modeling (● In Progress)
- [x] Foundational experiment tracking (DB tables).
- [x] Foundational model registry (DB tables).
- [x] Foundational feature store (`features.py` module).
- [ ] **Next:** Implement an ensemble of more advanced models (e.g., XGBoost).
- [ ] **Next:** Build a monitoring dashboard (e.g., using Streamlit).

### Phase 4: Self-Evolution & Autonomous Operation (○ Not Started)
- [ ] Self-Healing Module.
- [ ] Self-Evolution Engine.
- [ ] Advanced AI Integration (Quantum ML, GNNs, RL).# ai_project_v2
