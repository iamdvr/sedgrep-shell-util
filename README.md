# sedgrep-shell-util

Handles multi line logs efficiently...

One need to tell the start line pattern and the word to grep for...

Default NEW_LINE_PATTERN is ^\[

#Usage : 

    cat {INPUT_FILE_NAME}  | sedgrep  {NEW_LINE_PATTERN} {THREAD_OR_SEARCH_PATTERN} 
    cat {INPUT_FILE_NAME}  | sedgrep  {THREAD_OR_SEARCH_PATTERN} 
    sedgrep {NEW_LINE_PATTERN} {THREAD_OR_SEARCH_PATTERN} {INPUT_FILE_NAME}
    sedgrep {THREAD_OR_SEARCH_PATTERN} {INPUT_FILE_NAME}
    
#Example : 

    cat sampleInput.log | sedgrep 2016-05-23 DB_CONN
    cat sampleInput.log | sedgrep DB_CONN
    sedgrep 2016-05-23 DB_CONN sampleInput.log
    sedgrep DB_CONN sampleInput.log

Verify how it works...

Lets say you have file with content as below... (Assume filename is test.txt)
```
[2020-10-21 12:31:54,140]-TESTAPP[DEBUG][log4jsample.LogTest](main){}My First Log Line
[2020-10-21 12:31:54,140]-TESTAPP[DEBUG][log4jsample.LogTest](main){}My Second Log Line
[2020-10-21 12:31:54,140]-TESTAPP[DEBUG][log4jsample.LogTest](main){}My Thrid Log Line
[2020-10-21 12:31:54,140]-TESTAPP[ERROR][log4jsample.LogTest](main){}My Error1 Trace Line
java.lang.IllegalArgumentException: Something wrong in arguments
	at log4jsample.LogTest.main(LogTest.java:19) [classes/:?]
[2020-10-21 12:31:54,146]-TESTAPP[DEBUG][log4jsample.LogTest](main){}My Fourth Log Line
[2020-10-21 12:31:54,146]-TESTAPP[ERROR][log4jsample.LogTest](main){}My Error2 Trace Line
java.lang.IllegalArgumentException: Second time wrong in arguments
	at log4jsample.LogTest.main(LogTest.java:21) [classes/:?]

```
## If we have to grep for ERROR logs along with traces use below command
  
    cat test.txt |sedgrep ERROR   
    
Sample Output

    [2020-10-21 12:31:54,140]-TESTAPP[ERROR][log4jsample.LogTest](main){}My Error1 Trace Line
    java.lang.IllegalArgumentException: Something wrong in arguments
        at log4jsample.LogTest.main(LogTest.java:19) [classes/:?]
    [2020-10-21 12:31:54,146]-TESTAPP[ERROR][log4jsample.LogTest](main){}My Error2 Trace Line
    java.lang.IllegalArgumentException: Second time wrong in arguments
        at log4jsample.LogTest.main(LogTest.java:21) [classes/:?]



## If we have to grep for DEBUG logs along with traces use below command
  
    cat test.txt |sedgrep DEBUG   
    
Sample Output

    [2020-10-21 12:31:54,140]-TESTAPP[DEBUG][log4jsample.LogTest](main){}My First Log Line
    [2020-10-21 12:31:54,140]-TESTAPP[DEBUG][log4jsample.LogTest](main){}My Second Log Line
    [2020-10-21 12:31:54,140]-TESTAPP[DEBUG][log4jsample.LogTest](main){}My Thrid Log Line
    [2020-10-21 12:31:54,146]-TESTAPP[DEBUG][log4jsample.LogTest](main){}My Fourth Log Line

## If we have to grep for "My Error2" log line along with traces use below command
  
    cat test.txt |sedgrep "My Error2"   
    
Sample Output

    [2020-10-21 12:31:54,146]-TESTAPP[ERROR][log4jsample.LogTest](main){}My Error2 Trace Line
    java.lang.IllegalArgumentException: Second time wrong in arguments
        at log4jsample.LogTest.main(LogTest.java:21) [classes/:?]


