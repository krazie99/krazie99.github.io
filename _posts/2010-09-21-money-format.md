---
layout: post
title: Money Format
excerpt: "Objective-C에서 Money format 사용하기"
tags: [ios, objective-c]
---

#### Objective-C에서 Money format 사용하기

숫자에 돈을 세는 쉼표를 넣어주는 함수

{% highlight objective-c %}
-(NSString*)moneyFormat:(id)number{

    //Integer로 변경
    NSInteger nTmp = [number integerValue];

    NSNumberFormatter *fmt = [[NSNumberFormatter alloc] init];
    [fmt setNumberStyle:NSNumberFormatterDecimalStyle];

    //NSString 으로 저장
    NSString *formatedString = [fmt stringFromNumber:@(nTmp)];

    return formatedString;
}
{% endhighlight %}
