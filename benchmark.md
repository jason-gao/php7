## benchmark
* hello world
* php5.6 vs php7.2.1
* 127.0.0.1 php56.vm
* 127.0.0.1 php721.vm

* 配置
* centos6 vm |Mem 2G |cpu cores 2

## nginx conf
* php5.6.conf

```
server {
    listen       80;
    server_name  php56.vm;
    access_log  /var/log/nginx/php56.vm.access.log;
    error_log   /var/log/nginx/php56.vm.error.log;
    root /usr/local/src/phpCode/;
    index index.php index.html index.htm;


    location ~ \.php$ {
        fastcgi_pass   127.0.0.1:9007;
        fastcgi_index  index.php;
        include fastcgi.conf;
        include fastcgi_params;
    }

}

```
* php php7.2.1.conf
```
server {
    listen       80;
    server_name  php721.vm;
    access_log  /var/log/nginx/php721.vm.access.log;
    error_log   /var/log/nginx/php721.vm.error.log;
    root /usr/local/src/phpCode/;
    index index.php index.html index.htm;


    location ~ \.php$ {
        fastcgi_pass   127.0.0.1:9007;
        fastcgi_index  index.php;
        include fastcgi.conf;
        include fastcgi_params;
    }

}

```

* ab -c10 -n50000 http://php56.vm/
```
This is ApacheBench, Version 2.3 <$Revision: 655654 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking php56.vm (be patient)
Completed 5000 requests
Completed 10000 requests
Completed 15000 requests
Completed 20000 requests
Completed 25000 requests
Completed 30000 requests
Completed 35000 requests
Completed 40000 requests
Completed 45000 requests
Completed 50000 requests
Finished 50000 requests


Server Software:        nginx/1.8.1
Server Hostname:        php56.vm
Server Port:            80

Document Path:          /
Document Length:        11 bytes

Concurrency Level:      10
Time taken for tests:   6.996 seconds
Complete requests:      50000
Failed requests:        0
Write errors:           0
Total transferred:      8650000 bytes
HTML transferred:       550000 bytes
Requests per second:    7147.38 [#/sec] (mean)
Time per request:       1.399 [ms] (mean)
Time per request:       0.140 [ms] (mean, across all concurrent requests)
Transfer rate:          1207.52 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.1      0       8
Processing:     0    1   0.5      1       9
Waiting:        0    1   0.5      1       9
Total:          1    1   0.5      1      15

Percentage of the requests served within a certain time (ms)
  50%      1
  66%      1
  75%      2
  80%      2
  90%      2
  95%      2
  98%      3
  99%      3
 100%     15 (longest request)
```
* ab -c10 -n50000 http://php721.vm/
```
This is ApacheBench, Version 2.3 <$Revision: 655654 $>
Copyright 1996 Adam Twiss, Zeus Technology Ltd, http://www.zeustech.net/
Licensed to The Apache Software Foundation, http://www.apache.org/

Benchmarking php721.vm (be patient)
Completed 5000 requests
Completed 10000 requests
Completed 15000 requests
Completed 20000 requests
Completed 25000 requests
Completed 30000 requests
Completed 35000 requests
Completed 40000 requests
Completed 45000 requests
Completed 50000 requests
Finished 50000 requests


Server Software:        nginx/1.8.1
Server Hostname:        php721.vm
Server Port:            80

Document Path:          /
Document Length:        11 bytes

Concurrency Level:      10
Time taken for tests:   7.828 seconds
Complete requests:      50000
Failed requests:        0
Write errors:           0
Total transferred:      8800000 bytes
HTML transferred:       550000 bytes
Requests per second:    6387.28 [#/sec] (mean)
Time per request:       1.566 [ms] (mean)
Time per request:       0.157 [ms] (mean, across all concurrent requests)
Transfer rate:          1097.81 [Kbytes/sec] received

Connection Times (ms)
              min  mean[+/-sd] median   max
Connect:        0    0   0.0      0       1
Processing:     0    2   0.7      1      22
Waiting:        0    2   0.7      1      22
Total:          0    2   0.7      1      22
WARNING: The median and mean for the processing time are not within a normal deviation
        These results are probably not that reliable.
WARNING: The median and mean for the waiting time are not within a normal deviation
        These results are probably not that reliable.
WARNING: The median and mean for the total time are not within a normal deviation
        These results are probably not that reliable.

Percentage of the requests served within a certain time (ms)
  50%      1
  66%      2
  75%      2
  80%      2
  90%      2
  95%      3
  98%      3
  99%      3
 100%     22 (longest request)

```