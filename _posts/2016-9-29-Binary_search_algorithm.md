---
layout: post
title: Recursive Binary Search Algorithm
---

This is an example of how to implement a Binary Search Algorithm in ruby.

This type of searching algorithm is pretty quick, but will only work if your data is sorted, and of a comparable data type.
We need to know whether or not the data we are looking for comes in the former or latter half of the list

## Basic Idea

1. Given an array of n elements
2. Divide the array to find the middle element
3. Compare the value you are looking for to the middle element
	a. if the middle element is the element you're looking for, Great you found it!
	b. if the element you're looking for is greater than the middle element, discard the former half of the list and go to step: 2
	c. if the element you're looking for is less than the middle element, discard the latter half of the list and go to step: 2

- repeat until you either find the element or there are elements left in your array to compare.

## Example

```ruby
array = [:B, :C, :D, :E, :G, :H, :I]
item = :B

```

- Lets look at this example array
- We want to find the symbol B

- Based on our steps above we would first divide the array in half and look at the third index which is symbol E
- We know that B < E so we can remove all elements greater than E including E

```ruby
array = [:B, :C, :D]
item = :B

```

- We are left with an array that looks like this, now we repeat the steps
- Divide the array again, we get C
- B < C so we can remove the elements greater

```ruby
array = [:B]
item = :B

```

- Here we only have on element left which is infact the symbol we are looking for.

**it is important to note that ruby will floor integer division.**

## Code

- First lets define our method:

```ruby
def binary_search(item, array, indices_chopped = 0)

end
```

- Our method will take in an array of items to search through, an item to look for, and a counter to keep track of indices so we can return the proper index the item is found at

- Next we will need a way to find the middle index of the array

```ruby
  list_end = array.length - 1
  list_start = 0
  i = (list_end - ((list_end - list_start)/2))
```

- we set our list end equal to the length of the array minus 1. This will give us the index at which our last item is at
- The start of our list will always be at index 0
- So, our last index minus our start index divided by 2 will be the middle index.

- Next we will add in the code to determine if our item is equal to, before, or after the middle indexed element

```ruby
  if item == array[i]
    return i + indices_chopped

  elsif (list_end - list_start) == 1
    return nil

  elsif item > array[i]
    array = array.drop(i)
    indices_chopped += i
    binary_search(item, array, indices_chopped)

  elsif item < array[i]
    array = array.take(i)
    indices_chopped += 0
    binary_search(item, array, indices_chopped)
  end

```

- Here we are doing three things.
1. We check if the middle element is the element we were looking for
2. If its not, we want to see if its after that element.
3. Otherwise, we want to see if its before the element.

- If we have not found the element, we need to call the method again to continue to divide the array up until we either find the element or run out of items to compare

*One thing to not is that we are incrementing an indices_chopped variable if the element is in the latter half of the list.*
**This is because arrays are zero indexed, and when we remove the former parts of the array we would shift our array indices however many indices we removed. So we need to keep track of the number we are removing to add that back in when we display our index.**



- Our finished code will look something like this.

```ruby
def binary_search(item, array, indices_chopped = 0)
  list_end = array.length - 1
  list_start = 0
  i = (list_end - ((list_end - list_start)/2))

  if item == array[i]
    return i + indices_chopped

  elsif (list_end - list_start) == 1
    return nil

  elsif item > array[i]
    array = array.drop(i)
    indices_chopped += i
    binary_search(item, array, indices_chopped)

  elsif item < array[i]
    array = array.take(i)
    indices_chopped += 0
    binary_search(item, array, indices_chopped)
  end

end


```

- And there you GO! You have implemented a binary searching algorithm.