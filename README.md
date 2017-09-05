# R-Programming
<h2>R Programming Assignment 2: Lexical Scoping</h2>
<h3>Introduction</h3>
This second programming assignment will require you to write an R function is able to cache potentially time-consuming computations. For example, taking the mean of a numeric vector is typically a fast operation. However, for a very long vector, it may take too long to compute the mean, especially if it has to be computed repeatedly (e.g. in a loop). If the contents of a vector are not changing, it may make sense to cache the value of the mean so that when we need it again, it can be looked up in the cache rather than recomputed. In this Programming Assignment will take advantage of the scoping rules of the R language and how they can be manipulated to preserve state inside of an R object.
<br>
<h3>Example: Caching the Mean of a Vector</h3>
In this example we introduce the <<- operator which can be used to assign a value to an object in an environment that is different from the current environment. Below are two functions that are used to create a special object that stores a numeric vector and caches its mean.

The first function, makeVector creates a special “vector”, which is really a list containing a function to
<ul>
<li>set the value of the vector</li>
<li>get the value of the vector</li>
<li>set the value of the mean</li>
<li>get the value of the mean</li>
</ul>

<code>
makeVector <- function(x = numeric()) { 
</code> <br>
<code>
        m <- NULL</code> <br>
        <code>set <- function(y) { </code> <br>
        <code>x <<- y <br></code>  <br>
             <code>   m <<- NULL </code>  <br>
      <code>  } </code>  <br>
       <code> get <- function() x </code>  <br>
       <code> setmean <- function(mean) m <<- mean </code>  <br>
       <code> getmean <- function() m </code>  <br>
       <code> list(set = set, get = get,</code>  <br>
        <code>     setmean = setmean, </code>  <br>
        <code>     getmean = getmean) </code>  <br>
<code>}
</code>
<br>
<br>
The following function calculates the mean of the special “vector” created with the above function. However, it first checks to see if the mean has already been calculated. If so, it gets the mean from the cache and skips the computation. Otherwise, it calculates the mean of the data and sets the value of the mean in the cache via the setmean function.

<br>

<code> cachemean <- function(x, ...) {</code> <br>
 <code>       m <- x$getmean()</code><br>
       <code> if(!is.null(m)) {</code><br>
             <code>   message("getting cached data")</code><br>
                <code>return(m)</code><br>
       <code> }</code><br>
        <code>data <- x$get()</code><br>
       <code> m <- mean(data, ...)</code><br>
        <code> x$setmean(m) </code><br>
        <code>m </code><br>
<code>}</code>

<br>
<br>


<h3>Assignment: Caching the Inverse of a Matrix</h3>

Matrix inversion is usually a costly computation and there may be some benefit to caching the inverse of a matrix rather than compute it repeatedly (there are also alternatives to matrix inversion that we will not discuss here). Your assignment is to write a pair of functions that cache the inverse of a matrix.

Write the following functions:

<ul>
<li>makeCacheMatrix: This function creates a special “matrix” object that can cache its inverse.</li>
<li>cacheSolve: This function computes the inverse of the special “matrix” returned by makeCacheMatrix above.<br> If the inverse has already been calculated (and the matrix has not changed), then the cacheSolve should retrieve the inverse from the cache.</li>

</ul>

<h5>NOTE:</h5> For this assignment, assume that the matrix supplied is always invertible.

My SOlution is <b>cachematrix.R</b>.
