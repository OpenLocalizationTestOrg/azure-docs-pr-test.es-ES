---
title: "aaaCreate y administrar conexiones híbridas | Documentos de Microsoft"
description: "Obtenga información acerca de cómo administrar conexión hello toocreate una conexión híbrida e instalar Hola Administrador de conexiones híbridas. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: erikre
editor: 
ms.assetid: aac0546b-3bae-41e0-b874-583491a395ea
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: ccompy
ms.openlocfilehash: 561d8f3dd97318130a05c3bb2874ee8022e7f417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-hybrid-connections"></a>Creación y administración de conexiones híbridas

> [!IMPORTANT]
> Las Conexiones híbridas de BizTalk se han retirado y se han reemplazado por las Conexiones híbridas de App Service. Para obtener más información, incluido cómo toomanage las conexiones de híbrida de BizTalk existente, vea [las conexiones híbridas de servicio de aplicación de Azure](../app-service/app-service-hybrid-connections.md).


## <a name="overview-of-hello-steps"></a>Información general sobre los pasos de Hola
1. Crear una conexión híbrida escribiendo hello **nombre de host** o **FQDN** de recurso local de hello en su red privada.
2. Vincular sus aplicaciones web de Azure o aplicaciones móviles de Azure toohello conexión híbrida.
3. Instalar Administrador de conexiones híbridas de hello en el recurso local y conectar toohello conexión híbrida específica. Hola portal de Azure proporciona una experiencia de un solo clic tooinstall y conectarse.
4. Administre las conexiones híbridas y sus claves de conexión.

En este tema se muestran estos pasos. 

> [!IMPORTANT]
> Es posible tooset una dirección de IP de tooan de extremo de conexión híbrida. Si usa una dirección IP, puede o no se puede conectar con recursos locales de hello, dependiendo de su cliente. Hola conexión híbrida depende del cliente hello realizando una búsqueda de DNS. En la mayoría de los casos, Hola **cliente** es el código de aplicación. Si hello cliente no lleva a cabo una búsqueda de DNS, (no intente tooresolve Hola dirección IP como si fuera un nombre de dominio (x.x.x.x)), a continuación, no se envía el tráfico a través de hello conexión híbrida.
> 
> Por ejemplo (en pseudocódigo), defina **10.4.5.6** como host local:
> 
> **Hola siguiendo el escenario funciona:**  
> `Application code -> GetHostByName("10.4.5.6") -> Resolves too127.0.0.3 -> Connect("127.0.0.3") -> Hybrid Connection -> on-prem host`
> 
> **Hola siguiendo escenario no funciona:**  
> `Application code -> Connect("10.4.5.6") -> ?? -> No route toohost`
> 
> 

## <a name="CreateHybridConnection"></a>Creación de una conexión híbrida
Una conexión híbrida pueden crearse en hello portal de Azure con aplicaciones Web **o** con servicios de BizTalk. 

**Conexiones híbridas con aplicaciones Web toocreate**, consulte [tooan de aplicaciones Web de Azure conectarse recurso local](../app-service-web/web-sites-hybrid-connection-get-started.md). También puede instalar Hola híbrida Connection Manager (gestión) desde la aplicación web, que es el método preferido de hello. 

**las conexiones híbridas en servicios de BizTalk toocreate**:

1. Inicie sesión en toohello [portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. En el panel de navegación izquierdo de hello, seleccione **servicios de BizTalk** y, a continuación, seleccione su BizTalk Service. 
   
    Si no tiene un Servicio de BizTalk existente, puede [Crear un servicio de BizTalk](biztalk-provision-services.md).
3. Seleccione hello **conexiones híbridas** ficha:  
   ![Pestaña Conexiones híbridas][HybridConnectionTab]
4. Seleccione **crear una conexión híbrida** o seleccione hello **agregar** botón de barra de tareas de Hola. Escriba Hola siguiente:
   
   | Propiedad | Descripción |
   | --- | --- |
   | Nombre |Hello conexión híbrida de nombre debe ser único y no puede ser Hola mismo nombre como Hola BizTalk Service. Puede escribir cualquier nombre pero sea concreto con su finalidad. Algunos ejemplos son: <br/><br/>Payroll*SQLServer*<br/>SupplyList*SharepointServer*<br/>Customers*OracleServer* |
   | Nombre de host |Especificar nombre de host completo de hello, sólo nombre de host de hello, u Hola dirección IPv4 del recurso local de Hola. Algunos ejemplos son:<br/><br/>mySQLServer<br/>*mySQLServer*.*Domain*.corp.*yourCompany*.com<br/>*myHTTPSharePointServer*<br/>*myHTTPSharePointServer*.*yourCompany*.com<br/>10.100.10.10<br/><br/>Si usa la dirección IPv4 de hello, tenga en cuenta que el código de cliente o aplicación no puede resolver la dirección IP de Hola. Vea Hola importante nota al principio de Hola de este tema. |
   | Port |Escriba el número de puerto de Hola de recurso local de Hola. Por ejemplo, si utiliza Aplicaciones web, escriba los puertos 80 o 443. Si utiliza SQL Server, escriba el puerto 1433. |
5. Seleccione el programa de instalación de hello marca de verificación toocomplete Hola. 

#### <a name="additional"></a>Información adicional
* Se pueden crear varias conexiones híbridas. Vea hello [servicios de BizTalk: gráfico de ediciones](biztalk-editions-feature-chart.md) para número de Hola de conexiones permitidas. 
* Todas las conexiones híbridas se crean con un par de cadenas de conexión: las claves de aplicación que ENVÍAN y las claves locales que ESCUCHAN. Cada par tiene una clave principal y una secundaria. 

## <a name="LinkWebSite"></a>Vincular su aplicación web o móvil de Azure App Service
Seleccione toolink una aplicación Web o aplicación móvil en tooan de servicio de aplicaciones de Azure existente conexión híbrida, **usar una conexión híbrida existente** en la hoja de conexiones híbridas de Hola. Consulte [Acceso a recursos locales mediante conexiones híbridas en Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).

## <a name="InstallHCM"></a>Instalar Administrador de conexiones híbridas de hello en local
Después de crear una conexión híbrida, instale Hola Administrador de conexiones híbridas en recursos locales de Hola. Este se puede descargar desde Aplicaciones web de Azure o desde el Servicio de BizTalk. Pasos para los servicios de BizTalk: 

1. Inicie sesión en toohello [portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. En el panel de navegación izquierdo de hello, seleccione **servicios de BizTalk** y, a continuación, seleccione su BizTalk Service. 
3. Seleccione hello **conexiones híbridas** ficha:  
   ![Pestaña Conexiones híbridas][HybridConnectionTab]
4. En la barra de tareas de hello, seleccione **el programa de instalación local**:  
   ![Instalación local][HCOnPremSetup]
5. Seleccione **instalar y configurar** toorun o descarga Hola Administrador de conexiones híbridas en hello sistema local. 
6. Seleccione Hola marca de verificación toostart Hola instalación. 

<!--
You can also download hello Hybrid Connection Manager MSI file and copy hello file tooyour on-premises resource. Specific steps:

1. Copy hello on-premises primary Connection String. See [Manage Hybrid Connections](#ManageHybridConnection) in this topic for hello specific steps.
2. Download hello Hybrid Connection Manager MSI file. 
3. On hello on-premises resource, install hello Hybrid Connection Manager from hello MSI file. 
4. Using Windows PowerShell, type: 
> Add-HybridConnection -ConnectionString “*Your On-Premises Connection String that you copied*” 
--> 

#### <a name="additional"></a>Información adicional
* Administrador de conexiones híbridas puede instalarse en hello siguientes sistemas operativos:
  
  * Windows Server 2008 R2 (se requiere .NET Framework 4.5+ y Windows Management Framework 4.0+)
  * Windows Server 2012 (se requiere Windows Management Framework 4.0+)
  * Windows Server 2012 R2
* Después de instalar el Administrador de conexiones híbridas de hello, se produce el siguiente hello: 
  
  * Hola conexión híbrida hospedado en Azure está configurada automáticamente toouse Hola cadena de conexión de aplicación principal. 
  * recurso local de Hello está configurada automáticamente toouse Hola principal cadena de conexión local.
* Hola, Administrador de conexiones híbridas debe utilizar una cadena de conexión local válido para la autorización. Aplicaciones Web de Azure de Hola o aplicaciones móviles debe usar una cadena de conexión de aplicación válida para la autorización.
* Puede escalar las conexiones híbridas al instalar otra instancia del Administrador de conexiones híbridas de hello en otro servidor. Configurar Hola de toouse de agente de escucha Hola local igual de direcciones como agente de escucha de hello primera local. En esta situación, tráfico de hello es distribuido aleatoriamente (round robin) entre los agentes de escucha de hello local activa. 

## <a name="ManageHybridConnection"></a>Administración de conexiones híbridas
toomanage sus conexiones híbridas, puede:

* Usar Hola portal de Azure y seguir tooyour BizTalk Service. 
* Usar [API de REST](http://msdn.microsoft.com/library/azure/dn232347.aspx).

#### <a name="copyregenerate-hello-hybrid-connection-strings"></a>Copie y regenere las cadenas de conexión de hello híbrida
1. Inicie sesión en toohello [portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=213885).
2. En el panel de navegación izquierdo de hello, seleccione **servicios de BizTalk** y, a continuación, seleccione su BizTalk Service. 
3. Seleccione hello **conexiones híbridas** ficha:  
   ![Pestaña Conexiones híbridas][HybridConnectionTab]
4. Seleccione Hola conexión híbrida. En la barra de tareas de hello, seleccione **administrar conexión**:  
   ![Administrar opciones][HCManageConnection]
   
    **Administrar conexión** listas Hola aplicaciones locales y en las cadenas de conexión. Puede copiar hello las cadenas de conexión o volver a generar Hola clave de acceso que se utiliza en la cadena de conexión de Hola. 
   
    **Si selecciona Regenerate**, Hola usa dentro de Hola se cambia la cadena de conexión de la clave de acceso compartida. Hola siguientes:
   
   * Hola portal de Azure clásico, seleccione **claves sincronización** Hola aplicación de Azure.
   * Vuelva a ejecutar hello **el programa de instalación local**. Cuando vuelva a ejecutar Hola la instalación local, Hola recurso local es automáticamente configurado cadena de conexión principal de toouse Hola actualizado.

#### <a name="use-group-policy-toocontrol-hello-on-premises-resources-used-by-a-hybrid-connection"></a>Hola de toocontrol de directiva de grupo utilice recursos usados por una conexión híbrida local
1. Descargar hello [plantillas de administración de administrador de conexiones híbridas](http://www.microsoft.com/download/details.aspx?id=42963).
2. Extraiga los archivos de saludo.
3. En el equipo de Hola que modifica la directiva de grupo, Hola siguientes:  
   
   * Hola de copia. Archivos ADMX toohello *%WINROOT%\PolicyDefinitions* carpeta.
   * Hola de copia. ADML archivos toohello *%WINROOT%\PolicyDefinitions\en-us* carpeta.

Una vez copiado, puede usar Directiva de hello toochange del Editor de directivas de grupo.

## <a name="next"></a>Pasos siguientes
[Conectar aplicaciones Web de Azure tooan recurso local](../app-service-web/web-sites-hybrid-connection-get-started.md)  
[Conectar SQL Server local tooon desde aplicaciones Web de Azure](../app-service-web/web-sites-hybrid-connection-connect-on-premises-sql-server.md)   
[Introducción a las conexiones híbridas](integration-hybrid-connection-overview.md)

## <a name="see-also"></a>Otras referencias
[API REST para administrar BizTalk Services en Microsoft Azure](http://msdn.microsoft.com/library/azure/dn232347.aspx)  
[Servicios de BizTalk: Gráfico de ediciones](biztalk-editions-feature-chart.md)  
[Crear un Servicio de BizTalk mediante el portal de Azure clásico](biztalk-provision-services.md)  
[Servicios de BizTalk: pestañas Panel, Monitor y Escala](biztalk-dashboard-monitor-scale-tabs.md)

[HybridConnectionTab]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionTab.png
[HCOnPremSetup]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionOnPremSetup.png
[HCManageConnection]: ./media/integration-hybrid-connection-create-manage/WABS_HybridConnectionManageConn.png 
