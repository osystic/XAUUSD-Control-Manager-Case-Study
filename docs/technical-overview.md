# Technical overview

The confidential delivery is a MetaTrader 4 manual trade-control Expert Advisor. Public-safe architecture can be summarized as five layers:

1. on-chart editable controls and explicit actions;
2. shared XAUUSD settings synchronized across chart instances;
3. per-ticket protection state;
4. trade-management logic for initial SL, TP, Cover, stepping, break-even, SL-ALL, and explicit closing;
5. broker-aware validation for direction, executable Bid/Ask semantics, price normalization, StopLevel, and FreezeLevel.

The final Cover behavior uses the configured value as a favorable-move trigger only. Once reached, the protection target is original entry price. The private implementation is intentionally not published.
