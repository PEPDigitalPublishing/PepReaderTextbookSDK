# PepReaderTextbookSDK
SDK集成包


## SDK集成
1.将提供的PEPReaderTextbookSDK及资源.zip解压，拖入工程中
包括以下三个文件：

![image](https://github.com/PEPDigitalPublishing/PEPImageHost/raw/master/TextbookSDK/img1.jpg)


2.添加依赖
在 Target --> General 中 添加以下依赖
![image](https://github.com/PEPDigitalPublishing/PEPImageHost/raw/master/TextbookSDK/img2.jpg)


3. buldSetting 中设置 Allow Non-modular Includes In Framework Modules 为 YES
 ![image](https://github.com/PEPDigitalPublishing/PEPImageHost/raw/master/TextbookSDK/img3.jpg)

4.buldSetting 中设置 bitcode 为NO
![image](https://github.com/PEPDigitalPublishing/PEPImageHost/raw/master/TextbookSDK/img4.jpg)


## 功能

### 横屏配置
1.在 Target --> General 中 设置
![image](https://github.com/PEPDigitalPublishing/PEPImageHost/raw/master/TextbookSDK/img5.jpg)

2. 在Appdelecate中实现
```
- (UIInterfaceOrientationMask)application:(UIApplication *)application supportedInterfaceOrientationsForWindow:(UIWindow *)window {
    return UIInterfaceOrientationMaskAll;
}
```

### 初始化
导入#import <**PDFReaderSDKTextBook/PDFReaderSDKTextBook.h**>
```
- (void)setPEPTextbookConfig
{
    // 您的用户名和密码
    NSDictionary *param = @{
                            @"username":@"1000",
                            @"password":@"1234"
                            };
    NSString *AppID = @"41d89ab4624211e89c1e005056ae9a1b";
    
    // 用APPID初始化SDK工具类
    PEPReaderTextBookManager *manager = [PEPReaderTextBookManager shareManagerWithAPPID:AppID];
    // 用户名和密码 登录SDK
    [manager getUserAuthWithParam:param];
}
```

### 打开教材
```
- (void)openBookList:(UIButton *)sender
{
    PEPTextbookViewController *textBook = [[PEPTextbookViewController alloc] init];
    [self.navigationController pushViewController:textBook animated:YES];
}
```
### 其他暴露的接口
```
  PEPReaderTextBookManager *manager = [PEPReaderTextBookManager shareManagerWithAPPID:AppID];

// 设置SDK的BaseUrl
[manager setBaseURL:@""];

// 查询教材列表
  [manager queryTextbookListWithParam:nil withBlock:^(id response) {
        NSLog(@"list%@",response);
    }];
    
    // 查询教材详情
    [manager queryTextbookDetailWithParam:@{@"id":@"1211001102161"} withBlcok:^(id response) {
        NSLog(@"detail%@",response);
    }];
```
### 退出登录
  
```
  [manager quitCZPTuserAccount];
  
```


