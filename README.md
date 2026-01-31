Access4All — Accessibility Scoring for Airbnb Listings

Access4All computes a deterministic, rule-based accessibility score (0–100) for Airbnb listings across multiple cities.
The score reflects how accessible a listing is for users with mobility constraints.

This is not a machine-learning model.
It is a transparent, non-compensatory scoring system designed to be conservative and explainable.

A full methodological report has already been submitted; this repository contains the code and interface only.

Project Structure

The project is implemented as Databricks/Jupyter notebooks (.ipynb).
All datasets are pre-built and loaded from shared Azure Blob Storage.

Notebooks:

01_airbnb_data_loader.ipynb
Loads core Airbnb listing data used for UI enrichment only (URLs, location, details).
No scoring is performed here.

02_osm_wheelchair_poi_loader.ipynb
Loads OpenStreetMap wheelchair-related POI data used in the environmental accessibility layer (v2).

03_terrain_slope_layer.ipynb
Loads terrain and slope data used to assess physical accessibility constraints (v3).

score_engine.ipynb
Implements the full deterministic accessibility scoring logic.
Produces final scores, confidence values, limiting layers, and explanations.

final_evaluator.ipynb
Performs consistency and sanity checks on the final scores
(monotonicity, hard constraints, distribution checks).

interface_runner.ipynb
Final user interface for presenting results (Top-K listings per city).
No scoring or filtering logic is applied here.

Data Access

All tables are loaded from a shared Azure Blob Storage container (main project storage).

SAS tokens are not included in this repository.
You should insert their own SAS token where indicated in the notebooks.

How to Run the Interface:

Insert your Azure SAS token (data access only)

Run the interface notebook top to bottom

Select city and Top-K when prompted

To re-run with different widget selections, re-run starting from the Input Handling cell.

Loaded Tables (Interface):

access4all_final_scores

access4all_airbnb_v1_9cities (UI enrichment only)

Design Notes:

Scoring, evaluation, and UI are fully decoupled

All UI joins happen only at the final stage

A score of 0 indicates insufficient or conflicting evidence — not necessarily inaccessible

Outputs were intentionally cleared before submission for readability
