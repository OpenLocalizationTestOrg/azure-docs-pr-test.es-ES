---
title: "aaaAutomate StorSimple fileshare recuperación ante desastres con Azure Site Recovery | Documentos de Microsoft"
description: "Describe los pasos de Hola y procedimientos recomendados para crear una solución de recuperación ante desastres para los recursos compartidos hospedados en el almacenamiento de Microsoft Azure StorSimple."
services: storsimple
documentationcenter: NA
author: vidarmsft
manager: syadav
editor: 
ms.assetid: 23049a2c-055e-4d0e-b8f5-af2a87ecf53f
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/09/2017
ms.author: vidarmsft
ms.openlocfilehash: fa3e8d4e77ca0f6a7b5f9bbb956a4de12547642e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="automated-disaster-recovery-solution-using-azure-site-recovery-for-file-shares-hosted-on-storsimple"></a>Solución de recuperación ante desastres automatizada con Azure Site Recovery para recursos compartidos de archivos alojados en StorSimple
## <a name="overview"></a>Información general
StorSimple de Microsoft Azure es una solución de almacenamiento de nube híbrida que direcciones Hola complejidades de los datos no estructurados que suelen estar asociadas con recursos compartidos de archivos. StorSimple usa almacenamiento en la nube como solución local de una extensión de hello y automáticamente de capas de datos en un almacenamiento local y el almacenamiento en nube. Integra la protección de datos, con local e instantáneas en la nube, elimina la necesidad de Hola de una infraestructura de almacenamiento desorganizados.

[Azure Site Recovery](../site-recovery/site-recovery-overview.md) es un servicio basado en Azure que proporciona capacidades de recuperación ante desastres (DR) mediante la organización de la replicación, la conmutación por error y la recuperación de máquinas virtuales. Azure Site Recovery admite un número de replicación tecnologías tooconsistently replicate, proteger y conmutará por error con nubes de máquinas virtuales y aplicaciones tooprivate/público u hospedadas.

Con Azure Site Recovery, replicación de máquina virtual y capacidades de copias instantáneas de StorSimple en la nube, puede proteger el entorno del servidor de hello completa del archivo. En caso de hello de interrupción, puede utilizar un toobring un solo clic, el uso compartido de archivos en línea en Azure en tan solo unos minutos.

En este documento se explica en detalle cómo crear una solución de recuperación ante desastres para los recursos compartidos de archivos hospedados en el almacenamiento de StorSimple, así como realizar conmutaciones por error planeadas, no planeadas y de prueba usando un plan de recuperación de un solo clic. En esencia, muestra cómo puede modificar Hola Plan de recuperación en su tooenable de almacén de Azure Site Recovery StorSimple las conmutaciones por error durante situaciones de desastre. Además, se describen los requisitos previos y las configuraciones compatibles. Este documento se supone que está familiarizado con conceptos básicos de Hola de arquitecturas de Azure Site Recovery y StorSimple.

## <a name="supported-azure-site-recovery-deployment-options"></a>Opciones de implementación de Azure Site Recovery compatibles
Los clientes pueden implementar servidores de archivos como servidores físicos o máquinas virtuales (VM) que se ejecutan en Hyper-V o VMware y, después, crear recursos compartidos de archivos desde volúmenes extraídos del almacenamiento de StorSimple. Azure Site Recovery puede proteger ambos tooeither las implementaciones físicas y virtuales de un sitio secundario o tooAzure. Este documento cubre los detalles de una solución de recuperación ante desastres con Azure como sitio de recuperación de Hola para un servidor de archivos que máquinas virtuales hospedadas en Hyper-V y con recursos compartidos de archivos en el almacenamiento de StorSimple. Otros escenarios en qué servidor de archivos de hello máquina virtual está en una VM de VMware o en una máquina física se pueden implementar de forma similar.

## <a name="prerequisites"></a>Requisitos previos
Implementar una solución de recuperación ante desastres con un solo clic que usa Azure Site Recovery para recursos compartidos de archivos que se hospedan en el almacenamiento de StorSimple tiene Hola siguiendo los requisitos previos:

* VM de servidor de archivos Windows Server 2012 R2 local hospedada en Hyper-V, VMware o en una máquina física
* Dispositivo de almacenamiento StorSimple local registrado con Azure StorSimple Manager
* Dispositivo de StorSimple en la nube creado en el Administrador de StorSimple de Azure de hello (se mantiene en estado apagado)
* Recursos compartidos de archivos hospedados en volúmenes de hello configurados en el dispositivo de almacenamiento de StorSimple de Hola
* [Almacén de los servicios de Azure Site Recovery](../site-recovery/site-recovery-vmm-to-vmm.md) creado en una suscripción de Microsoft Azure

Además, si Azure es el sitio de recuperación, ejecute hello [herramienta de evaluación de preparación para la máquina Virtual de Azure](http://azure.microsoft.com/downloads/vm-readiness-assessment/) en tooensure de máquinas virtuales que sean compatibles con máquinas virtuales de Azure y Azure Site Recovery services.

problemas de latencia de tooavoid (lo que podrían ocasionar mayor será el costo), asegúrese de que crear su aplicación de nube de StorSimple, cuenta de automatización, y las cuentas de almacenamiento en Hola misma región.

## <a name="enable-dr-for-storsimple-file-shares"></a>Habilitación de la recuperación ante desastres para recursos compartidos de archivos de StorSimple
Cada componente de hello local entorno debe toobe protegido tooenable completar la replicación y la recuperación. En esta sección se describe cómo llevar a cabo las siguientes acciones:

* Configuración de la replicación de DNS y Active Directory (opcional)
* Usar la protección de Azure Site Recovery tooenable Hola del servidor de archivos virtual
* Habilitación de la protección de volúmenes de StorSimple
* Configurar red Hola

### <a name="set-up-active-directory-and-dns-replication-optional"></a>Configuración de la replicación de DNS y Active Directory (opcional)
Si desea que hello tooprotect máquinas que se ejecutan Active Directory y DNS para que estén disponibles en el sitio de recuperación ante desastres de hello, necesita tooexplicitly protegerlos (de modo que los servidores de archivos de hello son accesibles después de la conmutación por error con la autenticación). Hay dos opciones recomendadas basándose en complejidad Hola Hola del local del entorno de cliente.

#### <a name="option-1"></a>Opción 1
Si el cliente de hello tiene un número pequeño de aplicaciones, un controlador de dominio para toda Hola sitio local y se se conmuta por error todo sitio hello, a continuación, se recomienda usar la máquina del controlador de dominio de Azure Site Recovery replicación tooreplicate Hola sitio secundario de tooa (Esto es aplicable para el sitio a sitio y el sitio de Azure).

#### <a name="option-2"></a>Opción 2
Si cliente hello tiene un gran número de aplicaciones, ejecuta un bosque de Active Directory y se conmuta de unas pocas aplicaciones a la vez, se recomienda configurar un controlador de dominio adicional en el sitio de recuperación ante desastres de hello (ya sea un sitio secundario o en Azure).

Consulte demasiado[solución automatizada recuperación ante desastres de Active Directory y DNS con Azure Site Recovery](../site-recovery/site-recovery-active-directory.md) para obtener instrucciones al realizar un controlador de dominio disponible en el sitio de recuperación ante desastres de Hola. Para el resto de Hola de este documento, se asumirá que un controlador de dominio está disponible en el sitio de recuperación ante desastres de Hola.

### <a name="use-azure-site-recovery-tooenable-protection-of-hello-file-server-vm"></a>Usar la protección de Azure Site Recovery tooenable Hola del servidor de archivos virtual
Este paso requiere que preparar el entorno de servidor de archivos local de hello, crear y preparar un almacén de Azure Site Recovery y habilitar la protección de archivos del programa Hola a máquina virtual.

#### <a name="tooprepare-hello-on-premises-file-server-environment"></a>Hola tooprepare entorno de servidor de archivos local
1. Conjunto hello **User Account Control** demasiado**no notificarme nunca**. Esto es necesario para que pueda utilizar los destinos iSCSI de automatización de Azure scripts tooconnect Hola después de un error conmuta por recuperación de sitio de Azure.

   1. Presione la tecla de Windows hello + Q y busque **UAC**.
   2. Seleccione **Cambiar configuración de Control de cuentas de usuario**.
   3. Hola de arrastre de la barra inferior toohello hacia **no notificarme nunca**.
   4. Haga clic en **Aceptar** y, después, seleccione **Sí** cuando se le solicite.

      ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image1.png)
2. Instalar Hola agente de máquina virtual en cada servidor de archivos de hello las máquinas virtuales. Esto es necesario para que pueda ejecutar scripts de automatización de Azure en hello conmutado por error las máquinas virtuales.

   1. [Descargar agente hello](http://aka.ms/vmagentwin) demasiado`C:\\Users\\<username>\\Downloads`.
   2. Abra Windows PowerShell en modo de administrador (ejecutar como administrador) y, a continuación, escriba Hola ubicación de descarga de comando toonavigate toohello siguiente:

      `cd C:\\Users\\<username>\\Downloads\\WindowsAzureVmAgent.2.6.1198.718.rd\_art\_stable.150415-1739.fre.msi`

      > [!NOTE]
      > nombre de archivo de Hello puede cambiar dependiendo de la versión de Hola.
      >
      >
3. Haga clic en **Siguiente**.
4. Aceptar hello **términos del acuerdo** y, a continuación, haga clic en **siguiente**.
5. Haga clic en **Finalizar**
6. Cree recursos compartidos de archivos con volúmenes extraídos del almacenamiento de StorSimple. Para obtener más información, consulte [utilizar hello StorSimple Manager servicio toomanage volúmenes](storsimple-manage-volumes.md).

   1. En las máquinas virtuales locales, presione la tecla de Windows hello + Q y busque **iSCSI**.
   2. Seleccione **iniciador iSCSI**.
   3. Seleccione hello **configuración** ficha y copiar nombre de iniciador de Hola.
   4. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
   5. Seleccione hello **StorSimple** ficha y, a continuación, seleccione Hola el servicio StorSimple Manager que contiene el dispositivo físico de Hola.
   6. Cree contenedores de volumen y, luego, volúmenes. (Estos volúmenes son para recursos compartidos de archivo de hello en servidor de archivos de hello las máquinas virtuales). Copie el nombre del iniciador de Hola y asigne un nombre adecuado para hello registros de Control de acceso cuando se crean volúmenes Hola.
   7. Seleccione hello **configurar** ficha y anote la dirección IP de hello de dispositivo de Hola.
   8. En las máquinas virtuales locales, vaya toohello **iniciador iSCSI** nuevo y escriba IP Hola Hola sección conexión rápida. Haga clic en **conexión rápida** (dispositivo de hello ahora debe estar conectado).
   9. Hola abrir portal de Azure y seleccione Hola **volúmenes y dispositivos** ficha. Haga clic en **Autoconfigurar**. debería aparecer el volumen de Hola que acaba de crear.
   10. En el portal de hello, seleccione hello **dispositivos** ficha y, a continuación, seleccione **crear un nuevo dispositivo Virtual.** (Este dispositivo virtual se utilizará si se produce una conmutación por error). Se puede conservar este nuevo dispositivo virtual en un estado sin conexión tooavoid costos adicionales. tootake Hola dispositivo virtual sin conexión, vaya toohello **máquinas virtuales** sección Hola Portal y cerrarlo.
   11. Vuelva toohello máquinas virtuales locales y abra Administración de discos (presione la tecla de Windows hello + X y seleccione **administración de discos**).
   12. Observará algunos discos adicionales (en función del número de Hola de volúmenes que haya creado). Menú contextual Hola primero, seleccione **inicializar disco**y seleccione **Aceptar**. Menú contextual hello **sin asignar** sección, seleccione **nuevo volumen Simple**, asignarle una letra de unidad y finalice el Asistente de Hola.
   13. Repita el paso l para todos los discos de Hola. Ahora puede ver todos los discos de hello en **este PC** en el Explorador de Windows hello.
   14. Utilice Hola File and Storage Services rol toocreate recursos compartidos de archivos en estos volúmenes.

#### <a name="toocreate-and-prepare-an-azure-site-recovery-vault"></a>toocreate y preparar un almacén de Azure Site Recovery
Consulte toohello [documentación de Azure Site Recovery](../site-recovery/site-recovery-hyper-v-site-to-azure.md) tooget a trabajar con Azure Site Recovery antes de proteger el servidor de archivos de hello máquina virtual.

#### <a name="tooenable-protection"></a>protección de tooenable
1. Desconectar Hola iSCSI destinos de hello las máquinas virtuales que desea que tooprotect a través de Azure Site Recovery local:

   1. Presione la tecla Windows + Q y busque **iSCSI**.
   2. Seleccione **Configurar iniciador iSCSI**.
   3. Desconecte el dispositivo StorSimple Hola que se conectó anteriormente. Como alternativa, puede desactivar el servidor de archivos de Hola durante unos minutos al habilitar la protección.

   > [!NOTE]
   > Esto hará que hello toobe de recursos compartidos de archivo no está disponible temporalmente.
   >
   >
2. [Habilitar la protección de máquina virtual](../site-recovery/site-recovery-hyper-v-site-to-azure.md) Hola servidor de archivos VM desde el portal de Azure Site Recovery Hola.
3. Cuando se inicia la sincronización inicial de hello, puede volver a conectar el destino de hello nuevo. Paso toohello iniciador de iSCSI, seleccione el dispositivo de StorSimple de Hola y haga clic en **conectar**.
4. Cuando sincronización Hola está completa y estado de Hola de hello VM es **Protected**, seleccione Hola VM, seleccione hello **configurar** y a actualizar la red de Hola de hello VM en consecuencia (Esto es red Hola ese Hola conmutado por error máquinas virtuales formarán parte de). Si no se muestre red hello, significa que todavía está sucediendo sincronización Hola.

### <a name="enable-protection-of-storsimple-volumes"></a>Habilitación de la protección de volúmenes de StorSimple
Si no ha seleccionado hello **habilitar una copia de seguridad predeterminado para este volumen** opción para volúmenes de StorSimple de hello, vaya demasiado**directivas de copia de seguridad** en Hola el servicio StorSimple Manager y crear una copia de seguridad adecuado directiva para todos los volúmenes de Hola. Recomendamos que establezca frecuencia Hola de copias de seguridad toohello punto objetivo recuperación (RPO) que desearía toosee para la aplicación hello.

### <a name="configure-hello-network"></a>Configurar red Hola
Para la máquina virtual del servidor de archivos de hello, configurar configuración de red en Azure Site Recovery para que redes de VM de Hola estén conectados toohello correcta recuperación ante desastres red después de la conmutación por error.

Puede seleccionar Hola VM en hello **replican elementos** ficha Configuración de red de hello tooconfigure, como se muestra en hello siguiente ilustración.

![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image2.png)

## <a name="create-a-recovery-plan"></a>Creación de un plan de recuperación
Puede crear un plan de recuperación en proceso de conmutación por error de ASR tooautomate Hola de recursos compartidos de archivos de Hola. Si se produce una interrupción, también puede abrir recursos compartidos de archivos de hello en unos minutos con un solo clic. tooenable esta automatización, necesitará una cuenta de automatización de Azure.

#### <a name="toocreate-an-automation-account"></a>toocreate una cuenta de automatización
1. Vaya toohello portal de Azure &gt; **automatización** sección.
2. Haga clic en el botón **+Agregar**, se abre la hoja siguiente.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image11.png)

   * Nombre: escriba una nueva cuenta de Automation.
   * Suscripción: elija la suscripción.
   * Grupo de recursos: seleccione un grupo de recursos existente o cree uno nuevo.
   * Ubicación - Elegir ubicación, tenga en hello mismo geográfica o región en que Hola crearon dispositivo de StorSimple en la nube y las cuentas de almacenamiento.
   * Crear cuenta de ejecución de Azure: seleccione la opción **Sí**.

3. Vaya toohello cuenta de automatización, haga clic en **Runbooks** &gt; **explorar la galería** tooimport Hola a todos requeridos runbooks en la cuenta de automatización de Hola.
4. Agregar Hola después runbooks mediante la búsqueda de **recuperación ante desastres** etiqueta en la Galería de hello:

   * Limpieza de los volúmenes de StorSimple después de la conmutación por error de prueba (TFO)
   * Conmutación por error de contenedores de volúmenes de StorSimple
   * Montaje de volúmenes en el dispositivo StorSimple después de la conmutación por error
   * Desinstalación de la extensión de script personalizada en la máquina virtual de Azure
   * Inicio de StorSimple Virtual Appliance

     ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image3.png)

5. Publicar todos los scripts de hello seleccionando Hola runbook en la cuenta de automatización de Hola y haga clic en **editar** &gt; **publicar** y, a continuación, **Sí** toohello comprobación Mensaje. Después de este paso, Hola **Runbooks** ficha aparecerá como sigue:

    ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image4.png)

6. En la cuenta de automatización de hello, seleccione hello **activos** ficha &gt; haga clic en **Variables** &gt; **agregar una variable** y agregue Hola después de las variables. Puede elegir tooencrypt estos activos. Estas variables son específicas del plan de recuperación. Si la recuperación del plan (que se creará en el paso siguiente Hola) se denomina plan de pruebas, las variables deben estar StorSimRegKey del plan de pruebas, AzureSubscriptionName del plan de pruebas y así sucesivamente.

   * *RecoveryPlanName***- StorSimRegKey**: clave de registro de hello de hello el servicio StorSimple Manager.
   * *RecoveryPlanName***AzureSubscriptionName -**: nombre de Hola de hello suscripción de Azure.
   * *RecoveryPlanName***- ResourceName**: nombre de Hola de hello recurso StorSimple con el dispositivo de StorSimple Hola.
   * *RecoveryPlanName***- DeviceName**: dispositivo Hola con toobe conmutación por error.
   * *RecoveryPlanName***- VolumeContainers**: una cadena separada por comas de los contenedores de volúmenes presente en el dispositivo de Hola que necesitan toobe error; por ejemplo, volcon1, volcon2, volcon3.
   * *RecoveryPlanName***- TargetDeviceName**: Hola dispositivo StorSimple en la nube de en qué Hola contenedores son toobe conmutación por error.
   * *RecoveryPlanName***- TargetDeviceDnsName**: nombre del servicio Hola Hola del dispositivo de destino (se puede encontrar en hello **Máquina Virtual** sección: nombre del servicio Hola Hola igual como Hola Nombre DNS).
   * *RecoveryPlanName***- StorageAccountName**: nombre de cuenta de almacenamiento de hello en qué secuencia de comandos de hello (que ha toorun en hello conmutado por error máquinas virtuales) se almacenará. Esto puede ser cualquier cuenta de almacenamiento que tenga algún script de Hola espacio toostore temporalmente.
   * *RecoveryPlanName***- StorageAccountKey**: clave de acceso de Hola de Hola por encima de la cuenta de almacenamiento.
   * *RecoveryPlanName***- ScriptContainer**: Hola nombre del contenedor de hello en qué hello secuencia de comandos se almacenará en la nube de Hola. Si no existe el contenedor de hello, se creará.
   * *RecoveryPlanName***- VMGUIDS**: al proteger una máquina virtual, Azure Site Recovery asigna cada VM un identificador único que proporciona detalles de Hola de hello conmutado por error máquinas virtuales. Hola tooobtain VMGUID, seleccione hello **servicios de recuperación** ficha y haga clic en **elemento protegido** &gt; **grupos de protección** &gt; **Máquinas** &gt; **propiedades**. Si tiene varias máquinas virtuales, a continuación, agregue Hola GUID como una cadena separada por comas.
   * *RecoveryPlanName***- AutomationAccountName** : hello nombre de la cuenta de automatización de hello en el que ha agregado Hola runbooks y activos de Hola.

  Por ejemplo, si hello nombre del plan de recuperación de hello es fileServerpredayRP, la **credenciales** & **Variables** pestañas deben aparecer como se indica a continuación después de agregar todos los activos de Hola.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image5.png)

7. Vaya toohello **servicios de recuperación** sección y almacén de Azure Site Recovery Hola select que creó anteriormente.
8. Seleccione hello **planes de recuperación (Site Recovery)** opción de **administrar** grupo y cree un nuevo plan de recuperación como sigue:

   a.  Haga clic en el botón **+ Plan de recuperación** y se abrirá la hoja siguiente.

      ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image6.png)

   b.  Escriba un nombre de plan de recuperación, elija valores del modelo de origen, destino e implementación.

   c.  Seleccione las máquinas virtuales de Hola Hola grupo de protección que desea tooinclude Hola plan de recuperación y haga clic en **Aceptar** botón.

   d.  Seleccione el plan de recuperación que creó anteriormente, haga clic en **personalizar** botón Vista de personalización de plan de recuperación de tooopen Hola.

   e.  Haga clic con el botón derecho en **Cierre de todos los grupos** y haga clic en **Agregar acción anterior**.

   f.  Abre la hoja de la acción de insertar, escriba un nombre, seleccione **lado principal** opción en donde toorun opción, seleccione la cuenta de automatización (en el que se agregan Hola runbooks) y, a continuación, seleccione hello  **Conmutación por error-StorSimple-contenedores de volúmenes** runbook.

   g.  Haga clic con el botón secundario en **grupo 1: iniciar** y haga clic en **agregar elementos protegidos** opción, a continuación, seleccione las máquinas virtuales de hello son toobe protegido en el plan de recuperación de Hola y haga clic en **Aceptar** botón. Opcional, si ya hay VM seleccionadas.

   h.  Haga clic con el botón secundario en **grupo 1: iniciar** y haga clic en **acción posterior a la** opción, a continuación, agregar todos Hola después de las secuencias de comandos:

   * Runbook Start-StorSimple-Virtual-Appliance
   * Runbook Fail over-StorSimple-volume-containers
   * Runbook Mount-volumes-after-failover
   * Runbook Uninstall-custom-script-extension

   i.  Agregar una acción manual después de hello por encima de 4 scripts Hola mismo **grupo 1: pasos posteriores a la** sección. Esta acción es el punto de hello en el que puede comprobar que todo funciona correctamente. Esta acción debe toobe agregar solamente como parte de la conmutación por error (por lo que solo determinado hello **conmutación por error de prueba** casilla de verificación).

   j.  Después de la acción manual de hello, agregar hello **limpieza** script mediante Hola mismo procedimiento que utilizó para hello otros runbooks. **Guardar** plan de recuperación de Hola.

    > [!NOTE]
    > Cuando se ejecuta una prueba de conmutación por error, debe comprobar todos los elementos en el paso de acción manual Hola porque una vez completada la acción manual de hello, se eliminarán como parte de la limpieza de hello volúmenes de StorSimple de Hola que tenían han clonado en el dispositivo de destino de Hola.
    >

    ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image7.png)

## <a name="perform-a-test-failover"></a>Realización de una conmutación por error de prueba
Consulte toohello [solución de recuperación ante desastres de Active Directory](../site-recovery/site-recovery-active-directory.md) guía complementaria de consideraciones específicas tooActive directorio durante la conmutación por error de prueba de Hola. el programa de instalación local de Hello no está distribuida en absoluto cuando se produce la conmutación por error de prueba de Hola. Hola volúmenes de StorSimple que se han adjuntado VM son clonado toohello dispositivo de StorSimple en la nube en Azure a local de toohello. Una máquina virtual para fines de prueba se arranca en Azure y volúmenes clonados hello son adjunto toohello máquina virtual.

#### <a name="tooperform-hello-test-failover"></a>conmutación por error tooperform Hola
1. Hola portal de Azure, seleccione el almacén de site recovery.
2. Haga clic en el plan de recuperación de hello creado para la máquina virtual del servidor de archivos de Hola.
3. Haga clic en **Probar conmutación por error**.
4. Seleccione hello toowhich de red virtual de Azure que se conectarán las máquinas virtuales de Azure después de producirse la conmutación por error.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image8.png)
5. Haga clic en **Aceptar** conmutación por error de toobegin Hola. Puede seguir el progreso haciendo clic en hello VM tooopen sus propiedades o en hello **trabajo de conmutación por error de prueba** en nombre del almacén de &gt; **trabajos** &gt; **detrabajosderecuperacióndesitio**.
6. Una vez completada la conmutación por error de hello, también debe poder réplica de hello toosee máquina Azure aparecen en hello portal de Azure &gt; **máquinas virtuales**. Puede realizar sus validaciones.
7. Una vez haya validaciones de hello, haga clic en **validaciones completa**. Este hello de limpieza will volúmenes de StorSimple y cierre Hola dispositivo de StorSimple en la nube.
8. Una vez que haya terminado, haga clic en **conmutación por error de prueba de limpieza** Hola plan de recuperación. En el registro de notas y guarde las observaciones asociadas con hello probar conmutación por error. Esto eliminará la máquina virtual de Hola que se crearon durante la conmutación por error de prueba.

## <a name="perform-a-planned-failover"></a>Realización de una conmutación por error planeada
   Durante una conmutación por error planeada, Hola local servidor de archivos que VM se apaga correctamente y una nube que se toma la instantánea de copia de seguridad de los volúmenes de hello en el dispositivo StorSimple. volúmenes de StorSimple Hola se conmutan por toohello dispositivo virtual, una réplica se plantea VM en Azure, y volúmenes de hello son adjunto toohello máquina virtual.

#### <a name="tooperform-a-planned-failover"></a>tooperform una conmutación por error planeada
1. Hola portal de Azure, seleccione **servicios de recuperación** almacén &gt; **planes de recuperación (recuperación de sitio)** &gt; **recoveryplan_name** creado para máquina virtual del servidor de archivos de Hola.
2. En la hoja de plan de recuperación de hello, haga clic en **más** &gt; **conmutación por error planeada**.  

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image9.png)
3. En hello **confirmar conmutación por error planeada** hoja, elija origen hello y ubicaciones de destino y red de destino Seleccione y haga clic en el proceso de conmutación por error de hello comprobación icono ✓ toostart Hola.
4. Una vez creadas las máquinas virtuales de réplica, pasan a estar en estado pendiente de confirmación. Haga clic en **confirmar** conmutación por error de toocommit Hola.
5. Una vez completada la replicación, hello las máquinas virtuales se inician en la ubicación secundaria Hola.

## <a name="perform-a-failover"></a>Realización de una conmutación por error
Durante una conmutación por error no planeada, los volúmenes de StorSimple Hola se conmutan por toohello dispositivo virtual, una réplica de máquina virtual aparecerá en Azure, y volúmenes de hello son adjunto toohello máquina virtual.

#### <a name="tooperform-a-failover"></a>tooperform una conmutación por error
1. Hola portal de Azure, seleccione **servicios de recuperación** almacén &gt; **planes de recuperación (recuperación de sitio)** &gt; **recoveryplan_name** creado para máquina virtual del servidor de archivos de Hola.
2. En la hoja de plan de recuperación de hello, haga clic en **más** &gt; **conmutación por error**.  
3. En hello **confirmar conmutación por error** hoja, elija el origen de Hola y ubicaciones de destino.
4. Seleccione **apagar máquinas virtuales y sincronizar los datos más recientes de hello** toospecify que Site Recovery debe intente tooshut hacia abajo de la máquina virtual de hello protegida y sincronizar datos de Hola para que hello versión más reciente de los datos de hello será conmutación por error.
5. Después de la conmutación por error de hello, hello las máquinas virtuales están en un estado de confirmación pendiente. Haga clic en **confirmar** conmutación por error de toocommit Hola.


## <a name="perform-a-failback"></a>Realización de una conmutación por recuperación
Durante una conmutación por recuperación, contenedores de volúmenes de StorSimple se conmutan por error dispositivo físico de back-toohello después de que se realiza una copia de seguridad.

#### <a name="tooperform-a-failback"></a>tooperform una conmutación por recuperación
1. Hola portal de Azure, seleccione **servicios de recuperación** almacén &gt; **planes de recuperación (Site Recovery)** &gt; **recoveryplan_name** creado para máquina virtual del servidor de archivos de Hola.
2. En la hoja de plan de recuperación de hello, haga clic en **más** &gt; **conmutación por error planeada**.  
3. Elegir ubicaciones de origen y destino de hello, sincronización de datos adecuada de select hello y opciones de creación de la máquina virtual.
4. Haga clic en **Aceptar** botón proceso de conmutación por recuperación de toostart Hola.

   ![](./media/storsimple-disaster-recovery-using-azure-site-recovery/image10.png)

## <a name="best-practices"></a>Prácticas recomendadas
### <a name="capacity-planning-and-readiness-assessment"></a>Evaluación de disponibilidad y planeamiento de capacidad
#### <a name="hyper-v-site"></a>Sitio de Hyper-V
Hola de uso [herramienta de planificación de capacidad de usuario](http://www.microsoft.com/download/details.aspx?id=39057) toodesign Hola servidor, el almacenamiento y la infraestructura de red de su entorno de réplica de Hyper-V.

#### <a name="azure"></a>Azure
Puede ejecutar hello [herramienta de evaluación de preparación para la máquina Virtual de Azure](http://azure.microsoft.com/downloads/vm-readiness-assessment/) en tooensure de máquinas virtuales que sean compatibles con máquinas virtuales de Azure y servicios de Azure Site Recovery. Herramienta de evaluación de preparación de Hello comprueba las configuraciones de máquina virtual y advierte cuando las configuraciones son incompatibles con Azure. Por ejemplo, emite una advertencia si la unidad C: es mayor de 127 GB.

El planeamiento de capacidad se compone de al menos dos procesos importantes:

* Asignación de máquinas virtuales de Hyper-V tooAzure tamaños de máquina virtual (por ejemplo, A6, A7, A8 y A9) en local.
* Determinar Hola requiere ancho de banda de Internet.

## <a name="limitations"></a>Limitaciones
* Actualmente, solo 1 dispositivo de StorSimple puede conmutar por error (tooa un solo dispositivo de StorSimple en la nube). escenario de Hola de un servidor de archivos que abarca varios dispositivos de StorSimple no se admite todavía.
* Si recibe un error al habilitar la protección de una máquina virtual, asegúrese de que haya desconectado los destinos iSCSI Hola.
* Todos los contenedores de volúmenes de Hola que agrupan debido a las directivas de copia de seguridad que abarca a contenedores de volúmenes conmutarán por error conjuntamente.
* Todos los volúmenes de hello en contenedores de volúmenes de hello que ha elegido se conmute por error.
* Volúmenes que se agregan toomore de 64 TB no se conmutarán por error porque su capacidad máxima de un único dispositivo de nube de StorSimple hello es 64 TB.
* Si se produce un error en la conmutación por error planeada o no planeada de Hola y Hola máquinas virtuales se crean en Azure, a continuación, realice la limpieza no Hola máquinas virtuales. En su lugar, realice una conmutación por recuperación. Si elimina hello las máquinas virtuales, a continuación, Hola local de las máquinas virtuales no se activan de nuevo.
* Después de una conmutación por error, si no se pueden toosee Hola volúmenes, vaya toohello las máquinas virtuales, abra Administración de discos, vuelva a examinar los discos de Hola y ponerlos en línea.
* En algunos casos, letras de unidad de hello en el sitio de recuperación ante desastres de hello pueden ser distinto de hello letras local. Si esto ocurre, deberá toomanually problema de hello correcto una vez finalizada la conmutación por error de Hola.
* La autenticación multifactor debe deshabilitarse para hello Azure credencial que se escribe en la cuenta de automatización de Hola como un recurso. Si no se deshabilita esta autenticación, las secuencias de comandos no se permitirán toorun automáticamente y se producirá un error en el plan de recuperación de Hola.
* Tiempo de espera de trabajo de conmutación por error: Hola StorSimple script superará el tiempo de espera si Hola conmutación por error de contenedores de volúmenes es más lento que el límite de Azure Site Recovery de Hola por script (actualmente 120 minutos).
* Tiempo de espera del trabajo de copia de seguridad: Hola StorSimple script agota el tiempo si copia de seguridad de Hola de volúmenes es más lento que el límite de Azure Site Recovery de Hola por script (actualmente 120 minutos).

  > [!IMPORTANT]
  > Ejecutar copia de seguridad de hello manualmente desde Hola portal de Azure y, a continuación, ejecute el plan de recuperación de Hola de nuevo.

* Clonar tiempo de espera de trabajo: Hola StorSimple script agota el tiempo si Hola clonación de volúmenes es más lento que el límite de Azure Site Recovery de Hola por script (actualmente 120 minutos).
* Error de sincronización de tiempo: Hola StorSimple errores que dice que las copias de seguridad de hello eran correctamente aunque la copia de seguridad de hello es correcta en el portal de hello las secuencias de comandos. Una posible causa de esto podría ser que tiempo del ese dispositivo de StorSimple Hola podría fuera sincronizada con hello hora actual en la zona horaria de Hola.

  > [!IMPORTANT]
  > Sincronización Hola hora del dispositivo con hello hora actual en la zona horaria de Hola.

* Error de conmutación por error de dispositivo: Hola StorSimple script puede producir un error si se produce una conmutación por error de dispositivo cuando se ejecuta el plan de recuperación de Hola.

  > [!IMPORTANT]
  > Una vez completada la conmutación por error de dispositivo de hello, vuelva a ejecutar el plan de recuperación de Hola.


## <a name="summary"></a>Resumen
Con Azure Site Recovery, puede crear un plan de recuperación ante desastres automatizado completo para una máquina virtual de servidor de archivos con recursos compartidos de archivos hospedados en el almacenamiento de StorSimple. Se puede iniciar la conmutación por error de hello en segundos desde cualquier lugar en Hola eventos de interrupción y poner la aplicación hello en ejecución dentro de unos minutos.
