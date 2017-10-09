---
title: aaaTroubleshoot grupos de seguridad de red - PowerShell | Documentos de Microsoft
description: "Obtenga información acerca de cómo tootroubleshoot grupos de seguridad de red en la implementación de Azure Resource Manager Hola modelar con Azure PowerShell."
services: virtual-network
documentationcenter: na
author: AnithaAdusumilli
manager: narayan
editor: 
tags: azure-resource-manager
ms.assetid: 4c732bb7-5cb1-40af-9e6d-a2a307c2a9c4
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/23/2016
ms.author: anithaa
ms.openlocfilehash: 95fd60fa72cf6d17fa990e3c3eb7d980878f7c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-network-security-groups-using-azure-powershell"></a>Solución de problemas de los grupos de seguridad de red utilizando Azure PowerShell
> [!div class="op_single_selector"]
> * [Portal de Azure](virtual-network-nsg-troubleshoot-portal.md)
> * [PowerShell](virtual-network-nsg-troubleshoot-powershell.md)
> 
> 

Si configura los grupos de seguridad de red (NSG) en la máquina virtual (VM) y están experimentando problemas de conectividad de la máquina virtual, este artículo proporciona información general sobre las capacidades de diagnóstico para los NSG toohelp seguir solucionando el problema.

Los NSG permiten tipos de hello toocontrol de tráfico que fluyen dentro y fuera de sus máquinas virtuales (VM). Los NSG pueden toosubnets aplicados en una red Virtual de Azure (VNet), interfaces de red (NIC) o ambos. Hola efectivo reglas que se aplican tooa NIC son una agregación de reglas de Hola que existan en hello NSG aplicadas tooa hello y formación subred está conectado a. Las reglas en estos NSG a veces pueden entrar en conflicto entre sí y afectar la conectividad de red de la máquina virtual.  

Puede ver todas las reglas de seguridad eficaz Hola desde sus NSG, tal como se aplica en NIC de la máquina virtual. Este artículo muestra cómo los problemas de conectividad VM tootroubleshoot utilizando estas reglas en Hola modelo de implementación de Azure Resource Manager. Si no está familiarizado con conceptos de red virtual y NSG, leer hello [red Virtual](virtual-networks-overview.md) y [grupos de seguridad de red](virtual-networks-nsg.md) artículos de información general.

## <a name="using-effective-security-rules-tootroubleshoot-vm-traffic-flow"></a>Utilizando el flujo de tráfico de las reglas de seguridad efectivo tootroubleshoot VM
escenario de Hola que sigue es un ejemplo de un problema de conexión comunes:

Una máquina virtual denominada *VM1* forma parte de una subred *Subnet1* dentro de una red virtual denominada *WestUS VNet1*. Un toohello de tooconnect de intento de máquinas virtuales mediante RDP a través del puerto TCP 3389 se produce un error. Los NSG se aplican en ambos Hola NIC *VM1 NIC1* y Hola subred *subred1*. Se permite tráfico tooTCP puerto 3389 en hello NSG asociado a la interfaz de red de hello *VM1 NIC1*; sin embargo, produce un error de tooVM1 puerto 3389 de ping de TCP.

Aunque este ejemplo utiliza el puerto TCP 3389, Hola lo siguiente puede ser usado toodetermine errores de conexión entrantes y salientes a través de cualquier puerto.

## <a name="detailed-troubleshooting-steps"></a>Pasos de la solución de problemas detallada
Completar Hola siguiendo los pasos tootroubleshoot NSG para una máquina virtual:

1. Inicie un tooAzure de sesión y de inicio de sesión de PowerShell de Azure. Si no está familiarizado con el uso de PowerShell de Azure, lea hello [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview) artículo.
2. Escriba Hola siguiente comando tooreturn tooa NIC con el nombre de aplicar todas las reglas NSG *VM1 NIC1* en grupo de recursos de hello *RG1*:
   
        Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
   
   > [!TIP]
   > Si no conoce el nombre de Hola de una NIC, escriba Hola siguiendo los nombres de comando tooretrieve Hola de todas las NIC en un grupo de recursos: 
   > 
   > `Get-AzureRmNetworkInterface -ResourceGroupName RG1 | Format-Table Name`
   > 
   > 
   
    Hello texto siguiente es un ejemplo de Hola reglas efectivo salida que se devuelve para hello *VM1 NIC1* NIC:
   
        NetworkSecurityGroup   : {
                                   "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/VM1-NIC1-NSG"
                                 }
        Association            : {
                                   "NetworkInterface": {
                                     "Id": "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkInterfaces/VM1-NIC1"
                                   }
                                 }
        EffectiveSecurityRules : [
                                 {
                                 "Name": "securityRules/allowRDP",
                                 "Protocol": "Tcp",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "3389-3389",
                                 "SourceAddressPrefix": "Internet",
                                 "DestinationAddressPrefix": "0.0.0.0/0",
                                 "ExpandedSourceAddressPrefix": [… ],
                                 "ExpandedDestinationAddressPrefix": [],
                                 "Access": "Allow",
                                 "Priority": 1000,
                                 "Direction": "Inbound"
                                 },
                                 {
                                 "Name": "defaultSecurityRules/AllowVnetInBound",
                                 "Protocol": "All",
                                 "SourcePortRange": "0-65535",
                                 "DestinationPortRange": "0-65535",
                                 "SourceAddressPrefix": "VirtualNetwork",
                                 "DestinationAddressPrefix": "VirtualNetwork",
                                 "ExpandedSourceAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                 "ExpandedDestinationAddressPrefix": [
                                  "10.9.0.0/16",
                                  "168.63.129.16/32",
                                  "10.0.0.0/16",
                                  "10.1.0.0/16"
                                  ],
                                  "Access": "Allow",
                                  "Priority": 65000,
                                  "Direction": "Inbound"
                                  },…
                         ]
   
        NetworkSecurityGroup   : {
                                   "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/networkSecurityGroups/Subnet1-NSG"
                                 }
        Association            : {
                                   "Subnet": {
                                     "Id": 
                                 "/subscriptions/[Subscription ID]/resourceGroups/RG1/providers/Microsoft.Network/virtualNetworks/WestUS-VNet1/subnets/Subnet1"
                                 }
                                 }
        EffectiveSecurityRules : [
                                 {
                                "Name": "securityRules/denyRDP",
                                "Protocol": "Tcp",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "3389-3389",
                                "SourceAddressPrefix": "Internet",
                                "DestinationAddressPrefix": "0.0.0.0/0",
                                "ExpandedSourceAddressPrefix": [
                                   ... ],
                                "ExpandedDestinationAddressPrefix": [],
                                "Access": "Deny",
                                "Priority": 1000,
                                "Direction": "Inbound"
                                },
                                {
                                "Name": "defaultSecurityRules/AllowVnetInBound",
                                "Protocol": "All",
                                "SourcePortRange": "0-65535",
                                "DestinationPortRange": "0-65535",
                                "SourceAddressPrefix": "VirtualNetwork",
                                "DestinationAddressPrefix": "VirtualNetwork",
                                "ExpandedSourceAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "ExpandedDestinationAddressPrefix": [
                                "10.9.0.0/16",
                                "168.63.129.16/32",
                                "10.0.0.0/16",
                                "10.1.0.0/16"
                                ],
                                "Access": "Allow",
                                "Priority": 65000,
                                "Direction": "Inbound"
                                },...
                                ]
   
    Tenga en cuenta Hola siguiendo la información de salida de hello:
   
   * Hay dos secciones **NetworkSecurityGroup**: una está asociada a una subred (*Subnet1*) y otra está asociada a una NIC (*VM1- NIC1*). En este ejemplo, un NSG ha sido tooeach aplicada.
   * **Asociación** se muestran los recursos de hello (subred o NIC) está asociado a un NSG determinado. Si Hola recursos NSG es mover o eliminar la asociación inmediatamente antes de ejecutar este comando, puede necesitar toowait unos segundos para hello tooreflect de cambio en la salida del comando Hola. 
   * Hola nombres de las reglas que se prologa con *defaultSecurityRules*: se crea cuando un NSG, varias reglas de seguridad de forma predeterminada se crean dentro de él. Las reglas predeterminadas no se pueden quitar, pero pueden reemplazarse con reglas de prioridad más alta.
     Hola de lectura [información general NSG](virtual-networks-nsg.md#default-rules) toolearn artículo más información acerca de NSG predeterminado de las reglas de seguridad.
   * **ExpandedAddressPrefix** se expande prefijos de direcciones de Hola para las etiquetas predeterminadas NSG. Las etiquetas representan varios prefijos de direcciones. Expansión de etiquetas de hello puede ser útil al solucionar problemas de conectividad de la máquina virtual de prefijos de dirección específica. Por ejemplo, con el intercambio de tráfico de red virtual, etiqueta VIRTUAL_NETWORK expande tooshow emparejar los prefijos de red virtual en la salida anterior Hola.
     
     > [!NOTE]
     > Hola comando solo muestran efectivo reglas si un NSG está asociado a una subred, una NIC o ambos. Una máquina virtual puede tener varias NIC con diferentes NSG aplicados. Para solucionar el problema, ejecute el comando de Hola para cada NIC.
     > 
     > 
3. tooease filtrado a través de un número mayor de reglas NSG, escriba Hola después más tootroubleshoot de comandos: 
   
        $NSGs = Get-AzureRmEffectiveNetworkSecurityGroup -NetworkInterfaceName VM1-NIC1 -ResourceGroupName RG1
        $NSGs.EffectiveSecurityRules | Sort-Object Direction, Access, Priority | Out-GridView
   
    Un filtro para el tráfico RDP (puerto TCP 3389) es aplicar toohello vista de cuadrícula, como se muestra en hello después de imagen:
   
    ![Lista de reglas](./media/virtual-network-nsg-troubleshoot-powershell/rules.png)
4. Como puede ver en la vista de cuadrícula de hello, hay dos permiten y denegación las reglas para RDP. resultado del paso 2 Hello muestra ese hello *DenyRDP* regla se encuentra en hello NSG aplica toohello subred. Para las reglas de entrada, los NSG aplicados toohello subred se procesa en primer lugar. Si se encuentra una coincidencia, no se procesa la interfaz de red de hello NSG aplica toohello. En este caso, Hola *DenyRDP* regla de subred de hello bloquea RDP toohello VM (**VM1**).
   
   > [!NOTE]
   > Una máquina virtual puede tener varios tooit adjunto de NIC. Cada uno de ellos puede ser tooa conectado otra subred. Puesto que los comandos de hello en los pasos anteriores de Hola se ejecutan en una NIC, es importante tooensure que especifique Hola NIC tiene error de conectividad de Hola a. Si no está seguro, siempre puede ejecutar comandos de hello en cada máquina virtual de toohello NIC conectada.
   > 
   > 
5. tooRDP en VM1, cambio hello *denegar RDP (3389)* regla demasiado*permitir RDP(3389)* en hello **NSG subred1** NSG. Confirme que el puerto TCP 3389 está abierto abriendo una toohello de conexión RDP VM o utilizando la herramienta de PsPing Hola. Se puede obtener más información acerca de PsPing por leer hello [página de descarga de PsPing](https://technet.microsoft.com/sysinternals/psping.aspx)
   
    Puede o quitar reglas de un NSG con información de hello en la salida de hello de hello siguiente comando:
   
        Get-Help *-AzureRmNetworkSecurityRuleConfig

## <a name="considerations"></a>Consideraciones
Considere la posibilidad de hello siguientes puntos al solucionar problemas de conectividad:

* Reglas NSG predeterminadas bloqueará el acceso entrante de hello tráfico entrante de internet y sólo permitir red virtual. Las reglas deben agregarse explícitamente tooallow acceso de entrada desde Internet, según sea necesario.
* Si no hay ninguna regla de seguridad NSG causa toofail de conectividad de red de la máquina virtual, el problema de hello causa puede ser:
  * Software de firewall que se ejecuta en el sistema operativo de la máquina virtual de Hola
  * Rutas configuradas para dispositivos virtuales o para el tráfico local. Tráfico de Internet puede ser redirigido tooon local a través de tunelización forzada. Una conexión RDP/SSH de hello Internet tooyour VM no funcionen con esta configuración, dependiendo de cómo administra el hardware de red local de hello este tráfico. Hola de lectura [solución de problemas de rutas](virtual-network-routes-troubleshoot-powershell.md) artículo toolearn cómo toodiagnose dirigir los problemas que pueden ser y se impide Hola flujo de tráfico dentro y fuera de Hola máquina virtual. 
* Si ha emparejar las redes virtuales, de forma predeterminada, Hola etiqueta VIRTUAL_NETWORK expandirá automáticamente tooinclude prefijos para emparejar redes virtuales. Puede ver estos prefijos en hello **ExpandedAddressPrefix** enumerar, tootroubleshoot cualquier tooVNet relacionados problemas emparejamiento conectividad. 
* Las reglas de seguridad eficaz solo se muestran si hay que un NSG asociada a la máquina virtual de hello NIC y o subred. 
* Si no hay ningún NSG asociados con hello NIC o subred y tiene una dirección IP pública asignada tooyour VM, todos los puertos se abrirán para el acceso entrante y saliente. Si Hola máquina virtual tiene una dirección IP pública, aplicar los NSG toohello NIC o la subred se recomienda.  

