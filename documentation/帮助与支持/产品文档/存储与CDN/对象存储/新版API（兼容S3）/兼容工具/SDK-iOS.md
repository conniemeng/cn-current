SDK-iOS

为了您更能够正常使用SDK-Ios，请您下载京东云改造版aws-sdk-ios：[https://github.com/ZHCliang/aws-sdk-ios](https://github.com/ZHCliang/aws-sdk-ios)，

通过CocoaPods引入依赖的Podfile文件如下：
/# Uncomment the next line to define a global platform for your project platform :ios, '11.0' target 'S3UploadDemo' do /# Uncomment the next line if you're using Swift or would like to use dynamic frameworks /# use_frameworks! pod 'AWSCore', git: 'https://github.com/ZHCliang/aws-sdk-ios.git' pod 'AWSS3', git: 'https://github.com/ZHCliang/aws-sdk-ios.git' /# For file transfers end

下载地址：[http://s3-sdk-demo.oss.cn-north-1.jcloudcs.com/ios-sdk/S3UploadDemo-v1.zip](http://s3-sdk-demo.oss.cn-north-1.jcloudcs.com/ios-sdk/S3UploadDemo-v1.zip)