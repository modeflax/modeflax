import pygame
import random

# Initialize Pygame
pygame.init()

# Set up the screen
screen_width = 800
screen_height = 600
screen = pygame.display.set_mode((screen_width, screen_height))
pygame.display.set_caption("Free Fire Clone")

# Set up colors
WHITE = (255, 255, 255)
RED = (255, 0, 0)
GREEN = (0, 255, 0)
BLUE = (0, 0, 255)

# Set up player
player_width = 50
player_height = 50
player_x = screen_width // 2 - player_width // 2
player_y = screen_height - player_height - 10
player_speed = 5
player = pygame.Rect(player_x, player_y, player_width, player_height)

# Set up enemy
enemy_width = 50
enemy_height = 50
enemy_x = random.randint(0, screen_width - enemy_width)
enemy_y = random.randint(50, 150)
enemy_speed = 3
enemy = pygame.Rect(enemy_x, enemy_y, enemy_width, enemy_height)

# Game loop
running = True
while running:
    screen.fill(WHITE)
    
    # Event handling
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
    
    # Player movement
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT] and player_x > 0:
        player_x -= player_speed
    if keys[pygame.K_RIGHT] and player_x < screen_width - player_width:
        player_x += player_speed
    player.left = player_x
    
    # Enemy movement
    enemy.y += enemy_speed
    if enemy.y > screen_height:
        enemy.x = random.randint(0, screen_width - enemy_width)
        enemy.y = random.randint(50, 150)
    
    # Collision detection
    if player.colliderect(enemy):
        running = False
    
    # Draw player and enemy
    pygame.draw.rect(screen, GREEN, player)
    pygame.draw.rect(screen, RED, enemy)
    
    pygame.display.flip()

pygame.quit()
