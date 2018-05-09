#名次解释
“行高”顾名思意指一行文字的高度。具体来说是指两行文字间基线之间的距离。基线实在英文字母中用到的一个概念，我们刚学英语的时使用的那个英语本子每行有四条线，其中底部第二条线就是基线:
```
{
	vertical-align: top;  /* middle, baseline, bottom */
}
```
#line-height与line boxes高度
CSS中起高度作用的应该就是height以及line-height了吧！如果一个标签没有定义height属性(包括百分比高度)，那么其最终表现的高度一定是由line-height起作用.

问题：有一个空的`<div/>`，如果没有设置至少大于1像素高度`height`值时，该`div`的高度就是个0。如果该`div`里面打入了一个空格或是文字，则此`div`就会有一个高度。为什么div里面有文字后就会有高度呢？

* 一般回答：文字撑开的！文字占据空间，自然将`div`撑开
* 事实：不是文字撑开了`div`的高度，而是`line-height`

看实例-----------------------------

test1 `div`有文字大小，但行高为0，结果`div`的高度就是个0；test2 `div`文字大小为0，但是有行高，为20像素，结果`div`高度就是20像素。这就说明撑开`div`高度的是`line-height`不是文字内容

`line-height`是怎么产生的呢？在`inline box`模型中，有个`line boxes`，他的作用就是包裹每行文字。一行文字一个`line boxes`。`line boxes`什么特性也没有，就高度。在没有设置`height`属性的`div`的高度就是由一个一个`line boxes`的高度堆积而成的。

> 其实`line boxes`不是直接的生产者，属于中层干部，真正的活儿都是它的手下 – `inline boxes`干的，这些手下就是文字啦，图片啊，`<span>`之类的`inline`属性的标签啦。`line boxes`只是个考察汇报人员，考察它的手下谁的实际`line-height`值最高，谁最高，它就要谁的值，然后向上汇报，形成高度。例如，`<span style="line-height:20px;">`取手下`line-height``<span style="line-height:40px;">`最高`</span>`的值`span`。则`line boxes`的高度就是40像素了。

http://www.zhangxinxu.com/wordpress/2009/11/css行高line-height的一些深入理解及应用/