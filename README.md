import random
import pygame
from pygame import *
from random import randint

clock = pygame.time.Clock()

pygame.init()
screen = pygame.display.set_mode((1200, 700))
pygame.display.set_caption("Ghost")
icon = pygame.image.load('game 2/icons/icon.png').convert_alpha()
pygame.display.set_icon(icon)

# PLAYER
walk = [
    transform.scale(image.load('game 2/player/player_walk/walk1.png').convert_alpha(), (48, 48)),
    transform.scale(image.load('game 2/player/player_walk/walk2.png').convert_alpha(), (48, 48)),
    transform.scale(image.load('game 2/player/player_walk/walk3.png').convert_alpha(), (48, 48)),
    transform.scale(image.load('game 2/player/player_walk/walk4.png').convert_alpha(), (48, 48)),
    transform.scale(image.load('game 2/player/player_walk/walk5.png').convert_alpha(), (48, 48)),
    transform.scale(image.load('game 2/player/player_walk/walk6.png').convert_alpha(), (48, 48)),
    transform.scale(image.load('game 2/player/player_walk/walk7.png').convert_alpha(), (48, 48)),
    transform.scale(image.load('game 2/player/player_walk/walk8.png').convert_alpha(), (48, 48)),
    transform.scale(image.load('game 2/player/player_walk/walk9.png').convert_alpha(), (48, 48)),
    transform.scale(image.load('game 2/player/player_walk/walk10.png').convert_alpha(), (48, 48))
]
a_walk = 9

jump = [
    transform.scale(image.load('game 2/player/player_jump/pryzhok1.png').convert_alpha(), (48, 48)),
    transform.scale(image.load('game 2/player/player_jump/pryzhok2.png').convert_alpha(), (48, 48)),
    transform.scale(image.load('game 2/player/player_jump/pryzhok3.png').convert_alpha(), (48, 48)),
    transform.scale(image.load('game 2/player/player_jump/pryzhok4.png').convert_alpha(), (48, 48)),
    transform.scale(image.load('game 2/player/player_jump/pryzhok5.png').convert_alpha(), (48, 48)),
    transform.scale(image.load('game 2/player/player_jump/pryzhok6.png').convert_alpha(), (48, 48)),
    transform.scale(image.load('game 2/player/player_jump/pryzhok7.png').convert_alpha(), (48, 48))
]
a_jump = 6

player_anim_count = 0
player_anim_jump_count = 0
player_speed = 5
player_x = 15
player_y = 145

is_Jump = False
J_count = 9

# SKINS
player_costum1 = transform.scale(image.load('game 2/player/skin1/walk/walk1.png').convert_alpha(), (40, 60))

player_costum2 = transform.scale(image.load('game 2/player/skins/hat2.png').convert_alpha(), (45, 45))
player_costum3 = transform.scale(image.load('game 2/player/skins/witch hat2.png').convert_alpha(), (40, 40))
hat = False

player_costum4 = transform.scale(image.load('game 2/life/heart.png').convert_alpha(), (20, 20))

player_costum5 = transform.scale(image.load('game 2/fire/fireball.png').convert_alpha(), (25, 25))
player_costum6 = transform.scale(image.load('game 2/fire/sword.png').convert_alpha(), (45, 45))
player_costum7 = transform.scale(image.load('game 2/fire/rifle.png').convert_alpha(), (60, 60))

# ENEMY
enemy = pygame.image.load('game 2/enemy/enemy.png').convert_alpha()
enemy_timer = pygame.USEREVENT + 1
pygame.time.set_timer(enemy_timer, 2500)
enemy_list_in_game = []
enemy_speed = 10

# BOSSES
mini_boss1 = pygame.image.load('game 2/bosses/miniboss1.png').convert_alpha()
mini_boss1_timer = pygame.USEREVENT + 2
pygame.time.set_timer(mini_boss1_timer, 10000)
mini_boss1_list = []
mini_boss1_count = 0
mini_boss1_life = 5
mini_boss1_speed = 4
mini_boss1_flag = False

bomb = pygame.image.load('game 2/bosses/fire_boss/bomb.png').convert_alpha()
bombs_mini_boss1 = []
bombs_boss = []
bombs_final_boss = []

bomb_mini_boss1_timer = pygame.USEREVENT + 3
pygame.time.set_timer(bomb_mini_boss1_timer, 5000)
bomb_boss_timer = pygame.USEREVENT + 4
pygame.time.set_timer(bomb_boss_timer, 5000)
bomb_final_boss_timer = pygame.USEREVENT + 5
pygame.time.set_timer(bomb_final_boss_timer, 5000)

bomb_mini_boss1_x = 0
bomb_boss_x = 0
bomb_final_boss_x = 0
bomb_mini_boss1_speed = 20
bomb_boss_speed = 20
bomb_final_boss_speed = 15

boss = pygame.image.load('game 2/bosses/boss.png').convert_alpha()
boss_timer = pygame.USEREVENT + 6
pygame.time.set_timer(boss_timer, 25000)
boss_list = []
boss_life = 20
boss_count = 0
boss_speed = 3
boss_flag = False

final_boss = pygame.image.load('game 2/bosses/finalboss.png').convert_alpha()
final_boss_list = []
final_boss_life = 20
final_boss_speed = 3
final_boss_flag = False
win_flag = False

rain = transform.scale(image.load('game 2/bosses/fire_boss/skull.png').convert_alpha(), (60, 60))

rains = []
rain_timer = pygame.USEREVENT + 7
pygame.time.set_timer(rain_timer, 5000)
rain_y = 0
rain_speed = 5

rains_2 = []
rain_2_timer = pygame.USEREVENT + 8
pygame.time.set_timer(rain_2_timer, 6000)
rain_2_y = 0
rain_2_speed = 5

rains_3 = []
rain_3_timer = pygame.USEREVENT + 9
pygame.time.set_timer(rain_3_timer, 7000)
rain_3_y = 0
rain_3_speed = 5

rains_4 = []
rain_4_timer = pygame.USEREVENT + 10
pygame.time.set_timer(rain_4_timer, 8000)
rain_4_y = 0
rain_4_speed = 5

rains_5 = []
rain_5_timer = pygame.USEREVENT + 11
pygame.time.set_timer(rain_5_timer, 9000)
rain_5_y = 0
rain_5_speed = 5

# FIRE
bullet = pygame.image.load('game 2/fire/fireball.png').convert_alpha()
bullets = []
bullets_amount = 7
bul_distance = 45
bul_speed = 5

sword = pygame.image.load('game 2/fire/sword.png').convert_alpha()
swords = []
swords_amount = 2
sword_time = 500

rifle = transform.scale(image.load('game 2/fire/rifle.png').convert_alpha(), (32, 32))
rifles = []
rifles_amount = 1
rifle_time = 5000

rifle_bullet = transform.scale(image.load('game 2/fire/bullet.png').convert_alpha(), (20, 20))
rifle_bullets = []
rifle_bullets_amount = 3
rifle_bullet_speed = 5

# BOX
box = transform.scale(image.load('game 2/boxs/box.png').convert_alpha(), (55, 55))
boxs = []
boxs_speed = 10
box_timer = pygame.USEREVENT + 12
pygame.time.set_timer(box_timer, 50000)

# COIN
coin = pygame.image.load('game 2/coins/coin.png').convert_alpha()
coins = []
coin_amount = 0
coin_speed = 10
coin_timer = pygame.USEREVENT + 13
pygame.time.set_timer(coin_timer, 20000)

# LIFE
life = pygame.image.load('game 2/life/heart.png').convert_alpha()
life_count = 3

# BACKGROUND
bg = pygame.image.load('game 2/bg/фон.jpg').convert()
bg_x = 0
bg_speed = 10

menu_bg = transform.scale(image.load('game 2/menu/menu_bg.png').convert_alpha(), (1200, 700))

# SHOP
shop = transform.scale(image.load('game 2/shop/полкидлямагазина.jpg'), (1200, 700))
shop_x = 0

# SOUND
# main_sound = pygame.mixer.Sound('game 2/sounds/164b99c10472d02.mp3')
# main_sound.play()

# LABEL
label = pygame.font.Font('game 2/text/DMSans-Regular.ttf', 30)
label1 = pygame.font.Font('game 2/text/DMSans-Regular.ttf', 13)

# RESTART_LABEL and RESTART_FLAG
restart_label = label.render('RESTART', True, (255, 255, 255))
restart_label_rect = restart_label.get_rect(topleft=(900, 450))

restart_flag = False

# MENU_LABEL and MENU_FLAG
menu_label = label.render('MENU', True, (255, 255, 255))
menu_label_rect = menu_label.get_rect(topleft=(200, 450))
menu1_label_rect = menu_label.get_rect(topleft=(960, 550))

menu_flag = True

# START_LABEL
start_label = label.render('START', True, (0, 0, 0))
start_label_rect = start_label.get_rect(topleft=(140, 150))

# SHOP_LABEL and SHOP_FLAG
shop_label = label.render('SHOP', True, (0, 0, 0))
shop_label_rect = shop_label.get_rect(topleft=(144, 350))

shop_flag = False

# EXIT_LABEL
exit_label = label.render('EXIT', True, (0, 0, 0))
exit_label_rect = exit_label.get_rect(topleft=(1100, 630))

# GAME
gr = pygame.image.load('game 2/game over/gameoverlabel.jpg').convert()
game_count = 0

gameplay = False

# PAY_FLAGS
pay_1 = False
pay_2 = False
pay_3 = False
pay_4 = False
pay_5 = False
pay_6 = False
pay_7 = False

# PAUSE_FLAG and PAUSE_LABEL
pause_flag = 0
pause_label = label.render('PAUSE', True, (0, 0, 0))
pause_label_rect = pause_label.get_rect(topleft=(320, 250))


flag = True
while flag:
    keys = pygame.key.get_pressed()
    if keys[pygame.K_p]:
        pause_flag = True
    if keys[pygame.K_o]:
        pause_flag = False
        gameplay = True
    mouse = pygame.mouse.get_pos()

    if menu_flag:
        restart_flag = False
        gameplay = False
        shop_flag = False

        screen.blit(menu_bg, (0, 0))
        screen.blit(start_label, start_label_rect)
        screen.blit(shop_label, shop_label_rect)
        screen.blit(exit_label, exit_label_rect)

        if start_label_rect.collidepoint(mouse) and pygame.mouse.get_pressed()[0]:
            gameplay = True

        elif shop_label_rect.collidepoint(mouse) and pygame.mouse.get_pressed()[0]:
            shop_flag = True

        elif exit_label_rect.collidepoint(mouse) and pygame.mouse.get_pressed()[0]:
            flag = False

    if shop_flag:
        menu_flag = False
        gameplay = False
        restart_flag = False

        screen.blit(shop, (shop_x, 0))

        screen.blit(menu_label, menu1_label_rect)

        if menu1_label_rect.collidepoint(mouse) and pygame.mouse.get_pressed()[0]:
            menu_flag = True

        screen.blit(player_costum1, (228, 110))
        skin1_label = label1.render('5', True, (0, 0, 0))
        skin1_label_rect = skin1_label.get_rect(topleft=(233, 172))
        pygame.draw.rect(screen, (255, 255, 255), ((228, 170), (32, 20)))
        screen.blit(skin1_label, skin1_label_rect)
        screen.blit(coin, (240, 172))

        screen.blit(player_costum2, (225, 263))
        skin2_label = label1.render('2', True, (0, 0, 0))
        skin2_label_rect = skin2_label.get_rect(topleft=(237, 305))
        pygame.draw.rect(screen, (255, 255, 255), ((231, 303), (32, 20)))
        screen.blit(skin2_label, skin2_label_rect)
        screen.blit(coin, (243, 305))

        screen.blit(player_costum3, (227, 390))
        skin3_label = label1.render('5', True, (0, 0, 0))
        skin3_label_rect = skin3_label.get_rect(topleft=(237, 437))
        pygame.draw.rect(screen, (255, 255, 255), ((231, 435), (32, 20)))
        screen.blit(skin3_label, skin3_label_rect)
        screen.blit(coin, (243, 437))

        screen.blit(player_costum4, (961, 145))
        skin4_label = label1.render('8', True, (0, 0, 0))
        skin4_label_rect = skin4_label.get_rect(topleft=(960, 172))
        pygame.draw.rect(screen, (255, 255, 255), ((955, 170), (32, 20)))
        screen.blit(skin4_label, skin4_label_rect)
        screen.blit(coin, (968, 172))

        screen.blit(player_costum5, (959, 273))
        skin5_label = label1.render('10', True, (0, 0, 0))
        skin5_label_rect = skin5_label.get_rect(topleft=(959, 303))
        pygame.draw.rect(screen, (255, 255, 255), ((956, 301), (32, 20)))
        screen.blit(skin5_label, skin5_label_rect)
        screen.blit(coin, (970, 303))

        screen.blit(player_costum6, (959, 392))
        skin6_label = label1.render('10', True, (0, 0, 0))
        skin6_label_rect = skin6_label.get_rect(topleft=(965, 440))
        pygame.draw.rect(screen, (255, 255, 255), ((960, 438), (39, 20)))
        screen.blit(skin6_label, skin6_label_rect)
        screen.blit(coin, (980, 440))

        screen.blit(player_costum7, (573, 502))
        skin7_label = label1.render('15', True, (0, 0, 0))
        skin7_label_rect = skin7_label.get_rect(topleft=(586, 565))
        pygame.draw.rect(screen, (255, 255, 255), ((582, 563), (39, 20)))
        screen.blit(skin7_label, skin7_label_rect)
        screen.blit(coin, (600, 565))

        pygame.draw.rect(screen, (255, 255, 255), ((40, 50), (38, 22)))
        coins_count_label = label1.render(': ' + str(coin_amount), True, (0, 0, 0))
        screen.blit(coin, (40, 52))
        screen.blit(coins_count_label, (60, 52))

        if skin1_label_rect.collidepoint(mouse) and pygame.mouse.get_pressed()[0] and coin_amount >= 5:
            coin_amount -= 5
            walk = [
                transform.scale(image.load('game 2/player/skin1/walk/walk1.png').convert_alpha(), (40, 60)),
                transform.scale(image.load('game 2/player/skin1/walk/walk2.png').convert_alpha(), (40, 60)),
                transform.scale(image.load('game 2/player/skin1/walk/walk3.png').convert_alpha(), (40, 60)),
                transform.scale(image.load('game 2/player/skin1/walk/walk4.png').convert_alpha(), (40, 60)),
                transform.scale(image.load('game 2/player/skin1/walk/walk5.png').convert_alpha(), (40, 60)),
                transform.scale(image.load('game 2/player/skin1/walk/walk6.png').convert_alpha(), (40, 60)),
                transform.scale(image.load('game 2/player/skin1/walk/walk7.png').convert_alpha(), (40, 60)),
                transform.scale(image.load('game 2/player/skin1/walk/walk8.png').convert_alpha(), (40, 60)),
                transform.scale(image.load('game 2/player/skin1/walk/walk9.png').convert_alpha(), (40, 60))
            ]
            a_walk = 8

            jump = [
                transform.scale(image.load('game 2/player/skin1/jump/jump1.png').convert_alpha(), (40, 60)),
                transform.scale(image.load('game 2/player/skin1/jump/jump2.png').convert_alpha(), (40, 60)),
                transform.scale(image.load('game 2/player/skin1/jump/jump3.png').convert_alpha(), (40, 60)),
                transform.scale(image.load('game 2/player/skin1/jump/jump4.png').convert_alpha(), (40, 60)),
                transform.scale(image.load('game 2/player/skin1/jump/jump5.png').convert_alpha(), (40, 60)),
                transform.scale(image.load('game 2/player/skin1/jump/jump6.png').convert_alpha(), (40, 60)),
                transform.scale(image.load('game 2/player/skin1/jump/jump7.png').convert_alpha(), (40, 60)),
                transform.scale(image.load('game 2/player/skin1/jump/jump8.png').convert_alpha(), (40, 60)),
                transform.scale(image.load('game 2/player/skin1/jump/jump9.png').convert_alpha(), (40, 60)),
                transform.scale(image.load('game 2/player/skin1/jump/jump10.png').convert_alpha(), (40, 60)),
                transform.scale(image.load('game 2/player/skin1/jump/jump11.png').convert_alpha(), (40, 60)),
                transform.scale(image.load('game 2/player/skin1/jump/jump12.png').convert_alpha(), (40, 60))
            ]
            a_jump = 11
            hat = True
            pay_1 = True
        if pay_1:
            skin1_label1 = label1.render('sale', True, (0, 0, 0))
            skin1_label1_rect = skin1_label1.get_rect(topleft=(232, 172))
            pygame.draw.rect(screen, (255, 255, 255), ((228, 170), (32, 20)))
            screen.blit(skin1_label1, skin1_label1_rect)

        if skin2_label_rect.collidepoint(mouse) and pygame.mouse.get_pressed()[0] and coin_amount >= 2:
            coin_amount -= 2
            pay_2 = True
            hat = True
        if pay_2:
            skin2_label2 = label1.render('sale', True, (0, 0, 0))
            skin2_label2_rect = skin2_label2.get_rect(topleft=(235, 305))
            pygame.draw.rect(screen, (255, 255, 255), ((231, 303), (32, 20)))
            screen.blit(skin2_label2, skin2_label2_rect)

        if skin3_label_rect.collidepoint(mouse) and pygame.mouse.get_pressed()[0] and coin_amount >= 5:
            coin_amount -= 5
            pay_3 = True
        if pay_3:
            skin3_label3 = label1.render('sale', True, (0, 0, 0))
            skin3_label3_rect = skin3_label3.get_rect(topleft=(235, 437))
            pygame.draw.rect(screen, (255, 255, 255), ((231, 435), (32, 20)))
            screen.blit(skin3_label3, skin3_label3_rect)

        if skin4_label_rect.collidepoint(mouse) and pygame.mouse.get_pressed()[0] and coin_amount >= 8:
            coin_amount -= 8
            life_count += 1
            pay_4 = True
        if pay_4:
            skin4_label4 = label1.render('sale', True, (0, 0, 0))
            skin4_label4_rect = skin4_label4.get_rect(topleft=(959, 172))
            pygame.draw.rect(screen, (255, 255, 255), ((955, 170), (32, 20)))
            screen.blit(skin4_label4, skin4_label4_rect)

        if skin5_label_rect.collidepoint(mouse) and pygame.mouse.get_pressed()[0] and coin_amount >= 10:
            coin_amount -= 10
            bullets_amount += 1
            pay_5 = True
        if pay_5:
            skin5_label5 = label1.render('sale', True, (0, 0, 0))
            skin5_label5_rect = skin5_label5.get_rect(topleft=(960, 303))
            pygame.draw.rect(screen, (255, 255, 255), ((956, 301), (32, 20)))
            screen.blit(skin5_label5, skin5_label5_rect)

        if skin6_label_rect.collidepoint(mouse) and pygame.mouse.get_pressed()[0] and coin_amount >= 10:
            coin_amount -= 10
            swords_amount += 1
            pay_6 = True
        if pay_6:
            skin6_label6 = label1.render('sale', True, (0, 0, 0))
            skin6_label6_rect = skin6_label6.get_rect(topleft=(967, 440))
            pygame.draw.rect(screen, (255, 255, 255), ((960, 438), (39, 20)))
            screen.blit(skin6_label6, skin6_label6_rect)

        if skin7_label_rect.collidepoint(mouse) and pygame.mouse.get_pressed()[0] and coin_amount >= 15:
            coin_amount -= 15
            rifles_amount += 1
            rifle_flag = True
            pay_7 = True
        if pay_7:
            skin7_label7 = label1.render('sale', True, (0, 0, 0))
            skin7_label7_rect = skin7_label7.get_rect(topleft=(589, 565))
            pygame.draw.rect(screen, (255, 255, 255), ((582, 563), (39, 20)))
            screen.blit(skin7_label7, skin7_label7_rect)

    if gameplay:
        menu_flag = False
        restart_flag = False

        bul_speed = 5
        rifle_bullet_speed = 5
        player_speed = 5
        enemy_speed = 10
        mini_boss1_speed = 4
        boss_speed = 3
        final_boss_speed = 3
        bomb_mini_boss1_speed = 20
        bomb_boss_speed = 20
        bomb_final_boss_speed = 15
        rain_speed = 5
        rain_2_speed = 5
        rain_3_speed = 5
        rain_4_speed = 5
        rain_5_speed = 5

        screen.blit(bg, (bg_x, 0))
        screen.blit(bg, (bg_x + 1200, 0))
        pygame.draw.line(screen, (0, 0, 0), (0, 200), (1200, 200), width=7)

        player_rect = walk[0].get_rect(topleft=(player_x, player_y))
        if hat:
            if pay_2:
                screen.blit(player_costum2, (player_x + 3, player_y - 25))
            if pay_3:
                screen.blit(player_costum3, (player_x + 3, player_y - 25))

        if enemy_list_in_game:
            for (i, enemy_i) in enumerate(enemy_list_in_game):
                screen.blit(enemy, enemy_i)
                enemy_i.x -= enemy_speed

                if enemy_i.x < -10:
                    enemy_list_in_game.pop(i)

                if player_rect.colliderect(enemy_i):
                    enemy_list_in_game.pop(i)
                    life_count -= 1

        if life:
            for j in range(life_count):
                screen.blit(life, (975 + j * 30, 0))

        if game_count % 1000 == 0 and game_count > 2 and life_count < 3:
            life_count += 1

        if life_count <= 0:
            restart_flag = True

        keys = pygame.key.get_pressed()
        if not pause_flag:
            if keys[pygame.K_LEFT] and player_x > 0:
                player_x -= player_speed
            if keys[pygame.K_RIGHT] and player_x < 1000:
                player_x += player_speed
            if not is_Jump:
                if keys[pygame.K_SPACE]:
                    is_Jump = True
            else:
                if J_count >= -9:
                    if J_count < 0:
                        player_y += (J_count ** 2) / 3
                    else:
                        player_y -= (J_count ** 2) / 3
                    J_count -= 1
                else:
                    is_Jump = False
                    J_count = 9

        if player_anim_count == a_walk:
            player_anim_count = 0
        else:
            player_anim_count += 1

        if player_anim_jump_count == a_jump:
            player_anim_jump_count = 0
        else:
            player_anim_jump_count += 1

        if player_y == 145:
            screen.blit(walk[player_anim_count], (player_x, player_y))
        else:
            screen.blit(jump[player_anim_jump_count], (player_x, player_y))

        bg_x -= bg_speed
        if bg_x == -1200:
            bg_x = 0
        game_count += 1
        game_count_label = label1.render(str(round(game_count / 5)), True, (0, 0, 0))
        screen.blit(game_count_label, (1100, 0))

        if not pause_flag:
            if bullets:
                for (i, bullet_i) in enumerate(bullets):
                    screen.blit(bullet, (bullet_i.x, bullet_i.y))
                    bullet_i.x += bul_speed
                    if bullet_i.x > player_x + 48 + bul_distance:
                        bullets.pop(i)

                    if enemy_list_in_game:
                        for (index, enemy_el) in enumerate(enemy_list_in_game):
                            if bullet_i.colliderect(enemy_el):
                                enemy_list_in_game.pop(index)
                                bullets.pop(i)
                    if mini_boss1_list:
                        for (index, mini_boss1_el) in enumerate(mini_boss1_list):
                            if bullet_i.colliderect(mini_boss1_el):
                                bullets.pop(index)
                                mini_boss1_life -= 1
                    if boss_list:
                        for (index, boss_el) in enumerate(boss_list):
                            if bullet_i.colliderect(boss_el):
                                bullets.clear()
                                boss_life -= 5
                    if final_boss_list:
                        for (index, final_boss_el) in enumerate(final_boss_list):
                            if bullet_i.colliderect(final_boss_el):
                                bullets.pop(index)
                                final_boss_life -= 5

        bullets_count_label = label1.render(': ' + str(bullets_amount), True, (0, 0, 0))
        screen.blit(bullet, (15, 0))
        screen.blit(bullets_count_label, (32, 0))

        if not pause_flag:
            if sword:
                for (i, sword_i) in enumerate(swords):
                    screen.blit(sword, (sword_i.x, sword_i.y))

                    if sword_i.x > bg_x + sword_time:  # при изменении скорости bg изменяем sword_time
                        swords.pop(i)

                    if enemy_list_in_game:
                        for (index, enemy_el) in enumerate(enemy_list_in_game):
                            if sword_i.colliderect(enemy_el):
                                enemy_list_in_game.pop(index)
                                swords.pop(i)
                    if mini_boss1_list:
                        for (index, mini_boss1_el) in enumerate(mini_boss1_list):
                            if sword_i.colliderect(mini_boss1_el):
                                swords.pop(i)
                                mini_boss1_life -= 2
                    if boss_list:
                        for (index, boss_el) in enumerate(boss_list):
                            if sword_i.colliderect(boss_el):
                                swords.clear()
                                boss_life -= 8
                    if final_boss_list:
                        for (index, final_boss_el) in enumerate(final_boss_list):
                            if sword_i.colliderect(final_boss_el):
                                swords.clear()
                                final_boss_life -= 8
        swords_count_label = label1.render(': ' + str(swords_amount), True, (0, 0, 0))
        screen.blit(sword, (0, 20))
        screen.blit(swords_count_label, (32, 28))

        if not pause_flag:
            if rifles:
                for (i, rifle_i) in enumerate(rifles):
                    screen.blit(rifle, (rifle_i.x, rifle_i.y))

                    if rifle_i.x > bg_x + rifle_time:  # при изменении скорости bg изменяем rifle_time
                        rifles.pop(i)

                    if rifle_bullets:
                        for (k, rifle_bullet_k) in enumerate(rifle_bullets):
                            screen.blit(rifle_bullet, (rifle_bullet_k.x, rifle_bullet_k.y))
                            rifle_bullet_k.x += rifle_bullet_speed
                            if rifle_bullet_k.x < -10:
                                rifle_bullets.pop(i)

                            if enemy_list_in_game:
                                for (index, enemy_el) in enumerate(enemy_list_in_game):
                                    if rifle_bullet_k.colliderect(enemy_el):
                                        rifle_bullets.pop(k)
                                        enemy_list_in_game.pop(index)
                            if mini_boss1_list:
                                for (index, mini_boss1_el) in enumerate(mini_boss1_list):
                                    if rifle_bullet_k.colliderect(mini_boss1_el):
                                        rifle_bullets.pop(k)
                                        mini_boss1_list.pop(index)
                            if boss_list:
                                for (index, boss_el) in enumerate(boss_list):
                                    if rifle_bullet_k.colliderect(boss_el):
                                        rifle_bullets.pop(k)
                                        boss_list.pop(index)
                            if final_boss_list:
                                for (index, final_boss_el) in enumerate(final_boss_list):
                                    if rifle_bullet_k.colliderect(final_boss_el):
                                        rifle_bullets.pop(k)
                                        final_boss_life -= 10
        rifle_bullets_count_label = label1.render(': ' + str(rifle_bullets_amount), True, (0, 0, 0))
        screen.blit(rifle_bullet, (8, 49))
        screen.blit(rifle_bullets_count_label, (32, 49))

        if boxs:
            box_random = randint(1, 6)
            for (i, box_i) in enumerate(boxs):
                screen.blit(box, box_i)
                box_i.x -= boxs_speed

                if box_i.x < -10:
                    boxs.pop(i)
                if player_rect.colliderect(box_i):
                    if box_random == 1:
                        swords_amount += 1
                        boxs.pop(i)
                        sword_label = label1.render('YOU GOT IT', True, (0, 0, 0))
                        sword_label1 = label1.render('.', True, (0, 0, 0))
                        screen.blit(sword_label, (600, 600))
                        screen.blit(sword, (630, 600))
                        screen.blit(sword_label1, (640, 600))
                    if box_random == 2:
                        life_count += 1
                        boxs.pop(i)
                        life_label = label1.render('YOU GOT IT', True, (0, 0, 0))
                        life_label1 = label1.render('.', True, (0, 0, 0))
                        screen.blit(life_label, (600, 600))
                        screen.blit(life, (630, 600))
                        screen.blit(life_label1, (640, 600))
                    if box_random == 3:
                        bullets_amount += 1
                        boxs.pop(i)
                        bullet_label = label1.render('YOU GOT IT', True, (0, 0, 0))
                        bullet_label1 = label1.render('.', True, (0, 0, 0))
                        screen.blit(bullet_label, (600, 600))
                        screen.blit(bullet, (630, 600))
                        screen.blit(bullet_label1, (640, 600))
                    if box_random == 4:
                        rifle_bullets_amount += 3
                        boxs.pop(i)
                        rifle_bullet_label = label1.render('YOU GOT IT', True, (0, 0, 0))
                        rifle_bullet_label1 = label1.render('.', True, (0, 0, 0))
                        screen.blit(rifle_bullet_label, (600, 600))
                        screen.blit(rifle_bullet, (630, 600))
                        screen.blit(rifle_bullet_label1, (640, 600))
                    if box_random == 5 or box_random == 6:
                        boxs.pop(i)
        if coins:
            for (i, coin_i) in enumerate(coins):
                screen.blit(coin, coin_i)
                coin_i.x -= coin_speed
                if coin_i.x < -10:
                    coins.pop(i)
                if player_rect.colliderect(coin_i):
                    coins.pop(i)
                    coin_amount += 1
        coins_count_label = label1.render(': ' + str(coin_amount), True, (0, 0, 0))
        screen.blit(coin, (150, 0))
        screen.blit(coins_count_label, (170, 0))

        if mini_boss1_list:
            bul_distance += 1000
            sword_time += 200
            enemy_list_in_game.clear()
            for (i, mini_boss1_i) in enumerate(mini_boss1_list):
                screen.blit(mini_boss1, mini_boss1_i)
                mini_boss1_i.x -= mini_boss1_speed
                bomb_mini_boss1_x = mini_boss1_i.x
                if mini_boss1_i.x < 0:
                    mini_boss1_list.clear()
                if mini_boss1_life <= 0:
                    mini_boss1_list.clear()
                    #mini_boss1_count += 1
                    mini_boss1_flag = True
                if player_rect.colliderect(mini_boss1_i):
                    mini_boss1_list.clear()
                    restart_flag = True
            if bombs_mini_boss1:
                for (i, bomb_mini_boss1_i) in enumerate(bombs_mini_boss1):
                    screen.blit(bomb, (bomb_mini_boss1_i.x, bomb_mini_boss1_i.y))
                    bomb_mini_boss1_i.x -= bomb_mini_boss1_speed

                    if bomb_mini_boss1_i.x < 0:
                        bombs_mini_boss1.pop(i)

                    if bomb_mini_boss1_i.colliderect(player_rect):
                        bombs_mini_boss1.clear()
                        life_count -= 1
                    if bullets:
                        for (index, bullet_el) in enumerate(bullets):
                            if bomb_mini_boss1_i.colliderect(bullet_el):
                                bombs_mini_boss1.clear()
                                bullets.pop(index)
                    if swords:
                        for (index, sword_el) in enumerate(swords):
                            if bomb_mini_boss1_i.colliderect(sword_el):
                                bombs_mini_boss1.clear()
                                swords.pop(index)
                    if rifle_bullets:
                        for (index, rifle_bullet_el) in enumerate(rifle_bullets):
                            if bomb_mini_boss1_i.colliderect(rifle_bullet_el):
                                bombs_mini_boss1.clear()
                                rifle_bullets.pop(index)
        #if mini_boss1_count > 2 and
        if boss_list and boss_life > 0:
            bul_distance += 1000
            sword_time += 200
            enemy_list_in_game.clear()
            mini_boss1_list.clear()
            for (n, boss_n) in enumerate(boss_list):
                screen.blit(boss, boss_n)
                if boss_n.x < 900:
                    boss_n.x += boss_speed
                if boss_n.x > 1190:
                    boss_n.x -= boss_speed
                bomb_boss_x = boss_n.x
                if boss_life <= 0:
                    boss_list.pop(n)
                    boss_count += 1
                if player_rect.colliderect(boss_n):
                    boss_list.pop(n)
                    restart_flag = True
            if bombs_boss:
                for (i, bomb_boss_i) in enumerate(bombs_boss):
                    screen.blit(bomb, (bomb_boss_i.x, bomb_boss_i.y))
                    bomb_boss_i.x -= bomb_boss_speed

                    if bomb_boss_i.x < 0:
                        bombs_boss.pop(i)

                    if bomb_boss_i.colliderect(player_rect):
                        bombs_boss.clear()
                        life_count -= 1
                    if bullets:
                        for (index, bullet_el) in enumerate(bullets):
                            if bomb_boss_i.colliderect(bullet_el):
                                bullets.pop(index)
                                bombs_boss.clear()
                    if swords:
                        for (index, sword_el) in enumerate(swords):
                            if bomb_boss_i.colliderect(sword_el):
                                bombs_boss.clear()
                                swords.pop(index)
                    if rifle_bullets:
                        for (index, rifle_bullet_el) in enumerate(rifle_bullets):
                            if bomb_boss_i.colliderect(rifle_bullet_el):
                                bombs_boss.clear()
                                rifle_bullets.pop(index)
        if boss_count == 1:
            bul_distance += 1000
            sword_time += 200
            enemy_list_in_game.clear()
            mini_boss1_list.clear()
            boss_list.clear()
            for (i, final_boss_i) in enumerate(final_boss_list):
                screen.blit(final_boss, final_boss_i)
                if final_boss_i.x < 900:
                    final_boss_i.x += final_boss_speed
                if final_boss_i.x > 1190:
                    final_boss_i.x -= final_boss_speed
                if final_boss_i.x < 0:
                    final_boss_list.pop(i)
                if final_boss_life <= 0:
                    final_boss_list.pop(i)
                    win_flag = True
                    restart_flag = False
                    shop_flag = False
                if player_rect.colliderect(final_boss_i):
                    final_boss_list.pop(i)
                    restart_flag = True
                bomb_final_boss_x = final_boss_i.x
            if bombs_final_boss:
                for (i, bomb_final_boss_i) in enumerate(bombs_final_boss):
                    screen.blit(bomb, (bomb_final_boss_i.x, bomb_final_boss_i.y))
                    bomb_final_boss_i.x -= bomb_final_boss_speed

                    if bomb_final_boss_i.x < 0:
                        bombs_final_boss.pop(i)

                    if bomb_final_boss_i.colliderect(player_rect):
                        bombs_final_boss.clear()
                        life_count -= 1
                    if bullets:
                        for (index, bullet_el) in enumerate(bullets):
                            if bomb_final_boss_i.colliderect(bullet_el):
                                bullets.pop(index)
                                bombs_final_boss.pop(i)
                    if swords:
                        for (index, sword_el) in enumerate(swords):
                            if bomb_final_boss_i.colliderect(sword_el):
                                swords.pop(index)
                                bombs_final_boss.pop(i)
                    if rifle_bullets:
                        for (index, rifle_bullet_el) in enumerate(rifle_bullets):
                            if bomb_final_boss_i.colliderect(rifle_bullet_el):
                                bombs_final_boss.pop(i)
                                rifle_bullets.pop(index)
        if rains:
            for (i, rain_i) in enumerate(rains):
                rain_rect = rain.get_rect(topleft=(rain_i.x, rain_y))
                screen.blit(rain, (rain_i.x, rain_y))
                rain_y += rain_speed

                if pygame.Rect.colliderect(player_rect, rain_rect):
                    rains.clear()
                    life_count -= 1

                if rain_y > 350: # поработать с хитбоксом
                    rains.pop(i)
                    rain_y = 0
        if rains_2:
            for (i, rain_2_i) in enumerate(rains_2):
                rain_2_rect = rain.get_rect(topleft=(rain_2_i.x, rain_y))
                screen.blit(rain, (rain_2_i.x, rain_2_y))
                rain_2_y += rain_2_speed

                if pygame.Rect.colliderect(player_rect, rain_2_rect):
                    rains_2.clear()
                    life_count -= 1

                if rain_2_y > 350: # поработать с хитбоксом
                    rains_2.pop(i)
                    rain_2_y = 0
        if rains_3:
            for (i, rain_3_i) in enumerate(rains_3):
                rain_3_rect = rain.get_rect(topleft=(rain_3_i.x, rain_y))
                screen.blit(rain, (rain_3_i.x, rain_3_y))
                rain_3_y += rain_3_speed

                if pygame.Rect.colliderect(player_rect, rain_3_rect):
                    rains_3.clear()
                    life_count -= 1

                if rain_3_y > 350: # поработать с хитбоксом
                    rains_3.pop(i)
                    rain_3_y = 0
        if rains_4:
            for (i, rain_4_i) in enumerate(rains_4):
                rain_4_rect = rain.get_rect(topleft=(rain_4_i.x, rain_y))
                screen.blit(rain, (rain_4_i.x, rain_4_y))
                rain_4_y += rain_4_speed

                if pygame.Rect.colliderect(player_rect, rain_4_rect):
                    rains_4.clear()
                    life_count -= 1

                if rain_4_y > 350: # поработать с хитбоксом
                    rains_4.pop(i)
                    rain_4_y = 0
        if rains_5:
            for (i, rain_5_i) in enumerate(rains_5):
                rain_5_rect = rain.get_rect(topleft=(rain_5_i.x, rain_y))
                screen.blit(rain, (rain_5_i.x, rain_5_y))
                rain_5_y += rain_5_speed

                if pygame.Rect.colliderect(player_rect, rain_5_rect):
                    rains_5.clear()
                    life_count -= 1

                if rain_5_y > 350: # поработать с хитбоксом
                    rains_5.pop(i)
                    rain_5_y = 0

    if win_flag:
        win_label = label.render('YOU WIN', True, (0, 0, 0))
        win_label_rect = win_label.get_rect(topleft=(320, 250))
        screen.fill((255, 255, 255))
        screen.blit(win_label, win_label_rect)

    if restart_flag:
        menu_flag = False
        gameplay = False
        shop_flag = False

        screen.blit(gr, (-60, -20))
        screen.blit(restart_label, restart_label_rect)
        screen.blit(menu_label, menu_label_rect)

        if menu_label_rect.collidepoint(mouse) and pygame.mouse.get_pressed()[0]:
            menu_flag = True

        pygame.draw.rect(screen, (255, 255, 255), ((1100, 630), (60, 40)))
        screen.blit(exit_label, exit_label_rect)
        if exit_label_rect.collidepoint(mouse) and pygame.mouse.get_pressed()[0]:
            flag = False

        if restart_label_rect.collidepoint(mouse) and pygame.mouse.get_pressed()[0]:
            gameplay = True
            is_Jump = False
            mini_boss1_flag = False
            boss_flag = False
            player_y = 145
            player_x = 15
            J_count = 9
            enemy_list_in_game.clear()
            bullets.clear()
            swords.clear()
            rifle_bullets.clear()
            boxs.clear()
            coins.clear()
            bombs_mini_boss1.clear()
            bombs_boss.clear()
            bombs_final_boss.clear()
            mini_boss1_list.clear()
            boss_list.clear()
            final_boss_list.clear()
            rains.clear()
            rains_2.clear()
            rains_3.clear()
            rains_4.clear()
            rains_5.clear()
            #mini_boss1_count = 0
            boss_count = 0
            bullets_amount = 7
            swords_amount = 2
            rifle_bullets_amount = 3
            game_count = 0
            life_count = 3

    if pause_flag:
        menu_flag = False
        shop_flag = False
        gameplay = False
        win_flag = False
        restart_flag = False
        bul_speed = 0
        rifle_bullet_speed = 0
        player_speed = 0
        enemy_speed = 0
        mini_boss1_speed = 0
        boss_speed = 0
        final_boss_speed = 0
        bomb_mini_boss1_speed = 0
        bomb_boss_speed = 0
        bomb_final_boss_speed = 0
        rain_speed = 0
        rain_2_speed = 0
        rain_3_speed = 0
        rain_4_speed = 0
        rain_5_speed = 0

    pygame.display.update()

    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            flag = False
        if event.type == enemy_timer and not boss_list and not mini_boss1_list:
            enemy_list_in_game.append(enemy.get_rect(topleft=(820, 160)))
        if event.type == mini_boss1_timer and len(mini_boss1_list) == 0 and mini_boss1_flag == False:
            mini_boss1_list.append(mini_boss1.get_rect(topleft=(1200, 130)))
        if event.type == boss_timer and len(boss_list) == 0:
            boss_list.append(boss.get_rect(topleft=(900, 75)))
        if boss_count == 1 and len(final_boss_list) == 0:
            final_boss_list.append(final_boss.get_rect(topleft=(900, 120)))
            if event.type == rain_timer and final_boss and not pause_flag:
                rain_x = random.randint(0, 1200)
                rains.append(rain.get_rect(topleft=(rain_x, rain_y)))
            if event.type == rain_2_timer and final_boss and not pause_flag:
                rain_x2 = random.randint(0, 1200)
                rains_2.append(rain.get_rect(topleft=(rain_x2, rain_2_y)))
            if event.type == rain_3_timer and final_boss and not pause_flag:
                rain_x3 = random.randint(0, 1200)
                rains_3.append(rain.get_rect(topleft=(rain_x3, rain_3_y)))
            if event.type == rain_4_timer and final_boss and not pause_flag:
                rain_x4 = random.randint(0, 1200)
                rains_4.append(rain.get_rect(topleft=(rain_x4, rain_4_y)))
            if event.type == rain_5_timer and final_boss and not pause_flag:
                rain_x5 = random.randint(0, 1200)
                rains_5.append(rain.get_rect(topleft=(rain_x5, rain_5_y)))
                # rains.append(rain.get_rect(topleft=(600, 100)))
        if event.type == bomb_mini_boss1_timer:
            bombs_mini_boss1.append(bomb.get_rect(topleft=(bomb_mini_boss1_x, 150)))
        if event.type == bomb_boss_timer:
            bombs_boss.append(bomb.get_rect(topleft=(bomb_boss_x, 150)))
        if event.type == bomb_final_boss_timer:
            bombs_final_boss.append(bomb.get_rect(topleft=(bomb_final_boss_x, 150)))
        if event.type == box_timer and game_count > 200:
            boxs.append(box.get_rect(topleft=(750, 35)))
        if event.type == coin_timer:
            coins.append(coin.get_rect(topleft=(750, 50)))
        if gameplay and event.type == pygame.KEYUP and event.key == pygame.K_c and bullets_amount > 0:
            bullets.append(bullet.get_rect(topleft=(player_x + 20, player_y + 10)))
            bullets_amount -= 1
        if gameplay and event.type == pygame.KEYUP and event.key == pygame.K_v and swords_amount > 0:
            swords.append(sword.get_rect(topleft=(player_x + 40, player_y + 10)))
            swords_amount -= 1
        if gameplay and event.type == pygame.KEYUP and event.key == pygame.K_n and rifle_bullets_amount > 0:
            rifles.append(rifle.get_rect(topleft=(player_x + 40, player_y + 10)))
            rifle_bullets.append(rifle_bullet.get_rect(topleft=(player_x + 40, player_y + 10)))
            rifle_bullets_amount -= 1
        if pause_flag and event.type == pygame.KEYUP and event.key == pygame.K_p:
            screen.blit(pause_label, pause_label_rect)

    clock.tick(15)
