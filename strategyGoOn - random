from random import*
from numpy import*
from math import*

pieces = zeros((2, 4), int) 
piecesInGame = []
piecesInGame.append([])
piecesInGame.append([])


def firstMove(pieces, piecesInGame, number):
    counter = 3
    dice = 0
    while (counter > 0):
        dice = randint(1, 6)
        if (dice == 6):
            piece = randint(0, 3)
            pieces[number][piece] = 1
            piecesInGame[number].append(piece)
            pieces[number][piece] += randint(1, 6)
            toRemove = pieces[number][piece]
            for i in range(4):
                if(i in piecesInGame):
                    if(abs(pieces[((number+1)%2)][i] - toRemove) == 22):
                        pieces[((number+1)%2)][i] = 0
                        piecesInGame[((number+1)%2)].remove(i)
                        break
            break
        else:
            counter -= 1
    return counter
    

def strategyGoOn(pieces, piecesInGame, number, finish):
    piece = choice(piecesInGame[number])
    pieces[number][piece] += 6
    toRemove = pieces[number][piece]
    for i in range(4):
        if(i in piecesInGame):
            if(abs(pieces[(number+1)%2][i] - toRemove) == 22):
                pieces[((number+1)%2)][i] = 0
                piecesInGame[(number+1)%2].remove(i)
                break
    if((pieces[number][piece]) > 43):
        finish[number] += 1
        piecesInGame[number].remove(piece)
    dice = randint(1, 6)
    return dice


def strategyComeOut(pieces, piecesInGame, number):
    piece = 0
    for piece in range(4):
        if(pieces[number][piece] == 0):
            break;
    pieces[number][piece] = 1
    piecesInGame[number].append(piece)
    toRemove = 1
    for i in range(4):
        if(i in piecesInGame):
            if(abs(pieces[(number+1)%2][i] - toRemove) == 22):
                pieces[(number+1)%2][i] = 0
                piecesInGame[(number+1)%2].remove(i)
                break
        
    
def game(pieces, piecesInGame, number, finish):
    if(len(piecesInGame[number]) != 0):
        dice = randint(1, 6)
        flag = 1
        while(flag == 1):
            if(len(piecesInGame[number]) != 0):
                if(dice != 6):
                    flag = 0
                    piece = choice(piecesInGame[number])
                    pieces[number][piece] += dice
                    toRemove = pieces[number][piece]

                    if((pieces[number][piece]) > 43):
                        finish[number] += 1
                        piecesInGame[number].remove(piece)
                        
                    for i in range(4):
                        if(i in piecesInGame):
                            if(abs(pieces[(number+1)%2][i] - toRemove) == 22):
                                pieces[(number+1)%2][i] = 0
                                piecesInGame[(number+1)%2].remove(i)
                                break
                else:
                    s = 0
                    for i in range(4):
                        if(pieces[number][i] != 0):
                           s += 1
                    if(s != 4):
                        nb = randint(0, 1)
                        if(number == 0):
                            nb = 1
                        if(nb == 0):
                            strategyComeOut(pieces, piecesInGame, number)
                            flag = 0
                        else:
                            dice = strategyGoOn(pieces, piecesInGame, number, finish)
                    else:
                        dice = strategyGoOn(pieces, piecesInGame, number, finish)
            else:
                firstMove(pieces, piecesInGame, number)
    else:
        firstMove(pieces, piecesInGame, number)
                    

finish = [0, 0]

counter1 = 0
counter2 = 0
i = 0
j = 0
noWins = 0

for i in range (10000):
    finish = [0, 0]

    while(max(finish[0], finish[1])<4):
        if(counter1 == 0):
            counter1 = firstMove(pieces, piecesInGame, 0)
        else:
            game(pieces, piecesInGame, 0, finish)

        if(counter2 == 0):
            counter2 = firstMove(pieces, piecesInGame, 1)
        else: 
            game(pieces, piecesInGame, 1, finish)
    if(finish[0]==4):
        noWins += 1

print noWins        
