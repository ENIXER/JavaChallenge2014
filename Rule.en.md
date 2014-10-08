# Lang Wars - JavaChallenge 2014 *TBD*

*THIS DOCUMENT IS STILL BETA!*

## Overview of Game

You are programmer.
Let's propagandize programming languages and increase the number of believers of the programming languages.
Overreach rivals and become the pontiff of programming languages!

## Pseudo Code of Game Rule

If you want to read the game rule in a programming language, please see [pseudo code](#PseudoCode).

## Goal of Game

Get more _victory points_, which are calculated with the number of believers of each programming language, than other players.

## Flow of Game

There are four players and eight programming languages.

Lang Wars is a turn-based game. Players _propagandize_ their favorite programming languages and gather believers.
Because players' actions are partially hidden, it is important that bargaingin with each other.

Games end in 10 turns, then players gain victory points corresponding to the number of believers of programing languages.
The player who gathered the most number of the believers of a programming language gets the victory points of the language, in contrast, the player who gathered the least number of the believers of a programming language loses the victory points of the language.
Thus, players should propagate favorite programming languages and gather more believers than the other players, and also, propagate the other programming languages to prevent losing victory points.
The player who gains the most victory points will win!

## Game Start

The game system set random _attention degree_ (from 3 to 6) to every programming language, and reveal them to players at the beginning.
A language with higher attention degree has more victory points. Players who gathered the most/least number of believers of this language will gain/lose more victory points.

## Flow of Turn

There are two types of turns, workday turn and holiday turn.
The first turn is workday. Workday and holiday turns will alternately appear.
In other words, two turns is one week, odd turn is workday and even turn is holiday.
Players simultaneously select propagating programming languages.
They select programming languages five times in a workday turn, and two times in a holiday turn.
Players select a programming language to propagate one time, will gather one believer of that language.
Players can freely choose which programming languages to propagate.
For example, players can choose five programming languages to propagate each one time, or propagate the same programming language five times in a workday turn.
In addition, players propagate the same programming language with others, will not influence others to gather believers.

The number of the believers of each programming language will be calculated after all players select propagating languages.
If the turn is workday, which player propagates which programming language is revealed.
If the turn is holiday, only how many times each programming language is propagated is revealed.

The following table indicates the propagation feature in a workday turn and a holiday turn.

|                                                 | Workday | Holiday |
| ----------------------------------------------- | ------- | ------- |
| Propagation times                               | 5       | 2       |
| Number of believers gathered per propagation    | 1       | 1       |
| Revelation of propagation information           | ALL     | For each programming language, number of propagation times|

## End of Game

After 10 turns, the game ends and victory points are calculated.

The player who gathered the most/least number of the believers of a programming language gains/loses the attention degree of the language as victory points.
When multiple players gathered the most/least number of the believers, they gain/lose the attention degree divided by the number of the players.

After victory points of all the programming languages are calculated, the player who gained the most victory points wins.
When there are multiple players gained the most victory points, the game ends in a draw.

## Input Format of AI Programs

AI programs are executed at the start of the game.
AI programs should print `READY` to the standard output and read the settings of game.
Then, AI programs read current propagation information of each turn, and print the selected languages.

The Thinking time of AI is limited.
If an AI program exceeds the limited thinking time, it will be terminated by force and its behavior will be regarded as "select language 0 always" until the end.

### Output Format of Ready Message

When the AI programs prepared for the game, they must print `READY` to the standard output.
Note that, the ready message must be printed within 5 seconds from game start, otherwise the AI program will be terminated by force.

### Input Format of Game Settings

When the game starts (before the 1st turn), game system sends settings to every AI program through the standard input.
The format of settings are listed as following:

<pre>
T P N
A<sub>0</sub> A<sub>1</sub> A<sub>2</sub> ... A<sub>7</sub>
</pre>

* T: The number of all turns.
* P: The number of players.
* N: The number of programming language.
* A<sub>n</sub>: The attention degree of language n.

### Input Format of Turn Information

At the beginning of each turn, current information was sent through the standard input with following format:

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

* T: Current turn. (starts from 1)
* D: "W" stand for workday turn, "H" stand for holiday turn.
* B<sub>nm</sub>: The visible number (only counting the believers gathered in workday turn) of believers of programming language n gathered by player m. The play 0 is your AI program.
* R<sub>n</sub>: Your real number of believers of program n (counting the believers gathered in both workday and holiday turn).
* P<sub>n</sub>: Whether the programming language n was propagated in the previous holiday turn. 1 means propagated, 0 means not.

The last line (P<sub>0</sub> P<sub>1</sub> P<sub>2</sub> ... P<sub>7</sub>) is only revealed in workday turn.

### Output format of Actions

Print the propagating language to the standard output with following format:

* __Workday Turn__

  <pre>
  L<sub>0</sub> L<sub>1</sub> L<sub>2</sub> L<sub>3</sub> L<sub>4</sub>
  </pre>
  
* __Holiday Turn__

  <pre>
  L<sub>0</sub> L<sub>1</sub>
  </pre>

L<sub>n</sub>: The number of propagating programming language (from 0 to 7). The order of L<sub>0</sub> to L<sub>4</sub> is not concerned.

Once an AI program prints its action, its turn finished.
Note that, if an AI program does not print its action within 1 second from the beginning of a turn, it will be terminated by force.

<a name="PseudoCode"></a>

## Pseudo Code of Game Rule

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
            l.propagated = false

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
