+++
title = "Rubyで身長、体重比較"
date = 2018-11-26T00:17:29+09:00
draft = false
tags = ["hash","array","each","if","merge","ruby"]
categories = ["hash","array","each","if","merge","ruby"]
+++

## 身長が高い人が優れている、けど身長が一緒やったら体重が軽い方が優れている(A君B君C君がいます)

これをプログラムすると

まず、**splitメソッド**で空白スペースで入力出来る様にします

```hash.rb
a = gets.chomp.split(" ")
b = gets.chomp.split(" ")
c = gets.chomp.split(" ")
```

[入力例]<br>`170 60`<br>`180 70`<br>`160 50`

そして**mapメソッド**を使って配列の文字列を数値にします

```hash.rb
aa = a.map(&:to_i)
bb = b.map(&:to_i)
cc = c.map(&:to_i)
```

[出力例]<br>`aa[170, 60]`<br>`bb[180, 70]`<br>`cc[160, 50]`<br>↑今この様に配列になっているからこれをhashにします

```hash.rb
h = { "A" => aa[0], "B" => bb[0], "C" => cc[0]}
w = { "A" => aa[1], "B" => bb[1], "C" => cc[1]}
```

[出力例]<br>`h = { "A" => 170, "B" => 180, "C" => 160}`<br>`w = { "A" => 60, "B" => 70, "C" => 50}`

次に**sortメソッド**を使って身長の高いもん順にならべかえる

```hash.rb
hh = h.sort { |(key1, val1),(key2, val2)| val2 <=> val1 }
```

[出力例]<br>`[["B", 180], ["A", 170], ["C", 160]]`

[補足情報]<br>`val2 <=> val1`この部分を`val1 <=> val2`の様にすると値の低い順に出力される

次は体重の軽い順に**sort**する

```hash.rb
ww = w.sort { |(key1, val1),(key2, val2)| val1 <=> val2 }
```

[出力例]<br>`[["C", 50], ["A", 60], ["B", 70]]`



 体重よりも身長の方が優れている優先度が高いから、<br>身長が高い人に点数を多く与えてあげる、<br>**eachメソッド**を使って1位の人に30点をあげる、<br>そしてそこから身長が低くなるにつれて点数を10点ずつ低くする計算式を作る

 ```hash.rb
 lank =30
 previous = 0
 score = {"A" => 0, "B" => 0, "C" => 0}
 hh.each { |key, val|
   if previous > val then
     lank -= 10
   end
   previous = val
   score[key] = lank
  }
  ```

  ```
  lank = 30
  1位の人に30点を上げたいから30を代入して上げます
  ```

  ```
  previous = 0
  previousには前回の人の値が入る
  けど最初の人は前回の人がいないから初期値として
  0を入れといて上げます
  ```

  [出力例]<br>`{"A"=>20, "B"=>30, "C"=>10}`

  ここまでは身長、次は体重
  ***

  **体重は身長よりも優先度が低いから**一番軽い人に3点、次に2点、1点と与える様にする、身長も体重も一緒の値の人は同点になります。

  ```hash.rb
  lank2 = 4
  previous2 = 0
  score2 = {"A" => 0, "B" => 0, "C" => 0}
  ww.each { |key, val|
    if previous2 < val then
      lank2 -= 1
    end
    previous2 = val
    score2[key] = lank2
  }
  ```

  [出力例]<br>`{ "A"=>2, "B"=>1, "C"=>3 }`

  次に身長と体重の値を足して上げる(merge)

  ```hash.rb
  score3 = score.merge(score2){ |key, v0, v1| v0 + v1 }
  ```

  [出力例]<br>`{ "A"=>22, "B"=>31, "C"=>13 }`

  そしてまた**sortメソッド**を使って値の高いもん順に出力して上げる

  ```hash.rb
  score4 = score3.sort { |(key1, val1),(key2, val2)| val2 <=> val1 }
  ```

  [出力例]<br>`[["B", 31], ["A", 22], ["C", 13]]`

  これで後は**インデックス番号**を指定して上げて**完成！**

  ```hash.rb
  puts score4[0][0]
  puts score4[1][0]
  puts score4[2][0]
  ```

  [出力例]
  ```hash.rb
  B
  A
  C
  ```

  無駄のコードとかも多くリファクタリングが出来る。<br>また余裕のある時に見直そう。
