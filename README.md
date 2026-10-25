# Tibber — Grafana dashboard

A Grafana dashboard for a Tibber Prometheus exporter (such as
[terjesannum/tibber-exporter](https://github.com/terjesannum/tibber-exporter)
or the fork [Yornik/tibber-exporter](https://github.com/Yornik/tibber-exporter)).
It answers, in this order: is the meter data live, how much power is used now,
is power cheap now and in the next hour, what has today cost, and when was
power cheap over the selected range.

## Panels

- **Meter feed**: Live, Delayed or Stopped, with the time since the last
  reading. When the feed stops, every "now" value goes blank instead of
  showing an old number.
- **Power now**, **Price now** (with Tibber's level now and in 1 hour) and
  **Today so far** (kWh, cost, and the average price paid per kWh).
- **Next hour, per quarter**: the 15-minute slots that start in the next hour,
  with their price and level.
- **In the selected range**: energy, cost, the price paid per kWh, and the
  plain average of the slot prices. Paying less than that average means more
  power was used in cheaper slots.
- **Energy used at each price level**: the share of the kWh used at each of
  Tibber's 5 levels.
- **Price per 15-minute slot**: one bar per slot, coloured by its level.
  **Power** sits directly below it on the same time axis.
- **Energy per day** and **Cost per day** for the last 30 days. Today's bar is
  pale while the day is still running.
- **Meter and feed details** (collapsed): current per phase, feed history,
  minutes without readings, voltage per phase and meter signal strength.
- Grey regions on the time charts mark gaps in the meter feed.

Each level has one colour, chosen so that adjacent levels stay apart with
colour-vision deficiency, in both the light and the dark theme. The level is
also written out in every legend, tile and table.

## Required metrics

From a Tibber Prometheus exporter, with live measurements (Tibber Pulse or
Watty) enabled:

- `tibber_power_consumption`, `tibber_power_consumption_day_total`,
  `tibber_power_consumption_meter_total`
- `tibber_power_cost_day`, `tibber_power_cost_day_total`
- `tibber_power_price`, `tibber_power_price_level`,
  `tibber_power_price_next_hour`, `tibber_power_price_level_next_hour`
- `tibber_current`, `tibber_voltage`, `tibber_signal_strength`
- `tibber_home_info`, for the `home` variable

## Import

1. Grafana → Dashboards → New → **Import**.
2. Upload `dashboard.json` (or paste its contents).
3. Pick your Prometheus data source in the **Data source** variable at the
   top of the dashboard.

Tested with Grafana 13.2.4.

## Notes

- **Currency**: amounts are shown in euro. For another currency, change the
  unit of the price and cost panels.
- **Time zone**: the dashboard uses the browser's time zone. The per-day bars
  and "Today so far" follow the exporter's local midnight, so set the
  dashboard time zone to the home's time zone if your browser is elsewhere.
  The per-day bars assume a time zone less than 24 hours east of UTC.
- **Main fuse**: the per-phase current bars run to 25 A, with orange from
  20 A and red at 25 A. Change the maximum and thresholds to match your fuse.
- **Next hour**: Prometheus only holds prices 60 minutes ahead, so the
  next-hour table cannot show further. It is shown only when the time range
  ends now.

## Disclaimer

Independent, unofficial project — not affiliated with or endorsed by Tibber.
"Tibber" is a trademark of its respective owner, used here for identification
only.

## License

[MIT](LICENSE)
