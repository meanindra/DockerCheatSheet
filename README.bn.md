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
