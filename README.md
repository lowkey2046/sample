
### <a name="流程设计器"></a>流程设计器
*  `-`<a name="常用的几种流程设计器"></a>常用的几种流程设计器：
        
*  <a name="安装流程设计器"></a>安装流程设计器（以Activiti Designer为例）：  
        1.插件 
        2.把压缩包中的内容放入eclipse根目录的dropins文件夹  
        3.重启eclipse，点击新建工程new->Other…打开面板，如果看到下图内容： 
         <div align=center>
         
* <a name="使用流程设计器建立流程模型"></a>使用流程设计器建立流程模型(以精准营销demo的流程模型为例)：
   - `-`流程解析：
   		* 1) 精准营销流程图：此流程图由1个起始节点、一个排他网关（ExclusiveGateWay）、5个(userTask)处理人节点、一个结束节点组成，其中会计主管属性为多实例（Multi instance）userTask。
              <div align=center>
           
       *  2) palette拖拽工具：使用palette拖拽构建流程模型
              <div align=center>
          
       *  3) 设置属性
       	  * 设置流程主键processKey（通过点击流程图空白处设置）
       	     <div align=center>
         
       	  * 设置单实例userTask属性   
       	       *  设置id和name  
                          
               *  nrOfInstantces:实例的总数量   
               *  nrOfActiveInstances:当前活动的数量，未完成的实例，对于串行，这个参数的值始终是1   
               *  nrOfCompletedInstances:已经完成的实例数量  
               *  isSequential属性指定这个任务的实例是并行执行还是串行执行  
        *  4) bpmn文件（precision_marketing.bpmn）：通过流程设计器完成建模之后能够生成一个对应的bpnm文件。  
              内容主要部分为以下：
              标签含义：  
                    *  <process>标签代表流程模型  
                    *  <startEvent>代表起始节点  
                    *  <userTask>代表代理人 ，其中assignee通过el表达式写法可将代理人设置成流程变量
                    *  <multiInstanceLoopCharacteristics>代表此节点可以存在多个代理人
                    *  <completionCondition>多实例节点完成条件   
                    *  <sequenceFlow>代表每个节点间流程线，其中如有存在CDATA 且其中有对应el表达式，则需要传对应表达式中的参数才能执行该条线路

   