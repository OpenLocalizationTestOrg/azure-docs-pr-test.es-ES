---
title: "nubes de máquinas virtuales de Hyper-V en VMM aaaReplicate tooAzure | Documentos de Microsoft"
description: "Orquestar la replicación, la conmutación por error y la recuperación de máquinas virtuales de Hyper-V administrados en tooAzure de nubes de System Center VMM"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: tysonn
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: 84182fe4b63862ac7643208a22f236a7515a25a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a>Replicar máquinas virtuales de Hyper-V en tooAzure de nubes VMM con Site Recovery en hello portal de Azure
> [!div class="op_single_selector"]
> * [Portal de Azure](site-recovery-vmm-to-azure.md)
> * [Azure clásico](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [PowerShell clásico](site-recovery-deploy-with-powershell.md)


Este artículo describe cómo tooreplicate local máquinas virtuales de Hyper-V administrados en tooAzure de nubes de System Center VMM, con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure.

Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

Si desea toomigrate máquinas tooAzure (sin conmutación por recuperación), obtenga más información en [este artículo](site-recovery-migrate-to-azure.md).


## <a name="deployment-steps"></a>Pasos de implementación

Siga estos pasos de implementación de hello artículo toocomplete:


1. [Obtener más información](site-recovery-components.md) acerca de la arquitectura de Hola para esta implementación. Además, [conozca](site-recovery-hyper-v-azure-architecture.md) cómo funciona la replicación de Hyper-V en Site Recovery.
2. Compruebe los requisitos previos y las limitaciones.
3. Configure las cuentas de red y almacenamiento de Azure.
4. Preparar el servidor VMM local de Hola y hosts de Hyper-V.
5. Cree un almacén de Recovery Services. Hola almacén contiene valores de configuración y organiza la replicación.
6. Especifique la configuración de origen. Registrar servidor VMM de hello en el almacén de Hola. Instale hello Azure Site Recovery Provider en el agente de servicios de recuperación de Microsoft de hello instalar servidor VMM hello en hosts de Hyper-V.
7. Especifique la configuración de destino y replicación.
8. Habilitar la replicación de hello las máquinas virtuales.
9. Ejecutar un toomake de conmutación por error de prueba que todo funciona según lo previsto.



## <a name="prerequisites"></a>Requisitos previos


**Requisito de compatibilidad** | **Detalles**
--- | ---
**Las tablas de Azure** | Obtenga información sobre los [requisitos de Azure](site-recovery-prereq.md#azure-requirements)
**Servidores locales** | [Obtener más información](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-in-vmm-clouds-to-azure) sobre los requisitos para el servidor VMM local de Hola y hosts de Hyper-V.
**Máquinas virtuales de Hyper-V locales** | Las máquinas virtuales que desee tooreplicate debe estar en ejecución una [sistema operativo compatible](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)y cumplir con [requisitos previos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**Direcciones URL de Azure** | servidor VMM Hola necesita tener acceso a direcciones URL toothese:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Si tiene reglas de firewall basado en la dirección IP, asegúrate de que permiten tooAzure de comunicación.<br/></br> Permitir hello [intervalos de IP del centro de datos de Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)y Hola puerto HTTPS (443).<br/></br> Permitir que los intervalos de direcciones IP para hello región de Azure de su suscripción y oeste de Estados Unidos (utilizado para el Control de acceso y administración de identidades).


## <a name="prepare-for-deployment"></a>Preparación de la implementación
tooprepare para la implementación, debe:

1. [Configurar una red de Azure](#set-up-an-azure-network) en la que se coloquen las máquinas virtuales de Azure después de la conmutación por error.
2. [Configurar una cuenta de almacenamiento de Azure](#set-up-an-azure-storage-account) para datos replicados.
3. [Preparar el servidor VMM hello](#prepare-the-vmm-server) para la implementación de Site Recovery.
4. Preparar la asignación de red. Configurar redes para que pueda configurar la asignación de red durante la implementación de Site Recovery.

### <a name="set-up-an-azure-network"></a>Configurar una red de Azure
Es necesario un toowhich de red de Azure VM de Azure creadas después de que se conectará la conmutación por error.

* red de Hello debe formar parte de hello misma región que hello del almacén de servicios de recuperación.
* Según el modelo de recursos de Hola que desee toouse para conmutado por error máquinas virtuales de Azure, configurar el Hola con la red de Azure en [modo de administrador de recursos](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) o [modo clásico](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).
* Es recomendable configurar una red antes de empezar. Si no lo hace, deberá toodo durante la implementación de Site Recovery.
Las redes de Azure que usa recuperación del sitio no pueden ser [movido](../azure-resource-manager/resource-group-move-resources.md) dentro de hello mismo, o entre distintas, suscripciones.

### <a name="set-up-an-azure-storage-account"></a>Configurar una cuenta de almacenamiento de Azure
* Necesita una cuenta de almacenamiento de Azure toohold datos replican tooAzure estándar o premium. [Almacenamiento premium](../storage/common/storage-premium-storage.md) se usa para las máquinas virtuales que necesitan un rendimiento de E/S alto y cargas de trabajo intensivas de baja latencia toohost E/S. Si desea que toouse un toostore de cuenta premium los datos replicados, también necesita un registros de replicación toostore de la cuenta de almacenamiento estándar que captura continua cambia datos tooon locales. cuenta de Hello debe estar en hello misma región que hello del almacén de servicios de recuperación.
* Según el modelo de recursos de Hola que desee toouse para conmutado por error máquinas virtuales de Azure, configure una cuenta en [modo de administrador de recursos](../storage/common/storage-create-storage-account.md) o [modo clásico](../storage/common/storage-create-storage-account.md).
* Es recomendable configurar una cuenta antes de empezar. Si no lo hace, deberá toodo durante la implementación de Site Recovery.
- Tenga en cuenta que las cuentas de almacenamiento utilizadas por recuperación del sitio no pueden ser [movido](../azure-resource-manager/resource-group-move-resources.md) dentro de hello mismo, o entre distintas, suscripciones.

### <a name="prepare-hello-vmm-server"></a>Preparar el servidor VMM Hola
* Asegúrese de que ese servidor VMM Hola cumple con hello [requisitos previos](#prerequisites).
* Durante la implementación de recuperación del sitio, puede especificar que todas las nubes en un servidor VMM deben estar disponibles en hello portal de Azure. Si solo desea tooappear de nubes específicas en el portal de hello, puede habilitar a esa configuración en la nube de hello en la consola de administración VMM Hola.

### <a name="prepare-for-network-mapping"></a>Preparar la asignación de red
Debe configurar la asignación de red durante la implementación de Site Recovery. Asignación de red asigna entre redes de VM de VMM de origen y destino redes de Azure, hello tooenable siguientes:

* Máquinas que conmutan en hello misma red pueden conectarse tooeach otro, incluso si no está conmutación por error en Hola de igual manera u Hola mismo plan de recuperación.
* Si se configura una puerta de enlace de red en red Azure de destino de hello, máquinas virtuales de Azure puede conectarse a máquinas virtuales locales tooon.
* tooset la asignación de red, esto es lo necesita:

  * Asegúrese de que las máquinas virtuales en el origen de hello servidor host Hyper-V están conectado tooa red de VM de VMM. Esta red debe ser tooa vinculado red lógica que está asociado a la nube de Hola.
  * Una red de Azure como la descrita [anteriormente](#set-up-an-azure-network)

## <a name="create-a-recovery-services-vault"></a>Creación de un almacén de Recovery Services
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **Nuevo** > **Supervisión y administración** > **Backup y Site Recovery (OMS)**.

    ![Almacén nuevo](./media/site-recovery-vmm-to-azure/new-vault3.png)
3. En **nombre**, especificar un almacén de hello tooidentify nombre descriptivo. Si tiene más de una suscripción, seleccione una de ellas.
4. [Cree un grupo de recursos](../azure-resource-manager/resource-group-template-deploy-portal.md)o seleccione uno existente. Especifique una región de Azure. Las máquinas estén región toothis replicada. toocheck admite regiones, consulte disponibilidad geográfica en [detalles de precios de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
5. Si desea que tooquickly acceso Hola almacén de hello panel, haga clic en **Pin toodashboard** > **crear almacén**.

    ![Almacén nuevo](./media/site-recovery-vmm-to-azure/new-vault.png)

nuevo almacén de Hello aparece en hello **panel** > **todos los recursos**y en hello principal **servicios de recuperación de los almacenes de credenciales** hoja.


## <a name="select-hello-protection-goal"></a>Seleccione el objetivo de protección de Hola

Seleccione la acción que realizará tooreplicate, y donde quiera tooreplicate a.

1. En **servicios de recuperación de los almacenes de credenciales**, seleccione el almacén de Hola.
2. En **Introducción**, haga clic en **Site Recovery** > **Preparar infraestructura** > **Objetivo de protección**.

    ![Elegir objetivos](./media/site-recovery-vmm-to-azure/choose-goals.png)
3. En **objetivo de protección** seleccione **tooAzure**y seleccione **Sí, con Hyper-V**. Seleccione **Sí** tooconfirm usa toomanage Hyper-V hosts VMM y el sitio de recuperación de Hola. y, a continuación, haga clic en **Aceptar**.

## <a name="set-up-hello-source-environment"></a>Configurar el entorno de origen Hola

Instale hello Azure Site Recovery Provider en servidor VMM de Hola y registrar servidor hello en el almacén de Hola. Instalar a agente de servicios de recuperación de Azure de hello en hosts de Hyper-V.

1. Haga clic en **Preparar infraestructura** > **Origen**.

    ![Configurar origen](./media/site-recovery-vmm-to-azure/set-source1.png)

2. En **preparar origen**, haga clic en **+ VMM** tooadd un servidor VMM.

    ![Configurar origen](./media/site-recovery-vmm-to-azure/set-source2.png)

3. En **Agregar servidor**, compruebe que **servidor de System Center VMM** aparece en **tipo de servidor** y ese servidor VMM Hola cumple hello [requisitos previos y la dirección URL requisitos de](#prerequisites).
4. Descargar archivo de instalación del proveedor de Azure Site Recovery de Hola.
5. Descargue la clave de registro de hello. Se le solicitará cuando ejecute el programa de instalación. clave de Hello es válida durante cinco días después de generarlo.

    ![Configurar origen](./media/site-recovery-vmm-to-azure/set-source3.png)


## <a name="install-hello-provider-on-hello-vmm-server"></a>Instalar Hola proveedor en el servidor VMM Hola

1. Ejecute el archivo de configuración de proveedor de hello en el servidor VMM Hola.
2. En **Microsoft Update** puede optar por recibir actualizaciones para que las actualizaciones del proveedor se realicen según las directivas de Microsoft Update.
3. En **instalación**, acepte o modifique la ubicación de instalación de proveedor de hello predeterminada y haga clic en **instalar**.

    ![Ubicación de instalación](./media/site-recovery-vmm-to-azure/provider2.png)
4. Cuando finalice la instalación, haga clic en **registrar** tooregister servidor VMM hello en el almacén de Hola.
5. Hola **configuración del almacén** página, haga clic en **examinar** archivo clave del almacén de hello tooselect. Especifique la suscripción de Azure Site Recovery de Hola y el nombre del almacén de Hola.

    ![Registro de servidor](./media/site-recovery-vmm-to-azure/provider10.PNG)
6. En **conexión a Internet**, especifique cómo Hola proveedor se ejecuta en el servidor VMM Hola conectará tooSite recuperación sobre Hola internet.

   * Si desea Hola proveedor tooconnect directamente, seleccione **conectarse directamente tooAzure Site Recovery sin un proxy**.
   * Si el proxy existente requiere autenticación, o si desea toouse un proxy personalizado, seleccione **conectar tooAzure Site Recovery con un servidor proxy**.
   * Si usa a un proxy personalizado, especifique las credenciales, el puerto y dirección de Hola.
   * Si usa un proxy, se deben haber ya Hola direcciones URL permitidas se describe en [requisitos previos](#on-premises-prerequisites).
   * Si usa un proxy personalizado, una cuenta de ejecución de VMM (DRAProxyAccount) se creará automáticamente con hello especificada las credenciales del proxy. Configurar servidor proxy de Hola para que esta cuenta se pueda autenticar correctamente. configuración de la cuenta de Hello RunAs de VMM puede modificarse en la consola VMM Hola. En **configuración**, expanda **seguridad** > **cuentas de ejecución**y, a continuación, modificar contraseña Hola de DRAProxyAccount. Necesitará el servicio VMM hello toorestart para que esta configuración surta efecto.

     ![Internet](./media/site-recovery-vmm-to-azure/provider13.PNG)
7. Acepte o modifique la ubicación de Hola de un certificado SSL que se genera automáticamente para el cifrado de datos. Este certificado se usa si habilita el cifrado de datos para una nube protegida por Azure en el portal de Azure Site Recovery Hola. Mantenga el certificado en un lugar seguro. Al ejecutar una conmutación por error tooAzure necesitará toodecrypt, si está habilitado el cifrado de datos.

    > [!NOTE]
    > Se recomienda la capacidad de cifrado de hello toouse proporcionada por Azure para cifrar datos en reposo, en lugar de usar la opción de cifrado de datos de hello proporcionada por Azure Site Recovery. capacidad de cifrado de Hello proporcionada por Azure puede activarse para un almacenamiento > de la cuenta y le ayuda a lograr un mejor rendimiento como Hola cifrado/descifrado es controlado por el almacenamiento de Azure.
    > [Más información acerca del cifrado del servicio Storage desde Azure](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption).
    
8. En **nombre del servidor**, especifique un servidor VMM Nombre_descriptivo tooidentify hello en el almacén de Hola. En una configuración de clúster, especifique el nombre de rol de clúster VMM Hola.
9. Habilitar **metadatos de sincronización en la nube**, si desea toosynchronize metadatos para todas las nubes en el servidor VMM de hello con almacén de Hola. Esta acción solo debe toohappen una vez en cada servidor. Si no desea toosynchronize todas las nubes, puede dejar esta configuración desactivada y sincronizar cada nube individualmente en las propiedades de la nube de hello en la consola VMM Hola. Haga clic en **registrar** toocomplete proceso de Hola.

    ![Registro de servidor](./media/site-recovery-vmm-to-azure/provider16.PNG)
10. Con ello, se iniciará el registro. Después de que finalice el registro, el servidor de Hola se muestra en **infraestructura del sitio de recuperación** > **servidores VMM**.


## <a name="install-hello-azure-recovery-services-agent-on-hyper-v-hosts"></a>Instalar a agente de servicios de recuperación de Azure de hello en hosts de Hyper-V

1. Una vez hayas configurado Hola proveedor, debe archivo de instalación de toodownload hello para el agente de servicios de recuperación de Azure de Hola. Ejecute el programa de instalación en cada servidor de Hyper-V en hello nube de VMM.

    ![Sitios de Hyper-V](./media/site-recovery-vmm-to-azure/hyperv-agent1.png)
2. En **Comprobación de requisitos previos**, haga clic en **Siguiente**. Todos los requisitos previos que falten se instalarán automáticamente.

    ![Requisitos previos del agente de Recovery Services](./media/site-recovery-vmm-to-azure/hyperv-agent2.png)
3. En **configuración de la instalación**, acepte o modifique la ubicación de instalación de Hola y ubicación de la caché de Hola. Hola caché se puede configurar en una unidad que tenga al menos 5 GB de almacenamiento disponible, pero se recomienda una unidad de caché con 600 GB o más de espacio libre. Luego haga clic en **Instalar**.
4. Una vez completada la instalación, haga clic en **cerrar** toofinish.

    ![Registro del agente MARS](./media/site-recovery-vmm-to-azure/hyperv-agent3.png)

### <a name="command-line-installation"></a>Instalación de la línea de comandos
Hola agente de servicios de recuperación de Microsoft Azure se puede instalar desde la línea de comandos mediante el siguiente comando de hello:

     marsagentinstaller.exe /q /nu

### <a name="set-up-internet-proxy-access-toosite-recovery-from-hyper-v-hosts"></a>Configurar tooSite de acceso de proxy de internet recuperación hosts de Hyper-V

agente de servicios de recuperación de Hello ejecutan en hosts de Hyper-V necesita tooAzure de acceso a internet para la replicación de máquina virtual. Si va a acceder a Hola a internet a través de un proxy, se configura como se indica a continuación:

1. Abra Hola MMC de copia de seguridad de Microsoft Azure complemento en el host de Hyper-V de Hola. De forma predeterminada, un acceso directo para copia de seguridad de Microsoft Azure está disponible en el escritorio de Hola o en Agent\bin\wabadmin de servicios de recuperación de C:\Program Files\Microsoft Azure.
2. En el complemento de hello, haga clic en **cambiar las propiedades de**.
3. En hello **configuración de Proxy** ficha, especifique la información del servidor proxy.

    ![Registro del agente MARS](./media/site-recovery-vmm-to-azure/mars-proxy.png)
4. Compruebe que el agente Hola puede llegar a las direcciones URL de hello descritas en hello [requisitos previos](#on-premises-prerequisites).

## <a name="set-up-hello-target-environment"></a>Configurar el entorno de destino de Hola
Especificar toobe de cuenta de almacenamiento de Azure Hola usada para la replicación y hello toowhich de red de Azure máquinas virtuales de Azure se conectará tras la conmutación por error.

1. Haga clic en **preparar infraestructura** > **destino**, seleccione la suscripción de Hola y Hola donde desea hello toocreate conmutado por error máquinas virtuales de grupo de recursos. Elija el modelo de implementación de Hola que desee toouse en Azure (classic o recurso management) para hello conmutado por error máquinas virtuales.

    ![Storage](./media/site-recovery-vmm-to-azure/enablerep3.png)

2. Site Recovery comprueba que tiene una o más redes y cuentas de Azure Storage compatibles.

    ![Storage](./media/site-recovery-vmm-to-azure/compatible-storage.png)

3. Si no ha creado una cuenta de almacenamiento, y desea toocreate uno mediante el Administrador de recursos, haga clic en **+ cuenta de almacenamiento** toodo en esa línea.  En hello **crear cuenta de almacenamiento** hoja especificar un nombre de cuenta, el tipo, la suscripción y la ubicación. cuenta de Hello debe tener Hola misma ubicación que hello del almacén de servicios de recuperación.

   ![Storage](./media/site-recovery-vmm-to-azure/gs-createstorage.png)


   * Si desea toocreate una cuenta de almacenamiento con el modelo clásico de hello, hacer esto en hello portal de Azure. [Más información](../storage/common/storage-create-storage-account.md)
   * Si está usando una cuenta de almacenamiento premium para los datos replicados, configurar una cuenta de almacenamiento estándar adicional, registros de replicación de toostore que capturen datos tooon local de los cambios en curso.
5. Si no ha creado una red de Azure y desea toocreate uno mediante el Administrador de recursos, haga clic en **+ red** toodo en esa línea. En hello **crear red virtual** hoja especificar un nombre de red, intervalo de direcciones, detalles de subred, suscripción y ubicación. red de Hello debe formar parte de hello misma ubicación que hello del almacén de servicios de recuperación.

   ![Red](./media/site-recovery-vmm-to-azure/gs-createnetwork.png)

   Si desea que una red con el modelo clásico de hello toocreate, hacer esto en hello portal de Azure. [Más información](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).

### <a name="configure-network-mapping"></a>Configurar asignación de red

* [Lea](#prepare-for-network-mapping) una rápida introducción de lo que puede hacer la asignación de redes.
* Compruebe que máquinas virtuales en el servidor VMM Hola son redes VM de tooa conectado y que ha creado al menos una red virtual de Azure. Varias redes de VM pueden ser asignado tooa sola red de Azure.

Configure la asignación como sigue:

1. En **infraestructura del sitio de recuperación** > **asignaciones de red** > **asignación de red**, haga clic en hello **+ la asignación de red**  icono.

    ![Asignación de red](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. En **Agregar asignación de red**, seleccione servidor VMM de origen de hello, y **Azure** como destino de Hola.
3. Comprobar la suscripción de Hola y el modelo de implementación de hello después de la conmutación por error.
4. En **red de origen**, seleccione red VM de hello origen local que desee toomap de lista de hello asociado con el servidor VMM Hola.
5. En **red de destino**, seleccione Hola red de Azure en qué réplica de máquinas virtuales de Azure se ubicarán cuando se crean. y, a continuación, haga clic en **Aceptar**.

    ![Asignación de red](./media/site-recovery-vmm-to-azure/network-mapping2.png)

Esto es lo que sucede cuando comienza la asignación de red:

* Las máquinas virtuales existentes en la red de VM de origen Hola son redes de destino de toohello conectado cuando comience la asignación. Nueva red de VM de origen de toohello conectadas las máquinas virtuales conectadas toohello asigna red de Azure cuando se produce la replicación.
* Si modifica una asignación de red existente, máquinas virtuales de réplica conectarse con la nueva configuración de Hola.
* Si la red de destino de hello tiene varias subredes y una de estas subredes se Hola mismo nombre que la subred en la máquina virtual de origen de Hola se encuentra, máquina virtual de réplica de hello conecta toothat subred de destino después de la conmutación por error.
* Si no hay ninguna subred de destino con un nombre coincidente, máquina virtual de hello conecta toohello primera subred de red de Hola.

## <a name="configure-replication-settings"></a>Configuración de las opciones de replicación
1. toocreate una nueva directiva de replicación, haga clic en **preparar infraestructura** > **configuración de replicación** > **+ crear y asociar**.

    ![Red](./media/site-recovery-vmm-to-azure/gs-replication.png)
2. En **Crear y asociar directiva**, especifique un nombre de directiva.
3. En **copiar frecuencia**, especifique la frecuencia con desea tooreplicate diferencias de datos después de la replicación inicial de hello (cada 30 segundos, 5 o 15 minutos).

    > [!NOTE]
    >  No se admite una frecuencia de segundo 30 al replicar toopremium almacenamiento. limitación de Hello viene determinado por el número de Hola de instantáneas por blob (100) compatible con almacenamiento premium. [Más información](../storage/common/storage-premium-storage.md#snapshots-and-copy-blob)

4. En **retención de punto de recuperación**, especifique en horas cuánto va un período de retención Hola para cada punto de recuperación. Equipos protegidos pueden ser recuperado tooany punto dentro de una ventana.
5. En **Frecuencia de instantánea coherente con la aplicación**especifique la frecuencia (entre 1 y 12 horas) con la que se crearán los puntos de recuperación que contengan las instantáneas coherentes con la aplicación. Hyper-V usa dos tipos de instantáneas, una instantánea estándar que proporciona una instantánea incremental de la máquina virtual completa de hello y una instantánea coherente con la aplicación que toma una instantánea de tiempo de punto de datos de la aplicación hello dentro de la máquina virtual de Hola. Las instantáneas coherentes con la aplicación usan tooensure de servicio de instantáneas de volumen (VSS) que las aplicaciones están en un estado coherente cuando se tomó la instantánea de Hola. Tenga en cuenta que si habilita las instantáneas coherentes con la aplicación, afectará Hola rendimiento de aplicaciones que se ejecutan en máquinas virtuales de origen. Asegúrese de que el valor de hello especificado es menor que el número de Hola de puntos de recuperación adicionales que configure.
6. En **hora de inicio de la replicación inicial**, indicar al toostart Hola la replicación inicial. se produce la replicación de Hello sobre el ancho de banda de internet por lo que conviene tooschedule que fuera de su horario ocupado.
7. En **cifrar los datos almacenados en Azure**, especifique si tooencrypt datos de rest de almacenamiento de Azure. y, a continuación, haga clic en **Aceptar**.

    ![Directiva de replicación](./media/site-recovery-vmm-to-azure/gs-replication2.png)
8. Cuando se crea una nueva directiva automáticamente tiene asociadas con hello nube de VMM. Haga clic en **Aceptar**. Puede asociar más nubes de VMM (hello y máquinas virtuales en ellos) con esta directiva de replicación en **replicación** > nombre de directiva > **asociar la nube de VMM**.

    ![Directiva de replicación](./media/site-recovery-vmm-to-azure/policy-associate.png)

## <a name="capacity-planning"></a>Planificación de capacidad

Ahora que tiene la infraestructura básica configurada, planee la capacidad y averigüe si necesitará recursos adicionales.

Recuperación de sitio proporciona un toohelp planificador de capacidad, asignar recursos adecuados de Hola para su entorno de origen, componentes de Site Recovery, redes y almacenamiento. Puede ejecutar programador de hello en el modo rápido para realizar cálculos en función de un promedio de las máquinas virtuales, discos y almacenamiento, o en el modo detallado en el que había entrada figuras en nivel de carga de trabajo de Hola. Antes de comenzar:

* Recopilar información sobre su entorno de replicación, incluidas las máquinas virtuales, discos por máquina virtual y almacenamiento por disco.
* Tasa de cambio (renovación) diaria de estimación Hola tendrá de los datos replicados. Puede usar hello [planificador de capacidad de réplica de Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) toohelp para ello.

1. Haga clic en **descargar**, toodownload Hola herramienta y, a continuación, ejecútelo. [Leer el artículo de hello](site-recovery-capacity-planner.md) que acompaña a la herramienta de Hola.
2. ¿Cuando haya terminado, seleccione **Sí** en **han ejecutado Hola Capacity Planner**?

   ![Planificación de capacidad](./media/site-recovery-vmm-to-azure/gs-capacity-planning.png)

   Más información sobre el [control del ancho de banda de red](#network-bandwidth-considerations)




## <a name="enable-replication"></a>Habilitar replicación

Antes de empezar, asegúrese de que la cuenta de usuario de Azure tiene Hola necesario [permisos](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable la replicación de una nueva tooAzure de máquina virtual.

Ahora habilite la replicación como sigue:

1. Haga clic en **Paso 2: Replicar la aplicación** > **Origen**. Después de habilitar la replicación para hello la primera vez, haga clic en **+ replicar** en la replicación de tooenable de almacén de Hola para máquinas adicionales.

    ![Habilitar replicación](./media/site-recovery-vmm-to-azure/enable-replication1.png)
2. Hola **origen** hoja, seleccione Hola servidor VMM y en la nube hello en qué Hola Hyper-V están ubicados los hosts. y, a continuación, haga clic en **Aceptar**.

    ![Habilitar replicación](./media/site-recovery-vmm-to-azure/enable-replication-source.png)
3. En **destino**, seleccione la suscripción de hello, modelo de implementación de conmutación por error de post, y Hola cuenta de almacenamiento que está usando para los datos replicados.

    ![Habilitar replicación](./media/site-recovery-vmm-to-azure/enable-replication-target.png)
4. Seleccione la cuenta de almacenamiento de Hola que desee toouse. Si desea toouse una cuenta de almacenamiento diferentes que los tiene, puede [crear uno](#set-up-an-azure-storage-account). Si usa una cuenta de almacenamiento premium para los datos replicados, necesita tooselect un registros de replicación de toostore de cuenta de almacenamiento estándar adicional que capturan los cambios continuos tooon local data.toocreate una cuenta de almacenamiento mediante el modelo de administrador de recursos de Hola Haga clic en **crear nuevo**. Si desea toocreate una cuenta de almacenamiento con el modelo clásico de hello, hacerlo [Hola portal de Azure](../storage/common/storage-create-storage-account.md). y, a continuación, haga clic en **Aceptar**.
5. Seleccione hello Azure toowhich de red y subred de máquinas virtuales de Azure se conectará, cuando se crean después de la conmutación por error. Seleccione **configurar ahora para las máquinas seleccionadas**, tooapply Hola red configuración tooall máquinas que seleccione para la protección. Seleccione **configurar más adelante**, tooselect hello Azure red por máquina. Si desea toouse de las que tiene una red distinta, puede [crear uno](#set-up-an-azure-network). Haga clic en el modelo de administrador de recursos de Hola de toocreate una red con **crear nuevo**. Si desea toocreate una red con el modelo clásico de hello, hacerlo [Hola portal de Azure](../virtual-network/virtual-networks-create-vnet-classic-pportal.md). Seleccione una subred si es posible. y, a continuación, haga clic en **Aceptar**.
6. En **máquinas virtuales** > **seleccionar las máquinas virtuales**, haga clic en y seleccione cada máquina tooreplicate. Solo puede seleccionar aquellas máquinas en las que se pueda habilitar la replicación. A continuación, haga clic en **Aceptar**.

    ![Habilitar replicación](./media/site-recovery-vmm-to-azure/enable-replication5.png)

7. En **propiedades** > **configurar las propiedades**, seleccione sistema de operativo Hola Hola selecciona las máquinas virtuales y Hola disco del sistema operativo.

    - Comprueba cumple ese nombre de máquina virtual de Azure (nombre de destino) de hello [requisitos de la máquina virtual de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).   
    - De forma predeterminada se seleccionan todos los discos de Hola de hello VM para la replicación, pero puede borrar discos tooexclude ellos.

        - Puede ser conveniente tooexclude discos tooreduce del ancho de banda. Por ejemplo, puede no ser conveniente tooreplicate discos con los datos temporales o datos que se actualizan cada vez que un equipo o en las aplicaciones se reinicia (por ejemplo, pagefile.sys o tempdb de Microsoft SQL Server). Puede excluir disco Hola de replicación por disco de hello anule su selección.
        - Solo se pueden excluir los discos básicos. Los discos del sistema operativo no se pueden excluir.
        - Se recomienda no excluir discos dinámicos. Site Recovery no se puede identificar si un disco duro virtual de una máquina virtual invitada es básico o dinámico. Si no se excluyen todos los discos de los volúmenes dinámicos dependientes, disco dinámico protegido de Hola se mostrará como un disco con errores cuando hello máquina virtual conmuta por error y datos de hello en ese disco no será accesibles.
        - Una vez habilitada la replicación, no puede agregar ni quitar discos para la replicación. Si desea que tooadd o excluir un disco, necesita protección toodisable Hola VM y, a continuación, volver a habilitarla.
        - No se produce una conmutación por recuperación de los discos que se crean manualmente en Azure. Por ejemplo, si se producirá un error en más de tres discos y cree dos directamente en la máquina virtual de Azure, solo Hola tres discos que se han conmutado por error desde Azure tooHyper-V. No se incluyen discos creados manualmente en la conmutación por recuperación, o en la replicación inversa de Hyper-V tooAzure.
        - Si excluye un disco que se necesita para una aplicación toooperate, después de la conmutación por error tooAzure debe toocreate puede ejecutarse manualmente en Azure, por lo que ese saludo replica aplicación. Como alternativa, puede integrar automatización de Azure en un plan de recuperación, disco de hello toocreate durante la conmutación por error de la máquina de Hola.

    Haga clic en **Aceptar** toosave cambios. Puede establecer propiedades adicionales más adelante.

    ![Habilitar replicación](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

8. En **configuración de replicación** > **establecer configuración de replicación**, seleccione Directiva de replicación de Hola que desee tooapply para hello protegido máquinas virtuales. y, a continuación, haga clic en **Aceptar**. Puede modificar la directiva de replicación de hello en **directivas de replicación** > nombre de directiva > **modificar configuración**. Los cambios que aplique se utilizarán tanto para las máquinas que ya se estén replicando como para otras nuevas.

   ![Habilitar replicación](./media/site-recovery-vmm-to-azure/enable-replication7.png)

Puede seguir el progreso del programa Hola a **Habilitar protección** de trabajo en **trabajos** > **trabajos de recuperación del sitio**. Después de hello **finalización de protección** se ejecuta el trabajo, Hola máquina está lista para conmutación por error.

### <a name="view-and-manage-vm-properties"></a>Visualización y administración de las propiedades de la máquina virtual

Se recomienda que compruebe las propiedades de Hola de máquina de origen de Hola. Recuerde que ese nombre de máquina virtual de Azure Hola debe cumplir con los [requisitos de la máquina virtual de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

1. En **elementos protegidos**, haga clic en **replican elementos**, y seleccione Hola máquina toosee sus detalles.

    ![Habilitar replicación](./media/site-recovery-vmm-to-azure/vm-essentials.png)
2. En **propiedades**, puede ver la replicación y Hola de información de conmutación por error de máquina virtual.

    ![Habilitar replicación](./media/site-recovery-vmm-to-azure/test-failover2.png)
3. En **de proceso y de red** > **propiedades de proceso**, puede especificar el tamaño de nombre y de destino de la máquina virtual de Azure de Hola. Modificar Hola nombre toocomply con [requisitos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) si necesita. También puede ver y modificar la información acerca de la red de destino de hello, subred y dirección IP de Hola que asigna toohello máquina virtual de Azure.
Observe lo siguiente:

   * Puede establecer la dirección IP de destino de Hola. Si no proporciona una dirección, Hola conmutado por error equipo usará DHCP. Si establece una dirección que no está disponible en la conmutación por error, se producirá un error en la conmutación por error de Hola. Hola la misma dirección IP de destino puede usarse para la conmutación por error si está disponible en la red de conmutación por error de prueba de Hola Hola dirección.
   * número de Hola de adaptadores de red es dictados por tamaño de Hola que especifique para la máquina virtual de destino de hello, del siguiente modo:

     * Si el número de Hola de adaptadores de red en la máquina de origen de hello es menor o igual toohello de adaptadores permitidas para el tamaño de máquina de destino de hello, a continuación, tendrá destino Hola Hola el mismo número de adaptadores como origen de Hola.
     * Si se supera el número de Hola de adaptadores para la máquina virtual de origen de Hola Hola permitidas para el tamaño de destino de hello, a continuación, se utiliza el tamaño máximo de hello destino.
     * Por ejemplo, si una máquina de origen tiene dos adaptadores de red y tamaño de máquina de destino de hello es compatible con cuatro, el equipo de destino Hola tendrá dos adaptadores. Si la máquina de origen hello tiene dos adaptadores de pero hello tamaño de destino admitida solo admite un, equipo de destino de Hola tendrá solo un adaptador.     
     * Si Hola máquina virtual tiene varios adaptadores de red, se conectarán todos toohello misma red.

     ![Habilitar replicación](./media/site-recovery-vmm-to-azure/test-failover4.png)

4. En **discos** puede ver los discos de datos y sistema operativo de hello en hello máquina virtual que se replicarán.

#### <a name="managed-disks"></a>Discos administrados

En **de proceso y de red** > **propiedades de proceso**, puede establecer "Discos administrados por usar" configuración demasiado "Sí" para hello VM si desea que tooattach discos administrados tooyour máquina en tooAzure de migración. Discos administrados simplifica la administración de discos para máquinas virtuales de IaaS de Azure debido a que administra las cuentas de almacenamiento de hello asociadas con discos de máquina virtual de Hola. [Más información sobre discos administrados](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview).

   - Discos administrados son toohello creado y adjunta máquina virtual sólo una tooAzure de conmutación por error. Al habilitar la protección, datos de máquinas locales seguirán tooreplicate toostorage cuentas.
   Discos administrados pueden crearse únicamente para máquinas virtuales implementadas mediante el modelo de implementación de administrador de recursos de Hola.  

  > [!NOTE]
  > Conmutación por recuperación del entorno de Hyper-V de Azure tooon local no se admite actualmente para equipos con discos administrados. Establezca "Discos administrados por uso" demasiado "Sí" Si piensa toomigrate esta máquina a Azure.

   - Cuando se establece "Discos administrados por uso" demasiado "Sí", solo conjuntos de disponibilidad de grupo de recursos de hello con "Discos administrados por uso" conjunto demasiado "Sí" estaría disponibles para la selección. Esto es porque las máquinas virtuales con discos administrados sólo puede ser parte de los conjuntos de disponibilidad con el conjunto de propiedades de "Use administrado discos" demasiado "Sí". Asegúrese de crear conjuntos de disponibilidad con el conjunto de propiedades de "Use administrado discos" en función de los discos de intención toouse administrado en la conmutación por error.  Del mismo modo, cuando se establece "Discos administrados por uso" demasiado "No", solo conjuntos de disponibilidad de grupo de recursos de hello con "Discos administrados por uso" propiedad establecida demasiado "No" estaría disponibles para la selección. [Más información sobre discos administrados y conjuntos de disponibilidad](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability#use-managed-disks-for-vms-in-an-availability-set).

  > [!NOTE]
  > Si la cuenta de almacenamiento de hello usada para la replicación se cifró con cifrado de servicio de almacenamiento en cualquier momento en el tiempo, se producirá un error en la creación de discos administrados durante la conmutación por error. Se puede establecer "Discos administrados por uso" demasiado "No" y vuelva a intentar la conmutación por error o deshabilite la protección de máquina virtual de Hola y proteger tooa cuenta de almacenamiento que no tenía el cifrado del servicio de almacenamiento habilitado en cualquier momento en el tiempo.
  > [Más información sobre el Cifrado del servicio de Storage y los discos administrados](https://docs.microsoft.com/en-us/azure/storage/storage-managed-disks-overview#managed-disks-and-encryption).


## <a name="test-hello-deployment"></a>Implementación de prueba de Hola

implementación de Hola de tootest, puede ejecutar una prueba de conmutación por error para una sola máquina virtual o un plan de recuperación que contiene una o más máquinas virtuales.

### <a name="before-you-start"></a>Antes de comenzar

 - Si desea que tooconnect tooAzure máquinas virtuales mediante RDP después de la conmutación por error, obtenga información acerca de [preparar tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover).
 - prueba de toofully necesita toocopy de Active Directory y DNS en el entorno de prueba. [Más información](site-recovery-active-directory.md#test-failover-considerations).

### <a name="run-a-test-failover"></a>Ejecución de una conmutación por error de prueba

1. toofail a través de una sola máquina virtual, en **replican elementos**, haga clic en hello VM > **+ conmutación por error de prueba**.
2. toofail a través de una recuperación del plan, en **planes de recuperación**, plan de hello contextual > **conmutación por error de prueba**. un plan de recuperación, toocreate [, siga estas instrucciones](site-recovery-create-recovery-plans.md).
3. En **conmutación por error de prueba**, seleccione hello toowhich de red de Azure máquinas virtuales de Azure conectarse después de producirse la conmutación por error.
4. Haga clic en **Aceptar** conmutación por error de toobegin Hola. Puede seguir el progreso haciendo clic en hello VM tooopen sus propiedades o en hello **conmutación por error de prueba** de trabajo en **trabajos de recuperación del sitio**.
5. Una vez completada la conmutación por error de hello, también debe poder réplica de hello toosee máquina Azure aparecen en hello portal de Azure > **máquinas virtuales**. Debe asegurarse de que esa máquina virtual de hello es tamaño adecuado de hello, que ha conectado toohello de red adecuada y se está ejecutando.
6. Si preparado para las conexiones después de la conmutación por error, debe ser capaz de tooconnect toohello máquina virtual de Azure.
7. Una vez que haya terminado, haga clic en **conmutación por error de prueba de limpieza** Hola plan de recuperación. En **notas** registrar y guardar las observaciones asociadas con conmutación por error de prueba de Hola. Esto eliminará máquinas virtuales de Hola que se crearon durante la conmutación por error de prueba.

Para obtener más información, lea hello [tooAzure de conmutación por error de prueba](site-recovery-test-failover-to-azure.md) artículo.

## <a name="monitor-hello-deployment"></a>Implementación de Hola de Monitor

Le mostramos cómo puede supervisar los valores de configuración, estado y el estado de implementación de Site Recovery hello:

1. Haga clic en Hola de tooaccess de nombre de almacén de hello **Essentials** panel. En este panel puede ver los trabajos de Site Recovery, el estado de la replicación, los planes de recuperación, y el estado y los eventos del servidor.  Puede personalizar **Essentials** tooshow Hola iconos y las distribuciones que están tooyou más útil, incluido el estado de Hola de otros almacenes de copia de seguridad y recuperación del sitio.

    ![Essentials](./media/site-recovery-vmm-to-azure/essentials.png)
2. En **estado**, puede supervisar problemas en local (el servidor VMM o configuración) y Hola eventos que ocurran Site Recovery en hello últimas 24 horas.
3. Hola **replican elementos**, **planes de recuperación**, y **trabajos de recuperación de sitio** iconos puede administrar y supervisar la replicación. Puede ver más detalles de los trabajos en **Trabajos** > **Trabajos de Site Recovery**.

## <a name="command-line-installation-for-hello-azure-site-recovery-provider"></a>Instalación de línea de comandos para hello Azure Site Recovery Provider

Hola proveedor de Azure Site Recovery puede instalarse desde Hola de línea de comandos. Este método puede ser utilizado tooinstall Hola proveedor en Server Core de Windows Server 2012 R2.

1. Hola proveedor carpeta de instalación de archivos y registro tooa clave de descarga. Por ejemplo, C:\ASR.
2. Desde un símbolo del sistema con privilegios elevados, ejecute a estas instalador de proveedor de comandos tooextract hello:

            C:\Windows\System32> CD C:\ASR
            C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. Ejecute este comando tooinstall componentes hello:

            C:\ASR> setupdr.exe /i
4. A continuación, ejecute estos comandos, el servidor de hello tooregister en el almacén de hello:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>       

Donde:

* **/ Credenciales de**: parámetro obligatorio que especifica donde se encuentra archivo de clave de registro de hello.  
* **/ FriendlyName**: parámetro obligatorio Nombre hello del servidor de host de Hyper-V de Hola que aparece en el portal de Azure Site Recovery Hola.
* * **/ EncryptionEnabled**: tooAzure de nubes de parámetro opcional al replicar máquinas virtuales de Hyper-V en VMM. Especifique si desea que tooencrypt las máquinas virtuales en Azure (en el cifrado de rest). Asegúrese de que Hola nombre de archivo hello tiene un **.pfx** extensión. El cifrado está desactivado de forma predeterminada.

    > [!NOTE]
    > Se recomienda la capacidad de cifrado de hello toouse proporcionada por Azure para cifrar datos en reposo, en lugar de usar la opción de cifrado de hello (opción de EncryptionEnabled) proporcionada por Azure Site Recovery. capacidad de cifrado de Hello proporcionada por Azure puede activarse para una cuenta de almacenamiento y ayuda a lograr un mejor rendimiento como Hola cifrado/descifrado se realiza por Azure  
    > .
    > [Más información acerca del cifrado del servicio Storage en Azure](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption).
    
* **/proxyAddress**: parámetro opcional que especifica la dirección de saludo del servidor de proxy de Hola.
* **/proxyPort**: parámetro opcional que especifica el puerto de saludo del servidor de proxy de Hola.
* **/ proxyusername**: parámetro opcional que especifica el nombre de usuario de proxy de hello (si el servidor proxy requiere autenticación).
* **/ proxypassword**: parámetro opcional que especifica Hola contraseña tooauthenticate con el servidor proxy (si el proxy de hello requiere autenticación).


### <a name="network-bandwidth-considerations"></a>Consideraciones sobre el ancho de banda de red
Puede usar Hola capacidad planner herramienta toocalculate Hola ancho de banda que necesario para la replicación (la replicación inicial y, a continuación, delta). cantidad de hello toocontrol de uso de ancho de banda para la replicación, tiene algunas opciones:

* **Limitar ancho de banda**: tráfico de Hyper-V que se replica el sitio secundario tooa pasa a través de un host de Hyper-V específico. También puede limitar el ancho de banda en el servidor de host de Hola.
* **Ajustar el ancho de banda**: puede influir en el ancho de banda de hello utilizado para la replicación con un par de claves del registro.

#### <a name="throttle-bandwidth"></a>Limitar el ancho de banda
1. Abra Hola MMC de copia de seguridad de Microsoft Azure complemento en el servidor de host de Hyper-V de Hola. De forma predeterminada, un acceso directo para copia de seguridad de Microsoft Azure está disponible en el escritorio de Hola o en Agent\bin\wabadmin de servicios de recuperación de C:\Program Files\Microsoft Azure.
2. En el complemento de hello, haga clic en **cambiar las propiedades de**.
3. En hello **limitación** ficha, seleccione **Habilitar límite para las operaciones de copia de seguridad de uso de ancho de banda de internet**y establecer los límites de hello para el trabajo y no laborables horas. Intervalo válido es de 512 Kbps too102 Mbps por segundo.

    ![Limitar el ancho de banda](./media/site-recovery-vmm-to-azure/throttle2.png)

También puede usar hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) cmdlet tooset limitación. Aquí tiene un ejemplo:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** indica que no se requiere ninguna limitación.

#### <a name="influence-network-bandwidth"></a>Control del uso de ancho de banda de red
Hola **UploadThreadsPerVM** controles de valor del registro Hola número de subprocesos que se usan para la transferencia de datos (la replicación inicial o delta) de un disco. Un valor mayor aumenta el ancho de banda de red de hello usada para la replicación. Hola **DownloadThreadsPerVM** el valor del registro especifica el número de Hola de subprocesos usados para la transferencia de datos durante la conmutación por recuperación.

1. En el registro de hello, vaya demasiado**Backup\Replication de Azure HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows**.

   * Modificar valor de hello **UploadThreadsPerVM** (o crear clave de hello si no existe) toocontrol subprocesos que se utilizan para la replicación de disco.
   * Modificar valor de hello **DownloadThreadsPerVM** (o crear clave de hello si no existe) toocontrol subprocesos que se utilizan para el tráfico de la conmutación por recuperación de Azure.
2. valor predeterminado de Hello es 4. En una red de "sobreaprovisionada", estas claves del registro deben cambiarse de valores predeterminados de Hola. Hola máximo es 32. Supervisar el tráfico toooptimize Hola valor.

## <a name="next-steps"></a>Pasos siguientes

Después de la replicación inicial se ha completado y ha probado la implementación de hello, puede invocar las conmutaciones por error según sea necesario Hola. [Obtener más información](site-recovery-failover.md) acerca de los diferentes tipos de conmutaciones por error y cómo toorun ellos.
