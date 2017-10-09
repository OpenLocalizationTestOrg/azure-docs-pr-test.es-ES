---
title: Informes de aaaConfigure de copia de seguridad de Azure
description: "En este artículo se habla sobre la configuración de informes de Power BI para Azure Backup con el almacén de Recovery Services."
services: backup
documentationcenter: 
author: JPallavi
manager: vijayts
editor: 
ms.assetid: 86e465f1-8996-4a40-b582-ccf75c58ab87
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: pajosh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 503a240b36ea999e0fea434b6a50d26ddf7677bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-backup-reports"></a>Configuración de informes de Azure Backup
En este artículo se habla pasos tooconfigure informes para copia de seguridad de Azure con el almacén de servicios de recuperación y tooaccess estos informes mediante Power BI. Después de realizar estos pasos, directamente puede ir tooPower BI tooview todos los informes de hello, personalizar y crear informes. 

## <a name="supported-scenarios"></a>Escenarios admitidos
1. Informes de copia de seguridad de Azure son compatibles con la máquina virtual de Azure copia de seguridad y archivo/carpeta de copia de seguridad toocloud mediante el agente de servicios de recuperación de Azure.
2. Los informes de Azure SQL, DPM y Azure Backup Server no se admiten en este momento.
3. Puede ver informes a través de los almacenes y las suscripciones, si se configura la misma cuenta de almacenamiento para cada uno de los almacenes de Hola. Cuenta de almacenamiento seleccionado debe tener Hola almacén de servicios de la misma región que la recuperación.
4. frecuencia de Hola de actualización programada para los informes de hello es de 24 horas en Power BI. También puede realizar una actualización de ad-hoc de informes de hello en Power BI, en el que se usan datos más recientes de los casos en la cuenta de almacenamiento del cliente para representar los informes. 

## <a name="prerequisites"></a>Requisitos previos
1. Crear un [cuenta de almacenamiento de Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account) tooconfigure para informes. Esta cuenta de Storage se usa para almacenar datos relacionados de informes.
2. [Crear una cuenta de Power BI](https://powerbi.microsoft.com/landing/signin/) tooview, personalizar y crear sus propios informes mediante el portal de Power BI.
3. Registrar el proveedor de recursos de hello **Microsoft.insights** si no se ha registrado ya, con una suscripción Hola de cuenta de almacenamiento y también con una suscripción hello de servicios de recuperación del almacén de tooenable toohello de tooflow de datos de informes cuenta de almacenamiento. Hola toodo mismo, debe ir tooAzure portal > suscripción > proveedores de recursos y compruebe si este proveedor tooregister lo. 

## <a name="configure-storage-account-for-reports"></a>Configuración de la cuenta de Storage para los informes
Usar hello después de la cuenta de almacenamiento de pasos tooconfigure hello para el almacén de servicios de recuperación mediante el portal de Azure. Se trata de una única configuración y una vez que se configura la cuenta de almacenamiento, puede ir tooPower BI directamente Aproveche y paquete de contenido de tooview de informes.
1. Si ya tiene un almacén de servicios de recuperación abierto, continúe toonext paso. Si no tiene un abierto de almacén de servicios de recuperación, pero están en hello portal de Azure, en el menú del concentrador hello, haga clic en **examinar**.

   * En la lista de Hola de recursos, escriba **servicios de recuperación**.
   * Cuando empiece a escribir, Hola filtros de la lista con los datos especificados. Haga clic en **Almacenes de Recovery Services**cuando lo vea.

      ![Creación del almacén de Servicios de recuperación, paso 1](./media/backup-azure-vms-encryption/browse-to-rs-vaults.png) <br/>

     aparece en la lista de Hola de almacenes de servicios de recuperación. En lista de Hola de almacenes de servicios de recuperación, seleccione un almacén.

     de este modo se abrirá el panel de Hello almacén seleccionado.
2. En la lista de Hola de elementos que aparece en el almacén, haga clic en **informes de copia de seguridad** bajo supervisión e informes sección tooconfigure Hola cuenta de almacenamiento para los informes.

      ![Selección del elemento de menú Informes de copia de seguridad, paso 2](./media/backup-azure-configure-reports/backup-reports-settings.PNG)
3. En la hoja de hello informes de copia de seguridad, haga clic en **configurar** botón. Esto abre una hoja de Azure Application Insights de Hola que se utiliza para insertar la cuenta de almacenamiento de datos toocustomer.

      ![Configuración de la cuenta de Storage, paso 3](./media/backup-azure-configure-reports/configure-storage-account.PNG)
4. Establecer el botón de alternancia de estado de hello demasiado**en** y seleccione **tooa cuenta de almacenamiento de archivo** casilla de verificación para que los informes de datos pueden iniciar que fluyen en toohello cuenta de almacenamiento.

      ![Habilitación de diagnósticos, paso 4](./media/backup-azure-configure-reports/set-status-on.png)
5. Haga clic en el selector de cuenta de almacenamiento y la cuenta de almacenamiento de hello select de lista de Hola para almacenar los datos de informes y haga clic en **Aceptar**.

      ![Selección de cuenta de Storage, paso 5](./media/backup-azure-configure-reports/select-storage-account.png)
6. Seleccione **AzureBackupReport** casilla de verificación y mover el período de retención de hello control deslizante tooselect para este datos de informes. Datos de informes de cuenta de almacenamiento de Hola se mantienen por período de hello seleccionado mediante el control deslizante.

      ![Selección de cuenta de Storage, paso 6](./media/backup-azure-configure-reports/save-configuration.png)
7. Revise todos los cambios de Hola y haga clic en **guardar** situado en la parte superior, como se muestra en figura Hola anterior. Esta acción garantiza que todos los cambios se guardan, y la cuenta de Storage está ahora configurada para almacenar datos de informes.

> [!NOTE]
> Una vez que configure los informes por guardar la cuenta de almacenamiento, debe **espere 24 horas** para toocomplete de inserción de datos inicial. Debe importar el paquete de contenido de Azure Backup en Power BI solo después de ese tiempo. Consulte la [sección de preguntas frecuentes](#frequently-asked-questions) para obtener más detalles. 
>
>

## <a name="view-reports-in-power-bi"></a>Visualización de informes en Power BI 
Después de configurar la cuenta de almacenamiento para informes con el almacén de servicios de recuperación, tardará aproximadamente 24 horas para crear informes toostart de datos que fluyen en. Después de 24 horas de configuración de la cuenta de almacenamiento, utilice Hola siguientes pasos le indican tooview informes de Power BI:
1. [Inicie sesión en](https://powerbi.microsoft.com/landing/signin/) tooPower BI.
2. Haga clic en **Obtener datos** y haga clic en Get en **Servicios** en la Biblioteca de paquetes de contenido. Utilice los pasos mencionados en [tooaccess de documentación de Power BI content pack](https://powerbi.microsoft.com/en-us/documentation/powerbi-content-packs-services/).

     ![Importación del paquete de contenido](./media/backup-azure-configure-reports/content-pack-import.png)
3. Escriba **Azure Backup** en la barra de búsqueda y haga clic en **Obtenerla ahora**.

      ![Obtención del paquete de contenido](./media/backup-azure-configure-reports/content-pack-get.png)
4. Escriba el nombre de la cuenta de almacenamiento Hola configurado en el paso 5 anterior y haga clic en **siguiente** botón.

    ![Escribir el nombre de la cuenta de Storage](./media/backup-azure-configure-reports/content-pack-storage-account-name.png)    
5. Escriba la clave de cuenta de almacenamiento de Hola para esta cuenta de almacenamiento. También puede [ver y copiar las claves de acceso de almacenamiento](../storage/common/storage-create-storage-account.md#manage-your-storage-account) desplazándose tooyour cuenta de almacenamiento en el portal de Azure. 

     ![Escribir la cuenta de Storage](./media/backup-azure-configure-reports/content-pack-storage-account-key.png) <br/>
     
6. Haga clic en el botón **Iniciar sesión**. Después de iniciar sesión correctamente, obtiene la notificación **Importando datos**.

    ![Importando paquete de contenido](./media/backup-azure-configure-reports/content-pack-importing-data.png) <br/>
    
    Más tarde, obtendrá **correcto** notificación una vez completada la importación de Hola. Es posible que tarde poco más tooimport Hola paquete de contenido, si hay una gran cantidad de datos en la cuenta de almacenamiento de Hola.
    
    ![Importación correcta del paquete de contenido](./media/backup-azure-configure-reports/content-pack-import-success.png) <br/>
    
7. Una vez que los datos se importan correctamente, **copia de seguridad de Azure** paquete de contenido está visible en **aplicaciones** en el panel de navegación de Hola. lista de Hello ahora muestra el panel de copia de seguridad de Azure, informes y conjunto de datos con una estrella amarilla que indica los informes recién importados. 

     ![Paquete de contenido de Azure Backup](./media/backup-azure-configure-reports/content-pack-azure-backup.png) <br/>
     
8. Haga clic en **Azure Backup** en Paneles, donde se muestra un conjunto de informes de claves anclados.

      ![Panel de Azure Backup](./media/backup-azure-configure-reports/azure-backup-dashboard.png) <br/>
9. conjunto completo de hello tooview de informes, haga clic en cualquier informe de panel de Hola.

      ![Estado de la tarea de Azure Backup](./media/backup-azure-configure-reports/azure-backup-job-health.png) <br/>
10. Haga clic en cada ficha de hello informes tooview informes en esa área.

      ![Pestañas de informes de Azure Backup](./media/backup-azure-configure-reports/reports-tab-view.png)


## <a name="frequently-asked-questions"></a>Preguntas más frecuentes
1. **¿Cómo se puede comprobar si ha iniciado datos de informes que fluyen en toostorage cuenta?**
    
    Puede ir toohello almacenamiento contenedores configurados y seleccionados la cuenta. Si el contenedor de hello tiene una entrada para azurebackupreport de registros de visión, indica que la notificación de datos ha iniciado que fluyen.

2. **¿Cuál es la frecuencia de Hola de cuenta de toostorage de inserción de datos y el paquete de contenido de copia de seguridad de Azure en Power BI?**

   Para los usuarios de día 0, tardaría cuenta toostorage de aproximadamente 24 horas toopush datos. Una vez que esta inserción inicial se completa, los datos se actualizan con hello después de frecuencia que se muestra en la siguiente ilustración de Hola. 
      * Datos relacionados con demasiado**trabajos, alertas, elementos de copia de seguridad, los almacenes, servidores protegidos y las directivas de** se inserta toocustomer cuenta de almacenamiento como y cuando se haya iniciado.
      * Datos relacionados con demasiado**almacenamiento** se inserta cuenta de almacenamiento de toocustomer cada 24 horas.
   
    ![Frecuencia de inserción de datos de informes de Azure Backup](./media/backup-azure-configure-reports/reports-data-refresh-cycle.png)

  Power BI tiene una [actualización programada una vez al día](https://powerbi.microsoft.com/documentation/powerbi-refresh-data/#what-can-be-refreshed). Puede realizar una actualización manual de los datos de hello en Power BI para paquete de contenido de Hola.

3. **¿Cuánto tiempo se deben conservar los informes de hello?** 

   Al configurar la cuenta de almacenamiento, puede seleccionar el período de retención de datos de informes en la cuenta de almacenamiento de hello (con el paso 6 para configurar la cuenta de almacenamiento para la sección de informes anterior). Además de eso, también puede [analizar informes en Excel](https://powerbi.microsoft.com/documentation/powerbi-service-analyze-in-excel/) y guardarlos durante un período de retención más largo, según sus necesidades. 

4. **¿Se vea todos los datos en los informes después de configurar la cuenta de almacenamiento de hello?**

   Hola a todos los datos generados después de **"configurar la cuenta de almacenamiento"** se insertarán toohello cuenta de almacenamiento y estarán disponibles en los informes. No obstante, **los trabajos en curso no se insertan** para los informes. Una vez que el trabajo de hello complete o se produce un error, se envía tooreports.

5. **Si ya he configuré Hola almacenamiento cuenta tooview informes, ¿puedo cambiar Hola configuración toouse otra cuenta de almacenamiento?** 

   Sí, puede cambiar la cuenta de almacenamiento distinta de hello configuración toopoint tooa. Debe usar cuenta de almacenamiento de hello recién configurado durante la conexión tooAzure paquete de contenido de copia de seguridad. Además, después de configurar una cuenta de Storage distinta, los nuevos datos fluirán a esta cuenta de Storage. Pero los datos más antiguos (antes de cambiar la configuración de Hola) se siguen en cuenta de almacenamiento anterior Hola.

6. **¿Se pueden ver los informes en los almacenes y las suscripciones?** 

   Sí, puede configurar Hola misma cuenta de almacenamiento a través de diversos informes de almacén entre tooview los almacenes de credenciales. Además, puede configurar Hola misma cuenta de almacenamiento para almacenes de credenciales a través de suscripciones. A continuación, puede usar esta cuenta de almacenamiento al conectar el paquete de contenido de copia de seguridad de tooAzure en informes de Power BI tooview Hola. Sin embargo, cuenta de almacenamiento de hello seleccionado debe tener Hola almacén de servicios de la misma región que la recuperación.
   
## <a name="next-steps"></a>Pasos siguientes
Ahora que ha configurado la cuenta de almacenamiento de Hola e Importar paquete de contenido de copia de seguridad de Azure, paso siguiente hello es toocustomize estos informes y usar informes de toocreate de modelo de datos. Hola siguientes artículos para obtener más información, consulte.

* [Uso del modelo de datos de informes de Azure Backup](backup-azure-reports-data-model.md)
* [Filtrado de informes en Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-about-filters-and-highlighting-in-reports/)
* [Creación de informes en Power BI](https://powerbi.microsoft.com/documentation/powerbi-service-create-a-new-report/)

