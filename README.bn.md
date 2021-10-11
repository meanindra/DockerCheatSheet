> This repository is trending on Github since some days now. Watch it, we will add many updates in the future. 
> Thank you for your support.

[ওয়েবসাইট](http://dockercheatsheet.painlessdocker.com) চেক করুন।
* অন্যান্য ভাষায় এটি পড়ুন: [ইংরেজি](README.md), [রাশিয়ান](README.ru.md), [ফার্সি](README.fa.md), [চীনা](README.zh.md)*

# সূচীপত্র এর টেবিল

  * [ইনস্টলেশন](#সূচীপত্র)
  * [ডকার রেজিস্ট্রি এবং সংগ্রহস্থল](#ডকার-রেজিস্ট্রি-এবং-সংগ্রহস্থল)
  * [চালু কনটেইনার](#চালু-কনটেইনার)
  * [কনটেইনার শুরু এবং বন্ধ করা](#কনটেইনার-শুরু-এবং-বন্ধ-করা)
  * [কনটেইনার সম্পর্কে তথ্য পাওয়া](#কনটেইনার-সম্পর্কে-তথ্য-পাওয়া)
  * [নেটওয়ার্কিং](#নেটওয়ার্কিং)
    * [নিরাপত্তা](#নিরাপত্তা)
  * [ডকার পরিস্কার করা](#ডকার-পরিস্কার-করা)
  * [ডকার সোয়ার্ম](#ডকার-সোয়ার্ম)
  * [মন্তব্য](#মন্তব্য)
  
# চূড়ান্ত ডকার চিট শীট

# ইনস্টলেশন

## লিনাক্স

আরো তথ্যের জন্য, এখানে [দেখুন](https://docs.docker.com/install/#server)

```
curl -sSL https://get.docker.com/ | sh
```

## ম্যাক

আরো তথ্যের জন্য, এখানে [দেখুন](https://docs.docker.com/docker-for-mac/install/)

dmg ডাউনলোড করতে এই লিঙ্কটি ব্যবহার করুন।

```
https://download.docker.com/mac/stable/Docker.dmg
```

ডাউনলোড করা ফাইলটি খুলুন এবং ইনস্টলেশন নির্দেশাবলী অনুসরণ করুন।

## উইন্ডোজ

আরো তথ্যের জন্য, এখানে [দেখুন](https://docs.docker.com/docker-for-windows/install/)

msi ইনস্টলার ব্যবহার করুন:

```
https://download.docker.com/win/stable/InstallDocker.msi
```

ডাউনলোড করা ফাইলটি খুলুন এবং ইনস্টলেশন নির্দেশাবলী অনুসরণ করুন।

# ডকার রেজিস্ট্রি এবং সংগ্রহস্থল

## একটি রেজিস্ট্রিতে লগইন করুন

```
docker login
```

```
docker login localhost:8080
```

## একটি রেজিস্ট্রি থেকে লগ আউট করুন

```
docker logout
```

```
docker logout localhost:8080
```

## একটি ইমেজ সার্চ করা

```
docker search nginx
```

```
docker search --filter stars=3 --no-trunc nginx
```

## একটি ইমেজ পুল করা


```
docker image pull nginx
```

```
docker image pull eon01/nginx localhost:5000/myadmin/nginx
```

## একটি ইমেজ পুশ করা

```
docker image push eon01/nginx
```

```
docker image push eon01/nginx localhost:5000/myadmin/nginx
```

# চালু কনটেইনার

## একটি সাধারণ কনটেইনার তৈরি করুন এবং চালান

> -একটি [ubuntu:latest](https://hub.docker.com/_/ubuntu/) ইমেজ শুরু করুন
>  - **কন্টেইনার** এর পোর্ট `80` এর সাথে **হোস্ট** এর পোর্ট `80` সংলঙ্গন করুন
>  - কন্টেইনার- এ `/data`-তে বর্তমান ডিরেক্টরি মাউন্ট করুন
>  - দ্রষ্টব্য: **উইন্ডোজ** এ আপনাকে `-v ${PWD}:/data` কে`-v "C:\Data":/data` তে পরিবর্তন করতে হবে

```
docker container run --name infinite -it -p 3000:80 -v ${PWD}:/data ubuntu:latest
```

## একটি কনটেইনার তৈরি করা

```
docker container create -t -i eon01/infinite --name infinite
```

## একটি কনটেইনার চালানো

```
docker container run -it --name infinite -d eon01/infinite
```

## পুনরায় একটি কনটেইনার নামকরণ

```
docker container rename infinite infinity
```

## একটি কনটেইনার সরানো

```
docker container rm infinite
```
একটি কন্টেইনার ```docker stop``` কমান্ড ব্যবহার করে বন্ধ করার পরেই সরানো যেতে পারে। এটি এড়াতে, কনটেইনার চালানোর সময় "--rm" ফ্ল্যাগ যুক্ত করুন।

## একটি কনটেইনার আপডেট করা

```
docker container update --cpu-shares 512 -m 300M infinite
```

## একটি চলমান কনটেইনার একটি কমান্ড চালানো
```
docker exec -it infinite sh
```
উপরের উদাহরণে, ```bash``` এর বিকল্প হিসাবে ```sh``` ব্যবহার করা যেতে পারে (যদি উপরেরটি একটি ত্রুটি দেয়)।

# কনটেইনার শুরু এবং বন্ধ করা

## শুরু করা
```
docker container start nginx
```

## বন্ধ করা
```
docker container stop nginx
```

## পুনরায় শুরু করা
```
docker container restart nginx
```

## বিরাম করা
```
docker container pause nginx
```

## বিরামহীন করা

```
docker container unpause nginx
```

## কনটেইনার ব্লক করা

```
docker container wait nginx
```

## একটি SIGKILL পাঠানো

```
docker container kill nginx
```

## আরেকটি সিগন্যাল পাঠানো


```
docker container kill -s HUP nginx
```

## একটি বিদ্যমান কনটেইনার সংযুক্ত করা

```
docker container attach nginx
```


# কনটেইনার সম্পর্কে তথ্য পাওয়া

## চলমান কন্টেইনার থেকে

সংক্ষিপ্ত উপায়:
Shortest way:        
```
docker ps
```
বিকল্প উপায়:
```
docker container ls
```

## সব কন্টেইনার থেকে
```
docker ps -a
```
```
docker container ls -a
```

## কন্টেইনার লগ
```
docker logs infinite
```

## 'tail -f' কন্টেইনার এর লগ

```
docker container logs infinite -f
```

## কন্টেইনার পর্যবেক্ষণ

```
docker container inspect infinite
```

```
docker container inspect --format '{{ .NetworkSettings.IPAddress }}' $(docker ps -q)
```

## কন্টেইনার এর ঘটনাবলী

```
docker system events infinite
```

## পাবলিক পোর্টস

```
docker container port infinite
```

## চলমান প্রসেস

```
docker container top infinite
```

## কন্টেইনার এর রিসোর্স ব্যবহার

```
docker container stats infinite
```

## একটি কন্টেইনার ফাইল সিস্টেমে ফাইল বা ডিরেক্টরিগুলির পরিবর্তনগুলি পরিদর্শন

```
docker container diff infinite
```

## ইমেজ পরিচালনা করা

### বর্তমান ডিরেক্টরিতে একটি ডকারফিল থেকে


```
docker build .
```

### একটি রিমোট GIT রিপোসিটোরি থেকে

```
docker build github.com/creack/docker-firefox
```

### একটি প্রসঙ্গ নির্দিষ্ট করার পরিবর্তে, আপনি URL এ একটি ডকারফিল পাস করতে পারেন অথবা STDIN এর মাধ্যমে ফাইলটি পাইপ করতে পারেন

```
docker build - < Dockerfile
```

```
docker build - < context.tar.gz
```

### বিল্ডিং এবং ট্যাগিং

```
docker build -t eon/infinite .
```

### তৈরি করা এর প্রসঙ্গ উল্লেখ করার সময় একটি ডকারফিল তৈরি করা

```
docker build -f myOtherDockerfile .
```

### একটি রিমোট ডকারফিল URI থেকে  তৈরি করা

```
curl example.com/remote/Dockerfile | docker build -f - .
```

## একটি ইমেজ সরানো হচ্ছে

```
docker image rm nginx
```

## একটি ফাইল বা স্ট্যান্ডার্ড ইনপুট স্ট্রিম থেকে একটি ট্র্রেড রিপোসিটোরি লোড করা হচ্ছে

```
docker image load < ubuntu.tar.gz
```

```
docker image load --input ubuntu.tar
```

## একটি টার আর্কাইভে একটি ছবি সংরক্ষণ করা

```
docker image save busybox > ubuntu.tar
```

## একটি ইমেজ এর  ইতিহাস দেখানো

```
docker image history
```

## একটি কন্টেইনার থেকে একটি ইমেজ তৈরি করা

```
docker container commit nginx
```

## একটি ইমেজ ট্যাগ করা

```
docker image tag nginx eon01/nginx
```

## একটি ইমেজ পুশ করা

```
docker image push eon01/nginx
```


# নেটওয়ার্কিং

## নেটওয়ার্ক তৈরি করা

### একটি ওভারলে নেটওয়ার্ক তৈরি করা

```
docker network create -d overlay MyOverlayNetwork
```


### একটি ব্রিজ নেটওয়ার্ক তৈরি করা

```
docker network create -d bridge MyBridgeNetwork
```

### একটি কাস্টমাইজড ওভারলে নেটওয়ার্ক তৈরি করা

```
docker network create -d overlay \
  --subnet=192.168.0.0/16 \
  --subnet=192.170.0.0/16 \
  --gateway=192.168.0.100 \
  --gateway=192.170.0.100 \
  --ip-range=192.168.1.0/24 \
  --aux-address="my-router=192.168.1.5" --aux-address="my-switch=192.168.1.6" \
  --aux-address="my-printer=192.170.1.5" --aux-address="my-nas=192.170.1.6" \
  MyOverlayNetwork
```

## একটি নেটওয়ার্ক সরানো

```
docker network rm MyOverlayNetwork
```

##  নেটওয়ার্ক এর তালিকা

```
docker network ls
```

## একটি নেটওয়ার্ক সম্পর্কে তথ্য পাওয়া

```
docker network inspect MyOverlayNetwork
```

## একটি চলমান কন্টেইনারকে একটি নেটওয়ার্কে সংযুক্ত করা

```
docker network connect MyOverlayNetwork nginx
```

## একটি কন্টেইনারকে নেটওয়ার্কের সাথে সংযুক্ত করা যখন এটি শুরু হয়

```
docker container run -it -d --network=MyOverlayNetwork nginx
```

## একটি নেটওয়ার্ক থেকে একটি ধারক কন্টেইনারকে বিচ্ছিন্ন করা

```
docker network disconnect MyOverlayNetwork nginx
```

## এক্সপোজিং পোর্ট

ডকার-ফাইল ব্যাবহার করে, আপনি ব্যবহার করে কন্টেইনার এর একটি পোর্ট খুলতে পারেন:


```
EXPOSE <port_number>
```

হোস্ট পোর্ট এর সাথে কন্টেইনার এর পোর্ট এর ম্যাপিং করা যেতে পারে

```
docker run -p $HOST_PORT:$CONTAINER_PORT --name <container_name> -t <image>
```
উদাহরণ

```
docker run -p $HOST_PORT:$CONTAINER_PORT --name infinite -t infinite
```

# নিরাপত্তা

## নিরাপদ ডকার ছবি তৈরির জন্য নির্দেশিকা

1. নুন্নতম বসে ইমেজ ব্যবহার করা
2. সর্বনিম্ন সুবিধাপ্রাপ্ত ব্যবহারকারী হিসেবে কন্টেইনার এর নিবেদিত ব্যবহারকারী
3. MITM আক্রমণ কমানোর জন্য ইমেজ  স্বাক্ষর করুন এবং যাচাই করুন
4. ওপেন সোর্স দুর্বলতার জন্য খুঁজুন, ঠিক করুন এবং মনিটর করুন
5. ডকার ইমেজে সংবেদনশীল তথ্য ফাঁস করবেন না
6. অপরিবর্তনীয়তার জন্য নির্দিষ্ট ট্যাগ ব্যবহার করুন
7. ADD এর পরিবর্তে COPY ব্যবহার করুন
8. মেটাডেটার জন্য লেবেল ব্যবহার করুন
9. ছোট সুরক্ষিত ইমেজ জন্য মাল্টি-স্টেজ বিল্ড ব্যবহার করুন
10. একটি লিন্টার ব্যবহার করুন

আপনি Snyk এর [10 ডকার ইমেজ সিকিউরিটি বেস্ট প্র্যাকটিস](https://snyk.io/blog/10-docker-image-security-best-practices/) ব্লগ পোস্টে আরও তথ্য পেতে পারেন।