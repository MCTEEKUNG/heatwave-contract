# Heatwave Forecast Contract (schema_version 1)

Static JSON published for the HeatMAP frontend. No API server.

`forecast_provinces.json`:
- `schema_version` (int) = 1
- `model` (str), `generated_at` (ISO datetime, UTC), `n_provinces` (int, = 77)
- `provinces[]`: `id`, `code`, `name_th`, `name_en`, `region`, `lat`, `lon`, `issue_date` (YYYY-MM-DD)
  - `forecasts[]` (one per lead 2,3,4,5,6 weeks): `lead_weeks`, `probability` (0–1),
    `climatology_base_rate` (0–1), `ratio_vs_normal` (≥0), `risk_level_th`, `risk_level_en`
- Risk levels (`risk_level_en`): `Low | Normal | Elevated | High`
  - app mapping: Low→low, Normal→moderate, Elevated→high, High→extreme

Forecast `target_date` = `issue_date` + `lead_weeks` × 7 days.
Consumers MUST reject any object whose `schema_version` != 1.
Produced and validated by `DeepSeek_Heatwave/scripts/publish_bridge.py --publish`.
