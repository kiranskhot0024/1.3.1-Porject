import turtle as trtl
import time


wn = trtl.Screen()
wn.bgcolor("lime")
image = "cookie.gif"
wn.addshape(image)

cookie = trtl.Turtle()
cookie.penup()
cookie.hideturtle()
cookie.shape(image)

envelope = trtl.Turtle()
envelope.penup()
envelope.hideturtle()


card = trtl.Turtle()
card.penup()
card.hideturtle()


writer = trtl.Turtle()
writer.penup()
writer.hideturtle()


font_setup = ("Arial", 30, "bold")


line = trtl.Turtle()
line.hideturtle()
card.speed(0)
message_font = ("Verdana", 14, "normal")
message = (
    "Good morning senior citizen,\n\n"
    "I’m so glad you’re in good health. \n"
    "I miss you so dearly. \nWhen I was baking yesterday, \n"
    "I thought I’d bring you a cookie.\n\n"
    "They’re under the envelope. \nI hope you enjoy them!\n\n"
    "Sincerely,\n"
    "Pear, Talon & Kiran."
)




def open_card():
  #stage 1 of card opening, card is still in the envelope
  flip_open()
  writer.clear()
  card.goto(-200, 300)
  card.pendown()
  card.fillcolor("pink")
  card.begin_fill()
  card.setheading(0)
  card.forward(400)
  card.right(90)
  card.forward(163)
  card.goto(0, 20)
  card.goto(-200, 137)
  card.goto(-200, 300)
  card.end_fill()
  card.penup()
  card.hideturtle()
  write_ui_2()
  wn.onkeypress(full_open, "a")


#stage 2 of card opening, card is fully out of the envelope
def full_open():
  writer.clear()
  card.clear()
  card.goto(-200, 400)
  card.pendown()
  card.fillcolor("pink")
  card.begin_fill()
  card.setheading(0)
  card.forward(400)
  card.right(90)
  card.forward(500)
  card.right(90)
  card.forward(400)
  card.right(90)
  card.forward(500)
  card.end_fill()
  type_message(message)
  wn.onkeypress(reveal_cookies, "a")


def write_ui_1():
  writer.hideturtle()
  writer.goto(0, 350)
  writer.write("Press 'A' to open the card!", font=font_setup, align="center")


def write_ui_2():
  writer.clear()
  writer.goto(0, 350)
  writer.write("Press 'A' to take the card out!", font=font_setup, align="center")
  wn.onkeypress(full_open, "a")


def final_ui():
  writer.clear()
  writer.goto(0, -100)
  wn.onkeypress(reveal_cookies, "a")

def reveal_cookies():
   line.clear()
   writer.clear()
   card.clear()
   envelope.clear()
   cookie.showturtle()

def flip_open():
   line.fillcolor("lightblue")
   line.goto(225, 150)
   line.begin_fill()
   line.goto(0, 20)
   line.goto(-225, 150)
   line.goto(0 , 280)
   line.goto(225, 150)
   line.end_fill()
   line.pencolor("gray")
   line.goto(-225, 150)


def type_message(text):
    writer.goto(-170, 0) # Position text inside the pink card
    writer.pencolor("black")
   
    # This loop creates the typing effect
    current_text = ""
    for char in text:
        writer.clear()
        current_text += char
        writer.write(current_text, font=message_font, align="left")
        # Adjusting the sleep time changes typing speed
        time.sleep(0.0)
    writer.goto(0, -240)
    writer.write("Press 'A' to reveal the cookie!", font=font_setup, align="center")




#draw the envelope outline and fill with white
envelope.goto(-225, 150)
envelope.pendown()
envelope.fillcolor("white")
envelope.begin_fill()
for i in range(2):
  envelope.forward(450)
  envelope.right(90)
  envelope.forward(300)
  envelope.right(90)
envelope.end_fill()
envelope.hideturtle()


line.penup()
line.goto(-225, 150)
line.pendown()
line.pencolor("black")
line.goto(0, 20)
line.goto(225, 150)
line.hideturtle()


write_ui_1()
wn.onkeypress(open_card, "a")



wn.listen()
wn.mainloop()
