index=your_index host=your_host log_level=ERROR
| eventstats count by TxnName
| sort -count
| dedup TxnName
| head 5
| where TxnName IN (
    [ search index=your_index host=your_host log_level=ERROR
      | stats count by TxnName
      | sort -count
      | head 5
      | fields TxnName ]
)
| timechart span=1h count by TxnName



index=your_index host=your_host log_level=ERROR
| stats count by TxnName
| sort -count
| head 5
| fields TxnName
| map search="search index=your_index host=your_host log_level=ERROR TxnName=$TxnName$
    | timechart span=1h count by TxnName"
