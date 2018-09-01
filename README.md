# CNKI_SogouWechat_SogouNews_Spider

个人项目，代码已上传至我的github。
只支持**python3**.
需要说明的是，本文中介绍的都是小规模数据的爬虫（数据量<1G），大规模爬取需要会更复杂，本文不涉及这一块。另外，代码细节就不过多说了，只将一个大概思路以及趟过的坑。

---
##搜狗微信文章抓取
- 目标：**在搜狗微信模块下搜索关键词的文章，抓取链接保存文章标题，来源，时间，内容的内容**
- 采取的策略：selenium模拟搜索，登陆扫码采用手动扫描的模式，登陆后通过不同的关键词进行搜索，翻页等操作。
- 遇到的坑：
1.SogouWechat这个库只能抓到10个items（自己加入cookies也只能抓10个好像，反正我没成功的抓多个）
2.登陆只想到手动扫描这一块，没有其他更好的方法
3.搜索出来的文章链接时临时性的，要及时request并保存
4.在模拟翻页操作的时候，建议模拟一下页面滚动
5.网速不好的情况，要有sleep，要不然chrome会报错

##搜狗新闻抓取
- 目标：**在搜狗新闻搜索中搜索关键，将所有新闻的标题，时间，内容保存下来**
- 采取的策略：
1. request.get关键词，因为搜狗新闻就不涉及到cookies的问题，直接请求
2.ip隧道代理请求（阿布云代理）
3.news的具体页面，如果request获取不到文本，用selenium抓
- 遇到的坑：参照以上第三点。
##知网摘要信息抓取
- 目标：**指定文献来源或者单位，抓所有的文献的摘要，作者，时间等等**
- 采取的策略：
1.selenium模拟登陆，得到搜索页面
2.ajax抓包，构造请求发送到服务器
3.自动打码（云打码，效果还可以）
4.ip隧道代理
5.翻页用request构造
- 遇到的坑：
1.必须要登陆才能看到所有文献
2.打码失败的话one more time
3.数据量有点多，及时保存数据，我没有用数据库，我直接写到文件了
