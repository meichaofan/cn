#  	创建服务
目前，微服务网关服务支持两种调用方式：通过API网关进行外部调用、通过VPC代理模式进行VPC应用间的调用。本文将介绍如何基于 京东云API网关 和 京东云微服务平台的微服务网关， 搭建应用的微服务网关。

## 操作场景
如果用户正在实施微服务转型，并在京东云微服务平台上已经创建了一组微服务应用。那么，可以按照如下流程创建一组微服务网关服务，来提供外部请求与各个微服务之间的调用服务。


## 准备工作

假设用户已经在京东云平台上，创建了自己的VPC，开通了微服务平台产品并且创建了注册中心，同时微服务应用也已部署到了该注册中心里。


## 操作步骤

1、	登录微服务平台控制台

2、	在左侧导航栏点击微服务网关，进入服务列表页

3、	在服务列表上方，点击创建微服务网关服务，进入创建页。

4、	设置服务信息，单击立即购买按钮，完成创建。创建完成后，将创建一个微服务网关服务实例。如需提供外网访问，推荐通过API网关提供服务。

![](../../../../../image/Internet-Middleware/JD-Distributed-Service-Framework/jdsfgw-create-1.png)


| 信息项 |说明 |
|---|---|
| 地域和可用区 | 推荐使用系统分配方式，可最大程度保障系统高可用。创建时请注意，不同地域资源内网不互通且创建后不可更改。  |
| 微服务网关服务名称 |  该服务的名称，将做为API网关和微服务网关的桥梁，且创建后不可修改。   |
| 创建方式-微服务网关通用方式 | 用于进行各个微服务的调用，为微服务网关通用方式。选择此种方式搭配API网关使用时，需要在API网关创建API分组过程中，选择API分组类型时，选择“微服务API分组”。    |
| 创建方式-VPC代理 | 提供VPC内服务调用的方式。选择此种方式搭配API网关使用时，需要在API网关创建API分组过程中，选择API分组类型时，选择”通用API分组”。|

| 注册中心&应用列表  | 1个微服务网关服务只能归属于1个注册中心，同时还需选择指明该注册中心下的哪些应用可以被该微服务网关服务所调用，未被勾选的应用将不能被网关服务发现。应用可在微服务网关服务创建成功后再按需增加删除。
|  QPS规格  | 目前产品按照规格提供计费依据  |


## 结合API网关的操作流程

接下来将介绍结合API网关的操作流程。在介绍前，默认用户已经做好如下准备工作：

-  用户已经开通API网关产品、微服务平台产品。

-  用户已经有VPC。

-  用户已经在微服务平台上创建完注册中心、部署完应用。

-  用户已知API网关产品的常用信息和流程。


###    通过API网关发布微服务网关服务的通用步骤

######  STEP 1：创建微服务网关服务。其中创建方式选择“微服务网关”。
 ![](../../../../../image/Internet-Middleware/JD-Distributed-Service-Framework/jdsfgw-create-1.png)

######  STEP2:创建API分组。其中API分组类型选择“微服务API分组”。

![](../../../../../image/Internet-Middleware/JD-Distributed-Service-Framework/jdsfgw-APIdetail-1.png)

创建完成的API分组信息如下：

![](../../../../../image/Internet-Middleware/JD-Distributed-Service-Framework/jdsfgw-APIdetail-2.png)
 
说明：第1步和第2步之间创建时无强制要求线后关系。



######  STEP3：互相绑定。
有两处入口提供绑定：

1、在API网关产品里进行绑定。可在创建的API分组列表页中，点击相应的分组信息的“绑定“操作。点击后将跳转至微服务网关列表页。


2、在微服务网关产品里进行绑定。

绑定操作信息：

![](../../../../../image/Internet-Middleware/JD-Distributed-Service-Framework/jdsfgw-bondAPI.png)

注意：API分组的每个发布环境里只能绑定唯一一个后端服务，因此当在“预发“环境里尚未绑定过任何微服务时可以被绑定；如果已经被绑定过其它微服务，将不能再进行绑定。


绑定完成后信息如下：
 ![](../../../../../image/Internet-Middleware/JD-Distributed-Service-Framework/jdsfgw-jbxx-3apilist.png)


######   STEP4：发布API分组。

发布完成后，用户即可通过API网关进行公网调用。发布API分组有两个入口：

1、可在微服务网关服务的API分组列表页中，直接点击发布。

![](../../../../../image/Internet-Middleware/JD-Distributed-Service-Framework/jdsfgw-fb-jdsf.png)


2、可在API网关产品中，点击发布。

![](../../../../../image/Internet-Middleware/JD-Distributed-Service-Framework/jdsfgw-fb-apigw.png)



####    通过API网关发布VPC代理服务步骤

STEP 1：创建微服务网关服务。其中创建方式选择“VPC代理”
 ![](../../../../../image/Internet-Middleware/JD-Distributed-Service-Framework/jdsfgw-create-2vpc.png)

STEP2:创建API分组。API分组类型选择“通用API分组”。

 ![](../../../../../image/Internet-Middleware/JD-Distributed-Service-Framework/jdsfgw-fb-apigw.png)


STEP3：发布。有两处入口提供绑定：

1、在API网关产品里进行发布。

 ![](../../../../../image/Internet-Middleware/JD-Distributed-Service-Framework/jdsfgw-fb-apigw.png)

2、在微服务网关产品里进行发布。

 ![](../../../../../image/Internet-Middleware/JD-Distributed-Service-Framework/jdsfgw-fb-jdsf.png)
	





