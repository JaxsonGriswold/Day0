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

Branching: ---------------------------

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

FizzBuzz:-----------------------------------------------
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

While Loops: -----------------------------------
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
