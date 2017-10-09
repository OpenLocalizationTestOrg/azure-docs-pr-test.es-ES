---
title: "recuperación de aaaDisaster de cuenta de integración B2B; las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Recuperación ante desastres de Logic Apps B2B"
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: 
ms.assetid: cf44af18-1fe5-41d5-9e06-cc57a968207c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: e86564a3c5a2607d22514936c606e2843cba0416
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-b2b-cross-region-disaster-recovery"></a>Recuperación ante desastres de Logic Apps B2B entre regiones

Las cargas de trabajo de B2B implican transacciones monetarias como pedidos y facturas. Durante un desastre, es fundamental para un hello toomeet de negocios tooquickly recuperación que SLA de nivel de negocio acordados con sus socios. En este artículo se muestra cómo planear toobuild una continuidad del negocio para cargas de trabajo de B2B. 

* Preparación para la recuperación ante desastres 
* Conmutar por región toosecondary durante un evento de desastre 
* Revertir tooprimary región después de un evento de desastre

## <a name="disaster-recovery-readiness"></a>Preparación para la recuperación ante desastres  

1. Identificar una región secundaria y crear un [cuenta integración](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) en la región secundaria Hola.

2. Agregar socios comerciales, esquemas y acuerdos para flujos de mensajes de Hola necesario donde hello estado de ejecución necesita toobe replican toosecondary región integración cuenta.

   > [!TIP]
   > Asegúrese de que hay coherencia en la convención de nomenclatura del artefacto de cuenta de hello integración entre las regiones. 

3. Hola toopull estado de la ejecución de la región principal de hello, cree una aplicación de lógica en la región secundaria Hola. 

   Esta aplicación lógica debe tener un *desencadenador* y una *acción*. 
   desencadenador Hola debe conectarse la cuenta de integración de región tooprimary y acción de hello debe conectar con cuenta de integración de región de toosecondary. 
   En función de intervalo de tiempo de hello, desencadenador de Hola sondea la tabla de estado de la región principal ejecute hello y extrae los nuevos registros de hello, si existe. acción de Hello las actualiza toosecondary cuenta de integración de región. 
   Esto ayuda a estado incremental en tiempo de ejecución de tooget desde una región principal toosecondary otra.

4. Continuidad del negocio en aplicaciones de lógica de la cuenta de integración es diseñado toosupport basada en protocolos B2B - X12, AS2 y EDIFACT. toofind los pasos detallados, seleccione Hola enlaces correspondientes.

5. Hola recomendación es toodeploy todos los recursos de la región principal en una región secundaria demasiado. 

   Recursos de la región principal incluyen base de datos de SQL Azure o base de datos de Azure Cosmos, Service Bus de Azure y concentradores de eventos de Azure utiliza para la mensajería, administración de API de Azure y la característica de Azure Logic Apps hello en el servicio de aplicación de Azure.   

6. Establecer una conexión de una región secundaria de tooa de región principal. Hola toopull estado de la ejecución de una región principal, cree una aplicación de lógica en una región secundaria. 

   aplicación de la lógica de Hello debe tener un desencadenador y una acción. 
   desencadenador de Hello debe conectar tooa cuenta de integración de región principal. 
   acción de Hello debe conectar tooa cuenta de integración de región secundaria. 
   En función de intervalo de tiempo de hello, desencadenador de Hola sondea la tabla de estado de la región principal ejecute hello y extrae los nuevos registros de hello, si existe. 
   acción de Hello las actualiza tooa cuenta de integración de región secundaria. 
   Este proceso ayuda a estado incremental en tiempo de ejecución de tooget desde región secundaria de hello región principal toohello.

Continuidad del negocio en una cuenta de integración de aplicaciones lógicas proporciona compatibilidad basada en protocolos de B2B hello X12, AS2 y EDIFACT. Para ver los pasos detallados sobre cómo usar X12 y AS2, consulte [X12](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#x12) y [AS2](../logic-apps/logic-apps-enterprise-integration-b2b-business-continuity.md#as2) en este artículo.

## <a name="fail-over-tooa-secondary-region-during-a-disaster-event"></a>Conmutar por región secundaria tooa durante un evento de desastre

Durante un evento de desastre, cuando no está disponible para la continuidad del negocio, región secundaria de dirigir el tráfico toohello región principal Hola. Una región secundaria le ayuda a un toorecover empresariales rápidamente funciones hello toomeet RPO/RTO acordado con sus asociados. También minimiza toofail esfuerzos a través de una región tooanother otra. 

Hay una latencia esperada mientras se copiaban números de control de una región secundaria de tooa de región principal. tooavoid Enviar control generado duplicados números toopartners durante un evento de desastre, recomendación de hello es tooincrement números de control de hello en los contratos de la región secundaria de hello mediante [cmdlets de PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).

## <a name="fall-back-tooa-primary-region-post-disaster-event"></a>Revertir el evento de desastre posterior a la región principal tooa

región principal de toofall tooa atrás cuando esté disponible, siga estos pasos:

1. Dejar de aceptar mensajes de socios en la región secundaria Hola.  

2. Incrementar los números de control de hello generado para todos los contratos de la región principal de hello mediante el uso de [cmdlets de PowerShell](https://blogs.msdn.microsoft.com/david_burgs_blog/2017/03/09/fresh-of-the-press-new-azure-powershell-cmdlets-for-upcoming-x12-connector-disaster-recovery).  

3. Dirigir el tráfico de la región principal de hello región secundaria toohello.

4. Comprobar esa aplicación de lógica de hello creada en la región secundaria de Hola para extraer el estado de la ejecución de la región principal de Hola está habilitada.

## <a name="x12"></a>X12 

La continuidad empresarial de los documentos EDI X12 se basa en los números de control:

> [!TIP]
> También puede usar hello [X12 rápido iniciar plantilla](https://azure.microsoft.com/documentation/templates/201-logic-app-x12-disaster-recovery-replication/) toocreate las aplicaciones lógicas. Creación de cuentas de integración principal y secundaria es plantillas de hello toouse de requisitos previos. Hello plantilla ayuda toocreate dos aplicaciones de lógica, uno para números de control recibidos y otro para los números de control generado. Acciones y desencadenadores respectivos se crean en las aplicaciones lógicas de hello, conexión de cuenta de hello desencadenador toohello integración principal y cuenta de hello acción toohello integración secundaria.

**Requisitos previos**

recuperación ante desastres de tooenable para los mensajes entrantes, seleccione Configuración de comprobación de duplicados de hello en configuración de recepción del acuerdo de hello X12.

![Seleccionar comprobar la configuración duplicada](./media/logic-apps-enterprise-integration-b2b-business-continuity/dupcheck.png)  

1. Cree una [aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md) en una región secundaria.    

2. Busque en **X12** y seleccione **X12: Cuando se modifica un número de control**.   

   ![Búsqueda de X12](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn1.png)

   desencadenador de Hello solicita tooestablish una cuenta de conexión de integración tooan. 
   Hola desencadenador debe estar conectado tooa cuenta de integración de región principal.

3. Escriba un nombre de conexión, seleccione la *cuenta de integración de la región principal* de hello lista y elija **crear**.   

   ![Nombre de la cuenta de integración de la región primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn2.png)

4. Hola **número sincronización de fecha y hora toostart control** configuración es opcional. Hola **frecuencia** puede establecerse demasiado**día**, **hora**, **minuto**, o **segundo** con un intervalo.   

   ![DateTime y frecuencia](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

5. Seleccione **Nuevo paso** > **Agregar una acción**.

   ![Nuevo paso y Agregar una acción](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

6. Busque en **X12** y seleccione **X12: Permite agregar o actualizar números de control**.   

   ![Agregar o actualizar los números de control](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn5.png)

7. tooconnect una cuenta de integración de acción tooa región secundaria, seleccione **cambiar conexión** > **agregar nueva conexión** para obtener una lista de cuentas de integración disponible en Hola. Escriba un nombre de conexión, seleccione la *cuenta de integración de la región secundaria* de hello lista y elija **crear**. 

   ![Nombre de la cuenta de integración de la región secundaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

8. Intercambiar entradas de tooraw haciendo clic en el icono de hello en la esquina superior derecha.

   ![Intercambiar entradas tooraw](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12rawinputs.png)

9. Seleccione cuerpo en el selector de contenido dinámico de Hola y guarde la aplicación lógica de hello.

   ![Campos de contenido dinámico](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn7.png)

   Según el intervalo de tiempo de hello, desencadenador de hello sondea la tabla de números de control de región principal recibe hello y extrae los registros nuevos de Hola. 
   acción de Hello actualiza los registros de hello en la cuenta de integración de hello región secundaria. 
   Si no hay actualizaciones, estado de desencadenador de hello aparece como **omitidos**.   

   ![Tabla de número de control](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

En función de intervalo de tiempo de hello, estado incremental en tiempo de ejecución de hello replica desde una región secundaria de tooa de región principal. Durante un evento de desastre, cuando Hola principal región no está disponibles y directa tráfico toohello secundaria para continuidad del negocio. 

## <a name="edifact"></a>EDIFACT 

La continuidad empresarial de los documentos EDI EDIFACT se basa en los números de control.

**Requisitos previos**

recuperación ante desastres de tooenable para los mensajes entrantes, seleccione Configuración de comprobación de duplicados de hello en configuración de recepción de su acuerdo EDIFACT.

![Seleccionar comprobar la configuración duplicada](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactdupcheck.png)  

1. Cree una [aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md) en una región secundaria.    

2. Busque en **EDIFACT** y seleccione **EDIFACT: Cuando se modifica un número de control**.

   ![Búsqueda de EDIFACT](./media/logic-apps-enterprise-integration-b2b-business-continuity/edifactcn1.png)

   desencadenador de Hello solicita tooestablish una cuenta de conexión de integración tooan. 
   Hola desencadenador debe estar conectado tooa cuenta de integración de región principal. 

3. Escriba un nombre de conexión, seleccione la *cuenta de integración de la región principal* de hello lista y elija **crear**.    

   ![Nombre de la cuenta de integración de la región primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN2.png)

4. Hola **número sincronización de fecha y hora toostart control** configuración es opcional. Hola **frecuencia** puede establecerse demasiado**día**, **hora**, **minuto**, o **segundo** con un intervalo.    

   ![DateTime y frecuencia](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn3.png)

6. Seleccione **Nuevo paso** > **Agregar una acción**.    

   ![Nuevo paso y Agregar una acción](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn4.png)

7. Busque en **EDIFACT** y seleccione **EDIFACT: Permite agregar o actualizar números de control**.   

   ![Agregar o actualizar los números de control](./media/logic-apps-enterprise-integration-b2b-business-continuity/EdifactChooseAction.png)

8. tooconnect una cuenta de integración de acción tooa región secundaria, seleccione **cambiar conexión** > **agregar nueva conexión** para obtener una lista de cuentas de integración disponible en Hola. Escriba un nombre de conexión, seleccione la *cuenta de integración de la región secundaria* de hello lista y elija **crear**.

   ![Nombre de la cuenta de integración de la región secundaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12cn6.png)

9. Intercambiar entradas de tooraw haciendo clic en el icono de hello en la esquina superior derecha.

   ![Intercambiar entradas tooraw](./media/logic-apps-enterprise-integration-b2b-business-continuity/Edifactrawinputs.png)

10. Seleccione cuerpo en el selector de contenido dinámico de Hola y guarde la aplicación lógica de hello.   

   ![Campos de contenido dinámico](./media/logic-apps-enterprise-integration-b2b-business-continuity/X12CN7.png)

   Según el intervalo de tiempo de hello, desencadenador de hello sondea la tabla de números de control de región principal recibe hello y extrae los registros nuevos de Hola.
   acción de Hello actualiza cuenta de integración de hello registros toohello región secundaria. 
   Si no hay actualizaciones, estado de desencadenador de hello aparece como **omitidos**.

   ![Tabla de número de control](./media/logic-apps-enterprise-integration-b2b-business-continuity/x12recevicedcn8.png)

En función de intervalo de tiempo de hello, estado incremental en tiempo de ejecución de hello replica desde una región secundaria de tooa de región principal. Durante un evento de desastre, cuando Hola principal región no está disponibles y directa tráfico toohello secundaria para continuidad del negocio. 

## <a name="as2"></a>AS2 

Continuidad del negocio en documentos que utilizan el protocolo de AS2 Hola se basa en el Id. de mensaje de Hola y el valor MIC Hola.

> [!TIP]
> También puede usar hello [plantilla de inicio rápido de AS2](https://github.com/Azure/azure-quickstart-templates/pull/3302) toocreate las aplicaciones lógicas. Creación de cuentas de integración principal y secundaria es plantillas de hello toouse de requisitos previos. plantilla de Hello le ayuda a crear una aplicación de lógica que tiene un desencadenador y una acción. aplicación de la lógica de Hello crea una conexión de una cuenta de desencadenador tooa integración principal y una cuenta de acción tooa integración secundaria.

1. Crear un [aplicación lógica](../logic-apps/logic-apps-create-a-logic-app.md) en la región secundaria Hola.  

2. Busque en **AS2** y seleccione **AS2: Cuando se crea un valor MIC**.   

   ![Búsqueda de AS2](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid1.png)

   Un desencadenador le tooestablish una cuenta de conexión de integración tooan. 
   Hola desencadenador debe estar conectado tooa cuenta de integración de región principal. 
   
3. Escriba un nombre de conexión, seleccione la *cuenta de integración de la región principal* de hello lista y elija **crear**.

   ![Nombre de la cuenta de integración de la región primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid2.png)

4. Hola **sincronización de valor de fecha y hora toostart MIC** configuración es opcional. Hola **frecuencia** puede establecerse demasiado**día**, **hora**, **minuto**, o **segundo** con un intervalo.   

   ![DateTime y frecuencia](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid3.png)

5. Seleccione **Nuevo paso** > **Agregar una acción**.  

   ![Nuevo paso y Agregar una acción](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid4.png)

6. Busque en **AS2** y seleccione **AS2: Agregar o actualizar contenidos MIC**.  

   ![Incorporación o actualización de MIC](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid5.png)

7. Seleccione una cuenta de acción de integración secundaria tooa tooconnect **cambiar conexión** > **agregar nueva conexión** para obtener una lista de cuentas de integración disponible en Hola. Escriba un nombre de conexión, seleccione la *cuenta de integración de la región secundaria* de hello lista y elija **crear**.

   ![Nombre de la cuenta de integración de la región secundaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid6.png)

8. Intercambiar entradas de tooraw haciendo clic en el icono de hello en la esquina superior derecha.

   ![Intercambiar entradas tooraw](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2rawinputs.png)

9. Seleccione cuerpo en el selector de contenido dinámico de Hola y guarde la aplicación lógica de hello.   

   ![Contenido dinámico](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid7.png)

   En función de intervalo de tiempo de hello, desencadenador de hello sondea la tabla de la región principal de Hola y extrae los registros nuevos de Hola. acción de Hello las actualiza toohello cuenta de integración de región secundaria. 
   Si no hay actualizaciones, estado de desencadenador de hello aparece como **omitidos**.  

   ![Tabla de la región primaria](./media/logic-apps-enterprise-integration-b2b-business-continuity/as2messageid8.png)

En función de intervalo de tiempo de hello, estado incremental en tiempo de ejecución de hello replica de región secundaria de hello región principal toohello. Durante un evento de desastre, cuando Hola principal región no está disponibles y directa tráfico toohello secundaria para continuidad del negocio. 

## <a name="next-steps"></a>Pasos siguientes

[Supervisión de mensajes B2B](logic-apps-monitor-b2b-message.md)

