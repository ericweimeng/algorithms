# Top K Frequently Mentioned Keywords

> Given a list of `reviews`, a list of `keywords` and an integer `k`. Find the most popular `k` keywords in order of most to least frequently mentioned.
>
> The comparison of strings is case-insensitive.  
> Multiple occurances of a keyword in a review should be considred as a single mention.  
> If keywords are mentioned an equal number of times in reviews, sort alphabetically.
>
> **Example 1:**
>
> ```text
> Input:
> k = 2
> keywords = ["anacell", "cetracular", "betacellular"]
> reviews = [
>   "Anacell provides the best services in the city",
>   "betacellular has awesome services",
>   "Best services provided by anacell, everyone should use anacell",
> ]
>
> Output:
> ["anacell", "betacellular"]
>
> Explanation:
> "anacell" is occuring in 2 different reviews and "betacellular" is only occuring in 1 review.
> ```
>
> **Example 2:**
>
> ```text
> Input:
> k = 2
> keywords = ["anacell", "betacellular", "cetracular", "deltacellular", "eurocell"]
> reviews = [
>   "I love anacell Best services; Best services provided by anacell",
>   "betacellular has great services",
>   "deltacellular provides much better services than betacellular",
>   "cetracular is worse than anacell",
>   "Betacellular is better than deltacellular.",
> ]
>
> Output:
> ["betacellular", "anacell"]
>
> Explanation:
> "betacellular" is occuring in 3 different reviews. "anacell" and "deltacellular" are occuring in 2 reviews, but "anacell" is lexicographically smaller.
> ```

## Solutions

### Approach \#1

```python
import collections
import bisect
def get_top_K(reviews, keywords, k):
    
    f = collections.defaultdict(int)
    
    most_freq = 0
    
    for review in reviews:
        for w in keywords:
            if w in review.lower():
                f[w] += 1
                most_freq = max(most_freq, f[w])
    
    frequency = collections.defaultdict(list)
    for w, freq in f.items():
        bisect.insort(frequency[freq], w)
    
    res = []
    for i in range(most_freq, 0, -1):
        for w in frequency[i]:
            if not k:
                return res
            res.append(w)
            k -= 1
            
    return res

if __name__ == '__main__':
    
    reviews = [
      "I love anacell Best services; Best services provided by anacell",
      "betacellular has great services",
      "deltacellular provides much better services than betacellular",
      "cetracular is worse than anacell",
      "Betacellular is better than deltacellular.",
    ]
    
    keywords = ["anacell", "betacellular", "cetracular", "deltacellular", "eurocell"]
    
    k = 2
    
    res = get_top_K(reviews, keywords, k)
    print(res)
```

### Approach \#2

O\(N\*L+ LlogL\)

O\(L\)

```python
def freqWords(reviews, keywords, k):

	if not reviews or not keywords or not k:
		return []

	freq = collections.defaultdict(int)

	for review in reviews:
		for keyword in keywords:
			if keyword in review.lower():
				freq[keyword] += 1
	
	sorted_key_list = sorted(freq.items(), key=lambda x: (-x[1], x[0]))

	res = []
	for w, freq in sorted_key_list:
		if k:
			res.append(w)
			k -= 1
		else:
			return res
	
	return res
```

