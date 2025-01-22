# Flappy-bird
import pygame
import random

pygame.init()

screen = pygame.display.set_mode((800, 600))
pygame.display.set_caption("Flappy Bird")
clock = pygame.time.Clock()
font = pygame.font.Font(None, 36)
font2 = pygame.font.Font(None, 72)


score = 0




class Bird:
    def __init__(self):
        self.y = 400
        self.velocity = 0

    def flap(self):
        self.velocity = -3

    def physics(self):
        self.velocity += 0.1
        self.y += self.velocity

    def draw(self):
        pygame.draw.rect(screen, (255, 0, 0), (50, self.y, 30, 30))

bird = Bird()

class Pipe:
    def __init__(self, x):
        self.x = x
        self.height = random.randint(50, 400)
        self.gap = 150

    def move(self):
        self.x -= 2

    def draw(self):
        #top pipe
        pygame.draw.rect(screen, (0, 225, 0), (self.x, 0, 50, self.height))
        #bottom pipe
        pygame.draw.rect(screen, (0, 225, 0), (self.x, self.height + self.gap, 50, 600 - (self.height + self.gap)))

pipes = []
spawn_pipe = 0
       
def check_collision(bx, by, px, py):
    #top pipe check
    if bx + 30 > px and bx < px + 50 and by < py:
        return True
    #bottom pipe check
    if bx + 30 > px and bx < px + 50 and by + 30 > py + 150:
        return True
    return False

ticker = 0
running = True
while running: #======================Game Loop+++++++++++++++++++++++++++++++++++++++++
    clock.tick(60)
    ticker += 1
    if ticker%10 == 0:
        ticker = 0
        score += 1
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False
        if event.type == pygame.MOUSEBUTTONDOWN:
            bird.flap()
           

           
