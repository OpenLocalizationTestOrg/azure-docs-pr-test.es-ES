---
title: "las conexiones de aaaITSM en Conector de administración de servicios de TI de OMS | Documentos de Microsoft"
description: "Conectar los productos o servicios de ITSM con conector de administración de servicios de TI en OMS toocentrally monitor y administrar elementos de trabajo ITSM Hola."
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 8231b7ce-d67f-4237-afbf-465e2e397105
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2017
ms.author: v-jysur
ms.openlocfilehash: 53ef51bf75fb8ed15ea3ce5072d9365c221f9f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-itsm-productsservices-with-it-service-management-connector-preview"></a>Conexión de productos o servicios de ITSM con IT Service Management Connector (versión preliminar)
Este artículo proporciona información acerca de cómo tooconnect su tooIT de productos o servicios ITSM conector de administración de servicio de OMS y centralmente administrar los elementos de trabajo. Para más información sobre IT Service Management Connector, vea [Introducción](log-analytics-itsmc-overview.md).

se admite Hola después de productos y servicios:

- [System Center Service Manager](#connect-system-center-service-manager-to-it-service-management-connector-in-oms)
- [ServiceNow](#connect-servicenow-to-it-service-management-connector-in-oms)
- [Provance](#connect-provance-to-it-service-management-connector-in-oms)
- [Cherwell](#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="connect-system-center-service-manager-tooit-service-management-connector-in-oms"></a>Conectar System Center Service Manager tooIT conector de administración de servicio de OMS

Hello las secciones siguientes proporcionan detalles sobre cómo tooconnect su toohello de producto de System Center Service Manager conector de administración de servicios de TI en OMS.

### <a name="prerequisites"></a>Requisitos previos

Asegúrese de que haya Hola después cumplidos los requisitos previos:

- IT Service Management Connector se ha instalado.
Más información: [Configuración](log-analytics-itsmc-overview.md#configuration).
- Hola aplicación de administrador de servicios Web (aplicación Web) se ha implementado y configurado. [Aquí](#create-and-deploy-service-manager-web-app-service) se puede obtener información sobre la aplicación web.
- Conexión híbrida creada y configurada Obtener más información: [híbrido de hello configurar conexión](#configure-the-hybrid-connection).
- Versiones admitidas de Service Manager: 2012 R2 o 2016.
- Rol de usuario: [operador avanzado](https://technet.microsoft.com/library/ff461054.aspx).

### <a name="connection-procedure"></a>Procedimiento de conexión

Usar hello siguiendo el procedimiento tooconnect su toohello de instancia de System Center Service Manager conector de administración de servicios de TI:

1. Vaya demasiado**OMS** >**configuración** > **orígenes conectados**.
2. Seleccione **Conector ITSM**, haga clic en **Agregar nueva conexión**.

    ![Service Manager ](./media/log-analytics-itsmc/itsmc-service-manager-connection.png)
3. Proporcione información de hello tal y como se describe en hello en la tabla siguiente y haga clic en **guardar** conexión de Hola toocreate:

> [!NOTE]
> Todos estos parámetros son obligatorios.

| **Campo** | **Descripción** |
| --- | --- |
| **Name**   | Escriba un nombre para la instancia de System Center Service Manager de Hola que desea tooconnect con hello conector de administración de servicios de TI.  Usará este nombre más adelante cuando configure los elementos de trabajo en el análisis de registros detallados de la instancia o vista. |
| **Selección de tipo de conexión**   | Seleccione **System Center Service Manager**. |
| **Dirección URL del servidor**   | Escriba la dirección URL de Hola de hello aplicación Web de Service Manager. [Aquí](#create-and-deploy-service-manager-web-app-service) podrá obtener más información sobre la aplicación web de Service Manager.
| **Id. de cliente**   | Escriba el Id. de cliente de hello generado (mediante la secuencia de comandos automática de hello) para autenticar la aplicación Web de hello. Para obtener más información sobre el script de Hola automatizada es [aquí.](log-analytics-itsmc-service-manager-script.md)|
| **Secreto de cliente**   | Secreto de cliente de tipo hello, generado para este identificador.   |
| **Ámbito de sincronización de datos**   | Seleccione los elementos de trabajo de Service Manager de Hola que desea que toosync a través de hello conector de administración de servicios de TI.  Estos elementos de trabajo se importan en Log Analytics. **Opciones:** incidentes, solicitudes de cambio.|
| **Sincronización de datos** | Escriba Hola número de días pasados que desea Hola datos de. **Límite máximo**: 120 días. |
| **Creación de un elemento de configuración de solución ITSM** | Seleccione esta opción si desea que los elementos de configuración de hello toocreate de producto ITSM Hola. Cuando se selecciona, OMS crea elementos de configuración afectado de hello como elementos de configuración (en el caso de CI no existente) en hello admiten sistema ITSM. **Valor predeterminado**: deshabilitado. |

Cuando se ha conectado y sincronizado correctamente:

- Los elementos de trabajo seleccionados de Service Manager se importan en **Log Analytics** de OMS. Puede ver resumen de Hola de estos elementos de trabajo en el icono de conector de administración de servicios de TI de Hola.

- Desde OMS puede crear incidentes de alertas de OMS o de búsqueda de registros en esta instancia de Service Manager.

Más información: [Creación de elementos de trabajo de ITSM para alertas de OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) y [Creación de elementos de trabajo de ITSM desde registros de OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="create-and-deploy-service-manager-web-app-service"></a>Creación e implementación del servicio de aplicaciones web de Service Manager

tooconnect Hola local Service Manager con hello conector de administración del servicio de TI en OMS, Microsoft ha creado una aplicación Web de Service Manager en hello GitHub.

Hola tooset una aplicación Web de ITSM de hello para el administrador del servicio, después de:

- **Aplicación de Web Deploy hello** : implementar la aplicación Web de hello, establecer las propiedades de Hola y autenticarse con Azure AD. Puede implementar aplicaciones web de hello mediante hello [automatizada script](log-analytics-itsmc-service-manager-script.md) que Microsoft ha proporcionado.
- **Configurar la conexión híbrida de hello** - [configurar esta conexión](#configure-the-hybrid-connection), manualmente.

#### <a name="deploy-hello-web-app"></a>Implementar la aplicación web de Hola
Hola uso automatizada [script](log-analytics-itsmc-service-manager-script.md) toodeploy Hola aplicación Web, establecer las propiedades de Hola y autenticarse con Azure AD.

Ejecutar script de Hola proporcionando Hola detalles necesarios siguientes:

- Detalles de la suscripción de Azure
- Definición de un nombre de grupo de recursos
- Ubicación
- Detalles del servidor de Service Manager (nombre del servidor, dominio, nombre de usuario y contraseña)
- Prefijo de nombre de sitio de la aplicación web
- Espacio de nombres de ServiceBus.

Hello secuencia de comandos crea hello Web app con nombre hello especificado (junto con algunos toomake cadenas adicionales que único). Genera hello **dirección URL de la aplicación Web**, **Id. de cliente** y **secreto de cliente**.

Guardar los valores de hello, se utilizan cuando se crea una conexión con el conector de administración de servicios de TI.

**Comprobar la instalación de la aplicación Web Hola**

1. Vaya demasiado**portal de Azure** > **recursos**.
2. Seleccione la aplicación Web de hello, haga clic en **configuración** > **configuración de la aplicación**.
3. Confirmar la información de hello acerca de la instancia de Service Manager de Hola que proporciona en tiempo de presentación de la implementación de la aplicación hello mediante un script de Hola.

### <a name="configure-hello-hybrid-connection"></a>Configurar conexión de hello híbrida

Usar hello después de la conexión híbrida de Hola de tooconfigure de procedimiento que se conecta la instancia de Service Manager Hola con hello conector de administración de servicios de TI en OMS.

1. Buscar en hello aplicación Web de Service Manager, **recursos de Azure**.
2. Haga clic en **Configuración** > **Redes**.
3. En **Conexiones híbridas**, haga clic en **Configure los puntos de conexión de la conexión híbrida**.

    ![Redes de conexión híbrida](./media/log-analytics-itsmc/itsmc-hybrid-connection-networking-and-end-points.png)
4. Hola **conexiones híbridas** hoja, haga clic en **Agregar conexión híbrida**.

    ![Adición de conexión híbrida](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-add.png)

5. Hola **agregar conexiones híbridas** hoja, haga clic en **crear nueva híbrida conexión**.

    ![Conexión híbrida nueva](./media/log-analytics-itsmc/itsmc-create-new-hybrid-connection.png)

6. Escriba Hola siguientes valores:

    - **Nombre del extremo**: especifique un nombre para la conexión híbrida nueva de Hola.
    -  **Host del punto de conexión**: FQDN del servidor de administración de Service Manager Hola.
    - **Puerto del punto de conexión**: escriba 5724.
    - **Espacio de nombres de bus de servicio**: use un espacio de nombres de bus de servicio existente o cree uno.
    - **Ubicación**: Seleccionar ubicación de Hola.
    -  **Nombre**: especifique un bus de servicio de nombre toohello si va a crear.

    ![Valores de la conexión híbrida](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-values.png)
6. Haga clic en **Aceptar** tooclose hello **crear conexión híbrida** hoja y empezar a crear conexión híbrida de Hola.

    Una vez creada la conexión híbrida de hello, se muestra en la hoja de Hola.

7. Una vez creada la conexión híbrida de hello, seleccione la conexión de Hola y haga clic en **selecciona Agregar conexión híbrida**.

    ![Conexión híbrida nueva](./media/log-analytics-itsmc/itsmc-new-hybrid-connection-added.png)

#### <a name="configure-hello-listener-setup"></a>Configurar el programa de instalación del agente de escucha de Hola

Usar hello después de la instalación de agente de escucha de procedimiento tooconfigure Hola de conexión híbrida de Hola.

1. Hola **conexiones híbridas** hoja, haga clic en **descarga Hola Connection Manager** e instalarlo en la máquina de Hola que se ejecuta la instancia de System Center Service Manager.

    Una vez completada, la instalación de hello **Administrador de conexiones híbridas UI** opción está disponible en **iniciar** menú.

2. Haga clic en **Hybrid Connection Manager UI** (IU de administración de conexión híbrida), se le pedirán las credenciales de Azure.

3. Inicio de sesión con sus credenciales de Azure y seleccione la suscripción donde se creó Hola conexión híbrida.

4. Haga clic en **Guardar**.

La conexión híbrida se ha conectado correctamente.

![conexión híbrida correcta](./media/log-analytics-itsmc/itsmc-hybrid-connection-listener-set-up-successful.png)
> [!NOTE]

> Una vez creada la conexión híbrida de hello, comprobar y probar la conexión de hello visitando Hola implementa aplicación Web de Service Manager. Asegúrese de conexión de hello es correcta antes de intentar tooconnect toohello conector de administración de servicios de TI en OMS.

Hello siguiente imagen muestra detalles de Hola de una conexión correcta:

![Prueba de conexión híbrida](./media/log-analytics-itsmc/itsmc-hybrid-connection-test.png)

## <a name="connect-servicenow-tooit-service-management-connector-in-oms"></a>Conectar ServiceNow tooIT conector de administración de servicio de OMS

Hello las secciones siguientes proporcionan detalles sobre cómo tooconnect su toohello de producto de ServiceNow conector de administración de servicios de TI en OMS.

### <a name="prerequisites"></a>Requisitos previos

Asegúrese de que haya Hola después cumplidos los requisitos previos:

- IT Service Management Connector se ha instalado. Más información: [Configuración](log-analytics-itsmc-overview.md#configuration).
- Versiones admitidas de ServiceNow: Fuji, Ginebra, Helsinki.

Debe hacer ServiceNow Admins Hola siguiente en su instancia de ServiceNow:
- Generar Id. de cliente y el secreto del cliente para el producto de ServiceNow Hola. Para obtener información sobre cómo ver el identificador de cliente de toogenerate y el secreto, [el programa de instalación de OAuth](http://wiki.servicenow.com/index.php?title=OAuth_Setup).
- Instalar Hola aplicación de usuario para la integración de OMS de Microsoft (aplicación de ServiceNow). [Más información](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0 ).
- Crear rol de usuario de integración de aplicación de usuario de hello instalado. Obtener información acerca de cómo es el rol de usuario de integración de hello toocreate [aquí](#create-integration-user-role-in-servicenow-app).


### <a name="connection-procedure"></a>**Procedimiento de conexión**

Usar hello siguiendo el procedimiento toocreate una conexión de ServiceNow:

1. Vaya demasiado**OMS** > **configuración** > **orígenes conectados**.
2. Seleccione **Conector ITSM**, haga clic en **Agregar nueva conexión**.

    ![Conexión de ServiceNow](./media/log-analytics-itsmc/itsmc-servicenow-connection.png)

3. Proporcione información de hello tal y como se describe en hello en la tabla siguiente y haga clic en **guardar** conexión de Hola toocreate:

> [!NOTE]
> Todos estos parámetros son obligatorios.

| **Campo** | **Descripción** |
| --- | --- |
| **Name**   | Escriba un nombre para la instancia de ServiceNow Hola que desea tooconnect con hello conector de administración de servicios de TI.  Usará este nombre más adelante en OMS cuando configure los elementos de trabajo en el análisis de registros detallados de ITSM o vista. |
| **Selección de tipo de conexión**   | Seleccione **ServiceNow**. |
| **Nombre de usuario**   | Escriba el nombre de usuario de integración de Hola que creó en hello ServiceNow aplicación toosupport Hola conexión toohello conector de administración de servicios de TI. Más información: [Creación de un rol de usuario de integración de aplicación de ServiceNow](#create-integration-user-role-in-servicenow-app).|
| **Password**   | Escriba la contraseña de hello asociada con este nombre de usuario. **Tenga en cuenta**: nombre de usuario y contraseña se utilizan para generar tokens de autenticación solamente y no se almacenan en cualquier lugar en el servicio OMS de Hola.  |
| **Dirección URL del servidor**   | Escriba la dirección URL de Hola de instancia de ServiceNow de Hola que desea tooconnect tooIT conector de administración de servicio. |
| **Id. de cliente**   | Escriba el Id. de cliente de Hola que desee toouse para la autenticación de OAuth2, que se generó anteriormente.  Para más información acerca de cómo generar el identificador y el secreto del cliente, consulte el [programa de instalación de OAuth](http://wiki.servicenow.com/index.php?title=OAuth_Setup). |
| **Secreto de cliente**   | Secreto de cliente de tipo hello, generado para este identificador.   |
| **Ámbito de sincronización de datos**   | Seleccione elementos de trabajo de hello ServiceNow que desea tooOMS toosync, a través de hello conector de administración de servicios de TI.  valores de Hello seleccionada se importan en el análisis de registros.   **Opciones:** incidentes y solicitudes de cambio.|
| **Sincronización de datos** | Escriba Hola número de días pasados que desea Hola datos de. **Límite máximo**: 120 días. |
| **Creación de un elemento de configuración de solución ITSM** | Seleccione esta opción si desea que los elementos de configuración de hello toocreate de producto ITSM Hola. Cuando se selecciona, OMS crea elementos de configuración afectado de hello como elementos de configuración (en el caso de CI no existente) en hello admiten sistema ITSM. **Valor predeterminado**: deshabilitado. |


Cuando se ha conectado y sincronizado correctamente:

- Los elementos de trabajo seleccionados de la conexión de ServiceNow se importan en Log Analytics de OMS.  Puede ver resumen de Hola de estos elementos de trabajo en el icono de conector de administración de servicios de TI de Hola.
- Puede crear incidentes, alertas y eventos desde alertas de OMS o búsqueda de registros en esta instancia de ServiceNow.  


Más información: [Creación de elementos de trabajo de ITSM para alertas de OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) y [Creación de elementos de trabajo de ITSM desde registros de OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="create-integration-user-role-in-servicenow-app"></a>Creación de un rol de usuario de integración de aplicación de ServiceNow

Hola de usuario siguiendo el procedimiento:

1.  Visite hello [ServiceNow almacén](https://store.servicenow.com/sn_appstore_store.do#!/store/application/ab0265b2dbd53200d36cdc50cf961980/1.0.0) e instalar hello **aplicación de usuario para la integración de OMS de Microsoft y ServiceNow** a la instancia de ServiceNow.
2.  Después de la instalación, visite Hola izquierda de la barra de navegación de la instancia de ServiceNow hello, búsqueda y seleccione integrador de OMS de Microsoft.  
3.  Haga clic en **Installation Checklist** (Lista de comprobación de instalación).

    Hola estado se muestra como **no completó** si es el rol de usuario de hello aún toobe creado.

4.  En el texto hello casillas, demasiado**usuario de integración de crear**, escriba nombre de usuario de hello para el usuario de Hola que se puede conectar toohello conector de administración de servicios de TI en OMS.
5.  Escriba la contraseña de Hola para este usuario y haga clic en **Aceptar**.  

>[!NOTE]

> Usar estas conexiones de ServiceNow credenciales toomake Hola de OMS.

Hola usuario creado recientemente se muestra con roles predeterminados de hello asignados.

Roles predeterminados:
- personalize_choices
- import_transformer
-   x_mioms_microsoft.User
-   itil
-   template_editor
-   view_changer

Una vez que el usuario de Hola se crea correctamente, Hola estado de **Comprobar lista de comprobación de instalación** mueve tooCompleted, Hola detalles del rol de usuario de hello creado para la aplicación hello del anuncio.

> [!NOTE]

> un usuario toocreate tooallow **alertas** y **eventos** en ServiceNow de OMS:

> - Asegúrese de que dispone de módulo de administración de eventos de hello instalado en su instancia de ServiceNow.

> - Agregue Hola después de usuario de integración de toohello de roles:
>      - evt_mgmt_integration
>      - evt_mgmt_operator  


## <a name="connect-provance-tooit-service-management-connector-in-oms"></a>Conectar Provance tooIT conector de administración de servicio de OMS

Hello las secciones siguientes proporcionan detalles sobre cómo tooconnect su toohello de producto Provance conector de administración de servicios de TI en OMS.

### <a name="prerequisites"></a>Requisitos previos

Asegúrese de que haya Hola después cumplidos los requisitos previos:

- IT Service Management Connector se ha instalado. Más información: [Configuración](log-analytics-itsmc-overview.md#configuration).
- La aplicación Provance debe registrarse con Azure AD y estará disponible el identificador de cliente. Para obtener información detallada, vea [la autenticación de active directory de tooconfigure](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md).
- Rol de usuario: administrador.

### <a name="connection-procedure"></a>Procedimiento de conexión

Usar hello siguiendo el procedimiento toocreate una conexión de Provance:

1. Vaya demasiado**OMS** > **configuración** > **orígenes conectados**.
2. Seleccione **Conector ITSM**, haga clic en **Agregar nueva conexión**.  

    ![Conexión a Provance](./media/log-analytics-itsmc/itsmc-provance-connection.png)
3. Proporcione información de hello tal y como se describe en hello en la tabla siguiente y haga clic en **guardar** conexión de hello toocreate.

> [!NOTE]
> Todos estos parámetros son obligatorios.

| **Campo** | **Descripción** |
| --- | --- |
| **Name**   | Escriba un nombre para la instancia de hello Provance que desea tooconnect con hello conector de administración de servicios de TI.  Usará este nombre más adelante en OMS cuando configure los elementos de trabajo en el análisis de registros detallados de ITSM o vista. |
| **Selección de tipo de conexión**   | Seleccione **Provance**. |
| **Nombre de usuario**   | Escriba el nombre de usuario de Hola que se puede conectar toohello conector de administración de servicios de TI.    |
| **Password**   | Escriba la contraseña de hello asociada con este nombre de usuario. **Nota:** nombre de usuario y contraseña se utilizan para generar tokens de autenticación solamente y no se almacenan en cualquier lugar en el servicio OMS de Hola. _|
| **Dirección URL del servidor**   | Escriba la dirección URL de saludo de la instancia de Provance que desea tooconnect tooIT conector de administración de servicio. |
| **Id. de cliente**   | Escriba el Id. de cliente de Hola para autenticar esta conexión, que genera en la instancia de Provance.  Obtener más información sobre el identificador de cliente, consulte [la autenticación de active directory de tooconfigure](../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md). |
| **Ámbito de sincronización de datos**   | Seleccione elementos de trabajo de hello Provance que desea tooOMS toosync, a través de hello conector de administración de servicios de TI.  Estos elementos de trabajo se importan en Log Analytics.   **Opciones:** incidentes, solicitudes de cambio.|
| **Sincronización de datos** | Escriba Hola número de días pasados que desea Hola datos de. **Límite máximo**: 120 días. |
| **Creación de un elemento de configuración de solución ITSM** | Seleccione esta opción si desea que los elementos de configuración de hello toocreate de producto ITSM Hola. Cuando se selecciona, OMS crea elementos de configuración afectado de hello como elementos de configuración (en el caso de CI no existente) en hello admiten sistema ITSM. **Valor predeterminado**: deshabilitado.|

Cuando se ha conectado y sincronizado correctamente:

- Los elementos de trabajo seleccionados de la conexión a Provance se importan en **Log Analytics** de OMS.  Puede ver resumen de Hola de estos elementos de trabajo en el icono de conector de administración de servicios de TI de Hola.
- Puede crear incidentes y eventos desde alertas de OMS o búsqueda de registros en esta instancia de Provance.

Más información: [Creación de elementos de trabajo de ITSM para alertas de OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) y [Creación de elementos de trabajo de ITSM desde registros de OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

## <a name="connect-cherwell-tooit-service-management-connector-in-oms"></a>Conectar Cherwell tooIT conector de administración de servicio de OMS

Hello las secciones siguientes proporcionan detalles sobre cómo tooconnect su toohello de producto de Cherwell conector de administración de servicios de TI en OMS.

### <a name="prerequisites"></a>Requisitos previos

Asegúrese de que haya Hola después cumplidos los requisitos previos:

- IT Service Management Connector se ha instalado. Más información: [Configuración](log-analytics-itsmc-overview.md#configuration).
- Identificador de cliente generado. Más información: [Generación del identificador de cliente para Cherwell](#generate-client-id-for-cherwell).
- Rol de usuario: administrador.

### <a name="connection-procedure"></a>Procedimiento de conexión

Usar hello siguiendo el procedimiento toocreate una conexión de Cherwell:

1. Vaya demasiado**OMS** >  **configuración** > **orígenes conectados**.
2. Seleccione **Conector ITSM**, haga clic en **Agregar nueva conexión**.  

    ![Identificador de usuario de Cherwell](./media/log-analytics-itsmc/itsmc-cherwell-connection.png)

3. Proporcione información de hello tal y como se describe en hello en la tabla siguiente y haga clic en **guardar** conexión de hello toocreate.

> [!NOTE]
> Todos estos parámetros son obligatorios.

| **Campo** | **Descripción** |
| --- | --- |
| **Name**   | Escriba un nombre para la instancia de Cherwell Hola que desea tooconnect toohello conector de administración de servicios de TI.  Usará este nombre más adelante en OMS cuando configure los elementos de trabajo en el análisis de registros detallados de ITSM o vista. |
| **Selección de tipo de conexión**   | Seleccione **Cherwell.** |
| **Nombre de usuario**   | Escriba el nombre de usuario de Cherwell de Hola que se puede conectar toohello conector de administración de servicios de TI. |
| **Password**   | Escriba la contraseña de hello asociada con este nombre de usuario. **Nota:** nombre de usuario y contraseña se utilizan para generar tokens de autenticación solamente y no se almacenan en cualquier lugar en el servicio OMS de Hola.|
| **Dirección URL del servidor**   | Escriba la dirección URL de saludo de la instancia de Cherwell que desea tooconnect tooIT conector de administración de servicio. |
| **Id. de cliente**   | Escriba el Id. de cliente de Hola para autenticar esta conexión, que genera en la instancia de Cherwell.   |
| **Ámbito de sincronización de datos**   | Seleccione los elementos de trabajo de Cherwell de Hola que desea que toosync a través de hello conector de administración de servicios de TI.  Estos elementos de trabajo se importan en Log Analytics.   **Opciones:** incidentes, solicitudes de cambio. |
| **Sincronización de datos** | Escriba Hola número de días pasados que desea Hola datos de. **Límite máximo**: 120 días. |
| **Creación de un elemento de configuración de solución ITSM** | Seleccione esta opción si desea que los elementos de configuración de hello toocreate de producto ITSM Hola. Cuando se selecciona, OMS crea elementos de configuración afectado de hello como elementos de configuración (en el caso de CI no existente) en hello admiten sistema ITSM. **Valor predeterminado**: deshabilitado. |

Cuando se ha conectado y sincronizado correctamente:

- Los elementos de trabajo seleccionados de la conexión de Cherwell se importan en Log Analytics de OMS. Puede ver resumen de Hola de estos elementos de trabajo en el icono de conector de administración de servicios de TI de Hola.
- Puede crear incidentes y los eventos de esta instancia de Cherwell en OMS. Más información: Creación de elementos de trabajo de ITSM para alertas de OMS y Creación de elementos de trabajo de ITSM desde registros de OMS.

Más información: [Creación de elementos de trabajo de ITSM para alertas de OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts) y [Creación de elementos de trabajo de ITSM desde registros de OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs).

### <a name="generate-client-id-for-cherwell"></a>Generación del identificador de cliente para Cherwell

toogenerate Hola identificador/clave de cliente para Cherwell, usar hello siguiendo el procedimiento:

1. Inicie sesión en tooyour Cherwell instancia como administrador.
2. Haga clic en **Security** > **Edit REST API client settings** (Seguridad > Editar configuración de cliente de API de REST).
3. Seleccione **Create new client** > **client secret** (Crear nuevo cliente > Secreto de cliente).

    ![Identificador de usuario de Cherwell](./media/log-analytics-itsmc/itsmc-cherwell-client-id.png)


## <a name="next-steps"></a>Pasos siguientes
 - [Creación de elementos de trabajo de ITSM para alertas de OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-for-oms-alerts)

 - [Creación de elementos de trabajo de ITSM desde registros de OMS](log-analytics-itsmc-overview.md#create-itsm-work-items-from-oms-logs)

- [Ver análisis de registros para la conexión](log-analytics-itsmc-overview.md#using-the-solution)
