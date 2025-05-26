# Commodity Market Forecasting using Natural Language Processing

This repository contains a research project that combines time-series forecasting with natural language processing (NLP) to generate explainable forecasts of commodity futures prices. The focus is on leveraging government economic reports to predict price movements and provide textual explanations that align with economic rationale.

## Project Overview

Commodity markets are influenced by supply and demand factors often reflected in government reports. This project aims to:

- Forecast future prices of oil and natural gas using historical data and textual analysis of Energy Information Administration (EIA) reports.
- Generate economic explanations for predicted price movements.
- Evaluate multi-modal model architectures that combine time-series and text features.

## Key Contributions

- A custom dataset created from EIA reports and futures prices.
- Ground-truth labels for causality reasons generated using ChatGPT and validated by an economist.
- Implementation and evaluation of multiple model architectures:
  - Baseline models (ARIMA, Average, Last-Step, Autoformer, GPT2)
  - Improved models (Time Series Transformer, Supervised RoBERTa)
  - Language models (GPT2-Medium, LLAMA-2-7b with PEFT)
  - Multi-modal cascaded and joint models combining price prediction and explanation generation

## Data Pipeline

![Data Pipeline](./f98b061e-0d7b-4851-9b41-d8fb0af5a1e6.png)

*Figure 1: Data collection, cleaning, and annotation pipeline used to build the final dataset.*

## Model Architectures and Parameters

![Improved Models Diagram](./b4f22663-5d58-4e31-9274-7eaab581c76a.png)

*Figure 2: Diagram of improved models and training parameters used for forecasting and reasoning.*

## Model Extensions

The project explores two main architectural extensions: cascaded and joint models. Cascaded models separate price prediction and explanation generation, while joint models combine both tasks into a single training objective.

![Flow Chart for Extension](./829833a0-bf30-41d2-9bb7-48c750f2e9e2.png)

*Figure 3: Flow chart depicting cascaded and joint model architectures for multi-modal forecasting.*

## Data Sources

| Report Type            | Format | Start Year | Docs | Size      |
|------------------------|--------|------------|------|-----------|
| Natural Gas Reports    | HTML   | 2001       | 1136 | 1.5M words|
| Petroleum Reports      | Text   | 2011       | 533  | 580K words|
| Short-Term Energy Outlook (STEO) | Text | 1997 | 325  | 1M words  |
| Futures Prices         | CSV    | 1983       | -    | 17,891 rows|

## Methods

### Forecasting Models

- **Baselines:** Average, Last-step, ARIMA, GPT-2 Regression, Autoformer
- **Improved:** Time Series Transformer (TST), RoBERTa-based regression (SFT)

### Reasoning Models

- **Zero-shot:** LLAMA-2 prompted for explanations
- **Fine-tuned:** 
  - GPT2-Medium (full fine-tuning)
  - LLAMA-2-7b (PEFT using LoRA)

### Multi-Modal Architectures

- **Cascaded:** Predict price first, then generate reason using predicted vs. previous prices
- **Joint:** Simultaneously predict price and explanation using a fine-tuned GPT2-Medium

## Evaluation Metrics

- **Forecasting:** MSE, MAE, MAPE
- **Reasoning (text generation):** ROUGE-1, ROUGE-L, ROUGE-Lsum

### Results Summary

#### Forecasting (Best Model)

- **SFT + RoBERTa:** 
  - MSE: 0.017 (Oil+NG)
  - MAE: 0.095
  - MAPE: 0.22

#### Reasoning (Best Model)

- **SFT + Llama2 (PEFT):**
  - ROUGE-1: 0.62
  - ROUGE-L: 0.53
  - ROUGE-Lsum: 0.53

## Final Model

**Cascaded Model combining Time-Series Transformer + Llama2 (PEFT):**

- Trained on EIA report text and futures prices
- Designed to aid analysts in understanding market dynamics
- Not intended for trading or financial decisions

## Limitations and Ethics

- The model uses public EIA data. Ethical considerations were addressed during data scraping.
- Not suitable for high-stakes financial decisions; intended as a research and analysis tool.

## Future Work

- Expansion to additional commodities
- Integration of real-time news and dynamic data
- Fusion layer and cross-attention architectures for tighter integration of modalities

## Team Members

- Dana Golden  
- Dikshya Mohanty  
- Khushboo Singh
