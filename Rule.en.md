# Lang Wars - JavaChallenge 2014 (BETA)

*THIS DOCUMENT IS STILL BETA!*

## Overview of Game

You are programmer.
Let's propagandize programming languages and increase the population of the programming languages.
Overreach rivals and become the pontiff of programming languages!

## Pseudo Code of Game Rule

If you want to read the game rule in a programming language, please see [pseudo code](#PseudoCode).

## Goal of Game

Gain more _victory points_ calculated by the number of believers of each programming language than them of the other players.

## ゲームの大まかな流れ

プレイヤーは4人、プログラミング言語は8種類ある。

このゲームはターン制であり、各ターンごとに、プレイヤーたちは好きなプログラミング言語を _布教_ して信者を集める。
布教の情報は一部が隠されているため、他のプレイヤーとの駆け引きが重要となる。

10ターンでゲームが終了し、プレイヤーたちはそれぞれのプログラミング言語に対する信者数に応じて勝利点を得る。
各プログラミング言語の信者数が最も多いプレイヤーはその言語に対する勝利点を得るが、信者数が最も少ないプレイヤーは勝利点を失ってしまう。
したがって、目当てのプログラミング言語を積極的に布教して他プレイヤーより多くの信者を集めつつ、
他のプログラミング言語に対する信者数にも気を使って失点を防ぐことが重要である。
勝利点を最も多く獲得したプレイヤーの勝利となる。

## ゲームの開始

ゲームが開始すると、まずそれぞれのプログラミング言語に _注目度_ が3から6の間でランダムに設定され、プレイヤーに公開される。
注目度が高いプログラミング言語ほど、ゲーム終了時に得られる（または失う）勝利点が多くなる。

## ターンの流れ

ターンには _平日_ ターンと _休日_ ターンが存在する。
1ターン目は平日であり、1ターンごとに平日と休日が入れ替わる。
つまり、2ターンで一週間となる。

ターンが始まると、プレイヤーたちは一斉に布教する言語を選ぶ。
平日では1ターンで5回（5日分）布教をするが、休日では1ターンに2回（2日分）布教する。
1回の布教では1種類の言語を布教し、自分の布教した言語に対する信者数が1増える。
1ターン中の布教言語の割り振りは自由である。
例えば平日であれば、バラバラの5言語を1回ずつ布教しても良いし、同じ言語を5回布教しても良い。
なお、布教言語が他のプレイヤーと同じであっても、信者数の増加に影響はない。

全プレイヤーが布教言語を選んだら、各プログラミング言語に対する信者数が計算される。
そのターンが平日の場合、誰がどの言語を布教したかが全員に公開される。
そのターンが休日の場合、どのプログラミング言語が布教を1回以上されたかのみ公開される。

下の表は、平日と休日の布教の特徴をまとめたものである。

|                     | 平日 | 休日 |
| ------------------- | ---- | ---- |
| 布教回数            | 5    | 2    |
| 布教1回で増える信者数 | 1    | 1    |
| 布教情報の公開       | 全情報公開 | 各言語に対する布教の有無のみ公開 |

## ゲームの終了

10ターン目が終わると、ゲームが終了し、勝利点の計算に入る。

各プログラミング言語で得られる勝利点は、そのプログラミング言語に対する信者数を他のプレイヤーと比べて決められる。
そのプログラミング言語に対する信者数が全プレイヤー中で最も高い場合は、注目度と同じ点数の勝利点を得る。
逆に全プレイヤー中で最も低い場合は、注目度と同じ点数の勝利点を失う。
トップや最下位のプレイヤーが複数いる場合は、注目度をそれらのプレイヤーの人数で割った点数だけ得点あるいは失点する。

各プレイヤーの勝利点をすべてのプログラミング言語に対して計算したら、最も勝利点の高いプレイヤーを勝者とする。
最も勝利点の高いプレイヤーが複数いる場合は、そのゲームは引き分けである。

## AIの入出力形式

AIはゲーム開始時に実行される。
ゲームを始める準備ができたら`READY`と出力したのち、ゲームの設定を入力として受け取る。
また、ターンごとに現在の情報を入力として受け取り、そのターンでの布教言語を出力する。

AIの思考時間には制限がある。
制限時間を超過するとAIプログラムが強制的に停止され、それ以降の行動が「全日程で0番のプログラミング言語を布教する」として処理される。

### 準備完了メッセージの出力形式

ゲームを開始する準備ができたら、`READY`と標準出力に出力する。
ゲーム開始から5秒以内に出力がなければ、AIプログラムが強制的に停止される。

### ゲーム設定の入力形式

ゲーム開始時、つまり1ターン目の初めに、ゲームの設定が以下のフォーマットで標準入力に渡される。

<pre>
T P N
A<sub>0</sub> A<sub>1</sub> A<sub>2</sub> ... A<sub>7</sub>
</pre>

* T: 全ターン数。
* P: プレイヤー数。
* N: プログラミング言語の数。
* A<sub>n</sub>: プログラミング言語nの注目度。

### ターン情報の入力形式

各ターンの初めに、現在の情報が以下のフォーマットで標準入力に渡される。

<pre>
T D
B<sub>00</sub>　B<sub>01</sub> B<sub>02</sub> B<sub>03</sub>
B<sub>10</sub>　B<sub>11</sub> B<sub>12</sub> B<sub>13</sub>
B<sub>20</sub>　B<sub>21</sub> B<sub>22</sub> B<sub>23</sub>
:
:
B<sub>70</sub>　B<sub>71</sub> B<sub>72</sub> B<sub>73</sub>
R<sub>0</sub> R<sub>1</sub> R<sub>2</sub> ... R<sub>7</sub>
P<sub>0</sub> P<sub>1</sub> P<sub>2</sub> ... P<sub>7</sub>
</pre>

* T: 現在のターン数。1から始まる。
* D: 平日の場合は"W", 休日の場合は"H"。
* B<sub>nm</sub>: プログラミング言語nに対するプレイヤーmの公開されている（つまり平日の情報のみでわかる）信者数。このAIプレイヤー自身はプレイヤー0である。
* R<sub>n</sub>: プログラミング言語nに対するこのAIプレイヤーの真の（つまり休日も合わせた）信者数。
* P<sub>n</sub>: プログラミング言語nが前日の休日に布教をした(1)かしていない(0)か。

P<sub>0</sub> P<sub>1</sub> P<sub>2</sub> ... P<sub>7</sub>の行は、平日のターンでのみ含まれる。

### 行動の出力形式

そのターンでの布教言語は、以下のフォーマットで標準出力に出力する。

* __平日の場合__

  <pre>
  L<sub>0</sub> L<sub>1</sub> L<sub>2</sub> L<sub>3</sub> H<sub>L</sub>
  </pre>
  
* __休日の場合__

  <pre>
  L<sub>0</sub> L<sub>1</sub>
  </pre>

L<sub>n</sub>: 布教するプログラミング言語の番号（0から7で指定）。L<sub>0</sub>からL<sub>4</sub>の順番は関係しない。

一度行動を出力すると、そのAIのターンは終了となる。
なお、ターン開始から1秒以内に出力がなければ、AIプログラムが強制的に停止される。

<a name="PseudoCode"></a>

## ルールの疑似コード

    programming_language = (attention, revealed_believer[4], real_believer[4])

    main:
        init
        while turn <= 10:
            process_turn
            turn += 1
        finish

    init:
        players = player[4]
        languages = programming_language[8] (rand(3, 6), [0, 0, 0, 0], [0, 0, 0, 0])
        turn = 1

    process_turn:
        for l in languages:
            display_to_all_players(l.attention)
            display_to_all_players(l.revealed_believer)
            if not is_holiday:
                display_to_all_players(l.propagated)
            h.propagated = false

        for p in players:
            for i in [1 .. (is_holiday ? 2 : 5)]:
                target = languages[p.selected[i]]
                target.revealed_believer[p] += (is_holiday ? 0 : 1)
                target.real_believer[p] += 1
                target.propagated = true

    is_holiday:
        turn % 2 == 0

    finish:
        for l in languages:
            best_players = players.max_by(p -> l.real_believer[p])
            for p in best_players:
                p.victory_point += h.attention / best_players.size

            worst_players = players.min_by(p -> l.real_believer[p])
            for p in worst_players:
                p.victory_point -= h.attention / worst_players.size

        winners = players.max_by(p -> p.victory_point)
        draw if winners.size > 1
