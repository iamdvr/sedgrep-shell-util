# sedgrep-shell-util

Handles multi line logs efficiently...

One need to tell the start line pattern and the word to grep for...

#Usage : 

    cat {INPUT_FILE_NAME}  | sedgrep  {DATE_PATTERN} {THREAD_OR_SEARCH_PATTERN} 
    
    cat {INPUT_FILE_NAME}  | sedgrep  {THREAD_OR_SEARCH_PATTERN} 
    
    sedgrep {DATE_PATTERN} {THREAD_OR_SEARCH_PATTERN} {INPUT_FILE_NAME}
    
    sedgrep {THREAD_OR_SEARCH_PATTERN} {INPUT_FILE_NAME}
    
#Example : 

    cat sampleInput.log | sedgrep 2016-05-23 DB_CONN
    
    cat sampleInput.log | sedgrep DB_CONN
    
    sedgrep 2016-05-23 DB_CONN sampleInput.log
    
    sedgrep DB_CONN sampleInput.log
    
