---
layout: post
title: "What is Quick Sort , with C Program Example"
modified:   2015-07-20
categories: [ComputerSceince]
tags: [C, Algorithm]
image:
    feature: /Algo/algo.jpg
---
Merge sort is one of the most effiecient Divide and Conquer Algorithm. This runs on Big-Oh(O)(nlogn) at worst case.
Conceptually, a merge sort works as follows:


- Divide the unsorted list into n sublists, each containing 1 element (a list of 1 element is considered sorted).
- Repeatedly merge sublists to produce new sorted sublists until there is only 1 sublist remaining. This will be the sorted list.

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
