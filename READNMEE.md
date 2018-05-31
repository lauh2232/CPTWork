import random

separator = '-' * 20
spaces = [None] * 90
c_l_spaces = {r'slid down a snake ~~~: ': [[14, 3], [20, 15], [39, 33],[66, 53],[69, 58], [79, 67], [84, 71], [88,36]],'climbed up a ladder |=|': [[6, 17],[24, 26], [30, 44],[49, 62], [82, 86]]}
print("Do you want to begin?")
print("Type YES or NO")
a=input()
if a=='YES':
    print('Okay! Beginning your game...')
    print(' ')
elif a=='NO':
    print('Okay,Come back later')
if a =='YES':
    print('In your bedroom you see a light behind your closet.')
    print('You then peak in the closet and you get sucked into ')
    print('a dark and scary forest. The door closes behind you ')
    print('and automatically locks you in. You are now trapped! ')
    print('In order to escape you have to travel fifty blocks but ')
    print('beware of all the obstacles that you may encounter. ')
    print('First to escape from the forest leads them back to ')
    print('their house.')
    print("Type START to start")
input()
class Player:

    def __init__(self, number):
        self.number = number
        self.space = 0

    def move(self, roll):
        global spaces
        if (self.space + roll) > 90:
            return (1, 'Your roll would move you off the game board.You remain at space {0}.'.format(self.space))
        elif (self.space + roll) == 90:
            return (0, 'You moved to the last space. You won the game!')
        else:
            self.space += roll
            try:
                space_type = spaces[self.space - 1][0]
                self.space = spaces[self.space - 1][1]
            except TypeError:
                return (1, 'You moved to space {0}.'.format(self.space))
            else:
                return (1, 'You {0} to space {1}!'.format(space_type,self.space))
 
def roll_die():
    roll = random.randint(1, 6)
    print('You rolled {0}.'.format(roll))
    return roll

def populate_game_board():
    global spaces
    for key, values in c_l_spaces.items():
        for space in values:
            spaces[space[0] - 1] = [key, space[1]]

def initialize_players():
    while True:
        try:
            num_players = int(input('Enter the number of players trapped in the closet: '))
        except ValueError:
            print('You have entered an invalid response.n')
        else:
            if num_players == 0:
                print('You have quit the game.')
                return
            elif 1 <= num_players <= 4:
                break
            elif (num_players < 0) or (num_players > 4):
                print('You have entered an invalid number of players.n')

    players = []
    for num in range(num_players):
        players.append(Player(num + 1))

    return players

def start_game(players):
    game = 1
    while game:
        for player in players:
            print('Player {0}'.format(player.number))
            print('You are currently on space {0}.'.format(player.space))
            game_update = player.move(roll_die())
            import random
            for i in range(1,10):
                ops = ['+']
            num1 = random.randint(10,100)
            num2 = random.randint(10,100)
            operation = random.choice(ops)

            answer=int(input(str(num1) + operation + str(num2) + '='))
            sum =num1+num2

            if (answer==sum):
                print('Correct Move the number of steps to rolled')
            if (answer!=sum):
                print('Incorrect!Stay where you are.')

def initialize_game():
    global game_information
    players = initialize_players()
    if players:
        populate_game_board()
    start_game(players)
if __name__ == '__main__':
    initialize_game()
