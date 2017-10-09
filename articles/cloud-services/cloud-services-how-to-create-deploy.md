---
title: aaaHow toocreate e implementar un servicio de nube | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate e implementar un servicio de nube mediante el método de creación rápida de hello en Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 0ea78ccc-5e7d-40f8-bdb6-478c0eb0e265
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 09f889f81ccee6e8a7657116183aa4100410214c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a>¿Cómo tooCreate e implementar un servicio de nube
> [!div class="op_single_selector"]
> * [Portal de Azure](cloud-services-how-to-create-deploy-portal.md)
> * [Portal de Azure clásico](cloud-services-how-to-create-deploy.md)
> 
> 

proporciona dos maneras de toocreate Hello portal de Azure clásico e implementar un servicio de nube: **creación rápida** y **creación personalizada**.

Este tema explica cómo toouse Hola toocreate de método de creación rápida un nuevo servicio de nube y, a continuación, usar **cargar** tooupload e implementar un paquete de servicios de nube en Azure. Cuando utiliza este método, Hola portal de Azure clásico hace disponible vínculos adecuados para completar todos los requisitos a medida que avanza. Si está listo toodeploy la nube de servicio al crearlo, puede realizar tanto operaciones en hello mismo tiempo, use **creación personalizada**.

> [!NOTE]
> Si tiene previsto toopublish su servicio de nube desde Visual Studio Team Services (VSTS), use **creación rápida**y, a continuación, configure la publicación de VSTS desde **inicio rápido** o un panel de Hola.
> 
> 

## <a name="concepts"></a>Conceptos
Se necesitan tres componentes en toodeploy orden una aplicación como una nube de servicio en Azure:

* **Definición de servicio**  
  archivo de definición de servicio de nube de Hello (.csdef) define el modelo de servicio de hello, incluido el número de Hola de roles.
* **Configuración de servicio**  
  archivo de configuración de servicio (.cscfg) de Hello en la nube proporciona opciones de configuración de servicio en la nube hello y roles individuales, incluido el número de Hola de instancias de rol.
* **Paquete de servicio**  
  paquete de servicio de Hello (.cspkg) contiene el código de la aplicación hello y las configuraciones y archivo de definición de servicio de Hola.

Encontrará más información acerca de éstas y cómo toocreate un paquete [aquí](cloud-services-model-and-package.md).

## <a name="prepare-your-app"></a>Preparación de la aplicación
Antes de poder implementar un servicio de nube, debe crear el paquete de servicio de nube de hello (.cspkg) desde el código de aplicación y un archivo de configuración de servicio de nube (.cscfg). Hello Azure SDK proporciona herramientas para preparar estos archivos de implementación necesarios. Puede instalar Hola SDK de hello [descargas de Azure](https://azure.microsoft.com/downloads/) página en lenguaje de hello en el que prefiera toodevelop el código de aplicación.

Hay tres características del servicio en la nube que requieren configuraciones especiales antes de exportar un paquete de servicio:

* Si desea que un servicio de nube que utiliza Secure Sockets Layer (SSL) para el cifrado de datos, toodeploy [configurar la aplicación](cloud-services-configure-ssl-certificate.md#step-2-modify-the-service-definition-and-configuration-files) para SSL.
* Si desea que las instancias de toorole de conexiones de escritorio remoto tooconfigure, [configurar roles de hello](cloud-services-role-enable-remote-desktop.md) para escritorio remoto.
* Si desea tooconfigure detallado de supervisión para el servicio de nube, habilitar los diagnósticos de Azure para servicio de nube de Hola. *La supervisión mínima* (nivel de supervisión de predeterminado hello) usa contadores de rendimiento recopilados de los sistemas de operativos de host de Hola para instancias de rol (máquinas virtuales). "Supervisión detallada * recopila métricas adicionales basadas en datos de rendimiento de hello rol instancias tooenable un análisis más preciso de los problemas que se producen durante el procesamiento de la aplicación. toofind más información sobre cómo tooenable diagnósticos de Azure, consulte [habilitar diagnósticos en Azure](cloud-services-dotnet-diagnostics.md).

toocreate un servicio en la nube con implementaciones de roles web o roles de trabajo, debe [crear paquete de servicios de hello](cloud-services-model-and-package.md#servicepackagecspkg).

## <a name="before-you-begin"></a>Antes de empezar
* Si no tiene instalado hello Azure SDK, haga clic en **instalar Azure SDK** tooopen hello [página de descargas de Azure](https://azure.microsoft.com/downloads/)y, a continuación, descargar Hola SDK para el idioma de hello en el que prefiera toodevelop el código. (Tendrá una oportunidad toodo esto más adelante.)
* Si las instancias de rol requieren un certificado, crear certificados de Hola. Los servicios en la nube requieren un archivo .pfx con una clave privada. También puede [cargar Hola certificados tooAzure](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) como crear e implementar el servicio en la nube Hola.
* Si piensa que el grupo de afinidad de tooan de servicio de toodeploy hello en la nube, crear grupo de afinidad de Hola. Puede usar un grupo de afinidad toodeploy su servicio de nube y otro servicios de Azure toohello misma ubicación en una región. Puede crear el grupo de afinidad de Hola Hola **redes** área no cliente de portal de Azure clásico en Hola Hola **grupos de afinidad** página.

## <a name="how-to-create-a-cloud-service-using-quick-create"></a>Creación de un servicio en la nube usando Creación rápida
1. Hola [portal de Azure clásico](http://manage.windowsazure.com/), haga clic en **New**>**proceso**>**servicio de nube** > **Creación rápida**.
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_QuickCreate.png)
2. En **dirección URL**, escriba un toouse de nombre de subdominio en dirección URL pública de Hola para acceder a su servicio de nube en las implementaciones de producción. formato de dirección URL de Hola para las implementaciones de producción es: http://*myURL*. cloudapp.net.
3. En **región o grupo de afinidad**, seleccione Hola geográfica región o grupo de afinidad toodeploy hello en la nube de servicio a. Seleccione un grupo de afinidad si desea toodeploy su toohello de servicio de nube misma ubicación que otros servicios de Azure dentro de una región.
4. Haga clic en **Crear servicio en la nube**.
   
    ![CloudServices_Region](./media/cloud-services-how-to-create-deploy/CloudServices_Regionlist.png)
   
    Puede supervisar estado de saludo del proceso de hello en el área de mensajes de Hola final Hola de ventana hello.
   
    Hola **servicios en la nube** abre el área, con el nuevo servicio de nube hello muestra. Cuando cambia el estado de hello tooCreated, creación de servicios de nube se completó correctamente.
   
    ![CloudServices_CloudServicesPage](./media/cloud-services-how-to-create-deploy/CloudServices_CloudServicesPage.png)

## <a name="how-to-upload-a-certificate-for-a-cloud-service"></a>Carga de un certificado para un servicio en la nube
1. Hola [portal de Azure clásico](http://manage.windowsazure.com/), haga clic en **servicios en la nube**, haga clic en nombre de hello del servicio de nube de hello y, a continuación, haga clic en **certificados**.
   
    ![CloudServices_QuickCreate](./media/cloud-services-how-to-create-deploy/CloudServices_EmptyDashboard.png)
2. Haga clic en **Cargar un certificado** o en **Cargar**.
3. En **archivo**, use **examinar** certificado de hello tooselect (archivo .pfx).
4. En **contraseña**, escriba la clave privada de Hola de certificado de Hola.
5. Haga clic en **Aceptar** (marca de verificación).
   
    ![CloudServices_AddaCertificate](./media/cloud-services-how-to-create-deploy/CloudServices_AddaCertificate.png)
   
    Puede ver el progreso de Hola de carga de hello en el área de mensajes de Hola, que se muestra a continuación. Cuando se completa la carga de hello, certificado Hola se agrega toohello tabla. En el área de mensajes de Hola, haga clic en Aceptar tooclose mensaje de saludo.
   
    ![CloudServices_CertificateProgress](./media/cloud-services-how-to-create-deploy/CloudServices_CertificateProgress.png)

## <a name="how-to-deploy-a-cloud-service"></a>Implementación de un servicio en la nube
1. Hola [portal de Azure clásico](http://manage.windowsazure.com/), haga clic en **servicios en la nube**, haga clic en nombre de hello del servicio de nube de hello y, a continuación, haga clic en **panel**.
2. Haga clic en **Cargar una nueva implementación de producción** o **Cargar**.
3. En **etiqueta de implementación**, escriba un nombre para la nueva implementación hello: por ejemplo, MyCloudServicev4.
4. En **paquete**, use **examinar** tooselect Hola servicio paquete (.cspkg) del archivo toouse.
5. En **configuración**, use **examinar** servicio de hello tooselect configurar toouse de archivo (.cscfg).
6. Si servicio de nube de hello incluirá los roles con una única instancia, seleccione hello **implementar aunque uno o varios roles contengan una sola instancia** tooproceed de implementación de casilla de verificación tooenable Hola.
   
    Azure solo puede garantizar servicio en la nube 99,95 por ciento acceso toohello durante las actualizaciones de mantenimiento y el servicio si cada rol tiene al menos dos instancias. Si es necesario, puede agregar instancias de rol adicionales en hello **escala** página después de implementar el servicio en la nube Hola. Para obtener más información, consulte [Contratos de nivel de servicio](https://azure.microsoft.com/support/legal/sla/).
7. Haga clic en **Aceptar** implementación del servicio de nube de (marca de verificación) toobegin Hola.
   
    ![CloudServices_UploadaPackage](./media/cloud-services-how-to-create-deploy/CloudServices_UploadaPackage.png)
   
    Puede supervisar el estado de Hola de implementación de hello en el área de mensajes de Hola. Haga clic en Aceptar toohide mensaje de saludo.
   
    ![CloudServices_UploadProgress](./media/cloud-services-how-to-create-deploy/CloudServices_UploadProgress.png)

## <a name="verify-your-deployment-completed-successfully"></a>Compruebe que la implementación se haya completado correctamente.
1. Haga clic en **Panel**.
   
    Hello estado debe mostrar que el servicio de hello es **ejecutando**.
2. En **vista rápida**, haga clic en tooopen de dirección URL del sitio de hello su servicio en la nube en un explorador web.
   
    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy/CloudServices_QuickGlance.png)


## <a name="next-steps"></a>Pasos siguientes
* [Configuración general de su servicio en la nube](cloud-services-how-to-configure.md).
* Configuración de un [nombre de dominio personalizado](cloud-services-custom-domain-name.md).
* [Administración de su servicio en la nube](cloud-services-how-to-manage.md).
* Configuración de [certificados ssl](cloud-services-configure-ssl-certificate.md).

