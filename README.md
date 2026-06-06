# Tibber — Grafana dashboard

A Grafana dashboard for a Tibber Prometheus exporter (such as
[terjesannum/tibber-exporter](https://github.com/terjesannum/tibber-exporter)),
showing live power usage, per-phase current, electricity price, and daily cost.

## Panels

- Current power-consumption gauge + per-phase current (L1 / L2 / L3).
- Power-consumption heatmap and time series.
- Price per kWh, cost today, and cost over the selected period.
- A `home` template variable (from `tibber_home_info`).

## Required metrics

`tibber_power_consumption`, `tibber_current`, `tibber_power_consumption_day_total`,
`tibber_power_price`, `tibber_power_cost_day*`, and `tibber_home_info`, exported
by a Tibber Prometheus exporter.

## Import

1. Grafana → Dashboards → New → **Import**.
2. Upload `dashboard.json` (or paste its contents).
3. Select your Prometheus data source.

## Disclaimer

Independent, unofficial project — not affiliated with or endorsed by Tibber.
"Tibber" is a trademark of its respective owner, used here for identification
only.

## License

[MIT](LICENSE)
