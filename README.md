
## 前沿

* 新闻、电商、视频等 app 经常会看到这种 SegmentedControl 布局样式

* 这里的 SegmentedControl 采取的是腾讯新闻、网易新闻、礼物说等布局样式

* 版本升级（根据标题内容自动适配 SGPageTitleView 是静止还是滚动）

* 为什么要选取 SGPageView ？

###### 介绍：这种控件大部分采用 UILabel 或 UIButton 进行的封装，您可以搜索选取很多第三方

###### 说明：大部分的这种控件都是静止或滚动状态，只有封装很好的才会有静止滚动同时存在。之前的版本就是把静止状态与滚动状态分开而写，使用者还要自己选取，总感觉很不方便；如若遇到像网易新网、虎牙直播这种用户可以根据自己的需求定制标题个数，这种控件就不能再选取使用了。因此，版本进行了一次升级，升级之后的版本对滚动条做了相应的修改，升级之后的滚动条的样式减少了许多，但解决了可根据标题内容设置滚动条的宽度以及根据标题内容自动选取是静止还是滚动样式


## 主要内容的介绍

* `普通样式一`<br>

* `普通样式二`<br>

* `标题按钮文字渐显效果`<br>

* `导航栏样式`<br>


## 效果图

![](https://github.com/kingsic/SGPageView/raw/master/Gif/sorgle.gif) 


## 代码介绍

### * `SGPageView的使用（具体使用请参考 Demo）`<br>

  * 将项目中 SGPageView 文件夹导入工程

  * 导入 #import "SGPageView.h" 头文件
  
* 创建滚动内容视图

```Objective-C
    NSArray *titleArr = @[@"精选", @"电影", @"电视剧", @"综艺"];
    NSMutableArray *childMArr = [NSMutableArray array];
    UIViewController *vcs;
    for (int i = 0; i < titleArr.count; i++) {
        vcs = [[UIViewController alloc] init];
        vcs.view.backgroundColor = [UIColor colorWithRed:arc4random_uniform(255) / 255.0 green:arc4random_uniform(255) / 255.0 blue:arc4random_uniform(255) / 255.0 alpha:1.0];
        [self addChildViewController:vcs];
        [childMArr addObject:vcs];
    }
    CGFloat contentViewHeight = self.view.frame.size.height - 108;
    self.pageContentView = [SGPageContentView pageContentViewWithFrame:CGRectMake(0, 108, self.view.frame.size.width, contentViewHeight) parentVC:self childVCs:childMArr];
    _pageContentView.delegatePageContentView = self;
    [self.view addSubview:_pageContentView];
```

* * 滚动内容视图代理方法

```Objective-C
- (void)SGPageContentView:(SGPageContentView *)SGPageContentView progress:(CGFloat)progress originalIndex:(NSInteger)originalIndex targetIndex:(NSInteger)targetIndex {
    [self.pageTitleView setSegmentedControlWithProgress:progress originalIndex:originalIndex targetIndex:targetIndex];
}
```

* 创建滚动标题视图

```Objective-C
    self.pageTitleView = [SGPageTitleView pageTitleViewWithFrame:CGRectMake(0, 64, self.view.frame.size.width, 44) titleNames:titleArr];
    _pageTitleView.delegatePageTitleView = self;
    [self.view addSubview:_pageTitleView];
```

* * 滚动标题视图代理方法

```Objective-C
- (void)SGPageTitleView:(SGPageTitleView *)SGPageTitleView selectedIndex:(NSInteger)selectedIndex {
    [self.pageContentView setSGPageCententViewCurrentIndex:selectedIndex];
}
```


## 版本介绍

* 2016-10-7  --> 初始版本的创建
* 2017-4-13 --> 版本升级（根据标题内容自动适配 SGPageTitleView 是静止还是滚动）


## Concluding remarks

* 如在使用中, 遇到什么问题或有更好建议者, 请记得 [Issues me](https://github.com/kingsic/SGPageView/issues) 或 kingsic@126.com 邮箱联系我

