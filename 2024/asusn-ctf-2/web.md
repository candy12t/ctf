# Web

## SQL寿司

ID=50のお寿司を取得すればいいが、SQLクエリに`id`という文字列を含めることができないが、SQLクエリに大文字小文字の区別がないので、`id`ではなく`ID`にするとフラグを取得できる。

```sql
SELECT * FROM sushi WHERE ID = 50;
```

## インターネット探検隊

普通にwebサイトにアクセスしてもプログラミルクボーイのネタがあるだけ。

問題文の「※サポートの切れたOSやブラウザでインターネットに接続するのは危険です。十分注意してください。」と`CVE-2011-1998`がヒントになっており、リクエスト時のUser-AgentをIE9にすると、VBScriptが埋め込められたHTMLが取得できる。
ちなみに設定したUser-Agentは、`Mozilla/5.0 (compatible; MSIE 9.0; Windows NT 6.1; Trident/5.0; Tablet PC 2.0)`。

```html
<script language="VBScript">
    Sub DecodeAndDisplay()
        Dim encodedText, decodedText
    
        decodedText = AtbashCipher("zhfhm{Lg0mT4_1fMrd4_Xsi0N1Fn}")
    
        Document.getElementById("output").innerText = decodedText
    End Sub
    
    Function AtbashCipher(inputText)
        Dim i, currentChar, result
        result = ""

        For i = 1 To Len(inputText)
            currentChar = Mid(inputText, i, 1)
            If currentChar >= "A" And currentChar <= "Z" Then
                result = result & Chr(90 - (Asc(currentChar) - 65))
            ElseIf currentChar >= "a" And currentChar <= "z" Then
                result = result & Chr(122 - (Asc(currentChar) - 97))
            Else
                result = result & currentChar
            End If
        Next

        AtbashCipher = result
    End Function
    
    Call DecodeAndDisplay()
    </script>
```

フラグがアトバッシュ暗号で暗号化されているのがわかるので、CyberChef使って復号するとフラグが取得できる。

## JQ寿司

今度は`flag`という文字列が使うことができない。また、ソースコード見るとjqを実行して返却される結果が`id`, `name`, `price`の連想配列になっている必要がある。

```python
def get_sushi(query):
    result = jq.compile(query).input_value(data).all()
    return [(sushi['id'], sushi['name'], sushi['price']) for sushi in result[:3]]
```

ドキュメントやChatGPTの力も借りつつ、`'{id: del(.sushi) | to_entries | .[].value, name: .sushi[0].name, price: .sushi[0].price }'`でフラグが取得できる。
