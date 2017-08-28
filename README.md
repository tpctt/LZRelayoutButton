# LZRelayoutButton
```
pod 'LZRelayoutButton'
```
调整UIButton的title和image位置,
在原来的基础上增加了 imageSize 设置 image 的大小,而不是之前的7/8 的大小, 同时添加了 image 的 offset to top or right        LZRelayoutButton 可以在 cocoapods 的 master 中搜索到了,欢迎提 issue ,之前是 fork 的 LQQZYY,现在改动太多之后就闹独立了
##

<br>如果对您有帮助,还请star支持一下
<br>
<br>[博文讲解](http://blog.csdn.net/lqq200912408/article/details/51323336)
<br>
<img src="https://github.com/LQQZYY/LZButtonCategory/blob/master/LZButton.png" width="50%" height="50%" />


````

-(void)commonInit
{
    
    //字体不同 不可以同时设置行间距  14 3 10
    self.backgroundColor = k_color_C7;
    NSArray *titles = @[@"1111",@"2222",@"3333",@"4444"];
    NSArray *image  = @[@"icon_1111", @"icon_2222",@"icon_3333", @"icon_4444"];
    NSArray *selectedImage  = @[@"icon_1111", @"icon_2222",@"icon_3333", @"icon_4444"];
    
    UIView *pre = nil;
    for (NSInteger i = 0; i< titles.count; i++) {
        
        LZRelayoutButton *button = [[LZRelayoutButton alloc] init];
        
        button.lzType = LZRelayoutButtonTypeBottom;
        button.imageSize = CGSizeMake(45, 45);
        button.offset = 35;
        button.contentHorizontalAlignment = UIControlContentHorizontalAlignmentCenter ;
        button.backgroundColor = [UIColor clearColor];
        
        
        [button addTarget:self action:@selector(btnAct:) forControlEvents:UIControlEventTouchUpInside];
        [self addSubview:button];
        [button setImage:[UIImage imageNamed:image[i]] forState:UIControlStateNormal];
       // [button setImage:[UIImage imageNamed:selectedImage[i]] forState:UIControlStateHighlighted];
        
        button.tag = i;
        button.titleLabel.font = MYFONT(15);
        [button setTitleColor:k_white_color forState:0];
        [button setTitle:titles[i] forState:0];
        
        
        
        if (pre == nil) {
            [button mas_makeConstraints:^(MASConstraintMaker *make) {
                make.left.mas_equalTo( @0);
                make.top.mas_equalTo(self.mas_top);
                make.bottom.mas_equalTo(self.mas_bottom);

            }];
        }else if (i == titles.count - 1){
            [button mas_makeConstraints:^(MASConstraintMaker *make) {
                make.right.mas_equalTo( @0);
                make.left.mas_equalTo( pre.mas_right);
                make.top.mas_equalTo(self.mas_top);
                make.bottom.mas_equalTo(self.mas_bottom);
                make.width.equalTo(pre.mas_width);
            }];
        }else{
            [button mas_makeConstraints:^(MASConstraintMaker *make) {
                make.left.mas_equalTo( pre.mas_right);
                make.top.mas_equalTo(self.mas_top);
                make.bottom.mas_equalTo(self.mas_bottom);
                make.width.equalTo(pre.mas_width);
            }];
            
        }
        pre = button;
        
    }
}
````
