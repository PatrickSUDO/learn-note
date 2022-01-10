---
tags: 
  - java
  - spring
---





As the others have mentioned both Spring RestTemplate and Jersey Rest Client will do the job. I have used both. Both them work great with Jackson and IIRC they will automatically use it if found (spring for sure).

There is one advantage I like about Spring RestTemplate is that you can plugin Commons HTTP as the transport. So if you had some weird headers, cookies, timeout, threading you can configure Commons HTTP and then put it into the RestTemplate.