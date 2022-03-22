1.
        HTTP/1.1 301 Moved Permanently
        cache-control: no-cache, no-store, must-revalidate
        location: https://stackoverflow.com/questions
        x-request-guid: 25a64278-4427-44e9-9f4e-e080ab338b89
        feature-policy: microphone 'none'; speaker 'none'
        content-security-policy: upgrade-insecure-requests; frame-ancestors 'self' https://stackexchange.com
        Accept-Ranges: bytes
        Date: Tue, 22 Mar 2022 15:33:20 GMT
        Via: 1.1 varnish
        Connection: close
        X-Served-By: cache-bma1669-BMA
        X-Cache: MISS
        X-Cache-Hits: 0
        X-Timer: S1647963201.633618,VS0,VE101
        Vary: Fastly-SSL
        X-DNS-Prefetch-Control: off
        Set-Cookie: prov=2eaa451c-a6c7-635f-7852-4f03e0820ca2; domain=.stackoverflow.com; expires=Fri, 01-Jan-2055 00:00:00 GMT; path=/; HttpOnly

        Connection closed by foreign host.
 Установлен перманентный 301 редирект на https://stackoverflow.com/questions
 
2.
        Request URL: https://stackoverflow.com/
        Request Method: GET
        Status Code: 200 
        Remote Address: 151.101.193.69:443
        Referrer Policy: strict-origin-when-cross-origin
        accept-ranges: bytes
        cache-control: private
        content-encoding: gzip
        content-security-policy: upgrade-insecure-requests; frame-ancestors 'self' https://stackexchange.com
        content-type: text/html; charset=utf-8
        date: Tue, 22 Mar 2022 15:42:02 GMT
        feature-policy: microphone 'none'; speaker 'none'
        strict-transport-security: max-age=15552000
        vary: Accept-Encoding,Fastly-SSL
        via: 1.1 varnish
        x-cache: MISS
        x-cache-hits: 0
        x-dns-prefetch-control: off
        x-frame-options: SAMEORIGIN
        x-request-guid: 6bce9b4a-8698-4d38-a413-838b926aaaad
        x-served-by: cache-bma1679-BMA
        x-timer: S1647963722.059157,VS0,VE105
        :authority: stackoverflow.com
        :method: GET
        :path: /
        :scheme: https
        accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
        accept-encoding: gzip, deflate, br
        accept-language: ru-RU,ru;q=0.9,en-US;q=0.8,en;q=0.7
        cache-control: max-age=0
        cookie: prov=4f6ef703-e4e0-1d1a-8f83-22b75aa69a46; _ga=GA1.2.2056556746.1647963686; _gid=GA1.2.1349403552.1647963686; _gat=1
        dnt: 1
        sec-ch-ua: " Not A;Brand";v="99", "Chromium";v="99", "Google Chrome";v="99"
        sec-ch-ua-mobile: ?0
        sec-ch-ua-platform: "Windows"
        sec-fetch-dest: document
        sec-fetch-mode: navigate
        sec-fetch-site: none
        sec-fetch-user: ?1
        upgrade-insecure-requests: 1
        user-agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.74 Safari/537.36
Первый запрос обрабатывался дольше всего: 486 мс

<img src="https://i.ibb.co/BP8N8KH/5-1-1.jpg"></img>

3.
        vagrant@vagrant:~$ curl ipinfo.io/ip
        95.29.44.229

4.
        vagrant@vagrant:~$ whois 95.29.44.229
        inetnum:        95.24.0.0 - 95.30.255.255
        netname:        BEELINE-BROADBAND
        descr:          Dynamic IP Pool for broadband customers
        country:        RU
        <...>
        origin:         AS8402
5.
        vagrant@vagrant:~$ traceroute -IAn 8.8.8.8
        traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
         1  10.0.2.2 [*]  0.320 ms  0.288 ms  0.276 ms
         2  192.168.88.1 [*]  2.449 ms  2.571 ms  10.167 ms
         3  * * *
         4  78.107.38.144 [AS8402]  11.925 ms  12.141 ms  12.207 ms
         5  85.21.225.13 [AS8402]  19.669 ms  20.871 ms  20.905 ms
         6  78.107.184.250 [AS8402]  20.609 ms * *
         7  195.14.32.22 [AS8402]  13.912 ms  13.431 ms  14.005 ms
         8  108.170.250.33 [AS15169]  15.809 ms  16.134 ms  35.764 ms
         9  108.170.250.51 [AS15169]  14.737 ms  15.006 ms  15.075 ms
        10  142.251.49.158 [AS15169]  35.851 ms * *
        11  216.239.57.222 [AS15169]  36.068 ms  36.356 ms  32.001 ms
        12  142.250.56.129 [AS15169]  28.422 ms  31.724 ms  27.336 ms
        13  * * *
        14  * * *
        15  * * *
        16  * * *
        17  * * *
        18  * * *
        19  * * *
        20  * * *
        21  * * *
        22  * * *
        23  * * *
        24  8.8.8.8 [AS15169]  25.151 ms  25.525 ms  25.514 ms
6.
         My traceroute  [v0.93]
        vagrant (10.0.2.15)                                                                            2022-03-22T16:38:31+0000
        Keys:  Help   Display mode   Restart statistics   Order of fields   quit
                                                                                       Packets               Pings
         Host                                                                        Loss%   Snt   Last   Avg  Best  Wrst StDev
         1. AS???    10.0.2.2                                                         0.0%    44    0.9   0.7   0.1   1.2   0.2
         2. AS???    192.168.88.1                                                     0.0%    44    3.0  11.2   1.4 141.6  29.0
         3. AS8402   83.102.255.42                                                   72.1%    44    3.0   4.6   3.0   6.7   1.1
         4. AS8402   78.107.38.144                                                    0.0%    44    4.9   9.9   3.1  85.3  16.2
         5. AS8402   85.21.225.13                                                     0.0%    44   13.1  15.0  10.7  42.5   7.3
         6. AS8402   78.107.184.250                                                  97.7%    44   21.6  21.6  21.6  21.6   0.0
         7. AS8402   195.14.32.22                                                     0.0%    44   14.1  16.6  11.9  77.6  10.9
         8. AS15169  108.170.250.33                                                   0.0%    44   14.7  20.7  12.9 185.6  26.4
         9. AS15169  108.170.250.51                                                  20.5%    44   13.7  23.3  12.0 142.4  27.3
        10. AS15169  142.251.49.158                                                  29.5%    44   26.0  33.5  24.9  98.5  18.4
        high delay 11. AS15169  216.239.57.222                                        0.0%    44   29.2  44.7  28.1 219.3  42.9
        12. AS15169  142.250.56.129                                                   0.0%    44   27.7  36.0  26.0 176.2  27.2
        13. (waiting for reply)
        14. (waiting for reply)
        15. (waiting for reply)
        16. (waiting for reply)
        17. (waiting for reply)
        18. (waiting for reply)
        19. (waiting for reply)
        20. (waiting for reply)
        21. (waiting for reply)
        22. (waiting for reply)
        23. (waiting for reply)
        24. AS15169  8.8.8.8                                                          0.0%    43   26.8  28.0  24.7  74.3   7.9
7.
        vagrant@vagrant:~$ dig NS gmail.com

        ; <<>> DiG 9.16.1-Ubuntu <<>> NS gmail.com
        ;; global options: +cmd
        ;; Got answer:
        ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 39469
        ;; flags: qr rd ra; QUERY: 1, ANSWER: 4, AUTHORITY: 0, ADDITIONAL: 1

        ;; OPT PSEUDOSECTION:
        ; EDNS: version: 0, flags:; udp: 65494
        ;; QUESTION SECTION:
        ;gmail.com.                     IN      NS

        ;; ANSWER SECTION:
        gmail.com.              345600  IN      NS      ns2.google.com.
        gmail.com.              345600  IN      NS      ns4.google.com.
        gmail.com.              345600  IN      NS      ns3.google.com.
        gmail.com.              345600  IN      NS      ns1.google.com.
        
        vagrant@vagrant:~$ dig gmail.com

        ; <<>> DiG 9.16.1-Ubuntu <<>> gmail.com
        ;; global options: +cmd
        ;; Got answer:
        ;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 2093
        ;; flags: qr rd ra; QUERY: 1, ANSWER: 4, AUTHORITY: 0, ADDITIONAL: 1

        ;; OPT PSEUDOSECTION:
        ; EDNS: version: 0, flags:; udp: 65494
        ;; QUESTION SECTION:
        ;gmail.com.                     IN      A

        ;; ANSWER SECTION:
        gmail.com.              1359    IN      A       64.233.165.19
        gmail.com.              1359    IN      A       64.233.165.18
        gmail.com.              1359    IN      A       64.233.165.17
        gmail.com.              1359    IN      A       64.233.165.83
8.
        vagrant@vagrant:~$ dig -x  64.233.165.19
        
        ;; ANSWER SECTION:
        19.165.233.64.in-addr.arpa. 86400 IN    PTR     lg-in-f19.1e100.net.       

        
        vagrant@vagrant:~$ dig -x  64.233.165.18

        
        ;; ANSWER SECTION:
        18.165.233.64.in-addr.arpa. 68178 IN    PTR     lg-in-f18.1e100.net.

      
        vagrant@vagrant:~$ dig -x  64.233.165.17

        
        ;; ANSWER SECTION:
        17.165.233.64.in-addr.arpa. 86400 IN    PTR     lg-in-f17.1e100.net.


        vagrant@vagrant:~$ dig -x  64.233.165.83

       
       
        ;; ANSWER SECTION:
        83.165.233.64.in-addr.arpa. 81638 IN    PTR     lg-in-f83.1e100.net.

 
