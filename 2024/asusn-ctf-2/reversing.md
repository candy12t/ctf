# Reversing

## フラッシュ機械語リターンズ

ChatGPTの力を借りてスピード勝負。

## ターミナルトーク

bash風のアプリケーションでlsコマンドなど実行できるが、ジャンルがReversingなのでアプリの中身を見ていく。

macでは、`/Applications/bash-app.app/Contents/Resources/app/script/script.js`にlsなどのコマンドの挙動のコードが記述されているのがわかる。何やらbase64でエンコードされた文字があるので、デコードするとフラグが取得できる。

```js
async function myCommand() {
  document.querySelector("#audio_saiko").play();
  document.querySelector(".terminal-scroller").hidden = true;
  document.querySelector("#face_close").hidden = false;

  await sleep(400);
  await pakupaku(2);
  await sleep(200);
  await pakupaku(6);
  await sleep(1000);

  document.querySelector("#face_close").hidden = true;
  document.querySelector(".terminal-scroller").hidden = false;
  return atob("YXN1c257RWwzY1RyMG5fTTBfUzQxazBVZDRaM34hIX0=");
}
```

## whitespace

whitespaceで書かれたコードを[オンラインで実行できるインタプリタ](https://naokikp.github.io/wsi/whitespace.html)で実行すると、`What is the flag?(End with line break): `と出力される。これだけでは何もわからないので、パースだけしてメモリの操作を見る。

```
[0] SS STSTSTTTL (push 87)
[1] TLSS (prtc)
[2] SS STTSTSSSL (push 104)
[3] TLSS (prtc)
[4] SS STTSSSSTL (push 97)
[5] TLSS (prtc)
[6] SS STTTSTSSL (push 116)
[7] TLSS (prtc)
[8] SS STSSSSSL (push 32)
[9] TLSS (prtc)
[10] SS STTSTSSTL (push 105)
[11] TLSS (prtc)
[12] SS STTTSSTTL (push 115)
[13] TLSS (prtc)
[14] SS STSSSSSL (push 32)
[15] TLSS (prtc)
[16] SS STTTSTSSL (push 116)
[17] TLSS (prtc)
[18] SS STTSTSSSL (push 104)
[19] TLSS (prtc)
[20] SS STTSSTSTL (push 101)
[21] TLSS (prtc)
[22] SS STSSSSSL (push 32)
[23] TLSS (prtc)
[24] SS STTSSTTSL (push 102)
[25] TLSS (prtc)
[26] SS STTSTTSSL (push 108)
[27] TLSS (prtc)
[28] SS STTSSSSTL (push 97)
[29] TLSS (prtc)
[30] SS STTSSTTTL (push 103)
[31] TLSS (prtc)
[32] SS STTTTTTL (push 63)
[33] TLSS (prtc)
[34] SS STSTSSSL (push 40)
[35] TLSS (prtc)
[36] SS STSSSTSTL (push 69)
[37] TLSS (prtc)
[38] SS STTSTTTSL (push 110)
[39] TLSS (prtc)
[40] SS STTSSTSSL (push 100)
[41] TLSS (prtc)
[42] SS STSSSSSL (push 32)
[43] TLSS (prtc)
[44] SS STTTSTTTL (push 119)
[45] TLSS (prtc)
[46] SS STTSTSSTL (push 105)
[47] TLSS (prtc)
[48] SS STTTSTSSL (push 116)
[49] TLSS (prtc)
[50] SS STTSTSSSL (push 104)
[51] TLSS (prtc)
[52] SS STSSSSSL (push 32)
[53] TLSS (prtc)
[54] SS STTSTTSSL (push 108)
[55] TLSS (prtc)
[56] SS STTSTSSTL (push 105)
[57] TLSS (prtc)
[58] SS STTSTTTSL (push 110)
[59] TLSS (prtc)
[60] SS STTSSTSTL (push 101)
[61] TLSS (prtc)
[62] SS STSSSSSL (push 32)
[63] TLSS (prtc)
[64] SS STTSSSTSL (push 98)
[65] TLSS (prtc)
[66] SS STTTSSTSL (push 114)
[67] TLSS (prtc)
[68] SS STTSSTSTL (push 101)
[69] TLSS (prtc)
[70] SS STTSSSSTL (push 97)
[71] TLSS (prtc)
[72] SS STTSTSTTL (push 107)
[73] TLSS (prtc)
[74] SS STSTSSTL (push 41)
[75] TLSS (prtc)
[76] SS STTTSTSL (push 58)
[77] TLSS (prtc)
[78] SS STSTSL (push 10)
[79] TLSS (prtc)
[--] LSS STL (label STL)
[80] SS SSL (push 0)
[81] TLTS (readc)
[82] SS SSL (push 0)
[83] TTT (load)
[84] SLS (dup)
[85] SS STSTSL (push 10)
[86] TSST (sub)
[87] LTS SSL (jmpz SSL)
[88] LSL STL (jmp STL)
[--] LSS SSL (label SSL)
[89] SLL (pop)
[90] SS STL (push 1)
[91] SS SSL (push 0)
[92] TTS (store)
[93] SS STTTTTSTL (push 125)
[94] TSST (sub)
[95] SLS (dup)
[96] TSSL (mul)
[97] SS STL (push 1)
[98] TTT (load)
[99] TSSS (add)
[100] SS STL (push 1)
[101] SLT (swap)
[102] TTS (store)
[103] SS STTTSSTSL (push 114)
[104] TSST (sub)
[105] SLS (dup)
[106] TSSL (mul)
[107] SS STL (push 1)
[108] TTT (load)
[109] TSSS (add)
[110] SS STL (push 1)
[111] SLT (swap)
[112] TTS (store)
[113] SS STTSSTTL (push 51)
[114] TSST (sub)
[115] SLS (dup)
[116] TSSL (mul)
[117] SS STL (push 1)
[118] TTT (load)
[119] TSSS (add)
[120] SS STL (push 1)
[121] SLT (swap)
[122] TTS (store)
[123] SS STSSTSTTL (push 75)
[124] TSST (sub)
[125] SLS (dup)
[126] TSSL (mul)
[127] SS STL (push 1)
[128] TTT (load)
[129] TSSS (add)
[130] SS STL (push 1)
[131] SLT (swap)
[132] TTS (store)
[133] SS STTSSSTTL (push 99)
[134] TSST (sub)
[135] SLS (dup)
[136] TSSL (mul)
[137] SS STL (push 1)
[138] TTT (load)
[139] TSSS (add)
[140] SS STL (push 1)
[141] SLT (swap)
[142] TTS (store)
[143] SS STTSTSSL (push 52)
[144] TSST (sub)
[145] SLS (dup)
[146] TSSL (mul)
[147] SS STL (push 1)
[148] TTT (load)
[149] TSSS (add)
[150] SS STL (push 1)
[151] SLT (swap)
[152] TTS (store)
[153] SS STTSTSSSL (push 104)
[154] TSST (sub)
[155] SLS (dup)
[156] TSSL (mul)
[157] SS STL (push 1)
[158] TTT (load)
[159] TSSS (add)
[160] SS STL (push 1)
[161] SLT (swap)
[162] TTS (store)
[163] SS STSTTTTTL (push 95)
[164] TSST (sub)
[165] SLS (dup)
[166] TSSL (mul)
[167] SS STL (push 1)
[168] TTT (load)
[169] TSSS (add)
[170] SS STL (push 1)
[171] SLT (swap)
[172] TTS (store)
[173] SS STTSSTSTL (push 101)
[174] TSST (sub)
[175] SLS (dup)
[176] TSSL (mul)
[177] SS STL (push 1)
[178] TTT (load)
[179] TSSS (add)
[180] SS STL (push 1)
[181] SLT (swap)
[182] TTS (store)
[183] SS STSTSTSSL (push 84)
[184] TSST (sub)
[185] SLS (dup)
[186] TSSL (mul)
[187] SS STL (push 1)
[188] TTT (load)
[189] TSSS (add)
[190] SS STL (push 1)
[191] SLT (swap)
[192] TTS (store)
[193] SS STTSSSTL (push 49)
[194] TSST (sub)
[195] SLS (dup)
[196] TSSL (mul)
[197] SS STL (push 1)
[198] TTT (load)
[199] TSSS (add)
[200] SS STL (push 1)
[201] SLT (swap)
[202] TTS (store)
[203] SS STSSTSSSL (push 72)
[204] TSST (sub)
[205] SLS (dup)
[206] TSSL (mul)
[207] SS STL (push 1)
[208] TTT (load)
[209] TSSS (add)
[210] SS STL (push 1)
[211] SLT (swap)
[212] TTS (store)
[213] SS STTTSTTTL (push 119)
[214] TSST (sub)
[215] SLS (dup)
[216] TSSL (mul)
[217] SS STL (push 1)
[218] TTT (load)
[219] TSSS (add)
[220] SS STL (push 1)
[221] SLT (swap)
[222] TTS (store)
[223] SS STSTTTTTL (push 95)
[224] TSST (sub)
[225] SLS (dup)
[226] TSSL (mul)
[227] SS STL (push 1)
[228] TTT (load)
[229] TSSS (add)
[230] SS STL (push 1)
[231] SLT (swap)
[232] TTS (store)
[233] SS STSTSSTSL (push 82)
[234] TSST (sub)
[235] SLS (dup)
[236] TSSL (mul)
[237] SS STL (push 1)
[238] TTT (load)
[239] TSSS (add)
[240] SS STL (push 1)
[241] SLT (swap)
[242] TTS (store)
[243] SS STSTTTTTL (push 95)
[244] TSST (sub)
[245] SLS (dup)
[246] TSSL (mul)
[247] SS STL (push 1)
[248] TTT (load)
[249] TSSS (add)
[250] SS STL (push 1)
[251] SLT (swap)
[252] TTS (store)
[253] SS STSTSTSTL (push 85)
[254] TSST (sub)
[255] SLS (dup)
[256] TSSL (mul)
[257] SS STL (push 1)
[258] TTT (load)
[259] TSSS (add)
[260] SS STL (push 1)
[261] SLT (swap)
[262] TTS (store)
[263] SS STTTTSTTL (push 123)
[264] TSST (sub)
[265] SLS (dup)
[266] TSSL (mul)
[267] SS STL (push 1)
[268] TTT (load)
[269] TSSS (add)
[270] SS STL (push 1)
[271] SLT (swap)
[272] TTS (store)
[273] SS STTSTTTSL (push 110)
[274] TSST (sub)
[275] SLS (dup)
[276] TSSL (mul)
[277] SS STL (push 1)
[278] TTT (load)
[279] TSSS (add)
[280] SS STL (push 1)
[281] SLT (swap)
[282] TTS (store)
[283] SS STTTSSTTL (push 115)
[284] TSST (sub)
[285] SLS (dup)
[286] TSSL (mul)
[287] SS STL (push 1)
[288] TTT (load)
[289] TSSS (add)
[290] SS STL (push 1)
[291] SLT (swap)
[292] TTS (store)
[293] SS STTTSTSTL (push 117)
[294] TSST (sub)
[295] SLS (dup)
[296] TSSL (mul)
[297] SS STL (push 1)
[298] TTT (load)
[299] TSSS (add)
[300] SS STL (push 1)
[301] SLT (swap)
[302] TTS (store)
[303] SS STTTSSTTL (push 115)
[304] TSST (sub)
[305] SLS (dup)
[306] TSSL (mul)
[307] SS STL (push 1)
[308] TTT (load)
[309] TSSS (add)
[310] SS STL (push 1)
[311] SLT (swap)
[312] TTS (store)
[313] SS STTSSSSTL (push 97)
[314] TSST (sub)
[315] SLS (dup)
[316] TSSL (mul)
[317] SS STL (push 1)
[318] TTT (load)
[319] TSSS (add)
[320] SS STL (push 1)
[321] SLT (swap)
[322] TTS (store)
[323] SS STL (push 1)
[324] TTT (load)
[325] LTS STSL (jmpz STSL)
[326] SS STSSTTTSL (push 78)
[327] TLSS (prtc)
[328] SS STSSTTTTL (push 79)
[329] TLSS (prtc)
[330] SS STSSSSTL (push 33)
[331] TLSS (prtc)
[332] LSL STTL (jmp STTL)
[--] LSS STSL (label STSL)
[333] SS STSTTSSTL (push 89)
[334] TLSS (prtc)
[335] SS STSSSTSTL (push 69)
[336] TLSS (prtc)
[337] SS STSTSSTTL (push 83)
[338] TLSS (prtc)
[339] SS STSSSSTL (push 33)
[340] TLSS (prtc)
[--] LSS STTL (label STTL)
[341] LLL (end)
```

0~79までで先程の文字の出力をしているのがわかり、それ以降はjumpしたりなど怪しい操作しているので、`push`している値がフラグになると予想を立てて値を抜き出す。抜き出した結果をascii codeに当てはめるとリバースされたフラグになるので、元に戻すとフラグが取得できる。

```
97 115 117 115 110 123 85 95 82 95 119 72 49 84 101 95 104 52 99 75 51 114 125
```

