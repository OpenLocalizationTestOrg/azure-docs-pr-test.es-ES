---
title: "Copia de seguridad de Azure: Preparar tooback las máquinas virtuales | Documentos de Microsoft"
description: "Asegúrese de que el entorno esté preparado para hacer la copia de seguridad de máquinas virtuales en Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: copias de seguridad; realizar copia de seguridad
ms.assetid: e87e8db2-b4d9-40e1-a481-1aa560c03395
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: 5c3a41b5d3bd56e62ca5f207442867913aa99816
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-environment-tooback-up-resource-manager-deployed-virtual-machines"></a>Preparar su tooback entorno seguridad implementados por el Administrador de recursos de máquinas virtuales
> [!div class="op_single_selector"]
> * [Modelo de Resource Manager](backup-azure-arm-vms-prepare.md)
> * [Modelo clásico](backup-azure-vms-prepare.md)
>
>

Este artículo proporciona pasos de Hola para preparar su tooback entorno una máquina virtual que implementa el Administrador de recursos (VM). Hello pasos que se muestran en los procedimientos de hello usan hello portal de Azure.  

Hola servicio de copia de seguridad de Azure tiene dos tipos de almacenes de credenciales (copia de seguridad de almacenes y servicios de recuperación) para proteger las máquinas virtuales. Un almacén de copia de seguridad protege las máquinas virtuales implementadas mediante el modelo de implementación de hello clásico. Un almacén de Recovery Services protege **tanto las máquinas virtuales implementadas con el modelo clásico como las implementadas mediante Resource Manager**. Debe usar un tooprotect de almacén de servicios de recuperación una máquina virtual implementada por el Administrador de recursos.

> [!NOTE]
> Azure cuenta con dos modelos de implementación para crear recursos y trabajar con ellos: [Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md). Vea [preparar su tooback entorno las máquinas virtuales de Azure](backup-azure-vms-prepare.md) para obtener más información acerca de cómo trabajar con la implementación estándar de modelo máquinas virtuales.
>
>

Para proteger una máquina virtual implementada según el modelo de Resource Manager o realizar una copia de seguridad de una de estas máquinas, asegúrese de cumplir los siguientes requisitos previos:

* Crear un almacén de servicios de recuperación (o identificar un almacén de servicios de recuperación existente) *Hola misma ubicación que la máquina virtual*.
* Seleccionar un escenario, definir la directiva de copia de seguridad de Hola y definir elementos tooprotect.
* Compruebe la instalación de Hola de agente de máquina virtual en la máquina virtual.
* Ha comprobado la conectividad de la red
* Para máquinas virtuales de Linux, en caso de que desee toocustomize el entorno de copia de seguridad para las copias de seguridad coherente de aplicación siga hello [tooconfigure pasos previamente instantánea y posteriores a la instantánea las secuencias de comandos](https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent)

Si sabe que estas condiciones ya existen en su entorno, a continuación, continuar toohello [el artículo de máquinas virtuales de copia de seguridad](backup-azure-vms.md). Si necesita tooset o comprobar, cualquiera de estos requisitos previos, este artículo le guiará por hello pasos tooprepare ese requisito previo.

##<a name="supported-operating-system-for-backup"></a>Sistemas operativos compatibles para copia de seguridad
 * **Linux**: Copia de seguridad de Azure admite [una lista de distribuciones aprobadas por Azure](../virtual-machines/linux/endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) , con la excepción de CoreOS Linux. _Otras Bring-Your-posee-las distribuciones de Linux también pueden trabajar como agente de máquina virtual de hello está disponible en la máquina virtual de Hola y la compatibilidad con Python existe. Sin embargo, no respaldamos esas distribuciones para copia de seguridad._
 * **Windows Server**: no se admiten las versiones anteriores a Windows Server 2008 R2.

## <a name="limitations-when-backing-up-and-restoring-a-vm"></a>Limitaciones al realizar copias de seguridad y restaurar una máquina virtual
Antes de preparar su entorno, tenga en cuenta las limitaciones de Hola.

* No se admite la copia de seguridad de máquinas virtuales con más de 16 discos de datos.
* No se admite la copia de seguridad de máquinas virtuales con tamaños de disco de datos mayores que 1023 GB.
* No se admite la copia de seguridad de máquinas virtuales con una dirección IP reservada y sin puntos de conexión definidos.
* No se admite la copia de seguridad de máquinas virtuales cifradas simplemente mediante BEK. No se admite la copia de seguridad de máquinas virtuales Linux cifradas mediante el cifrado LUKS.
* No se recomienda la copia de seguridad de máquinas virtuales en la configuración Servidor de archivos de escalabilidad horizontal.
* Los datos de copia de seguridad no incluyen red montada las unidades conectadas tooVM.
* No se admite el reemplazo de una máquina virtual existente durante la restauración. Si intentas toorestore Hola VM cuando Hola máquina virtual no existe, se produce un error en la operación de restauración de Hola.
* No se admiten la restauración y la copia de seguridad entre regiones.
* Puede realizar copias de seguridad de máquinas virtuales en todas las regiones públicas de Azure (vea hello [lista de comprobación](https://azure.microsoft.com/regions/#services) de regiones admitidas). Si hoy es compatible región Hola que desea obtener, no aparecerá en la lista desplegable de Hola durante la creación del almacén.
* La restauración de una máquina virtual de controlador de dominio que forma parte de una configuración de varios controladores de dominio solo se admite a través de PowerShell. Más información sobre cómo [restaurar un controlador de dominio de varios controladores de dominio](backup-azure-restore-vms.md#restoring-domain-controller-vms)
* Se admite la restauración de máquinas virtuales que tengan Hola siguiendo las configuraciones de red especiales sólo a través de PowerShell. Máquinas virtuales creadas mediante el flujo de trabajo de restauración de Hola Hola interfaz de usuario no tendrá estas configuraciones de red una vez completada la operación de restauración de Hola. más información, consulte toolearn [restaurar las máquinas virtuales con las configuraciones de red especiales](backup-azure-restore-vms.md#restoring-vms-with-special-network-configurations).
  * Máquinas virtuales con la configuración del equilibrador de carga (interna y externa).
  * Máquinas virtuales con varias direcciones IP reservadas.
  * Máquinas virtuales con varios adaptadores de red.

## <a name="create-a-recovery-services-vault-for-a-vm"></a>Creación de un almacén de Servicios de recuperación para una máquina virtual
Un almacén de servicios de recuperación es una entidad que almacena las copias de seguridad de Hola y los puntos de recuperación que se han creado con el tiempo. almacén de servicios de recuperación de Hello también contiene directivas de copia de seguridad de hello asociadas a máquinas virtuales de hello protegido.

almacén de servicios de toocreate una recuperación:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú del concentrador hello, haga clic en **examinar** y en la lista de Hola de recursos, escriba **servicios de recuperación**. Cuando empiece a escribir, se filtrará la lista de hello en función de los datos especificados. Haga clic en **Almacén de Servicios de recuperación**.

    ![Haga clic en el botón de examinar hello y escriba los servicios de recuperación. Cuando vea Servicios de recuperación de hello del almacén de opción, haga clic en él hello tooopen del almacén de servicios de recuperación de hoja.](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

    se muestra la lista de Hola de almacenes de servicios de recuperación.
3. En hello **servicios de recuperación de los almacenes de credenciales** menú, haga clic en **agregar**.

    ![Creación del almacén de Servicios de recuperación, paso 2](./media/backup-azure-arm-vms-prepare/rs-vault-menu.png)

    Servicios de recuperación de Hello del almacén se abre de hoja, que le pide que tooprovide una **nombre**, **suscripción**, **grupo de recursos**, y **ubicación**.

    ![Creación del almacén de Servicios de recuperación, paso 5](./media/backup-azure-arm-vms-prepare/rs-vault-attributes.png)
4. Para **nombre**, escriba en el almacén de hello tooidentify un nombre descriptivo. nombre de Hello debe toobe único para hello suscripción de Azure. Escriba un nombre que tenga entre 2 y 50 caracteres. Debe comenzar por una letra y solo puede contener letras, números y guiones.
5. Haga clic en **suscripción** lista disponible de hello toosee de suscripciones. Si no está seguro de qué toouse de suscripción, utilice Hola predeterminado (o sugiere) suscripción. Solo habrá varias opciones si la cuenta de su organización está asociada a varias suscripciones de Azure.
6. Haga clic en **grupo de recursos** toosee Hola lista de grupos de recursos disponibles, o haga clic en **New** toocreate un nuevo grupo de recursos. Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
7. Haga clic en **ubicación** región geográfica de tooselect hello para el almacén de Hola. almacén de Hello **debe** en hello misma región que hello las máquinas virtuales que desea tooprotect.

   > [!IMPORTANT]
   > Si no está seguro de la ubicación de hello en el que existe la máquina virtual, cerrar el cuadro de diálogo de creación de almacén de Hola y vaya toohello lista de máquinas virtuales en el portal de Hola. Si tiene máquinas virtuales en varias regiones, deberá toocreate un almacén de servicios de recuperación de cada región. Crear almacén de hello en la primera ubicación de Hola antes de pasar la ubicación siguiente toohello. No hay ninguna cuenta de almacenamiento necesario toospecify datos de copia de seguridad de Hola toostore: almacén de servicios de recuperación de Hola y Hola servicio copia de seguridad de Azure se ocupan de ello automáticamente.
   >
   >

8. Haga clic en **Crear**. Puede tardar unos instantes para hello toobe creado del almacén de servicios de recuperación. Supervisar las notificaciones de estado de hello en el área superior de derecho hello en el portal de Hola. Una vez creado el almacén, aparece en la lista de Hola de almacenes de servicios de recuperación. Si no ve el almacén, haga clic en **Actualizar**.

    ![Lista de copias de seguridad](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    Ahora que ha creado el almacén, obtenga información acerca de cómo tooset Hola replicación de almacenamiento.

## <a name="set-storage-replication"></a>Configuración de la replicación de almacenamiento
opción de replicación de almacenamiento de Hello permite toochoose entre el almacenamiento con redundancia geográfica y almacenamiento con redundancia local. De forma predeterminada, el almacén tiene almacenamiento con redundancia geográfica. Deje Hola opción set toogeo redundantes almacenamiento si se trata de la copia de seguridad principal. Elija el almacenamiento con redundancia local si desea una opción más económica que no sea tan duradera.

configuración de replicación de almacenamiento de Hola tooedit:

1. En hello **servicios de recuperación de los almacenes de credenciales** hoja, seleccione el almacén.
    Al hacer clic en el almacén, Hola hoja de configuración (*que tiene el nombre de Hola de almacén de hello en la parte superior de hello*) y el almacén de hello detalles se abre la hoja.

    ![Elija el almacén de lista de Hola de almacenes de copia de seguridad](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. En hello **configuración** hoja, use Hola control deslizante vertical tooscroll hacia abajo toohello **administrar** sección. Haga clic en **infraestructura de copia de seguridad** tooopen su hoja. Hola **General** sección, haga clic **configuración de copia de seguridad** tooopen su hoja. En hello **configuración de copia de seguridad** hoja, elija la opción de replicación de almacenamiento de hello para el almacén. De forma predeterminada, el almacén tiene almacenamiento con redundancia geográfica. Si cambia el tipo de replicación de almacenamiento de hello, haga clic en **guardar**.

    ![Lista de copias de seguridad](./media/backup-azure-arm-vms-prepare/full-blade.png)

     Si usa Azure como punto de conexión del almacenamiento de copia de seguridad principal, siga utilizando el almacenamiento con redundancia geográfica. Si se usa Azure como punto de conexión de almacenamiento de copia de seguridad no principal, elija entonces el almacenamiento con redundancia local. Obtenga más información sobre [con redundancia geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) y [localmente redundante](../storage/common/storage-redundancy.md#locally-redundant-storage) opciones de almacenamiento en hello [información general sobre la replicación de almacenamiento de Azure](../storage/common/storage-redundancy.md).
    Después de elegir la opción de almacenamiento de hello para el almacén, está listo tooassociate Hola VM con el almacén de Hola. asociación de hello toobegin, debería detectar y registrar Hola máquinas virtuales de Azure.

## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>Seleccione un objetivo de copia de seguridad, establecer una directiva y definir elementos tooprotect
Antes de registrar una máquina virtual con un almacén, ejecute tooensure de proceso de detección de Hola que se identifican las máquinas virtuales nuevas que se han agregado toohello suscripción. Hola procesar consultas Azure para la lista de Hola de máquinas virtuales de suscripción de hello, junto con información adicional como el nombre del servicio de nube de Hola y región Hola. Hola portal de Azure, escenario hace referencia toowhat va tooput en el almacén de servicios de recuperación de Hola. Directiva es la programación de hello para la frecuencia y cuándo se realizan puntos de recuperación. La directiva también incluye la duración de retención de Hola Hola puntos de recuperación.

1. Si ya tiene un almacén de servicios de recuperación abierto, continúe toostep 2. Si no tiene un almacén de servicios de recuperación abierto, ábralo hello [portal de Azure](https://portal.azure.com/) y haga clic en el menú del concentrador hello, **más servicios**.

   * En la lista de Hola de recursos, escriba **servicios de recuperación**.
   * Cuando empiece a escribir, se filtrará la lista de hello en función de los datos especificados. Haga clic en **Almacenes de Recovery Services**cuando lo vea.

     ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-azure-arm-vms-prepare/browse-to-rs-vaults-updated.png) <br/>

     aparece en la lista de Hola de almacenes de servicios de recuperación. Si no hay almacenes en su suscripción, esta lista estará vacía.

    ![Lista de almacenes de credenciales de la vista de hello servicios de recuperación](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

   * En lista de Hola de almacenes de servicios de recuperación, seleccione un almacén tooopen su panel.

     hoja de configuración de Hola y Hola del almacén de panel para el almacén de hello elegido, se abre.

     ![Hoja del almacén abierta](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)
2. En el menú del panel de hello almacén, haga clic en **copia de seguridad** hoja de copia de seguridad de tooopen Hola.

    ![Hoja Backup abierta](./media/backup-azure-arm-vms-prepare/backup-button.png)

    Abra las hojas de copia de seguridad y el objetivo de copia de seguridad de Hola.

    ![Hoja Escenario abierta](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)

3. En la hoja de objetivo de copia de seguridad de hello, establezca **donde se está ejecutando la carga de trabajo** tooAzure y **especifique qué desea toobackup** tooVirtual automático, a continuación, haga clic en **Aceptar**.

    Esto registra Hola extensión de máquina virtual con el almacén de Hola. Objetivo de copia de seguridad se cierra la hoja de Hola y Hola **directiva de copia de seguridad** abre la hoja.

    ![Hoja Escenario abierta](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)
4. En la hoja de la directiva de copia de seguridad de hello, seleccione la directiva de copia de seguridad de Hola que desee tooapply toohello almacén.

    ![Seleccionar directiva de copia de seguridad](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    detalles de saludo de la directiva predeterminada de hello aparecen en el menú desplegable de Hola. Si desea toocreate una nueva directiva, seleccione **crear nuevo** desde el menú desplegable de Hola. Si quiere instrucciones para definir una directiva de copia de seguridad, consulte [Definición de una directiva de copia de seguridad](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).
    Haga clic en **Aceptar** directiva de copia de seguridad de hello tooassociate con el almacén de Hola.

    Hola hello y se cierra de hoja de directiva de copia de seguridad **seleccionar las máquinas virtuales** abre la hoja.
5. Hola **seleccionar las máquinas virtuales** hoja, elija hello tooassociate de máquinas virtuales con hello especifica la directiva y haga clic en **Aceptar**.

    ![Seleccionar carga de trabajo](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    máquina virtual de Hello seleccionado se valida. Si no ve hello las máquinas virtuales que espera toosee, compruebe que se encuentran en la misma ubicación de Azure que Hola servicios de recuperación de almacén y que ya no están protegido en otro almacén de Hola. se muestra la ubicación de Hola de hello que del almacén de servicios de recuperación en el panel del almacén de Hola.

6. Ahora que ha definido toda la configuración de almacén de hello, Hola hoja de copia de seguridad haga clic en **habilitar la copia de seguridad**. Esto implementa almacén de toohello de directiva de Hola y Hola las máquinas virtuales. No se crea punto de recuperación inicial de hello para la máquina virtual de Hola.

    ![Habilitar copia de seguridad](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

Después de habilitar correctamente la copia de seguridad de hello, la directiva de copia de seguridad se ejecutará en la programación. Si ahora desea toogenerate una tooback de trabajo de copia de seguridad a petición las máquinas virtuales de hello, consulte [trabajo de copia de seguridad de hello Triggering](./backup-azure-arm-vms.md#triggering-the-backup-job).

Si tiene problemas al registrar la máquina virtual de hello, vea Hola después de obtener información acerca de cómo instalar el agente de máquina virtual de Hola y de conectividad de red. Probablemente no necesitará Hola siguiente información si va a proteger las máquinas virtuales creadas en Azure. Sin embargo si ha migrado las máquinas virtuales en Azure, a continuación, asegúrese de que ha instalado correctamente agente de VM de Hola y de que la máquina virtual puede comunicarse con la red virtual de Hola.

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Instalar agente de máquina virtual de hello en la máquina virtual de Hola
Hello Azure VM Agent debe instalarse en la máquina virtual de Azure para toowork de extensión de copia de seguridad de Hola Hola. Si la máquina virtual se creó desde Hola Galería de Azure, Hola agente de máquina virtual ya está presente en la máquina virtual de Hola. Esta información se proporciona para situaciones de Hola que te encuentres *no* con una máquina virtual creado a partir de hello Galería de Azure: por ejemplo migrar una máquina virtual desde un centro de datos local. En tal caso, Hola agente de máquina virtual debe toobe instalado en la máquina virtual de orden tooprotect Hola. Obtenga información acerca de hello [agente de máquina virtual](../virtual-machines/windows/classic/agents-and-extensions.md#azure-vm-agents-for-windows-and-linux).

Si tiene problemas para realizar copias de seguridad Hola VM de Azure, compruebe que hello Azure VM Agent está instalado correctamente en la máquina virtual de hello (vea la siguiente tabla de Hola). Hello en la tabla siguiente proporciona información adicional sobre Hola VM agente para Windows y las máquinas virtuales de Linux.

| **operación** | **Windows** | **Linux** |
| --- | --- | --- |
| Hola instalar agente de máquina virtual |Descargue e instale hello [MSI agente](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). Necesitará la instalación de Hola de toocomplete de privilegios de administrador. |<li> Instalar más reciente hello [agente Linux](../virtual-machines/linux/agent-user-guide.md). Necesitará la instalación de Hola de toocomplete de privilegios de administrador. Se recomienda instalar el agente desde el repositorio de distribución. **No se recomienda** instalar el agente de máquina virtual Linux directamente desde github.  |
| Actualizar Hola agente de máquina virtual |Hola actualización de agente de máquina virtual es tan sencillo como Hola reinstalación [archivos binarios del agente de VM](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br>Asegúrese de que no se está ejecutando ninguna operación de copia de seguridad mientras se está actualizando el agente de máquina virtual de Hola. |Siga las instrucciones de hello en [actualizar Hola agente de máquina virtual Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Se recomienda actualizar el agente desde el repositorio de distribución. **No se recomienda** actualizar el agente de máquina virtual Linux directamente desde github.<br>Asegúrese de que no se está ejecutando ninguna operación de copia de seguridad al Hola que agente de máquina virtual se está actualizando. |
| Validar la instalación del agente de VM Hola |<li>Navegue toohello *C:\WindowsAzure\Packages* carpeta Hola VM de Azure. <li>Debería encontrar Hola WaAppAgent.exe archivo.<li> Haga clic en archivo hello, vaya demasiado**propiedades**y, a continuación, seleccione hello **detalles** campo de versión del producto de Hola de ficha debe ser 2.6.1198.718 o superior. |N/D |

### <a name="backup-extension"></a>Extensión de copia de seguridad
Una vez Hola que VM Agent esté instalado en la máquina virtual de hello, Hola servicio copia de seguridad de Azure instala Hola extensión de reserva toohello agente de máquina virtual. Hola servicio copia de seguridad de Azure sin problemas actualiza y revisiones de la extensión de copia de seguridad de Hola.

extensión de copia de seguridad de Hello está instalada por el servicio de copia de seguridad de Hola Hola VM está ejecutando o no. Una máquina virtual en ejecución proporciona mayor oportunidad de Hola de obtención de un punto de recuperación coherentes con la aplicación. Sin embargo, Hola servicio de copia de seguridad de Azure continúa tooback seguridad Hola VM incluso si se ha desactivado y no se pudo instalar la extensión de Hola. Esto se conoce como máquina virtual sin conexión. En este caso, será punto de recuperación de hello *coherente de bloqueo*.

## <a name="network-connectivity"></a>Conectividad de red
En las instantáneas de máquina virtual de orden toomanage hello, extensión de copia de seguridad de hello necesita conectividad toohello Azure direcciones IP públicas. Sin conectividad a Internet derecho hello, HTTP solicitudes hello y tiempo de espera de copia de seguridad operación Hola la máquina virtual produce un error. Si la implementación tiene restricciones de acceso establecidas (a través de un grupo de seguridad de red (NSG), por ejemplo), elija entonces una de estas opciones para proporcionar una ruta de acceso clara para el tráfico de copia de seguridad:

* [Intervalos IP de Azure del centro de datos de lista blanca Hola](http://www.microsoft.com/en-us/download/details.aspx?id=41653) : consulte el artículo de Hola para obtener instrucciones sobre cómo toowhitelist Hola direcciones IP.
* Implementación de un servidor proxy HTTP para enrutar el tráfico.

Al decidir qué opción toouse, Hola ventajas e inconvenientes son entre la capacidad de administración, un control granular y el coste.

| Opción | Ventajas | Desventajas |
| --- | --- | --- |
| Creación de una lista blanca con intervalos IP |Sin costos adicionales.<br><br>Para abrir el acceso en un NSG, usar hello <i>AzureNetworkSecurityRule conjunto</i> cmdlet. |Toomanage complejo como el cambio de intervalos IP de hello afectado con el tiempo.<br><br>Proporciona el conjunto de toohello de acceso de Azure y no solo en el almacenamiento de información. |
| Proxy HTTP |Control granular de proxy de hello sobre el almacenamiento de Hola que permite las direcciones URL.<br>TooVMs de acceso de punto único de Internet.<br>No tooAzure cambios en la dirección IP del firmante. |Costes adicionales para ejecutar una máquina virtual con el software de proxy de Hola. |

### <a name="whitelist-hello-azure-datacenter-ip-ranges"></a>Intervalos de IP de centro de datos Azure Hola de lista blanca de direcciones
intervalos de IP de toowhitelist hello Azure del centro de datos, vea hello [sitio Web de Azure](http://www.microsoft.com/en-us/download/details.aspx?id=41653) para obtener más información sobre los intervalos IP de hello e instrucciones.

### <a name="using-an-http-proxy-for-vm-backups"></a>Uso de un proxy HTTP para las copias de seguridad de máquinas virtuales
Cuando copia de seguridad de una máquina virtual, extensión de copia de seguridad de hello en hello VM envía Hola instantánea administración comandos tooAzure almacenamiento mediante una API de HTTPS. Redirigir el tráfico de extensión de reserva de Hola a través de proxy de hello HTTP ya que es el único componente de hello configurado para acceso toohello Internet pública.

> [!NOTE]
> No hay ninguna recomendación para el software de proxy de Hola que debe usarse. Asegúrese de que se elige a un proxy que sea compatible con los siguientes pasos de configuración de Hola.
>
>

imagen de ejemplo de Hola siguiente muestra pasos de configuración tres Hola necesarios toouse HTTP proxy:

* Las rutas de aplicación virtual para que todo el tráfico HTTP enlazado Hola red pública de Internet a través de la máquina virtual de Proxy.
* Proxy de máquina virtual permite el tráfico entrante desde máquinas virtuales en la red virtual de Hola.
* Grupo de seguridad de red (NSG) con el nombre de bloqueo sin fondos de Hello necesita un seguridad regla permitir Internet el tráfico saliente de máquina virtual de Proxy.

![Grupo de seguridad de red con el diagrama de implementación de proxy HTTP](./media/backup-azure-vms-prepare/nsg-with-http-proxy.png)

toouse HTTP proxy toocommunicating toohello red pública de Internet, siga estos pasos:

#### <a name="step-1-configure-outgoing-network-connections"></a>Paso 1. Configuración de las conexiones de red salientes
###### <a name="for-windows-machines"></a>Para máquinas Windows
En este paso se configura el servidor proxy para la cuenta de sistema local.

1. Descargue [PsExec](https://technet.microsoft.com/sysinternals/bb897553)
2. Ejecute el comando siguiente desde un símbolo del sistema con privilegios elevados.

     ```
     psexec -i -s "c:\Program Files\Internet Explorer\iexplore.exe"
     ```
     Se abrirá la ventana de Internet Explorer.
3. Vaya a tooTools -> Opciones de Internet -> conexiones -> configuración de LAN.
4. Compruebe la configuración de proxy de la cuenta del sistema. Configure la dirección IP de proxy y el puerto.
5. Cierre Internet Explorer.

Se configurará el proxy en todo el equipo y se usará para el tráfico saliente de HTTP/HTTPS.

Si tiene el programa de instalación de un servidor proxy en una cuenta de usuario actual (no una cuenta de sistema Local), use Hola siguientes script tooapply les tooSYSTEMACCOUNT:

```
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name DefaultConnectionSettings -Value $obj.DefaultConnectionSettings
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections" -Name SavedLegacySettings -Value $obj.SavedLegacySettings
   $obj = Get-ItemProperty -Path Registry::”HKEY_CURRENT_USER\Software\Microsoft\Windows\CurrentVersion\Internet Settings"
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name ProxyEnable -Value $obj.ProxyEnable
   Set-ItemProperty -Path Registry::”HKEY_USERS\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings" -Name Proxyserver -Value $obj.Proxyserver
```

> [!NOTE]
> Si ve el mensaje "(407) Se requiere autenticación del proxy" en el registro del servidor proxy, compruebe que su autenticación está configurada correctamente.
>
>

###### <a name="for-linux-machines"></a>Para máquinas Linux
Agregar Hola después línea toohello ```/etc/environment``` archivo:

```
http_proxy=http://<proxy IP>:<proxy port>
```

Agregar Hola después líneas toohello ```/etc/waagent.conf``` archivo:

```
HttpProxy.Host=<proxy IP>
HttpProxy.Port=<proxy port>
```

#### <a name="step-2-allow-incoming-connections-on-hello-proxy-server"></a>Paso 2: Permitir las conexiones entrantes en el servidor de proxy de hello:
1. En el servidor de proxy de hello, abra Firewall de Windows. firewall de Hola de manera más fácil de Hello tooaccess es toosearch Firewall de Windows con seguridad avanzada.

    ![Abra Hola Firewall](./media/backup-azure-vms-prepare/firewall-01.png)
2. En el cuadro de diálogo de Firewall de Windows hello, haga clic en **reglas de entrada** y haga clic en **nueva regla...** .

    ![Crear una nueva regla](./media/backup-azure-vms-prepare/firewall-02.png)
3. Hola **entrada Asistente para nueva regla**, elija hello **personalizado** opción para hello **tipo de regla** y haga clic en **siguiente**.
4. En Hola de hello página tooselect **programa**, elija **todos los programas** y haga clic en **siguiente**.
5. En hello **protocolo y puertos** página, escriba Hola siguiente información y haga clic en **siguiente**:

    ![Crear una nueva regla](./media/backup-azure-vms-prepare/firewall-03.png)

   * en *Tipo de protocolo*, elija *TCP*.
   * para *puerto Local* elegir *puertos específicos*, en el siguiente campo de hello especificar hello ```<Proxy Port>``` que se ha configurado.
   * En *Puerto remoto*, seleccione *Todos los puertos*.

     Para el resto de Hola de Asistente de hello, haga clic en todos los extremos de toohello de manera hello y asigne un nombre a esta regla.

#### <a name="step-3-add-an-exception-rule-toohello-nsg"></a>Paso 3: Agregue un toohello de regla de excepción NSG:
En un símbolo del sistema de PowerShell de Azure, escriba Hola siguiente comando:

Hola siguiente comando agrega un NSG de toohello de excepción. Esta excepción permite el tráfico TCP desde cualquier puerto 10.0.0.5 tooany dirección de Internet en el puerto 80 (HTTP) o 443 (HTTPS). Si necesita un puerto específico en Hola red pública de Internet, pueden tooadd seguro de que el puerto toohello ```-DestinationPortRange``` así.

```
Get-AzureNetworkSecurityGroup -Name "NSG-lockdown" |
Set-AzureNetworkSecurityRule -Name "allow-proxy " -Action Allow -Protocol TCP -Type Outbound -Priority 200 -SourceAddressPrefix "10.0.0.5/32" -SourcePortRange "*" -DestinationAddressPrefix Internet -DestinationPortRange "80-443"
```


*En estos pasos se utilizan valores y nombres específicos para este ejemplo. Use nombres de Hola y valores para su implementación cuando escriba, o cortar y pegar detalles en el código.*

Ahora que sabe que tiene conectividad de red, está listo tooback seguridad de la máquina virtual. Consulte [Copia de seguridad de máquinas virtuales de Azure en un almacén de Servicios de recuperación](backup-azure-arm-vms.md).

## <a name="questions"></a>¿Tiene preguntas?
Si tiene alguna pregunta, o si hay cualquier característica que le gustaría toosee incluido, [nos envíe sus comentarios](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Pasos siguientes
Ahora que ha preparado el entorno para realizar copias de seguridad de la máquina virtual, el siguiente paso lógico es toocreate una copia de seguridad. Hola planeación artículo proporciona información más detallada acerca de la copia de seguridad de las máquinas virtuales.

* [Copia de seguridad de máquinas virtuales](backup-azure-vms.md)
* [Planeación de la infraestructura de copia de seguridad de máquinas virtuales](backup-azure-vms-introduction.md)
* [Administración de copias de seguridad de máquinas virtuales](backup-azure-manage-vms.md)
