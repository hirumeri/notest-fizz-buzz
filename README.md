# notest-fizz-buzz
簡単なプログラムを例に取り、テストについて学びます。  
テストを書く目的はなんなのか。  
テストがあると何が嬉しいのか。  
そういったことを実感していただければと思います。

＊ TDD とかはやりません。

## How to start

```
$ git https://github.com/yo1000/notest-fizz-buzz.git
$ cd notest-fizz-buzz
$ cat src/main/java/com/yo1000/notest/FizzBuzz.java
```

## Exercise

### Step1
`com.yo1000.notest.FizzBuzz` に対して、テストを書きたいです。  
カバレッジは、C1 (分岐網羅) を満たしたいと思います。  
テストを書きはじめる前に、必要なケース数を算出してみましょう。

#### Answer
分岐先の数と、分岐箇所の数から、最低限必要なケース数を割り出すことができます。

| 分岐タイプ | 分岐先 | 箇所数 |
|:-----------|:-------|:-------|
| if         | 2      | 6 
| ?:         | 2      | 1

入力値にはいくつもの候補がありますが、  
あくまで C1 を満たす、ということを考えると、  
分岐に (入る / 入らない) の単純な経路のみで考えることができます。
  
それぞれ、分岐先は 2つずつであり、これが 7箇所あるので、  
以上から計算すると、全分岐経路を網羅するには、  
2^7 (=128) のケースを消化しなければならないことがわかります。

128 のテストケース、頑張ればギリギリ書けるレベルでしょうか。  
しかし、この程度の処理に、そこまでの頑張りは必要なのでしょうか。

### Step2
膨大なケース数を生み出してしまっている原因はなんでしょうか。  
どうしたら、より効率的に C1 を担保できるでしょうか。  
考えて、実践してみてください。

#### Answer
なぜこんなにも、ケース数が膨れ上がってしまうのでしょうか。  
たかだか、2つずつに分かれる、7つの分岐をテストするだけなのに、です。

その答えはシンプルです。  
原因は、悪いクラス設計 (および実装) にあります。

また、どうしたら効率的に C1 を担保できるのかに対しても、  
同様に答えはシンプルです。  
それぞれの分岐箇所が、独立したテストとして、  
書き起こすことが可能な状態であれば良いのです。

独立したテストとして、書き起こすことができる状態。  
ヒトコトでどのような状態のことであるかというと、  
それは、**それぞれの責務が分離された状態** のことです。

つまり、Step2 でテストを効率化するために行うべきことは、  
コードのリファクタリングなのです。

テストを考えることは、設計の妥当性を確認する行為に等しいといえます。  
テストを考えることで、悪い設計は炙りだされます。  
責務が適切に分離されていないクラスというのは、  
非常にテストがしづらく、先のように、たとえ単純なテストであっても、  
ケースが膨大になり、結果、テストの書きづらい状態を引き起こします。

コードを書く際には、必ずテストを行うことを念頭に置き、  
現在のコードはテストが書きやすいのか、  
C1 を満たすにはどの程度のケースが必要になりそうなのか、  
このような観点を、常に意識するようにしてください。  
責務は自然に、分離されていくことでしょう。

コーディングにおいて、責務を意識することの重要性はたびたび語られますが、  
その背景には、テストの書きやすさ (保守の行いやすさ)　が、  
理由のひとつとして存在することを、知っておくと良いでしょう。

### Step3
それでは、Step2 でリファクタリングされた、  
`com.yo1000.notest.FizzBuzz` に対して、実際にテストを書いてみましょう。

