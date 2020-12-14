<img src="https://github.com/seata/seata-samples/blob/master/doc/img/seata.png"  height="100" width="426">

# Seata: Simple Extensible Autonomous Transaction Architecture

[![Build Status](https://travis-ci.org/seata/seata.svg?branch=develop)](https://travis-ci.org/seata/seata)
[![codecov](https://codecov.io/gh/seata/seata/branch/develop/graph/badge.svg)](https://codecov.io/gh/seata/seata)
[![license](https://img.shields.io/github/license/seata/seata.svg)](https://www.apache.org/licenses/LICENSE-2.0.html)
[![maven](https://img.shields.io/maven-central/v/io.seata/seata-parent.svg)](https://search.maven.org/search?q=io.seata)
[![](https://img.shields.io/twitter/follow/seataio.svg?label=Follow&style=social&logoWidth=0)](https://twitter.com/intent/follow?screen_name=seataio)


## What is Seata?

A **distributed transaction solution** with high performance and ease of use for **microservices** architecture.
### Distributed Transaction Problem in Microservices

Let's imagine a traditional monolithic application. Its business is built up with 3 modules. They use a single local data source.

Naturally, data consistency will be guaranteed by the local transaction.

![Monolithic App](https://cdn.nlark.com/lark/0/2018/png/18862/1545296770244-4cedf37e-9dc6-4fc0-a97f-f4240b9d8640.png) 

Things have changed in microservices architecture. The 3 modules mentioned above are designed to be 3 services on top of 3 different data sources ([Pattern: Database per service](http://microservices.io/patterns/data/database-per-service.html)). Data consistency within every single service is naturally guaranteed by the local transaction. 

**But how about the whole business logic scope?**

![Microservices Problem](https://cdn.nlark.com/lark/0/2018/png/18862/1545296781231-4029da9c-8803-43a4-ac2f-6c8b1e2ea448.png) 

### How Seata do?

Seata is just a solution to the problem mentioned above. 

![Seata solution](https://cdn.nlark.com/lark/0/2018/png/18862/1545296791074-3bce7bce-025e-45c3-9386-7b95135dade8.png)

Firstly, how to define a **Distributed Transaction**?

We say, a **Distributed Transaction** is a **Global Transaction** which is made up with a batch of **Branch Transaction**, and normally **Branch Transaction** is just **Local Transaction**.

![Global & Branch](https://cdn.nlark.com/lark/0/2018/png/18862/1545015454979-a18e16f6-ed41-44f1-9c7a-bd82c4d5ff99.png) 

There are 3 basic components in Seata: 

- **Transaction Coordinator(TC):** Maintain status of global and branch transactions, drive the global commit or rollback.
- **Transaction Manager(TM):** Define the scope of global transaction: begin a global transaction, commit or rollback a global transaction.
- **Resource Manager(RM):** Manage resources that branch transactions working on, talk to TC for registering branch transactions and reporting status of branch transactions, and drive the branch transaction commit or rollback.

![Model](https://cdn.nlark.com/lark/0/2018/png/18862/1545013915286-4a90f0df-5fda-41e1-91e0-2aa3d331c035.png) 

A typical lifecycle of Seata managed distributed transaction:

1. TM asks TC to begin a new global transaction. TC generates an XID representing the global transaction.
2. XID is propagated through microservices' invoke chain.
3. RM register local transaction as a branch of the corresponding global transaction of XID to TC. 
4. TM asks TC for committing or rollbacking the corresponding global transaction of XID.
5. TC drives all branch transactions under the corresponding global transaction of XID to finish branch committing or rollbacking.

![Typical Process](https://cdn.nlark.com/lark/0/2018/png/18862/1545296917881-26fabeb9-71fa-4f3e-8a7a-fc317d3389f4.png) 

For more details about principle and design, please go to [Seata wiki page](https://github.com/seata/seata/wiki). 

### History

##### Ant Financial

- **XTS**: Extended Transaction Service. Ant Financial middleware team developed the distributed transaction middleware since 2007, which is widely used in Ant Financial and solves the problems of data consistency across databases and services.

- **DTX**: Distributed Transaction Extended. Since 2013, XTS has been published on the Ant Financial Cloud, with the name of DTX .

##### Alibaba

- **TXC**: Taobao Transaction Constructor. Alibaba middleware team start this project since 2014 to meet distributed transaction problem caused by application architecture change from monolithic to microservices.
- **GTS**: Global Transaction Service. TXC as an Aliyun middleware product with new name GTS was published since 2016.
- **Fescar**: we start the open source project Fescar based on TXC/GTS since 2019 to work closely with the community in the future.


##### Seata Community

- **Seata** :Simple Extensible Autonomous Transaction Architecture. Ant Financial joins Fescar, which make it to be a more neutral and open community for distributed transaction，and Fescar be renamed to Seata.



## Maven dependency
```xml
<seata.version>1.2.0</seata.version>

<dependency>
    <groupId>io.seata</groupId>
    <artifactId>seata-all</artifactId>
    <version>${seata.version}</version>
</dependency>

```
## Quick Start

[Quick Start](https://github.com/seata/seata/wiki/Quick-Start)

## Documentation


You can view the full documentation from the wiki: [Seata wiki page](https://github.com/seata/seata/wiki).

## Reporting bugs

Please follow the [template](https://github.com/seata/seata/blob/develop/.github/ISSUE_TEMPLATE/BUG_REPORT.md) for reporting any issues.


## Contributing

Contributors are welcomed to join the Seata project. Please check [CONTRIBUTING](./CONTRIBUTING.md) about how to contribute to this project.


## Contact

* [Twitter](https://twitter.com/seataio): Follow along for latest Seata news on Twitter.

* Mailing list: 
  * dev-seata@googlegroups.com , for dev/user discussion. [subscribe](mailto:dev-seata+subscribe@googlegroups.com), [unsubscribe](mailto:dev-seata+unsubscribe@googlegroups.com), [archive](https://groups.google.com/forum/#!forum/dev-seata)
  

<img src="https://img.alicdn.com/tfs/TB1NvtaFrj1gK0jSZFOXXc7GpXa-1218-404.jpg"  height="200" width="630">


## Seata ecosystem

* [Seata Ecosystem Entry](https://github.com/seata) - A GitHub group `seata` to gather all Seata relevant projects
* [Seata Samples](https://github.com/seata/seata-samples) - Samples for Seata
* [Seata Docker](https://github.com/seata/seata-docker) - Seata integration with docker
* [Seata K8s](https://github.com/seata/seata-k8s) - Seata integration with k8s
* [Awesome Seata](https://github.com/seata/awesome-seata) - Seata's slides and video address in meetup
* [Seata Website](https://github.com/seata/seata.github.io) - Seata official website

## Contributors

This project exists thanks to all the people who contribute. [[Contributors](https://github.com/seata/seata/graphs/contributors)].

## License

Seata is under the Apache 2.0 license. See the [LICENSE](https://github.com/seata/seata/blob/master/LICENSE) file for details.

## Who is using

These are only part of the companies using Seata, for reference only. If you are using Seata, please [add your company 
here](https://github.com/seata/seata/issues/1246) to tell us your scenario to make Seata better.

<div style='vertical-align: middle'>
    <img alt='Alibaba Group' height='40'  src='https://docs.alibabagroup.com/assets2/images/en/global/logo_header.png'  /img>
    <img alt='蚂蚁金服' height='40'  src='https://img.alicdn.com/tfs/TB1wuuCoET1gK0jSZFhXXaAtVXa-496-202.jpg'  /img>
    <img alt='阿里云' height='40'  src='https://img.alicdn.com/tfs/TB1Ly5oS3HqK1RjSZFPXXcwapXa-238-54.png'  /img>
    <img alt='中航信' height='40'  src='http://www.travelsky.net/publish/main/images/logo.gif'  /img>
    <img alt='中国铁塔' height='40'  src='https://www.china-tower.com/static/web/images/tower-logo.png'  /img>
    <img alt='滴滴' height='40'  src='https://website.didiglobal.com/dist/media/logo-zh.a7abd90d.svg'  /img>
	<img alt='联通(浙江)' height='40'  src='https://img.alicdn.com/tfs/TB1hvabw9f2gK0jSZFPXXXsopXa-174-100.png'  /img>
    <img alt='中国邮政' height='40'  src='http://www.chinapost.com.cn/res/chinapostplan/structure/181041269.png'  /img>
     <img alt='58集团' height='40'  src='http://img.58cdn.com.cn/logo/58/252_84/logo-o.png?v=2'  /img>
    <img alt='太极计算机' height='40'  src='https://img.alicdn.com/tfs/TB1.zqEoAL0gK0jSZFAXXcA9pXa-245-38.png'  /img>
    <img alt='政采云' height='40'  src='https://img.alicdn.com/tfs/TB1DDiCorY1gK0jSZTEXXXDQVXa-440-114.jpg'  /img>
    <img alt='浙江公安厅' height='40'  src='https://img.alicdn.com/tfs/TB1SXGzoxn1gK0jSZKPXXXvUXXa-426-180.jpg'  /img>
    <img alt='特步' height='40'  src='https://www.xtep.com/images/logo.png'  /img>
    <img alt='中通快递' height='40'  src='https://img.alicdn.com/tfs/TB1rCNSFxn1gK0jSZKPXXXvUXXa-172-31.png'  /img>
    <img alt='美的集团' height='40' src='https://img.alicdn.com/tfs/TB1cgvjwYj1gK0jSZFOXXc7GpXa-1040-282.png'  /img>    
    <img alt='浙江烟草' height='40'  src='https://img.alicdn.com/tfs/TB1e7Wiovb2gK0jSZK9XXaEgFXa-1028-160.jpg'  /img>
    <img alt='韵达快递' height='40'  src='http://www.yunda56.com/cn/images/ky_images/logo.png'  /img>
    <img alt='波司登' height='40'  src='https://img.alicdn.com/tfs/TB12cmCouL2gK0jSZFmXXc7iXXa-310-110.jpg'  /img>
    <img alt='凯京科技' height='40'  src='https://img.alicdn.com/tfs/TB1j0dEop67gK0jSZPfXXahhFXa-400-208.jpg'  /img>
    <img alt='点购集团' height='40'  src='https://dgmall-1258058953.cos.ap-chengdu.myqcloud.com/img/logo_t.png'  /img>
    <img alt='求是创新健康' height='40'  src='http://www.truthai.cn/static/logo800.png'  /img>
    <img alt='TCL' height='40'  src='https://img.alicdn.com/tfs/TB1oHThw.Y1gK0jSZFCXXcwqXXa-214-200.png'  /img>
    <img alt='科蓝' height='40'  src='https://img.alicdn.com/tfs/TB1tuSyouT2gK0jSZFvXXXnFXXa-304-94.jpg'  /img>
    <img alt='康美药业' height='40'  src='https://www.kanghehealth.com/images/logo.png'  /img>
    <img alt='雁联' height='40'  src='https://img.alicdn.com/tfs/TB1c8iCouL2gK0jSZFmXXc7iXXa-428-102.jpg'  /img>
    <img alt='学两手' height='40'  src='https://img.xue2shou.com/g-xue2shou/website/0.8.2/static/logo.png'  /img>
    <img alt='衣二三' height='40'  src='https://img.alicdn.com/tfs/TB1OCGioCf2gK0jSZFPXXXsopXa-500-179.jpg'  /img>
    <img alt='悦途出行' height='40'  src='http://yuetu365.com/uploads/allimg/20191016/d456dbbee0c54274a70d588af4ce6116.png'  /img>
    <img alt='睿颐软件' height='40'  src='https://img.alicdn.com/tfs/TB143R4op67gK0jSZPfXXahhFXa-148-42.png'  /img>
    <img alt='有利网' height='40'  src='https://www.yooli.com/v2/local/img/common/logo.png?version=20191126190304'  /img>
    <img alt='赛维' height='40'  src='http://www.savor.com.cn/common/img/logo.png'  /img>
    <img alt='安心保险' height='40'  src='https://query.95303.com/webins/images/logo.png'  /img>
    <img alt='科达科技' height='40'  src='https://img.alicdn.com/tfs/TB1JvOjouT2gK0jSZFvXXXnFXXa-386-146.jpg'  /img>
    <img alt='会分期' height='40'  src='https://img.alicdn.com/tfs/TB1ChKFoBr0gK0jSZFnXXbRRXXa-402-166.jpg'  /img>
    <img alt='会找房' height='40'  src='https://img.alicdn.com/tfs/TB1bNWFoBr0gK0jSZFnXXbRRXXa-398-336.jpg'  /img>
    <img alt='全房通' height='40'  src='https://img.alicdn.com/tfs/TB1iMSAopP7gK0jSZFjXXc5aXXa-398-182.jpg'  /img>
    <img alt='会通教育' height='40'  src='https://img.alicdn.com/tfs/TB1_D9Boxn1gK0jSZKPXXXvUXXa-580-218.jpg'  /img>
    <img alt='享住智慧' height='40'  src='http://image.xiangzhuzhihui.com/images/logo/logo_02.png'  /img>
    <img alt='兰亮网络' height='40'  src='https://img.alicdn.com/tfs/TB1_miroq61gK0jSZFlXXXDKFXa-283-70.png'  /img>
    <img alt='蓝天教育' height='40'  src='https://img.alicdn.com/tfs/TB1CaSroAT2gK0jSZPcXXcKkpXa-492-176.jpg'  /img>
    <img alt='烟台欣合' height='40'  src='https://shinhoglobal.com/img/logo-shinho.svg'  /img>
    <img alt='阿康健康' height='40'  src='https://img.alicdn.com/tfs/TB1JNSqouH2gK0jSZFEXXcqMpXa-450-182.jpg'  /img>
    <img alt='新脉远' height='40'  src='https://img.alicdn.com/tfs/TB1NV1uouH2gK0jSZJnXXaT1FXa-462-172.jpg'  /img>
    <img alt='乾动新能源' height='40'  src='http://www.cangowin.com/images/logo.png'  /img>
    <img alt='路客精品民宿' height='40'  src='https://img.alicdn.com/tfs/TB1CCavoBr0gK0jSZFnXXbRRXXa-240-100.png'  /img>
    <img alt='深圳好尔美' height='40'  src='https://img.alicdn.com/tfs/TB1IIivoxD1gK0jSZFyXXciOVXa-200-130.png'  /img>
    <img alt='浙大睿医' height='40'  src='https://img.alicdn.com/tfs/TB1kQThrFY7gK0jSZKzXXaikpXa-220-110.jpg'  /img>
    <img alt='居然之家' height='40'  src='https://img.alicdn.com/tfs/TB1LK6jrUT1gK0jSZFrXXcNCXXa-180-54.png'  /img>
    <img alt='臻善科技' height='40'  src='http://www.gisquest.com/static/web/img/img-1.png?v=v3'  /img>
    <img alt='中国支付通' height='40'  src='https://img.alicdn.com/tfs/TB1VGpTFET1gK0jSZFrXXcNCXXa-193-55.png'  /img>
    <img alt='众网小贷' height='40'  src='https://img.alicdn.com/tfs/TB19Y8XFEY1gK0jSZFMXXaWcVXa-160-60.png'  /img>
    <img alt='谐云科技' height='40'  src='https://img.alicdn.com/tfs/TB1V1YlrRv0gK0jSZKbXXbK2FXa-514-160.png'  /img>
    <img alt='浙江甄品' height='40'  src='https://img.alicdn.com/tfs/TB1oC2prND1gK0jSZFyXXciOVXa-246-124.jpg'  /img>
    <img alt='深圳海豚网' height='40'  src='https://img.alicdn.com/tfs/TB1defkrLb2gK0jSZK9XXaEgFXa-434-146.jpg'  /img>
    <img alt='汇通天下' height='40'  src='https://img.alicdn.com/tfs/TB1uIHmrHr1gK0jSZR0XXbP8XXa-1024-568.png'  /img>
    <img alt='九机网' height='40'  src='https://img.alicdn.com/tfs/TB1ERHlrUY1gK0jSZFMXXaWcVXa-120-60.png'  /img>
    <img alt='有好东西' height='40'  src='https://img.alicdn.com/tfs/TB1LT2lrNn1gK0jSZKPXXXvUXXa-300-300.jpg'  /img>
    <img alt='南京智慧盾' height='40'  src='https://img.alicdn.com/tfs/TB1s2LprUY1gK0jSZFCXXcwqXXa-618-148.jpg'  /img>
    <img alt='数跑科技' height='40'  src='https://img.alicdn.com/tfs/TB1qtGew7T2gK0jSZPcXXcKkpXa-294-104.png'  /img>
    <img alt='拉粉粉' height='40'  src='https://www.lafenfen.cn/img/icon03.png'  /img> 
    <img alt='汇通达' height='40'  src='https://img.alicdn.com/tfs/TB1KVJ9wWL7gK0jSZFBXXXZZpXa-145-59.png'  /img>
    <img alt='财新传媒' height='40'  src='http://file.caixin.com/file/content/images/new/logo_bottom.png'  /img>
    <img alt='易宝支付' height='40'  src='https://img.alicdn.com/tfs/TB1vWafw7T2gK0jSZFkXXcIQFXa-301-100.png'  /img>
    <img alt='维恩贝特' height='40'  src='http://www.vivebest.com/templates/crs/images/vnb_logo.png'  /img>
    <img alt='八库' height='40' src='https://img.alicdn.com/tfs/TB1hC5cwVY7gK0jSZKzXXaikpXa-318-134.png'  /img>
    <img alt='大诚若谷' height='40'  src='https://img.alicdn.com/tfs/TB1VuPhw4D1gK0jSZFyXXciOVXa-294-124.png'  /img>
    <img alt='成都数智索' height='40'  src='https://img.alicdn.com/tfs/TB1oJKiw4D1gK0jSZFyXXciOVXa-2053-377.png'  /img>  
     <img alt='北京超图' height='40'  src='https://img.alicdn.com/tfs/TB1eKFXFEz1gK0jSZLeXXb9kVXa-163-54.png'  /img>
    <img alt='深圳易佰' height='40'  src='https://img.alicdn.com/tfs/TB1gkXaFrr1gK0jSZR0XXbP8XXa-187-57.png'  /img>
    <img alt='宿迁民丰农商银行' height='40'  src='https://img.alicdn.com/tfs/TB1bH5fw7L0gK0jSZFAXXcA9pXa-442-39.png'  /img>
    <img alt='杭州喜团科技' height='40'  src='https://img.alicdn.com/tfs/TB1IXqgwYj1gK0jSZFuXXcrHpXa-197-58.png'  /img>
    <img alt='上海海智在线' height='40' src='https://img.alicdn.com/tfs/TB1xAJUFy_1gK0jSZFqXXcpaXXa-320-80.jpg'  /img>
    <img alt='丞家（上海）公寓管理' height='40'  src='https://image.cjia.com/website/apartment/webresource/image/logo_8f2f47fe.png'  /img>
    <img alt='安徽国科新材科' height='40'  src='https://img.alicdn.com/tfs/TB1ICJfFuH2gK0jSZJnXXaT1FXa-654-232.png'  /img>
    <img alt='易点生活' height='40'  src='https://img.alicdn.com/tfs/TB1AdI5FeL2gK0jSZPhXXahvXXa-1518-542.jpg'  /img>
    <img alt='商银信支付' height='40' src='https://img.alicdn.com/tfs/TB1rxndw4n1gK0jSZKPXXXvUXXa-150-68.png'   /img>
    <img alt='钛师傅云' height='40'  src='https://www.tsfyun.com/images/logo.png'  /img>
    <img alt='广州力生信息' height='40'  src='https://img.alicdn.com/tfs/TB1m0FcFuH2gK0jSZFEXXcqMpXa-139-48.png'  /img>
    <img alt='杭州启舰科技有限公司' height='40'  src='http://www.qijian-tech.com/assets/onepage/img/logo/red.png'  /img>
    <img alt='上海美浮特' height='40'  src='https://img.alicdn.com/tfs/TB1uUtaFuT2gK0jSZFvXXXnFXXa-370-45.jpg'  /img>    
    <img alt='杭州中威慧云医疗科技有限公司' height='40'  src='https://img.alicdn.com/tfs/TB1iqo_FaL7gK0jSZFBXXXZZpXa-361-54.jpg'  /img> 
    <img alt='易族智汇（北京）' height='40'  src='http://www.javamall.com.cn/images/logonew.jpg'  /img> 
    <img alt='佛山宅无限' height='40'  src='https://zwxnetwork.oss-cn-shenzhen.aliyuncs.com/static/temporary_official_website/logo.png'  /img>     
    <img alt='F5未来商店' height='40'  src='https://cdn.f5-store.cn/front_end/common_images/logo.png'  /img>  
    <img alt='甄品信息科技' height='40'  src='https://img.alicdn.com/tfs/TB1SxJWFEY1gK0jSZFCXXcwqXXa-185-65.png'  /img>  
    <img alt='行云全球汇跨境电商（杭州分部）' height='40'  src='http://www.xyb2b.com/_nuxt/img/5e5584f.png'  /img>  
    <img alt='世纪加华' height='40'  src='https://zhengxin-pub.bj.bcebos.com/logopic/a4ff4990e2ba2d57c90e8d16c649b952_fullsize.jpg?x-bce-process=image/resize,m_lfit,w_200'  /img>  
    <img alt='海牛电子商务' height='40'  src='http://www.hainiuec.com/public/assets/addons/cms/img/company-logo.png'  /img>    
    <img alt='杭州华网信息' height='40'  src='https://img.alicdn.com/tfs/TB1FFX6FqL7gK0jSZFBXXXZZpXa-288-101.png'  /img>   
    <img alt='快陪练' height='40'  src='https://img.alicdn.com/tfs/TB1rhNRFAL0gK0jSZFtXXXQCXXa-321-96.png'  /img> 
    <img alt='西南石油大学' height='40'  src='https://dss2.bdstatic.com/6Ot1bjeh1BF3odCf/it/u=829617221,290823158&fm=74&app=80&f=JPEG&size=f121,121?sec=1880279984&t=b0b603710dd0af061a278d11cfe327ae'  /img> 
    <img alt='领课网络' height='40'  src='https://img.alicdn.com/tfs/TB18TNRFEz1gK0jSZLeXXb9kVXa-244-60.jpg'  /img> 
    <img alt='美通社' height='40'  src='https://img.alicdn.com/tfs/TB1i1JTFCf2gK0jSZFPXXXsopXa-151-60.png'  /img> 
    <img alt='睿维科技有限公司' height='40'  src='https://img.alicdn.com/tfs/TB1ztXXFpY7gK0jSZKzXXaikpXa-179-60.png'  /img> 
    <img alt='郑州信源信息技术' height='40'  src='https://img.alicdn.com/tfs/TB1SkJ9FuT2gK0jSZFvXXXnFXXa-266-56.png'  /img>     
    <img alt='荣怀集团' height='40'  src='https://img.alicdn.com/tfs/TB1AzbWgZKfxu4jSZPfXXb3dXXa-1117-382.png'  /img>  
    <img alt='浙江群集大数据科技有限公司' height='40'  src='https://img.alicdn.com/tfs/TB1HtFZFq61gK0jSZFlXXXDKFXa-1375-214.png'  /img>  
    <img alt='北京易点租有限公司' height='40'  src='https://img.alicdn.com/tfs/TB1nax.FuH2gK0jSZFEXXcqMpXa-336-154.png'  /img>  
    </div>

https://www.cnblogs.com/kaleidoscope/p/9627573.html

	问题的起源

	在电商等业务中，系统一般由多个独立的服务组成，如何解决分布式调用时候数据的一致性？

	具体业务场景如下，比如一个业务操作，如果同时调用服务 A、B、C，需要满足要么同时成功；要么同时失败。A、B、C 可能是多个不同部门开发、部署在不同服务器上的远程服务。

	在分布式系统来说，如果不想牺牲一致性，CAP 理论告诉我们只能放弃可用性，这显然不能接受。为了便于讨论问题，先简单介绍下数据一致性的基础理论。

	强一致

	    当更新操作完成之后，任何多个后续进程或者线程的访问都会返回最新的更新过的值。这种是对用户最友好的，就是用户上一次写什么，下一次就保证能读到什么。根据 CAP 理论，这种实现需要牺牲可用性。


	弱一致性

	    系统并不保证续进程或者线程的访问都会返回最新的更新过的值。系统在数据写入成功之后，不承诺立即可以读到最新写入的值，也不会具体的承诺多久之后可以读到。


	最终一致性

	    弱一致性的特定形式。系统保证在没有后续更新的前提下，系统最终返回上一次更新操作的值。在没有故障发生的前提下，不一致窗口的时间主要受通信延迟，系统负载和复制副本的个数影响。DNS 是一个典型的最终一致性系统。



	在工程实践上，为了保障系统的可用性，互联网系统大多将强一致性需求转换成最终一致性的需求，并通过系统执行幂等性的保证，保证数据的最终一致性。但在电商等场景中，对于数据一致性的解决方法和常见的互联网系统（如 MySQL 主从同步）又有一定区别，群友的讨论分成以下 6 种解决方案。


	1. 规避分布式事务——业务整合

	业务整合方案主要采用将接口整合到本地执行的方法。拿问题场景来说，则可以将服务 A、B、C 整合为一个服务 D 给业务，这个服务 D 再通过转换为本地事务的方式，比如服务 D 包含本地服务和服务 E，而服务 E 是本地服务 A ~ C 的整合。

	优点：解决（规避）了分布式事务。

	缺点：显而易见，把本来规划拆分好的业务，又耦合到了一起，业务职责不清晰，不利于维护。

	由于这个方法存在明显缺点，通常不建议使用。


	2. 经典方案 - eBay 模式

	此方案的核心是将需要分布式处理的任务通过消息日志的方式来异步执行。消息日志可以存储到本地文本、数据库或消息队列，再通过业务规则自动或人工发起重试。人工重试更多的是应用于支付场景，通过对账系统对事后问题的处理。
	消息日志方案的核心是保证服务接口的幂等性。

	考虑到网络通讯失败、数据丢包等原因，如果接口不能保证幂等性，数据的唯一性将很难保证。



	eBay 方式的主要思路如下。

	Base：一种 Acid 的替代方案

	此方案是 eBay 的架构师 Dan Pritchett 在 2008 年发表给 ACM 的文章，是一篇解释 BASE 原则，或者说最终一致性的经典文章。文中讨论了 BASE 与 ACID 原则在保证数据一致性的基本差异。

	如果 ACID 为分区的数据库提供一致性的选择，那么如何实现可用性呢？答案是

	BASE (basically available, soft state, eventually consistent)

	BASE 的可用性是通过支持局部故障而不是系统全局故障来实现的。下面是一个简单的例子：如果将用户分区在 5 个数据库服务器上，BASE 设计鼓励类似的处理方式，一个用户数据库的故障只影响这台特定主机那 20% 的用户。这里不涉及任何魔法，不过它确实可以带来更高的可感知的系统可用性。

	文章中描述了一个最常见的场景，如果产生了一笔交易，需要在交易表增加记录，同时还要修改用户表的金额。这两个表属于不同的远程服务，所以就涉及到分布式事务一致性的问题。

	文中提出了一个经典的解决方法，将主要修改操作以及更新用户表的消息放在一个本地事务来完成。同时为了避免重复消费用户表消息带来的问题，达到多次重试的幂等性，增加一个更新记录表 updates_applied 来记录已经处理过的消息。

	系统的执行伪代码如下



	基于以上方法，在第一阶段，通过本地的数据库的事务保障，增加了 transaction 表及消息队列 。

	在第二阶段，分别读出消息队列（但不删除），通过判断更新记录表 updates_applied 来检测相关记录是否被执行，未被执行的记录会修改 user 表，然后增加一条操作记录到 updates_applied，事务执行成功之后再删除队列。

	通过以上方法，达到了分布式系统的最终一致性。进一步了解 eBay 的方案可以参考文末链接。


	3. 去哪儿网分布式事务方案

	随着业务规模不断地扩大，电商网站一般都要面临拆分之路。就是将原来一个单体应用拆分成多个不同职责的子系统。比如以前可能将面向用户、客户和运营的功能都放在一个系统里，现在拆分为订单中心、代理商管理、运营系统、报价中心、库存管理等多个子系统。

	拆分首先要面临的是什么呢？

	最开始的单体应用所有功能都在一起，存储也在一起。比如运营要取消某个订单，那直接去更新订单表状态，然后更新库存表就 ok 了。因为是单体应用，库在一起，这些都可以在一个事务里，由关系数据库来保证一致性。

	但拆分之后就不同了，不同的子系统都有自己的存储。比如订单中心就只管理自己的订单库，而库存管理也有自己的库。那么运营系统取消订单的时候就是通过接口调用等方式来调用订单中心和库存管理的服务了，而不是直接去操作库。这就涉及一个『分布式事务』的问题。



	分布式事务有两种解决方式

	1. 优先使用异步消息。

	上文已经说过，使用异步消息 Consumer 端需要实现幂等。

	幂等有两种方式，一种方式是业务逻辑保证幂等。比如接到支付成功的消息订单状态变成支付完成，如果当前状态是支付完成，则再收到一个支付成功的消息则说明消息重复了，直接作为消息成功处理。

	另外一种方式如果业务逻辑无法保证幂等，则要增加一个去重表或者类似的实现。对于 producer 端在业务数据库的同实例上放一个消息库，发消息和业务操作在同一个本地事务里。发消息的时候消息并不立即发出，而是向消息库插入一条消息记录，然后在事务提交的时候再异步将消息发出，发送消息如果成功则将消息库里的消息删除，如果遇到消息队列服务异常或网络问题，消息没有成功发出那么消息就留在这里了，会有另外一个服务不断地将这些消息扫出重新发送。



	2. 有的业务不适合异步消息的方式，事务的各个参与方都需要同步的得到结果。这种情况的实现方式其实和上面类似，每个参与方的本地业务库的同实例上面放一个事务记录库。

	比如 A 同步调用 B，C。A 本地事务成功的时候更新本地事务记录状态，B 和 C 同样。如果有一次 A 调用 B 失败了，这个失败可能是 B 真的失败了，也可能是调用超时，实际 B 成功。则由一个中心服务对比三方的事务记录表，做一个最终决定。假设现在三方的事务记录是 A 成功，B 失败，C 成功。那么最终决定有两种方式，根据具体场景：

	    重试 B，直到 B 成功，事务记录表里记录了各项调用参数等信息；

	    执行 A 和 B 的补偿操作(一种可行的补偿方式是回滚)。

	对 b 场景做一个特殊说明：比如 B 是扣库存服务，在第一次调用的时候因为某种原因失败了，但是重试的时候库存已经变为 0，无法重试成功，这个时候只有回滚 A 和 C 了。

	那么可能有人觉得在业务库的同实例里放消息库或事务记录库，会对业务侵入，业务还要关心这个库，是否一个合理的设计？

	实际上可以依靠运维的手段来简化开发的侵入，我们的方法是让 DBA 在公司所有 MySQL 实例上预初始化这个库，通过框架层（消息的客户端或事务 RPC 框架）透明的在背后操作这个库，业务开发人员只需要关心自己的业务逻辑，不需要直接访问这个库。

	总结起来，其实两种方式的根本原理是类似的，也就是将分布式事务转换为多个本地事务，然后依靠重试等方式达到最终一致性。


	4. 蘑菇街交易创建过程中的分布式一致性方案
	交易创建的一般性流程

	我们把交易创建流程抽象出一系列可扩展的功能点，每个功能点都可以有多个实现（具体的实现之间有组合/互斥关系）。把各个功能点按照一定流程串起来，就完成了交易创建的过程。


	面临的问题

	每个功能点的实现都可能会依赖外部服务。那么如何保证各个服务之间的数据是一致的呢？比如锁定优惠券服务调用超时了，不能确定到底有没有锁券成功，该如何处理？再比如锁券成功了，但是扣减库存失败了，该如何处理？


	方案选型

	服务依赖过多，会带来管理复杂性增加和稳定性风险增大的问题。试想如果我们强依赖 10 个服务，9 个都执行成功了，最后一个执行失败了，那么是不是前面 9 个都要回滚掉？这个成本还是非常高的。

	所以在拆分大的流程为多个小的本地事务的前提下，对于非实时、非强一致性的关联业务写入，在本地事务执行成功后，我们选择发消息通知、关联事务异步化执行的方案。

	消息通知往往不能保证 100% 成功；且消息通知后，接收方业务是否能执行成功还是未知数。前者问题可以通过重试解决；后者可以选用事务消息来保证。

	但是事务消息框架本身会给业务代码带来侵入性和复杂性，所以我们选择基于 DB 事件变化通知到 MQ 的方式做系统间解耦，通过订阅方消费 MQ 消息时的 ACK 机制，保证消息一定消费成功，达到最终一致性。由于消息可能会被重发，消息订阅方业务逻辑处理要做好幂等保证。

	所以目前只剩下需要实时同步做、有强一致性要求的业务场景了。在交易创建过程中，锁券和扣减库存是这样的两个典型场景。

	要保证多个系统间数据一致，乍一看，必须要引入分布式事务框架才能解决。但引入非常重的类似二阶段提交分布式事务框架会带来复杂性的急剧上升；在电商领域，绝对的强一致是过于理想化的，我们可以选择准实时的最终一致性。

	我们在交易创建流程中，首先创建一个不可见订单，然后在同步调用锁券和扣减库存时，针对调用异常（失败或者超时），发出废单消息到MQ。如果消息发送失败，本地会做时间阶梯式的异步重试；优惠券系统和库存系统收到消息后，会进行判断是否需要做业务回滚，这样就准实时地保证了多个本地事务的最终一致性。


	5. 支付宝及蚂蚁金融云的分布式服务 DTS 方案

	业界常用的还有支付宝的一种 xts 方案，由支付宝在 2PC 的基础上改进而来。主要思路如下，大部分信息引用自官方网站。
	分布式事务服务简介

	分布式事务服务 (Distributed Transaction Service, DTS) 是一个分布式事务框架，用来保障在大规模分布式环境下事务的最终一致性。DTS 从架构上分为 xts-client 和 xts-server 两部分，前者是一个嵌入客户端应用的 JAR 包，主要负责事务数据的写入和处理；后者是一个独立的系统，主要负责异常事务的恢复。


	核心特性

	传统关系型数据库的事务模型必须遵守 ACID 原则。在单数据库模式下，ACID 模型能有效保障数据的完整性，但是在大规模分布式环境下，一个业务往往会跨越多个数据库，如何保证这多个数据库之间的数据一致性，需要其他行之有效的策略。在 JavaEE 规范中使用 2PC (2 Phase Commit, 两阶段提交) 来处理跨 DB 环境下的事务问题，但是 2PC 是反可伸缩模式，也就是说，在事务处理过程中，参与者需要一直持有资源直到整个分布式事务结束。这样，当业务规模达到千万级以上时，2PC 的局限性就越来越明显，系统可伸缩性会变得很差。基于此，我们采用 BASE 的思想实现了一套类似 2PC 的分布式事务方案，这就是 DTS。DTS在充分保障分布式环境下高可用性、高可靠性的同时兼顾数据一致性的要求，其最大的特点是保证数据最终一致 (Eventually consistent)。

	简单的说，DTS 框架有如下特性：

	    最终一致：事务处理过程中，会有短暂不一致的情况，但通过恢复系统，可以让事务的数据达到最终一致的目标。

	    协议简单：DTS 定义了类似 2PC 的标准两阶段接口，业务系统只需要实现对应的接口就可以使用 DTS 的事务功能。

	    与 RPC 服务协议无关：在 SOA 架构下，一个或多个 DB 操作往往被包装成一个一个的 Service，Service 与 Service 之间通过 RPC 协议通信。DTS 框架构建在 SOA 架构上，与底层协议无关。

	    与底层事务实现无关： DTS 是一个抽象的基于 Service 层的概念，与底层事务实现无关，也就是说在 DTS 的范围内，无论是关系型数据库 MySQL，Oracle，还是 KV 存储 MemCache，或者列存数据库 HBase，只要将对其的操作包装成 DTS 的参与者，就可以接入到 DTS 事务范围内。



	以下是分布式事务框架的流程图

	实现

	    一个完整的业务活动由一个主业务服务与若干从业务服务组成。

	    主业务服务负责发起并完成整个业务活动。

	    从业务服务提供 TCC 型业务操作。

	业务活动管理器控制业务活动的一致性，它登记业务活动中的操作，并在活动提交时确认所有的两阶段事务的 confirm 操作，在业务活动取消时调用所有两阶段事务的 cancel 操作。”


	与 2PC 协议比较

	    没有单独的 Prepare 阶段，降低协议成本

	    系统故障容忍度高，恢复简单


	6. 农信网数据一致性方案
	1. 电商业务

	公司的支付部门，通过接入其它第三方支付系统来提供支付服务给业务部门，支付服务是一个基于 Dubbo 的 RPC 服务。

	对于业务部门来说，电商部门的订单支付，需要调用

	    支付平台的支付接口来处理订单；

	    同时需要调用积分中心的接口，按照业务规则，给用户增加积分。

	从业务规则上需要同时保证业务数据的实时性和一致性，也就是支付成功必须加积分。

	我们采用的方式是同步调用，首先处理本地事务业务。考虑到积分业务比较单一且业务影响低于支付，由积分平台提供增加与回撤接口。

	具体的流程是先调用积分平台增加用户积分，再调用支付平台进行支付处理，如果处理失败，catch 方法调用积分平台的回撤方法，将本次处理的积分订单回撤。

	2. 用户信息变更

	公司的用户信息，统一由用户中心维护，而用户信息的变更需要同步给各业务子系统，业务子系统再根据变更内容，处理各自业务。用户中心作为 MQ 的 producer，添加通知给 MQ。APP Server 订阅该消息，同步本地数据信息，再处理相关业务比如 APP 退出下线等。

	我们采用异步消息通知机制，目前主要使用 ActiveMQ，基于 Virtual Topic 的订阅方式，保证单个业务集群订阅的单次消费。

	总结

	分布式服务对衍生的配套系统要求比较多，特别是我们基于消息、日志的最终一致性方案，需要考虑消息的积压、消费情况、监控、报警等。




