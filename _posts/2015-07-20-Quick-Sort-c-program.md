---
layout: post
title: "What is Quick Sort , with C Program Example"
modified:   2015-07-20
categories: [ComputerSceince]
tags: [C, Algorithm]
sitemap:
    priority: 0.7
    changefreq: 'monthly'
    lastmod: 2017-08-01T12:49:30-05:00
image:
    feature: /Algo/algo.jpg
---
Quicksort is a divide and conquer algorithm. Quicksort first divides a large array into two smaller sub-arrays: the low elements and the high elements. Quicksort can then recursively sort the sub-arrays.

The steps are:

- Pick an element, called a pivot, from the array.
- Partitioning: reorder the array so that all elements with values less than the pivot come before the pivot, while all elements with values greater than the pivot come after it (equal values can go either way). After this partitioning, the pivot is in its final position. This is called the partition operation.
- Recursively apply the above steps to the sub-array of elements with smaller values and separately to the sub-array of elements with greater values.

The base case of the recursion is arrays of size zero or one, which never need to be sorted. In asymptotic notation Quick sort can take upto O(n²) in wrost case , however on average its takes O(n log n).

The pivot selection and partitioning steps can be done in several different ways; the choice of specific implementation schemes greatly affects the algorithm's performance.
![_config.yml]({{ site.baseurl }}/images/Algo/Quick.gif)

Program in C :

{% highlight c lineos %}
#include<stdio.h>
 
void quick_sort(int[],int,int);
int partition(int[],int,int);
 
int main()
{
    int a[50],n,i;
    printf("Enter no of elements:");
    scanf("%d",&n);
    printf("\nEnter array elements:");
    
    for(i=0;i<n;i++)
        scanf("%d",&a[i]);
        
    quick_sort(a,0,n-1);
    printf("\nArray after sorting:");
    
    for(i=0;i<n;i++)
        printf("%d ",a[i]);
    
    return 0;        
}
 
void quick_sort(int a[],int l,int u)
{
    int j;
    if(l<u)
    {
        j=partition(a,l,u);
        quick_sort(a,l,j-1);
        quick_sort(a,j+1,u);
    }
}
 
int partition(int a[],int l,int u)
{
    int v,i,j,temp;
    v=a[l];
    i=l;
    j=u+1;
do
    {
        do
            i++;
            
        while(a[i]<v&&i<=u);
        
        do
            j--;
        while(v<a[j]);
        
        if(i<j)
        {
            temp=a[i];
            a[i]=a[j];
            a[j]=temp;
        }
    }while(i<j);
    
    a[l]=a[j];
    a[j]=v;
    
    return(j);
}

{% endhighlight %}


- Output:


![_config.yml]({{ site.baseurl }}/images/Algo/image2.png)



Please comment below in case of any problem found during running the code or any other doubts.
