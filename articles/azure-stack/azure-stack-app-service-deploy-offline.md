---
title: "Implementación de App Service en un entorno sin conexión: Azure Stack | Microsoft Docs"
description: "Instrucciones detalladas sobre cómo toodeploy servicio de aplicaciones en un entorno desconectado de la pila de Azure protegidas por AD FS."
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
ms.date: 7/3/2017
ms.author: anwestg
ms.openlocfilehash: f7992c310532427b5ffb88555faab2679023c876
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-app-service-resource-provider-tooa-disconnected-azure-stack-environment-secured-by-ad-fs"></a>Agregar que un tooa de proveedor de recursos de servicio de aplicaciones desconectado entorno Azure pila protegido por AD FS

Debe agregar una [proveedor de recursos de servicio de aplicaciones de Azure](azure-stack-app-service-overview.md) tooyour implementación de pila de Azure:

* Si se ejecuta Azure Stack en un entorno aislado protegido por los Servicios de federación de Active Directory (AD FS). 
* Si desea que toogive los inquilinos hello web toocreate de capacidad, dispositivos móviles y aplicaciones de API y aplicaciones de funciones de Azure--con su suscripción de la pila de Azure. 

toodo por lo tanto, siga los pasos de hello en este artículo.

## <a name="download-hello-required-components"></a>Descargar los componentes necesario de Hola

1. Descargar hello [servicio de aplicaciones en el instalador de vista previa de Azure pila](http://aka.ms/appsvconmasrc1installer).

2. Descargar hello [servicio de aplicaciones en scripts de aplicación auxiliar de la implementación de Azure pila](http://aka.ms/appsvconmasrc1helper).

3. Extraiga los archivos de hello del archivo zip de hello auxiliar secuencias de comandos. Hello siguientes archivos y estructura de carpetas aparecen:

   - Create-AppServiceCerts.ps1
   - Create-IdentityApp.ps1
   - Módulos
      - AzureStack.Identity.psm1
      - GraphAPI.psm1

## <a name="create-an-offline-installation-package"></a>Creación de un paquete de instalación sin conexión

toodeploy servicio de aplicaciones en un entorno aislado, debe crear un paquete de instalación sin conexión desde un equipo que se conecta a Internet toohello.

1. Ejecute hello servicio de aplicaciones en el instalador de vista previa de Azure pila (AppService.exe) desde un equipo que está conectado a Internet toohello.

2. Haga clic en hello **avanzadas** ficha y haga clic en **crear paquete de instalación sin conexión**.

    ![Creación de un paquete de instalación sin conexión de App Service en Azure Stack][1]

3. Hola instalador del servicio de aplicaciones crea un paquete de instalación sin conexión, muestra la ruta de acceso de Hola y proporciona una carpeta de opción tooopen Hola.

   ![Paquete de instalación sin conexión de App Service en Azure Stack][2]

4. Copie Hola servicio de aplicaciones en el instalador de vista previa de Azure pila (AppService.exe) y equipo de host de hello instalación sin conexión paquete toohello pila de Azure.

## <a name="create-certificates-required-by-app-service-on-azure-stack"></a>Creación de certificados necesarios para App Service en Azure Stack

Este primer script funciona con hello Azure pila toocreate tres certificados de entidades emisoras que necesita el servicio de aplicaciones. Ejecutar script de hello en el host de la pila de Azure de Hola y asegúrese de que está ejecutando PowerShell como azurestack\administrator.

1. En una sesión de PowerShell que se ejecuta como azurestack\administrator, ejecute hello **AppServiceCerts.ps1 crear** script de ubicación de hello en la que extrajo las secuencias de comandos de aplicación auxiliar de Hola.  script de Hola crea tres certificados en hello misma carpeta que Hola Crear script de certificados que son necesarios para el servicio de aplicaciones.

2. Escriba una contraseña toosecure Hola los archivos .pfx y tome nota del mismo. Necesita tooenter en hello servicio de aplicaciones en el instalador de la pila de Azure.

### <a name="create-appservicecertsps1-parameters"></a>Parámetros de Create-AppServiceCerts.ps1

| Parámetro | Obligatorio/opcional | Valor predeterminado | Descripción |
| --- | --- | --- | --- |
| pfxPassword | Obligatorio | Null | La contraseña usa la clave privada del certificado de hello tooprotect |
| DomainName | Obligatorio | local.azurestack.external | Región y sufijo de dominio de Azure Stack |
| CertificateAuthority | Obligatorio | AzS-CA01.azurestack.local | Punto de conexión de entidad de certificación |

## <a name="complete-hello-offline-installation-of-app-service-on-azure-stack"></a>Completar la instalación sin conexión de hello del servicio de aplicaciones en la pila de Azure

> [!NOTE]
> Se *debe* usar un instalador de hello tooexecute cuenta con privilegios elevados (Administrador local o de dominio). Si se inicia sesión como azurestack\azurestackuser, se pedirán credenciales con privilegios elevados.

1. Ejecute appservice.exe como azurestack\administrator.

2. Haga clic en hello **avanzadas** ficha y haga clic en **completar la instalación sin conexión**.

    ![Realización de la instalación sin conexión de App Service en Azure Stack][3]

3. Especificar ubicación de Hola Hola sin conexión del paquete de instalación previamente creado y haga clic en **siguiente**.

    ![Ubicación del paquete de instalación sin conexión de App Service en Azure Stack][4]

4. Revise y acepte los términos de licencia de versión preliminar del Software de Microsoft de Hola y haga clic en **siguiente**.

5. Revise y acepte los términos de licencia de terceros de Hola y haga clic en **siguiente**.

6. Hola revisión servicio de aplicaciones de la información de configuración en la nube y haga clic en **siguiente**.

    ![Configuración de la nube de App Service en Azure Stack][5]

    > [!NOTE]
    > Hola servicio de aplicaciones en el instalador de la pila de Azure proporciona valores predeterminados de Hola para una instalación de la pila de Azure de un nodo. Si ha personalizado opciones cuando implementa la pila de Azure (por ejemplo, el sufijo de dominio hello), necesita valores de hello tooedit en esta ventana en consecuencia. Por ejemplo, si usa mycloud.com de sufijo de dominio de hello, el punto de conexión del Administrador de recursos de Azure de administración necesita toochange tooadminmanagement. [region]. mycloud.com.

7. Haga clic en hello **conectar** botón siguiente toohello **suscripciones de Azure pila** cuadro. Escriba la cuenta de administrador, por ejemplo, azurestackadmin@azurestack.local. Escriba la contraseña y haga clic en **Iniciar sesión**.

8. Seleccione la suscripción en hello **suscripciones de Azure pila** cuadro.

9. Hola **ubicaciones de la pila de Azure** cuadro Ubicación Hola seleccione correspondiente región toohello va a implementar. Por ejemplo, seleccione **local**. Haga clic en **Siguiente**.

    ![Selección de la suscripción de App Service en Azure Stack][6]

10. Escriba hello **nombre del grupo de recursos** para la implementación del servicio de aplicación. De forma predeterminada, se establece demasiado**APPSERVICE LOCAL**.

11. Escriba hello **nombre de la cuenta de almacenamiento** desea toocreate de servicio de aplicaciones como parte de la instalación de Hola. De forma predeterminada, se establece demasiado**appsvclocalstor**.

12. Escriba los detalles de SQL Server de Hola de instancia de Hola que toohost usado hello las bases de datos del proveedor de recursos de servicio de aplicaciones. Haga clic en **siguiente**, así como el instalador de hello valida propiedades de conexión de SQL de Hola.

13. Haga clic en hello **examinar** botón siguiente toohello **archivo de certificado SSL de servicio de aplicaciones predeterminado** cuadro. Vaya toohello **_.appservice.local.AzureStack.external** certificado [creado anteriormente](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps). Si especifica una ubicación diferente y el sufijo del dominio al crear el certificado de hello, seleccione el correspondiente certificado Hola.

14. Escriba la contraseña de certificado de Hola que estableciste cuando creaste certificado Hola.

15. Haga clic en hello **examinar** botón siguiente toohello **archivo de certificado SSL de proveedor de recursos** cuadro. Vaya toohello **api.appservice.local.AzureStack.external** certificado [creado anteriormente](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps). Si especifica una ubicación diferente y el sufijo del dominio al crear el certificado de hello, seleccione el correspondiente certificado Hola.

16. Escriba la contraseña de certificado de Hola que estableciste cuando creaste certificado Hola.

17. Haga clic en hello **examinar** botón siguiente toohello **archivo de certificado de raíz de proveedor de recursos** cuadro. Vaya toohello **AzureStackCertificationAuthority** certificado [creado anteriormente](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps).

18. Haga clic en **Siguiente**. instalador de Hello comprueba la contraseña del certificado de hello proporcionada.

    ![Detalles del certificado de App Service en Azure Stack][8]

19. Revise Hola configuración del rol de servicio de aplicaciones. valores predeterminados de Hola se rellenan con hello mínima recomendada instancia SKU para cada rol. Un resumen de los requisitos de memoria y los núcleos es siempre toohelp planear la implementación. Después de realizar las selecciones, haga clic en **Siguiente**.

    - **Controlador**: de forma predeterminada, se selecciona una instancia de Estándar A1. Se trata de mínimo de Hola que se recomienda. rol de controlador de Hello es responsable de administrar y mantener el estado de Hola de hello nube de servicio de aplicaciones.
    - **Administración**: de forma predeterminada, se selecciona una instancia de Estándar A2. conmutación por error tooprovide, se recomienda dos instancias. rol de administración de Hello es responsable de Hola, Administrador de recursos de aplicación de servicio de Azure y extremos de API, extensiones portales (administración, inquilino, el portal de funciones) y servicio de datos de Hola.
    - **Publicador**: de forma predeterminada, se selecciona una instancia de Estándar A1. Se trata de mínimo de Hola que se recomienda. rol de publicador Hello es responsable de publicar el contenido a través de la implementación de web y FTP.
    - **FrontEnd**: de forma predeterminada, se selecciona una instancia de Estándar A1. Se trata de mínimo de Hola que se recomienda. rol de front-end de Hello es responsable de aplicaciones de servicio de enrutamiento solicitudes tooApp.
    - **Trabajo compartido**: de forma predeterminada, se selecciona una instancia de A1 estándar, pero puede tooadd más. Como administrador, puede definir su oferta y elegir cualquier nivel de SKU. niveles de Hello deben tener un mínimo de un núcleo. rol de trabajo compartido Hello es responsable de hospedaje web, móviles, o aplicaciones de API y aplicaciones de funciones de Azure.

    ![Configuración del rol de App Service en Azure Stack][9]

    > [!NOTE]
    > En technical Preview hello, Hola instalador de proveedor de recursos de servicio de aplicaciones también implementa un toooperate de instancia estándar A1 como una saludos de toosupport Azure Resource Manager del servidor de archivos simple. Esto se conserva para el punto de contacto de un único nodo. Para las cargas de trabajo de producción, en hello servicio de aplicaciones de la disponibilidad general instalador permite uso de Hola de un servidor de archivos de alta disponibilidad.

20. Elija la implementación **Windows Server 2016** imagen de máquina virtual de las que están disponibles en el proveedor de recursos de proceso de Hola para hello nube de servicio de aplicaciones. Haga clic en **Siguiente**. 

    ![Selección de la imagen de VM de App Service en Azure Stack][10]

21. Escriba un nombre de usuario y una contraseña para los roles de trabajo de hello configurados en hello nube de servicio de aplicaciones. Escriba un nombre de usuario y una contraseña para todos los demás roles de App Service. Haga clic en **Siguiente**.

    ![Entrada de credenciales de App Service en Azure Stack][11]

22. En la pantalla de resumen de bienvenida, compruebe las selecciones de hello realizados. toomake cambios, vuelva a través de las pantallas de Hola y modificar sus selecciones. Si configuración de hello es su agrado, active la casilla de verificación de Hola. implementación de hello toostart, haga clic en **siguiente**. 

    ![Resumen de la selección de App Service en Azure Stack][12]

23. Realizar un seguimiento del progreso de la instalación de Hola. Servicio de aplicaciones en la pila de Azure tiene unos 45 toodeploy de minutos de too60 en función de las selecciones predeterminadas de Hola.

    ![Progreso de la instalación de App Service en Azure Stack][13]

24. Después de que el instalador de hello finalice correctamente, haga clic en **Exit**.

## <a name="configure-an-ad-fs-service-principal-for-virtual-machine-scale-set-integration-on-worker-tiers-and-sso-for-hello-azure-functions-portal-and-advanced-developer-tools"></a>Configurar una entidad de seguridad de servicio de AD FS para la integración de conjunto de escala de máquinas virtuales en los niveles de trabajo y SSO para herramientas de desarrollo de portal y avanzados de hello las funciones de Azure

>[!NOTE]
> Estos pasos aplican tooAD que FS protegidos solo entornos de pila de Azure.

Los administradores necesitan tooconfigure SSO para:

* Configurar a una entidad de servicio para la integración del conjunto de escalado de máquinas virtuales en los niveles de trabajo.
* Habilitar Hola avanzadas herramientas de desarrollo en el servicio de aplicaciones (Kudu).
* Habilitar el uso de Hola de experiencia del portal hello las funciones de Azure. 

Siga estos pasos:

1. Abra una instancia de PowerShell como azurestack\azurestackadmin.

2. Vaya a toohello ubicación de las secuencias de comandos de hello descargado y extraído Hola [requisito previo](#Download-Required-Components).

3. [Instale](azure-stack-powershell-install.md) y [configure un entorno de PowerShell de Azure Stack](azure-stack-powershell-configure-admin.md).

4. Hola misma sesión de PowerShell, ejecute hello **CreateIdentityApp.ps1** secuencia de comandos. Cuando se le pida el identificador de inquilino de Azure Active Directory (Azure AD), escriba **ADFS**.

5. Hola **credencial** ventana, escriba la cuenta de administrador de servicio de AD FS y la contraseña. Haga clic en **Aceptar**.

6. Escriba Hola certificado ruta de acceso y el certificado de contraseña del archivo de hello [certificado creado anteriormente](# Create certificates toobe used by App Service on Azure Stack). certificado de Hello creada para este paso de forma predeterminada es sso.appservice.local.azurestack.external.pfx.

7. script de Hola crea una nueva aplicación en Azure AD del inquilino de Hola y genera un nuevo script de PowerShell.

8. Copiar archivo de certificado de aplicación de identidad de Hola y Hola genera script toohello **CN0-VM** mediante una sesión de escritorio remota.

9. Devolver demasiado**CN0-VM**.

10. Abra una ventana de PowerShell de administrador y busque el directorio toohello donde el archivo de script de Hola y el certificado se copiaron en el paso 7.

11. Ejecute el archivo de script de Hola. Este archivo de script entra en Propiedades de Hola Hola servicio de aplicaciones en la configuración de la pila de Azure e inicia una operación de reparación en todos los front-end y la administración de roles.

| Parámetro | Obligatorio/opcional | Valor predeterminado | Descripción |
| --- | --- | --- | --- |
| DirectoryTenantName | Obligatorio | Null | Use **ADFS** para entorno de hello AD FS |
| TenantAzure Resource ManagerEndpoint | Obligatorio | management.local.azurestack.external | inquilino de Hello punto de conexión de administrador de recursos de Azure |
| AzureStackCredential | Obligatorio | Null | cuenta de administrador del servicio de Hello AD FS |
| CertificateFilePath | Obligatorio | Null | Archivo de certificado de aplicación en identidad de ruta de acceso toohello generado anteriormente |
| CertificatePassword | Obligatorio | Null | La contraseña usa la clave privada del certificado de hello tooprotect |
| DomainName | Obligatorio | local.azurestack.external | Región y sufijo de dominio de Azure Stack |
| AdfsMachineName | Opcional | Nombre de la máquina de AD FS, por ejemplo, AzS-ADFS01.azurestack.local |


## <a name="validate-hello-app-service-on-azure-stack-installation"></a>Validar Hola servicio de aplicaciones en la instalación de la pila de Azure

1. En el portal de administración de la pila de Azure de hello, vaya toohello grupo de recursos creado por el instalador de Hola. De forma predeterminada, este grupo es **APPSERVICE-LOCAL**.

2. Busque hello **CN0-VM**. tooconnect toohello de máquina virtual, haga clic en **conectar** en hello **Máquina Virtual** hoja.

3. En el escritorio de Hola de esta máquina virtual, haga doble clic en **consola de administración de Web en la nube**.

4. Vaya demasiado**servidores administrados por**.

5. Cuando todos Hola máquinas mostrar **listo** para uno o varios trabajadores, continuar toostep 6.

6. Cierre la máquina de escritorio remoto de Hola y máquina toohello devuelto donde ejecutó Hola instalador del servicio de aplicación.

    > [!NOTE]
    > No es necesario toowait para uno o más toodisplay de trabajadores **listo** instalación de hello toocomplete de servicio de aplicaciones en la pila de Azure. Sin embargo, se necesita un mínimo de un trabajador que está listo toodeploy un sitio web, móvil, o aplicación de API o funciones de Azure.
    
    ![Estado de los servidores administrados de App Service en Azure Stack][14]

## <a name="test-drive-app-service-on-azure-stack"></a>Prueba de App Service en Azure Stack

Después de implementar y registrar el proveedor de recursos de servicio de aplicaciones de hello, probarlo toomake seguro de que los inquilinos pueden implementar web, móviles y aplicaciones de API.

> [!NOTE]
> Debe toocreate una oferta con espacio de nombres de hello Microsoft.Web dentro de plan de Hola. A continuación, deberá toohave una suscripción de inquilino que se suscribe toothis oferta. Para más información, consulte [Create offer](azure-stack-create-offer.md) (Creación de una oferta) y [Create plan](azure-stack-create-plan.md) (Creación de un plan).
>

Se *debe* tiene un inquilino suscripción toocreate las aplicaciones que usan el servicio de aplicaciones en la pila de Azure. las capacidades solo de Hola que un administrador de servicios puede completarse dentro del portal de administración Hola están relacionados toohello administración del proveedor de recursos de servicio de aplicaciones. Entre estas funcionalidades se incluyen la adición de capacidad, la configuración de orígenes de implementación y la adición de niveles de trabajo y SKU.

A partir de hello tercera versión technical preview, toocreate web, móviles y aplicaciones de API debe usar el portal del inquilino de Hola y tener una suscripción de inquilino.  

1. En el portal del inquilino de Azure pila de hello, haga clic en **New** > **Web y móvil** > **aplicación Web**.

2. En hello **aplicación Web** hoja, escriba un nombre en hello **aplicación Web** cuadro.

3. En **Grupo de recursos**, haga clic en **Nuevo**. A continuación, escriba un nombre en hello **grupo de recursos** cuadro.

4. Haga clic en **Plan de App Service/Ubicación** > **Create New** (Crear nuevo).

5. En hello **plan de servicio de aplicaciones** hoja, escriba un nombre en hello **plan de servicio de aplicaciones** cuadro.

6. Haga clic en **Plan de tarifa** > **Free-Shared** (Gratis - Compartido) o **Shared-Shared** (Compartido - Compartido) > **Seleccionar** > **Aceptar** > **Crear**.

7. En menos de un minuto, un icono de la aplicación web nueva de hello aparece en panel de Hola. Haga clic en el icono de Hola.

8. En hello **aplicación Web** hoja, haga clic en **examinar** sitio Web de tooview Hola predeterminado para esta aplicación.

## <a name="deploy-a-wordpress-dnn-or-django-website-optional"></a>Implementación de un sitio web de WordPress, DNN o Django (opcional)

1. En el portal del inquilino de Azure pila de hello, haga clic en  **+** . Paso toohello Azure Marketplace, implementar un sitio Web de Django y esperar la finalización correcta. plataforma de Hello Django web usa una base de datos de archivo basado en el sistema. No requiere ningún proveedor de recursos adicional, como SQL o MySQL.

2. Si también implementa un proveedor de recursos de MySQL, puede implementar un sitio Web de WordPress de hello Marketplace. Cuando se le pide para los parámetros de la base de datos, escriba el nombre de usuario de hello como  *User1@Server1* , con nombre de usuario de Hola y el nombre del servidor de su elección.

3. Si también implementa un proveedor de recursos de SQL Server, puede implementar un sitio Web DNN de hello Marketplace. Cuando se le pide para los parámetros de la base de datos, elegir una base de datos en equipo de Hola que ejecuta SQL Server que es el proveedor de recursos de tooyour conectado.

## <a name="next-steps"></a>Pasos siguientes

También puede probar otros [servicios de Plataforma como servicio (PaaS)](azure-stack-tools-paas-services.md).

- [Proveedor de recursos de SQL Server](azure-stack-sql-resource-provider-deploy.md)
- [Proveedor de recursos de MySQL](azure-stack-mysql-resource-provider-deploy.md)

<!--Image references-->
[1]: ./media/azure-stack-app-service-deploy-offline/app-service-offline-step1.png
[2]: ./media/azure-stack-app-service-deploy-offline/app-service-offline-step2.png
[3]: ./media/azure-stack-app-service-deploy-offline/app-service-offline-step3.png
[4]: ./media/azure-stack-app-service-deploy-offline/app-service-offline-step4.png
[5]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-cloud-configuration.png
[6]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-subscription-location-populated.png
[7]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-resource-group-SQL.png
[8]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-certificates.png
[9]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-role-configuration.png
[10]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-vm-image-selection.png
[11]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-default-entries-step-role-credentials.png
[12]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-selection-summary.png
[13]: ./media/azure-stack-app-service-deploy-offline/app-service-exe-installation-progress.png
[14]: ./media/azure-stack-app-service-deploy-offline/managed-servers.png


<!--Links-->
[Azure_Stack_App_Service_preview_installer]: http://go.microsoft.com/fwlink/?LinkID=717531
[App_Service_Deployment]: http://go.microsoft.com/fwlink/?LinkId=723982
[AppServiceHelperScripts]: http://go.microsoft.com/fwlink/?LinkId=733525
