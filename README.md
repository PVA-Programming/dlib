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

Let's say you wanted to test if all of your tanks were below 1 PSI.

1. First we create an array of tanks to iterate over:
```asm
   DM TANKS[3]   
   TANKS[0]=aGAUGE1
   TANKS[1]=aGAUGE2
   TANKS[2]=aGAUGE3
```
2. Then we create a predicate function to test whether each tank is at a low PSI:
```asm
#LOWPSI
EN,,(AN_ACT[^a]<1)
```
This predicate takes a number corresponding to the analog and returns if the actual psi reading is below 1 psi.

To access the first argument passed to a function in DMC, you use ^a. If there were a second parameter you would use ^b, and so on.

To return a value from a function in DMC, you have to specify the value as part of the EN command after two ','s like this:

```asm
EN,,(AN_ACT[^a]<1)
```
The returned value can then be accessed through _JS.

The syntax is awful, but it works :^).

3. Finally, we can make use of #ALL
```asm
JS#ALL("TANKS", #LOWPSI)
ALL_LOW = _JS
```

Now ALL_LOW will tell us if all the tanks are low psi or not.

You could easily add more tanks to your check by adding another element to TANKS[], or you could change your PSI threshold by changing the #LOWPSI predicate.
You could check something else about the tanks by creating a new predicate function, etc.

The code is also (in my opinion) much clearer.

## What's in here?

- ### WAITFOR
  ```asm
  JS#WAITFOR(#PREDICATE)
  ```
  Waits until #PREDICATE evaluates to true.

- ### ALL
  ```asm
  #ALL("array", #PREDICATE)
  ```
  Checks if #PREDICATE returns true for all elements in the array

- ### FOREACH
  ```asm
  #FOREACH("array", #CALLBACK)
  ```
  Applies the #CALLBACK function to each element in the array. 
  
