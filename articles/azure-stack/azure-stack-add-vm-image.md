---
title: "aaaAdding una máquina virtual de la imagen tooAzure pila | Documentos de Microsoft"
description: "Agregar los imagen personalizada de Windows o Linux VM de su organización para los inquilinos toouse"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: e5a4236b-1b32-4ee6-9aaa-fcde297a020f
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: sngun
ms.openlocfilehash: 26dd6c289664c4d64d5932f4396ae778f3f1e1f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="make-a-custom-virtual-machine-image-available-in-azure-stack"></a>Hacer que una imagen de máquina virtual personalizada esté disponible en Azure Stack

Azure habilita la pila en la nube a los usuarios de los administradores toomake máquina virtual personalizada imágenes tootheir disponible. Estas imágenes pueden hacer referencia a plantillas del Administrador de recursos de Azure o agregan toothe interfaz de usuario de Azure Marketplace con creación de hello de un elemento de Marketplace. 

## <a name="add-a-vm-image-toomarketplace-with-powershell"></a>Agregar un toomarketplace de imagen de máquina virtual con PowerShell

Ejecute hello siguiendo los requisitos previos de hello [kit de desarrollo de](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-remote-desktop), o desde un cliente externo basado en Windows si está [conectado a través de VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)

* [Instale PowerShell para Azure Stack](azure-stack-powershell-install.md).  

* Descargar hello [toowork necesarios de herramientas con la pila de Azure](azure-stack-powershell-download.md).  

* Prepare una imagen de disco duro virtual del sistema operativo Windows o Linux en formato VHD (no VHDX).
   
   * Para las imágenes de Windows, Hola artículo [cargar una tooAzure de imagen de máquina virtual de Windows para las implementaciones del Administrador de recursos](../virtual-machines/windows/upload-generalized-managed.md) contiene instrucciones de preparación de imagen de hello **Hola preparar VHD para la carga** sección.
   * Para las imágenes de Linux, siga los pasos de Hola para preparar la imagen de Hola o usar una imagen de Linux de la pila de Azure existente tal como se describe en el artículo hello [máquinas virtuales Linux implementar en Azure pila](azure-stack-linux.md).  

Ahora ejecute hello después de marketplace de pasos tooadd Hola imagen toohello pila de Azure:

1. Importar módulos de conectar y ComputeAdmin de hello:
   
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
    
3. Agregar imagen de máquina virtual de hello invocando hello `Add-AzsVMImage` cmdlet. En el cmdlet Add-AzsVMImage de hello, especifique Hola osType como Windows o Linux. Incluir publicador hello, oferta, SKU y versión de imagen de máquina virtual de Hola. Vea hello [parámetros](#parameters) sección para obtener información acerca de hello permitida parámetros. Imagen de máquina virtual de Azure Resource Manager plantillas tooreference Hola utiliza estos parámetros. La siguiente es una invocación de ejemplo del script de Hola:
     
     ```powershell
     Add-AzsVMImage `
       -publisher "Canonical" `
       -offer "UbuntuServer" `
       -sku "14.04.3-LTS" `
       -version "1.0.0" `
       -osType Linux `
       -osDiskLocalPath 'C:\Users\AzureStackAdmin\Desktop\UbuntuServer.vhd' `
     ```

comando de Hola Hola siguientes:

* Autentica el entorno de Azure pila toohello
* Carga tooa Hola de disco duro virtual local recién creado la cuenta de almacenamiento temporal
* Agrega el repositorio de imágenes VM de toohello imagen VM de Hola y
* Crea un elemento de Marketplace

tooverify que el comando de Hola se ejecutó correctamente, vaya tooMarketplace en el portal de hello y, a continuación, compruebe dicha imagen VM Hola está disponible en hello **máquinas virtuales** categoría.

![Imagen de máquina virtual agregada correctamente](./media/azure-stack-add-vm-image/image5.PNG) 

## <a name="remove-a-vm-image-with-powershell"></a>Eliminación de una imagen de máquina virtual con PowerShell

Cuando ya no necesita hello imagen de máquina virtual que ha cargado anteriormente, puede eliminarla del marketplace de hello mediante el uso de hello siguiente cmdlet:

```powershell
Remove-AzsVMImage `
  -publisher "Canonical" `
  -offer "UbuntuServer" `
  -sku "14.04.3-LTS" `
  -version "1.0.0" `
```

## <a name="parameters"></a>parameters

| Parámetro | Descripción |
| --- | --- |
| **publisher** |segmento de nombre de publicador Hola de imagen de VM de Hola que los usuarios usan al implementar la imagen de Hola. Un ejemplo es 'Microsoft'. No incluya un espacio u otros caracteres especiales en este campo. |
| **offer** |segmento de nombre de la oferta de Hola de imagen de máquina virtual que los usuarios usan al implementar la imagen de máquina virtual de Hola Hola. Un ejemplo es 'WindowsServer'. No incluya un espacio u otros caracteres especiales en este campo. |
| **sku** |segmento de nombre de SKU de Hola de imagen de máquina virtual que los usuarios usan al implementar la imagen de máquina virtual de Hola Hola. Un ejemplo es 'Datacenter2016'. No incluya un espacio u otros caracteres especiales en este campo. |
| **version** |versión de Hola de imagen de máquina virtual que los usuarios usan al implementar la imagen de máquina virtual de Hola Hola. Esta versión está en formato de hello  *\#.\#. \#*. Un ejemplo es '1.0.0'. No incluya un espacio u otros caracteres especiales en este campo. |
| **osType** |Hola osType de imagen de hello debe ser 'Windows' o 'Linux'. |
| **osDiskLocalPath** |disco toohello SO de ruta de acceso local de Hello disco duro virtual que se va a cargar como un tooAzure de imagen VM pila. |
| **dataDiskLocalPaths** |Una matriz opcional de rutas de acceso local de Hola para discos de datos que se pueden cargar como parte de la imagen de máquina virtual de Hola. |
| **CreateGalleryItem** |Un indicador booleano que determina si un elemento de Marketplace toocreate. De forma predeterminada, se establece tootrue. |
| **title** |Hola nombre para mostrar del elemento de Marketplace. De forma predeterminada, se establece toohello Sku de oferta de publicador de la imagen de máquina virtual de Hola. |
| **descripción** |Descripción de Hello del elemento de Marketplace de Hola. |
| **ubicación** |debe publicarse la imagen de máquina virtual de Hello ubicación toowhich Hola. De forma predeterminada, este valor se establece toolocal.|
| **osDiskBlobURI** |Opcionalmente, este script también acepta un identificador URI de Blob Storage para disco de sistema operativo. |
| **dataDiskBlobURIs** |Opcionalmente, este script también acepta una matriz de almacenamiento de blobs de URI para agregar imagen de toohello de discos de datos. |

## <a name="add-a-vm-image-through-hello-portal"></a>Agregar una imagen de máquina virtual a través del portal de Hola

> [!NOTE]
> Este método requiere crear elemento de Marketplace de Hola por separado.

Un requisito de las imágenes es que se pueda hacer referencia a ellas con un identificador URI de Blob Storage. Preparar una imagen de sistema operativo Windows o Linux en formato de disco duro virtual (no VHDX) y, a continuación, cargue la cuenta de almacenamiento tooa Hola de imagen en Azure o Azure pila. Si la imagen ya está cargado toohello almacenamiento de blobs en Azure o la pila de Azure, puede omitir el paso 1.

1. [Cargar un tooAzure de imagen de máquina virtual de Windows para las implementaciones del Administrador de recursos](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/) o una imagen de Linux, siga las instrucciones de hello descritas en hello [máquinas virtuales Linux implementar en Azure pila](azure-stack-linux.md) artículo. Debe conocer Hola siguientes consideraciones antes de cargar imagen de hello:

   * Resulta más eficaz tooupload un almacenamiento de blobs de la pila de imagen tooAzure que tooAzure almacenamiento de blobs porque toma menos repositorio de imágenes tiempo toopush Hola imagen toohello pila de Azure. 
   
   * Al cargar hello [imagen de máquina virtual de Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/), que seguro Hola toosubstitute **tooAzure de inicio de sesión** paso con hello [configurar el entorno de PowerShell del operador de hello Azure pila](azure-stack-powershell-configure-admin.md)paso.  

   * Tome nota de hello URI donde cargar imagen de hello, que se encuentra en hello siguiendo el formato de almacenamiento de blobs:  *&lt;storageAccount&gt;/&lt;blobContainer&gt; / &lt;targetVHDName&gt;*.vhd

   * toomake Hola accesible de forma anónima, vaya toohello cuenta blob en contenedor de almacenamiento blob donde hello VM imagen VHD se cargó demasiado**Blob,** y, a continuación, seleccione **directiva de acceso**. Si lo desea, puede generar una firma de acceso compartido para el contenedor de Hola e incluirlo como parte del URI del blob de Hola.

   ![Navegue toostorage blobs de cuenta](./media/azure-stack-add-vm-image/image1.png)

   ![Set blob acceso toopublic](./media/azure-stack-add-vm-image/image2.png)

2. Inicie sesión en tooAzure pila como un administrador de la nube > en el menú de hello, haga clic en **más servicios** > **proveedores de recursos** > seleccione **proceso**  >  **Imágenes de máquina virtual** > **agregar**

3. En hello **agregar una imagen de VM** hoja, escriba publicador hello, oferta, SKU y versión de imagen de máquina virtual de Hola. Estos segmentos de nombre de referencia toohello imagen de máquina virtual en las plantillas de administrador de recursos. Asegúrese de que tooselect el **osType** correctamente. Para **URI de Blob del disco OD**, escriba Hola URI de Blob donde se cargó la imagen y haga clic en **crear** toobegin crear la imagen de máquina virtual.
   
   ![BEGIN toocreate Hola imagen](./media/azure-stack-add-vm-image/image4.png)

   Cuando se crea correctamente la imagen de hello, Hola estado de la imagen VM cambia too'Succeeded'.

4. toomake Hola imagen de máquina virtual más fácilmente disponible para consumo del usuario en la interfaz de usuario de hello, lo mejor es demasiado[crear un elemento de Marketplace](azure-stack-create-and-publish-marketplace-item.md).

## <a name="next-steps"></a>Pasos siguientes

[Aprovisionamiento de una máquina virtual](azure-stack-provision-vm.md)