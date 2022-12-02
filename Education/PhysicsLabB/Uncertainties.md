# Welcome!
Welcome to your (potentially first) python Jupyter Notebook program! Jupyter Notebook makes it very easy to write and execute code. Most of the code is already written for you and you will only have to make slight modifications to perform the experiments.

You can use the Table of Contents below to navigate to different sections of the code. These sections of the code correspond with the lab hand out, so make sure you follow along with the lab handout directions.

# Table of contents
1. [Activity I](#activityI)
1. [Activity II](#activityII)
3. [Experiment A: Flipping 1 single coin N times](#singlecoin)
4. [Experiment B: Flipping n fair coins N times](#multicoin)

## Activity I: Introduction to python<a name="activityI"></a>
### I.1 
First, execute the next cell below (the box with code in it) by clicking in the cell and pressing <b>Shift + Enter</b>. This will run only the code present in that cell.<br> 
    &nbsp; &nbsp; &nbsp; &nbsp;- When you see the value 'In [   ]' to the left of the cell increment to a higher number, this indicates you have successfully executed the code within that cell. If you see 'In [ * ]', this incidate the code is in the process of running.<br>
    &nbsp; &nbsp;&nbsp; &nbsp;- Anytime you see a '#' in a cell of code it indicates the start of a comment. These comments are not executed as code and provide more information to the reader about the code. <br><br>
    
    
Next, change the value of a and/or b and re-execute the cell.


```python
a = 2       #assigning a value to variable a
b = 3       #assigning a value to variable b
c = a + b   #adding variables a and b and storing the result in c
print(c)    #printing the value of c 
```

The previous cell defined variables a, b, and c and then prints the value of c. Now, try to write some code in the empty cell below to find the average of a and b and print the result. <br>
    &nbsp; &nbsp;&nbsp; &nbsp;- Just like any typical calculator, the order python executes operations is governed by PEMDAS.<br>
    &nbsp; &nbsp;&nbsp; &nbsp;- Remember to check you math - try a few values of a and b to confirm your code is working properly! <br>
    &nbsp; &nbsp;&nbsp; &nbsp;- Include a copy of your code in your lab notebook   (you can hand write or screenshot using <b>Command + Shift + 4 </b>).
    


```python
#enter your code for I.1 in this cell




```

### I.2
Now we will define a function named 'add' that performs the same operation as the code in the first cell you executed at the start of this activity. <br>
   &nbsp; &nbsp; &nbsp; &nbsp;- A function is a block of code that can be called at any point after it has been intially executed. The keyphrase 'def' indicates a new function is being defined. <br>
    &nbsp; &nbsp;&nbsp; &nbsp;- Note that indentations and colons are necessary most of the time in python. <br><br>
Execute the cell below to define the 'add' function.


```python
def add(a,b):   #a and b are the arguments or inputs to the function
    return a+b  #calling the function add with inputs will output a+b
```

Execute the cell below to now call the 'add' function with the given inputs for the variables a and b. <br><br>
Next, change the value of a and/or b and re-execute the cell.


```python
add(2,3)
```

Now that you have seen how to define functions and change the input, write some code in the empty cell below to define a function 'mean' that calculates the average of a and b and returns the result. <br>
    &nbsp; &nbsp;&nbsp; &nbsp;- Remember to check you math - try a few values of a and b to confirm your code is working properly!<br>
    &nbsp; &nbsp;&nbsp; &nbsp;- Include a copy of your function in your lab notebook and an example of your code working properly (you can hand write or screenshot this).


```python
#enter your code for I.2 in this cell




```

## Activity II : Graphical anaylsis<a name="activityII"></a>
### Initial Setup <a name="setup"></a>
The python language itself does not contain all the mathematics and visualization tools that would be helpful to use in experiments. However, there are vast amounts of open source python packages available online to expand the capabilities of the base python language. These packages contain predefined modules with helpful functions like the mean or standard deviation. That way, we do not need to actually write a lot of code from scratch - we can just use the functions that already exist in popular packages.
This next cell imports some helpful packages in python.



```python
#Execute, but do not edit this cell. 
import pandas as pd                       #Useful package for working with data tables
import numpy as np                        #Useful package for math operations
import matplotlib.pyplot as plt           #Useful package for plotting
import random as rnd                      #Package with a random number generator

plt.rcParams['figure.figsize']=[12,8.2]   #This makes all graphs bigger by default

```

## II.1 and II.2

This next cell uses the matplotlib.pyplot python package to generate a semi-log plot with no data. Run this cell, make sure you understand the output axes, and answer the corresponding questions in your lab manual.


```python
plt.xlabel('X')                                         #adds x-axis label
plt.ylabel('Log(Y)')                                    #adds y-axis label
plt.title('Semi-Log Plot')                              #adds title
plt.grid(which = 'both')                                #adds grid lines at tick marks
plt.yscale('log')                                       #sets y-axis scale
plt.ylim(0.1,100)                                       #defines the min and max y-value in plot
plt.xlim(0.1,100)                                       #defines the min and max x-value in plot
plt.show()                                              #displays plot
```


## Experiment A: Flipping 1 fair coin N times <a name="singlecoin"></a>

This first cell does two things: 
 1. it defines a variable N as the number of times a coin is flipped and 
 2. sets a 'seed' for a random number generator. 

A random number generator in any programming language is actually a psuedorandom number generator - it can produce a random distribution of numbers based on some user input restrictions, but is dependent on the seed. A seed is used so that <b>everytime</b> a list of random numbers is generated, the <b>same</b> list is produced. Here, the seed is just some integer value.


```python
N = 1000     #number of times a coin is flipped
seed = 1     #generates the same random number sequence each time
```

This next cell contains the code with the pseudorandom number generator. This pseudorandom number generator is coded to flip a fair coin N times and records the result of each flip in a table as the following: Heads = 1 and Tails = 0. 

This cell then prints a table with N rows and each row shows the result of a coin flip H(i). Notice that the python language is indexed starting at 0, not 1 and thus, the first row is labeled 0. This is still the first coin flip/first trial.

<b> Anytime you change the N or seed variable, you must re-execute this next cell. </b> Keeping N and the seed the same produce the same results each time the cell is executed.  


```python
#Execute, but do not edit this cell.
np.random.seed(seed) #generates the same random number sequence each time based on N and the seed
coin_flip = np.random.randint(2, size = N)#makes a table of the data
table = pd.DataFrame(coin_flip, columns = ['H(i)']) #stores array of random numbers as a table
print(table) #prints the table


```

Below is a function named statistics that has been predefined for you. It calculates a running mean, standard deviation, and standard error from the first trial to some user defined later trial number up to H(N). The number of flips can include the first 2 rows, the first 10 rows, the first 988 rows, or the entire data set. 


```python
#Execute, but do not edit this cell.
def statistics(number_of_trials):
    print('\n First ' + str(number_of_trials) + ' trials')
    print('Mean:                  ', "{:.3f}".format(np.mean(coin_flip[0:number_of_trials])))
    print('Standard Deviation:    ', "{:.3f}".format(np.std(coin_flip[0:number_of_trials],ddof = 1)))
    print('Standard Error:        ', "{:.3f}".format((np.std(coin_flip[0:number_of_trials],ddof = 1)
                                                      /np.sqrt(number_of_trials))))
    
    return 
```

To run the statistics function, change the number inside the parenthesis to the number of trials you would like to perform the statistics on. <br>
    &nbsp; &nbsp;&nbsp; &nbsp; - For example, if you want the mean of the first ten rows in your table, which is H(1) to H(10), execute 'statistics(10)'. <br>
    &nbsp; &nbsp;&nbsp; &nbsp;- If the function returns 'NaN,' this stands for 'Not a Number' and indicates the value could not be calculated.


```python
statistics(1000)
```

The next cell generates a semi-log graph that shows a 'running' cummulative mean value of H. The right-most data point is the mean of all the trials. It also adds the standard uncertainty of the mean as the error bars.


```python
cum_mean = table['H(i)'].expanding().mean()           #calculates cummulative mean of table
cum_sem = table['H(i)'].expanding().sem(ddof=0)       #calculates the cummulative st error of table
plt.errorbar(cum_mean.index.values,cum_mean,yerr=cum_sem, ecolor='red', capsize=3) #makes plot
plt.xlabel('Coin Flip')                               #adds x-axis label
plt.ylabel('Mean Result for H(i) from i=1 to N')      #adds y-axis label
plt.title('Mean Value (N = '+str(N)+' and Seed = ' + str(seed) +')') #adds title
major_ticks = np.arange(0,1,0.1)                      #defines the y-axis major tick values
plt.yticks(major_ticks)                               #adds y-axis ticks
plt.grid()                                            #adds grid lines
plt.xscale('log')                                     #try commenting out this line to see how the plot changes!
plt.ylim(0,1)                                         #defines the min and max y-value in plot
plt.show()                                            #displays plot
```

The next cell generates a graph that shows a 'running' cummulative standard deviation of H. The right-most data point is the standard deviation of all the trials.


```python
cum_std = table['H(i)'].expanding().std(ddof = 1)        #calculates cummulative st dev of table
plt.scatter(cum_std.index.values, cum_std)              #makes plot
plt.xlabel('Coin Flip')                                 #adds x-axis label
plt.ylabel('Standard Deviation Result for H(i) from i=1 to N') #adds y-axis label
plt.title('Standard Deviation (N = '+str(N)+' and Seed = ' + str(seed) +')') #adds title
plt.yticks(major_ticks)                                 #defines the y-axis major tick values
plt.grid()                                              #adds grid lines
plt.xscale('log')                                       #try commenting out to see how the plot changes!!
plt.ylim(0,1)                                           #defines the min and max y-value in plot
plt.show()                                              #displays plot
```

The next cell generates a log-log plot of the 'running' cummulative standard error of H.


```python
plt.scatter(cum_sem.index.values,cum_sem, s = 2) #makes plot
plt.xlabel('Coin Flip') #adds x-axis label
plt.ylabel('Standard Error Result for H(i) from i=1 to N') #adds y-axis label
plt.title('Standard Error Value (N = '+str(N)+' and Seed = ' + str(seed) +')') #adds title
major_ticks = np.arange(0.01,1,0.1) 
plt.yticks(major_ticks)                                 #defines the y-axis major tick values
plt.grid()                                              #adds grid lines
plt.xscale('log')                                       #makes x-axis log scale
plt.yscale('log')                                       #makes y-axis log scale
plt.ylim(.01,1)                                         #defines the min and max y-value in plot
plt.show()                                              #displays plot
```

## Experiment B: Flipping n fair coins N times<a name="multicoin"></a>

This next cell does two things: 
 1. it defines a variable n as the number of fair coins flipped at once
 2. it defines a variable N as the number of times n coin flips is repeated, and 
 3. sets a 'seed' for a random number generator. 


```python
n = 100       #number of fair coins flipped at once
N = 100     #number of times n coin flips is repeated
seed = 1
```

For this next cell, the output data table shows the number of heads m out of n coin flips. Do not worry too much about understanding every line of code, just focus on understanding the information given in the output data table. 

<b> Anytime you change n, N, or the seed variables, you must re-execute this next cell </b>. Keeping n, N, and the seed the same will produce the same results each time the cell is executed. 


```python
#Execute, but do not edit this cell. 
data = []
rnd.seed(seed)
for a in range(N):
    lst = []
    for b in range(n): 
        H = rnd.randint(0,1)  #generates single coin flip at heads or tails
        lst.append(H)
    m = lst.count(1)          #counts number of heads 
    data.append(m)
        
tableB = pd.DataFrame(data, columns = ['m']) #stores array of random numbers as table
print(tableB)
```

Below is a function named statistics2 that has been pre-defined for you. It calculates a running mean, standard deviation, and standard error from the first trial H(1) to some user defined later trial number up to H(N) just like the statistics function from Experiment A. 


```python
#Execute, but do not edit this cell.
def statistics2(number_of_trials):
    print('\n Statistcs for n = ' +str(n)+' coins flipped N = ' + str(N) +' times')
    print('Mean:                  ', "{:.3f}".format(np.mean(data[0:number_of_trials])))
    print('Standard Deviation:    ', "{:.3f}".format(np.std(data[0:number_of_trials]), ddof = 1))
    print('Standard Error:        ', "{:.3f}".format((np.std(data[0:number_of_trials], ddof = 1)
                                                      /np.sqrt(number_of_trials))))
    return 
```


```python
statistics2(1000)
```


```python
plt.hist(tableB['m'], rwidth = 0.95)     #makes plot
plt.xlabel('Values of m')                #adds x-axis label
plt.ylabel('Counts')                     #adds y-axis label
plt.grid(axis = 'y')                     #adds grid lines
plt.xlim((n/2) - 20, (n/2) + 20)         #defines x-axis limits
plt.title('Histogram (n = '+str(n)+', N = '+str(N)+', and Seed = ' + str(seed) +')') #adds title
```

Once complete, click the "Logout" button in the upper right corner of the Jupyter
Notebook. The notebook does not stop running when the browser tab is closed, so
you must make sure to shutdown the Notebook when complete. Logout of any open browser tab!
