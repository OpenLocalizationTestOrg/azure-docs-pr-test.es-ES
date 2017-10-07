---
title: aaaKey diferencias entre Azure y Azure pila al usar los servicios y compilar aplicaciones | Documentos de Microsoft
description: "¿Qué debe tooknow al usar los servicios o compilar aplicaciones para Azure pila."
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
ms.openlocfilehash: e302f20aeb3c74f944cb3daaee7e0db073ab5bfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="key-considerations-using-services-or-building-apps-for-azure-stack"></a>Consideraciones clave: uso de servicios o compilación de aplicaciones para Azure Stack

Si usa servicios o compila aplicaciones para Azure Stack, debe saber que existen diferencias entre Azure Stack y Azure. Este artículo proporciona información general de hello consideraciones clave cuando el destino Azure pila como el entorno de desarrollo de nube híbrida.

## <a name="overview"></a>Información general

Azure Stack es una plataforma en la nube híbrida que le permite usar servicios de Azure desde el centro de datos del proveedor de servicios o de su empresa. Como desarrollador, puede compilar aplicaciones que se ejecutan en Azure Stack. A continuación, puede implementar estos tooAzure de aplicaciones de la pila, tooAzure, o puede crear realmente aplicaciones híbridas que aprovechan la conectividad de hello entre una nube de la pila de Azure y Azure.

El Administrador de la nube de pila de Azure o el proveedor de servicios le permitirá saber qué servicios están disponibles para toouse y cómo son compatibles con tooget. Le proporcionará estos servicios a través de sus ofertas y planes personalizados.

Hola contenido técnico de Azure se da por supuesto que se están desarrollando aplicaciones para un servicio de Azure en lugar de la pila de Azure. Al compilar e implementar aplicaciones tooAzure pila, debe conocer algunas diferencias clave, como:

* Pila de Azure ofrece un subconjunto de hello servicios y características que están disponibles en Azure.
* El proveedor de la empresa o un servicio puede elegir los servicios que desean toooffer. Esto incluye aplicaciones o servicios personalizados.
* Debe usar hello corregir los extremos de Azure específica de la pila (por ejemplo, direcciones URL de Hola para dirección de portal de Hola y el extremo de Azure Resource Manager hello).
* Debe usar las versiones de PowerShell y de la API que son compatibles con Azure Stack. Esto garantiza que las aplicaciones funcionarán en Azure Stack y en Azure.

## <a name="cheat-sheet-high-level-differences"></a>Hoja de referencia rápida: diferencias de alto nivel

Hello tabla siguiente describen las diferencias de alto nivel de hello entre la pila de Azure y Azure. Téngalas en cuenta al desarrollar para Azure Stack o usar los servicios de Azure Stack.

| Ámbito | Azure (global) | Azure Stack |
| -------- | ------------- | ----------|
| ¿Quién lo administra? | Microsoft | Su empresa o proveedor de servicios.|
| ¿Quién es su contacto de soporte técnico? | Microsoft | Compatibilidad del Kit de desarrollo de pila de Azure, visite hello [foros de Microsoft](https://social.msdn.microsoft.com/Forums/home?forum=azurestack). Dado que el kit de desarrollo de hello es un entorno de evaluación, no hay ningún oficial de soporte técnico que ofrecen a través de servicios de admitir de cliente de Microsoft (CSS).
| Servicios disponibles | Ver lista de Hola de [productos de Azure](https://azure.microsoft.com/services/?b=17.04b). Los servicios disponibles varían según la región de Azure. | Azure Stack admite un subconjunto de servicios de Azure. <br><br>Servicios reales varían en función de lo que el proveedor de empresa o servicio elige toooffer.
| Punto de conexión de Azure Resource Manager* | https://management.azure.com | Kit de desarrollo de hello: https://management.local.azurestack.external
| URL del portal* | [https://portal.azure.com](https://portal.azure.com) | Kit de desarrollo de hello: https://portal.local.azurestack.external
| Region | Puede seleccionar qué región que desee toodeploy a. | Kit de desarrollo de hello región siempre estará **local**. <br><br>kit de desarrollo de Hello admite solo una región.
| Grupos de recursos | Un grupo de recursos puede abarcar varias regiones. | Kit de desarrollo de hello, hay sólo una región.
|Espacios de nombres, tipos de recursos y versiones de API compatibles | Hola más reciente (o versiones anteriores que no están aún en desuso). | Azure Stack es compatible con versiones específicas. Vea Hola versión sección "requisitos" de este artículo.
| | |

* Si es un operador de nube de pila de Azure, consulte [uso de portales de administrador y usuario de hello en Azure pila](azure-stack-manage-portals.md) para obtener información acerca de hello administrador portal y administrador del Administrador de recursos direcciones URL del extremo.

## <a name="helpful-tools-and-best-practices"></a>Herramientas útiles y prácticas recomendadas
 
 Microsoft proporciona varias herramientas e instrucciones que le ayudarán a desarrollar para Azure Stack.

| Recomendación | Referencias | 
| -------- | ------------- | 
| Instalar herramientas correcto de hello en la estación de trabajo de desarrollador. | - [Instalación de PowerShell](azure-stack-powershell-install.md)<br>- [Descarga de herramientas](azure-stack-powershell-download.md)<br>- [Configuración de PowerShell](azure-stack-powershell-configure-user.md)<br>- [Instalación de Visual Studio](azure-stack-install-visual-studio.md) 
| Revisar información sobre Hola siguientes:<br>- Consideraciones de la plantilla de Azure Resource Manager<br>-Cómo toofind plantillas de inicio rápido<br>: Use un toohelp de módulo de directiva usar toodevelop Azure para la pila de Azure | [Desarrollo para Azure Stack](azure-stack-developer.md) | 
| Revise y siga las prácticas recomendadas para plantillas de Hola. | [Plantillas de inicio rápido de Resource Manager](https://github.com/Azure/azure-quickstart-templates/blob/master/1-CONTRIBUTION-GUIDE/best-practices.md#best-practices)
| | |

## <a name="version-requirements"></a>Requisitos de versión

Azure Stack es compatible con versiones específicas de Azure PowerShell y de API del servicio Azure. Debe usar tooensure versiones admitidas que puede implementar la aplicación tooboth pila de Azure y tooAzure.

Asegúrese de que utilice una versión correcta de PowerShell de Azure, use toomake [perfiles de la versión de API](azure-stack-version-profiles.md). toodetermine Hola API versión perfil de más reciente que puede usar, debe saber qué versión de pila de Azure que está usando. Puede consultar esta información en el administrador de Azure Stack.

>[!NOTE]
 Si utilizas Hola Kit de desarrollo de pila de Azure y tiene acceso administrativo, vea la sección de "Determinar la versión actual de Hola" de Hola de [administrar las actualizaciones de](https://docs.microsoft.com/azure/azure-stack/azure-stack-updates#determine-the-current-version) toodetermine Hola compilación de la pila de Azure.

Para otras API, ejecute hello siguientes espacios de nombres Hola toooutput de comandos de PowerShell, tipos de recursos y las versiones de API que se admiten en la suscripción de la pila de Azure. Tenga en cuenta que aún es posible que existan diferencias en el nivel de propiedad. (Para este toowork comando, debe tener ya [instalado](azure-stack-powershell-install.md) y [configurado](azure-stack-powershell-configure-user.md) PowerShell para un entorno de pila de Azure. También debe tener una oferta de suscripción tooan pila de Azure.)

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

