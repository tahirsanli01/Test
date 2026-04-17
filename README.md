index=YOUR_INDEX earliest=-14d@d latest=@d

| eval period=if(_time>=relative_time(now(), "-7d@d"), "current", "prev")

| eval is_error=if(match(_raw,"(?i)error"),1,0)

| stats 
    count as total
    sum(is_error) as error_count
    by TxnName period

| eval error_rate = error_count / total

| xyseries TxnName period error_rate

| eval prev=coalesce(prev,0), current=coalesce(current,0)

| eval diff=current-prev
| eval rate_change=case(
    prev=0 AND current>0, 100,
    prev>0, round((diff/prev)*100,2),
    true(), null()
)

| table TxnName prev current diff rate_change
| sort -rate_change
