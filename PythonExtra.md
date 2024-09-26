#!/usr/bin/env python3

def q1(sentence):
    '''
    Given a string of multiple words separated by single spaces,
    return a new string with the sentence reversed. The words
    themselves should remain as they are. For example, given
    'it is accepted as a masterpiece on strategy', the returned
    string should be 'strategy on masterpiece a as accepted is it'.
    '''
    mylist = sentence.split(' ')
    print(mylist)

    newlist = []
    for i in range(len(mylist) -1, -1, -1):
        newlist.append(mylist[i])
    outstr = ' '.join(newlist)
    return outstr
    pass
q1('hello world pie test')

def q2(n):
    '''
    Given a positive integer, return its string representation with
    commas seperating groups of 3 digits. For example, given 65535
    the returned string should be '65,535'.
    '''
    return '{:,}'.format(n)
    pass

def q3(lst0, lst1):
    '''
    Given two lists of integers, return a sorted list that contains
    all integers from both lists in descending order. For example,
    given [3,4,9] and [8,1,5] the returned list should be [9,8,5,4,3,1].
    The returned list may contain duplicates.
    '''
    joinlist = lst0 + lst1
    joinlist.sort(reverse = True)
    return joinlist
    pass

def q4(s1,s2,s3):
    '''
    Given 3 scores in the range [0-100] inclusive, return 'GO' if
    the average score is greater than 50. Otherwise return 'NOGO'.
    '''
    listavg = sum([s1, s2, s3]) / 3
    if listavg > 50:
        return 'GO'
    return 'NOGO'
    pass

def q5(integer, limit):
    '''
    Given an integer and limit, return a list of even multiples of the
    integer up to and including the limit. For example, if integer==3 and
    limit==30, the returned list should be [0,6,12,18,24,30]. Note, 0 is
    a multiple of any integer except 0 itself.
    '''
    outlist = []
    for i in range(0,limit + 1, 1):
        if (i % integer == 0) and (i % 2 == 0):
            outlist.append(i)
    return outlist
    pass

def q6(f0, f1):
    '''
    Given two filenames, return a list whose elements consist of line numbers
    for which the two files differ. The first line is considered line 0.
    '''
    list1 = []
    with open(f0) as fp:
        for line in fp:
            list1.append(line)
    list2 = []
    with open(f1) as fp:
        for line in fp:
            list2.append(line)
    outlist = []
    for i in range(0, len(list1)):
        if list1[i] != list2[i]:
            outlist.append(i)
    return outlist
    pass

def q7(lst):
    '''
    Return the first duplicate value in the given list.
    For example, if given [5,7,9,1,3,7,9,5], the returned value should
    be 7.
    '''
    mylist = []
    for item in lst:
        mylist.append(item)
        if (mylist.count(item) > 1):
            return item
    pass

    uniquelist = []
    duplicatelist = []
    for item in lst:
        if item not in uniquelist:
            uniquelist.append(item)
        elif item no in jduplicatelist:
            duplicatelist.append(item)
    return duplicatelist[0]


def q8(strng):
    '''
    Given a sentence as a string with words being separated by a single space,
    return the length of the shortest word.
    '''
    pass

def q9(strng):
    '''
    Given an alphanumeric string, return the character whose ascii value
    is that of the integer represenation of all of the digits in the string
    concatenated in the order in which they appear. For example, given
    'hell9oworld7', the returned character should be 'a' which has
    the ascii value of 97.
    '''
    pass

def q10(arr):
    '''
    Given a list of positive integers sorted in ascending order, return
    the first non-consecutive value. If all values are consecutive, return
    None. For example, given [1,2,3,4,6,7], the returned value should be 6. 
    '''
    pass
-----------------------------------------------------------------------------------------------------------------------------------

####################NOTES#################################
if a question ask to return a list then you need to declare a list
printing all the variables that you get will show what the test is using as input 
and could be helpful to know what data types and values you are working with.
remember that only worry about args being a tuple.

if you get a ip you can split by the . and verify that the octect is valid
#example
def q1(ip):
  oct1 = False
  oct2 = False
  oct3 = False
  oct4 = False
  for i in ip.split('.'):
    if int(i) < 0 or int(i) > 255:
      return False
    else:
      oct1 = True



q1('5.800.99.100')





###numeric
evaluates a string and returns a boolean
'a'.isnumeric()
str(var).isnumeric()










!!!!!!!!!!!!!!!!!!!!!!CORRECT!!!!!!!!!!!!!!!!!!!!!!!
//////////////////////////question 1//////////////////////////

1 #!/usr/bin/env python3
  2 
  3 def q1(floatstr):
  4     '''
  5     TLO: 112-SCRPY002, LSA 3,4
  6     Given the floatstr, which is a comma separated string of
  7     floats, return a list with each of the floats in the 
  8     argument as elements in the list.
  9     '''
 10     numbers = floatstr.split(',')
 11     converted = []
 12     convert = 0.0
 13     for i in numbers:
 14         convert = float(i)
 15         converted.append(convert)
 16     print(converted)
 17     print(type(converted))
 18     return converted

###############instructor solution#####################
def q1(floatstr):
  lst = []
  for i in floatstr.split(','):
    lst.append(float(i))
  return lst
  pass

//////////////////////////1/////////////////////
!!!!!!!!!!!!!!!!!!!!!!CORRECT!!!!!!!!!!!!!!!!!!!!!!!
///////////////////////question 2//////////////////////
  def q2(*args):
      '''
      TLO: 112-SCRPY006, LSA 3
      TLO: 112-SCRPY007, LSA 4
      Given the variable length argument list, return the average
      of all the arguments as a float
      '''
      numbers = args
      converted = []
      convert = 0.0
      average = 0.0
      for i in numbers:
          convert = float(i)
          converted.append(convert)
      print(converted)
      print(type(converted))
      average = sum(converted)/len(converted)
      return average


#####################instructor solution1######################
def q2(*args):
  total = 0
  for i in args:
    total += i
  return total/len(args)
  pass
#####################instructor solution2######################
def q2(*args):
  return sum(args)/len(args)
//////////////////////////2////////////////////////
!!!!!!!!!!!!!!!!!!!!!!CORRECT!!!!!!!!!!!!!!!!!!!!!!!
///////////////////////question 3//////////////////////
41 def q3(lst,n):
 42     '''
 43     TLO: 112-SCRPY004, LSA 3
 44     Given a list (lst) and a number of items (n), return a new 
 45     list containing the last n entries in lst.
 46     '''
 47     itemnum = -n
 48     items = []
 49     converted = []
 50 
 51     for i in lst:
 52         converted.append(i)
 53     items = converted[itemnum:]
 54 
 55 
 56 
 57 
 58 
 59     return items
#####################instructor solution1######################
def q3(lst,n):

  return lst[-n::]
  pass
#####################instructor solution2######################
def q3(lst,n):


//////////////////////////3////////////////////////
!!!!!!!!!!!!!!!!!!!!!!CORRECT!!!!!!!!!!!!!!!!!!!!!!!
///////////////////////question 4//////////////////////
63 def q4(strng):
 64     '''
 65     TLO: 112-SCRPY004, LSA 1,2
 66     TLO: 112-SCRPY006, LSA 3
 67     Given an input string, return a list containing the ordinal numbers of 
 68     each character in the string in the order found in the input string.
 69     '''
 70 
 71 
 72 
 73     converted = []
 74     letters = []
 75     for letter in strng:
 76         letters.append(letter)
 77 
 78     for i in letters:
 79         converted.append(ord(i))
 80     return converted
#####################instructor solution1######################
def q4(strng):
  lst = []
  for i in strng:
    lst.append(ord(i))
  return lst
  pass


//////////////////////////4////////////////////////
!!!!!!!!!!!!!!!!!!!!!!CORRECT!!!!!!!!!!!!!!!!!!!!!!!
///////////////////////question 5//////////////////////
84 def q5(strng):
 85     '''
 86     TLO: 112-SCRPY002, LSA 1,3
 87     TLO: 112-SCRPY004, LSA 2
 88     Given an input string, return a tuple with each element in the tuple
 89     containing a single word from the input string in order.
 90     '''
 91     converted = ()
 92     words = strng.split()
 93     '''
 94     for word in words:
 95         converted.append(word)
 96     '''
 97     return tuple(words)


#####################instructor solution1######################
def q5(string):

return tuple(strng.split())
pass

//////////////////////////5////////////////////////
!!!!!!!!!!!!!!!!!!!!!!INCORRECT!!!!!!!!!!!!!!!!!!!!!!!
///////////////////////question 6//////////////////////
103 def q6(catalog, order):
104     '''
105     TLO: 112-SCRPY007, LSA 2
106     Given a dictionary (catalog) whose keys are product names and values are product
107     prices per unit and a list of tuples (order) of product names and quantities,
108     compute and return the total value of the order.
109 
110     Example catalog:
111     {
112         'AMD Ryzen 5 5600X': 289.99,
113         'Intel Core i9-9900K': 363.50,
114         'AMD Ryzen 9 5900X': 569.99
115     }
116 
117     Example order:
118     [
119         ('AMD Ryzen 5 5600X', 5), 
120         ('Intel Core i9-9900K', 3)
121     ]
122 
123     Example result:
124     2540.45 
125 
126     How the above result was computed:
127     (289.99 * 5) + (363.50 * 3)
128     '''
129     pass
#####################instructor solution1######################
def q6(catalog, order):
  total = 0
  for i in order:
    total += catalog[i[0]] * i[1]
  return total
  pass
//////////////////////////6////////////////////////
!!!!!!!!!!!!!!!!!!!!!!CORRECT!!!!!!!!!!!!!!!!!!!!!!!
///////////////////////question 7//////////////////////
135 def q7(filename):
136     '''
137     TLO: 112-SCRPY005, LSA 1
138     Given a filename, open the file and return the length of the first line 
139     in the file excluding the line terminator.
140     '''
141     with open(filename, 'r') as fp:
142         return len(fp.readline()) -1
143 
144         '''
145         converter = data.replace('\n', ' ').split(".")
146         
147         
148 
149 
150         for line in converter:
151             first_line = converter[line]
152             if first_line == 'terminator':
153                 continue
154             else:
155                 return len(first_line)
156         '''
157         '''
158         for line in fp:
159             first_line = line
160             return first_line
161         '''
162 
163 
164         '''
165         first_line = 0.0
166         
167         for line in fp:
168             if line == 'terminator':
169                 continue
170             else:
171                 
172                 return line
173                 break
174          
175         '''
#####################instructor solution1######################
def q7(filename):
  with open(filename) as fp:
    return len(fp.readline()) - 1
  pass
//////////////////////////7////////////////////////
!!!!!!!!!!!!!!!!!!!!!!INCORRECT!!!!!!!!!!!!!!!!!!!!!!!
///////////////////////question 8//////////////////////
178 def q8(filename,lst):
179     '''
180     TLO: 112-SCRPY003, LSA 1
181     TLO: 112-SCRPY004, LSA 1,2
182     TLO: 112-SCRPY005, LSA 1
183     Given a filename and a list, write each entry from the list to the file
184     on separate lines until a case-insensitive entry of "stop" is found in 
185     the list. If "stop" is not found in the list, write the entire list to 
186     the file on separate lines.
187     '''
188     pass
#####################instructor solution1######################
def q8(filename,lst):
  with open(filename, 'w') as fp:
    for line in lst:
      if line.lower() == 'stop':
        break
      else:
        fp.write('{}\n'.format(line))
  pass
//////////////////////////8////////////////////////
!!!!!!!!!!!!!!!!!!!!!!INCORRECT!!!!!!!!!!!!!!!!!!!!!!!
///////////////////////question 9//////////////////////
190 def q9(miltime):
191     '''
192     TLO: 112-SCRPY003, LSA 1
193     Given the military time in the argument miltime, return a string 
194     containing the greeting of the day.
195     0300-1159 "Good Morning"
196     1200-1559 "Good Afternoon"
197     1600-2059 "Good Evening"
198     2100-0259 "Good Night"
199     '''
200     pass
#####################instructor solution1######################
def q9(miltime):
if miltime >= 301 and miltime <= 1159:
return 'Good Morning'
elif miltime >= 1200 and miltime <=1559:
return 'Good Afternoon'
elif miltime >= 1600 and miltime <= 2059:
return 'Good Evening'
elif miltime >= 2100 and miltime <= 259:
return 'Good Night'

pass
//////////////////////////9////////////////////////
!!!!!!!!!!!!!!!!!!!!!!INCORRECT!!!!!!!!!!!!!!!!!!!!!!!
///////////////////////question 10//////////////////////
202 def q10(numlist):
203     '''
204     TLO: 112-SCRPY003, LSA 1
205     TLO: 112-SCRPY004, LSA 1
206     Given the argument numlist as a list of numbers, return True if all 
207     numbers in the list are NOT negative. If any numbers in the list are
208     negative, return False.
209     '''
210     pass
#####################instructor solution1######################
def q10(numlist):
  for i in numlist:
    if i < 0:
      return False
  return True
  pass
//////////////////////////10////////////////////////
