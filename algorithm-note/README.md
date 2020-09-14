# 最小生成树

## prim算法（稠密图适用–O(n^2)）

```cpp
#define inf 0x3f3f3f3f
#define N 505  //最大点数
int n,m;  //实际点数和边数 点从1开始，边从0开始
int mp[N][N];
int dis[N],vis[N];
int prim()
{
    memset(dis,inf,sizeof dis);
    int ans=0;
    memset(vis,0,sizeof vis);
    dis[1]=0;
    for(int k=0;k<n;k++)
    {
        int mint=inf,v;
        for(int i=1;i<=n;i++)
        {
            if((mint>dis[i]) && !vis[i])
            {
                mint=dis[i];v=i;
            }
        }
        if(mint==inf)
            return inf;
        vis[v]=1;
        ans+=mint;
        for(int i=1;i<=n;i++)
            dis[i]=min(dis[i],mp[v][i]);
    }
    return ans;
}
int main()
{
    cin>>n>>m;
    memset(mp,inf,sizeof mp);
    for(int i=0;i<m;i++)
    {
        int a,b,c;
        scanf("%d%d%d",&a,&b,&c);
        mp[a][b]=mp[b][a]=min(mp[a][b],c);
    }
    int ans=prim();
    if(ans==inf)
        cout<<"impossible"<<endl;
    else
        cout<<ans<<endl;
    return 0;
}
```

## kruskal算法（稀疏图适用—O(mlogm)）

```cpp
const int N =2e5+10; //最大点数
cosnt int M =2e5+10; //最大边数
#define inf 0x3f3f3f3f
int pre[N];
int n,m;   //实际点数和边数，点标号从1开始，边从0开始
struct edge
{
    int u,v,w;
}edges[M];
void init()
{
    for(int i=1;i<=n;i++)
        pre[i]=i;
}
bool cmp(edge x,edge y)
{
    return x.w<y.w;
}
int find(int x)
{
    if(x==pre[x])
        return x;
    return pre[x]=find(pre[x]);
}
int kruskal()
{
    int ans=0,sum=0;
    sort(edges,edges+m,cmp);
    for(int i=0;i<m;i++)
    {
        int u=edges[i].u,v=edges[i].v,w=edges[i].w;
        int fu=find(u),fv=find(v);
        if(fu!=fv)
        {
            pre[fu]=fv;ans+=w;
            sum++;
        }
    }
    if(sum!=n-1)
        return -1;
    return ans;
}
int main()
{
    cin>>n>>m;
    init();
    for(int i=0;i<m;i++)
    {
        int u,v,w;
        scanf("%d%d%d",&u,&v,&w);
        edges[i]={u,v,w};
    }
    int ans=kruskal();
    if(ans==-1)
        cout<<"impossible"<<endl;
    else
        cout<<ans<<endl;
    return 0;
}
```

