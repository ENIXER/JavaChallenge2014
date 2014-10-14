# Lang Wars - JavaChallenge 2014 *TBD*

*THIS DOCUMENT IS STILL BETA!*

## Overview of Game

You are programmer.
Let's propagandize programming languages and increase the population of the programming languages.
Overreach rivals and become the pontiff of programming languages!

## Pseudo Code of Game Rule

If you want to read the game rule in a programming language, please see [pseudo code](#PseudoCode).

## Goal of Game

Gain more _victory points_ calculated by the number of believers of each programming language than them of the other players.

## Flow of Game

There are four players and eight programming languages.

Lang Wars is a turn-based game. Players _propagate_ their favorite programming languages and gather believers.
Because players' actions are partially hidden, it is important that bargaingin with each other.

Games end in 10 turns, then players gain victory points corresponding to the number of believers of programing languages.
The player who gatherd the most number of the believers of a programming language gains the victory points corresponding to the language, in contrast, the player who gatherd the least number of the believers of a programming language loses the victory points corresponding to the language.
Thus, players should propagate favorite programming languages and gather more believers than the other players, and also, propagate the other programming languages to prevent losing victory points.
The player who gains the most victory points will win!

## Game Start

The game system set random integers (3-6) to _attention degree_ and reveal them to players at the beginning.
The higher attention degree a programming languages has, the more victory point the plyaer who gatherd the most/least number of the believers of the language gains/loses.

## Flow of Turn

There are both a workday turn and a holiday turn.
The first turn is workday. Workday and holiday turns will alternately change.
In other words, a week consists of two turns, odd turn is workday and even turn is holiday.
Players simultaneously select propagating programming languages.
They select programming languages five times in a workday turn, in contrast, they select programming languages two times in a holiday turn.
Players can select a programming language a propagation, then the number of the believers corresponing to the programming language rises one.
Players can freely allocate the number of propagations to programming languages.
For example, a player can propagate five programming languages or the same programming language five times in a workday turn.
When multiple players propagate the same programming language, it doesn't affect on increase in the number of believers.
In other words, increase in the number of believers is processed independently on duplicated selection.

The number of the believers corresponding to selected programming languages after all plyaers select propagating langugaes.
When the turn is workday, who propagates which programming language is revealed.
When the turn is holiday, which programming languages are propagated one or more times is revealed.

The following table indicates the propagation feature in a workday turn and a holiday turn.

|                                                 | Workday | Holiday |
| ----------------------------------------------- | ------- | ------- |
| Propagation times                               | 5       | 2       |
| Number of increased believers per a propagation | 1       | 1       |
| Release of propagation information              | ALL     | Presence or absence of propagation for each programming language |

## End of Game

After 10 turns, the game ends and victory points are calculated.

The player who gatherd the most/least number of the believers of a programming language gains/loses the attension degree of the language as victory points.
When multiple players gathered the most/least number of the believers, they gain/lose the attension degree divided by the number of the players.

After victory points of all the programming languages are calcuated, the player who gained the most victory points wins.
When there are multiple players gained the most victory points, the game ends in a draw.

## Input Format of AI Programs

AI programs are executed at the start of the game.
AI programs should write `READY` to the standard output and read the settings of game.

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

    programming_language = (attention, revealed_believers[4], real_believers[4])

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
            display_to_all_players(l.revealed_believers)
            if not is_holiday:
                display_to_all_players(l.propagated)
            h.propagated = 0

        for p in players:
            for i in [1 .. (is_holiday ? 2 : 5)]:
                target = languages[p.selected[i]]
                target.revealed_believers[p] += (is_holiday ? 0 : 1)
                target.real_believers[p] += 1
                target.propagated += 1

    is_holiday:
        turn % 2 == 0

    finish:
        for l in languages:
            best_players = players.max_by(p -> l.real_believers[p])
            for p in best_players:
                p.victory_points += h.attention / best_players.size

            worst_players = players.min_by(p -> l.real_believers[p])
            for p in worst_players:
                p.victory_points -= h.attention / worst_players.size

        winners = players.max_by(p -> p.victory_points)
        draw if winners.size > 1
