---
layout: post
title: "Basic Sorting Review"
date: 2019-01-14
---

I'm currently reviewing the basic sorting algorithms. I'm writing this blog to serve as my notes that I can look back when needed in the future.

Much thanks to this [YouTube channel](https://www.youtube.com/user/lcc0612/) for explaining the basic sorting algorithms very well. I really recommend his [playlist](https://www.youtube.com/watch?v=MrUMzthTXOs&list=PLJse9iV6Reqg-IffRqjxebaPg0zaPxWlt) explaining those algorithms.

### Basic Sorting Algorithms


#### Selection Sort
**Worst Case**: O(n<sup>2</sup>), **Average Case**: O(n<sup>2</sup>), **Best Case**: O(n<sup>2</sup>)

- sorting like a deck of cards
- running through the list to find the smallest number
- smallest number will be put in the end

#### Bubble Sort
**Worst Case**: O(n<sup>2</sup>), **Average Case**: O(n<sup>2</sup>), **Best Case**: O(n)

- moves (bubbles) the biggest / smallest to the end

#### Insertion Sort
**Worst Case**: O(n<sup>2</sup>), **Average Case**: O(n<sup>2</sup>), **Best Case**: O(n)

- only run through the list once
- swaps the smallet / largest to the end
- the end part is guaranteed to be sorted

#### Bucket Sort

- just break down the list into buckets or sublist
- then use another sorting algorithm to sort each buckets

#### Quick Sort
**Worst Case**: O(n<sup>2</sup>), **Average Case**: O(n log n), **Best Case**: O(n log n)

- sorting by using a pivot
- recursion on the left and right side of the pivot
- do recursion until sorted

#### Merge Sort
**Worst Case**: O(n log n), **Average Case**: O(n log n), **Best Case**: O(n log n)

- divide and conquer
- then do merging

These are the notes that I managed to write while watching the videos in the YouTueb playlist above. Currently, I'm watching videos about the more advanced sorting algorithms.
