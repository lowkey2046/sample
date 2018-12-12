# 统一工作流引擎简介 （v1.0）

Hello there! I’m **Workflow Engine** ：）  

- `-` [**目录**]() 
	* [**什么是工作流引擎（Workflow Engine ）**](#什么是工作流引擎)
	* [**工作流引擎优势**](#工作流引擎优势)
	* [**工作原理**](#工作原理)
	* [**流程设计器**](#流程设计器)
		* [**常用的几种流程设计器**](#常用的几种流程设计器)
		* [**安装流程设计器**](#安装流程设计器)
		* [**使用流程设计器建立流程模型**](#使用流程设计器建立流程模型)
	* [**发布流程**](#发布流程)
	* [**接口调用说明**](#接口调用说明)


 

### <a name="什么是工作流引擎"></a>什么是工作流引擎（Workflow Engine ）
* 例如开发一个系统最关键的部分不是系统的界面，也不是和数据库之间的信息交换，而是如何根据业务逻辑开发出符合实际需要的程序逻辑并确保其稳定性、易维护性（模块化和结构化）和弹性（容易根据实际业务逻辑的变化作出程序上的变动，例如决策权的改变、组织结构的变动和由于业务方向的变化产生的全新业务逻辑等等）。**Workflow 引擎**解决的就是这个问题：如果应用程序缺乏强大的逻辑层，势必变得容易出错（信息的路由错误、死循环等等）

### <a name="工作流引擎优势"></a>工作流引擎优势
* 通用		
	* 提供通用型restful api，支持跨域、跨技术平台、适应各种场景的流程架构服务。
* 高效
	* 根据真实业务场景，通过流程设计器构建流程模型，部署流程文件发布就能使用该流程服务。
* 安全
   * 具有高可维护性，统一的流程数据存储，方便数据移植、修改、备份等维护管理，避免数据丢失或出现数据不同步问题。 
* 灵活
   * 流程模型支持重构、迭代更新，流程模型能及时根据业务流程改变而调整。
* 稳定
	* 作为单独运载的服务，不受业务系统影响，服务更加稳定。
	
### <a name="工作原理"></a>工作原理
通过[**流程设计器**](#流程设计器)设计流程模型,[**发布流程**](#发布流程)后，调用流程引擎提供的restful api，流程引擎将处理发布流程，解析、执行、创建、管理（任务、流程实例）、查询历史等行为，以jsonp形式反馈结果信息。

### <a name="流程设计器"></a>流程设计器
*  `-`<a name="常用的几种流程设计器"></a>常用的几种流程设计器：

        1.Activiti Modeler，基于web的流程设计器。
        2.Eclipse的流程设计器插件  Activiti Designer（功能齐全，推荐使用）
        3.idea的流程设计器插件 actiBpm（部分功能缺失，体验较差不推荐）
        
*  <a name="安装流程设计器"></a>安装流程设计器（以Activiti Designer为例）：  
        1.插件 ![eclipse插件](https://gitee.com/mucho/SpringBoot_activiti/raw/master/src/main/resources/static/docImage/activiti_plugin.jpeg)   
        2.把压缩包中的内容放入eclipse根目录的dropins文件夹  
        3.重启eclipse，点击新建工程new->Other…打开面板，如果看到下图内容： 
         <div align=center>
         ![eclipse插件界面](https://gitee.com/mucho/SpringBoot_activiti/raw/master/src/main/resources/static/docImage/eclipse_activiti_plugin.png)
* <a name="使用流程设计器建立流程模型"></a>使用流程设计器建立流程模型(以精准营销demo的流程模型为例)：
   - `-`流程解析：
   		* 1) 精准营销流程图：此流程图由1个起始节点、一个排他网关（ExclusiveGateWay）、5个(userTask)处理人节点、一个结束节点组成，其中会计主管属性为多实例（Multi instance）userTask。
              <div align=center>
           ![精准营销流程图](https://gitee.com/mucho/SpringBoot_activiti/raw/master/src/main/resources/static/docImage/precision_marketing_workflow.png)
       *  2) palette拖拽工具：使用palette拖拽构建流程模型
              <div align=center>
           ![精准营销流程图](https://gitee.com/mucho/SpringBoot_activiti/raw/master/src/main/resources/static/docImage/palette.png)
       *  3) 设置属性
       	  * 设置流程主键processKey（通过点击流程图空白处设置）
       	     <div align=center>
          ![设置流程主键processKey](https://gitee.com/mucho/SpringBoot_activiti/raw/master/src/main/resources/static/docImage/setProcessKey.png)
       	  * 设置单实例userTask属性   
       	       *  设置id和name  
                   ![设置单实例userTask](https://gitee.com/mucho/SpringBoot_activiti/raw/master/src/main/resources/static/docImage/setUserTask.png)            
		       *  设置assignee（代理人采用el表达式设置变量）    
                   ![设置单实例userTask](https://gitee.com/mucho/SpringBoot_activiti/raw/master/src/main/resources/static/docImage/setUserTaskAssignee.png)  
          * 设置exclusivegateway（排他网关）
                *  设置两条分支flow的条件
                   ![设置flow条件](https://gitee.com/mucho/SpringBoot_activiti/raw/master/src/main/resources/static/docImage/flow3.png) 
                   ![设置flow条件](https://gitee.com/mucho/SpringBoot_activiti/raw/master/src/main/resources/static/docImage/flow4.png)    
                *  设置default flow       
                   ![设置flow条件](https://gitee.com/mucho/SpringBoot_activiti/raw/master/src/main/resources/static/docImage/exclusivegeteway.png) 
          * 设置多实例userTask  
                ![设置多实例userTask](https://gitee.com/mucho/SpringBoot_activiti/raw/master/src/main/resources/static/docImage/multUserTask1.png)   
                ![设置多实例userTask](https://gitee.com/mucho/SpringBoot_activiti/raw/master/src/main/resources/static/docImage/multUserTask2.png)     
               *  nrOfInstantces:实例的总数量   
               *  nrOfActiveInstances:当前活动的数量，未完成的实例，对于串行，这个参数的值始终是1   
               *  nrOfCompletedInstances:已经完成的实例数量  
               *  isSequential属性指定这个任务的实例是并行执行还是串行执行  
        *  4) bpmn文件（precision_marketing.bpmn）：通过流程设计器完成建模之后能够生成一个对应的bpnm文件。  
              内容主要部分为以下：
            ![bpmn文件](https://gitee.com/mucho/SpringBoot_activiti/raw/master/src/main/resources/static/docImage/bpmnImage.png)   
              标签含义：  
                    *  <process>标签代表流程模型  
                    *  <startEvent>代表起始节点  
                    *  <userTask>代表代理人 ，其中assignee通过el表达式写法可将代理人设置成流程变量
                    *  <multiInstanceLoopCharacteristics>代表此节点可以存在多个代理人
                    *  <completionCondition>多实例节点完成条件   
                    *  <sequenceFlow>代表每个节点间流程线，其中如有存在CDATA 且其中有对应el表达式，则需要传对应表达式中的参数才能执行该条线路
     
### <a name="发布流程"></a>发布流程 
 * 通过流程设计器建立完流程模型之后，将生成的bpmn格式文件通过流程发布web页发布流程，即可后续使用流程引擎接口服务。
    * web请求地址示例：
    ```
    http://${流程服务器地址}:9088/web/uploadProcess
    ```


### <a name="接口调用说明"></a>接口调用说明 
   *   流程引擎提供restful形式接口。 后台可直接调用解析，前端方面用ajax调用示例：   
   ```js
      $.ajax({     
           url:'http://[serviceUrl]:[port]/workFlow/startWF?processKey=processkey&...',                   
           type:'post',   
           dataType:'jsonp',   
           success:function(data){   
               alert("status:"+data[0].status+";msg:"+data[0].msg);   
           }  
        })   
      
   