# Movies on flight

> You are on a flight and wanna watch two movies during this flight.  
> You are given int\[\] movie\_duration which includes all the movie durations.  
> You are also given the duration of the flight which is d in minutes.  
> Now, you need to pick two movies and the total duration of the two movies is less than or equal to \(d - 30min\).  
> Find the pair of movies with the longest total duration. If multiple found, return the pair with the longest movie.
>
> e.g.  
> Input  
> movie\_duration: \[90, 85, 75, 60, 120, 150, 125\]  
> d: 250
>
> Output from aonecode.com  
> \[90, 125\]  
> 90min + 125min = 215 is the maximum number within 220 \(250min - 30min\)

## Solutions

### Approach \#1

1. maintain a copy of movieDuration and sort it.
2. use two pointers from left\(biggest ones\) + right \(smallest ones\), if the sum is smaller than d and then larger than the current maximum, then we find a solution.
3. update ans with the index, here we have to refer the index to the original movieDuration array.
4. `len(movieDurations) - movieDurations[::-1].index(newM[j]) - 1]` for the second index is to prevent returning the same indices when duplicate elements are provided \(see test case 5\)

```python
def moviesOnFlight(movieDurations, d):
    d = d-30
    newM = movieDurations
    newM = sorted(newM, reverse = True)
    maximum = 0
    ans = []
    for i in range(len(newM)):
        for j in range(len(newM)-1, i, -1):
            sum = newM[i]+ newM[j]
            if sum <= d:
                if sum > maximum:
                    maximum = newM[i] + newM[j]
                    ans = [movieDurations.index(newM[i]),len(movieDurations) - movieDurations[::-1].index(newM[j]) - 1]
            else:
                break
    
    return sorted(ans)

# [90, 85, 75, 60, 120, 150, 125], 250 | [0,6]
# [90, 85, 75, 60, 120, 150, 125], 50 | []
# [90, 85, 75, 60, 120, 150, 125], 220 | [3,6]
# [10, 50, 60] , 120 | [0,2]
# [90, 85, 75, 60, 120,110,110, 150, 125] , 250 | [5, 6]

print (moviesOnFlight([90, 85, 75, 60, 120,110,110, 150, 125] , 250))
```

