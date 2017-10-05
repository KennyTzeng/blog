---
title: '[Python]使用Pygame製作小遊戲'
catalog: true
date: 2017-07-30 18:09:12
subtitle:
header-img: "Post_header_img.png"
tags:
- "Python"
- "Pygame"
categories:
- "Python"
---

# [Python]使用Pygame製作小遊戲

&emsp;&emsp;今天要介紹的是用`Pygame`實作的一款小遊戲，[Pygame](http://www.pygame.org/wiki/about)是Python中一個免費且開源的library，支援鍵盤滑鼠輸入、聲音、圖像、文字等，適合拿來製作多媒體應用程式如遊戲，在[Pygame-GettingStarted](http://www.pygame.org/wiki/GettingStarted)中有各作業系統的安裝方式。
&emsp;&emsp;其實原本是想練習寫寫看Python的圖形視窗介面，Python有內建的模組`Tkinter`可使用，但功能較陽春因此適合作為較靜態的視窗應用程式，要做遊戲還是交給`Pygame`或其他模組吧！

&emsp;&emsp;它是一款類似彈珠台的遊戲，球會在空中快速前進、碰到牆會反彈，每隔一段時間球速便會提高，我們要做的是用滑鼠控制平台不讓球掉下去，時間越久分數越高分。

&emsp;&emsp;首先先把完整的程式碼貼上來，部分的解說待有空時補充還請見諒，程式的流程大致上是用while不斷循環，每次先檢查是否有收到系統事件(包含自定義的事件，例如球速提高)，之後便根據球的方向與速度更新位置，更新後馬上檢查是否有撞到牆或平台要反彈、或是碰到底部要Game Over出現分數與提示字樣，最後刷新畫面。
&emsp;&emsp;程式參考了[Github這篇](https://github.com/20021307/Pygame/tree/master/reaction_game)(感謝嗚嗚)，並且有用到相關字體檔與圖片檔，完整的專案檔案可以在[我的Github](https://github.com/KennyTzeng/pygame_ball)中檢視。

```python
import sys
import pygame

# pygame init
pygame.init()
pygame.display.set_caption("Reaction Game")

# window size
window_size = (window_width, window_height) = (400, 600)
# color
black = (0, 0, 0)
white = (255, 255, 255)
# logic control boolean 
game = True
round = True
# fonts
small_font = pygame.font.Font("bold.ttf", 18)
# score control
start_time = 0

# init objects
screen = pygame.display.set_mode(window_size)
clock = pygame.time.Clock()

ball = pygame.image.load("small-ball.png")
ballRect = ball.get_rect()
platform = pygame.image.load("small-platform.png")
platformRect = platform.get_rect()

def text_on_screen(text, color, y_displacement=0):
    
    textSurface = small_font.render(text, True, color, None)
    textRect = textSurface.get_rect()
    textRect.center = (int(window_width / 2), y_displacement)
    screen.blit(textSurface, textRect)

def calcScore(game_time):
    global start_time
    return game_time - start_time

def gameOver(game_time):
    global game
    global round
    # disable the level up timer
    pygame.time.set_timer(24, 0)
    text_on_screen("Game Over", white, 100)
    text_on_screen("Your score is : {}".format(calcScore(game_time)), white, 200)
    text_on_screen("Press 'r' to restart", white, 400)
    text_on_screen("Press 'q' to leave", white, 450)

    while round:
        for event in pygame.event.get():
            if event.type == pygame.QUIT: sys.exit()
            if event.type == pygame.KEYDOWN:
                if event.key == pygame.K_r:
                    round = False
                if event.key == pygame.K_q:
                    round = False
                    game = False

        clock.tick(60)
        pygame.display.flip()

def main():

    # element attribute
    global round
    round = True
    global start_time
    start_time = pygame.time.get_ticks()

    # define event.type = 24 to present level up per 10 seconds
    pygame.time.set_timer(24, 10000)

    ball_speed = 4
    ball_direction = [1, 1]
    ball_pos = [0, 0]
    platform_pos = [0, 0]

    ballRect.top = 1
    ballRect.left = 1
    platformRect.center = [0, 500]

    while round:
        for event in pygame.event.get():
            if event.type == 24:
                ball_speed = ball_speed + 1
                print("level up")
            if event.type == pygame.QUIT: sys.exit()
        
        for i in range(ball_speed):
            
            ball_pos = [(ballRect.left + ballRect.right)/2, (ballRect.top + ballRect.bottom)/2]
            mouse_pos = pygame.mouse.get_pos()
            platformRect.center = [mouse_pos[0], 500]
            ballRect.move_ip([ball_direction[0], ball_direction[1]])

            if ballRect.bottom == platformRect.top and platformRect.left <= ball_pos[0] <= platformRect.right:
                ball_direction[1] = -ball_direction[1]
                print("nice catch")
            elif platformRect.colliderect(ballRect):
                ball_direction[0] = -ball_direction[0]
                print("oops")   
            if ballRect.left < 0 or ballRect.right > window_width:
                ball_direction[0] = -ball_direction[0]
            if ballRect.top < 0:
                ball_direction[1] = -ball_direction[1]
            if ballRect.bottom > window_height:
                # game over
                gameOver(pygame.time.get_ticks())
                break
            
        screen.fill(black)
        screen.blit(ball, ballRect)
        screen.blit(platform, platformRect)
        clock.tick(60)
        pygame.display.flip()
    
if(__name__ == "__main__"):
    while game:
        main()
```