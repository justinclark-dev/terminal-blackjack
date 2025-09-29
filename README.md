<pre>
 ____    _      ____    ____    _   _        _   ____    ____    _   _
|  _ \  | |    /  _ \  /  _ \  | | / /      | | /  _ \  /  _ \  | | / /
| | \ | | |    | | | | | | \_\ | |/ /       | | | | | | | | \_\ | |/ /
| |_/ / | |    | |_| | | |     |   /        | | | |_| | | |     | / /
|  _  \ | |    |  _  | | |     |   \    _   | | |  _  | | |     |   \
| | \ | | |    | | | | | |  _  | |\ \  | |  | | | | | | | |  _  | |\ \
| |_/ | | |___ | | | | | |_/ / | | \ \ \ \__/ / | | | | | |_/ / | | \ \
|_____/ |_____||_| |_| \____/  |_|  \_\ \____/  |_| |_| \____/  |_|  \_\

                           .-------..-------.
                           |A      ||10     |
                           |   ♠   ||   ♥   |
                           |      A||     10|
                           '-------''-------'
</pre>

# READ ME

## SUMMARY
We didn't use ChatGPT for very much, we used it for the deck obect (deck.js)... which we ended up not using, then we used it for the card design and the basic rules for the game. We tried to implement the basic rules to the best that we could for the time we had available, and that is where we spent the majority of our time together on Friday with no additional time to collaborate over the weekend.

For our first few itterations we focused on buiding the game with just using prompts and printing text, later we added the card printing and lastly the title.

## GAME FLOW
For the flow of the game we started with a fuction to create a card object "dealCard()". The function created cards at random and returned a card object with a rank and a suit. We then built a function to build a hand of cards "buildHand(). This created an array of two cards by calling the dealCard() function, assigning each card to the hand array, then the hand array was returned by the function. Next we focused on the "gamePlay()" which is the main logic for controlling the game. We initialized the game by building a game obect to control our game data. The main game data where the dealerHand and playerHand properties, and the dealerHandValue and playerHandValue properites. The later two properties used a helper function called "evaluateHand()" that was used to create logic to handle adding the card values according to the numbered cards and the lettered cards, including how to handle the aces, which in the end returned the calculated value of the hand it was passed in.  We itterated by building in the rules, and then testing the game play flow. Later we added the ascii card design, and the ability to keep playing after winning or losing a round, and then lastly the ability to make gamble.

## CARD ART
Displaying the ascii card art was broken down into two functions. One that creates each individual card "createCard()", and one that prints all the cards in each hand "printCards()". The createCard() function takes in 2 paramaters (rank, suit) and returns an array of text for sections of the card. Originally, the function just returned a single string of text for each card, and when the printCards() function was called it printed each card vertically on top of each other. We wanted to instead display the all the cards for each, the dealer and player, horizontally. However, since each card is created of five rows of text. We needed to devise a way of spliting each card up by it's vertical sections in the createCard() function and build each deck by recombining the card sections in the proper order. So we played returning the card sections as an array of it's vertical parts and used a simple for loop to recreate the hand of cards to display... though this part took many tries before finally getting it correct. Also, after successfully displying the player and dealer cards horizontally, I looked up ANSI escape codes for text color and the background color for the terminal to make the cards look better.

## CHAT GPT
Here was our ChatGPT use:

  For creating the ascii cards:

      .-------.   .-------.   .-------.   .-------.
      |A      |   |10     |   |K      |   |Q      |
      |   ♠   |   |   ♦   |   |   ♥   |   |   ♣   |
      |      A|   |     10|   |      K|   |      Q|
      '-------'   '-------'   '-------'   '-------'
  
  The deck object in "deck.js": (which we ended up not using)

      const deck = [
        // Hearts
        { suit: 'Hearts', rank: 'A', value: 1 },
        { suit: 'Hearts', rank: '2', value: 2 },
        ...
        { suit: 'Spades', rank: 'K', value: 13 }
      ];

  For the rule of the game:
    `
      Blackjack (also called 21) is one of the most popular casino card games. The rules are straightforward, but strategy and decisions make it exciting. Here’s a breakdown of the rules:

      Objective
      * The goal is to have a hand value closer to 21 than the dealer’s without going over 21 (busting).
      * If you bust, you automatically lose the round, even if the dealer busts too.

      Card Values
      * Number cards (2–10): Face value (e.g., 7 = 7 points).
      * Face cards (J, Q, K): 10 points each.
      * Aces (A): Can be worth 1 or 11—whichever benefits your hand without busting.

      Setup
      1. Each player places a bet.
      2. Dealer gives two cards to each player and two to themselves:
         * One dealer card is face up (the "upcard"),
         * The other is face down (the "hole card").

      Player Actions
      After the initial deal, each player decides what to do:
      * Hit: Take another card.
      * Stand: Keep your current total; end your turn.
      * Double Down: Double your bet, take one more card only, then stand.
      * Split: If you have two cards of the same value, you can split them into two hands (requires another bet).
      * Surrender (optional rule): Give up half your bet immediately and end your hand (not always offered).

      Dealer Rules
      * Dealer reveals their hole card after all players finish.
      * Dealer must hit until their hand totals at least 17.
        * Some casinos require the dealer to hit on soft 17 (Ace + 6 = 17).
      * Dealer must stand on totals of 17 or higher (unless above rule applies).

      Winning
      * If you have a higher total than the dealer without busting, you win and are paid 1:1 (bet $10, win $10).
      * Blackjack (Ace + 10-value card on first deal): Pays 3:2 (bet $10, win $15).
      * If dealer and player tie, it’s a push (bet returned).
      * If dealer busts, all remaining players win.

      Optional Side Rules
      * Insurance: If the dealer's upcard is an Ace, players can bet half their original bet as insurance against the dealer having Blackjack. Pays 2:1 if dealer has it.
      * Even Money: If you have Blackjack and the dealer shows an Ace, you can take even money (1:1) instead of risking a push.
    `

  I tried to get ChatGPT to create the word Blackjack in ascii, but didn't like the results.

  <pre>   
       ____  _      _     _      _        _    
      | __ )| | __ | |   | |    (_)  __ _| | __
      |  _ \| |/ / | |   | |    | | / _` | |/ /
      | |_) |   <  | |___| |___ | || (_| |   < 
      |____/|_|\_\ |_____|_____|/ | \__,_|_|\_\

      BBBBB   L      AAA    CCCC   K  K   JJJJ    AAA    CCCC   K  K
      B   B   L     A   A  C       K K      J    A   A  C       K K 
      BBBB    L     AAAAA  C       KK       J    AAAAA  C       KK  
      B   B   L     A   A  C       K K    J J    A   A  C       K K 
      BBBBB   LLLLL A   A   CCCC   K  K    JJ    A   A   CCCC   K  K
    
  </pre>
  
  So I created my own manually:

  <pre>
   ____    _      ____    ____    _   _        _   ____    ____    _   _
  |  _ \  | |    /  _ \  /  _ \  | | / /      | | /  _ \  /  _ \  | | / /
  | | \ | | |    | | | | | | \_\ | |/ /       | | | | | | | | \_\ | |/ /
  | |_/ / | |    | |_| | | |     |   /        | | | |_| | | |     | / /
  |  _  \ | |    |  _  | | |     |   \    _   | | |  _  | | |     |   \
  | | \ | | |    | | | | | |  _  | |\ \  | |  | | | | | | | |  _  | |\ \
  | |_/ | | |___ | | | | | |_/ / | | \ \ \ \__/ / | | | | | |_/ / | | \ \
  |_____/ |_____||_| |_| \____/  |_|  \_\ \____/  |_| |_| \____/  |_|  \_\

  </pre>