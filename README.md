# udemy-programming-course

#### Links

- [course application - just-gif-it ](http://github.com/dustinschultz/just-gif-it)

#### Unique characters

##### Commands

- clear the screen

  ```sh
  clear
  ```

- add permissions to execute the file

  ```sh
  chmod +x first.sh
  ```

###### vim commands

- edit `i`
- write-quit-force `escape wq!`
- write `escape w`
- quit without saving `escape q`

##### Characters

- `#` - hash character - info for the system how to interpret the file `#!/bin/bash`
- `echo` - print on the console `echo "adadfaff"`
- `#whatever you type, will be ignored` comments 
- `${#name}` - display length of variable tea 
- `;` - end of the command
-  `$(( 2#111 ))`  - binary 7 to decimal
-  `cd ..` go 1 level up
-  `.` -  current directory
- `echo "\"Linux is awesome\""` escaping 
- `then :` do nothing  
-  `rm test*` remove everything starting with **test**
- `cd ~` go to current directory 
- `cd ~-` got to previous directory 

- many commands in one line

  ```sh
  # variable declaration
  var=10
  # sign ';' stands for end of line
  # if [ CONDITION ] then ... fi
  #-gt == >
  if [ "$var" -gt 0 ]; then echo "YES"; else echo "NO"
  fi
  ```

- single  `'  '` does not allow referencing variables

- double `" "` prevent from using special characters ie. word splitting

- displaying strings in a loop one by one

  ```sh
  colors="red black white"
  for col in $colors
  do
          echo $col
  done
  ```


- change variable to lowercase or uppercase

  ```sh
  var=DSLCoNnEctioN
  #change first letter to lowercase
  echo ${var,}
  #change all letters to lowercase
  echo ${var,,}
  #change first letter to uppercase
  echo ${var^}
  #change all letters to uppercase
  echo ${var^^}
  ```


- Assign echo results to a variable

  ```sh
  #let is used for calculations
  let val=500/2
  val2=`echo $val`
  echo "$val2"
  ```


- redirecting 

  ```sh
  #redirect text to the file (overwrite)
  echo "something else" > wood.txt
  #redirect text to the file (add to the end)
  echo "something more" >> wood.txt
  #clear the file
  echo : > wood.txt
  ```

- multiplication and exponentiation

  ```sh
  #multiplication
  let var=10*100
  #exponentiation
  let var2=2**3
  #1000 8
  echo "$var $var2"
  ```

- if..else inline

  ```sh
  var1=10
  echo $(( var2 = var1<20?1:0))
  ```

-  parenthesis

  ```sh
  var=5
  (var=10;)
  # value in () wont be taken into account by the script 
  echo $var
  ```

- curly brackets

  ```sh
  #displays list $test1$ $test2$..
  echo \${test1,test2,test3}\$
  #list from 0 to 9
  echo {0..9}
  ```

  ```sh
  var1=1
  var2=2
  #anonymous method
  {
    var1=11
    var2=12
  }
  #1 2
  echo "$var1 $var2"
  ```


- AND, OR

  ```sh
  #logical OR
  if [ "$var" -gt 0 ] || [ "$var" -eg 10 ]
  #logical AND
  if [ "$var" -gt 0 ] && [ "$var" -eg 10 ]
  ```

- modulo `let var=5%4` 

- Upper case

  ```bash
  someWord=tEsT
  # changes first character to upper case 
  echo ${someWord^}
  
  # changes all characters to upper case 
  echo ${someWord^^}
  ```

#### Variables and Parameters

##### Part 1 

```bash

var=10
# displays name of variable
echo var
# displays value of variable
echo $var

unset var
# displays nothing
echo $var

# in this specific example $ sign is not needed
var1=4
(( var2=var1<10?1:0))
echo $var2

# reading from the termninal
echo "type in some value"
read var2
echo $var2

# var is assigned with each element on the list 
for var in 1 2 3
do
    echo "Value of var is $var"
done    
```

##### Part 2

- types of variables:
  - int
  - string
  - float
  - double

```bash
# ""  - saves the white spaces
echo "$var"
# \ -  escape white spaces 
var=test1\ test2\ test3
echo "$var"
# 11 22 33
var1=11
var2=22
var3=33

echo "$var1 $var2 $var3"

# nothing = 0
var=
let "var +=10"
# 10
echo $var 

# test is assigned to hi
hi=`echo test`
echo $hi

# results of ls command are assigned to hi
hi=`ls /home/me`
echo $hi

# $ is necessary to convert operation to a reference variable 
hi=$(ls -la)
echo $hi
```

##### Part 3

- variables
  - local
  - enviromental

```bash
num=1100
let "num -= 10"
echo "$num"

# replacing 10 with B
var=${num/10/B}
echo "$var"

# this is calculated as int 0 
var=A0
let "var += 1"
echo "$var"


var=hey1100
echo "$var"
num=${var/hey/20}
# converted to 201100
echo "$num"

var1=
# var1=
echo "var1=$var1"
let "var1 += 10"
# var1=10
echo "$var1"
```

##### Part 4

- `-n "$var"` - test whether argument exists
- `$0` - name of the script
- `$#` - total number of passed arguments

```bash
MIN=10
# $1 parameter past to the script
if [ -n "$1" ]
then
    echo "1st one is $1"
fi 

if [ -n "$2" ]
then
    echo "2nd one is $2"
fi 

if [ -n "$3" ]
then
    echo "3rd one is $3"
fi 

if [ -n "$4" ]
then
    echo "4th one is $4"
fi 

if [ -n "$5" ]
then
    echo "5th one is $5"
fi 

if [ -n "$6" ]
then
    echo "6th one is $6"
fi 

if [ -n "$7" ]
then
    echo "7tf one is $7"
fi 

if [ -n "$8" ]
then
    echo "8th one is $8"
fi 

if [ -n "$9" ]
then
    echo "9th one is $9"
fi 

if [ -n "${10}" ]
then
    echo "10th one is ${10}"
fi 

echo "List of arguments: "$*""
echo "Name of Script: \""$0"\""
if [ $# -lt "$MIN" ]
then
    echo "Not enough arguments, need 10 to run"
fi    
```

#### Return Values

- `$?` -exit status of the last command executed in an function

```bash
NO_OF_ARGS=2
E_BADARGS=85
E_UNREADABLE=86

if [ $# -ne "$NO_OF_ARGS" ]
then
# basename - extract filename with an extension
    echo "Usage: `basename $0` testFile1 testFile2 "
exit $E_BADARGS
fi
# ! - not
# -r - is readable
if [[ ! -r "$1" || ! -r "$2" ]]
then
    echo "Files are not real"
    exit "$E_UNREADABLE"
fi
# cmp - compare byte by byte
# &> redirect including error messages 
cmp $1 $2 &> /dev/null

if [ $? -eq 0 ]
then
    echo "Files are the same"
else
    echo "Files are not the same"
fi 

```

#### Conditional statements

- `if [ ... ] then ... fi`
- `if [ ... ] then ... elif [ ]  .. fi`

```bash
num=1

if [ "$num" -gt 0 ]
then
    if [ "$num" -lt 5 ]
        then
            if [ "$num" -gt 3 ]
                echo "GT 0, LT 5, GT 3"
            fi
    fi
elif [ "$num" -eq 0 ]
    echo "EQ 0"
else
    echo "I HAVE NO IDEA"
fi    

```

- `-e` - exists check

```bash
var=/home/chronic/wood.txt
# -e - exist check
if [[ -e $var ]]
then
    echo "File exists"
else
    echo "File not exists"
fi    
```

- ((...))  - returns status after evaluating arithmetic expression 

```bash
# returns status after evaluating arithmetic expression 
# status != result
# 0 status - TRUE
# something else than 0 status - FALSE 
# 0 result transates to 1 status
((2 > 1))
echo "Exit status is $?"
```

- `-f` -  a file is a regular file (not device file)
- `-e` -  a file or directory exists
- `-s` - file is not zero size
- `-r` - user  can read the file
- `-x` - user can execute the file
- `-w `- user can write to the file
- `-z arg` - an argument is given (exists) 
- `cat` - displays the contents of the file

```bash
NO_OF_ARGS=2

E_NOARGS=65
E_BADARGS=85
E_UNREADABLE=86
E_NOFILE=87
E_SIZE=89

if [[ -z "$1" && -z "$2" ]]
then
    echo "No arguments given"
    exit $E_NOARGS
fi

if [ $# -ne "$NO_OF_ARGS" ]
then    
    echo "USAGE: `basename $0` file1 file2"
exit $E_BADARGS
fi

if [[ ! -e "$1" || ! -e "$2" ]]
then
    echo "Files do not exist"
    exit $E_NOFILE
elif [[ ! -f "$1" || ! -f "$2" ]] 
then
    echo "Files need to be regular files"
    exit $NOTFILE
elif [[ ! -r "$1" || ! -r "$2" ]]
then
    echo "No read permission"
    exit "$E_UNREADABLE"
elif [[ ! -s "$1" || ! -s "$2"]]
then
    echo "Files are zero size"
    exit "$E_SIZE"
fi

cat $1 $2 | sort > file.txt

if [ $? -eq 0 ]
then
    echo "Execution of the script was successful"
    cat file.txt
else
    echo "Execution of the script failed"
fi    
```

#### Variables

- `"$$"` - process Id
- `$BASH_VERSINFO` - bash version

```bash
for n in {0..5}
do 
    echo "BASH_VERSINFO[$n] = ${BASH_VERSINFO[$n]}"
done    
```



- $PATH - path env. variable
- $UID - user's id number
- $EUID - effective user's id

```bash
ROOT_UID=0

echo -n "YOU ARE: "

if [ "$UID" -eq "$ROOT_UID" ]
then
    echo "root. YOUR \$UID = $UID"
else
    echo "user. YOUR \$UID = $UID"
fi    
```

- `$FUNCNAME` - function name

```bash
someFunction()
{
    echo "Function name is $FUNCNAME"
}

someFunction

echo "Outside, \$FUNCNAME = $FUNCNAME"

```

- `$GROUPS` - groups to which a user belong
- `$HOME` - home directory of a user
- `$HOSTNAME`

```
if [[ $HOSTNAME && $USER && $HOME ]]
then
    echo "HOSTNAME: $HOSTNAME"
    echo "USER: $USER"
    echo "HOME: $HOME"
    echo "Variables are set" 
else
    echo "Variables ar enot set"    
fi    
```

- `$HOSTTYPE` - sys hardware

- `IFS`- field separator
- `$LINENO` - line number
- `$OLDPWD` - previous directory
- `$OSTYPE`
- `$PWD` - current directory
- `$PIPESTATUS`  - status of current and previous commands ie. `${PIPESTATUS[*]}`

```bash

colors1="red-brown-orange"
colors2="red+brown+orange"

echo "IFS=-"

IFS=-
# red brown orange
# red+brown+orange

echo $LINENO

echo $colors1
echo $colors2
```

- `$REPLY` - holds previously  read value from input

```bash
echo "Some Question"
read

echo "The answer to the question is $REPLY"

echo "Some other question"
# reaads input and save it into var 
read var

echo "Your answer is $var"
```

- $SECONDS - how long the script is running

```bash
LIMIT_TIME=9
TIME_INTERVAL=3

echo "This script will run for $LIMIT_TIME seconds."
echo "Press Ctrl-c to exit before the ime limit."

while [ "$SECONDS" -le "$LIMIT_TIME" ]
do
    echo "This script has been running for $SECONDS seconds"
    sleep $TIME_INTERVAL
done    
```

- `declare -r` - read only variable
- `declare -i` - declare as integer

```bash
declare -r var_r=5
echo "\$var = $var_r"

declare -i var_i=10
echo "\$var_i = $var_i"
var_i=blue
echo "\$var_i = $var_i"

##-----------
declare -i x
x=8/2
echo "\$x = $x"
##------------
declare -a x=(1 2 3 4 5)

for i in {0..4}
do
    echo "${x[$i]}"
    let "i += 1"
done

```

- `declare -f` - declare function as variable

```bash
declare -f someFunction

someFunction(){
    echo "hey are you having a  good time? Yes, no, maybe? Or you do not care at all"
}

someFunction
```

- declare -x  - exportable variable

```bash
declare -x var_x=10

echo "$var_x"
```

##### Random numbers

- $RANDOM - random function

```

MAX=10
i=1

while [ "$i" -le $MAX ]
do
    n=$RANDOM
    echo $n
    let "i += 1"
done    
```

#### Loops

##### For Loop

```bash
for i in 1 2 3 4 5
do
    echo "Outer Loop $i -----------------"

    for j in 1 2 3
    do  
        echo "Inner Loop $j !!!!!!!!!! Outer loop itereation $i"
    done
done    
```

##### While Loop

```bash
a=unset
prev=$a

while   echo "Previous variable = $prev"
        echo 
        prev=$a
        [ "$a" != end ]
do
        echo "Input end to exit or anything else to go on!"
        read a
        echo "variable = $a"
done                
```

##### Until Loop

```
until [ "$n" = end ]
do
    echo "Input end to exit or something else to move on"
    read n
    echo "$n"
done    
```

##### Break and Continue 

##### Part 1

```bash
UPPER_LIMIT=9

echo "Numbers 1 to 10 (but not 3 and 11)."

n=0

while [ "$n" -le "$UPPER_LIMIT" ]
do
    n=$(($n+1))

    if [ "$n" -eq 3 ] || [ "$n" -eq 11 ]
    then
        continue
    fi

    echo -n "$n "
done

echo

n=0

while [ "$n" -le "$UPPER_LIMIT" ]
do
    n=$(($n+1))

    if [ "$n" -gt 2 ]
    then
        break
    fi

    echo -n "$n "

done 
echo
```

##### Part 2

```bash
for i in 1 2
do
    echo "Loop 1: iteration $i"
    for j in 1 2 3
    do
        echo e "\tLoop 2: iteration $j"
        for k in 1 2 3 4
        do
            echo -e "\t\tLoop 3: iteration $k"
            if [ "$k" -eq 2 ]
            then
                # breakes 2nd and 3rd loop
                break 2
            fi
        done
    done 
done               

for i in 1 2 3 4 5
do
    echo "Loop 1: iteration $i"
    for j in 1 2 3
    do 
        echo -e "\tLoop 2: iteration $j"
        for k in 1 2 3 4
        do 
            echo -e "\t\tLoop 3: iteration $k"
            if [ "$k" -eq 2 ]
            then
                
                continue 3
            fi 
        done 
    done
done 

exit 0
```

##### Case Construct

```bash
echo -n "Enter a letter or a digit: "
read a 

case "$a" in
    [[:lower:]] ) echo "$a is a lowercase letter";;
    [[:upper:]] ) echo "$a is a uppercase letter";;
    [0-9]       ) echo "$a is a digit";;
    *           ) echo "$a is a special character";;
esac    
```

##### Select Construct

```bash
# prompt
PS3='Pick a color: '

echo

# it uses PS3 value
select color in "brown" "grey" "black" "orange" "red"
do
    echo "You selected this color: $color"
    break
done   
```

#### Internal commands

##### Printf

- formats an output

```bash
declare -r PI=3.1415926
# 1.2 second decimal
printf "Second decimal of PI is %1.2f\n" $PI 
```

##### Read

```bash
# key codes of the buttons
up=$'\x1b[A'
down=$'\x1b[B'
left=$'\x1b[D'
right=$'\x1b[C'
# -s does not echo input
# n3 - accept only 3 chars
# -p prompt
read -s -n3 -p "Press an arrow key: " arrow 

case "$arrow" in

    $up) echo "You pressed up";;
    $down) echo "You pressed down";;
    $left) echo "You pressed left";;
    $right) echo "You pressed right";;

esac    
```

- simple read

```bash
echo "Enter a string"
read -r var
echo "$var"
```

- reading a file

```bash
echo "Read"
while read var
do 
    echo "$var"
done <wood.txt
```

##### Eval and Set 

```bash
if [ ! -z $1 ]
then
    process="ps -e | grep $1"
fi
# executes 
eval $process
```

##### Set + unset

```bash
# enables history option
set +o history

set -o history

echo "Before setting the parameters"

echo "\$1 = $1"
echo "\$2 = $2"

set `echo "three four"`

echo "After setting parameters"

echo "\$1 = $1"
echo "\$2 = $2"
```

- Setting position parameters

```bash
var="1 2 3"
echo $var
# setting position params
set -- $var
i=1
while [ "$i" -le $# ]
do
    echo -n "\$$i = "
    eval echo \$$i
    (( i++ )) 
done

# cleaning position params
set --

echo "\$1 = $1"
echo "\$2 = $2"
echo "\$3 = $3"
```

- unsetting

```bash
var='1 2 3'
echo "$var"

unset var

echo "$var"
```

##### Getops

```bash
# getopts get the input arguments
while getopts :dm option
do
    case $option in
        d) d_option=1
        ;;
        m) m_option=1
        ;;
        *) echo "Usage: -dm"
    esac
done

day=`date | awk 'print $1 " " $2'`

if [[ ! -z $m_option ]]
then
    echo "Month is: $month"
fi    
# shift to next position arg index
shift $(($OPTIND -1))
```

##### Shopt type jobs disown

- `disown` - removes jobs from shell jobs table 

- `shopt`- allows you to change additional shell optional behavior

##### Fg kill command 

```
echo "Waiting for 5 seconds"

sleep 5 &

wait 

# displays time which took command to finish
times
echo "done"
```

- finding an PID `ps aux | grep -i first.sh`
- kill `<PID>` - killing a process 

```bash
ls ()
{
    echo "I do not know whatever"
}

# executes ls function
ls
echo "#############"

# executes bash command
command ls
```

#### Regular expressions

```bash
E_NOPATTERN=71

DICT=/usr/share/dict/linux.words

if [ -z "$1" ]
then
    echo 
    echo "Usage: "
    echo "`basename $0` \"pattern,\""
    echo "where \"pattern\" is in the form"
    echo
    echo "The o's are letters you already know,"
    echo "and the periods are missing letters."
    echo "Letters and periods can be in any position."
    echo "For example: w...i...n"
    echo
    exit $E_NOPATTERN
fi

# ^ - beginning of the line
# $ - end of the line
grep ^"$1"$ "$DICT"
```

##### Sed

```bash
E_BADARGS=65

# if no files passed
if [ $# -eq 0 ]
then
    echo "Usage: `basename $0` file"
    exit $E_BADARGS
else
    # operates on the position params
    for i
    do	
    	# deletes from the beginning to first blank, deletes all blank lines
        sed -e '1,/^$/d' -e '/^$/d' $i 
    done
fi        
```

##### Globing

- `ls -l [fw]*` - list files whose names start either from **f** or **w** 
- `ls -l [e-q]*` - files whose names can begin with letters from **e** to **q**
- `ls -l {w*. *oo*}` -files whose names start with  **w** of having **oo** inside 
- `echo w*` - files whose names  start with **w** 
- `echo woo?.txt` - ? - replaces one letter 

```bash
# * - every file name in a current dir
for file in *
do 
    ls -la "$file"
    # include .files
    shopt -s nullglob
done    
```

#### Input Output Redirection

##### STDOUT, STDIN, STDERR

```bash
file=wood.txt
# redirect a standard output into file
echo "this line is sent to $file" 1>$file
```

- `2> <file>` - redirects standard errors: `something 2>>wood.xml`

- redirects std output and errors to wood1.txt: `something >> wood1.txt 2>&1`

```bash
echo 12345 > fd.txt
# open fd.txt and assign 3 file descriptor
exec 3<>fd.txt
# read only 2 chars from file
read -n 2 <&3
# write a decimal point
echo -n . >&3
# closing file
exec 3>&-
cat fd.txt
```

```bash
E_FILE_ACCESS=70
E_BADARGS=71
# is the file readable
if [ ! -r "$1" ]
then
    echo "Can't read from inpt file!"
    echo "Usage: $0 input-file output-file"
    exit $E_FILE_ACCESS
fi
# is second parameter passed
if [ -z "$2" ]
then 
    echo "Specify output file!"
    echo "Usage: $0 input-file output-file"
    exit $E_BADARGS
fi
# link file descriptor 4 with stdinput
exec 4<&0
# read from input file
exec <$1

# link file descriptor 7 with stdoutput
exec 7>&1
# write to the output file
exec > $2

# transform lower case to upper case
tr a-z A-Z

#restore std output and close file desc 7
exec 1>&7 7>&-
#restore std inut and close file desc 4
exec 0<&4 4<&-    


```

```bash
count=0
# open wood.txt and assing 3
exec 3<> wood.txt

# read from the file
while read line <&3
    do
    {
        echo $line
        (( count++ ));

    }
    done
# close the file descriptors    
exec 3>&-

echo "Number of read lines is $count"
```

#### Functions

```bash
function1 (){
    echo "call \"f2\" from \"f1\"."
    function2
}

function2 (){
        echo "this is \"f2\""
}

function1
```

- Nested function

```bash
function1 (){

    function2 (){
        echo "this is nested function"
    }
}

function1
function2
```

- `$FUNCNAME` - variable with function name
- \$1, \$2.. - params passed to a function
- $? - exit status

```bash
#!/bin/bash

E_PARAM_ERR=250
EQUAL=251

function_max(){
    if [ -z "$2" ]
    then
        return $E_PARAM_ERR
    fi 

    if [ "$1" -eq "$2" ]
    then
        return $EQUAL
    else
        if [ "$1" -gt "$2" ]
        then
            return $1
        else 
            return $2
        fi
    fi                     
}

function_max 12 13 100
return_value=$?

if [ "$return_value" -eq $E_PARAM_ERR ]
then
    echo "Function needs two parameters"
elif [ "$return_value" -eq $EQUAL ]
then
    echo "Numbers are equal"
else
    echo "Max number is $return_value"
fi            
```

- $# - no of arguments

```bash
ARGS=1
E_BADARGS=85

FILE=/etc/passwd

pattern=$1

if [ $# -ne "$ARGS" ]
then
    echo "Usage: `basename $0` USERNAME"
    exit $E_BADARGS
fi 

get_real_name()
{
    while read line
    do
    # -F":" - field delimeter
        echo "$line" | grep $1 | awk -F":" '{ print $5 }'
    done    
} <$FILE # reading a file

get_real_name $pattern
```

#### Arrays

- `some_var[]` - array declaration 1

```
arr[0]=20
arr[1]=30

echo -e "${arr[0]} \n${arr[1]}"
```

- `declare -a some_var ` array declaration 2

```bash
declare -a arr
arr=( 10 20 30 40 50 60)

echo -e "${arr[0]} \n${arr[1]} \n${arr[2]} \n${arr[3]} \n${arr[4]}"
```

- `arr=()` - array declaration 3

```bash
arr=( [0]=first [1]="second" [7]=45 )


echo -e "${arr[0]} \n${arr[1]} \n${arr[7]} "
```



```bash

# assigning a string
a=something123
# * everything
echo ${a[*]}
# [0] first element
echo ${a[0]}
# [1] second element
echo ${a[1]}
# size of the array
echo ${#a[@]}
```

```bash
arr=( zero one two )

echo ${arr[0]}
# size of the first element
echo ${#arr[0]}
# size of an array
echo ${#arr[*]}
```

```bash
declare -a colors

echo "Your favourite colors separated by space: "
# you can pass multiple elemnets
read -a colors
# size of an array
count=${#colors[@]}

i=0

while [ "$i" -lt "$count" ]
do
    echo ${colors[$i]}
    (( i++ ))
done

echo ${colors[*]}
# delete 3rd element
unset ${colors[2]}
echo ${colors[*]}
# delete all elements
unset colors
echo "no colors. colors gone"
echo ${colors[*]}
```

- Reading file into an array

```bash
FILE=wood.txt
declare -a arr_file
# reading file to the array
arr_file=( `cat "$FILE"` )

echo ${arr_file[*]}
size=${#arr_file[*]}
echo "array size is $size"
```

- Bubble sort

```bash

swap()
{
        # temporary variable
        local tmp=${colors[$1]}
        colors[$1]=${colors[$2]}
        colors[$2]=$tmp

    return
}

declare -a colors

colors=( red black blue white brown )
# size of an array
size=${#colors[@]}

for (( last = $size -1 ; last >0 ; last--))
do
    for (( i = 0 ; i < last ; i++))
    do
        [[ "${colors[$i]}" > "${colors[$((i+1))]}" ]] && swap $i $((i+1))
    done
done        

echo ${colors[@]}
```

#### Lists

