---
title: "limitaciones de Shell en la nube (versión preliminar) aaaAzure | Documentos de Microsoft"
description: "Introducción a las limitaciones de Azure Cloud Shell"
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
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a>Limitaciones de Azure Cloud Shell
Shell de nube de Azure tiene los siguientes de hello limitaciones conocidas:

## <a name="system-state-and-persistence"></a>Persistencia y estado del sistema
máquina de Hola que proporciona la sesión de Shell en la nube es temporal y se recicla después de la sesión está inactiva durante 20 minutos. En la nube Shell requiere un toobe del recurso compartido de archivos montado. Como resultado, la suscripción debe ser capaz de tooset una tooaccess de recursos de almacenamiento en la nube Shell. Otras consideraciones:
* Con el almacenamiento montado, solo se conservan las modificaciones de los directorios `$Home` o `clouddrive`.
* Solo se pueden montar recursos compartidos de archivos desde la [región asignada](persisting-shell-storage.md#mount-a-new-clouddrive).
* Azure Files solo admite cuentas de almacenamiento con redundancia local o de almacenamiento con redundancia geográfica.

## <a name="user-permissions"></a>Permisos de usuario
Los permisos se establecen como usuarios normales sin acceso a sudo. No se conservará cualquier instalación fuera del directorio `$Home`.
Aunque ciertos comandos dentro de Hola `clouddrive` directorio, como `git clone`, no tiene los permisos adecuados, su `$Home` directorio tiene permisos.

## <a name="browser-support"></a>Compatibilidad con exploradores
Shell de nube es compatible con versiones más recientes de Hola de Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox y Safari de Apple. Safari en modo privado no es compatible.

## <a name="copy-and-paste"></a>Copiar y pegar
CTRL+c y CTRL+v no funcionan como copiar y pegar accesos directos en el Shell de nube en máquinas con Windows, utilice Ctrl + Insert y MAYÚS+INS toocopy y pegue respectivamente.

Opciones de copiar y pegar del menú contextual también están disponibles, pero contextual función acceso de Portapapeles toobrowser específico de asunto.

## <a name="editing-bashrc"></a>Editar .bashrc
Tenga cuidado al editar .bashrc, ya que puede producir errores inesperados en Cloud Shell.

## <a name="bashhistory"></a>.bash_history
El historial de comandos de Bash puede ser incoherente debido a una interrupción de la sesión de Cloud Shell o a sesiones simultáneas.

## <a name="usage-limits"></a>Límites de uso
Cloud Shell está pensado para casos de uso interactivos. Por tanto, todas las sesiones que no sean de este tipo y que se prolonguen durante mucho tiempo se finalizarán sin previo aviso.

## <a name="network-connectivity"></a>Conectividad de red
Tiempos de espera en el Shell de nube es conectividad a internet toolocal asunto, Shell de nube continúa tooattempt toocarry espera las instrucciones que se envíen.

## <a name="next-steps"></a>Pasos siguientes
[Inicio rápido de Cloud Shell](quickstart.md)
