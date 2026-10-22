# The-heart-animation-python

import turtle
import math

screen = turtle.Screen()
screen.title("My Heart Animation ❤️")
screen.bgcolor("black")
screen.setup(width=600, height=600)
screen.tracer(0)

heart = turtle.Turtle()
heart.hideturtle()
heart.speed(0)
heart.color("red")

def draw_heart(scale):
    heart.clear()
    heart.penup()

    for i in range(361):
        t = math.radians(i)
        x = 16 * math.sin(t) ** 3
        y = (
            13 * math.cos(t)
            - 5 * math.cos(2 * t)
            - 2 * math.cos(3 * t)
            - math.cos(4 * t)
        )

        heart.goto(x * scale, y * scale)
        if i == 0:
            heart.pendown()

    heart.penup()
    heart.goto(0, -20 * scale)
    heart.write("LOVE", align="center",
                font=("Arial", 16, "bold"))

scale = 10
growing = True

def animate():
    global scale, growing

    draw_heart(scale)
    screen.update()

    scale += 0.2 if growing else -0.2

    if scale >= 11:
        growing = False
    elif scale <= 9:
        growing = True

    screen.ontimer(animate, 40)

animate()
screen.mainloop()
