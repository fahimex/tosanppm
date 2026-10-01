# Tosun Product Portfolio Model

## Data model

Product master, calendar periods, configurable KPI definitions, immutable period observations, import batches, data-quality findings, alerts, lifecycle history, and decision history are separate entities. The natural observation key is Product ID + Period + KPI ID; imports stage changes before append and cannot silently replace history.

## KPI framework

KPI applicability is layered: common health metrics, business-line metrics, category templates, then product overrides. Every KPI stores its formula, unit, frequency, target, warning and critical thresholds, directionality, weight, applicable categories, lifecycle adjustments, and source. Templates cover POS hardware, Gold ATM, banking kiosk/cashless, banking software, payment switch, payment platform, AI products, and Tourist Card.

## Health scoring

Default weights are Financial 25%, Customer & Market 20%, Adoption & Usage 15%, Operational & Technical 15%, Strategic Fit 15%, and Lifecycle & Future Potential 10%. KPIs are normalized to 0–100 against lifecycle-aware targets, aggregated within dimensions, then weighted into the overall score. Missing values lower confidence and data-quality scores; they are never silently converted to zero.

## Decision engine

Recommendations combine health, multi-period trend, financial trajectory, customer/adoption movement, operational risk, market attractiveness, strategic fit, future potential, and lifecycle. Kill/Sunset requires multiple sustained negative signals and a low strategic-exception score; revenue alone never triggers it. Fast is treated as mission-critical infrastructure, so criticality and resilience remain separate from financial performance. Each recommendation saves its evidence and action in decision history.

## Information architecture

Company → Business Line → Product Category → Product → Health Dimension → KPI → Actual / Target / Trend → Lifecycle → Decision. Fourteen management views share global filters for business line, category, product, lifecycle, period, health, and recommendation.

## Excel import schema

The workbook uses seven sheets: Product Master, Financial Metrics, Customer Metrics, Usage Metrics, Operational Metrics, Strategic Metrics, and Decision History. Product ID and Period identify time-series rows. Imports are structure-checked, product-mapped, validated, quality-scored, previewed, and then appended; historical corrections require explicit confirmation.
