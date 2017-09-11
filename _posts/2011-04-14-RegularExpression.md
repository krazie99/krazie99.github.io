---
layout: post
title: 정규식 @ Objective-c
excerpt: Objective-c에서 정규식 사용하기
comments: true
tags: [ios, objective-c, 정규식, regularexpression]
---
## objective-c에서 정규식을 이용한 검색 예제
{% highlight objective-c %}
NSString *str = @"1234abcd";
NSString *ptn = @"[a-z]";

NSRange range = [str rangeOfString:ptn options:NSRegularExpressionSearch];

NSLog(@"%d", range.location);
NSLog(@"%d", range.length);
{% endhighlight %}
> range.location 값에 "a"의 index 번호가 들어온다.
