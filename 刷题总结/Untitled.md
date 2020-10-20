只去除两个之间间隔的竖线

```
//v[X]表示x这条竖线对答案的贡献值

if spce[x]==0
{
	//左边的线
	if(h>h[x-1]){
		ans+=h-h[x-1];
		h[x-1]=h;
		
	}else{
	ans-=h-h[x-1];
	}
	
	//右边的线
	if(h>h[x]){
		ans+=h-h[x];
		h[x]=h;
		
	}else{
	ans-=h-h[x];
	}  
}
else if(spce[x]==1)
{
	if(spce[x]>=h)continue;
	else if(space[x]<=h)
	{
		ans-=v[x-1];
		v[x-1]=abs(h-h[x-1]);
		ans+=v[x-1];
		h[x-1]=h;
		
		ans-=v[x];
		v[x]=abs(h-h[x]);
		ans+=v[x];
		h[x]=h;
	}
}
```

