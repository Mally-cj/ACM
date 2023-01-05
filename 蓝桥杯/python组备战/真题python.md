《卡片》真题演习

```
fau=0
mp=[2021]*10
ans=0
for i in range(20220):
    a=i
    
    while a!=0:
        b=int(a%10)
        if mp[b]>0:
            mp[b]=mp[b]-1
            a//=10
        else:
            fau=1
            break
    if fau:
        ans=i-1
        break
    

print(ans)

```

