# poj-3279
#include<iostream>
#include<algorithm>
#include<vector>
#include<queue>
#include<map>
#include<set>
#include<string.h>
#include<stack>
#include<cstdio>
#include<cmath>
#include<iomanip>
using namespace std;
 
typedef long long ll;
typedef long double ld;
typedef pair<int,int> P;
typedef pair<int,P> P1;
 
#define fr first
#define sc second
#define mp make_pair
#define pb push_back
#define rep(i,x) for(int i=0;i<x;i++)
#define rep1(i,x) for(int i=1;i<=x;i++)
#define rrep(i,x) for(int i=x-1;i>=0;i--)
#define rrep1(i,x) for(int i=x;i>0;i--)
#define so(v) sort(v.begin(),v.end())
#define re(s) reverse(s.begin(),s.end())
#define lb(v,a) lower_bound(v.begin(),v.end(),a)
#define ub(v,a) upper_bound(v.begin(),v.end(),a)
#define mp1(a,b,c) P1(a,P(b,c))
 
const int INF=1000000000;
const int dir_4[4][2]={{1,0},{0,1},{-1,0},{0,-1}};
const int dir_8[8][2]={{1,0},{1,1},{0,1},{-1,1},{-1,0},{-1,-1},{0,-1},{1,-1}};
const ll mod=1e9+7;
 
ll mod_pow(ll x,ll k){
  ll res=1;
  for(;k;k/=2,x=x*x%mod) if(k&1) res=res*x%mod;
  return res;
}

int m,n,tile[20][20],flip[20][20],opt[20][20];
int dy[5]={0,1,0,-1,0};
int dx[5]={-1,0,0,0,1};

int get(int Y, int X){

  int c=tile[Y][X];

  for(int i=0;i<5;i++){
    int y=Y+dy[i],x=X+dx[i];
    if(y>=0&&y<m&&x>=0&&x<n) c+=flip[y][x];
  }
  return c%2;
}

int calc(){

  for(int i=1;i<m;i++)
    for(int j=0;j<n;j++)
      if(get(i-1,j)) flip[i][j]=1;

  for(int i=0;i<n;i++) if(get(m-1,i)) return -1;

  int res=0;
  for(int i=0;i<m;i++)
    for(int j=0;j<n;j++) 
      res+=flip[i][j];

  return res;
}

int main(){
  
  int res=-1;
  
  cin>>m>>n;
  for(int i=0;i<m;i++)
    for(int j=0;j<n;j++) cin>>tile[i][j];

  for(int i=0;i<1<<n;i++){
    memset(flip,0,sizeof(flip));
    for(int j=0;j<n;j++) flip[0][n-1-j]=(i>>j)&1;
    int num=calc();
    if(num>=0&&(res<0||num<res)){
      res=num;
      memcpy(opt,flip,sizeof(flip));
    }
  }

  if(res<0) cout<<"IMPOSSIBLE"<<endl;
  else 
    for(int i=0;i<m;i++){
      for(int j=0;j<n;j++) cout<<opt[i][j]<<" ";
      cout<<endl;
    }
  return 0;
}
   
