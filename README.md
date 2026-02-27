# QuantFlowque

## Actualización - 27 de febrero de 2026

**Estatus actual:** Paper Trading automatizado implementado y en fase de validación (sistema listo para simular trades diarios con alertas vía WhatsApp, validando edge estadístico antes de despliegue live).

## Descripción del Proceso de Paper Trading

### Base para llegar a este punto
Tras backtesting inicial de estrategias (mean reversion y momentum, como recomienda Chan en *Quantitative Trading*), se identificó un edge estadístico prometedor con Sharpe >0.75 en datos históricos. Decidimos avanzar a paper trading para validar robustez out-of-sample, evitando overfitting mediante walk-forward testing y métricas como drawdown máximo <15%.

### Automatización del proceso
El sistema usa Python con APIs de datos de mercado (ej. yfinance) y WhatsApp Business API (vía Twilio o pywhatkit). Se integra con scheduler como APScheduler para runs diarios automáticos, registrando trades simulados en logs/CSV.

### Flujo de ejecución
1. Verificar hora (20:30-20:45 CET).
2. Obtener datos OHLCV.
3. Generar señales (ej. RSI & MA crossover).
4. Simular trade (posición, SL/TP).
5. Enviar WhatsApp y loggear.
6. Monitorear P&L.

### Ejemplo de mensaje WhatsApp
```
🚨 Paper Trade - 27/02/2026 20:35
EURUSD: BUY @1.0850 (RSI=28)
Size: 0.01 | SL:1.0820 | TP:1.0900
Sharpe: 0.85 #QuantEdge
```

### Razón del rango 20:30-20:45
Coincide con apertura NY (alta liquidez/volatilidad para forex). 15 min enfocado para alta-prob setups, alineado con sesiones óptimas y ritmos ultradianos.

Proyecto basado en principios de Ernest Chan, métodos de Rubén Martínez y SAR #2.