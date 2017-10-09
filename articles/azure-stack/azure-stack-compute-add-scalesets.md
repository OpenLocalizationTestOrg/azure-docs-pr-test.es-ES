---
title: "conjuntos de escalas de máquina virtual de aaaMake disponibles en la pila de Azure"
description: "Obtenga información acerca de cómo un administrador de la nube puede agregar toohello de escala de máquina virtual Azure Marketplace de pila"
services: azure-stack
author: anjayajodha
ms.service: azure-stack
ms.topic: article
ms.date: 8/4/2017
ms.author: anajod
keywords: 
ms.openlocfilehash: 14365d62ac2f2bc453c25ce4769464eb30180ea8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="make-virtual-machine-scale-sets-available-in-azure-stack"></a>Proporcionar conjuntos de escalado de máquinas virtuales en Azure Stack
Los conjuntos de escalado de máquinas virtuales son un recurso de proceso de Azure Stack. Puede usar toodeploy y administrar un conjunto de máquinas virtuales idénticos. Con todas las máquinas virtuales configuradas Hola igual, no requieren conjuntos de escalas previamente el aprovisionamiento de máquinas virtuales. Es más fácil de servicios a gran escala toobuild que tienen como destino de proceso intensivo, grandes cantidades de datos y las cargas de trabajo en contenedores.

En este tema le guía a través de conjuntos de escalas de hello proceso toomake disponibles en hello Azure Marketplace de pila. Después de completar este procedimiento, los usuarios pueden agregar a escala de máquinas virtuales establece tootheir suscripciones.

Los conjuntos de escalado de máquinas virtuales en Azure Stack son similares a los conjuntos de escalado de máquinas virtuales en Azure. Para obtener más información, vea Hola siguientes vídeos:
* [Mark Russinovich talks Azure Scale Sets](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/) (Mark Russinovich habla sobre los conjuntos de escalado de Azure)
* [Virtual Machine Scale Sets with Guy Bowerman](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

En Azure Stack, los conjuntos de escalado de máquinas virtuales no admiten escalado automático. Puede agregar más escala tooa de instancias establecido mediante el portal de Azure pila hello, plantillas de administrador de recursos o PowerShell.

## <a name="prerequisites"></a>Requisitos previos
* **PowerShell y herramientas**

   Instalar y PowerShell configurada para la pila de Azure y las herramientas de la pila de Azure de Hola. Consulte [Get up and running with PowerShell in Azure Stack](azure-stack-powershell-configure-quickstart.md) (Ponerse en marcha con PowerShell en Azure Stack).

   Después de instalar las herramientas de la pila de Azure de hello, asegúrese de que importar Hola después de módulo de PowerShell (ruta de acceso relativa toohello. \ComputeAdmin carpeta de hello AzureStack-herramientas-master):

        Import-Module .\AzureStack.ComputeAdmin.psm1

* **Imagen del sistema operativo**

   Si no ha agregado un tooyour de imagen de sistema operativo Azure Marketplace de pila, vea [marketplace de pila de Azure de agregar Hola VM de Windows Server 2016 imagen toohello](azure-stack-add-default-image.md).

   Para compatibilidad con Linux, descargar Ubuntu Server 16.04 y agregarlo mediante ```Add-AzsVMImage``` con hello parámetros siguientes: ```-publisher "Canonical" -offer "UbuntuServer" -sku "16.04-LTS"```.

## <a name="add-hello-virtual-machine-scale-set"></a>Agregar conjunto de escalas de máquina virtual de Hola

Editar Hola PowerShell siguiente para su entorno de script y vuelva a ejecutarlo tooadd un tooyour de conjunto de escala de máquina virtual Azure Marketplace de pila. 

``$User``es la cuenta de hello que usar portal del administrador tooconnect Hola. Por ejemplo: serviceadmin@contoso.onmicrosoft.com.

```
$Arm = "https://adminmanagement.local.azurestack.external"
$Location = "local"

Add-AzureRMEnvironment -Name AzureStackAdmin -ArmEndpoint $Arm

$Password = ConvertTo-SecureString -AsPlainText -Force "<your Azure Stack administrator password>"

$User = "<your Azure Stack service administrator user name>"

$Creds =  New-Object System.Management.Automation.PSCredential $User, $Password

$AzsEnv = Get-AzureRmEnvironment AzureStackAdmin
$AzsEnvContext = Add-AzureRmAccount -Environment $AzsEnv -Credential $Creds
Select-AzureRmProfile -Profile $AzsEnvContext

Select-AzureRmSubscription -SubscriptionName "Default Provider Subscription"

Add-AzsVMSSGalleryItem -Location $Location
```

## <a name="remove-a-virtual-machine-scale-set"></a>Eliminación de un conjunto de escalado de máquinas virtuales

tooremove un elemento de galería de conjunto de escala máquina virtual, ejecute el siguiente comando de PowerShell de hello:

    Remove-AzsVMSSGalleryItem

> [!NOTE]
> elemento de la Galería de Hello no se quitará de forma inmediata. Puede que tenga la forma en portal de hello toorefresh varias veces antes de quitarlo de hello Marketplace.


## <a name="next-steps"></a>Pasos siguientes
[Preguntas frecuentes acerca de Azure Stack](azure-stack-faq.md)

