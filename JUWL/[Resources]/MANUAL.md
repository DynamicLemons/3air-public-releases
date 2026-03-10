# Character Creation
##  Character ID/Init

Each character has an associated "ID-String". This is used for *all* of ECF's built handling for characters.  
The format for a character id is: `[Developer/Project]-[Character]`. For this document, I will be using `Sample-Rabbit`.  

To add a character to be properly handled, you will initialize them as follows.
```
function void ECF_buildCharList()
{
	ECF_allocChar("Sample-Rabbit")
	base.ECF_buildCharList()
}
```
This will automatically add them to the character internal list, and give them a "ID-Index".  

This Id is also used for sprite asset titles. (ie. `character_Sample-Rabbit_0xba`)
## Configuration

ECF comes with a couple of "configuration" functions, intended to lift some more menial work for you. These generally will all have a ID-String expected as an input.  
These are all within `engine\charfuncts.lemon`, along with other utility functions.  
A character's Display Name is handled via `ECF_getCharDisplayName([name])`, for example.  

Most importantly, each character has an expected "base-husk"- which they will use their respective object and code-hooks.  
This is intended to allow custom characters to "inherit" properties from a base-cast character (Sonic, Tails, or Knuckles).  
The game will read you as playing as your husk, and the engine will apply changes above that. (ie. A character based on Sonic will "internally" save as Sonic.)

## By-Default Changes (When Playing as a Custom Character)
- Character abilities are removed by default, to let you add in your abilities without having to remove the existing code first.
- Bits of game have been adjusted to allow for custom character heights to work a bit more automatically.
- ECF inherit some additions from *Yeah, you want "these" renderhooked, right? So here you go. Now, do something!* Allowing you to modify a couple more assets that base cast cannot touch by default, such as data select icons and the slot machine wheel.
- The Marble Garden Act 2 Boss (Egg Drillster Mk. 2) automatically removes Tails and replaces him with a much more character-neutral option- the Boss Top.
- The Signpost only spins between your character and Eggman.
- The Tornado's pilot will be Sonic.
- The Doomsday Zone is not visited in a campaign.
- The Best Ending Screen will only show your current played character.
- Tails is also removed in Carnival Night and Mushroom Hill. 
- The Bluespheres minigame screen's "bumpers" have been changed to "bobbles", to make the character selection a bit more obvious.

## Checking For your Character

`isECFCharAt(u32 address, string name)` is generally what you'll be using for your code-hooks/base-returns, `isECFCharA0` and `isECFCharA1` also exist as short-hands for that function call.  
`isECFCharP[player number]` also exists, and is a different way to check for such.

The former is equivalent to checking the `char.character` value on a player object, while the latter is equivalent to `isMainCharacter/isSecondCharacter`.
If a string variable is 0, it is assumed that it is base-cast.

# Framework Notes

## Character Registering
When `Init()` gets run, ECF starts a chain where it will store a character list where characters will be stored in order in a set of global variables.
*As I'm writing this, write-access arrays don't exist in Lemonscript yet.*  
ECF also implies numerical-ids for custom characters, though they are used as short hand for the string-id, and are entirely dependant on load order.
(ie. if "Sample-Rabbit" is passed first, it's inherent numerical-id would be 1.)
Numerical-id 0 is also used for data-select 

The framework holds a upper-character limit of 20, but if you wish, you can adjust this manually by changing the constant `ECF_charList_size` and indexing a couple more global variables.

## ...Mod Compatibility
ECF should generally be able to be accounted for via other mods. (It comes with a preprocessor check `EXTRA_CHARACTER_FRAMEWORK_ACTIVE`, even!)  

# ...
~ Lemm
