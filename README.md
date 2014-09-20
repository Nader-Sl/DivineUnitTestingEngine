# API Tester for BoL 2.0

## What is it?
This contains a special **API Tester** class and multiple **API tests** which help to find what is bugged out after new L patches.
Among present tests there are also few test-demos which demonstrate some bugs I've found.

## Hotkeys:
- **L** - runs **next** test
- **J** - runs **previous** test

Some tests may be performed automatically, in this case it will automatically start next test. Read console/chat during testing for more information.

## Important:
During automatic testing please don't use any spells and don't move your hero.


## TODO:
1. Add **initial** test, which tests common stuff like **_Utility.DelayAction_** and other stuff, which is required to perform basic tests.
2. Modify **current** myHero methods tests to also test for specific used **members** (such as **_myHero.pos_**, **_myHero.visionPos_**, **_myHero.isMoving_**, etc).