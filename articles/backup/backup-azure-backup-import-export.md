---
title: "Hola a aaaAzure copia de seguridad: copia de seguridad sin conexión o la propagación inicial con el servicio de importación y exportación de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de la copia de seguridad de Azure le permite toosend los datos fuera de red de hello mediante servicio de importación y exportación de Azure de Hola. Este artículo explica Hola sin conexión la propagación de los datos de copia de seguridad inicial de hello mediante el servicio de importación y exportación Azure Hola."
services: backup
documentationcenter: 
author: saurabhsensharma
manager: shivamg
editor: 
ms.assetid: ada19c12-3e60-457b-8a6e-cf21b9553b97
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 4/20/2017
ms.author: saurse;nkolli;trinadhk
ms.openlocfilehash: f1696957c3e9684b800c8d030131255905459f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="offline-backup-workflow-in-azure-backup"></a>Flujo de trabajo de copia de seguridad sin conexión en Azure Backup
Copia de seguridad de Azure tiene varias eficiencias integradas que guardan los costos de red y almacenamiento durante el saludo iniciales copias de seguridad completas de tooAzure de datos. Las copias de seguridad completas iniciales normalmente transferir grandes cantidades de datos y requieren más ancho de banda de red cuando se comparan las copias de seguridad de toosubsequent transferir solo Hola deltas/incrementales. Copia de seguridad de Azure comprime las copias de seguridad inicial de Hola. A través del proceso de Hola de propagación sin conexión, copia de seguridad de Azure pueden usar discos tooupload Hola comprimida los datos de copia de seguridad inicial sin conexión tooAzure.  

Hello propagación sin conexión el proceso de copia de seguridad de Azure está totalmente integrado con hello [servicio de importación y exportación de Azure](../storage/common/storage-import-export-service.md) que permite tootransfer datos tooAzure mediante el uso de discos. Si tienes terabytes (TB) de datos de copia de seguridad iniciales que necesita toobe transfiere a través de una red de alta latencia y ancho de banda bajo, puede usar Hola sin conexión propagación flujo de trabajo tooship Hola copia de seguridad inicial en una o varias unidades de disco duro tooan centro de datos de Azure. Este artículo proporciona información general de los pasos de Hola que completar este flujo de trabajo.

## <a name="overview"></a>Información general
Con capacidad sin conexión propagación Hola de copia de seguridad de Azure y la importación y exportación de Azure, es simple tooupload Hola datos sin conexión tooAzure mediante el uso de discos. En lugar de transferir copia inicial completa de Hola a través de red de hello, se escriben los datos de copia de seguridad de hello tooa *ubicación de almacenamiento provisional*. Una vez completada la ubicación de almacenamiento provisional toohello Hola copia mediante el uso de la herramienta de importación y exportación de Azure de hello, estos datos se escriben tooone o SATA más unidades, según la cantidad de Hola de datos. Estas unidades son enviado finalmente toohello más cercano de centro de datos de Azure.

Hola [actualización de agosto de 2016 de copia de seguridad de Azure (y versiones posteriores)](http://go.microsoft.com/fwlink/?LinkID=229525) incluye hello *herramienta de preparación de disco de Azure*, denominado AzureOfflineBackupDiskPrep, que:

* Le ayudará a preparar las unidades de disco para la importación de Azure mediante el uso de la herramienta de importación y exportación de Azure de Hola.
* Crea automáticamente un trabajo de importación de Azure para hello servicio de importación y exportación de Azure en hello [portal de Azure clásico](https://manage.windowsazure.com) como toocreating opuesto Hola mismo manualmente con versiones anteriores de copia de seguridad de Azure.

Una vez finalizada la carga de Hola de hello tooAzure de datos de copia de seguridad, copia de seguridad de Azure copia el almacén de copia de seguridad toohello Hola datos de copia de seguridad y se programan copias de seguridad incrementales de Hola.

> [!NOTE]
> Hola toouse herramienta de preparación de disco de Azure, asegúrese de que ha instalado la actualización de agosto de 2016 de Hola de copia de seguridad de Azure (o posterior) y lleve a cabo todos los pasos de Hola de flujo de trabajo de hello con él. Si está utilizando una versión anterior de copia de seguridad de Azure, puede preparar la unidad SATA Hola utilizando la herramienta de importación y exportación de Azure de hello tal como se detalla en secciones posteriores de este artículo.
>
>

## <a name="prerequisites"></a>Requisitos previos
* [Familiarizarse con el flujo de trabajo de importación y exportación de hello](../storage/common/storage-import-export-service.md).
* Antes de iniciar el flujo de trabajo de hello, asegúrese de hello siguiente:
  * Se ha creado un almacén de Azure Backup.
  * Se han descargado las credenciales del almacén.
  * se ha instalado el agente de copia de seguridad de Azure de Hello en Windows Server o Windows cliente o servidor de System Center Data Protection Manager y equipo de hello está registrado en el almacén de copia de seguridad de Azure Hola.
* [Descargue la configuración del archivo de publicación de Azure de hello](https://manage.windowsazure.com/publishsettings) en equipos de Hola desde el que tiene intención de tooback seguridad de los datos.
* Prepare una ubicación de almacenamiento provisional, lo que puede ser un recurso compartido de red o la unidad adicional en el equipo de Hola. Hola ubicación de almacenamiento provisional es almacenamiento transitorio y se utiliza temporalmente durante este flujo de trabajo. Asegúrese de que hello en la ubicación de almacenamiento provisional tiene suficiente toohold de espacio en disco la copia inicial. Por ejemplo, si está tratando de tooback de un servidor de archivos de 500 GB, asegúrese de que esa área de ensayo de hello es al menos de 500 GB. (Una menor cantidad se utiliza due toocompression.)
* Asegúrese de que está usando una unidad compatible. 2,5 solo se admiten SSD o 2,5 o 3,5 pulgadas SATA II/III discos duros internos para su uso con el servicio de importación/exportación de Hola. Puede utilizar unidades de disco duro hasta too10 TB. Comprobar hello [documentación del servicio de importación y exportación de Azure](../storage/common/storage-import-export-service.md#hard-disk-drives) para hello conjunto más reciente de las unidades que Hola admite el servicio.
* Habilitar BitLocker en hello equipo toowhich Hola SATA unidad grabador.
* [Descargar la herramienta de importación y exportación de Azure de hello](http://go.microsoft.com/fwlink/?LinkID=301900&clcid=0x409) toohello equipo toowhich Hola SATA unidad grabador. Este paso no es necesario si ha descargado e instalado la actualización de agosto de 2016 de Hola de copia de seguridad de Azure (o posterior).

## <a name="workflow"></a>Flujo de trabajo
información de Hello en esta sección le ayudará a completar el flujo de trabajo de copia de seguridad sin conexión de Hola para que los datos se pueden entregar tooan centro de datos de Azure y cargado tooAzure almacenamiento. Si tiene alguna pregunta sobre el servicio de importación de Hola o cualquier otro aspecto del proceso de hello, vea hello [Introducción al servicio de importación](../storage/common/storage-import-export-service.md) documentación mencionado anteriormente.

### <a name="initiate-offline-backup"></a>Inicio de la copia de seguridad sin conexión
1. Cuando se programa una copia de seguridad, vea Hola después de la pantalla (en Windows Server, el cliente de Windows o System Center Data Protection Manager).

    ![Pantalla de importación](./media/backup-azure-backup-import-export/offlineBackupscreenInputs.png)

    Aquí es pantalla de bienvenida correspondiente en System Center Data Protection Manager: <br/>
    ![Pantalla de importación de DPM](./media/backup-azure-backup-import-export/dpmoffline.png)

    Descripción de Hola de entradas de hello es como sigue:

    * **Ubicación de almacenamiento provisional**: Hola almacenamiento temporal ubicación toowhich Hola copia de seguridad inicial se escribe. Esta podría estar en un recurso compartido de red o en un equipo local. Si el equipo de copia de Hola y el equipo de origen son diferentes, se recomienda especificar ruta de acceso de red completa de Hola de hello ubicación de almacenamiento provisional.
    * **Nombre del trabajo de importación Azure**: nombre único de Hola por qué importación de Azure copia de seguridad de Azure y servicio realizar un seguimiento de transferencia Hola de los datos enviados en discos tooAzure.
    * **Configuración de publicación de Azure**: es un archivo XML que contiene información sobre el perfil de suscripción. También contiene credenciales seguras asociadas a su suscripción. También puede [Descargar archivo hello](https://manage.windowsazure.com/publishsettings). Proporcionar Hola ruta de acceso local toohello archivo de configuración de publicación.
    * **Identificador de suscripción de Azure**: Hola Id. de suscripción de Azure para la suscripción de Hola donde tenga intención de trabajo de importación de Azure de tooinitiate Hola. Si tiene varias suscripciones de Azure, use Hola identificador de suscripción de Hola que desee tooassociate con el trabajo de importación de Hola.
    * **Cuenta de almacenamiento de Azure**: cuenta de almacenamiento de tipos clásicos de Hola Hola proporciona suscripción de Azure que se asociará con el trabajo de importación de Azure Hola.
    * **Contenedor de almacenamiento de Azure**: nombre de Hola de blob de almacenamiento de destino de Hola Hola cuenta de almacenamiento de Azure donde se importan los datos de este trabajo.

    > [!NOTE]
    > Si se ha registrado su tooan de servidor del almacén de servicios de recuperación de Azure de hello [portal de Azure](https://portal.azure.com) para sus copias de seguridad y no están en una suscripción de proveedor de soluciones de nube (CSP), puede crear una cuenta de almacenamiento de tipos clásicos de Hola Portal de Azure y usarlo para el flujo de trabajo de copia de seguridad sin conexión de Hola.
    >
    >

     Guarde toda esta información porque necesita tooenter lo nuevo en los siguientes pasos. Hola solo *ubicación de almacenamiento provisional* es obligatorio si usa discos de hello Azure disco preparación herramienta tooprepare Hola.    
2. Completar flujo de trabajo de hello y, a continuación, seleccione **Back Up Now** en copia de hello Azure Backup administración consola tooinitiate Hola sin conexión-copia de seguridad. copia de seguridad inicial de Hola se escribe toohello área de almacenamiento provisional como parte de este paso.

    ![Realizar copia de seguridad ahora](./media/backup-azure-backup-import-export/backupnow.png)

    flujo de trabajo de toocomplete Hola correspondientes en System Center Data Protection Manager, haga clic en hello **grupo de protección**y, a continuación, elija hello **crear punto de recuperación** opción. A continuación, elija hello **protección en línea** opción.

    ![Realizar copia de seguridad de DPM ahora](./media/backup-azure-backup-import-export/dpmbackupnow.png)

    Una vez finalizada la operación de hello, Hola ubicación de almacenamiento provisional es listo toobe utilizado para la preparación del disco.

    ![Progreso de la copia de seguridad](./media/backup-azure-backup-import-export/opbackupnow.png)

### <a name="prepare-a-sata-drive-and-create-an-azure-import-job-by-using-hello-azure-disk-preparation-tool"></a>Preparar una unidad SATA y crear un trabajo de importación de Azure mediante la herramienta de preparación de disco de Azure de Hola
herramienta de preparación de disco de Azure de Hello está disponible en el directorio de instalación de agente de servicios de recuperación de hello (actualización de agosto de 2016 y versiones posteriores) en hello siguiendo la ruta de acceso.

   *\Microsoft**Azure**Recovery**Services* *Agent\Utils\*

1. Active directory toohello y Hola copia **AzureOfflineBackupDiskPrep** en qué Hola se montan toobe unidades preparado el equipo de copia de tooa del directorio. Asegúrese de hello siguiente con el equipo de copia de toohello de tener en cuenta:

    * Hello copia equipo pueda acceder a Hola ubicación provisional para el flujo de trabajo de hello propagación sin conexión mediante el uso de hello misma ruta de acceso que se proporcionó en Hola de red **iniciar copia de seguridad sin conexión** flujo de trabajo.
    * BitLocker está habilitado en el equipo de Hola.
    * equipo de Hello puede acceder a Hola portal de Azure.

    Si es necesario, equipo de copia de hello puede Hola igual que el equipo de origen de Hola.
2. Abra un símbolo del sistema con privilegios elevados en el equipo de copia de hello con directorio de herramienta de preparación de disco de Azure de hello como Hola actual y ejecute hello siguiente comando:

    `*.\AzureOfflineBackupDiskPrep.exe*   s:<*Staging Location Path*>   [p:<*Path tooPublishSettingsFile*>]`

    | Parámetro | Descripción |
    | --- | --- |
    | s:&lt;*Ruta de acceso de la ubicación de ensayo*&gt; |Entrada obligatoria que ha usado toohello de ruta de acceso de hello tooprovide ubicación que especificó en hello provisional **iniciar copia de seguridad sin conexión** flujo de trabajo. |
    | p:&lt;*tooPublishSettingsFile de ruta de acceso*&gt; |Entrada opcional que se utiliza toohello de ruta de acceso de hello tooprovide **configuración de publicación de Azure** archivo que especificó en hello **iniciar copia de seguridad sin conexión** flujo de trabajo. |

    > [!NOTE]
    > Hola &lt;tooPublishSettingFile de ruta de acceso&gt; valor es obligatorio cuando el equipo de copia de Hola y el equipo de origen son diferentes.
    >
    >

    Al ejecutar el comando de hello, herramienta de hello solicita selección Hola del trabajo de importación de Azure de Hola que corresponde a las unidades de toohello que necesitan toobe preparado. Si solo hay un trabajo de importación único asociado con hello proporciona la ubicación de almacenamiento provisional, verá una pantalla como Hola que sigue.

    ![Entrada de la herramienta de preparación de discos de Azure](./media/backup-azure-backup-import-export/azureDiskPreparationToolDriveInput.png) <br/>
3. Escriba la letra de unidad de hello sin Hola finales dos puntos para el disco montado Hola que quiere tooprepare de tooAzure de transferencia. Proporcione la confirmación para dar formato a Hola de unidad de hello cuando se le solicite.

    herramienta de Hello, a continuación, comienza disco de hello tooprepare con datos de copia de seguridad de saludo. Puede que tenga tooattach discos adicionales cuando se lo solicite herramienta Hola Hola facilita el disco no tiene suficiente espacio para datos de copia de seguridad de saludo. <br/>

    Al final de saludo de la ejecución correcta de la herramienta de hello, uno o más discos que proporcionó preparados para tooAzure de envío. Además, un trabajo de importación con el nombre de Hola que proporcionó durante hello **iniciar copia de seguridad sin conexión** flujo de trabajo se crea en Hola portal de Azure clásico. Por último, Hola herramienta muestra Hola envío dirección toohello centro de datos de Azure donde es necesario toobe incluye discos de Hola y Hola trabajo de importación de vínculo toolocate hello en hello portal de Azure clásico.

    ![Preparación de discos de Azure finalizada](./media/backup-azure-backup-import-export/azureDiskPreparationToolSuccess.png)<br/>

4. Envío Hola discos toohello esa herramienta Hola proporcionada de direcciones y mantener Hola número para futuras referencias de seguimiento.<br/>

5. Cuando vaya toohello vincular esa herramienta hello muestra, consulte cuenta de almacenamiento de Azure de Hola que especificó en hello **iniciar copia de seguridad sin conexión** flujo de trabajo. Aquí puede ver el trabajo de importación de hello recién creado en hello **importación/exportación** ficha de cuenta de almacenamiento de Hola.

    ![Trabajo de importación creado](./media/backup-azure-backup-import-export/ImportJobCreated.png)<br/>

6. Haga clic en **información de envío** final Hola de hello página tooupdate sus datos de contacto como se muestra en hello después de la pantalla. Microsoft usa esta tooship información finaliza su tooyou atrás de discos después de trabajo de importación de Hola.

    ![Información de contacto](./media/backup-azure-backup-import-export/contactInfoAddition.PNG)<br/>

7. Escriba Hola detalles de envío en la pantalla de bienvenida siguiente. Proporcionar hello **transportista de entrega** y **número de seguimiento** detalles correspondientes discos toohello que enviado toohello centro de datos de Azure.

    ![INFORMACIÓN DE ENVÍO](./media/backup-azure-backup-import-export/shippingInfoAddition.PNG)<br/>

### <a name="complete-hello-workflow"></a>Flujo de trabajo de hello completa
Cuando finalice el trabajo de importación de hello, datos de copia de seguridad inicial están disponibles en la cuenta de almacenamiento. Hola agente de servicios de recuperación, a continuación, copia el contenido de Hola de datos de Hola de este almacén de copia de seguridad de cuenta toohello o servicios de recuperación de almacén, lo que sea aplicable. Con antelación Hola ha programado la próxima copia de seguridad, agente de copia de seguridad de Azure de Hola realiza copia de seguridad incremental de hello en copia de seguridad inicial de Hola.

> [!NOTE]
> Hello las secciones siguientes aplican toousers de versiones anteriores de copia de seguridad de Azure que no tiene la herramienta de preparación de disco de Azure de toohello de acceso.
>
>

### <a name="prepare-a-sata-drive"></a>Preparación de una unidad de disco SATA
1. Descargar hello [herramienta de importación y exportación de Microsoft Azure](http://go.microsoft.com/fwlink/?linkid=301900&clcid=0x409) toohello equipo de copia. Asegúrese de que hello en la ubicación de almacenamiento provisional es accesible desde el equipo de hello en el que piensa conjunto siguiente de hello toorun de comandos. Si es necesario, equipo de copia de hello puede Hola igual que el equipo de origen de Hola.

2. Descomprima el archivo de hello WAImportExport.zip. Ejecute la herramienta de WAImportExport de Hola que da formato a la unidad SATA hello, escribe unidad SATA de hello datos de copia de seguridad toohello y la cifra. Antes de ejecutar el siguiente comando de hello, asegúrese de que BitLocker está habilitado en el equipo de Hola. <br/>

    `*.\WAImportExport.exe PrepImport /j:<*JournalFile*>.jrn /id: <*SessionId*> /sk:<*StorageAccountKey*> /BlobType:**PageBlob** /t:<*TargetDriveLetter*> /format /encrypt /srcdir:<*staging location*> /dstdir: <*DestinationBlobVirtualDirectory*>/*`

    > [!NOTE]
    > Si ha instalado la actualización de agosto de 2016 de Hola de copia de seguridad de Azure (o posterior), asegúrese de que Hola ubicación especificada de almacenamiento provisional es Hola igual que uno en Hola Hola **Back Up Now** contiene archivos de AIB y Blob de Base y de pantalla.
    >
    >

| Parámetro | Descripción |
| --- | --- |
| /j:<*ArchivoDiario*> |archivo de diario de toohello de ruta de acceso de Hola. Cada unidad debe tener exactamente un archivo de diario. no debe ser el archivo de diario de Hello en la unidad de destino de Hola. extensión de archivo de diario de Hello es .jrn y se crea como parte de la ejecución de este comando. |
| /id:<*IdSesión*> |Id. de sesión de Hello identifica una sesión de copia. Es utilizado tooensure recuperación precisa de una sesión de copia interrumpida. Archivos que se copian en una sesión de copia se almacenan en un directorio denominado Id. de sesión de hello en la unidad de destino de Hola. |
| /sk:<*ClaveCuentaAlmacenamiento*> |clave de cuenta de Hello para datos de saludo de hello almacenamiento cuenta toowhich se importa. Hola Hola de toobe necesidades clave igual a la se especificó durante la creación del grupo de protección o directiva de copia de seguridad. |
| /BlobType |tipo de Hola de blob. Este flujo de trabajo se realizará correctamente solo si se especifica **PageBlob** . Esto no es la opción predeterminada de Hola y se debe mencionar en este comando. |
| /t:<*LetraUnidadDestino*> |letra de unidad de Hello sin Hola finales dos puntos de la unidad de disco duro de destino de hello para la sesión de copia actual de Hola. |
| /format |unidad de Hello opción tooformat Hola. Especifique este parámetro cuando la unidad de hello necesita toobe formato; en caso contrario, omitirlo. Antes de hello herramienta dé formato a la unidad de hello, pide confirmación de la consola de Hola. toosuppress Hola confirmación, especifique el parámetro/silentmode de Hola. |
| /encrypt |unidad de Hello opción tooencrypt Hola. Especifique este parámetro cuando unidad Hola aún no se ha cifrado con BitLocker y necesita toobe cifrada mediante la herramienta de Hola. Si unidad Hola ya se ha cifrado con BitLocker, omite este parámetro, especifique parámetro /bk de hello y proporcionar la clave de BitLocker de hello existente. Si especifica el parámetro de Hola/Format, también debe especificar Hola / cifrar el parámetro. |
| /srcdir:<*DirectorioOrigen*> |directorio de origen de Hola que contiene archivos toobe copia toohello unidad de destino. Asegúrese de que ese nombre de directorio especificado hello tiene una ruta de acceso completa en lugar de relativo. |
| /dstdir:<*DirectorioVirtualBlobDestino*> |Hola ruta de acceso toohello directorio virtual de destino en su cuenta de almacenamiento de Azure. Ser toouse seguro de los nombres de contenedor válido al especificar los directorios virtuales de destino de Hola o blobs. Tenga en cuenta que los nombres de contenedor deben estar en minúsculas.  Este nombre de contenedor debe ser Hola que haya especificado durante la creación del grupo de protección o directiva de copia de seguridad. |

> [!NOTE]
> Se crea un archivo de diario en carpeta de WAImportExport de Hola que captura Hola toda información de flujo de trabajo de Hola. Necesitará este archivo cuando se crea un trabajo de importación en hello portal de Azure.
>
>

  ![Salida de PowerShell](./media/backup-azure-backup-import-export/psoutput.png)

### <a name="create-an-import-job-in-hello-azure-portal"></a>Crear un trabajo de importación en hello portal de Azure
1. Vaya tooyour cuenta de almacenamiento en hello [portal de Azure clásico](https://manage.windowsazure.com/), haga clic en **importación/exportación**y, a continuación, **crear trabajo de importación** en el panel de tareas de Hola.

    ![Ficha importación/exportación Hola portal de Azure](./media/backup-azure-backup-import-export/azureportal.png)

2. En el paso 1 del Asistente para hello, indican que ha preparado el disco y que tiene el archivo de diario de unidad de hello disponible.

3. En el paso 2 del Asistente para hello, proporcionar información de contacto para la persona de Hola que es responsable de este trabajo de importación.

4. En el paso 3, cargar archivos de diario de unidad de Hola que obtuvo en la sección anterior de Hola.

5. En el paso 4, escriba un nombre descriptivo para el trabajo de importación de Hola que especificó durante la creación del grupo de protección o directiva de copia de seguridad. nombre de Hola que especifique puede contener solo letras minúsculas, números, guiones y caracteres de subrayado, debe empezar por una letra y no puede contener espacios. nombre de Hola que elija es tootrack usa los trabajos mientras están en curso y una vez que se completen.

6. A continuación, seleccione su región de centro de datos de lista de Hola. región de centro de datos de Hello indica toowhich de centro de datos y la dirección de hello, debe enviar el paquete.

    ![Selección de la región del centro de datos](./media/backup-azure-backup-import-export/dc.png)

7. En el paso 5, seleccione el transportista de devolución de lista de Hola y escriba el número de cuenta del transportista. Microsoft usa esta cuenta tooship las unidades de disco espera tooyou después de que se complete el trabajo de importación.

8. Envíe el disco de Hola y escriba Hola seguimiento número tootrack Hola estado de envío de Hola. Una vez que llega disco hello en el centro de datos de hello, es copiar toohello cuenta de almacenamiento, y se actualiza el estado de saludo.

    ![Estado completado](./media/backup-azure-backup-import-export/complete.png)

### <a name="complete-hello-workflow"></a>Flujo de trabajo de hello completa
Después de datos de copia de seguridad inicial de saludo están disponibles en la cuenta de almacenamiento hello agente de servicios de recuperación de Microsoft Azure copia el contenido de Hola de datos de Hola desde este almacén de copia de seguridad de cuenta toohello o el almacén de servicios de recuperación, lo que sea aplicable. En la siguiente programación de hello tiempo de copia de seguridad, Hola agente de copia de seguridad de Azure realiza copia de seguridad incremental de hello en copia de seguridad inicial de Hola.

## <a name="next-steps"></a>Pasos siguientes
* Para las preguntas en el flujo de trabajo de importación y exportación de hello, consulte demasiado[usar Hola importación y exportación de Microsoft Azure service tootransfer datos tooBlob almacenamiento](../storage/common/storage-import-export-service.md).
* Consulte toohello sección de copia de seguridad sin conexión de copia de seguridad de Azure hello [preguntas más frecuentes sobre](backup-azure-backup-faq.md) si tiene alguna pregunta sobre el flujo de trabajo de Hola.
