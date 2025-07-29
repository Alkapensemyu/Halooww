File: src/main.py

import pygame from config import * from player import Player

pygame.init() screen = pygame.display.set_mode((WIDTH, HEIGHT)) pygame.display.set_caption("PixelQuest") clock = pygame.time.Clock()

player = Player(100, 100)

running = True while running: screen.fill((0, 0, 0))

for event in pygame.event.get():
    if event.type == pygame.QUIT:
        running = False

keys = pygame.key.get_pressed()
player.update(keys)
player.draw(screen)

pygame.display.flip()
clock.tick(FPS)

pygame.quit()

File: src/config.py

WIDTH = 800 HEIGHT = 600 FPS = 60 PLAYER_SPEED = 5

File: src/player.py

import pygame from config import *

class Player: def init(self, x, y): self.image = pygame.image.load("assets/characters/hero.png") self.rect = self.image.get_rect() self.rect.topleft = (x, y)

def update(self, keys):
    if keys[pygame.K_LEFT]:
        self.rect.x -= PLAYER_SPEED
    if keys[pygame.K_RIGHT]:
        self.rect.x += PLAYER_SPEED
    if keys[pygame.K_UP]:
        self.rect.y -= PLAYER_SPEED
    if keys[pygame.K_DOWN]:
        self.rect.y += PLAYER_SPEED

def draw(self, surface):
    surface.blit(self.image, self.rect)

File: requirements.txt

pygame==2.5.2

File: README.md

PixelQuest

PixelQuest adalah game petualangan bergaya pixel art. Kamu akan bermain sebagai pahlawan pixel yang menjelajahi dunia berbahaya!

Cara Menjalankan

pip install -r requirements.txt
python src/main.py

Kontrol

Panah ← ↑ → ↓ untuk bergerak

Tambahkan fitur serang di versi berikutnya!


Lisensi

Open source untuk tujuan pembelajaran.


---

Note: Jangan lupa

