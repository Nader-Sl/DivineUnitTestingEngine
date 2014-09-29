# Divine Unit Testing (DUT) Framework for BoL 2.0

## What is it?

It is a generic module-based BoL 2.0 API tester offering a neat dependencies handling architecture, which serves the purpose of automatically testing BOL 2 API features to check whether a certain part of the API is broken and what not, it can also be used to test your own functions separately from your script.


## How Does it work?
The main.add which is the main unit tester will load all other tests (modules of a certain syntax) contained in the same directory, after which that you choose the test you want to run (via hotkeys described below), it will check whether it relies on certain modules(other tests within same dir) referred to as <b>dependencies</b>, in case it does, it will iterate the whole dependency tree checking if they were successful to decide whether the currently selected test is eligible for testing or not, this check can either have ***dependencies status caching*** on or off, described in details below in the <b>Hotkeys</b> section below.
Note that every step in the process is logged to 3 outputs, the Console,Game Chat, and a Log file created in the same dir for reviewing.

<p><b>Log Output Example</b></p>
```
--------------------------------22:28:53-------------------------------
(Caching is On)


>Started Test[Test D] Desc [This is a Description for TestD] dependencies [none]
>Test D Was Successful!
>Started Test[Test B] Desc [This is a Description for TestB] dependencies [none]
>Test B Failed!
>Started Test[Test F] Desc [This is a Description for TestF] dependencies [Test C]
>Test F's dependency : Test C is of an unknown status , switching to test Test C
>Started Test[Test C] Desc [This is a Description for TestC] dependencies [Test B | Test D]
>Test C's dependency : Test B has been marked as FAILED , re-checking test [Test B]
>Started Test[Test B] Desc [This is a Description for TestB] dependencies [none]
>Test B Failed!
>Test B Failed , Retrying[1] because test Test C is depending on this
>Started Test[Test B] Desc [This is a Description for TestB] dependencies [none]
>Test B Failed!
>Test B Failed , Retrying[2] because test Test C is depending on this
>Started Test[Test B] Desc [This is a Description for TestB] dependencies [none]
>Test B Was Successful!
>Going back to test Test C
>Started Test[Test C] Desc [This is a Description for TestC] dependencies [Test B | Test D]
>Test C's dependency : Test B has been marked as SUCCESS [OK]
>Test C's dependency : Test D has been marked as SUCCESS [OK]
>Test C Was Successful!
>Going back to test Test F
>Started Test[Test F] Desc [This is a Description for TestF] dependencies [Test C]
>Test F's dependency : Test C has been marked as SUCCESS [OK]
>Test F Failed!
>Divine Unit Testing has been terminated by user
```

## How To Use?
#### *Hotkeys:
<pre style="color: red">
* Press <b>"l"</b> to jump to next test.
* Press <b>"j"</b> to jump to previous test.
* Press <b>"k"</b> to repeat current test.
* Toggle <b>"i"</b> to enable/disable dependencies status caching. (On by default)
</pre>
<p><u><b>*What Is Dependencies Status Caching?</b></u></p>
 When dependencies status caching is on, this means that on the next test you run, it will check for the dependency cached status in case it has been ran previously, in case the status was <b>"SUCCESS"</b>, it will not re-run the dependency and consider it successful, otherwise if the status was <b>"Fail"</b> or the dep wasn't previously ran, then it will re-run the dep.
 
 When dependency status caching is off, this means a test will always run the whole tree of dependencies it has, even if they were marked as successful previously in case they were ran.

