# AutoTyper For Mac

This app automatically types the contents of
a text script into an app. It's goal is to make it
easier to make screen recordings where typing
is necessary. Instead of doing it manually, 
the app will do it for you. Faster and without 
flubbing keys. 

You can check out an intro video here:

[![A screenshot of the AutoTyper Introduction Demonstration Video](http://img.youtube.com/vi/VrT6AG_jMwE/maxresdefault.jpg)](http://www.youtube.com/watch?v=VrT6AG_jMwE "AutoTyper Introduction Demonstration")

## Installation

- Download the AutoTyper.zip file. Unzip it
and copy the AutoTyper.app file to your
Applications folder. 

## Usage

1. Create a .txt file with instructions in it (the full list of
available instructions is in the Instructions sections further below).

2. Use the 'Choose Instructions File' button to select your script file.

3. Click on the app you want to output the script to in the 'Select App' section.

4. Click 'Run'. You may be asked to allow the app permissions in the System Preferences. This is required to let AutoTyper simulate a keyboard to do that actual typing. (Note that sometimes you have to delete the AutoTyper item, click Run, and turn it back on to reset it.)

## General Notes

- The basic ways to type are `type: TEXT`, `type-line: TEXT`, 
and `type-down:TEXT`. For example:

    `type: Hello, World`

    `type-line: Hello, World`

    `type-down: Hello, World`

- The `type: TEXT` instruction doesn't add a `return/enter` after it finishes typing.
(That it, it only types in the characters from your `TEXT`)

- `type-line: TEXT` presses `return/enter` after typing your `TEXT`

- `type-down: TEXT` presses the down arrow after typing your `TEXT`

- The `press: KEY` instruction is used for pressing a specific `KEY`. (The 
full list of available keys is in the Keys section further below)

- The `press: MODIFIER: KEY` instruction holds the specific `MODIFIER`
while pressing the `KEY`. For example:

    `press: command: a`

- Multiple `MODIFIER` keys can be held while pressing a key like:

    `press: option: shift: right-arrow`

- The `pause` instruction pauses typing until you press `F4` on your
keyboard. This is the main thing I use to create breaks for 
talking when I'm doing scree recordings. 

- The `pause: TIME` instruction pauses for the specified time 
(measured in seconds). I generally use this for little pauses 
(e.g. `pause: 0.3`) to make it easier to track when I do thing
like highlight and delete code.

## Examples

Here are a few scripts to get you started. 

### Basic Hello, World

```
type: Hello, World!
```

Outputs:

```
Hello, World!
```

---

### Multiple Lines

```
type-line: Hello, 
type: World!
```

Outputs:

```
Hello, 
World!
```

---

### Type, Pause, Type

```
type: Hello,
pause
press: space
type: World!
```

Outputs:

`Hello`

Then, waits for you to press `F4` at which point
it types a space followed by `World!`

---

### Type A Block Of Text

```
start-lines
Lorem ipsum dolor sit amet, consectetur 
adipiscing elit. Donec velit ex, tincidunt 
vel posuere ut volutpat. 

In velit. Suspendisse euismod sed nisi 
id malesuada. Proin id lacus aliquet.
end-lines
```

Outputs the block of text between `start-lines`
and `end-lines`

---


### Type, Select, Overwrite In VS Code

```
type: alfa, bravo, charlie
pause: 0.8
repeat: 2: option: left-arrow
press: option: shift: right-arrow
pause: 0.8
type: DELTA
```

This example types:

`alfa, bravo, charlie`

then selects `bravo` and overwrites it with `DELTA`. 
Pauses are added in to make it easier to see
what's going on. 

This works in apps like VS Code where `option + left/right-arrow`
jumps words and `option + shift + left/right-arrow` selects
words. 

---

### Type, Select, Overwrite In Neovim

```
press: escape
type: i
type: alfa, bravo, charlie
pause: 0.8
press: escape
type: 3bdwi
type: DELTA
```

Presses `escape` to make sure you're not already in 
`INSERT` mode then `i` to switch to it. Next, it
types `alfa, bravo, charlie` then pause before
pressing `escape` again to switch to `NORMAL` mode
and typing in the commands to back up 3 time, delete
the word and switch back to `INSERT` mode before
typing `DELTA`


## Instructions

This is the list of available instructions


<table>
<thead><tr><th>Instruction</th><th>Description</th></tr></thead>
<tbody>
<tr><td>debug: off</td><td>
Restores all pauses so the instruction runs with their specified delays and pauses.
<br />

<br />
~ Usage ~
<br />

<br />
debug: off
<br />
</td></tr>
<tr><td>debug: on</td><td>
Remove all delays and pauses to fast-forward until 'debug: off' or the end of the script.
<br />

<br />
~ Usage ~
<br />

<br />
debug: on
<br />
</td></tr>
<tr><td>down</td><td>
Press the down arrow key one time. 
<br />

<br />
~ Usage ~
<br />

<br />
down
<br />
</td></tr>
<tr><td>down: NUMBER</td><td>
Presses the down arrow key the specified NUMBER of times.
<br />

<br />
~ Usage ~
<br />

<br />
down: 3
<br />
</td></tr>
<tr><td>end-lines</td><td>
Ends capturing lines that will be pasted via 'command + v' one at a time followed by pressing 'return' to move to a new line. 
<br />

<br />
The capture is started with 'start-lines'.
<br />

<br />
~ Example ~
<br />

<br />
start-lines
<br />
Lorem ipsum dolor sit amet, consectetur 
<br />
adipiscing elit. 
<br />

<br />
Curabitur dignissim pretium justo nec 
<br />
tincidunt. 
<br />
end-lines
<br />
</td></tr>
<tr><td>end-lines-down</td><td>
Ends capturing lines that will be pasted via 'command + v' one at a time followed by pressing the down arrow. 
<br />

<br />
The capture is started with 'start-lines-down'.
<br />

<br />
~ Example ~
<br />

<br />
start-lines-down
<br />
Lorem ipsum dolor sit amet, consectetur 
<br />
adipiscing elit. 
<br />

<br />
Curabitur dignissim pretium justo nec 
<br />
tincidunt. 
<br />
end-lines-down
<br />
</td></tr>
<tr><td>left</td><td>
Presses the left arrow key one time.
<br />

<br />
~ Usage ~
<br />

<br />
left
<br />
</td></tr>
<tr><td>left: Number</td><td>
Presses the left arrow key the specified NUMBER of times. 
<br />

<br />
~ Usage ~
<br />

<br />
left: 3
<br />
</td></tr>
<tr><td>paste: TEXT</td><td>
Pastes the TEXT by pressing 'command + v'. 
<br />

<br />
~ Usage ~
<br />

<br />
paste: The quick brown fox
<br />
</td></tr>
<tr><td>paste-down: TEXT</td><td>
Pastes the TEXT by pressing 'command + v' then presses the down arrow.
<br />

<br />
~ Usage ~
<br />

<br />
paste-down: The quick brown fox
<br />
</td></tr>
<tr><td>paste-line: TEXT</td><td>
Pastes the TEXT by pressing 'command + v' then presses the return key to move to the next line. 
<br />

<br />
~ Usage ~
<br />

<br />
paste-line: The quick brown fox
<br />
</td></tr>
<tr><td>paste-file: PATH</td><td>
Pastes the contents of the file at the given PATH by pressing 'command + v'.
<br />

<br />
~ Usage ~
<br />

<br />
paste-file: /Users/alan/Desktop/example.txt
<br />

<br />
~ Note ~
<br />

<br />
You can get the PATH for a file by right clicking on it in the Finder then holding the 'option' key. When you do, the 'Copy' menu item will turn into 'Copy ... as Pathname' which is what PATH uses. 
<br />
</td></tr>
<tr><td>paste-file-lines: PATH</td><td>
Pastes the contents of the file at the given PATH. Each line in the file is pasted individually via 'command + v'. The 'return' key is pressed after each line is pasted to move to the next line. 
<br />

<br />
~ Usage ~
<br />

<br />
paste-file-lines: /Users/alan/Desktop/example.txt
<br />

<br />
~ Note ~
<br />

<br />
You can get the PATH for a file by right clicking on it in the Finder then holding the 'option' key. When you do, the 'Copy' menu item will turn into 'Copy ... as Pathname' which is what PATH uses. 
<br />
</td></tr>
<tr><td>paste-file-lines-down: PATH</td><td>
Pastes the contents of the file at the given PATH. Each line in the file is pasted individually via 'command + v'. The down arrow is pressed after each line is pasted to move to the next line. 
<br />

<br />
~ Usage ~
<br />

<br />
paste-file-lines-down: /Users/alan/Desktop/example.txt
<br />

<br />
~ Note ~
<br />

<br />
You can get the PATH for a file by right clicking on it in the Finder then holding the 'option' key. When you do, the 'Copy' menu item will turn into 'Copy ... as Pathname' which is what PATH uses. 
<br />
</td></tr>
<tr><td>pause</td><td>
Pauses typing until F4 is pressed on the keyboard. 
<br />

<br />
~ Usage ~
<br />

<br />
pause
<br />
</td></tr>
<tr><td>pause: TIME</td><td>
Pauses typing for the given amount of TIME which is measured in seconds. 
<br />

<br />
~ Examples ~
<br />

<br />
pause: 1 
<br />

<br />
pause: 1.2
<br />

<br />
pause: 0.3
<br />

<br />
</td></tr>
<tr><td>press: KEY</td><td>
Presses the given KEY one time. 
<br />

<br />
~ Examples ~
<br />

<br />
press: a
<br />

<br />
press: space
<br />

<br />
press: right-arrow
<br />

<br />
~ Note ~ 
<br />

<br />
- Only lower case letters can be used with 'press:'. Use 'press: shift: KEY' to make them upper case. 
<br />

<br />
- The list of available KEYs is provided in the Keys tab above. 
<br />
</td></tr>
<tr><td>press: MODIFIERS: KEY</td><td>
Press the given KEY one time while holding down the MODIFIERS. 
<br />

<br />
The MODIFIERS are:
<br />

<br />
- command
<br />
- control
<br />
- option
<br />
- shift
<br />

<br />
One or more MODIFIERS can be used at a time.
<br />

<br />
~ Examples ~
<br />

<br />
press: command: a
<br />

<br />
press: option: right-arrow
<br />

<br />
press: option: shift: right-arrow
<br />

<br />
~ Note ~
<br />

<br />
- Only lower case letters can be used with 'press:'. Use 'press: shift: KEY' to make them upper case. 
<br />

<br />
- The list of available KEYs is provided in the Keys tab above. 
<br />

<br />
</td></tr>
<tr><td>repeat: KEY</td><td>
Presses the KEY the specified NUMBER of times.
<br />

<br />
~ Examples ~
<br />

<br />
repeat: 3: space
<br />

<br />
repeat: 3: up-arrow
<br />

<br />
~ Notes ~ 
<br />

<br />
- Only lower case letters can be used with 'repeat:'. Use 'repeat: NUMBER: shift: KEY' to make them upper case. 
<br />

<br />
- The list of available KEYs is provided in the Keys tab above. 
<br />
</td></tr>
<tr><td>repeat: MODIFIERS: KEY</td><td>
Press the given KEY the specified NUMBER of times while holding down the MODIFIERS. 
<br />

<br />
The MODIFIERS are:
<br />

<br />
- command
<br />
- control
<br />
- option
<br />
- shift
<br />

<br />
One or more MODIFIERS can be used at a time.
<br />

<br />
~ Examples ~
<br />

<br />
repeat: 3: shift: a
<br />

<br />
repeat: 5: option: right-arrow
<br />

<br />
repeat: 2: option: shift: right-arrow
<br />

<br />
~ Notes ~
<br />

<br />
- Only lower case letters can be used with 'repeat:'. Use 'repeat: NUMBER: shift: KEY' to make them upper case. 
<br />

<br />
- The list of available KEYs is provided in the Keys tab above. 
<br />
</td></tr>
<tr><td>reset-delay</td><td>
Resets the minimum and maximum times that the random delay between key presses uses to their default values. 
<br />

<br />
~ Usage ~
<br />

<br />
reset-delay
<br />
</td></tr>
<tr><td>return</td><td>
Presses the 'return' key one time.
<br />

<br />
~ Usage ~
<br />

<br />
return
<br />
</td></tr>
<tr><td>return: NUMBER</td><td>
Presses the 'return' key the specified NUMBER of times. 
<br />

<br />
~ Example ~
<br />

<br />
return: 3
<br />
</td></tr>
<tr><td>right</td><td>
Presses the right arrow key one time.
<br />

<br />
~ Usage ~
<br />

<br />
right
<br />
</td></tr>
<tr><td>right: NUMBER</td><td>
Presses the right arrow key the specified NUMBER of times.
<br />

<br />
~ Example ~
<br />

<br />
right: 3
<br />
</td></tr>
<tr><td>set-delay: TIME</td><td>
Sets the delay between key presses to TIME which is measured in seconds. 
<br />

<br />
~ Example ~
<br />

<br />
set-delay: 0.04
<br />
</td></tr>
<tr><td>set-delay: MIN: MAX</td><td>
Resets the minimum and maximum times that the random delay between key presses uses to MIN_TIME and MAX_TIME, respectively.
<br />

<br />
~ Example ~
<br />

<br />
set-delay: 0.05: 0.1
<br />
</td></tr>
<tr><td>space</td><td>
Presses the 'space' key one time.
<br />

<br />
~ Usage ~
<br />

<br />
space
<br />
</td></tr>
<tr><td>space: NUMBER</td><td>
Presses the 'space' key the specified NUMBER of times. 
<br />

<br />
~ Example ~
<br />

<br />
space: 3
<br />
</td></tr>
<tr><td>start-lines</td><td>
Starts capturing lines that will be pasted via 'command + v' one at a time followed by pressing 'return' to move to a new line. 
<br />

<br />
The capture continues until an 'end-lines' instruction is found. 
<br />

<br />
~ Example ~
<br />

<br />
start-lines
<br />
Lorem ipsum dolor sit amet, consectetur 
<br />
adipiscing elit. 
<br />

<br />
Curabitur dignissim pretium justo nec 
<br />
tincidunt. 
<br />
end-lines
<br />
</td></tr>
<tr><td>start-lines-down</td><td>
Starts capturing lines that will be pasted via 'command + v' one at a time followed by pressing the down arrow. 
<br />

<br />
The capture continues until an 'end-lines-down' instruction is found. 
<br />

<br />
~ Example ~
<br />

<br />
start-lines-down
<br />
Lorem ipsum dolor sit amet, consectetur 
<br />
adipiscing elit. 
<br />

<br />
Curabitur dignissim pretium justo nec 
<br />
tincidunt. 
<br />
end-lines-down
<br />
</td></tr>
<tr><td>stop</td><td>
Stops the script from running.
<br />
</td></tr>
<tr><td>tab</td><td>
Presses the 'tab' key one time.
<br />

<br />
~ Usage ~
<br />

<br />
tab
<br />
</td></tr>
<tr><td>tab: NUMBER</td><td>
Presses the 'tab' key the specified NUMBER of times. 
<br />

<br />
~ Example ~
<br />

<br />
tab: 3
<br />
</td></tr>
<tr><td>type: TEXT</td><td>
Types the given TEXT
<br />

<br />
~ Example ~
<br />

<br />
type: The quick brown fox
<br />

<br />
~ Notes ~
<br />

<br />
- Neither the 'return' key or down-arrow is presses after the TEXT is types. This provides as way to edit text in the middle of a line without making or moving to a new line. 
<br />

<br />
- Any spaces at the start of the TEXT are removed.
<br />

<br />
- Any spaces at the end of the TEXT are removed.
<br />

<br />
- Use a 'press: space' instruction to add spaces at either the start or the end of a piece of text if necessary. 
<br />
</td></tr>
<tr><td>type-down: TEXT</td><td>
Types the given TEXT followed by pressing the down arrow key. 
<br />

<br />
~ Example ~
<br />

<br />
type-down: The quick brown fox
<br />

<br />
~ Notes ~
<br />

<br />
- Any spaces at the start of the TEXT are removed.
<br />

<br />
- Any spaces at the end of the TEXT are removed.
<br />

<br />
- Use a 'press: space' instruction to add spaces at either the start or the end of a piece of text if necessary. 
<br />
</td></tr>
<tr><td>type-line: TEXT</td><td>
Types the given TEXT followed by pressing the 'return' key. 
<br />

<br />
~ Example ~
<br />

<br />
type-line: The quick brown fox
<br />

<br />
~ Notes ~
<br />

<br />
- Any spaces at the start of the TEXT are removed.
<br />

<br />
- Any spaces at the end of the TEXT are removed.
<br />

<br />
- Use a 'press: space' instruction to add spaces at either the start or the end of a piece of text if necessary. 
<br />
</td></tr>
<tr><td>up</td><td>
Presses the up arrow one time.
<br />

<br />
~ Usage ~
<br />

<br />
up
<br />
</td></tr>
<tr><td>up: NUMBER</td><td>
Presses the up arrow the specified NUMBER of times
<br />

<br />
~ Example ~
<br />

<br />
up: 3
<br />
</td></tr>
</tbody>
</table>

## Keys

This is the list of keys available for use in 
`press:` and `repeat:` instructions. 

- =

- '

- ,

- \-

- .

- /

- 0

- 1

- 2

- 3

- 4

- 5

- 6

- 7

- 8

- 9

- ;

- [

- \

- ]

- a

- b

- c

- caps-lock

- command

- control

- d

- delete

- down-arrow

- e

- end

- enter

- escape

- f

- f1

- f10

- f11

- f12

- f13

- f14

- f15

- f16

- f17

- f18

- f19

- f2

- f20

- f3

- f4

- f5

- f6

- f7

- f8

- f9

- F1

- F2

- F3

- F4

- F5

- F6

- F7

- F8

- F9

- F10

- F11

- F12

- F13

- F14

- F15

- F16

- F17

- F18

- F19

- forward-delete

- function

- g

- h

- help

- home

- i

- iso-section

- j

- jis-eisu

- jis-underscore

- jis-yen

- jis_kana

- k

- keypad-0

- keypad-1

- keypad-2

- keypad-3

- keypad-4

- keypad-5

- keypad-6

- keypad-7

- keypad-8

- keypad-9

- keypad-clear

- keypad-decimal

- keypad-divide

- keypad-enter

- keypad-equals

- keypad-jis-comma

- keypad-minus

- keypad-multiply

- keypad-plus

- l

- left-arrow

- m

- mute

- n

- o

- option

- p

- page-down

- page-up

- q

- r

- return

- right-arrow

- s

- shift

- space

- t

- tab

- u

- up-arrow

- v

- volume-down

- volume-up

- w

- x

- y

- z

- ~




## Notes

- The app works on macOS 14.x. I'm not currently 
set up to test other versions. 

- The app was built on a U.S. keyboard. I'm not
currently set up to test other keyboards. I 
think there will be some work to do to get 
other character sets to work. I don't know
enough about that yet to know what to expect
or what would need to be done. 



