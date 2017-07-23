---
layout: post
title:  "IEEE Workshop Codes"
categories: c++ DTU Workshop
image: cody.jpg
---

Codes from IEEE-DTU Workshop on Recursion, Backtracking etc.

### Kadane's Maximum Subarray Sum Problem
Time Complexity `O(N)`

```c
#include<iostream>
using namespace std;


int maxSum(int *a,int n){

    int cs = 0,ms = 0;

    for(int i=0;i<n;i++){
            cs = cs  + a[i];
            if(cs<0){
                cs = 0;
            }
            ms = max(ms,cs);
    }
    return ms;
}

int main(){
    int a[] = { 1,-2,3,4,6,-5,8,1,-4, 2} ;
    int n = sizeof(a)/sizeof(int);
    cout<<maxSum(a,n)<<endl;

return 0;
}


```


### Square Root of a number using binary search
Complexity 'O(LogN+p)`


```c
#include<iostream>
using namespace std;

float squareRoot(int n,int p){

    int s =0,e=n-1;
    float ans;

    while(s<=e){
        int mid = (s+e)/2;

        if(mid*mid==n){
            return mid;
        }
        else if(mid*mid<n){
            ans = mid;
            s = mid+1;
        }
        else{
            e = mid - 1;
        }
    }
    ///For the floating part
    float inc = 0.1;
    for(int place=1;place<=p;place++){

        while(ans*ans<=n){
            ans = ans + inc;
        }
        ans = ans - inc;
        inc = inc/10;

    }
    return ans;
}

int main(){
    int n;
    cin>>n;
    int p;
    cin>>p;

    cout<<squareRoot(n,p)<<endl;

return 0;
}


```

### Subsequences Iteratively
Time Complexity `O(N*2^N)

```c
#include<iostream>
using namespace std;

int mask(char input[],int no){

    int i=0;

    for( ;no>0;no>>=1){
        if(no&1){
            cout<<input[i];
        }
        i++;
    }
    cout<<endl;

}

int main(){

   char input[10] ="abc";
    int n = 3;

   for(int i=0; i< (1<<n); i++){
        mask(input,i);
   }

return 0;
}


```

### Set Bits in a Number
Time Complexity `O(No of Set Bits)`


```c
#include<iostream>
using namespace std;


int main(){

    int n;
    cin>>n;
    int count =0;
    while(n){
        count++;
        n = n&(n-1);
    }
    cout<<count<<endl;

    return 0;
}


```

### Rat in Maze - Backtracking
Time Complexity O(2^mn) Exponential.

```c
#include<iostream>
using namespace std;

bool solveMaze(char maze[][10],int soln[][10],int m,int n,int i,int j){
    ///Base Case
    if(i==m && j==n){
        soln[i][j] = 1;
        ///Print solution matrix
        for(int i=0;i<=m;i++){
            for(int j=0;j<=n;j++){
                cout<<soln[i][j]<<" ";
            }
            cout<<endl;
        }
        return true;
    }


    ///Rec Case
    ///Assume current cell is part of soln
    soln[i][j] = 1;

    ///Try moving right
    if(j+1<=n && maze[i][j+1]!='X'){

        bool rastaMilaKya = solveMaze(maze,soln,m,n,i,j+1);
        if(rastaMilaKya==true){
            return true;
        }

    }
    ///Try Moving Down
    if(i+1<=m && maze[i+1][j]!='X'){
        bool rastaMilaKya = solveMaze(maze,soln,m,n,i+1,j);
        if(rastaMilaKya==true){
            return true;
        }

    }
    ///Backtracking
    soln[i][j] = 0;
    return false;

}

int main(){
    char maze[10][10] = {
        "00X0",
        "0000",
        "0XX0",
        "00XX",
        "X000"
    };
    int m=4;
    int n=3;

   int soln[10][10]={0};
    solveMaze(maze,soln,m,n,0,0);

}


```

### N-Queen Problem

```c
#include<iostream>
using namespace std;

bool canPlace(int board[][100],int i,int j,int n){
    ///Check for the col
    for(int x=0;x<i;x++){
        if(board[x][j]==1){
            return false;
        }
    }
    ///Check for Top Left Diagonal
    int x=i;
    int y = j;

    while(x>=0&&y>=0){
        if(board[x][y]==1){
            return false;
        }
        x--;
        y--;
    }
    ///Check for Top Right Diagonal
    x =i;
    y = j;

    while(x>=0 && y<n){
        if(board[x][y]==1){
            return false;
        }
        x--;
        y++;
    }

    return true;
}

bool solveNQueen(int board[][100],int n,int i){
    ///Base Case
    if(i==n){
        ///Print the board
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                cout<<board[i][j]<<" ";
            }
            cout<<endl;
        }

        return true;
    }
    ///Rec Case
    ///Try to place the queeen in ith fow
    for(int j=0;j<n;j++){
        if(canPlace(board,i,j,n)){
            board[i][j] = 1;
            bool nextQueenRakhPaye = solveNQueen(board,n,i+1);

            if(nextQueenRakhPaye==true){
                return true;
            }
            ///backtracking
            board[i][j] =0;

        }

    }
    ///Backtracking
    return false;


}

int main(){
    int board[100][100] = {0};
    int n;
    cin>>n;

    solveNQueen(board,n,0);


}


```

### Graph Basics - BFS Shortest Path
Time Complexity `O(E+V)`


```c
#include<iostream>
#include<list>
#include<queue>
using namespace std;

class Graph{
public:
    int V;

    list<int> *l;

    Graph(int v){
        V = v;
        l = new list<int>[V];
    }

    void addEdge(int u,int v){
        l[u].push_back(v);
        l[v].push_back(u);
    }
    void shortestPath(int s){

        queue<int> q;
        int *dist = new int[V];

        for(int i=0;i<V;i++){
            dist[i] = INT_MAX;
        }

        dist[s] = 0;
        q.push(s);

        while(!q.empty()){
            int f = q.front();
            q.pop();
            ///Neigbours
            for(auto it=l[f].begin();it!=l[f].end();it++){
                if(dist[*it]==INT_MAX){
                    dist[*it] = dist[f] + 1;
                    q.push(*it);
                }
            }
        }

        ///Print the distances from src
        for(int i=0;i<V;i++){
            cout<<i<<" - "<<dist[i]<<endl;

        }






    }

    void printAdjList(){
        for(int i=0;i<V;i++){
            ///Traverse ith linked list
            cout<<i<<" : ";

            for(auto it=l[i].begin();it!=l[i].end();it++){
                cout<<*it<<"->";
            }
            cout<<endl;


        }

    }

};


int main(){
    Graph g(6);
    g.addEdge(0,1);
    g.addEdge(1,2);
    g.addEdge(0,2);
    g.addEdge(0,3);
    g.addEdge(3,4);
    g.addEdge(3,2);
    g.addEdge(2,5);
    g.addEdge(4,5);
    g.printAdjList();
    g.shortestPath(0);

    return 0;
}


```



