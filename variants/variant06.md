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
cut -f4 -f10 -d' ' log.txt |  awk ' {if (substr($1, 1, 12)in arr) { arr[substr($1, 1, 12)]++;} else {arr[substr($1, 1, 12)]=$2}} END { for (i in arr) print arr[i],i,arr[i]*100/541881 }'| sort  -k1n| tail -r -10|awk '{print substr($2,2,12),"-", $1,"-", $3,"%"}'
