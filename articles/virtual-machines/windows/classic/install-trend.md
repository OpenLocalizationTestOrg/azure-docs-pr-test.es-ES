---
title: "aaaInstall trendmicro Deep Security en una máquina virtual | Documentos de Microsoft"
description: "Este artículo se describe cómo tooinstall y configurar la seguridad de Trend Micro en una máquina virtual creada con el modelo de implementación clásica de hello en Azure."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: e991b635-f1e2-483f-b7ca-9d53e7c22e2a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: iainfou
ms.openlocfilehash: dc5492db07a37a2296df5da673183a14c6d5b1f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-trend-micro-deep-security-as-a-service-on-a-windows-vm"></a>¿Cómo tooinstall y configurar trendmicro Deep Security como un servicio en una VM de Windows
> [!IMPORTANT]
> Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md). Este artículo tratan con modelo de implementación de hello clásico. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.

Este artículo muestra cómo tooinstall y configurar trendmicro Deep Security como un servicio en una existente o nueva máquina virtual (VM) con Windows Server. Deep Security como servicio proporciona protección antimalware, firewall, sistema de prevención contra intrusiones y supervisión de integridad.

Hola cliente se instala como una extensión de seguridad a través de hello agente de máquina virtual. En una nueva máquina virtual, instale Hola Deep Security Agent, como Hola que Hola portal de Azure crea automáticamente el agente de máquina virtual.

Una máquina virtual existente que se creó mediante el portal clásico de hello, hello Azure CLI o PowerShell podría no tener un agente de máquina virtual. Para una máquina virtual existente que no tenga Hola agente de máquina virtual, es necesario toodownload y, a continuación, deberá instalarlo primero. Este artículo trata ambas situaciones.

Si tiene una suscripción de Trend Micro actual para una solución local, se puede usar toohelp proteger máquinas virtuales de Azure. Si todavía no es cliente, puede suscribirse para una prueba. Para obtener más información sobre esta solución, consulte Hola Trend Micro entrada de blog [Microsoft Azure VM Agent extensión para Deep Security](http://go.microsoft.com/fwlink/p/?LinkId=403945).

## <a name="install-hello-deep-security-agent-on-a-new-vm"></a>Instalar Hola Deep Security Agent en una nueva máquina virtual

Hola [portal de Azure](http://portal.azure.com) le permite instalar la extensión de seguridad de Trend Micro hello cuando se usa una imagen de hello **Marketplace** máquina virtual de toocreate Hola. Si va a crear una única máquina virtual, usar el portal de hello es una protección de tooadd de manera sencilla de Trend Micro.

Uso de una entrada de hello **Marketplace** abre un asistente que le ayuda a configura la máquina virtual de Hola. Usar hello **configuración** hoja, el tercer panel del Asistente para hello, tooinstall Hola extensión de seguridad de Trend Micro de Hola.  Para obtener instrucciones generales, vea [crear una máquina virtual que ejecuta Windows en el portal de Azure hello](tutorial.md).

Al obtener toohello **configuración** Hola hoja del Asistente para hello, lo siguiente:

1. Haga clic en **extensiones**, a continuación, haga clic en **Agregar extensión** en panel siguiente Hola.

   ![Empezar a agregar la extensión de Hola][1]

2. Seleccione **Deep Security Agent** en hello **nuevo recurso** panel. En el panel de Deep Security Agent hello, haga clic en **crear**.

   ![Identificar agente de Deep Security][2]

3. Escriba hello **identificador del inquilino** y **contraseña de activación del inquilino** para extensión de Hola. Opcionalmente, puede especificar un **identificador de directiva de seguridad**. A continuación, haga clic en **Aceptar** cliente de hello tooadd.

   ![Proporcionar detalles de la extensión][3]

## <a name="install-hello-deep-security-agent-on-an-existing-vm"></a>Instalar Hola Deep Security Agent en una máquina virtual existente
agente de hello tooinstall en una máquina virtual existente, debe Hola siguientes elementos:

* módulo de PowerShell de Azure de Hello, versión 0.8.2 o posterior, instalado en el equipo local. Puede comprobar la versión de PowerShell de Azure que ha instalado mediante Hola Hola **Get-Module azure | versión de formato de tabla** comando. Para obtener instrucciones y una versión más reciente de toohello de vínculo, vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview). Inicie sesión con suscripción de Azure de tooyour `Add-AzureAccount`.
* Agente de VM instalado en la máquina virtual de destino de Hola Hola.

En primer lugar, compruebe que Hola que ya está instalado el agente de máquina virtual. Rellene el nombre del servicio de nube de Hola y el nombre de la máquina virtual y, a continuación, ejecute hello siga los comandos en un símbolo de PowerShell de Azure de nivel de administrador. Reemplace todo el contenido de las comillas de hello, incluidos los caracteres de Hola < y >.

    $CSName = "<cloud service name>"
    $VMName = "<virtual machine name>"
    $vm = Get-AzureVM -ServiceName $CSName -Name $VMName
    write-host $vm.VM.ProvisionGuestAgent

Si no conoce el servicio de nube de Hola y el nombre de la máquina virtual, ejecute **Get-AzureVM** toodisplay que Hola a información para todas las máquinas virtuales en su suscripción actual.

Si hello **escritura host** comando devuelve **True**, Hola está instalado el agente de máquina virtual. Si devuelve **False**, consulte las instrucciones de Hola y un toohello vínculo Descargar en la entrada de blog de Azure de hello [agente de máquina virtual y extensiones: parte 2](http://go.microsoft.com/fwlink/p/?LinkId=403947).

Si está instalado Hola agente de máquina virtual, ejecute estos comandos.

    $Agent = Get-AzureVMAvailableExtension TrendMicro.DeepSecurity -ExtensionName TrendMicroDSA

    Set-AzureVMExtension -Publisher TrendMicro.DeepSecurity –Version $Agent.Version -ExtensionName TrendMicroDSA -VM $vm | Update-AzureVM

## <a name="next-steps"></a>Pasos siguientes
Se tarda unos minutos para hello agente toostart ejecutando cuando se instala. Después de eso, necesita tooactivate Deep Security en la máquina virtual de Hola para poder ser administrado por un administrador de seguridad profundo. Vea Hola siguientes artículos para obtener instrucciones adicionales:

* Artículo de Trend sobre esta solución, [Instant-On Cloud Security for Microsoft Azure (Seguridad en la nube instantánea para Microsoft Azure)](http://go.microsoft.com/fwlink/?LinkId=404101)
* A [script de Windows PowerShell de ejemplo](http://go.microsoft.com/fwlink/?LinkId=404100) máquina virtual de tooconfigure Hola
* [Instrucciones](http://go.microsoft.com/fwlink/?LinkId=404099) de ejemplo de Hola

## <a name="additional-resources"></a>Recursos adicionales
[¿Cómo toolog en la máquina virtual de tooa ejecuta Windows Server]

[Características y extensiones de máquina virtual de Azure]

<!-- Image references -->
[1]: ./media/install-trend/new_vm_Blade3.png
[2]: ./media/install-trend/find_SecurityAgent.png
[3]: ./media/install-trend/SecurityAgentDetails.png

<!-- Link references -->
[¿Cómo toolog en la máquina virtual de tooa ejecuta Windows Server]:connect-logon.md
[Características y extensiones de máquina virtual de Azure]: http://go.microsoft.com/fwlink/p/?linkid=390493&clcid=0x409
