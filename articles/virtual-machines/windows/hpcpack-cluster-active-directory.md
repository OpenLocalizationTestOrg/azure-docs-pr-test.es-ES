---
title: "aaaHPC módulo de clúster con Azure Active Directory | Documentos de Microsoft"
description: "Obtenga información acerca de cómo agrupar toointegrate una 2016 de HPC Pack en Azure con Azure Active Directory"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
ms.assetid: 9edf9559-db02-438b-8268-a6cba7b5c8b7
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 11/14/2016
ms.author: danlep
ms.openlocfilehash: 0806e544a468e27ca0567e18c55554811584fbc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-hpc-pack-cluster-in-azure-using-azure-active-directory"></a>Administrar un clúster de HPC Pack en Azure con Azure Active Directory
[Microsoft HPC Pack 2016](https://technet.microsoft.com/library/cc514029) admite la integración con [Azure Active Directory](../../active-directory/index.md) (Azure AD) para los administradores que implementación un clúster de HPC Pack en Azure.



Siga los pasos de hello en este artículo para hello siguiente las tareas de nivel alto: 
* Integración manual del clúster de HPC Pack con el inquilino de Azure AD
* Administración y programación de trabajos en el clúster de HPC Pack en Azure 

Integrar una solución de clúster de HPC Pack con Azure AD sigue los pasos estándar toointegrate otras aplicaciones y servicios. En este artículo se da por supuesto que está familiarizado con la administración básica de usuarios en Azure AD. Para obtener más información y contexto, vea hello [documentación de Azure Active Directory](../../active-directory/index.md) y Hola pasos de la sección.

## <a name="benefits-of-integration"></a>Ventajas de la integración


Azure Active Directory (Azure AD) es un multiempresa en la nube identidades y directorios servicio de administración que proporciona acceso de inicio de sesión único (SSO) toocloud soluciones.

Integración de un clúster de HPC Pack con Azure AD puede ayudarle a conseguir Hola siguientes objetivos:

* Quitar el controlador de dominio de Active Directory tradicional de Hola de clúster de HPC Pack Hola. Esto puede ayudar a reducir los costes de Hola de mantenimiento de clúster de hello si esto no es necesario para su empresa y el proceso de implementación de acelerar Hola.
* Aprovechar Hola después ventajas señalados por Azure AD:
    *   Inicio de sesión único 
    *   Con una identidad de AD local para el clúster de HPC Pack hello en Azure 

    ![Entorno de Azure Active Directory](./media/hpcpack-cluster-active-directory/aad.png)


## <a name="prerequisites"></a>Requisitos previos
* **Clúster de HPC Pack 2016 implementado en máquinas virtuales de Azure**: Para conocer los pasos, consulte [Deploy an HPC Pack 2016 cluster in Azure](hpcpack-2016-cluster.md) (Implementación de un clúster de HPC Pack 2016 en Azure). Necesita el nombre DNS de hello del nodo principal de Hola y las credenciales de Hola de un administrador de clústeres para completar los pasos de hello en este artículo.

  > [!NOTE]
  > La integración con Azure Active Directory no se admite en versiones de HPC Pack antes a HPC Pack 2016.



* **Equipo cliente** -necesita un Windows o Windows Server cliente equipo ejecuta demasiado HPC Pack utilidades de cliente. Si solo desea portal web de toouse Hola HPC Pack o trabajos de toosubmit de API de REST, puede usar todos los equipos cliente de su elección.

* **Utilidades de cliente de HPC Pack** -instalar utilidades de cliente de HPC Pack Hola en los equipos de cliente de hello con el paquete de instalación gratuito de hello disponible desde Microsoft Download Center Hola.


## <a name="step-1-register-hello-hpc-cluster-server-with-your-azure-ad-tenant"></a>Paso 1: Registrar servidor de clúster HPC de hello con su inquilino de Azure AD
1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Haga clic en **Active Directory** en Hola menú izquierdo y, a continuación, haga clic en directorio que desee hello en su suscripción. Debe tener permisos de los recursos tooaccess en el directorio de Hola.
3. Haga clic en **Usuarios** y asegúrese de que ya hay cuentas de usuario creadas o configuradas.
4. Haga clic en **Aplicaciones** > **Agregar** y luego en **Agregar una aplicación que mi organización está desarrollando**. Escriba Hola después información Hola asistente:
    * **Nombre**: HPCPackClusterServer
    * **Tipo**: Seleccione **Aplicación web y/o API web**
    * **Dirección URL de inicio de sesión**: hello dirección URL base para el ejemplo hello, que de forma predeterminada`https://hpcserver`
    * **URI de id. de aplicación** - `https://<Directory_name>/<application_name>`. Reemplace `<Directory_name`> con el nombre completo del inquilino de Azure AD, por ejemplo, hello `hpclocal.onmicrosoft.com`y reemplace `<application_name>` con nombre hello elegido anteriormente.

5. Después de agrega la aplicación hello, haga clic en **configurar**. Configurar Hola propiedades siguientes:
    * Seleccione **Sí** en **La aplicación es multiempresa**.
    * Seleccione **Sí** para **usuario asignación requiere tooaccess aplicación**.

6. Haga clic en **Guardar**. Cuando se complete el almacenamiento, haga clic en **Administrar manifiesto**. Esta acción descarga la notación de objetos JavaScript (JSON) del manifiesto de la aplicación. Editar manifiesto de hello descargado ubicando hello `appRoles` establecimiento y adición de hello después de rol de aplicación:
    ```json
    "appRoles": [
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "displayName": "HpcAdminMirror",
        "id": "61e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "description": "HpcAdminMirror",
        "value": "HpcAdminMirror"
        },
        {
        "allowedMemberTypes": [
            "User",
            "Application"
        ],
        "description": "HpcUsers",
        "displayName": "HpcUsers",
        "id": "91e10148-16a8-432a-b86d-ef620c3e48ef",
        "isEnabled": true,
        "value": "HpcUsers"
        }
    ],
    ```
7. Guarde el archivo hello. Haga clic en el portal de hello, **administrar manifiesto** > **cargar manifiesto**. A continuación, puede cargar el manifiesto editado de Hola.
8. Haga clic en **Usuarios**, seleccione un usuario y luego haga clic en **Asignar**. Asignar uno de usuario de toohello (HpcUsers o HpcAdminMirror) roles disponibles de Hola. Repita este paso con otros usuarios en el directorio de Hola. Para información general sobre de los usuarios de clúster, consulte [Managing Cluster Users](https://technet.microsoft.com/library/ff919335(v=ws.11).aspx) (Administrar usuarios de clústeres).

   > [!NOTE] 
   > toomanage los usuarios, recomendamos usar la hoja de vista previa de Azure Active Directory de Hola Hola [portal de Azure](https://portal.azure.com).
   >


## <a name="step-2-register-hello-hpc-cluster-client-with-your-azure-ad-tenant"></a>Paso 2: Registrar el cliente de clúster HPC de hello con su inquilino de Azure AD

1. Inicie sesión en toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Haga clic en **Active Directory** en Hola menú izquierdo y, a continuación, haga clic en directorio que desee hello en su suscripción. Debe tener permisos de los recursos tooaccess en el directorio de Hola.
3. Haga clic en **Aplicaciones** > **Agregar** y luego en **Agregar una aplicación que mi organización está desarrollando**. Escriba Hola después información Hola asistente:

    * **Nombre**: HPCPackClusterClient
    * **Tipo**: Seleccione **Aplicación de cliente nativo**
    * **URI de redirección** - `http://hpcclient`

4. Después de agrega la aplicación hello, haga clic en **configurar**. Hola copia **Id. de cliente** valor y guárdelo. Lo necesitará más adelante cuando configure la aplicación.

5. En **permisos tooother aplicaciones**, haga clic en **Agregar aplicación**. Buscar y Agregar aplicación de hello HpcPackClusterServer (creado en el paso 1).

6. Hola **permisos delegados** lista desplegable, seleccione **HpcClusterServer de acceso**. A continuación, haga clic en **Guardar**.


## <a name="step-3-configure-hello-hpc-cluster"></a>Paso 3: Configurar el clúster de HPC de Hola

1. Conecte el nodo principal de HPC Pack 2016 toohello en Azure.

2. Inicie PowerShell HPC.

3. Ejecute el siguiente comando de hello:

    ```powershell

    Set-HpcClusterRegistry -SupportAAD true -AADInstance https://login.microsoftonline.com/ -AADAppName HpcClusterServer -AADTenant <your AAD tenant name> -AADClientAppId <client ID> -AADClientAppRedirectUri http://hpcclient
    ```
    donde

    * `AADTenant`Especifica el nombre del inquilino de Azure AD de hello, como`hpclocal.onmicrosoft.com`
    * `AADClientAppId`Especifica el identificador de cliente de hello para la aplicación hello creado en el paso 2.

4. Reinicie el servicio de hello HpcSchedulerStateful.

    En un clúster con varios nodos principales, puede ejecutar Hola siguiente comandos de PowerShell de hello nodo principal tooswitch Hola réplica principal de servicio de Hola HpcSchedulerStateful:

    ```powershell
    Connect-ServiceFabricCluster

    Move-ServiceFabricPrimaryReplica –ServiceName “fabric:/HpcApplication/SchedulerStatefulService”

    ```

## <a name="step-4-manage-and-submit-jobs-from-hello-client"></a>Paso 4: Administrar y enviar trabajos de cliente hello

Utilidades de cliente de HPC Pack tooinstall hello en el equipo, descargue los archivos de instalación de HPC Pack 2016 (instalación completa) de hello Microsoft Download Center. Al comenzar la instalación de hello, elija la opción de instalación de Hola para hello **utilidades de cliente de HPC Pack**.

equipo de cliente de tooprepare hello, instalar certificado de hello usa durante la [el programa de instalación de clúster HPC](hpcpack-2016-cluster.md) en el equipo cliente de Hola. Usar Windows estándares de certificados administración procedimientos tooinstall Hola certificado público toohello **certificados – usuario actual** > **entidades de certificación raíz de confianza** almacenar. 

Ahora puede ejecutar comandos de HPC Pack Hola o usar Hola GUI del Administrador de trabajos de HPC Pack toosubmit y administrar trabajos del clúster mediante el uso de la cuenta de hello Azure AD. Para opciones de envío de trabajos, consulte [clúster de HPC enviar trabajos tooan HPC Pack en Azure](hpcpack-cluster-submit-jobs.md#step-3-run-test-jobs-on-the-cluster).

> [!NOTE]
> Al tratar de clúster de HPC Pack del toohello tooconnect en Azure para hello primera vez, aparece una ventana emergente. Escriba su toolog de credenciales de Azure AD en. símbolo (token) de Hello, a continuación, se almacena en caché. Clúster de toohello conexiones posterior Hola de uso de Azure almacena en caché símbolo (token), a menos que los cambios de autenticación o hello almacenado en memoria caché se borra.
>
  
Por ejemplo, después de completar los pasos anteriores de hello, puede consultar para trabajos desde un cliente local como sigue:

```powershell 
Get-HpcJob –State All –Scheduler https://<Azure load balancer DNS name> -Owner <Azure AD account>
```

## <a name="useful-cmdlets-for-job-submission-with-azure-ad-integration"></a>Cmdlets útiles para el envío de trabajos con integración de Azure AD 

### <a name="manage-hello-local-token-cache"></a>Administrar la caché de tokens local Hola

HPC Pack 2016 proporciona dos nuevos cmdlets de PowerShell de HPC en caché de tokens local toomanage Hola. Estos cmdlets son útiles para enviar trabajos de una manera no interactiva. Vea el siguiente ejemplo de Hola:

```powershell
Remove-HpcTokenCache

$SecurePassword = "<password>" | ConvertTo-SecureString -AsPlainText -Force

Set-HpcTokenCache -UserName <AADUsername> -Password $SecurePassword -scheduler https://<Azure load balancer DNS name> 
```

### <a name="set-hello-credentials-for-submitting-jobs-using-hello-azure-ad-account"></a>Establecer las credenciales de hello para el envío de trabajos con cuenta de hello Azure AD 

En ocasiones, puede que desee toorun trabajo de hello en el usuario del clúster HPC de hello (para un clúster HPC Unidos a un dominio, ejecutar como usuario de un dominio; para un clúster HPC no unido a un dominio, ejecutar como un usuario local en el nodo principal de hello).

1. Usar hello siguiendo las credenciales de Hola de tooset de comandos:

    ```powershell
    $localUser = “<username>”

    $localUserPassword=”<password>”

    $secpasswd = ConvertTo-SecureString $localUserPassword -AsPlainText -Force

    $mycreds = New-Object System.Management.Automation.PSCredential ($localUser, $secpasswd)

    Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name>
    ```

2. A continuación, enviar trabajo hello como se indica a continuación. Hola trabajo o tarea se ejecuta en $localUser en nodos de proceso de Hola.

    ```powershell
    $emptycreds = New-Object System.Management.Automation.PSCredential ($localUser, (new-object System.Security.SecureString))
    ...
    $job = New-HpcJob –Scheduler https://<Azure load balancer DNS name>

    Add-HpcTask -Job $job -CommandLine "ping localhost" -Scheduler https://<Azure load balancer DNS name>

    Submit-HpcJob -Job $job -Scheduler https://<Azure load balancer DNS name> -Credential $emptycreds
    ```
    
   Si `–Credential` no se especifica con `Submit-HpcJob`, Hola trabajo o la tarea se ejecuta bajo un usuario local asignado como Hola cuenta de Azure AD. (clúster de HPC de hello crea un usuario local con hello mismo nombre como tarea de Azure AD cuenta toorun hello hello).
    
3. Establecer datos extendidos para hello cuenta de Azure AD. Esto es útil cuando se ejecuta un trabajo de MPI en nodos de Linux con cuenta de hello Azure AD.

   * Establecer datos extendidos para hello propia cuenta de Azure AD

      ```powershell
      Set-HpcJobCredential -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data> -AadUser
      ```
      
   * Establezca los datos extendidos y realice la ejecución como usuario del clúster HPC.
   
      ```powershell
      Set-HpcJobCredential -Credential $mycreds -Scheduler https://<Azure load balancer DNS name> -ExtendedData <data>
      ```

