#Libraries
import time
import turtle

#convert bpm to milliseconds
def bpm_to_ms(bpm):
    return 60000/bpm

#convert rhythm pattern to duration  
def calculate_rhythm_duration(bpm, rhythm):
    ms_ms = bpm_to_ms(bpm)
    return [ms_ms * length for length in rhythm] 

#setting up turtle screen and pen
screen = turtle.Screen()
screen.title("Rhythm Vizualizer")
screen.bgcolor("white")

pen = turtle.Turtle()
pen.hideturtle()
pen.speed(0)
pen.penup()
pen.color("white")
pen.fillcolor("red")

#Beats and label drawing
def beat_drawing(x, y, size, label):


    #move toward the top-left corner of the square
    half = size / 2
    pen.goto(x - half, y + half)
    pen.pendown()
    pen.begin_fill()

    #draw square
    for _ in range(4):
        pen.forward(size)
        pen.right(90)
    
    pen.end_fill()
    pen.penup()

    #draw label above the square
    pen.goto(x, y + half)
    pen.write(label, align = "center", font = ("Times New Roman", 14, "normal"))

#input
bpm = int(input("Enter BPM:"))
rhythm = input("Enter 2 or more note rhythm number seperated by comma (eg: 0.5, 1, 0.5): ")

rhythm = [float(x.strip()) for x in rhythm.split(",")]
duration = calculate_rhythm_duration(bpm, rhythm)


#animation loop
while True:
    x_pos = -100 
    step = 50
    for i, dur in enumerate(duration):
        label = f"{rhythm[i]} beat"
        beat_drawing(x_pos + i*step, 0, 25, label)
        time.sleep((dur / 1000) * 0.2)
    time.sleep(1)

#keep the turtle window open
screen.mainloop()


