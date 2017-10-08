---
title: aaaAzure SDK para .NET 2.9 notas
description: "Notas de la versión de SDK de Azure para .NET 2.9"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 96df2b80224190cc2093e6bf350eaec224ac2e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a>Notas de la versión de SDK de Azure para .NET 2.9

Este tema incluye notas de la versión para las versiones 2.9 y 2.9.6 del SDK de Azure para. NET.

##<a name="azure-sdk-for-net-296-release-summary"></a>Resumen de la versión de SDK de Azure para .NET 2.9.6.

Fecha de lanzamiento: 16/11/2016
 
No hay toohello de cambios de separación de Azure SDK 2.9 se han introducido en esta versión. No hay también ninguna tooleverage del proceso de actualización necesitado este SDK con proyectos de servicio en la nube existentes.

### <a name="visual-studio-2017-release-candidate"></a>Versión candidata para lanzamiento de Visual Studio 2017

- En Visual Studio de 2017 RC, esta versión de hello Azure SDK para .NET se basa Hola cargas de trabajo de Azure. Todas las herramientas de hello necesita toodo desarrollo de Azure va a formar parte de Visual Studio de 2017 RC en el futuro. Para Visual Studio 2015 y Visual Studio 2013, Hola SDK estará disponible a través de WebPI. Cuando la versión de Visual Studio 2017 sea definitiva, se interrumpirán las versiones del SDK de Azure para .NET para Visual Studio 2013l. Siga este toodownload vínculo Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/

### <a name="azure-diagnostics"></a>Diagnóstico de Azure

- Hola modificada comportamiento tooonly almacenar una cadena de conexión parcial con clave de hello reemplazado por un token de cadena de conexión de almacenamiento de información de diagnóstico de servicios en la nube. clave de almacenamiento real de Hola ahora se almacena en la carpeta de perfil de usuario de hello, por lo que se puede controlar el acceso. Visual Studio leerá clave de almacenamiento de Hola de carpeta de perfil de usuario para la depuración local y el proceso de publicación. 
- En cambio toohello de respuesta se ha descrito anteriormente, Visual Studio Online team Hola mejorada plantilla de tarea de implementación de servicios de nube de Azure para que los usuarios especificar clave de almacenamiento de Hola para establecer la extensión de diagnóstico al publicar tooAzure de integración continua y la implementación.
- Que hemos hecho posible toostore cadena de conexión segura y tokenización para diagnósticos de Azure (WAD), toohelp solucionar problemas con la configuración entre entornos.
 
### <a name="windows-server-2016-virtual-machines"></a>Máquinas virtuales Windows Server 2016

- Visual Studio ahora admite la implementación de servicios en la nube de tooOS máquinas virtuales de familia 5 (Windows Server 2016). Para los servicios de nube existente, puede cambiar su configuración tootarget Hola nueva familia del SO. Al crear nuevos servicios de nube, si decide que el servicio de hello toocreate mediante .net 4.6 o posterior, serán Hola servicio toouse 5 de la familia de SO.  Para obtener más información, puede revisar hello [familia del SO invitado compatible con la tabla](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).

#### <a name="known-issues"></a>Problemas conocidos

- Azure SDK para .NET 2.9.6 introdujo una restricción que bloquea la implementación de proyectos mediante tooany de marcos de trabajo (por ejemplo, .NET 4.6) .NET familia del SO no compatible < 5. Se proporciona una solución alternativa [aquí](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).

 
### <a name="azure-in-role-cache"></a>Caché en rol de Azure 

- La compatibilidad con Azure In-Role Cache finaliza el 30 de noviembre de 2016. Para más detalles, haga clic [aquí](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).

### <a name="azure-resource-manager-templates-for-azure-stack"></a>Plantillas de Azure Resource Manager para Azure Stack

- Hemos introducido Azure Stack como un destino de implementación para las plantillas de Azure Resource Manager.


## <a name="azure-sdk-for-net-29-summary"></a>Resumen del SDK de Azure para .NET 2.9

## <a name="overview"></a>Información general
Este documento contiene notas de la versión de Hola para hello Azure SDK para la versión 2.9. NET. 

Para obtener información detallada acerca de las actualizaciones en esta versión, vea hello [post de anuncio de Azure SDK 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a>SDK de Azure 2.9 para Visual Studio 2015 Update 2 y vista previa de Visual Studio "15"
Esta actualización incluye Hola después de correcciones de errores:

* Emitir relacionado tooREST generación de API de cliente en la cadena de Hola "Tipo desconocido" aparecería como nombre de Hola de carpeta de generación de código de hello u Hola del espacio de nombres de hello colocado en el código de hello generado.
* Emitir WebJobs tooScheduled relacionados en qué Hola información de autenticación producía un error toobe pasado el proceso de aprovisionamiento de toohello programador.

Esta actualización incluye Hola siguiendo la nueva característica:

* Compatibilidad con los servicios de aplicación secundarios en la ficha de "Servicios" hello de hello diálogo de aprovisionamiento del servicio de aplicaciones. 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a>Azure Data Lake Tools para Visual Studio 2015 Update 2
Esta actualización incluye siguiente de hello:

* **Azure Data Lake Tools** para Visual Studio ahora se combinan en hello Azure SDK para la versión de .NET. herramienta de Hola se instala automáticamente al instalar el SDK de Azure. 
  
    herramienta de Hola se actualiza con frecuencia, vaya [aquí](http://aka.ms/datalaketool) tooget Hola actualizaciones.
* **Explorador de servidores** ahora permite tooview todos y crear algunas entidades de metadatos de U-SQL. Para más información, consulte [este blog](https://azure.microsoft.com/documentation/services/data-lake-analytics/) .

## <a name="hdinsight-tools"></a>Herramientas de HDInsight
**Herramientas de HDInsight** para Visual Studio ahora admite HDInsight versión 3.3, incluida la visualización de gráficos Tez y otras correcciones de lenguaje.

## <a name="azure-resource-manager"></a>Azure Resource Manager
Esta versión agrega compatibilidad de [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) con plantillas de Resource Manager.

## <a name="see-also"></a>Otras referencias
[Announcing the Visual Studio Azure Tools and SDK 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

