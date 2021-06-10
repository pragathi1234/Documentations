#! /bin/bash

### **ECHO COMMAND**
echo Hello World!

### **VARIABLES**  
Uppercase by convention  
Letters, numbers, underscores  
NAME="Bob"  
echo "My name is $NAME"  
echo "My name is ${NAME}"  

### **USER INPUT** 
read -p "Enter your name: " NAME  
echo "Hello $NAME, nice to meet you!"  

### **SIMPLE IF STATEMENT**
if [ "$NAME" == "Brad" ]  
then  
&nbsp;&nbsp;&nbsp;&nbsp;echo "Your name is Brad"  
fi  

### **IF-ELSE**
if [ "$NAME" == "Brad" ]  
then  
&nbsp;&nbsp;&nbsp;&nbsp;echo "Your name is Brad"  
else   
&nbsp;&nbsp;&nbsp;&nbsp;echo "Your name is NOT Brad"    
fi

### **ELSE-IF (elif)**  
if [ "$NAME" == "Brad" ]  
then  
&nbsp;&nbsp;&nbsp;&nbsp;echo "Your name is Brad"  
elif [ "$NAME" == "Jack" ]  
then    
&nbsp;&nbsp;&nbsp;&nbsp;echo "Your name is Jack"  
else   
&nbsp;&nbsp;&nbsp;&nbsp;echo "Your name is NOT Brad or Jack"
fi

### **COMPARISON**
NUM1=31  
NUM2=5  
if [ "$NUM1" -gt "$NUM2" ]  
then  
&nbsp;&nbsp;&nbsp;&nbsp;echo "$NUM1 is greater than $NUM2"  
else  
&nbsp;&nbsp;&nbsp;&nbsp;echo "$NUM1 is less than $NUM2"  
fi  

########  
val1 -eq val2 Returns true if the values are equal  
val1 -ne val2 Returns true if the values are not equal  
val1 -gt val2 Returns true if val1 is greater than val2  
val1 -ge val2 Returns true if val1 is greater than or equal to val2  
val1 -lt val2 Returns true if val1 is less than val2  
val1 -le val2 Returns true if val1 is less than or equal to val2  
########



### **FILE CONDITIONS**
FILE="test.txt"  
if [ -e "$FILE" ]  
then  
&nbsp;&nbsp;&nbsp;&nbsp;echo "$FILE exists"  
else  
&nbsp;&nbsp;&nbsp;&nbsp;echo "$FILE does NOT exist"  
fi  
 
########  
-d file   True if the file is a directory  
-e file   True if the file exists (note that this is not particularly portable, thus -f is generally used)
-f file   True if the provided string is a file  
-g file   True if the group id is set on a file  
-r file   True if the file is readable  
-s file   True if the file has a non-zero size  
-u    True if the user id is set on a file  
-w    True if the file is writable  
-x    True if the file is an executable  
########

### **CASE STATEMENT**
read -p "Are you 21 or over? Y/N " ANSWER  
case "$ANSWER" in    
&nbsp;&nbsp;&nbsp;&nbsp;  [yY] | [yY][eE][sS])  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;echo "You can have a beer :)"  
&nbsp;&nbsp;&nbsp;&nbsp;   ;;  
&nbsp;&nbsp;&nbsp;&nbsp;  [nN] | [nN][oO])  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;echo "Sorry, no drinking"  
&nbsp;&nbsp;&nbsp;&nbsp;   ;;  
&nbsp;&nbsp;*)  
&nbsp;&nbsp;echo "Please enter y/yes or n/no"  
&nbsp;&nbsp;;;  
esac

### **SIMPLE FOR LOOP**
NAMES="Brad Kevin Alice Mark"  
&nbsp;&nbsp;&nbsp;&nbsp;for NAME in $NAMES  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;do  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   echo "Hello $NAME"  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;done

### **FOR LOOP TO RENAME FILES**
FILES=$(ls *.txt)  
NEW="new"  
for FILE in $FILES    
&nbsp;&nbsp;&nbsp;&nbsp;  do  
&nbsp;&nbsp;&nbsp;&nbsp;    echo "Renaming $FILE to new-$FILE"  
&nbsp;&nbsp;&nbsp;&nbsp;    mv $FILE $NEW-$FILE  
done  

### WHILE LOOP - READ THROUGH A FILE LINE BY LINE

LINE=1

while read -r CURRENT_LINE  
  do  
&nbsp;&nbsp;&nbsp;&nbsp;echo "$LINE:   
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;$CURRENT_LINE"  
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;   ((LINE++))

done < "./new-1.txt"

### **FUNCTION**
function sayHello() {

  echo "Hello World"

}  
sayHello

### **FUNCTION WITH PARAMS**
function greet() {  
&nbsp;&nbsp;&nbsp;&nbsp;echo "Hello, I am $1 and I am $2"  
}

greet "Brad" "36"

### **CREATE FOLDER AND WRITE TO A FILE**
mkdir hello  
touch "hello/world.txt"  
echo "Hello World" >> "hello/world.txt"  
echo "Created hello/world.txt"