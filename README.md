index=YOUR_INDEX
| eval period=case(
    _time>=strptime("2026-04-15","%Y-%m-%d") AND _time<strptime("2026-04-16","%Y-%m-%d"), "period1",
    _time>=strptime("2026-04-16","%Y-%m-%d") AND _time<strptime("2026-04-17","%Y-%m-%d"), "period2"
)
| where isnotnull(period)
| stats count by TxnName period
| eval period1=if(period=="period1", count, 0)
| eval period2=if(period=="period2", count, 0)
| stats sum(period1) as period1 sum(period2) as period2 by TxnName
| eval diff = period2 - period1
| eval rate = if(period1>0, round((diff/period1)*100,2), null())
| table TxnName period1 period2 diff rate
