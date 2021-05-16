#include<bits/stdc++.h>
using namespace std;
#define ll long long int
 
ll a[1000005];
ll seg[2*1000005];
 
 
void build(ll ind , ll low,ll high){
    if(low==high){
        seg[ind] = a[low];
        return ;
    }
    
    ll mid = (low+high)/2;
    build(2*ind+1,low,mid);
    build(2*ind+2,mid+1,high);
    
    seg[ind] = seg[2*ind+1]+ seg[2*ind+2];
}
 
ll  rangeSum(ll ind,ll low,ll high,ll a,ll b){
    //no overlap 
    //a b low high || low high a b
    if( b < low || a >high){
        return 0;
    }
    // complete overlap 
    //low a b high
    if(a<=low && high<=b){
         return seg[ind];
    }
    //partial over lap goto left and goto right the compute
    ll mid = (low+high)>>1;
    ll left = rangeSum(2*ind+1,low,mid,a,b);
    ll right = rangeSum(2*ind+2,mid+1,high,a,b);
    return left+ right;
}
 
 
int main(){
    ll n,m;
    cin>>n>>m;
    // ll a[n];
    for(ll i = 0;i<n;i++){
        cin>>a[i];
    }
    
    //  for(int i = 0;i<n;i++){
    //     cout<<a[i]<<" ";
    // }
    
    build(0,0,n-1);
    // for(int i = 0;i<2*n;i++){
    //     cout<<seg[i]<<" ";
    // }
    // cout<<"\n";
    while(m--){
        ll  a,b;
        cin>>a>>b;
        a--;
        b--;
        ll ans = rangeSum(0,0,n-1,a,b);
        cout<<ans<<"\n";
    }
    
}
