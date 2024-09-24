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
