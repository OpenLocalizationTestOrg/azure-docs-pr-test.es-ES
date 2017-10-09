---
title: aaaUse tooback de servidor de copia de seguridad de Azure de las cargas de trabajo tooAzure | Documentos de Microsoft
description: Usar el servidor de copia de seguridad de Azure tooprotect o respaldar las cargas de trabajo toohello portal de Azure.
services: backup
documentationcenter: 
author: PVRK
manager: shivamg
editor: 
keywords: servidor de copia de seguridad de Azure; proteger cargas de trabajo; copias de seguridad de cargas de trabajo
ms.assetid: e7fb1907-9dc1-4ca1-8c61-50423d86540c
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: a99b2919ffd44c6133960e3a935038a2bb1281c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>Preparar tooback seguridad cargas de trabajo utilizando el servidor de copia de seguridad de Azure
> [!div class="op_single_selector"]
> * [Servidor de Copia de seguridad de Azure](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
>
>

Este artículo se explica cómo tooprepare su tooback entorno seguridad cargas de trabajo utilizando el servidor de copia de seguridad de Azure. Con Azure Backup Server, puede proteger cargas de trabajo de aplicaciones como máquinas virtuales de Hyper-V, Microsoft SQL Server, SharePoint Server, Microsoft Exchange y clientes Windows desde una única consola.

> [!NOTE]
> El servidor de copia de seguridad de Azure ahora puede proteger máquinas virtuales de VMware y proporciona mejores funcionalidades de seguridad. Instalar el producto de hello tal como se describe en secciones de hello siguientes; aplicar actualizaciones 1 y Hola a agente de copia de seguridad más reciente de Azure. toolearn más información acerca de la copia de seguridad de servidores de VMware con el servidor de copia de seguridad de Azure, vea el artículo de hello, [tooback de servidor de copia de seguridad de Azure de uso de un servidor de VMware](backup-azure-backup-server-vmware.md). toolearn acerca de las capacidades de seguridad, consulte demasiado[documentación de características de seguridad de copia de seguridad de Azure](backup-azure-security-feature.md).
>
>

También puede proteger las cargas de trabajo de Infraestructura como servicio (IaaS), como es el caso de las máquinas virtuales de Azure.

> [!NOTE]
> Azure cuenta con dos modelos de implementación para crear recursos y trabajar con ellos: [Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md). Este artículo proporciona información de Hola y procedimientos para restaurar máquinas virtuales implementadas mediante el modelo de administrador de recursos de Hola.
>
>

Servidor de copia de seguridad de Azure hereda la mayor parte de la funcionalidad de copia de seguridad de cargas de trabajo de Hola de Data Protection Manager (DPM). En este artículo se vincula tooDPM documentación tooexplain algunos Hola funcionalidad comparten. Aunque el servidor de copia de seguridad de Azure comparten gran parte de hello misma funcionalidad que DPM. Servidor de copia de seguridad de Azure no respaldar tootape ni se integra con System Center.

## <a name="1-choose-an-installation-platform"></a>1. Elección de una plataforma de instalación
Hola primer paso hacia obtener Hola servidor de copia de seguridad de Azure y ejecutar es tooset de un servidor de Windows. El servidor puede estar en Azure o en el entorno local.

### <a name="using-a-server-in-azure"></a>Uso de un servidor en Azure
Al elegir un servidor para ejecutar el servidor de Copia de seguridad de Azure, se recomienda comenzar con una imagen de la galería de Windows Server 2012 R2 Datacenter. artículo de Hello, [crear la primera máquina virtual de Windows en el portal de Azure hello](../virtual-machines/virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), proporciona un tutorial de introducción a Hola recomienda la máquina virtual de Azure, incluso si nunca ha utilizado Azure antes. Hola recomienda requisitos mínimos para la máquina virtual de servidor hello (VM) debe ser: A2 estándar con dos núcleos y 3,5 GB de RAM.

La protección de cargas de trabajo con el servidor de Copia de seguridad de Azure tiene muchos matices. artículo de Hello, [instalar DPM como una máquina virtual de Azure](https://technet.microsoft.com/library/jj852163.aspx), le ayudará a comprender estas matices. Antes de implementar la máquina de hello, leer este artículo en su totalidad.

### <a name="using-an-on-premises-server"></a>Uso de un servidor local
Si no desea que toorun Hola base servidor en Azure, puede ejecutar el servidor de hello en una máquina virtual de Hyper-V, una VM de VMware o en un host físico. Hola recomienda requisitos mínimos de hardware del servidor hello son dos núcleos y 4 GB de RAM. Hola admitida los sistemas operativos se muestran en hello en la tabla siguiente:

| Sistema operativo | Plataforma | SKU |
|:--- | --- |:--- |
| Windows Server 2012 R2 y SP más recientes |64 bits |Standard, Datacenter, Foundation |
| Windows Server 2012 y SP más recientes |64 bits |Datacenter, Foundation, Standard |
| Windows Storage Server 2012 R2 y SP más recientes |64 bits |Standard, Workgroup |
| Windows Storage Server 2012 y SP más recientes |64 bits |Standard, Workgroup |

Puede desduplicar el almacenamiento DPM de hello con desduplicación de Windows Server. Más información sobre cómo funcionan juntos [DPM y la desduplicación](https://technet.microsoft.com/library/dn891438.aspx) al implementarlos en máquinas virtuales de Hyper-V.

> [!NOTE]
> Servidor de copia de seguridad de Azure está diseñado toorun en un servidor dedicado de propósito único. No se puede instalar Azure Backup Server en:
> - Un equipo que se ejecuta como controlador de dominio
> - Un equipo en qué servidor de aplicaciones de hello rol está instalado
> - Un equipo que sea un grupo de administración de System Center Operations Manager
> - Un equipo en el que se ejecute Exchange Server
> - Un equipo que sea un nodo de un clúster

Unirse a dominio de tooa del servidor de copia de seguridad de Azure. Si tiene previsto dominio diferente del tooa toomove Hola server, se recomienda que unirse Hola server toohello nuevo dominio antes de instalar el servidor de copia de seguridad de Azure. Mover un servidor de copia de seguridad de Azure existente máquina tooa nuevo dominio después de la implementación es *no admite*.

## <a name="2-recovery-services-vault"></a>2. Almacén de Recovery Services
Si enviar datos de copia de seguridad tooAzure o mantenerlo localmente, software de hello necesita tooAzure toobe conectado. toobe más específica, el equipo del servidor de copia de seguridad de Azure de hello debe toobe registrado con un almacén de servicios de recuperación.

almacén de servicios de toocreate una recuperación:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú del concentrador hello, haga clic en **examinar** y en la lista de Hola de recursos, escriba **servicios de recuperación**. Cuando empiece a escribir, Hola filtros de la lista con los datos especificados. Haga clic en **Almacén de Servicios de recuperación**.

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png) <br/>

    se muestra la lista de Hola de almacenes de servicios de recuperación.
3. En hello **servicios de recuperación de los almacenes de credenciales** menú, haga clic en **agregar**.

    ![Creación del almacén de Servicios de recuperación, paso 2](./media/backup-azure-microsoft-azure-backup/rs-vault-menu.png)

    Servicios de recuperación de Hello del almacén se abre de hoja, que le pide que tooprovide una **nombre**, **suscripción**, **grupo de recursos**, y **ubicación**.

    ![Creación del almacén de Servicios de recuperación, paso 5](./media/backup-azure-microsoft-azure-backup/rs-vault-attributes.png)
4. Para **nombre**, escriba en el almacén de hello tooidentify un nombre descriptivo. nombre de Hello debe toobe único para hello suscripción de Azure. Escriba un nombre que tenga entre 2 y 50 caracteres. Debe comenzar por una letra y solo puede contener letras, números y guiones.
5. Haga clic en **suscripción** lista disponible de hello toosee de suscripciones. Si no está seguro de qué toouse de suscripción, utilice Hola predeterminado (o sugiere) suscripción. Solo hay varias opciones si la cuenta de su organización está asociada a más de una suscripción de Azure.
6. Haga clic en **grupo de recursos** toosee Hola lista de grupos de recursos disponibles, o haga clic en **New** toocreate un nuevo grupo de recursos. Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
7. Haga clic en **ubicación** región geográfica de tooselect hello para el almacén de Hola.
8. Haga clic en **Crear**. Puede tardar unos instantes para hello toobe creado del almacén de servicios de recuperación. Supervisar las notificaciones de estado de hello en el área superior de derecho hello en el portal de Hola.
   Una vez creado el almacén, se abre en el portal de Hola.

### <a name="set-storage-replication"></a>Configuración de la replicación de almacenamiento
opción de replicación de almacenamiento de Hello permite toochoose entre el almacenamiento con redundancia geográfica y almacenamiento con redundancia local. De forma predeterminada, el almacén tiene almacenamiento con redundancia geográfica. Si este almacén es el almacén principal, deje Hola almacenamiento opción set toogeo el almacenamiento con redundancia. Elija el almacenamiento con redundancia local si desea una opción más económica que no sea tan duradera. Obtenga más información sobre [con redundancia geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) y [localmente redundante](../storage/common/storage-redundancy.md#locally-redundant-storage) opciones de almacenamiento en hello [información general sobre la replicación de almacenamiento de Azure](../storage/common/storage-redundancy.md).

configuración de replicación de almacenamiento de Hola tooedit:

1. Seleccione el panel de almacén de credenciales de almacén tooopen hello y hoja de configuración de Hola. Si hello **configuración** hoja no se abre, haga clic en **toda la configuración de** en el panel del almacén de Hola.
2. En hello **configuración** hoja, haga clic en **infraestructura de copia de seguridad** > **configuración de copia de seguridad** tooopen hello **configuración de copia de seguridad** hoja. En hello **configuración de copia de seguridad** hoja, elija la opción de replicación de almacenamiento de hello para el almacén.

    ![Lista de copias de seguridad](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    Después de elegir la opción de almacenamiento de hello para el almacén, está listo tooassociate Hola VM con el almacén de Hola. asociación de hello toobegin, debería detectar y registrar Hola máquinas virtuales de Azure.

## <a name="3-software-package"></a>3. Paquete de software
### <a name="downloading-hello-software-package"></a>Descargar paquete de software de Hola
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Si ya tiene un almacén de servicios de recuperación abierto, continúe toostep 3. Si no tiene un abierto de almacén de servicios de recuperación, pero están en hello portal de Azure, en el menú del concentrador hello, haga clic en **examinar**.

   * En la lista de Hola de recursos, escriba **servicios de recuperación**.
   * Cuando empiece a escribir, se filtrará la lista de hello en función de los datos especificados. Haga clic en **Almacenes de Recovery Services**cuando lo vea.

     ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-azure-microsoft-azure-backup/open-recovery-services-vault.png)

     aparece en la lista de Hola de almacenes de servicios de recuperación.
   * En lista de Hola de almacenes de servicios de recuperación, seleccione un almacén.

     de este modo se abrirá el panel de Hello almacén seleccionado.

     ![Hoja del almacén abierta](./media/backup-azure-microsoft-azure-backup/vault-dashboard.png)
3. Hola **configuración** hoja se abre de forma predeterminada. Si está cerrado, haga clic en **configuración** hoja de configuración de tooopen Hola.

    ![Hoja del almacén abierta](./media/backup-azure-microsoft-azure-backup/vault-setting.png)
4. Haga clic en **copia de seguridad** Asistente para introducción de tooopen Hola.

    ![Introducción a la copia de seguridad](./media/backup-azure-microsoft-azure-backup/getting-started-backup.png)

    Hola **Introducción a la copia de seguridad** hoja que se abre, **objetivos de copia de seguridad** estará seleccionado automáticamente.

    ![Backup-goals-default-opened](./media/backup-azure-microsoft-azure-backup/getting-started.png)

5. Hola **objetivo de copia de seguridad** hoja de hello **donde se está ejecutando la carga de trabajo** menú, seleccione **local**.

    ![entorno local y cargas de trabajo como objetivos](./media/backup-azure-microsoft-azure-backup/backup-goals-azure-backup-server.png)

    De hello **especifique qué desea toobackup?** menú desplegable, las cargas de trabajo de hello select que desee tooprotect utilizando el servidor de copia de seguridad de Azure y, a continuación, haga clic en **Aceptar**.

    Hola **Introducción a la copia de seguridad** Asistente conmutadores hello **preparar la infraestructura** tooback opción seguridad tooAzure de cargas de trabajo.

   > [!NOTE]
   > Si solo desea tooback seguridad de archivos y carpetas, se recomienda con el agente de copia de seguridad de Azure de Hola y Hola instrucciones en el artículo de hello, [primer vistazo: copia de seguridad de archivos y carpetas](backup-try-azure-backup-in-10-mins.md). Si va tooprotect en un futuro hello, seleccione más de los archivos y carpetas o va a protección de hello tooexpand necesita las cargas de trabajo.
   >
   >

    ![Cambio del Asistente para introducción](./media/backup-azure-microsoft-azure-backup/getting-started-prep-infra.png)

6. Hola **preparar infraestructura** hoja que aparece, haga clic en hello **descargar** vínculos para instalar el servidor de copia de seguridad de Azure y descargar credenciales de almacén. Utilice las credenciales de almacén de Hola durante el registro del almacén de servicios de recuperación de toohello de servidor de copia de seguridad de Azure. vínculos de Hello permitirán toohello donde hello paquete de software se puede descargar el centro de descarga.

    ![Preparación de la infraestructura del Servidor de Copia de seguridad de Azure](./media/backup-azure-microsoft-azure-backup/azure-backup-server-prep-infra.png)

7. Seleccione todos los archivos de Hola y haga clic en **siguiente**. Descarga que todos Hola archivos procedentes de la página de descarga de copia de seguridad de Microsoft Azure de Hola y Hola a todos los archivos en el lugar Hola misma carpeta.

    ![Centro de descarga 1](./media/backup-azure-microsoft-azure-backup/downloadcenter.png)

    Puesto que hello tamaño de descarga de todos los archivos de hello juntos > 3G, en un vínculo de descarga de 10 Mbps puede llevar hasta too60 minutos para hello descargan toocomplete.

### <a name="extracting-hello-software-package"></a>Extraer el paquete de software de Hola
Una vez que haya descargado todos los archivos de hello, haga clic en **MicrosoftAzureBackupInstaller.exe**. Esto iniciará hello **el Asistente para la instalación de Microsoft Azure copia de seguridad** el programa de instalación de tooextract Hola archivos ubicación tooa especificado por el usuario. Continuar con el Asistente de Hola y haga clic en hello **extraer** botón proceso de extracción de toobegin Hola.

> [!WARNING]
> Al menos 4GB de espacio libre es necesario tooextract Hola los archivos de instalación.
>
>

![Asistente para instalación de Microsoft Azure Backup](./media/backup-azure-microsoft-azure-backup/extract/03.png)

Una vez el proceso de extracción de hello completando, verificación Hola cuadro toolaunch Hola recién extraído *setup.exe* toobegin instalar el servidor de copia de seguridad de Microsoft Azure y haga clic en hello **finalizar** botón.

### <a name="installing-hello-software-package"></a>Instalar el paquete de software de Hola
1. Haga clic en **copia de seguridad de Microsoft Azure** Asistente para la instalación de toolaunch Hola.

    ![Asistente para instalación de Microsoft Azure Backup](./media/backup-azure-microsoft-azure-backup/launch-screen2.png)
2. En la pantalla de bienvenida de bienvenida, haga clic en hello **siguiente** botón. Esto le llevará toohello *Prerequisite Checks* sección. En esta pantalla, haga clic en **comprobar** toodetermine si se cumplen los requisitos previos de hardware y software de hello para el servidor de copia de seguridad de Azure. Si todos los requisitos previos se cumplen correctamente, verá un mensaje que indica que la máquina Hola cumple los requisitos de Hola. Haga clic en hello **siguiente** botón.

    ![Azure Backup Server - Bienvenida y requisitos previos](./media/backup-azure-microsoft-azure-backup/prereq/prereq-screen2.png)
3. Servidor de copia de seguridad de Microsoft Azure requiere SQL Server Standard y paquete de instalación del servidor de copia de seguridad de Azure de hello viene incluido con los binarios de SQL Server adecuados Hola necesitados. Cuando se inicia con una nueva instalación de servidor de copia de seguridad de Azure, debe elegir la opción de hello **instalar nueva instancia de SQL Server con este programa de instalación** y haga clic en hello **comprobar e instalar** botón. Una vez que los requisitos previos de Hola se instalaron correctamente, haga clic en **siguiente**.

    ![Azure Backup Server - Comprobación de SQL](./media/backup-azure-microsoft-azure-backup/sql/01.png)

    Si se produce un error con una máquina de recomendación toorestart hello, hacerlo y haga clic en **comprobar de nuevo**.

   > [!NOTE]
   > Azure Backup Server no funcionará con una instancia remota de SQL Server. instancia de Hola que se utiliza por servidor de copia de seguridad de Azure debe toobe local.
   >
   >
4. Proporcionar una ubicación para la instalación de Hola de archivos del servidor de copia de seguridad de Microsoft Azure y haga clic en **siguiente**.

    ![Requisitos previos de Microsoft Azure Backup2](./media/backup-azure-microsoft-azure-backup/space-screen.png)

    ubicación del borrador Hello es un requisito para copia de seguridad tooAzure. Asegúrese de ubicación del borrador hello es al menos del 5% de los datos de hello planeada toobe copia toohello en la nube. Para la protección de disco, es necesario toobe configuran una vez que finalice la instalación de hello discos independientes. Para obtener más información acerca de los grupos de almacenamiento, consulte [Configuración de bloques de almacenamiento y almacenamiento en disco](https://technet.microsoft.com/library/hh758075.aspx).
5. Proporcione una contraseña segura para las cuentas de usuario locales con permisos restringidos y haga clic en **Next**(Siguiente).

    ![Requisitos previos de Microsoft Azure Backup2](./media/backup-azure-microsoft-azure-backup/security-screen.png)
6. Seleccione si desea toouse *Microsoft Update* toocheck si hay actualizaciones y haga clic en **siguiente**.

   > [!NOTE]
   > Se recomienda tener Windows Update redirigir tooMicrosoft actualización, lo que ofrece seguridad y actualizaciones importantes para Windows y otros productos, como servidor de copia de seguridad de Microsoft Azure.
   >
   >

    ![Requisitos previos de Microsoft Azure Backup2](./media/backup-azure-microsoft-azure-backup/update-opt-screen2.png)
7. Hola de revisión *resumen de la configuración* y haga clic en **instalar**.

    ![Requisitos previos de Microsoft Azure Backup2](./media/backup-azure-microsoft-azure-backup/summary-screen.png)
8. instalación de Hello sucede en fases. Hola Hola de fase primer agente de servicios de recuperación de Microsoft Azure está instalado en el servidor de Hola. Asistente de Hello también comprueba si la conectividad a Internet. Si está disponible la conectividad a Internet puede continuar con la instalación, si no, debe tooprovide proxy detalles tooconnect toohello Internet.

    Hola siguiente paso es hello tooconfigure agente de servicios de recuperación de Microsoft Azure. Como parte de la configuración de hello, tendrá tooprovide los servicios de recuperación almacén credenciales tooregister Hola máquina toohello almacén. También ofrecerá una frase de contraseña tooencrypt/descifrar Hola datos enviados entre Azure y sus instalaciones. Puede generar una frase de contraseña automáticamente o proporcionar la suya propia, con un mínimo de 16 caracteres. Continúe con el Asistente de hello hasta que se ha configurado el agente de Hola.

    ![Requisitos previos de Azure Backup Server2](./media/backup-azure-microsoft-azure-backup/mars/04.png)
9. Una vez se complete correctamente el registro del servidor de copia de seguridad de Microsoft Azure hello, hello general Asistente para la instalación continúa toohello instalación y configuración de SQL Server y los componentes de servidor de copia de seguridad de Azure Hola. Una vez completada la instalación de componentes de SQL Server de Hola, se instalan los componentes de servidor de copia de seguridad de Azure Hola.

    ![Azure Backup Server](./media/backup-azure-microsoft-azure-backup/final-install/venus-installation-screen.png)

Cuando haya finalizado el paso de instalación de hello, hello iconos del escritorio del producto se habrá creados así. Hacer doble clic en el producto de hello icono toolaunch Hola.

### <a name="add-backup-storage"></a>Incorporación de almacenamiento de copia de seguridad
copia de seguridad primera Hola se mantiene en almacenamiento conectado toohello máquina del servidor de copia de seguridad de Azure. Para obtener más información acerca de los discos, consulte [Configuración de bloques de almacenamiento y almacenamiento en disco](https://technet.microsoft.com/library/hh758075.aspx).

> [!NOTE]
> Se necesita almacenamiento de copia de seguridad de tooadd incluso si tiene previsto toosend datos tooAzure. En la arquitectura actual de saludo del servidor de copia de seguridad de Azure, el almacén de copia de seguridad de Azure hello contiene hello *segundo* copia de datos de hello mientras almacenamiento local de hello contiene Hola primera (y obligatoria) copia de seguridad.
>
>

## <a name="4-network-connectivity"></a>4. Conectividad de red
Servidor de copia de seguridad de Azure requiere el servicio de copia de seguridad de Azure toohello de conectividad para hello producto toowork correctamente. toovalidate si máquina hello tiene tooAzure de conectividad de hello, usar hello ```Get-DPMCloudConnection``` cmdlet en la consola de servidor de copia de seguridad de Azure PowerShell Hola. Si hello salida del cmdlet de hello es TRUE, a continuación, existe una conexión, lo contrario, no hay conectividad.

En hello simultáneamente, Hola suscripción de Azure debe toobe en un estado correcto. toofind el estado de saludo de su suscripción y toomanage lo, inicio de sesión toohello [portal de suscripción](https://account.windowsazure.com/Subscriptions).

Una vez que sepa el estado de Hola de hello Azure conectividad y de hello suscripción de Azure, puede usar tabla hello toofind out impacto hello en la funcionalidad de copia de seguridad/restauración de Hola que ofrece.

| Estado de conectividad | Suscripción de Azure | Hacer copia de seguridad tooAzure | Hacer copia de seguridad toodisk | Restauración desde Azure | Restauración desde disco |
| --- | --- | --- | --- | --- | --- |
| Conectado |Active |Permitida |Permitida |Permitida |Permitida |
| Conectado |Expirada |Stopped |Stopped |Permitida |Permitida |
| Conectado |Desaprovisionada |Stopped |Stopped |Detenida y puntos de recuperación de Azure eliminados |Stopped |
| Pérdida de conectividad > 15 días |Active |Stopped |Stopped |Permitida |Permitida |
| Pérdida de conectividad > 15 días |Expirada |Stopped |Stopped |Permitida |Permitida |
| Pérdida de conectividad > 15 días |Desaprovisionada |Stopped |Stopped |Detenida y puntos de recuperación de Azure eliminados |Stopped |

### <a name="recovering-from-loss-of-connectivity"></a>Recuperación de una pérdida de conectividad
Si tiene un firewall o un proxy que impide el acceso tooAzure, necesita hello toowhitelist después de direcciones de dominio en el perfil de firewall/proxy hello:

* www.msftncsi.com
* \*.Microsoft.com
* \*.WindowsAzure.com
* \*.microsoftonline.com
* \*.windows.net

Una vez conectividad tooAzure ha sido restaurada toohello máquina de servidor de copia de seguridad de Azure, operaciones de Hola que pueden realizarse dependen de hello estado de suscripción de Azure. tabla de Hello anterior incluye detalles acerca de las operaciones de hello permitidas una vez máquina hello es "conectado".

### <a name="handling-subscription-states"></a>Control de los estados de la suscripción
Es posible tootake una suscripción de Azure desde una *expirado* o *Deprovisioned* estado toohello *Active* estado. Sin embargo esto tiene algunas implicaciones en el comportamiento del producto Hola aunque no es el estado de hello *Active*:

* A *Deprovisioned* suscripción pierde la funcionalidad de período de Hola se desaprovisiona. En cambio *Active*, se restableció la funcionalidad del producto Hola de copia de seguridad/restauración. datos de copia de seguridad de Hello en el disco local de hello también se pueden recuperar si se ha conservado con un período de retención lo suficientemente grande. Sin embargo, se pierden todavía se puede datos de copia de seguridad de hello en Azure una vez Hola entra en hello *Deprovisioned* estado.
* Una suscripción con estado *Expirado* solo pierde la funcionalidad hasta que pase de nuevo al estado *Activo*. Las copias de seguridad programadas para el período de Hola que Hola suscripción era *expirado* no se ejecutará.

## <a name="troubleshooting"></a>Solución de problemas
Si el servidor de copia de seguridad de Microsoft Azure con errores se produce un error durante la fase de la instalación de hello (o copia de seguridad o restauración), consulte toothis [documento de códigos de error](https://support.microsoft.com/kb/3041338) para obtener más información.
También puede hacer referencia demasiado[preguntas más frecuentes relacionados con la copia de seguridad de Azure](backup-azure-backup-faq.md)

## <a name="next-steps"></a>Pasos siguientes
También puede obtener información detallada sobre [preparar el entorno para que DPM](https://technet.microsoft.com/library/hh758176.aspx) en el sitio de Microsoft TechNet Hola. También contiene información sobre las configuraciones admitidas en las que se puede implementar y usar Azure Backup Server.

Puede usar estos toogain artículos una comprensión más profunda de protección de cargas de trabajo usando el servidor de copia de seguridad de Microsoft Azure.

* [Copia de seguridad de SQL Server](backup-azure-backup-sql.md)
* [Copia de seguridad de una granja de SharePoint](backup-azure-backup-sharepoint.md)
* [Copia de seguridad de otro servidor](backup-azure-alternate-dpm-server.md)
