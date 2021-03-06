# 2. 変数と標準入出力
## 目次
[2.1 変数](#21-変数)  
[2.2 文字の出力と入力](#22-文字の出力と入力)  
[一覧表](#一覧表)  
[演習問題](#演習問題)  

## 2.1 変数
次のC言語で書かれた簡単なコードを見てください。

```c
#include <stdio.h>

int main()
{
    int a;
    a = 10;

    printf("aには%dが入っています\n", a);

    return 0;
}
```

これを実行してみると `a には 10 が入っています` と表示されるはずです。では、軽く目を通してみましょう。

最初の `#include` から始まる一文についてはプログラムを実行するためのおまじないだと思ってください。プログラムを作成するときはコードの一番上にこの一文を書いてください。

次の `int main` から始まる一行について、プログラムはここから一行ずつ実行されていきます。プログラムを実行すると、 `int main` の下の { の部分から始まり

`int a;` という命令を行い、 `a = 10;` という命令を行い、 `printf(　～ );`  という文字を表示する命令を行っています。printfの詳しい説明は次の2.2章で行います。

`return 0;` という命令もおまじないだと思ってください。最後に } の部分でコードの記述は終了します。また、見てわかるように命令文を書いたらその命令文の一番後ろに ;(セミコロン) が必要になります。

少し内容を詳しく見てみましょう。int aというのはintという形のaという名前の変数を作れと言っています。

変数とは箱のようなものです。中にさまざまなデータを格納することができます。その箱の中にデータを入れれば、箱が壊れるまでずっとデータを保持することができます。C言語における変数の作り方は次のようにします。

```c
int variable;
```

variableというのはその変数の名前で、自由に決めてよいですが、アルファベットの大文字と小文字、＿(アンダーバー)、及び数字しか使えません。ただし、最初の一文字には数字は使えません。

また、変数名にはintやreturnなどの予約語を使うことが出来ません。予約語とは、C言語のプログラムの記述で使うキーワードのことです。

上のコードで言えば `int a;` のaが変数名です。intというのはその変数の型、すなわち箱の形で、これは中に整数を入れることができる箱を示しています。  
※ 変数の型と変数名の間は1つ以上のスペースであけなければなりません。

ここで、C言語で使われる主な変数の型にどんなものがあるか見てみましょう。

|型    |解説                                         |例              |
|:----:|---------------------------------------------|----------------|
|int   |整数を入れることができます。                 |int i = 1;      |
|float |実数を入れることができます。                 |float f = 1.23; |
|double|floatの倍の精度で実数を入れることができます。|double d = 1.23;|
|char  |文字を一文字入れることができます。           |char c = '1';   |

変数にデータ(整数、小数、文字等)を代入するには `=` を使用します。C言語では `=` は等しいという意味ではなく、右辺を左辺に代入するという意味を持つので注意が必要です。

```c
#include <stdio.h>

int main()
{
    int tanaka; // int 型の tanaka という名前の変数を作る
    tanaka = 10; // 変数 tanaka に整数 10 を代入する

    double tanaka2; // double 型の tanaka2 という名前の変数を作る
    tanaka2 = 10.52; // tanaka2 という名前の変数に実数 10.52 を代入する

    printf("tanaka = %d\n", tanaka);
    printf("tanaka2 = %.2f\n", tanaka2);

    return 0;
}
```

`//` はコメント(注釈)という意味で、それより右の文章はプログラムとして認識されなくなります。このコードがすべて実行されると、tanakaには10が、tanaka2には10.52が入っている状態となります。

変数の役割は値を保持することだけではありません。演算した結果を保存したり、変数同士で演算させてこそ始めて真価が見えてきます。

まずは次のコードを見てください。

```c
#include <stdio.h>

int main()
{
    int a = 20;  // 作成と同時に代入
    int b = 30; // 同様にして作成
    int c = a + b; // 作成と同時に a + b を代入

    printf("%d\n", c);
    printf("%d\n", c++); //cをインクリメント
    printf("%d\n", --c); //cをデクリメント

    return 0;
}
```

この結果、cには50が入ることになります。cが生成される(作られる)までに、aとbにはそれぞれ20と30が入っています。それを+したもの、すなわち20 + 30をcに代入しているわけです。この+の事を演算子と呼びます。

**主な演算子**

|演算子| 概要 |  例   |結果|
|:----:|:----:|:-----:|:--:|
|  +   |足し算|10 + 20| 30 |
|  -   |引き算|10 - 20| -10|
|  *   |掛け算|10 * 20| 200|
|  /   |割り算|20 / 10|  2 |
|  %   |あまり|10 % 20| 10 |

割り算は注意が必要で、分母が0だった場合、エラーを起こしてしまいます。

インクリメントは変数内の値を1つ加算し、デクリメントは変数内の値を1つ減算します。それぞれ次のように書きます。

インクリメント演算子: ++  
デクリメント演算子: --  

それぞれ変数の前につけるか後ろにつけるかによって動作が異なってきます。インクリメントを例に挙げて解説します。変数の先におかれた場合、先加算を行います。記述すると次のようになります。

```c
a = ++b;
```

この場合、

```c
b = b + 1;
a = b;
```

という動作を意味します。変数の後におかれた場合、後加算を行います。記述すると次のようになります。

```c
a = b++;
```

この場合、

```c
a = b;
b = b + 1;
```

という動作を意味します。デクリメントでも同様になります。

最後にchar型です。char型とは型の説明でもあった通り、一文字を格納することができます。

```c
char a = '1';
```

これでaには1という文字が入っています。1の前後にある'(シングルクォーテーション)は文字を示す際に必ずつけなければなりません。aという文字を表すなら `'a'` 、Nなら `'N'` と書きます。

```c
#include <stdio.h>

int main()
{
    char a = '1';
    printf("aは%c\n", a);

    return 0;
}
```

## 2.2 文字の出力と入力
変数について簡単に抑え終わったところで、printfについて見ていきましょう。printfは単刀直入にいうと、()の中に入った""(ダブルクォーテーション)で囲まれた文字列を出力するという命令です。(プログラミングではプログラムの結果を表示することを「出力する」と表現します。)このような命令文は関数と呼ばれていて、()の中にその関数の動作を記述します。

printfの場合、 `printf("文字列");` を実行すると、文字列の部分が出力されることになります(""は含まれません)。では、次のコードを見てください。2.1章でも出てきたものです。

```c
#include <stdio.h>

int main()
{
    int tanaka; // int 型の tanaka という名前の変数を作る
    tanaka = 10; // 変数 tanaka に整数 10 を代入する

    double tanaka2; // double 型の tanaka2 という名前の変数を作る
    tanaka2 = 10.52; // tanaka2 という名前の変数に実数 10.52 を代入する

    printf("tanaka = %d\n", tanaka);
    printf("tanaka2 = %.2f\n", tanaka2);

    return 0;
}
```

ここで、上のコードのprintfを見てみると、%dや%.2fという文字が書かれています。これはフォーマット指定子と呼ばれ、%dはint型の変数の中身を直接文字列に埋め込む事ができます 。

表示する変数は" "で区切られた文字列の後ろに ,(コンマ)で区切って列挙します。同様にしてdouble型変数なら%f、char型変数なら%cとなっています。%.2fは小数点以下2桁まで表示するという意味です。\nは改行を意味します。例えば、

```c
int a = 100; // 変数は作成と同時に数値を入れることができます
double b = 3.14;
```

という変数があって、この2つの変数の中身を出力させたいときは、

```c
printf("aの中身は%dで、bの中身は%fです\n", a, b);
```

と記述することができます。後ろに列挙する変数の順番はその指定子の並びと同じ並び順にしなくてはいけません。

**printfのフォーマット指定子と変数の型**

|型    |int|float|double|char|
|:----:|:-:|:---:|:----:|:--:|
|指定子| %d|  %f |  %f  | %c |

printfの他にも文字や文字列を出力することのできる命令があります。その中でも代表的なものはputsとputcharです。

```c
#include <stdio.h>

int main()
{
    puts("ABC");
    printf("DEF");
    putchar('\n');

    return 0;
}
```

このプログラムの結果は

```c
ABC
DEF
```

と表示されます。

putsは文字列を出力して改行を行います。putsで表示できるのは文字列だけなので、printfのように**今までに学んだ**変数を出力することはできないので注意してください。

putcharは1文字だけを表示する命令です。 `\n` はプログラム内では改行を表し、1文字として数えられます。putcharでは1文字を表示するので"(ダブルクォーテーション)ではなく'(シングルクォーテーション)を使います。putcharもprintfのように様々な変数を出力することはできませんが、char型の変数だけ出力することができます。そのときは `putchar(変数)` と書きます。シングルクォーテーションは必要ないので注意しましょう。

それでは次にプログラムに文字や数字を入力することのできるscanfとgetcharを学びます。

```c
#include <stdio.h>

int main()
{
    int n;
    char c;

    puts("正の整数と文字を１つずつ入力してください");
    scanf("%d", &n);
    c = getchar();
    printf("%d%c\n", n);

    return 0;
}
```

例えばこのプログラムに `12C` と入力すると `12C` と表示されます。scanfで12を受け取り、getcharでCを受け取ってprintfで出力しています。

キーボードから数値などを読み込むために用いられるのがscanfです。ここでの%dはprintfの場合と同様で整数の指定を行っています。したがって上のコードではキーボードから整数を読み込んで、その値をnに格納するという命令を書いています。ただし、printfとは異なり変数の前に&という記号をつけなければなりません。&は今はおまじないだと思ってください。

scanfのフォーマット指定子もprintfとほとんど同じですがdouble型だけ%lfというprintfと違う指定子になるので注意してください。

**scanfのフォーマット指定子と変数の型**

|型    |int|float|double|char|
|:----:|:-:|:---:|:----:|:--:|
|指定子| %d|  %f |  %lf | %c |

getcharは1文字だけを受け取る命令です。上のプログラムで `12CD` と入力しても `12C` としか表示されません。書き方が `変数 = getchar()` と今まで学んだ他の命令と異なるので注意しましょう。

## 一覧表
**変数の型**

|型    |解説                                         |例              |
|:----:|---------------------------------------------|----------------|
|int   |整数を入れることができます。                 |int i = 1;      |
|float |実数を入れることができます。                 |float f = 1.23; |
|double|floatの倍の精度で実数を入れることができます。|double d = 1.23;|
|char  |文字を一文字入れることができます。           |char c = '1';   |

**主な演算子**

|演算子| 概要 |  例   |結果|
|:----:|:----:|:-----:|:--:|
|  +   |足し算|10 + 20| 30 |
|  -   |引き算|10 - 20| -10|
|  *   |掛け算|10 * 20| 200|
|  /   |割り算|20 / 10|  2 |
|  %   |あまり|10 % 20| 10 |

**文字の出力と入力**

```c
printf("文字列と指定子", 変数1, 変数2);
puts("文字列");
putchar('一文字');

scanf("指定子", &変数);
変数 = getchar();
```
 
**printfのフォーマット指定子と変数の型**

|型    |int|float|double|char|
|:----:|:-:|:---:|:----:|:--:|
|指定子| %d|  %f |  %f  | %c |

**scanfのフォーマット指定子と変数の型**

|型    |int|float|double|char|
|:----:|:-:|:---:|:----:|:--:|
|指定子| %d|  %f |  %lf | %c |

## 演習問題
１. 2つの数字を入力してその和を出力するプログラムを作成してください。

```
入力例
1 2

出力例
3
```

２. 次の2つの変数の中身を入れ替えて表示してください。(ヒント：変数が別にもう一つ必要になります。)

```
int a = 1;
int b = 2;
```

