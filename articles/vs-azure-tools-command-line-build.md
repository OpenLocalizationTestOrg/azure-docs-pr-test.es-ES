---
title: "compilación de la línea de aaaCommand de Azure | Documentos de Microsoft"
description: "Compilación de línea de comandos de Azure"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 94b35d0d-0d35-48b6-b48b-3641377867fd
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/05/2017
ms.author: kraigb
ms.openlocfilehash: 295b61ba162dd4373ee3f56cc1462decb3e16762
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="building-azure-projects-from-hello-command-line"></a>Compilar proyectos de Azure desde la línea de comandos de Hola
Con hello Microsoft Build Engine (MSBuild), puede compilar productos en entornos de laboratorio de compilación donde no está instalado Visual Studio. MSBuild utiliza un formato XML para archivos de proyecto que es ampliable y totalmente compatible con Microsoft. Usa el formato de archivo de MSBuild hello, puede describir qué elementos se deben compilar en una o varias plataformas y configuraciones.

También puede ejecutar MSBuild en la línea de comandos de hello y, en este tema describe ese enfoque. Estableciendo propiedades en la línea de comandos de hello, puede crear configuraciones específicas de un proyecto. Del mismo modo, también puede definir los destinos de Hola que MSBuild crea. Para obtener más información sobre los parámetros de línea de comandos y MSBuild, consulte [Referencia de la línea de comandos de MSBuild](https://msdn.microsoft.com/library/ms164311.aspx).

## <a name="msbuild-parameters"></a>Parámetros de MSBuild
toocreate de manera más sencilla de Hello un paquete es toorun MSBuild con hello `/t:Publish` opción. De forma predeterminada, este comando crea un directorio en carpeta de raíz de toohello de relación para el proyecto de hello, como `<ProjectDirectory>\bin\Configuration\app.publish\`. Cuando compila un proyecto de Azure, se generan dos archivos: Hola propio archivo de paquete y el archivo de configuración complementario de hello:

* Archivo de paquete (`project.cspkg`)
* Archivo de configuración (`ServiceConfiguration.TargetProfile.cscfg`)

De manera predeterminada, cada proyecto de Azure incluye un archivo de configuración del servicio para las compilaciones locales (depuración) y otro para las compilaciones en la nube (ensayo o producción). Sin embargo, puede agregar o quitar archivos de configuración del servicio según sea necesario. Al compilar un paquete de Visual Studio, se le preguntará qué tooinclude de archivo de configuración del servicio junto con el paquete de saludo. Al compilar un paquete con MSBuild, archivo de configuración del servicio local de hello se incluye de forma predeterminada. archivo tooinclude una configuración de servicio diferente, conjunto hello `TargetProfile` propiedad de hello comando MSBuild (`MSBuild /t:Publish /p:TargetProfile=ProfileName`).

Si desea que toouse un directorio alternativo para hello almacena archivos de paquete y la configuración, establecer la ruta de hello mediante el uso de hello `/p:PublishDir=Directory\` opción, incluidos los Hola separador de barra diagonal inversa final.

## <a name="next-steps"></a>Pasos siguientes
Después de creación de paquete de hello, puede implementarlo tooAzure. Para obtener un tutorial que muestra cómo tooautomate que procesar, consulte [la entrega continua de los servicios de nube de Azure](./cloud-services/cloud-services-dotnet-continuous-delivery.md).

