+++
title = "3ステップで学ぶRuby入門"
date = 2018-11-22T11:33:12+09:00
draft = false
tags = ["file","regexp","csv"]
categories = ["file","regexp","csv"]
+++

**-3ステップで学ぶRuby入門-**
この参考書の10章の「ファイルを書き換えよう」とゆう問題で
つまづいたのでメモ。

Ruby初心者にわかりやすい解説をしてくださってるグラミー先生とゆう方の記事を拝見させてもらいました。<br>こちらがグラミー先生のサイトです(^ ^)<br>[https://www.grami-sensei.com/](https://www.grami-sensei.com/"グラミー先生")

わかりやすく親切丁寧に説明をしてくださっているのでとても参考になりました。グラミー先生ありがとうございます( ´∀｀)

グラミー先生の記事を引用させてもらいました。

-----------------------------------------------------------

1.**クラスの雛形を記述する**<br>以下のようなクラスの雛形とクラスのインスタンスを
生成して実行するプログラムを記述し、
ファイル名をdata_replacement.rbとして保存します。

```data_replacement.rb

class DataReplacement
  attr_writer :inputfile, :outputfile

  def replace
    p 1
  end
end

replacement = DataReplacement.new
replacement.inputfile = ARGV[0]
replacement.outputfile = ARGV[1]
replacement.replace

```
[補足情報1]<br>ARGV[1]とARGV[2]はRubyをCLIで実行する時に外部のファイルなどの情報を処理するためのものです。<br>[補足情報2]<br>attr_writerで書き込み専用のアクセサメソッドを設定しています。

----------------------------------------------------------

2.**クラスの雛形を記述したプログラムを実行する**<br>コマンドライン上で保存したファイルを指定してプログラムを実行します。実行結果に1が表示されます。
```
$ ruby data_replacement.rb
1
```

----------------------------------------------------------
3.**ファイル読み込みを実装する**<br>以下のようにreplaceメソッドとcontentsメソッドを記述し保存します。

```data_replacement.rb

class DataReplacement
  attr_writer :inputfile, :outputfile

  def replace
    contents.each do |content|
      p content
    end
  end

  private

    def contents
      fail 'Specify inputfile.' if @inputfile.nil?
      File.read(@inputfile).split("\n")
    end
end

replacement = DataReplacement.new
replacement.inputfile = ARGV[0]
replacement.outputfile = ARGV[1]
replacement.replace

```

----------------------------------------------------------

4.**元のCSV形式のファイルを用意する**<br>以下のようなCSV形式のデータが記述してファイル名をinputdata.csvで保存します。

```inputdata.csv

山田 太郎,1,09012345678
山田 花子,2,09023456789
鈴木 次郎,1,09034567890
鈴木 桃子,2,09045678901
田中 三郎,1,09056789012
田中 梅子,2,09067890123
高橋 四郎,1,09078901234
高橋 桜子,2,09089012345
佐藤 五郎,1,09090123456
佐藤 李子,2,09001234567

```

[補足情報]<br>**CSVファイルとは**<br>「CSV」とは "Comma Separated Value" の略で、データをカンマ(" , ")区切った値の事です。アプリケーション間でデータをやり取りする際に使われます。CSV形式で保存されたファイルを「CSVファイル」と呼びます。
CSV形式のファイルは、メモ帳などのテキストエディターで作成することができます。項目と項目の間にカンマを入れてデーターを記入してゆきます。ファイルの拡張子は「csv」で保存します。メモ帳でカンマ区切りのデーターを作成し、「txt」ファイルとして保存すると、それは「CSVファイル」ではなくただの「テキストファイル」になりますので気をつけて下さい。

----------------------------------------------------------

5.**保存したプログラムを引数を指定して実行する**<br>コマンドライン上で以下のようにプログラムを実行します。実行結果がinputdata.csvの中身と同じであることを確認します。

```
$ ruby  data_replacement.rb inputdata.csv
```

```inputdata.csv

"山田 太郎,1,09012345678"
"山田 花子,2,09023456789"
"鈴木 次郎,1,09034567890"
"鈴木 桃子,2,09045678901"
"田中 三郎,1,09056789012"
"田中 梅子,2,09067890123"
"高橋 四郎,1,09078901234"
"高橋 桜子,2,09089012345"
"佐藤 五郎,1,09090123456"
"佐藤 李子,2,09001234567"

```

----------------------------------------------------------

6.**名前、性別、携帯電話番号を書き換える処理を記述して保存する**<br>以下のようにプログラムを記述し保存します。

```data_replacement.rb

class DataReplacement
  attr_writer :inputfile, :outputfile

  def replace
    contents.map do |content|
      name, sex_code, tel = content.split(',')
      last_name, first_name = name.split
      [last_name, first_name, sex(sex_code), separated_tel(tel)].join(',')
    end
  end

  private

    def contents
      fail 'Specify inputfile.' if @inputfile.nil?
      File.read(@inputfile).split("\n")
    end

    def sex(code)
      code.to_i == 1 ? '男性' : '女性'
    end

    def separated_tel(number)
      number.match(/(\d{3})(\d{4})(\d{4})/)
      "#{$1}-#{$2}-#{$3}"
    end
end

replacement = DataReplacement.new
replacement.inputfile = ARGV[0]
replacement.outputfile = ARGV[1]
p replacement.replace

```

----------------------------------------------------------

7.**名前、性別、携帯電話番号を書き換える処理を記述したプログラムを実行する**<br>コマンドライン上で保存したプログラムを以下のように実行します。
実行結果に書き換えた後の行毎の配列が表示されます。

```
$ ruby data_replacement.rb inputdata.csv
```

```inputdata.csv

["山田,太郎,男性,090-1234-5678", "山田,花子,女性,090-2345-6789",
   "鈴木,次郎,男性,090-3456-7890", "鈴木,桃子,女性,090-4567-8901",
   "田中,三郎,男性,090-5678-9012", "田中,梅子,女性,090-6789-0123",
    "高橋,四郎,男性,090-7890-1234", "高橋,桜子,女性,090-8901-2345",
    "佐藤,五郎,男性,090-9012-3456", "佐藤,李子,女性,090-0123-4567"]

```

----------------------------------------------------------


8.**ファイルに書き出す処理を追加する**<br>以下のようにプログラムを記述し保存します。

```data_replacement.rb

class DataReplacement
  attr_writer :inputfile, :outputfile

  def replace
    output = contents.map do |content|
      name, sex_code, tel = content.split(',')
      last_name, first_name = name.split
      [last_name, first_name, sex(sex_code), separated_tel(tel)].join(',')
    end.join("\n")
    write_file(output)
  end

  private

    def contents
      fail 'Specify inputfile.' if @inputfile.nil?
      File.read(@inputfile).split("\n")
    end

    def sex(code)
      code.to_i == 1 ? '男性' : '女性'
    end

    def separated_tel(number)
      number.match(/(\d{3})(\d{4})(\d{4})/)
      "#{$1}-#{$2}-#{$3}"
    end

    def write_file(output)
      fail 'Specify outputfile.' if @outputfile.nil?
      File.write(@outputfile, output)
    end
end

replacement = DataReplacement.new
replacement.inputfile = ARGV[0]
replacement.outputfile = ARGV[1]
replacement.replace

```

----------------------------------------------------------

9.**ファイルに書き出す処理を追加したプログラムを実行する**<br>コマンドライン上で保存したプログラムを以下のように実行します。
実行結果には何も表示されません。

```
$ ruby data_replacement.rb inputdata.csv outputdata.csv
```

[補足情報]<br>outputdata.csvが生成される。

----------------------------------------------------------

10.**書き出したファイルを確認する**<br>プログラム実行時に指定した書き出し用のファイルである
outputdata.csvを開いて確認します。
inputdata.csvを書き換えた内容が表示されます。

```inputdata.csv

山田,太郎,男性,090-1234-5678
山田,花子,女性,090-2345-6789
鈴木,次郎,男性,090-3456-7890
鈴木,桃子,女性,090-4567-8901
田中,三郎,男性,090-5678-9012
田中,梅子,女性,090-6789-0123
高橋,四郎,男性,090-7890-1234
高橋,桜子,女性,090-8901-2345
佐藤,五郎,男性,090-9012-3456
佐藤,李子,女性,090-0123-4567

```

----------------------------------------------------------

試しに自分の名前、性別、番号をinputdata.csvに書き込んでから

```
$ ruby data_replacement.rb inputdata.csv outputdata.csv
```

をしたらしっかりと記述されました:kissing_closed_eyes: 
