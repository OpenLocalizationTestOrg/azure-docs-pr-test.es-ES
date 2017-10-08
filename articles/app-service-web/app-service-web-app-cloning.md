---
title: "aaaWeb aplicación clonación con PowerShell"
description: "Obtenga información acerca de cómo tooclone las aplicaciones de Web toonew de aplicaciones Web con PowerShell."
services: app-service\web
documentationcenter: 
author: ahmedelnably
manager: stefsch
editor: 
ms.assetid: f9a5cfa1-fbb0-41e6-95d1-75d457347a35
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/13/2016
ms.author: aelnably
ms.openlocfilehash: b8882370d6db6939f8e4473ccc1414091bdcb8f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-app-cloning-using-powershell"></a>Clonación de aplicaciones del Servicio de aplicaciones de Azure mediante PowerShell
Con versión de Hola de Microsoft Azure PowerShell versión 1.1.0 una nueva opción ha sido agregado AzureRMWebApp tooNew que daría Hola usuario Hola capacidad tooclone una aplicación de tooa que acaba de crear aplicación Web existente en una región diferente o en hello misma región. Esto le permitirá clientes toodeploy un número de aplicaciones en diferentes regiones rápida y fácilmente.

La clonación de aplicaciones actualmente solo se admite para los planes de Servicio de aplicaciones de nivel Premium. los usos de característica nuevos Hola Hola mismo limitaciones como característica de copia de seguridad de aplicaciones Web, consulte [copia de seguridad una aplicación web en el servicio de aplicación de Azure](web-sites-backup.md).

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

toolearn sobre el uso de Azure Resource Manager según toomanage de cmdlets de PowerShell de Azure, la protección de aplicaciones Web [Azure Resource Manager según los comandos de PowerShell para la aplicación Web de Azure](app-service-web-app-azure-resource-manager-powershell.md)

## <a name="cloning-an-existing-app"></a>Clonación de una aplicación existente
Escenario: Una aplicación web existente en la región Ee.uu. Central sur, usuario Hola gustaría tooclone Hola contenido tooa nueva aplicación web en la región Ee.uu. Central Norte. Esto puede realizarse con la versión de Azure Resource Manager de Hola de hello PowerShell cmdlet toocreate una nueva aplicación web con la opción de hello - SourceWebApp.

Conocer los recursos de hello nombre del grupo que contiene la aplicación web de origen de hello, podemos usar Hola siguiendo la información de la aplicación de PowerShell comando tooget Hola origen web (en este caso denominado webapp de origen):

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

toocreate un nuevo Plan de servicio de aplicación, podemos utilizar comando New-AzureRmAppServicePlan como en el siguiente ejemplo de Hola

    New-AzureRmAppServicePlan -Location "South Central US" -ResourceGroupName DestinationAzureResourceGroup -Name NewAppServicePlan -Tier Premium

Con hello AzureRmWebApp nuevo comando, podemos crear nueva aplicación de web hello en región de hello Ee.uu. Central Norte y asociar los niveles de premium existente tooan Plan de servicio de aplicaciones, además, podemos utilizar Hola mismo recurso de grupo como aplicación web de origen de Hola o definir un nuevo grupo de recursos , siguiente Hola demuestra que:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp

tooclone una aplicación web existente incluidas todas las ranuras de implementación asociado, el usuario de hello deberá toouse Hola IncludeSourceWebAppSlots parámetro, Hola siguiente comando de PowerShell muestra el uso de Hola de ese parámetro con hello AzureRmWebApp nuevo comando:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -IncludeSourceWebAppSlots

tooclone una aplicación web existente en hello misma región, el usuario de hello deberá toocreate un nuevo grupo de recursos y un nuevo servicio de aplicación plan Hola Hola misma región y, a continuación, usar después de la aplicación web de PowerShell comando tooclone hello

    $destapp = New-AzureRmWebApp -ResourceGroupName NewAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan NewAppServicePlan -SourceWebApp $srcap

## <a name="cloning-an-existing-app-tooan-app-service-environment"></a>Clonar un tooan de aplicación existente entorno del servicio de aplicaciones
Escenario: Una aplicación web existente en la región Ee.uu. Central sur, usuario Hola gustaría tooclone Hola contenido tooa nueva web app tooan existente entorno de servicio de aplicación (ASE).

Conocer los recursos de hello nombre del grupo que contiene la aplicación web de origen de hello, podemos usar Hola siguiendo la información de la aplicación de PowerShell comando tooget Hola origen web (en este caso denominado webapp de origen):

    $srcapp = Get-AzureRmWebApp -ResourceGroupName SourceAzureResourceGroup -Name source-webapp

Conocer el nombre del saludo ASE y nombre de grupo de recursos de Hola Hola ASE pertenece a, usuario de hello puede utilizar comandos Hola New-AzureRmWebApp toocreate Hola nueva aplicación web incluida en hello existente ASE, Hola después de que muestra:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -ASEName DestinationASE -ASEResourceGroupName DestinationASEResourceGroupName -SourceWebApp $srcapp

parámetro de ubicación de Hello es necesario debido a razón de toolegacy, pero en caso de hello de creación de una aplicación en un ASE se omitirán. 

## <a name="cloning-an-existing-app-slot"></a>Clonación de una ranura de aplicación existente
Escenario: usuario Hola gustaría tooclone un tooeither de ranura de aplicación Web una nueva aplicación Web existente o una nueva ranura de aplicación Web. Hola nueva aplicación Web puede estar en hello misma región como ranura de aplicación Web de hello original o en una región distinta.

Conocer los recursos de hello nombre del grupo que contiene la aplicación web de origen de hello, podemos usar Hola siguiente información de tooget Hola origen ranura de aplicación web (en este caso se denomina origen webappslot) vinculada tooWeb de aplicación origen webapp de comando de PowerShell:

    $srcappslot = Get-AzureRmWebAppSlot -ResourceGroupName SourceAzureResourceGroup -Name source-webapp -Slot source-webappslot

siguiente Hello muestra cómo crear un clon de hello web app tooa nueva aplicación web de origen:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "North Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcappslot

## <a name="configuring-traffic-manager-while-cloning-a-app"></a>Configuración del Administrador de tráfico durante la clonación de una aplicación
Crear aplicaciones web de varias regiones y configurar Azure Traffic Manager tooroute tráfico tooall estas aplicaciones web, es un tooinsure n escenario importante que las aplicaciones de los clientes son de alta disponibilidad, al clonar una aplicación web existente que tenga Hola opción tooconnect ambos web aplicaciones tooeither un nuevo perfil de administrador de tráfico o uno existente: tenga en cuenta que el Administrador de recursos de Azure solo la versión de Traffic Manager es compatible.

### <a name="creating-a-new-traffic-manager-profile-while-cloning-a-app"></a>Creación de un nuevo perfil del Administrador de tráfico durante la clonación de una aplicación
Escenario: usuario Hola gustaría tooclone una región de tooanother de aplicación web, al configurar un perfil de administrador de tráfico de Azure Resource Manager que incluyen las dos aplicaciones web. siguiente Hello muestra cómo crear un clon de hello web app tooa nueva aplicación web de origen al configurar un nuevo perfil de Traffic Manager:

    $destapp = New-AzureRmWebApp -ResourceGroupName DestinationAzureResourceGroup -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileName newTrafficManagerProfile

### <a name="adding-new-cloned-web-app-tooan-existing-traffic-manager-profile"></a>Agregar nueva clonado aplicación Web tooan Traffic Manager perfil existente
Escenario: Hola el usuario tiene un perfil de administrador de tráfico de Azure Resource Manager que gustaría tooadd ambas aplicaciones como extremos web. toodo por lo tanto, es necesario tooassemble Hola existente de Id. de perfil de administrador de tráfico, necesitamos Id. de suscripción de Hola, nombre del grupo de recursos y nombre de perfil de tráfico existente de hello manager.

    $TMProfileID = "/subscriptions/<Your subscription ID goes here>/resourceGroups/<Your resource group name goes here>/providers/Microsoft.TrafficManagerProfiles/ExistingTrafficManagerProfileName"

Si tiene Id. de administrador de tráfico de hello, siguiente hello muestra la creación de un clon de hello web app tooa nueva aplicación web de origen al agregarlos tooan perfil de Traffic Manager existente:

    $destapp = New-AzureRmWebApp -ResourceGroupName <Resource group name> -Name dest-webapp -Location "South Central US" -AppServicePlan DestinationAppServicePlan -SourceWebApp $srcapp -TrafficManagerProfileId $TMProfileID

## <a name="current-restrictions"></a>Restricciones actuales
Esta característica está actualmente en vista previa, estamos trabajando tooadd nuevas capacidades con el tiempo, Hola lista siguiente se Hola restricciones conocidas de la versión actual de Hola de clonación de la aplicación:

* No se clona la configuración de escalado automático.
* No se clona la configuración de programación de copia de seguridad.
* No se clona la configuración de red virtual.
* Detalles de aplicaciones no se establecen automáticamente en la aplicación web de destino de Hola
* No se clona la configuración de Easy Auth.
* No se clona la extensión Kudu.
* No se clonan las reglas de TiP.
* No se clona el contenido de la base de datos

### <a name="references"></a>Referencias
* [Comandos de PowerShell basados en Azure Resource Manager para aplicación web de Azure](app-service-web-app-azure-resource-manager-powershell.md)
* [Clonación de aplicaciones web con el Portal de Azure](app-service-web-app-cloning-portal.md)
* [Hacer copia de seguridad de una aplicación web en el Servicio de aplicaciones de Azure](web-sites-backup.md)
* [Compatibilidad de Azure Resource Manager con Traffic Manager (versión preliminar)](../traffic-manager/traffic-manager-powershell-arm.md)
* [Introducción tooApp entorno del servicio](app-service-app-service-environment-intro.md)
* [Uso de Azure PowerShell con Azure Resource Manager](../powershell-azure-resource-manager.md)

