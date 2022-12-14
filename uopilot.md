The given documentation contains the description of language of the scripts of the program UOPilot of the version 1.07 beta 5. Be attentive at use of earlier versions of the program.

Conditional designations:
<> - obligatory parameter
[] - unessential parameter


SYNTAX
===========

In one line there can be only one command. The first word in a line - command, other words - parameters. If the first word in a line not the command - the line is considered as the comment.

The words consist of symbols 0-9, A-z, A-y.

Symbols *, $, %, +, -, *, /, >, <, =, :, ., (, ), [,] are service, other separators.

It is possible to write the comments after all parameters. Also that consider everything, that goes after '//'. It is extremely recommended to use such method.

The pauses in commands are specified by default in ms (1/1000 seconds), but the instruction(indication) of time and obviously, in hours, minutes, seconds is possible:
- wait 500 // to wait for 0.5 seconds
- wait 5s // to wait for 5 seconds
- wait 1m // to wait 1 minute
- wait 1h // to wait 1 hour


Variable
===========

In a name variable the symbols - are allowable ['0'.. '9', 'A'.. 'z', 'A'..'y'], register am not taken into account. Maximal length of a name variable 255 symbols.

Variable can be numerical and line. Syntax numerical variable '#name', where name - name variable. Syntax line variable '$name', where name - name variable.
For example:
set #i 20
set $s test string

Also you can use arrays. The symbol of percent '%' is considered as the identifier of a array. The indexes of a array are specified after a name in square brackets '[' and ']'. The size of a array is equal to the maximal used index. The giving of values is carried out to each element individually by command set. The elements of a array can contain both line, and number. Is allowable to refer to arrays of the parallel scripts, having specified after a name of a array, through a point, number of the script. At the indication only of first index in two-dimension a array, result will be a line from all elements of the second dimension of a array appropriate to the specified index, and divided by a space.
For example:
set %ar [4] oano // an one-dimensional array on 4 elements
set %arr [50 1] 544
set %arr [50 2] 800 // an two-dimensional a array on 50 times till 2 elements
set %ar.2 [5] // an one-dimensional array in parallel script
left %arr [50] // click by the left button on coordinates 544 800

Take into account, that the elements of arrays cannot directly be used in the conditional operators:
if charposx <> %arr [50 1]

Before use variable in the scripts you should define it through the command 'set'. Variable change only at participation 'set' and 'for', the command 'repeat' uses value, not changing it.
For example:
set #i #i + 1

Syntax of the command Set:
--------------------------------------- --
set $<name> <value> or
set #<name> <value1> [<a mark of operation> <value2>]
set %<name> [an element] <value>
Between a mark of operation and values there should be a separator. The following operations are supported: +, -, *, /, also you can use brackets for change of priorities of performance of mathematical operations. At division the result is approximated to smaller whole.
For example:
set #q ((5+4)/(3+-2)* #e )-(2-(-5+9))*3

With line variable some mathematical operations are possible:
set $s1 1
set $s2 2
set $s $s1 + $s2
Result will be $s = '1 + 2', i.e. at giving something line variable, it all is appropriated up to the end of a line, with the appropriate replacements
set #n $s1 + $s2
Result will be #n = 3, i.e. if line variable, contains line performance of an integer, it can be used as numerical variable.

In the command 'set' you can use the generator of random numbers: random (number) returns number in a range from 0 up to number-1
For example:
set #a random (2)

At two or more started scripts you can address to variable, certain in other scripts of the pilot. Syntax of the instruction such variable following:
#i.2 - we address to variable #i from the script which is taking place in a window number 2.

Variable during performance of the script can be changed through the table of display variable. The change variable occurs synchronously to a character set.


Reserved variable
=============================

The note 1: [W] means, that you can change value by this variable in the scripts through the command 'set', all others variable only for reading

The note 2: For correct definition by the Pilot of the majority of parameters of the character at you on the UO screen the Character Status window should be opened.


hour - current time (hour)

min - current time (minute)

sec - current time (second)
For example:
say current time is hour : min . sec

timer - considers(counts) quantity(amount) ms from a beginning of performance of the script. Can be used practically in any operators and combinations.
set timer // establishes value timer in 0

name - name of the character

str - force

int - intelligence

dex - dexterity 

hits - health 

mana - mana

stam - stamina

gold - amount of money 

wght - current weight

armor - armor class 

charposx - position on a horizontal

charposy - position on a vertical

charposz - z coordinate (height)

chardir - direction of a sight of the character (where the character revolves)
0 - the character looks at north, everyone 45 degrees of turn clockwise add 1. i.e. 7 - the character looks at northwest

lastmsg - last message of the server

lastobjectid - identifier of last used object [W]

lastobjecttype - type of last used object [W]

lasttargetid - identifier of last purpose [W]

lasttargetx - coordinate of last purpose [W]

lasttargety - - " - [W]

lasttargetz - - " - [W]

lasttargetkind - class of last purpose (1 - item; 2 - ground; 3 - static's or water) (i.e. if is necessary for you by a shovel click on a surface of the cave in the given coordinates, it is necessary to specify '3'; if it is necessary to click through 'lasttarget' on a item, it is necessary to specify '1' and 'Id' of a item; catching a fish we indicate coordinates of a point and class '2'). [W]

lastliftedid - identifier of a thing, which by last was touched from a place (is moved, has visited in 'hand'). [W]

lastskill - number last scill which was used through the menu Skills [W]

lastspell - number of last spell which was used through the book [W]

laststatictype - type of last static purpose (tree...) [W]

target - kind of the cursor (0 - hand; 1 - sight) [W]

At two or more started scripts you can address to variable, certain in other scripts of the pilot for others characters, having added to a name variable number of the script through a point. For example:
set lasttargetid.1 7
say hits.1


The conditional operators, cycles, transitions
==================================

In the conditional operators and cycles you can use the following operations: >, <, =, <>, and also logic operations (and, or, xor). The priorities are not present, is processed consistently.
For example:
if hour = 23 and min = 45 or #count = 100

For change of priorities use parentheses:
while (#a > 1 and #a < 3) or ((#a = 1 and 130, 9 7295) or #a = 5)

In the conditional operators you can use the generator of random numbers: random (number) returns number in a range from 0 up to number-1
For example:
while (#a = #b) or (random (5) > 3)

For interruption of action of the operators 'while', 'for' and 'repeat' you can use the command 'Break'. Syntax:
Break [a level]
If the level is more 1, interrupts given amount parental cycles.

The operator 'Continue' continues execution of a cycle on the following step. Can be used in cycles 'repeat', 'for', 'while'.

At use of last message from the server in the conditional operators, there is some rule of syntax:
if lastmsg the text of last message or its part
Or
if lastmsg = $a [or lastmsg = $b ...]
I.e. if directly is specified in a condition the text of the message, there should not be more nothing, including marks of any operations.


The operator IF
--------------------
Syntax:
if <condition>
...
end_if

Or

if <condition>
...
else
...
end_if

Or

if_not <condition>
...
end_if

Or

if_not <condition>
...
else
...
end_if

Three variants of conditions are possible:

1) Check any variable, syntax:
if <value> <a mark of operation> <value> 
The note: between is a mark of operation and values there should be a separator.
For example:
if hits < 45

2) Check of last message from the server:
If lastmsg <last message>
If in last message from the server there is a specified line
For example:
if lastmsg too heavy

3) Check of colour in the certain coordinates:
if <coordinate> <color> [color2]
If the color in a point <coordinate> is equal <color>
The note: if is given color2, the color of a point is checked on an accessory to a range from color up to color2. Take into account, that the check of color in the certain coordinates correctly works only at the unwrapped window of the UO.


The operator WHILE
----------------------------
Syntax:
While <condition>
...
end_while

Or

While_not <condition>
...
end_while

Three variants of conditions are possible:

1) Check any variable, syntax:
While <value> <a mark of operation> <value>
The note: between is a mark of operation and values there should be a separator.
For example:
While hits > 45

2) Check of last message from the server:
While lastmsg <last message>
To do(make) while in last message from the server there is a specified line
For example:
while lastmsg too heavy

3) Check of colour in the certain coordinates:
While <coordinate> <color> [color2]
While the color in a point <coordinate> is equal <color>
The note: if is given color2, the color of a point is checked on an accessory to a range from color up to color2
For example:
While 320 240 1489121


The operator FOR
------------------------

Syntax:
For #<name> <beginning> <end> [a step]
...
End_for
Cycle, with increase variable. If variable #<name> existed, it is replaced, differently is added. After end of a cycle variable is equal <end>. If the step is not specified, it is equal 1.
For example:
For #i 0 10 2

Take into account, that if you set boundary conditions of a cycle through variable, the pilot reads out values these variable at an input in a cycle and more value these variable does not check. Therefore change of borders of a cycle inside a cycle is impossible.


The operator REPEAT
-------------------------------

Repetition of actions the specified quantity of time
Syntax:
Repeat <number>
...
End_Repeat


The operator GOTO
---------------------------

Transition to the specified label
Syntax:
Goto <label>

The label should be specified in the script in the following syntax:
:<Label>

For example:
Goto end
:end


Call of the subroutines
-----------------------------------

Syntax of a call of the subroutine:
gosub <label>

Subroutine begins with
:<Label>
Also comes to an end
return

The subroutines it is recommended to have at the end of the script and before them to put either 'end_script', or 'goto' by the beginning of the script.


Call of procedure
------------------------------

Syntax of a call of procedure:
call <name>
The procedure with the specified name is searched at first in current script, and then, if not is found, in "a file of procedures" - script with number 99. To load there something it is possible with the help of the appropriate item of the menu. The enclosed call of procedures is supported.

Procedures it is possible to have in any place of the program. At detection of a beginning of procedure, its end is automatically searched, and the performance proceeds with next lines. The enclosed description is not supported.

The process of performance of procedure is not displayed, the parameters yet are not transferred.

Procedure begins with
proc <name>
Also comes to an end
end_proc

For example:
proc saying_message
say test passed
end_proc
call saying_message
end_script


Managements of work of the script
=========================


Closing-up of the script
--------------------------------------- -------

The script in a window is carried out step-by-step, from the first line to last, except for cases of transitions on the conditional operators, cycles, labels, and subroutines. After performance of last line the script automatically will repeat at first.

For the termination of performance of the script use the command:
End_Script
The parameters are not present.

Or command:
stop_script
Without the indication of any parameters.


Pauses
-----------

Wait <number> - to wait.
It is possible to set parameter <number> in various units of measurements:
wait 1 // 1 ms
wait 1s // 1 second
wait 1m // 1 minute
wait 1h // 1 hour

WaitForTarget [wait time] - to wait for "sight" (in ms).
Stops performance of the script, while the cursor in the UO will not take the form sight, or yet interval of time specified as parameter in ms will not expire. The default value for 'wait time' makes 10000 (that is 10 seconds).

pause_script
The command pause_script without the instruction of parameters stops performance of the current script. To start it again, you should set the command resume_script in the FRIEND SCRIPT with the link to number current (see following)


Management of work of other scripts
================================

You can operate work of other scripts started in other windows THIS UoPilot through below-mentioned commands. Thus as parameter <number> you specify number of a window of the appropriate script in the UoPilot.

start_script <number>
If the script with such number exists, it will be started

stop_script [number | all]
If the script with such number exists, it will be stopped

pause_script [number | all]
If the script with such number exists, it will be suspended

resume_script <number | all>
If the script with such number exists, its performance will be continued

In all these commands, except for first, instead of numbers of the script you can set parameter 'all' - then the action of the given command will be distributed on all scripts, loaded in all existing window of the UoPilot.

Concerning use of commands 'pause_script' and 'stop_script' without parameters - look previous.


Commands of the interface and call of the external programs
======================================= =====

Alarm [a file.wav]
Issues a sound signal contained in a file [a file.wav]. At a mistake of reproduction of a file (incorrect format), or if parameter [a file.wav] is not specified - the standard sound signal earlier contained in a file msg.wav is reproduced. If the file is not found, the command is ignored.
For example:
alarm welcome.wav

Msg [the text]
On the screen the window containing the specified text is deduced the performance of the script thus stops before closing a window. The window with the text is deduced atop of all windows.

Flash
To blink in taskbar. Thus in taskbar blinks a window of the Pilot. If you want, that should blink that window of the UO, to which the current script is adhered, specify the command flash with any parameter.
For example:
flash something

Exec <command> [parameters]
To start the specified application, to transfer it the specified parameters. For use as parameters reserved variable, put before them an attribute variable '#'.
Pay attention, that you use a mark '#' both for numerical variable, and for line!
For example:
exec c:\test.exe #name #lastmsg

Terminate <caption of a window>
To finish the specified application. It is necessary to use with care, differently it is possible to closing at all that would be desirable.

macro_load <a name of a file>
To load the macros, earlier written down and kept in a file. If not the path is specified, is searched in the UoPilot folder.

macro_play [number]
To start loaded macros [number] times, and to wait ending its performance. If [number] =0 - macros will be carried out indefinitely, by default once. To stop or start manually it is possible by standard shortcuts.


Commands of work with the mouse
=======================

All commands of work with the mouse, and also some other require the indication of coordinates. The pilot supports two ways of the indication of coordinates: absolute coordinates (coordinate of a point from the left top corner of the screen) and relative coordinates (coordinate of a point from the left top corner of the UO screen. The caption of a UO window is not taken into account). Set in the scripts of coordinate you can, having guided the cursor of the mouse on a necessary point and having pressed a combination Ctrl-A. Thus remember:

1) The window of the UoPilot should be active. That is arrange a window of the UO under a window of the pilot, choose a window of the pilot, guide the cursor of the mouse, the necessary point NOT PRESSING ON BUTTONS of the MOUSE and press Ctrl-A.

2) In a window of the pilot one of tags 'Automatically  insert relative point coordinates into script' or 'Automatically  insert Absolute point coordinates into script'. Otherwise, the coordinates can be inserted into the script manually, click by the mouse on the button with coordinates

3) If you specify in commands absolute coordinates (it is impossible to use in the command drag) - you it is necessary after coordinates to specify of the identifier of absolute coordinates - a keyword "abs", being in last parameter in the command.
For example:
double_left 218, 242 abs

On execution time of commands of work with the mouse on absolute coordinates, there is a capture of the mouse.

Move <coordinate>
Moves the cursor to the specified coordinates.
Attention! It is extremely recommended to set this command before the task any of two below-mentioned commands.

Left <coordinate>
To click the left key of the mouse 1 time in the specified coordinates

Right <coordinate>
To click the right key of the mouse 1 time in the specified coordinates

Double_Left <coordinate>
To click the left key of the mouse 2 times in the specified coordinates

Double_Right <coordinate>
To click the right key of the mouse 2 times in the specified coordinates

left_down <coordinate>
Presses the left button of the mouse in the specified coordinates

left_up <coordinate>
Releases the left button of the mouse in the specified coordinates

right_down <coordinate>
Presses the right button of the mouse in the specified coordinates

right_up <coordinate>
Releases the right button of the mouse in the specified coordinates


Other commands
==============

Send <a key [a pause]> | <the text>
"To press" a key and to wait the specified number ms. If parameter is not recognized as a managing key, it is sent as the text. In the latter case command works similarly to command say, except for finishing 'Enter'.

Sendex < the list of keys >
"To press" consistently some keys. Sends practically all combinations of keys. The keys Ctrl, Alt, Shift are coded by symbols ^, @ and ~ accordingly. All function keys should be made in braces, for example: {Enter}. In one command there can be a whole offer from keys:
sendex ~closing ~application @{f4}
There is a following property: the application will accept only those keys (symbolical), which correspond established in it layout of the keyboard.
In execution time of the command, the application should be active and on it the focus should be directed.

Drag <whence> <where> [amount]
To transfer from a point with coordinates <whence>, to a point with coordinates <where>, specified amount of items. The coordinates <whence> and <where> can be only relative. If not to specify amount, one will be transferred a not stacked item (the window with amount does not emerge) if to specify 'all', all items will be transferred.
For example:
Drag #x #y 320, 240

Say [the text]
To type the text and to press Enter. For example:
say my x: coordx y: coordy and armor: ar



================================