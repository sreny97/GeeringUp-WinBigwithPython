import random

# ------------------- CLASSES --------------------
class Card:
  def __init__(self, suit, rank, value):
    self.suit = suit
    self.rank = rank
    self.value = value

class Player:
  def __init__(self, name):
    self.name = name
    self.points = 0

class Dealer:
  def __init__(self):
    self.points = 0

# ------------------- FUNCTIONS ------------------
def createPlayer():
  print('Enter your name: ')
  name = input()
  print()
  print("Hello, " + name + '.')
  player = Player(name)
  return player

def newCard():
  # randomly generate the suit (doesn't matter for Blackjack)
  suit = random.randint(1,4)
  if (suit == 1):
    suit = "Hearts"
  elif (suit == 2):
    suit = "Diamonds"
  elif (suit == 3):
    suit = "Clubs"
  elif (suit == 4):
    suit = "Spades"

  # randomly generate the rank to determine point value
  number = random.randint(1,13)
  if (number == 11):
    rank = "J"
    value = 10
  elif (number == 12):
    rank = "Q"
    value = 10
  elif (number == 13):
    rank = "K"
    value = 10
  elif (number == 1):
    rank = "A"
    value = 11
  else:
    rank = number
    value = number
    
  # pass the suit and value to the card
  return Card(suit, rank, value)

def dealCards(player, dealer):
  print("Dealing cards...")
  print()

  # player's cards
  cardP1 = newCard()
  cardP2 = newCard()
  player.points = cardP1.value + cardP2.value

  # dealer's cards
  cardD1 = newCard()
  cardD2 = newCard()
  dealer.points = cardD1.value + cardD2.value

  # say what cards the dealer has
  print("The dealer has the " + str(cardD1.rank) + " of " + cardD1.suit + " and their other card is face down.")
  print()

  # say what cards we have
  print("You have the " + str(cardP1.rank) + " of " + cardP1.suit + " and the " + str(cardP2.rank) + " of " + cardP2.suit + '.')
  print("Your have " + str(player.points) + " points.")
  print()

  return cardD2

def playerHit(player):
  cardPN = newCard()
  player.points += cardPN.value
  print("Your new card is the " + str(cardPN.rank) + " of " + cardPN.suit + '.')
  print("Your have " + str(player.points) + " points.")

def playerStand(player, dealer, cardD2):
  # first, reveal the dealer's face down card
  print("The dealer flips their other card over. It is the " + str(cardD2.rank) + " of " + cardD2.suit + '.')
  print("The dealer has " + str(dealer.points) + " points.")
  print()

  # dealer takes new cards until they are over 17 points
  while (dealer.points < 17):
    dealerHit(dealer)

  # dealer has stopped, now see who wins
  if (dealer.points > 21):
    print("Dealer has more then 21 points! You win!")
    print()
  elif (dealer.points == 21):
    print("Dealer has Blackjack! You lose.")
    print()
  elif (dealer.points > player.points):
    print("Dealer has " + str(dealer.points) + " points and you have " + str(player.points) + " points. You lose.")
    print()
  elif (dealer.points < player.points):
    print("Dealer has " + str(dealer.points) + " points and you have " + str(player.points) + " points. You win!")
    print()
  elif (dealer.points == player.points):
    print("You both have " + str(dealer.points) + " points! No one wins.")
    print()
  else:
    # should never get to this (logically impossible)
    print("ERROR")
    print()

def dealerHit(dealer):
  cardDN = newCard()
  dealer.points += cardDN.value
  print("The dealer takes the " + str(cardDN.rank) + " of " + cardDN.suit + '.')
  print("The dealer now has " + str(dealer.points) + " points.")
  print()

def playBlackjack(player, dealer):
  # why don't we want to do this?
  '''
  player = Player(name)
  dealer = Dealer()
  '''

  # reset everyone's points
  player.points = 0
  dealer.points = 0

  # deal cards, keeping the dealer's hidden card
  cardD2 = dealCards(player, dealer)

  while(True):
    # first check if you are over 21 points
    if (player.points > 21):
      print("You have more than 21 points! You lose.")
      print()
      break

    # if you have Blackjack
    if (player.points == 21):
      # must also check if dealer has Blackjack as well
      if (dealer.points == 21):
        print("Both of you have Blackjack! No one wins.")
        print()
        break
      else:
        print("You have Blackjack! You win!")
        print()
        break

    # otherwise (you are less than 21 points)
    else:
      # ask if the player wants another card
      print("Would you like another card? (Y/N)")
      answer = input()
      print()

      if (answer == "Y"):
        # "hit" the player with a new card
        playerHit(player)
      else:
        # the player stops, now it is the dealer's turn
        playerStand(player, dealer, cardD2)
        # exit the while loop to end the game
        break

def startGame():
  # create the player
  player = createPlayer()

  # create the dealer
  dealer = Dealer()

  # keep playing as long as the player wants
  while(True):
    print("Would you like to play Blackjack? (Y/N)")
    answer = input()
    print()

    if (answer == "Y"):
      playBlackjack(player, dealer)
    else:
      break

# play the game!
startGame()