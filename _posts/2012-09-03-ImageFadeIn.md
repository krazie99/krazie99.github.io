---
layout: post
title: UIImageView 페이드 효과
excerpt: "UIImageView에 이미지가 변경시 Fade In 효과 주기"
tags: [ios, objective-c, UIImageView, FadeIn]
---
## CATransition 페이드 함수

{% highlight objective-c %}
-(void)setImage:(UIImage *)image
{
    CATransition *animation = [CATransition animation];
    animation.duration = 0.188;
    animation.type = kCATransitionFade;
    [[self layer] addAnimation:animation forKey:@"imageFade"];
    [super setImage:image];
}
{% endhighlight %}
