---
title: "aaaReplicate máquinas virtuales de Hyper-V en VMM con SAN mediante el uso de Azure Site Recovery | Documentos de Microsoft"
description: "Este artículo se describe cómo tooreplicate Hyper-V de máquinas virtuales entre dos sitios con Azure Site Recovery con replicación de SAN."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: eb480459-04d0-4c57-96c6-9b0829e96d65
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: cee4ff519a8e9e7f29e17e923a9533fb339634b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-vms-in-vmm-clouds-tooa-secondary-site-with-azure-site-recovery-by-using-san"></a>Replicar máquinas virtuales de Hyper-V en el sitio secundario tooa VMM nubes con Azure Site Recovery mediante SAN


Utilice este artículo si desea toodeploy [Azure Site Recovery](site-recovery-overview.md) toomanage replicación de máquinas virtuales de Hyper-V (que se administran en nubes de System Center Virtual Machine Manager) tooa VMM sitio secundario, con Azure Site Recovery en el portal clásico de Hola. Este escenario no está disponible en el nuevo portal de Azure Hola.



Registrar los comentarios al final de Hola de este artículo. Obtenga respuestas tootechnical preguntas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="why-replicate-with-san-and-site-recovery"></a>¿Por qué replicar con SAN y Site Recovery?

* SAN proporciona una solución de replicación de nivel empresarial y escalable para que un sitio primario que contengan Hyper-V con SAN puede replicar LUN tooa sitio secundario con SAN. VMM administra el almacenamiento, y se organizan la replicación y la conmutación por error con Site Recovery.
* Recuperación de sitio ha trabajado con varios [socios de almacenamiento de SAN](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx) tooprovide la replicación en almacenamiento de canal de fibra e iSCSI.  
* Utilice las aplicaciones existentes de SAN infraestructura tooprotect críticas implementadas en clústeres de Hyper-V. Las máquinas virtuales se pueden replicar como grupo para que se pueda llevar a cabo la conmutación por error coherente de las aplicaciones de n niveles.
* La replicación de SAN garantiza la coherencia de la replicación entre distintos niveles de una aplicación, con replicación sincronizada para un bajo RTO y RPO, y la replicación no sincronizada para una gran flexibilidad (según las funcionalidades de la matriz de almacenamiento).  
* Puede administrar el almacenamiento de SAN en hello tejido de VMM y usar SMI-S en un almacenamiento VMM toodiscover existente.  

Observe lo siguiente:
- Replicación de sitio a sitio con SAN no está disponible en hello portal de Azure. Solo está disponible en el portal clásico de Hola. No se puede crear almacenes nuevos en el portal clásico de Hola. Se pueden mantener los existentes.
- No se admite la replicación de SAN tooAzure.
- No se puede replicar Vhdx compartidos o unidades lógicas (LUN) que están directamente conectan tooVMs a través de iSCSI o canal de fibra. Se pueden replicar clústeres invitados.


## <a name="architecture"></a>Arquitectura

![Arquitectura SAN](./media/site-recovery-vmm-san/architecture.png)

- **Azure**: configurar un almacén de Site Recovery en hello portal de Azure.
- **Almacenamiento SAN**: almacenamiento de SAN se administra en hello tejido de VMM. Agregar proveedor de almacenamiento de hello, cree clasificaciones de almacenamiento y configurar grupos de almacenamiento.
- **VMM e Hyper-V**: se recomienda un servidor VMM en cada sitio. Configure nubes privadas VMM y coloque los clústeres de Hyper-V en ellas. Durante la implementación, Hola proveedor de Azure Site Recovery está instalado en cada servidor VMM y Hola servidor está registrado en el almacén de Hola. Hola proveedor se comunica con la replicación de toomanage de servicio de recuperación de sitio de hello, conmutación por error y conmutación por recuperación.
- **Replicación**: después de configurar el almacenamiento en VMM y configurar la replicación de Site Recovery, la replicación se produce entre el almacenamiento de SAN Hola principal y secundario. Se envía ningún dato de replicación tooSite recuperación.
- **Conmutación por error**: habilitar la conmutación por error en el portal de Site Recovery Hola. No hay ninguna pérdida de datos durante la conmutación por error porque la replicación es sincrónica.
- **Conmutación por recuperación**: toofail back, habilitar cambios diferenciales de tootransfer la replicación inversa desde el sitio principal de hello sitio secundario toohello. Una vez completada la replicación inversa, ejecute una conmutación por error planeada de tooprimary secundaria. Esta conmutación por error planeada deja de réplica de hello las máquinas virtuales en el sitio secundario de Hola y los inicia en el sitio principal de Hola.


## <a name="before-you-start"></a>Antes de comenzar


**Requisitos previos** | **Detalles**
--- | ---
**Las tablas de Azure** |Necesita una cuenta de [Microsoft Azure](https://azure.microsoft.com/) . Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/). [Más información](https://azure.microsoft.com/pricing/details/site-recovery/) sobre los precios de Site Recovery. Crear un tooconfigure de almacén de Azure Site Recovery y administra la replicación y conmutación por error.
**VMM** | Puede usar un solo servidor VMM y replicar entre nubes diferentes, pero se recomienda un VMM en el sitio primario de hello y otro en el sitio secundario de Hola. Se puede implementar VMM como servidor físico o virtual independiente, o bien como clúster. <br/><br/>servidor VMM Hola debe disponer de System Center 2012 R2 o posterior con hello últimas actualizaciones acumulativas.<br/><br/> Necesita al menos una nube configurada en servidor VMM principal Hola desea tooprotect y una nube configurada en el servidor VMM secundario de Hola que desee toouse para conmutación por error.<br/><br/> nube de origen Hola debe contener uno o varios grupos de host VMM.<br/><br/> Todas las nubes VMM deben tener el perfil de capacidad de Hyper-V de hello establecida.<br/><br/> Para más información acerca de la configuración de nubes VMM, consulte [Implementación de una nube privada de VMM](https://technet.microsoft.com/en-us/system-center-docs/vmm/scenario/cloud-overview).
**Hyper-V** | Necesita uno o varios clústeres de Hyper-V en las nubes VMM principal y secundaria.<br/><br/> clúster de Hyper-V de origen Hola debe contener una o más máquinas virtuales.<br/><br/> grupos de host VMM Hello en sitios primarios y secundarios de hello deben contener al menos uno de los clústeres de Hyper-V de Hola.<br/><br/>los servidores de Hyper-V de host y de destino de Hello deben estar ejecutando Windows Server 2012 o posterior con actualizaciones más recientes de hello y rol de hello Hyper-V instalado.<br/><br/> Si está ejecutando Hyper-V en un clúster, tenga en cuenta que ese agente de clúster no se creará automáticamente si tiene un clúster basado en una dirección IP estática. Debe configurarlo manualmente. Para más información, consulte [Preparing host clusters for Hyper-V replica](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters) (Preparación de clústeres de host para la réplica de Hyper-V).
**Almacenamiento SAN** | Puede replicar máquinas virtuales agrupadas en clústeres invitados con almacenamiento de canal o iSCSI, o mediante discos duros virtuales (VHDX) compartidos.<br/><br/> Necesita dos matrices de SAN: uno en el sitio primario de hello y el sitio secundario de hello en uno.<br/><br/> Una infraestructura de red debe configurarse entre matrices de Hola. Es necesario configurar la replicación y el emparejamiento. Licencias de replicación deben configurarse según los requisitos de matriz de almacenamiento de Hola.<br/><br/>Configurar la red entre los servidores de host de Hyper-V de Hola y matriz de almacenamiento de Hola para que los hosts puedan comunicarse con LUN de almacenamiento mediante iSCSI o canal de fibra.<br/><br/> Consulte las [matrices de almacenamiento compatibles](http://social.technet.microsoft.com/wiki/contents/articles/28317.deploying-azure-site-recovery-with-vmm-and-san-supported-storage-arrays.aspx).<br/><br/> Se deben instalar los proveedores de SMI-S de fabricantes de matriz de almacenamiento y matrices de SAN de hello deben ser administradas por el proveedor de Hola. Configurar instrucciones de toomanufacturer de hello proveedor correspondiente.<br/><br/>Asegúrese de que el proveedor de SMI-S de la matriz de hello está en un servidor que VMM Hola server puede tener acceso a través de red de hello con una dirección IP o FQDN.<br/><br/> Cada matriz de SAN debe tener uno o varios bloques de almacenamiento disponibles.<br/><br/> servidor VMM principal de Hello debe administrar la matriz principal de Hola y servidor VMM secundario Hola debe administrar la matriz secundaria Hola.
**Asignación de red** | Configurar la asignación de red para que las máquinas virtuales replicadas se colocan de forma óptima en los servidores secundarios de host de Hyper-V después de la conmutación por error, de modo que sean más redes de VM tooappropriate conectado. Si no configura la asignación de red, las máquinas virtuales de réplica no será tooany conectado red después de la conmutación por error.<br/><br/> Asegúrese de que las redes de VMM estén configuradas correctamente, para que pueda configurar la asignación de red durante la implementación de Site Recovery. En VMM, hello las máquinas virtuales en el host de Hyper-V de origen Hola debe ser conectado tooa red de VM de VMM. Esta red debe ser tooa vinculado red lógica que está asociado a la nube de Hola.<br/><br/> nube de destino de Hello debe tener una red VM correspondiente y, a su vez debe ser tooa vinculado correspondiente red lógica que está asociado a la nube de destino de Hola.<br/><br/>.

## <a name="step-1-prepare-hello-vmm-infrastructure"></a>Paso 1: Preparar la infraestructura de VMM Hola
tooprepare su infraestructura de VMM, debe:

1. Comprobar las nubes VMM.
2. Integrar y clasificar el almacenamiento SAN en VMM.
3. Crear LUN y asignar almacenamiento.
4. Crear grupos de replicación.
5. Configurar redes de máquinas virtuales.

### <a name="verify-vmm-clouds"></a>Comprobar las nubes VMM

Asegúrese de que las nubes VMM estén configuradas correctamente antes de empezar la implementación de Site Recovery.

### <a name="integrate-and-classify-san-storage-in-hello-vmm-fabric"></a>Integre y clasifique el almacenamiento SAN en hello tejido de VMM

1. En la consola VMM de hello, vaya demasiado**tejido** > **almacenamiento** > **agregar recursos** > **dedispositivosdealmacenamiento**.
2. Hola **agregar dispositivos de almacenamiento** asistente, seleccione **seleccione un tipo de proveedor de almacenamiento** y seleccione **dispositivos SAN y NAS detectados y administrados por un proveedor de SMI-S**.

    ![Tipo de proveedor](./media/site-recovery-vmm-san/provider-type.png)

3. En hello **especifique el protocolo y la dirección del proveedor de SMI-S de almacenamiento de hello** página, seleccione **CIMXML SMI-S** y especifique la configuración de hello para el proveedor de conexión toohello.
4. En **dirección IP del proveedor o FQDN** y **puerto TCP/IP**, especifique la configuración de Hola de proveedor de conexión toohello. Solo puede utilizar una conexión SSL para SMI-S CIMXML.

    ![Conexión de proveedor](./media/site-recovery-vmm-san/connect-settings.png)
5. En **cuenta de identificación**, especifique una cuenta de identificación de VMM que puede tener acceso a proveedor de Hola o crear una cuenta.
6. En hello **recopilar información** página, VMM intenta automáticamente con toodiscover e importar información de dispositivo de almacenamiento de Hola. detección de tooretry, haga clic en **proveedor de examen**. Si se realiza correctamente el proceso de detección de hello, Hola detecta matrices de almacenamiento, grupos de almacenamiento, fabricante, modelo y capacidad se muestran en la página de Hola.

    ![Detección de almacenamiento](./media/site-recovery-vmm-san/discover.png)
7. En **seleccione tooplace de grupos de almacenamiento bajo la administración y asignar una clasificación**, seleccione los grupos de almacenamiento de Hola que VMM administrará y asígneles una clasificación. Se importa información de LUN de grupos de almacenamiento de Hola. Crear LUN basándose en las aplicaciones de hello necesita tooprotect, sus requisitos de capacidad y los requisitos para lo que debe tooreplicate juntos.

    ![Clasificación de almacenamiento](./media/site-recovery-vmm-san/classify.png)

### <a name="create-luns-and-allocate-storage"></a>Crear LUN y asignar almacenamiento

Crear LUN basándose en las aplicaciones de Hola necesita tooprotect, requisitos de capacidad y los requisitos para lo que debe tooreplicate juntos.

1. Después de que aparezca en el almacenamiento de Hola Hola tejido de VMM, puede [aprovisionar LUN](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-storage-host-groups#create-a-lun-in-vmm).

     > [!NOTE]
     > No agregue discos duros virtuales para máquinas virtuales que están habilitadas para replicación tooLUNs Hola. Si los LUN no están en un grupo de replicación de Site Recovery, puede que este no los detecte.
     >

2. Asigne el clúster de hosts de Hyper-V de toohello de capacidad de almacenamiento para que VMM pueda implementar toohello aprovisionar almacenamiento de datos de máquina virtual:

   * Antes de asignar el clúster de almacenamiento toohello, necesita tooallocate, grupo de host VMM toohello en qué Hola que reside el clúster. Para obtener más información, consulte [cómo tooa de unidades lógicas de almacenamiento de tooallocate alojar grupo en VMM](https://technet.microsoft.com/library/gg610686.aspx) y [cómo tooa grupo de host en VMM los grupos de almacenamiento de tooallocate](https://technet.microsoft.com/library/gg610635.aspx).
   * Asignar el clúster de toohello de capacidad de almacenamiento como se describe en [cómo agrupar tooconfigure almacenamiento en un host de Hyper-V en VMM](https://technet.microsoft.com/library/gg610692.aspx).

    ![Tipo de proveedor](./media/site-recovery-vmm-san/provider-type.png)
3. En **especifique el protocolo y la dirección del proveedor de SMI-S de almacenamiento de hello**, seleccione **CIMXML SMI-S**. Especificar la configuración de Hola para conectar el proveedor de toohello. Solo puede utilizar una conexión SSL para SMI-S CIMXML.

    ![Conexión de proveedor](./media/site-recovery-vmm-san/connect-settings.png)
4. En **cuenta de identificación**, especifique una cuenta de identificación de VMM que puede tener acceso a proveedor de Hola o crear una cuenta.
5. En **recopilar información**, VMM intenta automáticamente la información de dispositivo de almacenamiento de hello toodiscover e importación. Si necesita tooretry, haga clic en **proveedor de examen**. Cuando el proceso de detección de Hola se realiza correctamente, matrices de almacenamiento de hello, capacidad, fabricante, modelo y grupos de almacenamiento se muestran en la página de Hola.

    ![Detección de almacenamiento](./media/site-recovery-vmm-san/discover.png)
7. En **seleccione tooplace de grupos de almacenamiento bajo la administración y asignar una clasificación**, seleccione los grupos de almacenamiento de Hola que VMM se administrar y asígneles una clasificación. Se importa información de LUN de grupos de almacenamiento de Hola.

    ![Clasificación de almacenamiento](./media/site-recovery-vmm-san/classify.png)


### <a name="create-replication-groups"></a>Crear grupos de replicación

Crear un grupo de replicación que incluye todos los LUN de Hola que necesitarán tooreplicate juntos.

1. En la consola VMM de hello, abra hello **grupos de replicación** ficha de propiedades de matriz de almacenamiento de hello y, a continuación, haga clic en **nuevo**.
2. Crear grupo de replicación de Hola.

    ![Grupo de replicación de SAN](./media/site-recovery-vmm-san/rep-group.png)

### <a name="set-up-networks"></a>Configuración de redes

Si desea que la asignación de red tooconfigure, Hola siguientes:

1. Consulte Asignación de redes de Site Recovery.
2. Prepare las redes de máquinas virtuales en VMM:

   * [Configure redes lógicas](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-logical-networks).
   * [Configure redes de máquinas virtuales](https://technet.microsoft.com/en-us/system-center-docs/vmm/manage/manage-network-vm-networks).


## <a name="step-2-create-a-vault"></a>Paso 2: Creación de un almacén

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com) desde el servidor VMM Hola desea tooregister en el almacén de Hola.
2. Expanda **Data Services** > **Recovery Services** y haga clic en **Almacén de Site Recovery**.
3. Haga clic en **Crear nuevo	** > **Creación rápida**.
4. En **nombre**, escriba en el almacén de hello tooidentify un nombre descriptivo.
5. En **región**, seleccione Hola región geográfica para el almacén de Hola. regiones de toocheck compatibles, consulte [detalles de precios de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Haga clic en **Crear almacén**.

    ![Almacén nuevo](./media/site-recovery-vmm-san/create-vault.png)

Compruebe tooconfirm de barra de estado de Hola que Hola almacén se creó correctamente. almacén de Hola se mostrarán como **Active** en hello principal **servicios de recuperación** página.

### <a name="register-hello-vmm-servers"></a>Registrar servidores VMM Hola

1. Abra hello **inicio rápido** página de hello **servicios de recuperación** página. Inicio rápido también se puede abrir en cualquier momento seleccionando el icono de Hola.

    ![Icono de inicio rápido](./media/site-recovery-vmm-san/quick-start-icon.png)
2. En el cuadro de lista desplegable de hello, seleccione **entre Hyper-V sitio mediante replicación de matriz local**.

    ![Clave de registro](./media/site-recovery-vmm-san/select-san.png)
3. En **servidores VMM preparar**, descargue Hola la versión más reciente del archivo de instalación del proveedor de Azure Site Recovery de Hola.
4. Ejecute este archivo hello servidor VMM de origen. Si VMM está implementado en un clúster y está instalando hello proveedor para hello primera vez, instale Hola proveedor en un nodo activo y finalizar Hola instalación tooregister Hola servidor VMM en el almacén de Hola. Instale Hola proveedor en hello otros nodos. Si va a actualizar Hola proveedor, tendrá que tooupgrade en todos los nodos para que han Hola misma versión del proveedor.
5. el instalador de Hello comprueba los requisitos y las solicitudes permiso toostop Hola instalación del proveedor de toobegin de servicio VMM. servicio de Hola se reiniciará automáticamente cuando finaliza el programa de instalación. En un clúster VMM, podrá rol de clúster de hello toostop solicitadas.
6. En **Microsoft Update**, puede participar en actualizaciones y las actualizaciones del proveedor se instalarán según la directiva de Microsoft Update tooyour.

    ![Microsoft Updates](./media/site-recovery-vmm-san/ms-update.png)

7. De forma predeterminada, ubicación de instalación de Hola para hello proveedor es <SystemDrive>\Program System Center 2012 R2\Virtual Machine Manager\bin. Haga clic en **instalar** toobegin.

    ![Ubicación de instalación](./media/site-recovery-vmm-san/install-location.png)

8. Después de instala el proveedor de hello, haga clic en **registrar** tooregister servidor VMM hello en el almacén de Hola.

    ![Instalación completa](./media/site-recovery-vmm-san/install-complete.png)

9. En **conexión a Internet**, especifique cómo Hola proveedor conecta a Internet toohello. Seleccione **usar configuración de proxy del sistema predeterminada** si desea toouse Hola configuración predeterminada de Internet conexión en el servidor de Hola.

    ![Configuración de Internet](./media/site-recovery-vmm-san/proxy-details.png)

   * Si desea toouse un proxy personalizado, configurarla antes de instalar el proveedor de Hola. Al configurar el proxy personalizado, ejecuta una prueba conexión del proxy toocheck Hola.
   * Si usa a un proxy personalizado, o si el proxy predeterminado requiere autenticación, debe especificar los detalles del proxy hello, incluido el puerto y la dirección de Hola.
   * Hola requiere que direcciones URL deben ser accesible desde el servidor VMM Hola.
   * Si usa un proxy personalizado, una cuenta ejecutar como del VMM (DRAProxyAccount) se crea automáticamente mediante el uso de hello especificada las credenciales del proxy. Configurar el servidor de proxy de Hola para que pueda autenticar esta cuenta. Puede modificar Hola ejecutar como configuración de la cuenta en la consola VMM hello (**configuración** > **seguridad** > **cuentas de ejecución**  >  **DRAProxyAccount**). Debe reiniciar el servicio VMM Hola para cambiar tootake efecto de Hola.
10. En **clave de registro**, seleccione clave Hola que ha descargado desde un servidor VMM hello toohello portal y copiado.
11. En **nombre del almacén**, compruebe el nombre de Hola de almacén de hello en qué Hola se registrará el servidor.

    ![Registro de servidor](./media/site-recovery-vmm-san/vault-creds.png)
12. opción de cifrado de Hello solo se usa para la replicación de tooAzure VMM. Puede pasarla por alto.

    ![Registro de servidor](./media/site-recovery-vmm-san/encrypt.png)
13. En **nombre del servidor**, especifique un servidor VMM Nombre_descriptivo tooidentify hello en el almacén de Hola. En una configuración de clúster, especifique el nombre de rol de clúster VMM Hola.
14. En **sincronización inicial de metadatos en la nube**, seleccione si desea toosynchronize metadatos para todas las nubes en el servidor VMM Hola. Esta acción solo debe toohappen una vez en cada servidor. Si no desea toosynchronize todas las nubes, puede dejar esta configuración desactivada y sincronizar cada nube individualmente en las propiedades de la nube de hello en la consola VMM Hola.

    ![Registro de servidor](./media/site-recovery-vmm-san/friendly-name.png)

15. Haga clic en **siguiente** toocomplete proceso de Hola. Después del registro, Azure Site Recovery recupera metadatos desde un servidor VMM Hola. Hola servidor se muestra en **servidores** > **servidores VMM** en el almacén de Hola.

### <a name="command-line-installation"></a>Instalación mediante línea de comandos

Hola proveedor de Azure Site Recovery también puede instalarse mediante el uso de hello después de la línea de comandos. Este método puede ser proveedor de hello tooinstall usado en Server Core de Windows Server 2012 R2.

1. Hola proveedor carpeta de instalación de archivos y registro tooa clave de descarga. Por ejemplo, C:\ASR.
2. Detener servicio VMM Hola.
3. Extraiga el instalador de proveedor de Hola. Ejecute estos comandos como administrador:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Instalar Hola proveedor:

        C:\ASR> setupdr.exe /i
5. Registrar Hola proveedor:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>         

Parámetros:

* **/ Credenciales de**: parámetro necesario para la ubicación de hello en qué Hola se encuentra el archivo de clave de registro.  
* **/ FriendlyName**: parámetro necesario para el nombre de saludo del servidor de host de Hyper-V de Hola que aparece en el portal de Azure Site Recovery Hola.
* **/ EncryptionEnabled**: parámetro opcional que se usa solo cuando se replican desde VMM tooAzure.
* **/proxyAddress**: parámetro opcional que especifica la dirección de saludo del servidor de proxy de Hola.
* **/proxyPort**: parámetro opcional que especifica el puerto de saludo del servidor de proxy de Hola.
* **/ proxyusername**: parámetro opcional que especifica el nombre de usuario de proxy de hello (si el proxy de hello requiere autenticación).
* **/ proxypassword**: parámetro opcional que especifica la contraseña de Hola para autenticar con el servidor de proxy de hello (si el proxy de hello requiere autenticación).

## <a name="step-3-map-storage-arrays-and-pools"></a>Paso 3: Asignación de grupos y matrices de almacenamiento

Asignar toospecify matrices principal y secundarias qué grupo de almacenamiento secundario recibe datos de replicación de grupo principal de Hola. Asignar almacenamiento antes de configurar la replicación, porque se usa la información de asignación de hello al habilitar la protección para grupos de replicación.

Antes de empezar, compruebe que las nubes de VMM aparecen en el almacén de Hola. Las nubes se detectan cuando sincronice todas las nubes durante la instalación del proveedor o al sincronizar una nube específica en la consola VMM Hola.

1. Haga clic en **Recursos** > **Almacenamiento del servidor** > **Asignar matrices de almacenamiento de origen y destino**.
    ![Registro de servidor](./media/site-recovery-vmm-san/storage-map.png)

2. Seleccione Hola matrices de almacenamiento en el sitio principal de Hola y asignarlos toostorage matrices en el sitio secundario de Hola. En **grupos de almacenamiento**, seleccione un origen y destino toomap del grupo de almacenamiento.

    ![Registro de servidor](./media/site-recovery-vmm-san/storage-map-pool.png)

## <a name="step-4-configure-replication-settings"></a>Paso 4: Configuración de opciones de replicación

Una vez que los servidores VMM estén registrados, configure la protección de la nube.

1. En hello **inicio rápido** página, haga clic en **configurar la protección para nubes de VMM**.
2. En hello **elementos protegidos** ficha, seleccione en la nube hello **configuración**.
3. En **Destino**, seleccione **VMM**.
4. En **ubicación de destino**, seleccione servidor VMM de Hola que administra en la nube Hola desea toouse para la recuperación.
5. En **nube de destino**, seleccione Hola nube de destino que desee toouse para conmutación por error de máquina virtual.
   * Le recomendamos que seleccione una nube de destino que cumpla los requisitos de recuperación para máquinas virtuales de Hola que proteger.
   * Una nube solo puede pertenecer par de nube único tooa--como principal o una nube de destino.
6. Site Recovery comprueba que las nubes tienen acceso tooSAN almacenamiento y que se asignan a las matrices de almacenamiento de Hola.
7. Si la comprobación se realiza correctamente, en **Tipo de replicación**, seleccione **SAN**.

Después de guardar los valores de hello, se crea un trabajo que se pueden supervisar en hello **trabajos** ficha. Se puede modificar la configuración en hello **configurar** ficha. Si desea toomodify ubicación de destino de Hola o nube de destino, debe quitar la configuración de nube de hello y, a continuación, volver a configurar en la nube Hola.

## <a name="step-5-enable-network-mapping"></a>Paso 5: habilitación de la asignación de redes

1. En hello **inicio rápido** página, haga clic en **asignar redes**.
2. Seleccionar servidor VMM de origen de hello y, a continuación, seleccione Hola destino VMM toowhich saludos del servidor se asignarán las redes. se muestra la lista de Hola de redes de origen y sus redes de destino asociadas. En el caso de las redes no asignadas, aparece un valor en blanco. Haga clic en hello información icono siguiente toohello origen y destino nombres tooview Hola subredes de red para cada red.
3. Seleccione una red en **Red en origen** y haga clic en **Asignar**. Hola servicio detecta las redes de VM de hello en el servidor de destino de Hola y las muestra.

    ![Arquitectura SAN](./media/site-recovery-vmm-san/network-map1.png)
4. Seleccione uno de redes de VM de Hola Hola servidor de destino VMM.

    ![Arquitectura SAN](./media/site-recovery-vmm-san/network-map2.png)

5. Al seleccionar una red de destino, hello nubes protegidas que usan la red de origen Hola se muestran. También se muestran las redes de destino disponibles. Se recomienda que seleccione una red de destino que esté disponible tooall nubes de Hola que está usando para la replicación.
6. Haga clic en el proceso de asignación de hello marca de verificación toocomplete Hola. Se inicia un trabajo que realiza un seguimiento del progreso. Puede verlo en hello **trabajos** ficha.

## <a name="step-6-enable-replication-for-replication-groups"></a>Paso 6: Habilitación de la replicación para los grupos de replicación

Antes de poder habilitar la protección para máquinas virtuales, necesitará tooenable replicación para grupos de replicación de almacenamiento.

1. En hello **propiedades** página de la nube principal de Hola Hola portal de Site Recovery, abra hello **máquinas virtuales** ficha y haga clic en **Agregar grupo de replicación**.
2. Seleccione uno o más VMM grupos de replicación que están asociados a la nube de hello, compruebe las matrices de origen y destino de Hola y especificar la frecuencia de replicación de Hola.

Site Recovery, VMM y los proveedores de SMI-S de hello aprovisionar LUN de almacenamiento del sitio de destino de Hola y habilitar la replicación de almacenamiento. Si ya se replica el grupo de replicación de hello, Site Recovery reutiliza la relación de replicación existente de Hola y actualizaciones Hola información.

## <a name="step-7-enable-protection-for-virtual-machines"></a>Paso 7: Habilitación de la protección para las máquinas virtuales


Cuando se replica un grupo de almacenamiento, habilitar la protección de máquinas virtuales en la consola VMM Hola con uno de los siguientes métodos de hello:

* **Nueva máquina virtual**: cuando se crea una máquina virtual, habilitar la replicación y asocie Hola VM con el grupo de replicación de Hola.
  Con esta opción, VMM usa almacenamiento de máquina virtual de selección de ubicación inteligente toooptimally lugar hello en LUN Hola Hola del grupo de replicación. Site Recovery organiza la creación de hello de una máquina virtual en el sitio secundario de hello sombra y asigna la capacidad para que las máquinas virtuales de réplica se pueden iniciar después de la conmutación por error.
* **Máquina virtual existente**: si una máquina virtual ya está implementada en VMM, puede habilitar la replicación y realizar un grupo de replicación de tooa de migración de almacenamiento. Después de detectar la finalización, VMM y Site Recovery Hola nueva máquina virtual y empezar a administrar en Site Recovery. Máquina virtual se crea una sombra en el sitio secundario de Hola y capacidad se asigna para que esa réplica Hola VM se puede iniciar después de la conmutación por error.

![Habilitar protección](./media/site-recovery-vmm-san/enable-protect.png)

Después de que las máquinas virtuales están habilitadas para replicación, aparecen en la consola de Site Recovery Hola. Puede ver las propiedades de la máquina virtual, realizar un seguimiento del estado y hacer un seguimiento de la conmutación por error de los grupos de replicación que contengan varias máquinas virtuales. En la replicación de SAN, todas las máquinas virtuales asociadas a un grupo de replicación deben realizar la conmutación por error de manera conjunta. Esto es porque la conmutación por error se produce en la capa de almacenamiento de hello en primer lugar. Es importante toogroup grupos correctamente de la replicación y colocar solo las máquinas virtuales asociadas conjuntamente.

> [!NOTE]
> Después de habilitar la replicación para una máquina virtual, no agregue su tooLUNs de discos duros virtuales a menos que se encuentran en un grupo de replicación de Site Recovery. Si los LUN no están en un grupo de replicación de Site Recovery, este no los detectará.
>
>

Puede seguir el progreso, incluida la replicación inicial de hello, en hello **trabajos** ficha. Después de ejecutar el trabajo de finalización de la protección de hello, máquina virtual de hello está preparado para conmutación por error.

![Virtual machine protection job](./media/site-recovery-vmm-san/job-props.png)

## <a name="step-8-test-hello-deployment"></a>Paso 8: Probar la implementación de Hola

Probar la toomake de implementación seguro de que las máquinas virtuales conmute por error según lo previsto. toodo esto, cree un plan de recuperación y ejecute una conmutación por error de prueba.

1. En hello **planes de recuperación** , haga clic en **crear un Plan de recuperación**.
2. Especifique un nombre para el plan de recuperación de Hola y seleccionar los servidores VMM de origen y de destino. servidor de origen de Hello debe tener las máquinas virtuales que están habilitadas para conmutación por error y recuperación. Seleccione **SAN** tooview solo las nubes que están configuradas para la replicación de SAN.

    ![Creación de un plan de recuperación](./media/site-recovery-vmm-san/r-plan.png)

3. En **Seleccionar máquinas virtuales**, seleccione grupos de replicación. Todas las máquinas virtuales asociadas a grupo de Hola se agregan toohello plan de recuperación. Estas máquinas virtuales se agregan el grupo predeterminado de plan de recuperación toohello (grupo 1). Puede agregar más grupos si es necesario. Después de la replicación, las máquinas virtuales se numeran según el orden de toohello de grupos de planes de recuperación de Hola.

    ![Selección de máquinas virtuales](./media/site-recovery-vmm-san/r-plan-vm.png)
4. Después de crea el plan de recuperación de hello, aparece en la lista de hello en hello **planes de recuperación** ficha. Seleccione el plan de Hola y elija **conmutación por error de prueba**.
5. En hello **confirmar la conmutación por error** página, seleccione **ninguno**. Con esta opción habilitada, Hola conmutado por error máquinas virtuales de réplica no estará conectada tooany red. Realizará pruebas en ese Hola conmutar las máquinas virtuales según lo previsto, pero no prueba el entorno de red de Hola. Para más información sobre otras opciones de redes, consulte [Conmutación por error en Site Recovery](site-recovery-failover.md).

    ![Selección de la red de prueba](./media/site-recovery-vmm-san/test-fail1.png)

6. máquina virtual de prueba de Hola se crea en Hola mismo host como host de hello en qué réplica Hola existe la máquina virtual. No se agrega en la nube toohello en qué Hola VM de réplica se encuentra.
2. Después de la replicación, VM de réplica de hello tendrá una dirección IP diferente que las máquinas virtuales de hello principal. Si emite direcciones desde DHCP, se actualizará automáticamente. Si no está usando DHCP y desea Hola mismo direcciones, necesita toorun un par de secuencias de comandos.
3. Ejecute esta dirección IP de secuencia de comandos tooretrieve hello:

       $vm = Get-SCVirtualMachine -Name <VM_NAME>
       $na = $vm[0].VirtualNetworkAdapters>
       $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
       $ip.address  

4. Ejecute este tooupdate de secuencia de comandos de ejemplo DNS. Especificar dirección IP de hello recuperada.

       [string]$Zone,
       [string]$name,
       [string]$IP
       )
       $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
       $newrecord = $record.clone()
       $newrecord.RecordData[0].IPv4Address  =  $IP
       Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord


## <a name="next-steps"></a>Pasos siguientes

Una vez ejecutado un toocheck de conmutación por error de prueba que su entorno está funcionando según lo previsto, consulte [conmutación por error de Site Recovery](site-recovery-failover.md) toolearn acerca de los diferentes tipos de conmutaciones por error.
