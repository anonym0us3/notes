# Exercises
* Work in your Chrome Developer Console.  
    - Pro-Tip: use the "up" arrow key to save yourself some typing: it will pull up previously entered code.
* See `solutions.md` for solutions. No Peeking!


#### Login
When a user trys to login to our website we want to check that they actually input a value for username and a value for password. If they typed both in, give them an "All Good". But if either the username or the password are missing, give them an error: "Missing Username" / "Missing Password".
* username // string
* password // string


#### Superman?
We need a quick way to determine if that blip on the radar is superman or not. Sometimes it's just a bird. Sometimes it's just a plane. But we definitely want to know if its superman. Write some code which will alert: "It's superman!" when the following are true (it's up to you to decide what makes the most sense):
* isBirdlike // boolean
* isPlanelike // boolean
* hasFeathers // boolean
* isMadeOfMetal // boolean


#### Alert the Guards!
Alert the guards! Can you modify this code to only alert when a Bad Thing (TM) is happening?
```
var badThingHappening = true;
alert("Guards!") // this always alerts!
```

Bonus: Can you trigger the alert without using "if"?


#### Four Letter Word
No more four letter words! If a word has four letters replace it with "\*\*\*\*" and output "You said: \*\*\*\*". Otherwise print out what I said, e.g. "You said: pajamas".

```
var word = "okay"; // uh oh!
// your code here...

// simple test
console.log( output === "You said: ****" ) 
```


#### Make it a SloppyBurger.
The lovely cashier at SloppyBurger will assume you want a SloppyBurger unless you say otherwise. Better speak up!

On the left is what you said when you ordered. The output, on the right, is what you actually got. Can you transform the input (the order) into the output?

| input | output |
|:--------------|:--------------|
| "" | "One SloppyBurger" |
"Burger" | "One SloppyBurger" |
"DoubleBurger" | "One SloppyDoubleBurger" |
"Fries" | "One SloppyFries" |
"SloppyJoe" | "One SloppySloppyJoe" |

Bonus: Can you do it without using "if"?



#### Open Sesame
Ask me for the password. If I say "Open Sesame" let me in. Otherwise, kick me out. You will need to use a `prompt`.

```
var answer = prompt("What's the password")
// your code here
```



#### For Here
Sales tax can be tricky for restaurants to calculate. For example, sales tax is not charged on hot beverages, hot bakery goods, and cold prepared foods when ordered "to go." Otherwise the sale is taxed 7.75%. Use the following variables, and write some tests to check for the correct total:
* isHotBeverage // boolean
* isHotBakedGood // boolean
* isColdPreparedFood // boolean
* forHere // boolean
* total // floating point number



#### Get to work
- I will ride my bike when the temperature is between 50 and 90 degrees, assuming it's not raining. It takes 25-30 minutes.
- Otherwise I'm happy to take the bart. It takes 20-40 minutes.
- However, if my roommate is driving into work, I'll catch a ride with her. It takes 30-45 minutes.
- Assuming I always leave at 8am. What time will I get to work?
- Variable Names:  
    + temperature
    + isRaining
    + canCatchRide
- Example Output: "ETA: 8:30-8:45"




#### Can I ride?
An amusement park has the following requirements for a roller coaster ride:  
- Must have 5 tokens                              ("Sorry, too poor!")
- Must be at least 4ft tall                       ("Sorry, too short!")
- Must be at least 12 years old                   ("Sorry, too young!")
- Riders under 12 must be accompanied by an adult ("Sorry, must be accompanied!")
- (If the boss isn't looking, you can sneak in!)

Your job is to figure out if a customer is allowed on the ride or not. If they're not, tell them why. If they are, tell them "Step Right Up!" (and don't forget to take their tokens!).

Customers:  
- Jimmy, 13 years old, 100 tokens, 56 inches tall, unaccompanied
- Chris, 12 years old, 4 tokens, 48 inches tall, accompanied
- Jessie, 9, 10 tokens, 49 inches tall, accompanied
- Chadwick, 11, 10 tokens, 48 inches tall, unaccompanied, boss-not-looking


#### Bottles Of Beer
Create the "Bottles of beer on the wall" song (watch out for infinite loops!):
```
    5 bottles of beer on the wall,
    5 bottles of beer!
    Take one down and pass it around,
    4 bottles of beer on the wall...
    
    4 bottles of beer on the wall,
    4 bottles of beer!
    Take one down and pass it around,
    3 bottles of beer on the wall...
    etc.
```

* How would you change "0" to "No more"?
* How would you fix "1 bottles of beer"?


#### Shush
Welcome me to the library, then keep saying "shhh" until I shut up. You will need to use a `prompt` for this in combination with a loop (watch out for infinite loops!).

| what I said | what you said |
|--------------:|--------------:|
| "sorry?" | "shhh" |
| "Oh come on!" | "shhh" |
| "..." | "shhh" |
| "" | "" (exit the loop) |
