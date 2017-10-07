---
title: "máquinas virtuales de Hyper-V en el sitio secundario de VMM tooa (clásico de Azure) aaaReplicate | Documentos de Microsoft"
description: "Este artículo describe cómo tooreplicate máquinas virtuales de Hyper-V en VMM nubes tooa sitio secundario de VMM con Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a63acba3-8fb3-4926-aa29-b1e64a765681
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ms.openlocfilehash: fe551e1f741579044f540ea0e50a6e36d48133ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>Replicar máquinas virtuales de Hyper-V en el sitio secundario de VMM de VMM nubes tooa
> [!div class="op_single_selector"]
> * [Portal de Azure](site-recovery-vmm-to-vmm.md)
> * [Portal clásico](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell: administrador de recursos](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Hola servicio Azure Site Recovery contribuye tooyour la continuidad del negocio y estrategia de recuperación (BCDR) mediante la replicación de organización, la conmutación por error y la recuperación de máquinas virtuales y servidores físicos. Máquinas pueden ser replicada tooAzure o centro de datos local secundario tooa. Para obtener una introducción rápida, lea [¿Qué es Site Recovery?](site-recovery-overview.md)

## <a name="overview"></a>Información general
Este artículo describe cómo máquinas virtuales de Hyper-V tooreplicate en Hyper-V hospedar servidores que se administran en el sitio de VMM del toosecondary de nubes VMM con Azure Site Recovery.

artículo de Hello incluye los requisitos previos, muestra también cómo instalar tooset un almacén de Site Recovery, Hola proveedor de Azure Site Recovery en el origen y los servidores VMM de destino, registrar servidores de hello en el almacén de hello, establecer la configuración de protección para nubes de VMM y, a continuación, habilitar protección para máquinas virtuales de Hyper-V. Finalice prueba toomake de conmutación por error de Hola que todo funciona según lo previsto.

Enviar comentarios o preguntas en parte inferior de este artículo, o en Hola de hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="architecture"></a>Arquitectura
Figura Hola siguiente muestra los canales de comunicación diferentes de Hola y puertos usados por Azure Site Recovery para la orquestación y la replicación

![Topología E2E](./media/site-recovery-vmm-to-vmm-classic/e2e-topology.png)

## <a name="before-you-start"></a>Antes de comenzar
Asegúrese de que tiene preparados estos requisitos previos:

| **Requisitos previos** | **Detalles** |
| --- | --- |
| **Las tablas de Azure** |Necesita una cuenta de [Microsoft Azure](https://azure.microsoft.com/) . Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/). [más información](https://azure.microsoft.com/pricing/details/site-recovery/) sobre los precios de Site Recovery. |
| **VMM** |Necesita al menos un servidor VMM.<br/><br/>servidor VMM Hola debe disponer de al menos System Center 2012 SP1 con hello últimas actualizaciones acumulativas.<br/><br/>Si desea que tooset la protección con un solo servidor VMM, necesita al menos dos nubes configuradas en el servidor de Hola.<br/><br/>Si desea que la protección toodeploy con dos servidores VMM, cada servidor debe tener al menos una nube configurada en servidor VMM principal Hola desea tooprotect y una nube configurada en el servidor VMM secundario de hello desea toouse para la protección y recuperación<br/><br/>Todas las nubes VMM deben tener el perfil de capacidad de Hyper-V de hello establecida.<br/><br/>nube de origen de Hola que desea tooprotect debe contener uno o varios grupos de host VMM. |
| **Hyper-V** |Necesita uno o más servidores de host de Hyper-V en grupos de host VMM de principal y secundarios hello y una o varias máquinas virtuales en cada servidor de host de Hyper-V.<br/><br/>Hello servidores de Hyper-V de host y de destino deben estar ejecutando al menos Windows Server 2012 con el rol de Hyper-V de Hola y Hola a las últimas actualizaciones instaladas.<br/><br/>Cualquier servidor de Hyper-V que contiene máquinas virtuales que desee tooprotect debe estar ubicado en una nube de VMM.<br/><br/>Si está ejecutando Hyper-V en un clúster, tenga en cuenta que ese agente de clúster no se crea automáticamente si tiene un clúster basado en una dirección IP estática. Necesita a un agente de clúster hello tooconfigure manualmente. [Más información](https://www.petri.com/use-hyper-v-replica-broker-prepare-host-clusters) en la entrada de blog de Aidan Finn. |
| **Asignación de red** |Puede configurar toomake de asignación de red seguro de que las máquinas virtuales replicadas se colocan de forma óptima en los servidores secundarios de host de Hyper-V después de la conmutación por error, y que se pueden conectar redes de VM de tooappropriate. Si no configura la asignación de red, las máquinas virtuales de réplica no será tooany conectado red después de la conmutación por error.<br/><br/>tooset la asignación de red durante la implementación, asegúrese de que máquinas virtuales de hello en el servidor de host de Hyper-V de origen Hola están conectado tooa red de VM de VMM. Esa red deben estar vinculados tooa red lógica que está asociado a la nube Hola. < br /<br/>nube de destino de Hello en el servidor VMM secundario Hola que usar para la recuperación debe tener configurada una red VM correspondiente y, a su vez debe ser tooa vinculado correspondiente de la red lógica que está asociado a la nube de destino de Hola. |
| **Asignación de almacenamiento** |De forma predeterminada cuando se replica una máquina virtual en un origen Hyper-V host servidor tooa Hyper-V host servidor de destino, los datos replicados se almacenan en la ubicación predeterminada de hello indicada para el host de Hyper-V de destino de hello en el Administrador de Hyper-V. Para obtener más control sobre dónde se almacenan los datos replicados, puede configurar la asignación de almacenamiento<br/><br/> almacenamiento de tooconfigure asignación, necesita tooset los sectores de almacenamiento en el origen de Hola y servidores VMM de destino antes de comenzar la implementación. |

## <a name="step-1-create-a-site-recovery-vault"></a>Paso 1: Creación de un almacén de recuperación del sitio
1. Inicie sesión en toohello [Portal de administración](https://portal.azure.com) desde el servidor VMM Hola desea tooregister.
2. Expanda **Data Services** > **Recovery Services** y haga clic en **Almacén de Site Recovery**.
3. Haga clic en **Crear nuevo	** > **Creación rápida**.
4. En **nombre**, escriba en el almacén de hello tooidentify un nombre descriptivo.
5. En **región** seleccione Hola región geográfica para el almacén de Hola. toocheck admite regiones, consulte disponibilidad geográfica en [detalles de precios de Azure Site Recovery](http://go.microsoft.com/fwlink/?LinkId=389880).
6. Haga clic en **Crear almacén**.

    ![Crear almacén](./media/site-recovery-vmm-to-vmm-classic/create-vault.png)

Se creó la verificación en ese almacén Hola la barra de estado de Hola. almacén de Hola se mostrarán como **Active** en la página principal de servicios de recuperación de Hola.

## <a name="step-2-generate-a-vault-registration-key"></a>Paso 2: Generación de una clave de registro de almacén
Generar una clave de registro en el almacén de Hola. Después de descargar hello Azure Site Recovery Provider e instalarlo en el servidor VMM hello, deberá usar este servidor VMM de hello tooregister clave en el almacén de Hola.

1. Hola **servicios de recuperación** página, haga clic en página de inicio rápido de hello almacén tooopen Hola. Inicio rápido también se puede abrir en cualquier momento mediante el icono de Hola.

    ![Icono de inicio rápido](./media/site-recovery-vmm-to-vmm-classic/quick-start-icon.png)
2. En la lista desplegable de hello, seleccione **entre dos sitios VMM local**.
3. En **Preparar servidores VMM**, haga clic en **Generar archivo de clave de registro**. archivo de clave de Hola se genera automáticamente y es válida durante 5 días después de generarlo. Si no va a acceder a Hola portal de Azure desde un servidor VMM Hola deberá toocopy este servidor de archivos de toohello.

    ![Clave de registro](./media/site-recovery-vmm-to-vmm-classic/register-key.png)

## <a name="step-3-install-hello-azure-site-recovery-provider"></a>Paso 3: Instalar hello Azure Site Recovery Provider
1. En hello **inicio rápido** página **servidores VMM preparar**, haga clic en **descargar Microsoft Azure Site Recovery Provider para su instalación en servidores VMM** tooobtain hello más reciente versión del archivo de instalación del proveedor de Hola.
2. Ejecute este archivo hello servidor VMM de origen.

   > [!NOTE]
   > Si VMM está implementado en un clúster y está instalando hello proveedor para hello primera vez instalarlo en un nodo activo y finalizar Hola instalación tooregister Hola servidor VMM en el almacén de Hola. Instale Hola proveedor en hello otros nodos. Tenga en cuenta que si va a actualizar Hola proveedor necesita tooupgrade en todos los nodos, ya que deberían todos pueden ejecutar Hola misma versión del proveedor.
   >
   >
3. Hola instalador algunos **comprobación de requisitos previos** y solicitudes de Hola de toostop permiso VMM toobegin la instalación del proveedor de servicio. Hola servicio VMM se reiniciará automáticamente cuando finaliza el programa de instalación. Si va a instalar en un clúster VMM que le pedirá el rol de clúster de toostop Hola.
4. En **Microsoft Update** puede optar por recibir actualizaciones. Con esta configuración habilitadas actualizaciones de proveedor se instalarán según la directiva de Microsoft Update tooyour.

    ![Microsoft Updates](./media/site-recovery-vmm-to-vmm-classic/ms-update.png)
5. ubicación de instalación de Hola se establece demasiado**<SystemDrive>\Program System Center 2012 R2\Virtual Machine Manager\bin**. Haga clic en hello instalación botón toostart instalar Hola proveedor.

    ![InstallLocation](./media/site-recovery-vmm-to-vmm-classic/install-location.png)
6. Después de hello proveedor está instalado, haga clic en **registrar** tooregister servidor de hello en el almacén de Hola.

    ![InstallComplete](./media/site-recovery-vmm-to-vmm-classic/install-complete.png)
7. En **nombre del almacén**, compruebe el nombre de Hola de almacén de hello en qué Hola se registrará el servidor. Haga clic en *Siguiente*.

    ![Registro de servidor](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
8. En **conexión a Internet** especificar cómo Hola proveedor se ejecuta en hello VMM toohello Internet conecta el servidor. Seleccione **conectar con la configuración de proxy existente** configuración de la conexión de Internet de toouse Hola predeterminado configurado en el servidor de Hola.

    ![Configuración de Internet](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   * Si desea que toouse un proxy personalizado debe configurarla antes de instalar el proveedor de Hola. Al establecer la configuración de proxy personalizada ejecutará una prueba conexión del proxy toocheck Hola.
   * Si usa a un proxy personalizado o el proxy predeterminado requiere autenticación necesita detalles del proxy hello tooenter, incluido el puerto y dirección de proxy de Hola.
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
13. Haga clic en **siguiente** toocomplete proceso de Hola. Después del registro, Azure Site Recovery recupera metadatos desde un servidor VMM Hola. Hola servidor se muestra en **servidores VMM** > **servidores** en el almacén de Hola.

    ![Servidores](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)

### <a name="command-line-installation"></a>Instalación de la línea de comandos
Hola proveedor de Azure Site Recovery también puede instalarse desde la línea de comandos de Hola. Este método puede ser proveedor de hello tooinstall usado en un núcleo de servidor para Windows Server 2012 R2.

1. Hola proveedor carpeta de instalación de archivos y registro tooa clave de descarga. Por ejemplo, C:\ASR.
2. Detener servicio de System Center Virtual Machine Manager Hola
3. Extraiga el instalador de proveedor de hello ejecutando estos comandos desde un símbolo del sistema con **administrador** privilegios:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
4. Instale al proveedor de hello con:

        C:\ASR> setupdr.exe /i
5. Registrar un proveedor Hola ejecutando:

        CD C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin
        C:\Program Files\Microsoft System Center 2012 R2\Virtual Machine Manager\bin\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>     

Donde hello parámetros son:

* **/ Credenciales de**: parámetro obligatorio que especifica la ubicación de hello en qué Hola se encuentra el archivo de clave de registro  
* **/ FriendlyName**: parámetro obligatorio Nombre hello del servidor de host de Hyper-V de Hola que aparece en el portal de Azure Site Recovery Hola.
* **/ EncryptionEnabled**: parámetro opcional que debe toouse solo en hello VMM tooAzure escenario si necesita cifrado de las máquinas virtuales en reposo en Azure. Asegúrese de que el nombre hello del archivo hello proporcionan tiene un **.pfx** extensión.
* **/proxyAddress**: parámetro opcional que especifica la dirección de saludo del servidor de proxy de Hola.
* **/proxyPort**: parámetro opcional que especifica el puerto de saludo del servidor de proxy de Hola.
* **/ proxyusername**: parámetro opcional que especifica el nombre de usuario de Proxy de hello (si el servidor proxy requiere autenticación).
* **/ proxypassword**: parámetro opcional que especifica Hola contraseña para autenticar con el servidor de proxy de hello (si el servidor proxy requiere autenticación).  

## <a name="step-4-configure-cloud-protection-settings"></a>Paso 4: Configuración de la protección de la nube
Una vez que los servidores VMM están registrados, puede configurar la protección de la nube. Si habilita la opción de hello **sincronizar datos en la nube con el almacén de hello** cuando instaló Hola proveedor aparecerán todas las nubes en el servidor VMM de hello en hello **elementos protegidos** ficha en el almacén de Hola. Si no se puede sincronizar una nube específica con Azure Site Recovery en hello **General** ficha de página de propiedades de nube de hello en la consola VMM Hola.

![Nube publicada](./media/site-recovery-vmm-to-vmm-classic/clouds-list.png)

1. En la página de inicio rápido de hello, haga clic en **configurar la protección para nubes de VMM**.
2. En hello **nubes de VMM** ficha, seleccione en la nube Hola que desee tooconfigure y vaya toohello **configuración** ficha.
3. En **Destino**, seleccione **VMM**.
4. En **ubicación de destino**, seleccione Hola servidor VMM local que administra en la nube Hola desea toouse para la recuperación.
5. En **nube de destino**, seleccione Hola nube de destino que desee toouse para conmutación por error de máquinas virtuales en la nube de origen Hola. Observe lo siguiente:

   * Le recomendamos que seleccione una nube de destino que cumpla los requisitos de recuperación para máquinas virtuales de Hola a proteger.
   * Una nube solo puede pertenecer tooa par de nube único, como un elemento principal o una nube de destino.
6. En **Copiar frecuencia**, especifique con qué frecuencia se deben sincronizar los datos entre las ubicaciones de origen y de destino. Tenga en cuenta que esta opción solo es pertinente cuando host de Hyper-V de saludo se está ejecutando Windows Server 2012 R2. En el caso de otros servidores, se utiliza una configuración predeterminada de cinco minutos.
7. En **puntos de recuperación adicionales**, especifique si desea que los puntos de toocreate adicionales. valor de cero por defecto de Hello indica que solo Hola último punto de recuperación para una máquina virtual principal se almacena en un servidor de host de réplica. Tenga en cuenta que al habilitar varios puntos de recuperación se necesita almacenamiento adicional para las instantáneas de Hola que se almacenan en cada punto de recuperación. De forma predeterminada, los puntos de recuperación se crean cada hora, por lo que cada punto de recuperación contiene datos equivalentes a una hora. valor de punto de recuperación de Hola que asigne a la máquina virtual de hello en la consola VMM hello no debe ser menor que valor Hola que asigne en la consola de Azure Site Recovery Hola.
8. En **frecuencia de las instantáneas coherentes con la aplicación**, especifique con qué frecuencia las instantáneas coherentes con la aplicación de toocreate. Hyper-V usa dos tipos de instantáneas, una instantánea estándar que proporciona una instantánea incremental de la máquina virtual completa de hello y una instantánea coherente con la aplicación que toma una instantánea de tiempo de punto de datos de la aplicación hello dentro de la máquina virtual de Hola. Las instantáneas coherentes con la aplicación usan tooensure de servicio de instantáneas de volumen (VSS) que las aplicaciones están en un estado coherente cuando se tomó la instantánea de Hola. Tenga en cuenta que si habilita las instantáneas coherentes con la aplicación, afectará Hola rendimiento de aplicaciones que se ejecutan en máquinas virtuales de origen. Asegúrese de que el valor de hello especificado es menor que el número de Hola de puntos de recuperación adicionales que configure.

    ![Configuración de los valores de protección](./media/site-recovery-vmm-to-vmm-classic/cloud-settings.png)
9. En **Compresión de transferencia de datos**, especifique si se deben comprimir los datos replicados que se transfieren.
10. En **autenticación**, especifique cómo se autentica el tráfico entre Hola principal y los servidores de host de Hyper-V de recuperación. Seleccione HTTPS a menos que tenga un entorno de Kerberos configurado en funcionamiento. Azure Site Recovery configurará automáticamente los certificados para la autenticación de HTTPS. No se requiere configuración manual. Si selecciona Kerberos, se usará un vale de Kerberos para la autenticación mutua de servidores de host de Hola. De forma predeterminada, los puertos 8083 y 8084 (para certificados) se abrirá en Hola Firewall de Windows en los servidores de host de Hyper-V de Hola. Observe que esta configuración solo es pertinente para servidores host de Hyper-V que se ejecutan en Windows Server 2012 R2.
11. En **puerto**, modifique el número de puerto de hello en el origen de Hola y escucha de los equipos host para el tráfico de replicación de destino. Por ejemplo, podría modificar configuración de hello si desea que la limitación para el tráfico de replicación el ancho de banda de red a calidad de servicio (QoS) de tooapply. Compruebe que el puerto hello no está usando ninguna otra aplicación y que está abierto en la configuración de firewall de Hola.
12. En **el método de replicación**, especifique cómo el que se tratará la replicación inicial de datos de origen tootarget ubicaciones de hello, antes de que inicie la replicación normal:

    * **A través de red**: copiar datos de red de hello puede resultar laborioso y gran cantidad de recursos. Se recomienda que use esta opción si en la nube hello contiene máquinas virtuales con discos duros virtuales relativamente pequeños y sitio primario de hello es sitio secundario toohello conectado mediante una conexión con mucho ancho de banda. Puede especificar que copia Hola debe iniciar inmediatamente o seleccionar una hora. Si utiliza la replicación de red, le recomendamos programarla evitando las horas de mayor consumo.
    * **Sin conexión**: este método especifica que la replicación inicial Hola se realizará usando medios externos. Resulta útil si desea tooavoid una degradación del rendimiento de la red, o para ubicaciones remotas geográficamente. toouse este método se especifica la ubicación de exportación de hello en la nube de origen de Hola y ubicación de importación de hello en nube de destino de Hola. Al habilitar la protección de una máquina virtual, disco duro virtual de hello es toohello copiado especificado ubicación de exportación. Enviar toohello sitio de destino y cópielo toohello ubicación de importación. Hola sistema copias Hola importa máquinas virtuales de información toohello réplica.
13. Seleccione **eliminar Máquina Virtual de réplica** toospecify que Hola máquina virtual de réplica debe eliminarse si se detiene la protección de máquina virtual de hello seleccionando hello **eliminar la protección de máquina virtual de Hola**  opción en la pestaña de máquinas virtuales de Hola de propiedades de la nube de Hola. Con esta opción habilitada, al deshabilitar la máquina virtual de Hola de protección se quita de Azure Site Recovery, configuración de Site Recovery de hello para la máquina virtual de Hola se quita en la consola VMM de Hola y Hola réplica se eliminó.

    ![Configuración de los valores de protección](./media/site-recovery-vmm-to-vmm-classic/cloud-settings-replica.png)

Después de guardar los valores de hello un trabajo se crearán y se pueden supervisar en hello **trabajos** ficha. Todos los servidores de host de Hyper-V en hello nube de origen VMM se configurarán para la replicación. Se puede modificar la configuración de la nube en hello **configurar** ficha. Si desea que toomodify ubicación de destino de Hola o nube de destino debe quitar la configuración de nube de hello y, a continuación, volver a configurar en la nube Hola.

### <a name="prepare-for-offline-initial-replication"></a>Preparación para la replicación inicial sin conexión
Necesitará hello toodo después tooprepare de acciones para la replicación inicial sin conexión:

* En el servidor de origen de hello, especificará una ubicación de ruta de acceso de qué Hola llevará a cabo la exportación de datos. Asignar Control total para los permisos de recurso compartido y NTFS toohello servicio VMM en la ruta de acceso de exportación de Hola. En el servidor de destino de hello, especificará una ubicación de ruta de acceso desde la que importación datos de Hola se producirá. Asignar Hola mismos permisos en esta ruta de acceso de importación.
* Si hello importar o se comparte la ruta de acceso de exportación, asignar la pertenencia de grupo administrador, usuario avanzado, operador de impresión u operador de servidor para la cuenta de servicio VMM hello en el equipo remoto hello en qué Hola compartido se encuentra.
* Si usas los hosts de tooadd ejecutar como cuentas, en hello importar y exportar las rutas de acceso, asigne lectura y permisos de escritura toohello cuentas de ejecución en VMM.
* Hola importar y exportar recursos compartidos no se deben encontrar en cualquier equipo que se usa como un servidor de host de Hyper-V, porque la configuración de bucle invertido no es compatible con Hyper-V.
* En Active Directory, en cada servidor de host de Hyper-V que contiene máquinas virtuales que desea tooprotect, habilitar y configurar la delegación restringida tootrust Hola remota los equipos en qué Hola importación y exportación en las rutas de acceso se encuentran, como se indica a continuación:
  1. En el controlador de dominio de hello, abra **equipos y usuarios de Active Directory**.
  2. En el árbol de consola de hello, haga clic en **DomainName** > **equipos**.
  3. Nombre del servidor de host de Hyper-V de Hola de contextual > **propiedades**.
  4. En hello **delegación** ficha, haga clic en T**óxido este equipo para servicios solo de delegación toospecified**.
  5. Haga clic en **Usar cualquier protocolo de autenticación**.
  6. Haga clic en **Agregar** > **Usuarios y equipos**.
  7. Nombre del tipo hello del equipo de Hola que hospeda la ruta de acceso de exportación de hello > **Aceptar**. En la lista hello de servicios disponibles, mantenga presionada la tecla CTRL de Hola y haga clic en **cifs** > **Aceptar**. Repita para nombre de hello del equipo de hello esa ruta de acceso de importación de Hola de hosts. Repita según sea necesario para servidores host de Hyper-V adicionales.

## <a name="step-5-configure-network-mapping"></a>Paso 5: Configuración de la asignación de red
1. En la página de inicio rápido de hello, haga clic en **asignar redes**.
2. Seleccionar servidor VMM de origen Hola desde el que desee toomap redes y, a continuación, Hola saludos de toowhich del servidor VMM de destino se asignarán las redes. se muestra la lista de Hola de redes de origen y sus redes de destino asociadas. En el caso de las redes no asignadas, aparece un valor en blanco.
3. Seleccione una red en **Red en origen** > **Asignar**. Hola servicio detecta las redes de VM de hello en el servidor de destino de Hola y las muestra. Haga clic en hello información icono siguiente toohello origen y destino nombres tooview Hola subredes de red para cada red.

    ![Configurar asignación de red](./media/site-recovery-vmm-to-vmm-classic/network-mapping1.png)
4. En el cuadro de diálogo de hello seleccionarlos Hola redes de VM del servidor VMM de destino de Hola.

    ![Selección de una red de destino](./media/site-recovery-vmm-to-vmm-classic/network-mapping2.png)
5. Al seleccionar una red de destino, hello nubes protegidas que usan la red de origen Hola se muestran. También se muestran las redes de destino disponibles que están asociadas con nubes de hello usadas para la protección. Se recomienda que seleccione una red de destino que esté disponible tooall nubes de Hola que se usa para la protección. O bien, también puede ir toohello servidor VMM y modificar Hola nube propiedades tooadd Hola red lógica correspondiente toohello red de vm que desea toochoose.
6. Haga clic en el proceso de asignación de hello marca de verificación toocomplete Hola. Progreso de asignación de hello tootrack inicia un trabajo. Puede verlo en hello **trabajos** ficha.

## <a name="step-6-configure-storage-mapping"></a>Paso 6: Configuración de la asignación de almacenamiento
De forma predeterminada cuando se replica una máquina virtual en un origen Hyper-V host servidor tooa Hyper-V host servidor de destino, los datos replicados se almacenan en la ubicación predeterminada de hello indicada para el host de Hyper-V de destino de hello en el Administrador de Hyper-V. Para obtener más control sobre dónde se almacenan los datos replicados, puede configurar la asignación de almacenamiento de la manera siguiente:

1. Defina las clasificaciones de almacenamiento en ambos origen hello y servidores VMM de destino. [Más información](https://technet.microsoft.com/library/gg610685.aspx). Las clasificaciones deben estar disponibles toohello servidores de host de Hyper-V en nubes de origen y destino. Las clasificaciones no necesitan toohave Hola el mismo tipo de almacenamiento. Por ejemplo puede asignar una clasificación de origen que contiene la clasificación de destino de tooa de recursos compartidos SMB que contiene CSV.
2. Cuando estén definidas las clasificaciones, podrá crear las asignaciones. toodo esto en hello **inicio rápido** página > **asignar almacenamiento**.
3. Haga clic en hello **almacenamiento** ficha > **asignar clasificaciones de almacenamiento**.
4. En hello **asignar clasificaciones de almacenamiento** ficha, seleccione las clasificaciones en el origen de Hola y servidores VMM de destino. Guarde la configuración.

    ![Selección de una red de destino](./media/site-recovery-vmm-to-vmm-classic/storage-mapping.png)

## <a name="step-7-enable-virtual-machine-protection"></a>Paso 7: Habilitación de la protección de máquinas virtuales
Después de servidores, las nubes y las redes están configuradas correctamente, puede habilitar la protección de máquinas virtuales en la nube de Hola.

1. En hello **máquinas virtuales** , haga clic en la nube de hello en qué Hola se encuentra la máquina virtual **habilitar la protección** > **agregar máquinas virtuales**.
2. En lista de Hola de máquinas virtuales en la nube de hello, seleccione Hola uno desea tooprotect.

    ![Habilitar protección de máquina virtual](./media/site-recovery-vmm-to-vmm-classic/enable-protection.png)
3. Realizar seguimiento del progreso de la acción Habilitar protección en Hola Hola **trabajos** ficha, incluida la replicación inicial de Hola. Después del trabajo de finalización de la protección de hello ejecuciones Hola virtual machine está preparado para conmutación por error. Después de habilitar la protección y máquinas virtuales se replican, podrá tooview capaz de ellas en Azure.

    ![Virtual machine protection job](./media/site-recovery-vmm-to-vmm-classic/vm-jobs.png)

> [!NOTE]
> También puede habilitar la protección de máquinas virtuales en la consola VMM Hola. Haga clic en **Habilitar protección** en la barra de herramientas de Hola Hola **Azure Site Recovery** ficha de propiedades de la máquina virtual de Hola.
>
>

### <a name="on-board-existing-virtual-machines"></a>Incorporación de máquinas virtuales existentes
Si tiene máquinas virtuales existentes en VMM que va a replicar con la réplica de Hyper-V, necesitará tooonboard para protección de Azure Site Recovery como sigue:

1. Compruebe que dispone de nubes principales y secundarias. Asegúrese de que servidor hello Hyper-V que hospeda la máquina virtual existente de Hola se encuentra en la nube principal hello y ese servidor de Hyper-V de hello hospeda la máquina virtual de réplica de Hola se encuentra en la nube secundaria Hola. Asegúrese de que configure los ajustes de protección para nubes de Hola. configuración de Hello debe coincidir con la configuración actual de réplica de Hyper-V. En caso contrario, es posible que la replicación de las máquinas virtuales no funcione según lo esperado.
2. A continuación, habilite la protección de máquina virtual principal de Hola. Azure Site Recovery y VMM garantizará que hello mismo host de réplica y la máquina virtual se detecta y Azure Site Recovery reutilizará y restablecerá la replicación mediante valores de hello configurados durante la configuración de la nube.

## <a name="test-your-deployment"></a>Prueba de la implementación
plan de la implementación, puede ejecutar una prueba de conmutación por error para una sola máquina virtual, o crear un plan de recuperación que consta de varias máquinas virtuales y ejecutar una prueba de conmutación por error para hello tootest.  La conmutación por error de prueba simula su mecanismo de conmutación por error y recuperación en una red aislada.

### <a name="create-a-recovery-plan"></a>Creación de un plan de recuperación
1. En hello **planes de recuperación** , haga clic en **crear un Plan de recuperación**.
2. Especifique un nombre para el plan de recuperación de Hola y servidores VMM de origen y de destino. servidor de origen de Hello debe tener máquinas virtuales que están habilitadas para conmutación por error y recuperación. Seleccione **Hyper-V** tooview solo las nubes que están configuradas para la replicación de Hyper-V.

    ![Creación de un plan de recuperación](./media/site-recovery-vmm-to-vmm-classic/recovery-plan1.png)
3. En **Seleccionar máquina virtual**, seleccione grupos de replicación. Todas las máquinas virtuales asociadas al grupo de replicación de Hola se seleccionarán y agrega el plan de recuperación de toohello. Estas máquinas virtuales se agregan toohello grupo de manera predeterminada de plan de recuperación: grupo 1. Puede agregar más grupos si es necesario. Tenga en cuenta que después de máquinas virtuales de replicación se iniciarán según el orden de Hola de grupos de planes de recuperación de Hola.

    ![Agregar máquinas virtuales](./media/site-recovery-vmm-to-vmm-classic/recovery-plan2.png)

Una vez creado un plan de recuperación, aparece en la lista de hello en hello **planes de recuperación** ficha.

### <a name="run-a-test-failover"></a>Ejecución de una conmutación por error de prueba
1. En hello **planes de recuperación** ficha, seleccione el plan de Hola y haga clic en **conmutación por error de prueba**.
2. En hello **confirmar la conmutación por error** página, seleccione **ninguno**. Tenga en cuenta que con esta opción habilitada Hola conmutado por error máquinas virtuales de réplica no sea red tooany conectado. Esto probará que Hola se produce un error de máquina virtual más según lo previsto, pero no prueba el entorno de red de replicación. Veamos cómo demasiado[ejecutar una prueba de conmutación por error](site-recovery-failover.md) para obtener más información acerca de cómo toouse las opciones de red diferentes.
3. máquina virtual de prueba de Hola se creará en el mismo host como host de hello en qué Hola existe la máquina virtual de réplica de Hola. Se agrega toohello mismo en la nube en qué Hola se encuentra la máquina virtual de réplica.

### <a name="run-a-recovery-plan"></a>Ejecución de un plan de recuperación
Después de replicación Hola máquina virtual no tenga una dirección IP que es hello igual que la dirección IP de Hola de Hola máquina virtual principal. Máquinas virtuales se actualizará el servidor DNS de Hola que están utilizando después de que se inicien. También puede agregar un tooensure de servidor DNS de secuencia de comandos tooupdate Hola oportuna actualización.

#### <a name="script-tooretrieve-hello-ip-address"></a>Dirección IP de secuencia de comandos tooretrieve Hola
Ejecute esta dirección IP de ejemplo script tooretrieve Hola.

        $vm = Get-SCVirtualMachine -Name <VM_NAME>
        $na = $vm[0].VirtualNetworkAdapters>
        $ip = Get-SCIPAddress -GrantToObjectID $na[0].id
        $ip.address  

#### <a name="script-tooupdate-dns"></a>Secuencia de comandos tooupdate DNS
Ejecute este tooupdate de secuencia de comandos de ejemplo DNS, especificar la dirección IP de Hola recuperada mediante el script de ejemplo de Hola anterior.

        string]$Zone,
        [string]$name,
        [string]$IP
        )
        $Record = Get-DnsServerResourceRecord -ZoneName $zone -Name $name
        $newrecord = $record.clone()
        $newrecord.RecordData[0].IPv4Address  =  $IP
        Set-DnsServerResourceRecord -zonename $zone -OldInputObject $record -NewInputObject $Newrecord



## <a name="privacy-information-for-site-recovery"></a>Información de privacidad para Site Recovery
Esta sección proporciona información adicional de privacidad para hello service de Microsoft Azure Site Recovery ("servicio"). declaración de privacidad de hello tooview para servicios de Microsoft Azure, consulte la [declaración de privacidad de Microsoft Azure](http://go.microsoft.com/fwlink/?LinkId=324899)

**Característica: Registro**

* **Qué hace**: registra el servidor en el servicio para que las máquinas virtuales se puedan proteger.
* **Información recopilada**: después de registrar Hola servicio recopila, procesa y transmite la información de certificado de administración de servidor VMM de Hola que ha designado la recuperación ante desastres de tooprovide con nombre de servicio de Hola Hola del servidor de VMM, y el nombre de Hola de nubes de máquinas virtuales en el servidor VMM.
* **Uso de la información**:

  * Certificado de administración, se utiliza toohelp identificar y autenticar el servidor VMM Hola registrado para acceso toohello servicio. Hola servicio utiliza la parte de clave pública de Hola de hello certificado toosecure registrado de un token que Hola solo servidor VMM puede obtener acceso a. servidor de Hello debe toouse esta características del servicio de token toogain acceso toohello.
  * Nombre del servidor VMM Hola: nombre del servidor VMM hello es necesario tooidentify y comunicarse con el servidor VMM adecuado hello en qué Hola se ubican las nubes.
  * Nombres de nube del servidor VMM Hola: nombre de nube de hello es obligatorio cuando se usa en la nube Hola servicio emparejamiento o desemparejamiento característica se describe a continuación. Cuando decida toopair la nube de un centro de datos principal con otra nube en el centro de datos de recuperación de hello, se muestran los nombres de Hola de todas las nubes de Hola desde el centro de datos de recuperación de Hola.
* **Opción**: esta información es una parte fundamental del proceso del servicio de registro de hello porque le ayuda a y Hola servicio tooidentify Hola VMM servidor para que desee tooprovide protección de Azure Site Recovery, así como tooidentify Hola servidor VMM registrado correcto. Si no desea toosend este servicio de información toohello, no utilice este servicio. Si registra el servidor y, a continuación, más adelante, desea toounregister, puede hacerlo mediante la eliminación de información del servidor VMM Hola Hola portal de servicio (que es Hola portal de Azure).

**Característica: Habilitación de la protección de Azure Site Recovery**

* **Lo que hace**: Hola proveedor de Azure Site Recovery instalado en el servidor VMM hello es el conducto de Hola para comunicarse con hello servicio. Hola proveedor es una biblioteca de vínculos dinámicos (DLL) hospedada en proceso VMM Hola. Después de hello que proveedor está instalado, la característica de "Recuperación de centro de datos" Hola obtiene habilitada en la consola de administrador VMM de Hola. Cualquier máquina virtual nueva o existente en una nube puede habilitar una propiedad denominada "Recuperación de centro de datos" toohelp proteger la máquina virtual de Hola. Una vez que se establece esta propiedad, Hola proveedor envía Hola nombre e identificador de la máquina virtual de hello toohello servicio. habilita la protección virtual de Hello mediante la tecnología de replicación de Windows Server 2012 o Windows Server 2012 R2 Hyper-V. datos de máquina virtual de Hola se replicarán desde una tooanother de host de Hyper-V (que normalmente se encuentra en un centro de datos de "recuperación" diferente).
* **Información recopilada**: Hola servicio recopila, procesa y transmite los metadatos de la máquina virtual de hello, que incluye nombre hello, Id., red virtual y nombre de Hola de nube de Hola a la que pertenece.
* **Uso de la información**: Hola servicio usa Hola por encima de la información de la máquina virtual de información toopopulate hello en el portal de servicio.
* **Opción**: Esto es una parte esencial del servicio de hello y no se puede desactivar. Si no desea que esta información se envíe toohello servicio, no habilite la protección de Azure Site Recovery para las máquinas virtuales. Tenga en cuenta que todos los datos enviados por el proveedor de hello toohello servicio se envían a través de HTTPS.

**Característica: Plan de recuperación**

* **Lo que hace**: esta característica ayuda a toobuild un plan de orquestación Hola "recuperación" Centro de datos. Puede definir el orden de hello en qué Hola se debe iniciar las máquinas virtuales o un grupo de máquinas virtuales en el sitio de recuperación de Hola. También puede especificar cualquier toobe scripts automatizados que se ejecute, o cualquier toobe acción manual realizada en Hola de recuperación para cada máquina virtual. Conmutación por error (que se describe en la sección siguiente Hola) se desencadena normalmente en hello nivel Plan de recuperación para la recuperación coordinada.
* **Información recopilada**: Hola servicio recopila, procesa y transmite los metadatos de plan de recuperación de hello, incluidos los metadatos de la máquina virtual y los metadatos de todos los scripts de automatización y las notas de la acción manual.
* **Uso de la información**: metadatos Hola se ha descrito anteriormente están el plan de recuperación de hello toobuild usado en el portal de servicio.
* **Opción**: Esto es una parte esencial del servicio de hello y no se puede desactivar. Si no desea que esta información se envíe toohello servicio, no se compilan planes de recuperación en este servicio.

**Característica: Asignación de red**

* **Lo que hace**: esta característica permite toomap información de red del centro de datos de recuperación de toohello centro de datos principal de Hola. Cuando se recuperan hello las máquinas virtuales en el sitio de recuperación de hello, esta asignación permite establecer la conectividad de red para ellos.
* **Información recopilada**: como parte de la característica de asignación de red de hello, Hola servicio recopila, procesa y transmite los metadatos de Hola de redes lógicas de Hola para cada sitio (principal y centro de datos).
* **Uso de la información**: Hola servicio usa Hola metadatos toopopulate el portal de servicio donde puede asignar la información de red de Hola.
* **Opción**: Esto es una parte esencial del servicio de hello y no se puede desactivar. Si no desea que esta información se envíe toohello servicio, no use la característica de asignación de red de Hola.

**Característica :Conmutación por error - Planeada, no planeada, prueba**

* **Lo que hace**: esta característica ayuda a la conmutación por error de una máquina virtual desde un centro de datos administrados de VMM de tooanother de centro de datos administrados por VMM. acción de conmutación por error de Hola se desencadena por el usuario de hello en el portal de servicio. Las posibles razones para una conmutación por error incluyen un evento no planeado (por ejemplo en el caso de hello de un disaster0 natural; un evento planificado (por ejemplo Centro de datos de equilibrio de carga); una conmutación por error de prueba (por ejemplo un ensayo de plan de recuperación).

Hola proveedor en el servidor VMM Hola recibe notificaciones de evento de Hola de hello servicio y ejecuta una acción de conmutación por error en el host de Hyper-V de Hola a través de interfaces VMM. Conmutación por error real de la máquina virtual de Hola desde una tooanother de host de Hyper-V (normalmente ejecutándose en un centro de datos de diferentes "recuperación") se controla mediante la tecnología de replicación de Windows Server 2012 o Windows Server 2012 R2 Hyper-V de Hola. Una vez completada la conmutación por error de hello, Hola proveedor instalado en el servidor VMM Hola Hola "recuperación" del centro de datos envía Hola correcto información toohello servicio.

* **Información recopilada**: Hola servicio usa Hola por encima del estado de hello toopopulate de información de la información de acción de conmutación por error de hello en el portal de servicio.
* **Uso de la información**: Hola servicio use Hola sobre la información de la manera siguiente:

  * Certificado de administración, se utiliza toohelp identificar y autenticar el servidor VMM Hola registrado para acceso toohello servicio. Hola servicio utiliza la parte de clave pública de Hola de hello certificado toosecure registrado de un token que Hola solo servidor VMM puede obtener acceso a. servidor de Hello debe toouse esta características del servicio de token toogain acceso toohello.
  * Nombre del servidor VMM Hola: nombre del servidor VMM hello es necesario tooidentify y comunicarse con el servidor VMM adecuado hello en qué Hola se ubican las nubes.
  * Nombres de nube del servidor VMM Hola: nombre de nube de hello es obligatorio cuando se usa en la nube Hola servicio emparejamiento o desemparejamiento característica se describe a continuación. Cuando decida toopair la nube de un centro de datos principal con otra nube en el centro de datos de recuperación de hello, se muestran los nombres de Hola de todas las nubes de Hola desde el centro de datos de recuperación de Hola.
* **Opción**: Esto es una parte esencial del servicio de hello y no se puede desactivar. Si no desea que esta información se envíe toohello servicio, no utilice este servicio.

## <a name="next-steps"></a>Pasos siguientes
Una vez ejecutado un toocheck de conmutación por error de prueba de su entorno está funcionando según lo esperado, [conocer](site-recovery-failover.md) diferentes tipos de conmutaciones por error.
