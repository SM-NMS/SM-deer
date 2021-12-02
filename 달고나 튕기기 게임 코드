import pygame

#랜덤 함수 지정
import random

pygame.init()

A= random.randint(1,3)  # 1 이상 3이하의 정수 난수

background = pygame.display.set_mode((1600, 900)) # 파이게임 창 크기 
pygame.display.set_caption("달고나 튕기기 게임")         # 게임 이름 지정

# 배경 및 게임구성요소 이미지 로드
image_bg = pygame.image.load("image/배경.png")
image_dalgona = pygame.image.load("image/네모.png")
image_dog = pygame.image.load("image/개.png")

# 배경 크기
size_bg_width = background.get_size()[0]   
size_bg_height = background.get_size()[1]

# 달고나 크기
size_dalgona_width = image_dalgona.get_rect().size[0]
size_dalgona_height = image_dalgona.get_rect().size[1]

# 달고나 위치
x_pos_dalgona = size_bg_width/2 - size_dalgona_width/2 # 배경의 가운데에서 달고나 시작
y_pos_dalgona = 0

# 달고나의 초기 속도를 임의로 지정하는 구간

x_speed_dalgona = 5 
y_speed_dalgona = 5

# 개의 크기
size_dog_width = image_dog.get_rect().size[0]
size_dog_height = image_dog.get_rect().size[1]

# 개의 위치
x_pos_dog = size_bg_width/2 - size_dog_width/2 # 배경의 가운데에서 개 시작
y_pos_dog = size_bg_height - size_dog_height # 배경의 바닥 부분에서 개 시작

to_x = 0

point = 0 # 시작 점수
font_point = pygame.font.SysFont(None,150) # 점수 폰트 및 크기

# 게임 승리 표시
font_gameend = pygame.font.SysFont(None,250) 
text_gameend = font_gameend.render('You   Win',True,(0,0,255)) 

size_text_width = text_gameend.get_rect().size[0]    # 게임 승리 텍스트 크기 
size_text_height = text_gameend.get_rect().size[1]

x_pos_text = size_bg_width/2-size_text_width/2         # 게임 승리 텍스트 표시 위치 
y_pos_text = size_bg_height/2-size_text_height/2

# 게임오버 표시
font_gameover = pygame.font.SysFont(None,200) 
text_gameover = font_gameover.render('Game Over',True,(255,0,0))

size_text_width = text_gameover.get_rect().size[0]    # 게임오버 텍스트 크기
size_text_height = text_gameover.get_rect().size[1]

x_pos_text = size_bg_width/2-size_text_width/2        # 게임오버 텍스트 표시 위치
y_pos_text = size_bg_height/2-size_text_height/2

play = True  
while play:
    for event in pygame.event.get():         # 닫기 누르면 게임 종료
        if event.type == pygame.QUIT:        
            play = False
        if event.type == pygame.KEYDOWN:        # 키보드로 개 조종
            if event.key == pygame.K_RIGHT:
                to_x = 10                    # 방향키를 눌렀을 때 개의 이동 범위를 지정
            if event.key == pygame.K_LEFT:
                to_x = -10                   # 방향키를 눌렀을 때 개의 이동 범위를 지정

        if event.type == pygame.KEYUP:
            if event.key == pygame.K_RIGHT:
                to_x = 0
            elif event.key == pygame.K_LEFT:
                to_x = 0

    if x_pos_dog<0:                              # 개가 움직이는 범위 설정
        x_pos_dog = 0
    elif x_pos_dog>size_bg_width-size_dog_width:
        x_pos_dog =size_bg_width-size_dog_width
    else:
        x_pos_dog += to_x

# 달고나 벽에 튕기기
    x_pos_dalgona += x_speed_dalgona 
    y_pos_dalgona += y_speed_dalgona

    if x_pos_dalgona <= 0:
        x_speed_dalgona = -x_speed_dalgona
        x_pos_dalgona = 0
    elif x_pos_dalgona >= size_bg_width-size_dalgona_width:
        x_speed_dalgona = -x_speed_dalgona
        x_pos_dalgona = size_bg_width-size_dalgona_width

    if y_pos_dalgona <=0:
        y_speed_dalgona = -y_speed_dalgona  
        y_pos_dalgona = 0
    elif y_pos_dalgona >= size_bg_height-size_dalgona_height:   
        background.blit(text_gameover, (x_pos_text,y_pos_text))
        pygame.display.update()
        pygame.time.delay(800)         # 게임 종료 지연

        play = False
     
    if point ==  10:                 # 점수 10점 이상이면 승리 텍스트 표시 후 종료
        background.blit(text_gameend, (x_pos_text, y_pos_text))
        pygame.display.update()
        pygame.time.delay(800)                
                        
        play = False  

# 개와 달고나의 충돌   
    rect_dalgona = image_dalgona.get_rect()  # 달고나 직사각형 모양
    rect_dalgona.left = x_pos_dalgona
    rect_dalgona.top = y_pos_dalgona

    rect_dog = image_dog.get_rect()        # 개 직사각형 모양
    rect_dog.left = x_pos_dog
    rect_dog.top = y_pos_dog

    if rect_dog.colliderect(rect_dalgona):
         x_speed_dalgona = -x_speed_dalgona
         y_speed_dalgona = -y_speed_dalgona
         point += 1
         x_speed_dalgona = point*A+5 #개 개와 달고나가 닿았을 때 달고나의 속도가 증가 

# blit()함수로 화면에 이미지 표시 
    background.blit(image_bg, (0, 0))
    background.blit(image_dalgona, (x_pos_dalgona, y_pos_dalgona))
    background.blit(image_dog, (x_pos_dog, y_pos_dog))

# 점수 입력
    text_point = font_point.render(str(point),True,(0,0,0))
    background.blit(text_point, (10,10))
 
    pygame.display.update()
    
pygame.quit()  # while문 종료 후 게임 종료

