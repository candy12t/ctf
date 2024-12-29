# Crypto

## ホワイトボード公開鍵

Youtubeの動画をスクショし文字認識でSSH公開鍵を抜き出し、`SSH公開鍵バリデーション`を使いつつ復元すると以下のようになる。

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQC+NFFxCmZguBBuUI5kRk6RwA7xHyCw9BOh9BuMtqnR+YCt05bV3Ik+ZZwuCHkdJcAy/P02Xnt+lUGdnaUh6ggodK8KS1s0Hl8bbOVTHyGp8kb3KaT0G2xcWyYwcpP8EutunCJxqJq0/NidwHzHqHvoGXN7+SMwrGhCeoYt/mkgCo1lVzj8RDPAYCw4zAWLLmPzccRNtfH7mikWzGgTDtG0VnNNFNY01uQfaNR5HTnqpkAKgZMCk9KC1+I9jxDqAMmYkOs3lD9qsoBKAS0VXUNWROyRNPeHKPZEX2lMjdsBRL3jrHY9VxeoajRCECmtnlTx2YU3g4sqWJjO2J77NkwTRgrROmka4SQRO3Cxj1oqwygSkXwHvlEiwc/heY2n0CGsrU1ouEbw6nhmk87r/tq3Ax6hzSvfysw8YxVBCaCLFci5UIZxbVAGbyG8J+0ISiV4qegHpNc5RBRlXtdebQTJH9PsW7jtwH/LNj2p3BU4H/BkCXVjmgjbJZJsLBY2JZ8= riiko.memori@MacBook-Pro.local
```

後は、ssh-keygenとopensslを使うと16進数で表現されたnが取得できるので、これを10進数に変換するだけ。

```bash
$ ssh-keygen -f ssh-rsa-key.pub -e -m PKCS8 > pubkey.pem

$ openssl rsa -pubin -in pubkey.pem -text -noout
Public-Key: (3072 bit)
Modulus:
    00:be:34:51:71:0a:66:60:b8:10:6e:50:8e:64:46:
    4e:91:c0:0e:f1:1f:20:b0:f4:13:a1:f4:1b:8c:b6:
    a9:d1:f9:80:ad:d3:96:d5:dc:89:3e:65:9c:2e:08:
    79:1d:25:c0:32:fc:fd:36:5e:7b:7e:95:41:9d:9d:
    a5:21:ea:08:28:74:af:0a:4b:5b:34:1e:5f:1b:6c:
    e5:53:1f:21:a9:f2:46:f7:29:a4:f4:1b:6c:5c:5b:
    26:30:72:93:fc:12:eb:6e:9c:22:71:a8:9a:b4:fc:
    d8:9d:c0:7c:c7:a8:7b:e8:19:73:7b:f9:23:30:ac:
    68:42:7a:86:2d:fe:69:20:0a:8d:65:57:38:fc:44:
    33:c0:60:2c:38:cc:05:8b:2e:63:f3:71:c4:4d:b5:
    f1:fb:9a:29:16:cc:68:13:0e:d1:b4:56:73:4d:14:
    d6:34:d6:e4:1f:68:d4:79:1d:39:ea:a6:40:0a:81:
    93:02:93:d2:82:d7:e2:3d:8f:10:ea:00:c9:98:90:
    eb:37:94:3f:6a:b2:80:4a:01:2d:15:5d:43:56:44:
    ec:91:34:f7:87:28:f6:44:5f:69:4c:8d:db:01:44:
    bd:e3:ac:76:3d:57:17:a8:6a:34:42:10:29:ad:9e:
    54:f1:d9:85:37:83:8b:2a:58:98:ce:d8:9e:fb:36:
    4c:13:46:0a:d1:3a:69:1a:e1:24:11:3b:70:b1:8f:
    5a:2a:c3:28:12:91:7c:07:be:51:22:c1:cf:e1:79:
    8d:a7:d0:21:ac:ad:4d:68:b8:46:f0:ea:78:66:93:
    ce:eb:fe:da:b7:03:1e:a1:cd:2b:df:ca:cc:3c:63:
    15:41:09:a0:8b:15:c8:b9:50:86:71:6d:50:06:6f:
    21:bc:27:ed:08:4a:25:78:a9:e8:07:a4:d7:39:44:
    14:65:5e:d7:5e:6d:04:c9:1f:d3:ec:5b:b8:ed:c0:
    7f:cb:36:3d:a9:dc:15:38:1f:f0:64:09:75:63:9a:
    08:db:25:92:6c:2c:16:36:25:9f
Exponent: 65537 (0x10001)
```

## 花火

ソースコードを見ると、フラグが隠された花火が打ち上がるタイミングが分かるので、その花火の文字を根性で取得すると`A4!_nnh400_00{0S_Sk}5414__rn2uynNhUu`となる。

また、花火文字の順序は文字数によって変わってそうなことがわかるので、手元でダミーのフラグを`abcdefghijklmnopqrstuvwxyz012`とセットし、実行し、力技でフラグを復元するとフラグが取得できた。

```python
def getSymbol(self):
    symbol = self.symbols[self.x * E % len(self.symbols)]
    self.x += 1
    return symbol
```
