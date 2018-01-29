---
title: "Configuración de orígenes de implementación para App Services en Azure Stack | Microsoft Docs"
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
ms.date: 10/10/2017
ms.author: anwestg
ms.openlocfilehash: dc341d872a3b8943a934217ace21537f45bafd10
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 12/08/2017
---
# <a name="configure-deployment-sources"></a>Configuración de orígenes de implementación

App Service en Azure Stack admite la implementación a petición de varios proveedores de control de código fuente. Esta característica permite a los desarrolladores de aplicaciones implementar directamente desde sus repositorios de control de código fuente. Si los usuarios desean configurar App Service con el fin de conectarse a sus repositorios, en primer lugar, un operador en la nube debe configurar la integración entre App Service en Azure Stack y el proveedor de control de código fuente.  

Los proveedores de control de código fuente compatibles, además de Git local, son los siguientes:

* GitHub
* BitBucket
* OneDrive
* Dropbox

## <a name="view-deployment-sources-in-app-service-administration"></a>Visualización de orígenes de implementación en la administración de App Service

1. Inicie sesión en el Portal de administración de Azure Stack (https://adminportal.local.azurestack.external) como administrador del servicio.
2. Vaya a **Proveedores de recursos** y seleccione **App Service Resource Provider Admin** (Administración de proveedores de recursos de App Service).  ![Opción de administración de proveedores de recursos de App Service][1]
3. Haga clic en la **Source control configuration** (Configuración de control de código fuente).  Aquí verá la lista de todos los orígenes de implementación configurados.
    ![Configuración de control de código fuente de hoja de administración de proveedores de recursos de App Service][2]

## <a name="configure-github"></a>Configuración de GitHub

Debe tener una cuenta de GitHub para completar esta tarea. Puede que desee usar una cuenta de su organización en lugar de una personal.

1. Inicie sesión en GitHub, vaya a https://www.github.com/settings/developers y haga clic en **Register a new application** (Registrar una nueva aplicación).
    ![GitHub: Registro de una nueva aplicación][3]
2. Escriba el **nombre de la aplicación**, por ejemplo, App Service en Azure Stack.
3. Escriba la **dirección URL de la página principal**. La dirección URL de la página de inicio debe ser la de Azure Stack Portal. Por ejemplo, https://portal.local.azurestack.external.
4. Escriba la **descripción de la aplicación**.
5. Escriba la **URL de devolución de llamada de autorización**.  En una implementación de Azure Stack predeterminada, la dirección URL tiene el formato https://portal.local.azurestack.external/tokenauthorize. Si está usando otro dominio, sustituya el suyo por azurestack.local.
    ![GitHub: registro de una aplicación nueva con valores completados][4]
6. Haga clic en **Register application** (Registrar aplicación).  Se le mostrará ahora con una página con el **identificador de cliente** y el **secreto de cliente** de la aplicación.
    ![GitHub - Registro de aplicación completado][5]
7.  En una nueva pestaña o ventana del explorador, inicie sesión en el Portal de administración de Azure Stack (https://adminportal.local.azurestack.external) como administrador de servicios.
8.  Vaya a **Proveedores de recursos** y seleccione **App Service Resource Provider Admin** (Administración de proveedores de recursos de App Service).
9. Haga clic en la **Source control configuration** (Configuración de control de código fuente).
10. Copie y pegue el **identificador de cliente** y el **secreto del cliente** en los cuadros de entrada correspondientes de GitHub.
11. Haga clic en **Guardar**.

## <a name="configure-bitbucket"></a>Configuración de BitBucket

Debe tener una cuenta de BitBucket para llevar a cabo esta tarea. Puede que desee usar una cuenta de su organización en lugar de una personal.

1. Inicie sesión en BitBucket y vaya a **Integraciones** en su cuenta.
    ![Panel de BitBucket: integraciones][7]
2. Haga clic en **OAuth** en Administración de acceso y en **Add consumer** (Agregar consumidor).
    ![BitBucket Agregar consumidor OAuth][8]
3. Escriba un **nombre** para el consumidor, por ejemplo, App Service en Azure Stack.
4. Escriba una **descripción** para la aplicación.
5. Escriba la **URL de devolución de llamada**.  En una implementación de Azure Stack predeterminada, la dirección URL de devolución de llamada tiene el formato https://portal.local.azurestack.external/TokenAuthorize. Si está usando otro dominio, sustituya el suyo por azurestack.local.  La URL debe seguir el patrón de mayúsculas y minúsculas que se muestra aquí para que la integración con BitBucket se realice correctamente.
6. Escriba la dirección **URL**: debe ser la de Azure Stack Portal; por ejemplo, https://portal.local.azurestack.external.
7. Seleccione los **permisos** necesarios:
    - **Repositorios**: *Lectura*
    - **Webhooks**: *Lectura y escritura*
8. Haga clic en **Guardar**.  Ahora verá esta nueva aplicación, junto con la **clave** y el **secreto** en **OAuth consumers** (Consumidores de OAuth).
    ![Lista de aplicaciones de BitBucket][9]
9.  En una nueva pestaña o ventana del explorador, inicie sesión en el Portal de administración de Azure Stack (https://adminportal.local.azurestack.external) como administrador de servicios.
10.  Vaya a **Proveedores de recursos** y seleccione **App Service Resource Provider Admin** (Administración de proveedores de recursos de App Service).
11. Haga clic en la **Source control configuration** (Configuración de control de código fuente).
12. Copie y pegue la **clave** en el cuadro de entrada de **identificador de cliente**, y el **secreto** en el cuadro de entrada de **secreto de cliente** de BitBucket.
13. Haga clic en **Guardar**.


## <a name="configure-onedrive"></a>Configuración de OneDrive

Debe tener una cuenta de Microsoft vinculada a una de OneDrive para completar esta tarea.  Puede que desee usar una cuenta de su organización en lugar de una personal.

> [!NOTE]
> En estos momentos, no se admiten las cuentas de OneDrive para la Empresa.

1. Vaya a https://apps.dev.microsoft.com/?referrer=https%3A%2F%2Fdev.onedrive.com%2Fapp-registration.htm e inicie sesión con su cuenta Microsoft.
2. En **Mis aplicaciones**, haga clic en **Agregar una aplicación**.
![Aplicaciones de OneDrive][10]
3. Escriba un **nombre** para el nuevo registro de aplicación, especifique **App Service en Azure Stack** y haga clic en **Crear aplicación**.
4. En la pantalla siguiente se enumeran las propiedades de la nueva aplicación. Anote el **identificador de aplicación**. ![Propiedades de la aplicación OneDrive][11]
5. En **Secretos de aplicación**, haga clic en **Generar nueva contraseña**. Tome nota de la **nueva contraseña generada**. Es el secreto de aplicación y no se puede recuperar tras hacer clic en **Aceptar** en esta fase.
6. En **Plataformas**, haga clic en **Agregar plataforma** y seleccione **Web**.
7. Copie el **URI de redirección**.  En una implementación de Azure Stack predeterminada, el URI de redirección tiene el formato https://portal.local.azurestack.external/tokenauthorize. Si está usando otro dominio, sustituya el suyo por azurestack.local. ![Aplicación de OneDrive - Agregar plataforma web][12]
8. Agregue los **permisos de Microsoft Graph** - **Permisos delegados**
    - **Files.ReadWrite.AppFolder**
    - **User.Read**  
      ![Aplicación de OneDrive - Permisos de Graph][13]
9. Haga clic en **Guardar**.
10.  En una nueva pestaña o ventana del explorador, inicie sesión en el Portal de administración de Azure Stack (https://adminportal.local.azurestack.external) como administrador de servicios.
11.  Vaya a **Proveedores de recursos** y seleccione **App Service Resource Provider Admin** (Administración de proveedores de recursos de App Service).
12. Haga clic en la **Source control configuration** (Configuración de control de código fuente).
13. Copie y pegue el **identificador de aplicación** en el cuadro de entrada de **identificador de cliente**, y la **contraseña** en el cuadro de entrada de **secreto de cliente** de OneDrive.
14. Haga clic en **Guardar**.

## <a name="configure-dropbox"></a>Configuración de Dropbox

> [!NOTE]
> Necesita una cuenta de Dropbox para completar esta tarea.  Puede que desee usar una cuenta de su organización en lugar de una personal.

1. Vaya a https://www.dropbox.com/developers/apps e inicie sesión con su cuenta de Dropbox.
2. Haga clic en **Create app**(Crear aplicación).

    ![Aplicaciones de dropbox][14]

3. Seleccione la **API de Dropbox**.
4. Establezca el nivel de acceso en **App Folder** (Carpeta de aplicaciones).
5. Escriba el **nombre** de la aplicación.
![Registro de aplicaciones de Dropbox][15]
6. Haga clic en **Create app** (Crear aplicación).  Ahora se mostrará una página con la configuración de la aplicación, incluidos la **clave de aplicación** y el **secreto de la aplicación**.
7. Compruebe que el **nombre de la carpeta de aplicaciones** es **App Service en Azure Stack**.
8. Establezca el **URI de redirección de OAuth 2** y haga clic en **Add** (Agregar).  En una implementación de Azure Stack predeterminada, la dirección URL de redirección tiene el formato https://portal.local.azurestack.external/tokenauthorize. Si está usando otro dominio, sustituya el suyo por azurestack.local.
![Configuración de aplicaciones de Dropbox][16]
9.  En una nueva pestaña o ventana del explorador, inicie sesión en el Portal de administración de Azure Stack (https://adminportal.local.azurestack.external) como administrador de servicios.
10.  Vaya a **Proveedores de recursos** y seleccione **App Service Resource Provider Admin** (Administración de proveedores de recursos de App Service).
11. Haga clic en la **Source control configuration** (Configuración de control de código fuente).
12. Copie y pegue la **clave de aplicación** en el cuadro de entrada de **identificador de cliente**, y el **secreto de aplicación** en el cuadro de entrada de **secreto de cliente** de Dropbox.
13. Haga clic en **Guardar**.


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

## <a name="next-steps"></a>Pasos siguientes

Los usuarios ahora pueden usar los orígenes de implementación para utilidades como la [implementación continua](https://docs.microsoft.com/azure/app-service-web/app-service-continuous-deployment), la [implementación de Git local](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-local-git) y la [sincronización de carpetas en la nube](https://docs.microsoft.com/azure/app-service-web/app-service-deploy-content-sync).
