---
title: aaaMigrating tooAzure almacenamiento Premium con Azure Site Recovery | Documentos de Microsoft
description: "Migre su tooAzure de máquinas virtuales existentes almacenamiento Premium con Site Recovery. El Almacenamiento premium le ofrece compatibilidad con discos de alto rendimiento y baja latencia para cargas de trabajo con un uso intensivo de E/S, que se ejecutan en máquinas virtuales de Azure."
services: storage
cloud: Azure
documentationcenter: na
author: luywang
manager: kavithag
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: luywang
ms.openlocfilehash: cb71c06e4a1a73d484e226a573d1ade48c87664d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-toopremium-storage-using-azure-site-recovery"></a>Migrar tooPremium almacenamiento con Azure Site Recovery

[Azure Premium Storage](storage-premium-storage.md) le ofrece soporte de disco de alto rendimiento y latencia baja para máquinas virtuales (VM) que ejecutan cargas de trabajo intensivas de E/S. Hola de esta guía sirve toohelp usuarios migración sus discos de máquina virtual de un tooa de cuenta de almacenamiento estándar cuenta de almacenamiento Premium mediante [Azure Site Recovery](../site-recovery/site-recovery-overview.md).

Recuperación del sitio es un servicio de Azure que contribuye tooyour la continuidad del negocio y estrategia de recuperación ante desastres mediante la coordinación de Hola replicación de servidores físicos locales y máquinas virtuales en la nube toohello (Azure) o tooa centro de datos secundario. Cuando se producen interrupciones en la ubicación principal, conmutación por error tookeep aplicaciones de toohello ubicación secundaria y las cargas de trabajo disponibles. Producirá un error de ubicación principal tooyour atrás cuando devuelve toonormal operación. Site Recovery ofrece toosupport de recuperación ante desastres de las conmutaciones por error de prueba sin que afecte a los entornos de producción. Puede ejecutar conmutaciones por error con la mínima pérdida de datos (según la frecuencia de replicación) para desastres inesperados. En el escenario de Hola de migrar tooPremium almacenamiento, puede usar hello [conmutación por error de Site Recovery](../site-recovery/site-recovery-failover.md) en tooa de discos de destino de Azure Site Recovery toomigrate cuenta de almacenamiento Premium.

Se recomienda migrar tooPremium almacenamiento mediante el uso de Site Recovery porque esta opción proporciona el tiempo de inactividad mínimo y evita la ejecución manual de Hola de copiar los discos y la creación de nuevas máquinas virtuales. Site Recovery de forma sistemática copiará los discos y creará nuevas máquinas virtuales durante la conmutación por error. Site Recovery admite varios tipos de conmutación por error con un tiempo de inactividad mínimo, o ninguno. tooplan la pérdida de datos de tiempo de inactividad y la estimación, vea hello [tipos de conmutación por error](../site-recovery/site-recovery-failover.md) tabla en Site Recovery. Si se [preparar tooconnect tooAzure las máquinas virtuales después de la conmutación por error](../site-recovery/site-recovery-vmware-to-azure.md), debe ser capaz de tooconnect toohello máquina virtual de Azure con RDP después de la conmutación por error.

![][1]

## <a name="azure-site-recovery-components"></a>Componentes de Azure Site Recovery

Estos son los componentes de Site Recovery de Hola que son relevantes toothis escenario de migración.

* El **servidor de configuración** es una máquina virtual de Azure que coordina la comunicación y administra los procesos de replicación y recuperación de datos. En esta máquina virtual se ejecutará un servidor de configuración de instalación de un solo archivo tooinstall hello y un componente adicional, denominado un servidor de procesos, como una puerta de enlace de replicación. Lea sobre los [requisitos previos del servidor de configuración](../site-recovery/site-recovery-vmware-to-azure.md). Servidor de configuración sólo necesita toobe configurarse una vez y se puede utilizar para todos los toohello migraciones misma región.

* **Servidor de procesos** es una puerta de enlace de replicación que recibe datos de replicación de máquinas virtuales de origen optimiza Hola datos con almacenamiento en caché, la compresión y cifrado y lo envía tooa cuenta de almacenamiento. También controla la instalación de inserción de toosource de servicio de movilidad de hello las máquinas virtuales y realiza la detección automática de las máquinas virtuales de origen. servidor de proceso de Hello predeterminado está instalado en el servidor de configuración de Hola. Puede implementar tooscale de servidores de proceso adicional independiente de la implementación. Obtenga información sobre [los procedimientos recomendados para la implementación de servidor de procesos](https://azure.microsoft.com/blog/best-practices-for-process-server-deployment-when-protecting-vmware-and-physical-workloads-with-azure-site-recovery/) y [la implementación de los servidores de procesos adicionales](../site-recovery/site-recovery-plan-capacity-vmware.md#deploy-additional-process-servers). Solo necesita toobe una vez configurado el servidor de procesos y puede utilizarse para todos los toohello de migraciones misma región.

* **Servicio de movilidad** es un componente que se implementa en cada máquina virtual estándar que desee tooreplicate. Captura escrituras de datos en Hola VM estándar y los reenvía toohello servidor de procesos. Lea sobre los [requisitos previos de máquinas replicadas](../site-recovery/site-recovery-vmware-to-azure.md).

En el gráfico se muestra cómo interactúan estos componentes.

![][15]

> [!NOTE]
> Recuperación de sitio no admite la migración de Hola de discos de espacios de almacenamiento.

Para los componentes adicionales para otros escenarios, consulte demasiado[arquitectura del escenario](../site-recovery/site-recovery-vmware-to-azure.md).

## <a name="azure-essentials"></a>Información esencial de Azure

Estos son Hola requisitos de Azure para este escenario de migración.

* Una suscripción de Azure
* Un toostore de cuenta de almacenamiento de Azure Premium los datos replicados
* Cuando se crean en la conmutación por error, se conectará un toowhich de red virtual de Azure (VNet) las máquinas virtuales. red virtual de Azure Hello debe ser una en Hola la misma región como Hola uno en qué Hola se ejecuta la recuperación del sitio
* Una cuenta de almacenamiento de Azure estándar en los registros de replicación de toostore. Puede tratarse de Hola la misma cuenta de almacenamiento como discos de hello VM que se está migrando

## <a name="prerequisites"></a>Requisitos previos

* Entender los componentes del escenario de migración relevante Hola Hola sección anterior
* Planear el tiempo de inactividad por aprendizaje sobre hello [conmutación por error de Site Recovery](../site-recovery/site-recovery-failover.md)

## <a name="setup-and-migration-steps"></a>Pasos de configuración y migración

Puede utilizar Site Recovery toomigrate máquinas virtuales de IaaS de Azure entre regiones o dentro de la misma región. Hello las instrucciones siguientes se han adaptado a este escenario de migración de artículo hello [replicar máquinas virtuales de VMware o en servidores físicos tooAzure](../site-recovery/site-recovery-vmware-to-azure.md). Siga los vínculos de Hola para obtener pasos detallados en instrucciones de toohello adicionales en este artículo.

1. **Creación de un almacén de Recovery Services** Crear y administrar el almacén de Site Recovery de Hola a través de hello [portal de Azure](https://portal.azure.com). Haga clic en **Nuevo** > **Administración** > **Backup** y **Site Recovery (OMS)**. También puede hacer clic en **Examinar** > **Almacén de Recovery Services** > **Agregar**. Máquinas virtuales será región toohello replicada que especifique en este paso. A fin de saludo de la migración en hello misma región, región de hello seleccione dónde están las máquinas virtuales de origen y la cuentas de almacenamiento de origen. Tenga en cuenta que las cuentas de almacenamiento de migración tooPremium solo se admite en hello [portal de Azure](https://portal.azure.com), no Hola [portal clásico](https://manage.windowsazure.com).

2. Hello pasos siguientes le ayudarán a **elegir los objetivos de protección**.

    2a. En VM donde desea que el servidor de configuración de tooinstall Hola Hola, abra hello [portal de Azure](https://portal.azure.com). Vaya demasiado**servicios de recuperación de los almacenes de credenciales** > **configuración**. En **Configuración**, seleccione **Site Recovery**. En **Site Recovery**, seleccione **Paso 1: Preparar la infraestructura**. En **Preparar la infraestructura**, seleccione **Objetivo de protección**.

    ![][2]

    2b. En **objetivo de protección**, en Hola la primera lista desplegable, seleccione **tooAzure**. En la lista desplegable segundo de hello, seleccione **no virtualizados / otros**y, a continuación, haga clic en **Aceptar**.

    ![][3]

3. Hello pasos siguientes le ayudarán a **configurar el entorno de origen (servidor de configuración) de hello**.

    3a. Descargar hello **instalación unificada de Azure Site Recovery** hello y **clave de registro del almacén** por van toohello **preparar infraestructura**  >  **Origen preparación** > **Agregar servidor** hoja. Necesitará Hola toorun clave Hola unificado de instalación de almacén de registro. clave de Hello es válida durante 5 días después de generarlo.

    ![][4]

    3b. Agregar servidor de configuración de hello **Agregar servidor** hoja.

    ![][5]

    3c. En la máquina virtual que se va a utilizar como servidor de configuración de Hola Hola, ejecutar servidores de configuración de instalación unificada tooinstall Hola y Hola procesos. Puede comenzar con capturas de pantalla de hello [aquí](../site-recovery/site-recovery-vmware-to-azure.md) instalación de hello toocomplete. Puede hacer referencia a toohello siguientes capturas de pantalla de pasos especificados en este escenario de migración.

    En **antes de comenzar**, seleccione **instalar servidores de configuración de Hola y procesos**.

    ![][6]

    3d. En **registro**, busque y seleccione la clave de registro de hello descargó desde el almacén de Hola.

    ![][7]

    3e. En **detalles del entorno**, seleccione si se va a máquinas virtuales de VMware tooreplicate. En este escenario de migración, elija **No**.

    ![][8]

    3f. Una vez completada la instalación de hello, verá hello **servidor de configuración de recuperación de sitio de Microsoft Azure** ventana. Usar hello **administrar cuentas** pestaña cuenta de hello toocreate que puede usar Site Recovery para la detección automática. (En caso de hello sobre cómo proteger los equipos físicos, configurar la cuenta de hello no es relevante, pero necesita al menos un tooenable cuenta uno de hello siguiendo los pasos. En este caso, puede asignar Hola cuenta y la contraseña como ninguno.) Hola de uso **registro del almacén** archivo de credenciales de almacén de ficha tooupload Hola.

    ![][9]

4. **Configurar el entorno de destino de hello**. Haga clic en **preparar infraestructura** > **destino**y especifique el modelo de implementación de Hola que desea toouse para las máquinas virtuales después de la conmutación por error. Puede elegir **Clásico** o **Resource Manager**, en función de su escenario.

    ![][10]

    Site Recovery comprueba que tiene una o más redes y cuentas de Azure Storage compatibles. Tenga en cuenta que si usa una cuenta de almacenamiento Premium para los datos replicados, necesario tooset la una replicación de toostore de cuenta de almacenamiento estándar adicional registros.

5. **Configure las opciones de replicación**. Siga [establecer la configuración de replicación](../site-recovery/site-recovery-vmware-to-azure.md) tooverify que el servidor de configuración se asoció correctamente al crear la directiva de replicación de Hola.

6. **Planeamiento de capacidad** Hola de uso [planificador de capacidad](../site-recovery/site-recovery-capacity-planner.md) ancho de banda de red de estimación de tooaccurately, almacenamiento y otro requisitos toomeet necesita la replicación. Cuando haya terminado, seleccione **Sí** en **¿Completó el planeamiento de capacidad?**.

    ![][11]

7. Hello pasos siguientes le ayudarán a **instalar el servicio de movilidad y habilitar la replicación**.

    7a. Puede elegir demasiado[instalación de inserción](../site-recovery/site-recovery-vmware-to-azure.md) tooyour origen máquinas virtuales o demasiado[instalar manualmente el servicio de movilidad](../site-recovery/site-recovery-vmware-to-azure-install-mob-svc.md) en el origen de las máquinas virtuales. Puede encontrar requisito Hola de instalación de inserción y la ruta de acceso de hello del instalador manual de hello en el vínculo de hello proporcionado. Si está realizando una instalación manual, deberá toouse un servidor de configuración de IP dirección toofind Hola interno.

    ![][12]

    Hola se conmutó por error máquina virtual tendrá dos discos temporales: uno de Hola hello otro creado durante el aprovisionamiento de Hola de máquina virtual en la región de recuperación de Hola y máquina virtual principal. tooexclude Hola temporal en el disco antes de la réplica, instale el servicio de movilidad de hello antes de habilitar la replicación. toolearn más información acerca de cómo tooexclude Hola disco temporal, consulte demasiado[excluir discos de replicación](../site-recovery/site-recovery-vmware-to-azure.md).

    7b. Ahora habilite la replicación como sigue:
      * Haga clic en **Replicar la aplicación** > **Origen**. Después de habilitar la replicación para hello la primera vez, haga clic en + replicar en la replicación de tooenable de almacén de Hola para máquinas adicionales.
      * En el paso 1, configure el origen como servidor de procesos.
      * En el paso 2, especifique modelo de implementación de conmutación por error de post hello, un toomigrate de cuenta de almacenamiento Premium a, registros de toosave de la cuenta de almacenamiento estándar y un toofail de red virtual a.
      * En el paso 3, agregar máquinas virtuales protegidas por dirección IP (es posible que tenga una toofind de dirección IP interna ellos).
      * En el paso 4, configurar propiedades de hello seleccionando cuentas Hola que configuró anteriormente en el servidor de procesos de Hola.
      * En el paso 5, seleccione Directiva de replicación de Hola que creó anteriormente, establecer la configuración de replicación.
      Haga clic en **Aceptar** y habilite la replicación.

    > [!NOTE]
    > Cuando se cancela la asignación y vuelva a iniciar una VM de Azure, no hay ninguna garantía de que obtendrá Hola la misma dirección IP. Si la dirección IP de hello del servidor de proceso del servidor de configuración de Hola o hello protegida cambio de máquinas virtuales de Azure, la replicación de hello en este escenario no funcionen correctamente.

    ![][13]

    Cuando se diseña el entorno de Azure Storage, se recomienda utilizar cuentas de almacenamiento separadas para cada máquina virtual en un conjunto de disponibilidad. Es recomendable que siga el procedimiento recomendado de hello en la capa de almacenamiento de hello demasiado[utilizar varias cuentas de almacenamiento para cada conjunto de disponibilidad](../virtual-machines/windows/manage-availability.md). Distribución de cuentas de almacenamiento VM discos toomultiple ayuda a tooimprove la disponibilidad de almacenamiento y distribuye Hola E/S por la infraestructura de almacenamiento de Azure Hola. Si las máquinas virtuales están en un conjunto de disponibilidad, en lugar de replicar los discos de todas las máquinas virtuales en una cuenta de almacenamiento, se recomienda migrar varias máquinas virtuales varias veces, por lo que Hola hello las máquinas virtuales en el mismo conjunto de disponibilidad no comparten una única cuenta de almacenamiento. Hola de uso **Habilitar replicación** tooset de hoja de una cuenta de almacenamiento de destino para cada máquina virtual, uno en uno. Puede elegir un modelo de implementación de conmutación por error de post según la necesidad de tooyour. Si elige el Administrador de recursos (RM) como su modelo de implementación de conmutación por error de post, puede conmutar por error un tooan RM VM RM VM o puede conmutar por error un tooan VM clásico VM de RM.

8. **Ejecute una conmutación por error de prueba**. toocheck si la replicación ha finalizado, haga clic en la recuperación del sitio y, a continuación, haga clic en **configuración** > **replican elementos**. Verá el estado de Hola y el porcentaje de su proceso de replicación. Después de la replicación inicial es toovalidate de conmutación por error completa, ejecute la estrategia de replicación. Para obtener pasos detallados de conmutación por error de prueba, consulte demasiado[ejecutar una prueba de conmutación por error de Site Recovery](../site-recovery/site-recovery-vmware-to-azure.md). Puede ver el estado de Hola de conmutación por error de prueba en **configuración** > **trabajos** > **YOUR_FAILOVER_PLAN_NAME**. En la hoja de hello, verá un desglose de los pasos de Hola y resultados de correcto o con errores. Si se produce un error en la conmutación por error de prueba de Hola en cualquier paso, haga clic en el mensaje de error de hello paso toocheck Hola. Asegúrese de que las máquinas virtuales y la estrategia de replicación cumplan requisitos de hello antes de ejecutar una conmutación por error. Lectura [tooAzure probar conmutación por error de Site Recovery](../site-recovery/site-recovery-test-failover-to-azure.md) para obtener más información e instrucciones de conmutación por error de prueba.

9. **Ejecute una conmutación por error**. Una vez completada la conmutación por error de prueba de hello, ejecute una conmutación por error toomigrate el almacenamiento de discos tooPremium y replicar instancias de máquina virtual de Hola. Siga Hola detallan los pasos en [ejecutar una conmutación por error](../site-recovery/site-recovery-failover.md#run-a-failover). Asegúrese de seleccionar **apagar las máquinas virtuales y sincronizar los datos más recientes de hello** toospecify que Site Recovery debe intente tooshut hacia abajo Hola protegida las máquinas virtuales y sincronizar los datos de Hola para que hello versión más reciente de los datos de hello conmutarán por error. Si no selecciona esta opción u Hola intento no tiene éxito Hola conmutación por error será desde el punto de recuperación más reciente disponible de Hola para hello VM. Recuperación de sitio creará una instancia VM cuyo tipo es hello igual o similar tooa Premium con capacidad de almacenamiento: VM. Puede comprobar el rendimiento de Hola y el precio de varias instancias de máquina virtual yendo demasiado[precios de máquinas virtuales de Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/) o [precios de máquinas virtuales de Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/).

## <a name="post-migration-steps"></a>Pasos posteriores a la migración

1. **Configurar la disponibilidad de toohello máquinas virtuales replicada defina si es necesario**. Recuperación del sitio no admite la migración de máquinas virtuales junto con el conjunto de disponibilidad de Hola. Dependiendo de la implementación de hello de la máquina virtual replicada, siga uno de los procedimientos de hello:
  * Para una máquina virtual que creó mediante el modelo de implementación clásica de hello: agregar Hola VM toohello conjunto de disponibilidad en hello portal de Azure. Para obtener instrucciones detalladas, vaya demasiado[agrega un conjunto de disponibilidad de tooan de máquina virtual existente](../virtual-machines/windows/classic/configure-availability.md#addmachine).
  * Para el modelo de implementación del Administrador de recursos de hello: guardar la configuración del programa Hola a máquina virtual y, a continuación, eliminar y volver a crear las máquinas virtuales de hello en el conjunto de disponibilidad de Hola. toodo usar por lo tanto, el script de Hola en [establecer Azure Resource Manager VM conjunto de disponibilidad](https://gallery.technet.microsoft.com/Set-Azure-Resource-Manager-f7509ec4). Compruebe la limitación de Hola de esta secuencia de comandos y planear el tiempo de inactividad antes de ejecutar script de Hola.

2. **Elimine las máquinas virtuales y los discos antiguos**. Antes de eliminar estos, asegúrese de que los discos Premium Hola son coherentes con hello que nuevas máquinas virtuales realizan Hola la misma función que el origen de hello las máquinas virtuales y discos de origen. En el modelo de implementación del Administrador de recursos (RM) hello, eliminar Hola VM y eliminar discos Hola de las cuentas de almacenamiento de origen en hello portal de Azure. En el modelo de implementación clásica de hello, puede eliminar Hola VM y discos en el portal clásico de Hola o portal de Azure. Si hay un problema en qué Hola disco no se elimina aunque eliminado Hola VM, consulte [solucionar errores al eliminar discos duros virtuales](storage-resource-manager-cannot-delete-storage-account-container-vhd.md).

3. **Infraestructura de Azure Site Recovery Hola limpia**. Si ya no es necesaria la recuperación de sitio, puede limpiar su infraestructura eliminando los elementos replicados, servidor de configuración de Hola y Hola directiva de recuperación, y, a continuación, eliminar el almacén de Azure Site Recovery de Hola.

## <a name="troubleshooting"></a>Solución de problemas

* [Protección de supervisión y solución de problemas para las máquinas virtuales y los servidores físicos](../site-recovery/site-recovery-monitoring-and-troubleshooting.md)
* [Foro de Microsoft Azure Site Recovery](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr)

## <a name="next-steps"></a>Pasos siguientes

Vea Hola recursos para escenarios específicos para migrar máquinas virtuales siguientes:

* [Migrar máquinas virtuales de Azure entre cuentas de almacenamiento](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [Crear y cargar un VHD de Windows Server tooAzure.](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Crear y cargar un disco duro Virtual que contiene Hola sistema operativo Linux](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Migración de máquinas virtuales de Amazon AWS tooMicrosoft Azure](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

Además, vea Hola después recursos toolearn más información sobre el almacenamiento de Azure y máquinas virtuales de Azure:

* [Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Máquinas virtuales de Azure](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Almacenamiento premium: Almacenamiento de alto rendimiento para cargas de trabajo de máquina virtual de Azure](storage-premium-storage.md)

[1]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-1.png
[2]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-2.png
[3]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-3.png
[4]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-4.png
[5]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-5.png
[6]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-6.PNG
[7]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-7.PNG
[8]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-8.PNG
[9]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-9.PNG
[10]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-10.png
[11]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-11.PNG
[12]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-12.PNG
[13]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-13.png
[14]:../site-recovery/media/site-recovery-vmware-to-azure/v2a-architecture-henry.png
[15]:./media/storage-migrate-to-premium-storage-using-azure-site-recovery/migrate-to-premium-storage-using-azure-site-recovery-14.png
