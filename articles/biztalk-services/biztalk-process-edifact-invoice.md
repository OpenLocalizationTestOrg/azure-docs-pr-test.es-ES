---
title: 'Tutorial: procesamiento de facturas de EDIFACT mediante Azure BizTalk Services | Microsoft Docs'
description: "¿Cómo toocreate y configurar la aplicación de conector de la caja o API de hello y utilizarlo en una aplicación de lógica en el servicio de aplicación de Azure"
services: biztalk-services
documentationcenter: .net,nodejs,java
author: msftman
manager: erikre
editor: 
ms.assetid: 7e0b93fa-3e2b-4a9c-89ef-abf1d3aa8fa9
ms.service: biztalk-services
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 05/31/2016
ms.author: deonhe
ms.openlocfilehash: 4ca021c9084b9b6540c93ef15fc3d44be0966970
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-process-edifact-invoices-using-azure-biztalk-services"></a>Tutorial: procesamiento de facturas de EDIFACT mediante los Servicios de BizTalk de Azure

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Puede usar Hola BizTalk Services Portal tooconfigure e implementar contratos X12 y EDIFACT. En este tutorial, veremos cómo toocreate un acuerdo de EDIFACT para intercambiar facturas entre socios comerciales. Este tutorial se centra en una solución empresarial integral que involucra a dos socios comerciales, Northwind y Contoso, que intercambian mensajes EDIFACT.  

## <a name="sample-based-on-this-tutorial"></a>Ejemplo basado en este tutorial
Este tutorial se centra en un ejemplo, **enviar facturas de EDIFACT mediante servicios de BizTalk**, que es toodownload disponible de hello [MSDN Code Gallery](http://go.microsoft.com/fwlink/?LinkId=401005). Podría utilizar el ejemplo de Hola y seguir este tutorial toounderstand cómo se creó el ejemplo de Hola. O bien, puede usar este tutorial toocreate su propia solución desde cero. Este tutorial está destinado a segundo enfoque de Hola que comprender cómo se compiló esta solución. Además, tanto como sea posible, tutorial Hola es coherente con el ejemplo hello y utiliza Hola mismos nombres para los artefactos (por ejemplo, esquemas, transformaciones) que se usan en el ejemplo de Hola.  

> [!NOTE]
> Dado que esta solución implica enviar un mensaje de un puente EDI de tooan de puente EAI, reutiliza hello [BizTalk Services Bridge encadenamiento ejemplo](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104) ejemplo.  
> 
> 

## <a name="what-does-hello-solution-do"></a>¿Cómo funciona esta solución Hola?
En esta solución, Northwind recibe facturas EDIFACT de Contoso. Estas facturas no están en un formato EDI estándar. Por lo tanto, antes de enviar Hola factura tooNorthwind, debe ser documento de factura (también llamada INVOIC) de EDIFACT tooan transformado. Al recibirla, Northwind debe procesar facturas EDIFACT de Hola y devolver un tooContoso de mensaje (también llamado CONTRL) del control.

![][1]  

tooachieve este escenario empresarial, Contoso usa características de hello proporcionados con los servicios de BizTalk de Microsoft Azure.

* Contoso usa EAI puentes tootransform Hola original factura tooEDIFACT INVOIC.
* puente EAI de Hello, a continuación, envía tooan de mensaje de Hola envío de EDI puente implementado como parte de un acuerdo configurado en hello Portal de servicios de BizTalk.
* puente de envío EDI de Hello procesa hello INVOIC EDIFACT y lo enruta tooNorthwind.
* Después de recibir la factura de hello, Northwind devuelve un toohello de mensaje CONTRL implementado como parte del acuerdo de Hola de puente de recepción EDI.  

> [!NOTE]
> Si lo desea, esta solución también demuestra cómo toouse procesamiento por lotes toosend Hola facturas en lotes, en lugar de enviar cada factura por separado.  
> 
> 

escenario de hello toocomplete, usamos colas de Service Bus toosend factura de Contoso tooNorthwind o recibir la confirmación de Northwind. Estas colas se pueden crear mediante una aplicación de cliente, que está disponible como una descarga y se incluye en el paquete de ejemplo de Hola que está disponible como parte de este tutorial.  

## <a name="prerequisites"></a>Requisitos previos
* Debe tener un espacio de nombres de Bus de servicio. Para instrucciones sobre cómo crear un espacio de nombres, consulte [How To: Create or Modify a Service Bus Service Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx). Supongamos que ya tiene un espacio de nombres del Bus de servicio aprovisionado, llamado **edifactbts**.
* Debe tener una suscripción a Servicios de BizTalk. Para instrucciones, consulte [Creación de Servicios de BizTalk mediante el Portal de Azure clásico](http://go.microsoft.com/fwlink/?LinkID=302280). En este tutorial, supongamos que tiene una suscripción a Servicios de BizTalk, llamada **contosowabs**.
* Registre su suscripción de servicios de BizTalk en hello Portal de servicios de BizTalk. Para obtener instrucciones, consulte [registrar una implementación de servicio de BizTalk en hello Portal de servicios de BizTalk](https://msdn.microsoft.com/library/hh689837.aspx)
* Debe tener instalado Visual Studio.
* Debe tener instalado el SDK de Servicios de BizTalk. Puede descargar Hola SDK de [http://go.microsoft.com/fwlink/?LinkId=235057](http://go.microsoft.com/fwlink/?LinkId=235057)  

## <a name="step-1-create-hello-service-bus-queues"></a>Paso 1: Crear hello las colas de Bus de servicio
Esta solución usa mensajes de tooexchange de colas de Bus de servicio entre socios comerciales. Contoso y Northwind envían mensajes toohello colas desde donde los puentes EAI o EDI Hola consumen. Para esta solución, necesita tres colas de Bus de servicio:

* **northwindreceive** : Northwind recibe facturas Hola de Contoso por esta cola.
* **contosoreceive** : Contoso recibe confirmación de Hola de Northwind por esta cola.
* **suspende** : todos los mensajes suspendidos son toothis enrutado cola. Los mensajes se suspenden si tienen un error durante el procesamiento.

Puede crear estas colas de Bus de servicio mediante una aplicación cliente incluida en el paquete de ejemplo de Hola.  

1. En la ubicación de Hola donde descargó el ejemplo hello, abra **Tutorial enviar facturas utilizando BizTalk Services EDI Bridges.sln**.
2. Presione **F5** toobuild e inicie hello **Tutorial Client** aplicación.
3. En la pantalla de bienvenida, escriba el espacio de nombres de hello ACS de Bus de servicio, nombre del emisor y clave del emisor.
   
   ![][2]  
4. Aparece un mensaje que indica que se crearán las tres colas en el espacio de nombres del Bus de servicio. Haga clic en **Aceptar**.
5. Deje Hola Tutorial Client se está ejecutando. Abra hello, haga clic en **Service Bus** > ***el espacio de nombres de Bus de servicio*** > **colas**y compruebe que se crean las colas de hello tres.  

## <a name="step-2-create-and-deploy-trading-partner-agreement"></a>Paso 2: Creación e implementación del contrato entre socios comerciales
Cree un contrato entre los socios comerciales Contoso y Northwind. Un acuerdo entre socios comerciales define un contrato comerciales entre socios comerciales de hello dos, por ejemplo, qué toouse de esquema de mensaje, que mensajería toouse de protocolo, etcetera. Un acuerdo entre socios comerciales incluye dos puentes EDI, uno toosend mensajes tootrading asociados (llamado hello **puente de envío EDI**) y los mensajes de uno tooreceive de los socios comerciales (llamado hello **depuentederecepciónEDI**).

En el contexto de Hola de esta solución, puente de envío EDI de Hola corresponde toohello envíos del acuerdo de Hola y es usado toosend Hola EDIFACT factura de Contoso tooNorthwind. De igual forma, el puente de recepción EDI Hola corresponde toohello lado de recepción del acuerdo de Hola y es utilizado tooreceive las confirmaciones de Northwind.  

### <a name="create-hello-trading-partners"></a>Crear hello los socios comerciales
toostart, crear socios comerciales para Contoso y Northwind.  

1. Hola Portal de servicios de BizTalk, en hello **socios** , haga clic en **agregar**.
2. En la página nuevo socio comercial de hello, escriba **Contoso** como nombre del asociado y, a continuación, haga clic en **guardar**.
3. Hola repita paso toocreate Hola segundo socio comercial, **Northwind**.  

### <a name="create-hello-agreement"></a>Crear acuerdo Hola
Los contratos entre socios comerciales se crean entre perfiles de negocio de socios comerciales. Esta solución utiliza perfiles de socios comerciales de hello predeterminado que se crean automáticamente cuando se crean los socios de Hola.  

1. Hola Portal de servicios de BizTalk, haga clic en **contratos** > **agregar**.
2. Del nuevo acuerdo de hello **configuración General** página, especifique los valores de hello tal y como se muestra en la imagen de hello siguiente y, a continuación, haga clic en **continuar**.
   
   ![][3]  
   
   Después de hacer clic en **Continuar**, dos pestañas, **Configuración de recepción** y **Configuración de envío** se vuelven disponibles.
3. Crear acuerdo de envío de hello entre Contoso y Northwind. Este acuerdo rige la forma en que Contoso envía Hola EDIFACT factura tooNorthwind.
   
   1. Haga clic en **Configuración de envío**.
   2. Conservar los valores predeterminados de hello en hello **dirección URL de entrada**, **transformar**, y **procesamiento por lotes** pestañas.
   3. En hello **protocolo** ficha, en hello **esquemas** sección, cargue hello **EFACT_D93A_INVOIC.xsd** esquema. Este esquema está disponible con el paquete de ejemplo de Hola.
      
      ![][4]  
   4. En hello **transporte** pestaña, especifique los detalles de Hola para colas de Service Bus Hola. Para hello acuerdo de envío, usamos hello **northwindreceive** toosend Hola EDIFACT factura tooNorthwind de cola y Hola **suspendido** tooroute en cola los mensajes que se producirá un error durante el procesamiento y son suspendido. Crear estas colas en **paso 1: crear colas de Bus de servicio de hello** (en este tema).
      
      ![][5]  
      
      En **configuración de transporte > tipo de transporte** y **configuración de suspensión de mensaje > tipo de transporte**, seleccione Service Bus de Azure y proporcionar los valores de hello tal y como se muestra en la imagen de Hola.
4. Crear Hola recibir acuerdo entre Contoso y Northwind. Este acuerdo rige cómo Contoso recibe confirmación de Hola de Northwind.
   
   1. Haga clic en **Configuración de recepción**.
   2. Conservar los valores predeterminados de hello en hello **transporte** y **transformar** pestañas.
   3. En hello **protocolo** ficha, en hello **esquemas** sección, cargue hello **EFACT_4.1_CONTRL.xsd** esquema. Este esquema está disponible con el paquete de ejemplo de Hola.
   4. En hello **ruta** ficha, cree un tooensure de filtro que solo las confirmaciones de Northwind se tooContoso enrutado. En **configuración de ruta**, haga clic en **agregar** toocreate Hola filtro del enrutamiento.
      
      ![][6]  
      
      1. Proporcione los valores de **nombre de la regla**, **regla de ruta**, y **destino de ruta** tal y como se muestra en la imagen de Hola.
      2. Haga clic en **Guardar**.
   5. En hello **ruta** pestaña nuevo, especifique dónde se enrutan las confirmaciones suspendidas (confirmaciones con error durante el procesamiento). Establecer tooAzure de tipo de transporte de hello Bus de servicio, tipo de destino de ruta demasiado**cola**, tipo de autenticación demasiado**firma de acceso compartido** (SAS), proporcione la cadena de conexión de SAS de Hola para hello Bus de servicio espacio de nombres y, a continuación, escriba el nombre de la cola de hello como **suspendido**.
5. Por último, haga clic en **implementar** acuerdo de hello toodeploy. Puntos de conexión de nota Hola donde hello enviar y recibir los acuerdos se implementan.
   
   * En hello **configuración de envío** ficha **dirección URL de entrada**, tenga en cuenta el punto de conexión de Hola. toosend un mensaje de tooNorthwind de Contoso con hello puente de envío de EDI, debe enviar un punto de conexión de toothis de mensajes.
   * En hello **configuración de recepción** ficha **transporte**, tenga en cuenta el punto de conexión de Hola. puente de recepción de toosend un mensaje de tooContoso Northwind mediante Hola EDI, debe enviar un punto de conexión de toothis de mensajes.  

## <a name="step-3-create-and-deploy-hello-biztalk-services-project"></a>Paso 3: Crear e implementar el proyecto de servicios de BizTalk de Hola
En el paso anterior de hello, implementó Hola EDI de envío y recepción contratos tooprocess facturas y confirmaciones EDIFACT. Estos acuerdos solo pueden procesar mensajes que cumplen el esquema de mensaje toohello estándar EDIFACT. Sin embargo, cada escenario de Hola para esta solución, Contoso envía una tooNorthwind de factura en un esquema interno propio. Por lo tanto, antes de envían mensajes de bienvenida toohello puente de envío de EDI, se debe transformar del esquema de facturas de hello esquema interno toohello estándar EDIFACT. proyecto de BizTalk Services EAI Hola hace eso.

proyecto de servicios de BizTalk de Hello, **InvoiceProcessingBridge**, que transformaciones Hola mensaje también se incluye como parte del ejemplo de Hola que descargó. proyecto de Hello incluye Hola siguientes artefactos:

* **INHOUSEINVOICE. XSD** : esquema de factura interna Hola que se envía tooNorthwind.
* **EFACT_D93A_INVOIC. XSD** : esquema de factura EDIFACT estándar de Hola.
* **EFACT_4.1_CONTRL. XSD** : esquema de confirmación de saludo EDIFACT que Northwind envía tooContoso.
* **INHOUSEINVOICE_to_D93AINVOIC. TRFM** : Hola transformación que asigna el esquema de facturas de hello factura interna esquema toohello estándar EDIFACT.  

### <a name="create-hello-biztalk-services-project"></a>Crear proyecto de servicios de BizTalk de Hola
1. En hello solución de Visual Studio, expanda el proyecto InvoiceProcessingBridge de hello y, a continuación, abra hello **MessageFlowItinerary.bcs** archivo.
2. Haga clic en cualquier lugar en el lienzo de Hola y establezca hello **dirección URL del servicio de BizTalk** en Hola toospecify del cuadro de propiedad, el nombre de la suscripción de servicios de BizTalk. Por ejemplo: `https://contosowabs.biztalk.windows.net`.
   
   ![][7]  
3. En el cuadro de herramientas de hello, arrastre un **puente unidireccional Xml** toohello lienzo. Conjunto hello **nombre de la entidad** y **dirección relativa** propiedades de hello cubrir demasiado**ProcessInvoiceBridge**. Haga doble clic en **ProcessInvoiceBridge** superficie de configuración del puente tooopen Hola.
4. Dentro de hello **tipos de mensaje** cuadro, haga clic en Hola signo más (**+**) esquema de hello toospecify de botón de mensaje de Hola entrantes. Como mensaje entrante de Hola para hello puente EAI es siempre factura interna de hello, establezca esta opción demasiado**INHOUSEINVOICE**.
   
   ![][8]  
5. Haga clic en hello **transformación Xml** forma y en hello cuadro de propiedades, hello **mapas** propiedad, haga clic en el botón de puntos suspensivos hello (**...** ) botón. Hola **selección de mapas** cuadro de diálogo, seleccione hello **INHOUSEINVOICE_to_D93AINVOIC** transformar el archivo y, a continuación, haga clic en **Aceptar**.
   
   ![][9]  
6. Vuelva demasiado**MessageFlowItinerary.bcs**y en el cuadro de herramientas de hello, arrastre un **extremo de servicio externo bidireccional** toohello derecha de hello **ProcessInvoiceBridge**. Establecer su **nombre de la entidad** propiedad demasiado**EDIBridge**.
7. Hola el Explorador de soluciones, expanda hello **MessageFlowItinerary.bcs** y haga doble clic en hello **EDIBridge.config** archivo. Reemplazar el contenido de Hola de hello **EDIBridge.config** con siguiente Hola.
   
   > [!NOTE]
   > ¿Por qué necesito el archivo .config de tooedit Hola? extremo de servicio externo de Hola que agregamos lienzo del diseñador toohello puente representa los puentes de hello EDI que implementamos antes. Los puentes EDI son puentes bidireccionales, con un lado de envío y otro de recepción. Sin embargo, hello puente EAI que agregamos toohello diseñador es un puente unidireccional. Por lo tanto, patrones de intercambio de toohandle Hola mensaje diferente de los dos puentes de hello, utilizamos un comportamiento de puente personalizado e incluimos su configuración en el archivo .config de Hola. Además, comportamiento personalizado de hello también controla el extremo del puente de envío de hello autenticación toohello EDI. Este comportamiento personalizado está disponible como muestra independiente en [puente de servicios de BizTalk encadenamiento ejemplo - EAI tooEDI](http://code.msdn.microsoft.com/BizTalk-Bridge-chaining-2246b104). Esta solución reutiliza el ejemplo hello.  
   > 
   > 
   
   ```
   <?xml version="1.0" encoding="utf-8"?>
   <configuration>
     <system.serviceModel>
       <extensions>
         <behaviorExtensions>
           <add name="BridgeAuthentication" 
                 type="Microsoft.BizTalk.Bridge.Behaviour.BridgeBehaviorElement, Microsoft.BizTalk.Bridge.Behaviour, Version=1.0.0.0, Culture=neutral, PublicKeyToken=ae58f69b69495c05" />
         </behaviorExtensions>
       </extensions>
       <behaviors>
         <endpointBehaviors>
           <behavior name="BridgeAuthenticationConfiguration">
             <!-- Enter hello ACS namespace, issuer name and issuer secret of hello BizTalk Services deployment -->
             <BridgeAuthentication acsnamespace="[YOUR ACS NAMESPACE]" 
                                   issuername="owner" 
                                   issuersecret="[YOUR ACS SECRET]" />
             <webHttp />
           </behavior>
         </endpointBehaviors>
       </behaviors>
       <bindings>
         <webHttpBinding>
           <binding name="BridgeBindingConfiguration">
             <security mode="Transport" />
           </binding>
         </webHttpBinding>
       </bindings>
       <client>
         <clear />
         <!--
           Go BizTalk Portal > Agreement > Send Settings > Inbound URL
           Copy hello Endpoint URL and paste it in hello below address field
         -->
         <endpoint name="TwoWayExternalServiceEndpointReference1" 
                   address="[YOUR EDI BRIDGE SEND URI]" 
                   behaviorConfiguration="BridgeAuthenticationConfiguration" 
                   binding="webHttpBinding" 
                   bindingConfiguration="BridgeBindingConfiguration" 
                   contract="System.ServiceModel.Routing.IRequestReplyRouter" />
       </client>
     </system.serviceModel>
   </configuration>
   
   ```
8. Actualizar detalles de configuración de hello EDIBridge.config archivo tooinclude
   
   * En  *<behaviors>* , proporcionar Hola espacio de nombres ACS y clave asociados a Hola suscripción a los servicios de BizTalk.
   * En  *<client>* , proporcionar extremo Hola donde se implementa Hola acuerdo de envío de EDI.
   
   Guardar los cambios y cierre el archivo de configuración de Hola.
9. En hello cuadro de herramientas, haga clic en hello **conector** combinación hello y **ProcessInvoiceBridge** y **EDIBridge** componentes. Seleccione el conector de hello y, en el cuadro de propiedades, establezca **condición de filtro** demasiado**coincide con todo**. Esto asegura que todos los mensajes procesados por hello puente EAI se enrutan toohello puente EDI.
   
   ![][10]  
10. Guarde los cambios toohello solución.  

### <a name="deploy-hello-project"></a>Implementar proyecto de Hola
1. En el equipo de Hola donde creó el proyecto de servicios de BizTalk de hello, descargue e instale el certificado SSL de hello para la suscripción de servicios de BizTalk. En BizTalk Services, haga clic en **Panel** y luego haga clic en **Descargar certificado SSL**. Haga doble clic en el certificado de Hola y siga hello toocomplete prompt Hola instalación. Asegúrese de instalar el certificado de hello en **entidades de certificación raíz de confianza** almacén de certificados.
2. En Visual Studio Solution Explorer, haga clic en hello **InvoiceProcessingBridge** del proyecto y, a continuación, haga clic en **implementar**.
3. Proporcione los valores de hello tal y como se muestra en la imagen de hello y, a continuación, haga clic en **implementar**. Puede obtener credenciales de hello ACS para los servicios de BizTalk, haga clic en **información de conexión** desde el panel de servicios de BizTalk de Hola.
   
   ![][11]  
   
   En panel de salida de hello, copie el extremo de Hola donde se implementa Hola puente EAI, por ejemplo, `https://contosowabs.biztalk.windows.net/default/ProcessInvoiceBridge`. Necesitará esta dirección URL del punto de conexión más adelante.  

## <a name="step-4-test-hello-solution"></a>Paso 4: Probar la solución de Hola
En este tema, veremos cómo tootest Hola soluciones mediante el uso de hello **Tutorial Client** aplicación proporcionada como parte del ejemplo de Hola.  

1. En Visual Studio, presione F5 toostart hello **Tutorial Client**.
2. pantalla de bienvenida debe tener valores de hello completados del paso de Hola donde creamos hello las colas de Bus de servicio. Haga clic en **Siguiente**.
3. En la siguiente ventana de hello, proporcione las credenciales de ACS para la suscripción a los servicios de BizTalk y Hola extremos donde EAI y EDI (recepción) han implementado los puentes.
   
   Extremo del puente EAI Hola ya copió en el paso anterior de Hola. Para punto de conexión de puente de recepción de EDI en hello Portal de servicios de BizTalk, consulte toohello acuerdo > configuración de recepción > transporte > extremo.
   
   ![][12]  
4. En la ventana siguiente hello, Contoso, haga clic en hello **Enviar factura interna** botón. Hola archivo abrir el cuadro de diálogo, abra el archivo INHOUSEINVOICE.txt de Hola. Examinar contenido Hola de archivo hello y, a continuación, haga clic en **Aceptar** factura de hello toosend.
   
   ![][13]  
5. Hola de unos segundos, recibe la factura en Northwind. Haga clic en hello **Ver mensaje** factura de vínculo toosee Hola recibida por Northwind. Observe cómo factura Hola recibida por Northwind es un esquema EDIFACT estándar al Hola uno enviado por Contoso estaba en formato interno.
   
   ![][14]  
6. Seleccione la factura de hello y, a continuación, haga clic en **Enviar confirmación**. En el cuadro de diálogo de Hola que aparece, observe dicho intercambio Hola A que ID es el mismo en hello recibido hello y factura enviada la confirmación de que se va. Haga clic en Aceptar en hello **Enviar confirmación** cuadro de diálogo.
   
   ![][15]  
7. En unos segundos, la confirmación de Hola se recibe correctamente en Contoso.
   
   ![][16]  

## <a name="step-5-optional-send-edifact-invoice-in-batches"></a>Paso 5 (opcional): Envío de facturas EDIFACT en lotes
Los puentes EDI de Servicios de BizTalk también admiten el procesamiento en lotes de los mensajes salientes. Esta característica es útil para socios receptores que prefieren tooreceive un lote de mensajes (que cumpla ciertos criterios) en lugar de los mensajes individuales.

aspecto más importante de Hello cuando se trabaja con lotes es lanzamiento del lote de hello, también denominado criterios de lanzamiento de Hola Hola. criterios de lanzamiento de Hello pueden basarse en cómo socio receptor Hola desea tooreceive mensajes. Si está habilitado el procesamiento por lotes, Hola puente EDI no envía toohello Hola de mensaje saliente recibir a asociado hasta que hello criterios de lanzamiento se cumple. Por ejemplo, un criterio de procesamiento en lotes basado en el tamaño del mensaje libera un lote una vez que se procesan "n" mensajes en el lote. Un criterio de procesamiento por lotes también se puede basar en la hora, de modo que se envíe un lote a una hora fijada todos los días. En esta solución, intentamos Hola criterios basados en el tamaño del mensaje.

1. Hola Portal de servicios de BizTalk, haga clic en acuerdo de Hola que creó anteriormente. Haga clic en Configuración de envío > Procesamiento por lotes > Agregar lote.
2. Para el nombre del lote, escriba **InvoiceBatch**, proporcione una descripción y luego haga clic en **Siguiente**.
3. Especifique un criterio de procesamiento por lotes, que defina qué mensajes se deben procesar por lotes. En esta solución, procesamos por lote todos los mensajes. Por lo tanto, seleccione la opción usar definiciones avanzadas de Hola y escriba **1 = 1**. Esta es una condición que siempre será verdadera y, por eso, todos los mensajes se procesarán por lotes. Haga clic en **Siguiente**.
   
   ![][17]  
4. Especifique un criterio de liberación por lotes. En el cuadro desplegable hello, seleccione **MessageCountBased**y para **recuento**, especifique **3**. Esto significa que se enviará un lote de tres mensajes tooNorthwind. Haga clic en **Siguiente**.
   
   ![][18]  
5. Revise el resumen de hello y, a continuación, haga clic en **guardar**. Haga clic en **implementar** acuerdo de hello tooredeploy.
6. Volver atrás toohello **Tutorial Client**, haga clic en **Enviar factura interna**y siga Hola indicaciones toosend Hola factura. Observará que no recibe ninguna factura en Northwind porque no se cumple el tamaño de lote de Hola. Repita este paso dos veces más, para que tenga tres mensajes de factura enviados tooNorthwind. Esto cumple los criterios de lanzamiento de lote de 3 mensajes de Hola y ahora debería ver una factura en Northwind.

<!--Image references-->
[1]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-1.PNG  
[2]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-2.PNG  
[3]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-3.PNG
[4]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-4.PNG  
[5]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-5.PNG  
[6]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-6.PNG  
[7]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-7.PNG  
[8]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-8.PNG
[9]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-9.PNG  
[10]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-10.PNG  
[11]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-11.PNG  
[12]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-12.PNG  
[13]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-13.PNG
[14]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-14.PNG  
[15]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-15.PNG  
[16]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-16.PNG  
[17]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-17.PNG  
[18]: ./media/biztalk-process-edifact-invoice/process-edifact-invoices-with-auzure-bts-18.PNG

