---
title: "información general de DSC de automatización aaaAzure | Documentos de Microsoft"
description: "Una información general de Configuración de estado deseado (DSC) de Automatización de Azure, sus condiciones y problemas conocidos"
services: automation
documentationcenter: dev-center-name
author: eslesar
manager: carmonm
keywords: "powershell dsc, configuración de estado deseado, powershell dsc azure"
ms.assetid: fd40cb68-c1a6-48c3-bba2-710b607d1555
ms.service: automation
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: TBD
ms.date: 06/15/2017
ms.author: eslesar
ms.openlocfilehash: 5b8e5104c7b5bed848c015ac26a8b7d1f5b24de9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-automation-dsc-overview"></a>Información general de DSC de Automatización de Azure

DSC de automatización de Azure es un servicio de Azure que le permite toowrite, administrar y compilar la configuración de estado deseado (DSC) de PowerShell [configuraciones](https://msdn.microsoft.com/powershell/dsc/configurations), importar [recursos de DSC](https://msdn.microsoft.com/powershell/dsc/resources)y asignar nodos de tootarget configuraciones, todo en nube Hola.

## <a name="why-use-azure-automation-dsc"></a>¿Por qué usar DSC de Azure Automation?

DSC de Azure Automation proporciona varias ventajas con respecto a DSC fuera de Azure.

### <a name="built-in-pull-server"></a>Servidor de extracción integrado

Automatización de Azure ofrece un [servidor de extracción de DSC](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) para que los nodos de destino recibirán automáticamente las configuraciones, se ajustan estado toohello deseado e informar sobre su cumplimiento.
servidor de extracción integrados de Hello en automatización de Azure elimina Hola necesidad tooset seguridad y mantener su propio servidor de extracción.
Automatización de Azure puede tener como destino máquinas físicas o virtuales de Windows o Linux, en la nube de Hola o de forma local.

### <a name="management-of-all-your-dsc-artifacts"></a>Administración de todos los artefactos de DSC

DSC de automatización de Azure aporta Hola misma capa de administración demasiado[la configuración de estado deseado de PowerShell](https://msdn.microsoft.com/powershell/dsc/overview) como la automatización de Azure proporciona para secuencias de comandos de PowerShell.

Hola portal de Azure o desde PowerShell, puede administrar todos sus DSC configuraciones, los recursos y nodos de destino.

![Captura de pantalla de hoja de automatización de Azure Hola](./media/automation-dsc-overview/azure-automation-blade.png)

### <a name="import-reporting-data-into-log-analytics"></a>Importación de datos de informes a Log Analytics

Los nodos que se administran con el DSC de automatización de Azure enviar detallada estado datos toohello extracción integrada servidor de informes.
Puede configurar toosend de DSC de automatización de Azure en esta área de trabajo de análisis de registros de Microsoft Operations Management Suite (OMS) de tooyour de datos.
toolearn toosend DSC estado datos tooyour área de trabajo de análisis de registros, vea [al día Azure DSC de automatización reporting datos tooOMS análisis de registros](automation-dsc-diagnostics.md).

## <a name="introduction-video"></a>Vídeo de presentación

¿Prefiere ver tooreading? Eche un vistazo a Hola después de vídeo de mayo de 2015, se presentó por primera vez al DSC de automatización de Azure.

>[!NOTE]
>Aunque los conceptos de Hola y ciclo de vida que se describe en este vídeo son correctas, DSC de automatización de Azure ha progresado mucho porque este vídeo se grabó.
>Ahora está disponible con carácter general, tiene una interfaz de usuario mucho más amplia de hello portal de Azure y admite muchas funciones adicionales.

> [!VIDEO https://channel9.msdn.com/Events/Ignite/2015/BRK3467/player]

## <a name="next-steps"></a>Pasos siguientes

* toolearn cómo tooonboard toobe de nodos administrados con el DSC de automatización de Azure, consulte [incorporar máquinas para la administración mediante el DSC de automatización de Azure](automation-dsc-onboarding.md)
* tooget a usar DSC de automatización de Azure, consulte [Introducción a DSC de automatización de Azure](automation-dsc-getting-started.md)
* toolearn sobre la compilación de configuraciones de DSC para que pueda asignar nodos tootarget, consulte [compilación de configuraciones de DSC de automatización de Azure](automation-dsc-compile.md)
* Para ver la referencia de cmdlets de PowerShell para DSC de Azure Automation, consulte [Cmdlets de DSC de Azure Automation](/powershell/module/azurerm.automation/#automation).
* Para obtener información de precios, consulte [Precios de DSC de Azure Automation](https://azure.microsoft.com/pricing/details/automation/).
* toosee muestra un ejemplo del uso de DSC de automatización de Azure en una canalización de implementación continua, vea [tooIaaS de implementación continua DSC de automatización de Azure usando máquinas virtuales y Chocolatey](automation-dsc-cd-chocolatey.md)
