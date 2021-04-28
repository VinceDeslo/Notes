# Python

# Python:

List:

```python
my_list = [1, 15, 23, 7]

# iteration:for val in my_list:    
print(val)
first_el = z[0] # 3
last_el = z[-1] # 2
# slicing: first inclusive, second not inclusive
slice = z[0:2] # [3, 7]
slice = z[2:] # [4, 2]

# functions
min(z)
max(z)
len(z)
sum(z)

# methods:
c = z.count(4)          # c = 1
c = z.index(4, 2, 4)    # find first starting at index 2 and ending at index 4 (c = 2)
z.sort()                # A-Z for string or ascending for numerical
z.sort(reverse = True)  # Z-A or descending for numerical
new_list = sorted(z)    # copies list without altering original
z.append(3)             # appends at last element
z.remove(3)             # removes element with value 3
z.pop(2)                # removes and returns the value at index 2
z.extend([4, 5])        # concats to end of list
y = z + x               # concats two lists of any type
z.insert(4, [4, 5])     # inserts a nested list
```

Comprehensions:

```python
my_list = [1, ‘4’, 9, ‘a’, 0, 4]

squared_ints = [ e**2 for e in my_list if type(e) == types.IntType ]

print squared_ints # [ 1, 81, 0, 16 ]
```

Tuple:

```python
my_tuple = ("item1", 10, "item2", 5.37)
# iteration
for val in my_tuple:    
	print(val)
```

Sets:

```python
my_set = {10, 15, 20, 25, 10}
# iteration: will print everything without duplicates (10, 15, 20, 25)
for val in my_set:    
	print(val)
```

Dictionaries:

```python
my_dict = dict(name="Bob", salary="80k") # with constructor
my_dict = {"name": "Bob", "salary": "80k"}
	
print(my_dict)            # prints dictionnary
my_dict["age"] = 45       # adds value to dictionnary
my_dict.popitem()         # removes last item addeddel 
my_dict["salary"]         # removes item at specified key
my_dict.clear()           # clears the dictionnary, object stille exists
del my_dict               # removes entire dictionnary
new_dict = my_dict.copy() # clones dictionnnary
```

Casting:

```python
number = int(1.8)  # gives 1
decimal = float(1) # gives 1.0
word = str(3)      # gives "3"
```

Assignment expressions (Walrus operator):

```python
name := expression

# Example: Filtering over length
words = ["hi","this","is","a","test"]
for word in words:    
	if (length := len(val)) > 3:        
		print(word)
```

Lambdas (Anonymous functions):

```python
# lambda arguments : expression 
x = lambda arg1, arg2 : arg1 + arg2 
x(5, 10) # returns 15
```

Decorators:

```python
#functions are defined as objects in Python (kinda like pointer to address of object)  

#wrapper function:  
def f1(func):      
	def wrapper():          
		print("started")          
		func()          
		print("ended")      
	return wrapper  

#Calls the returned wrapped function  
f1(f)()  

# added decorator instantly applies the wrapper to f() no need for aliasing  
@f1  
def f()    
	print("howdy")  

#function aliasing  
x = f1(f)  
x()  

# To handle variable parameters, *args **kwargs  
def f1(func):      
	def wrapper(*args, **kwargs):          
		print("started")          
		func(*args, **kwargs)          
		print("ended")      
return wrapper

#......................................... 
# return values from decorated functions  
@f1  
def add(x, y):      
	return x+y  

# return value from wrapper  
def f1(func):      
	def wrapper(*args, **kwargs):          
		print("started")          
		val = func(*args, **kwargs)          
	print("ended")          
	return val      
return wrapper
```

Iterators:

```python
#must contain following methods    
__iter__()    
__next__()    

mlist = [4, 7, 0, 3]    
# returns iterator of object    
i = iter(mlist)    
next(mlist)    
# Last element will throw exception    

for element in mlist:        
	print(element)    

# custom Iterator    
class Iter():        
	def __init__(self, max = 0):            
			self.max = max        
	def __iter__(self):            
			self.n = 0            
			return self.n        
	def __next__(self):            
			if self.n <= self.max:                
				result = 2 ** self.n                
				self.n += 1                
				return result            
			else:                
				raise StopIteration    

# Use
for i in Iter(5):        
	print(i)
```

Generators:

```python
# Generators automate creation or iterators
# Generator returns an object that is iterable
# yield pauses the function and keeps states (returns one at a time)

def my_gen():    
	n = 1    
	print("Printed first")    
	yield n    
	
	n+=1    
	print("Printed last")    
	yield n

# Iteration over a generator
for i in my_gen():    
	print(i)

# precreates the range list
def range(start, stop, step = 1)    
	numbers = []    
	while start < stop:        
		numbers.append(start)        
		start += step    
	return numbers

# returns many values without creating list
def xrange(start, stop, step = 1):    
	while start < stop:        
		yield start        
		start += step

# Uses 10 times more memory then xrange because of list
for i in range(0, 10000):    
	pass
# Yields only current value as iteration is done
for i in xrange(0, 10000):    
	pass
```

---

# DATA STRUCTURES:

Stack:

```python
# List form with 0(n) complexity
stack = []
stack.append()
stack.pop() # pop returns poped value

# Deque form with 0(1) complexity for append and pop
from collections import deque
stack = deque()
stack.append()
stack.pop() # pop returns poped value

# With queue module
from queue import LifoQueue
stack = LifoQueue(maxsize = 3)
stack.qsize() # prints queue size
stack.put() # adds to queue
stack.get() # pops from queue
stack.empty() # indicates if empty
stack.full() # indicates if full
stack.put_nowait() #
stack.get_nowait() # returns item once one is available
```

Queue:

```python
# List form with 0(n) complexity
queue = []
stack.append()
stack.pop(0) # pop(0) returns poped first value

# Deque form with 0(1) complexity for append and pop
from collections import deque
q = deque()
q.append()
q.popleft() # returns poped value

# With queue module
from queue import Queue
q = Queue(maxsize = 3)
q.qsize() # prints queue size
q.put() # adds to queue
q.get() # pops from queue
q.empty() # indicates if empty
q.full() # indicates if full
q.put_nowait() #
q.get_nowait() # returns item once one is available
```

Binary Tree:

```python
class Node:    
	def __init__(self, data):        
		self.left = None        
		self.right = None        
		self.data = data
	
	# Recursive print
	def PrintTree(self):       
			if self.left:            
				self.left.PrintTree()        
			print( self.data)        
			if self.right:            
				self.right.PrintTree()

# Inorder traversal
# Left -> Root -> Right    
def inorderTraversal(self, root):        
	res = []        
	if root:            
		res = self.inorderTraversal(root.left)            
		res.append(root.data)            
		res = res + self.inorderTraversal(root.right)        
	return res

# Preorder traversal
# Root -> Left ->Right    
def PreorderTraversal(self, root):        
	res = []        
	if root:            
		res.append(root.data)            
		res = res + self.PreorderTraversal(root.left)           
		res = res + self.PreorderTraversal(root.right)        
	return res

# Postorder traversal
# Left ->Right -> Root    
def PostorderTraversal(self, root):        
	res = []        
	if root:            
		res = self.PostorderTraversal(root.left)            
		res = res + self.PostorderTraversal(root.right)           
		res.append(root.data)       
	return res
```

---

# OOP

Class:

```python
class MyClass(object):    
	
	# Constructor    
	def __init__(self, val='Yeet'):        
		self.name = val    
	
	# member    
	x = 5   
	
	# Class method    
	def ClassMethod(arg1):        
		print(arg1)    
	
	# Getter method    
	@property    
	def name(self):        
		return self.__name    

	# Setter method    
	@name.setter    
	def name(self, val):        
		self.__name = val    

	# Deleter method    
	@name.deleter    
	def name(self):       
		del self.__name

# Instantiation
item = MyClass(5)
print(item.val) # access
item.val = 10   # modification
```

---

# MATH STUFF

Factorial:

```python
def factorial(n):   
	if n == 1:       
		return n   
	else:       
		return n * factorial(n-1)
```

Fibonacci:

```python
def fibo(n):    
	if n <= 0:        
		print("Incorrect input")    
	# First Fibonacci number is 0    
	elif n == 1:        
		return 0    
	# Second Fibonacci number is 1    
	elif n == 2:        
		return 1    
	else:        
		return Fibonacci(n - 1) + Fibonacci(n - 2)
```

Prime numbers:

```python
def primes(lower, higher):    
	primes = []    
	for num in range(lower, higher):    
		if all((num % i) != 0 for i in range(2, num)):       
			primes.append(num)
```

Splitting numbers into digits:

```python
n = 123
list_digits = [int(i) for i in str(n)]
print(list_digits) # prints [1,2,3]
```

---

# System programming

Sys module:

```python
import sys

sys.argv # All arguments passed to the script
sys.argc # Number of arguments passed to the script
sys.display # Hook for shell display
sys.stdin   # input stream
sys.stdout  # output stream
sys.stderr  # error stream
sys.stdout = open("file.txt", "w")  # Redirection of a stream to a file
```

OS module:

```python
import os

os.system() # Executing shell scripts (bash)

# Process related
pid = os.fork() # clone process (if pid=0 in child)
os.getpid() # gets current process id
os.execl() # execute a program from code (check out all exec variations)

# Thread related (Kernel threads and User threads)
import threading

# Pipes (FIFO)
```

---

# C Specific stuff

enum:

```python
class EnumName(object):    
	Member1 = 0    
	Member2 = 1    
	Member3 = 2

call -> SomeClass.MemberX
```

C structs:

```python
class StructName(ctypes.LittleEndianStructure):    
	_fields_ = [        
		("Header", ctypes.c_uint16, 16), #[0..15]        
		("Load", ctypes.c_uint8 * 32), # 32 words of data        
		("Trailer", ctypes.c_uint16, 1) # 1 bit of frame    
	]

Frame = Structname()    # Instantiation
Frame.Header = 0x1010   # Data Packing
```