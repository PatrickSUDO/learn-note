# Webhook

Webhook：
「Sometimes people call webhooks reverse APIs」但更精準的來說，Webhook比API 省略了一個request的步驟。前面有提到API是「request followed by a response」有問才有答，Webhook則是「it just sends the data when it’s available」「Whenever there’s something new, the webhook will send it to your URL.」主動告知。通常client端需要有一個url提供給server端，server端在有client端關心的訊息發生時，主動透過client端提供的url，發(request)一個POST告知client內容，而client則回傳一個簡單的response ok(status_code= 200)。
以下圖來舉例說明的話：
"data" =
POST -d '{"ID":"1122112", "gender":"female","change":"yes"} -H 'Content-Type:application/json' -H 'Accept:application/json' -H 'Authorization:<token>' https://api.shannon-client.com/receive
"thanks:)" =
HTTP/1.1 200 OK
{"text":"thanks:)"}