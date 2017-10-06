---
title: "depuración remota con la entrega continua aaaEnable | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooenable depuración remota al utilizar la entrega continua toodeploy tooAzure"
services: cloud-services
documentationcenter: .net
author: kraigb
manager: ghogen
editor: 
ms.assetid: 7d423639-3b2f-4ca5-ac5a-9ac19a217c29
ms.service: cloud-services
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: d9d9d1cfe5304c9526586a9164f172746a448e4e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-debugging-when-using-continuous-delivery-toopublish-tooazure"></a>Habilitar la depuración remota al utilizar la entrega continua toopublish tooAzure
Puede habilitar la depuración remota en Azure, para los servicios en la nube o máquinas virtuales, cuando se usa [la entrega continua](cloud-services-dotnet-continuous-delivery.md) toopublish tooAzure siguiendo estos pasos.

## <a name="enabling-remote-debugging-for-cloud-services"></a>Habilitación de la depuración remota para los servicios en la nube
1. En el agente de compilación de hello, configurar Hola inicial entorno de Azure como se describe en [de línea de comandos de compilación para Azure](http://msdn.microsoft.com/library/hh535755.aspx).
2. Porque se requiere para el paquete de Hola Hola tiempo de ejecución de depuración remota (msvsmon.exe), instale hello **herramientas remotas para Visual Studio**.

    * [Herramientas remotas para Visual Studio 2017](https://go.microsoft.com/fwlink/?LinkId=746570)
    * [Herramientas remotas para Visual Studio 2015](https://go.microsoft.com/fwlink/?LinkId=615470)
    * [Herramientas remotas para Visual Studio 2013 Update 5](https://www.microsoft.com/download/details.aspx?id=48156)
    
    Como alternativa, puede copiar los archivos binarios de depuración remota de Hola desde un sistema que tiene instalado Visual Studio.

3. Cree un certificado como se describe en [Información general de los certificados para los servicios en la nube de Azure](cloud-services-certs-create.md). Mantener .pfx hello y huella digital del certificado RDP y cargar el servicio de nube de destino de hello certificado toohello.
4. Usar hello siguientes opciones en toobuild de línea de comandos de MSBuild Hola y el paquete con la depuración remota habilitada. (Sustituya los archivos de proyecto y del sistema de tooyour en las rutas de acceso real para los elementos entre corchetes angulares de hello).
   
        msbuild /TARGET:PUBLISH /PROPERTY:Configuration=Debug;EnableRemoteDebugger=true;VSX64RemoteDebuggerPath="<remote tools path>";RemoteDebuggerConnectorCertificateThumbprint="<thumbprint of hello certificate added toohello cloud service>";RemoteDebuggerConnectorVersion="2.7" "<path tooyour VS solution file>"
   
    `VSX64RemoteDebuggerPath`es toohello carpetas de hello ruta de acceso que contiene msvsmon.exe en Hola de herramientas remotas para Visual Studio.
    `RemoteDebuggerConnectorVersion`es la versión de SDK de Azure de hello en el servicio de nube. También debe coincidir con versión de Hola que se instala con Visual Studio.
5. Publicar toohello servicio de nube de destino mediante el archivo de paquete y .cscfg de hello generado en el paso anterior de Hola.
6. Importar máquina Hola de toohello del certificado (archivo .pfx) que tiene Visual Studio con Azure SDK para .NET instalado. Asegúrese de que toohello tooimport `CurrentUser\My` almacén de certificados, en caso contrario, adjuntar depurador toohello en Visual Studio se producirá un error.

## <a name="enabling-remote-debugging-for-virtual-machines"></a>Habilitación de la depuración remota para las máquinas virtuales
1. Cree una máquina virtual de Azure. Consulte [Creación de una máquina virtual que ejecuta Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) o [Creación y administración de máquinas virtuales de Azure en Visual Studio](../virtual-machines/windows/classic/manage-visual-studio.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).
2. En hello [página del portal de Azure clásico](http://go.microsoft.com/fwlink/p/?LinkID=269851), ver panel toosee Hola máquinas virtuales del Hola máquinas virtuales **huella digital del certificado de RDP**. Este valor se utiliza para hello `ServerThumbprint` valor de configuración de la extensión de Hola.
3. Crear un certificado de cliente, tal como se describe en [Introducción a los certificados para servicios en la nube](cloud-services-certs-create.md) (mantenga Hola .pfx y la huella digital de certificado RDP).
4. Instalar Azure Powershell (versión 0.7.4 o posterior) como se describe en [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).
5. Ejecute hello después de la extensión de script tooenable hello RemoteDebug. Reemplace las rutas de acceso de Hola y sus datos personales con su cuenta, como el nombre de suscripción, el nombre del servicio y la huella digital.
   
   > [!NOTE]
   > Este script está configurado para Visual Studio 2015. Si usa Visual Studio 2013 o Visual Studio de 2017, modificar hello `$referenceName` y `$extensionName` asignaciones siguiente demasiado`RemoteDebugVS2013` o `RemoteDebugVS2017`.

    ```powershell   
    Add-AzureAccount

    Select-AzureSubscription "My Microsoft Subscription"

    $vm = Get-AzureVM -ServiceName "mytestvm1" -Name "mytestvm1"

    $endpoints = @(
                    ,@{Name="RDConnVS2013"; PublicPort=30400; PrivatePort=30398}
                    ,@{Name="RDFwdrVS2013"; PublicPort=31400; PrivatePort=31398}
                )

    foreach($endpoint in $endpoints)
    {
        Add-AzureEndpoint -VM $vm -Name $endpoint.Name -Protocol tcp -PublicPort $endpoint.PublicPort -LocalPort $endpoint.PrivatePort
    }

    $referenceName = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug.RemoteDebugVS2015"
    $publisher = "Microsoft.VisualStudio.WindowsAzure.RemoteDebug"
    $extensionName = "RemoteDebugVS2015"
    $version = "1.*"
    $publicConfiguration = "<PublicConfig><Connector.Enabled>true</Connector.Enabled><ClientThumbprint>56D7D1B25B472268E332F7FC0C87286458BFB6B2</ClientThumbprint><ServerThumbprint>E7DCB00CB916C468CC3228261D6E4EE45C8ED3C6</ServerThumbprint><ConnectorPort>30398</ConnectorPort><ForwarderPort>31398</ForwarderPort></PublicConfig>"

    $vm | Set-AzureVMExtension -ReferenceName $referenceName -Publisher $publisher -ExtensionName $extensionName -Version $version -PublicConfiguration $publicConfiguration

    foreach($extension in $vm.VM.ResourceExtensionReferences)
    {
        if(($extension.ReferenceName -eq $referenceName) `
        -and ($extension.Publisher -eq $publisher) `
        -and ($extension.Name -eq $extensionName) `
        -and ($extension.Version -eq $version))
        {
            $extension.ResourceExtensionParameterValues[0].Key = 'config.txt'
            break
        }
    }

    $vm | Update-AzureVM
    ```

6. Importar máquina Hola de toohello del certificado (.pfx) que tiene Visual Studio con Azure SDK para .NET instalado.

