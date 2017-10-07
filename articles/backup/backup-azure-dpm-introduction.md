---
title: aaaUse DPM tooback de portal de cargas de trabajo tooAzure | Documentos de Microsoft
description: "Un toobacking de introducción de los servidores DPM con el servicio de copia de seguridad de Azure Hola"
services: backup
documentationcenter: 
author: adigan
manager: nkolli
editor: 
keywords: System Center Data Protection Manager, Data Protection Manager, copia de seguridad de DPM
ms.assetid: c8c322cf-f5eb-422c-a34c-04a4801bfec7
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: adigan;giridham;jimpark;markgal;trinadhk
ms.openlocfilehash: 1dd988ae55012ac7dc485d2416458542c60b6ae3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="preparing-tooback-up-workloads-tooazure-with-dpm"></a>Preparar tooback una tooAzure de las cargas de trabajo con DPM
> [!div class="op_single_selector"]
> * [Servidor de Copia de seguridad de Azure](backup-azure-microsoft-azure-backup.md)
> * [SCDPM](backup-azure-dpm-introduction.md)
> * [Azure Backup Server (clásico)](backup-azure-microsoft-azure-backup-classic.md)
> * [SCDPM (clásico)](backup-azure-dpm-introduction-classic.md)
>
>

Este artículo proporciona una tooprotect de copia de seguridad de Microsoft Azure toousing de introducción de los servidores de System Center Data Protection Manager (DPM) y las cargas de trabajo. Cuando lo lea, comprenderá:

* Cómo funciona la copia de seguridad de servidor DPM de Azure
* requisitos previos de Hello tooachieve una experiencia sin problemas de copia de seguridad
* Hola típicos errores detectados y cómo toodeal con ellos
* Escenarios admitidos

> [!NOTE]
> Azure cuenta con dos modelos de implementación para crear recursos y trabajar con ellos: [Resource Manager y el modelo clásico](../azure-resource-manager/resource-manager-deployment-model.md). Este artículo proporciona información de Hola y procedimientos para restaurar máquinas virtuales implementadas mediante el modelo de administrador de recursos de Hola.
>
>

Datos de aplicación y archivo de copia de seguridad de System Center DMP. Datos de copia de seguridad tooDPM se pueden almacenar en cinta, en el disco, o copias de seguridad tooAzure con copia de seguridad de Microsoft Azure. DPM interactúa con Azure Backup de la manera siguiente:

* **DPM implementado como una máquina de virtual server o de forma local física** : Si DPM se implementa como un servidor físico o como máquina virtual de Hyper-V local puede realizar copias de seguridad de datos tooa servicios de recuperación además del almacén de toodisk y copia de seguridad en cinta.
* **DPM implementado como una máquina virtual de Azure** : desde System Center 2012 R2 con Update 3, DPM puede implementarse como una máquina virtual de Azure. Si DPM se implementa como una máquina virtual de Azure, puede realizar copias de seguridad datos tooAzure discos conectados máquina virtual de Azure de DPM de toohello o puede descargar el almacenamiento de datos de hello al hacer una copia de seguridad tooa que del almacén de servicios de recuperación.

## <a name="why-backup-from-dpm-tooazure"></a>¿Por qué copia de seguridad de DPM tooAzure?
ventajas empresariales de Hola de copia de seguridad de servidores DPM mediante copia de seguridad de Azure incluyen:

* Para la implementación local de DPM, puede usar Azure como un tootape de implementación toolong-término alternativo.
* Para las implementaciones de DPM en Azure, copia de seguridad de Azure permite almacenamiento toooffload de hello disco de Azure, permitiéndole tooscale seguridad almacenando datos antiguos en el almacén de servicios de recuperación y los datos nuevos en el disco.

## <a name="prerequisites"></a>Requisitos previos
Preparar la copia de seguridad de Azure tooback datos de DPM como se indica a continuación:

1. **Crear un almacén de Servicios de recuperación** : cree un almacén en el Portal de Azure.
2. **Descargar las credenciales de almacén** : descargar credenciales de Hola que use tooregister Hola DPM server tooRecovery del almacén de servicios.
3. **Instalar el agente de copia de seguridad de Azure de Hola** : de Azure Backup, instalar el agente de hello en cada servidor DPM.
4. **Registrar servidor hello** : almacén de servicios de registro de hello DPM server tooRecovery.

### <a name="1-create-a-recovery-services-vault"></a>1. Creación de un almacén de Servicios de recuperación
almacén de servicios de toocreate una recuperación:

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. En el menú del concentrador hello, haga clic en **examinar** y en la lista de Hola de recursos, escriba **servicios de recuperación**. Cuando empiece a escribir, se filtrará la lista de hello en función de los datos especificados. Haga clic en **Almacén de Servicios de recuperación**.

    ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-azure-dpm-introduction/open-recovery-services-vault.png)

    se muestra la lista de Hola de almacenes de servicios de recuperación.
3. En hello **servicios de recuperación de los almacenes de credenciales** menú, haga clic en **agregar**.

    ![Creación del almacén de Servicios de recuperación, paso 2](./media/backup-azure-dpm-introduction/rs-vault-menu.png)

    Servicios de recuperación de Hello del almacén se abre de hoja, que le pide que tooprovide una **nombre**, **suscripción**, **grupo de recursos**, y **ubicación**.

    ![Creación del almacén de Servicios de recuperación, paso 5](./media/backup-azure-dpm-introduction/rs-vault-attributes.png)
4. Para **nombre**, escriba en el almacén de hello tooidentify un nombre descriptivo. nombre de Hello debe toobe único para hello suscripción de Azure. Escriba un nombre que tenga entre 2 y 50 caracteres. Debe comenzar por una letra y solo puede contener letras, números y guiones.
5. Haga clic en **suscripción** lista disponible de hello toosee de suscripciones. Si no está seguro de qué toouse de suscripción, utilice Hola predeterminado (o sugiere) suscripción. Solo habrá varias opciones si la cuenta de su organización está asociada a varias suscripciones de Azure.
6. Haga clic en **grupo de recursos** toosee Hola lista de grupos de recursos disponibles, o haga clic en **New** toocreate un nuevo grupo de recursos. Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
7. Haga clic en **ubicación** región geográfica de tooselect hello para el almacén de Hola.
8. Haga clic en **Crear**. Puede tardar unos instantes para hello toobe creado del almacén de servicios de recuperación. Supervisar las notificaciones de estado de hello en el área superior de derecho hello en el portal de Hola.
   Una vez creado el almacén, se abre en el portal de Hola.

### <a name="set-storage-replication"></a>Configuración de la replicación de almacenamiento
opción de replicación de almacenamiento de Hello permite toochoose entre el almacenamiento con redundancia geográfica y almacenamiento con redundancia local. De forma predeterminada, el almacén tiene almacenamiento con redundancia geográfica. Deje Hola opción set toogeo redundantes almacenamiento si se trata de la copia de seguridad principal. Elija el almacenamiento con redundancia local si desea una opción más económica que no sea tan duradera. Obtenga más información sobre [con redundancia geográfica](../storage/common/storage-redundancy.md#geo-redundant-storage) y [localmente redundante](../storage/common/storage-redundancy.md#locally-redundant-storage) opciones de almacenamiento en hello [información general sobre la replicación de almacenamiento de Azure](../storage/common/storage-redundancy.md).

configuración de replicación de almacenamiento de Hola tooedit:

1. Seleccione el panel de almacén de credenciales de almacén tooopen hello y hoja de configuración de Hola. Si hello **configuración** hoja no se abre, haga clic en **toda la configuración de** en el panel del almacén de Hola.
2. En hello **configuración** hoja, haga clic en **infraestructura de copia de seguridad** > **configuración de copia de seguridad** tooopen hello **configuración de copia de seguridad** hoja. En hello **configuración de copia de seguridad** hoja, elija la opción de replicación de almacenamiento de hello para el almacén.

    ![Lista de copias de seguridad](./media/backup-azure-vms-first-look-arm/choose-storage-configuration-rs-vault.png)

    Después de elegir la opción de almacenamiento de hello para el almacén, está listo tooassociate Hola VM con el almacén de Hola. asociación de hello toobegin, debería detectar y registrar Hola máquinas virtuales de Azure.

### <a name="2-download-vault-credentials"></a>2. Descarga de las credenciales de almacén
archivo de credenciales de almacén de Hello es un certificado generado por el portal de Hola para cada almacén de copia de seguridad. portal de Hello, a continuación, carga hello toohello clave pública Access Control Service (ACS). clave privada de Hello del certificado de Hola estará disponible toohello usuario como parte del flujo de trabajo de Hola que se proporciona como una entrada en el flujo de trabajo de registro de hello máquina. Esto autentica Hola máquina toosend una copia de seguridad tooan identificado almacén Hola servicio copia de seguridad de Azure.

las credenciales del almacén Hola se utilizan solo durante el flujo de trabajo de registro de hello. Es tooensure de responsabilidad del usuario de Hola que hello las credenciales de almacén archivo no se ve comprometido. Si se encuentra en manos de Hola de cualquier usuario no autorizado, archivo de credenciales de almacén de hello puede ser usado tooregister otras máquinas en Hola mismo almacén. Sin embargo, como datos de copia de seguridad de Hola se cifran con una frase de contraseña que pertenece al cliente de toohello, los datos de copia de seguridad existentes no pueden estar en peligro. toomitigate este problema, las credenciales de almacén se establecen tooexpire en 48 horas. Puede descargar las credenciales de almacén de hello de servicios de recuperación de un número ilimitado de veces: pero solo Hola archivo más reciente almacén credencial sigue intacta durante el flujo de trabajo de registro de hello.

archivo de credenciales de almacén de Hola se descarga a través de un canal seguro de hello portal de Azure. Hola servicio de copia de seguridad de Azure no es consciente de clave privada de hello del certificado de Hola y clave privada de hello no se conserva en el portal de Hola o servicio Hola. Usar hello siguiendo los pasos toodownload Hola almacén credencial archivo tooa equipo local.

1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com/).
2. Abra Servicios de recuperación almacén toowhich toowhich desea tooregister el equipo de DPM.
3. La hoja Configuración se abre de forma predeterminada. Si está cerrado, haga clic en **configuración** en la hoja de configuración de almacén panel tooopen Hola. En dicha hoja, haga clic en **Propiedades**.

    ![Hoja del almacén abierta](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
4. En la página de propiedades de hello, haga clic en **descargar** en **credenciales de copia de seguridad**. portal de Hello genera el archivo de credenciales de almacén de hello, que están disponible para su descarga.

    ![Descargar](./media/backup-azure-dpm-introduction/vault-credentials.png)

portal de Hello generará una credencial de almacén mediante una combinación de nombre de almacén de Hola y Hola fecha actual. Haga clic en **guardar** toodownload Hola almacén credenciales toohello cuenta local descargas de carpeta o seleccione Guardar como de hello Guardar menú toospecify una ubicación para las credenciales de almacén de Hola. Ocupará el minuto tooa Hola archivo toobe generado.

### <a name="note"></a>Nota:
* Asegúrese de que ese archivo de credenciales de almacén de Hola se guarda en una ubicación que se puede acceder desde el equipo. Si se almacena en un recurso compartido de archivo/SMB, busque los permisos de acceso de Hola.
* archivo de credenciales de almacén de Hola se utiliza solo durante el flujo de trabajo de registro de hello.
* archivo de credenciales de almacén de Hello expira después de 48 horas y puede descargarse desde el portal de Hola.

### <a name="3-install-backup-agent"></a>3. Instalación del agente de copia de seguridad
Después de crear el almacén de copia de seguridad de Azure hello, debe instalarse un agente en cada uno de los equipos de Windows (Windows Server, el cliente de Windows, servidor de System Center Data Protection Manager o equipo del servidor de copia de seguridad de Azure) que permite realizar copias de seguridad de datos y aplicaciones tooAzure.

1. Abra Servicios de recuperación almacén toowhich toowhich desea tooregister el equipo de DPM.
2. La hoja Configuración se abre de forma predeterminada. Si está cerrado, haga clic en **configuración** hoja de configuración de tooopen Hola. En dicha hoja, haga clic en **Propiedades**.

    ![Hoja del almacén abierta](./media/backup-azure-dpm-introduction/vault-settings-dpm.png)
3. En la página de configuración de hello, haga clic en **descargar** en **Azure Backup Agent**.

    ![Descargar](./media/backup-azure-dpm-introduction/azure-backup-agent.png)

   Una vez que se descarga el agente de hello, haga doble clic en instalación de hello MARSAgentInstaller.exe toolaunch de agente de copia de seguridad de Azure Hola. Elija la carpeta de instalación de Hola y carpeta temporal requerido para el agente de Hola. ubicación de caché de Hello especificada debe tener espacio libre que es al menos del 5% de datos de copia de seguridad de saludo.
4. Si utiliza un toohello de tooconnect de servidor proxy internet Hola **configuración de Proxy** pantalla, escriba los detalles del servidor proxy Hola. Si usa a un proxy autenticado, escriba los detalles de nombre y la contraseña del usuario de hello en esta pantalla.
5. agente de copia de seguridad de Azure Hola instala .NET Framework 4.5 y Windows PowerShell (si aún no está disponible) toocomplete Hola instalación.
6. Una vez instalado el agente de hello, **cerrar** ventana hello.

   ![cierre](../../includes/media/backup-install-agent/dpm_FinishInstallation.png)
7. demasiado**Hola de registrar el servidor DPM** toohello almacén, Hola **administración** ficha, haga clic en **Online**. Después, seleccione **Registrar**. Se abrirá el Asistente para registrar el programa de instalación de Hola.
8. Si utiliza un toohello de tooconnect de servidor proxy internet Hola **configuración de Proxy** pantalla, escriba los detalles del servidor proxy Hola. Si usa a un proxy autenticado, escriba los detalles de nombre y la contraseña del usuario de hello en esta pantalla.

    ![Configuración de proxy](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Proxy.png)
9. En la pantalla de credenciales de almacén de hello, examinar tooand archivo de credenciales de almacén de hello select que se descargó anteriormente.

    ![Credenciales de almacén](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Credentials.jpg)

    archivo de credenciales de almacén de Hello es válido únicamente para los 48 horas (después de descargarlo desde el portal de hello). Si se produce algún error en esta pantalla (por ejemplo, "Del almacén de credenciales de archivo proporcionado ha expirado"), inicio de sesión toohello Azure portal y descarga Hola almacén archivo de credenciales de nuevo.

    Asegúrese de que ese archivo de credenciales de almacén de hello está disponible en una ubicación que se puede acceder mediante la aplicación de instalación de Hola. Si se producen errores relacionados de acceso, las credenciales de almacén de copia hello tooa ubicación temporal en esta máquina del archivo y vuelva a intentar la operación de Hola.

    Si se produce un error de credencial de almacén no es válido (por ejemplo, "almacén no es válido credenciales proporcionadas") archivo hello está dañado o no haya Hola últimas credenciales asociadas con el servicio de recuperación de Hola. Vuelva a intentar la operación de hello después de descargar un nuevo archivo de credenciales de almacén desde el portal de Hola. Normalmente, este error aparece si hace clic en un usuario de hello en hello **descarga las credenciales del almacén** opción Hola portal de Azure, en una sucesión rápida. En este caso, solo Hola segundo almacén credencial archivo es válido.
10. uso de hello toocontrol de ancho de banda de red durante el trabajo y horas de descanso, Hola **configuración de límite** pantalla, puede establecer límites de uso de ancho de banda de Hola y definir el trabajo de hello y no laborables horas.

    ![Configuración de límite](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Throttling.png)
11. Hola **configuración de la carpeta de recuperación** pantalla, Buscar carpeta Hola donde descargan los archivos de Hola de Azure se almacenará provisionalmente temporalmente.

    ![Recovery Folder Setting](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_RecoveryFolder.png)
12. Hola **configuración de cifrado** pantalla, puede generar una frase de contraseña o proporcione una frase de contraseña (mínimo de 16 caracteres). Recuerde la frase de contraseña de toosave hello en una ubicación segura.

    ![Cifrado](../../includes/media/backup-install-agent/DPM_SetupOnlineBackup_Encryption.png)

    > [!WARNING]
    > Si hello frase de contraseña se pierde u olvida; Microsoft no puede ayudar en la recuperación de datos de copia de seguridad de Hola. usuario final de Hello posee Hola frase de contraseña y Microsoft no tiene visibilidad en la frase de contraseña de hello usada por el usuario final de Hola. Guarde el archivo de hello en una ubicación segura ya que es necesario durante una operación de recuperación.
    >
    >
13. Una vez que pulses hello **registrar** botón, hello máquina se ha registrado correctamente toohello almacén y si ahora está listo toostart copia de seguridad tooMicrosoft Azure.
14. Al usar el Administrador de protección de datos, puede modificar la configuración de hello especificado durante el flujo de trabajo de registro de hello haciendo clic en hello **configurar** opción seleccionando **en línea** en hello  **Administración** ficha.

## <a name="requirements-and-limitations"></a>Requisitos y limitaciones
* DPM se puede ejecutar como un servidor físico o como una máquina virtual de Hyper-V, instalado en System Center 2012 SP1 o System Center 2012 R2. También se puede ejecutar como una máquina virtual de Azure que ejecuta System Center 2012 R2 con al menos el paquete acumulativo de actualizaciones 3 para DPM 2012 R2, o como una máquina virtual de Windows en VMWare que se ejecuta en System Center 2012 R2 con al menos el paquete acumulativo de actualizaciones 5.
* Si ejecuta DPM con System Center 2012 SP1, debe instalar el paquete acumulativo de actualizaciones 2 para System Center Data Protection Manager SP1. Esto es necesario para poder instalar hello Azure Backup Agent.
* servidor DPM de Hello debe tener Windows PowerShell y .net Framework 4.5 instalado.
* DPM puede respaldar la mayoría de las cargas de trabajo de tooAzure copia de seguridad. Para obtener una lista completa de los elementos compatibles, vea Hola copia de seguridad de Azure admite los siguientes elementos.
* No se puede recuperar los datos almacenados en la copia de seguridad de Azure con la opción de "Copiar tootape" Hola.
* Necesitará una cuenta de Azure con la característica de copia de seguridad de Azure Hola habilitada. En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos. Lea acerca de los [Precios de Backup](https://azure.microsoft.com/pricing/details/backup/).
* Mediante copia de seguridad de Azure requiere hello Azure Backup Agent toobe instalado en los servidores de hello que desea tooback. Cada servidor debe tener al menos del 5% del tamaño de Hola de datos de Hola que están haciendo copias de seguridad, disponible como espacio de almacenamiento local. Por ejemplo, la copia de seguridad de 100 GB de datos requiere un mínimo de 5 GB de espacio libre en la ubicación del borrador Hola.
* Datos se almacenarán en hello almacén de Azure. No hay ninguna cantidad de toohello límite de datos que pueda respaldar el almacén de copia de seguridad de Azure tooan pero tamaño Hola de un origen de datos (por ejemplo una máquina virtual o una base de datos) no debe superar 54400 GB.

Se admiten estos tipos de archivo de copia de seguridad tooAzure:

* Cifrados (solo copias de seguridad completas)
* Comprimidos (copias de seguridad incrementales compatibles)
* Dispersos (copias de seguridad incrementales compatibles)
* Comprimidos y dispersos (tratados como dispersos)

No se admiten los siguientes:

* Servidores de sistemas de archivos que distinguen entre mayúsculas y minúsculas.
* Vínculos físicos (omitidos)
* Puntos de reanálisis (omitidos)
* Cifrados y comprimidos (omitidos)
* Cifrados y dispersos (omitidos)
* Flujo comprimido
* Flujo disperso

> [!NOTE]
> Desde en System Center 2012 DPM con SP1 y posteriores, puede hacer una copia seguridad de cargas de trabajo protegidas por tooAzure DPM mediante copia de seguridad de Microsoft Azure.
>
>
