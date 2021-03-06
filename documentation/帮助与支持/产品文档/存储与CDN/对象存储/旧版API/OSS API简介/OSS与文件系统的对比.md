# **OSS与文件系统的对比**

OSS是一个分布式的对象存储服务，提供的是一个Key-Value对形式的对象存储服务。用户可以根据Object的名称（Key）唯一的获取该Object的内容。虽然用户可以使用类似 test1/test.jpg的名字，但是这并不表示用户的Object是保存在test1目录下面的。对于OSS 来说，test1/test.jpg仅仅只是一个字符串，和a.jpg这种并没有本质的区别。因此不同名称的Object之间的访问消耗的资源是类似的。

文件系统是一种典型的树状索引结构，一个名为test1/test.jpg的文件，访问过程需要先访问到 test1这个目录，然后再在该目录下查找名为test.jpg的文件。因此文件系统可以很轻易的支持文件夹的操作，比如重命名目录、删除目录、移动目录等，因为这些操作仅仅只是针对目录节点的操作。这种组织结构也决定了文件系统访问越深的目录消耗的资源也越大，操作拥有很多文件的目录也会非常慢。

对于OSS来说，可以通过一些操作来模拟类似的功能，但是代价非常昂贵。比如重命名目录，希望将 test1 目录重命名成test2，那么OSS的实际操作是将所有以test1/开头的 Object都重新复制成以test2/ 开头的Object，这是一个非常消耗资源的操作。因此在使用OSS的时候要尽量避免类似的操作。

OSS保存的Object不支持修改。用户哪怕是仅仅需要修改一个字节也需要重新上传整个 Object。而文件系统的文件支持修改，比如修改指定偏移位置的内容、截断文件尾部等，这些特点也使得文件系统拥有广泛的适用性。但另外一方面，OSS能支持海量的用户并发访问，而文件系统会受限于单个设备的性能。

因此，将OSS映射为文件系统是非常低效的，也是不建议的做法。如果一定要挂载成文件系统的话，建议尽量只做写新文件、删除文件、读取文件这几种操作。使用OSS应该充分发挥其优点，即海量数据处理能力，优先用来存储海量的非结构化数据，比如图片、视频、文档等。

以下是OSS与文件系统的概念对比：
对象存储 OSS

文件系统Object

文件Bucket

主目录Region

无Endpoint

无AccessKey

无无

多级目录GetService

获取主目录列表GetBucket

获取文件列表PutObject

写文件GetObject

读文件DeleteObject

删除文件无

修改文件内容CopyObject （目的和源相同）

修改文件属性CopyObject
复制文件