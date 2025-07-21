Here’s a simple Python game using the `pygame` library. It’s a basic **“Dodge the Enemy”** game where the player controls a square that moves left and right to avoid falling blocks.

### 🔹 Requirements:

Make sure you have `pygame` installed. You can install it with:

```bash
pip install pygame
```

---

### 🕹️ Simple Python Game Code

```python
import pygame
import random

# Initialize Pygame
pygame.init()

# Screen settings
WIDTH, HEIGHT = 500, 600
screen = pygame.display.set_mode((WIDTH, HEIGHT))
pygame.display.set_caption("Dodge the Enemy")

# Colors
WHITE = (255, 255, 255)
PLAYER_COLOR = (50, 205, 50)
ENEMY_COLOR = (255, 0, 0)

# Player settings
player_size = 50
player_pos = [WIDTH // 2, HEIGHT - player_size]
player_speed = 10

# Enemy settings
enemy_size = 50
enemy_pos = [random.randint(0, WIDTH-enemy_size), 0]
enemy_speed = 5

# Game loop flag
running = True
clock = pygame.time.Clock()

# Main Game Loop
while running:
    screen.fill(WHITE)

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Movement
    keys = pygame.key.get_pressed()
    if keys[pygame.K_LEFT] and player_pos[0] > 0:
        player_pos[0] -= player_speed
    if keys[pygame.K_RIGHT] and player_pos[0] < WIDTH - player_size:
        player_pos[0] += player_speed

    # Move enemy
    enemy_pos[1] += enemy_speed
    if enemy_pos[1] > HEIGHT:
        enemy_pos[1] = 0
        enemy_pos[0] = random.randint(0, WIDTH - enemy_size)

    # Collision Detection
    if (
        enemy_pos[1] < player_pos[1] + player_size and
        enemy_pos[1] + enemy_size > player_pos[1] and
        enemy_pos[0] < player_pos[0] + player_size and
        enemy_pos[0] + enemy_size > player_pos[0]
    ):
        print("Game Over!")
        running = False

    # Draw player and enemy
    pygame.draw.rect(screen, PLAYER_COLOR, (*player_pos, player_size, player_size))
    pygame.draw.rect(screen, ENEMY_COLOR, (*enemy_pos, enemy_size, enemy_size))

    pygame.display.update()
    clock.tick(30)

pygame.quit()
```

---

### ✅ Features:

* Arrow key controls (left/right)
* One falling enemy block
* Ends game when you collide with the enemy
