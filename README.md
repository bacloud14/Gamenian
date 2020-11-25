# Outscore Card Game

"Outscore" Card Game is a novel card game out of my imagination. I believe most viable and loved card games have these properties:

- Easy to learn rules and an intuitive goal
- Open possibilies for endless fun and also skills improvement 
- Chance assures: 
    - An entertaining partie.
    - Players cannot predict a win at anytime in a partie.
- Uses common and cheap tools (like the standard 52-card dec, domino tiles, stones and sticks, etc.).

## Properties and goals of "Outscore"

### A Trick-taking games

The object of a trick-taking game is based on the play of multiple rounds, or tricks, in each of which each player plays a single card from their hand, and based on the values of played cards one player wins or "takes" the trick. The specific object varies with each game and can include taking as many tricks as possible, taking as many scoring cards within the tricks won as possible, taking as few tricks (or as few penalty cards) as possible, taking a particular trick in the hand, or taking an exact number of tricks. Bridge, Whist, Euchre, 500, Spades, and the various Tarot card games are popular examples. [Wikipedia]

## Goal

- The goal in "Outscore" is to simply have the biggest accumulated score (sum) at the end of a partie. It is a mix of chance, feeling and reflexion; In other words: Two exposed hands at game start cannot conclude the winner but can say one seems to be luckier.

- To understand the "win propertie" before diving into rules, let's imagine the game is 100% chance; Assuming this, having two hands without gameplay we can conclude scores like the following:

We sum and compare two hands simply with these weights: `Ace->1 , 1->1, ..., Jack->11, Queen->12, King->13`.

The hand with the biggest sum is the winner. Easy! This is like a preschool kids scoring right :( ? well, rules in fact are as easy as this but but brings more intertaining to the game :) ; Just follow up with me.

## Rules, gameplay and strategy:

### Codification and language:

To ease our latin language and for possible machine implementation, let's admit the following mini language:

`P_i` is player i for example P_1 is player 1

`Cd_Num` is one card in {Ace, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10} cards no matter the suits: clubs (♣), diamonds (♦), hearts (♥) or spades (♠).

`Cd_Face` is one card in {Jack, Queen, King} cards no matter the suits: clubs (♣), diamonds (♦), hearts (♥) or spades (♠).

`P_i::Cd` is a "Pplay": it is one move (facing up a card) of two opponents at one time. `P_i::Cd` is in `{P_i::Cd_Num, P_i::Face}`.

`[P_i::##, P_j::##]` is one play. For example 
- `[P_1::Cd_Num, P_2::Cd_Face]` is a play with player 1 playing `Cd_Num` card and player 2 playing `Cd_Face` card
- `[P_1::Cd_Num*, P_2::Cd_Face*]` is a play with player 1 playing only `Cd_Num` cards and player 2 playing only `Cd_Face` cards in an ongoing round 

`Round_i` is the i(th) round, (first, second, ...). A Round determines one win for one player; The winner takes a plus score and the loser conserves his previsous score (of `Round_(i-1)`).

`Score_i` is a score that goes to the winner after `Round_i`. It is the cumulative sum of `[Score_0, Score_1, ..., Score_i]`.

`P_i_Score` is the accumulated score for player i.

*A "round" can be more than two "plays".*

Let's explain a "round" in a two oppenents version:

### Rules and gameplay

The game starts with two hands. Players choose sequentially one card from hand and face it up one after the other.
A one round can be one of the followings:

- `[Pi::Cd_Num, Pj..Cd_Num]` is a one play round with the lowest Num is added to the opponent score *while cards go to the table.*
- `[Pi::Cd_Face, Pj..Cd_Face]` is a one play round with the lowest Face card goes to the opponent hand *and not to the table.*
- `[Pi::Cd_Num, Pj..Cd_Face]` or `[Pi::Cd_Face, Pj..Cd_Num]` are not sufficient for a round unless it is the last possible play. Another play is needed (this is a tie play and the round is not dealt).
- A round with more than one play is critical, to win, we only compare `Cd_Face` and `Cd_Num` respectively, with the lowest `Cd_Face` winning the highest `Cd_Face` (going to the winner's hand) and the highest `Cd_Num` winning the lowest `Cd_Num` (going to the winner score). In this case, It is never a win round, but a win of `Cd_Num` scores to one player, and a win of `Cd_Face` to the other. It is not a tie if and only if one player has a mix of `Cd_Num` and `Cd_Face` cards.
- If it is a tie play -with `[P_i::Cd_Num*, P_j::Cd_Face*]` and there are no more cards in hands for at least one player, it is still a tie round (`Round_n`). It is a final tie round and score is maintained (`Round_n-1`).

## Strategy

 - For each play, in each round, (at any moment of gameplay) a player feels he will be winning and tries to maximize score, or feels he will be losing and tries to lower the score for the current round or for the whole game partie.
 - One strategy for player A is to feel the growing greed of player B; When player B is becoming greedy he may want to come up with big scoring cards (`Cd_Face` mostly); Player A would absorb the push by coming up with low cards (low `Cd_Num` mostly).
 - When player A feels winning the game and wants to maintain the current score, he may want to continue plays yielding a tie round; With the risk of losing a lot !

-to be continued
