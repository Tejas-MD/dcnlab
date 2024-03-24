# Program 2: 

``` awk
BEGIN{
 ctcp=0;
 cudp=0;
}
{
   pkt=$5;
if(pkt=="cbr"){cudp++;}
if(pkt=="tcp"){ctcp++;}
}
END{
printf("TCP=%d\n UDP=%d\n",ctcp,cudp);
}
```

# Program 3: 

``` awk
BEGIN{
pkt=0;
time=0;
}
{
if($1=="r" && $3=="3" && $4=="4")
{
pkt = pkt + $6;
time =$2;
}
}
END{
printf("throughput:%fMbps",(( pkt / time) * (8 / 1000000)));
}
```


# Program 4: 

``` tcl
BEGIN {
}
{
if($6=="cwnd_") 
printf("%f\t%f\t\n",$1,$7); 
}
END {
}
```
### Commands:
``` bash
$ awk -f program4.awk file1.tr > a1
$ awk -f program4.awk file2.tr > a2
$ xgraph a1 a2
```


# Program 6: 

``` awk
BEGIN{
count1=0
count2=0
pack1=0
pack2=0
time1=0
time2=0
}
{
if($1=="r"&& $3=="_1_" && $4=="AGT")
{
count1++
pack1=pack1+$8
time1=$2
}
if($1=="r" && $3=="_2_" && $4=="AGT")
{
count2++
pack2=pack2+$8
time2=$2
}
}
END{
printf("\n **************************************************************************\n");
printf("The Throughput from n0 to n1: %f Mbps \n", ((pack1*8)/(time1*1000000)));
printf("The Throughput from n1 to n2: %f Mbps \n", ((pack2*8)/(time2*1000000))); 
printf("\n **************************************************************************\n");
}
```


## Prog 1 and 5 : 
``` bash
grep -c "^d" out.tr
```