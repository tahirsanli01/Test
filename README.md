index=YOUR_INDEX earliest=-14d@d latest=@d
| eval period=if(_time>=relative_time(now(), "-7d@d"), "current", "prev")
| stats count by TxnName period
| xyseries TxnName period count
| eval prev=coalesce(prev,0), current=coalesce(current,0)
| eval diff=current-prev
| eval rate=case(
    prev=0 AND current>0, 100,
    prev>0, round((diff/prev)*100,2),
    true(), null()
)
| where prev > 10 OR current > 10
| table TxnName prev current diff rate
| sort -rate
