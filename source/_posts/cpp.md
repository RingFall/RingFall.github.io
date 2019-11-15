---
title: c艹
date: 2017-7-22 15:34:47
categories: Blog
thumbnail:  "https://s1.ax1x.com/2017/12/31/pSsfHS.png"
---
##### 大三上算法作业吐血采坑更新

- 后面要判断的值初始化时一定得赋值
- 明明是满足某条件是才加不要无脑加
- ~~窝。。。题意mmp~~ 一定要理解题意啊微笑
- 无脑递归t了。。。那就用假装dp的记忆化数组√
- 另一题跟着思路又数组了。。。好久不见的Segmentation fault超限，最后暴力过？这样例是有多弱？？？

第一次作业summary：好久没OJ手感略失，对这种猜题意感到极度自闭x

- 取余会出现负值，可能是溢出了，用ll
- dp公式好难推啊哭

第二次作业summary：算法算法算法

第一次实验课：

- 学习到了一个神奇的方法三分，就是在类似二次函数那样有顶点的时候通过三个点依靠单调性判断顶点所在位置
- 嗯？之前遇到的溢出居然没在这记录过？又得重新查。。。用malloc动态建立，记得释放

第三次作业QAQ

- 结构体和类使用sort函数时重写cmp函数就好，也可重载符号什么的，sort时记得end是数组个数乘struct里的参数数目
- 一眼看去觉得搜索会超时就往dp想x
- strcmp和strcpy挺好用的
- 发现一个新函数：lower_bound( begin,end,num)：从数组的begin位置到end-1位置二分查找第一个大于或等于num的数字，找到返回该数字的地址，不存在则返回end。通过返回的地址减去起始地址begin,得到找到数字在数组中的下标

summary：越来越难惹嘤嘤嘤，已经到了百度之后都看不懂的程度了吗QVQ

后面的都是直接百度。。。然后占分最高的实验作业窝不就是做得枣了点嘛，结果bfm老师就叫窝讲。。哭惹，最搞笑的是窝第一时间找圆脸抱怨，她嗦彼此彼此哈哈哈哈哈嗝，她也被叫去讲实验惹23333

然后就好好学习了一下这几题。。。然后就觉得好简单。。。讲道理。圆脸么嗦她讲的简单，于是我们得出我们只是没好好学习的结论2333

最后要机考。。好慌，来这整理一波算法。

##### 进制转换（递归

```
void eight(int x)
{
    if(x<8)
        cout<<x;
    else
    {
        eight(x/8);
        cout<<x%8;
    }
}
```

##### 全排列（递归

```
void line(char list[],int s,int e)
{
    if(s==e)
    {
        if(a!=0)
            cout<<' ';
        printf("%s",list);
        a++;
    }
    else
    {
        for(int i=s;i<=e;i++)
        {
            swap1(list,s,i);
            line(list,s+1,e);
            swap2(list,s,i);
        }
    }
}
```

##### 快速幂（递归

```
long long qaq(long long x,long long n)
{
    long long res = 1;
    if(n == 0) 
    	return 1;
    res = qaq(x * x % mod, n/2);
    if(n % 2)
        res = res * x % mod;
    return res;
}
```

##### 第k小（直接sort惹

动态建立数组：

`str=(int *)malloc (n*sizeof(int));`

##### 沙子的质量（dp

`define INF 1<<29` 

```
for(int i=1;i<=n;i++)
         {
               cin>>str[i];
               s[i]=s[i-1]+str[i];
        }
        for(int len=2;len<=n;len++)
        {
            for(int i=1;i<=n-len+1;i++)
            {
                int end=i+len-1;
                int mi=INF;
                for(int k=i;k<end;k++)
                {
                   mi=min(mi,dp[i][k]+dp[k+1][end]+s[end]-s[i-1]);
                }
                dp[i][end]=mi;
            }
        }
        cout<<dp[1][n]<<endl;
```

##### 最长公共子序列

```
for(int x=0;x<=len1;x++)
        {
            for(int y=0;y<=len2;y++)
            {
                if (x == 0 || y == 0)
                    ll[x][y]=0;
                else if (str1[x-1] == str2[y-1])
                    ll[x][y]=ll[x-1][y-1] + 1;
                else
                    ll[x][y]=max(ll[x-1][y],ll[x][y-1]);
            }
        }
        cout<<ll[len1][len2]<<endl;
```

##### 跳台阶（dp

```
long long int f(int a)
{
    if(a<1000) return s[a];
    else return (f(a-1)+f(a-2))%1000000007;
}
...
while(cin>>n)
{
    if(n<1000)
    {
        for(int i=2;i<=n;i++)
        {
            s[i]=(s[i-1]+s[i-2])%1000000007;
        }
        cout<<s[n]<<endl;
    }
    else
        cout<<f(n)<<endl;
}
```

##### 奶牛的聚会（三分

```
四舍五入
int round_double(double number)
{
    return (number > 0.0) ? (number + 0.5) : (number - 0.5); 
}
```

```
double getRes(double ans) {
    double res = 0;
    for(int i=1;i<=n;i++) {
        double dis = fabs(x[i]-ans);
        res += dis * dis * dis * w[i];
    }
    return res;
}
...
for(int i=1;i<=n;i++) {
	scanf("%lf %lf", &x[i], &w[i]);
	l = min(l, x[i]);
	r = max(r, x[i]);
}
for(int i=1;i<=500;i++) {
    double t1 = l + (r-l)/3;
    double t2 = l + 2*(r-l)/3;
    double res1 = getRes(t1);
    double res2 = getRes(t2);
    if(res1 < res2)
    	r = t2;
    else if(res1 > res2)
    	l = t1;
    else
    	r = t2;
}
```

##### 矩阵连乘（dp

```
for(int r=2;r<=len;r++)
{
	for(int i=1;i<=len-r+1;i++)
	{
		int q=i+r-1;
		mm[i][q]=mm[i+1][q]+p[i-1]*p[i]*p[q];
		for(int k=i+1;k<q;k++)
		{
			int t=mm[i][k]+mm[k+1][q]+p[i-1]*p[k]*p[q];
			if(t<mm[i][q])
				mm[i][q]=t;
		}
	}
}
```

##### 01背包（dp

```
memset(dp,0,sizeof(dp));
    int n,W;
    cin>>W>>n;
    for(int i=0;i<n;i++) 
        cin>>w[i]>>v[i];
    for(int i=0;i<n;i++)
        for(int j=W;j>=w[i];j--)
            dp[j]=max(dp[j],dp[j-w[i]]+v[i]);
    cout<<dp[W]<<endl;
```

##### 最大子段和

```
int maxs(int A[],int n)
{
         int maxSum=0,result=0;
         for(int i=0;i<n;i++)
         {
                  maxSum=max(maxSum+A[i],0);
                  if(maxSum>result)
                          result=maxSum;
         }
         return result;
}
```

##### 最长递减子序列（dp

```
void print(int x) //递归输出round数组里记录的前一个数
{
    if(x) 
    {
        print(roud[x]);
        if(x!=mmax)     
            cout<<ai[x]<<" "; 
        else
            cout<<ai[x]<<endl;
    }
} 
...
for(int i=1;i<=n;i++)
    {   
        dp[i]=1;
        roud[i]=0;  
        for(int j=1;j<i;j++)
        {
             if(ai[i]<ai[j]&&dp[i]<dp[j]+1)
             {
                  dp[i]=dp[j]+1;
                  roud[i]=j;
             }
        }
        if(dp[i]>dp[mmax])
        {
            mmax=i;
        }                   
    }
    print(mmax);
```

##### 矩形滑雪场（dp

```
struct node
{
    int h,x,y;
}a[40040];
bool compare(node a,node b)
{
    return a.h<b.h;
}
bool check(node a,node b)
{
    if(((a.x==b.x&&abs(a.y-b.y)==1)||(a.y==b.y&&abs(a.x-b.x)==1))&&b.h>a.h)
        return true;
    return false;
}
...
sort(a,a+m*n,compare);
int mmax=1;
for(int i=0;i<num;i++)
{
    dp[i]=1;
    for(int j=0;j<i;j++)
    {
        if(check(a[j],a[i]))
        {
            dp[i]=max(dp[i],dp[j]+1);
        }
    }
    if(dp[i]>mmax) 
        mmax=dp[i];
}
```

##### Homework（贪心

```
class juan
{
public:
    int a;
    int b;
    double c;
};
bool operator<(const juan& s1, const juan& s2)
{
    return s1.c > s2.c; 
}
int main()
{
    int m,n;
    while(cin>>m>>n&&m&&n)
    {
        juan j[10010];
        for(int i=0;i<m;i++)
        {
            cin>>j[i].a>>j[i].b;
            j[i].c=j[i].b*1.0/j[i].a;
        }
        sort(j,j+m*3);
        double re=0;
        for(int i=0;i<m;i++)
        {
           if(n>=j[i].a)
            {
                re+=j[i].b;
                n-=j[i].a;
            }
            else if(n>=j[i].c)
            {
                re+=n*j[i].c;
                n=0;
            }
            else
                break;
        }
        printf("%.2lf\n",re);
    }
    return 0;
}
```

##### 区间包含（贪心

```
struct node{
    int s,e;    
};
bool cmp(node a,node b){
    return a.e < b.e;
}
...
for(int i = 0;i < n;i++){
	scanf("%d %d",&a[i].s,&a[i].e);
}
sort(a,a+n,cmp);  
for(int j=0;j <m;j++)
{
	int num = 0;
	scanf("%d %d",&b[j].s,&b[j].e);
	for(int k = 0;k < n; k++)
	{
		if(a[k].s >= b[j].s)
		{
			if(a[k].e <=  b[j].e)
			{
				num++;
				b[j].s = a[k].e; 
			}
			else break;
		}
	}
	printf("%d\n",num);
}
```

##### 汽车费用（dp

```
for(int i=1;i<=10;i++){
    for(int j=1;j<=n;j++){
        if(j>=i) dp[j]=min(dp[j],dp[j-i]+c[i]);
    }
}
```

##### 法师康的工人

```
struct worker{
    int start,end;
}w[5010];
bool cmp(worker a ,worker b){
    if(a.start == b.start){
        return a.end<b.end;
    }else
        return a.start<b.start;
}
int main(){
    int n;
    cin>>n;
    for(int i=0;i<n;i++){
        cin>>w[i].start>>w[i].end;
    }
    sort(w,w+n,cmp);
    int re = w[0].end - w[0].start,gap = 0,t1 = w[0].start,t2 = w[0].end;
    for(int i = 0;i<n;i++){
        if(w[i].start > t2)
        {
            gap = max(gap,w[i].start-t2);
            t1 = w[i].start;
        }
        t2 = max(t2,w[i].end); 
        re  = max(re,t2-t1);
    }
    cout<<re<<" "<<gap<<endl;  
    return 0;
}
```

##### 凯撒加密

```
a%=26;
if(str[i]>='a'&&str[i]<='z')
{
	str[i] = (int(str[i]-'a')+(26-a))%26+'a';
}
else if(str[i]>='A'&&str[i]<='Z')
{
	str[i] = (int(str[i]-'A')+(26-a))%26+'A';
}
```

##### Vigenère 

```
while(nowc<strlen(C)){
    if(C[nowc]<'a')
        M[nowc]=((C[nowc]-'A'+26)-(K[nowk]-'a'))%26+'A';
    else
        M[nowc]=((C[nowc]-'a'+26)-(K[nowk]-'a'))%26+'a';
    nowc++;
    nowk++;
    if(nowk==strlen(K)) 
        nowk=0;
}
```

##### 简单的密码（找规律

```
void init(){
    d[3][0] = d[3][2] = d[3][3] = 1;//d[1][3] = d[2][3] = 0;
    d[3][1] = 2;
    d[3][0] = 4;
    for(int i = 4; i <= 30; i++){
        d[i][0] = d[i-1][0] + d[i-1][1] + d[i-1][2];
        d[i][1] = d[i-1][0];
        d[i][2] = d[i-1][1];
        d[i][3] = d[i-1][3]*2 + d[i-1][2];
    }
}
```

##### 素数环（回溯

```
void AA(int cur){
    if(cur==n&&isp(a[0]+a[n-1]))
    {
        re++;
        return ;
    }
    else
        for (int i=2;i<= n;i++)
        {
            if(!in[i]&&isp(i+a[cur-1]))
            {
                a[cur]=i;
                in[i]=true;
                AA(cur+1);
                in[i]=false;
            }
        }
}
```

##### 字典序最小

```
    while(cin>>t)
    {
        char s[2010];
        cin>>s;
        int begin=0,end=strlen(s)-1;
        while(begin<=end)
        {
            bool left=true;
            for(int i=begin;i<=end;i++)
            {
                if(s[i]>s[begin+end-i])
                {
                    left=false;
                    break;
                }
                else if(s[i]<s[begin+end-i])
                {
                    left=true;
                    break;
                }
            }
            if(left)
            cout<<s[begin++];
            else
            cout<<s[end--];
        }
        cout<<endl;
    }
```

##### 渊子赛马

```
        sort(a,a+n);
        sort(b,b+n);
          
        for(i=0,j=0,k=n-1,m=n-1,win=0,lose=0;i<n;i++)
        {
            if(a[i]>b[j])
            {
                win++;
                j++;
            }
            else if(a[i]<b[j])
            {
                lose++;
                m--;
            }
            else
            {
                if(a[k]>b[m])
                {
                    win++;
                    k--;
                    m--;
                }
                else if(a[k]<b[m])
                {
                    lose++;
                    k--;
                    m--;
                }
                else
                {
                    lose++;
                    m--;
                }
            }
              
            if(win>n/2)
            {
                cout<<"YES"<<endl;
                break;
            }
        }      
        if(win<=n/2)
            cout<<"NO\n";
```

##### 八皇后（回溯

```
bool backtrack(int r, int c) {  
    for (int i = 0; i < r; i++) {  
        if (x[i] == c) return false;  
        if (abs(r - i) == abs(c - x[i])) return false;  
    }  
    return true;  
}  
   
void queen(int k) {
    if (k == n) 
    { 
        ans = max(ans, tmp); 
        return; 
    }
   
    for (int i = 0; i < n; i++) {  
        if (backtrack(k, i)) { 
            x[k] = i;  
            tmp += chess[k][i];  
            queen(k + 1);  
            x[k] = -1;
            tmp -= chess[k][i];  
        }  
    }  
}  
```

##### 组合运算式

```
int calc() {
    int len = 0;
    for (int i = 0; i < j; i++) {
        if (' ' != gap[i]) cpy[len++] = gap[i];
    }
    cpy[len] = '\0';
  
    int ans = 0, tmp = 1, i = 0;
    while (i < len) {
        ans += tmp*atoi(cpy + i);
        while (isdigit(cpy[i])) i++;
        tmp = cpy[i] == '+' ? 1 : -1;
        i++;
    }
    return ans;
}
  
void solve(int k) {
    if (k == j) {
        if (0 == calc()) 
        {
            for(int i=0;i<n*2-1;i++)
                cout<<gap[i];
            cout<<endl;
        }
        return;
    }
    gap[k] = ' ';
    solve(k + 2);
    gap[k] = '+';
    solve(k + 2);
    gap[k] = '-';
    solve(k + 2);
}
  
int main() {
    scanf("%d", &n);
        memset(gap, 0, sizeof(gap));
        memset(cpy, 0, sizeof(cpy));
        for (i = 1, j = 1; i <= n; i++, j += 2) {
            gap[j - 1] = i + 48;
            if (j == 2 * n - 1) 
                break;
        }
        solve(1);
     
    return 0;
}
```

##### 试管

```
int A, B, C;
int dp[30][30][30];
vector<int> ans;
  
void solve(int a, int b, int c) {
    if (dp[a][b][c]) return;
    dp[a][b][c] = 1;
    if (0 == a) ans.push_back(c);
  
    if (a <= B - b) solve(0, a + b, c);
    else solve(a + b - B, B, c);
  
    if (b <= A - a) solve(a + b, 0, c);
    else solve(A, a + b - A, c);
  
    if (a <= C - c) solve(0, b, a + c);
    else solve(a + c - C, b, C);
  
    if (c <= A - a) solve(a + c, b, 0);
    else solve(A, b, a + c - A);
  
    if (b <= C - c) solve(a, 0, b + c);
    else solve(a, b + c - C, C);
  
    if (c <= B - b) solve(a, b + c, 0);
    else solve(a, B, b + c - B);
}
  
int main() {
    while (scanf("%d%d%d", &A, &B, &C) == 3) {
        memset(dp, 0, sizeof(dp));
        ans.clear();
        solve(0, 0, C);
        sort(ans.begin(), ans.end());
        int len = ans.size();
        for (int i = 0; i < len; i++)
            printf("%d%c", ans[i], i + 1 == len ? '\n' : ' ');
    }
    return 0;
}
```

##### 哈夫曼编码

```
const int N = 2000;
char s[N];
int vis[233], ans;
priority_queue <int, vector<int>, greater<int> > q;
 
int main()
{
    int t, n;
    scanf("%d", &t);
    while(t--){
        getchar();
        scanf("%s", s);
        while(!q.empty()) q.pop(); 
        ans = n = 0; 
        memset(vis,0,sizeof vis);
        for(int i = 0; s[i]; i++) vis[s[i]]++;
        for(int i = 0; s[i]; i++){
            if(vis[s[i]]){
                q.push(vis[s[i]]);
                n++;
            }
            vis[s[i]] = 0;
        }
        int x, y;
        if(n == 1) ans = q.top();
        while(--n){
            x = q.top(); q.pop();
            y = q.top(); q.pop();
            ans += x+y;
            q.push(x+y);
        }
        printf("%d\n", ans);
    }
    return 0;
} 
```

###### 2n皇后问题

```
int blackQueen(int pos);
int whiteQueen(int pos);
  
int blackQueen(int pos)
{
    int i,j;
    for(i=0;i<pos-1;i++)
    {
        if(blackFlag[i]==blackFlag[pos-1] || fabs(double(pos-1-i))==fabs(double(blackFlag[i]-blackFlag[pos-1])))
            return 0;
    }
    if(pos==n)
    {
        counter++;
        return 0;
    }
    for(j=0;j<n;j++)
    {
        if(j!=whiteFlag[pos] && chessBoard[pos][j]==1)
        {
            blackFlag[pos]=j;
            blackQueen(pos+1);
        }
    }
}
  
int whiteQueen(int pos)
{
    int i,j;
    for(i=0;i<pos-1;i++)
    {
        if(whiteFlag[i]==whiteFlag[pos-1] || fabs(double(pos-1-i))==fabs(double(whiteFlag[i]-whiteFlag[pos-1])))
            return 0;
    }
    if(pos==n)
    {
        blackQueen(0);
        return 0;
    }
    for(j=0;j<n;j++)
    {
        if(chessBoard[pos][j]==1)
        {
            whiteFlag[pos]=j;
            whiteQueen(pos+1);
        }
    }
}
  
  
int main()
{
    int i,j;
    cin>>n;
    for(i=0;i<n;i++)
        for(j=0;j<n;j++)
            cin>>chessBoard[i][j];
    whiteQueen(0);
    cout<<counter<<endl;
    return 0;
} 
```

##### 图的m着色

```
const int maxn = 2e3 + 5;
int n,k,m,sum=0;
int map[maxn][maxn];
int color[maxn];
void backtrack(int t)
{
        if(t > n)
        {
                sum++;
                return;
        }
        for(int i = 1; i <= m; i++)    
        {
                int flag = 1;
                for(int j = 1; j <= n; j++)     
                {
                        if(map[t][j] && color[j] == i)  
                        {
                                flag = 0;
                                break;
                        }
                }
                if(flag)
                {
                        color[t] = i;   
                        backtrack(t+1);       
                        color[t] = 0;   
                }
        }
}
int main()
{
        cin>>n>>k>>m;
        for(int i = 0; i < k; i++)
        {
                int tmp1,tmp2;
                scanf("%d %d",&tmp1,&tmp2);
                map[tmp1][tmp2] = 1;
                map[tmp2][tmp1] = 1;
        }
        backtrack(1);
        cout<<sum<<endl;
        return 0;
}
```

##### 部分和

```
int n,k,a[21],sum,flag;
void dfs(int pos)
{
    if(flag==1)
        return ;
    if(sum==k)
    {
        printf("Yes\n");
        flag=1;
        return ;
    }
    for(int i=pos;i<n;i++)
    {
        sum+=a[i];
        dfs(i+1);
        sum-=a[i];
    }
}
int main()
{
    while(~scanf("%d",&n))
    {
        memset(a,0,sizeof(a));
        for(int i=0;i<n;i++)
            scanf("%d",&a[i]);
        scanf("%d",&k);
        flag=0;
        sum=0;
        dfs(0);
        if(flag==0)
            printf("No\n");
    }
    return 0;
}
```

然后复习下stl神器吧。。

- string
- vector
- set
- list
- map

嗯。

***

以下是大一写的。。太丑没脸看x

正如老师嗦的，C艹是一个偏底层的，作为计算机专业必须掌握的语言恩。（那你咋就教些基础的不得了的呐x
讲道理觉得周围的同学学完了这门课依旧一脸萌比，而且都是偏理论，完全没有寄几动手的编程能力。（说着说着感觉在嗦自己（扶额
毕竟湿乎乎嗦要锻炼编程能力来着
总而言之这里是一些刷过哒（最水的）OJ和做过哒算法题大集合~~~（其实只是为了备份一下，，不然寄几电脑上的这些cpp舍不得删2333
唔有些在学校电脑上做的就没存啦，莫名感觉质量高的都是在各种比赛的时候做的（误

## HDU 入门最合适哒（三周）
### 1062 Text Reverse
```
#include<iostream>
using namespace std;
int main()
{
	int i;
	while(cin>>i)
	{
		getchar();
		while(i--)
		{
			int b;
			char s[1000];
			gets(s);
			int a=0;
			for(;s[a]!='\0';a++)
			{
				if(s[a]==' ')
				{
					b=a-1;
					for(;s[b]!=' '&&b>=0;b--)
					{
						cout<<s[b];
						if(b==0)
							break;
					}
					cout<<' ';
				}
			}
			if(s[a]=='\0')
				{
					b=a-1;
					for(;s[b]!=' '&&b>=0;b--)
					{
						cout<<s[b];
						if(b==0)
							break;
		}
			}
			cout<<endl;
	}
	}
	return 0;
}
```
### 1064 Financial Management
```
include<iostream>
using namespace std;
int main()
{
	float a,sum,b;
	sum=0;
	for(int i=0;i<12;i++)
	{
		cin>>a;
		sum+=a;
	}
	b=sum/12.0;
	printf("$%.2f\n",b);
	return 0;
}
```
### 1170 Balloon Comes!
```
#include<iostream>
using namespace std;
int main()
{
	int i;
	cin>>i;
	while(i--)
	{
		char c;
		int a,b;
		cin>>c>>a>>b;
		if(c=='+')
			cout<<a+b<<endl;
		else if(c=='-')
			cout<<a-b<<endl;
		else if(c=='*')
			cout<<a*b<<endl;
		else
		{
			if(a%b==0)
				cout<<a/b<<endl;
			else
			{
			double n;
		    n=a/(b*1.0);
		    printf("%.2f",n);
			cout<<endl;
			}
		}
     }
	return 0;
}
```
### 1197 Specialized Four-Digit Numbers
```
#include<iostream>
using namespace std;
int jinzhi(int,int);
int main()
{
	int l,x,z,s;
	for(s=1000;s<10000;s++)
	{
		l=jinzhi(10,s);
		x=jinzhi(12,s);
		z=jinzhi(16,s);
		if(l==x&&l==z)
			cout<<s<<endl;
	}
}
int jinzhi(int a,int b)
{
	int sum;
	if(b/a==0)
		sum=b;
	else
	{
		int x=b%a;
		sum=jinzhi(a,b/a);
		sum+=x;
	}
	return sum;
}
```
### 1720 A+B Coming
```
#include<iostream>
#include<cstring>
using namespace std;
int Fun(char[]);
int main()
{
	
	int a,b;
   char str1[100],str2[100];
   while(cin>>str1>>str2)
   {
	   a=Fun(str1);
	   b=Fun(str2);
	   cout<<a+b<<endl;
   }
   return 0;
}
int Fun(char str[])
{
	
	int m[100];
	m[0]=1;
	for(int z=1;z<100;z++)
	{
		m[z]=16*m[z-1];
	}
	int s,n;
	 s=0;
	 n=strlen(str);
   for(int x=0;str[x]!='\0';x++)
   {
       if(str[x]=='A'||str[x]=='a')
	   {
	      s+=10*m[n-1];
	   }
	   else if(str[x]=='B'||str[x]=='b')
	   {
	      s+=11*m[n-1];
	   }
	    else if(str[x]=='C'||str[x]=='c')
	   {
	      s+=12*m[n-1];
	   }
	    else if(str[x]=='D'||str[x]=='d')
	   {
	      s+=13*m[n-1];
	   }
	    else if(str[x]=='E'||str[x]=='e')
	   {
	      s+=14*m[n-1];
	   }
	    else if(str[x]=='F'||str[x]=='f')
	   {
	      s+=15*m[n-1];
	   }
		else
		{
			s+=((str[x]-'0')*m[n-1]);
		}
		n--;
   }
   return s;
}

```
### 2014 青年歌手大奖赛_评委会打分
```
#include<iostream>
using namespace std;
int main()
{
	int m,n;
	while(cin>>n>>m)
	{
		if(n==-1&&m==-1)
			break;
		else
		{
			for(int t=m%n;t;t=m%n)
			{
				m = n;
				n = t;
		    }
			if( n > 1)
		        { 
		          cout<<"POOR Haha"<<endl;
		        }
		    else
		    {         
			      cout<<"YES"<<endl;
		    }	
	}
	}
	return 0;
}
```
### 2629 Identity Card
```
#include<iostream>
using namespace std;
int main()
{
	int i;
	cin>>i;
	while(i--)
	{
		char s[19];
		int x=18;
		int a=0;
		while(x--)
		{
			cin>>s[a];
			a++;
		}
		s[19]='\0';
		cout<<"He/She is from ";
		if(s[0]=='3'&&s[1]=='3')
			cout<<"Zhejiang";
		else if(s[0]=='1'&&s[1]=='1')
			cout<<"Beijing";
		else if(s[0]=='7'&&s[1]=='1')
			cout<<"Taiwan";
		else if(s[0]=='8'&&s[1]=='1')
			cout<<"Hong Kong";
		else if(s[0]=='8'&&s[1]=='2')
			cout<<"Macao";
		else if(s[0]=='5'&&s[1]=='4')
			cout<<"Tibet";
		else if(s[0]=='2'&&s[1]=='1')
			cout<<"Liaoning";
		else if(s[0]=='3'&&s[1]=='1')
			cout<<"Shanghai";
		cout<<",and his/her birthday is on ";
		cout<<s[10]<<s[11];
		cout<<",";
		cout<<s[12]<<s[13];
		cout<<",";
		cout<<s[6]<<s[7]<<s[8]<<s[9];
		cout<<" based on the table."<<endl;
	}
	return 0;
}
```
### 2734 Quicksum
```
#include<iostream>
using namespace std;
int main()
{
	char s[1000];
	while(gets(s))
	{
		if(s[0]=='#')
			break;
		else
		{
			int sum=0;
			for(int i=0;s[i]!='\0';i++)
			{
				int a=i+1;
				if(s[i]==' ')
					sum+=(a*0);
				else
				{
					sum+=((s[i]-64)*a);
				}
			}
			cout<<sum<<endl;
		}
	}
	return 0;
}
```
### 2012 素数判定
```
#include<iostream>
using namespace std;
bool sushu(int);
int main()
{
	int n,x,y;
	while(cin>>x>>y)
	{
		if(x==0&&y==0)
			break;
		else
		{
			if(x>=y)
			{
               for(n=y;n<=x;n++)
			   {
			       int N=n*n+n+41;
				   if(sushu(N)==0)
					   break;
			   }
			   if(n==x+1)
				   cout<<"OK"<<endl;
			   else
				   cout<<"Sorry"<<endl;
			}
			else
			{
				for(n=x;n<=y;n++)
			   {
			       int N=n*n+n+41;
				   if(sushu(N)==0)
					   break;
			   }
			   if(n==y+1)
				   cout<<"OK"<<endl;
			    else
				   cout<<"Sorry"<<endl;
			}
		}
	}
	return 0;
}
bool sushu(int N)
{
	bool s;
	if(N==1||N%2==0)
		s=0;
	else
	{
		int x=3;
		for(;x*x<=N;x++)
		{
			if(N%x==0)
				break;
		}
		if(x*x>N)
			s=1;
		else
			s=0;
	}
	return s;
}
```
### 2013
```
#include<iostream>
using namespace std;
int main()
{
	int n,k;
	while(cin>>n)
	{
		k=1;
		n-=1;
		while(n--)
			k=((k+1)*2);
	    cout<<k<<endl;
	}
	return 0;
}
```
### 2014
```
#include<iostream>
using namespace std;
int main()
{
	int i;
	int str[200];
	while(cin>>i)
	{
		int I=i,ii=i,iii=i,iiii=i,min,max;
		for(int x=0;I!=0;I--)
		{
			cin>>str[x];
			x++;
		}
		min=str[0];
		for(int a=1;(i-1)!=0;i--)
		{
			if(min>str[a])
			{
				min=str[a];
				str[a]=str[0];
				str[0]=min;
				
			}
			a++;
		}
		max=str[iiii-1];
		for(int b=0;(ii-1)!=0;ii--)
		{
			if(max<str[b])
			{
				max=str[b];
				str[b]=str[iiii-1];
				str[iiii-1]=max;
				
			}
			b++;
		}
		str[0]=0;
		str[iiii-1]=0;
		int sum=0;
		for(int l=0;iii!=0;iii--)
		{
			sum+=str[l];
			l++;
		}
		float z=((sum*1.00)/(iiii-2));
		printf("%.2f",z);
		cout<<endl;
	}
	return 0;
}
```
### 2015
```
#include<iostream>
using namespace std;
int main()
{
	int n,m;
	while(cin>>n>>m)
	{
		int nn=n;
		int N[200];
		int b=0;
		for(int a=0;nn!=0;nn--)
		{
			b+=2;
			N[a]=b;
			a++;
		}
		int l=n/m;
		int L=l-1,LL=l;
		int x=0;
		int sj[200];
		int z=0;
		while(l--)
		{
			int M=m;
			int sum=0;
			for(;M!=0;M--)
			{
				sum+=N[x];
				x++;
			}
			sj[z]=(sum/m);
			z++;
		}
		int s=n%m;
		if(s!=0)
		{
		int S=s;
		int ave=0;
		for(;S!=0;S--)
		{
			ave+=N[x];
			x++;
		}
		sj[z]=(ave/s);
		int v=0;
		for(;LL!=0;LL--)
		{
			cout<<sj[v]<<' ';
			v++;
		}
		cout<<sj[v];
		}
		else
		{
			int v=0;
			for(;L!=0;L--)
		{
			cout<<sj[v]<<' ';
			v++;
		}
			cout<<sj[v];
		}
		cout<<endl;
	}
	return 0;
}
```
### 2016
```
#include<iostream>
using namespace std;
int main()
{
	int n;
	while(cin>>n)
	{
		if(n==0)
			break;
		else
		{
			int N=n,nn=n,nnn=n;
			int sl[200];
			for(int x=0;N!=0;N--)
			{
				cin>>sl[x];
				x++;
			}
			int min=sl[0];
			for(int x=0;nn!=0;nn--)
			{
				if(min>sl[x])
					min=sl[x];
				x++;
			}
			for(int x=0;nnn!=0;nnn--)
			{
				if(sl[x]==min)
				{
					sl[x]=sl[0];
					sl[0]=min;
					break;
				}
				x++;
			}
			for(int x=0;n!=0;n--)
			{
				if(n==1)
					cout<<sl[x];
				else
				{
					cout<<sl[x];
					cout<<' ';
				}
				x++;
			}
			cout<<endl;
		}
	}
	return 0;
}
```
### 2017
```
#include<iostream>
using namespace std;
int main()
{
	int n;
	cin>>n;
	while(n--)
	{
		char s[200];
		cin>>s;
		int l=0;
		for(int x=0;s[x]!='\0';x++)
		{
			if(s[x]=='0'||s[x]=='1'||s[x]=='2'||s[x]=='3'||s[x]=='4'||s[x]=='5'||s[x]=='6'||s[x]=='7'||s[x]=='8'||s[x]=='9')
				l+=1;
		}
		cout<<l<<endl;
	}
	return 0;
}
```
### 2018
```
#include<iostream>
using namespace std;
int jsj(int);
int main()
{
	int n;
	while(cin>>n)
	{
		if(n==0)
			break;
		else
		{
			cout<<(jsj(n))<<endl;
		}
	}
	return 0;
}
int jsj(int n)
{
	int j;
	if(n==1)
		j=1;
	else if(n==2)
		j=2;
	else if(n==3)
		j=3;
	else if(n==4)
		j=4;
	else
	{
		j=(jsj(n-1)+jsj(n-3));
	}
	return j;
}
```
### 2019
```
#include<iostream>
using namespace std;
int main()
{
	int n,m;
	while(cin>>n>>m)
	{
		if(n==0&&m==0)
			break;
		else
		{
		int N=n;
		int x[200];
		for(int l=0;N!=0;N--)
		{
			cin>>x[l];
			l++;
		}
		int l=0;
		for(;x[l]<m;)
			l++;
		int s=n-l+1;
		int nn=n;
		for(;s!=0;s--)
		{
			x[nn]=x[nn-1];
			nn--;
		}
		x[nn+1]=m;
		for(int z=0;(n+1)!=0;n--)
		{
			if(n==0)
				cout<<x[z];
			else
			{
			cout<<x[z]<<' ';
			}
			z++;
		}
		cout<<endl;
		}
	}
}
```
### 2020
```
#include<iostream>
using namespace std;
int main()
{
	int n;
	while(cin>>n)
	{
		if(n==0)
			break;
		else
		{
			int N=n,nn=n,str[200],str1[200];
			for(int x=0;N!=0;N--)
			{
				cin>>str[x];
				x++;
			}
			for(int x=0;nn!=0;nn--)
			{
				if(str[x]<0)
					str1[x]=-(str[x]);
				else
					str1[x]=(str[x]);
				x++;
			}


			int i,j;
			int t;
			for(j=0;j<(n-1);j++)
			{
				for(i=0;i<(n-1-j);i++)
				{
					if(str1[i]<str1[i+1])
					{
						t=str1[i];
						str1[i]=str1[i+1];
						str1[i+1]=t;
						t=str[i];
						str[i]=str[i+1];
						str[i+1]=t;
					}
				}
			}
			for(int z=0;n!=0;n--)
			{
				if(n==1)
					cout<<str[z];
				else
				{
					cout<<str[z]<<' ';
				}
				z++;
			}
			cout<<endl;
		}
	}
	return 0;
}
```
### 1004
```
#include<iostream>
#include<cstring>
using namespace std;
bool bijiao(char*c,char(*al)[30],int*ss,int q)
{
	for(int b=0;b<q;b++)
	{
		if(strcmp(c,al[b])==0)
		{
			ss[b]++;
			return true;
		}
	}
	return false;
}
int main()
{
	int n;
	while(cin>>n)
	{
		if(n==0)
			break;
		else
		{
			int s[1002]={0};
			char all[1002][30];
			char(*a)[30]=all;
		for(int i=0;i<n;i++)
		{
			char co[30];
			cin>>co;
			if(!bijiao(co,a,s,i-1))
			{
				strcpy(all[i],co);
				s[i]=1;
			}
		}
		int m=0;
		for(int j=0;j<n;j++)
			if(s[j]>m)
				m=s[j];
		//cout<<m<<endl;
		for(int d=0;d<n;d++)
			if(s[d]==m)
			{
				cout<<all[d]<<endl;
				break;
			}
		}
	}
	return 0;
}
```
### 2031
```
#include<iostream>
using namespace std;
void change(int a,int b)
{
	if(a<b)
	{
		if(a>=10)
			cout<<(char)(a+55);
		else
		    cout<<a;
	}
	else
	{
		change(a/b,b);
		if(a%b>=10)
			cout<<(char)(a%b+55);
		else
		    cout<<a%b;
	}
}
int main()
{
	int a,b;
	while(cin>>a>>b)
	{
		if(a>=0)
		{
		  change(a,b);
		}
		else
		{
			cout<<'-';
			change(-a,b);
		}
		cout<<endl;
	}
	return 0;
}
```
### 2033
```
#include<iostream>
using namespace std;
int main()
{
	int z;
	while(cin>>z)
	{
		while(z--)
		{
		int liu[5];
		for(int x=0;x<6;x++)
			cin>>liu[x];
		int a,b,c;
		c=liu[2]+liu[5];
		while(c>59)
		{
			c=c-60;
			liu[1]++;
		}
		b=liu[1]+liu[4];
		while(b>59)
		{
			b=b-60;
			liu[0]++;
		}
		a=liu[0]+liu[3];
		cout<<a<<' '<<b<<' '<<c<<endl;
		}
	}
	return 0;
}
```
### 2072
```
#include<iostream>
#include<cstring>
using namespace std;
bool bijiao(char *a,char *b)
{
    int y=0,w=0;
    int x=0;
    for(;*(a+x)!=' '&&*(a+x)!='\0';x++)
        y++;
    x=0;
    for(;*(b+x)!=' '&&*(b+x)!='\0';x++)
        w++;
    if(y!=w)
        return false;
    else
    {
    x=0;
    for(;*(a+x)!=' '&&*(b+x)!=' ';x++)
    {
        if(*(a+x)!=*(b+x))
        {
            break;
        }
    }
    if(*(a+x)==' '||*(b+x)==' ')
        return true;
    else
        return false;
    }
}
int wuliao(char *p)
{
    int x=1,a=1,s[10000]={0},z=0,l=0,len=strlen(p);
    for(;l<len;l++)
    {
        if(p[l]==' '&&p[l+1]!=' '&&p[l+1]!='\0')
        {
            s[z+1]=l+1;
            z++;
            a++;
        }
    }
    int aa=a;
    for(int b=1;b<aa;b++)
    {
        int bbb=b;
        for(int bb=0;bb<bbb;bb++)
        {
            if(bijiao((p+s[b]),(p+s[bb]))==true)
            {
                a--;
                break;
            }
        }
    }
	if(p[0]==' ')
		a=a-1;
    return a;
}
int main()
{
    char n[1000];
    while(gets(n))
    {
        if(n[0]=='#')
            break;
        else
        {
            char *p=n;
            int x;
            x=wuliao(p);
            cout<<x<<endl;
        }
    }
    return 0;
}
```
## 2016-12-09 安安的破壳日礼物 好羞耻好中二（感觉写的完全没有技术含量x
```
#include<iostream>
#include<cstring>
using namespace std;
char what_you_say[100000];
bool suijiao(char *ll)
{
	return 1;
}
void my_answer(char*you)
{
	int len=strlen(you);
	for(int i=0;i<len;i++)
	{
		if(you[i]=='i')
			cout<<"安安安安安安安~"<<' ';
		if(you[i]=='d'&&you[i+1]=='y')
			cout<<"最喜欢子安惹"<<' ';
		if(you[i]=='g')
			if(suijiao(you+i))
				cout<<"wanan"<<' ';
	}
}
void you();          //I'm afraid of return.
int main()     
{
	while(gets(what_you_say))
	{
		if(what_you_say[0]=='b')
		{
			cout<<"灰灰"<<endl;
			break;
		}
		else
		{
		    char*love=what_you_say;
		    my_answer(love);
		    cout<<"喵~~~~~~"<<endl;
		}
	}
	return 0;
}
```
## 作业题 大一上
### 10.29 82-2
```
#include<iostream>
using namespace std;
bool runnian(int);
int main()
{
	int n,y,r;
	cin>>n>>y>>r;
	int sum=0;
	for(int i=1;i<y;i++)
	{
		if(i==1||i==3||i==5||i==7||i==8||i==10||i==12)
			sum+=31;
		else if(i==2)
			sum+=28;
		else
			sum+=30;
	}
	if(runnian(n)==1&&y>2)
		sum+=1;
	sum+=r;
	cout<<sum<<endl;
	return 0;
}
bool runnian(int a)
{
	bool x;
	if((a%4==0&&a%100!=0)||a%400==0)
		x=1;
	else
		x=0;
	return x;
}
```
### 82-3
```
#include<iostream>
using namespace std;
int digit(long,int);
int main()
{
	int x,k;
	long n;
	cin>>n>>k;
	x=digit(n,k);
	cout<<x<<endl;
}
int digit(long n,int k)
{
	int m;
	k-=1;
	while(k--)
	{
		n=n/10;
	}
	if(n==0)
		m=-1;
	else
	    m=n%10;
	return m;
}
```
### 82-6
```
#include<iostream>
using namespace std;
void goldbach(int);
bool prime(int);
int main()
{
	int n;
	cin>>n;
	goldbach(n);
	return 0;
}
void goldbach(int a)
{
	for(int i=3;i*2<a;i++)
	{
		if(prime(i)&&prime(a-i))
		{
			cout<<a<<'='<<i<<'+'<<a-i<<endl;
			return;
		}
	}
}
bool prime(int b)
{
	bool l;
	int z=3;
	if(b%2==0)
		l=0;
	for(;z*z<=b;z++)
	{
		if(b%z==0)
			break;
	}
	if(z*z>=b)
		l=1;
	else
		l=0;
	return l;
}
```
### 83-11
```
#include<iostream>
using namespace std;
void bian(int);
int main()
{
	int i;
	cin>>i;
	bian(i);
	return 0;
}
void bian(int x)
{
	cout<<x%10;
	if(x/10==0)
	  return;
	else
	  bian(x/10);
}
```
### 11.7 106-1
```
#include<iostream>
using namespace std;
int main()
{
	int a[8]={2,33,-6,5,-82,30,99,21},b[8];
	int ii=0;
	for(int i=0;i<8;i++)
	{
		
		if(a[i]<0)
		{
			b[ii]=a[i];
			ii++;
		}
	}
	for(int i=0;i<8;i++)
	{
		if(a[i]>0&&(a[i]%3==0))
		{
			b[ii]=a[i];
			ii++;
		}
	}
	for(;ii<8;ii++)
		b[ii]=0;
	for(int n=0;n<8;n++)
	    cout<<b[n];
	return 0;
}
```
### 106-6
```
#include<iostream>
using namespace std;
int main()
{
	char str[200];
	while(gets(str))
	{
		int n=0,a=0,b=0,c=0,d=0,e=0,f=0,g=0,h=0,i=0,j=0;
		for(int i=0;str[i]!='\0';i++)
		{
			if(str[i]>'0'&&str[i]<'9')
				n++;
			if(str[i]=='0')
				a++;
			if(str[i]=='1')
				b++;
			if(str[i]=='2')
				c++;
			if(str[i]=='3')
				d++;
			if(str[i]=='4')
				e++;
			if(str[i]=='5')
				f++;
			if(str[i]=='6')
				g++;
			if(str[i]=='7')
				h++;
			if(str[i]=='8')
				i++;
			if(str[i]=='9')
				j++;
		}
	cout<<n<<endl;
	cout<<a<<' '<<b<<' '<<c<<' '<<d<<' '<<e<<' '<<f<<' '<<g<<' '<<h<<' '<<i<<' '<<j<<endl;
	}
	return 0;
}
```
### 106-9
```
#include<iostream>
using namespace std;
int main()
{
	int str[10];
	for(int i=0;i<10;i++)
		cin>>str[i];
	int x=0,s[10]={0};
	for(int i=0;i<10;i++)
	{
		for(int j=i+1;j<10;j++)
		{
			if(str[i]==str[j]&&str[i]!=0)
			{
				str[j]=0;
				s[i]++;
			}
		}
	}
	int num=0;
	for(int x=0;x<10;x++)
	{
		if(str[x]!=0)
			num++;
	}
	cout<<num<<endl;
	int m=0;
	for(int z=0;z<10;z++)
	{
		if(m<s[z])
			m=s[z];
	}
	for(int z=0;z<10;z++)
	{
		if(m==s[z])
			cout<<str[z]<<' '<<s[z]+1<<endl;
	}
	return 0;
}
```
### 106-11
```
#include<iostream>
using namespace std;
int main()
{
	int x[6]={1,3,5,7,9},n;
	while(cin>>n)
	{
		int l=0;
		for(;l<5;l++)
			if(n>x[l]&&n<x[l+1])
				break;
		for(int z=4;z>l;z--)
		{
			x[z+1]=x[z];
		}
		x[l+1]=n;
		for(int y=0;y<6;y++)
			cout<<x[y];
		cout<<endl;
	}
	return 0;
}
```
### 11.27 134-1
```
#include<iostream>
#include<string>
using namespace std;
void balala(char *b)
{
	int z,j;
	for(z=j=0;z<strlen(b);z++)
	{
		if(*(b+z)!=' ')
		{
			*(b+j++)=*(b+z);
		}
	}
	*(b+j)='\0';
}
int main()
{
	int i;
	char x[100];
	while(gets(x))
	{
		char *p=x;
	    balala(p);
	    puts(x);
	}
	return 0;
}
```
### 134-2
```
#include<iostream>
#include<string>
using namespace std;
int replace(char *p)
{
	int n=0;
	for(int a=0;a<strlen(p);a++)
	{
		if(*(p+a)=='t')
		{
			*(p+a)='e';
			n++;
		}
		else if(*(p+a)=='T')
		{
			*(p+a)='E';
			n++;
		}
	}
	return n;
}
int main()
{
	char x[100];
	int n;
	cin>>x;
	char *p=x;
	n=replace(x);
	cout<<x<<endl;
	cout<<n<<endl;
	return 0;
}
```
### 134-5
```
#include<iostream>
#include<string>
using namespace std;
int cun(char *b,int *t)
{
	int c=0;
	for(;*(b+c)>='0'&&*(b+c)<='9';)
         c++;
	int s,cc=1;
	s=((*(b)-'0'));
	for(;cc<c;cc++)
	{
		s=s*10+(*(b+cc)-'0');
	}
	*t=s;
	return c;
}
int chun(char *p,int *P)
{
	int c=0,w,v=0;
	for(int q=0;q<strlen(p);)
	{
		w=0;
		if(*(p+q)>='0'&&*(p+q)<='9')
		{
			w=cun((p+q),(P+v));
			c++;
			v++;
		}
		
		q=q+w+1;
	}
	return c;
}
int main()
{
	char x[100];
	
	while(gets(x))
	{
		int a[100]={0};
		char *p=x;
		int *P=a;
		int l;
		l=chun(p,P);
		cout<<l<<endl;
		for(int m=0;a[m]!=0;m++)
			cout<<a[m]<<' ';
		cout<<endl;
	}
	return 0;
}
```
### 12.7 185-2
```
#include<iostream>
using namespace std;
class Score
{
private:
	 int No;
	 char Name[8];
	 int Math;
	 int Phi;
	 int Eng;
public:
	void Input()
	{
		cin>>No>>Name>>Math>>Phi>>Eng;
	}
	int Sum()
	{
		return Math+Phi+Eng;
	}
	void Show()
	{
		cout<<Sum()<<endl;
	}
};
int main()
{
	Score s1;
	s1.Input();
	s1.Sum();
	s1.Show();
	return 0;
}
```
### 186-5
```
#include<iostream>
using namespace std;
class Clock
{
	int hh,mm,ss;
public:
	Clock(int h=0,int m=0,int s=0):hh(h),mm(m),ss(s){}
	void setClock(int h=0,int m=0,int s=0);
	void increamentHour()
	{
		hh++;
		if(hh==24)
			hh=0;
	}
	void increamentMinute()
	{
		mm++;
		if(mm==60)
		{
			mm=0;
			increamentHour();
		}
	}
	void increamentSecond()
	{
		ss++;
		if(ss==60)
		{
			increamentMinute();
			ss=0;
		}
	}
	void show()
	{
		cout<<hh<<':'<<mm<<':'<<ss<<endl;
	}
};
int main()
{
	Clock c1;
	c1.show();
	return 0;
}
```
### 186-7
```
#include<iostream>
using namespace std;
class Date
{
private:
	int year;
	int month;
	int day;
public:
	void setDate(int m,int d)
	{
		month=m;
		day=d;
	}
	void setyear(int yy)
	{
		year=yy;
	}
	void getyear()
	{
		int yy;
		cin>>yy;
		setyear(yy);
	}
	bool isleapyear(int year)
	{
		if(year%400==0||(year%4==0&&year%100!=0))
			return true;
		else
			return false;
	}
	int getskip(int m1,int d1)
	{
		int l=0;
		for(int i=month;i<m1;i++)
		{
			if(i==1||i==3||i==5||i==7||i==8||i==10||i==12)
				l+=31;
			else if(i==2)
			{
				if(isleapyear(year))
					l+=29;
				else
					l+=28;
			}
		}
		l=l-day+d1;
		cout<<l<<endl;
		return l;
	}
};
int main()
{
	Date date;
	date.getyear();
	int a,b;
	cin>>a>>b;
	date.setDate(a,b);
	int c,z;
	cin>>c>>z;
	date.getskip(c,z);
	return 0;
}
```
### 186-9
```
#include<iostream>
#include <cmath>
using namespace std;
class Beeline
{
public:
	int x1;
	int x2;
	int y1;
	int y2;
	Beeline(int a,int b,int c,int d):x1(a),y1(b),x2(c),y2(d){}
	double Lengh()
	{
		double l;
		double x;
		x=(x1-x2)*(x1-x2)+(y1-y2)*(y1-y2);
		l=sqrt(x);
		return l;
	}
	void show()
	{
		cout<<'('<<x1<<','<<y1<<')'<<endl;
		cout<<'('<<x2<<','<<y2<<')'<<endl;
	}
};
class Triangle
{
private:
	int l1,l2,l3;
	
	 Beeline line1;
	Beeline line2;
	Beeline line3;
public:
	Triangle(int a,int b,int c,int d,int e,int f):line1(a,b,c,d),line2(c,d,e,f),line3(e,f,a,b)
	{}
	int Area()
	{
		return ((1/2)*(line1.x1*line1.y2+line1.x2*line2.y2+line2.x2*line1.y1-line1.x1*line2.y2-line1.x2*line1.y1-line2.x2*line1.y2));
	}
	void Print()
	{
		line1.show();
		line2.show();
		line3.show();
		cout<<Area()<<endl;
	}
};
int main()
{
	Triangle tri(10,10,20,10,20,20);
	tri.Print();
	return 0;
}
```
### 211-1
```
#include<iostream>
using namespace std;
const int n=3;
template<class T>
class A
{
private:
	T*p;
	int x;
public:
	A(T *q,int n)
	{
		p=q;
		x=n;
	}
	void search(T x)
	{
		for(int j=0;j<n;j++)
		{
			if(p[j]==x)
				cout<<j<<endl;;
		}
	}
};
int mian()
{
	int Ta[n]={1,2,3};
	int *p=Ta;
	A<int> x(Ta,2);
	x.search(2);
	return 0;
}
```
### 211-5
```
#include<iostream>
using namespace std;
class Student
{
private:
	char name[10];
	int score;
public:
	Student(char*p,int s)
	{
		name[0]=*p;
		score=s;
	}
	friend void output(Student &s);
};
void output(Student &s)
{
	if(s.score>=90)
		cout<<"优"<<endl;
	else if(s.score>=80)
		cout<<"良"<<endl;
	else if(s.score>=70)
		cout<<"中"<<endl;
	else if(s.score>=60)
		cout<<"及格"<<endl;
	else
		cout<<"不及格"<<endl;
}
int main()
{
	char x[10];
	int s;
	cin>>x;
	cin>>s;
	char*p=x;
	Student stu(p,s);
	output(stu);
	return 0;
}
```
### 12.22 258-1
```
#include<iostream>
using namespace std;
class Shape
{
private:
	int x;
public:
	Shape(int xx){x=xx;}
};

class Rectangle:public Shape
{
private:
	int a,b;
public:
	Rectangle(int aa,int bb):Shape(2){a=aa;b=bb;}
	int s(){return a*b;}
};

class Circle:public Shape
{
private:
	int c;
public:
	Circle(int cc):Shape(1){c=cc;}
	int s(){return 3.14*c*c;}
};

class Square:public Rectangle
{
private:
	int d;
public:
	Square(int dd):Rectangle(dd,dd){d=dd;}
	int s(){return d*d;}
};

void main()
{
	Rectangle rec(2,3);
	cout<<rec.s ()<<endl;
	Circle cir(2);
	cout<<cir.s()<<endl;
	Square squ(3);
	cout<<squ.s ()<<endl;
}
```
### 259-3
```
#include<iostream>
using namespace std;

class Person {
	char name[30]; 
	char sex; 
	int age; 
public:
	Person (char * na, char sx, int ag){strcpy(name,na);sex=sx;age=ag;}; 
	void Display(){cout<<name<<' '<<sex<<' '<<age<<endl;};
};


class Teacher:public Person { 
	char post[30],course[30]; 
	public:
		Teacher(char * na, char sx, int ag,char*po,char*cour):Person(na,sx,ag){strcpy(post,po);strcpy(course,cour);};
		void Display(){Person::Display ();cout<<post<<' '<<course<<endl;}
};
class Student:public Person { 
	int Reg_Number; 
	char department[30]; 
	public:
	    Student(char * na, char sx, int ag,int r,char*de):Person(na,sx,ag){Reg_Number=r;strcpy(department,de);};
		void Display(){Person::Display ();cout<<Reg_Number<<' '<<department<<endl;}
};
class Worker:public Person{
	char job[30]; 
	public:
	    Worker(char * na, char sx, int ag,int r,char*jo):Person(na,sx,ag){strcpy(job,jo);};
		void Display(){Person::Display ();cout<<job<<endl;}
	
};
void main() {
	Person per1("sun", 'M', 42);
	Student stu1("guo", 'F', 22, 1001, "comp");
	Teacher teach1("fang", 'M', 38, "professor", "english");
	Worker wor1("wu", 'M', 25, 1021, "cleaner");
	cout<<"== per1.Display() => name,age,sex"<<endl;
	per1.Display();
	cout<<"== stu1.Display() => name,age,sex,Reg_Number,department"<<endl;
	stu1.Display();
	cout<<"== teach1.Display() => name,age,sex,post,course"<<endl;
	teach1.Display();
	cout<<"== wor1.Display() => name,age,sex,";
	cout<<"job"<<endl;
	wor1.Display();
}

```
## PAT 也是比较入门的模拟啊之类的（保持手感必备2333
### 2
```
#include<iostream>
using namespace std;
int main()
{
	int n;
	char m;
	while(cin>>n>>m)
	{
		int z=1,i=3;
		for(;z<=n;)
		{
			z+=(2*i);
			i+=2;
		}
		z=z-2*(i-2);
		i-=2;
		int r=n-z;
		int ii=i;
		for(int k=0;k<ii-2;k++)
		{
			//cout<<i<<k<<endl;
			if(k<((ii-1)/2))
			{
			for(int j=0;j<k;j++)
				cout<<' ';
			i-=2;
			}
			
			else
			{
				for(int j=0;j<ii-k-3;j++)
				    cout<<' ';
				i+=2;
			}
			for(int l=0;l<i;l++)
				cout<<m;
			cout<<endl;
		}
		cout<<r<<endl;
	}

	return 0;
}
```
### 13
```
#include<iostream>
#include<cstring>
using namespace std;
int main()
{
	char str[1010];
	while(cin>>str)
	{
		int s[10];
		memset(s,0,sizeof(s));
		int strl=strlen(str);
		for(int i=0;i<strl;i++)
		{
			if(str[i]=='0')
				s[0]++;
			else if(str[i]=='1')
				s[1]++;
			else if(str[i]=='2')
				s[2]++;
			else if(str[i]=='3')
				s[3]++;
			else if(str[i]=='4')
				s[4]++;
			else if(str[i]=='5')
				s[5]++;
			else if(str[i]=='6')
				s[6]++;
			else if(str[i]=='7')
				s[7]++;
			else if(str[i]=='8')
				s[8]++;
			else if(str[i]=='9')
				s[9]++;
		}
		for(int p=0;p<10;p++)
		{
			if(s[p]!=0)
				cout<<p<<':'<<s[p]<<endl;
		}
	}
	return 0;
}
```
### 17
```
#include<iostream>
#include<cstring>
using namespace std;
int main()
{
	char s[10000];
	while(cin>>s)
	{
		int len=strlen(s);int i=0;
		for(;i<len-1;i++)
		{
			if(s[i]=='-')
				cout<<"fu";
			if(s[i]=='1')
				cout<<"yi";
			if(s[i]=='2')
				cout<<"er";
			if(s[i]=='3')
				cout<<"san";
			if(s[i]=='4')
				cout<<"si";
			if(s[i]=='5')
				cout<<"wu";
			if(s[i]=='6')
				cout<<"liu";
			if(s[i]=='7')
				cout<<"qi";
			if(s[i]=='8')
				cout<<"ba";
			if(s[i]=='9')
				cout<<"jiu";
			if(s[i]=='0')
				cout<<"ling";
			cout<<' ';
		}
		if(s[i]=='-')
				cout<<"fu";
			if(s[i]=='1')
				cout<<"yi";
			if(s[i]=='2')
				cout<<"er";
			if(s[i]=='3')
				cout<<"san";
			if(s[i]=='4')
				cout<<"si";
			if(s[i]=='5')
				cout<<"wu";
			if(s[i]=='6')
				cout<<"liu";
			if(s[i]=='7')
				cout<<"qi";
			if(s[i]=='8')
				cout<<"ba";
			if(s[i]=='9')
				cout<<"jiu";
			if(s[i]=='0')
				cout<<"ling";
			cout<<endl;
	}
	return 0;
}
```
### 1001
```
#include<iostream>
using namespace std;
int res;
void m(int x)
{
	if(x==1)
		return;
	else if(x%2==0)
	{
		res++;
		m(x/2);
	}
	else
	{
		res++;
		m((3*x+1)/2);
	}
}
int main()
{
	int n;
	while(cin>>n)
	{
		res=0;
		m(n);
		cout<<res<<endl;
	}
	return 0;
}
```
### 1002
```
#include<iostream>
#include<cstring>
using namespace std;
void rf(int q)
{
	if(q==0)
		cout<<"ling";
	else if(q==1)
		cout<<"yi";
	else if(q==2)
		cout<<"er";
	else if(q==3)
		cout<<"san";
	else if(q==4)
		cout<<"si";
	else if(q==5)
		cout<<"wu";
	else if(q==6)
		cout<<"liu";
	else if(q==7)
		cout<<"qi";
	else if(q==8)
		cout<<"ba";
	else if(q==9)
		cout<<"jiu";
}
void digui(int s)
{
	if(s!=0)
	{
		digui(s/10);
		rf(s%10);
		cout<<' ';
	}
}
int main()
{
	char str[200];
	while(cin>>str)
	{
		int strl=strlen(str);
		int z=0;
		for(int t=0;t<strl;t++)
		{
			z+=(str[t]-'0');
		}
		digui(z/10);
		z=z%10;
		rf(z);
		cout<<endl;
	}
	return 0;
}
```
### 1003
```
#include<iostream>
#include<cstring>
using namespace std;
bool judgea(char*p,int len)
{
	int pp=0,t=0,a=0;
	for(int i=0;i<len;i++)
	{
				if(!(p[i]=='P'||p[i]=='A'||p[i]=='T'))
				{
					cout<<"NO"<<endl;
					return true;
				}
				if(p[i]=='P')
					pp++;
				if(p[i]=='T')
					t++;
				if(p[i]=='A')
					a++;
	}
	if(pp!=1||t!=1||a==0)
		{
					cout<<"NO"<<endl;
					return true;
		}
	else
		return false;
}
int j(char*p)
{
	int q=0;
	if(p[1]=='A'&&p[2]=='T')
		return 1;
	else
		{
			int y=1;
			for(;p[y]=='A';y++)
			{
				q++;
			}
			if(p[y]=='T')
				return q;
		}
	cout<<"NO"<<endl;
	return 0;
}
bool judgeb(char*p,int len)
{
	int l;
	int i=0;
	for(;i<len;i++)
	{
		if(p[i]=='P')
		{
			l=j(p+i);
			if(l==0)
				return false;
			break;
		}
	}
	l=l*i;
	int n=0;
	for(;n<len;n++)
	{
		if(p[n]=='T')
			break;

	}
	if(l==(len-n-1))
		return true;
	else
		{
					cout<<"NO"<<endl;
					return false;
		}
}
int main()
{
	int n;
	while(cin>>n)
	{
		while(n--)
		{
		    char str[110];
			cin>>str;
			int len=strlen(str);
			if(!judgea(str,len))
			{
				if(judgeb(str,len))
					cout<<"YES"<<endl;
			}
		}
	}
	return 0;
}
```
### 1004
```
#include<iostream>
using namespace std;
struct Stu
{
	char name[15];
	char num[15];
	int grade;
};
int main()
{
	int n;
	while(cin>>n)
	{
		Stu stus[10000];
		for(int i=0;i<n;i++)
		{
			cin>>stus[i].name>>stus[i].num>>stus[i].grade;
		}
		int min=stus[0].grade;
		int max=stus[1].grade;
		int mi=0,ma=1;
		for(int x=0;x<n;x++)
		{
			if(stus[x].grade>max)
			{
				max=stus[x].grade;
				ma=x;
			}
			if(stus[x].grade<min)
			{
				min=stus[x].grade;
				mi=x;
			}
		}
		printf("%s ",stus[ma].name);
		printf("%s\n",stus[ma].num);
		printf("%s ",stus[mi].name);
		printf("%s\n",stus[mi].num);
	}
	return 0;
}
```
### 1005
```
#include <stdio.h>
#include <string.h>

int main(void)
{
    int i, j, num, x;
    int cnt[101];
    int bucket[101];
    int flag = 0;

    scanf("%d", &num);
    for(i = 0; i < num; i++)
        scanf("%d", &cnt[i]);

    memset(bucket, 0x00, sizeof(bucket));

    for(i = 0; i < num; i++)
    {
        x = cnt[i];        
        if(bucket[x] == 1)
            continue ; 

        while(x != 1 && x != 0)
        {
            if(x % 2 == 0)
                x = x / 2;
            else
                x = (3 * x + 1) / 2;
            if(x <= 100)
                bucket[x] = 1;

        }
    }

    for(j = 0; j < num; j++)
    {
        if(bucket[cnt[j]] == 0)
            flag++;
    }

    for(i = sizeof(bucket)/sizeof(bucket[0])-1; i >= 0; i--)
    {
        if(bucket[i] != 1)
        {
            for(j = 0; j < num; j++)
            {
                if(cnt[j] == i)
                {
                    printf(flag > 1 ? "%d " : "%d", i);
                    flag -= 1;
                }
            }
        }
    }
    
    return 0;    
}
```
### 1006
```
#include<iostream>
using namespace std;
void solve(int x)
{
	if(x>99)
	{
		int t=x/100;
		while(t--)
			cout<<'B';
		int j=(x%100)/10;
		while(j--)
			cout<<'S';
		int q=x%10;
		for(int i=1;i<=q;i++)
			cout<<i;
	}
	else if(x>9)
	{
		int j=x/10;
		while(j--)
			cout<<'S';
		int q=x%10;
		for(int i=1;i<=q;i++)
			cout<<i;
	}
	else
	{
		for(int i=1;i<=x;i++)
			cout<<i;
	}
}
int main()
{
	int x;
	while(cin>>x)
	{
		solve(x);
		cout<<endl;
	}
	return 0;
}
```
### 1007
```
#include<iostream>
using namespace std;
bool panduan(int i)
{
	if(i%2==0)
		return false;
	int s=3;
	for(;s*s<=i;s++)
	{
		if(i%s==0)
			break;
	}
	if(s*s>i)
		return true;
	else
		return false;
}
int su[100000];
int main()
{
	su[0]=2;
	int n;
	while(cin>>n)
	{
		for(int i=2,a=1;i<n;i++)
		{
			if(panduan(i))
			{
				su[a]=i;
				a++;
			}
		}
		int res=0;
		for(int p=1;su[p]!=0;p++)
		{
			if((su[p]-su[p-1])==2)
				res++;
		}
		cout<<res<<endl;
	}
	return 0;
}
```
### 1008
```
#include<iostream>
using namespace std;
int main()
{
	int n,m;
	while(cin>>n>>m)
	{
		int str[110];
		for(int i=0;i<n;i++)
			cin>>str[i];
		if((m-n)!=0)
		{
		for(int q=(n-m);q<n;q++)
		{
			cout<<str[q]<<' ';
		}
		}
		int w=0;
		if(w<n-m-1)
		{
		for(;w<(n-m-1);w++)
		{
			cout<<str[w]<<' ';
		}
		}
		cout<<str[w]<<endl;
	}
	return 0;
}
```
### 1010
```
#include<iostream>
using namespace std;
int main()
{
	long long int a,b,c;
	while(cin>>a>>b>>c);
	{
		if(a+b>c)
			cout<<1<<endl;
		else
			cout<<0<<endl;
	}
	return 0;
}
```
### 2010
```
#include<iostream>
using namespace std;
int main()
{
	int y;
	while(cin>>y)
	{
		int s[10000];
		s[0]=y;
		int x,i=1;
		for(;;i++)
		{
			cin>>x;
			if(x!=0)
				s[i]=x;
			else
			{s[i]=x;
			break;}
		}
		for(int j=0;j<i;)
		{
			if(s[j+1]!=1&&s[j+1]!=0)
			{
				cout<<s[j]*s[j+1]<<' '<<s[j+1]-1<<' ';

			}
			else if(s[j+1]==1)
				cout<<s[j]<<' ';
			else if(s[j+1]==0)
				cout<<0<<endl;
			j+=2;
		}
	}
	return 0;
}
```
## 寒假看着白书的VOJ划水之路（大概算是acm入门必经之路？反正窝就围观围观
### 数据结构 1
```
#include<iostream>
#include<algorithm>
#include<queue>
using namespace std;
struct node
{
	int x,y;
};
bool cmp(node a,node b)
{
	return a.x<b.x;
}
int main()
{
	int N,l,p;
	while(cin>>N)
	{
		node s[10100];
		int n=0;
		for(;n<N;n++)
		{
			cin>>s[n].x>>s[n].y;
		}
		cin>>l>>p;
		for(int i = 0; i < N; i++)
             s[i].x = l - s[i].x;
		s[N].x=l;
		s[N].y=0;
		N++;
		sort(s,s+N,cmp);
		int res=0;
		int f=p;
		int j=0;
		priority_queue<int>que;
		for(int i=0;i<N;i++)
		{
			int d=s[i].x-j;
			while(f<d)
			{
				if(que.empty())
				{
					cout<<-1<<endl;
					return 0;
				}
				f+=que.top();
				que.pop();
				res++;
			}
			f-=d;
			j=s[i].x;
			que.push(s[i].y);
		}
	cout<<res<<endl;
	}
	return 0;
}
```
### 搜索 1-lake couting
```
#include<iostream>
using namespace std;
char map[110][110];
int fx[3]={-1,0,1,},fy[3]={-1,0,1};
int n,m;
void dfs(int i,int j)
{
	map[i][j]='.';
	for(int x=0;x<3;x++)
	{
		for(int y=0;y<3;y++)
		{
			int l1,l2;
			l1=i+fx[x];
			l2=j+fy[y];
		    if(map[l1][l2]=='W'&&l1<n&&l1>=0&&l2>=0&&l2<m)
				{
					dfs(l1,l2);
				}
		}
	}
}
int main()
{
	while(cin>>n>>m)
	{
		for(int i=0;i<n;i++)
			for(int j=0;j<m;j++)
				cin>>map[i][j];
		int s=0;
		for(int i=0;i<n;i++)
			for(int j=0;j<m;j++)
			{
				if(map[i][j]=='W')
				{
					dfs(i,j);
					s++;
				}
			}
			cout<<s<<endl;
	}
	return 0;
}
```
### 2-red and black
```
#include<iostream>
using namespace std;
int n,m,rf;
char map[22][22];
char dx[4][2]={-1,0,1,0,0,1,0,-1};
void dfs(int i,int j)
{
	map[i][j]='*';
	for(int x=0;x<4;x++)
	{
		int q,w;
		q=i+dx[x][0];
		w=j+dx[x][1];
		if(map[q][w]=='.'&&q>=0&&w>=0&&q<n&&w<m)
		{
			rf++;
			dfs(q,w);
		}
	}
}
int main()
{
	while(cin>>m>>n)
	{
		if(n==0&&m==0)
			break;
		else
		{
			rf=1;
		for(int i=0;i<n;i++)
			for(int j=0;j<m;j++)
				cin>>map[i][j];
		for(int i=0;i<n;i++)
			for(int j=0;j<m;j++)
			{
				if(map[i][j]=='@')
					dfs(i,j);
			}
			cout<<rf<<endl;
		}
	}
	return 0;
}
```
### 3-curling
```
#include<iostream>
using namespace std;
int map[22][22];
int n,m;
int xx;
int ch[4][2]={-1,0,0,-1,0,1,1,0};
struct RF
{
	int map1[22][22];
	int x,y;    //zhuangtai
};
void dfs(RF rf,int x)    //x is bushu
{
	if(x>=xx)
		return;
	else
	{
		for(int ll=0;ll<4;ll++)
		{
			RF rf1;
			for(int i=0;i<n;i++)
				for(int j=0;j<m;j++)
					rf1.map1[i][j]=rf.map1[i][j];
			rf1.x =rf.x+ch[ll][0];
			rf1.y =rf.y+ch[ll][1];
			if(!(rf1.x>=0&&rf1.x<n&&rf1.y>=0&&rf1.y<m))
					continue;
			if(rf1.map1[rf1.x ][rf1.y ]==3)
			   {
				xx=x;
				return;
			   }
			if(rf1.map1[rf1.x ][rf1.y ]!=0)
			{
				//cout<<rf1.x <<' '<<rf1.y <<endl;
				continue;
			}
			while(rf1.map1[rf1.x ][rf1.y ]==0||rf1.map1[rf1.x ][rf1.y ]==3)
			{
				if(rf1.map1[rf1.x ][rf1.y ]==3)
			   {
				xx=x;
				return;
			   }
				rf1.x =rf1.x+ch[ll][0];
			    rf1.y =rf1.y+ch[ll][1];
				if(!(rf1.x>=0&&rf1.x<n&&rf1.y>=0&&rf1.y<m))
					break;
			}
			
			if(!(rf1.x>=0&&rf1.x<n&&rf1.y>=0&&rf1.y<m))
					continue;
			if(rf1.map1[rf1.x ][rf1.y ]==1)
			{
				RF rf11;
				for(int i=0;i<n;i++)
				  for(int j=0;j<m;j++)
					rf11.map1[i][j]=rf1.map1[i][j];
				rf11.map1[rf1.x ][rf1.y ]=0;
				rf11.x =rf1.x-ch[ll][0] ;
				rf11.y =rf1.y-ch[ll][1];
				dfs(rf11,x+1);
			}
		}
		return;
	}

}
int main()
{
	while(cin>>m>>n)
	{
		if(n==0&&m==0)
			break;
		else
		{
			xx=11;
			RF rf;
			for(int i=0;i<n;i++)
				for(int j=0;j<m;j++)
					cin>>map[i][j];
			for(int i=0;i<n;i++)
				for(int j=0;j<m;j++)
				{
					if(map[i][j]==2)
					{
						rf.x =i;
						rf.y =j;
						map[i][j]=0;
					}
					
				}
			for(int i=0;i<n;i++)
				for(int j=0;j<m;j++)
					rf.map1[i][j]=map[i][j];
			dfs(rf,1);
			if(xx==11)
				cout<<-1<<endl;
			else
				cout<<xx<<endl;
		}
	}
	return 0;
}
```
### 4-meteor shower
```
#include<iostream>
#include<queue>
using namespace std;
int map[333][333];
int fx[4][2]={1,0,0,1,-1,0,0,-1};
bool visit[333][333];
struct RF
{
	int x,y;
	int i;
};

int bfs()
{
	queue<RF> q;
	RF a;
	a.x =0;
	a.y =0;
	a.i =0;
	q.push(a);
	visit[0][0]=1;
	while(!q.empty ())
	{
		a=q.front ();
		q.pop();
		for(int m=0;m<4;m++)
		{
			RF b;
			b.x =fx[m][0]+a.x ;
			b.y =fx[m][1]+a.y ;
			b.i =1+a.i ;
			if((!(b.x >=0&&b.x <333&&b.y>=0&&b.y<333))||visit[b.x][b.y]==1)
				continue;
			if(map[b.x ][b.y ]==-1)
			{
				return b.i ;
			}
			if(map[b.x ][b.y ]<=b.i )
				continue;
			visit[b.x][b.y]=1;
			q.push(b);
		}
	}
	return -1;
}



int main()
{
	int z;
	int met[5];
	while(cin>>z)
	{
		for(int r=0;r<333;r++)
			for(int f=0;f<333;f++)
				visit[r][f]=0;
        
		for(int r=0;r<333;r++)
			for(int f=0;f<333;f++)
				map[r][f]=-1;
		for(int a=0;a<z;a++)
		{
			cin>>met[0];
			cin>>met[1];
			cin>>met[2];
			if((map[met[0]][met[1]]>met[2]||map[met[0]][met[1]]==-1))
				         
			        map[met[0]][met[1]]=met[2];
			for(int chun=0;chun<4;chun++)
			{
				met[3]=met[0]+fx[chun][0];
				met[4]=met[1]+fx[chun][1];
				if(met[3]>=0&&met[3]<333&&met[4]>=0&&met[4]<333)
				{
					if((map[met[3]][met[4]]>met[2]||map[met[3]][met[4]]==-1))
				          map[met[3]][met[4]]=met[2];
				}
			}
		}
		if(map[0][0]==-1)
		{
			cout<<0<<endl;
			continue;
		}
		if(map[0][0]==0)
		{
			cout<<-1<<endl;
			continue;
		}
		cout<<bfs()<<endl;

	}
	return 0;
}
```
### 贪心 1-优先队列
```
#include<iostream>
#include<queue>
#include<cmath> 
#include<cstdio> 
using namespace std;
int main()
{
	int n;
	while(cin>>n)
	{
		priority_queue<double>q;
		int m;
		while(n--)
		{
			cin>>m;
			q.push(m);
		}
		double r=q.top();
		while(q.size()>1)
		{
			double a=q.top();  
            q.pop();  
            double b=q.top();  
            q.pop();  
            r=2*sqrt(a*b);  
            q.push(r);  
		}
		printf("%.3f\n",r);
	}
	return 0;
}
```
### 2
```
#include<iostream>
#include<cstring>
using namespace std;
char bj(char*a,char*b)
{

	if(*a==*b)
		return bj(++a,--b);
	else
	  return (*a)>(*b)?'r':'l';
}
void change(char* cow1,int n,char* cow2)
{
	if(n==1)
	{
		cow2[0]=cow1[0];
		cow2[1]='\0';
		return;
	}
	else if(n==0)
	{
		cow2[0]='\0';
		return;
	}
	else
	{
		if(bj(cow1,cow1+n-1)=='r')
		{
			cow2[0]=cow1[n-1];
			change(cow1,n-1,++cow2);
		}
		else if(bj(cow1,cow1+n-1)=='l')
		{
			cow2[0]=cow1[0];
			change(++cow1,n-1,++cow2);
		}
	}
	
}
int main()
{
	int N;
	while(cin>>N)
	{
		char cow1[2100],cow2[2100];
		for(int n=0;n<N;n++)
			cin>>cow1[n];
		change(cow1,N,cow2);
		int len=strlen(cow2);
		for(int i=0;i<len;i++)
		{
			
			if(i%80==79)
				cout<<cow2[i]<<endl;
			else
				cout<<cow2[i];
		}
		cout<<endl;
	}
	return 0;
}
```
### 3
```
#include<iostream>
using namespace std;
int res;
void zz(int*str,bool*str1,int r)
{
	int x=0;
	for(;*(str+x)<=(*str+r);x++)
		*(str1+x)=true;
	for(int s=x;*(str+s)<=(*(str+x-1)+r);s++)
		*(str1+s)=true;
	res++;
}
int main()
{
	int r,n;
	while(cin>>r>>n)
	{
		if(r==-1&&n==-1)
		{
			break;
		}
		else
		{
			res=0;
			int s[1100];
			bool ss[1100];
			for(int N=0;N<n;N++)
				cin>>s[N];
			for(int N=0;N<n;N++)
				ss[N]=false;
			for(int i=1;i<n;i++)
			{
				for(int j=0;j<n-i;j++)
				{
					if(s[j]>s[j+1])
					{
						int t;
						t=s[j+1];
						s[j+1]=s[j];
						s[j]=t;
					}
				}
			}
			for(int N=0;N<n;N++)
			{
				if(ss[N]==false)
					zz(s+N,ss+N,r);
			}
			cout<<res<<endl;

		}
	}
	return 0;
}
```
### 4
```
#include<iostream>
using namespace std;
long long res;
void cut(int *str,int x)
{
	if(x==2)
		res+=str[0]+str[1];
	else
	{
	int m1=0;
	int m2=1;
	for(int m=0;m<x;m++)
	{
		if(str[m1]>str[m])
		{
			int t;
			t=str[m];
			str[m]=str[m1];
			str[m1]=t;
		}
		
	}
	for(int m=0;m<x;m++)
	{
		if(m==m1)
			continue;
	    else if(str[m2]>str[m])
		{
			int t;
			t=str[m];
			str[m]=str[m2];
			str[m2]=t;
		}
	}
	res+=(str[m1]+str[m2]);
	str[m1]=(str[m1]+str[m2]);
	str[m2]=str[x-1];
	cut(str,x-1);
	}
}
int main()
{
	int n;
	while(cin>>n)
	{
		res=0;
		int str[20100];
		for(int m=0;m<n;m++)
			cin>>str[m];
		cut(str,n);
		cout<<res<<endl;
	}
	return 0;
}
```
## 数据结构 煤大OJ 大一下
### 1A
```
#include<iostream>
#include<cstring>
using namespace std;
int main()
{
	char s1[110],s2[110],s3[110];
	while(cin>>s1)
	{
		cin>>s2;
		int len1=strlen(s1);
		int len2=strlen(s2);
		for(int i=len1-1,ii=len2-1,j=0;i>=0;i--,j++,ii--)
		{
			if(ii>=0)
			{
			   if(s1[i]>=s2[ii])
				s3[j]=s1[i]-s2[ii]+48;
			   else
			   {
				s3[j]=s1[i]-s2[ii]+58;
				 if(s1[i-1]>'0')
				    s1[i-1]=s1[i-1]-'1'+48;
				 else
				 {
					int q=1;
					while(s1[i-q]=='0')
					{
						s1[i-q]='9';
						q++;
					}
					s1[i-q]=s1[i-q]-'1'+48;
				 }
			   }
			}
			else
			{
			   
				s3[j]=s1[i];
			   
			}
		}
		int z=len1-1;
		
		while(s3[z]=='0')
			z--;
		for(;z>=0;z--)
		    cout<<s3[z];
		cout<<endl;
	}
	
	return 0;
}
```
### 1B
```
#include<iostream>
using namespace std;
int main()
{
	int a;
	while(cin>>a)
	{
		int s[10];
		s[0]=a;
		for(int i=1;i<10;i++)
		{
			cin>>s[i];
		}
		int b;
		cin>>b;
		int res=0;
		for(int j=0;j<10;j++)
		{
			if(s[j]<=b+30)
				res++;
		}
		cout<<res<<endl;
	}
	return 0;
}
```
### 1C
```
#include<iostream>
using namespace std;
int main()
{
	int a,b;
	while(cin>>a>>b)
	{
		int s[10010]={0};
		while(b--)
		{
			int x,y;
			cin>>x>>y;
			for(int i=x;i<=y;i++)
			{
				s[i]=1;
			}
		}
		int res=0;
		for(int j=0;j<=a;j++)
		{
			if(s[j]==1)
				res++;
		}
		cout<<a-res+1<<endl;
	}
	return 0;
}
```
### 1D
```
#include<iostream>
#include<cstring>
using namespace std;
int main()
{
	int n;
	while(cin>>n)
	{
		if(n>0)
		{
		while(n--)
		{
			char s[10];
			cin>>s;
			int l=strlen(s);
			cout<<l<<' ';
			for(int i=l-1;i>=0;i--)
				cout<<s[i];
			cout<<endl;
		}
		}
	}
	return 0;
}
```
### 1E
```
#include<iostream>
#include<cstring>
using namespace std;
int main()
{
	char s[110];
	while(cin>>s)
	{
		int len=strlen(s);
		for(int i=0;i<len;i++)
		{
			if((s[i]>='a'&&s[i]<='u')||(s[i]>='A'&&s[i]<='U'))
				cout<<char (s[i]+5);
			else if((s[i]>'u'&&s[i]<='z')||(s[i]>'U'&&s[i]<='Z'))
				cout<<char (s[i]+5-26);
		}
		cout<<endl;
	}
	return 0;
}
```
### 1F
```
#include<iostream>
using namespace std;
int main()
{
	int a;
	while(cin>>a)
	{
		while(a--)
		{
			char s[10];
			cin>>s;
			cout<<((s[0]-48)*10+s[1]-48)*3600+((s[3]-48)*10+s[4]-48)*60+((s[6]-48)*10+s[7]-48)<<endl;
		}
	}
	return 0;
}
```
### 1G
```
#include<iostream>
using namespace std;
int main()
{
	int a,b;
	while(cin>>a)
	{
		int s[220],ss[110];
		for(int i=0;i<a;i++)
			cin>>s[i];
		cin>>b;
		for(int j=0;j<b;j++)
			cin>>ss[j];
		for(int i=0;i<a-1;i++)
			cout<<s[i]<<' ';
		cout<<s[a-1]<<endl;
		for(int i=0;i<b-1;i++)
			cout<<ss[i]<<' ';
		cout<<ss[b-1]<<endl;
		int aa=a;
		for(int j=0;j<b;j++)
		{
			int i=0;
			for(;i<a;i++)
			{
				if(s[i]==ss[j])
				{
					for(int ii=0;ii<aa-1;ii++)
			              cout<<s[ii]<<' ';
		            cout<<s[aa-1]<<endl;
					break;
				}
			}
			if(i==a)
			{
				s[aa]=ss[j];
				for(int ii=0;ii<aa;ii++)
			              cout<<s[ii]<<' ';
		            cout<<s[aa]<<endl;
					aa++;
			}
		}
		cout<<endl;
	}
	return 0;
}
```
### 1H
```
#include<iostream>
#include<algorithm>
using namespace std;
int main()
{
	int a,b;
	while(cin>>a)
	{
		int s[10000];
		for(int i=0;i<a;i++)
			cin>>s[i];
		cin>>b;
		for(int i=0;i<b;i++)
			cin>>s[a+i];
		
		sort(s,s+a+b);
		for(int i=0;i<a+b;i++)
		{
			if(i==0)
				cout<<s[i];
			else
		       cout<<' '<<s[i];
		}
		cout<<endl;
	}
	return 0;
}
```
### 1J
```
#include<iostream>
#include<stdlib.h>
#include<stdio.h>
using namespace std;
typedef int ElemType;

typedef struct LNode{
	ElemType data;
	struct LNode *next;
}LNode,*LinkList;

int GetElem_L(LinkList &L,int i,ElemType &e)
{
	LinkList p;
	p=L->next;
	int j=1;
	while(p&&j<i)
	{
		p=p->next;
		++j;
	}
	if(!p||j>i)
		return 0;
	e=p->data;
	return 1;
}

int ListInsert_L(LinkList &L,int i,ElemType e)
{
	LinkList p,s;
	p=L;
	int j=0;
	while(p&&j<i-1)
	{
		p=p->next;
		++j;
	}
	if(!p||j>i-1)
		return 0;
	s=(LinkList) malloc(sizeof(LNode));
	s->data=e;
	s->next=p->next;
	p->next=s;
	return 1;
}

int ListDelete_L(LinkList &L,int i,ElemType &e)
{
	LinkList p,q;
	p=L;
	int j=0;
	while(p->next&&j<i-1)
	{
		p=p->next;
		++j;
	}
	if(!(p->next)||j>i-1)
		return 0;
	q=p->next;
	p->next=q->next;
	e=q->data;
	free(q);
	return 1;
}

void CreateList_L(LinkList &L,int n)
{
	LinkList p;
	int i;
	L=(LinkList) malloc(sizeof(LNode));
	L->next=NULL;
	for(i=n;i>0;--i)
	{
		p=(LinkList) malloc(sizeof(LNode));
		scanf("%d",&p->data);
		p->next=L->next;
		L->next=p;
	}
}
int main()
{
	int n;
	scanf("%d",&n);//cin>>n;
	LinkList L;
	CreateList_L(L,n);
	int m,x,e,a;
	scanf("%d",&m);//cin>>m;
	char s[10];
	while(m--)
	{
		scanf("%s",s);//cin>>s;
		if(s[0]=='g'&&s[1]=='e'&&s[2]=='t')
		{
			scanf("%d",&x);//cin>>x;
			if(GetElem_L(L,x,e))
				printf("%d\n",e);//cout<<e<<endl;
			else
				printf("get fail\n");//cout<<"get fail"<<endl;
		}
		else if(s[0]=='i'&&s[1]=='n'&&s[2]=='s'&&s[3]=='e'&&s[4]=='r'&&s[5]=='t')
		{
			scanf("%d%d",&a,&e);//cin>>a>>e;
			if(ListInsert_L(L,a,e))
				printf("insert OK\n");//cout<<"insert OK"<<endl;
			else
				printf("insert fail\n");//cout<<"insert fail"<<endl;
		}
		else if(s[0]=='d'&&s[1]=='e'&&s[2]=='l'&&s[3]=='e'&&s[4]=='t'&&s[5]=='e')
		{
			scanf("%d",&x);//cin>>x;
			if(ListDelete_L(L,x,e))
				printf("delete OK\n");//cout<<"delete OK"<<endl;
			else
				printf("delete fail\n");//cout<<"delete fail"<<endl;
		}
		else if(s[0]=='s'&&s[1]=='h'&&s[2]=='o'&&s[3]=='w')
		{
			if(!GetElem_L(L,1,e))
				printf("Link list is empty\n");//cout<<"Link list is empty\n"<<endl;
			else{
			  for(int z=1;GetElem_L(L,z,e);z++)
			  {
				if(z==1)
					cout<<e;
				else
					cout<<' '<<e;
			  }
			  cout<<endl;
			}
		}
	}
	return 0;
}
```
### 1K
```
#include<iostream>
#include<cstdio>
#include<string>
#include <stdio.h>
#include<string.h>
using namespace std;  

#define MAXSIZE 11  
  
typedef char ElemType[8];  
  
typedef struct {  
    ElemType data;  
    int cur;  
}NodeType;  
  
NodeType space[MAXSIZE];  
  
typedef struct {  
    int elem;  
    int length;  
    int listsize;  
}Slinklist;  
 Slinklist s; 
  
void Initspace()
{  
    memset(space, 0, sizeof(space));  
    for (int i = 0; i < MAXSIZE - 1; i++)  
    {  
        space[i].cur = i + 1;  
    }  
    space[0].cur = 2;  
    space[1].cur = 0;  
    space[MAXSIZE - 1].cur = 0;
}  
  
int Malloc()
{  
    int i = space[0].cur;  
    if (space[0].cur)  
        space[0].cur = space[space[0].cur].cur;  
    return i;  
}  
  
void  Insert(NodeType space[], int n, char b[])
{  
    int m = Malloc();  
    strcpy(space[m].data, b);  
    int j = 1, i = 1;  
    while (j <n&&space[i].cur)  
    {  
        i = space[i].cur;  
        j++;  
    }  
    space[m].cur = space[i].cur;  
    space[i].cur = m;  
    s.length++;  
}  

  
void Free(int k)  
{  
    space[k].cur = space[0].cur;  
    space[0].cur = k;  
}  

void Delete()  
{  
	int n;
	cin>>n;
    int i,j=1;  
    i =1;  
    while (j<n&&space[i].cur)  
    {  
        j++;  
        i= space[i].cur;  
    }  
    j = space[i].cur;  
    space[i].cur = space[j].cur;  
    space[j].cur = space[0].cur;  
    space[0].cur = j;  
}  


int Search(char b[])
{  
    int i = space[1].cur;  
    while (i&&strcmp(space[i].data, b))  
    {  
        i = space[i].cur;  
    }  
	return i;
}  
 
int main()  
{  
    char a[10], b[10]; int n;  
    s.elem = 1, s.length = 0, s.listsize = 10;  
    Initspace();  
    while(~scanf("%s", a))
    {  
        if(!strcmp("show", a))  
        {  
            for(int i = 0; i < 11; i++)  
            {  
               printf("%-8s%2d\n", space[i].data, space[i].cur);  
             }  
             printf("********************\n");  
        }  
        if(!strcmp("insert", a))  
        {  
            scanf("%d", &n);  
            scanf("%s", &b, 10);  
            Insert(space, n, b); 
        }  
        if(!strcmp("delete", a))  
        { 
            Delete();  
        }  
        if(!strcmp("search", a))  
        {  
            getchar();  
            scanf("%s", &b, 10);  
            int i=Search(b);  
            printf("%2d\n", i);  
            printf("********************\n");  
        }  
    }  
    return 0;  
}
```
### 1L
```
#include<iostream>
#include<stdlib.h>
#include<stdio.h>
using namespace std;

typedef int ElemType;
typedef struct DuLNode
{
	ElemType data;
	struct DuLNode *prior;
	struct DuLNode *next;
}DuLNode,*DuLinkList;

void ListCreate_Dul(DuLinkList &L)
{
	L=(DuLinkList) malloc(sizeof(DuLNode));
	L->prior=L;
	L->next=L;
}

DuLinkList GetElemP_DuL(DuLinkList L,int i)
{
	DuLinkList p;
	p=L->next;
	int j=1;
	while(p!=L&&j<i)
	{
		p=p->next;
		++j;
	}
	if(p==L&&j<i)
		return NULL;
	else
		return p;
}

int ListInsert_DuL(DuLinkList &L,int i,ElemType e)
{
	DuLinkList p,s;
	if(!(p=GetElemP_DuL(L,i)))
		return 0;
	if(!(s=(DuLinkList) malloc(sizeof(DuLNode))))
		return 0;
	s->data=e;
	s->prior=p->prior;
	p->prior->next=s;
	s->next=p;
	p->prior=s;
	return 1;
}

int ListDelete_DuL(DuLinkList &L,int i,ElemType &e)
{
	DuLinkList p;
	if(!(p=GetElemP_DuL(L,i)))
		return 0;
	e=p->data;
	p->prior->next=p->next;
	p->next->prior=p->prior;
	free(p);
	return 1;
}
int main()
{
	int a;
	DuLinkList L;
	ListCreate_Dul(L);
	while(cin>>a)
	{
		if(a==1)
		{
			int b,c;
			cin>>b>>c;
			ListInsert_DuL(L,b,c);
			//	cout<<'1'<<endl;

		}
		else if(a==2)
		{
			int b;
			cin>>b;
			DuLinkList c;
			c=GetElemP_DuL(L,b);
			ListDelete_DuL(L,b,c->data);
		}
		else if(a==0)
		{
			int i=2;
			DuLinkList z;
			z=L->next;
			cout<<z->data;
			//cout<<z<<' '<<GetElemP_DuL(L,2)<<' ';
			z=z->next;
			if(z==L)
				cout<<endl;
			else
			{
				while(z!=L)
			  {
				cout<<' '<<z->data;
				z=z->next;
				//cout<<endl<<z<<endl;
				i++;
			  }
			  cout<<endl;
			}
			//DuLinkList z,zz;
			//z=GetElemP_DuL(L,1);
			//cout<<z->data;
			//zz=GetElemP_DuL(L,2);
			//cout<<z<<' '<<zz<<' ';
			//if(z!=zz)
			//cout<<zz->data<<endl;
			//cout<<L<<' '<<L->next->data<<' '<<L->next->next->data<<' '<<GetElemP_DuL(L,1)->data<<' '<<GetElemP_DuL(L,2)->data;
		}
	}
	return 0;
}
```
### 1M
```
#include<iostream>
#include<stdlib.h>
#include<stdio.h>
#include<cstring>
#include<string.h>
using namespace std;
void hs(char*str,int *ss,int *sss)
{
	    char *p=NULL;
		int zan;
		zan=atoi(strtok(str," "));
        for(int q=0;(p =strtok(NULL," "));q++)
		{
			if(q%2==0)
			{
				if(atoi(p)>=0)
				   ss[atoi(p)]=zan;
				else
					sss[-1*atoi(p)]=zan;
			}
			else
			{
				zan=atoi(p);
			}
		}
		return;
}

void hss(char*str,int *ss,int *sss)
{       char *p1=NULL;
        int zan1;
		zan1=atoi(strtok(str," "));
		//cout<<zan1<<endl;
        for(int q=0;(p1 =strtok(NULL," "));q++)
		{
			if(q%2==0)
			{
				if(atoi(p1)>=0)
				   ss[atoi(p1)]+=zan1;
				else
					sss[-1*atoi(p1)]+=zan1;
				//if(ss[atoi(p1)]>0)
				//    ss[atoi(p1)]+=zan1;
				//else
				//	ss[atoi(p1)]=zan1;
				//cout<<ss[atoi(p1)]<<endl;
			}
			else
			{
				zan1=atoi(p1);
				//cout<<zan1<<endl;
			}
		}
		return;
}

int main()
{
	
	char strA[500],strB[500];
	while(gets(strA) && strlen(strA))
	{
		int ss[300]={0},sss[300]={0};
		hs(strA,ss,sss);
		if(gets(strB)&& strlen(strB))
			hss(strB,ss,sss);

		int gg;
		for(int j=0;j<150;j++)
		{
			if(ss[j]!=0)
				gg=j;
		}
		//gg--;
		for(;gg>=0;gg--)
		  if(ss[gg]!=0)
			  cout<<ss[gg]<<' '<<gg<<' ';
		for(int y=0;y<300;y++)
			if(sss[y]!=0)
				cout<<sss[y]<<' '<<-1*y<<' ';
		cout<<endl;
	}
	return 0;
}
```
### 1N
```
#include<iostream>
using namespace std;
void zh(int x)
{
	if(x>=8)
	{
		
	    zh(x/8);
	    cout<<x%8;
	}
	else
		cout<<x;
}
int main()
{
	int x;
	while(cin>>x)
	{
		zh(x);
		cout<<endl;
	}
	return 0;
}
```
### 2A
```
#include<iostream>
#include<stdlib.h>
#include<cstdio>
#include<cstring>
using namespace std;
bool bijiao(char*c,char(*al)[30],int*ss,int q)
{
	for(int b=0;b<q;b++)
	{
		if(strcmp(c,al[b])==0)
		{
			ss[b]++;
			return true;
		}
	}
	return false;
}
int compare(const void*elem1,const void *elem2)
{
	return(strcmp((char*)elem1,(char*)elem2));
}
int main()
{
	int n;
	while(cin>>n)
	{
		if(n==0)
			break;
		else
		{
			int s[1002]={0};
			char all[1002][30];
			char(*a)[30]=all;
		for(int i=0;i<n;i++)
		{
			char co[30];
			cin>>co;
			if(!bijiao(co,a,s,i-1))
			{
				strcpy(all[i],co);
				s[i]=1;
			}
		}
		int m=0;
		for(int j=0;j<n;j++)
			if(s[j]>m)
				m=s[j];
		//cout<<m<<endl;
		char res[100][20];
		int qa=0;
		for(int d=0;d<n;d++)
			if(s[d]==m)
			{
				strcpy(res[qa],all[d]);
				qa++;
				//break;
			}
		qsort(res,qa,20,compare);
		for(int qaq=0;qaq<qa;qaq++)
			cout<<res[qaq]<<endl;
		}
	}
	return 0;
}
```
### 2B
```
#include<iostream>
using namespace std;
int main()
{
	int a;
	while(cin>>a)
	{
		if(!a)
			break;
		else
		{
		int n=0,res=a*5;
		while(a--)
		{
			int x;
			cin>>x;
			int xx=x-n;
			if(xx>=0)
				res+=(xx*6);
			else
				res-=(xx*4);
			n=x;
		}
		cout<<res<<endl;
		}
	}
}
```
### 2C
```
#include<iostream>
#include<cstring>
#include<stack>
using namespace std;
bool match(char a,char b)
{
	if(a=='<'&&b=='>')
		return true;
	else if(a=='('&&b==')')
		return true;
	else if(a=='['&&b==']')
		return true;
	else
		return false;
}
int main()
{
    stack<char> st;
	int x;
	cin>>x;
	while(x--)
	{
		int hong=0,lv=0,lan=0;
	      char s[1100];
          cin>>s;
		  int len=strlen(s);
		  for(int i=0;i<len;i++)
		  {
			  if(s[i]=='<'||s[i]=='('||s[i]=='[')
			  {
				  st.push(s[i]);
			  }
			  else if(s[i]=='>'||s[i]==')'||s[i]==']')
			  {
				  if(match(st.top(),s[i]))
					  st.pop();
			  }
			  else if(!st.empty())
			  {
				  if(st.top()=='<')
					  lv++;
				  else if(st.top()=='(')
					  hong++;
				  else if(st.top()=='[')
					  lan++;
			  }
		  }
		  cout<<hong<<' '<<lv<<' '<<lan<<endl;
	}
	return 0;
}
```
### 2D
```
#include<iostream>
#include<cstring>
#include<stack>
using namespace std;
int main()
{
	char s[1100];
	while(cin>>s)
	{
		stack<char> st;
		int len=strlen(s);
		for(int i=0;i<len;i++)
		{
			if(s[i]=='G')
			{
				cout<<st.size()<<endl;
				break;
			}
			if(s[i]=='(')
				st.push(s[i]);
			else if(s[i]==')')
				st.pop();
		}
	}
	return 0;
}
```
### 2E
```
#include<iostream>
using namespace std;
struct no
{
	int le;
	int ri;
	bool vi;
};
int pan(no *q,int aaa)
{
	 if(q[0].le==-1&&q[0].ri==-1)
		return 2; 
	 else if(q[0].le==-1)
		 return 0;
	 else if(q[0].ri==-1&&pan(q-aaa+q[0].le,q[0].le))
		return 3;
	
	 else if(pan(q-aaa+q[0].le,q[0].le)&&pan(q-aaa+q[0].ri,q[0].ri)&&pan(q-aaa+q[0].le,q[0].le)<=pan(q-aaa+q[0].ri,q[0].ri))
		return 1;
	 return 0;
}

int main()
{
	int n;
	cin>>n;
	while(n--)
	{
		no ss[30];
		int a;
		cin>>a;
		for(int aa=1;aa<=a;aa++)
		{
			cin>>ss[aa].le>>ss[aa].ri;
			//ss[aa].vi=false;
		}
		no *s=ss;
		int aa=1;
		for(;aa<=a;aa++)
		{   
			//cout<<s[aa].le<<' '<<s[aa].ri<<endl;
			//continue;
			if(s[aa].le==-1&&s[aa].ri!=-1)
			{
				cout<<"No"<<endl;
				break;
			}
			//if(s[aa].vi==true)
			//	continue;
			
			
			
			else if(s[aa].le==-1&&s[aa].ri==-1)
				continue;
			else if(s[aa].ri==-1)
			{
				if(pan(s+s[aa].le,s[aa].le))
					continue;
				else
				{
					cout<<"No"<<endl;
				    break;
				}
			}
			else if(pan(s+aa,aa))
				continue;
			else
			{
				cout<<"No"<<endl;
				break;
			}
		}
		if(aa==a+1)
			cout<<"Yes"<<endl;
	}
	return 0;
}
```
### 2F
```
#include<iostream>
using namespace std;
int zou1[4]={0,1,0,-1};
int zou2[4]={1,0,-1,0};
char map[10][11];
bool dfs(int ii,int jj)
{
	if(map[ii][jj]=='E')
	{
	    map[ii][jj]='*';
		return true;
	}
	else
	{
		//cout<<ii<<' '<<jj<<endl;
	    map[ii][jj]='*';
		int iii,jjj;
		int z=0;
		 for(;z<4;z++)
		  {
		    if(ii+zou1[z]>=0&&ii+zou1[z]<10&&jj+zou2[z]>=0&&jj+zou2[z]<10&&(map[ii+zou1[z]][jj+zou2[z]]==' '||map[ii+zou1[z]][jj+zou2[z]]=='E'))
		    {
			  iii=ii+zou1[z];
			  jjj=jj+zou2[z];
			 if(dfs(iii,jjj))
			 {
				 //cout<<iii<<' '<<jjj<<endl;
			   return true;
			 }
			 else
				 continue;
		    }
			
		  }
		 if(z==4)
			{
	             map[ii][jj]='!';
	             return false;

			}
	    //}
	}
	return false;
}
int main()
{
	for(int i=0;i<10;i++)
	{
		for(int j=0;j<10;j++)
			map[i][j]=getchar();
		getchar();
	}
	for(int i=0;i<10;i++)
	{
		for(int j=0;j<10;j++)
		{
			if(map[i][j]=='S')
				dfs(i,j);
		}
	}
	for(int i=0;i<10;i++)
	{
		for(int j=0;j<10;j++)
			cout<<map[i][j];
		cout<<endl;
	}
	return 0;
}
```
### 2G
```
#include<iostream>
#include<cstring>
#include<stdio.h>
#include<stack>
using namespace std;
#define OPSETSIZE 7
unsigned char Prior[7][7] = {
        { '>', '>', '<', '<', '<', '>', '>' },
        { '>', '>', '<', '<', '<', '>', '>' },
        { '>', '>', '>', '>', '<', '>', '>' },
        { '>', '>', '>', '>', '<', '>', '>' },
        { '<', '<', '<', '<', '<', '=',  ' ' },
        { '>', '>', '>', '>', ' ', '>', '>' },
        { '<', '<', '<', '<', '<', ' ', '=' } };
  
char OPSET[OPSETSIZE]= { '+', '-', '*', '/', '(', ')', '#' };
int ReturnOpOrd(char op, char* TestOp) {
    int i;
    for (i = 0; i < OPSETSIZE; i++) {
        if (op == TestOp[i])
            return i;
    }
    return 0;
}
char precede(char Aop, char Bop) {
    return Prior[ReturnOpOrd(Aop, OPSET)][ReturnOpOrd(Bop, OPSET)];
}
int In(char Test, char* TestOp) {
    int Find = 0;
    int i;
    for (i = 0; i < OPSETSIZE; i++) {
        if (Test == TestOp[i])
            Find = 1;
    }
    return Find;
}
int Operate(int a, unsigned char theta, int b) {
    switch (theta) {
    case '+':
        return a + b;
    case '-':
        return a - b;
    case '*':
        return a * b;
    case '/':
        return a / b;
    default:
        return 0;
    }
}
int EvaluateExpression(char* MyExpression) { 
    stack<char> OPTR; 
    stack<int> OPND; 
    char TempData[20];
    int Data, a, b;
    char *c, Dr[2];
    int theta;

    OPTR.push( '#');

    c = MyExpression;
    strcpy(TempData, "\0");
    while (*c != '#' || OPTR.top() != '#') {
        if (!In(*c, OPSET)) { 
            Dr[0] = *c;
            Dr[1] = '\0';
            strcat(TempData, Dr);
            c++;
            if (In(*c, OPSET)) {
                Data = atoi(TempData);
                OPND.push(Data);
                strcpy(TempData, "\0");
            }
        } else {
            switch (precede(OPTR.top(), *c)) {
            case '<': // 栈顶元素优先权低
                OPTR.push( *c);
                c++;
                break;
            case '=': // 脱括号并接收下一字符
                OPTR.pop();
                c++;
                break;
            case '>': // 退栈并将运算结果入栈
                theta=OPTR.top();
				OPTR.pop();
                b=OPND.top();
				OPND.pop();
                a=OPND.top();
				OPND.pop();
                OPND.push(Operate(a, theta, b));
                break;
            }
        }
    }
    return OPND.top();
}
  
int main(){
  
    char MyExpression[100]; 
    while(gets(MyExpression) && strlen(MyExpression)){
        printf("%d\n", EvaluateExpression(MyExpression));
    }
    return 0;
}
```
### 2H
```
#include<iostream>
#include<stdio.h>
using namespace std;
int q;
void hs(int a,char x,char y,char z)
{
	if(a==1)
		printf("%2d. Move disk %d from %c to %c\n",q++,1,x,z);
	else
	{
		hs(a-1,x,z,y);
		printf("%2d. Move disk %d from %c to %c\n",q++,a,x,z);
		hs(a-1,y,x,z);
	}
	return;
}
int main()
{
	int i;
	char x='X',y='Y',z='Z';
	while(cin>>i)
	{
		q=1;
		hs(i,x,y,z);
		cout<<endl;
	}
	return 0;
}
```
### 2I
```
#include<iostream>
#include<stdio.h>
using namespace std;
int max(int a,int b)
{
	if(a>=b)
		return a;
	else 
		return b;
}
int main()
{
	int m,to;
	while(cin>>m>>to)
	{
		double res=0.0;
		int s[30]={0},too=to;
	  while(to--)
	  {
		int d,z;
		cin>>d>>z;
		int cha=-999;
		for(int i=0;i<m;i++)
		{
			if(d-s[i]>cha)
				cha=d-s[i];
		}
		//cout<<cha<<endl;
		for(int i=0;i<m;i++)
		{
			if(cha==d-s[i])
			{
				if(cha>=0)
					s[i]=max(d+z,s[i]+z);
				else
				{
					res-=cha;
					//cout<<res<<' '<<cha<<endl;
					s[i]=max(d+z,s[i]+z);
				}
				break;
			}
		}
	  }
	  printf("%.2f\n",res/too);
	}
	return 0;
}
```
### 2J
```
#include<iostream>
#include<stdio.h>
#include<string.h>
using namespace std;
int main(){
	char a[110],b[110];
	while(cin>>a>>b)
	{
		char *s;
		if(s=strstr(a,b))
			cout<<s-a+1<<endl;
		else
			cout<<0<<endl;
	}
    return 0;
}
```
### 2K
```
#include<iostream>
#include<cstring>
using namespace std;
int main()
{
	char s[150];
	while(cin>>s)
	{
		char ss[150];
		cin>>ss;
		int ii;
		cin>>ii;
		for(int i=0;i+1<ii;i++)
			cout<<s[i];
		int len=strlen(s);
		cout<<ss;
		for(int i=ii-1;i<len;i++)
			cout<<s[i];
		cout<<endl;
	}
	return 0;
}
```
### 2L
```
#include<iostream>
#include<stdio.h>
#include<string.h>
#include<cstring>
using namespace std;
int main(){
	char a[110],b[110];
	while(cin>>a>>b)
	{
		int len1=strlen(a),len2=strlen(b);
		for(int i=0;i<len1;i++)
		{
		    int j=0;
			cout<<a[i];
			if(a[i]==b[j])
			{
				int ii=i;
				for(;a[ii]==b[j]&&j<len2;j++)
				{
					   ii++;
					   if(j+1!=len2)
				          cout<<a[ii];
				}
				if(j==len2)
				     break;
				else
				{
					continue;
				}
			}
		}
		cout<<endl;
		char *s;
        if(s=strstr(a,b))
            cout<<s-a+1<<endl;
        else
            cout<<0<<endl;
	}
    return 0;
}
```
### 2M
```
#include<iostream>
#include<cstring>
using namespace std;
void g(char *t,int *next,int len)
{
	int i=1;
	next[1]=0;
	int j=0;
	while(i<len)
	{
		if(j==0||t[i]==t[j])
		{
			++i;
			++j;
			next[i]=j;
			//cout<<j<<' ';
		}
		else
		{
			j=next[j];
			//cout<<j<<' ';
		}
	}
}

int main()
{
	char s[110];
	int next[110];
	cin>>s+1;
	int len=strlen(s);
	g(s,next,len);
	for(int i=1;i<=len-1;i++)
		cout<<next[i]<<' ';
	return 0;
}
```
### 2O
```
/*#include <stdio.h>
#define MAXSIZE 12500                           // 假设非零元个数的最大值为12500
#define OK 1
#define ERROR 0
typedef int Status;
typedef int ElemType;                           // 定义基本元素的类型为 int 型
typedef struct{
    int i, j;                                   // 该非零元的行下标和列下标
    ElemType e;
}Triple;
  
typedef struct{
    Triple data[MAXSIZE+1];                     // 非零元三元组表，data[0]未用
    int mu, nu, tu;                             // 矩阵的行数、列数和非零元个数
}TSMatrix;
  
void InputMatrix(TSMatrix &M){                  // 读入矩阵 M，r、c为该矩阵的行和列数
    int i, j;
    int data;                                   // 用来存储临时读取近来的数据
    M.tu = 0;                                   // 先将非零元地数目初始化为0
    for(i=1; i<=M.mu; i++){
        for(j=1; j<=M.nu; j++){
            scanf("%d", &data);                 // 读入元素
            if(data){                           // 如果 data 为非零元
                M.tu++;                         // 先对非零元地数目加1，因为data[0]未用
                M.data[M.tu].e = data;          // 储存非零元
                M.data[M.tu].i = i;             // 记录当前元素的行号
                M.data[M.tu].j = j;             // 记录当前元素的列号
            }
        }
    }
}
  
void OutputMatrix(TSMatrix M){                  // 输出矩阵
    int i, j;                                   // 定义迭代变量
    int t = 1;                                  // 定位需要输出矩阵中的位置
    for(i=1; i<=M.mu; i++){
        for(j=1; j<=M.nu; j++){
            if(i==M.data[t].i && j==M.data[t].j){   // 需要输出非零元
                printf("%d ", M.data[t].e);
                t++;                            // 定位下次需要输出的元素
            }else{
                printf("0 ");                   // 输出零元
            }
        }
        putchar('\n');                          // 换行
    }
}
  
Status FastTransposeSMatrix(TSMatrix M, TSMatrix &T) {  // 算法5.2
    // 采用三元组顺序表存储表示，求稀疏矩阵M的转置矩阵T
    int col, t, p, q;
    int num[200], cpot[200];
    T.mu = M.nu;  T.nu = M.mu;  T.tu = M.tu;
    if (T.tu) {
        for (col=1; col<=M.nu; ++col) num[col] = 0;
        for (t=1; t<=M.tu; ++t)                  // 求 M 中每一列所含非零元的个数
        ++num[M.data[t].j];
        cpot[1] = 1;         
        // 求 M 中每一列的第一个非零元在 b.data 中的序号
        for (col=2; col<=M.nu; ++col) cpot[col] = cpot[col-1]+num[col-1];
        for (p=1; p<=M.tu; ++p) {    
            col = M.data[p].j;   q = cpot[col];
            T.data[q].i =M.data[p].j;  T.data[q].j =M.data[p].i;
            T.data[q].e =M.data[p].e;  ++cpot[col]; 
        } // for
    } // if
    return OK;
} // FastTransposeSMatrix
  
int main() {
    TSMatrix M, T;        // 定义存储矩阵的变量
    scanf("%d%d", &M.mu, &M.nu);
    InputMatrix(M);
    FastTransposeSMatrix(M, T);
    OutputMatrix(T);
    return 0;
}*/
#include<iostream>
using namespace std;
struct D
{
	int i;
	int j;
	int e;
};
struct JZ
{
	D data[12510];
	int mu;
	int nu;
	int tu;
};
bool zhuan(JZ a,JZ &b)
{
	int p,q,col;
	b.mu=a.nu;
	b.nu=a.mu;
	b.tu=a.tu;
	if(b.tu)
	{
		q=1;
		for(col=1;col<=a.nu;++col)
			for(p=1;p<=a.tu;++p)
				if(a.data[p].j==col)
				{
					b.data[q].i=a.data[p].j;
						//cout<<b.data[q].i<<' '<<a.data[p].j<<' '<<endl;
					b.data[q].j=a.data[p].i;
					b.data[q].e=a.data[p].e;
					++q;
				}
	}
	return true;
}
int main()
{
	int r,c;
	while(cin>>r>>c)
	{
		JZ m,n;
		int x,qa=0;
		m.mu=r;
		m.nu=c;
		for(int ii=1;ii<=r;ii++)
		{
			for(int jj=1;jj<=c;jj++)
			{
				if(cin>>x&&x)
				{
					qa++;
					m.data[qa].i=ii;
					m.data[qa].j=jj;
					m.data[qa].e=x;
				}
			}
		}
		m.tu=qa;
		zhuan(m,n);
		//cout<<m.data[3].e<<' '<<m.data[3].j<<' '<<m.data[3].i<<' '<<m.data[2].e<<endl;
		//cout<<n.data[1].e<<' '<<n.data[1].i<<' '<<n.data[1].j<<' '<<n.data[2].e<<endl;
		int p=0,qaq=1;
		for(int ii=1;ii<=c;ii++)
		{
			//for(int qaq=0;m.data[qaq].i==ii;qaq++)
			//{
				for(int jj=1;jj<=r;jj++)
				{
				  if(n.data[qaq].i==ii&&n.data[qaq].j==jj)
				  {
					cout<<n.data[qaq].e<<' ';
					qaq++;
				  }
				  else
					cout<<0<<' ';
				}
				cout<<endl;
			//}
		}
	}
	return 0;
}
```
### 3F
```
#include<iostream>
#include<stdio.h>
using namespace std;
struct node{
	node *le;
	node *ri;
	char i;
};
void qian(node *a)
{
	if(a!=NULL)
	{
	  cout<<(*a).i<<' ';
	  if((*a).le!=NULL)
	       qian((*a).le);
	  if((*a).ri!=NULL)
	      qian((*a).ri);
	}
	return;
}
void zhong(node *a)
{
	if(a!=NULL)
	{
	  if((*a).le!=NULL)
	       zhong((*a).le);
	  cout<<(*a).i<<' ';
	  if((*a).ri!=NULL)
	      zhong((*a).ri);
	}
	return;
}
void hou(node *a)
{
	if(a!=NULL)
	{
	  if((*a).le!=NULL)
	       hou((*a).le);
	  if((*a).ri!=NULL)
	      hou((*a).ri);
	  cout<<(*a).i<<' ';
	}
	return;
}
node *t=new node;
void zao(node *tt,char q)
{
	 (*tt).i=q;
	 char a,b;
	 scanf("%c",&a);
	 if(a==' ')
		 (*tt).le=NULL;
	 else
	 {
	     (*tt).le=new node;
          zao((*tt).le,a);
	 }
	 scanf("%c",&b);
	 if(b==' ')
		 (*tt).ri=NULL;
	 else
	 {
	     (*tt).ri=new node;
          zao((*tt).ri,b);
	 }
	 return;
}
int main()
{
	char a;
	scanf("%c",&a);
	zao(t,a);
	qian(t);
	cout<<endl;
	zhong(t);
	cout<<endl;
	zhong(t);
	cout<<endl;
	return 0;
}
```
作为一只程序猿，想必还是要和西加加打交道哒啦~待续吧
<br>