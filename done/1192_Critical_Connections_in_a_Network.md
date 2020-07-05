# Critical Connections in a Network

There are n servers numbered from 0 to n-1 connected by undirected server-to-server connections forming a network where connections[i] = [a, b] represents a connection between servers a and b. Any server can reach any other server directly or indirectly through the network.

A critical connection is a connection that, if removed, will make some server unable to reach some other server.

Return all critical connections in the network in any order.

![alt text](https://assets.leetcode.com/uploads/2019/09/03/1537_ex1_2.png)


```
Input: n = 4, connections = [[0,1],[1,2],[2,0],[1,3]]
Output: [[1,3]]
Explanation: [[3,1]] is also accepted
```

## First Solution

Detect circle

https://www.youtube.com/watch?v=aZXi1unBdJA

https://leetcode.com/problems/critical-connections-in-a-network/discuss/401340/Clean-Java-Solution-With-Explanation!!!-Great-Question!


Runtime: **172 ms**

Memory: **283.9 MB**


```java
class Solution 
{   
    private int visitedTime = 0;
    
    public List<List<Integer>> criticalConnections(int n, List<List<Integer>> connections) 
    { 
        // safe check
        if(connections == null || connections.size() == 0)
            return Collections.emptyList();
        
        //Build graph from connections
        List[] graph = buildGraph(n, connections);
        
        int[] visitedTimes = new int[n];
        boolean[] visited = new boolean[n];
        List<List<Integer>> criticalConnections = new ArrayList<>();
        
        criticalConnectionsUtils(0, -1, visitedTimes, visited, graph, criticalConnections);

        return criticalConnections;
    }
    
    private void criticalConnectionsUtils(int current, int parent, int[] visitedTimes, boolean [] visited, List[] graph,
                                          List<List<Integer>> criticalConnections)
    {
        if(visited[current])
            return;
        
        visited[current] = true;
        visitedTimes[current] = visitedTime++;
        int currentVisitedTimes = visitedTimes[current];
        
        for(int neighbour : (List<Integer>)graph[current])
        {
            if(neighbour == parent)
                continue;
            
            criticalConnectionsUtils(neighbour, current, visitedTimes, visited, graph, criticalConnections);
            visitedTimes[current] = Math.min(visitedTimes[neighbour], visitedTimes[current]);
            
            if(currentVisitedTimes < visitedTimes[neighbour])
                criticalConnections.add(Arrays.asList(current, neighbour));
        }
    }
    
    
    private List[] buildGraph(int n, List<List<Integer>> connections)
    {
        List[] graph = new ArrayList[n];
        
        for(int i=0; i<graph.length; i++)
            graph[i] = new ArrayList<Integer>();
        
        for(List<Integer> connection : connections)
        {
            graph[connection.get(0)].add(connection.get(1));
            graph[connection.get(1)].add(connection.get(0));
        }
        
        return graph;
    }
}
```

**Time Complexity: O(n)**

**Space Complexity: O(n)**