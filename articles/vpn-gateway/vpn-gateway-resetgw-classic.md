---
title: "Restablecer un tooreestablish de puerta de enlace de VPN de Azure túneles IPsec | Documentos de Microsoft"
description: "Este artículo le guiará a través de restablecimiento de los puerta de enlace de VPN de Azure los túneles IPsec tooreestablish. las puertas de enlace tooVPN en hello clásico y modelos de implementación del Administrador de recursos de Hola aplica el artículo de Hola."
services: vpn-gateway
documentationcenter: na
author: cherylmc
manager: timlt
editor: 
tags: azure-resource-manager,azure-service-management
ms.assetid: 79d77cb8-d175-4273-93ac-712d7d45b1fe
ms.service: vpn-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/24/2017
ms.author: cherylmc
ms.openlocfilehash: 84dd741f0bebd6b18cb235216a68a88da5fe17b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="reset-a-vpn-gateway"></a>Restablecimiento de una puerta de enlace de VPN

Restablecer una puerta de enlace de VPN de Azure es útil si se pierde la conectividad VPN entre locales en uno o varios túneles VPN de sitio a sitio. En esta situación, los dispositivos VPN local son todo funciona correctamente, pero son tooestablish imposibilidad de túneles de IPsec con puertas de enlace de VPN de Azure de Hola. Este artículo lo ayuda a restablecer la puerta de enlace de VPN.

### <a name="what-happens-during-a-reset"></a>¿Qué ocurre durante el restablecimiento?

Una puerta de enlace de VPN se compone de dos instancias de VM que se ejecutan en una configuración de modo de espera activo. Si se restablece la puerta de enlace de hello, se reinicia la puerta de enlace de hello, y, a continuación, vuelve a aplicar Hola entre entornos tooit configuraciones. puerta de enlace de Hello mantiene Hola la dirección IP pública ya tiene. Esto significa que no necesita configuración del enrutador VPN tooupdate Hola con una nueva dirección IP pública para la puerta de enlace VPN de Azure.

Cuando se emite la puerta de enlace de hello comando tooreset hello, instancias activas actuales de Hola de puerta de enlace de VPN de Azure Hola se reinicia inmediatamente. Habrá un breve intervalo durante la conmutación por error de Hola de hello instancias activas (está reiniciando), instancia de toohello en espera. espacio de Hello debe ser inferior a un minuto.

Si no se restaura la conexión de hello después del primer reinicio de hello, problema Hola mismo nuevo comando tooreboot Hola segunda VM instancia (Hola nueva active puerta de enlace). Si dos reinicios de hello están solicitada tooback atrás, habrá un período más largo ligeramente donde se están reiniciando ambas instancias VM (activos y en espera). Esto hará que un intervalo más largo en la conectividad VPN de hello, seguridad too2 too4 minutos para los reinicios de las máquinas virtuales toocomplete Hola.

Después de dos reinicios, si sigue experimentando problemas de conectividad entre entornos, abra una solicitud de soporte técnico de hello portal de Azure.

## <a name="before"></a>Antes de empezar

Antes de restablecer la puerta de enlace, compruebe los elementos clave de hello enumeran a continuación para cada túnel VPN de IPsec sitio a sitio (S2S). Si hay alguna incoherencia en los elementos de hello producirá disconnect Hola de túneles VPN S2S. Comprobar y corregir las configuraciones de Hola para su entorno local y puertas de enlace VPN de Azure evita reinicios innecesarios y las interrupciones de Hola otras conexiones de trabajo en puertas de enlace de Hola.

Compruebe los siguientes elementos antes de restablecer la puerta de enlace de hello:

* Hola Internet IP direcciones (VIP) para ambos puerta de enlace de VPN de Azure de Hola y puerta de enlace VPN están configurados correctamente en ambas directivas VPN Hola hello y Azure local a local de Hola.
* clave compartida previamente de Hello debe ser Hola lo mismo en puertas de enlace VPN de Azure y local.
* Si aplica la configuración de IPsec/IKE específica, como cifrado, algoritmos hash y PFS (confidencialidad directa perfecta), asegúrese de ambos hello Azure y puertas de enlace VPN local tienen Hola misma configuración.

## <a name="portal"></a>Azure Portal

Puede restablecer una puerta de enlace de VPN de administrador de recursos mediante Hola portal de Azure. Si desea tooreset una puerta de enlace clásico, vea hello [PowerShell](#resetclassic) pasos.

### <a name="resource-manager-deployment-model"></a>Modelo de implementación del Administrador de recursos

1. Abra hello [portal de Azure](https://portal.azure.com) y navegar por el enlace de red virtual del Administrador de recursos toohello que desea tooreset.
2. En la hoja de Hola para puerta de enlace de red virtual de hello, haga clic en 'Restablecer'.

  ![Hoja de restablecimiento de puerta de enlace de VPN](./media/vpn-gateway-howto-reset-gateway/reset-vpn-gateway-portal.png)
3. En hello restablecer hoja, haga clic en hello **restablecer** botón.

## <a name="ps"></a>PowerShell

### <a name="resource-manager-deployment-model"></a>Modelo de implementación del Administrador de recursos

Hola cmdlet para restablecer una puerta de enlace es **AzureRmVirtualNetworkGateway restablecimiento**. Antes de realizar un restablecimiento, asegúrese de que tiene Hola versión más reciente de hello [cmdlets de PowerShell del Administrador de recursos](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0). Hello en el ejemplo siguiente se restablece una puerta de enlace de red virtual denominado VNet1GW en el grupo de recursos de Hola TestRG1:

```powershell
$gw = Get-AzureRmVirtualNetworkGateway -Name VNet1GW -ResourceGroup TestRG1
Reset-AzureRmVirtualNetworkGateway -VirtualNetworkGateway $gw
```

Resultado:

Cuando reciba un resultado devuelto, puede asumir Hola puerta de enlace se restableció correctamente. Sin embargo, hay nada en el resultado devuelto Hola que indica explícitamente que Hola se restableció correctamente. Si desea que toolook estrechamente en hello historial toosee exactamente cuando restablecimiento de puerta de enlace de Hola se ha producido, puede ver esa información en hello [portal de Azure](https://portal.azure.com). En el portal de hello, navegue demasiado**"GatewayName" -> mantenimiento de recursos**.

### <a name="resetclassic"></a>Modelo de implementación clásica

Hola cmdlet para restablecer una puerta de enlace es **Reset-AzureVNetGateway**. Antes de realizar un restablecimiento, asegúrese de que tiene Hola versión más reciente de hello [cmdlets de PowerShell Service Management (SM)](https://docs.microsoft.com/powershell/azure/install-azure-ps?view=azuresmps-3.7.0). Hello en el ejemplo siguiente se restablece puerta de enlace de Hola para una red virtual denominada "ContosoVNet":

```powershell
Reset-AzureVNetGateway –VnetName “ContosoVNet”
```

Resultado:

```powershell
Error          :
HttpStatusCode : OK
Id             : f1600632-c819-4b2f-ac0e-f4126bec1ff8
Status         : Successful
RequestId      : 9ca273de2c4d01e986480ce1ffa4d6d9
StatusCode     : OK
```

## <a name="cli"></a>Azure CLI

puerta de enlace de tooreset hello, use hello [restablece az red red virtual de puerta de enlace](https://docs.microsoft.com/cli/azure/network/vnet-gateway#reset) comando. Hello en el ejemplo siguiente se restablece una puerta de enlace de red virtual denominado VNet5GW en el grupo de recursos de Hola TestRG5:

```azurecli
az network vnet-gateway reset -n VNet5GW -g TestRG5
```

Resultado:

Cuando reciba un resultado devuelto, puede asumir Hola puerta de enlace se restableció correctamente. Sin embargo, hay nada en el resultado devuelto Hola que indica explícitamente que Hola se restableció correctamente. Si desea que toolook estrechamente en hello historial toosee exactamente cuando restablecimiento de puerta de enlace de Hola se ha producido, puede ver esa información en hello [portal de Azure](https://portal.azure.com). En el portal de hello, navegue demasiado**"GatewayName" -> mantenimiento de recursos**.
