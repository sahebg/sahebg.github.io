---
layout: post
title: "Minimum spanning tree-Prim's algorithm, with C Program Example"
modified:   2017-07-08
categories: [ComputerSceince]
tags: [C, Algorithm, Graph, Greedy Algorithm]
sitemap:
    priority: 0.7
    changefreq: 'monthly'
    lastmod: 2017-08-10T12:49:30-05:00
author: Saheb Ghosh
description: Minimum spanning tree Problem explanation and algorithmic solution. C Program example of Prim's algorithm.
image: /images/Algo/algo.jpg
pic:
    feature: /Algo/algo.jpg
date: 2017-08-09T12:49:30-05:00
---
Prim's algorithm to find the minimum cost spanning tree of for a weighted undirected graph, uses the greedy approach. Prim's algorithm, in contrast with Kruskal's algorithm, treats the nodes as a single tree and keeps on adding new nodes to the spanning tree from the given graph.
## Prim’s algorithm

- Initialize a tree with a single vertex, chosen arbitrarily from the graph.
- Grow the tree by one edge: of the edges that connect the tree to vertices not yet in the tree, find the minimum-weight edge, and transfer it to the tree.
- Repeat step 2 (until all vertices are in the tree).

![_config.yml]({{ site.baseurl }}/images/Algo/prim.gif)

The time complexity of Prim's algorithm depends on the data structures used for the graph and for ordering the edges by weight, which can be done using a priority queue. 
The average runtime= O((n+e)log n), where n=number of vertices, and e= number of edges.

## Program in C :

{% highlight c lineos %}
#include<stdio.h>
#include<stdlib.h>

#define infinity 9999
#define LIMIT 10
#define NIL -1
#define PERMANENT 1
#define TEMPORARY 0

struct edge
{
      int v;
      int u;
};

int n;	
int predecessor[LIMIT];
int adjacency_matrix[LIMIT][LIMIT];
int length[LIMIT];
int status[LIMIT];

int min_temp();
void new_graph();
void maketree(int root_var, struct edge tree[LIMIT]);

int main()
{
      int tree_weight = 0; 
      int count, root;
      struct edge tree[LIMIT];
      new_graph();
      printf("\nEnter Root Vertex:\t");
      scanf("%d", &root);
      maketree(root, tree);
      printf("Enter Edges of the Spanning Tree:\n");
      for(count = 1; count <= n - 1; count++)
      {
            printf("%d->", tree[count].u);
            printf("%d\n", tree[count].v);
            tree_weight = tree_weight + adjacency_matrix[tree[count].u][tree[count].v];
      }
      printf("Spanning Tree Weight:\t%d\n", tree_weight);
      return 0;
}

void new_graph()
{
      int count, LIMIT_edges, origin, destination, weight;
      printf("Enter Number of Vertices:\t");
      scanf("%d", &n);
      LIMIT_edges = n * (n - 1) /2;
      for(count = 1; count <= LIMIT_edges; count++)
      {
            printf("Enter Co- Ordinates of Edge No. %d(-1 -1 to quit):\n",count);
            printf("Enter Origin Vaue:\t");
            scanf("%d", &origin);
            printf("Enter Destination Vaue:\t");
            scanf("%d", &destination);
            if((origin == -1) && (destination == -1))
            {
                  break;
            }
            printf("Enter Weight of this Edge:\t");
            scanf("%d", &weight);
            if(destination < 0 || destination >= n || origin < 0 || origin >= n)
            {
                  printf("Invalid Edge\n");
                  count--;
            }
            else
            {
                  adjacency_matrix[origin][destination] = weight;
                  adjacency_matrix[destination][origin] = weight;
            }
      }
}

void maketree(int root_var, struct edge tree[LIMIT])
{	
      int current, count;
      int temp = 0;
      for(count = 0; count < n; count++)
      {
            predecessor[count] = NIL;
            length[count] = infinity;
            status[count] = TEMPORARY;
      }
      length[root_var] = 0;
      while(1)
      {
            current = min_temp();
            if(current == NIL) 
            {
                  if(temp == n - 1)
                  {
                        return;
                  }
                  else	
                  {
                        printf("No Spanning Tree is Possible because Graph is disconnected\n");
                        exit(1);
                  }
            }
            status[current] = PERMANENT;
            if(current != root_var)
            {
                  count++;
                  tree[temp].u = predecessor[current];
                  tree[temp].v = current;
            }
            for(count = 0; count < n; count++)
            {
                  if(adjacency_matrix[current][count] > 0 && status[count] == TEMPORARY)
                  {
                        if(adjacency_matrix[current][count] < length[count])
                        {
                              predecessor[count] = current;
                              length[count] = adjacency_matrix[current][count];
                        }
                  }
            }
      }
}

int min_temp()
{
      int count;
      int min = infinity;
      int x = -1;
      for(count = 0; count < n; count++)
      {
            if(status[count] == TEMPORARY && length[count] < min)
            {
                  min = length[count];
                  x = count;
            }
      }
      return x;
}
{% endhighlight %}


## Output:


![_config.yml]({{ site.baseurl }}/images/Algo/image10.png)



Please comment below in case of any problem found during running the code or any other doubts.
