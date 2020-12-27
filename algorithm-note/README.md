# 拓扑排序

```cpp
const int maxn=550;
int L[maxn];  // 拓扑排序的顺序
vector<int>g[maxn];  // 图  
int du[maxn],n,m;   // du-> 入度  n点的个数 从1开始计数

bool topsort(){
    memset(du,0,sizeof(du));
    for(int i=1;i<=n;i++)
        for(int j=0;j<g[i].size();j++)
            du[g[i][j]]++;
    int tot=0;
    priority_queue<int,vector<int>,greater<int> >Q; // 小编号优先
    // queue<int>Q;   // 不需要小编号优先
    for(int i=1;i<=n;i++){
        if(du[i]==0)Q.push(i);  // 先将入度为0的点加入队列
    }
    while(!Q.empty()){
        int x=Q.top();Q.pop();    // 每次取入度为0的点，后继点入度减一，并看其是否减为0（为0（为0则入队），
        L[tot++]=x;
        for(int j=0;j<g[x].size();j++){
            int t=g[x][j];
            du[t]--;
            if(!du[t])Q.push(t);
        }
    }
    if(tot==n)return 1;  // 可以形成拓扑排序 
    return 0;   // 不可以形成
}

// 使用 
```



# 树状数组

```cpp
const int N = 200005;
typedef long long ll;
ll b[N];
ll shu_n;

void init(ll n){
    shu_n = n;
    memset(b,0,sizeof(b));
}
int lowbit(int x) {
    return x & (-x);
}
void update(ll x, ll k) { // x位置 加上 k
    while(x <= shu_n) {
        b[x] += k;
        x += lowbit(x);
    }
}
ll getSum(ll x) {  // 1~x位置 的和
    ll res = 0;
    while(x > 0) {
        res += b[x];
        x -= lowbit(x);
    } return res;
}
ll sum(ll l,ll r){   //位置[l,r]的和
    return getSum(r)-getSum(l-1);
}

// 使用
init(1000);  // 初始化
update(1,2);   // 1位置加上2
cout<<sum(1,3)<<endl;    // 得到 位置1~3的和
```

# 线段树

```cpp
const int maxn=1e5+5;
int sum[maxn*4],add[maxn*4];
int a[maxn];
void pushup(int root)  //根节点的和=两个子节点的和
{
    sum[root]=(sum[root*2]+sum[root*2+1]);
}
void build(int l,int r,int root)//建树，使用数组a作为初始值建树
{
    if(l==r)
  {
      sum[root] = a[l];
     return;
 }
    int mid=(l+r)/2;
    build(l,mid,root*2);
    build(mid+1,r,root*2+1);
    pushup(root);
}
void Add(int num,int val,int l,int r,int root)//修改值，位置num加上val
{
    if(l==r&&num==l)
    {
        a[num]+=val;
        sum[root]=a[num];
        return;
    }
    int mid=(l+r)/2;
    if(num<=mid)
        Add(num,val,l,mid,root*2);
    else
        Add(num,val,mid+1,r,root*2+1);
    pushup(root);
}
int Query(int be,int ed,int l,int r,int root)//查询区间[l,r]的和
{
    if(be<=l&&r<=ed)
        return sum[root];
    int mid=(l+r)/2;
    int ans=0;
    if(be<=mid)
        ans+=Query(be,ed,l,mid,root*2);
    if(mid<ed)
        ans+=Query(be,ed,mid+1,r,root*2+1);
    return ans;
}

// 使用
cin>>n;
memset(a,0,sizeof(a)); // 全零初始化
for(int i=1;i<=n;i++){cin>>a[i];}  // 有初始值的初始化
build(1,n,1);
Add(1,2,1,n,1);  // 位置1加上2
Query(2,3,1,n,1); // 查询区间[2,3]的和
    
```



# 字典树

```cpp
#include <iostream>

using namespace std;

const int N = 1e5+5;

int m;
char str[N];
int son[N][26], cnt[N], idx;    // 根节点和空节点的下标均为0,idx类似于单链表

void init(){
    memset(son,0,sizeof(son));
    memset(cnt,0,sizeof(cnt));
    idx = 0;
}

void insert(char str[]) {
    int p = 0;
    for (int i = 0; str[i]; ++i) {  // c++字符串结尾\0，可以以此判断是否结尾
        int u = str[i] - 'a';
        if (!son[p][u]) son[p][u] = ++idx; // 不存在则创建，前置++,树头结点为0,存储从1开始，保存下一个节点的位置
        p = son[p][u];      // 走到下一个点，若存在直接走下去，若不存在已经在上面创建了 
    }
    
    cnt[p] ++;
}

int query(char str[]) {
    int p = 0;
    for (int i = 0; str[i]; ++i) {
        int u = str[i] - 'a';
        if (!son[p][u]) return 0;
        p = son[p][u];
    }
    
    return cnt[p];
}

// 使用
init();
insert(str);  // 插入字符串
query(str);  // 查询字符串的数量
```

# 并查集

```cpp
int father[100005];
void init(int n)  //初始化
{
    for (int i=0;i<=n;i++) 
    {
        father[i]=i;
    }
}
int find(int x) 
{
    if(x==father[x]) return x;
    else return father[x]=find(father[x]);
}
bool same(int x, int y)  //是否联通
{
    return find(x)==find(y);
}
void merge(int x, int y)  // 加边
{
    x=find(x);
    y=find(y);
    if(x==y) return ;
    else father[y] = x;
} 

// 使用
cin>>n;
init(n);
merge(u,v);  //增加一条(u,v)的边， 即u,v联通了
same(u,v);  //查询u,v是否联调
```

# 最短路

```cpp
vector<vector<pair<int,int>>> g(N);
for(auto& v:times){
    g[v[0]].push_back({v[2],v[1]});  //add edge
}
int ans = -1;
priority_queue<pair<int,int>> que;
que.push({0,K});  // init
vector<int> dis(N,INT_MAX);
dis[K] = 0;   // start node is K
while(!que.empty()){
    auto [d,node] = que.top();
    que.pop();
    if(d>dis[node]){  
        continue;
    } 
    for(auto& [d,nodeNext]:g[node]){
        if(dis[nodeNext] > dis[node] + d){
            dis[nodeNext] = dis[node] + d;
            que.push({dis[nodeNext], nodeNext});
        }
    }
}
```



# 遍历容器

```cpp
vector<int> v;
for(int& it : v){}  //引用形式。改变it会改变v
string s;
for(char& c : s){}
vector<string> v; 
for(string s : v){}  //非引用，改变it不改变原容器
```



# 排列组合

```python
from scipy.special import comb, perm
# LeetCode 不用import了，直接用函数即可
comb(4,2)  # 6
perm(4,2)  # 12 
```

# python记忆化搜索

```python

@lru_cache(None)
def dfs()
```



# 二分

```python
while l<=r:
    mid = (l+r)//2
    if check(mid):
        ans = mid
        l = mid + 1
    else:
        r = mid -1
```



# vector建图

```cpp
// 建图和初始化
vector<vector<int> >e(500005);
for(int i=1;i<=n;i++){
            e[i].clear();
}
// 添加 边(x,y)
e[x].push_back(y);
// 遍历
for(int i=0;i<e[x].size();i++){
        ans+=dfs(e[x][i],d+1);
}
```



# gcd

```cpp
int gcd(int x, int y) {
	return !x ? y : gcd(y % x, x);
}
```

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

# string

```cpp
//初始话
string s;
string s="123";
string s("123");
//赋值
s = "123";
//比较
s[i] == '#';
s.push_back(c);
s.pop_back(c);
for(char c:s){}
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
for(int num:v){}
//排序
sort(v.begin(),v.end());
//添加
v.push_back(11);
v.emplace_back();  //参数为空时，添加一个默认的值。如int -> 0  ,vector<int> -> 空的vector。
//清空
v.clear(); //元素个数清为0
v.resize(n,v);  //重新设置大小
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

