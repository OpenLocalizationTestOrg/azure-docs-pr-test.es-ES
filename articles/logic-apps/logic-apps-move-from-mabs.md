---
title: aaaMove a las aplicaciones de servicios de BizTalk tooAzure Logic Apps | Documentos de Microsoft
description: Mover o migrar Azure BizTalk Services MABS tooLogic aplicaciones
services: logic-apps
documentationcenter: 
author: jonfancey
manager: anneta
editor: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: ladocs; jonfan; mandia
ms.openlocfilehash: b3b065b90a37002f72305b0fc866c24231fb5f9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="move-from-biztalk-services-toologic-apps"></a>Mover de tooLogic aplicaciones de servicios de BizTalk

Microsoft Azure BizTalk Services (MABS) está en retirada. Utilice este tema toomove su tooAzure de soluciones de integración de MABS Logic Apps. 

## <a name="overview"></a>Información general

BizTalk Services consta de dos subservicios:

1.  Conexiones híbridas de Microsoft BizTalk Services
2.  Integración basada en puente de EAI y EDI

Si busca las conexiones híbridas de toomove, a continuación, [las conexiones híbridas de servicio de aplicación de Azure](../app-service/app-service-hybrid-connections.md) describe los cambios de Hola y las características de este servicio. Conexiones híbridas de Azure reemplaza a Conexiones híbridas de BizTalk Services. Las conexiones híbridas de Azure está disponible con el servicio de aplicación de Azure y se ofrece en hello portal de Azure. Las conexiones híbridas de Azure también proporciona un nuevo toomanage de administrador de conexiones híbridas conexiones híbridas de servicios de BizTalk existentes y nuevas conexiones híbridas en que crear Hola portal. Conexiones híbridas de Azure App Service está disponible con carácter general (GA).

Para la integración basada en el puente EAI y EDI, Logic Apps es sustituto de Hola. Lógica de aplicaciones proporciona que todos Hola mismas capacidades que los servicios de BizTalk y mucho más. Lógica de aplicaciones proporciona a escala de nube consumo características basadas en orquestaciones y flujo de trabajo que le permiten tooquickly y crear fácilmente soluciones de integración complejas mediante un explorador o con herramientas de Visual Studio.

Hello en la tabla siguiente proporciona una asignación de funciones de servicios de BizTalk tooLogic aplicaciones.

| Servicios de BizTalk   | Aplicaciones lógicas            | Propósito                  |
| ------------------ | --------------------- | ---------------------------- |
| Conector          | Conector             | Envío y recepción de datos   |
| Puente             | Aplicación lógica             | Procesador de canalización           |
| Fase de validación     | Acción de validación XML      | Validación de un documento XML con respecto a un esquema             |
| Fase de enriquecimiento       | Tokens de datos      | Promoción de propiedades en mensajes o para enrutar decisiones             |
| Fase de transformación    | Acción de transformación      | Convertir los mensajes XML de un formato tooanother             |
| Fase de descodificación       | Acción de descodificación de archivo plano      | Convertir de tooXML de archivo sin formato             |
| Fase de codificación       |  Acción de codificación de archivo plano      | Convertir archivo de tooflat XML             |
| Inspector de mensajes       |  Azure Functions o API Apps      | Ejecución de código personalizado en las integraciones             |
| Acción de enrutamiento      |  Condición o modificador      | Ruta tooone de mensajes de Hola especificado conectores             |

Existe una gran cantidad de tipos de artefactos distintos en BizTalk Services.

## <a name="connectors"></a>Conectores
Conectores en servicios de BizTalk permiten toosend de puentes y reciban datos, incluidos los puentes bidireccionales que habilita las interacciones de solicitud/respuesta basada en HTTP. En la lógica de aplicaciones, Hola se utiliza la misma terminología. Conectores de aplicaciones lógicas servir Hola misma finalidad y también incluyen más de 140 que se pueden conectar tooa amplia gama de tecnologías y servicios, tanto de manera local mediante Hola local Data Gateway (reemplazando Hola servicio de adaptador de BizTalk utilizan los servicios de BizTalk) y a los servicios de SaaS y PaaS, como OneDrive, Office 365, Dynamics CRM y mucho más.

Orígenes de servicios de BizTalk son tooFTP limitado, SFTP y cola de Bus de servicio o suscripción de tema.

![](media/logic-apps-move-from-mabs/sources.png)

Cada puente tiene un extremo HTTP de forma predeterminada, que está configurado con hello dirección en tiempo de ejecución y las propiedades de la dirección relativa de Hola de puente Hola. Hola tooachieve igual a las aplicaciones lógicas, use hello [solicitud y respuesta](../connectors/connectors-native-reqres.md) acciones.

## <a name="xml-processing-and-bridges"></a>Puentes y procesamiento de XML
Un puente en servicios de BizTalk es la canalización de procesamiento de tooa análoga. Un puente puede tomar los datos recibidos de un conector y realizar algunas operaciones con datos de hello y, a continuación, enviarla tooanother sistema. Lógica de aplicaciones Hola mismo admitiendo Hola misma interacción basada en la canalización de patrones como servicios de BizTalk y también proporciona una serie de otros patrones de integración. Hola [puente de solicitud y respuesta XML](https://msdn.microsoft.com/library/azure/hh689781.aspx) en servicios de BizTalk se conoce como una canalización VETER formada por fases por las que pueden:

* (V) Validación
* (E) Enriquecimiento
* (T) Transformación
* (E) Enriquecimiento
* (R) EnRutamiento

Tal como se muestra en hello después de la imagen, procesamiento de Hola se divide entre la solicitud y respuesta y permite controlar la solicitud de Hola y Hola rutas de acceso de respuesta por separado (por ejemplo, con diferentes asignaciones para cada uno):

![](media/logic-apps-move-from-mabs/xml-request-reply.png)

Además, un puente unidireccional XML agrega las fases de descodificación y codificación al principio de Hola y al final del procesamiento y puente de paso a través de hello contiene una sola fase de enriquecimiento.

### <a name="message-processing-and-decodingencoding"></a>Procesamiento y descodificación/codificación de mensajes
En servicios de BizTalk, recibirá mensajes XML de diferentes tipos y determinar esquema coincidente de hello para el mensaje de Hola recibido. Esto se realiza en hello **tipos de mensaje** fase del programa Hola a la canalización de procesamiento de recepción. A continuación, Hola fase de descodificación usa toodecode de tipo de mensaje de Hola detectado mediante el esquema de hello proporcionado. Si el esquema de hello es flatfile, convierte Hola entrantes flatfile tooXML. 

Logic Apps proporciona funcionalidades similares. Se recibe un flatfile en una gran variedad de distintos protocolos mediante desencadenadores de conector diferentes hello (sistema de archivos, FTP, HTTP etc.) y usar hello [descodificar de archivo sin formato](../logic-apps/logic-apps-enterprise-integration-flatfile.md) tooXML de datos entrantes de acción tooconvert Hola. Puede mover los esquemas de archivo sin formato existente directamente toologic aplicaciones sin necesidad de realizar cualquier cambia y, a continuación, cargue esquemas tooyour cuenta de integración.

### <a name="validation"></a>Validación
Una vez hello los datos entrantes tooXML convertido (o si XML tenía el formato de mensaje de Hola recibido), la validación ejecuta toodetermine si tooyour un esquema XSD ajusta el mensaje de bienvenida. toodo en lógica de aplicaciones, use hello [validación XML](../logic-apps/logic-apps-enterprise-integration-xml-validation.md) acción. Una vez más, puede usar Hola mismos esquemas de servicios de BizTalk sin realizar ningún cambio.

### <a name="transform-messages"></a>Transformación de mensajes
En servicios de BizTalk, fase de transformación de hello convierte una tooanother de formato de mensajes basado en XML. Esto se realiza aplicando un mapa, mediante el asignador de TRFM-based Hola. En la lógica de aplicaciones, el proceso de hello es similar. Hola acción transformación ejecuta un mapa de la cuenta de integración. Hola principal diferencia es que están en formato XSLT mapas en aplicaciones de la lógica. XSLT incluye Hola capacidad tooreuse existente ya tiene, incluidos los mapas creados para el servidor BizTalk Server que contienen functoids XSLT. 

### <a name="routing-rules"></a>Reglas de enrutamiento
Servicios de BizTalk se toma una decisión de enrutamiento en qué punto de conexión/conector toosend mensajes/datos de entrada. Hola capacidad tooselect uno de una serie de puntos de conexión configuradas previamente es posible mediante la opción de filtro de enrutamiento de hello:

![](media/logic-apps-move-from-mabs/route-filter.png)

Logic Apps ofrece funcionalidades lógicas más sofisticadas con [Condition](../logic-apps/logic-apps-use-logic-app-features.md) (Condición) y [Switch](../logic-apps/logic-apps-switch-case.md) (Modificador), lo que permite un flujo de control y enrutamiento avanzados. Convertir los filtros de enrutamiento en BizTalk Services se logra mejor con una **condición** *si* solo hay dos opciones. Si hay más de dos, use un **modificador**.

### <a name="enrich"></a>Enriquecimiento
Hola fase de enriquecimiento en servicios de BizTalk procesamiento aporta el contexto de mensaje toohello de propiedades asociada con los datos de hello recibidos. Por ejemplo, promover una toouse de propiedad para el enrutamiento (descrito a continuación) de una búsqueda de la base de datos o extrayendo un valor utilizando una expresión XPath. Lógica de aplicaciones proporciona acceso tooall datos contextuales salidas desde delante acciones, lo que tooreplicate sencillo Hola mismo comportamiento. Por ejemplo, si se usa hello `Get Row` acción de conexión de SQL, devuelve datos de una base de datos de SQL Server y usar los datos de hello en una acción de decisión para el enrutamiento. Del mismo modo, las propiedades en el Bus de servicio entrantes mensajes en cola un desencadenador son direccionable, así como XPath usando la expresión de lenguaje de definición de flujo de trabajo de hello xpath.

### <a name="use-custom-code"></a>Uso de código personalizado
Servicios de BizTalk proporciona capacidad de hello demasiado[ejecutar código personalizado](https://msdn.microsoft.com/library/azure/dn232389.aspx) cargado en sus propios ensamblados. Esto se implementa mediante hello [IMessageInspector](https://msdn.microsoft.com/library/microsoft.biztalk.services.imessageinspector.aspx) interfaz. Cada fase de puente Hola incluye dos propiedades (On Enter Inspector y On Exit Inspector) proporcionado por el tipo de .net Hola creaste que implementa esta interfaz. Código personalizado permite tooperform más complejas de procesamiento de datos de hello, así como reutilizar el código existente en ensamblados que realizan la lógica empresarial común. 

Lógica de aplicaciones proporciona dos métodos principales para código personalizado tooexecute: funciones de Azure y aplicaciones de API. Es posible crear y llamar a Azure Functions desde aplicaciones lógicas. Consulte [Adición y ejecución de código personalizado para aplicaciones lógicas con Azure Functions](../logic-apps/logic-apps-azure-functions.md). Usar aplicaciones de API, parte del servicio de aplicaciones de Azure, toocreate sus propios desencadenadores y acciones. Obtenga más información sobre [crear una personalizada toouse de API a las aplicaciones lógicas](../logic-apps/logic-apps-create-api-app.md). 

Si tienes código personalizado en assmeblies que se llame desde servicios de BizTalk, se puede mover este código tooAzure funciones o crear API personalizadas con aplicaciones de API; Dependiendo de lo que se está implementando. Por ejemplo, si tiene código que ajusta otro servicio que lógica de aplicaciones no tiene un conector, a continuación, crear una API App y usar la aplicación de API se proporciona dentro de la aplicación lógica de acciones de Hola. Si tiene funciones auxiliares o bibliotecas, funciones de Azure es probable Hola mejor ajuste.

### <a name="edi-processing-and-trading-partner-management"></a>Administración de entidades y procesamiento de EDI
BizTalk Services incluye procesamiento de EDI y B2B con compatibilidad con AS2 (Applicability Statement 2), X12 y EDIFACT. Logic Apps también lo hace. En servicios de BizTalk, el crear puentes EDI y crear y administrar socios comerciales y acuerdos en el portal de administración y seguimiento de dedicado Hola.

En la lógica de aplicaciones, esta funcionalidad se incluye con hello [paquete de integración empresarial](../logic-apps/logic-apps-enterprise-integration-overview.md). Se compone de las acciones de cuenta de integración y B2B de hello para el procesamiento EDI y B2B. Hola [cuenta integración](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) es toocreate usado y administrar [los socios comerciales](../logic-apps/logic-apps-enterprise-integration-partners.md) y [contratos](../logic-apps/logic-apps-enterprise-integration-agreements.md). Una vez que cree una cuenta de integración, puede asociar uno o más cuentas de toohello de aplicaciones de la lógica. Una vez asociado, puede usar Hola B2B acciones tooaccess comerciales información de socio en la aplicación lógica. se proporciona Hola siguientes acciones:

* Codificación AS2
* Descodificación AS2
* Codificación X12
* Descodificación X12
* Codificación EDIFACT
* Descodificación EDIFACT

A diferencia de los servicios de BizTalk, estas acciones se desacoplan de protocolos de transporte de Hola. Por lo tanto, al crear las aplicaciones lógicas, tiene más flexibilidad en los conectores que utilice toosend y recibe datos. Por ejemplo, es posible tooreceive X12 archivos como datos adjuntos de correo electrónico y, a continuación, procesar estos archivos en una aplicación de lógica. 

## <a name="manage-and-monitor"></a>Administración y supervisión
Así como la administración de socios comerciales, Hola dedicado portal de servicios de BizTalk siempre toomonitor capacidades de seguimiento y solucionar problemas. 

Lógica de aplicaciones proporciona más enriquecida de seguimiento y supervisión capacidades en hello [portal de Azure](../logic-apps/logic-apps-monitor-your-logic-apps.md)y con hello [solución B2B Operations Management Suite](../logic-apps/logic-apps-monitor-b2b-message.md), incluida una aplicación móvil para mantener un ojo de cosas Cuando esté en hello mover.

## <a name="high-availability"></a>Alta disponibilidad
tooachieve alta disponibilidad (HA) en servicios de BizTalk, use más de una instancia de un saludo de tooshare región determinada carga de procesamiento. Con las aplicaciones lógicas, la alta disponibilidad en la región está integrada y no supone ningún costo adicional. En el caso de la recuperación ante desastres fuera de la región para el procesamiento B2B en BizTalk Services, se requiere un proceso de copia de seguridad y restauración. En la lógica de aplicaciones, un entre regiones activo/pasivo [capacidad de recuperación ante desastres](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md) se proporciona; lo que permite la sincronización de Hola de B2B datos a través de las cuentas de integración en regiones diferentes para la continuidad empresarial.

## <a name="next"></a>Pasos siguientes
* [¿Qué es Logic Apps?](logic-apps-what-are-logic-apps.md)
* [Cree la primera aplicación lógica](logic-apps-create-a-logic-app.md) o empiece a trabajar rápidamente mediante una [plantilla precompilada](logic-apps-use-logic-app-templates.md)  
* [Vista de Hola a todos los conectores disponibles](../connectors/apis-list.md) puede utilizar en una aplicación de lógica
