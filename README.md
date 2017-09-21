# CWCNavigationBarAlapha
动态改变当前视图的导航透明度，其它视图不受影响

![image](https://github.com/wenchang1989/CWCNavigationBarAlapha/blob/master/2017-09-21%2017_01_55.gif?raw=true)

经测试导航栏设置为图片，也可达到效果，但是在设置Translucent时会调用视图滑动的代理，重新设置透明度，这不是我们想要的，所以需跳出视图时取消滑动代理，进入视图再加上代理（代码没有修改，请自行添加）

- (void)viewWillAppear:(BOOL)animated{

    [super viewWillAppear:animated];
    
    self.navigationController.navigationBar.barStyle = UIBarStyleBlack;//导航栏的背景色是黑色, 字体为白色
    [self scrollViewDidScroll:self.mytableView];
    self.mytableView.delegate = self;
    [self.navigationController.navigationBar setShadowImage:[UIImage new]];//用于去除导航栏的底线，也就是周围的边线
    
}

- (void)viewWillDisappear:(BOOL)animated{

    [super viewWillDisappear:animated];
    self.mytableView.delegate = nil;
    [[[self.navigationController.navigationBar subviews] objectAtIndex:0] setAlpha:1];
}



