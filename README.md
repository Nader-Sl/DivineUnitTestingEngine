# Divine APITestsLoader for BoL 2.0

## What is it?

It is a generic module-based BoL 2.0 API tester offering a neat dependencies handling architecture, which serves the purpose of automatically testing BOL 2 API features to check whether a certain part of the API is broken and what not, it can also be used to test your own functions separately from your script.


## How Does it work?
The main.add which is the APITestsLoader will load all other tests (modules) contained in the same directory which follow a specific syntax, then when you come to choose the test that you want to run (via hotkeys), it will check if it relies on dependencies, which are other tests in the same dir, in case it does, it will check the whole dependency tree to make sure whether the currently selected test is eligible for testing or not, this check can either have ***dependencies status caching*** on or off, described in details below in the hotkeys section below.
Every step in the process is logged to 3 outputs, the Console,Game Chat, and a Log file created in the same dir for reviewing.

## How to use:
All the modules (tests) should follow a certain syntax where all the required field should be added and defined to each test taking into consideration the supported comments next to each:
```lua
 _G.TestA = {}

--{{ INITIALIZE ALL CONSTANTS HERE! ]]--
TestA.name = "Test A" -- REQUIRED FIELD
TestA.desc = "This is a Description for TestA" --REQUUIRED FIELD
--[[
INITIALIZE ALL VARIABLES IN THE INIT METHOD TO AVOID VALUES CACHING, WHEN TEST IS RAN AGAIN THIS METHOD IS CALLED AGAIN TO RE INITIALIZE THE VALS.
]]
function TestA.Init() -- THIS STRUCT SHOULD BE DEFINED IN THE _G ENV AND SHOULD MATCH WITH THE TEST FILE'S NAME.
TestA.dependencies = {_G.TestC,_G.TestB}  -- REQUIRED FIELD (MUST BE DEFINED IN INIT())
TestA.status = UNKNOWN -- REQUIRED FIELD
TestA.i = 0
end

 --[[
   DEFINE BOL 2.0 CALLBACK FUNCTIONS IN THE TEST'S STRUCT CONTEXT (function names should exactly match BoL 2.0's Callback names)
   {Tick,Draw,etc..} 
   ]]
function TestA.Tick()
TestA.i = TestA.i + 1
if TestA.i >= 50 then TestA.status = math.random(1,10) < 5 and SUCCESS or FAIL end
end

function TestA.Draw()

 Graphics.DrawText("Tick Count : "..TestA.i, 12, 100,100, Graphics.ARGB(255,255,255,255))

end

```
## HOTKEYS
<pre style="color: red">
* Press "l" to jump to next test.
* Press "j" to jump to previous test.
* Press "k" to repeat current test.
* Toggle "i" to enable/disable dependencies status caching. (On by default)
</pre>
<p><u><b>What Is Dependencies Status Caching?</b></u></p>
 When dependencies status caching is on, this means that on the next test you run, it will check for the dependency cached status in case it has been ran previously, in case the status was "SUCCESS", it will not re-run the dependency and consider it successful, otherwise if the status was "Fail" or the dep wasn't previously ran, then it will re-run the dep.
 
 When dependency status caching is off, this means a test will always run the whole tree of dependencies it has, even if they were marked as successful previously in case they were ran.

