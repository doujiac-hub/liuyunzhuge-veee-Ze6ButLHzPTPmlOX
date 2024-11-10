[合集 \- OI(23\)](https://github.com)[1\.\[OI] 树上背包问题02\-16](https://github.com/HaneDaCafe/articles/18017467)[2\.\[OI] 图论02\-14](https://github.com/HaneDaCafe/articles/18015633)[3\.\[OI] 关于最小环和负权环02\-08](https://github.com/HaneDaCafe/articles/18012138)[4\.\[OI] 分层图最短路02\-08](https://github.com/HaneDaCafe/articles/18012137)[5\.\[OI] 关于Eratosthenes筛法的优化思路02\-08](https://github.com/HaneDaCafe/articles/18012139)[6\.\[OI] DP02\-17](https://github.com/HaneDaCafe/articles/18017835)[7\.\[OI] 线段树02\-19](https://github.com/HaneDaCafe/articles/18020361)[8\.\[OI] 扫描线02\-28](https://github.com/HaneDaCafe/articles/18042064)[9\.\[OI] KMP04\-28](https://github.com/HaneDaCafe/p/18160318)[10\.\[OI] 二分图05\-12](https://github.com/HaneDaCafe/p/18188064)[11\.\[OI] 平衡树06\-28](https://github.com/HaneDaCafe/p/18272852)[12\.\[OI] pb\_ds07\-09](https://github.com/HaneDaCafe/p/18291425):[豆荚加速器](https://yirou.org)[13\.\[OI] Kruskal 重构树07\-30](https://github.com/HaneDaCafe/p/18325982)[14\.\[OI] 模拟退火07\-30](https://github.com/HaneDaCafe/p/18331495)[15\.\[OI] 可持久化数据结构08\-13](https://github.com/HaneDaCafe/p/18357386)[16\.\[OI] Testlib08\-15](https://github.com/HaneDaCafe/p/18361036)[17\.\[OI] 交互 \| pipe08\-19](https://github.com/HaneDaCafe/p/18367938)[18\.\[OI] 二项式期望 DP08\-22](https://github.com/HaneDaCafe/p/18374059)[19\.\[OI] 整体二分09\-03](https://github.com/HaneDaCafe/p/18395475)[20\.\[OI] 结构体引用类型转换09\-26](https://github.com/HaneDaCafe/p/18433744)[21\.\[OI] 猫树09\-30](https://github.com/HaneDaCafe/p/18442358)[22\.\[OI] 树链剖分10\-05](https://github.com/HaneDaCafe/p/18448012)23\.Borůvka 算法11\-09收起
## 详解


Borůvka 算法的本质是一种多路 Prim 最小生成树算法，复杂度 mlog⁡n，但劣于 Kruskal 的 log


算法功能：求简单图的最小生成树


算法流程是这样的


考虑当前的图（未连边），一定由若干连通块构成，我们考虑连接连通块


可以想到，对于任意一个连通块，一定应该与尽可能优的连通块连边，并且，如果该连通块不在本操作连边，无论以后的操作如何改变其他连通块的状态，连通块总是单调不减的，花费也一定是单调不减的，因此直接在本操作连边即可


根据上述原理，可以尝试枚举所有边，然后尝试用这条边去更新端点所在连通块，对于连通块，则选择一个最优的边来更新自身


可以想到在一次操作中，总有至少一半的连通块被连接而消失，复杂度 mlog⁡n


需要注意的有以下几点


* “最优的边” 在这里必须是严格的，即你需要保证不存在 i,j∈\[1,m]，使得两条边 ei\=ej，至于为什么要这么做，一个经典的例子是重边，如果现在有 (1,2,w\=1) 和 (2,1,w\=1) 两条边，这两条边使得连通块 1 和连通块 2 都能被更新到，这样在合并的时候会连出环来，保证严格的最优性一般采用编号做第二关键字的办法
* 当然，你在无向图上跑最小生成树也会连出环，这个时候的解决办法是你在第二个循环里合并连通块之前判一下


Borůvka 需要判的东西比较多，注意不要漏掉


### P3366 【模板】最小生成树



```
#include
using namespace std;
int n,m;
int best[100001];
struct edge{
    int from,to,w;
    int id;
    bool used;
    bool operator <(const edge&A)const{
        if(w==A.w) return idreturn we={{0,0,0,0,true}};
struct dsu{
    int fa[100001];
    void clear(){
        for(int i=1;i<=n;++i){
            fa[i]=i;
        }
    }
    int find(int id){
        if(id==fa[id]) return id;
        return fa[id]=find(fa[id]);
    }
    bool samefa(int x,int y){
        int fx=find(x),fy=find(y);
        return fx==fy;
    }
    bool join(int x,int y){
        int fx=find(x),fy=find(y);
        if(fx==fy) return false;
        fa[fx]=fy;
        return true;
    }
}d;
int main(){
    ios::sync_with_stdio(false);
    cin>>n>>m;
    for(int i=1;i<=m;++i){
        int x,y,z;
        cin>>x>>y>>z;
        e.push_back({x,y,z,i,false});
    }
    d.clear();
    int ans=0,tot=0;
    while(1){
        bool flag=false;
        memset(best,0,sizeof best);
        for(edge i:e){
            if(i.used or d.samefa(i.from,i.to)) continue;
            int tmp=d.find(i.from);
            int tmp2=d.find(i.to);
            if(best[tmp]==0 or iif(best[tmp2]==0 or ifor(int i=1;i<=n;++i){
            if(d.find(i)==i){
                if(best[i]!=0 and e[best[i]].used==false){
                    e[best[i]].used=true;
                    ans+=e[best[i]].w;
                    tot++;
                    d.join(e[best[i]].from,e[best[i]].to);
                    flag=true;
                }
            }
        }
        if(!flag) break;
    }
    if(tot!=n-1) cout<<"orz";
    else cout<
```

## 使用


显然，Borůvka 在稠密图上的表现不如 Prim，在稀疏图上的表现不如 Kruskal


那要这玩意有什么用吗


是因为 Borůvka 适用于一类特殊条件


这类特殊条件形如 给你一个完全图，完全图上的边权可以通过端点的点权经过某种计算得出，求最小生成树


这样的条件充分利用了 Borůvka 只会合并 log⁡n 次的性质，这是其他两个最小生成树算法做不到的


但是这并不意味着你套模板就行了，暴力 Borůvka 仍然在 n2log 级别，需要一些有性质的图来优化算法（一般是快速找到最小边权）


### 星际联邦



> 完全图上每个点有点权 ai，定义 (u,v)(u\<v) 的边权为 av−au，求最小生成树


(大概绿\-蓝)


我们在每一轮需要找到这个点向外到另一个联通块内的最小边。注意到当 i 固定时，最小边要么是前缀 \[1,i) 的最大值取到的，要么是 (i,n] 内的后缀最小值取到的。我们只需要对每个前缀维护最大值，以及和最大值不在同一个联通块内的最大值，后缀同理，就可以快速求出该联通块向外的最小边


时间复杂度为 O(nlog⁡n)



```
#include
using namespace std;
const long long inf=0x3f3f3f3f3f3f3f3f;
int n;
int a[300005];
struct val_t{
	long long val,pos;
	inline bool operator<(const val_t&A)const{
        return valinline bool operator>(const val_t&A)const{
        return val>A.val;
    }
	inline bool operator!=(const val_t&A)const{
        return pos!=A.pos;
    }
};
inline val_t max(val_t a,val_t b){
    return a>b?a:b;
}
inline val_t min(val_t a,val_t b){
    return astruct pairval_t{
    val_t x,y;
};
const val_t pos_inf={inf,0};
const val_t neg_inf={-inf,0};
inline pairval_t max(pairval_t a,pairval_t b){
	pairval_t ans={max(a.x,b.x),neg_inf};
	if(a.x!=ans.x and a.x>ans.y) ans.y=a.x;
	if(a.y!=ans.x and a.y>ans.y) ans.y=a.y;
	if(b.x!=ans.x and b.x>ans.y) ans.y=b.x;
	if(b.y!=ans.x and b.y>ans.y) ans.y=b.y;
	return ans;
}
inline pairval_t min(pairval_t a,pairval_t b){
	pairval_t ans={min(a.x,b.x),pos_inf};
	if(a.x!=ans.x and a.xif(a.y!=ans.x and a.yif(b.x!=ans.x and b.xif(b.y!=ans.x and b.yreturn ans;
}
struct pairval_t maxn[300001],minn[300001];
struct val_t val[300001];
inline val_t askmax(int x,int pos){
    return (maxn[x].x.pos==pos)?maxn[x].y:maxn[x].x;
}
inline val_t askmin(int x,int pos){
    return (minn[x].x.pos==pos)?minn[x].y:minn[x].x;
}
struct dsu{
    int fa[300001];
    inline void clear(){
        for(int i=1;i<=n;++i){
            fa[i]=i;
        }
    }
    int operator[](int id){
        if(id==fa[id]) return id;
        return fa[id]=this->operator[](fa[id]);
    }
}d;
inline long long Roukusaka(){
	long long ans=0;
    d.clear();
	for(int i=1;i<=n;++i){
		maxn[i].x={a[i],i};
        maxn[i].y=neg_inf;
		minn[i].x={a[i],i};
        minn[i].y=pos_inf;
	}
	for(int i=2;i<=n;++i){
        maxn[i]=max(maxn[i-1],maxn[i]);
    }
	for(int i=n-1;i>=1;--i){
        minn[i]=min(minn[i+1],minn[i]);
    }
	while(1){
        bool flag=false;
		for(int i=1;i<=n;++i){
            val[i]=pos_inf;
        }
		for(int i=1;i<=n;++i){
			int now=d[i];
			val_t p=askmin(i,now);
            val_t q=askmax(i,now);
			if(q.val!=-inf and a[i]-q.val<=val[now].val){
                val[now]={a[i]-q.val,q.pos};
            }
			if(p.val!=inf and p.val-a[i]<=val[now].val){
                val[now]={p.val-a[i],p.pos};
            }
		}
		for(int i=1;i<=n;++i){
			if(d[i]==i){
                if(d[val[i].pos]==i or val[i].val==inf) continue;
                d.fa[d[val[i].pos]]=i;
                ans+=val[i].val;
                flag=true;
            }
		}
		for(int i=1;i<=n;++i){
			maxn[i].x={a[i],d[i]};
            maxn[i].y=neg_inf;
			minn[i].x={a[i],d[i]};
            minn[i].y=pos_inf;
		}
		for(int i=2;i<=n;++i){
            maxn[i]=max(maxn[i-1],maxn[i]);
        }
		for(int i=n-1;i>=1;--i){
            minn[i]=min(minn[i+1],minn[i]);
        }
        if(!flag) break;
	}
	return ans;
}
int main(){
	ios::sync_with_stdio(false);
    cin>>n;
	for(int i=1;i<=n;++i){
        cin>>a[i];
    }
	cout<<Roukusaka();
}


```

### CF888G Xor\-MST



> 完全图上每个点有点权 ai，定义 (u,v)(u≠v) 的边权为 auxorav，求最小生成树


考虑放到 trie 树上维护异或和最值


码量还行，找个时间码了


(紫)


### 图



> 给定两颗带权无向树 T1,T2，定义 disi(x,y) 表示树 Ti 上 x,y 间的距离，现有一完全二分图，左部，右部分别有 n 个点，定义左部点 i 与右部点 j 之间的边权为 maxx\=1n(dis1(i,x)\+dis2(j,x))，求完全二分图最小生成树


[https://h.hszxoj.com/d/hztg/contest/6716222721518607d314c04f/file/graph.cpp](https://github.com)


