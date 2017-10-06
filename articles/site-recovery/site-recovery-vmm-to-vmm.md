---
title: "máquinas virtuales de Hyper-V aaaReplicate tooa sitio secundario con Azure Site Recovery | Documentos de Microsoft"
description: "Describe cómo tooreplicate máquinas virtuales de Hyper-V en VMM nubes tooa secundaria VMM sitio usando Hola portal de Azure."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: b33a1922-aed6-4916-9209-0e257620fded
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: e79dbdeab74266e843e5146298dc5aadfe66b5df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site-using-hello-azure-portal"></a>Replicar máquinas virtuales de Hyper-V en VMM nubes tooa VMM sitio secundario mediante Hola portal de Azure
> [!div class="op_single_selector"]
> * [Portal de Azure](site-recovery-vmm-to-vmm.md)
> * [Portal clásico](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell: administrador de recursos](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

Este artículo describe cómo tooreplicate local máquinas virtuales de Hyper-V administrados en nubes de System Center Virtual Machine Manager (VMM), uso de sitio secundario de tooa [Azure Site Recovery](site-recovery-overview.md) Hola portal de Azure. Aprenda más sobre la [arquitectura de este escenario](site-recovery-components.md).

Después de leer este artículo, registrar cualquier comentario final hello, o en hello [foro de servicios de recuperación de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites"></a>Requisitos previos

**Requisito previo** | **Detalles**
--- | ---
**Las tablas de Azure** | Necesita una cuenta de [Microsoft Azure](http://azure.microsoft.com/) . Puede comenzar con una [evaluación gratuita](https://azure.microsoft.com/pricing/free-trial/). [Más información](https://azure.microsoft.com/pricing/details/site-recovery/) sobre los precios de Site Recovery.
**VMM local** | Se recomienda que tener dos servidores VMM, uno en el sitio primario de hello y otro en hello secundaria.<br/><br/> Puede replicar entre nubes en un único servidor VMM.<br/><br/> Servidores VMM se deben ejecutar al menos System Center 2012 SP1 con las últimas actualizaciones de Hola.<br/><br/> Los servidores VMM necesitan acceso a Internet.
**Nubes VMM** | Deben tener todos los servidores VMM en una o varias nubes y todas las nubes deben establecerse perfil de capacidad de Hyper-V de Hola. <br/><br/>Las nubes deben incluir uno o más grupos de hosts de VMM.<br/><br/> Si sólo tiene un servidor VMM, necesita al menos dos nubes, tooact como servidor principal y secundaria.
**Hyper-V** | Servidores de Hyper-V deben ejecutar al menos Windows Server 2012 con el rol de Hyper-V de Hola y Hola a las últimas actualizaciones instaladas.<br/><br/> Un servidor de Hyper-V debe contener una o varias máquinas virtuales.<br/><br/>  Servidores de host de Hyper-V deben estar en grupos host en nubes VMM principales y secundarias de Hola.<br/><br/> Si ejecuta Hyper-V en un clúster con Windows Server 2012 R2, instale la [actualización 2961977](https://support.microsoft.com/kb/2961977).<br/><br/> Si ejecuta Hyper-V en un clúster con Windows Server 2012, el agente de clúster no se crea automáticamente si tiene un clúster basado en una dirección IP estática. Configurar a un agente de clúster Hola manualmente. [Más información](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).<br/><br/> Los servidores de Hyper-V necesitan acceso a Internet.
**URLs** | Servidores VMM y hosts de Hyper-V deben ser capaz de tooreach estas direcciones URL:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]

## <a name="deployment-steps"></a>Pasos de implementación

Se debe hacer lo siguiente:

1. Compruebe los requisitos previos.
2. Preparar el servidor VMM de Hola y hosts de Hyper-V.
3. Cree un almacén de Recovery Services. Hola almacén contiene valores de configuración y organiza la replicación.
4. Especifique la configuración de origen, destino y replicación.
5. Implementar el servicio de movilidad de hello en máquinas virtuales que desee tooreplicate.
6. Prepare la replicación y habilítela para máquinas virtuales de Hyper-V.
7. Ejecutar un toomake de conmutación por error de prueba que todo funciona según lo previsto.

## <a name="prepare-vmm-servers-and-hyper-v-hosts"></a>Preparación de servidores VMM y hosts de Hyper-V

tooprepare para la implementación:

1. Asegúrese de que servidor VMM de Hola y hosts de Hyper-V cumplan con requisitos previos de Hola que se ha descrito anteriormente y pueden llegar a las direcciones URL de hello necesario.
2. Configure las redes VMM para poder configurar la [asignación de red](#network-mapping-overview).

    - Asegúrese de que las máquinas virtuales en el origen de hello servidor host Hyper-V están conectado tooa red de VM de VMM. Esta red debe ser tooa vinculado red lógica que está asociado a la nube de Hola.
    Compruebe que Hola secundaria en la nube que utiliza para la recuperación tiene configurada una red VM correspondiente. Dicha red de máquina virtual debe ser tooa vinculado red lógica que esté asociada con la nube secundaria Hola.

3. Preparar una [única implementación de servidor](#single-vmm-server-deployment), si desea que las máquinas virtuales de tooreplicate entre nubes en hello mismo servidor VMM.

## <a name="create-a-recovery-services-vault"></a>Creación de un almacén de Recovery Services
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. Haga clic en **Nuevo** > **Administración** > **Recovery Services**.
3. En **nombre**, especificar un almacén de hello tooidentify nombre descriptivo. Si tiene más de una suscripción, seleccione una de ellas.
4. [Cree un grupo de recursos](../azure-resource-manager/resource-group-template-deploy-portal.md)o seleccione uno existente. Especifique una región de Azure. Las máquinas están replicados toothis región. toocheck admite regiones, consulte disponibilidad geográfica en [detalles de precios de Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/)
5. Si desea que tooquickly acceso Hola almacén de hello panel, haga clic en **Pin toodashboard** > **crear almacén**.

    ![Almacén nuevo](./media/site-recovery-vmm-to-vmm/new-vault-settings.png)

nuevo almacén de Hello aparece en hello **panel**, en **todos los recursos**y en hello principal **servicios de recuperación de los almacenes de credenciales** hoja.


## <a name="choose-a-protection-goal"></a>Elección de un objetivo de protección

Seleccione en qué desea tooreplicate y donde quiera tooreplicate a.

2. Haga clic en **Site Recovery** > **Paso 1: Preparar la infraestructura** > **Objetivo de protección**.
3. Seleccione **toorecovery sitio**y seleccione **Sí, con Hyper-V**.
4. Seleccione **Sí** tooindicate utilizas hosts de Hyper-V de hello toomanage VMM.
5. Seleccione **Sí** si tiene un servidor VMM secundario. Si va a implementar la replicación entre nubes en un solo servidor VMM, haga clic en **No**. y, a continuación, haga clic en **Aceptar**.

    ![Elegir objetivos](./media/site-recovery-vmm-to-vmm/choose-goals.png)

## <a name="set-up-hello-source-environment"></a>Configurar el entorno de origen Hola

Instale hello Azure Site Recovery Provider en servidores VMM y detectar y registrar los servidores en el almacén de Hola.

1. Haga clic en **Paso 1: Preparar la infraestructura** > **Origen**.

    ![Configurar origen](./media/site-recovery-vmm-to-vmm/goals-source.png)
2. En **preparar origen**, haga clic en **+ VMM** tooadd un servidor VMM.

    ![Configurar origen](./media/site-recovery-vmm-to-vmm/set-source1.png)
3. En **Agregar servidor**, compruebe que **servidor de System Center VMM** aparece en **tipo de servidor** y ese servidor VMM Hola cumple hello [requisitos previos](#prerequisites).
4. Descargar archivo de instalación del proveedor de Azure Site Recovery de Hola.
5. Descargue la clave de registro de hello. Se le solicitará cuando ejecute el programa de instalación. clave de Hello es válida durante cinco días después de generarlo.

    ![Configurar origen](./media/site-recovery-vmm-to-vmm/set-source3.png)
6. Instale hello Azure Site Recovery Provider en servidor VMM de Hola. No es necesario tooexplicitly ninguna instalación adicional en los servidores de host de Hyper-V.


### <a name="install-hello-azure-site-recovery-provider"></a>Instalar hello Azure Site Recovery Provider

1. Ejecute el archivo de configuración de proveedor de hello en cada servidor VMM. Si VMM está implementado en un clúster, siguiente Hola Hola primera vez que instale:
    -  Instalar el proveedor de hello en un nodo activo y finalizar Hola instalación tooregister Hola servidor VMM en el almacén de Hola.
    - A continuación, instale Hola proveedor en hello otros nodos. Los nodos del clúster deben ejecutarse todos Hola misma versión de Hola proveedor.
2. El programa de instalación ejecuta algunas comprobaciones de requisitos previos y las solicitudes de servicio VMM de permiso toostop Hola. Hola servicio VMM se reiniciará automáticamente cuando finaliza el programa de instalación. Si instala en un clúster VMM, está el rol de clúster de hello toostop solicitadas.
3. En **Microsoft Update**, puede participar en toospecify que están instaladas las actualizaciones del proveedor con arreglo a la directiva de Microsoft Update.
4. En **instalación**, acepte o modifique la ubicación de instalación predeterminada de Hola y haga clic en **instalar**.

    ![Ubicación de instalación](./media/site-recovery-vmm-to-vmm/provider-location.png)
5. Una vez completada la instalación, haga clic en **registrar** tooregister servidor de hello en el almacén de Hola.

    ![Ubicación de instalación](./media/site-recovery-vmm-to-vmm/provider-register.png)
6. En **nombre del almacén**, compruebe el nombre de Hola de almacén de hello en qué Hola se registrará el servidor. Haga clic en *Siguiente*.

    ![Registro de servidor](./media/site-recovery-vmm-to-vmm-classic/vaultcred.PNG)
7. En **conexión a Internet**, especifique cómo se proveedor Hola que se ejecuta en el servidor VMM Hola conecta tooAzure.

    ![Configuración de Internet](./media/site-recovery-vmm-to-vmm-classic/proxydetails.PNG)

   - Puede especificar ese proveedor Hola debe conectarse directamente toohello internet, o a través de un servidor proxy.
   - Especifique la configuración de proxy si es necesario.
   - Si usa un proxy, una cuenta de ejecución de VMM (DRAProxyAccount) se crea automáticamente con hello especificada las credenciales del proxy. Configurar servidor proxy de Hola para que esta cuenta se pueda autenticar correctamente. Hello configuración de la cuenta de ejecución puede modificarse en la consola VMM hello > **configuración** > **seguridad** > **cuentas de ejecución**. Reinicie los cambios de tooupdate de servicio VMM Hola.
8. En **clave de registro**, seleccione clave de Hola que descargó desde Azure Site Recovery y copió toohello servidor VMM.
9. configuración de cifrado de Hello sólo se utiliza al replicar las máquinas virtuales de Hyper-V en tooAzure de nubes VMM. Si replica tooa de sitio secundario no se utiliza.
10. En **nombre del servidor**, especifique un servidor VMM Nombre_descriptivo tooidentify hello en el almacén de Hola. En una configuración de clúster especificar nombre de rol de clúster VMM Hola.
11. En **sincronizar metadatos de nube**, seleccione si desea toosynchronize metadatos para todas las nubes en el servidor VMM de hello con almacén de Hola. Esta acción solo debe toohappen una vez en cada servidor. Si no desea toosynchronize todas las nubes, puede dejar esta configuración desactivada y sincronizar cada nube individualmente en las propiedades de la nube de hello en la consola VMM Hola.
12. Haga clic en **siguiente** toocomplete proceso de Hola. Después del registro, Azure Site Recovery recupera metadatos desde un servidor VMM Hola. servidor Hola se muestra en hello **servidores VMM** ficha en hello **servidores** página en el almacén de Hola.

    ![Server](./media/site-recovery-vmm-to-vmm-classic/provider13.PNG)
13. Después de hello servidor está disponible en la consola de Site Recovery hello, en **origen** > **preparar origen** seleccione servidor VMM de Hola y en qué Hola Hyper-V host se encuentra en la nube Hola select. y, a continuación, haga clic en **Aceptar**.

También puede instalar el proveedor de Hola desde línea de comandos de hello:

[!INCLUDE [site-recovery-rw-provider-command-line](../../includes/site-recovery-rw-provider-command-line.md)]


## <a name="set-up-hello-target-environment"></a>Configurar el entorno de destino de Hola

Seleccione en la nube y servidor VMM de destino de Hola.

1. Haga clic en **preparar infraestructura** > **destino**y el servidor VMM de destino Hola seleccione desea toouse.
2. Se mostrarán las nubes en el servidor de Hola que se sincronizan con Site Recovery. Seleccione la nube de destino de Hola.

   ![Destino](./media/site-recovery-vmm-to-vmm/target-vmm.png)

## <a name="set-up-replication-settings"></a>Configuración de las opciones de replicación

- Cuando se crea una directiva de replicación, todos los hosts mediante la directiva de hello debe haber Hola mismo sistema operativo. Hola nube de VMM puede contener hosts de Hyper-V que ejecutan versiones distintas de Windows Server, pero en este caso, se necesitan varias directivas de replicación.
- Puede realizar Hola la replicación inicial sin conexión. [Más información](#prepare-for-initial-offline-replication)

1. Haga clic en una nueva directiva de replicación de toocreate **preparar infraestructura** > **configuración de replicación** > **+ crear y asociar**.

    ![Red](./media/site-recovery-vmm-to-vmm/gs-replication.png)
2. En **Crear y asociar directiva**, especifique un nombre de directiva. Hello tipo de origen y de destino debe ser **Hyper-V**.
3. En **versión de host de Hyper-V**, seleccione el sistema operativo que se ejecuta en el host de Hola.
4. En **tipo de autenticación** y **puerto de autenticación**, especifique cómo se autentica el tráfico entre Hola principal y los servidores de host de Hyper-V de recuperación. Seleccione **Certificado** , a menos que tenga un entorno Kerberos activo. Azure Site Recovery configurará automáticamente los certificados para la autenticación de HTTPS. No es necesario toodo nada manualmente. De forma predeterminada, los puertos 8083 y 8084 (para certificados) se abrirá en Hola Firewall de Windows en los servidores de host de Hyper-V de Hola. Si selecciona **Kerberos**, se usará un vale de Kerberos para la autenticación mutua de los servidores de host de Hola. Observe que esta configuración solo es pertinente para servidores host de Hyper-V que se ejecutan en Windows Server 2012 R2.
5. En **copiar frecuencia**, especifique la frecuencia con desea tooreplicate diferencias de datos después de la replicación inicial de hello (cada 30 segundos, 5 o 15 minutos).
6. En **retención de punto de recuperación**, especifique en horas cuánto va un período de retención Hola para cada punto de recuperación. Equipos protegidos pueden ser recuperado tooany punto dentro de una ventana.
7. En **Frecuencia de instantánea coherente con la aplicación**especifique la frecuencia (entre 1 y 12 horas) con la que se crearán los puntos de recuperación que contengan las instantáneas coherentes con la aplicación. Hyper-V usa dos tipos de instantáneas, una instantánea estándar que proporciona una instantánea incremental de la máquina virtual completa de hello y una instantánea coherente con la aplicación que toma una instantánea de tiempo de punto de datos de la aplicación hello dentro de la máquina virtual de Hola. Las instantáneas coherentes con la aplicación usan tooensure de servicio de instantáneas de volumen (VSS) que las aplicaciones están en un estado coherente cuando se tomó la instantánea de Hola. Si habilita las instantáneas coherentes con la aplicación, afectará al rendimiento de Hola de aplicaciones que se ejecutan en máquinas virtuales de origen. Asegúrese de que el valor de hello especificado es menor que el número de Hola de puntos de recuperación adicionales que configure.
8. En **Compresión de transferencia de datos**, especifique si se deben comprimir los datos replicados que se transfieren.
9. Seleccione **Eliminar réplica VM**, toospecify que Hola máquina virtual de réplica debe eliminarse si se deshabilita la protección para una VM de origen Hola. Si habilita a esta configuración, al deshabilitar la protección para el origen de hello máquina virtual se quita de la consola de Site Recovery hello, configuración de Site Recovery para hello VMM se quita de la consola VMM de Hola y Hola réplica se eliminó.
10. En **inicial del método de replicación**, si se está replicando a través de la red hello, especifique si toostart la replicación inicial de Hola o programarlo. ancho de banda de red toosave, conviene tooschedule que fuera de su horario ocupado. y, a continuación, haga clic en **Aceptar**.

     ![Directiva de replicación](./media/site-recovery-vmm-to-vmm/gs-replication2.png)
11. Cuando se crea una nueva directiva automáticamente tiene asociadas con hello nube de VMM. En **Directiva de replicación**, haga clic en **Aceptar**. Puede asociar más nubes de VMM (hello y máquinas virtuales en ellos) con esta directiva de replicación en **replicación** > nombre de directiva > **asociar la nube de VMM**.

     ![Directiva de replicación](./media/site-recovery-vmm-to-vmm/policy-associate.png)


### <a name="configure-network-mapping"></a>Configurar asignación de red

- Aprenda sobre la [asignación de red](#prepare-for-network-mapping) antes de empezar.
- Compruebe que máquinas virtuales en servidores VMM red de VM tooa conectado.


1. En **Configuración** > **Infraestructura de Site Recovery** > **Asignación de red**Asignaciones de red, haga clic en **+Asignación de red**.

    ![Asignación de red](./media/site-recovery-vmm-to-azure/network-mapping1.png)
2. En **Agregar asignación de red** ficha, seleccione el origen de Hola y servidores VMM de destino. redes de VM de Hello asociadas con servidores VMM Hola se recuperan.
3. En **red de origen**, seleccione red Hola desea toouse de lista de Hola de redes de VM asociadas con el servidor VMM principal de Hola.
4. En **red de destino**, seleccione red Hola desea toouse en servidor VMM secundario Hola. y, a continuación, haga clic en **Aceptar**.

    ![Asignación de red](./media/site-recovery-vmm-to-vmm/network-mapping2.png)

Esto es lo que sucede cuando comienza la asignación de red:

* Las máquinas virtuales de réplica existente que corresponden toohello red de VM de origen será conectado toohello red de VM de destino.
* Nuevas máquinas virtuales que son redes VM de origen conectado toohello será red asignada de destino conectados toohello después de la replicación.
* Si modifica una asignación existente con una nueva red, máquinas virtuales de réplica se conectarán utilizando una nueva configuración de Hola.
* Si la red de destino de hello tiene varias subredes y una de estas subredes se Hola mismo nombre que la subred en la máquina virtual de origen de Hola se encuentra, entonces Hola máquina virtual será toothat conectado subred de destino después de la conmutación por error. Si no hay ninguna subred de destino con un nombre coincidente, máquina virtual de hello estará conectado toohello primera subred de red de Hola.

### <a name="configure-storage-mapping"></a>Configure la asignación de almacenamiento.

[Asignación de almacenamiento](#prepare-for-storage-mapping) no es compatible con el nuevo portal de Azure Hola. Sin embargo, se puede habilitar con PowerShell. [Más información](site-recovery-vmm-to-vmm-powershell-resource-manager.md#step-7-configure-storage-mapping).

## <a name="step-5-capacity-planning"></a>Paso 5: Pleaneamiento de capacidad

Ahora que tiene la infraestructura básica configurada, planee la capacidad y averigüe si necesitará recursos adicionales.

- Descargue y ejecute hello [planificador de capacidad de recuperación del sitio de Azure](site-recovery-capacity-planner.md), toogather información sobre su entorno de replicación, incluidas las máquinas virtuales, discos por máquina virtual y almacenamiento por disco.
- Después de haber recopilado la información de replicación en tiempo real, puede modificar el ancho de banda de hello NetQos directiva toocontrol replicación para máquinas virtuales. Lea más sobre la [limitación del tráfico de réplica de Hyper-V](http://www.thomasmaurer.ch/2013/12/throttling-hyper-v-replica-traffic/) en el blog de Thomas Maurer. Obtener más información acerca de hello [cmdlet New-NetQosPolicy](https://technet.microsoft.com/library/hh967468.aspx.).

## <a name="enable-replication"></a>Habilitar replicación

1. Haga clic en **Paso 2: Replicar la aplicación** > **Origen**. Después de habilitar la replicación para hello la primera vez, haga clic en **+ replicar** en la replicación de tooenable de almacén de Hola para máquinas adicionales.

    ![Habilitar replicación](./media/site-recovery-vmm-to-vmm/enable-replication1.png)
2. En **origen**, seleccione servidor VMM de Hola y Hola en la nube en qué Hola están ubicados los hosts de Hyper-V que desee tooreplicate. y, a continuación, haga clic en **Aceptar**.

    ![Habilitar replicación](./media/site-recovery-vmm-to-vmm/enable-replication2.png)
3. En **destino**, compruebe el servidor VMM secundario de Hola y en la nube.
4. En **máquinas virtuales**, seleccione hello las máquinas virtuales que desee tooprotect de lista de Hola.

    ![Habilitar protección de máquina virtual](./media/site-recovery-vmm-to-vmm/enable-replication5.png)

Puede seguir el progreso de hello **habilitar la protección de** acción en **trabajos** > **trabajos de recuperación del sitio**. Después de hello **finalización de protección** trabajo se completa, máquina virtual de hello está preparado para conmutación por error.

Observe lo siguiente:

- También puede habilitar la protección de máquinas virtuales en la consola VMM Hola. Haga clic en **Habilitar protección** en barra de herramientas de hello en Propiedades de la máquina virtual de hello > **Azure Site Recovery** ficha.
- Después de habilitar la replicación, puede ver propiedades de hello VM en **replican elementos**. En hello **Essentials** panel, puede ver información acerca de la directiva de replicación de hello hello VM y su estado. Haga clic en **Propiedades** para obtener más información.

### <a name="onboard-existing-virtual-machines"></a>Incorporación de máquinas virtuales existentes
Si tiene máquinas virtuales en VMM que se replican mediante Réplica de Hyper-V, puede incorporarlas a la replicación de Azure Site Recovery de la forma siguiente:

1. Compruebe que el servidor Hyper-V de Hola Hola que máquina virtual existente se encuentra en la nube principal Hola de hospedaje, y ese servidor de Hyper-V de hello hospeda la máquina virtual de réplica de Hola se encuentra en la nube secundaria Hola.
2. Asegúrese de que se configura una directiva de replicación para la nube VMM principal Hola.
3. Habilitar la replicación de máquina virtual principal de Hola. Azure Site Recovery y VMM aseguran de que hello mismo host de réplica y la máquina virtual se detecta y volverá a utilizar Azure Site Recovery y restablecer la replicación mediante Hola especificada la configuración.

## <a name="test-your-deployment"></a>Prueba de la implementación

tootest la implementación, puede ejecutar una [probar conmutación por error](site-recovery-test-failover-vmm-to-vmm.md) para una sola máquina virtual, o [crear un plan de recuperación](site-recovery-create-recovery-plans.md) que contiene una o más máquinas virtuales.



## <a name="prepare-for-offline-initial-replication"></a>Preparación para la replicación inicial sin conexión

Para hacer la replicación sin conexión para la copia de datos iniciales de Hola. Para preparar esta operación, haga lo siguiente:

* En el servidor de origen de hello, especifique una ubicación de ruta de acceso de qué Hola llevará a cabo la exportación de datos. Asigne Control total para los permisos NTFS y recurso compartido de servicio VMM de toohello en la ruta de acceso de exportación de Hola. En el servidor de destino de hello, especifique una ubicación de ruta de acceso desde la que importación datos de Hola se producirá. Asignar Hola mismos permisos en esta ruta de acceso de importación.
* Si hello importar o se comparte la ruta de acceso de exportación, asignar la pertenencia de grupo administrador, usuario avanzado, operador de impresión u operador de servidor para la cuenta de servicio VMM hello en el equipo remoto hello en qué Hola compartido se encuentra.
* Si usas los hosts de tooadd ejecutar como cuentas, en hello importar y exportar las rutas de acceso, asigne lectura y permisos de escritura toohello cuentas de ejecución en VMM.
* Hola importar y exportar recursos compartidos no se deben encontrar en cualquier equipo que se usa como un servidor de host de Hyper-V, porque la configuración de bucle invertido no es compatible con Hyper-V.
* En Active Directory, en cada servidor de host de Hyper-V que contiene máquinas virtuales que desea tooprotect, habilitar y configurar la delegación restringida tootrust Hola remota los equipos en qué Hola importación y exportación en las rutas de acceso se encuentran, como se indica a continuación:
  1. En el controlador de dominio de hello, abra **equipos y usuarios de Active Directory**.
  2. En el árbol de consola de hello, haga clic en **DomainName** > **equipos**.
  3. Nombre del servidor de host de Hyper-V de Hola de contextual > **propiedades**.
  4. En hello **delegación** , haga clic en **confiar en este equipo para servicios solo de delegación toospecified**.
  5. Haga clic en **Usar cualquier protocolo de autenticación**.
  6. Haga clic en **Agregar** > **Usuarios y equipos**.
  7. Nombre del tipo hello del equipo de Hola que hospeda la ruta de acceso de exportación de hello > **Aceptar**. En la lista hello de servicios disponibles, mantenga presionada la tecla CTRL de Hola y haga clic en **cifs** > **Aceptar**. Repita para nombre de hello del equipo de hello esa ruta de acceso de importación de Hola de hosts. Repita según sea necesario para servidores host de Hyper-V adicionales.



## <a name="prepare-for-network-mapping"></a>Preparar la asignación de red
Mapas de asignación de red entre redes de VM de VMM en servidores VMM de hello principales y secundarias para:

* Colocar óptimamente las máquinas virtuales de réplica en los hosts de Hyper-V secundarios tras la conmutación por error.
* Conectar redes de VM de tooappropriate de las máquinas virtuales de réplica después de la conmutación por error.

Observe lo siguiente:
- Asignación de red se puede configurar entre redes de VM en dos servidores VMM o en un único servidor VMM si administra dos sitios Hola mismo servidor.
- Cuando se configura correctamente la asignación y está habilitada la replicación, una máquina virtual en la ubicación principal Hola será red tooa conectado y se conectará su réplica en la ubicación de destino de hello tooits asigna la red.
- Si redes se ha configurado correctamente en VMM, al seleccionar una red de VM de destino durante la asignación de red, nubes de origen VMM de Hola que usan la red de VM de origen Hola se mostrarán junto con redes de VM de destino disponibles de hello en nubes de destino de Hola que sirven para protección.
- Si la red de destino de hello tiene varias subredes y una de dichas subredes tiene Hola mismo nombre como Hola subred en qué Hola máquina virtual de origen se encuentra, a continuación, Hola máquina virtual de réplica será toothat conectado subred de destino después de la conmutación por error. Si no hay ninguna subred de destino con un nombre coincidente, máquina virtual de hello estará conectado toohello primera subred de red de Hola.


Este es un ejemplo tooillustrate este mecanismo. Vamos a utilizar una organización con dos ubicaciones en Nueva York y Chicago.

| **Ubicación** | **Servidor VMM** | **Redes de máquinas virtuales** | **Asignado a** |
| --- | --- | --- | --- |
| Nueva York |VMM-NewYork |VMNetwork1-NewYork |TooVMNetwork1-Chicago asignada |
| VMNetwork2-NewYork |No asignado | | |
| Chicago |VMM-Chicago |VMNetwork1-Chicago |TooVMNetwork1-NewYork asignada |
| VMNetwork2-Chicago |No asignado | | |

Con este ejemplo:

* Cuando se crea una máquina virtual de réplica para cualquier máquina virtual que está conectado tooVMNetwork1-NewYork, estará conectado tooVMNetwork1-Chicago.
* Cuando se crea una máquina virtual de réplica para VMNetwork2-NewYork o VMNetwork2-Chicago, no estará conectada tooany red.

Aquí es cómo se configuran las nubes de VMM en nuestra organización de ejemplo y redes lógicas Hola asociadas a nubes de Hola.

### <a name="cloud-protection-settings"></a>Configuración de la protección de la nube
| **Nube protegida** | **Proteger nube** | **Red lógica (Nueva York)** |
| --- | --- | --- |
| GoldCloud1 |GoldCloud2 | |
| SilverCloud1 |SilverCloud2 | |
| GoldCloud2 |<p>N/D</p><p></p> |<p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p> |
| SilverCloud2 |<p>N/D</p><p></p> |<p>LogicalNetwork1-NewYork</p><p>LogicalNetwork1-Chicago</p> |

### <a name="logical-and-vm-network-settings"></a>Configuración de la red lógica y máquinas virtuales
| **Ubicación** | **Red lógica** | **Red de VM asociada** |
| --- | --- | --- |
| Nueva York |LogicalNetwork1-NewYork |VMNetwork1-NewYork |
| Chicago |LogicalNetwork1-Chicago |VMNetwork1-Chicago |
| LogicalNetwork2Chicago |VMNetwork2-Chicago | |

### <a name="target-networks"></a>Redes de destino
Según estos valores, al seleccionar red de VM de destino de hello, hello en la tabla siguiente muestra las opciones de Hola que estarán disponibles.

| **Selección** | **Nube protegida** | **Proteger nube** | **Red de destino disponible** |
| --- | --- | --- | --- |
| VMNetwork1-Chicago |SilverCloud1 |SilverCloud2 |Disponible |
| GoldCloud1 |GoldCloud2 |Disponible | |
| VMNetwork2-Chicago |SilverCloud1 |SilverCloud2 |No disponible |
| GoldCloud1 |GoldCloud2 |Disponible | |


### <a name="failback"></a>Conmutación por recuperación
toosee lo que ocurre en el caso de hello de conmutación por recuperación (replicación inversa), vamos a suponer que VMNetwork1-NewYork está asignada tooVMNetwork1-Chicago, con hello después de la configuración.

| **Máquina virtual** | **Red tooVM conectado** |
| --- | --- |
| VM1 |VMNetwork1-Network |
| VM2 (réplica de VM1) |VMNetwork1-Chicago |

Con esta configuración, revisemos lo que ocurre en un par de escenarios posibles.

| **Escenario** | **Resultado** |
| --- | --- |
| Ningún cambio hello en Propiedades de red de VM-2 después de la conmutación por error. |VM-1 permanece conectado toohello red de origen. |
| Las propiedades de red de VM-2 cambian después de la conmutación por error y está desconectada. |VM-1 se desconecta. |
| Propiedades de red de VM-2 cambian después de la conmutación por error y está conectado tooVMNetwork2-Chicago. |Si no está asignada VMNetwork2-Chicago, se desconectará VM-1. |
| Se cambia la asignación de redes de VMNetwork1-Chicago. |VM-1 será toohello conectado red ahora asignada tooVMNetwork1-Chicago. |


## <a name="prepare-for-single-server-deployment"></a>Preparación para la implementación de un solo servidor


Si solo tiene un único servidor VMM, puede replicar las máquinas virtuales en hosts de Hyper-V en la nube de VMM Hola demasiado[Azure](site-recovery-vmm-to-azure.md) o una nube VMM secundaria tooa. Se recomienda la primera opción de hello porque replicar entre nubes no es perfecta. Si desea tooreplicate entre nubes, puede replicar con un servidor VMM única e independiente o con un solo servidor VMM implementado en un clúster de Windows con Stretch

### <a name="standalone-vmm-server"></a>Servidor VMM independiente

En este escenario, implementar Hola único servidor de VMM como una máquina virtual en el sitio primario de Hola y replicar este sitio secundario de tooa VM con Site Recovery y réplica de Hyper-V.

1. **Configurar VMM en una máquina virtual Hyper-V**. Se recomienda la colocación de instancia de SQL Server de hello utilizado por VMM en hello misma máquina virtual. Esto ahorra tiempo ya que solo una máquina virtual tiene toobe creado. Si desea toouse la instancia remota de SQL Server y se produce una interrupción, deberá toorecover esa instancia para poder recuperar VMM.
2. **Asegúrese de servidor VMM hello tiene al menos dos nubes configuradas**. Una nube contendrá hello las máquinas virtuales que desee tooreplicate y Hola otra nube servirá como ubicación secundaria Hola. Hola en la nube que contiene máquinas virtuales de hello desea deben cumplir tooprotect [requisitos previos](#prerequisites).
3. Configure Site Recovery tal como se describe en este artículo. Crear y registrar el servidor VMM de hello en un almacén, configurar una directiva de replicación y habilitar la replicación. los nombres VMM de origen y de destino de Hola se se Hola mismo. Especificar que la replicación inicial realiza a través de red de Hola.
4. Al configurar la asignación de red asignar red de VM de Hola Hola nube principal toohello red de VM de nube secundaria Hola.
5. En la consola de administrador de Hyper-V de hello, habilitar réplica de Hyper-V en el host de Hyper-V de Hola que contiene Hola VM de VMM y habilitar la replicación en hello máquina virtual. Asegúrese de que no agregue tooclouds de máquina virtual VMM de Hola que están protegidos por recuperación del sitio, tooensure que configuración de réplica de Hyper-V no se invalidan Site Recovery.
6. Si crea planes de recuperación para conmutación por error que usa Hola mismo servidor VMM de origen y de destino.
7. En una interrupción completa, se conmuta por error y se recupera de la siguiente forma:

   1. Ejecute una conmutación por error no planeada en la consola de administrador de Hyper-V de hello en el sitio secundario hello, toofail a través del sitio secundario del principal toohello VM de VMM de Hola.
   2. Compruebe que Hola que VM de VMM está activo y ejecutándose y en el almacén de hello, ejecutar una conmutación por error imprevista toofail a máquinas virtuales de Hola de nubes toosecondary principal. Confirmar conmutación por error de Hola y seleccione un punto de recuperación alternativo si es necesario.
   3. Una vez hello conmutación por error imprevista completada, todos los recursos son accesibles desde el sitio primario de hello nuevo.
   4. Cuando hay sitio primario de Hola de nuevo, en la consola de administrador de Hyper-V de hello en el sitio secundario de hello, habilitar la replicación inversa para hello VM de VMM. Esto inicia la replicación para hello VM desde tooprimary secundaria.
   5. Ejecute una conmutación por error planeada en la consola de administrador de Hyper-V de hello en el sitio secundario hello, toofail sobre Hola sitio primario de toohello de VM de VMM. Confirmar conmutación por error de Hola. A continuación, habilitar la replicación inversa, para que hello VM de VMM se vuelva a replicar desde toosecondary principal.
   6. En el almacén de servicios de recuperación de hello, habilitar la replicación inversa para cargas de trabajo de hello las máquinas virtuales, toostart replicándolos de tooprimary secundaria.
   7. En el almacén de servicios de recuperación hello, que se ejecute un conmutación por error planeada toofail Hola back-carga de trabajo VM toohello sitio primario. Confirmar toocomplete de conmutación por error de Hola. A continuación, habilite la replicación inversa toostart replicación Hola carga de trabajo máquinas virtuales de toosecondary principal.

### <a name="stretched-vmm-cluster"></a>Clúster de VMM estirado

En lugar de implementar un servidor VMM independiente como una máquina virtual que se replica tooa de sitio secundario, puede hacer que VMM alta disponibilidad mediante la implementación como una máquina virtual en un clúster de conmutación por error de Windows. De esta forma, se garantiza la resistencia de las cargas de trabajo y la protección frente a los errores del hardware. toodeploy con hello de Site Recovery VM de VMM debe implementarse en un clúster de stretch en sitios dispersos geográficamente. toodo esto:

1. Instalar VMM en una máquina virtual en un clúster de conmutación por error de Windows y seleccione Hola opción toorun Hola servidor como de alta disponibilidad durante la instalación.
2. instancia de SQL Server de Hello usada por VMM se debe replicar con grupos de disponibilidad AlwaysOn de SQL Server, por lo que hay una réplica de base de datos de hello en el sitio secundario de Hola.
3. Siga las instrucciones de hello en este toocreate artículo un almacén, Registrar servidor hello y configure la protección. Necesita tooregister clúster de cada servidor VMM en hello en hello del almacén de servicios de recuperación. toodo, instalar Hola proveedor en un nodo activo y registrar el servidor VMM Hola. A continuación, instalar Hola proveedor en otros nodos.
4. Cuando se produce una interrupción, servidor VMM de Hola y su base de datos de SQL Server correspondiente se conmutarán por error y se tiene acceso desde el sitio secundario de Hola.



## <a name="prepare-for-storage-mapping"></a>Preparación de la asignación de almacenamiento


Configurar el almacenamiento asignando las clasificaciones de almacenamiento en un origen y destino siguiente de Hola de toodo de servidores VMM:

  * **Identificar el almacenamiento de destino para máquinas virtuales de réplica**: un disco duro de máquina virtual de origen se replicarán almacenamiento toohello especificado (recurso compartido de SMB o clúster volúmenes compartidos (CSV)) en la ubicación de destino de Hola.
  * **Selección de máquina virtual de réplica**: asignación de almacenamiento es coloca las máquinas virtuales usadas toooptimally réplica en servidores de host de Hyper-V. Máquinas virtuales de réplica se colocarán en hosts que pueden tener acceso a la clasificación de almacenamiento de hello asignado.
  * **Ninguna asignación de almacenamiento**: si no configura la asignación de almacenamiento, máquinas virtuales será la ubicación de almacenamiento predeterminada replicada toohello especificado en el servidor de host de Hyper-V de hello asociado a la máquina virtual de réplica de Hola.

Observe lo siguiente:
- Puede configurar la asignación entre dos nubes VMM en un solo servidor.
- Las clasificaciones de almacenamiento deben estar disponibles toohello grupos de host ubicados en nubes de origen y de destino.
- Las clasificaciones no necesitan toohave Hola el mismo tipo de almacenamiento. Por ejemplo, puede asignar una clasificación de origen que contiene la clasificación de destino de tooa de recursos compartidos SMB que contiene CSV.

### <a name="example"></a>Ejemplo
Si las clasificaciones estén configuradas correctamente en VMM cuando se selecciona el origen de Hola y de servidor VMM de destino durante la asignación de almacenamiento, se mostrará las clasificaciones de origen y destino de Hola. Este es un ejemplo de recursos compartidos de archivos de almacenamiento y clasificaciones para una organización con dos ubicaciones en Nueva York y Chicago.

| **Ubicación** | **Servidor VMM** | **Recurso compartido de archivos (origen)** | **Clasificación (origen)** | **Asignado a** | **Recurso compartido de archivos (destino)** |
| --- | --- | --- | --- | --- | --- |
| Nueva York |VMM_Source |SourceShare1 |GOLD |GOLD_TARGET |TargetShare1 |
| SourceShare2 |SILVER |SILVER_TARGET |TargetShare2 | | |
| SourceShare3 |BRONZE |BRONZE_TARGET |TargetShare3 | | |
| Chicago |VMM_Target | |GOLD_TARGET |No asignado | |
|  |SILVER_TARGET |No asignado | | | |
|  |BRONZE_TARGET |No asignado | | | |

Con este ejemplo:

* Cuando se crea una máquina virtual de réplica para cualquier máquina virtual en almacenamiento GOLD (SourceShare1), será tooa replicada gold_destino almacenamiento (TargetShare1).
* Cuando se crea una máquina virtual de réplica para cualquier máquina virtual en almacenamiento SILVER (SourceShare2), ser replicadas tooa SILVER_TARGET (TargetShare2) almacenamiento y así sucesivamente.

### <a name="multiple-storage-locations"></a>Múltiples cuentas de almacenamiento
Si se asigna la clasificación de destino de hello toomultiple recursos compartidos de SMB o CSV, ubicación de almacenamiento óptima de Hola se seleccionará automáticamente cuando la máquina virtual de hello está protegida. Si no está disponible con ningún almacenamiento de destino adecuado Hola especificó la clasificación, de forma predeterminada Hola ubicación de almacenamiento especificada en el host de Hyper-V de hello es tooplace usado Hola réplica los discos duros virtuales.

Hello en la tabla siguiente muestra cómo clasificación de almacenamiento y volúmenes compartidos de clúster se configuran en nuestro ejemplo.

| **Ubicación** | **Clasificación** | **Almacenamiento asociada** |
| --- | --- | --- |
| Nueva York |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> |
| SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p> | |
| Chicago |GOLD_TARGET |<p>C:\ClusterStorage\TargetVolume1</p><p>\\FileServer\TargetShare1</p> |
| SILVER_TARGET |<p>C:\ClusterStorage\TargetVolume2</p><p>\\FileServer\TargetShare2</p> | |

Esta tabla resume el comportamiento de hello al habilitar la protección para máquinas virtuales (VM1 - VM5) en este entorno de ejemplo.

| **Máquina virtual** | **Almacenamiento de origen** | **Clasificación de origen** | **Almacenamiento de destino asignado** |
| --- | --- | --- | --- |
| VM1 |C:\ClusterStorage\SourceVolume1 |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\\FileServer\SourceShare1</p><p>Ambos GOLD_TARGET</p> |
| VM2 |\\FileServer\SourceShare1 |GOLD |<p>C:\ClusterStorage\SourceVolume1</p><p>\\FileServer\SourceShare1</p> <p>Ambos GOLD_TARGET</p> |
| VM3 |C:\ClusterStorage\SourceVolume2 |SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\FileServer\SourceShare2</p> |
| VM4 |\FileServer\SourceShare2 |SILVER |<p>C:\ClusterStorage\SourceVolume2</p><p>\\FileServer\SourceShare2</p><p>Ambos SILVER_TARGET</p> |
| VM5 |C:\ClusterStorage\SourceVolume3 |N/D |Ninguna asignación, por lo que se utiliza la ubicación de almacenamiento predeterminada de Hola de host de Hyper-V de Hola |



### <a name="data-privacy-overview"></a>Información general sobre la privacidad de los datos

En esta tabla se resume cómo se almacenan los datos en este escenario:

- - -
| Acción | **Detalles** | **Datos recopilados** | **Uso** | **Obligatorio** |
| --- | --- | --- | --- | --- |
| **Registro** | Registra un servidor VMM en un almacén de Servicios de recuperación. Si posteriormente desea toounregister un servidor, puede hacerlo eliminando la información del servidor hello de hello portal de Azure. | Después de registra un servidor VMM Site Recovery recopila, procesa y transfiere los metadatos sobre el servidor VMM de Hola y los nombres de Hola de nubes VMM Hola detectadas mediante la recuperación del sitio. | datos de Hello es tooidentify usado y comunicarán con el servidor VMM adecuado de Hola y configuración opciones adecuadas para nubes de VMM. | Esta característica es necesaria. Si no desea toosend esta tooSite información recuperación no debe usar el servicio de Site Recovery Hola. |
| **Habilitar replicación** | Hola proveedor de Azure Site Recovery está instalado en el servidor VMM de Hola y es Hola conducto para la comunicación con hello servicio Site Recovery. Hola proveedor es una biblioteca de vínculos dinámicos (DLL) hospedada en proceso VMM Hola. Después de hello que proveedor está instalado, la característica de "Recuperación de centro de datos" Hola obtiene habilitada en la consola de administrador VMM de Hola. Máquinas virtuales nuevas y existentes pueden habilitar esta protección tooenable de característica para una máquina virtual. |Con este conjunto de propiedades, Hola proveedor envía Hola nombre e identificador de hello VM tooSite recuperación.  La replicación se habilita mediante la réplica de Hyper-V de Windows Server 2012 o Windows Server 2012 R2. datos de máquina virtual de Hola se replicarán desde una tooanother de host de Hyper-V (que normalmente se encuentra en un centro de datos de "recuperación" diferente). |Recuperación del sitio utiliza información de máquina virtual de hello metadatos toopopulate Hola Hola portal de Azure. | Esta característica es una parte esencial del servicio de hello y no se puede desactivar. Si no desea toosend esta información, no habilite la protección de recuperación del sitio para las máquinas virtuales. Tenga en cuenta que todos los datos enviados por el proveedor de hello tooSite recuperación se envía a través de HTTPS. |
| **Plan de recuperación** | Planes de recuperación le ayudará a generar un plan de orquestación de centro de datos de recuperación de Hola. Puede definir el orden de hello en el que se debe iniciar las máquinas virtuales o un grupo de máquinas virtuales en el sitio de recuperación de Hola. También puede especificar cualquier toobe scripts automatizados que se ejecute, o cualquier toobe acción manual realizada en Hola de recuperación para cada máquina virtual. Conmutación por error se desencadena normalmente en el nivel de plan de recuperación de hello para la recuperación coordinada. | Recuperación de sitio recopila, procesa y transmite los metadatos de plan de recuperación de hello, incluidos los metadatos de la máquina virtual y los metadatos de todos los scripts de automatización y las notas de la acción manual. |metadatos de Hello están plan de recuperación de hello toobuild usado en hello portal de Azure. |Esta característica es una parte esencial del servicio de hello y no se puede desactivar. Si no desea toosend esta tooSite información recuperación, no se crean los planes de recuperación. |
| **Asignación de red** | Mapas de red información desde el centro de datos de recuperación de toohello centro de datos principal de Hola. Cuando se recuperan las máquinas virtuales en el sitio de recuperación de hello, asignación de red ayuda a establecer la conectividad de red. |Recuperación de sitio recopila, procesa y transmite los metadatos de Hola de redes lógicas de Hola para cada sitio (principal y centro de datos). |metadatos de Hello son toopopulate usa configuración de red para que se puede asignar la información de red de Hola. | Esta característica es una parte esencial del servicio de hello y no se puede desactivar. Si no desea toosend esta tooSite información recuperación, no use la asignación de red. |
| **Conmutación por error (planeada o no planeada y prueba)** | Conmutación por error conmuta por error las máquinas virtuales de tooanother del centro de datos administrados de VMM. acción de conmutación por error de Hello sea de forma manual en hello portal de Azure. |Hola proveedor en el servidor VMM Hola recibe una notificación de evento de conmutación por error de Hola por Site Recovery y ejecuta una acción de conmutación por error en el host de Hyper-V de Hola a través de interfaces VMM. Conmutación por error real de una máquina virtual desde un tooanother de host de Hyper-V y controlada por Windows Server 2012 o Windows Server 2012 R2 Hyper-V réplica. Posterior recuperación de sitio usa información de hello enviado el estado de hello toopopulate de información de acción de conmutación por error de hello en hello portal de Azure. | Esta característica es una parte esencial del servicio de hello y no se puede desactivar. Si no desea toosend esta tooSite información recuperación, no use la conmutación por error. |

## <a name="next-steps"></a>Pasos siguientes

Después de haberlo probado implementación hello, obtener más información sobre otros tipos de [conmutación por error](site-recovery-failover.md)
