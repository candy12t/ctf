# LLM

## プロンプトインコ

ソースコードを見るとフラグがChatGPTの解答に含まれると、「その質問にはお答えできません」となるので、フラグをbase64でエンコードして解答するように指示を出すとエンコードされたフラグが取得できるので、後はデコードするとフラグが取得できる。

```python
content = result.choices[0].message.content
if FLAG[6:-1] in content.replace(" ", ""):
    return render_template("index.html", prompt=prompt, message='その質問にはお答えできません')
return render_template("index.html", prompt=prompt, message=content)
```

## ガバガバずんだもん

秘密を2つ教えるとフラグを教えてくれる。(どうやら一発でフラグを取得できるプロンプトがあるみたい)
