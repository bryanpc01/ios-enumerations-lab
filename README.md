# Enumerations lab

Fork and clone this repo. On your fork, answer and commit the follow questions. When you are finished, submit the link to your repo on Canvas.


## Question 1

a) Define an enumeration called `iOSDeviceTypes` with member values `iPhone`, `iPad`, `iWatch`. Create a variable called `myDevice` and assign it one member value.

b) Adjust your code above so that `iPhone` and `iPad` have associated values of type String which represents the model number, eg: `iPhone("6 Plus")`. Use a switch case and let syntax to print out the model number of each device.

```swift
enum iOSDeviceTypes: String {
    case iPhone = "Xs Plus"
    case iPad = "10 inch LTE"
    case iWatch
}

// Create a variable called `myDevice` and assign it one member value.
var myDevice = iOSDeviceTypes.iPhone

// Adjust your code above so that `iPhone` and `iPad` have associated values of type String which represents the model number, eg: `iPhone("6 Plus")`. Use a switch case and let syntax to print out the model number of each device.
print(iOSDeviceTypes.iPhone.rawValue)
print(iOSDeviceTypes.iPad.rawValue)
print(iOSDeviceTypes.iWatch.rawValue)
```

## Question 2

a) Write an enum called `Shape` and give it cases for `triangle`, `rectangle`, `square` and `hexagon`.

b) Write a method inside `Shape` that returns how many sides the shape has. Then assign a variable to `Shape.pentagon` and then print how many sides it has.

c) Re-write `Shape` so that each case has an associated value of type Int that will represent the length of the sides (assume the shapes are regular polygons so all the sides are the same length) and write a method inside that returns the perimeter of the shape.

```swift
enum Shape{
case triangle(inches: Int)
case rectangle(inches: Int)
case square(inches: Int)
case hexagon(inches: Int)
case pentagon(inches: Int)

func numberOfSides() -> Int{
    switch self {
    case .triangle:
        return 3
    case .square:
        return 4
    case .rectangle:
        return 4
    case .pentagon:
        return 5
    case .hexagon:
        return 6
    }
}
func perimeter() -> Int {
    switch self {
        case let .triangle(inches):
            return numberOfSides() * inches
        case let .square(inches):
            return numberOfSides() * inches
        case let .rectangle(inches):
            return numberOfSides() * inches
        case let .pentagon(inches):
            return numberOfSides() * inches
        case let .hexagon(inches):
            return numberOfSides() * inches
        }
    }
}

```

## Question 3

Write an enum called `OperatingSystems` and give it cases for `Windows`, `Mac`, and `Linux`. Create an array of 10 `OperatingSystems` where each one is set to a random operating system. Then, iterate through the array and print out a message depending on the operating system.

```swift
enum OperatingSystems: CaseIterable, CustomStringConvertible {
    // From CustomStringConvertible protocol
    var description: String {
        switch self {
        case .windows:
            return "Windows"
        case .mac:
            return "Mac"
        case .linux:
            return "Linux"
        }
    }

    case windows
    case mac
    case linux

    static func random() -> OperatingSystems {
        // allCases is from the CaseIteriable Protocol
        return self.allCases.randomElement() ?? self.mac
    }
}

var arrayOfOperatingSystems = [OperatingSystems]()
for _ in 1...10 {
    arrayOfOperatingSystems.append(OperatingSystems.random())
}

for system in arrayOfOperatingSystems {
    switch system {
    case .linux:
        print("Linux:\nHey, which distro do you use?\n")
    case .mac:
        print("Mac:\nXcode, Xcode, Xcode\n")
    case .windows:
        print("Windows:\nI hope you are a gamer!\n")
    }
}
```


## Question 4

You are working on a game in which your character is exploring a grid-like map. You get the original location of the character and the steps he will take.

- A step .Up will increase the y coordinate by 1.
- A step .Down will decrease the y coordinate by 1.
- A step .Right will increase the x coordinate by 1.
- A step .Left will decrease the x coordinate by 1.
- Print the final location of the character after all the steps have been taken.

```swift
enum Direction {
    case up
    case down
    case left
    case right

    func move(location: (x: Int, y: Int)) -> (x: Int, y: Int){
        switch self {
        case .up:
            return (location.x, location.y + 1)
        case .down:
            return (location.x, location.y - 1)
        case .left:
            return (location.x - 1, location.y)
        case .right:
            return (location.x + 1, location.y)
        }
    }
}

var location = (x: 0, y: 0)
var steps: [Direction] = [.up, .up, .left, .down, .left]

for step in steps {
    location = step.move(location: location)
}
print(location)
```


## Question 5

a) Define an enumeration named `HandShape` with three members: `.rock`, `.paper`, `.scissors`.

b) Define an enumeration named `MatchResult` with three members: `.win`, `.draw`, `.lose`.

c) Write a function called `match` that takes two `HandShapes` and returns a `MatchResult`. It should return the outcome for the first player (the one with the first hand shape).

Hint: Rock beats scissors, paper beats rock, scissor beats paper

```swift
enum HandShape {
    case rock, paper, scissors
}

enum MatchResult: String{
    case win = "Player 1 Wins!"
    case draw = "Game was a draw :|"
    case lose = "Player 2 wins!"
}

func match(_ matchTuple: (player1: HandShape,player2: HandShape)) -> MatchResult {
    switch matchTuple {
    case (.rock, .scissors), (.paper, .rock), (.scissors, .paper):
        return .win
    case (.scissors, .rock), (.rock, .paper), (.paper, .scissors):
        return .lose
    case (.rock, .rock), (.paper, .paper), (.scissors, .scissors):
        return .draw
    }
}


print(match((player1: .scissors, player2: .scissors)).rawValue)
```

## Question 6

a) You are given a `CoinType` enumeration which describes different coin values. Print the total value of the coins in the array `moneyArray` which contains tuples of type (`quantity`, `CoinType`).

```swift
enum CoinType: Int {
    case penny = 1
    case nickle = 5
    case dime = 10
    case quarter = 25

    func toMakeDollar() -> Int {
        return 100 / self.rawValue
    }
}

var moneyArray:[(Int,CoinType)] = [(10,.penny),
                                   (15,.nickle),
                                   (3,.quarter),
                                   (20,.penny),
                                   (3,.dime),
                                   (7,.quarter)]
var sum = 0
for (quantity, coin) in moneyArray {
    sum += quantity * coin.rawValue
}
print("The total sum of the coins is \(sum) cents.")

// Write a method in the `CoinType` enum that returns an Int representing how many coins of that type you need to have a dollar. Then, create an instance of `CoinType` set to `.nickle` and use your method to print out how many nickels you need to have to make a dollar.

let myNickel = CoinType.nickle
print("I will need \(myNickel.toMakeDollar()) \(myNickel)'s to make a dollar.")
```


## Question 7

a) Write an enum called `DayOfWeek` to represent the days of the week with a raw value of type String.

b) Given the array `poorlyFormattedDays`, write code that will produce an array of enums that match the days.

`let poorlyFormattedDays = ["MONDAY", "wednesday", "Sunday", "monday", "Tuesday", "WEDNESDAY", "thursday", "SATURDAY", "tuesday", "FRIDAy", "Wednesday", "Monday", "Friday", "sunday"]`

c) Write a method in `DayOfWeek` called `isWeekend` that determines whether a day is part of the weekend or not and write code to calculate how many week days appear in `poorlyFormattedDays`.

```swift
//  a) Write an enum called `DayOfWeek` to represent the days of the week with a raw value of type String.

enum DayOfWeek: String, CustomStringConvertible{
    var description: String {
        switch self {
        case .sunday:
            return "Sunday"
        case .monday:
            return "Monday"
        case .tuesday:
            return "Tuesday"
        case .wednesday:
            return "Wednesday"
        case .thursday:
            return "Thursday"
        case .friday:
            return "Friday"
        case .saturday:
            return "Saturday"
        }
    }

    case sunday = "Sunday"
    case monday = "Monday"
    case tuesday = "Tuesday"
    case wednesday = "Wednesday"
    case thursday = "Thursday"
    case friday = "Friday"
    case saturday = "Saturday"

    func isWeekend() -> Bool{
        return self == .saturday || self == .sunday
    }
}

// b) Given the array `poorlyFormattedDays`, write code that will produce an array of enums that match the days.

let poorlyFormattedDays = ["MONDAY", "wednesday", "Sunday", "monday", "Tuesday", "WEDNESDAY", "thursday", "SATURDAY", "tuesday", "FRIDAy", "Wednesday", "Monday", "Friday", "sunday"]

func arrayOfDaysInEnum(_ arr: [String]) -> [DayOfWeek] {
    var output = [DayOfWeek]()
    for day in arr {
        if let day = DayOfWeek(rawValue: day.capitalized) {
            output.append(day)
        }
    }
    return output
}

print(arrayOfDaysInEnum(poorlyFormattedDays))

// c) Write a method in `DayOfWeek` called `isWeekend` that determines whether a day is part of the weekend or not and write code to calculate how many week days appear in `poorlyFormattedDays`.
var weekendDaysCount = 0
for day in arrayOfDaysInEnum(poorlyFormattedDays) where day.isWeekend() {
    weekendDaysCount += 1
}

print("There are \(weekendDaysCount) weekend days in the array.")
```


## Question 8

a) Create an enum called `MetroLine` with cases for the colors of the metro train lines. Create an instance of `MetroLine`.

b) Modify your enum so that each case has an associated value of either Character or Int that will represent the train on that line. Create a new instance of `MetroLine` and give it an appropriate train letter or number.

c) Write code that prints the train letter or number of your instance of `MetroLine`.

```swift
// Create an enum called `MetroLine` with cases for the colors of the metro train lines. Create an instance of `MetroLine`

// Modify your enum so that each case has an associated value of either Character or Int that will represent the train on that line. Create a new instance of `MetroLine` and give it an appropriate train letter or number.

enum MetroLine {
    case red(Int)
    case blue(Character)
    case green(Int)
    case yellow(Character)
    case purple(Int)
    case orange(Character)
}

let myFavoriteLine = MetroLine.red(3)

// Write code that prints the train letter or number of your instance of `MetroLine`.
switch myFavoriteLine {
case .red(let line):
    print("My favorite line is \(line).")
case .blue(let line):
    print("My favorite line is \(line).")
default:
    print("I have no favorite line.")
}
```


## Question 9

a) Think of your own example of something that can be modeled as an enum and write it. Remember that enums allow you to create instances of a defined list of cases.

b) Add a method to your enum.... try to have the method make sense.

```swift
enum Cookie {
    case chocoalteChip
    case oatmeal
    case sugar

    func canMake(ingredients: [String]) -> Bool {
        switch self {
        case .chocoalteChip:
            return ingredients.contains("Chocolate Chips")
        case .oatmeal:
            return ingredients.contains("Oatmeal") && ingredients.contains("Rasins")
        case .sugar:
            return true
        }
    }
}

let ingredients = ["Chocolate Chips", "Oatmeal"]
let cookieMomWantsForBirthday: Cookie = .oatmeal

print(cookieMomWantsForBirthday.canMake(ingredients: ingredients))
```
