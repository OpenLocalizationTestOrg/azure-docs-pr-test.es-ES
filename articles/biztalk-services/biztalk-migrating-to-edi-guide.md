---
title: "aaaMigrating soluciones EDI de BizTalk Server tooBizTalk guía técnica de servicios | Documentos de Microsoft"
description: Migrar EDI tooMABS; Servicios de BizTalk de Microsoft Azure
services: biztalk-services
documentationcenter: na
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 61c179fa-3f37-495b-8016-dee7474fd3a6
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 34cca3c939a6a7845a860ead6858287000d03ee7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-biztalk-server-edi-solutions-toobiztalk-services-technical-guide"></a>Migrar soluciones EDI de BizTalk Server tooBizTalk Services: Guía técnica

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Autor: Tim Wieman y Nitin Mehrotra

Revisores: Karthik Bharthy

Escrito con: Microsoft Azure BizTalk Services (versión de febrero de 2014).

## <a name="introduction"></a>Introducción
Electronic Data Interchange (EDI) es uno de los medios más frecuentes de hello mediante el cual las empresas intercambian datos electrónicamente, también conocidas como las transacciones de negocio a negocio o B2B. BizTalk Server lleva teniendo compatibilidad con EDI de más de una década, desde la versión inicial BizTalk Sever de Hola. Con los servicios de BizTalk, Microsoft continúa Hola compatibilidad con las soluciones EDI en la plataforma de Microsoft Azure Hola. Las transacciones B2B son principalmente tooan externo organización y, por lo tanto, resulta más fácil tooimplement si se implementa en una plataforma de nube. Microsoft Azure proporciona esta capacidad a través de Servicios de BizTalk.

Aunque algunos clientes consideran en servicios de BizTalk como un plataforma "virgen" para nuevas soluciones EDI, muchos otros tienen soluciones actuales de EDI de BizTalk Server que es posible que deseen toomigrate tooAzure. Dado que BizTalk Services EDI es una arquitectura adecuada hello en función de misma clave entidades EDI de BizTalk Server arquitectura (los socios comerciales, entidades, acuerdos), es posible toomigrate EDI de BizTalk Server artefactos tooBizTalk de servicios.

Este documento describen algunas diferencias Hola de migración tooBizTalk de artefactos de EDI de BizTalk Server Services. En este documento se da por hecho que se dispone de un conocimiento práctico del procesamiento de EDI de BizTalk Server y de los contratos de socios comerciales. Para obtener más información sobre EDI de BizTalk Server, consulte [Administración de socios comerciales mediante BizTalk Server](https://msdn.microsoft.com/library/bb259970.aspx).

## <a name="which-version-of-biztalk-server-edi-artifacts-can-be-migrated-toobiztalk-services"></a>¿La versión de artefactos de EDI de BizTalk Server puede migrarse tooBizTalk Services?
módulo de Hello EDI de BizTalk Server se mejoró significativamente para BizTalk Server 2010, cuando estaba tooinclude familiarizarse socios, perfiles y acuerdos. Usos de los servicios de BizTalk Hola Hola de tooorganize mismo modelo los socios comerciales y Hola divisiones de negocio dentro de los socios comerciales. Como resultado, la migración de EDI de servicios de artefactos de BizTalk Server 2010 y tooBizTalk de versiones posterior, es un proceso mucho más sencillo. artefactos EDI toomigrate asociados con las versiones anteriores tooBizTalk Server 2010, primero debe actualizar tooBizTalk Server 2010 y, a continuación, migrar los artefactos de EDI tooBizTalk servicios.

## <a name="scenariosmessage-flow"></a>Escenarios y flujo de mensajes
Como con BizTalk Server, el procesamiento de EDI en Servicios de BizTalk se basa en una solución de Administración de socios comerciales (TPM). Hola solución TPM tiene Hola clave de los componentes siguientes:

* Los socios comerciales, que representan una organización en una transacción B2B.
* Los perfiles, que representan divisiones dentro de un socio comercial.
* Comerciales acuerdos de socios comerciales (o acuerdos), que representa el contrato de negocio de hello entre dos socios o perfiles.

Hola siguientes ilustración muestra similitudes hello, así como las diferencias entre una solución de EDI de BizTalk Server y una solución EDI de servicios de BizTalk:

![][EDImessageflow]

Hola principales diferencias y similitudes entre un flujo de solución EDI en BizTalk Server y servicios de BizTalk son:

* Al igual que BizTalk Server utiliza un tooreceive de canalización EDIReceive un mensaje EDI y una toosend de canalización EDISend un mensaje EDI, servicios de BizTalk utiliza un tooreceive de puente de recepción EDI y toosend de puente de envío EDI los mensajes EDI. En BizTalk Server, las canalizaciones de hello están asociadas a un acuerdo mediante el uso de envío o puertos de recepción. En servicios de BizTalk, el propio acuerdo Hola denota el envío de Hola o puente de recepción.
* En BizTalk Server, después de procesos de canalización EDIReceive Hola Hola mensaje EDI, mensaje de bienvenida es los tooa base de datos de SQL Server. canalización EdiSend de Hello, a continuación, recoge el mensaje de saludo de base de datos de SQL Server de hello, lo procesa y, a continuación, lo envía toohello socio comercial.
  
    En servicios de BizTalk, una vez Hola EDI reciba el mensaje EDI de puente procesos hello, enruta el proceso externo de hello mensaje tooan. proceso externo de Hello podría ejecutarse en Microsoft Azure o de forma local. proceso externo de Hello debe redirigir toohello de mensaje de Hola puente; de envío de EDI puente de envío de Hello no lo extrae intrínsecamente mensajes de bienvenida. Después de procesar el mensaje de Hola Hola puente de envío EDI enruta a socio comercial de toohello de mensaje de Hola.

Servicios de BizTalk proporciona un tooquickly de la experiencia de configuración fácil de usar crear e implementar un acuerdo B2B entre socios comerciales sin configurar cualquier proceso de Microsoft Azure instancias (roles Web o de trabajo), las bases de datos de SQL de Microsoft Azure o cualquiera Cuentas de almacenamiento de Microsoft Azure. Escenarios más complejos requerirán enlazar flujos de trabajo u otro procesamiento de servicio "alrededor de hello bordes" de un acuerdo de socio comercial, es decir, antes o después del procesamiento de puente EDI de acuerdo de socios comerciales. En detalle, hello siguientes secuencias de eventos se producen durante un mensaje EDI de procesamiento en servicios de BizTalk.

1. Se recibe un mensaje EDI del socio comercial, Fabrikam.  Para recibir mensajes EDI de socios comerciales, los Servicios de BizTalk admiten protocolos de transporte como FTP, SFTP, AS2 y HTTP/S.
2. Hola comerciales de procesamiento de recepción del acuerdo de socios comerciales desensambla formato de tooXML de mensaje de Hola EDI.  Puede enrutar con extremos de Bus de hello desensamblado EDI mensaje (en formato XML) tooService como un extremo de retransmisión de Bus de servicio, el tema de Bus de servicio, cola de Bus de servicio o un puente de servicios de BizTalk.
3. Hello mensajes XML desensamblados pudieron recibirse entonces desde el extremo de Hola para un procesamiento personalizado adicional.  Estos extremos pudieron procesarse por un componente local o un mensaje de Hola de cálculo de Microsoft Azure instancia toofurther proceso en un servicio de flujo de trabajo de Windows (WF) o Windows Communication Foundation (WCF), por ejemplo.
4. Hello "procesamiento de envío" del acuerdo de socio comercial de hello, a continuación, ensambla los mensajes de bienvenida del XML en formato EDI y lo envía a tootrading socio comercial, Contoso.  Para enviar mensajes EDI tootrading asociados, servicios de BizTalk admite Hola mismos protocolos que se utilizaron para recibir los mensajes EDI.

Este documento proporciona instrucciones conceptuales sobre servicios de migración de algunos de hello tooBizTalk de artefactos de EDI de BizTalk Server diferentes.

## <a name="sendreceive-ports-tootrading-partners"></a>Puertos de envío/recepción tooTrading asociados
En BizTalk Server configurar ubicaciones de recepción y mensajes EDI/XML tooreceive de puertos de recepción de los socios comerciales y configurar el asociado tootrading mensajes de puertos de envío toosend EDI/XML. A continuación se asocian estos tooa de puertos mediante la consola de administración de BizTalk Server Hola de acuerdo de socio comercial. En servicios de BizTalk, Hola ubicaciones donde recibe los mensajes de socios comerciales y dónde enviar los asociados de tootrading de mensajes están configurados como parte del acuerdo de socios (como parte de la configuración de transporte) comerciales de Hola Hola Portal de servicios de BizTalk .  Por lo tanto no realmente tiene concepto Hola "puertos de envío" y "ubicaciones de recepción", sí mismo, en servicios de BizTalk. Para obtener más información, consulte [Creación de contratos](https://msdn.microsoft.com/library/windowsazure/hh689908.aspx).

## <a name="pipelines-bridges"></a>Canalizaciones (puentes)
En EDI de BizTalk Server, las canalizaciones son entidades de procesamiento de mensajes que también pueden incluir una lógica personalizada para capacidades de procesamiento específicas, según sea necesario mediante la aplicación hello. Para los servicios de BizTalk, Hola equivalente sería un puente EDI. Sin embargo en servicios de BizTalk, por ahora, Hola puentes EDI están "cerrados".  Es decir, no se puede agregar su propio puente EDI de tooan de actividades personalizadas. Cualquier procesamiento personalizado debe realizarse fuera puente EDI de hello en la aplicación, antes o después de puente Hola configurado como parte del acuerdo de socio comercial de hello entra en el mensaje de bienvenida. Los puentes EAI tienen procesamiento personalizado de la opción hello toodo. Si desea que el procesamiento personalizado, puede usar puentes EAI antes o después de procesan mensajes de bienvenida del puente EDI de Hola. Para obtener más información, consulte [cómo tooInclude de código personalizado en puentes](https://msdn.microsoft.com/library/azure/dn232389.aspx).

Puede insertar un flujo de publicación/suscripción con código personalizado y/o usar colas y temas de mensajería antes Hola acuerdo de socio comercial recibe mensajes de bienvenida, o después de acuerdo de hello procesa mensajes de bienvenida y lo enruta el extremo de Service Bus tooa de Bus de servicio.

Vea **escenarios y flujo de mensajes** en este tema para el modelo de flujo de mensajes de Hola.

## <a name="agreements"></a>Contratos
Si está familiarizado con hello que acuerdos de socio comercial de BizTalk Server 2010 se utiliza para procesamiento de EDI, acuerdos de socios comerciales de servicios de BizTalk parecerán conocidos. La mayoría de contrato de Hola se Hola misma configuración y uso de Hola misma terminología. En algunos casos, Hola configuración del acuerdo es mucho más sencillo toohello comparado misma configuración de BizTalk Server. Servicios de BizTalk de Microsoft Azure es compatible con el transporte X12, EDIFACT y AS2.

Servicios de BizTalk de Azure de Microsoft también proporciona un **migración de datos de TPM** herramienta toomigrate de socios comerciales y acuerdos de socio comercial de BizTalk Server módulo tooBizTalk el Portal de servicios. herramienta de migración de datos de TPM de Hello está disponible como parte de un paquete de herramientas, que puede descargarse desde hello [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057). paquete de Hello también incluye un archivo Léame que se proporciona instrucciones sobre cómo toouse Hola herramienta y la información básica de solución de problemas de Hola herramienta.

## <a name="schemas"></a>Esquemas
Servicios de BizTalk proporciona esquemas EDI que se pueden usar en soluciones de Servicios de BizTalk.  Además, los esquemas EDI de BizTalk Server también sirve con servicios de BizTalk porque es el mismo nodo de raíz de Hola de esquema de hello EDI en BizTalk Server, así como servicios de BizTalk. Por lo tanto, se pueden toodirectly capaz de realizar sus esquemas EDI de BizTalk Server y usarlos en las soluciones EDI de Hola que desarrolle mediante servicios de BizTalk. También puede descargar esquemas Hola de hello [MABS SDK](http://go.microsoft.com/fwlink/p/?LinkId=235057).

## <a name="maps-transforms"></a>Asignaciones (transformaciones)
Las asignaciones en BizTalk Server se llaman transformaciones en Servicios de BizTalk. Migración de mapas de tooBizTalk de BizTalk Server de que Services pudieron ser uno Hola tooachieve de las tareas más compleja (según la complejidad del mapa). herramienta de asignación de Hello utilizada para los servicios de BizTalk es diferente de asignador de BizTalk de Hola. Aunque Hola mapeador mira principalmente Hola igual, formato de mapa de hello subyacente es diferente. Hola functoids (denominado **operaciones de asignación** en servicios de BizTalk) toohello disponibles a los usuarios también son diferentes.  De hecho, no se puede usar directamente una asignación de BizTalk en Servicios de BizTalk. Además, no todos los functoids de hello disponibles en BizTalk Server están disponibles como operaciones de asignación en servicios de BizTalk.

### <a name="new-transform-operations"></a>Nuevas operaciones de transformación
Aunque lista de Hola de operaciones de asignación de transformación disponibles puede ser bastante diferente de hello el asignador de BizTalk Server, BizTalk Services transforma tienen formas nuevas de realizar Hola mismas tareas. Por ejemplo, las transformaciones de Servicios de BizTalk tienen **operaciones de lista** disponibles. Esto no estaba disponible en el asignador de BizTalk Hola.  Hola **operaciones de lista** permiten toocreate y operar con una "lista", donde una lista es un conjunto de elementos (también conocido como "filas") y cada elemento puede tener varios miembros (también conocido como "columnas").  Puede ordenar la lista hello, selección de elementos en función de una condición, etcetera.

Otro ejemplo de la nueva funcionalidad en BizTalk Services transforma son hello **operaciones de bucle**.  Es difícil toocreate anidado bucles en hello el asignador de BizTalk Server.  Por lo tanto, operaciones de asignación de bucle de Hola se agregan para hello transforma de servicios de BizTalk.

Otro ejemplo es hello **If-Then-Else** operación de asignación de expresión.  Realizar una operación de if-then-else era posible en el asignador de BizTalk hello, pero requería varios functoids tooaccomplish una tarea aparentemente simple.

### <a name="migrating-biztalk-server-maps"></a>Migración de asignaciones de BizTalk Server
Servicios de BizTalk de Microsoft Azure proporciona que un toomigrate herramienta BizTalk Server asigna tooBizTalk servicios transformaciones. Hola **BTMMigrationTool** está disponible como parte del programa Hola a **herramientas** paquete suministrado con hello [descarga del SDK de servicios de BizTalk](http://go.microsoft.com/fwlink/p/?LinkId=235057). Para obtener más información acerca de la herramienta de hello, consulte [convertir un tooa de asignación de BizTalk transformación de servicios de BizTalk](https://msdn.microsoft.com/library/windowsazure/hh949812.aspx).

También puede ver un ejemplo realizado por Sandro Pereira, MVP de BizTalk, en forma demasiado[migrar transformaciones de servicios de BizTalk Server mapas tooBizTalk](http://social.technet.microsoft.com/wiki/contents/articles/23220.migrating-biztalk-server-maps-to-windows-azure-biztalk-services-wabs-maps.aspx).

## <a name="orchestrations"></a>Orquestaciones
Si necesita toomigrate tooMicrosoft de procesamiento de orquestación de BizTalk Server Azure, las orquestaciones de hello necesitaría toobe reprogramarse, puesto que Microsoft Azure no admite la ejecución de las orquestaciones de BizTalk Server.  Podría reescribir la funcionalidad de orquestación de hello en un servicio de Windows Workflow Foundation 4.0 (WF4).  Esto sería una reescritura completa porque no hay actualmente ninguna migración de tooWF4 de orquestaciones de BizTalk Server. Estos son algunos recursos para el flujo de trabajo de Windows:

* [*Cómo toointegrate Service de un flujo de trabajo WCF con temas y colas de Bus de servicio* ](https://msdn.microsoft.com/library/azure/hh709041.aspx) , de Paolo Salvatori. 
* [*Generar aplicaciones con Windows Workflow Foundation y Azure* sesión](http://go.microsoft.com/fwlink/p/?LinkId=237314) de la conferencia Build 2011 Hola.
* [*Centro para desarrolladores de Windows Workflow Foundation*](http://go.microsoft.com/fwlink/p/?LinkId=237315) en MSDN.
* [*Documentación de Windows Workflow Foundation 4 (WF4)*](https://msdn.microsoft.com/library/dd489441.aspx) en MSDN.

## <a name="other-considerations"></a>Otras consideraciones
A continuación se facilitan algunas consideraciones que debe realizar durante el uso de Servicios de BizTalk.

### <a name="fallback-agreements"></a>Contratos de reserva
Procesamiento de EDI de BizTalk Server tiene el concepto de Hola de "Acuerdos de retroceso".  Servicios de BizTalk **no** tiene un concepto de contrato de reserva hasta ahora.  Vea los temas de la documentación de BizTalk [Hola rol de los acuerdos en el procesamiento de EDI](http://go.microsoft.com/fwlink/p/?LinkId=237317) y [configuración globales o propiedades del acuerdo de reserva](https://msdn.microsoft.com/library/bb245981.aspx) para obtener información sobre cómo se usan los acuerdos de retroceso en BizTalk Servidor.

### <a name="routing-toomultiple-destinations"></a>Destinos de enrutamiento toomultiple
Puentes de servicios de BizTalk, en su estado actual no admite enrutamiento destinos de toomultiple de mensajes mediante una publicación-modelo de suscripción. En su lugar, puede enrutar los mensajes de un tema de Bus de servicio de servicios de BizTalk puente tooa, que, a continuación, se puede tener el mensaje de bienvenida de varias suscripciones tooreceive en más de un punto de conexión.

## <a name="conclusion"></a>Conclusión
Servicios de BizTalk de Microsoft Azure se actualiza a intervalos regulares tooadd más características y capacidades. Con cada actualización, esperamos toosupporting mayor funcionalidad toofacilitate crear soluciones de end-to-end mediante servicios de BizTalk y otras tecnologías de Azure.

## <a name="see-also"></a>Otras referencias
[Desarrollo de aplicaciones empresariales con Azure](https://msdn.microsoft.com/library/azure/hh674490.aspx)

[EDImessageflow]: ./media/biztalk-migrating-to-edi-guide/IC719455.png
