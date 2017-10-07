---
title: plantillas de Azure Resource Manager aaaUse en pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo toouse plantillas de Azure Resource Manager en recursos de tooprovision de pila de Azure."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 2022dbe5-47fd-457d-9af3-6c01688171d7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: bcc73756fa712ecff9791301d43d227112be8362
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-resource-manager-templates-in-azure-stack"></a>Uso de plantillas de Administrador de recursos de Azure en Azure Stack
Plantillas de administrador de recursos de Azure implementación y aprovisionar todos los recursos de Hola para su aplicación en una única operación coordinada. También puede volver a implementar plantillas toomake cambios toohello recursos en grupo de recursos de Hola.

Estas plantillas se pueden implementar con el portal de Microsoft Azure pila hello, PowerShell, línea de comandos de Hola y Visual Studio.

Después de plantillas de inicio rápido de Hello está disponible en [GitHub](http://aka.ms/azurestackgithub):

## <a name="deploy-sharepoint-non-high-availability"></a>Implementación de SharePoint (sin alta disponibilidad)
Usar Hola granja de toocreate un servidor de SharePoint 2013 de extensión de DSC de PowerShell que incluye Hola recursos siguientes:

* Una red virtual
* Tres cuentas de almacenamiento
* Dos equilibradores de carga externos
* Una máquina virtual configurada como controlador de dominio para un nuevo bosque con un único dominio
* Una máquina virtual configurada como un servidor independiente de SQL Server 2014
* Una máquina virtual configurada como una granja de servidores de SharePoint 2013 de la máquina

## <a name="deploy-ad-non-high-availability"></a>Implementación de AD (sin alta disponibilidad)
Utilice toocreate de extensión de DSC de PowerShell de hello un servidor de controlador de dominio de AD que incluye Hola recursos siguientes:

* Una red virtual
* Una cuenta de almacenamiento
* Un equilibrador de carga externo
* Una máquina virtual configurada como controlador de dominio para un nuevo bosque con un único dominio

## <a name="deploy-adsql-non-high-availability"></a>Implementación de AD/SQL (sin alta disponibilidad)
Usar Hola DSC de PowerShell extensión toocreate un SQL Server 2014 server independiente que incluye Hola recursos siguientes:

* Una red virtual
* Dos cuentas de almacenamiento
* Un equilibrador de carga externo
* Una máquina virtual configurada como controlador de dominio para un nuevo bosque con un único dominio
* Una máquina virtual configurada como un servidor independiente de SQL Server 2014

## <a name="vm-dsc-extension-azure-automation-pull-server"></a>Extensión DSC de máquina virtual para un servidor de extracción de Automatización de Azure
Utilice tooconfigure de extensión de DSC de PowerShell de hello una máquina virtual existente Administrador de configuración Local (LCM) y registrar tooan servidor de extracción de DSC de Azure automatización de la cuenta.

## <a name="create-a-virtual-machine-from-a-user-image"></a>Creación de una máquina virtual desde una imagen de usuario
Cree una máquina virtual desde una imagen de usuario personalizada. Esta plantilla también implementa una red virtual (con DNS), una dirección IP pública y una interfaz de red.

## <a name="simple-vm"></a>VM simple
Implemente una máquina virtual de Windows que incluya una red virtual (con DNS), una dirección IP pública y una interfaz de red.

## <a name="cancel-a-running-template-deployment"></a>Cancelación de una implementación de la plantilla en ejecución
toocancel una implementación de plantilla de ejecución, utilice hello `Stop-AzureRmResourceGroupDeployment` cmdlet de PowerShell.

## <a name="next-steps"></a>Pasos siguientes
[Implementación de plantillas con el portal de Hola](azure-stack-deploy-template-portal.md)

[Información general sobre Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)

