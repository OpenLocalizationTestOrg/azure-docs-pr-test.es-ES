---
title: "aaaReplicate tooAzure de máquinas virtuales de Hyper-V en el portal clásico de hello | Documentos de Microsoft"
description: "Este artículo describe cómo tooreplicate virtual de Hyper-V máquinas tooAzure cuando los equipos no están administrados en nubes de VMM."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 3f4c4483-e3dd-495a-bd02-c16e9e28c88d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 02/21/2017
ms.author: raynew
ms.openlocfilehash: 12d08d950a79e956436cb03ffc87ab40e86c589e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-between-on-premises-hyper-v-virtual-machines-and-azure-without-vmm-with-azure-site-recovery"></a>Replicación entre máquinas virtuales de Hyper-V local y Azure (sin VMM) con Azure Site Recovery
> [!div class="op_single_selector"]
> * [Portal de Azure](site-recovery-hyper-v-site-to-azure.md)
> * [PowerShell: administrador de recursos](site-recovery-deploy-with-powershell-resource-manager.md)
> * [Portal clásico](site-recovery-hyper-v-site-to-azure-classic.md)
>
>

Este artículo describe cómo tooreplicate local tooAzure de máquinas virtuales de Hyper-V, con hello [Azure Site Recovery](site-recovery-overview.md) servicio Hola portal de Azure. En este escenario, los servidores Hyper-V no se administran en nubes VMM.

Después de leer este artículo, registrar los comentarios en la parte inferior de Hola o hacer preguntas técnicas en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="site-recovery-in-hello-azure-portal"></a>Site Recovery en hello portal de Azure

Azure tiene dos [modelos de implementación](../resource-manager-deployment-model.md) diferentes para crear recursos y trabajar con ellos: el de Azure Resource Manager y el clásico. Azure también tiene dos portales: Hola portal de Azure clásico y Hola portal de Azure.

Este artículo se describe cómo toodeploy en portal clásico de Hola. portal clásico de Hello puede ser almacenes existentes toomaintain usado. No se puede crear almacenes nuevos mediante el portal clásico de Hola.

## <a name="site-recovery-in-your-business"></a>Site Recovery en su empresa

Las organizaciones necesitan una estrategia BCDR que determina cómo las aplicaciones y los datos permanecen disponibles y ejecutarse durante el tiempo de inactividad planeado y no planeado y recuperación las condiciones de trabajo de toonormal tan pronto como sea posible. Esto es lo que Site Recovery puede hacer:

* Protección remota para aplicaciones empresariales que se ejecutan en máquinas virtuales de Hyper-V.
* Una tooset única ubicación, administrar y supervisar la replicación, la conmutación por error y la recuperación.
* TooAzure de conmutación por error simple y conmutación por recuperación (restore) de los servidores de host de Azure tooHyper-V en su sitio local.
* Planes de recuperación que incluyen varias máquinas virtuales de modo que las cargas de trabajo de la aplicación en capas experimenten la conmutación por error al mismo tiempo.

## <a name="azure-prerequisites"></a>Requisitos previos de Azure
* Necesita una cuenta de [Microsoft Azure](https://azure.microsoft.com/) . Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Necesita un toostore replicado de datos de la cuenta de almacenamiento de Azure. cuenta de Hello tiene habilitada la replicación geográfica. Debe quedar en Hola misma región que el almacén de Azure Site Recovery de Hola y asociarse Hola misma suscripción. [Más información sobre Almacenamiento de Azure](../storage/common/storage-introduction.md). Tenga en cuenta que no se admiten mover las cuentas de almacenamiento creadas mediante hello [nuevo portal de Azure](../storage/common/storage-create-storage-account.md) en grupos de recursos.
* Necesitará una red virtual para que máquinas virtuales de Azure estará conectado tooa red cuando conmuta por error desde el sitio primario.

## <a name="hyper-v-prerequisites"></a>Requisitos previos de Hyper-V
* En el sitio local de hello origen necesitará uno o varios servidores que ejecutan **Windows Server 2012 R2** con instalado el rol de Hyper-V de Hola o **Microsoft Hyper-V Server 2012 R2**. Este servidor debe:
* Contener una o más máquinas virtuales.
* Ser toohello conectado Internet, ya sea directamente o a través de un servidor proxy.
* Ejecutar correcciones Hola descritos en KB [2961977](https://support.microsoft.com/en-us/kb/2961977 "KB2961977").

## <a name="virtual-machine-prerequisites"></a>Requisitos previos de las máquinas virtuales
Deben cumplir con las máquinas virtuales que desea tooprotect [requisitos de la máquina virtual de Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

## <a name="provider-and-agent-prerequisites"></a>Requisitos previos del proveedor y del agente
Como parte de la implementación de Azure Site Recovery podrá instalar Hola proveedor de Azure Site Recovery y hello Azure Backup Agent en cada servidor de Hyper-V. Observe lo siguiente:

* Le recomendamos que siempre se ejecutan agente y versiones más recientes de Hola de hello proveedor. Están disponibles en el portal de Site Recovery Hola.
* Debe ha Hola a todos los servidores de Hyper-V en un almacén de versiones de hello proveedor mismo y el agente.
* Proveedor que se ejecuta en el servidor de Hola Hola conecta tooSite recuperación sobre Hola internet. Puede hacerlo sin un proxy, con la configuración de proxy de hello configurada actualmente en el servidor de Hyper-V de hello, o con la configuración de proxy personalizada que se configura durante la instalación del proveedor. Necesitará toomake seguro de ese servidor de proxy de hello desea toouse puede tener acceso a estas direcciones URL de Hola para conectar tooAzure:

  * *.accesscontrol.windows.net
  * *.backup.windowsazure.com
  * *.hypervrecoverymanager.windowsazure.com
  * *.store.core.windows.net      
  * *.blob.core.windows.net
  - https://www.msftncsi.com/ncsi.txt
  - time.windows.com
  - time.nist.gov
* Asimismo permitir direcciones IP de Hola se describe en [intervalos de IP del centro de datos de Azure](https://www.microsoft.com/download/details.aspx?id=41653) y el protocolo HTTPS (443). Tener intervalos IP de hello tooallow de hello región de Azure que piensa toouse y del oeste de Estados Unidos.

Este gráfico muestra los canales de comunicación diferentes de Hola y puertos utilizados por Site Recovery para la orquestación y la replicación

![Topología B2A](./media/site-recovery-hyper-v-site-to-azure-classic/b2a-topology.png)

## <a name="step-1-create-a-vault"></a>Paso 1: Creación de un almacén
1. Inicie sesión en toohello [Portal de administración](https://portal.azure.com).
2. Expanda **Data Services** > **Recovery Services** y haga clic en **Almacén de Site Recovery**.
3. Haga clic en **Crear nuevo	** > **Creación rápida**.
4. En **nombre**, escriba en el almacén de hello tooidentify un nombre descriptivo.
5. En **región**, seleccione Hola región geográfica para el almacén de Hola. toocheck admite regiones, consulte disponibilidad geográfica en [detalles de precios de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Haga clic en **Crear almacén**.

    ![Almacén nuevo](./media/site-recovery-hyper-v-site-to-azure-classic/vault.png)

Compruebe tooconfirm de barra de estado de Hola que Hola almacén se creó correctamente. almacén de Hola se mostrarán como **Active** en la página principal de servicios de recuperación de Hola.

## <a name="step-2-create-a-hyper-v-site"></a>Paso 2: Creación de un sitio de Hyper-V
1. En la página de servicios de recuperación de hello, haga clic en página de inicio rápido de hello almacén tooopen Hola. Inicio rápido también se puede abrir en cualquier momento mediante el icono de Hola.

    ![Inicio rápido](./media/site-recovery-hyper-v-site-to-azure-classic/quick-start-icon.png)
2. En la lista desplegable de hello, seleccione **entre un sitio de Hyper-V local y Azure**.

    ![Escenario de sitio de Hyper-V](./media/site-recovery-hyper-v-site-to-azure-classic/select-scenario.png)
3. En **Crear un sitio Hyper-V** haga clic en **Crear un sitio Hyper-V**. Especifique un nombre de sitio y guarde.

    ![Sitio de Hyper-V](./media/site-recovery-hyper-v-site-to-azure-classic/create-site.png)

## <a name="step-3-install-hello-provider-and-agent"></a>Paso 3: Instalar hello proveedor y agente
Instalar Hola proveedor y el agente en cada servidor de Hyper-V que tienen máquinas virtuales que desee tooprotect.

Si va a instalar en un clúster de Hyper-V, realiza los pasos 5-11 en cada nodo de clúster de conmutación por error de Hola. Después de que se registran todos los nodos y está habilitada la protección, máquinas virtuales estarán protegidas incluso si migra en nodos de clúster de Hola.

1. En **Preparar servidores Hyper-V**, haga clic en **Descargar una clave de registro**.
2. En hello **Descargar clave de registro** página, haga clic en **descargar** siguiente sitio toohello. Hola tooa clave ubicación segura que se puede acceder fácilmente por servidor hello Hyper-V de descarga. clave de Hello es válida durante 5 días después de generarlo.

    ![Clave de registro](./media/site-recovery-hyper-v-site-to-azure-classic/download-key.png)
3. Haga clic en **descarga Hola proveedor** versión más reciente de tooobtain Hola.
4. Ejecute el archivo hello en cada servidor de Hyper-V que desee tooregister en el almacén de Hola. archivo Hello instala dos componentes:
   * **Proveedor de Azure Site Recovery**: controla la comunicación y orquestación entre servidor hello Hyper-V y el portal de Azure Site Recovery Hola.
   * **Agente de servicios de recuperación de Azure**: controla el transporte de datos entre máquinas virtuales se ejecutan en el servidor de Hyper-V de origen de Hola y el almacenamiento de Azure.
5. En **Microsoft Update** puede optar por recibir actualizaciones. Con esta opción habilitada, se instalará las actualizaciones del proveedor y el agente según la directiva de Microsoft Update tooyour.

    ![Microsoft Updates](./media/site-recovery-hyper-v-site-to-azure-classic/provider1.png)
6. En **instalación** especificar donde desea tooinstall Hola proveedor y agente de servidor Hyper-V de Hola.

    ![Ubicación de instalación](./media/site-recovery-hyper-v-site-to-azure-classic/provider2.png)
7. Una vez completada la instalación continúe tooregister configuración del servidor de hello en el almacén de Hola.
8. En hello **configuración del almacén** página, haga clic en **examinar** archivo de clave tooselect Hola. Especifique la suscripción de Azure Site Recovery Hola, nombre del almacén de hello, y pertenece Hola Hyper-V sitio toowhich Hola Hyper-V server.

    ![Registro de servidor](./media/site-recovery-hyper-v-site-to-azure-classic/provider8.PNG)
9. En hello **conexión a Internet** página especificar cómo Hola proveedor conecta tooAzure Site Recovery. Seleccione **usar configuración de proxy del sistema predeterminada** configuración de la conexión de Internet de toouse Hola predeterminado configurado en el servidor de Hola. Si no se especifica un valor Hola de forma predeterminada se usa la configuración.

   ![Configuración de Internet](./media/site-recovery-hyper-v-site-to-azure-classic/provider7.PNG)
10. Registro inicia el servidor de Hola de tooregister en el almacén de Hola.

    ![Registro de servidor](./media/site-recovery-hyper-v-site-to-azure-classic/provider15.PNG)
11. Después de que finalice el registro metadatos de hello Hyper-V server se recupera por Azure Site Recovery y servidor Hola se muestra en hello **sitios de Hyper-V** ficha en hello **servidores** página en el almacén de Hola.

### <a name="install-hello-provider-from-hello-command-line"></a>Instalar Hola proveedor desde la línea de comandos de Hola
Como alternativa puede instalar hello Azure Site Recovery Provider desde línea de comandos de Hola. Debe usar este método si desea que tooinstall Hola proveedor en un equipo que ejecuta Windows Server Core 2012 R2. Ejecutar desde la línea de comandos de hello, como se indica a continuación:

1. Hola proveedor carpeta de instalación de archivos y registro tooa clave de descarga. Por ejemplo, C:\ASR.
2. Ejecute un símbolo del sistema como administrador y escriba:

        C:\Windows\System32> CD C:\ASR
        C:\ASR> AzureSiteRecoveryProvider.exe /x:. /q
3. A continuación, instale Hola proveedor con:

        C:\ASR> setupdr.exe /i
4. Ejecute hello tras el registro de toocomplete:

        CD C:\Program Files\Microsoft Azure Site Recovery Provider
        C:\Program Files\Microsoft Azure Site Recovery Provider\> DRConfigurator.exe /r  /Friendlyname <friendly name of hello server> /Credentials <path of hello credentials file> /EncryptionEnabled <full file name toosave hello encryption certificate>         

Los parámetros son:

* **/ Credenciales de**: especificar ubicación de Hola Hola clave de registro descargado.
* **/ FriendlyName**: especificar un servidor de host de Hyper-V de Hola de nombre tooidentify. Este nombre aparecerá en el portal de Hola
* **/EncryptionEnabled**: opcional. Especifique si desea tooencrypt máquinas de virtuales de réplica en Azure (en el cifrado de rest).
* **/proxyAddress**; **/proxyport**; **/proxyUsername**; **/proxyPassword**: opcional. Especifique los parámetros de proxy si desea que toouse un proxy personalizado o el proxy existente requiere autenticación.

## <a name="step-4-create-an-azure-storage-account"></a>Paso 4: Creación de una cuenta de almacenamiento de Azure
* En **preparar recursos** seleccione **crear cuenta de almacenamiento** toocreate una cuenta de almacenamiento de Azure si no tiene uno. cuenta de Hello debe tener habilitada la replicación geográfica. Debe quedar en Hola misma región que el almacén de Azure Site Recovery de Hola y asociarse Hola misma suscripción.

    ![Crear cuenta de almacenamiento](./media/site-recovery-hyper-v-site-to-azure-classic/create-resources.png)

> [!NOTE]
> 1. No se admite mover Hola de cuentas de almacenamiento creados mediante hello [nuevo portal de Azure](../storage/common/storage-create-storage-account.md) en grupos de recursos.
> 2. [Migración de cuentas de almacenamiento](../azure-resource-manager/resource-group-move-resources.md) a través de recursos grupos dentro Hola misma suscripción o en las suscripciones no se admite para las cuentas de almacenamiento utilizadas para la implementación de Site Recovery.
>

## <a name="step-5-create-and-configure-protection-groups"></a>Paso 5: Creación y configuración de grupos de protección
Grupos de protección son agrupaciones lógicas de máquinas virtuales que desea usar tooprotect Hola misma configuración de protección. Aplicar grupo de protección de tooa de configuración de protección, y esas configuraciones aplicadas tooall las máquinas virtuales que agregue toohello grupo.

1. En **Crear y configurar grupos de protección**, haga clic en **Crear un grupo de protección**. Si no están establecidos los requisitos previos, se emitirá un mensaje y podrá hacer clic en **Ver detalles** para obtener más información.
2. Hola **grupos de protección** ficha, agregar un grupo de protección. Especifique un nombre, el sitio de Hyper-V de origen de hello, el destino de hello **Azure**, el nombre de la suscripción de Azure Site Recovery y Hola cuenta de almacenamiento de Azure.

    ![Grupo de protección](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group.png)
3. En **configuración de replicación** conjunto hello **copiar frecuencia** toospecify con qué frecuencia se debe sincronizar datos delta de hello entre Hola origen y de destino. Puede establecer a too30 segundos, 5 minutos o 15 minutos.
4. En **Conservar puntos de recuperación** , especifique el número de horas del historial de recuperación que se deben almacenar.
5. En **frecuencia de las instantáneas coherentes con la aplicación** puede especificar si las instantáneas de tootake que usan tooensure de servicio de instantáneas de volumen (VSS) que las aplicaciones están en un estado coherente cuando se tomó la instantánea de Hola. De forma predeterminada, estas no se capturan. Asegúrese de que este valor se establece a que no requiere herramientas que número Hola de puntos de recuperación adicionales que configure. Esto solo se admite si la máquina virtual de hello está ejecutando un sistema operativo Windows.
6. En **hora de inicio de la replicación inicial** especifica cuándo se enviará a la replicación inicial de máquinas virtuales en el grupo de protección de hello tooAzure.

    ![Grupo de protección](./media/site-recovery-hyper-v-site-to-azure-classic/protection-group2.png)

## <a name="step-6-enable-virtual-machine-protection"></a>Paso 6: Habilitación de la protección de máquinas virtuales
Agregar máquinas virtuales tooa protección del tooenable de grupo de protección para ellos.

> [!NOTE]
> No se admite la protección de máquinas virtuales que ejecutan Linux con una dirección IP estática.
>
>

1. En hello **máquinas** ficha Hola grupo de protección, haga clic en ** Agregar máquinas virtuales tooprotection grupos tooenable protección **.
2. En hello **habilitar la protección de máquina Virtual** página Seleccione hello las máquinas virtuales que desee tooprotect.

    ![Habilitar protección de máquina virtual](./media/site-recovery-hyper-v-site-to-azure-classic/add-vm.png)

    trabajos de habilitar la protección de Hello comienza. Puede realizar el seguimiento del progreso en hello **trabajos** ficha. Después del trabajo de finalización de la protección de hello ejecuciones Hola virtual machine está preparado para conmutación por error.
3. Una vez configurada la protección, puede:

   * Ver máquinas virtuales en **elementos protegidos** > **grupos de protección** > *protectiongroup_name*  >  **Máquinas virtuales** puede explorar en profundidad los detalles de toomachine en hello **propiedades** ficha...
   * Configurar las propiedades de conmutación por error de Hola para una máquina virtual en **elementos protegidos** > **grupos de protección** > *protectiongroup_name*  >  **Máquinas virtuales** *virtual_machine_name* > **configurar**. Puede configurar:

     * **Nombre**: nombre de Hola de máquina virtual de hello en Azure.
     * **Tamaño**: Hola tamaño de destino de la máquina virtual de Hola que conmuta por error.

       ![Configuración de propiedades de la máquina virtual](./media/site-recovery-hyper-v-site-to-azure-classic/vm-properties.png)
   * Establecer la configuración de una máquina virtual adicional en *Elementos protegidos** > **Grupos de protección** > *nombre_grupoProtección* > **Máquinas virtuales** *nombre_máquina_virtual* > **Configurar**, lo que incluye lo siguiente:

     * **Adaptadores de red**: número de Hola de adaptadores de red es dictados por tamaño de Hola que especifique para la máquina virtual de destino de Hola. Comprobar [las especificaciones de tamaño de máquina virtual](../virtual-machines/linux/sizes.md) para el número de Hola de NIC compatibles con tamaño de máquina virtual de Hola.

       Cuando modifique tamaño Hola una máquina virtual y guardar la configuración de hello, cambiará el número de hello del adaptador de red cuando se abre **configurar** Hola página próxima vez. número de Hola de adaptadores de red de máquinas virtuales de destino es mínimo de número de Hola de adaptadores de red de máquina virtual de origen y número máximo de adaptadores de red admitido por el tamaño de Hola de máquina virtual de hello elegida. Se explica a continuación:

       * Si el número de Hola de adaptadores de red en la máquina de origen de hello es menor o igual toohello de adaptadores permitidas para el tamaño de máquina de destino de hello, a continuación, tendrá destino Hola Hola el mismo número de adaptadores como origen de Hola.
       * Si número Hola de adaptadores para la máquina virtual de origen de hello supera número Hola permitido para el tamaño de destino de hello después máximo de tamaño de destino de Hola se usará.
       * Por ejemplo, si una máquina de origen tiene dos adaptadores de red y tamaño de máquina de destino de hello es compatible con cuatro, el equipo de destino Hola tendrá dos adaptadores. Si la máquina de origen hello tiene dos adaptadores de pero hello tamaño de destino admitida solo admite un equipo de destino de Hola tendrá solo un adaptador.

     * **Red de Azure**: especificar deben conmutar las máquinas virtuales de hello red toowhich Hola. Si la máquina virtual de hello tiene varios adaptadores de red de todos los adaptadores deben toohello conectado misma red de Azure.
     * **Subred** para cada adaptador de red en la máquina virtual de hello, subred Hola select en la máquina de hello Azure red toowhich Hola debe conectarse después de la conmutación por error.
     * **Dirección IP de destino**: si el adaptador de red de Hola de máquina virtual de origen está configurado toouse estática de una dirección IP direcciones, a continuación, puede especificar la dirección IP de Hola para tooensure de máquina virtual de destino de Hola que Hola máquina tiene Hola misma dirección IP después de la conmutación por error .  Si no se especifica una dirección IP se asignará ninguna dirección disponible en tiempo de Hola de conmutación por error. Si especifica una dirección que está en uso, se producirá un error en la conmutación por error.

     > [!NOTE]
     > [Migración de redes](../azure-resource-manager/resource-group-move-resources.md) a través de recursos grupos dentro Hola misma suscripción o en las suscripciones no se admite para las redes usadas para la implementación de Site Recovery.
     >

     ![Configuración de propiedades de la máquina virtual](./media/site-recovery-hyper-v-site-to-azure-classic/multiple-nic.png)




## <a name="step-7-create-a-recovery-plan"></a>Paso 7: Creación de un plan de recuperación
En la implementación de orden tootest Hola puede ejecutar una prueba de conmutación por error para una sola máquina virtual o un plan de recuperación que contiene una o más máquinas virtuales. [Más](site-recovery-create-recovery-plans.md) acerca de la creación de un plan de recuperación.

## <a name="step-8-test-hello-deployment"></a>Paso 8: Probar la implementación de Hola
Hay dos toorun formas un tooAzure de conmutación por error de prueba.

* **Probar la conmutación por error sin una red de Azure**: este tipo de conmutación por error de prueba comprueba que la máquina virtual Hola aparece correctamente en Azure. máquina virtual de Hello no estará conectada tooany red de Azure después de la conmutación por error.
* **Probar la conmutación por error con una red de Azure**: este tipo de conmutación por error comprueba que Hola entorno de replicación total aparece como se esperaba y que se conmutaron hello las máquinas virtuales conecta toohello red Azure de destino especificado. Tenga en cuenta que para conmutación por error de prueba subred Hola de máquina virtual de prueba de Hola se decidirá basado en la subred de Hola Hola máquina virtual de réplica. Se trata de replicación diferentes tooregular cuando subred Hola de máquina virtual de réplica se basa en la subred de Hola de máquina virtual de origen de Hola.

Si desea toorun una conmutación por error de prueba sin especificar una red de Azure no es necesario tooprepare nada.

toorun una conmutación por error de prueba con un destino de red de Azure necesitará toocreate una nueva red de Azure que esté aislada de la red de producción de Azure (comportamiento predeterminado cuando se crea una nueva red de Azure). Para más detalles, lea [Ejecución de una conmutación por error de prueba](site-recovery-failover.md) .

toofully probar la implementación de la replicación y la red deberá tooset una infraestructura de Hola para que ese Hola replica toowork de máquina virtual como se espera. Una manera de hacer este tootooset una máquina virtual como un controlador de dominio con DNS y replicar tooAzure con toocreate de Site Recovery en la prueba de Hola de red mediante la ejecución de una prueba de conmutación por error.  [Más información sobre](site-recovery-active-directory.md#test-failover-considerations) consideraciones de la conmutación por error de prueba para Active Directory.

Ejecute la conmutación por error de prueba de hello como sigue:

> [!NOTE]
> tooget Hola obtener el mejor rendimiento cuando se realiza una conmutación por error tooAzure, asegúrese de que ha instalado Hola agente de Azure en la máquina de hello protegido. Esto contribuye a que el arranque se realice antes y también a realizar el diagnóstico en caso de problemas. Se puede encontrar el agente de Linux [aquí](https://github.com/Azure/WALinuxAgent) y el agente de Windows, [aquí](http://go.microsoft.com/fwlink/?LinkID=394789).
>
>

1. En hello **planes de recuperación** ficha, seleccione el plan de Hola y haga clic en **conmutación por error de prueba**.
2. En hello **confirmar la conmutación por error** página, seleccione **ninguno** o una red de Azure específica.  Tenga en cuenta que si selecciona **ninguno** conmutación por error de prueba de hello comprobará que la máquina virtual Hola replicado correctamente tooAzure pero no comprueba la configuración de red de replicación.

    ![Probar conmutación por error](./media/site-recovery-hyper-v-site-to-azure-classic/test-nonetwork.png)
3. En hello **trabajos** ficha que pueda seguir el progreso de la conmutación por error. También debe ser capaz de toosee réplica de prueba de máquina virtual de hello en Hola portal de Azure. Si está configurado tooaccess las máquinas virtuales de la red local puede iniciar una máquina virtual de escritorio remoto conexión toohello.
4. Cuando llegue a conmutación por error de Hola Hola **realice las pruebas oportunas** fase, haga clic en **prueba completada** toofinish la conmutación por error de prueba de Hola. Puede explorar en profundidad toohello **trabajo** ficha tooperform y el estado y el progreso de la conmutación por error de tootrack todas las acciones que se necesitan.
5. Después de la conmutación por error estará toosee capaz de réplica de prueba de máquina virtual de Hola Hola portal de Azure. Si está configurado tooaccess las máquinas virtuales de la red local puede iniciar una máquina virtual de escritorio remoto conexión toohello.

   1. Compruebe que las máquinas virtuales de Hola se inician correctamente.
   2. Si desea tooconnect toohello virtual machine en Azure mediante Escritorio remoto después de la conmutación por error de hello, habilite la conexión a Escritorio remoto en la máquina virtual de hello antes de ejecutar la conmutación por error de prueba de Hola. También necesitará un punto de conexión RDP en la máquina virtual de hello tooadd. Puede aprovechar una [runbook de automatización de Azure](site-recovery-runbook-automation.md) toodo que.
   3. Después de conmutación por error si usa una máquina de virtual toohello pública del tooconnect de dirección IP en Azure mediante Escritorio remoto, asegúrese de no hay ninguna directiva de dominio que le impedirían conectando la máquina virtual de tooa con una dirección pública.
6. Una vez finalizada la prueba de Hola Hola siguientes:

   * Haga clic en **conmutación por error de prueba de hello**. Limpiar Hola power tooautomatically de entorno de prueba desactivar y eliminar máquinas virtuales de prueba de Hola.
   * Haga clic en **notas** toorecord y guardar las observaciones asociadas con conmutación por error de prueba de Hola.
7. Cuando llegue a conmutación por error de Hola Hola **realice las pruebas oportunas** fase finalizar comprobación de hello como sigue:
   1. Ver la máquina virtual de réplica de hello en hello portal de Azure. Compruebe que la máquina virtual Hola se inicia correctamente.
   2. Si está configurado tooaccess las máquinas virtuales de la red local puede iniciar una máquina virtual de escritorio remoto conexión toohello.
   3. Haga clic en **prueba completa hello** toofinish lo.
   4. Haga clic en **notas** toorecord y guardar las observaciones asociadas con conmutación por error de prueba de Hola.
   5. Haga clic en **conmutación por error de prueba de hello**. Limpiar Hola power tooautomatically de entorno de prueba desactivar y eliminar la máquina virtual de prueba de Hola.

## <a name="next-steps"></a>Pasos siguientes
Después de que la implementación esté configurada y en ejecución, [obtenga más información](site-recovery-failover.md) acerca de la conmutación por error.
