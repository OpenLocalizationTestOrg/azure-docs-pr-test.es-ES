---
title: "aaaAzure supervisión y máquinas virtuales de Windows | Documentos de Microsoft"
description: "Tutorial: Supervisar una máquina virtual Windows con Azure PowerShell"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/04/2017
ms.author: davidmu
ms.custom: mvc
ms.openlocfilehash: 191dc5a30d41c25a9e38f8ec2a32efdc05e03015
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-a-windows-virtual-machine-with-azure-powershell"></a>Supervisar una máquina virtual Windows con Azure PowerShell

Supervisión de Azure usa arranque toocollect de agentes y los datos de rendimiento de las máquinas virtuales de Azure, almacenar estos datos en el almacenamiento de Azure y hacerla accesible a través del portal, módulo de PowerShell de Azure de Hola y Hola CLI de Azure. En este tutorial, aprenderá a:

> [!div class="checklist"]
> * Habilitar los diagnósticos de arranque en una máquina virtual
> * Ver los diagnósticos de arranque
> * Ver las métricas del host de la máquina virtual
> * Instalar extensión de diagnósticos de Hola
> * Ver las métricas de la máquina virtual
> * Crear una alerta
> * Configurar la supervisión avanzada

Este tutorial requiere hello Azure PowerShell versión 3.6 o posterior del módulo. Ejecutar ` Get-Module -ListAvailable AzureRM` toofind versión de Hola. Si necesita tooupgrade, consulte [módulo instalar Azure PowerShell](/powershell/azure/install-azurerm-ps).

ejemplo de Hola a toocomplete en este tutorial, debe tener una máquina virtual existente. Si es necesario, este [script de ejemplo](../scripts/virtual-machines-windows-powershell-sample-create-vm.md) puede crear una. Al trabajar con el tutorial de hello, reemplace el grupo de recursos de hello, el nombre de máquina virtual y la ubicación donde sea necesario.

## <a name="view-boot-diagnostics"></a>Ver los diagnósticos de arranque

Máquinas virtuales de Windows arrancar, agente de diagnóstico de arranque de hello captura salida de pantalla que se puede usar para solucionar problemas de uso. Esta funcionalidad está habilitada de forma predeterminada. Hola captura pantalla capturas se almacenan en una cuenta de almacenamiento de Azure, que también se crea de forma predeterminada. 

Puede obtener datos de diagnóstico de arranque de hello con hello [Get AzureRmVMBootDiagnosticsData](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmbootdiagnosticsdata) comando. En el siguiente ejemplo de Hola, diagnóstico de arranque es la raíz de toohello descargado de Hola * c:\* unidad. 

```powershell
Get-AzureRmVMBootDiagnosticsData -ResourceGroupName myResourceGroup -Name myVM -Windows -LocalPath "c:\"
```

## <a name="view-host-metrics"></a>Visualización de las métricas del host

Una máquina virtual Windows tiene una máquina virtual host dedicada en Azure con la que interactúa. Las métricas se recopilan automáticamente para hello Host y pueden verse en hello portal de Azure.

1. Hola portal de Azure, haga clic en **grupos de recursos**, seleccione **myResourceGroup**y, a continuación, seleccione **myVM** en la lista de recursos de Hola.
2. Haga clic en **métricas** en Hola hoja de la máquina virtual y, a continuación, seleccione cualquiera de las métricas de Host de hello en **métricas disponibles** toosee el rendimiento de hello máquina virtual de Host.

    ![Visualización de las métricas del host](./media/tutorial-monitoring/tutorial-monitor-host-metrics.png)

## <a name="install-diagnostics-extension"></a>Instalar la extensión de Diagnostics

métricas de host básica Hello están disponibles, pero toosee más granular y métricas específica de la máquina virtual, se tooneed tooinstall hello Azure extensión de diagnósticos en hello VM. Hola extensión de diagnósticos de Azure permite toobe de datos de diagnóstico recuperados de hello VM y supervisión adicional. Puede ver estas métricas de rendimiento y crear alertas basadas en cómo realiza Hola máquina virtual. extensión de diagnóstico de Hola se instala a través de hello portal de Azure como sigue:

1. Hola portal de Azure, haga clic en **grupos de recursos**, seleccione **myResourceGroup**y, a continuación, seleccione **myVM** en la lista de recursos de Hola.
2. Haga clic en **Configuración de diagnóstico**. lista de Hello muestra que *diagnósticos de arranque* ya están habilitados desde la sección anterior de Hola. Haga clic en la casilla de verificación hello *métricas básicas*.
3. Haga clic en hello **habilitar la supervisión de nivel de invitado** botón.

    ![Ver métricas de diagnósticos](./media/tutorial-monitoring/enable-diagnostics-extension.png)

## <a name="view-vm-metrics"></a>Ver las métricas de la máquina virtual

Puede ver las métricas de máquina virtual de Hola Hola igual que ver las métricas de máquina virtual de host de hello:

1. Hola portal de Azure, haga clic en **grupos de recursos**, seleccione **myResourceGroup**y, a continuación, seleccione **myVM** en la lista de recursos de Hola.
2. toosee cómo está realizando Hola VM, haga clic en **métricas** en Hola hoja de la máquina virtual y, a continuación, seleccione cualquiera de las métricas de diagnóstico de hello en **métricas disponibles**.

    ![Ver las métricas de la máquina virtual](./media/tutorial-monitoring/monitor-vm-metrics.png)

## <a name="create-alerts"></a>Creación de alertas

Puede crear alertas basadas en métricas de rendimiento concretas. Las alertas pueden ser usado toonotify cuando uso medio de CPU supera un determinado umbral o espacio en disco disponible cae por debajo de una determinada cantidad, por ejemplo. Las alertas se muestran en el portal de Azure de Hola o se pueden enviar por correo electrónico. También puede desencadenar runbooks de automatización de Azure o las aplicaciones lógicas de Azure en tooalerts de respuesta que se está generando.

Hello en el ejemplo siguiente se crea una alerta para el uso medio de CPU.

1. Hola portal de Azure, haga clic en **grupos de recursos**, seleccione **myResourceGroup**y, a continuación, seleccione **myVM** en la lista de recursos de Hola.
2. Haga clic en **reglas de alerta** en la hoja de la máquina virtual de hello, a continuación, haga clic en **Agregar alerta métrica** a través de la parte superior de Hola de hoja de alertas de Hola.
4. Especifique un **nombre** para la alerta, como *myAlertRule*.
5. tootrigger una alerta cuando el porcentaje de CPU supera 1.0 durante cinco minutos, deje Hola todos los demás valores predeterminados seleccionados.
6. Si lo desea, active casilla de Hola para *correo electrónico a los propietarios, contributors y readers* toosend notificación de correo electrónico. acción predeterminada de Hello es toopresent una notificación en el portal de Hola.
7. Haga clic en hello **Aceptar** botón.

## <a name="advanced-monitoring"></a>Supervisión avanzada 

Mediante [Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) se puede realizar una supervisión más avanzada de la máquina virtual. Si aún no lo ha hecho, puede suscribirse para disfrutar de una [evaluación gratuita](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-trial) de Operations Management Suite.

Cuando se tiene acceso toohello OMS portal, puede encontrar identificador de clave y el área de trabajo del área de trabajo de hello en la hoja de configuración de Hola. Hola de uso [conjunto AzureRmVMExtension](https://docs.microsoft.com/powershell/module/azurerm.compute/set-azurermvmextension) suministra tootooadd Hola OMS extensión toohello máquina virtual. Actualización Hola valores de las variables en hello debajo de ejemplo tooreflect, Id. de área de trabajo y clave de área de trabajo OMS  

```powershell
$omsId = "<Replace with your OMS Id>"
$omsKey = "<Replace with your OMS key>"

Set-AzureRmVMExtension -ResourceGroupName myResourceGroup `
  -ExtensionName "Microsoft.EnterpriseCloud.Monitoring" `
  -VMName myVM `
  -Publisher "Microsoft.EnterpriseCloud.Monitoring" `
  -ExtensionType "MicrosoftMonitoringAgent" `
  -TypeHandlerVersion 1.0 `
  -Settings @{"workspaceId" = $omsId} `
  -ProtectedSettings @{"workspaceKey" = $omsKey} `
  -Location eastus
```

Después de unos minutos, debería ver Hola nueva máquina virtual en el área de trabajo OMS Hola. 

![Hoja OMS](./media/tutorial-monitoring/tutorial-monitor-oms.png)

## <a name="next-steps"></a>Pasos siguientes
En este tutorial, ha configurado y revisado las máquinas virtuales con Azure Security Center. Ha aprendido a:

> [!div class="checklist"]
> * Crear una red virtual
> * Crear un grupo de recursos y una máquina virtual 
> * Habilitar los diagnósticos de arranque en hello VM
> * Ver los diagnósticos de arranque
> * Visualización de las métricas del host
> * Instalar extensión de diagnósticos de Hola
> * Ver las métricas de la máquina virtual
> * Crear una alerta
> * Configurar la supervisión avanzada

Avanzar toohello siguiente toolearn de tutorial acerca del centro de seguridad de Azure.

> [!div class="nextstepaction"]
> [Administración de la seguridad de máquinas virtuales](./tutorial-azure-security.md)