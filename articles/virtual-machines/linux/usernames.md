---
title: aaaSelecting nombres de usuario de Linux | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooselect usuario asigna un nombre para una máquina virtual de Linux en Azure."
services: virtual-machines-linux
documentationcenter: 
author: szarkos
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: 33b50c97-92f1-46c9-a623-e37f67459c5c
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/02/2017
ms.author: szark
ms.openlocfilehash: c65e2ac46f40bb8c9d74cccbaf248a070c0fa6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="selecting-user-names-for-linux-on-azure"></a>Selección de nombres de usuario para Linux en Azure
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

Cuando aprovisiona una máquina virtual de Linux en Azure debe especificar nombre de Hola de un usuario no es de raíz que posteriormente, puede usar toolog en hello VM. Puede elegir nombre Hola de nuevo usuario de hello, o si el aprovisionamiento a través de Hola portal de Azure clásico puede aceptar predeterminado Hola nombre "azureuser".

En la mayoría de los casos, este usuario no existe en la imagen base hello y se creará durante el proceso de aprovisionamiento de Hola. Si el usuario Hola existe en la imagen de máquina virtual base hello, a continuación, Hola Linux de Azure agente simplemente configura contraseña Hola o clave SSH para ese usuario basándose en información de Hola que especificó al crear Hola máquina virtual.

**Sin embargo**, Linux define un conjunto de nombres de usuario que no se deben usar al crear usuarios nuevos. Hola will del proceso de aprovisionamiento **producirá un error** si intentas tooprovision una VM de Linux con un usuario de sistema existente, que se define como un usuario con UID 0 y 99. Un ejemplo típico es hello `root` usuario, que tiene el UID 0.

* Consulte también: [Base estándar de Linux - Intervalos de identificadores de usuarios](http://refspecs.linuxfoundation.org/LSB_4.1.0/LSB-Core-generic/LSB-Core-generic/uidrange.html)

Hola aquí te mostramos una lista de usuarios de sistema integradas comunes para CentOS y Ubuntu debe evitar el uso de al aprovisionar una máquina virtual de Linux en Azure. Esta lista es sólo un ejemplo, consulte toohello documentación para su distribución tooensure ese nombre de usuario de Hola que elija no entra en conflicto con un usuario del sistema existente.

## <a name="centos"></a>CentOS
* abrt
* adm
* audio
* bin
* cdrom
* cgred
* daemon
* dbus
* dialout
* dip
* disk
* floppy
* ftp
* ftp
* games
* gopher
* haldaemon
* halt
* kmem
* lock
* lp
* mail
* man
* mem
* nfsnobody
* nobody
* ntp
* operator
* oprofile
* postdrop
* postfix
* qpidd
* root
* rpc
* rpcuser
* saslauth
* shutdown
* slocate
* sshd
* stapdev
* stapusr
* sync
* sys
* tape
* test
* tcpdump
* tty
* users
* utempter
* utmp
* uucp
* vcsa
* video
* wheel

## <a name="ubuntu"></a>Ubuntu
* adm
* admin
* audio
* backup
* bin
* cdrom
* crontab
* daemon
* dialout
* dip
* disk
* fax
* floppy
* fuse
* games
* gnats
* irc
* kmem
* landscape
* libuuid
* list
* lp
* mail
* man
* messagebus
* mlocate
* netdev
* news
* nobody
* nogroup
* operator
* plugdev
* proxy
* root
* sasl
* shadow
* src
* ssh
* sshd
* staff
* sudo
* sync
* sys
* syslog
* tape
* tty
* users
* utmp
* uucp
* video
* voice
* whoopsie
* www-data

