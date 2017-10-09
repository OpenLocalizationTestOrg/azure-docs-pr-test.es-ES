---
title: aaaHow toocreate e implementar un servicio de nube | Documentos de Microsoft
description: "Obtenga información acerca de cómo toocreate e implementar un servicio de nube mediante Hola portal de Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 56ea2f14-34a2-4ed9-857c-82be4c9d0579
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: dc8b81a594f3514e662c49c9a46a33da8a551f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-deploy-a-cloud-service"></a>¿Cómo toocreate e implementar un servicio de nube
> [!div class="op_single_selector"]
> * [Portal de Azure](cloud-services-how-to-create-deploy-portal.md)
> * [Portal de Azure clásico](cloud-services-how-to-create-deploy.md)
>
>

proporciona dos maneras de toocreate Hello portal de Azure e implementar un servicio de nube: *creación rápida* y *creación personalizada*.

Este artículo explica cómo toouse Hola toocreate de método de creación rápida un nuevo servicio de nube y, a continuación, usar **cargar** tooupload e implementar un paquete de servicios de nube en Azure. Cuando utiliza este método, Hola portal de Azure hace disponible vínculos adecuados para completar todos los requisitos a medida que avanza. Si está listo toodeploy la nube de servicio al crearlo, puede realizar tanto operaciones en hello simultánea mediante Creación personalizada.

> [!NOTE]
> Si tiene previsto toopublish su servicio de nube desde Visual Studio Team Services (VSTS), use creación rápida y, a continuación, configure la publicación de VSTS desde panel de inicio rápido de Azure u Hola Hola. Para obtener más información, consulte [tooAzure la entrega continua mediante el uso de Visual Studio Team Services][TFSTutorialForCloudService], o consulte la ayuda para hello **inicio rápido** página.
>
>

## <a name="concepts"></a>Conceptos
Tres componentes son necesario toodeploy una aplicación como un servicio de nube en Azure:

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

* Si desea que un servicio de nube que utiliza Secure Sockets Layer (SSL) para el cifrado de datos, toodeploy [configurar la aplicación](cloud-services-configure-ssl-certificate-portal.md#modify) para SSL.
* Si desea que las instancias de toorole de conexiones de escritorio remoto tooconfigure, [configurar roles de hello](cloud-services-role-enable-remote-desktop-new-portal.md) para escritorio remoto.
* Si desea tooconfigure detallado de supervisión para el servicio de nube, habilitar los diagnósticos de Azure para servicio de nube de Hola. *La supervisión mínima* (nivel de supervisión de predeterminado hello) usa contadores de rendimiento recopilados de los sistemas de operativos de host de Hola para instancias de rol (máquinas virtuales). *Supervisión detallada* recopila métricas adicionales basadas en datos de rendimiento de hello rol instancias tooenable un análisis más preciso de los problemas que se producen durante el procesamiento de la aplicación. toofind más información sobre cómo tooenable diagnósticos de Azure, consulte [habilitar diagnósticos en Azure](cloud-services-dotnet-diagnostics.md).

toocreate un servicio en la nube con implementaciones de roles web o roles de trabajo, debe [crear paquete de servicios de hello](cloud-services-model-and-package.md#servicepackagecspkg).

## <a name="before-you-begin"></a>Antes de empezar
* Si no tiene instalado hello Azure SDK, haga clic en **instalar Azure SDK** tooopen hello [página de descargas de Azure](https://azure.microsoft.com/downloads/)y, a continuación, descargar Hola SDK para el idioma de hello en el que prefiera toodevelop el código. (Tendrá una oportunidad toodo esto más adelante.)
* Si las instancias de rol requieren un certificado, crear certificados de Hola. Los servicios en la nube requieren un archivo .pfx con una clave privada. Puede cargar Hola certificados tooAzure como crear e implementar el servicio en la nube Hola.

## <a name="create-and-deploy"></a>Creación e implementación
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Haga clic en **nuevo > proceso**y, a continuación, desplácese hacia abajo de tooand haga clic en **servicio de nube**.

    ![Publicación del servicio en la nube](media/cloud-services-how-to-create-deploy-portal/create-cloud-service.png)
3. Hola nueva **servicio de nube** hoja, escriba un valor para hello **nombre DNS**.
4. Cree un nuevo **Grupo de recursos** o seleccione uno existente.
5. Seleccione una **ubicación**.
6. Haga clic en **Paquete**. Se abrirá hello **cargar un paquete** hoja. Rellene los campos de hello necesario. Si cualquiera de los roles contiene una sola instancia, asegúrese de que la casilla **Implementar aunque uno o varios roles contengan una sola instancia** esté seleccionada.
7. Asegúrese de que la opción **Iniciar implementación** esté seleccionada.
8. Haga clic en **Aceptar** que va a cerrar hello **cargar un paquete** hoja.
9. Si no tiene ningún tooadd de certificados, haga clic en **crear**.

    ![Publicación del servicio en la nube](media/cloud-services-how-to-create-deploy-portal/select-package.png)

## <a name="upload-a-certificate"></a>Carga de un certificado
Si el paquete de implementación se ha [configurado toouse certificados](cloud-services-configure-ssl-certificate-portal.md#modify), puede cargar el certificado de hello ahora.

1. Seleccione **certificados**y en hello **agregar certificados** hoja, seleccione archivo de PFX de certificado SSL de hello y, a continuación, proporcionar hello **contraseña** certificado hello,
2. Haga clic en **adjuntar certificado**y, a continuación, haga clic en **Aceptar** en hello **agregar certificados** hoja.
3. Haga clic en **crear** en hello **servicio de nube** hoja. Cuando alcanza implementación Hola Hola **listo** estado, puede continuar toohello pasos.

    ![Publicación del servicio en la nube](media/cloud-services-how-to-create-deploy-portal/attach-cert.png)

## <a name="verify-your-deployment-completed-successfully"></a>Compruebe que la implementación se haya completado correctamente.
1. Haga clic en la instancia de servicio de nube de Hola.

    Hello estado debe mostrar que el servicio de hello es **ejecutando**.
2. En **Essentials**, haga clic en hello **dirección URL del sitio** tooopen la nube de servicio en un explorador web.

    ![CloudServices_QuickGlance](./media/cloud-services-how-to-create-deploy-portal/running.png)

[TFSTutorialForCloudService]: http://go.microsoft.com/fwlink/?LinkID=251796

## <a name="next-steps"></a>Pasos siguientes
* [Configuración general de su servicio en la nube](cloud-services-how-to-configure-portal.md).
* Configuración de un [nombre de dominio personalizado](cloud-services-custom-domain-name-portal.md).
* [Administración de su servicio en la nube](cloud-services-how-to-manage-portal.md).
* Configuración de [certificados ssl](cloud-services-configure-ssl-certificate-portal.md).
