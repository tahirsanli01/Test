index=* host=* ERROR "Stack Trace:"

| where ((CustomerID=="$SearchCustomerNo$" OR "$SearchCustomerNo$"=="0")

    AND (TxnName=="$SearchTransactionName$" OR "$SearchTransactionName$"=="Arama"))

| rex field=_raw "(?i)Stack Trace:\s*(?<HataMesaji>[^\r\n]+)"

| eval HataMesaji = trim(HataMesaji)

| where HataMesaji != ""

| stats count by HataMesaji

| sort -count
