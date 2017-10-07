---
title: "máquinas virtuales de Hyper-V aaaReplicate en tooAzure de nubes VMM | Documentos de Microsoft"
description: "Este artículo describe cómo tooreplicate máquinas de virtuales de Hyper-V en hosts de Hyper-V ubicado en tooAzure de nubes de System Center VMM."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 9d526a1f-0d8e-46ec-83eb-7ea762271db5
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: 136f68585534c17b615ecc4e82c0133bf813503f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure"></a>Replicar máquinas virtuales de Hyper-V en tooAzure de nubes VMM
> [!div class="op_single_selector"]
> * [Azure Portal](site-recovery-vmm-to-azure.md)
> * [PowerShell: administrador de recursos](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [Portal clásico](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell: clásico](site-recovery-deploy-with-powershell.md)
>
>

Hola servicio Azure Site Recovery contribuye tooyour la continuidad del negocio y estrategia de recuperación (BCDR) mediante la replicación de organización, la conmutación por error y la recuperación de máquinas virtuales y servidores físicos. Máquinas pueden ser replicada tooAzure o centro de datos local secundario tooa. Para obtener una introducción rápida, lea [¿Qué es Site Recovery?](site-recovery-overview.md)

## <a name="overview"></a>Información general
Este artículo describe cómo toodeploy Site Recovery tooreplicate Hyper-V máquinas virtuales Hyper-V hospedar servidores que se encuentran en tooAzure de nubes privadas de VMM.

artículo de Hello incluye requisitos previos para el escenario de Hola y muestra cómo tooset un almacén de Site Recovery, obtener Hola proveedor de Azure Site Recovery instalado en el servidor VMM de origen de hello, Registrar servidor hello en el almacén de hello, agregar una cuenta de almacenamiento de Azure, instale Hola Agente de servicios de recuperación de Azure en servidores de host de Hyper-V, configurar la protección para nubes VMM que será aplicado tooall protegido las máquinas virtuales y, a continuación, habilitar la protección de las máquinas virtuales. Finalice prueba toomake de conmutación por error de Hola que todo funciona según lo previsto.

Enviar comentarios o preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architecture"></a>Arquitectura
![Arquitectura](./media/site-recovery-vmm-to-azure-classic/topology.png)

* Hola proveedor de Azure Site Recovery está instalado en hello VMM durante la implementación de Site Recovery y servidor VMM de hello está registrado en el almacén de Site Recovery Hola. Hola proveedor se comunica con la orquestación de replicación de Site Recovery toohandle.
* agente de servicios de recuperación de Azure de Hola se instala en los servidores de host de Hyper-V durante la implementación de Site Recovery. Controla el almacenamiento de tooAzure de replicación de datos.

## <a name="azure-prerequisites"></a>Requisitos previos de Azure
Esto es lo que necesita en Azure:

| **Requisito previo** | **Detalles** |
| --- | --- |
| **Cuenta de Azure** |Necesitará una cuenta de [Microsoft Azure](https://azure.microsoft.com/) . Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/). [Más información](https://azure.microsoft.com/pricing/details/site-recovery/) sobre los precios de Site Recovery. |
| **Almacenamiento de Azure** |Necesitará un toostore replicado de datos de la cuenta de almacenamiento de Azure. Los datos replicados se almacenan en el almacenamiento de Azure y las máquinas virtuales de Azure se ponen en marcha cuando se produce la conmutación por error. <br/><br/>Necesita una [cuenta de almacenamiento con redundancia geográfica de tipo estándar](../storage/common/storage-redundancy.md#geo-redundant-storage). debe ser la cuenta de Hello en Hola misma región que el servicio de Site Recovery de Hola y asociarse Hola misma suscripción. Tenga en cuenta que las cuentas de almacenamiento de toopremium de replicación no se admite actualmente y no deben usarse.<br/><br/>[Más información sobre](../storage/common/storage-introduction.md) almacenamiento de Azure. |
| **Red de Azure** |Necesitará una red virtual de Azure que se conectarán las máquinas virtuales de Azure se produce la conmutación por error de toowhen. red virtual de Azure Hello debe ser una Hola misma región que el almacén de Site Recovery Hola. |

## <a name="on-premises-prerequisites"></a>Requisitos previos locales
Esto es lo que necesita en el entorno local.

| **Requisito previo** | **Detalles** |
| --- | --- |
| **VMM** |Necesitará al menos un servidor VMM implementado como un servidor físico o virtual independiente o como un clúster virtual. <br/><br/>servidor VMM Hola debe ejecutar System Center 2012 R2 con hello últimas actualizaciones acumulativas.<br/><br/>Necesitará al menos una nube configurada en el servidor VMM Hola.<br/><br/>nube de origen de Hola que desea tooprotect debe contener uno o varios grupos de host VMM.<br/><br/>Puede obtener más información sobre cómo configurar nubes de VMM en [Walkthrough: Creating private clouds with System Center 2012 SP1 VMM (Tutorial: Creación de nubes privadas) con System Center 2012 SP1 VMM](http://blogs.technet.com/b/keithmayer/archive/2013/04/18/walkthrough-creating-private-clouds-with-system-center-2012-sp1-virtual-machine-manager-build-your-private-cloud-in-a-month.aspx) en el blog de Keith Mayer. |
| **Hyper-V** |Necesitará uno o más servidores de host de Hyper-V o clústeres en hello nube de VMM. debe tener el servidor de host de Hello y una o más máquinas virtuales. <br/><br/>servidor Hello Hyper-V debe ejecutarse en al menos **Windows Server 2012 R2** con el rol de Hyper-V de Hola o **Microsoft Hyper-V Server 2012 R2** y ha hello las últimas actualizaciones instaladas.<br/><br/>Cualquier servidor de Hyper-V que contiene máquinas virtuales que desee tooprotect debe estar ubicado en una nube de VMM.<br/><br/>Si está ejecutando Hyper-V en un clúster, tenga en cuenta que ese agente de clúster no se crea automáticamente si tiene un clúster basado en una dirección IP estática. Necesitará a un agente de clúster hello tooconfigure manualmente. [Más información](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters) en la entrada de blog de Aidan Finn. |
| **Máquinas protegidas** | Máquinas virtuales que desea que deben cumplir tooprotect [requisitos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements). |

## <a name="network-mapping-prerequisites"></a>Requisitos previos de asignación de redes
Al proteger las máquinas virtuales en mapas de asignación de red de Azure entre redes de VM Hola servidor VMM de origen y destino siguiente de hello tooenable de redes de Azure:

* Todas las máquinas que conmutan en hello mismo pueden conectar tooeach otro, independientemente del plan de recuperación que se encuentran en red.
* Si se configura una puerta de enlace de red en red Azure de destino de hello, máquinas virtuales pueden conectarse a máquinas virtuales de tooother local.
* Si no configura la red asignación solo las máquinas virtuales que conmutan en hello mismo plan de recuperación será capaz de tooconnect tooeach otros después tooAzure de conmutación por error.

Si desea que la asignación de red toodeploy, necesitará la siguiente de hello:

* Hello las máquinas virtuales que desee tooprotect Hola servidor VMM de origen debe ser una red de VM tooa conectado. Esta red debe ser tooa vinculado red lógica que está asociado a la nube de Hola.
* Puede conectar una red Azure toowhich replicado a máquinas virtuales después de la conmutación por error. Esta red seleccionará en tiempo de Hola de conmutación por error. red de Hello debe formar parte de hello misma región que su suscripción de Azure Site Recovery.


Prepare las redes en VMM:

   * [Configure redes lógicas](https://technet.microsoft.com/library/jj721568.aspx).
   * [Configure redes de máquinas virtuales](https://technet.microsoft.com/library/jj721575.aspx).


## <a name="step-1-create-a-site-recovery-vault"></a>Paso 1: Creación de un almacén de recuperación del sitio
1. Inicie sesión en toohello [Portal de administración](https://portal.azure.com) desde el servidor VMM Hola desea tooregister.
2. Haga clic en **Servicios de datos** > **Servicios de recuperación** > **Almacén de Site Recovery**.
3. Haga clic en **Crear nuevo	** > **Creación rápida**.
4. En **nombre**, escriba en el almacén de hello tooidentify un nombre descriptivo.
5. En **región**, seleccione Hola región geográfica para el almacén de Hola. toocheck admite regiones, consulte disponibilidad geográfica en [detalles de precios de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Haga clic en **Crear almacén**.

    ![Almacén nuevo](./media/site-recovery-vmm-to-azure-classic/create-vault.png)

Compruebe tooconfirm de barra de estado de Hola que Hola almacén se creó correctamente. almacén de Hola se mostrarán como **Active** en la página principal de servicios de recuperación de Hola.

## <a name="step-2-generate-a-vault-registration-key"></a>Paso 2: Generación de una clave de registro de almacén
Generar una clave de registro en el almacén de Hola. Después de descargar hello Azure Site Recovery Provider e instalarlo en el servidor VMM hello, deberá usar este servidor VMM de hello tooregister clave en el almacén de Hola.

1. Hola **servicios de recuperación** página, haga clic en página de inicio rápido de hello almacén tooopen Hola. Inicio rápido también se puede abrir en cualquier momento mediante el icono de Hola.

    ![Icono de inicio rápido](./media/site-recovery-vmm-to-azure-classic/qs-icon.png)
2. En la lista desplegable de hello, seleccione **entre un sitio VMM local y Microsoft Azure**.
3. En **Preparar servidores VMM**, haga clic en **Generar archivo de clave de registro**. archivo de clave de Hola se genera automáticamente y es válida durante 5 días después de generarlo. Si no va a acceder a Hola portal de Azure desde un servidor VMM Hola deberá toocopy este servidor de archivos de toohello.

    ![Clave de registro](./media/site-recovery-vmm-to-azure-classic/register-key.png)

## <a name="step-3-install-hello-azure-site-recovery-provider"></a>Paso 3: Instalar hello Azure Site Recovery Provider
1. En **inicio rápido** > **servidores VMM preparar**, haga clic en **descargar Microsoft Azure Site Recovery Provider para su instalación en servidores VMM** tooobtain Hola última versión del archivo de instalación del proveedor de hello.
2. Ejecute este archivo hello servidor VMM de origen.

   > [!NOTE]
   > Si VMM está implementado en un clúster y está instalando hello proveedor para hello primera vez instalarlo en un nodo activo y finalizar Hola instalación tooregister Hola servidor VMM en el almacén de Hola. Instale Hola proveedor en hello otros nodos. Tenga en cuenta que si va a actualizar Hola proveedor deberá tooupgrade en todos los nodos ya que deberían todos pueden ejecutar Hola misma versión del proveedor.
   >
   >
3. Hola instalador realiza una comprobación de requisitos previos y las solicitudes de permiso toostop Hola VMM servicio toobegin proveedor el programa de instalación. Hola servicio VMM se reiniciará automáticamente cuando finaliza el programa de instalación. Si va a instalar en un clúster VMM que le pedirá el rol de clúster de toostop Hola.
4. En **Microsoft Update** puede optar por recibir actualizaciones. Con esta configuración habilitadas actualizaciones de proveedor se instalarán según la directiva de Microsoft Update tooyour.

    ![Microsoft Updates](./media/site-recovery-vmm-to-azure-classic/updates.png)
5. Hola ubicación de instalación de hello proveedor está establecido demasiado**<SystemDrive>\Program System Center 2012 R2\Virtual Machine Manager\bin**. Haga clic en **Instalar**.

   ![InstallLocation](./media/site-recovery-vmm-to-azure-classic/install-location.png)
6. Después de hello proveedor está instalado, haga clic en **registrar** tooregister servidor de hello en el almacén de Hola.

    ![InstallComplete](./media/site-recovery-vmm-to-azure-classic/install-complete.png)
7. En **nombre del almacén**, compruebe el nombre de Hola de almacén de hello en qué Hola se registrará el servidor. Haga clic en *Siguiente*.

    ![Registro de servidor](./media/site-recovery-vmm-to-azure-classic/vaultcred.PNG)
8. En **conexión a Internet** especificar cómo Hola proveedor se ejecuta en hello VMM toohello Internet conecta el servidor. Seleccione **conectar con la configuración de proxy existente** configuración de la conexión de Internet de toouse Hola predeterminado configurado en el servidor de Hola.

    ![Configuración de Internet](./media/site-recovery-vmm-to-azure-classic/proxydetails.PNG)

   * Si desea que toouse un proxy personalizado debe configurarla antes de instalar el proveedor de Hola. Al establecer la configuración de proxy personalizada ejecutará una prueba conexión del proxy toocheck Hola.
   * Si usa a un proxy personalizado o el proxy predeterminado requiere autenticación necesitará detalles del proxy hello tooenter, incluido el puerto y dirección de proxy de Hola.
   * Las siguientes direcciones URL deben ser accesible desde hello servidor VMM y hosts de Hyper-v de Hola
     * *.hypervrecoverymanager.windowsazure.com
     * *.accesscontrol.windows.net
     * *.backup.windowsazure.com
     * *.blob.core.windows.net
     * *.store.core.windows.net
   * Permitir que se describe en las direcciones IP hello [intervalos de IP del centro de datos de Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) y el protocolo HTTPS (443). ¿Tienen intervalos IP de toowhite-list de hello región de Azure que piensa toouse y del oeste de Estados Unidos.
   * Si usa un proxy personalizado una cuenta de ejecución de VMM (DRAProxyAccount) se creará automáticamente con hello especificada las credenciales del proxy. Configurar servidor proxy de Hola para que esta cuenta se pueda autenticar correctamente. configuración de la cuenta de Hello RunAs de VMM puede modificarse en la consola VMM Hola. toodo, abra hello **configuración** área de trabajo, expanda **seguridad**, haga clic en **cuentas de ejecución**y, a continuación, modificar contraseña Hola de DRAProxyAccount. Necesitará el servicio VMM hello toorestart para que esta configuración surta efecto.
9. En **clave de registro**, seleccione clave de Hola que descargó desde Azure Site Recovery y copió toohello servidor VMM.
10. configuración de cifrado de Hello sólo se utiliza al replicar las máquinas virtuales de Hyper-V en tooAzure de nubes VMM. Si replica tooa de sitio secundario no se utiliza.
11. En **nombre del servidor**, especifique un servidor VMM Nombre_descriptivo tooidentify hello en el almacén de Hola. En una configuración de clúster especificar nombre de rol de clúster VMM Hola.
12. En **sincronizar metadatos de nube** seleccione si desea toosynchronize metadatos para todas las nubes en el servidor VMM de hello con almacén de Hola. Esta acción solo debe toohappen una vez en cada servidor. Si no desea toosynchronize todas las nubes, puede dejar esta configuración desactivada y sincronizar cada nube individualmente en las propiedades de la nube de hello en la consola VMM Hola.
13. Haga clic en **siguiente** toocomplete proceso de Hola. Después del registro, Azure Site Recovery recupera metadatos desde un servidor VMM Hola. servidor Hola se muestra en hello **servidores VMM** ficha en hello **servidores** página en el almacén de Hola.

    ![Última página](./media/site-recovery-vmm-to-azure-classic/provider13.PNG)

Después del registro, Azure Site Recovery recupera metadatos desde un servidor VMM Hola. servidor Hola se muestra en hello **servidores VMM** ficha en hello **servidores** página en el almacén de Hola.

### <a name="command-line-installation"></a>Instalación de la línea de comandos
Hello Azure Site Recovery Provider se puede instalar también con hello después de la línea de comandos. Este método puede ser proveedor de hello tooinstall usado en un núcleo de servidor para Windows Server 2012 R2.

1. Hola proveedor carpeta de instalación de archivos y registro tooa clave de descarga. Por ejemplo, C:\ASR.
2. Detener servicio de System Center Virtual Machine Manager de Hola
3. Desde un símbolo del sistema con privilegios elevados, extraiga el instalador de proveedor de hello con estos comandos:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Instalar el proveedor de hello como se indica a continuación:

        C:\ASR> setupdr.exe /i
5. Registrar Hola proveedor como sigue:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>       

Los parámetros son los siguientes:

* **/ Credenciales de** : parámetro obligatorio que especifica la ubicación de hello en qué Hola se encuentra el archivo de clave de registro  
* **/ FriendlyName** : parámetro obligatorio Nombre hello del servidor de host de Hyper-V de Hola que aparece en el portal de Azure Site Recovery Hola.
* **/ EncryptionEnabled** : parámetro opcional toospecify si desea tooencryption las máquinas virtuales en Azure (en el cifrado de rest). nombre de archivo de Hello debe tener un **.pfx** extensión.
* **/proxyAddress** : parámetro opcional que especifica la dirección de saludo del servidor de proxy de Hola.
* **/proxyPort** : parámetro opcional que especifica el puerto de saludo del servidor de proxy de Hola.
* **/ proxyusername** : parámetro opcional que especifica el nombre de usuario de proxy de Hola.
* **/ proxypassword** : parámetro opcional que especifica la contraseña del proxy Hola.  

## <a name="step-4-create-an-azure-storage-account"></a>Paso 4: Creación de una cuenta de almacenamiento de Azure
1. Si no tienes una cuenta de almacenamiento de Azure haga clic en **agregar una cuenta de almacenamiento de Azure** toocreate una cuenta.
2. Cree una cuenta con la replicación geográfica habilitada. Debe Hola misma región que Hola servicio Azure Site Recovery en y asociarse con hello misma suscripción.

    ![Cuenta de almacenamiento](./media/site-recovery-vmm-to-azure-classic/storage.png)

> [!NOTE]
> [Migración de cuentas de almacenamiento](../azure-resource-manager/resource-group-move-resources.md) a través de recursos grupos dentro Hola misma suscripción o en las suscripciones no se admite para las cuentas de almacenamiento utilizadas para la implementación de Site Recovery.
>
>

## <a name="step-5-install-hello-azure-recovery-services-agent"></a>Paso 5: Instalar Hola agente de servicios de recuperación de Azure
Instalar a agente de servicios de recuperación de Azure de hello en cada servidor de host de Hyper-V en hello nube de VMM.

1. Haga clic en **inicio rápido** > **descargar los agente de servicios de recuperación de sitio de Azure e instalarlo en hosts** versión más reciente de tooobtain Hola Hola agente del archivo de instalación.

    ![Install Recovery Services Agent](./media/site-recovery-vmm-to-azure-classic/install-agent.png)
2. Ejecute el archivo de instalación de hello en cada servidor de host de Hyper-V.
3. En hello **comprobación de requisitos previos** página haga clic en **siguiente**. Todos los requisitos previos que falten se instalarán automáticamente.

    ![Requisitos previos del agente de Recovery Services](./media/site-recovery-vmm-to-azure-classic/agent-prereqs.png)
4. En hello **configuración de la instalación** página, especifique dónde desea tooinstall agente de Hola y la ubicación de caché de hello select en la que se instalarán los metadatos de copia de seguridad. Luego haga clic en **Instalar**.
5. Una vez finalizada instalación haga clic en **cerrar** Asistente de hello toocomplete.

    ![Registro del agente MARS](./media/site-recovery-vmm-to-azure-classic/agent-register.png)

### <a name="command-line-installation"></a>Instalación de la línea de comandos
También puede instalar agente de servicios de recuperación de Microsoft Azure Hola de línea de comandos de hello mediante este comando:

    marsagentinstaller.exe /q /nu

## <a name="step-6-configure-cloud-protection-settings"></a>Paso 6: Configuración de la protección de la nube
Una vez registrado el servidor VMM de hello, puede configurar los valores de protección. Habilitada opción hello **sincronizar datos en la nube con el almacén de hello** cuando instaló Hola proveedor aparecerán todas las nubes en el servidor VMM de hello en hello <b>elementos protegidos</b> ficha en el almacén de Hola.

![Nube publicada](./media/site-recovery-vmm-to-azure-classic/clouds-list.png)

1. En la página de inicio rápido de hello, haga clic en **configurar la protección para nubes de VMM**.
2. En hello **elementos protegidos** pestaña, haga clic en la nube de Hola que desee tooconfigure y vaya toohello **configuración** ficha.
3. En **Red de destino** select **Azure**.
4. En **cuenta de almacenamiento** seleccione Hola cuenta de almacenamiento de Azure utiliza para la replicación.
5. Establecer **cifrar datos almacenados** demasiado**desactivar**. Esta configuración especifica que los datos se deben cifrar durante la replicación entre el sitio local de Hola y Azure.
6. En **copiar frecuencia** deje la configuración predeterminada de Hola. Este valor especifica la frecuencia con que se deben sincronizar los datos entre las ubicaciones de origen y de destino.
7. En **conservar puntos de recuperación para**, deje la configuración predeterminada de Hola. Con un valor predeterminado de cero, solo Hola último punto de recuperación para una máquina virtual principal se almacena en un servidor de host de réplica.
8. En **frecuencia de las instantáneas coherentes con la aplicación**, deje la configuración predeterminada de Hola. Este valor se especifica con qué frecuencia toocreate instantáneas. Instantáneas usan el servicio de instantáneas de volumen (VSS) tooensure que las aplicaciones están en un estado coherente cuando se tomó la instantánea de Hola.  Si establece un valor, asegúrese de que es menor que el número de Hola de puntos de recuperación adicionales que configure.
9. En **tiempo de inicio de la replicación**, especifique cuándo debe comenzar la replicación inicial de tooAzure de datos. se utilizará la zona horaria de Hello en el servidor de host de Hyper-V de Hola. Se recomienda que programe la replicación inicial de Hola durante horas de poca actividad.

    ![Cloud replication settings](./media/site-recovery-vmm-to-azure-classic/cloud-settings.png)

Después de guardar los valores de hello un trabajo se crearán y se pueden supervisar en hello **trabajos** ficha. Todos los servidores de host de Hyper-V en hello nube de origen VMM se configurarán para la replicación.

Después de guardar, se puede modificar la configuración de la nube en hello **configurar** ficha toomodify Hola destino ubicación destino cuenta de almacenamiento o que necesitan una configuración de nube de hello tooremove y, a continuación, volver a configurar en la nube Hola. Tenga en cuenta que si cambia Hola almacenamiento cuenta Hola cambio solo se aplica para máquinas virtuales que están habilitadas para la protección después de que se ha modificado la cuenta de almacenamiento de Hola. No se migran las máquinas virtuales existentes toohello nueva cuenta de almacenamiento.

## <a name="step-7-configure-network-mapping"></a>Paso 7: Configuración de la asignación de red
Antes de empezar la asignación de red Compruebe que máquinas virtuales en el servidor VMM de origen Hola son red de VM tooa conectado. Además, cree una o varias redes virtuales de Azure. Tenga en cuenta que varias redes de VM pueden ser asignado tooa sola red de Azure.

1. En la página de inicio rápido de hello, haga clic en **asignar redes**.
2. En hello **redes** ficha **ubicación de origen**, seleccione servidor VMM de origen Hola. En **Ubicación de destino** , seleccione Azure.
3. En **origen** se muestran las redes una lista de redes de VM asociada con el servidor VMM Hola. En **destino** redes hello Azure se muestran las redes asociadas a la suscripción de Hola.
4. Seleccione la red de VM de origen de Hola y haga clic en **mapa**.
5. En hello **seleccionar una red de destino** página destino Hola seleccione red de Azure que desee toouse.
6. Haga clic en el proceso de asignación de hello marca de verificación toocomplete Hola.

    ![Cloud replication settings](./media/site-recovery-vmm-to-azure-classic/map-networks.png)

Después de guardar los valores de hello inicia un trabajo tootrack progreso de asignación de Hola y puede supervisarse en la ficha trabajos del saludo. Las máquinas virtuales de réplica existente que corresponden toohello red de VM de origen será toohello conectado redes de Azure de destino. Nuevas máquinas virtuales que son redes VM de origen conectado toohello será toohello conectado de red Azure asignada después de la replicación. Si modifica una asignación existente con una nueva red, máquinas virtuales de réplica se conectarán utilizando una nueva configuración de Hola.

Tenga en cuenta que si la red de destino de hello tiene varias subredes y una de estas subredes se Hola mismo nombre que la subred en la máquina virtual de origen de Hola se encuentra, entonces Hola máquina virtual será toothat conectado subred de destino después de la conmutación por error. Si no hay ninguna subred de destino con un nombre coincidente, máquina virtual de hello estará conectado toohello primera subred de red de Hola.

> [!NOTE]
> [Migración de redes](../azure-resource-manager/resource-group-move-resources.md) a través de recursos grupos dentro Hola misma suscripción o en las suscripciones no se admite para las redes usadas para la implementación de Site Recovery.
>
>

## <a name="step-8-enable-protection-for-virtual-machines"></a>Paso 8: Habilitación de la protección para las máquinas virtuales
Después de servidores, las nubes y las redes están configuradas correctamente, puede habilitar la protección de máquinas virtuales en la nube de Hola. Tenga en cuenta los siguiente hello:

* Las máquinas virtuales de deben cumplir los [requisitos de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
* sistema operativo de tooenable protección hello y propiedades del disco de sistema operativo deben establecerse para la máquina virtual de Hola. Cuando se crea una máquina virtual en VMM mediante una plantilla de máquina virtual puede establecer la propiedad Hola. También puede establecer estas propiedades para las máquinas virtuales existentes en hello **General** y **configuración de Hardware** fichas de propiedades de la máquina virtual de Hola. Si no establece estas propiedades en VMM estará tooconfigure capaz de ellas en el portal de Azure Site Recovery Hola.

    ![Create virtual machine](./media/site-recovery-vmm-to-azure-classic/enable-new.png)

    ![Modify virtual machine properties](./media/site-recovery-vmm-to-azure-classic/enable-existing.png)

1. protección de tooenable, vaya a hello **máquinas virtuales** , haga clic en la nube de hello en qué Hola se encuentra la máquina virtual **habilitar la protección** > **agregar máquinas virtuales**.
2. En lista de Hola de máquinas virtuales en la nube de hello, seleccione Hola uno desea tooprotect.

    ![Habilitar protección de máquina virtual](./media/site-recovery-vmm-to-azure-classic/select-vm.png)

    Realizar seguimiento del progreso del programa Hola a **Habilitar protección** acción Hola **trabajos** ficha, incluida la replicación inicial de Hola. Después de hello **finalización de protección** ejecuciones del trabajo Hola virtual machine está preparado para conmutación por error. Después de habilitar la protección y máquinas virtuales se replican, podrá tooview capaz de ellas en Azure.

    ![Virtual machine protection job](./media/site-recovery-vmm-to-azure-classic/vm-jobs.png)

1. Compruebe las propiedades de la máquina virtual de Hola y modifíquela según sea necesario.

    ![Verify virtual machines](./media/site-recovery-vmm-to-azure-classic/vm-properties.png)
2. En hello **configurar** ficha de propiedades de la máquina virtual de hello propiedades de red siguientes se puede modificar.

* **Número de adaptadores de red de máquina virtual de destino de hello** -número de Hola de adaptadores de red es dictados por tamaño de Hola que especifique para la máquina virtual de destino de Hola. Comprobar [las especificaciones de tamaño de máquina virtual](../virtual-machines/linux/sizes.md) para el número de Hola de adaptadores compatibles con el tamaño de la máquina virtual de Hola. Al modificar el tamaño de Hola para una máquina virtual y guardar la configuración de hello, número de Hola de adaptadores de red cambiará Hola próxima vez que abra hello **configurar** página. número de Hola de adaptadores de red de máquinas virtuales de destino es número mínimo de Hola de adaptadores de red en la máquina virtual y Hola número máximo de origen de los adaptadores de red compatible con hello tamaño de máquina virtual de hello elegido, como se indica a continuación:

  * Si el número de Hola de adaptadores de red en la máquina de origen de hello es menor o igual toohello de adaptadores permitidas para el tamaño de máquina de destino de hello, a continuación, tendrá destino Hola Hola el mismo número de adaptadores como origen de Hola.
  * Si número Hola de adaptadores para la máquina virtual de origen de hello supera número Hola permitido para el tamaño de destino de hello después máximo de tamaño de destino de Hola se usará.
  * Por ejemplo, si una máquina de origen tiene dos adaptadores de red y tamaño de máquina de destino de hello es compatible con cuatro, el equipo de destino Hola tendrá dos adaptadores. Si la máquina de origen hello tiene dos adaptadores de pero hello tamaño de destino admitida solo admite un equipo de destino de Hola tendrá solo un adaptador.     
* **Red de máquina virtual de destino de hello** -máquina virtual de hello red toowhich Hola se conecta toois determinado por la asignación de red de red de Hola de máquina virtual de origen. Si la máquina virtual de origen de hello tiene más de una redes de origen y el adaptador de red son redes de toodifferent asignada en destino, deberá toochoose entre una de las redes de destino de Hola.
* **Subred de cada adaptador de red** : para cada adaptador de red puede seleccionar Hola Hola de toowhich de subred conmutado por máquina virtual se conectará a.
* **Dirección IP de destino** : si el adaptador de red de Hola de máquina virtual de origen está configurado toouse una dirección IP estática de direcciones, puede proporcionar direcciones IP de hello para la máquina virtual de destino de Hola. Utilice esta característica conservar Hola la dirección IP de una máquina virtual de origen después de una conmutación por error. Si no se proporciona ninguna dirección IP de cualquier dirección IP disponible es proporcionada toohello adaptador de red en el momento de Hola de conmutación por error. Si se especifica, dirección IP de destino de hello pero ya está en uso por otra máquina virtual que se ejecuta en Azure, a continuación, se producirá un error conmutación por error.  

    ![Modificación de las propiedades de red](./media/site-recovery-vmm-to-azure-classic/multi-nic.png)

> [!NOTE]
> No se admiten máquinas virtuales de Linux con una dirección IP estática.
>
>

## <a name="test-hello-deployment"></a>Implementación de prueba de Hola
plan de la implementación, puede ejecutar una prueba de conmutación por error para una sola máquina virtual, o crear un plan de recuperación que consta de varias máquinas virtuales y ejecutar una prueba de conmutación por error para hello tootest.  

La conmutación por error de prueba simula su mecanismo de conmutación por error y recuperación en una red aislada. Observe lo siguiente:

* Si desea tooconnect toohello virtual machine en Azure mediante Escritorio remoto después de la conmutación por error de hello, habilite la conexión a Escritorio remoto en la máquina virtual de hello antes de ejecutar la conmutación por error de prueba de Hola.
* Después de la conmutación por error, use un toohello de tooconnect de dirección IP pública VM de Azure mediante Escritorio remoto. Si desea toodo esto, asegúrese de que no hay ninguna directiva de dominio que impiden la conexión máquina virtual de tooa con una dirección pública.

> [!NOTE]
> tooget Hola obtener el mejor rendimiento cuando se conmuta por error tooAzure, asegúrese de que ha instalado Hola agente de Azure en hello máquina virtual. Esto proporciona un arranque más rápido y ayuda a solucionar problemas. Descargar hello [agente Linux](https://github.com/Azure/WALinuxAgent), o hello [el agente de Windows](http://go.microsoft.com/fwlink/?LinkID=394789).
>
>

### <a name="create-a-recovery-plan"></a>Creación de un plan de recuperación
1. En hello **planes de recuperación** ficha, agregue un nuevo plan. Especifique un nombre, **VMM** en **tipo de origen de**y el servidor VMM de origen de hello en **origen**. destino de Hello será Azure.

    ![Creación de un plan de recuperación](./media/site-recovery-vmm-to-azure-classic/recovery-plan1.png)
2. Hola **seleccionar máquinas virtuales** página, seleccione las máquinas virtuales tooadd toohello recuperación plan. Estas máquinas virtuales se agregan toohello grupo de manera predeterminada de plan de recuperación: grupo 1. Se ha probado un máximo de 100 máquinas virtuales en un solo plan de recuperación.

* Si desea que las propiedades de máquina virtual de hello tooverify antes de agregarlas toohello plan, haga clic en máquina virtual de hello en página de propiedades de Hola de nube de Hola donde encuentre. También puede configurar propiedades de la máquina virtual de hello en la consola VMM Hola.
* Todas máquinas virtuales de Hola que se muestran se han habilitado para protección. lista de Hello incluye ambas máquinas virtuales que están habilitadas para protección y la replicación inicial se ha completado y los que están habilitados para la protección con replicación inicial pendiente. Solo las máquinas virtuales con la replicación inicial completada pueden conmutar por error como parte de un plan de recuperación.

    ![Creación de un plan de recuperación](./media/site-recovery-vmm-to-azure-classic/select-rp.png)

Una vez creado un plan de recuperación aparece en hello **planes de recuperación** ficha. También puede agregar [runbooks de automatización de Azure](site-recovery-runbook-automation.md) acciones de tooautomate del plan de recuperación de toohello durante la conmutación por error.

### <a name="run-a-test-failover"></a>Ejecución de una conmutación por error de prueba
Hay dos toorun formas un tooAzure de conmutación por error de prueba.

* **Probar la conmutación por error sin una red de Azure**: este tipo de conmutación por error de prueba comprueba que la máquina virtual Hola aparece correctamente en Azure. máquina virtual de Hello no estará conectada tooany red de Azure después de la conmutación por error.
* **Probar la conmutación por error con una red de Azure**: este tipo de conmutación por error comprueba que Hola entorno de replicación total aparece como se esperaba y que se conmutaron hello las máquinas virtuales estarán conectados toohello red Azure de destino especificado. Para la gestión de subred, para conmutación por error de prueba subred Hola de máquina virtual de prueba de Hola se decidirá basado en la subred de Hola Hola máquina virtual de réplica. Se trata de replicación diferentes tooregular cuando subred Hola de máquina virtual de réplica se basa en la subred de Hola de máquina virtual de origen de Hola.

Si desea toorun una conmutación por error de prueba para una máquina virtual habilitada para protección tooAzure sin especificar una red de destino de Azure no es necesario tooprepare nada. toorun una conmutación por error de prueba con un destino de red de Azure necesitará toocreate una nueva red de Azure que esté aislada de la red de producción de Azure (comportamiento predeterminado cuando se crea una nueva red de Azure). Veamos cómo demasiado[ejecutar una prueba de conmutación por error](site-recovery-failover.md) para obtener más detalles.

También necesitará tooset una infraestructura de Hola para saludo replican toowork de máquina virtual según lo previsto. Por ejemplo, una máquina virtual con el controlador de dominio y DNS puede ser replicada tooAzure con Azure Site Recovery y pueden crearse en la red de prueba de hello mediante probar conmutación por error. Consulte la sección [Consideraciones sobre la conmutación por error de prueba para Active Directory](site-recovery-active-directory.md#test-failover-considerations) para más información.

Hola toorun una conmutación por error de prueba después de:

1. En hello **planes de recuperación** ficha, seleccione el plan de Hola y haga clic en **conmutación por error de prueba**.
2. En hello **confirmar la conmutación por error** página, seleccione **ninguno** o una red de Azure específica.  Tenga en cuenta que si selecciona ninguno le de conmutación por error de prueba de hello Compruebe que Hola máquina virtual replicado correctamente tooAzure pero no comprueba la configuración de red de replicación.

    ![Sin red](./media/site-recovery-vmm-to-azure-classic/test-no-network.png)
3. Si está habilitado el cifrado de datos de nube de hello en **clave de cifrado** certificado Hola seleccione emitida durante la instalación del programa Hola proveedor en el servidor VMM hello, al activar el cifrado de datos tooenable opción Hola para una nube .
4. En hello **trabajos** ficha que pueda seguir el progreso de la conmutación por error. También debe ser capaz de toosee réplica de prueba de máquina virtual de hello en Hola portal de Azure. Si está configurado tooaccess las máquinas virtuales de la red local puede iniciar una máquina virtual de escritorio remoto conexión toohello.
5. Cuando llegue a conmutación por error de Hola Hola **realice las pruebas oportunas** fase, haga clic en **prueba completa** toofinish lo. Puede explorar en profundidad toohello **trabajo** ficha tooperform y el estado y el progreso de la conmutación por error de tootrack todas las acciones que se necesitan.
6. Después de la conmutación por error, puede ver la réplica de prueba de la máquina virtual de Hola Hola portal de Azure. Si está configurado tooaccess las máquinas virtuales de la red local puede iniciar una máquina virtual de escritorio remoto conexión toohello. Hola siguientes:

   1. Compruebe que las máquinas virtuales de Hola se inician correctamente.
   2. Si desea tooconnect toohello virtual machine en Azure mediante Escritorio remoto después de la conmutación por error de hello, habilite la conexión a Escritorio remoto en la máquina virtual de hello antes de ejecutar la conmutación por error de prueba de Hola. También necesita un punto de conexión RDP en la máquina virtual de hello tooadd. Puede aprovechar una [Runbooks de automatización de Azure](site-recovery-runbook-automation.md) toodo que.
   3. Después de la conmutación por error, si usa una máquina de virtual toohello pública del tooconnect de dirección IP en Azure mediante Escritorio remoto, asegúrese de que no hay ninguna directiva de dominio que impiden la conexión de máquina virtual de tooa con una dirección pública.
7. Una vez finalizada la prueba de Hola Hola siguientes:

   * Haga clic en **conmutación por error de prueba de hello**. Limpiar Hola power tooautomatically de entorno de prueba desactivar y eliminar máquinas virtuales de prueba de Hola.
   * Haga clic en **notas** toorecord y guardar las observaciones asociadas con conmutación por error de prueba de Hola.


## <a name="next-steps"></a>Pasos siguientes
Aprenda sobre la [configuración de los planes de recuperación](site-recovery-create-recovery-plans.md) y la [conmutación por error](site-recovery-failover.md).
