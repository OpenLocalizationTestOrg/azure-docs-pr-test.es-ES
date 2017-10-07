---
title: "aaaConfigure orígenes de implementación para los servicios de aplicación en la pila de Azure | Documentos de Microsoft"
description: "En este artículo se explica cómo un administrador de servicios puede configurar los orígenes de implementación (Git, GitHub, BitBucket, Dropbox y OneDrive) para App Services en Azure Stack."
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: anwestg
ms.openlocfilehash: 2eaf0a7f4b6e52d64a302000c1dd3c3eb5d6a6ca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-deployment-sources"></a>Configuración de orígenes de implementación

App Service en Azure Stack admite la implementación a petición de varios proveedores de control de código fuente.  Esta característica habilita la aplicación a los desarrolladores toobe capaz de toodeploy directa desde sus repositorios de control de código fuente.  En orden para los inquilinos toobe capaz de tooconfigure tooconnect de servicio de aplicaciones tootheir repositorios, los administradores primero deben configurar la integración de hello entre el servicio de aplicaciones en la pila de Azure y Hola proveedor de Control de código fuente.  Proveedores de Control de código fuente de Hello admite, además toolocal Git, son:

* GitHub
* BitBucket
* OneDrive
* Dropbox

## <a name="view-deployment-sources-in-app-service-administration"></a>Visualización de orígenes de implementación en la hoja de administración de App Services

1. Inicie sesión en el Portal de administración de Azure pila (https://adminportal.local.azurestack.external) toohello como administrador de servicios de Hola.
2. Examinar demasiado**proveedores de recursos** y seleccione hello **App Admin de proveedor de recursos de servicio**.  ![Opción de administración de proveedores de recursos de App Service][1]
3. Haga clic en la **Source control configuration** (Configuración de control de código fuente).  Aquí verá lista Hola de todos los orígenes de implementación configurado.
    ![Configuración de control de código fuente de hoja de administración de proveedores de recursos de App Service][2]

## <a name="configure-github"></a>Configuración de GitHub

> [!NOTE]
> Necesita un toocomplete de cuenta de GitHub esta tarea.  Es recomendable toouse una cuenta para su organización en lugar de una cuenta personal.

1. Inicie sesión en tooGitHub, toohttps://www.github.com/settings/developers y haga clic en **registrar una nueva aplicación** ![GitHub - registrar una nueva aplicación][3]
2. Escriba el **nombre de la aplicación**, por ejemplo, App Service en Azure Stack.
3. Escriba hello **dirección URL de la página principal de**.  **Hola dirección URL de la página de inicio debe ser la dirección de Portal de la pila de Azure de hello** https://portal.local.azurestack.external por ejemplo:
4. Escriba la **descripción de la aplicación**.
5. Escriba hello **dirección URL de devolución de llamada de autorización**.  En una implementación predeterminada de la pila de Azure, dirección Url de hello está en hello formulario https://portal.local.azurestack.external/tokenauthorize, si está trabajando en un sustituto de otro dominio a su dominio para azurestack.local ![GitHub - registrar una nueva aplicación con valores rellena][4]
6. Haga clic en **Register application** (Registrar aplicación).  Se le mostrará ahora con un saludo de la lista de página **Id. de cliente** y **secreto de cliente** para la aplicación hello.
    ![GitHub - Registro de aplicación completado][5]
7.  En un explorador nueva pestaña o ventana, inicie sesión en el Portal de administración de pila de Azure (https://adminportal.local.azurestack.external) como administrador de servicios de hello toohello. 
8.  Examinar demasiado**proveedores de recursos** y seleccione hello **App Admin de proveedor de recursos de servicio**. 
9. Haga clic en la **Source control configuration** (Configuración de control de código fuente).
10. Copie y pegue hello **Id. de cliente** y **secreto del cliente** en cuadros de entrada correspondientes de Hola para GitHub.
11. Haga clic en **Guardar**.
12. Si no desea tooconfigure cualquier otro origen de implementación, continúe demasiado[reparación de Roles de administración de programación](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).


## <a name="configure-bitbucket"></a>Configuración de BitBucket

> [!NOTE]
> Necesita un toocomplete de cuenta BitBucket esta tarea.  Es recomendable toouse una cuenta para su organización en lugar de una cuenta personal.

1. Inicie sesión en tooBitBucket y examinar demasiado**integraciones** en su cuenta ![BitBucket panel - integraciones][7]
2. Haga clic en **OAuth** en Administración de acceso y en **Add consumer** (Agregar consumidor). ![Opción de agregar consumidor de OAuth en BitBucket][8]
3. Escriba un **nombre** de consumidores de hello, por ejemplo el servicio de aplicaciones en la pila de Azure
4. Escriba un **descripción** para la aplicación hello
5. Escriba hello **dirección URL de devolución de llamada**.  En una implementación de la pila de Azure de forma predeterminada, Hola dirección Url de devolución de llamada está en hello formulario https://portal.local.azurestack.external/TokenAuthorize, si está trabajando en un dominio diferente, sustituya su dominio para azurestack.local.  dirección Url de Hello debe seguir mayúsculas y minúsculas de hello como se muestra aquí para toosucceed de integración de BitBucket.
6. Escriba hello **URL** -esta dirección Url debe ser Hola URL del Portal de Azure pila, por ejemplo https://portal.local.azurestack.external
7. Seleccione hello **permisos** requiere **repositorios**: **lectura** **Webhooks**: **de lectura y escritura**
8. Haga clic en **Guardar**.  Ahora verá esta nueva aplicación, junto con hello **clave** y **secreto** en **OAuth consumidores**.
    ![Lista de aplicaciones de BitBucket][9]
9.  En un explorador nueva pestaña o ventana, inicie sesión en el Portal de administración de pila de Azure (https://adminportal.local.azurestack.external) como administrador de servicios de hello toohello. 
10.  Examinar demasiado**proveedores de recursos** y seleccione hello **App Admin de proveedor de recursos de servicio**. 
11. Haga clic en la **Source control configuration** (Configuración de control de código fuente).
12. Copie y pegue hello **clave** en hello **Id. de cliente** cuadro de entrada y **secreto** en hello **secreto de cliente** cuadro de entrada para BitBucket.
13. Haga clic en **Guardar**.
14. Si no desea tooconfigure cualquier otro origen de implementación, continúe demasiado[reparación de Roles de administración de programación](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).

## <a name="configure-onedrive"></a>Configuración de OneDrive

> [!NOTE]
> En estos momentos, no se admiten las cuentas de OneDrive para la Empresa.  Debe toohave una tooa Account Microsoft vinculada OneDrive cuenta toocomplete esta tarea.  Es recomendable toouse una cuenta para su organización en lugar de una cuenta personal.

1. Examinar toohttps://apps.dev.microsoft.com/?referrer=https%3A%2F%2Fdev.onedrive.com%2Fapp-registration.htm e inicie sesión con su Account de Microsoft.
2. Haga clic en **Agregar una aplicación** en **Mis aplicaciones**
![Aplicaciones de OneDrive][10]
3. Escriba un **nombre** para hello nuevo registro de aplicación, escriba **servicio de aplicaciones en Azure pila**y haga clic en **crear aplicación**
4. pantalla de bienvenida siguiente enumera las propiedades de hello de la nueva aplicación. Hola de registro **Id. de aplicación**
![propiedades de la aplicación de OneDrive][11]
5. En **aplicación secretos** haga clic en **generar nueva contraseña** registro hello y **nueva contraseña generada** -se trata de la clave secreta de la aplicación.
> [!NOTE]
> Anote toomake seguro de una nueva contraseña de hello ya que no se puede recuperar una vez que haga clic en Aceptar en esta fase.
6. En **Plataformas**, haga clic en **Agregar plataforma** y seleccione **Web**.
7. Escriba hello **URI de redireccionamiento**.  En una implementación predeterminada de la pila de Azure, hello URI de redireccionamiento es en hello formulario https://portal.local.azurestack.external/tokenauthorize, si está trabajando en un sustituto de otro dominio a su dominio para azurestack.local ![OneDrive aplicación: Agregar plataforma Web][12]
8. Conjunto hello **Microsoft Graph permisos** - **permisos delegados**
    - **Files.ReadWrite.AppFolder**
    - **User.Read**  
      ![Aplicación de OneDrive - Permisos de Graph][13]
10. Haga clic en **Guardar**.
11.  En un explorador nueva pestaña o ventana, inicie sesión en el Portal de administración de pila de Azure (https://adminportal.local.azurestack.external) como administrador de servicios de hello toohello. 
12.  Examinar demasiado**proveedores de recursos** y seleccione hello **App Admin de proveedor de recursos de servicio**. 
13. Haga clic en la **Source control configuration** (Configuración de control de código fuente).
14. Copie y pegue hello **Id. de aplicación** en hello **Id. de cliente** cuadro de entrada y **contraseña** en hello **secreto de cliente** cuadro de entrada de OneDrive.
15. Haga clic en **Guardar**.
16. Si no desea tooconfigure cualquier otro origen de implementación, continúe demasiado[reparación de Roles de administración de programación](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).

## <a name="configure-dropbox"></a>Configuración de Dropbox

> [!NOTE]
> Deberá toohave un toocomplete de cuenta de DropBox esta tarea.  Es recomendable toouse una cuenta para su organización en lugar de una cuenta personal.

1. Examinar toohttps://www.dropbox.com/developers/apps e inicie sesión con su cuenta de DropBox
2. Haga clic en **Create app (Creación aplicación)** 
![Dropbox applications (Aplicaciones de Dropbox)][14]
3. Seleccione la **API de Dropbox**.
4. Establecer el nivel de acceso de hello demasiado**carpeta de la aplicación**
5. Escriba el **nombre** de la aplicación.
![Registro de aplicaciones de Dropbox][15]
6. Haga clic en **Create app** (Crear aplicación).  Se le mostrará ahora con una página enumerar la configuración de Hola para incluir de aplicación Hola **clave de aplicación** y **secreto de la aplicación**.
7. Comprobar hello **nombre de la carpeta de aplicación** se establece demasiado**servicio de aplicaciones en la pila de Azure**
8. Conjunto hello **URI de redirección de OAuth 2** y haga clic en **agregar**.  En una implementación predeterminada de la pila de Azure, hello URI de redireccionamiento es en hello formulario https://portal.local.azurestack.external/tokenauthorize, si está trabajando en un sustituto de otro dominio a su dominio para azurestack.local ![aplicación de Dropbox configuración][16]
9.  En un explorador nueva pestaña o ventana, inicie sesión en el Portal de administración de pila de Azure (https://adminportal.local.azurestack.external) como administrador de servicios de hello toohello. 
10.  Examinar demasiado**proveedores de recursos** y seleccione hello **App Admin de proveedor de recursos de servicio**. 
11. Haga clic en la **Source control configuration** (Configuración de control de código fuente).
12. Copie y pegue hello **clave de aplicación** en hello **Id. de cliente** cuadro de entrada y **secreto de la aplicación** en hello **secreto de cliente** cuadro de entrada de DropBox.
13. Haga clic en **Guardar**.
14. Si no desea tooconfigure cualquier otro origen de implementación, continúe demasiado[reparación de Roles de administración de programación](azure-stack-app-service-configure-deployment-sources.md#schedule-repair-of-management-roles).

## <a name="schedule-repair-of-management-roles"></a>Programación de la reparación de roles de administración
Para la configuración de hello actualizado en la configuración de Hola de hello aplica distintos toobe de orígenes de implementación, funciones de administración de Hola deben toobe reparar.  Este proceso garantiza que se aplican correctamente los valores de configuración de Hola y Hola configurar orígenes de implementación se realizan tootenants disponible.

1. En un explorador nueva pestaña o ventana, inicie sesión en el Portal de administración de pila de Azure (https://adminportal.local.azurestack.external) como administrador de servicios de hello toohello.
2. Examinar demasiado**proveedores de recursos** y seleccione hello **App Admin de proveedor de recursos de servicio**.
3. Haga clic en la **Source control configuration** (Configuración de control de código fuente).
4. Copie y pegue hello **Id. de cliente** y **secreto del cliente** en cuadros de entrada correspondientes de Hola para GitHub.
5. Haga clic en **Guardar**
6. Haga clic en **Roles**.
7. Haga clic en **Management Server** (Servidor de administración).
8. Haga clic en **Repair All** (Reparar todo) y seleccione **Yes** (Sí).  Esta operación programa una reparación en la integración de todos los servidores de administración toocomplete Hola.  las operaciones de reparación Hola son el tiempo de inactividad toominimize administrado.
    ![Administración de proveedores de recursos de App Service - Roles - Opción para programar una reparación en los servidores de administración][6]

<!--Image references-->
[1]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin.png
[2]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-source-control-configuration.png
[3]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-github-developer-applications.png
[4]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-github-register-a-new-oauth-application-populated.png
[5]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-github-register-a-new-oauth-application-complete.png
[6]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-roles-management-server-repair-all.png
[7]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-bitbucket-dashboard.png
[8]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-bitbucket-access-management-add-oauth-consumer.png
[9]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-bitbucket-access-management-add-oauth-consumer-complete.png
[10]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-applications.png
[11]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-application-registration.png
[12]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-application-platform.png
[13]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Onedrive-application-graph-permissions.png
[14]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Dropbox-applications.png
[15]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Dropbox-application-registration.png
[16]: ./media/azure-stack-app-service-configure-deployment-sources/App-service-provider-admin-Dropbox-application-configuration.png
