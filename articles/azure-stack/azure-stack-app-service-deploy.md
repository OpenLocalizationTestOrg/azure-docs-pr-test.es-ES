---
title: "Implementación de App Services: Azure Stack | Microsoft Docs"
description: "Guía detallada para implementar App Service en Azure Stack"
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
ms.openlocfilehash: 41be7bca865f39b445e8f99450c4acde535c0806
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-app-service-resource-provider-tooazure-stack"></a>Agregar un tooAzure de proveedor de recursos pila de servicio de aplicaciones

Si desea tooenable los inquilinos toocreate web, móviles y las aplicaciones de API con su suscripción de la pila de Azure, debe agregar una [proveedor de recursos de servicio de aplicaciones de Azure](azure-stack-app-service-overview.md) tooyour implementación de pila de Azure. Siga los pasos de hello en este artículo.

## <a name="download-hello-required-components"></a>Descargar los componentes necesario de Hola

1. Descargar hello [servicio de aplicaciones en el instalador de vista previa de Azure pila](http://aka.ms/appsvconmasrc1installer).

2. Descargar hello [servicio de aplicaciones en scripts de aplicación auxiliar de la implementación de Azure pila](http://aka.ms/appsvconmasrc1helper).

3. Extraiga los archivos de hello del archivo zip de hello auxiliar secuencias de comandos. Hello siguientes archivos y estructura de carpetas aparecen:

   - Create-AppServiceCerts.ps1
   - Create-IdentityApp.ps1
   - Módulos
      - AzureStack.Identity.psm1
      - GraphAPI.psm1
   
## <a name="create-certificates-required-by-app-service-on-azure-stack"></a>Creación de certificados necesarios para App Service en Azure Stack

Este primer script funciona con hello Azure pila toocreate tres certificados de entidades emisoras que son necesarios para el servicio de aplicaciones. Ejecutar script de hello en el host de la pila de Azure de Hola y asegúrese de que está ejecutando PowerShell como azurestack\AzureStackAdmin.

1. En una sesión de PowerShell que se ejecuta como azurestack\AzureStackAdmin, ejecute hello **AppServiceCerts.ps1 crear** script desde la carpeta de hello en la que extrajo las secuencias de comandos de aplicación auxiliar de Hola. script de Hola crea tres certificados en hello misma carpeta Hola Crear script de certificados que el servicio aplicación necesita.

2. Escriba una contraseña toosecure Hola los archivos .pfx y tome nota del mismo. Deberá tooenter en hello servicio de aplicaciones en el instalador de la pila de Azure.

### <a name="create-appservicecertsps1-parameters"></a>Parámetros de Create-AppServiceCerts.ps1

| Parámetro | Obligatorio/opcional | Valor predeterminado | Descripción |
| --- | --- | --- | --- |
| pfxPassword | Obligatorio | Null | La contraseña usa la clave privada del certificado de hello tooprotect |
| DomainName | Obligatorio | local.azurestack.external | Región y sufijo de dominio de Azure Stack |
| CertificateAuthority | Obligatorio | AzS-CA01.azurestack.local | Punto de conexión de entidad de certificación |

## <a name="use-hello-installer-toodownload-and-install-app-service-on-azure-stack"></a>Utiliza toodownload de instalador de hello e instala el servicio de aplicaciones en pila de Azure

instalador de Hello appservice.exe hará lo siguiente:

* Símbolo del sistema tooaccept Hola Microsoft y los términos de licencia del Software de terceros.
* Recopilará información de la implementación de Azure Stack.
* Crear un blob en contenedor Hola especifica la cuenta de almacenamiento de la pila de Azure.
* Descargar Hola archivos necesarios tooinstall Hola proveedor de recursos de servicio de aplicaciones.
* Preparar hello toodeploy de instalación Hola proveedor de recursos de servicio de aplicaciones en el entorno de Azure pila Hola.
* Cargar archivos de hello toohello cuenta de almacenamiento del servicio de aplicaciones.
* Implementar Hola proveedor de recursos de servicio de aplicaciones.
* Creará una zona DNS y las entradas para App Service.
* Hola registrar proveedor de recursos de servicio de aplicaciones.
* Registrar los elementos de la Galería de servicio de aplicaciones de Hola.

Hello siguientes pasos le guiarán etapas de la instalación de Hola.

> [!NOTE]
> Se *debe* usar un instalador de hello toorun cuenta con privilegios elevados (Administrador local o de dominio). Si se inicia sesión como azurestack\azurestackuser, se pedirán credenciales con privilegios elevados.

1. Ejecute appservice.exe como azurestack\AzureStackAdmin.

2. Haga clic en **Implemente App Service en su nube de Azure Stack**.

    ![Instalador de App Service en Azure Stack][1]

3. Revise y acepte los términos de licencia de versión preliminar del Software de Microsoft de Hola y haga clic en **siguiente**.

4. Revise y acepte los términos de licencia de terceros de Hola y haga clic en **siguiente**.

5. Hola revisión servicio de aplicaciones de la información de configuración en la nube y haga clic en **siguiente**.

    ![Configuración de la nube de App Service en Azure Stack][2]

    > [!NOTE]
    > Hola servicio de aplicaciones en el instalador de la pila de Azure proporciona valores predeterminados de Hola para una instalación de la pila de Azure de un nodo. Si ha personalizado opciones cuando implementa la pila de Azure (por ejemplo, el sufijo de dominio hello), necesita valores de hello tooedit en esta ventana en consecuencia. Por ejemplo, si usa mycloud.com de sufijo de dominio de hello, el punto de conexión del Administrador de recursos de Azure de administración necesita toochange tooadminmanagement. [region]. mycloud.com.

6. Haga clic en hello **conectar** botón siguiente toohello **suscripciones de Azure pila** cuadro.

   - Si se usa Azure Active Directory (Azure AD), se debe escribir la cuenta de administrador y la contraseña de Azure AD. Haga clic en **Iniciar sesión**. Se *debe* especificar cuenta de hello Azure AD que proporcionó cuando se implementa la pila de Azure.
   - Si se usan los Servicios de federación de Active Directory (AD FS), se debe proporcionar la cuenta de administrador, por ejemplo, azurestackadmin@azurestack.local. Escriba la contraseña y haga clic en **Iniciar sesión**.

7. Seleccione la suscripción en hello **suscripciones de Azure pila** cuadro.

8. Hola **ubicaciones de la pila de Azure** cuadro Ubicación Hola seleccione correspondiente región toohello va a implementar. Por ejemplo, seleccione **local**. Haga clic en **Siguiente**.

    ![Selección de la suscripción de App Service en Azure Stack][3]

9. Escriba hello **nombre del grupo de recursos** para la implementación del servicio de aplicación. De forma predeterminada, se establece demasiado**APPSERVICE LOCAL**.

10. Escriba hello **nombre de la cuenta de almacenamiento** desea toocreate de servicio de aplicaciones como parte de la instalación de Hola. De forma predeterminada, se establece demasiado**appsvclocalstor**.

11. Escriba los detalles de SQL Server de Hola de instancia de Hola que toohost usado hello las bases de datos del proveedor de recursos de servicio de aplicaciones. Haga clic en **siguiente**, así como el instalador de hello valida propiedades de conexión de SQL de Hola.

    ![Grupo de recursos de App Service en Azure Stack, almacenamiento e información de SQL Server][4]

12. Haga clic en hello **examinar** botón siguiente toohello **archivo de certificado SSL de servicio de aplicaciones predeterminado** cuadro. Vaya toohello **_.appservice.local.AzureStack.external** certificado [creado anteriormente](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps). Si especifica una ubicación diferente y el sufijo del dominio al crear el certificado de hello, seleccione el correspondiente certificado Hola.

13. Escriba la contraseña de certificado de Hola que estableciste cuando creaste certificado Hola.

14. Haga clic en hello **examinar** botón siguiente toohello **archivo de certificado SSL de proveedor de recursos** cuadro. Vaya toohello **api.appservice.local.AzureStack.external** certificado [creado anteriormente](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps). Si especifica una ubicación diferente y el sufijo del dominio al crear certificados, seleccione el correspondiente certificado Hola.

15. Escriba la contraseña de certificado de Hola que estableciste cuando creaste certificado Hola.

16. Haga clic en hello **examinar** botón siguiente toohello **archivo de certificado de raíz de proveedor de recursos** cuadro. Vaya toohello **AzureStackCertificationAuthority** certificado [creado anteriormente](#Create-Certificates-To-Be-Used-By-Azure-Stack-Web-Apps).

17. Haga clic en **Siguiente**. instalador de Hello comprueba la contraseña del certificado de hello proporcionada.

    ![Detalles del certificado de App Service en Azure Stack][5]

18. Revise Hola configuración del rol de servicio de aplicaciones. valores predeterminados de Hola se rellenan con hello mínima recomendada instancia SKU para cada rol. Un resumen de los requisitos de memoria y los núcleos es siempre toohelp planear la implementación. Después de realizar las selecciones, haga clic en **Siguiente**.

    - **Controlador**: de forma predeterminada, se selecciona una instancia de Estándar A1. Se trata de mínimo de Hola que se recomienda. rol de controlador de Hello es responsable de administrar y mantener el estado de Hola de hello nube de servicio de aplicaciones.
    - **Administración**: de forma predeterminada, se selecciona una instancia de Estándar A2. conmutación por error tooprovide, se recomienda dos instancias. rol de administración de Hello es responsable de Hola, Administrador de recursos de aplicación de servicio de Azure y extremos de API, extensiones portales (administración, inquilino, el portal de funciones) y servicio de datos de Hola.
    - **Publicador**: de forma predeterminada, se selecciona una instancia de Estándar A1. Se trata de mínimo de Hola que se recomienda. rol de publicador Hello es responsable de publicar el contenido a través de la implementación de web y FTP.
    - **FrontEnd**: de forma predeterminada, se selecciona una instancia de Estándar A1. Se trata de mínimo de Hola que se recomienda. rol de front-end de Hello es responsable de aplicaciones de servicio de enrutamiento solicitudes tooApp.
    - **Trabajo compartido**: de forma predeterminada, se selecciona una instancia de A1 estándar, pero puede tooadd más. Como administrador, puede definir su oferta y elegir cualquier nivel de SKU. niveles de Hello deben tener un mínimo de un núcleo. rol de trabajo compartido Hello es responsable de hospedaje web, móviles, o aplicaciones de API y aplicaciones de funciones de Azure.

    ![Configuración del rol de App Service en Azure Stack][6]

    > [!NOTE]
    > En technical Preview hello, Hola instalador de proveedor de recursos de servicio de aplicaciones también implementa un toooperate de instancia estándar A1 como un toosupport de servidor de archivos simple Azure Resource Manager. Esto se conserva para el kit de desarrollo de un único nodo. Para las cargas de trabajo de producción, en hello servicio de aplicaciones de la disponibilidad general instalador permite uso de Hola de un servidor de archivos de alta disponibilidad.

19. Elija la implementación **Windows Server 2016** imagen de máquina virtual de las que están disponibles en el proveedor de recursos de proceso de Hola para hello nube de servicio de aplicaciones. Haga clic en **Siguiente**.

    ![Selección de la imagen de VM de App Service en Azure Stack][7]

20. Escriba un nombre de usuario y una contraseña para los roles de trabajo de hello configurados en hello nube de servicio de aplicaciones. Escriba un nombre de usuario y una contraseña para todos los demás roles de App Service. Haga clic en **Siguiente**.

    ![Entrada de credenciales de App Service en Azure Stack][8]

21. En la pantalla de resumen de bienvenida, compruebe las selecciones de hello realizados. toomake cambios, vuelva a través de las pantallas de Hola y modificar sus selecciones. Si configuración de hello es su agrado, active la casilla de verificación de Hola. implementación de hello toostart, haga clic en **siguiente**.

    ![Resumen de la selección de App Service en Azure Stack][9]

22. Realizar un seguimiento del progreso de la instalación de Hola. Servicio de aplicaciones en la pila de Azure tiene unos 45 toodeploy de minutos de too60 en función de las selecciones predeterminadas de Hola.

    ![Progreso de la instalación de App Service en Azure Stack][10]

23. Después de que el instalador de hello finalice correctamente, haga clic en **Exit**.

## <a name="validate-hello-app-service-on-azure-stack-installation"></a>Validar Hola servicio de aplicaciones en la instalación de la pila de Azure

1. En el portal de administración de la pila de Azure de hello, vaya toohello grupo de recursos creado por el instalador de Hola. De forma predeterminada, este grupo es **APPSERVICE-LOCAL**.

2. Busque **CN0-VM**. tooconnect toohello de máquina virtual, haga clic en **conectar** en hello **Máquina Virtual** hoja.

3. En el escritorio de Hola de esta máquina virtual, haga doble clic en **consola de administración de Web en la nube**.

4. Vaya demasiado**servidores administrados por**.

5. Cuando todos Hola máquinas mostrar **listo** para uno o varios trabajadores, continuar toostep 6.

6. Cierre la máquina de escritorio remoto de Hola y máquina toohello devuelto donde ejecutó Hola instalador del servicio de aplicación.

    > [!NOTE]
    > No es necesario toowait para uno o más toodisplay de trabajadores **listo** instalación de hello toocomplete de servicio de aplicaciones en la pila de Azure. Sin embargo, se necesita un mínimo de un trabajador que está listo toodeploy un sitio web, móvil, o aplicación de API o funciones de Azure.

    ![Estado de los servidores administrados de App Service en Azure Stack][11]

## <a name="configure-an-azure-ad-service-principal-for-virtual-machine-scale-set-integration-on-worker-tiers-and-sso-for-hello-azure-functions-portal-and-advanced-developer-tools"></a>Configurar una entidad de seguridad de servicio de Azure AD para la integración de conjunto de escala de máquinas virtuales en los niveles de trabajo y SSO para herramientas de desarrollo de portal y avanzados de hello las funciones de Azure

>[!NOTE]
> Estos pasos aplican tooAzure que AD protegidos solo entornos de pila de Azure.

Los administradores necesitan tooconfigure SSO para:

* Habilitar Hola avanzadas herramientas de desarrollo en el servicio de aplicaciones (Kudu).
* Habilitar el uso de Hola de experiencia del portal hello las funciones de Azure.

Siga estos pasos:

1. Abra una instancia de PowerShell como azurestack\azurestackadmin.

2. Vaya a toohello ubicación de las secuencias de comandos de hello descargado y extraído Hola [requisito previo](#Download-Required-Components).

3. [Instale](azure-stack-powershell-install.md) y [configure un entorno de PowerShell de Azure Stack](azure-stack-powershell-configure-admin.md).

4. Hola misma sesión de PowerShell, ejecute hello **CreateIdentityApp.ps1** secuencia de comandos. Cuando se le pide el identificador de inquilino de Azure AD, escriba el Id. de inquilino de Azure AD Hola que está usando para la implementación de la pila de Azure, por ejemplo, myazurestack.onmicrosoft.com.

5. Hola **credencial** ventana, escriba la cuenta de administrador del servicio de Azure AD y la contraseña. Haga clic en **Aceptar**.

6. Escriba Hola certificado ruta de acceso y el certificado de contraseña del archivo de hello [certificado creado anteriormente](# Create certificates toobe used by App Service on Azure Stack). certificado de Hello creada para este paso de forma predeterminada es sso.appservice.local.azurestack.external.pfx.

7. crea una nueva aplicación en Azure AD del inquilino de hello Hello secuencia de comandos y genera un nuevo script de PowerShell denominado **UpdateConfigOnController.ps1**.

    >[!NOTE]
    > Tome nota de hello **identificador de la aplicación** que se devuelve en la salida de PowerShell Hola. Necesita esta información toosearch para él en el paso 12.

8. Copiar archivo de certificado de aplicación de identidad de Hola y script de Hola genera demasiado**CN0-VM** mediante una sesión de escritorio remota.

9. Abra una nueva ventana del explorador e inicie sesión toohello portal de Azure (portal.azure.com) como hello **Administrador de servicio de Azure Active Directory**.

10. Abrir el proveedor de recursos de hello Azure AD.

11. Haga clic en **Registros de aplicaciones**.

12. Busque hello **Id. de aplicación** formando parte del paso 7. Se muestra una aplicación de App Service.

13. Haga clic en **aplicación** en lista de Hola y Hola abierto **claves** hoja.

14. Agregue una nueva clave con **descripción - funciones Portal**, conjunto hello y **fecha de expiración** demasiado**nunca caduca**.

15. Haga clic en **guardar**y, a continuación, copia Hola clave generada.

    >[!NOTE]
    > Ser seguro de clave de Hola de toonote o copia cuando se generan. Una vez guardada, no se pueden ver de nuevo, y deberá tooregenerate una nueva clave.

    ![Claves de aplicación de App Service en Azure Stack][12]

16. Devolver toohello **registro de la aplicación** en Azure AD.

17. Haga clic en **Permisos necesarios** > **Conceder permisos** > **Sí**.

    ![Concesión de SSO de App Service en Azure Stack][13]

18. Devolver demasiado**CN0-VM**, abra hello y **consola de administración de Web en la nube** una vez más.

19. Seleccione hello **configuración** nodo en el panel izquierdo de Hola y Hola, busque **ApplicationClientSecret** configuración.

20. Haga clic con el botón derecho y seleccione **Editar**. Pegue la clave de hello generada en el paso 15 y haga clic en **Aceptar**.

    ![Claves de aplicación de App Service en Azure Stack][14]

21. Abra una ventana de PowerShell como administrador. Busque el directorio toohello donde el archivo de script de Hola y el certificado se copiaron en el paso 7.

22. Ejecute el archivo de script de Hola. Este archivo de script entra en Propiedades de Hola Hola servicio de aplicaciones en la configuración de la pila de Azure e inicia una operación de reparación en todos los front-end y la administración de roles.

| Parámetro | Obligatorio/opcional | Valor predeterminado | Descripción |
| --- | --- | --- | --- |
| DirectoryTenantName | Obligatorio | Null | Identificador de inquilino de Azure AD. Proporcionar Hola GUID o una cadena, por ejemplo, myazureaaddirectory.onmicrosoft.com |
| TenantAzure Resource ManagerEndpoint | Obligatorio | management.local.azurestack.external | inquilino de Hello punto de conexión de administrador de recursos de Azure |
| AzureStackCredential | Obligatorio | Null | Administrador de Azure AD |
| CertificateFilePath | Obligatorio | Null | Archivo de certificado de aplicación en identidad de ruta de acceso toohello generado anteriormente |
| CertificatePassword | Obligatorio | Null | La contraseña usa la clave privada del certificado de hello tooprotect |
| DomainName | Obligatorio | local.azurestack.external | Región y sufijo de dominio de Azure Stack |
| AdfsMachineName | Opcional | Pasar por alto en caso de hello de implementación de Azure AD, pero es necesario en la implementación de AD FS. Nombre de la máquina de AD FS, por ejemplo, AzS-ADFS01.azurestack.local |

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

4. Hola misma sesión de PowerShell, ejecute hello **CreateIdentityApp.ps1** secuencia de comandos. Cuando se le pida el identificador de inquilino de Azure AD, escriba **ADFS**.

5. Hola **credencial** ventana, escriba la cuenta de administrador de servicio de AD FS y la contraseña. Haga clic en **Aceptar**.

6. Proporcionar Hola certificado ruta de acceso y el certificado de contraseña del archivo de hello [certificado creado anteriormente](# Create certificates toobe used by App Service on Azure Stack). certificado de Hello creada para este paso de forma predeterminada es sso.appservice.local.azurestack.external.pfx.

7. crea una nueva aplicación en Azure AD del inquilino de hello Hello secuencia de comandos y genera un nuevo script de PowerShell denominado **UpdateConfigOnController.ps1**.

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

## <a name="test-drive-app-service-on-azure-stack"></a>Prueba de App Service en Azure Stack

Después de implementar y registrar el proveedor de recursos de servicio de aplicaciones de hello, probarlo toomake seguro de que los inquilinos pueden implementar web, móviles y aplicaciones de API.

> [!NOTE]
> Debe toocreate una oferta con espacio de nombres de hello Microsoft.Web dentro de plan de Hola. A continuación, deberá toohave una suscripción de inquilino que se suscribe toothis oferta. Para más información, consulte [Create offer](azure-stack-create-offer.md) (Creación de una oferta) y [Create plan](azure-stack-create-plan.md) (Creación de un plan).
>
Se *debe* tiene un inquilino suscripción toocreate las aplicaciones que usan el servicio de aplicaciones en la pila de Azure. las capacidades solo de Hola que un administrador de servicios puede completarse dentro del portal de administración Hola están relacionados toohello administración del proveedor de recursos de servicio de aplicaciones. Entre estas funcionalidades se incluyen la adición de capacidad, la configuración de orígenes de implementación y la adición de niveles de trabajo y SKU.
>
A partir de hello tercera versión technical preview, toocreate web, móviles, API y Azure las funciones de aplicaciones, debe usar el portal del inquilino de Hola y disponer de una suscripción de inquilino. 

1. En el portal del inquilino de Azure pila de hello, haga clic en **New** > **Web y móvil** > **aplicación Web**.

2. En hello **aplicación Web** hoja, escriba un nombre en hello **aplicación Web** cuadro.

3. En **Grupo de recursos**, haga clic en **Nuevo**. Escriba un nombre en hello **grupo de recursos** cuadro.

4. Haga clic en **Plan de App Service/Ubicación** > **Create New** (Crear nuevo).

5. En hello **plan de servicio de aplicaciones** hoja, escriba un nombre en hello **plan de servicio de aplicaciones** cuadro.

6. Haga clic en **Plan de tarifa** > **Free-Shared** (Gratis - Compartido) o **Shared-Shared** (Compartido - Compartido) > **Seleccionar** > **Aceptar** > **Crear**.

7. En menos de un minuto, un icono de la aplicación web nueva de hello aparece en panel de Hola. Haga clic en el icono de Hola.

8. En hello **aplicación Web** hoja, haga clic en **examinar** sitio Web de tooview Hola predeterminado para esta aplicación.

## <a name="deploy-a-wordpress-dnn-or-django-website-optional"></a>Implementación de un sitio web de WordPress, DNN o Django (opcional)

1. En el portal del inquilino de Azure pila de hello, haga clic en  **+** , vaya toohello Azure Marketplace, implementar un sitio Web de Django y esperar la finalización correcta. plataforma de Hello Django web usa una base de datos de archivo basado en el sistema. No requiere ningún proveedor de recursos adicional, como SQL o MySQL.

2. Si también implementa un proveedor de recursos de MySQL, puede implementar un sitio Web de WordPress de hello Marketplace. Cuando se le pide para los parámetros de la base de datos, escriba el nombre de usuario de hello como  *User1@Server1* , con nombre de usuario de Hola y el nombre del servidor de su elección.

3. Si también implementa un proveedor de recursos de SQL Server, puede implementar un sitio Web DNN de hello Marketplace. Cuando se le pide para los parámetros de la base de datos, elija una base de datos en el equipo Hola que ejecuta SQL Server que es el proveedor de recursos de tooyour conectado.

## <a name="next-steps"></a>Pasos siguientes

También puede probar otros [servicios de Plataforma como servicio (PaaS)](azure-stack-tools-paas-services.md).

- [Proveedor de recursos de SQL Server](azure-stack-sql-resource-provider-deploy.md)
- [Proveedor de recursos de MySQL](azure-stack-mysql-resource-provider-deploy.md)

<!--Image references-->
[1]: ./media/azure-stack-app-service-deploy/app-service-exe-start.png
[2]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-cloud-configuration.png
[3]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-subscription-location-populated.png
[4]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-resource-group-sql.png
[5]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-certificates.png
[6]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-role-configuration.png
[7]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-vm-image-selection.png
[8]: ./media/azure-stack-app-service-deploy/app-service-exe-default-entries-step-role-credentials.png
[9]: ./media/azure-stack-app-service-deploy/app-service-exe-selection-summary.png
[10]: ./media/azure-stack-app-service-deploy/app-service-exe-installation-progress.png
[11]: ./media/azure-stack-app-service-deploy/managed-servers.png
[12]: ./media/azure-stack-app-service-deploy/app-service-sso-keys.png
[13]: ./media/azure-stack-app-service-deploy/app-service-sso-grant.png
[14]: ./media/azure-stack-app-service-deploy/app-service-application-secret.png

<!--Links-->
[Azure_Stack_App_Service_preview_installer]: http://go.microsoft.com/fwlink/?LinkID=717531
[App_Service_Deployment]: http://go.microsoft.com/fwlink/?LinkId=723982
[AppServiceHelperScripts]: http://go.microsoft.com/fwlink/?LinkId=733525
