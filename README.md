## In class exercise

1. If you wanted to reuse this program for a file that had 17 headers lines. What line of code
would you change in our program?

        Write the line of code that you will replace here:__
You would have to mpdify this line: if LineNumber > 0
        What will be the new code?
you would change number 0 to the appropiate headers 
        Write the new code here:___
You would have to modify to this: LineNumber > 17:

2. would happen if we don’t included `import sys` in our program?

        Write you answer here:___
Then the commands that are part of sys will not function. Python will not recognize them.

3. Let’s suppose that the third file that the user provides as input
has only one column. What error message will be generated?

        Write you answer here:___
MasterList[RecordNum] += ('\t' + ElementList[1]) # += adding instead of replacing
IndexError: list index out of range

4. Our program split lines of input files (except the first file) into elements
that are tab delimitated. However, data could be split by `,` or many other
characters. In this case is a good idea to define a new variable that takes the delimiter
provide by the user. Using what you learn about `sys.argv` in this class`.
Write a variable that reads a delimiter (e.g ',') provided as the first input file.

        Write your code here#!/usr/bin/env python
Usage = """
Mergefiles.py - version 1.0
Convert a series of X Y tab-delimited files
to X Y Y Y format and print them to the screen.
Usage:
        python Mergefiles.py *.txt > combinedfile.dat
"""

import sys
import re

if len(sys.argv) < 2:
    print Usage
else:
    FileList= sys.argv[1:]
    FileNum = 0
    MasterList = []
    Header = "lambda"
    for InfileName in FileList: # statement done one per line
        Header += "userdelimiter" + re.sub('.txt','', InfileName)
        Infile = open(InfileName, 'r')
        # The line number within each file, resets for each file
        LineNumber = 0
        RecordNum = 0 # The record number within the table
        for line in Infile:
            if LineNumber > 0: #skipe first line
                Line=line.strip('\n')
                if FileNum == 0:
                    MasterList.append(Line)
                else:
                    ElementList = Line.split('\t')
                    if len(ElementList) > 0:
                        MasterList[RecordNum] += ('\t' + ElementList[1]) # += adding instead of replacing
                        RecordNum += 1
                    else:
                        sys.stderr.write("Line %d not XY format in file %s\n" % (LineNumber,InfileName))
            LineNumber += 1
        Infile.close()
        FileNum += 1 # the last stament in the file loop

    print(Header)
    for Item in MasterList:
        print(Item)

    sys.stderr.write("Converted %d file(s)\n" % FileNum):__
