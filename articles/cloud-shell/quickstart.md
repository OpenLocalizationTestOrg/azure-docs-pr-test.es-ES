---
title: "Inicio rápido de nube Shell (versión preliminar) aaaAzure | Documentos de Microsoft"
description: "Inicio rápido para hello Shell en la nube de Azure"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: e60700b92c10c331910dd8bb3c627fe1a024091c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-using-hello-azure-cloud-shell"></a>Inicio rápido para usar Hola Shell en la nube de Azure

Este documento detalla cómo toouse Hola Shell en la nube de Azure en hello [portal de Azure](https://ms.portal.azure.com/).

## <a name="start-cloud-shell"></a>Inicio de Cloud Shell
1. Iniciar **Shell en la nube** de navegación superior de Hola de hello portal de Azure <br>
![](media/shell-icon.png)
2. Seleccione una suscripción toocreate una cuenta de almacenamiento y el recurso compartido de archivos de Azure
3. Seleccione "Create storage" (Creación de almacenamiento)

> [!TIP]
> Usted se autentica automáticamente para la CLI de Azure 2.0 en todas las sesiones.

### <a name="set-your-subscription"></a>Establecimiento de la suscripción
1. Enumere las suscripciones a las que tiene acceso: <br>
`az account list`
2. Establezca su suscripción preferida: <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> La suscripción se recordará para sesiones futuras mediante `/home/<user>/.azure/azureProfile.json`.

### <a name="create-a-resource-group"></a>Crear un grupo de recursos
Cree un nuevo grupo de recursos en la región oeste de EE. UU. llamado "MyRG": <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a>Creación de una máquina virtual Linux
Cree una máquina virtual con Ubuntu en su nuevo grupo de recursos. Hola 2.0 de CLI de Azure creará las claves de SSH y el programa de instalación Hola VM con ellos. <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> Hola tooauthenticate de claves pública y privada que usa la máquina virtual se colocan en `/User/.ssh/id_rsa` y `/User/.ssh/id_rsa.pub` 2.0 de CLI de Azure de forma predeterminada. La carpeta .ssh se conserva en la imagen de 5 GB adjunta del recurso compartido de archivos de Azure.

Su nombre de usuario en esta máquina virtual será el nombre de usuario utilizado en Cloud Shell ($User@Azure:).

### <a name="ssh-into-your-linux-vm"></a>Conexión SSH con la máquina virtual Linux
1. Buscar el nombre de máquina virtual en la barra de búsqueda del portal Azure de Hola
2. Haga clic en "Conectar" y ejecute: `ssh username@ipaddress`

![](media/sshcmd-copy.png)

Al establecer la conexión de SSH de hello, debería ver mensaje bienvenida de hello Ubuntu.
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a>Limpiar 
Elimine el grupo de recursos y cualquier recurso dentro del mismo: <br>
Ejecute `az group delete -n MyRG`

## <a name="next-steps"></a>Pasos siguientes
[Obtenga información sobre la persistencia del almacenamiento en Cloud Shell](persisting-shell-storage.md) <br>
[Más información sobre la CLI de Azure 2.0](https://docs.microsoft.com/cli/azure/) <br>
[Información sobre Azure File Storage](../storage/files/storage-files-introduction.md) <br>