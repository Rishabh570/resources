---
layout: post
title:  "Incredible Hulk- Bitmasking"
categories: c++ hackerblocks bitmasking
src: https://www.youtube.com/embed/OQ8WvxOHZo8?list=PLl4Y2XuUavmuDnf7r9Ij7MrdWtc1qvb05
img: 
---


Incredible Hulk Problem from HackerBlocks.
Try this Question Now - 
https://hack.codingblocks.com/practice-section/p/66/135



**Solution** 
```c
#include<iostream>
using namespace std;

int computeBits(int n){
    
    int ans = 0;
    while(n>0){
        ans++;
        n = n&(n-1);
    }
    return ans;
    
}


int main() {
    int t,n;
    cin>>t;
    
    while(t--){
        cin>>n;
        cout<<computeBits(n)<<endl;
        
    }
    
        
	return 0;
}


```

Complexity is `O(No of Set Bits)`