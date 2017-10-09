---
title: "privilegios de raíz de aaaUse en máquinas virtuales de Linux | Documentos de Microsoft"
description: "Obtenga información acerca de cómo los privilegios de toouse raíz en una máquina virtual de Linux en Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: a2c106a2-dceb-43a3-9dd1-50ed77685952
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: 9411588c5fd0c86c4c73b3e44fbb56ab150013d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="using-root-privileges-on-linux-virtual-machines-in-azure"></a>Uso de privilegios raíz en máquinas virtuales con Linux en Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

De forma predeterminada, Hola `root` usuario está deshabilitado en las máquinas virtuales de Linux en Azure. Los usuarios pueden ejecutar comandos con privilegios elevados mediante el uso de hello `sudo` comando. Sin embargo, la experiencia de Hola puede variar dependiendo de cómo se haya proporcionado el sistema Hola.

1. **Clave SSH y contraseña OR solo** -máquina virtual de Hola se haya proporcionado con un certificado (`.CER` archivo) o clave SSH, así como una contraseña, o simplemente un nombre de usuario y una contraseña. En este caso `sudo` solicitará contraseña del usuario de hello antes de ejecutar el comando de Hola.
2. **La clave SSH** -máquina virtual de Hola se haya proporcionado con un certificado (`.cer`, `.pem`, o `.pub` archivo) o clave SSH, pero no hay ninguna contraseña.  En este caso `sudo` **no** solicitar una contraseña de usuario de hello antes de ejecutar el comando de Hola.

## <a name="ssh-key-and-password-or-password-only"></a>Clave SSH y contraseña o solo contraseña
Inicie sesión en la máquina virtual de Linux de hello mediante la autenticación de clave o contraseña SSH, a continuación, ejecutar comandos mediante `sudo`, por ejemplo:

    # sudo <command>
    [sudo] password for azureuser:

En este caso usuario Hola le pedirá una contraseña. Después de escribir la contraseña de hello `sudo` se ejecutará el comando hello con `root` privilegios.

También puede habilitar sudo passwordless mediante la edición de hello `/etc/sudoers.d/waagent` de archivos, por ejemplo:

    #/etc/sudoers.d/waagent
    azureuser ALL = (ALL) NOPASSWD: ALL

Este cambio permitirá passwordless sudo usuario Hola "azureuser".

## <a name="ssh-key-only"></a>Solo clave SSH
Inicie sesión en la máquina virtual de Linux de hello mediante la autenticación de clave SSH y vuelva a ejecutar comandos mediante `sudo`, por ejemplo:

    # sudo <command>

En este caso le usuario hello **no** se le solicite una contraseña. Después de presionar `<enter>`, `sudo` se ejecutará el comando hello con `root` privilegios.

