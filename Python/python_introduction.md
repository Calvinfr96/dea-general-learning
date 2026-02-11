# Python Introduction

## Data Types
- Integer (int) - Represents whole numbers.
- Floating Point (float) - Represents decimal numbers.
- String (str) - Represents an ordered sequence of characters.
- List (list) - Represents an ordered sequence of **mutable** primitives or objects, enclosed in square brackets. Ex: [2, 3.4, "5"]
- Dictionary (dict) - Represents an unordered sequence of key-value pairs, enclosed in curly braces. Ex: {"Key": "value", "Name": "John", "Age": 45}
- Tuple (tup) - Represents an ordered sequence of **immutable** objects, enclosed in parentheses. Once a tuple is created, it cannot be modified. Ex: (23, 45, "Hello", 100.0)
- Boolean (bool) - Represents a true or false value.
  - The `==` operator is used to determine equality of two objects and returns a boolean.
- The `type()` function can be used to determine the type of a primitive or object.

### Numbers
- Integers and floating point numbers are the two types of numbers in python.
- Arithmetic can be performed with integers, floats, or a combination of the two. For example, adding two integers will result in an integer. However, adding an integer and a float will result in a float.

## Variable Assignments
- Variables in python can contain letters, numbers, and underscores. A variable must start with either a letter or underscore, it cannot start with a number. For example:
  ```
  name = "John"
  _name = "Jerry"
  last_name = "Doe"
  name2 = "Joe"
  ```
- Python variables are **case sensitive** and cannot contain spaces or special characters other than underscore.
- Python naming convention is to separate words in variables using underscores, instead of camel-case (i.e. `first_name` instead of `firstName`).
- The `print()` function can be used to print the value of a variable to the console.

## Lists
- A python list is a mutable collection of objects separated by commas and enclosed in square brackets. For example: `list = [1, 2, 3, 4, 5]`.
- Python uses zero-based indexing to refer to elements within lists. In the above example, 1 has an index of 0 and 5 has an index of 4. Python also uses negative indexes, which start with -1. In the above example, 1 has an index of -5 and 5 has an index of -1. Elements within a list can be referenced using the zero-based or negative index. For example, 1 can be referred to using either an index of 0 or -5.
  - One helpful example of the negative index is finding the last element in a list of unknown length. The index of the last element will always be -1.
  - To address elements in a list using their respective index, you use square brackets as follows: `list[3] = 4`.
- The `len()` function can be used to find the length of a list. For example: `len(list) = 5`.
- The `pop()` function can be used to remove the last element of a list. For example: `list.pop() = 5` and now `list = [1, 2, 3, 4]`.
- The `reverse()` function can be used to reverse the elements in a list. For example: `list.reverse() = [4, 3, 2, 1]`.
- The `append()` function can be used to add an element to the end of a list. For example: `list.append(5)` will result in `list = [1, 2, 3, 4, 5]`.

## Strings
- A python string is an ordered sequence of characters enclosed in either single or double quotes. As with lists, characters within a string can be referenced using zero-based or negative indexes. For example: `str = "Hello"` and `str[0] = 'H'` or `str[-5] = 'H'`.
- The escape character in python is `\`, just like Java. To create a new line within a string, you use `\n`. For example: `'Hello \nWorld'` will print 'Hello' and 'World' on two separate lines.
- Another commonly used escape character is `\t`, which is used to create a tab. For example: `'Hello\tWorld'` would print as `Hello  World`.
- Just as with lists, the `len()` function can be used to find the length of a string, including all spaces. For example: `len("Hello World") = 11`.

### String Slicing
- String slicing in python is a method used to extract a certain sequence of characters from a string. For example, if `str = "Hello World"`, then `str[:] = 'Hello World'`. However, `str[0:5] = Hello`. The range specified excludes the ending index.
- Another interesting way to slice strings in python involves  "jumping", where you specify an exclusive range of indexes, as well as how many characters you want to jump. For example: `str_1 = "I love python"` and `str[0:6:2] = "Ilv"` because the range include 'I love' and the "jump size" is two, so it starts with 'I', then includes every other character up to the 5th character.
- To reverse a string, you can use `::-1`. For example: `str[::-1] = "dlroW olleH"`.

### String Methods and Properties
- You can concatenate strings in python using the + symbol. For example: `str = "Hello " + "World"` would print `'Hello World'`.
- String concatenation can also be performed using the * symbol. For example: If `str = "Hello"` then `str * 3` would print `'HelloHelloHello'`
- Common String Methods (`str = "Hello World"`):
  - `upper()`: `str.upper() = 'HELLO WORLD'`.
  - `lower()`: `str.lower() = 'hello world'`.
  - `split()`: `str.split() = ['Hello', 'World']` because the default split character is a space. `str.split('o') = ['Hell', ' W', 'rld']`. 

### String Formatting
- String formatting in python is a method used to form strings dynamically based on the value of one or more variables.
- When printing a string, you use `{}` as a placeholder for the variable, along with the `format()` method. For example: `print("My name is {}".format("John"))` will print 'My name is John'. Similarly, `print("My name is {} and I am {} years old".format("John", 20))` will print 'My name is John and I am 20 years old'.
  - You can also use the index of elements in the format list to specify which value the placeholder should be replaced with. For example: `print("My name is {1} and I am {0} years old".format("John", 20))` would print 'My name is 20 and I am John years old' because John was listed first and 20 second.
  - Instead of using indexes, you can assign the elements in the format list to variables and use those. For example: `print("My name is {name} and I am {age} years old".format(name = "John", age = 20))` would print 'My name is John and I am 20 years old' because of the way we assigned the variables in the format list.
- Formatting floating point numbers in strings is done as follows:
  ```
  number = 22/7 # 3.142857142857143
  print("My result is {number:1.3f}".format(number)) # number is optional in this case since it's the only value in the format list.
  # Prints '3.143' because the width (numbers before the decimal) is one and the precision (numbers after the decimal) is three.
  # The general form of this notation is {value:width.precision f} (leave out the space).
  ```
- F-String Method:
  ```
  name = "John"
  print(f"My name is {name}") # Prints 'My name is John'
  # Simply placing an 'f' in front of the string enables formatting.
  ```

## Dictionaries
- A python dictionary is an unordered collection of key-value pairs enclosed in curly braces. For example: `d =  {"key1":"value1", "key2":"value2"}`.
- As with lists, you use square brackets to extract a specific value from a dictionary using the key. For example: `d['key1'] = 'value1'`. Similar to lists, dictionaries can also contain key-value pairs of any type. For example: If `d2 = {'k1':100, 'k2':'python', 'k3':[2, 3, 4]}`, then `d2['k3'][2] = 4`.
- The `keys()` function of a dictionary will return a list of keys. For example: `d2.keys() = ['k1', 'k2', 'k3']`.
- The `values()` function of a dictionary will return a list of values. For example: `d2.values() = [100, 'python', [2, 3, 4]]`.
- The `items()` function of a dictionary will return a list of tuples, each of which represents a key-value pair. For example: `d2.items() = [('k1', 100), ('k2', 'python'), ('k3', [2, 3, 4])]`.
- A new key-value pair can be assigned to a dictionary as follows: `d2['k4'] = 25`. Now, `d2 = {'k1':100, 'k2':'python', 'k3':[2, 3, 4], 'k4':25}`. This method can also be used to modify the value of an existing key. For example: `d2['k1'] = 101`. Now, `d2 = {'k1':101, 'k2':'python', 'k3':[2, 3, 4], 'k4':25}`.

## Tuples
- A python tuple is an immutable sequence of objects enclosed in parentheses. For example: `t = ('a', 'b', 'c', 'a', 'a', 'd', 'b')`.
- The `count()` function tells you how many times an object appears in a tuple. For example: `t.count('a') = 3`.
- The `index()` function tells you the index of an element in a tuple. For example: `t.index('c') = 2`. For elements that appear multiple times, `index()` will return the index of the first occurrence. For example: `t.index('a') = 0`.
- Elements within a tuple are retrieved the same way they are for a list. For example: `t[4] = 'a'`.

## Sets 
- A python set is an unordered collection of **unique** elements, enclosed in curly braces.
- The `set()` function can be used to create an empty set. For example: `my_set = set()`.
  - This function can also be used to remove duplicate elements from a list. For example:
    ```
    lst = [1, 1, 1, 2, 3, 4, 4, 5, 6, 7]
    s = set(list) # results in {1, 2, 3, 4, 5, 6, 7}
    ```
- The `add()` function can be used to add an element to a set. For example: `my_set.add(2)` will update the set from `{}` to `{2}`.
  - If we were to use this function to add 2 again, it wouldn't throw an error. It would simply have no effect on the set.
- The `list()` function can be used to convert a set to list. For example: `lst = list(my_set)` would result in a list of `[2]`.

## Booleans
- A python boolean is a true or false value that can be either `True` or `False`, or 1 or 0. They are mostly used in control flow of data.
- An example of something that returns a boolean value is a comparison operator. For example: `4>3 = True`.

## Comparison and Logical Operators
- Comparison operators in python include: `==, !=, >, >=. <, <=`.
- All comparison operators will return a boolean value. For example: `4 == 3` returns `False`.
- Comparison of strings in python is case sensitive. For example: `"Boy" == "boy"` returns `False` while `"Boy" == "Boy"` returns `True`.
- Logical operators in python include: `and`, `or`, as well as `not`. These operators can be used to chain comparison operators.
  - `and` requires that both boolean values be true for the expression to return true.
  - `or` requires that at least one boolean value to be true for the expression to return true.
  - `not` negates the boolean value of the expression.
- Example:
  ```
  2<3 and 4<5 # true
  2>3 and 4>5 # false
  2>3 and 4<5 # false
  2<3 and 4>5 # false
  2<3 or 4<5 # true
  2>3 or 4>5 # false
  2>3 or 4<5 # true
  2<3 or 4>5 # true
  not(2<3 or 4<5) # false
  not(2>3 or 4>5) # true
  ```

## Control Flow Statements
- The three control flow statements in python are: `if`, `elif` and `else`. Control flow statements work as follows:
  ```
  if boolean_expression_a:
    Code to execute if boolean_expression_a returns True.
  elif boolean_expression_b:
    Code to execute if boolean_expression_a returns False and boolean_expression_b returns True.
  else:
    Code to execute by default.
  ```
  - You can have as many `elif` statements as you want, but only one `if` and one `else`.
  - The code will execute for the first boolean expression to return True, or if none return True and an `else` statement is provided, the code within the `else` statement. All statements after the first one to return True will not be evaluated.
  - The indentation is required in these statements.

## Loops
- As in other programming languages, loops in python are used to operate on iterable objects, such as lists and strings. There are `for` and `while` loops in python.
- For loop syntax:
  ```
  for item in iterable:
    Code to execute for each item.
  ```
- For loop examples:
  ```
  lst = [1, 2, 3]

  for item in lst:
    print(item) # Prints 1, 2, and 3 on separate lines (one line for each execution of the code block).
  ```
  ```
  lst = [1, 2, 3, 4, 5, 6, 7, 8, 9]

  for item in lst:
    if item%2 == 0:
      print(item) # prints just the number for even numbers.
    else:
      print("{item} is an odd number".format(item)) # prints '{item} is an odd number' for odd numbers, where {item} is replaced by the value in the list.
  ```
  ```
  phrase = "Hello World"

  for item in phrase:
    print(item) # prints each character (including spaces) in the string.
  ```
  ```
  lst = [(1, 2), (3, 4), (5, 6), (7, 8)]

  for item in lst:
    print(item) # prints each tuple (ex: '(1, 2)') on a separate line (four prints in total).

  for (a, b) in lst:
    print(a, b) # prints the elements in each tuple separated by a space (ex: '1 2'. four prints in total).
  
  for (a, b) in lst:
    print(a) # prints the first value in each tuple
    print(b) # prints the second value in each tuple
    # There will be 8 prints in total printing 1 through 8 consecutively. The code block operates on each tuple independently.
    # This methodology can also be used when working with key-value pairs in dictionaries.
  ```
  ```
  lst = [1, 2, 3, 4, 5, 6, 7, 8, 9]

  total_sum = 0
  for item in lst
    total_sum = total_sum + item # you can also write total_sum += item
  print("Total sum is", total_sum) # prints 'Total sum is 45' because the print statement is outside of the for loop (not indented).

  for item in lst:
    total_sum = total_sum + item
    print("Total sum is", total_sum) # prints the statement for each execution of the loop because the print statement is inside the for loop (is indented). 
  ```
- While loops in python repeat code based on a condition. Specifically, the code in a while loop will continue to execute until the provided boolean expression becomes False.
- When working with while loops, it's very important to avoid infinite loops, where the provided boolean expression never becomes False and the loop executes indefinitely.
- While loop syntax:
  ```
  while boolean_expression:
    Code to execute as long as boolean_expression returns True
  else:
    Code to execute after boolean_expression returns False # optional and only executes once.
  ```
- While loop examples:
  ```
  x = 0

  while x<5:
    print(x) # infinite loop because x will always be less than 5.
  
  while x<5:
    print(x) # prints 0, 1, 2, 3, and 4 (does not print 5 because 5<5 returns False).
    x = x + 1
  ```
- The `break` and `continue` keywords in python are used to interrupt the execution of a loop. `break` stops the entire future execution of the loop. `continue` skips all code below it and proceeds to the next execution of the loop. `pass` simply does nothing (does not interrupt execution of the code) and is often used as a placeholder for actual code within the loop (comments do not suffice). `pass` can also be used as a placeholder in other places, such as `if` statements. For example:
  ```
  lst = [1, 2, 3, 4, 5]

  for item in lst:
    pass # no code within the loop is executed.
  ```
  ```
  lst = [1, 2, 3, 4, 5]

  for item in lst:
    if item%2 == 0:
      continue # note the indentation required for both the for loop and if statement.
    print(item) # will only print odd numbers
  ```
  ```
  x = 0
  while x < 5:
    if x > 3:
      break
    print(x) # prints 0, 1, 2 , and 3 because 4 > 3 and will cause the break statement to execute.
    x+=1
  ```

## Important Functions
- The `range()` function helps avoid needing to create a list of consecutive numbers. The syntax is `range(start, stop, step)`. Only one argument is required. For example:
  ```
  for item in range(10):
    print(item) # prints numbers 1 through 9 because it is exclusive of the last number. The default step argument is 1 and the default start argument is 0.
  
  for item in range(3, 10):
    print(item) # prints numbers 3 through 9.
  
  for item in range(0, 10, 2) # prints even numbers.

  # range() can also be used to generate lists:
  lst = list(range(0, 10)) # creates a list of numbers 1 through 9.
  ```
- The `enumerate` function creates a series of tuples where each pair consists of an item's index in a list or string, followed by its value. For example:
  ```
  test_string = "Hello_World"

  for item in enumerate(test_string):
    print(item) # prints (0, 'H'), (1, 'e'), (2, 'l), and so on. Each on a new line.
  ```
- The `zip()` function creates a series of tuples based on lists (typically of equal length, but not required) by placing the nth index of each list in the tuple. For example:
  ```
  list_1 = [1, 2, 3]
  list_2 = ['a', 'b', 'c']
  list_3 = ['d', 'e', 'f']

  zipped_2_lists = list(zip(list_1, list_2)) # creates a list of [(1, 'a'), (2, 'b'), (3, 'c')]
  zipped_3_lists = list(zip(list_1, list_2, list_3)) # creates a list of [(1, 'a', 'd'), (2, 'b', 'e'), (3, 'c', 'f')]

  for i,j,k in zipped_3_lists:
    print(i,j,k) # prints the elements in each tuple separated by spaces.
    print(i) # prints the first element in each tuple.
    print(j) # prints the second element in each tuple.
    print(k) # prints the third element in each tuple.
  
  # If the lists are of unequal length, it will create tuples based on the length of the shortest list:
  list_a = [1, 2, 3, 4, 5]
  list_b = [1, 2, 3, 4]
  list_c = [1, 2, 3]

  zipped_3_lists = list(zip(list_a, list_b, list_c)) # creates a list of [(1, 1, 1), (2, 2, 2), (3, 3, 3)].
  ```
- The `in` function will check if an element is present in a list or string. For example:
  ```
  'o' in "Hello World" # returns True.
  'a' in "Hello World" # returns False.
  1 in [1, 2, 3] # returns True.
  4 in [1, 2, 3] # returns False.
  'key' in {'key': 10} # returns True. Only checks keys in dictionaries, not values.
  'key1' {'key': 10} # returns False.
  10 in {'key': 10} # returns False.
  ```
- The `min()` and `max()` functions check the minimum and maximum numerical value in a list. For example:
  ```
  min([2, 4, 6, 8, 10]) # returns 2
  max([2, 4, 6, 8, 10]) # returns 10
  ``` 
- The `input()` function will prompt input from the user and optionally store that string value in a variable. For example:
  ```
  name = input('Enter name here: ') # if the user enters 'Jose' when prompted, then name will be assigned a value of 'Jose'. 
  ```
- The `randint()` function produces a random integer (requires importing a library). For example:
  ```
  from random import randint

  number = randint(0,100) # assigns a random integer between 0 and 100 (exclusive).
  ```