---
title: "aaaHow tooconfigure un servicio de nube (portal clásico) | Documentos de Microsoft"
description: "Obtenga información acerca de cómo servicios en la nube tooconfigure en Azure. Obtenga información acerca de la configuración del servicio de nube de tooupdate hello y configurar instancias de toorole de acceso remoto."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4902f79d-ea91-41ca-89a4-7c818180ee5f
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: adegeo
ms.openlocfilehash: 1ea2320f97f667153f7984e4d61d373a6344cf6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-cloud-services"></a>Cómo tooConfigure los servicios de nube
> [!div class="op_single_selector"]
> * [Portal de Azure](cloud-services-how-to-configure-portal.md)
> * [Portal de Azure clásico](cloud-services-how-to-configure.md)
> 
> 

Puede configurar valores de hello suelen usada para un servicio de nube en hello portal de Azure clásico. O bien, si le gusta tooupdate los archivos de configuración directamente, descargar una tooupdate de archivo de configuración de servicio y, a continuación, cargar Hola Actualizar archivo y actualización Hola servicio en la nube con los cambios de configuración de Hola. En cualquier caso, se insertan las actualizaciones de configuración de hello tooall instancias de rol.

Hello portal de Azure clásico también le permite demasiado[Habilitar conexión a Escritorio remoto para un rol de servicios de nube de Azure](cloud-services-role-enable-remote-desktop.md)

Azure solo puede asegurar de disponibilidad de servicio del 99,95 por ciento durante hello las actualizaciones de configuración si tiene al menos dos instancias de rol para cada rol. Que permite las solicitudes de cliente de tooprocess de máquina virtual mientras se está actualizando Hola otro. Para obtener más información, consulte [Contratos de nivel de servicio](https://azure.microsoft.com/support/legal/sla/).

## <a name="change-a-cloud-service"></a>Cambiar un servicio en la nube
1. Hola [portal de Azure clásico](http://manage.windowsazure.com/), haga clic en **servicios en la nube**, haga clic en nombre de hello del servicio de nube de hello y, a continuación, haga clic en **configurar**.
   
    ![Página de configuración](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage1.png)
   
    En hello **configurar** página, puede configurar la supervisión, configuración de roles de actualización y elija Hola sistema operativo y la familia de instancias de rol. 
2. En **supervisión**, Hola conjunto tooVerbose nivel de supervisión o mínima y configurar cadenas de conexión de diagnósticos de Hola que son necesarias para la supervisión detallada.
3. Para los roles de servicio (agrupados por rol), puede actualizar Hola después de configuración:
   
    * **Configuración de** modificar valores de hello varias opciones de configuración se especifican en hello *ConfigurationSettings* elementos Hola servicio (.cscfg) del archivo de configuración.

    * **Certificados**  
        Cambio Hola huella digital del certificado que se utiliza en el cifrado SSL para un rol. toochange un certificado, debe cargar primero un nuevo certificado hello (en hello **certificados** página). A continuación, actualice huella digital de hello en hello certificado cadena que se muestra en la configuración de rol de Hola.
4. En **sistema operativo**, puede cambiar la familia de sistemas operativos de Hola o una versión de instancias de rol, o elegir **automática** tooenable actualizaciones automáticas de versión del sistema operativo actual Hola. configuración del sistema operativo Hola aplica tooweb roles y roles de trabajo, pero no afectan a las máquinas virtuales.
   
    Durante la implementación, se instala la versión de sistema operativo más reciente de Hola en todas las instancias de rol y sistemas operativos de Hola se actualizan automáticamente de forma predeterminada. 
   
    Si necesita para su toorun de servicio de nube en una versión de sistema operativo diferente debido a los requisitos de compatibilidad en el código, puede elegir una familia del sistema operativo y versión. Cuando se elige una versión de sistema operativo específico, se suspenden las actualizaciones automáticas del sistema operativo para servicio de nube de Hola. Necesitará tooensure sistemas operativos de Hola recibir actualizaciones.
   
    Si resuelve todos los problemas de compatibilidad con las aplicaciones con la versión de sistema operativo más reciente de hello, puede habilitar las actualizaciones automáticas del sistema operativo por versión del sistema operativo Hola establecer demasiado**automática**. 
   
    ![Configuración del SO](./media/cloud-services-how-to-configure/CloudServices_ConfigurePage_OSSettings.png)
5. toosave las opciones de configuración e insertarlas toohello instancias de rol, haga clic en **guardar**. (Haga clic en **descartar** cambios de hello toocancel.) **Guardar** y **descartar** se agregan toohello barra de comandos después de cambiar una configuración.

## <a name="update-a-cloud-service-configuration-file"></a>Actualizar un archivo de configuración del servicio en la nube
1. Descargar un archivo de configuración del servicio de nube (.cscfg) con la configuración actual de Hola. En hello **configurar** página de servicio en la nube hello, haga clic en **descargar**. A continuación, haga clic en **guardar**, o haga clic en **Guardar como** archivo de hello toosave.
2. Después de actualizar el archivo de configuración de servicio de hello, cargar y aplicar las actualizaciones de configuración de hello:
   
   1. En hello **configurar** página, haga clic en **cargar**.
      
       ![Cargar configuración](./media/cloud-services-how-to-configure/CloudServices_UploadConfigFile.png)
   2. En **archivo de configuración**, use **examinar** tooselect Hola actualiza el archivo .cscfg.
   3. Si su servicio en la nube contiene los roles que tienen una única instancia, seleccione hello **aplicar configuración aunque uno o varios roles contengan una sola instancia** actualizaciones de configuración de casilla de verificación tooenable Hola para hello roles tooproceed.
      
       A menos que defina como mínimo dos instancias de cada rol, Azure no puede garantizar una disponibilidad de su servicio en la nube de al menos un 99,95 % durante las actualizaciones de la configuración del servicio. Para obtener más información, consulte [Contratos de nivel de servicio](https://azure.microsoft.com/support/legal/sla/).
   4. Haga clic en **Aceptar** (marca de verificación). 

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de cómo demasiado[implementar un servicio de nube](cloud-services-how-to-create-deploy.md).
* Configuración de un [nombre de dominio personalizado](cloud-services-custom-domain-name.md).
* [Administración de su servicio en la nube](cloud-services-how-to-manage.md).
* [Habilitar la conexión a Escritorio remoto para un rol de servicios en la nube de Azure](cloud-services-role-enable-remote-desktop.md)
* Configuración de [certificados ssl](cloud-services-configure-ssl-certificate.md).

