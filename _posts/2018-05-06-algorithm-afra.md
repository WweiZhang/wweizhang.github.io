---
layout: post
title: 'DFS & BFS'
date: 2018-05-06
author: wweizhang
cover: '/assets/img/girl.jpg'
tags: algorithm
---

>DFS
**以下是DFS模板**

```DFS
#include<cstdio>  
#include<cstring>  
#include<cstdlib>  
using namespace std;  
const int maxn=100;  
bool vst[maxn][maxn];  
int map[maxn][maxn];  
int dir[4][2]={0,1,0,-1,1,0,-1,0};  
bool CheckEdge(int x,int y)  
{
    if(!vst[x][y]&&...)  
        return 1;  
    else return 0;  
}  
void dfs(int x,int y)  
{  
    vst[x][y]=1;  
    if(map[x][y]==G)  
    {  
        .....  
        return;  
    }  
    for(int i=0;i<4;i++)  
    {  
        if(CheckEdge(x+dir[i][0],y+dir[i][1]))  
            dfs(x+dir[i][0],y+dir[i][1]);  
    }  
    return;  
}  
int main()  
{  
    .....  
    return 0;  
}  
```


**以下是bfs模板**

```BFS
#include<cstdio>
#include<cstring>
#include<queue>
#include<algorithm>
using namespace std;
const int maxn=100;
bool vst[maxn][maxn]; //访问
int dir[4][2]={0,1,0,-1,1,0,-1,0};
struct State //状态
{
    int x,y; //坐标位置
    int Step_Counter;   //步数
};
State a[maxn];
bool CheckState(State s) 
{
    if(!vst[s.x][s.y]&&...) 
        return 1;
    else return 0;
}
void bfs(State st)
{
    queue<State>q;
    State now,next; 
    st.Step_Counter=0;
    q.push(st);
    vst[st.x][st.y]=1;
    while(!q.empty())
    {
        now=q.front();
        if(now==G) 
        {
            ... //exit
            return;
        }
        for(int i=0;i<4;i++)
        {
            next.x=now.x+dir[i][0];
            next.y=now.y+dir[i][1];
            next.Step_Counter=now.Step_Counter+1;
            if(CheckState(next))
            {
                q.push(next);
                vst[next.x][next.y]=1;
            }
        }
        q.pop();
    }
    return;
}
int main()
{
    .....
    return 0;
}

```


###ps:昨日shell已更新