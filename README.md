index=* host=* ERROR "Stack Trace:"
| where ((CustomerID=="$SearchCustomerNo$" OR "$SearchCustomerNo$"=="0")
    AND (TxnName=="$SearchTransactionName$" OR "$SearchTransactionName$"=="Arama"))
| eval HataMesaji = mvindex(split(_raw, "Stack Trace:"), 1)
| eval HataMesaji = mvindex(split(HataMesaji, "\n"), 0)
| eval HataMesaji = trim(HataMesaji)
| where HataMesaji != ""
| stats count by HataMesaji
| sort -count
