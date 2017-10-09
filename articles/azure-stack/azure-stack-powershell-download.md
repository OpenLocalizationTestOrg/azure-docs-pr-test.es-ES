---
title: aaaDownload pila de Azure tools desde GitHub | Documentos de Microsoft
description: "Obtenga información acerca de cómo las herramientas de toodownload necesario toowork con la pila de Azure."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: a88c97b0ef1dd70e63771f0607cc07ec7a00b533
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="download-azure-stack-tools-from-github"></a>Descarga de herramientas de Azure Stack desde GitHub

Herramientas de AzureStack es un repositorio de GitHub que hospeda módulos de PowerShell que puede usar toomanage e implementar recursos tooAzure pila. Puede descargar y usar a estos módulos toohello Kit de desarrollo de pila de Azure o tooa basados en windows externo cliente de PowerShell si tiene previsto tooestablish conectividad VPN. tooobtain estas herramientas, clonar el repositorio de GitHub de Hola o hello AzureStack herramientas carpeta de descarga. 

repositorio de hello tooclone, descargue [Git](https://git-scm.com/download/win) para Windows, abra una ventana del símbolo del sistema y ejecute la siguiente secuencia de comandos de hello:

```PowerShell
# Change directory toohello root directory 
cd \

# clone hello repository
git clone https://github.com/Azure/AzureStack-Tools.git --recursive

# Change toohello tools directory
cd AzureStack-Tools
```

carpeta de herramientas en hello toodownload, ejecute la siguiente secuencia de comandos de hello:

```PowerShell
# Change directory toohello root directory 
cd \

# Download hello tools archive
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

# Expand hello downloaded files
expand-archive master.zip `
  -DestinationPath . `
  -Force

# Change toohello tools directory
cd AzureStack-Tools-master

```

## <a name="functionalities-provided-by-hello-modules"></a>Funcionalidades proporcionadas por módulos de Hola

repositorio de Hello AzureStack-Tools contiene los módulos de PowerShell que admiten Hola siga funcionalidades para la pila de Azure:  

| Funcionalidad | Descripción | ¿Quién puede usar este módulo? |
| --- | --- | --- |
| [Funcionalidades en la nube](azure-stack-validate-templates.md) | Utilice este capacidades de módulo tooget hello en la nube de una nube. Por ejemplo, puede obtener capacidades de la nube de hello como versión de API, los recursos de Azure Resource Manager, etc. de extensiones de máquina virtual para la pila de Azure y Azure nubes mediante este módulo. | Usuarios y administradores de la nube. |
| [Administración de procesos de Azure Stack](azure-stack-add-vm-image.md) | Use este módulo tooadd o quitar una imagen de VM de marketplace de Azure pila Hola. | Administradores de la nube. |
| [Administración de la infraestructura de Azure Stack](https://github.com/Azure/AzureStack-Tools/blob/master/Infrastructure/README.md) | Use esta infraestructura de Azure pila módulo toomanage máquinas virtuales, alertas, actualizaciones etcetera. |  Administradores de la nube.|
| [Directiva de Resource Manager para Azure Stack](azure-stack-policy-module.md) | Utilice este tooconfigure módulo una suscripción de Azure o grupo de un recurso de Azure con hello mismo control de versiones y el servicio de disponibilidad como la pila de Azure. | Usuarios y administradores de la nube |
| [Registro con Azure](azure-stack-register.md) | Utilice este módulo tooregister la instancia del kit de desarrollo con Azure. Después de registrar, puede descargar los elementos de marketplace de Hola de Azure y usarlos en la pila de Azure. | Administradores de nube |
| [Implementación de Azure Stack](azure-stack-run-powershell-script.md) | Utilice este toodeploy del equipo de host de módulo tooprepare hello Azure pila y volver a implementar mediante hello Disk(VHD) de disco duro Virtual de Azure pila imagen. | Administradores de la nube. |
| [Pila de conexión tooAzure](azure-stack-connect-powershell.md) | Utilice esta instancia de Azure pila módulo tooconnect tooan a través de PowerShell y tooconfigure tooAzure de conectividad VPN pila. | Usuarios y administradores de la nube |
| [Administración de servicios de Azure Stack](azure-stack-create-offer.md) | Azure administradores de pila pueden usar este toocreate módulo ofrecen un inquilino de forma predeterminada con una cuota de ilimitado a través de servicios de proceso, almacenamiento, red y el almacén de claves.   | Administradores de la nube.|
| [Validador de plantilla](azure-stack-validate-templates.md) | Use este módulo tooverify si una plantilla nueva o existente puede ser implementado tooAzure pila. | Usuarios y administradores de la nube |


## <a name="next-steps"></a>Pasos siguientes
* [Configurar el entorno de PowerShell del usuario de hello pila de Azure](azure-stack-powershell-configure-user.md)   
* [Conectar tooAzure Kit de desarrollo de pila a través de una VPN](azure-stack-connect-azure-stack.md)  
