+++
title = "Rubyで便利だなって思うあれこれ"
date = 2018-12-04T23:47:52+09:00
draft = false
tags = ["method"]
categories = ["method"]
+++

***
**・正規表現で文字列の中から数字だけを取り出す**
```first.rb
a = gets.chomp
↓
AWBWCWDWEWFWGWH
puts a.gsub(/[AEGIOSZ]/,"A" => "a", "B" => "b",
                       "C" => "c", "D" => "d", "F" => "f",
                       "G" => "g", "H" => "h")
↓
aWBWCWDWWFWgWH

```

```
[AEGIOSZ]←はこの中で当てはまるものだけって事
```
***
**・１部分の文字を正規表現で消す(破壊的)**
```first.rb
a = "aaabbbcccddd"
puts a.gsub!(/ccc+/, '')
↓
aaabbbddd
```
***
**・正規表現で文字列の置き換え**

```first.rb
a = gets.chomp
↓
kamukayakarakauy
puts a.gsub(/(ka)/, "///")
↓
///mu///ya///ra///uy
```
***
**・文字列になっている数字を数値に変換する**
```first.rb
a = ["9", "9", "8", "6", "1"]
a.map(&:to_i)
↓
[9, 9, 8, 6, 1]
```
***
**・配列に入っている数値の合計を求める**
```first.rb
a = [9, 9, 8, 6, 1]
a.inject(:+)
↓
33
```
***
**・配列の要素を半角スペース区切りで出力する**
**・1次元配列の場合**
```first.rb
array = ["aaa", "bbb", "ccc"]
puts array.join(' ')
↓
aaa bbb ccc
```

**・多次元配列の場合も一緒**
```first.rb
array = ["aa", ["bb", "cc", ["dd", "ee"]], ["ff", "gg"]]
puts array.join(' ')
↓
aa bb cc dd ee ff gg
```
***
**・絶対値を求める**
```first.rb
a = gets.chomp.to_i
↓
-1 -98 5
p a.abs
↓
1 98 5
```
***
**・printで空白スペースで出力したい**
```first.rb
print 'foo',
print 123,
print 'bar'
↓
foo 123 bar
```
***
**・繰り返し処理で横に出力したい時
はprintメソッドを使う。**<br>そして空白を空けたい時は
```
(i,(' '))
```
な書き方にする。
```first.rb
1.upto 5 do |i|
  print(i,(' '))
end
↓
1 2 3 4 5空白
```
けどこの時,5の横に空白がある状態,空白がない様に出力したい時は
```first.rb
1.upto 4 do |i|
  print(i,(' '))
end
5.upto 5 do |i|
  print i
end
↓
1 2 3 4 5
```
***
**・配列のインデックス番号を全部取得したい時**
```first.rb
ary = [5, 4, 1, 7, 3, 8]

p ary.each_with_index.select{|e, i| e >= 5}.map{|e| e[1]}
↓
[0, 3, 5]
```
他にも色々あるみたい、
```first.rb
ary.each_with_index.each_with_object([]){|(e, i), acc| acc << i if e >= 5}

ary.each_with_index.select{|e, i| e >= 5}.map{|e| e[1]}

ary.each_with_index.each_with_object([]){|(e, i), acc| acc << i if e >= 5}

ary.flat_map.with_index{|e,i|e>=5 ? i : []}
```
