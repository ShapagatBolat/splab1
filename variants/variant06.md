### Variant 06
Output the following information:

* Top 10 dates as per number of downloaded bytes
* The number of request for each of the dates
* The percentage of requests for each of the dates

Sample output:

```
1. 2006-10-18 - 1200 - 36%   
2. 2006-10-01 - 1130 - 34%
3. 2006-10-02 - 1000 - 30%
```






#!/bin/bash  

sum=$(cut -f4 -f10 -d' ' $1| awk ' {if (substr($1, 1, 12)in arr) { arr[substr($1, 1, 12)]++;} else {arr[substr($1, 1, 12)]=$2}} END { for (i in arr) print arr[i],i,k += arr[i]}'|awk '{print substr($2,2,12),"-", $1,"-", $3,"%"}'|tail -r -1|awk '{print $5}')

arr=$(cut -f4 -f10 -d' ' $1|  awk ' {if (substr($1, 1, 12)in arr) { arr[substr($1, 1, 12)]++;} else {arr[substr($1, 1, 12)]=$2}} END { for (i in arr) print arr[i],i,arr[i]*100}'| awk '{print $3}'| sort  -k1n| tail -r -10)
arr1=$(cut -f4 -f10 -d' ' log.txt |  awk ' {if (substr($1, 1, 12)in arr) { arr[substr($1, 1, 12)]++;} else {arr[substr($1, 1, 12)]=$2}} END { for (i in arr) print arr[i],i }'| sort  -k1n| tail -r -10|awk '{print substr($2,2,12),"-", $1}')
 


arr2=$(for x in $arr; do echo "$(expr $x / $sum ).$(expr $x % $sum )"; done;)
echo $arr2

for ((i=0;i<${#arr[@]};i++))
do
    echo ${arr1[$i]} ${arr2[$i]};

done

