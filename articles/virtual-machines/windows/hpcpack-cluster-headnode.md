---
title: "aaaCreate un nodo principal de HPC Pack en una máquina virtual de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toouse Hola implementación de administrador de recursos de hello y portal de Azure modelo toocreate un nodo principal de Microsoft HPC Pack 2012 R2 en una VM de Azure."
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: e6a13eaf-9124-47b4-8d75-2bc4672b8f21
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 3ddefb74b053a48a15f1ba1ca8edbc0192da51a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-hello-head-node-of-an-hpc-pack-cluster-in-an-azure-vm-with-a-marketplace-image"></a>Crear el nodo principal de Hola de un clúster de HPC Pack en una máquina virtual de Azure con una imagen de Marketplace
Use un [imagen de máquina virtual de Microsoft HPC Pack 2012 R2](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) Hola hello y Azure Marketplace toocreate portal Azure Hola nodo principal de un clúster de HPC. Esta imagen de máquina virtual de HPC Pack se basa en Windows Server 2012 R2 Datacenter con HPC Pack 2012 R2 Update 3 preinstalado. Utilice este nodo principal para una implementación de prueba de concepto de HPC Pack en Azure. A continuación, puede agregar cargas de trabajo de proceso nodos toohello clúster toorun HPC.

> [!TIP]
> toodeploy un clúster de HPC Pack 2012 R2 completando en Azure que incluye el nodo principal de Hola y nodos de proceso, se recomienda que utilice un método automatizado. Las opciones incluyen hello [script de implementación de IaaS de HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) y plantillas de administrador de recursos como hello [clúster de HPC Pack para cargas de trabajo de Windows](https://azure.microsoft.com/marketplace/partners/microsofthpc/newclusterwindowscn/). Las plantillas de Resource Manager también están disponibles para [clústeres de Microsoft HPC Pack 2016](https://github.com/MsHpcPack/HPCPack2016/tree/master/newcluster-templates). 
> 
> 

## <a name="planning-considerations"></a>Consideraciones de planeación
Como se muestra en la figura siguiente de Hola, implemente nodo principal de HPC Pack hello en un dominio de Active Directory en una red virtual de Azure.

![Nodo principal de HPC Pack][headnode]

* **Dominio de Active Directory**: hello debe ser el nodo principal de HPC Pack 2012 R2 Unidos a un dominio de Active Directory tooan en Azure antes de iniciar los servicios de HPC de hello en hello VM. Como se muestra en este artículo, para una implementación de prueba de concepto, puede promover Hola VM que se crea para el nodo principal de Hola como un controlador de dominio antes de iniciar los servicios HPC de Hola. Otra opción es toodeploy un controlador de dominio independientes y bosque en Azure toowhich unir Hola VM del nodo principal.

* **Modelo de implementación**: para la mayoría de las implementaciones nuevas, Microsoft recomienda que usar el modelo de implementación del Administrador de recursos de Hola. En este artículo se da por supuesto que utiliza este modelo de implementación.

* **Red virtual de Azure**: cuando se usa el nodo principal del Hola de toodeploy de hello Administrador de recursos implementación modelo, especificar o crear una red virtual de Azure. Usar red virtual de hello si tiene un dominio de Active Directory existente de toojoin Hola nodo principal tooan. También se necesitan clúster toohello de máquinas virtuales de nodos de proceso tooadd más adelante.

## <a name="steps-toocreate-hello-head-node"></a>Nodo principal de pasos toocreate Hola
Siguientes son pasos de alto nivel toouse hello toocreate portal Azure una máquina virtual de Azure para el nodo principal de HPC Pack Hola utilizando el modelo de implementación del Administrador de recursos de Hola. 

1. Si desea toocreate un nuevo bosque de Active Directory en Azure con máquinas virtuales de controlador de dominio independientes, una opción es toouse una [plantilla del Administrador de recursos](https://github.com/Azure/azure-quickstart-templates/tree/master/active-directory-new-domain-ha-2-dc). Para una sencilla implementación de prueba de concepto, tiene un preciso tooomit este paso y configurar el nodo principal de hello propia máquina virtual como un controlador de dominio. Esta opción se describe más adelante en este artículo.
2. En hello [HPC Pack 2012 R2 en Windows Server 2012 R2 página](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) en hello Azure Marketplace, haga clic en **crear Máquina Virtual**. 
3. En el portal de hello, en hello **HPC Pack 2012 R2 en Windows Server 2012 R2** página, seleccione hello **el Administrador de recursos** modelo de implementación y, a continuación, haga clic en **crear**.
   
    ![Imagen de HPC Pack][marketplace]
4. Usar la configuración de hello tooconfigure portal hello y cree Hola máquina virtual. Si le tooAzure nuevo, siga el tutorial de hello [crear una máquina virtual de Windows en el portal de Azure hello](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Para una implementación de prueba de concepto, normalmente se puede aceptar el valor predeterminado de Hola o la configuración recomendada.
   
   > [!NOTE]
   > Si desea tooan de nodo principal de hello toojoin existente de dominio de Active Directory en Azure, asegúrese de que especificar la red virtual de Hola para ese dominio al crear Hola VM.
   > 
   > 
5. Después de crear VM de Hola y Hola máquina virtual se está ejecutando, [conectar toohello VM](connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) mediante Escritorio remoto. 
6. Unir el bosque de dominio de Active Directory de hello VM tooan eligiendo una de las siguientes opciones de hello:
   
   * Si ha creado Hola VM en una red virtual de Azure con un bosque de dominio existente, unir bosque toohello de hello VM mediante el uso de herramientas estándar del administrador del servidor o Windows PowerShell. Después, reinicie.
   * Si ha creado Hola VM en una nueva red virtual (sin un bosque de dominio existente), promover, a continuación, Hola VM como un controlador de dominio. Utilice los pasos estándar tooinstall y configurar el rol de servicios de dominio de Active Directory de hello en el nodo principal de Hola. Para ver los pasos detallados, consulte [Instalar un nuevo bosque de Active Directory de Windows Server 2012 (nivel 200)](https://technet.microsoft.com/library/jj574166.aspx).
7. Después de hello VM está ejecutando y está tooan Unidos a un bosque de Active Directory, inicie Servicios de HPC Pack hello de la forma siguiente:
   
    a. Conectar el nodo principal de toohello máquina virtual con una cuenta de dominio que sea miembro del grupo local de administradores de Hola. Por ejemplo, usar la cuenta de administrador de Hola que configuró al crear máquina virtual del nodo principal Hola.
   
    b. Para una configuración de nodo principal de forma predeterminada, inicie Windows PowerShell como administrador y escriba Hola siguiente:
   
    ```PowerShell
    & $env:CCP_HOME\bin\HPCHNPrepare.ps1 –DBServerInstance ".\ComputeCluster"
    ```
   
    Puede tardar varios minutos para toostart de servicios de HPC Pack Hola.
   
    Para las opciones adicionales de configuración del nodo principal, escriba `get-help HPCHNPrepare.ps1`.

## <a name="next-steps"></a>Pasos siguientes
* Ahora puede trabajar con el nodo principal de Hola de su clúster de HPC Pack. Por ejemplo, inicie el Administrador de clústeres de HPC y Hola completa [lista de tareas de implementación](https://technet.microsoft.com/library/jj884141.aspx).
* Si desea tooincrease Hola clúster de proceso capacidad a petición, agregue [Azure en ráfagas nodos](classic/hpcpack-cluster-node-burst.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) en un servicio de nube. 
* Intentar ejecutar una carga de trabajo de prueba en clúster de Hola. Para obtener un ejemplo, vea Hola HPC Pack [Guía de introducción](https://technet.microsoft.com/library/jj884144).

<!--Image references-->
[headnode]: ./media/hpcpack-cluster-headnode/headnode.png
[marketplace]: ./media/hpcpack-cluster-headnode/marketplace.png
