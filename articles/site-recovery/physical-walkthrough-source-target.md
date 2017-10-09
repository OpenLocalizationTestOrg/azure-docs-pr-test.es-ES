---
title: "aaaSet seguridad Hola origen y de destino para tooAzure de replicación de servidor físico con Azure Site Recovery | Documentos de Microsoft"
description: "Resume Hola pasos tooset la configuración de origen y de destino para la replicación de almacenamiento de tooAzure de servidores físicos con hello servicio Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 2e3d03bc-4e53-4590-8a01-f702d3cc9500
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: e75ef23174d77509bf54380eba8f251a7337a45f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-hello-source-and-target-for-physical-server-replication-tooazure"></a>Paso 7: Configurar origen de Hola y de destino para tooAzure de replicación del servidor físico

Este artículo describe cómo tooconfigure de configuración de origen y de destino cuando se replican de manera local tooAzure de servidores físicos, mediante hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.

Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Configurar el entorno de origen Hola

Configurar el servidor de configuración de hello, registrar en el almacén de Hola y detectar máquinas.

1. Haga clic en **Site Recovery** > **Paso 1: Preparar la infraestructura** > **Origen**.
2. Si no tiene un servidor de configuración, haga clic en **+Servidor de configuración**.
3. En **Agregar servidor**, compruebe que aparezca **Servidor de configuración** en **Tipo de servidor**.
4. Descargue el archivo de instalación de configuración de Site Recovery unificado de Hola.
5. Descargue la clave de registro del almacén de Hola. Se le solicitará cuando ejecute la instalación unificada. clave de Hello es válida durante cinco días después de generarlo.

   ![Configurar origen](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a>Registrar el servidor de configuración de hello en el almacén de Hola

Realice la siguiente Hola antes de iniciar después ejecutar el programa de instalación unificada tooinstall servidor de configuración de hello, servidor de procesos de Hola y servidor de destino maestro Hola. Hola vídeo describe cómo configurar los componentes de hello para la replicación de VM de VMware tooAzure. Sin embargo, hello mismo proceso es válido para la replicación de tooAzure de servidor físico.

- En la máquina virtual del servidor de configuración de hello, asegúrese de que el reloj del sistema de Hola se sincroniza con un [servidor horario](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Deben ser iguales. Si hay una diferencia de 15 minutos, antes o después, se podría producir un error en la instalación.
- Ejecute el programa de instalación como administrador Local en el equipo del servidor de configuración de Hola.
- Asegúrese de que TLS 1.0 está habilitado en hello máquina virtual.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> También se puede instalar el servidor de configuración de Hello [desde la línea de comandos de hello](http://aka.ms/installconfigsrv).




## <a name="set-up-hello-target-environment"></a>Configurar el entorno de destino de Hola

Antes de configurar el entorno de destino de hello, asegúrese de que tiene una cuenta de almacenamiento de Azure y la configuración de red virtual.

1. Haga clic en **preparar infraestructura** > **destino**, y seleccione Hola desea toouse de suscripción de Azure.
2. Especifique si el modelo de implementación de destino está basado en Resource Manager o si es el clásico.
3. Site Recovery comprueba que tiene una o más cuentas de almacenamiento y redes compatibles.

   ![Destino](./media/physical-walkthrough-source-target/gs-target.png)

4. Si no ha creado una cuenta de almacenamiento o red, haga clic en **+ cuenta de almacenamiento** o **+ red**, toocreate un administrador de recursos cuenta o red en línea.

## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 8: configurar una directiva de replicación](physical-walkthrough-replication.md)
