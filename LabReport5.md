
# Lab Report 5

For Lab Report 5, I chose to redo Lab Report 4 but this time with a bash
script to make everything much much quicker.
This script logs into the secure shell and redirects the local script
to standard in for the ssh.

The local script then git clones the correct files, 
compiles the files and runs the tester.
Once the failed tests have been displayed, the script automatically
corrects the error in the code using the 'sed' command, then re-compiles
and reruns the tests.
After that, the script automatically git adds the changed file,
git commits it with the message "Committed"
and then git pushes the changed file before exiting the remote server.

SSH script:
```
#!/bin/bash -e

ssh cs15lwi23adc@ieng6.ucsd.edu  'bash -s' < script.sh
```

Command script:
```
#!/bin/bash -e
  
git clone  https://github.com/JGalil/lab7.git
  
cd  lab7
  
javac -cp  .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar  *.java
  
java -cp  .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar 
#these are two separate lines because the save to pdf bugged
#otherwise
org.junit.runner.JUnitCore  ListExamplesTests

  
sed -i  '43s/index1/index2/'  ListExamples.java
  
git commit
  
javac -cp  .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar  *.java
  
java -cp  .:lib/hamcrest-core-1.3.jar:lib/junit-4.13.2.jar  
#these are two separate lines because the save to pdf bugged
#otherwise
org.junit.runner.JUnitCore  ListExamplesTests

  
git add  .  ListExamples.java

git commit  ListExamples.java  -m  "Committed"

git push

exit
```

Here is a picture of what the code looks like when it runs:


![image](https://user-images.githubusercontent.com/122497361/224590807-78971b4c-7ca6-456a-83ec-e1ddc4ff544e.png)

