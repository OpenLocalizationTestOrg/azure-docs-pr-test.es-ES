---
title: "aaaCreate una conexión a Internet cargar equilibrador - PowerShell de Azure clásico | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate una conexión a Internet equilibrador de carga de modo clásico con PowerShell"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-service-management
ms.assetid: 73e8bfa4-8086-4ef0-9e35-9e00b24be319
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 76d9a712a0acda223fc86b80be9c35c0ed9f3a50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internet-facing-load-balancer-classic-in-powershell"></a>Introducción a la creación de un equilibrador de carga orientado a Internet (clásico) en PowerShell

> [!div class="op_single_selector"]
> * [Portal de Azure clásico](../load-balancer/load-balancer-get-started-internet-classic-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-classic-ps.md)
> * [CLI de Azure](../load-balancer/load-balancer-get-started-internet-classic-cli.md)
> * [Servicios en la nube de Azure](../load-balancer/load-balancer-get-started-internet-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

> [!IMPORTANT]
> Antes de trabajar con recursos de Azure, es importante toounderstand que Azure tiene dos modelos de implementación: Administrador de recursos de Azure y clásico. Asegúrese de que comprende los [modelos de implementación y las herramientas](../azure-classic-rm.md) antes de trabajar con recursos de Azure. Puede ver documentación de Hola de distintas herramientas, haga clic en las pestañas de hello en parte superior de Hola de este artículo. Este artículo trata el modelo de implementación clásica de Hola. También puede [Obtenga información acerca de cómo toocreate una conexión a Internet cargar equilibrador mediante Azure Resource Manager](load-balancer-get-started-internet-arm-ps.md).

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="set-up-load-balancer-using-powershell"></a>Configurar el equilibrador de carga con PowerShell

tooset de un equilibrador de carga con powershell, siga Hola pasos:

1. Si nunca ha usado PowerShell de Azure, consulte [cómo tooInstall y configurar Azure PowerShell](/powershell/azure/overview) y siga instrucciones de hello todos los toohello de manera Hola finalizar toosign en Azure y seleccione su suscripción.
2. Después de crear una máquina virtual, puede usar cmdlets de PowerShell tooadd una máquina de tooa de un equilibrador de carga dentro de hello mismo servicio en la nube.

Hola el ejemplo siguiente se va a agregar un conjunto de equilibrador de carga denominada "granja de servidores Web" toocloud máquinas "mytestcloud" (o myctestcloud.cloudapp.net), agregar extremos de Hola para hello toovirtual de equilibrador de carga de servicio denominada "web1" y "web2". equilibrador de carga Hello recibe tráfico de red en el puerto 80 y equilibra la carga entre máquinas virtuales de hello definidas por el extremo local de hello (en este caso puerto 80) mediante TCP.

### <a name="step-1"></a>Paso 1

Crear un extremo con equilibrio de carga para máquinas virtuales de primera Hola "web1"

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web1" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

### <a name="step-2"></a>Paso 2

Cree otro punto de conexión para hello en segundo lugar máquina virtual "web2" con hello mismo carga nombre del equilibrador de conjunto

```powershell
Get-AzureVM -ServiceName "mytestcloud" -Name "web2" | Add-AzureEndpoint -Name "HttpIn" -Protocol "tcp" -PublicPort 80 -LocalPort 80 -LBSetName "WebFarm" -ProbePort 80 -ProbeProtocol "http" -ProbePath '/' | Update-AzureVM
```

## <a name="remove-a-virtual-machine-from-a-load-balancer"></a>Quitar una máquina virtual de un equilibrador de carga

Puede usar Remove-AzureEndpoint tooremove un punto de conexión de máquina virtual de equilibrador de carga de Hola

```powershell
Get-azureVM -ServiceName mytestcloud  -Name web1 |Remove-AzureEndpoint -Name httpin | Update-AzureVM
```

## <a name="next-steps"></a>Pasos siguientes

También puede [empezar a crear un equilibrador de carga interno](load-balancer-get-started-ilb-classic-ps.md) y configurar el tipo de [modo de distribución](load-balancer-distribution-mode.md) para un comportamiento del tráfico de red de un equilibrador de carga específico.

Si su aplicación necesita que las conexiones de tookeep activo de servidores detrás de un equilibrador de carga, puede conocer más acerca de [inactivo de la configuración de tiempo de espera TCP para un equilibrador de carga](load-balancer-tcp-idle-timeout.md). Cuando se usa el equilibrador de carga de Azure le servirá de ayuda toolearn acerca del comportamiento de conexión inactiva.
