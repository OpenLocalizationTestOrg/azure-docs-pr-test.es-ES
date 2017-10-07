---
title: "aaaSet seguridad Hola origen y de destino para tooAzure de replicación de Hyper-V (con System Center VMM) con Azure Site Recovery | Documentos de Microsoft"
description: "Resume Hola pasos tooset la configuración de origen y de destino para la replicación de máquinas virtuales de Hyper-V en el almacenamiento de tooAzure de nubes VMM con Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5edb6d87-25a5-40fe-b6f1-ddf7b55a6b31
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/25/2017
ms.author: raynew
ms.openlocfilehash: 3f8c5386cb64527c775aef636980bac098ee9905
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-hello-source-and-target-for-hyper-v-with-vmm-replication-tooazure"></a>Paso 8: Configurar origen de Hola y de destino para tooAzure de replicación de Hyper-V (con VMM)

Después de [crear un almacén](vmm-to-azure-walkthrough-create-vault.md) y especificar lo que desee tooreplicate, usar este origen de tooconfigure de artículo y configuración de destino al replicar máquinas virtuales de Hyper-V local en System Center Virtual Machine Manager (VMM) nubes tooAzure, con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.

Envíe los comentarios y preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="set-up-hello-source-environment"></a>Configurar el entorno de origen Hola

S1. Haga clic en **Preparar infraestructura** > **Origen**.

    ![Set up source](./media/vmm-to-azure-walkthrough-source-target/set-source1.png)

2. En **preparar origen**, haga clic en **+ VMM** tooadd un servidor VMM.

    ![Configurar origen](./media/vmm-to-azure-walkthrough-source-target/set-source2.png)

3. En **Agregar servidor**, compruebe que **servidor de System Center VMM** aparece en **tipo de servidor** y ese servidor VMM Hola cumple hello [requisitos previos y la dirección URL requisitos de](#prerequisites).
4. Descargar archivo de instalación del proveedor de Azure Site Recovery de Hola.
5. Descargue la clave de registro de hello. Se le solicitará cuando ejecute el programa de instalación. clave de Hello es válida durante cinco días después de generarlo.

    ![Configurar origen](./media/vmm-to-azure-walkthrough-source-target/set-source3.png)

## <a name="install-hello-provider-on-hello-vmm-server"></a>Instalar Hola proveedor en el servidor VMM Hola

1. Ejecute el archivo de configuración de proveedor de hello en el servidor VMM Hola.
2. En **Microsoft Update** puede optar por recibir actualizaciones para que las actualizaciones del proveedor se realicen según las directivas de Microsoft Update.
3. En **instalación**, acepte o modifique la ubicación de instalación de proveedor de hello predeterminada y haga clic en **instalar**.

    ![Ubicación de instalación](./media/vmm-to-azure-walkthrough-source-target/provider2.png)
4. Cuando finalice la instalación, haga clic en **registrar** tooregister servidor VMM hello en el almacén de Hola.
5. Hola **configuración del almacén** página, haga clic en **examinar** archivo clave del almacén de hello tooselect. Especifique la suscripción de Azure Site Recovery de Hola y el nombre del almacén de Hola.

    ![Registro de servidor](./media/vmm-to-azure-walkthrough-source-target/provider10.png)
6. En **conexión a Internet**, especifique cómo Hola proveedor se ejecuta en el servidor VMM Hola conectará tooSite recuperación sobre Hola internet.

   * Si desea Hola proveedor tooconnect directamente, seleccione **conectarse directamente tooAzure Site Recovery sin un proxy**.
   * Si el proxy existente requiere autenticación, o si desea toouse un proxy personalizado, seleccione **conectar tooAzure Site Recovery con un servidor proxy**.
   * Si usa a un proxy personalizado, especifique las credenciales, el puerto y dirección de Hola.
   * Si usa un proxy, se deben haber ya Hola direcciones URL permitidas se describe en [requisitos previos](#on-premises-prerequisites).
   * Si usa un proxy personalizado, una cuenta de ejecución de VMM (DRAProxyAccount) se creará automáticamente con hello especificada las credenciales del proxy. Configurar servidor proxy de Hola para que esta cuenta se pueda autenticar correctamente. configuración de la cuenta de Hello RunAs de VMM puede modificarse en la consola VMM Hola. En **configuración**, expanda **seguridad** > **cuentas de ejecución**y, a continuación, modificar contraseña Hola de DRAProxyAccount. Necesitará el servicio VMM hello toorestart para que esta configuración surta efecto.

     ![Internet](./media/vmm-to-azure-walkthrough-source-target/provider13.png)
7. Acepte o modifique la ubicación de Hola de un certificado SSL que se genera automáticamente para el cifrado de datos. Este certificado se usa si habilita el cifrado de datos para una nube protegida por Azure en el portal de Azure Site Recovery Hola. Mantenga el certificado en un lugar seguro. Al ejecutar una conmutación por error tooAzure necesitará toodecrypt, si está habilitado el cifrado de datos.
8. En **nombre del servidor**, especifique un servidor VMM Nombre_descriptivo tooidentify hello en el almacén de Hola. En una configuración de clúster, especifique el nombre de rol de clúster VMM Hola.
9. Habilitar **metadatos de sincronización en la nube**, si desea toosynchronize metadatos para todas las nubes en el servidor VMM de hello con almacén de Hola. Esta acción solo debe toohappen una vez en cada servidor. Si no desea toosynchronize todas las nubes, puede dejar esta configuración desactivada y sincronizar cada nube individualmente en las propiedades de la nube de hello en la consola VMM Hola. Haga clic en **registrar** toocomplete proceso de Hola.

    ![Registro de servidor](./media/vmm-to-azure-walkthrough-source-target/provider16.png)
10. Con ello, se iniciará el registro. Después de que finalice el registro, el servidor de Hola se muestra en **infraestructura del sitio de recuperación** > **servidores VMM**.


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a>Instalar a agente de servicios de recuperación de Azure de hello en hosts de Hyper-V

1. Una vez hayas configurado Hola proveedor, debe archivo de instalación de toodownload hello para el agente de servicios de recuperación de Azure de Hola. Ejecute el programa de instalación en cada servidor de Hyper-V en hello nube de VMM.

    ![Sitios de Hyper-V](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent1.png)
2. En **Comprobación de requisitos previos**, haga clic en **Siguiente**. Todos los requisitos previos que falten se instalarán automáticamente.

    ![Requisitos previos del agente de Recovery Services](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent2.png)
3. En **configuración de la instalación**, acepte o modifique la ubicación de instalación de Hola y ubicación de la caché de Hola. Hola caché se puede configurar en una unidad que tenga al menos 5 GB de almacenamiento disponible, pero se recomienda una unidad de caché con 600 GB o más de espacio libre. Luego haga clic en **Instalar**.
4. Una vez completada la instalación, haga clic en **cerrar** toofinish.

    ![Registro del agente MARS](./media/vmm-to-azure-walkthrough-source-target/hyperv-agent3.png)

### <a name="command-line-installation"></a>Instalación de la línea de comandos
Hola agente de servicios de recuperación de Microsoft Azure se puede instalar desde la línea de comandos mediante el siguiente comando de hello:

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a>Configurar tooSite de acceso de proxy de internet recuperación hosts de Hyper-V

agente de servicios de recuperación de Hello ejecutan en hosts de Hyper-V necesita tooAzure de acceso a internet para la replicación de máquina virtual. Si va a acceder a Hola a internet a través de un proxy, se configura como se indica a continuación:

1. Abra Hola MMC de copia de seguridad de Microsoft Azure complemento en el host de Hyper-V de Hola. De forma predeterminada, un acceso directo para copia de seguridad de Microsoft Azure está disponible en el escritorio de Hola o en Agent\bin\wabadmin de servicios de recuperación de C:\Program Files\Microsoft Azure.
2. En el complemento de hello, haga clic en **cambiar las propiedades de**.
3. En hello **configuración de Proxy** ficha, especifique la información del servidor proxy.

    ![Registro del agente MARS](./media/vmm-to-azure-walkthrough-source-target/mars-proxy.png)
4. Compruebe que el agente Hola puede llegar a las direcciones URL de hello descritas en hello [requisitos previos](#on-premises-prerequisites).

## <a name="set-up-hello-target-environment"></a>Configurar el entorno de destino de Hola
Especificar toobe de cuenta de almacenamiento de Azure Hola usada para la replicación y hello toowhich de red de Azure máquinas virtuales de Azure se conectará tras la conmutación por error.

1. Haga clic en **preparar infraestructura** > **destino**, seleccione la suscripción de Hola y Hola donde desea hello toocreate conmutado por error máquinas virtuales de grupo de recursos. Elija el modelo de implementación de Hola que desee toouse en Azure (classic o recurso management) para hello conmutado por error máquinas virtuales.

    ![Storage](./media/vmm-to-azure-walkthrough-source-target/enablerep3.png)

2. Site Recovery comprueba que tiene una o más redes y cuentas de Azure Storage compatibles.

    ![Storage](./media/vmm-to-azure-walkthrough-source-target/compatible-storage.png)

3. Si no ha creado una cuenta de almacenamiento, y desea toocreate uno mediante el Administrador de recursos, haga clic en **+ cuenta de almacenamiento** toodo en esa línea.  En hello **crear cuenta de almacenamiento** hoja especificar un nombre de cuenta, el tipo, la suscripción y la ubicación. cuenta de Hello debe tener Hola misma ubicación que hello del almacén de servicios de recuperación.

   ![Storage](./media/vmm-to-azure-walkthrough-source-target/gs-createstorage.png)


   * Si desea toocreate una cuenta de almacenamiento con el modelo clásico de hello, hacer esto en hello portal de Azure. [Más información](../storage/common/storage-create-storage-account.md)
   * Si está usando una cuenta de almacenamiento premium para los datos replicados, configurar una cuenta de almacenamiento estándar adicional, registros de replicación de toostore que capturen datos tooon local de los cambios en curso.
5. Si no ha creado una red de Azure y desea toocreate uno mediante el Administrador de recursos, haga clic en **+ red** toodo en esa línea. En hello **crear red virtual** hoja especificar un nombre de red, intervalo de direcciones, detalles de subred, suscripción y ubicación. red de Hello debe formar parte de hello misma ubicación que hello del almacén de servicios de recuperación.

   ![Red](./media/vmm-to-azure-walkthrough-source-target/gs-createnetwork.png)

   Si desea que una red con el modelo clásico de hello toocreate, hacer esto en hello portal de Azure. [Más información](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).





## <a name="next-steps"></a>Pasos siguientes

Vaya demasiado[paso 9: configurar la asignación de red](vmm-to-azure-walkthrough-network-mapping.md)
