---
title: "nodos de proceso de clúster de HPC Pack aaaManage | Documentos de Microsoft"
description: "Obtenga información acerca de tooadd de herramientas de script de PowerShell, quitar, iniciar y detener nodos de proceso de clúster de HPC Pack 2012 R2 en Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>Administrar el número de Hola y la disponibilidad de nodos de proceso en un clúster de HPC Pack en Azure
Si ha creado un clúster de HPC Pack 2012 R2 en máquinas virtuales de Azure, conviene formas tooeasily agregar, quitar, iniciar (aprovisionar) o detenga (Cancelar aprovisionamiento) algunas máquinas virtuales de nodos del clúster de proceso. toodo estas tareas, ejecutar scripts de PowerShell de Azure que están instalados en la máquina virtual del nodo principal Hola. Estos scripts ayudan a controlar el número de Hola y la disponibilidad de los recursos de clúster de HPC Pack para poder controlar los costos.

> [!IMPORTANT] 
> En este artículo se aplica solo tooHPC Pack 2012 R2 clústeres en Azure creados mediante el modelo de implementación clásica de Hola. Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.
> Además, los scripts de PowerShell de Hola se describe en este artículo no están disponibles en HPC Pack 2016.

## <a name="prerequisites"></a>Requisitos previos
* **Clúster de HPC Pack 2012 R2 en máquinas virtuales de Azure**: crear un clúster de HPC Pack 2012 R2 en el modelo de implementación clásica de Hola. Por ejemplo, puede automatizar la implementación de hello mediante un script de PowerShell de Azure y de imagen de máquina virtual de HPC Pack 2012 R2 de hello en hello Azure Marketplace. Para obtener información y requisitos previos, consulte [crear un clúster de HPC con hello script de implementación de IaaS de HPC Pack](hpcpack-cluster-powershell-script.md).
  
    Después de la implementación, encontrar Hola scripts de administración de nodo en Hola % CCP\_carpeta principal % bin en el nodo principal de Hola. Ejecutar cada una de las secuencias de comandos de hello como administrador.
* **Certificado de administración o el archivo de configuración de publicación de Azure**: necesita toodo uno de los siguientes hello en el nodo principal de hello:
  
  * **Archivo de configuración de publicación de hello importación Azure**. toodo, ejecución Hola siguientes cmdlets de PowerShell de Azure en el nodo principal de hello:
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * **Configurar certificado de administración de Azure de hello en el nodo principal de hello**. Si tiene el archivo .cer de hello, impórtelo en el almacén de certificados de hello CurrentUser\My y, a continuación, ejecute Hola siguiente cmdlet de PowerShell de Azure para el entorno de Azure (nube de Azure o AzureChinaCloud):
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a>Agregar máquinas virtuales de nodo de ejecución
Agregar nodos de proceso con hello **Add-HpcIaaSNode.ps1** secuencia de comandos.

### <a name="syntax"></a>Sintaxis
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a>parameters
* **ServiceName**: nombre del servicio de nube de Hola que calculan nuevas máquinas virtuales de nodos se agregan a.
* **ImageName**: nombre de imagen de máquina virtual de Azure, que puede obtenerse a través del portal de Azure clásico de Hola o cmdlet de PowerShell de Azure **Get-AzureVMImage**. imagen de Hello debe cumplir Hola según los requisitos:
  
  1. Debe haber instalado un sistema operativo Windows.
  2. HPC Pack debe instalarse en función del nodo de proceso de Hola.
  3. imagen de Hello debe ser una imagen privada en la categoría de usuario de hello, no es una imagen de máquina virtual de Azure pública.
* **Cantidad**: número de toobe de las máquinas virtuales de nodo de proceso agregado.
* **InstanceSize**: tamaño de hello máquinas virtuales de nodos de proceso.
* **Dominionombre_de_usuario**: nombre de usuario de dominio, que es usado toojoin Hola nuevas máquinas virtuales toohello dominio.
* **DomainUserPassword**: contraseña de usuario de dominio de Hola.
* **NodeNameSeries** (opcional): modelo de nomenclatura para hello nodos de proceso. Hola formato debe ser &lt; *raíz\_nombre*&gt;&lt;*iniciar\_número*&gt;%. Por ejemplo, Mine % 10% significa una serie de hello calcula nombres de nodo a partir de MyCN11. Si no se especifica, Hola script utiliza Hola configurado serie de nombres de nodo de clúster de HPC de Hola.

### <a name="example"></a>Ejemplo
Hello en el ejemplo siguiente se agrega 20 máquinas virtuales de nodos de proceso gran tamaño en el servicio de nube de hello *hpcservice1*, en función de la imagen de máquina virtual de hello *hpccnimage1*.

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a>Quitar máquinas virtuales de nodo de ejecución
Quitar nodos de proceso con hello **Remove-HpcIaaSNode.ps1** secuencia de comandos.

### <a name="syntax"></a>Sintaxis
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a>parameters
* **Nombre**: quitan nombres de toobe de nodos de clúster. Se admite caracteres comodín. nombre de conjunto de parámetros de Hello es nombre. No se pueden especificar ambos hello **nombre** y **nodo** parámetros.
* **Nodo**: objeto HpcNode Hola para hello nodos toobe quitado, que puede obtenerse a través del cmdlet de PowerShell de HPC de hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). nombre de conjunto de parámetros de Hello es nodo. No se pueden especificar ambos hello **nombre** y **nodo** parámetros.
* **DeleteVHD** (opcional): configuración toodelete discos Hola asociado para hello las máquinas virtuales que se quitan.
* **Force** (opcional): configuración tooforce los nodos HPC antes de eliminarlos.
* **Confirmar** (opcional): pedir confirmación antes de ejecutar el comando Hola.
* **WhatIf**: configuración toodescribe lo que sucedería si ejecutara Hola comando sin realmente ejecutar comando Hola.

### <a name="example"></a>Ejemplo
Hello en el ejemplo siguiente se fuerza nodos sin conexión hello cuyos nombres empiezan *HPCNode-CN -* y ellos elimina los nodos de Hola y sus discos asociados.

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a>Iniciar máquinas virtuales de nodos de ejecución
Inicio de proceso nodos con hello **Start-HpcIaaSNode.ps1** secuencia de comandos.

### <a name="syntax"></a>Sintaxis
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a>parameters
* **Nombre**: nombres de toobe de nodos de clúster de hello iniciado. Se admite caracteres comodín. nombre de conjunto de parámetros de Hello es nombre. No se pueden especificar ambos hello **nombre** y **nodo** parámetros.
* **Nodo**-objeto HpcNode Hola para hello nodos toobe iniciado, que puede obtenerse a través del cmdlet de PowerShell de HPC de hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). nombre de conjunto de parámetros de Hello es nodo. No se pueden especificar ambos hello **nombre** y **nodo** parámetros.

### <a name="example"></a>Ejemplo
Hello en el ejemplo siguiente se inicia nodos cuyos nombres empiezan *HPCNode-CN -*.

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a>Detener máquinas virtuales de nodo de ejecución
Detener nodos de proceso con hello **Stop-HpcIaaSNode.ps1** secuencia de comandos.

### <a name="syntax"></a>Sintaxis
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a>parameters
* **Nombre de**-nombres de toobe de nodos de clúster de hello detenido. Se admite caracteres comodín. nombre de conjunto de parámetros de Hello es nombre. No se pueden especificar ambos hello **nombre** y **nodo** parámetros.
* **Nodo**: objeto HpcNode Hola para hello nodos toobe detenido, que puede obtenerse a través del cmdlet de PowerShell de HPC de hello [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx). nombre de conjunto de parámetros de Hello es nodo. No se pueden especificar ambos hello **nombre** y **nodo** parámetros.
* **Force** (opcional): configuración tooforce los nodos HPC antes de detenerlos.

### <a name="example"></a>Ejemplo
Hello en el ejemplo siguiente se fuerza sin conexión nodos cuyos nombres empiezan *HPCNode-CN -* y, a continuación, se detiene Hola nodos.

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a>Pasos siguientes
* tooautomatically aumentar o reducir los nodos del clúster Hola según la carga de trabajo actual de Hola de trabajos y tareas en clúster de hello, consulte [automáticamente aumentar y reducir los recursos de clúster de HPC Pack hello en Azure correspondiente toohello clúster cargas de trabajo](hpcpack-cluster-node-autogrowshrink.md).

