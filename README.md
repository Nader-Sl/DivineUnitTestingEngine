# API Tester for BoL 2.0

## What is it?
This contains a special **API Tester** class and multiple **API tests** which help to find what is bugged out after new L patches.
Among present tests there are also few test-demos which demonstrate some bugs I've found.

## How to use:
The **main point** of this tester is to fill it with **fully _automated_ tests** as much as possible, so they will start on their own as soon as script is loaded and game is started.
Basically you just have to load it and **let it do the job**. Additionally you can switch between tests (go back or forward through tests) with **_hotkeys_**.

## Hotkeys:
- **L** - runs **next** test
- **J** - runs **previous** test

Some tests may be performed automatically, in this case it will automatically start next test. Read console/chat during testing for more information.

## Important:
During automatic testing please don't use any spells and don't move your hero.



## Script related tasks:
### ToDo:
1. Modify **current** myHero methods tests to also test for specific used **members** (such as **_myHero.pos_**, **_myHero.visionPos_**, **_myHero.isMoving_**, etc).

### Done:
* Add **initial** test, which tests common stuff like **_Utility.DelayAction_** and other stuff, which is required to perform basic tests.


## Spudgy's bugs farm:
### Unfixed:
1. If there is **_Graphics.DrawLine()_** and **_Render.Line_** with same **_width_** - it bugs out and draws only one of them.
2. **_myHero.animation_** is still buggy.
3. **_Callback.Unbind()_** is often causing bugsplats.
5. **_"GameStart"_** callback gets triggered before actual game start if you reload the script during loading screen.

### Fixed:
1. Calling **_myHero.level_** is causing bugsplats
2. **_Graphics.DrawText()_** completely ignores **_size_** parameter
3. Didn't find **_WINDOW_W_**, **_WINDOW_H_** alternatives.
4. [Note: We don't really need it] Separate BoL 1.0 like **_GetTextArea()_** function. Right now it's inside **_Render.Text_** class, but it won't hurt to have it as standalone additionally.