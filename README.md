index=your_index host=your_host log_level=ERROR earliest=@d latest=now
| eval TxnName=lower(trim(TxnName))
| eventstats count by TxnName
| sort -count TxnName
| dedup TxnName
| head 5
| fields TxnName
| append [
    search index=your_index host=your_host log_level=ERROR earliest=@d latest=now
    | eval TxnName=lower(trim(TxnName))
    | timechart span=1h count by TxnName
]
| where isnotnull(_time)
