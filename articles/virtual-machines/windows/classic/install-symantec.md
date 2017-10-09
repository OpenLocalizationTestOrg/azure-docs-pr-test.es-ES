---
title: "aaaInstall Symantec Endpoint Protection en una máquina virtual de Windows en Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooinstall y configure la extensión de seguridad de Symantec Endpoint Protection de hello en un nuevo o VM de Azure existente creado con el modelo de implementación clásica de Hola."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 19dcebc7-da6b-4510-907b-d64088e81fa2
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: iainfou
ms.openlocfilehash: cb6083366185c26c9f43ff94d835cd90725de5b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-symantec-endpoint-protection-on-a-windows-vm"></a>¿Cómo tooinstall y configurar Symantec Endpoint Protection en una VM de Windows
> [!IMPORTANT] 
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

Este artículo muestra cómo tooinstall y configurar el cliente de Symantec Endpoint Protection de hello en una máquina virtual (VM) existente con Windows Server. Este es el cliente completo, que incluye servicios como protección contra virus y spyware, firewall y prevención de intrusiones. cliente de Hola se instala como una extensión de seguridad mediante el uso de hello agente de máquina virtual.

Si tiene una suscripción de Symantec para una solución local, se puede usar tooprotect máquinas virtuales de Azure. Si todavía no es cliente, puede suscribirse para una prueba. Para obtener más información sobre esta solución, consulte [Symantec Endpoint Protection en la plataforma de Microsoft Azure][Symantec]. Esta página también contiene información de toolicensing vínculos e instrucciones para instalar el cliente de hello si ya tiene un cliente de Symantec.

## <a name="install-symantec-endpoint-protection-on-an-existing-vm"></a>Instalación de Symantec Endpoint Protection en una máquina virtual existente
Antes de empezar, necesita Hola siguiente:

* módulo de PowerShell de Azure de Hello, versión 0.8.2 o posterior, en el equipo de trabajo. Puede comprobar la versión de Hola de PowerShell de Azure que ha instalado con hello **Get-Module azure | versión de formato de tabla** comando. Para obtener instrucciones y una versión más reciente de toohello de vínculo, vea [cómo tooInstall y configurar Azure PowerShell][PS]. Inicie sesión con suscripción de Azure de tooyour `Add-AzureAccount`.
* Hola Hola de agente de máquina virtual que se ejecuta en máquinas virtuales de Azure.

En primer lugar, compruebe que Hola que ya está instalado el agente de máquina virtual en la máquina virtual de Hola. Rellene el nombre del servicio de nube de Hola y el nombre de la máquina virtual y, a continuación, ejecute hello siga los comandos en un símbolo de PowerShell de Azure de nivel de administrador. Reemplace todo el contenido de las comillas de hello, incluidos los caracteres de Hola < y >.

> [!TIP]
> Si no conoce el servicio de nube de Hola y nombres de máquina virtual, ejecute **Get-AzureVM** nombres de hello toolist para todas las máquinas virtuales en su suscripción actual.

```powershell
$CSName = "<cloud service name>"
$VMName = "<virtual machine name>"
$vm = Get-AzureVM -ServiceName $CSName -Name $VMName
write-host $vm.VM.ProvisionGuestAgent
```

Si hello **escritura host** comando muestra **True**, Hola está instalado el agente de máquina virtual. Si muestra **False**, consulte las instrucciones de Hola y un toohello vínculo Descargar en la entrada de blog de Azure de hello [agente de máquina virtual y extensiones: parte 2][Agent].

Si está instalado Hola agente de máquina virtual, ejecútelo estos comandos tooinstall Hola Symantec Endpoint Protection.

```powershell
$Agent = Get-AzureVMAvailableExtension -Publisher Symantec -ExtensionName SymantecEndpointProtection

Set-AzureVMExtension -Publisher Symantec –Version $Agent.Version -ExtensionName SymantecEndpointProtection \
    -VM $vm | Update-AzureVM
```

tooverify que Hola Symantec extensión de seguridad se ha instalado y está actualizada:

1. Inicie sesión en la máquina virtual de toohello. Para obtener instrucciones, consulte [cómo tooLog en la máquina Virtual que ejecuta Windows Server tooa][Logon].
2. Para Windows Server 2008 R2, haga clic en **Inicio > Symantec Endpoint Protection**. Para Windows Server 2012 o Windows Server 2012 R2, desde la pantalla de inicio de bienvenida, escriba **Symantec**y, a continuación, haga clic en **Symantec Endpoint Protection**.
3. De hello **estado** ficha de hello **estado Symantec Endpoint Protection** ventana, aplicar actualizaciones o reinicie si es necesario.

## <a name="additional-resources"></a>Recursos adicionales
[¿Cómo tooLog en tooa Máquina Virtual que ejecuta Windows Server][Logon]

[Características y extensiones de máquina virtual de Azure][Ext]

<!--Link references-->
[Symantec]: http://www.symantec.com/connect/blogs/symantec-endpoint-protection-now-microsoft-azure

[Create]:tutorial.md

[PS]: /powershell/azureps-cmdlets-docs

[Agent]: http://go.microsoft.com/fwlink/p/?LinkId=403947

[Logon]:connect-logon.md

[Ext]: http://go.microsoft.com/fwlink/p/?linkid=390493
