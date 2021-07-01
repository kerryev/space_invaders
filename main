import pygame
import random
import math

pygame.init()  # Initialize the pygame
screen = pygame.display.set_mode((800, 600))  # Display is created

# How to chnage caption, logo, title, background colour
pygame.display.set_caption('Space Invaders')
icon = pygame.image.load('launch.png')
pygame.display.set_icon(icon)

# Background

background = pygame.image.load('bb.jpg')

# Player
playerImg = pygame.image.load('ship.png')
playerX = 370
playerY = 480
playerX_change = 0

# Enemy
enemyImg = []
enemyX = []
enemyY = []
enemyX_change = []
enemyY_change = []
numofenemies = 6
for i in range(numofenemies):
    enemyImg.append(pygame.image.load('space-ship.png'))
    enemyX.append(random.randint(1, 736))
    enemyY.append(random.randint(50, 150))
    enemyX_change.append(0.2)
    enemyY_change.append(40)

# Bullet
bulletImg = pygame.image.load('bullet.png')
bulletX = 0
bulletY = 480
bulletX_change = 0
bulletY_change = 0.7
bullet_state = "ready"

# Score
score = 0
font = pygame.font.Font('freesansbold.ttf', 32)
textX = 10
textY = 10


def show_score(x, y):
    scoretext = font.render('Score: ' + str(score), True, (255, 255, 255))
    screen.blit(scoretext, (x, y))


def player(x, y):
    screen.blit(playerImg, (x, y))


def enemy(x, y, i):
    screen.blit(enemyImg[i], (x, y))


def firebullet(x, y):
    global bullet_state
    bullet_state = "fire"
    screen.blit(bulletImg, (x + 16, y + 10))


def iscollision(enemyX, enemyY, bulletX, bulletY):
    distance = math.sqrt(math.pow(enemyX - bulletX, 2) +
                         math.pow(enemyY-bulletY, 2))
    if distance < 40:
        return True
    else:
        return False


# GAME LOOP
running = True
while running == True:
    #rbg = red, green, blue
    screen.fill((0, 0, 0))
    # Backgroud image
    screen.blit(background, (0, 0))
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        # Checks for keystroke
        if event.type == pygame.KEYDOWN:
            if event.key == pygame.K_LEFT:
                playerX_change = - 0.5
            if event.key == pygame.K_RIGHT:
                playerX_change = 0.5
            if event.key == pygame.K_SPACE:
                if bullet_state == "ready":
                    bulletX = playerX
                    firebullet(playerX, bulletY)
        if event.type == pygame.KEYUP:
            if event.key == pygame.K_LEFT or event.key == pygame.K_RIGHT:
                playerX_change = 0
    # Player movements and boundaries
    playerX += playerX_change
    if playerX <= 0:
        playerX = 0
    if playerX >= 736:
        playerX = 736

    # Enemy movements and boundaries
    for i in range(numofenemies):
        enemyX[i] += enemyX_change[i]
        if enemyX[i] <= 0:
            enemyX_change[i] += 0.1
            enemyY[i] += enemyY_change[i]
        elif enemyX[i] >= 736:
            enemyX_change[i] -= 0.1
            enemyY[i] += enemyY_change[i]
        # Collision
        collision = iscollision(enemyX[i], enemyY[i], bulletX, bulletY)
        if collision:
            bulletY = 480
            bullet_state = "ready"
            score += 1
            enemyX[i] = random.randint(1, 736)
            enemyY[i] = random.randint(50, 150)

        enemy(enemyX[i], enemyY[i], i)

    # Bulet movement
    if bulletY <= 0:
        bulletY = 480
        bullet_state = "ready"
    if bullet_state == "fire":
        firebullet(bulletX, bulletY)
        bulletY -= bulletY_change

    player(playerX, playerY)
    show_score(textX, textY)
    pygame.display.update()
