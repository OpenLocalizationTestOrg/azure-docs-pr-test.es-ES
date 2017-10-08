---
title: marketplace de aaaAdd Hola predeterminado VM imagen toohello pila de Azure | Documentos de Microsoft
description: "Agregue el catálogo de soluciones de hello VM de Windows Server 2016 predeterminada imagen toohello pila de Azure."
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 9b5a6f4e4c73c706b059e3c3622a968b5eef9a27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-hello-windows-server-2016-vm-image-toohello-azure-stack-marketplace"></a>Agregue el catálogo de soluciones de hello VM de Windows Server 2016 imagen toohello pila de Azure

De forma predeterminada, no hay ninguna imagen de máquina virtual disponible en marketplace de hello pila de Azure. Administrador de la nube de Hello Azure pila debe agregar un marketplace de toohello imagen antes de que los usuarios puedan usarlos. Puede agregar el catálogo de soluciones de Windows Server 2016 Hola imagen toohello pila de Azure mediante uno de hello siguiendo dos métodos:

* [Agregar imagen de hello descargándolo desde hello Azure Marketplace](#add-the-image-by-downloading-it-from-the-Azure-marketplace) -Utilice esta opción si está trabajando en un escenario conectado y si se ha registrado la instancia de la pila de Azure con Azure.

* [Agregar imagen de hello mediante PowerShell](#add-the-image-by-using-powershell) -Utilice esta opción si ha implementado en una situación sin conexión o en escenarios de pila de Azure con conectividad limitada.

## <a name="add-hello-image-by-downloading-it-from-hello-azure-marketplace"></a>Agregar imagen de hello descargándolo desde hello Azure Marketplace

1. Después de implementar la pila de Azure, inicie sesión en tooyour Kit de desarrollo de pila de Azure.

2. Haga clic en **Más servicios** > **Marketplace Management** (Administración de Marketplace)  > **Add from Azure** (Agregar desde Azure). 

3. Buscar o buscar hello **centro de datos de Windows Server 2016: Eval** imagen > haga clic en **descargar**

   ![Descarga de la imagen desde Azure](media/azure-stack-add-default-image/download-image.png)

Una vez finalizada la descarga de hello, imagen Hola se agrega toohello **Marketplace administración** hoja y se pone a disposición de hello **máquinas virtuales** hoja.

## <a name="add-hello-image-by-using-powershell"></a>Agregar imagen de hello mediante PowerShell

### <a name="prerequisites"></a>Requisitos previos 

Ejecute hello siguiendo los requisitos previos de hello [kit de desarrollo de](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), o desde un cliente externo basado en Windows si está [conectado a través de VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn):

* Instale los [módulos de Azure PowerShell compatibles con Azure Stack](azure-stack-powershell-install.md).  

* Descargar hello [toowork necesarios de herramientas con la pila de Azure](azure-stack-powershell-download.md).  

* Vaya toohttps://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016 y descargar la evaluación de Windows Server 2016 Hola. Cuando se le pida, seleccione hello **ISO** versión de descarga de Hola. Toohello de ruta de acceso de registro Hola descargar ubicación, que se utiliza más adelante en estos pasos. Este paso requiere conectividad a Internet.  

Ahora ejecute hello después de marketplace de pasos tooadd Hola imagen toohello pila de Azure:
   
1. Importar módulos de Azure Connect de pila y ComputeAdmin de hello mediante el uso de hello siguientes comandos:

   ```powershell
   Set-ExecutionPolicy RemoteSigned

   # import hello Connect and ComputeAdmin modules   
   Import-Module .\Connect\AzureStack.Connect.psm1
   Import-Module .\ComputeAdmin\AzureStack.ComputeAdmin.psm1

   ```

2. Inicie sesión en tooyour entorno de pila de Azure. Siguiente ejecución Hola secuencias de comandos en función de si su entorno de pila de Azure se implementa mediante el uso de AAD o AD FS (nombre de inquilino AAD de marca tooreplace seguro hello):  

   a. **Azure Active Directory**, usar hello siguiente cmdlet:

   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

   Set-AzureRmEnvironment `
    -Name "AzureStackAdmin" `
    -GraphAudience "https://graph.windows.net/"

   $TenantID = Get-AzsDirectoryTenantId `
     -AADTenantName "<myDirectoryTenantName>.onmicrosoft.com" `
     -EnvironmentName AzureStackAdmin

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```

   b. **Los servicios de federación de Active Directory**, usar hello siguiente cmdlet:
    
   ```PowerShell
   # Create hello Azure Stack cloud administrator's AzureRM environment by using hello following cmdlet:
   Add-AzureRMEnvironment `
     -Name "AzureStackAdmin" `
     -ArmEndpoint "https://adminmanagement.local.azurestack.external"

   Set-AzureRmEnvironment `
     -Name "AzureStackAdmin" `
     -GraphAudience "https://graph.local.azurestack.external/" `
     -EnableAdfsAuthentication:$true

   $TenantID = Get-AzsDirectoryTenantId `
     -ADFS 
     -EnvironmentName AzureStackAdmin 

   Login-AzureRmAccount `
     -EnvironmentName "AzureStackAdmin" `
     -TenantId $TenantID 
   ```
   
3. Agregar el catálogo de soluciones de Windows Server 2016 Hola imagen toohello pila de Azure (asegúrese de que tooreplace hello *Path_to_ISO* con toohello de ruta de acceso de hello ISO WS2016 descargó):

   ```PowerShell
   $ISOPath = "<Fully_Qualified_Path_to_ISO>"

   # Add a Windows Server 2016 Evaluation VM Image.
   New-AzsServer2016VMImage `
     -ISOPath $ISOPath

   ```

tooensure que Hola imagen de máquina virtual de Windows Server 2016 tiene Hola actualización acumulativa más reciente, incluyen hello `IncludeLatestCU` parámetro al ejecutar hello `New-AzsServer2016VMImage` cmdlet. Vea hello [parámetros](#parameters) sección para obtener información acerca de los parámetros permitidos para hello `New-AzsServer2016VMImage` cmdlet. Se tarda aproximadamente un mercado hora toopublish Hola imagen toohello pila de Azure. 

## <a name="parameters"></a>parameters

|Parámetros de New-AzsServer2016VMImage|¿Necesario?|Descripción|
|-----|-----|------|
|ISOPath|Sí|Hello toohello de ruta de acceso completa descarga Windows Server 2016 ISO.|
|Net35|No|Este parámetro permite tooinstall Hola .NET 3.5 runtime en la imagen de Windows Server 2016 Hola. De forma predeterminada, este valor se establece tootrue. Es obligatorio que esa imagen hello contiene Hola 3.5 de .NET en tiempo de ejecución tooinstall Hola SQL y MYSQL proveedores de recursos. |
|Versión|No|Este parámetro permite toochoose si tooadd una **Core** o **completa** o **ambos** imágenes de Windows Server 2016. De forma predeterminada, este valor se establece demasiado "Full".|
|VHDSizeInMB|No|Establece el tamaño de hello (en MB) de toobe de imagen de disco duro virtual de hello agrega entorno de Azure pila tooyour. De forma predeterminada, este valor se establece too40960 MB.|
|CreateGalleryItem|No|Especifica si se debe crear un elemento de Marketplace de imagen de Windows Server 2016 Hola. De forma predeterminada, este valor se establece tootrue.|
|location |No |Especifica la imagen de Windows Server 2016 de hello ubicación toowhich Hola debe publicarse.|
|IncludeLatestCU|No|Establecer este modificador tooapply hello más reciente Windows Server 2016 actualización acumulativa toohello nuevo disco duro virtual.|
|CUUri |No |Establecer esta actualización acumulativa de valor toochoose Hola Windows Server 2016 desde un URI concreto. |
|CUPath |No |Establecer esta actualización acumulativa de valor toochoose Hola Windows Server 2016 desde una ruta de acceso local. Esta opción es útil si ha implementado la instancia de la pila de Azure de hello en un entorno desconectado.|

## <a name="next-steps"></a>Pasos siguientes

[Aprovisionamiento de una máquina virtual](azure-stack-provision-vm.md)
