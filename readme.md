#### Last reboot of Linux
```
> uptime
21:27:39 up 1 day,  1:34, 28 users,  load average: 3.02, 2.77, 2.40
```
#### Combination of cut and grep using perl
Greps for all lines whose fifth field (tab separated) matches a regular expression.
```
cat file.txt | perl -F"\t" -ane 'print if $F[5] =~ /^2015061/'
```  
#### Pattern based cut
```
perl -nE '/<id>(AMQ.+)<\/id>/; say $1'
```
#### List files with creation time
```ls -c
ls -ltrc```
#### Remove old files
```find . -mtime +167 -exec rm {} \;```
#### Count occurences using uniq -c
    cat someFiles | 
        grep 'userName' | 
        cut -c 15-22 | 
        sort | 
        uniq -c
#### Count occurences using perl including sorting of results
    cat someFiles | 
        grep 'userName' | 
        cut -c 15-22 | 
        perl -nE 'chomp; 
            $count{$_}++; 
            END { say join "\t", $_, $count{$_} foreach sort { $count{$b} <=> $count{$a} } keys %count }'
#### Other Perl
    perl -nE 'chomp; 
        ($month) = /(\d{6})/; $count{$month}++; 
        END { say join "\t", $_, $count{$_} foreach sort keys %count }' someFile
        
### Grep in a huge number of files
    > find . | xargs grep -c 4694799288 | grep -v '0$'
    ./20180629103427317_000001056872016998858496.txt:1
