
index=* host=* ERROR "Stack Trace:"
| where ((CustomerID=="$SearchCustomerNo$" OR "$SearchCustomerNo$"=="0")
    AND (TxnName=="$SearchTransactionName$" OR "$SearchTransactionName$"=="Arama"))
| rex field=_raw "(?i)Stack Trace:\s*(?<HataMesaji>[^\r\n]+)"
| eval HataMesaji = trim(HataMesaji)
| where HataMesaji != ""
| stats count by HataMesaji
| sort -count





index=* host=* ERROR "Stack Trace:"
| where ((CustomerID=="$SearchCustomerNo$" OR "$SearchCustomerNo$"=="0")
    AND (TxnName=="$SearchTransactionName$" OR "$SearchTransactionName$"=="Arama"))
| rex field=_raw "(?i)Stack Trace:\s*(?<HataMesaji>[^\r\n]+)"
| eval HataMesaji = trim(HataMesaji)
| where HataMesaji != ""
| stats count by HataMesaji
| sort -count





index=YOUR_INDEX

| eval period=case(
    _time>=strptime("2026-04-01","%Y-%m-%d") AND _time<strptime("2026-04-08","%Y-%m-%d"), "prev",
    _time>=strptime("2026-04-08","%Y-%m-%d") AND _time<strptime("2026-04-15","%Y-%m-%d"), "current"
)

| where isnotnull(period)

| eval is_error=if(match(_raw,"(?i)NullReferenceException"),1,0)

| stats 
    count as total
    sum(is_error) as error_count
    by TxnName period

| eval error_rate = error_count / total

| xyseries TxnName period error_rate

| eval prev=coalesce(prev,0), current=coalesce(current,0)

| eval diff = current - prev
| eval rate_change = case(
    prev=0 AND current>0, 100,
    prev>0, round((diff/prev)*100,2),
    true(), null()
)

| table TxnName prev current diff rate_change
| sort -rate_change
