# **在URL中包含签名**

除了使用Authorization Head，用户还可以在URL中加入签名信息，这样用户就可以把该URL转给第三方实现授权访问。

实现方式：

URL签名示例:
[http://s.jcloud.com/mybucket/public/index.html?Expires=1369191796&AccessKey=9c379f079214447fad2959c4621cd6feVb797oH1&Sigature=tzEQUA%2Bj%2BUHcEp%2FBUMKeMd5bqGc%3D](http://s.jcloud.com/mybucket/public/index.html?Expires=1369191796&AccessKey=9c379f079214447fad2959c4621cd6feVb797oH1&Sigature=tzEQUA%2Bj%2BUHcEp%2FBUMKeMd5bqGc%3D)

基于查询字符串的认证请求不需要任何特殊的 HTTP Header，它通过查询字符串来指定认证信息。

URL签名，必须至少包含Signature，Expires，AccessKey三个参数。

1. Expires这个参数的值是一个UNIX时间（自UTC时间1970年1月1号0时开始的秒数），用于标识该URL的超时时间。超过该时间的请求都会被拒绝。例如：当前时间是1141889060，开发者希望创建一个60秒后自动失效的URL，则可以设置Expires时间为1141889120。

2. AccessKey即密钥中的AccessKey。

3. Signature表示签名信息。所有京东云支持的请求和各种Header参数，在URL中进行签名的算法和在Header中包含签名的算法基本一样。
Signature=URL-Encode(Base64(HMAC-SHA1(UTF-8-Encoding-Of(SecretKey,StringToSign))));

StringToSign =HTTP-Verb + "\n"

+Content-MD5 +"\n"

+Content-Type +"\n"

+Expires +"\n"

+ CanonicalizedHeaders

+CanonicalizedResource;

其中，与header中包含签名相比主要区别如下：

1. 需要对计算出来的签名进行 URL-Encode 编码

2. 将StringToSign 中的 Date 换成 Expires

3. 不支持同时在URL和Head中包含签名。

示例代码：

URL中添加签名的JAVA示例代码：
AccessKey

9c379f079214447fad2959c4621cd6feVb797oH1AccessKeySecret

41oUzT1opT69jpedWVg1vFTb31FvrewWSXnnZ7i1import javax.crypto.Mac;

import javax.crypto.spec.SecretKeySpec;

import org.apache.commons.codec.binary.Base64;

String secretKey = "41oUzT1opT69jpedWVg1vFTb31FvrewWSXnnZ7i1";

String signString = "GET\n\n\n1369191796\n/mybucket/index.html";

SecretKeySpec signingKey = new SecretKeySpec(secretKey.getBytes("UTF-8"), "HmacSHA1");

Mac mac = Mac.getInstance("HmacSHA1");

mac.init(signingKey);

byte[] rawHmac = mac.doFinal(signString.getBytes("UTF-8"));

String signature = new String(Base64.encodeBase64(rawHmac), "UTF-8");

最后的URL应该为：

http://mybucket.s.jcloud.com/index.html?Expires=1369191796&AccessKey=9c379f079214447fad2959c4621cd6feVb797oH1&Signature=mBb1uuC3y2GeyeqlW5+gN/tla6s=

Host:[s.jcloud.com](http://s.jcloud.com/)

细节分析：

1. 使用在URL中签名的方式，会将你授权的数据在过期时间以内曝露在互联网上，请预先评估使用风险。

2. 在URL中添加签名时，Signature，Expires，AccessKey顺序可以交换，但是如果Signature，AccessKey缺少其中的一个或者多个，返回400 错误。错误码：InvalidURI。

3. 如果访问的当前时间晚于请求中设定的Expires时间，返回返回400 Forbidden。错误码：ExpiredToken。

生成签名字符串时，除Date被替换成Expires参数外，仍然包含Content-Type、Content-MD5等Header。