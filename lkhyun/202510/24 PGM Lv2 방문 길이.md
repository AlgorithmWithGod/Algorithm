```python
def solution(dirs):
    answer = 0
    history = set()
    posX = 0
    posY = 0
    for dir in dirs:
        if(dir == 'L'):
            if posX == -5: continue
            history.update([(posX,posY,posX-1,posY),(posX-1,posY,posX,posY)])
            posX -= 1
        elif(dir == 'R'):
            if posX == 5: continue
            history.update([(posX,posY,posX+1,posY),(posX+1,posY,posX,posY)])
            posX += 1
        elif(dir == 'U'):
            if posY == 5: continue
            history.update([(posX,posY,posX,posY+1),(posX,posY+1,posX,posY)])
            posY += 1
        elif(dir == 'D'):
            if posY == -5: continue
            history.update([(posX,posY,posX,posY-1),(posX,posY-1,posX,posY)])
            posY -= 1
    return len(history)/2
```
