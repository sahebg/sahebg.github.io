---
layout: post
seo:
   name: Welcome to Saheb's blog - Random Access Memories.
   type: BlogPosting
title: "Travelling Salesman Problem , with C Program Example"
modified:   2017-07-08
categories: [ComputerSceince]
tags: [C, Algorithm]
sitemap:
    priority: 0.7
    changefreq: 'monthly'
    lastmod: 2017-08-03T12:49:30-05:00
author: Saheb Ghosh
description: Travelling Salesman Problem explanation and algorithmic solution. C Program example of Travelling Salesman Problem.
image: /images/Algo/algo.jpg
pic:
    feature: /Algo/algo.jpg
date: 2017-08-02T12:49:30-05:00
---
Travelling Salesman Problem is defined as "Given a list of cities and the distances between each pair of cities, what is the 
shortest possible route that visits each city exactly once and returns to the origin city?" It is an NP-hard problem.

Bellman–Held–Karp algorithm:
Compute the solutions of all subproblems starting with the smallest. Whenever computing a solution requires solutions for 
smaller problems using the above recursive equations, look up these solutions which are already computed. To compute a minimum 
distance tour, use the final equation to generate the 1st node, and repeat for the other nodes. For this problem, we cannot 
know which subproblems we need to solve, so we solve them all.

![_config.yml]({{ site.baseurl }}/images/Algo/tsp.gif)

Program in C :

{% highlight c lineos %}
#include <stdio.h>
int matrix[25][25], visited_cities[10], limit, cost = 0;
 
int tsp(int c)
{
 int count, nearest_city = 999;
 int minimum = 999, temp;
 for(count = 0; count < limit; count++)
 {
 if((matrix[c][count] != 0) && (visited_cities[count] == 0))
 {
 if(matrix[c][count] < minimum)
 {
 minimum = matrix[count][0] + matrix[c][count];
 }
 temp = matrix[c][count];
 nearest_city = count;
 }
 }
 if(minimum != 999)
 {
 cost = cost + temp;
 }
 return nearest_city;
}
 
void minimum_cost(int city)
{
 int nearest_city;
 visited_cities[city] = 1;
 printf("%d ", city + 1);
 nearest_city = tsp(city);
 if(nearest_city == 999)
 {
 nearest_city = 0;
 printf("%d", nearest_city + 1);
 cost = cost + matrix[city][nearest_city];
 return;
 }
 minimum_cost(nearest_city);
}
 
int main()
{ 
 int i, j;
 printf("Enter Total Number of Cities:\t");
 scanf("%d", &limit);
 printf("\nEnter Cost Matrix\n");
 for(i = 0; i < limit; i++)
 {
 printf("\nEnter %d Elements in Row[%d]\n", limit, i + 1);
 for(j = 0; j < limit; j++)
 {
 scanf("%d", &matrix[i][j]);
 }
 visited_cities[i] = 0;
 }
 printf("\nEntered Cost Matrix\n");
 for(i = 0; i < limit; i++)
 {
 printf("\n");
 for(j = 0; j < limit; j++)
 {
 printf("%d ", matrix[i][j]);
 }
 }
 printf("\n\nPath:\t");
 minimum_cost(0);
 printf("\n\nMinimum Cost: \t");
 printf("%d\n", cost);
 return 0;
}
{% endhighlight %}


- Output:


![_config.yml]({{ site.baseurl }}/images/Algo/image3.png)



Please comment below in case of any problem found during running the code or any other doubts.
