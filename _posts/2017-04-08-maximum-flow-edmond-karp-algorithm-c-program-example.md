---
layout: post
seo:
   name: Welcome to Saheb's blog - Random Access Memories.
   type: BlogPosting
title: "Maximum flow problem - Edmonds–Karp algorithm, with C Program Example"
modified:   2017-07-08
categories: [ComputerSceince]
tags: [C, Algorithm, Graph, Augmenting Path]
sitemap:
    priority: 0.7
    changefreq: 'monthly'
    lastmod: 2017-08-10T12:49:30-05:00
author: Saheb Ghosh
description: Maximum flow Problem explanation and algorithmic solution. C Program example of Edmonds–Karp algorithm.
image: /images/Algo/algo.jpg
pic:
    feature: /Algo/algo.jpg
date: 2017-08-07T12:49:30-05:00
---
Edmonds–Karp algorithm is an implementation of the Ford–Fulkerson method for computing the maximum flow in a flow network in much more optimized approach.
Edmonds-Karp is identical to Ford-Fulkerson except for one very important trait. The search order of augmenting paths is well defined. As a refresher from the Ford-Fulkerson wiki, augmenting paths, along with residual graphs, are the two important concepts to understand when finding the max flow of a network.

## Edmonds–Karp algorithm
Augmenting paths are simply any path from the source to the sink that can currently take more flow. Over the course of the algorithm, flow is monotonically increased. So, there are times when a path from the source to the sink can take on more flow, and that is an augmenting path.
This can be found by a breadth-first search, as we let edges have unit length. The running time of O(V E2) is found by showing that each augmenting path can be found in O(E) time, that every time at least one of the E edges becomes saturated (an edge which has the maximum possible flow), that the distance from the saturated edge to the source along the augmenting path must be longer than last time it was saturated, and that the length is at most V. Another property of this algorithm is that the length of the shortest augmenting path increases monotonically.

![_config.yml]({{ site.baseurl }}/images/Algo/ek.jpg)

Notice how the length of the augmenting path found by the algorithm (in red) never decreases. The paths found are the shortest
possible. The flow found is equal to the capacity across the minimum cut in the graph separating the source and the sink. 
There is only one minimal cut in this graph, partitioning the nodes into the sets { A , B , C , E }  and { D , F , G } , with the capacity

    c ( A , D ) + c ( C , D ) + c ( E , G ) = 3 + 1 + 1 = 5.

## Program in C :

{% highlight c lineos %}
#include<cstdio>
#include<cstdio>
#include<queue>
#include<cstring>
#include<vector>
#include<iostream>
#include<conio.h>
using namespace std;
int capacities[10][10];

int flowPassed[10][10];

vector<int> graph[10];

int parentsList[10];       

int currentPathCapacity[10];  

 

int bfs(int startNode, int endNode)

{

    memset(parentsList, -1, sizeof(parentsList));

    memset(currentPathCapacity, 0, sizeof(currentPathCapacity));

 

    queue<int> q;

    q.push(startNode);

 

    parentsList[startNode] = -2;

    currentPathCapacity[startNode] = 999;

 

    while(!q.empty())

    {

        int currentNode = q.front();

        q.pop();

 

        for(int i=0; i<graph[currentNode].size(); i++)

        {

            int to = graph[currentNode][i];

            if(parentsList[to] == -1)

            {

                if(capacities[currentNode][to] - flowPassed[currentNode][to] > 0)

                {

                    parentsList[to] = currentNode;

                    currentPathCapacity[to] = min(currentPathCapacity[currentNode], 

                    capacities[currentNode][to] - flowPassed[currentNode][to]);

                    if(to == endNode)

                    {

                        return currentPathCapacity[endNode];

                    }

                    q.push(to);

                }

            }

        }

    }

    return 0;

}

 

int edmondsKarp(int startNode, int endNode)

{

    int maxFlow = 0;

      while(true)

    {

        int flow = bfs(startNode, endNode);

        if (flow == 0) 

        {

            break;

        }

        maxFlow += flow;

        int currentNode = endNode;

        while(currentNode != startNode)

        {

            int previousNode = parentsList[currentNode];

            flowPassed[previousNode][currentNode] += flow;

            flowPassed[currentNode][previousNode] -= flow;

            currentNode = previousNode;

        }

    }

    return maxFlow;

}
int main(){

    int nodesCount, edgesCount;

    cout<<"enter the number of nodes and edges\n";

    cin>>nodesCount>>edgesCount;
    int source, sink;

    cout<<"enter the source and sink\n";

    cin>>source>>sink;

    for(int edge = 0; edge < edgesCount; edge++)

    {
        cout<<"enter the start and end vertex alongwith capacity\n";

        int from, to, capacity;

        cin>>from>>to>>capacity;

 

        capacities[from][to] = capacity;

        graph[from].push_back(to);

 

        graph[to].push_back(from);

    }
    int maxFlow = edmondsKarp(source, sink);
    cout<<endl<<endl<<"Max Flow is:"<<maxFlow<<endl;
    getch();
}

{% endhighlight %}


## Output:


![_config.yml]({{ site.baseurl }}/images/Algo/image11.png)



Please comment below in case of any problem found during running the code or any other doubts.
