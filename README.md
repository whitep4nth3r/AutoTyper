# AutoTyper For Mac

This app automatically types the contents of
a text script into an app. It's goal is to make it
easier to make screen recordings where typing
is necessary. Instead of doing it manually, 
the app will do it for you. Faster and without 
flubbing keys. 

You can [check out an intro video here](http://www.youtube.com/watch?v=VrT6AG_jMwE):

[![A screenshot of the AutoTyper Introduction Demonstration Video](https://img.youtube.com/vi/VrT6AG_jMwE/maxresdefault.jpg)](http://www.youtube.com/watch?v=VrT6AG_jMwE "AutoTyper Introduction Demonstration")

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


## Examples

Here are a few scripts to get you started. 

### Hello, World

<table>
    <tr>
        <td><pre><code>type: Hello, World!</code></pre></td>
        <td><img src="./DocExamples/01-hello-world.gif" /></td>
    </tr>
</table>

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


## Instructions

This is the list of available instructions

| Instruction | Description | Notes | Example Usage |
|---|---|---|---|
| debug | Restores all pauses so the instruction runs with their specified delays and pauses. |  | debug: off |
|  | Remove all delays and pauses to fast-forward until 'debug: off' or the end of the script. |  | debug: on |
| down: NUMBER | Presses the down arrow key the specified NUMBER of times. |  | down: 3 |
| end-lines | Ends capturing lines that will be pasted via 'command + v' one at a time followed by pressing 'return' to move to a new line. |  | start-lines<br><br>Lorem ipsum dolor sit amet, consectetur<br>adipiscing elit.<br><br>Curabitur dignissim pretium justo nec<br>tincidunt.<br><br>end-lines |
| end-lines-down | Ends capturing lines that will be pasted via 'command + v' one at a time followed by pressing the down arrow.<br><br>The capture is started with 'start-lines-down'. |  | start-lines-down<br><br>Lorem ipsum dolor sit amet, consectetur<br>adipiscing elit.<br><br>Curabitur dignissim pretium justo nec<br>tincidunt.<br><br>end-lines-down |
| left | Presses the left arrow key one time. |  | left |
| left: NUMBER | Presses the left arrow key the specified NUMBER of times. |  | left: 3 |
| paste: TEXT | Pastes the TEXT by pressing 'command + v'. |  | paste: The quick brown fox |
| paste-down: TEXT | Pastes the TEXT by pressing 'command + v' then presses the down arrow. |  | paste-down: The quick brown fox |
| paste-line: TEXT | Pastes the TEXT by pressing 'command + v' then presses the return key to move to the next line. |  | paste-line: The quick brown fox |
| paste-file: PATH | Pastes the contents of the file at the given PATH by pressing 'command + v'. | You can get the PATH for a file by right clicking on it in the Finder then holding the 'option' key. When you do, the 'Copy' menu item will turn into 'Copy ... as Pathname' which is what PATH uses. | paste-file: /Users/alan/Desktop/example.txt |
| paste-file-lines: PATH | Pastes the contents of the file at the given PATH. Each line in the file is pasted individually via 'command + v'. The 'return' key is pressed after each line is pasted to move to the next line. | You can get the PATH for a file by right clicking on it in the Finder then holding the 'option' key. When you do, the 'Copy' menu item will turn into 'Copy ... as Pathname' which is what PATH uses. | paste-file-lines: /Users/alan/Desktop/example.txt |
| paste-file-lines-down: PATH | Pastes the contents of the file at the given PATH. Each line in the file is pasted individually via 'command + v'. The down arrow is pressed after each line is pasted to move to the next line.Pauses typing until F4 is pressed on the keyboard. | You can get the PATH for a file by right clicking on it in the Finder then holding the 'option' key. When you do, the 'Copy' menu item will turn into 'Copy ... as Pathname' which is what PATH uses. | paste-file-lines-down: /Users/alan/Desktop/example.txt |
| pause | Pauses typing until F4 is pressed on the keyboard. |  | pause |
| pause: TIME | Pauses typing for the given amount of TIME which is measured in seconds. |  | pause: 1<br>pause: 1.2<br>pause: 0.3 |
| press: KEY | Presses the given KEY one time. | - Only lower case letters can be used with 'press:'. Use 'press: shift: KEY' to make them upper case.<br>- The list of available KEYs is provided in the Keys tab above. | press: a<br>press: space<br>press: right-arrow |
| press: MODIFIERS: KEY | Press the given KEY one time while holding down the MODIFIERS. | The MODIFIERS are: command \| control \| option \| shift<br><br>- One or more MODIFIERS can be used at a time.<br>- Only lower case letters can be used with 'press:'. Use 'press: shift: KEY' to make them upper case.<br>- The list of available KEYs is provided in the Keys tab above. | press: command: a<br>press: option: right-arrow<br>press: option: shift: right-arrow |
| repeat: KEY | Presses the KEY the specified NUMBER of times. | - Only lower case letters can be used with 'repeat:'. Use 'repeat: NUMBER: shift: KEY' to make them upper case.<br>- The list of available KEYs is provided in the Keys tab above. | repeat: 3: space<br>repeat: 3: up-arrow |
| repeat: MODIFIERS: KEY | Press the given KEY the specified NUMBER of times while holding down the MODIFIERS. | The MODIFIERS are: command \| control \| option \| shift<br><br>- One or more MODIFIERS can be used at a time.<br>- Only lower case letters can be used with 'press:'. Use 'press: shift: KEY' to make them upper case.<br>- The list of available KEYs is provided in the Keys tab above. | repeat: 3: shift: a<br>repeat: 5: option: right-arrow<br>repeat: 2: option: shift: right-arrow |
| reset-delay | Resets the minimum and maximum times that the random delay between key presses uses to their default values. |  | reset-delay |
| return | Presses the 'return' key one time. |  | return |
| return: NUMBER | Presses the 'return' key the specified NUMBER of times. |  | return: 3 |
| right | Presses the right arrow key one time. |  | right |
| right: NUMBER | Presses the right arrow key the specified NUMBER of times. |  | right: 3 |
| set-delay: TIME | Sets the delay between key presses to TIME which is measured in seconds. |  | set-delay: 0.04 |
| set-delay: MIN: MAX | Resets the minimum and maximum times that the random delay between key presses uses to MIN_TIME and MAX_TIME, respectively. |  | set-delay: 0.05: 0.1 |
| space | Presses the 'space' key one time. |  | space |
| space: NUMBER | Presses the 'space' key the specified NUMBER of times. |  | space: 3 |
| start-lines | Starts capturing lines that will be pasted via 'command + v' one at a time followed by pressing 'return' to move to a new line.<br><br>The capture continues until an 'end-lines' instruction is found. |  | start-lines<br><br>Lorem ipsum dolor sit amet, consectetur<br>adipiscing elit.<br><br>Curabitur dignissim pretium justo nec<br>tincidunt.<br><br>end-lines |
| start-lines-down | Starts capturing lines that will be pasted via 'command + v' one at a time followed by pressing the down arrow.<br><br>The capture continues until an 'end-lines-down' instruction is found. |  | start-lines-down<br><br>Lorem ipsum dolor sit amet, consectetur<br>adipiscing elit.<br><br>Curabitur dignissim pretium justo nec<br>tincidunt.<br><br>end-lines-down |
| stop | Stops the script from running. |  | stop |
| tab | Presses the 'tab' key one time. |  | tab |
| tab: NUMBER | Presses the 'tab' key the specified NUMBER of times. |  | tab: 3 |
| type: TEXT | Types the given TEXT. | - Neither the 'return' key or down-arrow is presses after the TEXT is types. This provides as way to edit text in the middle of a line without making or moving to a new line.<br>- Any spaces at the start of the TEXT are removed.<br>- Any spaces at the end of the TEXT are removed.<br>- Use a 'press: space' instruction to add spaces at either the start or the end of a piece of text if necessary. | type: The quick brown fox |
| type-down: TEXT | Types the given TEXT followed by pressing the down arrow key. | - Any spaces at the start of the TEXT are removed.<br>- Any spaces at the end of the TEXT are removed.<br>- Use a 'press: space' instruction to add spaces at either the start or the end of a piece of text if necessary. | type-down: The quick brown fox |
| type-line: TEXT | Types the given TEXT followed by pressing the 'return' key. | - Any spaces at the start of the TEXT are removed.<br>- Any spaces at the end of the TEXT are removed.<br>- Use a 'press: space' instruction to add spaces at either the start or the end of a piece of text if necessary. | type-line: The quick brown fox |
| up | Presses the up arrow one time. |  | up |
| up: NUMBER | Presses the up arrow the specified NUMBER of times |  | up: 3 |

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