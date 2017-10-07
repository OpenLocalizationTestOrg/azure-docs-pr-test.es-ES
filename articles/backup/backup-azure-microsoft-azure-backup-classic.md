---
title: "aaaUse tooback de servidor de copia de seguridad de Azure de portal clásico de cargas de trabajo tooAzure | Documentos de Microsoft"
description: "Asegúrese de que su entorno está preparado correctamente tooback seguridad cargas de trabajo utilizando el servidor de copia de seguridad de Azure"
services: backup
documentationcenter: 
author: pvrk
manager: shivamg
editor: 
keywords: "azure backup server; almacén de copia de seguridad"
ms.assetid: d86450e8-da63-4283-8fd7-2ee629fa14ab
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: masaran;trinadhk;pullabhk;markgal
ms.openlocfilehash: 7b574824c448096e0c0ba74a872ab8f2a434f6a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-using-azure-backup-server"></a>Preparar tooback seguridad cargas de trabajo utilizando el servidor de copia de seguridad de Azure
> [!div class="op_single_selector"]
> * [Servidor de Copia de seguridad de Azure](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure Backup Server (clásico)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (clásico)](backup-azure-dpm-introduction-classic.md)
>
>

Este artículo es sobre cómo preparar su tooback entorno seguridad cargas de trabajo utilizando el servidor de copia de seguridad de Azure. Con Azure Backup Server, puede proteger cargas de trabajo de aplicaciones como máquinas virtuales de Hyper-V, Microsoft SQL Server, SharePoint Server, Microsoft Exchange y clientes Windows desde una única consola:

> [!WARNING]
> Servidor de copia de seguridad de Azure hereda la funcionalidad de Hola de Data Protection Manager (DPM) para copia de seguridad de cargas de trabajo. Encontrará punteros tooDPM documentación para algunas de estas características. Sin embargo, Azure Backup Server no ofrece protección en cinta o integración con System Center.
>
>

## <a name="1-windows-server-machine"></a>1. Máquina de Windows Server
![step1](./media/backup-azure-microsoft-azure-backup/step1.png)

Hola primer paso hacia obtener Hola servidor de copia de seguridad de Azure y ejecutar es toohave una máquina de Windows Server.

| Ubicación | Requisitos mínimos | Instrucciones adicionales |
| --- | --- | --- |
| Azure |Máquina virtual de Azure IaaS<br><br>A2 Standard: 2 núcleos, 3,5 GB de RAM |Puede comenzar por una galería de imágenes sencilla de Windows Server 2012 R2 Datacenter. [La protección de cargas de trabajo de IaaS con Azure Backup Server (DPM)](https://technet.microsoft.com/library/jj852163.aspx) presenta numerosos matices. Asegúrese de leer el artículo de hello completamente antes de implementar la máquina de Hola. |
| Local |Máquina virtual de Hyper-V,<br> Máquina virtual de VMware<br> o un host físico<br><br>2 núcleos y 4 GB de RAM |Puede desduplicar el almacenamiento DPM de hello con desduplicación de Windows Server. Más información sobre cómo funcionan juntos [DPM y la desduplicación](https://technet.microsoft.com/library/dn891438.aspx) al implementarlos en máquinas virtuales de Hyper-V. |

> [!NOTE]
> Se recomienda instalar el Azure Backup Server en una máquina con Windows Server 2012 R2 Datacenter. Muchos de los requisitos previos de Hola se tratan automáticamente con la versión más reciente de Hola de sistema operativo de Windows hello.
>
>

Si tiene previsto dominio tooa de toojoin servidor de copia de seguridad de Azure, se recomienda unir Hola de servidor físico o una máquina virtual toohello dominio antes de instalar el software del servidor de copia de seguridad de Azure Hola. Mover un servidor de copia de seguridad de Azure tooa nuevo dominio, después de la implementación, es *no admite*.

## <a name="2-backup-vault"></a>2. Almacén de copia de seguridad
![step2](./media/backup-azure-microsoft-azure-backup/step2.png)

Si enviar datos de copia de seguridad tooAzure o mantenerlo localmente, Hola servidor de copia de seguridad de Azure debe ser almacén tooa registrados. Si es un usuario nuevo de la copia de seguridad de Azure y desea toouse servidor de copia de seguridad de Azure, vea hello Azure portal versión de este artículo - [preparar tooback seguridad cargas de trabajo utilizando el servidor de copia de seguridad de Azure](backup-azure-microsoft-azure-backup.md).

> [!IMPORTANT]
> A partir de marzo de 2017, no podrá usar almacenes de copia de seguridad de hello toocreate portal clásico.
> Ahora puede actualizar los almacenes de servicios de tooRecovery de almacenes de copia de seguridad. Para obtener más información, consulte el artículo de hello [actualizar un tooa de almacén de copia de seguridad del almacén de servicios de recuperación](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft le anima tooupgrade tooRecovery almacenes de servicios de almacenes de credenciales de la copia de seguridad.<br/> Después de 15 de octubre de 2017, no puede usar almacenes de copia de seguridad de toocreate de PowerShell. **El 1 de noviembre de 2017**:
>- Todos los almacenes de copia de seguridad restantes será almacenes de servicios de tooRecovery actualizado automáticamente.
>- No será capaz de tooaccess los datos de copia de seguridad en el portal clásico de Hola. En su lugar, use hello tooaccess portal Azure los datos de copia de seguridad en los almacenes de servicios de recuperación.
>



## <a name="3-software-package"></a>3. Paquete de software
![step3](./media/backup-azure-microsoft-azure-backup/step3.png)

### <a name="downloading-hello-software-package"></a>Descargar paquete de software de Hola
Credenciales toovault similar, puede descargar Microsoft Azure Backup para cargas de trabajo de aplicación de Hola **página Inicio rápido** de almacén de copia de seguridad de Hola.

1. Haga clic en **para las cargas de aplicaciones (disco tooDisk tooCloud)**. Esto le llevará página del centro de descarga de toohello desde donde se puede descargar el paquete de software de Hola.

    ![Pantalla de bienvenida de Microsoft Azure Backup](./media/backup-azure-microsoft-azure-backup/dpm-venus1.png)
2. Haga clic en **Descargar**.

    ![Centro de descarga 1](./media/backup-azure-microsoft-azure-backup/downloadcenter1.png)
3. Seleccione todos los archivos de Hola y haga clic en **siguiente**. Descarga que todos Hola archivos procedentes de la página de descarga de copia de seguridad de Microsoft Azure de Hola y Hola a todos los archivos en el lugar Hola misma carpeta.
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
2. En la pantalla de bienvenida de bienvenida, haga clic en hello **siguiente** botón. Esto le llevará toohello *Prerequisite Checks* sección. En esta pantalla, haga clic en hello **comprobar** botón toodetermine si se cumplen los requisitos previos de hardware y software de hello para el servidor de copia de seguridad de Azure. Si todos Hola son requisitos previos se cumplieron correctamente, verá un mensaje que indica que la máquina Hola cumple los requisitos de Hola. Haga clic en hello **siguiente** botón.

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

    Hola siguiente paso es hello tooconfigure agente de servicios de recuperación de Microsoft Azure. Como parte de la configuración de hello, deberá tooprovide el Hola almacén credenciales tooregister Hola máquina toohello almacén. También ofrecerá una frase de contraseña tooencrypt/descifrar Hola datos enviados entre Azure y sus instalaciones. Puede generar una frase de contraseña automáticamente o proporcionar la suya propia, con un mínimo de 16 caracteres. Continúe con el Asistente de hello hasta que se ha configurado el agente de Hola.

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
![step4](./media/backup-azure-microsoft-azure-backup/step4.png)

Servidor de copia de seguridad de Azure requiere el servicio de copia de seguridad de Azure toohello de conectividad para hello producto toowork correctamente. toovalidate si máquina hello tiene tooAzure de conectividad de hello, usar hello ```Get-DPMCloudConnection``` commandlet en la consola de servidor de copia de seguridad de Azure PowerShell Hola. Si hello salida de hello commandlet es TRUE, a continuación, existe una conexión, lo contrario, no hay conectividad.

En hello simultáneamente, Hola suscripción de Azure debe toobe en un estado correcto. toofind el estado de saludo de su suscripción y toomanage lo, inicio de sesión toohello [portal de suscripción](https://account.windowsazure.com/Subscriptions).

Una vez que sepa el estado de Hola de hello Azure conectividad y de hello suscripción de Azure, puede usar tabla hello toofind out impacto hello en la funcionalidad de copia de seguridad/restauración de Hola que ofrece.

| Estado de conectividad | Suscripción de Azure | Copia de seguridad tooAzure | Copia de seguridad toodisk | Restauración desde Azure | Restauración desde disco |
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
