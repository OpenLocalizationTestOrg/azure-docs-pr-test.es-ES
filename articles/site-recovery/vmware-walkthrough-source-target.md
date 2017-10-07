---
title: "aaaSet seguridad Hola origen y de destino para tooAzure de replicación de VMware con Azure Site Recovery | Documentos de Microsoft"
description: "Resume Hola pasos tooset la configuración de origen y de destino para la replicación de almacenamiento de máquinas virtuales VMware tooAzure con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99e422e-daf7-4fa8-af3c-af2340340136
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: ef33a44bc5da17afb0442be63f576925f5b9a8b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-vmware-replication-tooazure"></a>Paso 8: Configurar origen de Hola y de destino para tooAzure de replicación de VMware

Este artículo describe cómo tooconfigure de configuración de origen y de destino cuando se replican de manera local tooAzure de máquinas virtuales de VMware, mediante hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.

Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Configurar el entorno de origen Hola

Configurar el servidor de configuración de hello, registrar en el almacén de Hola y detectar máquinas virtuales.

1. Haga clic en **Site Recovery** > **Paso 1: Preparar la infraestructura** > **Origen**.
2. Si no tiene un servidor de configuración, haga clic en **+Servidor de configuración**.
3. En **Agregar servidor**, compruebe que aparezca **Servidor de configuración** en **Tipo de servidor**.
4. Descargue el archivo de instalación de configuración de Site Recovery unificado de Hola.
5. Descargue la clave de registro del almacén de Hola. Se le solicitará cuando ejecute la instalación unificada. clave de Hello es válida durante cinco días después de generarlo.

   ![Configurar origen](./media/vmware-walkthrough-source-target/set-source2.png)


## <a name="register-hello-configuration-server-in-hello-vault"></a>Registrar el servidor de configuración de hello en el almacén de Hola

Realice la siguiente Hola antes de iniciar después ejecutar el programa de instalación unificada tooinstall servidor de configuración de hello, servidor de procesos de Hola y servidor de destino maestro Hola.
    - Vea un vídeo introductorio rápido

        > [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video1-Source-Infrastructure-Setup/player]

    - En la máquina virtual del servidor de configuración de hello, asegúrese de que el reloj del sistema de Hola se sincroniza con un [servidor horario](https://technet.microsoft.com/windows-server-docs/identity/ad-ds/get-started/windows-time-service/windows-time-service). Deben ser iguales. Si hay una diferencia de 15 minutos, antes o después, se podría producir un error en la instalación.
    - Ejecute el programa de instalación como administrador Local en la máquina virtual del servidor de configuración de Hola.
    - Asegúrese de que TLS 1.0 está habilitado en hello máquina virtual.


[!INCLUDE [site-recovery-add-configuration-server](../../includes/site-recovery-add-configuration-server.md)]

> [!NOTE]
> También se puede instalar el servidor de configuración de Hello [desde la línea de comandos de hello](http://aka.ms/installconfigsrv).



## <a name="connect-toovmware-servers"></a>Conectar servidores tooVMware

tooallow Azure Site Recovery toodiscover máquinas virtuales que ejecutan en su entorno local, debe tooconnect el servidor VMware vCenter o hosts de ESXi vSphere con Site Recovery. Tenga en cuenta los siguiente Hola antes de empezar:

- Si Agregar servidor de vCenter Hola o vSphere hosts tooSite recuperación con una cuenta sin privilegios de administrador en el servidor de hello, cuenta de hello necesita estos privilegios habilitados:
    - Centro de datos, Almacén de datos, Carpeta, Host, Red, Recurso, Máquina virtual, vSphere Distributed Switch.
    - servidor de vCenter Hola necesita permisos de vistas de almacenamiento.
- Al agregar servidores de VMware tooSite recuperación, se pueden tardar 15 minutos o más para ellos tooappear en el portal de Hola.

### <a name="add-hello-account-for-automatic-discovery"></a>Agregar cuenta de hello para la detección automática

[!INCLUDE [site-recovery-add-vcenter-account](../../includes/site-recovery-add-vcenter-account.md)]

### <a name="set-up-a-connection"></a>Configuración de una conexión

Conectar tooservers como se indica a continuación:

1. Seleccione **+ vCenter** toostart conectar un servidor VMware vCenter o un host de VMware vSphere ESXi.
2. En **agregar vCenter**, especifique un nombre descriptivo para el servidor de vCenter o host de vSphere de hello y, a continuación, especifique la dirección IP de Hola o FQDN del servidor de Hola.
3. Deje el puerto de hello como 443 a menos que los servidores de VMware son toolisten configurado para las solicitudes en un puerto diferente. Seleccionar cuenta de hello tooconnect toohello servidor de VMware vCenter o vSphere ESXi. Haga clic en **Aceptar**.
4. Recuperación del sitio conecta a servidores de tooVMware mediante Hola especifica la configuración y detecta las máquinas virtuales.

> [!NOTE]
> Si va a agregar un servidor o un host con una cuenta que no tiene privilegios de administrador en el servidor de vCenter o host de hello, asegúrese de que la cuenta de hello tiene estos privilegios habilitados: Centro de datos, almacén de datos, carpeta, Host, red, recurso, Máquina Virtual, y vSphere conmutador distribuida. Además, servidor hello VMware vCenter necesita vistas de almacenamiento de hello habilitar privilegio.


## <a name="set-up-hello-target-environment"></a>Configurar el entorno de destino de Hola

Antes de configurar el entorno de destino de hello, asegúrese de que tiene una cuenta de almacenamiento de Azure y la configuración de red virtual.

1. Haga clic en **preparar infraestructura** > **destino**, y seleccione Hola desea toouse de suscripción de Azure.
2. Especifique si el modelo de implementación de destino está basado en Resource Manager o si es el clásico.
3. Site Recovery comprueba que tiene una o más cuentas de almacenamiento y redes compatibles.

   ![Destino](./media/vmware-walkthrough-source-target/gs-target.png)
4. Si no ha creado una cuenta de almacenamiento o red, haga clic en **+ cuenta de almacenamiento** o **+ red**, toocreate un administrador de recursos cuenta o red en línea.

## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 9: configurar una directiva de replicación](vmware-walkthrough-replication.md)
