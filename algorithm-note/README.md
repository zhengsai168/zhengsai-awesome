# STL

## 二分 lower_bound和upper_bound

```cpp
//必须有序，二分查找位置
int a[]={1,3,4,5,6};
sort(a,a+5);  
lower_bound(a,a+5,2)-a;
//返回第一个大于等于2的元素的位置
upper_bound(a,a+5,2)-a;
//返回第一个大于2的元素的位置
vector<int> a；
lower_bound(a.begin(),a.end(),2)-a.begin();
upper_bound(a.begin(),a.end(),2)-a.begin();

```



## pair

```cpp
// 定义
typedef pair<int,int> int_p;
int_p p1 = make_pair(1,2);
pair<int,int> tmp(1,2);

// 访问
p1.first=1;
p1.second=2;
// 自定义排序
bool cmp(int_p p1,int_p p2){
    if(p1.first==p2.first){
        return p1.second<p2.second;
    }
    else {
        return p1.first<p2.first;
    }
}
int_p p_arr[100];
sort(p_arr,p_arr+100,cmp);
// 不加cmp，默认先比第一个，再比第二个，升序
```

## vector

```cpp
// 定义
vector<int> v;  //空的vecotr，可以通过push_back添加
vector<int> v(100); //长度为100，默认填充0
vector<int> v(100,2); //长100，填充2
vector<vector<int> >e(100);
//访问
v[0]=1;
v.size() //个数
//排序
sort(v.begin(),v.end());
//添加
v.push_back(11);
//清空
v.clear(); //元素个数清为0
```

## stack 栈

```cpp
// 定义
stack<int>s;
s.empty() //栈为空则返回真

s.pop() //移除栈顶元素

s.push() //在栈顶增加元素

s.size() //返回栈中元素数目

s.top() //返回栈顶元素
```

## queue  队列

```cpp
queue<int>q;
q.front(); //队首
q.back();  //队尾
q.empty(); //是否为空
q.size();  //个数
q.push();  //队尾插入元素
q.pop();   //队首弹出元素
```

## deque 双端队列

``` cpp
deque<int>q;
q.front(); //队首
q.back();  //队尾
q.empty(); //是否为空
q.size();  //个数
q.push_back();  //队尾插入元素
q.push_front(); //队首插入元素
q.pop_back();   //队尾弹出元素
q.pop_front();  //队首弹出元素
```

## priority_queue 优先队列

```cpp
//小顶堆
priority_queue <int,vector<int>,greater<int> > q;
//大顶堆
priority_queue <int,vector<int>,less<int> >q;
//默认为大顶堆
priority_queue<int>q;

top //访问队头元素
empty //队列是否为空
size //返回队列内元素个数
push //插入元素到队尾 (并排序)
pop //弹出队头元素

//自定义优先级
struct tmp1 //运算符重载<
{
    int x;
    tmp1(int a) {x = a;}
    bool operator<(const tmp1& a) const
    {
        return x < a.x; //大顶堆
    }
};    

// 传pair，先比较第一个再比较第二个，默认大顶
priority_queue<pair<int, int> > a;
// 小顶
priority_queue<pair<int, int> , vector<pair<int, int> >, greater<pair<int, int> > > q;
```

## set(不重复)  multiset(可重复)

```cpp
set<int>s; 
s.insert(1);  //插入
s.erase(1);  //删除，删除没有的元素不报错。
s.count(1);  //
s.begin();  //默认升序，返回第一个
s.end();
s.size();
auto it = s.lower_bound(1);
auto it = s.find(1);
it++;
*it;
```

## map

```cpp
map<int,int>mp;
mp[0]=1;  //默认为0
cout<<mp[0]<<endl;
```



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

