---
title: "Стандартные конечные точки | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3fcb4225-addc-44f2-935d-30e4943a8812
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Стандартные конечные точки
Конечные точки определяются адресом, привязкой и контрактом.Кроме того, для конечной точки можно задать и другие параметры — конфигурацию поведения, заголовки и URI прослушивания.Эти значения не изменяются для определенных типов конечных точек.Например, конечные точки обмена метаданными всегда используют контракт <xref:System.ServiceModel.Description.IMetadataExchange>.Другим конечным точкам, например <xref:System.ServiceModel.Web.WebHttpEndpoint>, всегда требуется определенное поведение конечной точки.Конечную точку можно сделать более удобной для использования, определив значения по умолчанию для часто используемых свойств.Стандартные конечные точки дают разработчику возможность определить значения свойств по умолчанию, а также создавать конечные точки, где одно или несколько свойств не изменяются.Это позволяет не указывать данные статического характера.Стандартная конечная точка может использоваться в качестве конечной точки инфраструктуры и приложения.  
  
## Конечные точки инфраструктуры  
 Служба может включать конечные точки, некоторые из свойств которых реализованы автором службы неявным образом.Например, конечная точка обмена метаданными обеспечивает доступ по контракту <xref:System.ServiceModel.Description.IMetadataExchange>, однако автору службы не обязательно реализовывать этот интерфейс, он будет реализован WCF.Такие конечные точки инфраструктуры имеют значения по умолчанию для одного или более свойств, некоторые из которых могут быть неизменяемыми.Свойство <xref:System.ServiceModel.Description.ServiceEndpoint.Contract%2A> конечной точки обмена метаданными должно быть реализацией интерфейса <xref:System.ServiceModel.Description.IMetadataExchange>, в то время как другие свойства, например привязка, могут быть определены разработчиком.Конечные точки инфраструктуры определяются установкой свойства <xref:System.ServiceModel.Description.ServiceEndpoint.IsSystemEndpoint%2A> в значение `true`.  
  
## Конечные точки приложения  
 Разработчик приложения может определить свои стандартные конечные точки, определяющие значения по умолчанию для адреса, привязки или контракта.Определение стандартной конечной точки осуществляется через наследование класса <xref:System.ServiceModel.Description.ServiceEndpoint> и задание соответствующих свойств конечной точки.Могут быть предусмотрены значения по умолчанию для изменяемых свойств.Некоторые другие свойства будут иметь неизменяемые статические значения.Следующий пример демонстрирует процесс реализации стандартной конечной точки.  
  
```  
public class CustomEndpoint : ServiceEndpoint  
    {  
        public CustomEndpoint()  
            : this(string.Empty)  
        {  
        }  
  
        public CustomEndpoint(string address)  
            : this(address, ContractDescription.GetContract(typeof(ICalculator)))  
        {  
        }  
  
        // Create the custom endpoint with a fixed binding  
        public CustomEndpoint(string address, ContractDescription contract)  
            : base(contract)  
        {  
            this.Binding = new BasicHttpBinding();  
            this.IsSystemEndpoint = false;  
        }  
  
        // Definition of the additional property of this endpoint  
        public bool Property  
        {  
            get;  
            set;  
        }  
    }  
```  
  
 Чтобы использовать определенную пользователем настраиваемую конечную точку в файле конфигурации, необходимо унаследовать класс <xref:System.ServiceModel.Configuration.StandardEndpointElement>, унаследовать класс <xref:System.ServiceModel.Configuration.StandardEndpointCollectionElement>, а затем зарегистрировать новую стандартную конечную точку в разделе расширений в файле app.config или machine.config.<xref:System.ServiceModel.Configuration.StandardEndpointElement> обеспечивает поддержку настройки стандартной конечной точки, как показано в следующем примере.  
  
```  
public class CustomEndpointElement : StandardEndpointElement  
    {  
        // Definition of the additional property for the standard endpoint element  
        public bool Property  
        {  
            get { return (bool)base["property"]; }  
            set { base["property"] = value; }  
        }  
  
        // The additional property needs to be added to the properties of the standard endpoint element  
        protected override ConfigurationPropertyCollection Properties  
        {  
            get  
            {  
                ConfigurationPropertyCollection properties = base.Properties;  
                properties.Add(new ConfigurationProperty("property", typeof(bool), false, ConfigurationPropertyOptions.None));  
                return properties;  
            }  
        }  
  
        // Return the type of this standard endpoint  
        protected override Type EndpointType  
        {  
            get { return typeof(CustomEndpoint); }  
        }  
  
        // Create the custom service endpoint  
        protected override ServiceEndpoint CreateServiceEndpoint(ContractDescription contract)  
        {  
            return new CustomEndpoint();  
        }  
  
        // Read the value given to the property in config and save it  
        protected override void OnApplyConfiguration(ServiceEndpoint endpoint, ServiceEndpointElement serviceEndpointElement)  
        {  
            CustomEndpoint customEndpoint = (CustomEndpoint)endpoint;  
            customEndpoint.Property = this.Property;  
        }  
  
        // Read the value given to the property in config and save it  
        protected override void OnApplyConfiguration(ServiceEndpoint endpoint, ChannelEndpointElement channelEndpointElement)  
        {  
            CustomEndpoint customEndpoint = (CustomEndpoint)endpoint;  
            customEndpoint.Property = this.Property;  
        }  
  
        // No validation in this sample  
        protected override void OnInitializeAndValidate(ServiceEndpointElement serviceEndpointElement)  
        {  
        }  
  
        // No validation in this sample  
        protected override void OnInitializeAndValidate(ChannelEndpointElement channelEndpointElement)  
        {  
        }  
    }  
  
```  
  
 <xref:System.ServiceModel.Configuration.StandardEndpointCollectionElement> реализует резервный тип для коллекции, который появляется в разделе \<`standardEndpoints`\> конфигурации стандартной конечной точки.В следующем примере показана реализация этого класса.  
  
```  
public class CustomEndpointCollectionElement : StandardEndpointCollectionElement<CustomEndpoint, CustomEndpointElement>  
    {  
         // ...  
  
    }  
```  
  
 В следующем примере показана регистрация стандартной конечной точки в разделе расширений.  
  
```  
<extensions>  
      <standardEndpointExtensions>  
        <add  
          name="customStandardEndpoint"  
          type="CustomEndpointCollectionElement, Example.dll,  
                Version=1.0.0.0, Culture=neutral, PublicKeyToken=ffffffffffffffff"/>  
  
```  
  
## Настройка стандартной конечной точки  
 Стандартные конечные точки могут быть добавлены через код или в файле конфигурации.Чтобы добавить стандартную конечную точку через код, необходимо создать экземпляр соответствующего типа стандартной конечной точки и добавить его в узел службы, как показано в следующем примере:  
  
```csharp  
serviceHost.AddServiceEndpoint(new CustomEndpoint());  
```  
  
 Чтобы добавить стандартную конечную точку в файле конфигурации, добавьте элемент \<`endpoint`\> в элемент \<`service`\>, а все необходимые параметры конфигурации — в элемент \<`standardEndpoints`\>.В следующем примере показано добавление <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>, одной из стандартных конечных точек, поставляемых в составе [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)].  
  
```xml  
<services>  
  <service>  
    <endpoint isSystemEndpoint=”true” kind=”udpDiscoveryEndpoint” />  
  </service>  
</services>  
<standardEndpoints>    
  <udpDiscoveryEndpoint>  
     <standardEndpoint multicastAddress="soap.udp://239.255.255.250:3702" />   
  </udpDiscoveryEndpoint>  
</ standardEndpoints >  
```  
  
 Тип стандартной конечной точки указывается с помощью атрибута типа в элементе \<`endpoint`\>.Конечная точка настраивается в элементе \<`standardEndpoints`\>.В приведенном выше примере добавляется и настраивается конечная точка <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>.Элемент \<`udpDiscoveryEndpoint`\> содержит элемент \<`standardEndpoint`\>, в котором определяется свойство <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint.MulticastAddress%2A> для <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>.  
  
## Стандартные конечные точки, поставляемые в составе платформы .NET Framework  
 В приведенной ниже таблице перечислены стандартные конечные точки, которые поставляются в составе [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)].  
  
 `Mex Endpoint`  
 Стандартная конечная точка, используемая для отображения метаданных службы.  
  
 <xref:System.ServiceModel.Discovery.AnnouncementEndpoint>  
 Стандартная конечная точка, используемая службами для отправки сообщений объявления.  
  
 <xref:System.ServiceModel.Discovery.DiscoveryEndpoint>  
 Стандартная конечная точка, используемая службами для передачи сообщений обнаружения.  
  
 <xref:System.ServiceModel.Discovery.UdpDiscoveryEndpoint>  
 Стандартная конечная точка, заранее настроенная для операций обнаружения через привязку для многоадресной рассылки UDP.  
  
 <xref:System.ServiceModel.Discovery.UdpAnnouncementEndpoint>  
 Стандартная конечная точка, используемая службами для отправки сообщений объявления через привязку UDP.  
  
 <xref:System.ServiceModel.Discovery.DynamicEndpoint>  
 Стандартная конечная точка, которая использует WS\-Discovery для динамического обнаружения адреса конечной точки во время выполнения.  
  
 <xref:System.ServiceModel.Description.ServiceMetadataEndpoint>  
 Стандартная конечная точка для обмена метаданными.  
  
 <xref:System.ServiceModel.Description.WebHttpEndpoint>  
 Стандартная конечная точка с привязкой <xref:System.ServiceModel.WebHttpBinding>, которая автоматически добавляет поведение <xref:System.ServiceModel.Description.WebHttpBehavior>.  
  
 <xref:System.ServiceModel.Description.WebScriptEndpoint>  
 Стандартная конечная точка с привязкой <xref:System.ServiceModel.WebHttpBinding>, которая автоматически добавляет поведение <xref:System.ServiceModel.Description.WebScriptEnablingBehavior>.  
  
 <xref:System.ServiceModel.Description.WebServiceEndpoint>  
 Стандартная конечная точка с привязкой <xref:System.ServiceModel.WebHttpBinding>.  
  
 <xref:System.ServiceModel.Activities.WorkflowControlEndpoint>  
 Стандартная конечная точка, позволяющая вызывать операции управления для экземпляров рабочих процессов.  
  
 <xref:System.ServiceModel.Activities.WorkflowHostingEndpoint>  
 Стандартная конечная точка, поддерживающая создание рабочих процессов и возобновление закладок.