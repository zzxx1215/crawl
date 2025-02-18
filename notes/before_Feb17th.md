## java 开发 爬虫


1. 爬虫有哪些关键模块
 
2. 主要有哪些功能
页面下载、资源提取、URL管理：重复、选取、内容抽取（链接提取）
3. 基本知识点
URL:用来识别资源的字符串
1. 主要类型
   宽度爬虫： 找页面 针对页面进行无差别抓取 难点在于：快、多线程、分布式、内容管理
   垂直性爬虫：找关注信息 难点：精准、保存


包解析
jsoup 是一个用于解析 HTML 和 XML 文档的 Java 库。它提供了方便的 API，使开发者能够轻松地从 HTML 文档中提取数据、操作 DOM 树、处理 CSS 选择器等。版本号 1.18.1 确定了使用的具体版本，在项目中引入 jsoup 后，就可以在代码中使用 jsoup 提供的各种功能来处理网页解析任务。
httpclient5 是 Apache HTTP Components 项目中的一个 HTTP 客户端库，用于在 Java 应用程序中发送 HTTP 请求和接收 HTTP 响应。
httpcore5 是 Apache HTTP Components 项目中的核心 HTTP 协议处理库，它为 HTTP 客户端和服务器提供了底层的网络连接和数据传输功能。与 httpclient5 配合使用
commons-io 是 Apache Commons 项目中的一个实用工具库，主要用于文件和 IO 操作。它提供了一系列方便的方法来进行文件读取、写入、复制、删除等操作，简化了在 Java 应用程序中对文件系统的处理。
slf4j-api（Simple Logging Facade for Java）是一个日志门面框架，它提供了一套统一的日志 API，允许开发者在不依赖具体日志实现的情况下进行日志记录操作。org.slf4j 是其组织标识，1.7.30 是版本号。
logback-classic 是 Logback 日志框架的经典实现，它是 slf4j 的一个实现框架。在项目中引入 logback-classic 后，结合 slf4j-api，就可以使用 slf4j 提供的统一日志 API 在项目中进行日志记录。ch.qos.logback 是 Logback 的组织标识，1.2.3 是版本号。

a 标签是一个识别符号 判断哪里是超链接




<details>
<summary>笔记</summary>


1. 把单一爬虫完成
2. 回答主要由哪些模块
    管理url 
    获取 url
    图片解析
3. 每一块的东西有哪些主要包构成，主要完成哪些内容


    <details>
    <summary>内容解析及持久化</summary>
    
    apacheHttpClient：具有强大的网络解析功能的包，能够获取网站的源代码，但是需要写很多东西，在本项目中不采用
    RuntimeException(e) 错误输出
    
    </details>

   <details>
   
   
    <summary>url</summary>
    
    urlpool
        main
            调用geturl
        geturl
            匹配初试地址并加入待爬取表
            crawlink
                获取待爬取地址
                    判断是否需要爬取：正则表达式
                    存入oldlink
                在待读取的url中读取链接、A标签
                    这一步进来的是之前的基础网页：主网页
                    打开链接，将链接作为一个实例
                    数据从字节转化为字符，放到buffer里边
                    读取buffer里边的每行，找到超链接
                        将链接修正为绝对位置
                    过滤和添加链接
            把newmap与oldmap合并
        变量解析
            newmap
                待读取超链接
            oldmap
                已经读取超链接
            oldlink
                上级网页
                    newlink
                        从上级网页中获取的超链接
        如何实现递归
    
    </details>

        

 
5. 知道常见的反爬技术和应对策略

```
<map>
  <node ID="root" TEXT="爬虫代码解析">
    <node TEXT="urlpool" ID="4j1anfAgWY" _mubu_text="%3Cspan%3Eurlpool%3C/span%3E" STYLE="bubble" POSITION="right">
      <node TEXT="main" ID="MEveSuKoRa" _mubu_text="%3Cspan%3Emain%3C/span%3E" STYLE="fork">
        <node TEXT="调用geturl" ID="jG0PeL3M8X" _mubu_text="%3Cspan%3E%E8%B0%83%E7%94%A8geturl%3C/span%3E" STYLE="fork"/>
      </node>
      <node TEXT="geturl" ID="1Q7wLO2idy" _mubu_text="%3Cspan%3Egeturl%3C/span%3E" STYLE="fork">
        <node TEXT="匹配初试地址并加入待爬取表" ID="1b3VDJU8fs" _mubu_text="%3Cspan%3E%E5%8C%B9%E9%85%8D%E5%88%9D%E8%AF%95%E5%9C%B0%E5%9D%80%E5%B9%B6%E5%8A%A0%E5%85%A5%E5%BE%85%E7%88%AC%E5%8F%96%E8%A1%A8%3C/span%3E" STYLE="fork"/>
        <node TEXT="crawlink" ID="LGsqUF2e48" _mubu_text="%3Cspan%3Ecrawlink%3C/span%3E" STYLE="fork">
          <node TEXT="获取待爬取地址" ID="KmQ1TuqIVN" _mubu_text="%3Cspan%3E%E8%8E%B7%E5%8F%96%E5%BE%85%E7%88%AC%E5%8F%96%E5%9C%B0%E5%9D%80%3C/span%3E" STYLE="fork">
            <node TEXT="判断是否需要爬取：正则表达式" ID="dIPOjydVDx" _mubu_text="%3Cspan%3E%E5%88%A4%E6%96%AD%E6%98%AF%E5%90%A6%E9%9C%80%E8%A6%81%E7%88%AC%E5%8F%96%EF%BC%9A%E6%AD%A3%E5%88%99%E8%A1%A8%E8%BE%BE%E5%BC%8F%3C/span%3E" STYLE="fork"/>
            <node TEXT="存入oldlink" ID="QkL48TmDdr" _mubu_text="%3Cspan%3E%E5%AD%98%E5%85%A5oldlink%3C/span%3E" STYLE="fork"/>
          </node>
          <node TEXT="在待读取的url中读取链接、A标签" ID="w6wdz4glBA" _mubu_text="%3Cspan%3E%E5%9C%A8%E5%BE%85%E8%AF%BB%E5%8F%96%E7%9A%84url%E4%B8%AD%E8%AF%BB%E5%8F%96%E9%93%BE%E6%8E%A5%E3%80%81A%E6%A0%87%E7%AD%BE%3C/span%3E" STYLE="fork">
            <node TEXT="这一步进来的是之前的基础网页：主网页" ID="SlZPmkPahq" _mubu_text="%3Cspan%3E%E8%BF%99%E4%B8%80%E6%AD%A5%E8%BF%9B%E6%9D%A5%E7%9A%84%E6%98%AF%E4%B9%8B%E5%89%8D%E7%9A%84%E5%9F%BA%E7%A1%80%E7%BD%91%E9%A1%B5%EF%BC%9A%E4%B8%BB%E7%BD%91%E9%A1%B5%3C/span%3E" STYLE="fork"/>
            <node TEXT="打开链接，将链接作为一个实例" ID="Vzlr8g0lpJ" _mubu_text="%3Cspan%3E%E6%89%93%E5%BC%80%E9%93%BE%E6%8E%A5%EF%BC%8C%E5%B0%86%E9%93%BE%E6%8E%A5%E4%BD%9C%E4%B8%BA%E4%B8%80%E4%B8%AA%E5%AE%9E%E4%BE%8B%3C/span%3E" STYLE="fork"/>
            <node TEXT="数据从字节转化为字符，放到buffer里边" ID="GkUPkeaPXj" _mubu_text="%3Cspan%3E%E6%95%B0%E6%8D%AE%E4%BB%8E%E5%AD%97%E8%8A%82%E8%BD%AC%E5%8C%96%E4%B8%BA%E5%AD%97%E7%AC%A6%EF%BC%8C%E6%94%BE%E5%88%B0buffer%E9%87%8C%E8%BE%B9%3C/span%3E" STYLE="fork"/>
            <node TEXT="读取buffer里边的每行，找到超链接" ID="tABdau6TcA" _mubu_text="%3Cspan%3E%E8%AF%BB%E5%8F%96buffer%E9%87%8C%E8%BE%B9%E7%9A%84%E6%AF%8F%E8%A1%8C%EF%BC%8C%E6%89%BE%E5%88%B0%E8%B6%85%E9%93%BE%E6%8E%A5%3C/span%3E" STYLE="fork">
              <node TEXT="将链接修正为绝对位置" ID="klwdLPAbdF" _mubu_text="%3Cspan%3E%E5%B0%86%E9%93%BE%E6%8E%A5%E4%BF%AE%E6%AD%A3%E4%B8%BA%E7%BB%9D%E5%AF%B9%E4%BD%8D%E7%BD%AE%3C/span%3E" STYLE="fork"/>
            </node>
            <node TEXT="过滤和添加链接" ID="NQmrfin6Sx" _mubu_text="%3Cspan%3E%E8%BF%87%E6%BB%A4%E5%92%8C%E6%B7%BB%E5%8A%A0%E9%93%BE%E6%8E%A5%3C/span%3E" STYLE="fork"/>
          </node>
        </node>
        <node TEXT="把newmap与oldmap合并" ID="yWmEKHVxux" _mubu_text="%3Cspan%3E%E6%8A%8Anewmap%E4%B8%8Eoldmap%E5%90%88%E5%B9%B6%3C/span%3E" STYLE="fork"/>
      </node>
      <node TEXT="变量解析" ID="c2uBx7zaN6" _mubu_text="%3Cspan%3E%E5%8F%98%E9%87%8F%E8%A7%A3%E6%9E%90%3C/span%3E" STYLE="fork">
        <node TEXT="newmap" ID="HDF0DYgWrL" _mubu_text="%3Cspan%3Enewmap%3C/span%3E" STYLE="fork">
          <node TEXT="待读取超链接" ID="dN9FptAlAd" _mubu_text="%3Cspan%3E%E5%BE%85%E8%AF%BB%E5%8F%96%E8%B6%85%E9%93%BE%E6%8E%A5%3C/span%3E" STYLE="fork"/>
        </node>
        <node TEXT="oldmap" ID="DzObt07LCb" _mubu_text="%3Cspan%3Eoldmap%3C/span%3E" STYLE="fork">
          <node TEXT="已经读取超链接" ID="AT6JqKWA4M" _mubu_text="%3Cspan%3E%E5%B7%B2%E7%BB%8F%E8%AF%BB%E5%8F%96%E8%B6%85%E9%93%BE%E6%8E%A5%3C/span%3E" STYLE="fork"/>
        </node>
        <node TEXT="oldlink" ID="MPuwzstJrn" _mubu_text="%3Cspan%3Eoldlink%3C/span%3E" STYLE="fork">
          <node TEXT="上级网页" ID="M0b7OD1Tgk" _mubu_text="%3Cspan%3E%E4%B8%8A%E7%BA%A7%E7%BD%91%E9%A1%B5%3C/span%3E" STYLE="fork">
            <node TEXT="newlink" ID="0E99EZv5k7" _mubu_text="%3Cspan%3Enewlink%3C/span%3E" STYLE="fork">
              <node TEXT="从上级网页中获取的超链接" ID="Vb36nJX4MW" _mubu_text="%3Cspan%3E%E4%BB%8E%E4%B8%8A%E7%BA%A7%E7%BD%91%E9%A1%B5%E4%B8%AD%E8%8E%B7%E5%8F%96%E7%9A%84%E8%B6%85%E9%93%BE%E6%8E%A5%3C/span%3E" STYLE="fork"/>
            </node>
          </node>
        </node>
      </node>
      <node TEXT="如何实现递归" ID="D9JgSjeGdQ" _mubu_text="%3Cspan%3E%E5%A6%82%E4%BD%95%E5%AE%9E%E7%8E%B0%E9%80%92%E5%BD%92%3C/span%3E" STYLE="fork"/>
    </node>
    <node TEXT="imageCrawl" ID="M2K2FqZLKu" _mubu_text="%3Cspan%3EimageCrawl%3C/span%3E" STYLE="bubble" POSITION="right">
      <node TEXT="目的" ID="mHzkFOcReG" _mubu_text="%3Cspan%3E%E7%9B%AE%E7%9A%84%3C/span%3E" STYLE="fork">
        <node TEXT="获取url,找到代表图片的那个标签" ID="T45aphLImh" _mubu_text="%3Cspan%3E%E8%8E%B7%E5%8F%96url,%E6%89%BE%E5%88%B0%E4%BB%A3%E8%A1%A8%E5%9B%BE%E7%89%87%E7%9A%84%E9%82%A3%E4%B8%AA%E6%A0%87%E7%AD%BE%3C/span%3E" STYLE="fork">
          <node TEXT="本网址" ID="BBoIJOeK3E" _mubu_text="%3Cspan%3E%E6%9C%AC%E7%BD%91%E5%9D%80%3C/span%3E" STYLE="fork">
            <node TEXT="src" ID="r0wYXVMWW9" _mubu_text="%3Cspan%3Esrc%3C/span%3E" STYLE="fork"/>
          </node>
        </node>
      </node>
      <node TEXT="爬虫" ID="Gd0ZpA3oq1" _mubu_text="%3Cspan%3E%E7%88%AC%E8%99%AB%3C/span%3E" STYLE="fork">
        <node TEXT="有些网站不希望被爬" ID="p1fXkKIXJT" _mubu_text="%3Cspan%3E%E6%9C%89%E4%BA%9B%E7%BD%91%E7%AB%99%E4%B8%8D%E5%B8%8C%E6%9C%9B%E8%A2%AB%E7%88%AC%3C/span%3E" STYLE="fork"/>
      </node>
      <node TEXT="apacheheetclient" ID="2m8vSP990r" _mubu_text="%3Cspan%3Eapacheheetclient%3C/span%3E" STYLE="fork">
        <node TEXT="把目标网址获取，同时设置反爬虫" ID="prtm6IGJZ9" _mubu_text="%3Cspan%3E%E6%8A%8A%E7%9B%AE%E6%A0%87%E7%BD%91%E5%9D%80%E8%8E%B7%E5%8F%96%EF%BC%8C%E5%90%8C%E6%97%B6%E8%AE%BE%E7%BD%AE%E5%8F%8D%E7%88%AC%E8%99%AB%3C/span%3E" STYLE="fork">
          <node TEXT="获取页面源码" ID="n7M1zVucQh" _mubu_text="%3Cspan%3E%E8%8E%B7%E5%8F%96%E9%A1%B5%E9%9D%A2%E6%BA%90%E7%A0%81%3C/span%3E" STYLE="fork"/>
        </node>
      </node>
      <node TEXT="jsoup" ID="bPwQleqOAJ" _mubu_text="%3Cspan%3Ejsoup%3C/span%3E" STYLE="fork">
        <node TEXT="首先要人工解析网站结构" ID="pKIRvEtzSq" _mubu_text="%3Cspan%3E%E9%A6%96%E5%85%88%E8%A6%81%E4%BA%BA%E5%B7%A5%E8%A7%A3%E6%9E%90%E7%BD%91%E7%AB%99%E7%BB%93%E6%9E%84%3C/span%3E" STYLE="fork"/>
        <node TEXT="找到对应的图片" ID="CuGEDpaOp5" _mubu_text="%3Cspan%3E%E6%89%BE%E5%88%B0%E5%AF%B9%E5%BA%94%E7%9A%84%E5%9B%BE%E7%89%87%3C/span%3E" STYLE="fork"/>
        <node TEXT="使用代理IP反爬虫" ID="aa1nwea62p" _mubu_text="%3Cspan%3E%E4%BD%BF%E7%94%A8%E4%BB%A3%E7%90%86IP%E5%8F%8D%E7%88%AC%E8%99%AB%3C/span%3E" STYLE="fork"/>
        <node TEXT="规避名字重复问题" ID="r01AZPp7kt" _mubu_text="%3Cspan%3E%E8%A7%84%E9%81%BF%E5%90%8D%E5%AD%97%E9%87%8D%E5%A4%8D%E9%97%AE%E9%A2%98%3C/span%3E" STYLE="fork"/>
      </node>
    </node>
    <node TEXT="常见的爬虫和反爬虫技术" ID="60RzvYvw8R" _mubu_text="%3Cspan%3E%E5%B8%B8%E8%A7%81%E7%9A%84%E7%88%AC%E8%99%AB%E5%92%8C%E5%8F%8D%E7%88%AC%E8%99%AB%E6%8A%80%E6%9C%AF%3C/span%3E" STYLE="bubble" POSITION="left">
      <node TEXT="技术限制" ID="2iISXs3d9f" _mubu_text="%3Cspan%3E%E6%8A%80%E6%9C%AF%E9%99%90%E5%88%B6%3C/span%3E" STYLE="fork">
        <node TEXT="频次控制" ID="rXxt0Uhkgi" _mubu_text="%3Cspan%3E%E9%A2%91%E6%AC%A1%E6%8E%A7%E5%88%B6%3C/span%3E" STYLE="fork"/>
        <node TEXT="个人隐私不能爬" ID="RKqGUf8N2z" _mubu_text="%3Cspan%3E%E4%B8%AA%E4%BA%BA%E9%9A%90%E7%A7%81%E4%B8%8D%E8%83%BD%E7%88%AC%3C/span%3E" STYLE="fork"/>
        <node TEXT="不要突破反爬虫" ID="pM17NlJt6M" _mubu_text="%3Cspan%3E%E4%B8%8D%E8%A6%81%E7%AA%81%E7%A0%B4%E5%8F%8D%E7%88%AC%E8%99%AB%3C/span%3E" STYLE="fork"/>
        <node TEXT="不要上串代码" ID="h6Yx4JWPYG" _mubu_text="%3Cspan%3E%E4%B8%8D%E8%A6%81%E4%B8%8A%E4%B8%B2%E4%BB%A3%E7%A0%81%3C/span%3E" STYLE="fork"/>
        <node TEXT="不要用付费内容" ID="BeGxORbp6f" _mubu_text="%3Cspan%3E%E4%B8%8D%E8%A6%81%E7%94%A8%E4%BB%98%E8%B4%B9%E5%86%85%E5%AE%B9%3C/span%3E" STYLE="fork"/>
      </node>
      <node TEXT="robots.txt" ID="CdytvnXF7B" _mubu_text="%3Cspan%3Erobots.txt%3C/span%3E" STYLE="fork">
        <node TEXT="爬虫协议" ID="Vot6w4AAh2" _mubu_text="%3Cspan%3E%E7%88%AC%E8%99%AB%E5%8D%8F%E8%AE%AE%3C/span%3E" STYLE="fork"/>
      </node>
      <node TEXT="常见的反爬虫技术" ID="jlzJdPahOm" _mubu_text="%3Cspan%3E%E5%B8%B8%E8%A7%81%E7%9A%84%E5%8F%8D%E7%88%AC%E8%99%AB%E6%8A%80%E6%9C%AF%3C/span%3E" STYLE="fork">
        <node TEXT="hearder限制" ID="7EQDqqfAvU" _mubu_text="%3Cspan%3Ehearder%E9%99%90%E5%88%B6%3C/span%3E" STYLE="fork">
          <node TEXT="hearder限制" ID="RPhXojUSv8" _mubu_text="%3Cspan%3Ehearder%E9%99%90%E5%88%B6%3C/span%3E" STYLE="fork">
            <node TEXT="检查客户端" ID="JilEsDom18" _mubu_text="%3Cspan%3E%E6%A3%80%E6%9F%A5%E5%AE%A2%E6%88%B7%E7%AB%AF%3C/span%3E" STYLE="fork"/>
            <node TEXT="检查请求来源" ID="iAkLgBWbpV" _mubu_text="%3Cspan%3E%E6%A3%80%E6%9F%A5%E8%AF%B7%E6%B1%82%E6%9D%A5%E6%BA%90%3C/span%3E" STYLE="fork"/>
            <node TEXT="检测cookie次数" ID="udu7l3FdgN" _mubu_text="%3Cspan%3E%E6%A3%80%E6%B5%8Bcookie%E6%AC%A1%E6%95%B0%3C/span%3E" STYLE="fork"/>
          </node>
          <node TEXT="应对：jsoup" ID="B3Zsgi8g9Z" _mubu_text="%3Cspan%3E%E5%BA%94%E5%AF%B9%EF%BC%9Ajsoup%3C/span%3E" STYLE="fork">
            <node TEXT="绕开" ID="QfXTnysIMy" _mubu_text="%3Cspan%3E%E7%BB%95%E5%BC%80%3C/span%3E" STYLE="fork"/>
          </node>
          <node TEXT="容易误伤用户" ID="UhhOgdDzpS" _mubu_text="%3Cspan%3E%E5%AE%B9%E6%98%93%E8%AF%AF%E4%BC%A4%E7%94%A8%E6%88%B7%3C/span%3E" STYLE="fork"/>
        </node>
        <node TEXT="IP限制" ID="MGBCB9fUZp" _mubu_text="%3Cspan%3EIP%E9%99%90%E5%88%B6%3C/span%3E" STYLE="fork">
          <node TEXT="限制" ID="9s5VLbGLXn" _mubu_text="%3Cspan%3E%E9%99%90%E5%88%B6%3C/span%3E" STYLE="fork">
            <node TEXT="IP访问频率" ID="OWaaJHeEhJ" _mubu_text="%3Cspan%3EIP%E8%AE%BF%E9%97%AE%E9%A2%91%E7%8E%87%3C/span%3E" STYLE="fork"/>
          </node>
          <node TEXT="应对" ID="Sw07lJw4rs" _mubu_text="%3Cspan%3E%E5%BA%94%E5%AF%B9%3C/span%3E" STYLE="fork">
            <node TEXT="使用高匿IP" ID="IySVJLB7n8" _mubu_text="%3Cspan%3E%E4%BD%BF%E7%94%A8%E9%AB%98%E5%8C%BFIP%3C/span%3E" STYLE="fork"/>
          </node>
          <node TEXT="问题" ID="PHRUqTCMKk" _mubu_text="%3Cspan%3E%E9%97%AE%E9%A2%98%3C/span%3E" STYLE="fork">
            <node TEXT="局域网统一IP" ID="sEcmfS8KF9" _mubu_text="%3Cspan%3E%E5%B1%80%E5%9F%9F%E7%BD%91%E7%BB%9F%E4%B8%80IP%3C/span%3E" STYLE="fork"/>
            <node TEXT="随机IP" ID="qY0f4fMkAu" _mubu_text="%3Cspan%3E%E9%9A%8F%E6%9C%BAIP%3C/span%3E" STYLE="fork"/>
          </node>
        </node>
        <node TEXT="账号限制：类似于IP限制" ID="pZWLrxPg6L" _mubu_text="%3Cspan%3E%E8%B4%A6%E5%8F%B7%E9%99%90%E5%88%B6%EF%BC%9A%E7%B1%BB%E4%BC%BC%E4%BA%8EIP%E9%99%90%E5%88%B6%3C/span%3E" STYLE="fork">
          <node TEXT="应对" ID="e2FPaKOx8C" _mubu_text="%3Cspan%3E%E5%BA%94%E5%AF%B9%3C/span%3E" STYLE="fork">
            <node TEXT="判断次数上限" ID="eHNGn9ER6i" _mubu_text="%3Cspan%3E%E5%88%A4%E6%96%AD%E6%AC%A1%E6%95%B0%E4%B8%8A%E9%99%90%3C/span%3E" STYLE="fork"/>
            <node TEXT="重新登录" ID="nfErgCpL5V" _mubu_text="%3Cspan%3E%E9%87%8D%E6%96%B0%E7%99%BB%E5%BD%95%3C/span%3E" STYLE="fork"/>
          </node>
        </node>
        <node TEXT="蜜罐陷阱" ID="LReytiIcYD" _mubu_text="%3Cspan%3E%E8%9C%9C%E7%BD%90%E9%99%B7%E9%98%B1%3C/span%3E" STYLE="fork">
          <node TEXT="爬虫识别技术" ID="7G02fzzsWd" _mubu_text="%3Cspan%3E%E7%88%AC%E8%99%AB%E8%AF%86%E5%88%AB%E6%8A%80%E6%9C%AF%3C/span%3E" STYLE="fork">
            <node TEXT="不显示元素" ID="9E9bdZZUls" _mubu_text="%3Cspan%3E%E4%B8%8D%E6%98%BE%E7%A4%BA%E5%85%83%E7%B4%A0%3C/span%3E" STYLE="fork"/>
          </node>
          <node TEXT="应对" ID="92Q85CMHGB" _mubu_text="%3Cspan%3E%E5%BA%94%E5%AF%B9%3C/span%3E" STYLE="fork">
            <node TEXT="添加判断是否可见的逻辑" ID="iqZYweV7z6" _mubu_text="%3Cspan%3E%E6%B7%BB%E5%8A%A0%E5%88%A4%E6%96%AD%E6%98%AF%E5%90%A6%E5%8F%AF%E8%A7%81%E7%9A%84%E9%80%BB%E8%BE%91%3C/span%3E" STYLE="fork">
              <node TEXT="反反爬虫" ID="h41MBioRFe" _mubu_text="%3Cspan%3E%E5%8F%8D%E5%8F%8D%E7%88%AC%E8%99%AB%3C/span%3E" STYLE="fork"/>
            </node>
          </node>
        </node>
        <node TEXT="数据污染" ID="uCLA6WWoBg" _mubu_text="%3Cspan%3E%E6%95%B0%E6%8D%AE%E6%B1%A1%E6%9F%93%3C/span%3E" STYLE="fork">
          <node TEXT="应对" ID="mlJXOadcjo" _mubu_text="%3Cspan%3E%E5%BA%94%E5%AF%B9%3C/span%3E" STYLE="fork">
            <node TEXT="解密" ID="mO398xF018" _mubu_text="%3Cspan%3E%E8%A7%A3%E5%AF%86%3C/span%3E" STYLE="fork"/>
            <node TEXT="图像数据" ID="Clho36Nqj2" _mubu_text="%3Cspan%3E%E5%9B%BE%E5%83%8F%E6%95%B0%E6%8D%AE%3C/span%3E" STYLE="fork"/>
            <node TEXT="破解映射规律" ID="RKzhppSmnH" _mubu_text="%3Cspan%3E%E7%A0%B4%E8%A7%A3%E6%98%A0%E5%B0%84%E8%A7%84%E5%BE%8B%3C/span%3E" STYLE="fork"/>
          </node>
          <node TEXT="限制" ID="8l33VPRqxx" _mubu_text="%3Cspan%3E%E9%99%90%E5%88%B6%3C/span%3E" STYLE="fork">
            <node TEXT="核心数据加密" ID="7oopLzzgNg" _mubu_text="%3Cspan%3E%E6%A0%B8%E5%BF%83%E6%95%B0%E6%8D%AE%E5%8A%A0%E5%AF%86%3C/span%3E" STYLE="fork"/>
            <node TEXT="制造脏数据" ID="j0qkWySEne" _mubu_text="%3Cspan%3E%E5%88%B6%E9%80%A0%E8%84%8F%E6%95%B0%E6%8D%AE%3C/span%3E" STYLE="fork"/>
          </node>
        </node>
        <node TEXT="增加爬取难度" ID="U9gTuMQmlC" _mubu_text="%3Cspan%3E%E5%A2%9E%E5%8A%A0%E7%88%AC%E5%8F%96%E9%9A%BE%E5%BA%A6%3C/span%3E" STYLE="fork">
          <node TEXT="限制" ID="aDgGJDTtCo" _mubu_text="%3Cspan%3E%E9%99%90%E5%88%B6%3C/span%3E" STYLE="fork">
            <node TEXT="图片验证码" ID="cOxeiOKB3Q" _mubu_text="%3Cspan%3E%E5%9B%BE%E7%89%87%E9%AA%8C%E8%AF%81%E7%A0%81%3C/span%3E" STYLE="fork"/>
            <node TEXT="ajex异步请求" ID="Qgv7WzvPkR" _mubu_text="%3Cspan%3Eajex%E5%BC%82%E6%AD%A5%E8%AF%B7%E6%B1%82%3C/span%3E" STYLE="fork"/>
          </node>
          <node TEXT="应对" ID="iagFNiVokb" _mubu_text="%3Cspan%3E%E5%BA%94%E5%AF%B9%3C/span%3E" STYLE="fork">
            <node TEXT="selenium" ID="rOxojfQCVP" _mubu_text="%3Cspan%3Eselenium%3C/span%3E" STYLE="fork"/>
          </node>
        </node>
        <node TEXT="降低反应速度" ID="uVODNodP9a" _mubu_text="%3Cspan%3E%E9%99%8D%E4%BD%8E%E5%8F%8D%E5%BA%94%E9%80%9F%E5%BA%A6%3C/span%3E" STYLE="fork">
          <node TEXT="设置合适的时间" ID="6WIniAWZ2k" _mubu_text="%3Cspan%3E%E8%AE%BE%E7%BD%AE%E5%90%88%E9%80%82%E7%9A%84%E6%97%B6%E9%97%B4%3C/span%3E" STYLE="fork"/>
        </node>
      </node>
    </node>
  </node>
</map>
```

</details>






---




# 流式框架完成URL管理模块 #
   - [x] 知识点解析
   - [x] 框架解析
   - [x] 环境部署的知识学习
   - [x] 环境部署
   - [ ] 数据库获取
   - [ ] 数据操作
   - [ ] 数据保存
今天主要完成学习过程，需要回答的问题：
1. 什么是流式计算框架
能够实时处理数据的计算模型
2. 它主要由什么实现，为什么要用流式计算框架
目前主要用flink实现，因为Flink一致性高、流批一体处理、高容错、并且有很好的SQL接口
1. 找到一个参考，解析他主要由哪些模块组成，模块的逻辑是什么（流式计算部分）
    1. Flink 本质是一个处理数据的软件，很多编程语言都有接口能够和这种软件进行交互。（用代码操作软件）主要分为依赖导入、环境创建、数据源接入、数据处理、数据输出、数据状态管理。Flink类似于一个数据的管理员，一般不对数据进行什么直接的操作。
    2. 
    > https://github.com/jiahong1314/DistributedCrawler
    首先需要确定什么是分布式，分布式系统一定是由多个节点组成的系统。其中，节点指的是计算机服务器，而且这些节点一般不是孤立的，而是互通的。一开始，我们将Flink的TaskManager管理不同的JobManager当作是一种分布式实现，将流式计算处理过程中的任务分配理解为爬虫系统中多个爬虫进行爬取数据。这种理解其实是错误的，我们在经过多次讨论后终于发现这个问题，最后选择采用基于redis实现分布式爬虫的方法。技术架构图如下。
    这一块是一个做过相同问题的项目的分析，其实两种理解都是对的。
    3. 基本模块解读
![基本模块](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9bdf46794dbc41868156dcb709572692~tplv-k3u1fbpfcp-zoom-in-crop-mark:1512:0:0:0.awebp?)
创建工作环境：创建环境、添加数据源、处理数据
数据源：获取数据、关闭数据库、管理数据
转换操作：用爬虫将对url进行操作，获取里边的内容
数据输出：主要功能是将 UrlList 对象中的高优先级和低优先级 URL 分别存储到 Redis 中对应的列表中。

1. 怎么安排到我的内容中？
   1. 这个里边获取url、flink处理、爬虫的先后顺序是什么？ 
   *存疑：我的理解是，一边解析地址，新地址储存，目标数据输出，最后储存完以后整体输出。*
   
   
2/15 
今天的时间不是很充足，主要是把项目的flink环境部署下来


---

# 2/16 
解析一下那个项目中的很多操作， 可以间接一下，所有解析器，下载器，规避方法都是作为爬虫类里边的函数。

我的这个流式flink下载好后，我需要完成这几步把这个任务搭建起来

- [x] 创建爬虫的类：我需要知道我要把爬虫弄成一个什么样的类 这个需要解读一下现有项目的代码
- [x] 创建流式工作环境：代码红色为什么
- [x] 添加数据源：这个数据源要是怎么样的，先本地弄一个行不行
- [x] 处理数据：解读一下这每一行代码，我的爬虫类和目标函数应该是什么样的类型
- [x] 添加数据类型


1. 问题1 
回答：我需要一个实现标记接口Serializable的类，能够告诉程序，我能够实现序列化。同时为了保证爬虫程序的单一性，我需要让这个爬虫类是单一实例爬虫。

1. 问题2
   回答：因为包没有背合适的导入
2. 这个分发规则是基于redis实现的，flink主要负责数据流。
3. 添加数据源：学习的项目中[爬虫项目](https://github.com/jiahong1314/DistributedCrawler) 采用的是Redis作为数据库，那么为什么要采用这个，流计算一定要用这种类型的数据库吗？我先做一个简单的事实更新的数据可不可行？
   回答：
   ```DataStreamSource<String> stream = env.addSource(new MyRedisSource());```
   这个是一个指定数据源的代码块，myredissource 是自定义的一个类，负责实现env的读取数据接口SourceFunction。DataStreamSource<String>是作为一个数据源。不一定，一些简单的数据类型也可以。
 ```SingleOutputStreamOperator<UrlList> urlListSingleOutputStreamOperator = stream.flatMap(new SpiderFlatMapFunction(iSpider));```
flatMap：把映射的结果全部放到一起
SingleOutputStreamOperator<UrlList>： 是 Flink 中表示经过转换操作后得到的单输出流的操作符类，<urllist>是一个定义的
stream：它是一个 DataStream 对象，代表一个已经存在的数据流
