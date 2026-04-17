index=YOUR_INDEX earliest=-14d@d latest=@d
| eval period=if(_time>=relative_time(now(), "-7d@d"), "current", "prev")

| eval is_error=if(status="ERROR",1,0)

| stats 
    count as total
    sum(is_error) as error_count
    by TxnName period

| eval error_rate = error_count / total

| xyseries TxnName period error_rate

| eval prev=coalesce(prev,0), current=coalesce(current,0)

| eval diff = current - prev
| eval rate_change = if(prev>0, round((diff/prev)*100,2), null())

| table TxnName prev current diff rate_change
| sort -rate_change


index=YOUR_INDEX

| eval period=case(
    _time>=strptime("2026-04-01","%Y-%m-%d") AND _time<strptime("2026-04-08","%Y-%m-%d"), "prev",
    _time>=strptime("2026-04-08","%Y-%m-%d") AND _time<strptime("2026-04-15","%Y-%m-%d"), "current"
)

| where isnotnull(period)

| eval is_error=if(status="ERROR",1,0)

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

| where total > 100

| table TxnName prev current diff rate_change
| sort -rate_change



