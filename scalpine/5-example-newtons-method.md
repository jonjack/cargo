# Example - Newtons Method




---

### Recursive functions always have explicit return type

To determine the return type of a function (if it is not stated explicity) the Scala compiler needs to inspect the right-hand side of the function definition. Since recursive functions call themselves, this means the compiler would get into an infinite loop when attempting to inspect the right-hand side of the function. In order to avoid this the Scala compiler requires that we always explicitly provide the return type for a recursive function.

---

### Newtons Method Example

To find the square root of a number we can use Newton's method of successive approximations.

You start off with an initial arbitrary estimate value `y` eg. `y = 1`    
`x` = the number we want to find the square root of eg. `2`      
`y` = our initial arbitrary guess eg. `1`       

Then repeatedly improve the estimate by taking the mean between the two numbers `y` and the result of `x/y`. This will move the estimate closer and closer towards the true square root.

Example

```scala
// Estimate		Quotient    				Mean (between estimate and quotient)
//											(estimate + quotient) / 2

    1       	2 / 1 = 2      				(1 + 2) / 2 				= 	1.5
 	1.5     	2 / 1.5 = 1.3333			(1.5 + 1.3333) / 2			=	1.4167
 	1.4167		2 / 1.4167 = 1.4118			(1.4167 + 1.4118) / 2		=	1.4142
 	1.4142

 	1.4142 * 1.4142 = 1.99996 (pretty close to 2)
```

Solution source

```scala
package week1

object session {

  // return the absolute number of x
  def abs(x: Double) = if(x < 0) -x else x
  
  
  /*
   * sqrtIter is a recursive function which shall call itself until it finds a close enough
   * 					approximation to the square root, at which point it stops and returns it
   * guess 	= our initial estimate
   * x 			= the number we want the square root of
   *
   */
  def sqrtIter(guess: Double, x: Double): Double = {

  	println(guess)
  	
  	// check if the estimate is close to the square root and if so return it
  	if(isGoodEnough(guess, x)) guess

  		// or else call ourself again with the result of improving the estimate
  		else sqrtIter(improve(guess, x), x)
  }

  
  /* what is a good approximation?
   * if we multiply the estimate (called `guess`) by itself and then compare this to the
   * number we want the square root of then they should be the same if `guess` is the true square root
   * if compare to some infinitestimal small value (epsilon) and its less than it then we can say that
   * we are really close to the real square root and can accept the approximation
   */
  def isGoodEnough(guess: Double, x: Double) =
  	abs(guess * guess - x) / x < 0.001
  	
  def improve(guess: Double, x: Double) =
  	(guess + x / guess) / 2
  	
  // Now a function we can call which brings it all togethor
  // It simply passes our argument x and an arbitrary estimate 1.0 to sqrtIter()
  def sqrt(x: Double) = sqrtIter(1.0, x)
  
  
  // TESTING IT OUT
  sqrt(2)
  sqrt(4)
  
  // there are some problems though
  
  // very small numbers it is not accurate enough 1e-6 -> 0.000001
  sqrt(1e-6)
  
  // 1e25 -> 10,000,000,000
  sqrt(1e+10)
  // the + is not strictly necessary
  sqrt(1e10)
  
  // for very large numbers it leads to non-termination
  // the following just hangs!
  // sqrt(1e60)
  
}
```

---

### Excercise

In considering the above, here is an exercise.

#### 1. The `isGoodEnough` test is not very precise for small numbers and can lead to non-termination for very large numbers. Explain why.

##### For small numbers

The epsilon value is too large so we could try making it smaller ie. 0.001 --> 0.000000000000001 ?

##### For very large numbers
What `isGoodEnough` essentially does is compare how far away from each other the square of the guessed square root `guess` and the number we are trying to find the square root of `x` are.

`guess` = estimated square root    
`guess * guess` = square of the estimate    
`x` = number we are trying to the square root of 

if `(guess * guess)` = `x` then our square root is spot on    

eg. lets say    
`guess` = `2`    
`x` = `4`

`2 * 2` = `x`    
`2 * 2` = `4`    
`2 * 2 - x` = `0`    

so `(guess * guess - x) < 0.001` = `true`

If the difference between `(guess * guess)` and `x` is `< 0.001` then we are saying in the following expression that that is acceptable eough to return `true`

The problem (according to Odersky) is that 2 very large numbers might always be further apart than 0.001 which means `isGoodEnough` never evaluates to `true`. This is because of the number of places in the mantissa of the large floating point number apparently. This means that `(guess * guess - x) < 0.001` never evaluates to `true`. This means the iteration never stops since we never find a value that is good enough.


#### 2. Design a different version of `isGoodEnough` that does not have these problems.

For the small numbers issue I will try setting the epsilon value to `0.000000000000001`

According to Odersky - the solution to both problems is to make the test proportional to `x` as follows. This divides the result of the comparison by `x` and then compares the result of this to `0.001`.

```scala
abs(guess * guess - x) / x < 0.001

// eg.
x = 4
guess = 
```

#### 3. Test your version with some very very small and large numbers.

	eg.    
	0.001    
	0.1e-20    
	1.0e20    
	1.0e50    



