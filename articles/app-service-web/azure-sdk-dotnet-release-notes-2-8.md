---
title: aaaAzure SDK para .NET 2.8 notas
description: "Notas de la versión de SDK de Azure para .NET 2.8."
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: de7207ff-ba4f-4008-9141-8742fcaa3254
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 2722dcdd27bf9ab65b48e91dcdb545536f987dd8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-28-281-and-282"></a>Azure SDK para .NET 2.8, 2.8.1 y 2.8.2
## <a name="overview"></a>Información general
Este artículo contiene las notas de la versión de hello (que incluye los problemas conocidos y los cambios recientes) para hello Azure SDK para .NET 2.8, 2.8.1 y 2.8.2 libera. 

Para una lista completa de nuevas características y las actualizaciones realizadas en esta versión, vea hello [2.8 de SDK de Azure para Visual Studio 2013 y Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/) anuncio. 

## <a name="azure-sdk-for-net-28"></a>SDK de Azure para .NET 2.8
### <a name="download-azure-sdk-for-net-28"></a>Descarga del SDK de Azure para .NET 2.8
[SDK de Azure para .NET 2.8 para Visual Studio 2015](http://go.microsoft.com/fwlink/?LinkId=699285) 

[SDK de Azure para .NET 2.8 para Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkId=699287)

### <a name="net-452-support"></a>Compatibilidad con .NET 4.5.2
#### <a name="known-issues"></a>Problemas conocidos
Azure 2.8 del SDK de .NET permite toocreate .NET 4.5.2 paquetes de servicios de nube. Sin embargo 4.5.2 de .NET framework no se instalará en predeterminado Hola imágenes de SO invitado hasta que el SO invitado de enero de 2016 de la versión. Antes de eso, .NET Framework 4.5.2 estará disponible mediante una versión de sistema operativo invitado distinta (2 de noviembre de 2015). Vea hello [versiones del SO invitado de Azure y la matriz de compatibilidad de SDK](../cloud-services/cloud-services-guestos-update-matrix.md) tootrack de página cuando se lanzarán imagen Hola.  Una vez que se libera la imagen de hello noviembre de 2015-02 puede elegir esa imagen toouse actualizando el archivo de configuración de servicio en la nube (.cscfg). En configuración del servicio Hola archivo establece el atributo de osVersion de Hola de cadena de hello ServiceConfiguration elemento toohello "WA-GUEST-OS-4.26_201511-02". Si elige tooopt en toouse esta imagen entonces ya no recibirá actualizaciones automáticas toohello SO invitado. se debe establecer tooget Hola actualizaciones automáticas Hola osVersion demasiado "*" y .NET 4.5.2 solo estarán disponibles a través de actualizaciones automáticas en enero de 2016.

### <a name="azure-data-factory"></a>Azure Data Factory
#### <a name="known-issues"></a>Problemas conocidos
Durante una **plantilla de la factoría de datos** proyecto creación que implican datos de ejemplo que puede producir un error en la secuencia de comandos de azure power shell si versión de azure power shell instalada en el equipo de hello es posterior a 0.9.8.

En orden toosuccessfully crear este tipo de proyecto, debe instalar [versión de azure power shell 0.9.8](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi).

### <a name="azure-resource-manager-tools"></a>Herramientas del Administrador de recursos de Azure
#### <a name="breaking-changes"></a>Cambios drásticos
script de PowerShell proporcionada por el proyecto del grupo de recursos de Azure de Hola Hola se ha actualizado en esta toowork versión con hello nuevos cmdlets de PowerShell de Azure versión 1.0.  Esta nueva secuencia de comandos no funcionará desde con Visual Studio cuando se usa una versión de Hola SDK anteriores too2.8.  

Scripts de proyectos creados en versiones anteriores de hello SDK no se ejecutan desde dentro de Visual Studio cuando utilizando Hola 2,8 SDK.  Todos los scripts seguirán toowork fuera de Visual Studio con la versión adecuada de Hola de hello cmdlets de PowerShell de Azure.  

Hello SDK 2,8 requiere la versión 1.0 de hello cmdlets de PowerShell de Azure.  Todas las demás versiones de hello SDK requieren la versión 0.9.8 de hello cmdlets de PowerShell de Azure.  Para más información, vea [este blog](http://go.microsoft.com/fwlink/?LinkID=623011) .

### <a name="web-tools-extensions"></a>Extensiones de herramientas web
#### <a name="known-issues"></a>Problemas conocidos
Hola problemas conocidos siguientes se solucionarán en hello después de la versión.

* El gesto del Explorador de servidores y la nube relacionado con el Servicio de aplicaciones en los entornos que no son de producción (como clientes de Azure China y Azure Stack) no funcionará. Para publicación los clientes en estas áreas afectadas, descargar Hola perfil de hello portal de Azure habilitará capacidad de publicación. Una versión futura reparará gestos como "Adjuntar depurador" y "Ver registros de streaming" para los clientes de Azure China y Azure Stack. 
* Los clientes pueden producirse errores durante la creación cuando visión de aplicación Hola toowhich que va a implementar la instancia está en una región que no sea este de EE. el servicio de aplicaciones. En estos casos, crear un servicio de aplicaciones en portal de Hola y descargar Hola perfil de publicación permitirá escenarios de publicación. 

### <a name="azure-hdinsight-tools"></a>Herramientas de HDInsight de Azure
#### <a name="new-updates"></a>Nuevas actualizaciones
* Puede ejecutar la consulta de Hive en clúster de Hola a través de HiveServer2 con casi ninguna sobrecarga y ver registros de trabajo de hello en tiempo real.
* Con hello nueva Hive tareas vista de ejecución ya puede adentrarse en el trabajo más profundo, obtener más información e identificar posibles problemas.

Para obtener información, vea [SDK 2.8 de Azure para Visual Studio 2013 y Visual Studio 2015](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/). 

## <a name="azure-sdk-for-net-281"></a>SDK de Azure para .NET 2.8.1
### <a name="known-issues-for-visual-studio-2013-and-visual-studio-2015"></a>Problemas conocidos de Visual Studio 2013 y Visual Studio 2015
1. Trabajo Web desencadenada publica will tooslots mostrar y error y no conjunto una programación, pero se insertará hello tooAzure de trabajo Web. Los clientes que necesitan un trabajo programado, a continuación, pueden usar hello Azure Portal tooset la programación de Hola para hello trabajo Web. 
2. Los clientes de Python pueden experimentar problemas con el depurador. Equipo de servicio está efectuando una corrección de este, pero si los clientes están afectados, le agradeceré Microsoft conoce en los foros de Hola o en el blog del anuncio de Hola o sección de comentarios de notas de la versión. 
3. Los clientes de determinadas regiones (por ejemplo, el sur de la India) experimentarán errores de aprovisionamiento del Servicio de aplicaciones. Esto es coherente con el portal de Hola y aquellos clientes que experimenten este problema pueden usar hello Azure toorequest portal acceso toopublish toothese regiones geográficas. Una vez que solicitan acceso toothese regiones mediante debería funcionar Hola aprovisionamiento portal de Azure. 

## <a name="azure-sdk-for-net-282"></a>Azure SDK para .NET 2.8.2
Después de la instalación de Hola de herramientas de hello 2.8.2, pueden experimentar los clientes Hola siguiendo el problema.         

* Si usa Windows 10 y no ha instalado Internet Explorer, puede que reciba un error de tipo "No se encontró Internet Explorer".
  problema de hello tooresolve, instalar Internet Explorer utilizando Hola agregar/quitar el cuadro de diálogo componentes de Windows.

Si observa este problema, utilice Hola enviar una sonrisa característica tooreport lo.

Para más información, consulte [este](https://azure.microsoft.com/blog/announcing-azure-sdk-2-8-2-for-net/) artículo.

## <a name="other-updates"></a>Otras actualizaciones
Para ver otras actualizaciones, vea la [publicación del anuncio de Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).

## <a name="also-see"></a>Consulte también:
[Publicación de anuncio de SDK de Azure 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)

[Información de retirada para hello Azure SDK para .NET y las API y soporte técnico](https://msdn.microsoft.com/library/azure/dn479282.aspx)

