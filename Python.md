Python Day 1:
when creating a script add .py to make sure syntax colors show
15 // 8    integer division, takes last whole integer      answer would be 1 instead of 1.875
3**4=81
---tuple('hello world')
('h', 'e', 'l', 'l', 'o', ' ', 'w', 'o', 'r', 'l', 'd')
+=     add this to itself
.append()      allows you to append things to list
.join()        join a list together,     ''.join()
.split()       splits based on the character you want        passwd.split(':')            ['root', 'x', '0', '0', 'root'] 

 

Excercise 1:
1 string1 = 'name@somewhere.com'
2 split1 = string1.split('@')
3 split2 = string1.split('.')
4 
5 print(['name','somewhere','com'])
----output: -----
['name', 'somewhere', 'com']
Alternate:
email = 'name@domain.com'
'''
a = email.split('@')
b = '.'.join(a)
c = b.split('.')
print(c)
'''
Second Alternate:
print(('.'.join(email.split('@'))).split('.'))

lst = []      makes a blank list that will allow you to append to it

## Branching: ---------------------------

if <condition>:
    <indented code block>
elif <condition>:
    <indented code block>
elif <condition>:
    <indented code block>
else:
    <indented code block>
Example:

  1 usr = input('Pick a color:\n')
  2 if usr == 'Orange' or usr == 'Yellow':
  3     print('The color {} sucks'.format(usr))
  4 elif usr == 'Red':
  5     print('Good Choice')
  6 else:
  7     print('Pick a different color!')

Example 2:
  1 num = int(input('Type a number:\n'))
  2 if num >= 0 and num <= 10:
  3     print('{} is between 0 and 10.'.format(num))
  4 elif num > 10:
  5     print('{} is greater than 10.'.format9num))
  6 else:
  7     print('Type a POSITIVE number please!')

## FizzBuzz:-----------------------------------------------
  1 #!/usr/bin/env python3
  2 num = int(input('Enter a number:\n '))
  3 if num % 5 == 0 and num % 3 == 0:
  4     print('fizzbuzz')
  5 elif num % 3 == 0:
  6     print('fizz')
  7 elif num % 5 == 0:
  8     print('buzz')
  9 else:
 10     print(num)

## While Loops: -----------------------------------
def test():
 while True:
   user = input("Type 'Pass', 'Break', 'Continue, 'Return':\n").lower()
   if user == 'pass':
      pass
      print(this is Pass.')
   elif user == 'Break':
      break
      print('This is Break.')
   elif user == 'continue':
      continue
      print('This is Continue.')
   elif user == 'return':
      return 'This is return'
   else:
      print('Please choose a valid option.')
  test()

def guess_number(n):
   while True:
      usr = int(input('Type a number:\n;))
      if usr == n:
         print('WIN')
         break
      elif usr < n:
         print('too low')
      elif usr > n:
         print('too high')
guess_number(44)

## For Loop:

AFCwest = ['Broncos', 'Chargers', 'Chiefs', 'Raiders']
for team == 'Chiefs':
   print('Boooo{}'.format(team))
elif team == 'Broncos':
   print('Please {} win again :\'('.format(team))
else:
   print(team)

## Slicing:
numbers[0::1]
[1, 2, 3, 4, 5]


## Range:
range(10)
list(range(10))
-----start at 0, stop at 10, step by 2             list(range(0,10,2)
                                                   0, 2, 4, 6, 8
## Len: Shows the amount inside a list
len(AFCwest)
4

## Dictionaries
Dictionary.py
  1 catalog = {'Apex':50, 'Cod':79.99, 'MVP':154.49, 'Tarkov':200}
  2 
  3 for game in catalog:
  4     print('{}: {}'.format(game,catalog[game]))
Output: --------------------------------
Apex: 50
Cod: 79.99
MVP: 154.49
Tarkov: 200

  1 catalog = {'Apex':50, 'Cod':79.99, 'MVP':154.49, 'Tarkov':200}
  2 order = [('MVP',5),('Tarkov',2)]
  3 print(order[0][1] * 154.49)
Output:-----------------------------------
772.45
  
  Gives the Total---------------------------------------------------------
  1 catalog = {'Apex':50, 'Cod':79.99, 'MVP':154.49, 'Tarkov':200}
  2 order = [('MVP',5),('Tarkov',2)]
  3 total = 0
  4 for i in order:
  5     print(catalog[i[0]] * i[1])
  6     total += catalog[i[0]] * i[1]
  7 print(total)
Output:------------------------------
772.45
400
1172.45

###FileIO
## Open
with open("test.txt") as fp:
pass
when inside you can adjust what mode youre in with 'w'(write) and  

Example: --------------------------
with open('test.txt', 'w') as fp:
    fp.write('First line\n')
    lines = ['Second line\n', 'Third line\n', 'Fourth line\n', 'Last line\n']
    fp.writelines(lines)
￼
with open("test.txt",'w') as fp:
   fp.write('First line\n')
   lines = ['Second Line\n', 'Third Line\n', 'Fourth Line\n', 'Last Line\n']
   fp.writelines(lines)

## Read Files
with open('test.txt', 'r') as fp:
    fp.read()

with open('test.txt') as fp:
    fp.read(5)                  ----- Reads the specified amount of characters shown
    
with open('test.txt') as fp:
    for line in fp:
        print(line, end='')     ----- 

## File IO - Chapter 10.15 Questions

The textfile, travel_plans.txt, contains the summer travel plans for someone with some commentary. Find the total number of characters in the file and save to the variable num.
with open)'travelplans.txt', 'r') as fp:
   num = len(anything.read())

## Args+Kwargs
---ord('Z')
90
---chr(90)
'Z'
---'1'.isnumeric(1)
True
---'a'.isnumeric(a)
False

Python Practice
Question 1
Given the floatstr, which is a comma separated string of floats, return a list with each of the floats in the argument as elements in the list.

lst = []
for i in floatstr.split(','):
    lst.append(float(i))
Question 2
Given the variable length argument list, return the average of all the arguments as a float.

type(args)
    sum = 0 
    for addend in args:
        sum += addend
        avg = sum / float(len(args))
    return avg 
Question 3
Given a list (lst) and a number of items (n), return a new list containing the last n entries in lst.

lst1 = []
    for i in lst[-n:]:
        lst1.append(int(i))
    return lst1
Question 4
Given an input string, return a list containing the ordinal numbers of each character in the string in the order found in the input string.

  lst = []
    for i in strng:
        lst.append(ord(i))
    return lst 
Question 5
Given an input string, return a tuple with each element in the tuple containing a single word from the input string in order.

 arr = []
    arr = strng.split(' ')
    t = tuple(arr)
    return t
Question 6
Given a dictionary (catalog) whose keys are product names and values are product prices per unit and a list of tuples (order) of product names and quantities, compute and return the total value of the order.

 total = 0
    for i in order:
        total += catalog[i[0]]*i[1]
    return total
Question 7
Given a filename, open the file and return the length of the first line in the file excluding the line terminator.

 with open(filename, 'r') as fp:
        i = fp.readline()
        return(len(i)) -1
Question 8
Given a filename and a list, write each entry from the list to the file on separate lines until a case-insensitive entry of "stop" is found in the list. If "stop" is not found in the list, write the entire list to the file on separate lines.

with open(filename, 'w') as fp:
        for word in lst:
            if word.lower() == 'stop':
                break
            else:
                fp.write('{}\n'.format(word))
Question 9
Given the military time in the argument miltime, return a string containing the greeting of the day. 0300-1159 "Good Morning" 1200-1559 "Good Afternoon" 1600-2059 "Good Evening" 2100-0259 "Good Night"

 if miltime >= 300 and miltime <= 1159:
        return "Good Morning"
 elif miltime >= 1200 and miltime <= 1559:
        return "Good Afternoon"
 elif miltime >= 1600 and miltime <= 2059:
        return "Good Evening"
 elif miltime >= 2100 and miltime <= 259:
        return "Good Night"
Question 10
Given the argument numlist as a list of numbers, return True if all numbers in the list are NOT negative. If any numbers in the list are negative, return False.

 for i in numlist:
        if i < 0:
            return False
 return True       

Python Practice 2
def q1(radius):
    # Given the radius of a sphere, calculate and return 
    # its surface area. Surface area is given by the following:
    # A = 4*PI*(r**2) where PI is the constant 3.14159 and r
    # is the radius of the sphere.

    return 4*3.14159*(radius**2)

    pass
def q2(addr):
    # Given an IPv4 address as a string in dotted decimal notation,
    # return True if the address is multicast, otherwise return False.
    # IPv4 multicast addresses are those in the range 224.0.0.0 to
    # 239.255.255.255.
    # ipaddress.IPv4Address has been disabled for this function.
    counter = 0
    arr = addr.split('.')
    if int(arr[0]) >= 224 and int(arr[0]) <= 239:
        return True
    else:
        return False
    if counter == 1:
        return True


    #pass
def q3():
    # Return the well-known ports as a list of integers.
    # Ports 0 through 1023 are considered well-known.

    arr = []
    for x in range(1024):
        arr.append(x)
    return arr

    pass
def q4(number):
    # Given a string for a number spelled out as a word,
    # return the number as an integer. The number will
    # only be 'zero','one','two','three', or 'four'.

    if number == 'zero':
        return 0
    elif number == 'one':
        return 1
    elif number == 'two':
        return 2
    elif number == 'three':
        return 3
    elif number == 'four':
        return 4


    pass
def q5():
    # Read a string from the user and return the integer conversion of it.
    # Ensure the conversion is successful by removing any non-numeric characters.
    # You may assume that the input will contain at least 1 numeric character.
    bruh = ''
    arr = ['0','1','2','3','4','5','6','7','8','9']
    a = input()
    for x in list(a):
        if x in arr:
            bruh += x
        else:
            continue
    return int(bruh)


    pass
def q6(first,middle,last,domain):
    # Given a name and domain, print to the screen their email address.
    # The address should take the form: 
    # <first>.<middle initial>.<last>@<domain>.com
    # Only include a middle initial (the first letter of the middle name).
    # Ensure the address is all lowercase.
    # Append '.com' to the given domain.
    
    print(f'{first.lower()}.{middle[0]}.{last.lower()}@{domain}.com')


    pass
def q7(infile,outfile):
    # Copy the contents of the file whose filename is given in 
    # infile to the file whose name is given in outfile. Overwrite
    # outfile if it already exists.
    # shutil.copyfile, copy, and copy2 have been disabled for this function.
    with open(infile, 'r+') as fp, open(outfile, 'w') as out:
        out.write(fp.read())
            

    pass
def q8(address):
    # Given an email address of the form:
    # <first>.<middle initial>.<last>@<domain>.com
    # return the 4 elements of the address as a tuple in the order
    # that they appear in the address.
    # For example, if given 'nicholas.r.yost@somedomain.com,
    # ('nicholas','r','yost','somedomain') should be returned.

    
    return tuple((address.replace('.com','')).replace('@','.').split('.'))

    pass
def q9(strng):
    # Given a string, return a dictionary whose keys are the set of
    # unique characters within the string and whose values are the
    # count of occurances of each character.
    # For example, if given 'hello', the returned dictionary should be
    # { 'l':2, 'h':1, 'e':1, 'o':1 }
    # collections.Counter has been disabled for this function.
    count = 0
    dict = {}
    for x in list(strng):
        dict[x] = strng.count(x)
    return dict
    
    pass    
def q10():
    # Return your last name as a string. Use all lowercase letters.
    pass

    return 'hunt'

if __name__ == '__main__':
    pass

