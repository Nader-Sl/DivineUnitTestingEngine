# Divine APITestsLoader for BoL 2.0

## What is it?

It is a generic module-based BoL 2.0 API tester offering a neat dependencies handling architecture, which serves the purpose of automatically testing BOL 2 API features to check whether a certain part of the API is broken and what not, it can also be used to test your own functions separately from your script.


## How Does it work?:
The main.add which is the APITestsLoader will load all other tests (modules) contained in the same directory which follow a specific syntax, then when you come to choose the test that you want to run (via hotkeys), it will check if it relies on dependencies, which are other tests in the same dir, in case it does, it will test run the whole dependency tree to make sure whether the currently selected test is eligable for testing or not.

## How to use:
All the modules (tests) should follow a certain syntax where all the required field should be added and defined to each test taking into consideration the supported comments next to each:

 _G.TestA = {} -- THIS STRUCT SHOULD BE DEFINED IN THE _G ENV AND SHOULD MATCH WITH THE TEST FILE'S NAME.

 --{{ INITIALIZE ALL CONSTANTS HERE! ]]--
 TestA.name = "Test A" -- REQUIRED FIELD
 TestA.desc = "This is a Description for TestA" --REQUUIRED FIELD
 
 --[[
 INITIALIZE ALL VARIABLES IN THE INIT METHOD TO AVOID VALUES CACHING, WHEN TEST IS RAN AGAIN THIS METHOD IS CALLED AGAIN TO RE INITIALIZE THE VALS.
 ]]
 function TestA.Init() 
 TestA.dependencies = {_G.TestC,_G.TestB}  -- REQUIRED FIELD (MUST BE DEFINED IN INIT())
 TestA.status = UNKNOWN -- REQUIRED FIELD
 TestA.i = 0
 
 end
 --[[
   DEFINE BOL 2.0 CALLBACK FUNCTIONS IN THE TEST'S STRUCT CONTEXT (function names should exactly match BoL 2.0's Callback names)
   {Tick,Draw,etc..} 
   ]]
   
  function TestA.Tick()
  --log("TestATick"..TestA.i)
  TestA.i = TestA.i + 1
  if TestA.i >= 50 then TestA.status = math.random(1,10) < 5 and SUCCESS or FAIL end
 end 
 
 function TestA.Draw() 

  Graphics.DrawText("Tick Count : "..TestA.i, 12, 100,100, Graphics.ARGB(255,255,255,255))

 end


- **L** - runs **next** test
- **J** - runs **previous** test

Some tests may be performed automatically, in this case it will automatically start next test. Read console/chat during testing for more information.

## Important:
During automatic testing please don't use any spells and don't move your hero.



## Script related tasks:
#### ToDo:
1. Modify **current** myHero methods tests to also test for specific used **members** (such as **_myHero.pos_**, **_myHero.visionPos_**, **_myHero.isMoving_**, etc).

#### Done:
* Add **initial** test, which tests common stuff like **_Utility.DelayAction_** and other stuff, which is required to perform basic tests.


## Spudgy's bugfarm:
#### Unfixed:
1. If there is **_Graphics.DrawLine()_** and **_Render.Line_** with same **_width_** - it bugs out and draws only one of them.
2. **_myHero.animation_** is still buggy.
3. **_Callback.Unbind()_** is often causing bugsplats.
5. **_"GameStart"_** callback gets triggered before actual game start if you reload the script during loading screen.

#### Fixed:
* Calling **_myHero.level_** is causing bugsplats
* **_Graphics.DrawText()_** completely ignores **_size_** parameter
* Didn't find **_WINDOW_W_**, **_WINDOW_H_** alternatives.
* [Note: We don't really need it] Separate BoL 1.0 like **_GetTextArea()_** function. Right now it's inside **_Render.Text_** class, but it won't hurt to have it as standalone additionally.