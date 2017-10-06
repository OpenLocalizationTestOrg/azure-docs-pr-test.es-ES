---
title: "aaaAccess orígenes de datos de forma local para las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Configurar la puerta de enlace de datos de hello local por lo que puede tener acceso a orígenes de datos en instalaciones de aplicaciones lógicas"
keywords: "obtener acceso a datos, local, transferencia de datos, cifrado, orígenes de datos"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a>Orígenes de datos de Access de forma local desde las aplicaciones lógicas con puerta de enlace de datos de hello local

orígenes de datos tooaccess local desde las aplicaciones lógicas, configure una puerta de enlace de datos local que pueden usar las aplicaciones lógicas con conectores compatibles. puerta de enlace de Hello actúa como un puente que permite el cifrado entre los orígenes de datos de forma local y las aplicaciones lógicas y transferencia de datos rápidamente. puerta de enlace de Hello transmite datos desde orígenes locales en los canales cifrados a través de hello Azure Service Bus. Todo el tráfico se origina como proteger el tráfico saliente desde el agente de puerta de enlace de Hola. Obtenga más información sobre [cómo funciona la puerta de enlace de datos de hello](logic-apps-gateway-install.md#gateway-cloud-service). 

puerta de enlace de Hello es compatible con orígenes de datos de las conexiones toothese local:

*   BizTalk Server 2016
*   DB2  
*   Sistema de archivos
*   Informix
*   MQ
*   MySQL
*   Base de datos de Oracle
*   PostgreSQL
*   Servidor de aplicaciones de SAP 
*   Servidor de mensajes de SAP
*   SharePoint
*   SQL Server
*   Teradata

Estos pasos muestra cómo tooset seguridad Hola local toowork de puerta de enlace de datos con las aplicaciones lógicas. Para obtener más información sobre las conexiones admitidas, consulte [Conectores para Azure Logic Apps](../connectors/apis-list.md). 

Para obtener información acerca de cómo toouse Hola puerta de enlace con otros servicios, vea estos artículos:

*   [Puerta de enlace de datos local de Microsoft Power BI](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Puerta de enlace de datos local de Azure Analysis Services](../analysis-services/analysis-services-gateway.md)
*   [Puerta de enlace de datos local de Microsoft Flow](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Administración de una puerta de enlace de datos local en Microsoft PowerApps](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a>Requisitos

* Debe tener ya [instalada la puerta de enlace de datos de hello en un equipo local](logic-apps-gateway-install.md).

* Cuando inicias sesión en toohello portal de Azure, tendrá toouse Hola mismo trabajo o académica de cuenta que se usó demasiado[instalar la puerta de enlace de datos de hello local](logic-apps-gateway-install.md#requirements). Su cuenta de inicio de sesión también debe tener una suscripción de Azure toouse cuando se crea un recurso de puerta de enlace en hello portal de Azure para la instalación de puerta de enlace.

* No puede haber ningún recurso de puerta de enlace de Azure que ya haya solicitado la instalación de la puerta de enlace. Puede asociar el recurso de una puerta de enlace de Azure de puerta de enlace instalación tooonly. Notificación se produce cuando se crea el recurso de puerta de enlace de Hola para que no está disponible para otros recursos de la instalación de Hola.

## <a name="set-up-hello-data-gateway-connection"></a>Configurar conexión de puerta de enlace de datos de Hola

### <a name="1-install-hello-on-premises-data-gateway"></a>1. Hola de instalación de puerta de enlace de datos local

Si no lo ha hecho ya, siga hello [puerta de enlace de pasos tooinstall Hola local datos](logic-apps-gateway-install.md). Antes de continuar con hello otros pasos, asegúrese de que instaló la puerta de enlace de datos de hello en un equipo local.

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a>2. Crear un recurso de Azure para puerta de enlace de datos de hello local

Después de instalar la puerta de enlace de hello en un equipo local, debe crear la puerta de enlace de datos como un recurso de Azure. En este paso también se asocia el recurso de puerta de enlace a su suscripción de Azure.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com "portal de Azure"). Asegúrese de que toouse Hola mismo trabajo de Azure o dirección de correo electrónico educativa usa puerta de enlace de tooinstall Hola.

2. En el menú de la izquierda de hello en Azure, elija **New** > **integración empresarial** > **puerta de enlace de datos local** tal y como se muestra aquí:

   ![Busque "Puerta de enlace de datos local".](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. En hello **crear puerta de enlace de conexión** hoja, proporcione estos detalles toocreate el recurso de puerta de enlace de datos:

    * **Nombre**: escriba un nombre para el recurso de puerta de enlace. 

    * **Suscripción**: seleccione Hola tooassociate de suscripción de Azure con su recurso de puerta de enlace. 
    Esta suscripción debe ser Hola misma suscripción que la aplicación lógica.
   
      suscripción de Hello predeterminada se basa en hello cuenta de Azure que usan toosign en.

    * **Grupo de recursos**: cree un grupo de recursos o seleccione uno existente para implementar el recurso de puerta de enlace. 
    Los grupos de recursos le ayudan a administrar recursos de Azure relacionados como una colección.

    * **Ubicación**: Azure restringe este toohello ubicación misma región que se seleccionó para su servicio de nube de puerta de enlace de Hola durante [instalación de puerta de enlace](logic-apps-gateway-install.md). 

      > [!NOTE]
      > Asegúrese de que ubicación de recursos de puerta de enlace de hello coincide con ubicación del servicio de nube de puerta de enlace de Hola. En caso contrario, la instalación de puerta de enlace no puede aparecer en lista de puertas de enlace de Hola instalado para tooselect en el paso siguiente de saludo.
      > 
      > Puede usar regiones diferentes para el recurso de puerta de enlace y la aplicación lógica.

    * **Nombre de la instalación**: si la instalación de puerta de enlace no está seleccionada, seleccionar la puerta de enlace de Hola que instaló anteriormente. 

    tooyour de recursos de puerta de enlace tooadd hello Azure panel, elija **toodashboard Pin**. 
    Cuando termine, seleccione **Crear**.

    Por ejemplo:

    ![Proporcionar detalles toocreate la puerta de enlace de datos local](./media/logic-apps-gateway-connection/createblade.png)

    toofind o vista de la puerta de enlace de datos en cualquier momento, en hello Azure izquierdo menú principal, vaya demasiado **más servicios** > **integración empresarial** > **datos locales Las puertas de enlace**.

    ![Vaya demasiado "Más servicios", "Integración de la empresa", "Puertas de enlace de datos locales"](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a>3. Conectar la puerta de enlace de datos de lógica aplicación toohello local

Ahora que ha creado el recurso de puerta de enlace de datos y su suscripción de Azure asociada a ese recurso, crear una conexión entre la lógica hello y aplicación datos puerta de enlace.

> [!NOTE]
> La ubicación de la conexión de puerta de enlace debe existir en hello misma región que la aplicación lógica, pero puede usar una puerta de enlace de datos que existe en una región distinta.

1. Hola portal de Azure, cree o abra la aplicación lógica en el Diseñador de la lógica de aplicación.

2. Agregue un conector que admita conexiones locales, como SQL Server.

3. Siguiendo el orden de Hola se muestra, seleccione **conectar a través de puerta de enlace de datos local**, proporcione un nombre único de conexión y Hola información necesaria y seleccionar recurso de puerta de enlace de datos de Hola que desea toouse. Cuando termine, seleccione **Crear**.

   > [!TIP]
   > Un nombre de conexión único le ayuda a identificar fácilmente la conexión más adelante, especialmente al crear varias conexiones. Si procede, incluir dominio completo de hello para el nombre de usuario. 

   ![Creación de conexiones entre la aplicación lógica y la puerta de enlace de datos](./media/logic-apps-gateway-connection/blankconnection.png)

Enhorabuena, su conexión de puerta de enlace ya está lista para su toouse de aplicación lógica.

## <a name="edit-your-gateway-connection-settings"></a>Editar la configuración de conexión de la puerta de enlace

Después de crear una conexión de puerta de enlace de la aplicación lógica, podría interesarle toolater configuración de Hola de actualización para esa conexión concreta.

1. conexión de puerta de enlace de Hola toofind:

   * En la hoja de la aplicación de lógica de hello, en **herramientas de desarrollo**, seleccione **API conexiones**. 
   
     Hola **API conexiones** panel muestra todas las conexiones de API asociadas a la aplicación lógica, incluidas las conexiones de puerta de enlace.

     ![Vaya tooyour lógica aplicación, seleccione "API de conexiones"](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * O bien, en hello Azure izquierdo menú principal, vaya demasiado **más servicios** > **Web y servicios móviles** > **API conexiones** para todas las conexiones de API, incluidas las conexiones de puerta de enlace, que están asociados a su suscripción de Azure. 

   * O bien, en hello Azure izquierdo menú principal, vaya demasiado**todos los recursos** para todas las conexiones de API, incluidas las conexiones de puerta de enlace, que están asociadas a su suscripción de Azure.

2. Seleccionar conexión de puerta de enlace de Hola que desee tooview o editar y elija **conexión editar API**.

   > [!TIP]
   > Si las actualizaciones no surten efecto, intente [detener y reiniciar el servicio de puerta de enlace de Windows hello](./logic-apps-gateway-install.md#restart-gateway).

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a>Cambiar o eliminar el recurso de puerta de enlace de datos local

toocreate un recurso de la puerta de enlace diferente, asociar la puerta de enlace a un recurso diferente o quitar recursos de la puerta de enlace de hello, puede eliminar los recursos de la puerta de enlace de hello sin afectar a la instalación de puerta de enlace de Hola. 

1. En hello Azure izquierdo menú principal, vaya demasiado**todos los recursos**. 
2. Busque y seleccione el recurso de puerta de enlace de datos.
3. Elija **puerta de enlace de datos local**y en la barra de herramientas de recursos de hello, elija **eliminar**.

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a>Pasos siguientes

* [Protección de las aplicaciones lógicas](./logic-apps-securing-a-logic-app.md)
* [Ejemplos y escenarios habituales de las aplicaciones lógicas](./logic-apps-examples-and-scenarios.md)
