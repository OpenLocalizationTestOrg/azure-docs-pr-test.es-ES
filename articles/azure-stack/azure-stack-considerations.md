---
title: Diferencias clave entre Azure y Azure Stack al usar los servicios y compilar aplicaciones | Microsoft Docs
description: Lo que necesita saber si usa servicios o compila aplicaciones para Azure Stack.
services: azure-stack
documentationcenter: 
author: twooley
manager: byronr
editor: 
ms.assetid: c81f551d-c13e-47d9-a5c2-eb1ea4806228
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: twooley
ms.openlocfilehash: 0567811e36102177af9f9c339587b251e04a1ff5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="key-considerations-using-services-or-building-apps-for-azure-stack"></a>Consideraciones clave: uso de servicios o compilación de aplicaciones para Azure Stack

Si usa servicios o compila aplicaciones para Azure Stack, debe saber que existen diferencias entre Azure Stack y Azure. En este artículo se proporciona información general de las consideraciones clave al usar Azure Stack como entorno de desarrollo de nube híbrida.

## <a name="overview"></a>Información general

Azure Stack es una plataforma en la nube híbrida que le permite usar servicios de Azure desde el centro de datos del proveedor de servicios o de su empresa. Como desarrollador, puede compilar aplicaciones que se ejecutan en Azure Stack. A continuación, puede implementar estas aplicaciones en Azure Stack o en Azure, o bien puede compilar aplicaciones realmente híbridas que aprovechen la conectividad entre una nube de Azure Stack y Azure.

El proveedor de servicios o el administrador de la nube de Azure Stack le permitirá saber de qué servicios dispone y cómo obtener soporte técnico. Le proporcionará estos servicios a través de sus ofertas y planes personalizados.

El contenido técnico de Azure da por supuesto que las aplicaciones se están desarrollando para un servicio de Azure en lugar de para Azure Stack. Al compilar e implementar aplicaciones en Azure Stack, debe comprender algunas diferencias clave, como:

* Azure Stack ofrece un subconjunto de los servicios y características que están disponibles en Azure.
* El proveedor del servicio o la empresa pueden elegir qué servicios desean ofrecer. Esto incluye aplicaciones o servicios personalizados.
* Debe usar los puntos de conexión específicos de Azure Stack correctos (por ejemplo, las URL de la dirección del portal y el punto de conexión de Azure Resource Manager).
* Debe usar las versiones de PowerShell y de la API que son compatibles con Azure Stack. Esto garantiza que las aplicaciones funcionarán en Azure Stack y en Azure.

## <a name="cheat-sheet-high-level-differences"></a>Hoja de referencia rápida: diferencias de alto nivel

En la tabla siguiente se describen las diferencias de alto nivel entre Azure Stack y Azure. Téngalas en cuenta al desarrollar para Azure Stack o usar los servicios de Azure Stack.

| Ámbito | Azure (global) | Azure Stack |
| -------- | ------------- | ----------|
| ¿Quién lo administra? | Microsoft | Su empresa o proveedor de servicios.|
| ¿Quién es su contacto de soporte técnico? | Microsoft | Para obtener soporte técnico para el kit de desarrollo de Azure Stack, visite los [foros de Microsoft](https://social.msdn.microsoft.com/Forums/home?forum=azurestack). Dado que el kit de desarrollo es un entorno de evaluación, no se ofrece ningún soporte técnico oficial a través de los servicios de soporte al cliente (CSS) de Microsoft.
| Servicios disponibles | Consulte la lista de [productos de Azure](https://azure.microsoft.com/services/?b=17.04b). Los servicios disponibles varían según la región de Azure. | Azure Stack admite un subconjunto de los servicios de Azure. <br><br>Los servicios reales variarán en función de lo que el proveedor de servicios o la empresa decidan ofrecer.
| Punto de conexión de Azure Resource Manager* | https://management.azure.com | Para el kit de desarrollo: https://management.local.azurestack.external
| URL del portal* | [https://portal.azure.com](https://portal.azure.com) | Para el kit de desarrollo: https://portal.local.azurestack.external
| Region | Puede seleccionar en qué región desea implementar. | Para el kit de desarrollo, la región siempre será **local**. <br><br>El kit de desarrollo admite solo una región.
| Grupos de recursos | Un grupo de recursos puede abarcar varias regiones. | Para el kit de desarrollo, solo hay una región.
|Espacios de nombres, tipos de recursos y versiones de API compatibles | La versión más reciente (o versiones anteriores que no están en desuso). | Azure Stack es compatible con versiones específicas. Vea la sección "Requisitos de versión" de este artículo.
| | |

*Si es un operador en la nube de Azure Stack, consulte [Using the Azure Stack administrator and user portals](azure-stack-manage-portals.md) (Uso de los portales de usuario y administrador de Azure Stack) para obtener información acerca del portal de administración y las URL del punto de conexión de Resource Manager del administrador.

## <a name="helpful-tools-and-best-practices"></a>Herramientas útiles y prácticas recomendadas
 
 Microsoft proporciona varias herramientas e instrucciones que le ayudarán a desarrollar para Azure Stack.

| Recomendación | Referencias | 
| -------- | ------------- | 
| Instalar las herramientas adecuadas en la estación de trabajo de desarrollador. | - [Instalación de PowerShell](azure-stack-powershell-install.md)<br>- [Descarga de herramientas](azure-stack-powershell-download.md)<br>- [Configuración de PowerShell](azure-stack-powershell-configure-user.md)<br>- [Instalación de Visual Studio](azure-stack-install-visual-studio.md) 
| Consulte información acerca de lo siguiente:<br>- Consideraciones de la plantilla de Azure Resource Manager<br>- Cómo buscar plantillas de inicio rápido<br>- Usar un módulo de directivas que le ayude a usar Azure para desarrollar para Azure Stack | [Desarrollo para Azure Stack](azure-stack-developer.md) | 
| Revise y siga las prácticas recomendadas para plantillas. | [Plantillas de inicio rápido de Resource Manager](https://github.com/Azure/azure-quickstart-templates/blob/master/1-CONTRIBUTION-GUIDE/best-practices.md#best-practices)
| | |

## <a name="version-requirements"></a>Requisitos de versión

Azure Stack es compatible con versiones específicas de Azure PowerShell y de API del servicio Azure. Debe usar las versiones compatibles para asegurarse de que la aplicación se puede implementar tanto en Azure Stack como en Azure.

Para asegurarse de que está usando una versión correcta de Azure PowerShell, use [perfiles de la versión de API](azure-stack-version-profiles.md). Para determinar el perfil de la versión de API más reciente que puede usar, debe saber qué compilación de Azure Stack está usando. Puede consultar esta información en el administrador de Azure Stack.

>[!NOTE]
 Si está usando el kit de desarrollo de Azure Stack y tiene acceso administrativo, consulte la sección "Determine the current version" (Determinar la versión actual) de [Manage updates](https://docs.microsoft.com/azure/azure-stack/azure-stack-updates#determine-the-current-version) (Administrar actualizaciones) para determinar la compilación de Azure Stack.

Para otras API, ejecute el siguiente comando de PowerShell para generar los espacios de nombres, los tipos de recursos y las versiones de API compatibles con la suscripción de Azure Stack. Tenga en cuenta que aún es posible que existan diferencias en el nivel de propiedad. (Para que funcione este comando, ya debe haber [instalado](azure-stack-powershell-install.md) y [configurado](azure-stack-powershell-configure-user.md) PowerShell para un entorno de Azure Stack. También debe tener una suscripción a una oferta de Azure Stack).

 ```powershell
Get-AzureRmResourceProvider | Select ProviderNamespace -Expand ResourceTypes | Select * -Expand ApiVersions | `
Select ProviderNamespace, ResourceTypeName, @{Name="ApiVersion"; Expression={$_}} 
```

Resultado de ejemplo (truncado): ![resultado de ejemplo del comando Get-AzureRmResourceProvider](media/azure-stack-considerations/image1.png)
 
## <a name="next-steps"></a>Pasos siguientes

Para obtener más información detallada acerca de las diferencias en un nivel de servicio, consulte:

* [Considerations for Virtual Machines in Azure Stack](azure-stack-vm-considerations.md) (Consideraciones para máquinas virtuales de Azure Stack)
* [Considerations for Storage in Azure Stack](azure-stack-acs-differences.md) (Consideraciones para almacenamiento en Azure Stack)
* [Considerations for Azure Stack networking](azure-stack-network-differences.md) (Consideraciones para los servicios de red de Azure Stack)

