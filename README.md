# Note

#Android App启动步骤
整个应用程序的启动过程要执行很多步骤，但是整体来看，主要分为以下五个阶段：

一. Launcher通过Binder进程间通信机制通知ActivityManagerService，它要启动一个Activity；

二. ActivityManagerService通过Binder进程间通信机制通知Launcher进入Paused状态；

三. Launcher通过Binder进程间通信机制通知ActivityManagerService，它已经准备就绪进入Paused状态，于是ActivityManagerService就创建一个新的进程，用来启动一个ActivityThread实例，即将要启动的Activity就是在这个ActivityThread实例中运行；

四. ActivityThread通过Binder进程间通信机制将一个ApplicationThread类型的Binder对象传递给ActivityManagerService，以便以后ActivityManagerService能够通过这个Binder对象和它进行通信；

五. ActivityManagerService通过Binder进程间通信机制通知ActivityThread，现在一切准备就绪，它可以真正执行Activity的启动操作了。

#Android任务和返回栈完全解析
参考文章
[http://blog.csdn.net/guolin_blog/article/details/41087993](http://blog.csdn.net/guolin_blog/article/details/41087993)

#深入了解View
参考文章
[http://blog.csdn.net/guolin_blog/article/details/12921889](http://blog.csdn.net/guolin_blog/article/details/12921889)
[http://blog.csdn.net/guolin_blog/article/details/16330267](http://blog.csdn.net/guolin_blog/article/details/16330267)
[http://www.jianshu.com/p/75dc9e4b67ae](http://www.jianshu.com/p/75dc9e4b67ae)
##新的Android工具集
[http://tools.android.com/tech-docs/jackandjill](http://tools.android.com/tech-docs/jackandjill)
##MVC、MVP、MVVP
[http://www.tianmaying.com/tutorial/AndroidMVC](http://www.tianmaying.com/tutorial/AndroidMVC)
##Caused by: java.lang.IllegalStateException: Can not perform this action after onSaveInstanceState
commit方法是在Activity的onSaveInstanceState()之后调用的，这样会出错，因为onSaveInstanceState方法是在该Activity即将被销毁前调用，来保存Activity数据的，如果在保存玩状态后再给它添加Fragment就会出错。解决办法就是把commit（）方法替换成 commitAllowingStateLoss()就行了
##ArcMenu与CircularFloatingActionMenu对比
ArcMenu占用空间较大
CircularFloatingActionMenu位置不灵活
##Android控件显示顺序控制
`bringToFront()`这个方法可以改变ViewGroup内子控件在Z轴坐标得顺序，使得当前控件在所有兄弟控件得最前面，同时在4.4之前得版本，还需要它的父控件调用requestLayout()和invalidate()来重新绘制子控件的顺序。
而且要注意的一点是，需要在所有控件都加载完之后才能调用 bringToFront（）来设置指定控件的顺序，否则后加载的控件还是可能覆盖你想要上提的控件的。
这样我们就可以通过这个方法来排列子控件的覆盖顺序啦。
##什么是MIME

MIME, 全称为“Multipurpose Internet Mail Extensions”, 比较确切的中文名称为“多用途互联网邮件扩展”。它是当前广泛应用的一种电子邮件技术规范，基本内容定义于RFC 2045-2049

什么是MIME类型?-在把输出结果传送到浏览器上的时候，浏览器必须启动适当的应用程序来处理这个输出文档。

这可以通过多种类型MIME（多功能网际邮件扩充协议）来完成。在HTTP中，MIME类型被定义在Content-Type header中。

例 如，架设你要传送一个Microsoft Excel文件到客户端。那么这时的MIME类型就是“application/vnd.ms-excel”。 

在大多数实际情况中，这个文件然后将传送给 Execl来处理（假设我们设定Execl为处理特殊MIME类型的应用程序）。在ASP中，设定MIME类 型的方法是通过Response对象的 ContentType属性。

多媒体文件格式MIME

最早的HTTP协议中，并没有附加的数据类型信息，所有传送的数据都被客户程序解释为超文本标记语言HTML 文档，而为了支持多媒体数据类型，HTTP协议中就使用了附加在文档之前的MIME数据类型信息来标识数据类型。

然而当它被HTTP协议支持之后，它的意义就更为显著了。它使得HTTP传输的不仅是普通的文本，而变得丰富多彩。

每个MIME类型由两部分组成，前面是数据的大类别，例如声音audio、图象image等，后面定义具体的种类。

常见的MIME类型

超文本标记语言文本 .html,.html text/html

普通文本 .txt text/plain

RTF文本 .rtf application/rtf

GIF图形 .gif image/gif

JPEG图形 .ipeg,.jpg image/jpeg

au声音文件 .au audio/basic

MIDI音乐文件 mid,.midi audio/midi,audio/x-midi

RealAudio音乐文件 .ra, .ram audio/x-pn-realaudio

MPEG文件 .mpg,.mpeg video/mpeg

AVI文件 .avi video/x-msvideo

GZIP文件 .gz application/x-gzip

TAR文件 .tar application/x-tar

Internet 中有一个专门组织IANA来确认标准的MIME类型，但Internet发展的太快，很多应用程序等不及IANA来确认他们使用的 MIME类型为标准类 型。因此他们使用在类别中以x-开头的方法标识这个类别还没有成为标准，例如：x-gzip，x-tar等。事实上这些类型运用的很广泛，已经成为了事实 标准。只要客户机和服务器共同承认这个MIME类型，即使它是不标准的类型也没有关系，客户程序就能根据MIME类型，采用具体的处理手段来处理数据。而 Web服务器和浏览器（包括操作系统）中，缺省都设置了标准的和常见的MIME类型，只有对于不常见的 MIME类型，才需要同时设置服务器和客户浏览 器，以进行识别。

由于MIME类型与文档的后缀相关，因此服务器使用文档的后缀来区分不同文件的MIME类型，服务器中必须定义文档后缀 和MIME类型之间的对应关系。而客户程序从服务器上接收数据的时候，它只是从服务器接受数据流，并不了解文档的名字，因此服务器必须使用附加信息来告诉 客户程序数据的MIME类型。服务器在发送真正的数据之前，就要先发送标志数据的MIME类型的信息，这个信息使用Content-type关键字进行定 义，例如对于HTML文档，服务器将首先发送以下两行MIME标识信息,这个标识并不是真正的数据文件的一部分。

Content-type: text/html

注意，第二行为一个空行，这是必须的，使用这个空行的目的是将MIME信息与真正的数据内容分隔开。

## Android之SplashActivity的巧妙之处
[http://blog.csdn.net/way_ping_li/article/details/9863033](http://blog.csdn.net/way_ping_li/article/details/9863033)

##manifest元素详解
[http://developer.android.com/intl/zh-cn/guide/topics/manifest/activity-element.html#screen](http://developer.android.com/intl/zh-cn/guide/topics/manifest/activity-element.html#screen)

##通过adb shell删除系统预装软件
1.进入adb shell，输入su获得ROOT权限

2.接着输入mount，查看哪个分区挂载了/system,例如我的是：
mount -o remount -r -w /system
3.在shell中cd到/system/app文件夹，使用ls命令，查看里面的文件：
4.从名字中，能大体分辨出是什么应用。使用rm YOUR_APK_NAME.apk删除你想删掉的apk，对应的应用也就自动消失了。
##深入浅出RenderThread
[http://blog.chengdazhi.com/index.php/190](http://blog.chengdazhi.com/index.php/190)
