---
title: "problemas comunes de aaaHow tootroubleshoot durante la creación del disco duro virtual | Documentos de Microsoft"
description: "Solución de problemas de respuestas toocommon preguntas y problemas durante la creación del disco duro virtual."
services: Azure Marketplace
documentationcenter: 
author: HannibalSII
manager: 
editor: 
ms.assetid: e39563d8-8646-4cb7-b078-8b10ac35b494
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 09/26/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: e4ff09a979bdf575badff2d33f2299abb17c947d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootroubleshoot-common-issues-encountered-during-vhd-creation"></a>¿Cómo encontraron problemas comunes de tootroubleshoot durante la creación del disco duro virtual
Este artículo es proporciona toohelp un publicador de Azure Marketplace o Coadministrador que puede experimentar un problema o tiene preguntas comunes al publicar o administrar sus soluciones de máquina virtual.

1. ¿Cómo se cambia el nombre de hello del host de hello?
   
    Una vez creada la máquina virtual, los usuarios no pueden actualizar nombre de hello del host de Hola.
2. ¿Cómo tooreset Hola servicios de escritorio remoto o su contraseña de inicio de sesión?
   
   * [Referencia para máquinas virtuales con Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-reset-rdp/)
   * [Referencia para máquinas virtuales con Linux](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
3. ¿Cómo toogenerate nueva ssh certificados?
   
   Consulte el vínculo de toohello: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
4. ¿Cómo abrir el certificado VPN tooconfigure?
   
   Consulte el vínculo de toohello: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)
5. ¿Qué es la directiva de soporte técnico de Hola para ejecutar el software de servidor de Microsoft en el entorno de máquina virtual de Microsoft Azure hello (infraestructura como-servicio)?
   
   Consulte el vínculo de toohello: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)
6. ¿Las máquinas virtuales tienen un identificador único?
   
   Azure codifica un identificador exclusivo de máquina virtual de Azure en cada máquina virtual. Vea los detalles en este blog y en la documentación.
7. En una máquina virtual ¿cómo puedo administrar extensión de script personalizado de hello en la tarea de inicio de hello?
   
   Consulte el vínculo de toohello: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)
8. ¿Cómo toocreate una máquina virtual desde hello Azure portal mediante Hola VHD cargado toopremium almacenamiento?
   
   Aún no se admite esta característica.
9. ¿Es una aplicación de 32 bits compatible en hello Azure Marketplace?
   
   Consulte toohello vínculo para obtener más información sobre la directiva de soporte técnico de hello: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)
10. Cada vez que estoy tratando de toocreate una imagen desde Mis discos duros virtuales, obtengo un error de Hola ". Disco duro virtual ya está registrado con el repositorio de imágenes como recurso de Hola"en PowerShell. No he creado ninguna imagen antes ni he encontrado ninguna imagen con este nombre en Azure. ¿Cómo se resuelve este problema?
    
    Esto suele suceder si usuario Hola aprovisiona una máquina virtual desde este disco duro virtual y no hay un bloqueo en ese archivo VHD. Compruebe que no haya ninguna máquina virtual asignada desde este VHD. Si persiste error hello, por favor, genera una incidencia de soporte técnico mediante este vínculo o de hello publicación portal sobre esta (detalles figuran en la respuesta de saludo de la pregunta 11).
