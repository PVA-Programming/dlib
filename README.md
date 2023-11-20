# dlib
Awesome library of useful DMC algorithms created by the world's most handsome programmer

## Why would I care?
These functions implement basic things you'll often want to do like:
 - iterating over all elements of an array and doing something to each one
 - waiting until certain conditions are met
 - query an array to see what is true about all, some, or none of the elements

Using them could be convenient and can make DMC code a little more expressive and readable.

## How do I use these?

Here's an example:
The #ALL function takes:
1. an array
2. a Predicate function (a function that evaluate an input and return 1 or 0, *true* or *false*)

Like this: 
```
JS#ALL("array",#Predicate)
```
It will loop over all the elements of the array and pass them to your predicate function. 
If any of these calls to the predicate return 0 (false), #ALL will return 0. If all of the calls to the predicate return 1 (true), #ALL will return 1 (true).

Here's an example of how to use #ALL in real code:

We want to know if all the of the tanks are at a low PSI.

1. First we create an array of tanks to iterate over:
```
   DM TANKS[3]   
   TANKS[0]=aGAUGE1
   TANKS[1]=aGAUGE2
   TANKS[2]=aGAUGE3
```
2. Then we create a predicate function to test whether each tank is at a low PSI:
```
REM Returns if the psi of analog is lower than 1
REM 
REM ^a - The analog number
#LOWPSI
EN,,(AN_ACT[^a]<1)
```
This predicate takes a number corresponding to the analog and returns if the actual psi reading is below 1 psi.

To access the first argument passed to a function in DMC, you use ^a. If there were a second paramter you would use ^b, and so on.

To return a value from a function in DMC, you have to specify the value as part of the EN command after two ','s like this:

```
EN,,(AN_ACT[^a]<1)
```
The returned value can then be accessed through _JS.

The syntax is awful, but it works :^).

3. Finally, we can make use of #ALL
```
JS#ALL("TANKS", #LOWPSI)
ALL_LOW = _JS
```

Now ALL_LOW will tell us if all the tanks are low psi or not.

## What's in here?

- ### WAITFOR
  ```
  JS#WAITFOR(#PREDICATE)
  ```
  Waits until #PREDICATE evaluates to true.

- ### ALL
  ```
  #ALL("array", #PREDIATE)
  ```
  Checks if #PREDICATE returns true for all elements in the array

- ### FOREACH
  ```
  #FOREACH("array", #CALLBACK)
  ```
  Applies the #CALLBACK function to each element in the array. 
  
