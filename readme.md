#### My favorite date format

    date "+%Y%m%d-%H%M%S"

#### Swap two colon-separated columns
    perl -p -e 's/(.*):(.*)/$2:$1/'

#### Combination of cut and grep using perl
Greps for all lines whose fifth field (tab separated) matches a regular expression.

    cat file.txt | perl -F"\t" -ane 'print if $F[5] =~ /^2015061/'

#### Pattern based cut

    perl -nE '/<id>(AMQ.+)<\/id>/; say $1'

#### List files with creation time
    
    ls -c
    ls -ltrc

#### Remove old files

    find . -mtime +167 -exec rm {} \;

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

#### Last reboot of Linux (Option 1)

    > uptime
    21:27:39 up 1 day,  1:34, 28 users,  load average: 3.02, 2.77, 2.40

#### Last reboot of Linux (Option 2)

    > last reboot | head
    reboot   system boot  2.6.32-754.29.1. Wed Jun  3 19:53 - 09:50 (1+13:57)   
    reboot   system boot  2.6.32-754.28.1. Thu Apr 23 02:08 - 19:43 (41+17:35)  
    reboot   system boot  2.6.32-754.25.1. Wed Mar 11 19:15 - 22:37 (42+02:22)
    
#### Environment variables of a Linux process

    cat /proc/<pid>/environ           (e.g. SHELL_OWNER=testuser)

    
