---
title: "aaaUse Hola representación de lote de Azure servicio toorender en la nube de hello | Documentos de Microsoft"
description: "Represente trabajos en máquinas virtuales de Azure directamente desde Maya y según la modalidad de pago por uso."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: hero-article
ms.date: 07/31/2017
ms.author: tamram
ms.openlocfilehash: 3fb78d883311bbc3ab62743b7d1b111ffad177cd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-rendering-service"></a>Empezar a trabajar con hello servicio de procesamiento por lotes

Hola servicio de procesamiento por lotes de Azure ofrece capacidades de representación de la escala de nube en forma de pago por uso. Hola servicio de procesamiento por lotes controla la programación de trabajos y puesta en cola, administrar errores y reintentos y la escala automática para el trabajo de procesamiento. Hola servicio por lotes de representación admite Autodesk Maya, 3ds Max y Arnold, con compatibilidad con otras aplicaciones que estarán disponibles próximamente. Hola lote complemento para Maya 2017 resulta fácil toostart un trabajo de representación en Azure directamente desde el escritorio. 

## <a name="supported-applications"></a>Aplicaciones admitidas

Hola servicio por lotes de representación admite actualmente Hola derivados de la solicitud:

- Autodesk Maya
- Autodesk 3ds Max
- Autodesk Arnold

## <a name="prerequisites"></a>Requisitos previos

servicio de procesamiento por lotes de Hola de toouse, necesita:

- Una [cuenta de Azure](https://azure.microsoft.com/free/). 
- **Una cuenta de Azure Batch** Para obtener instrucciones sobre cómo crear una cuenta de lote en hello portal de Azure, consulte [crear una cuenta de lote con hello portal de Azure](batch-account-create-portal.md).
- **Una cuenta de Azure Storage.** activos de Hola que se utilizan para el trabajo de representación se almacenan en el almacenamiento de Azure. Puede crear una cuenta de almacenamiento automáticamente al configurar su cuenta de Batch. También puede usar una cuenta de almacenamiento existente. toolearn más información acerca de las cuentas de almacenamiento, consulte [cómo toocreate, administrar o eliminar una cuenta de almacenamiento en el portal de Azure hello](https://docs.microsoft.com/azure/storage/storage-create-storage-account).

Hola toouse lote complemento para Maya, necesita:

- **Maya 2017**
- **Arnold para Maya**

También puede usar hello [portal de Azure](https://portal.azure.com) toocreate grupos de máquinas virtuales que están preconfiguradas con Maya, 3ds Max y Arnold. Puede usar los trabajos de portal toomonitor hello y diagnosticar errores de las tareas mediante la descarga de registros de la aplicación y conectar de forma remota máquinas virtuales de tooindividual con RDP o SSH.

## <a name="basic-batch-concepts"></a>Conceptos básicos sobre Batch

Antes de empezar a usar el servicio de procesamiento por lotes de hello, resulta útil toobe familiarizado con algunos conceptos de lote, como nodos de proceso, los grupos y los trabajos. toolearn más información sobre el lote de Azure en general, vea [ejecutar cargas de trabajo paralelos intrínsecamente con lote](batch-technical-overview.md).

### <a name="pools"></a>Grupos

Batch es un servicio de plataforma para la ejecución de trabajos de proceso intensivo, como la representación de un **grupo** de **nodos de proceso**. Cada nodo de proceso de un grupo es una máquina virtual (VM) de Azure que ejecuta Linux o Windows. 

Para obtener más información sobre los grupos de proceso por lotes y nodos de proceso, vea hello [grupo](batch-api-basics.md#pool) y [de nodos de proceso](batch-api-basics.md#compute-node) secciones en [paralelas a gran escala de desarrollar soluciones con el lote de proceso](batch-api-basics.md).

### <a name="jobs"></a>Trabajos

Un lote **trabajo** es una colección de tareas que se ejecutan en hello nodos de cálculo en un grupo. Cuando se envía un trabajo de representación, lote divide el trabajo de hello en tareas y distribuye los nodos de proceso de hello tareas toohello en hello grupo toorun.

Para obtener más información acerca de los trabajos por lotes, vea hello [trabajo](batch-api-basics.md#job) sección [paralelas a gran escala de desarrollar soluciones con el lote de proceso](batch-api-basics.md).

## <a name="use-hello-batch-plug-in-for-maya-toosubmit-a-render-job"></a>Hola complemento para Maya toosubmit un trabajo de procesamiento del lote de uso

Con hello lote complemento para Maya, puede enviar un servicio de procesamiento por lotes directamente desde Maya toohello de trabajo. Hola las secciones siguientes describe cómo tooconfigure Hola trabajo de hello complemento y, a continuación, enviarla. 

### <a name="load-hello-batch-plug-in-in-maya"></a>Hola de carga por lotes complemento en Maya

Hola lote complemento está disponible en [GitHub](https://github.com/Azure/azure-batch-maya/releases). Descomprima el directorio de archivo tooa y Hola de su elección. Puede cargar Hola complemento directamente desde hello *azure_batch_maya* directory.

Hola de tooload complemento en Maya:

1. Ejecute Maya.
2. Abra **Window (Ventana)** > **Settings/Preferences (Configuración/Preferencias)** > **Plug-in Manager (Administrador de complementos)**.
3. Haga clic en **Examinar**.
4. Navegue seleccione tooand *azure_batch_maya/plug-in/AzureBatch.py*.

### <a name="authenticate-access-tooyour-batch-and-storage-accounts"></a>Autenticar cuentas de lote y el almacenamiento de tooyour de acceso

Hola toouse complemento debe tooauthenticate usando su lote de Azure y claves de la cuenta de almacenamiento de Azure. tooretrieve las claves de cuenta:

1. Hola mostrar complemento en Maya y seleccione hello **Config** ficha.
2. Navegue toohello [portal de Azure](https://portal.azure.com).
3. Seleccione **las cuentas de lote** del menú izquierdo Hola. Si es necesario, haga clic en **Más servicios** y filtre por _Batch_.
4. Busque la cuenta de lote de hello deseado en lista de Hola.
5. Seleccione hello **claves** toodisplay de elemento de menú su nombre de cuenta, URL de la cuenta y las teclas de acceso:
    - Pegue la URL hello de la cuenta de lote en hello **servicio** campo Hola lote complemento.
    - Pegar el nombre de cuenta de hello en hello **cuenta de lote** campo.
    - Clave de cuenta principal de pegar hello en hello **clave lote** campo.
7. Seleccione las cuentas de almacenamiento desde el menú izquierdo Hola. Si es necesario, haga clic en **Más servicios** y filtre por _Storage_.
8. Ubicar la cuenta de almacenamiento de hello deseado en la lista de Hola.
9. Seleccione hello **teclas de acceso** nombre de cuenta de almacenamiento de hello toodisplay de elemento de menú y las claves.
    - Nombre de cuenta de almacenamiento de pegar hello en hello **cuenta de almacenamiento** campo Hola lote complemento.
    - Clave de cuenta principal de pegar hello en hello **clave de almacenamiento** campo.
10. Haga clic en **Authenticate** tooensure que Hola complemento puede tener acceso a ambas cuentas.

Una vez que se haya autenticado correctamente, conjuntos de complemento de Hola Hola campo estado demasiado**autenticado**: 

![Autenticación de las cuentas de Batch y Storage](./media/batch-rendering-service/authentication.png)

### <a name="configure-a-pool-for-a-render-job"></a>Configuración de un grupo para un trabajo de representación

Cuando se hayan autenticado las cuentas de Batch y Storage, configure un grupo para el trabajo de representación. Hola complemento guarda las selecciones entre sesiones. Una vez haya configurado su configuración preferida, no necesitará toomodify, a menos que lo cambie.

Hello secciones siguientes le guían a través de opciones disponibles de hello, disponibles en hello **enviar** ficha:

#### <a name="specify-a-new-or-existing-pool"></a>Especificación de un grupo nuevo o existente

toospecify un grupo en qué trabajo de procesamiento de hello toorun, seleccione hello **enviar** ficha. Esta pestaña proporciona opciones para la creación de un grupo o la selección de un grupo existente:

- También puede **automáticamente aprovisionar un grupo para este trabajo** (Hola la opción predeterminada). Cuando elige esta opción, por lotes crea el grupo de hello exclusivamente para el trabajo actual de Hola y automáticamente el grupo de Hola de eliminaciones cuando Hola representar el trabajo se completa. Esta opción es mejor cuando tenga un toocomplete de trabajo de procesamiento único.
- También puede **reutilizar un grupo persistente existente**. Si tiene un grupo existente que está inactivo, puede especificar ese grupo de trabajo en ejecución Hola render, selecciónelo en la lista desplegable de Hola. Reutilizar un grupo existente persistente ahorra Hola tiempo necesario tooprovision Hola grupo.  
- También puede **crear un nuevo grupo persistente**. Si elige esta opción, crea un nuevo grupo para ejecutar el trabajo de Hola. No elimina el grupo de hello cuando se complete, el trabajo de Hola para que se puede reutilizar para futuros trabajos. Seleccione esta opción cuando tenga un toorun continua necesario procesar trabajos. En los trabajos posteriores, puede seleccionar **volver a usar un grupo existente persistente** toouse Hola grupo persistente que ha creado para el primer trabajo de Hola.

![Especificación del grupo, la imagen del SO, el tamaño de máquina virtual y la licencia](./media/batch-rendering-service/submit.png)

Para obtener más información sobre cómo cargas se incrementan con máquinas virtuales de Azure, vea hello [P+F de precios de Linux](https://azure.microsoft.com/pricing/details/virtual-machines/linux/#faq) y [P+F de precios de Windows](https://azure.microsoft.com/pricing/details/virtual-machines/windows/#faq).

#### <a name="specify-hello-os-image-tooprovision"></a>Especificar Hola SO imagen tooprovision

Puede especificar tipo de Hola de nodos de proceso de tooprovision de toouse de imagen de sistema operativo en grupo de Hola de hello **Env** ficha (entorno). Lote admite actualmente Hola opciones de imagen para presentar los trabajos siguientes:

|Sistema operativo  |Imagen  |
|---------|---------|
|Linux     |Versión preliminar de CentOS para Batch |
|Windows     |Versión preliminar de Windows para Batch |

#### <a name="choose-a-vm-size"></a>Selección del tamaño de la máquina virtual

Puede especificar el tamaño de máquina virtual de hello en hello **Env** ficha. Para más información sobre los tamaños de máquina virtual disponibles, consulte [Tamaños de las máquinas virtuales Linux en Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sizes) y [Tamaños de las máquinas virtuales Windows en Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sizes). 

![Especificar imagen de sistema operativo de la máquina virtual de Hola y el tamaño en la ficha de Env Hola](./media/batch-rendering-service/environment.png)

#### <a name="specify-licensing-options"></a>Especificación de las opciones de licencia

Puede especificar licencias Hola desea toouse en hello **Env** ficha. Las opciones incluyen:

- **Maya**, que está habilitado de forma predeterminada.
- **Arnold**, que está habilitada si se detecta Arnold como motor de representación active hello en Maya.

 Si desea que toorender mediante su propia licencia, puede configurar el punto final de licencia mediante la adición de la tabla de toohello de variables de entorno adecuadas de Hola. Ser seguro toodeselect opciones de licencia de hello predeterminada si lo hace.

> [!IMPORTANT]
> Se le facturará para el uso de licencias de hello mientras se ejecutan las máquinas virtuales en el grupo de hello, incluso si hello las máquinas virtuales no se usan actualmente para la representación. tooavoid recargos, navegue toohello **grupos** ficha y cambiar el tamaño de la too0 nodos de hello grupo hasta que esté listo toorun otro trabajo de procesamiento. 
>
>

#### <a name="manage-persistent-pools"></a>Administración de grupos persistentes

Puede administrar un grupo existente persistente en hello **grupos** ficha. Al seleccionar un grupo de lista de hello muestra el estado actual de hello del grupo de Hola de.

De hello **grupos** pestaña, también puede eliminar el grupo de Hola y cambiar el tamaño de número de Hola de máquinas virtuales en el grupo de Hola. Puede cambiar el tamaño de una tooavoid de nodos de grupo too0 incurrir en costos entre las cargas de trabajo.

![Visualización, cambio de tamaño y eliminación de grupos](./media/batch-rendering-service/pools.png)

### <a name="configure-a-render-job-for-submission"></a>Configuración de un trabajo de representación para su envío

Una vez que ha especificado parámetros de Hola para grupo de Hola que se ejecutará el trabajo de procesamiento de hello, configure el propio trabajo Hola. 

#### <a name="specify-scene-parameters"></a>Especificación de los parámetros de escena

Hola lote complemento detecta qué motor de representación que está usando actualmente en Maya y muestra hello adecuado representar valores en hello **enviar** ficha. Estas opciones incluyen el marco de inicio de hello, fotograma final, prefijo de salida y el paso de marco. Puede invalidar configuración de procesamiento de archivos de escena Hola especificando valores diferentes en hello complemento. Los cambios que realice toohello configuración del complemento no son persistentes toohello back-configuración de representación de archivo de escena, por lo que puede realizar cambios en una base de trabajos por trabajo sin necesidad de archivo de escena hello tooreupload.

Hola complemento advierte si Hola representar motor que seleccionó en Maya no se admite.

Si carga una nueva escena mientras Hola complemento está abierto, haga clic en hello **actualizar** botón toomake seguro Hola valores se actualicen.

#### <a name="resolve-asset-paths"></a>Resolución de las rutas de acceso a los recursos

Cuando se carga el complemento hello, examina el archivo de escena hello para las referencias a archivos externos. Estas referencias se muestran en hello **activos** ficha. Si no se puede resolver una ruta de acceso que se hace referencia, Hola complemento intentos de archivo de hello toolocate en algunas ubicaciones predeterminadas, incluidos:

- ubicación de Hello del archivo de escena hello 
- Hola actual del proyecto _sourceimages_ directory
- directorio de trabajo actual de Hola. 

Si activo Hola todavía no se encuentra, se muestra con un icono de advertencia:

![Los recursos que faltan se muestran con un icono de advertencia.](./media/batch-rendering-service/missing_assets.png)

Si conoce la ubicación Hola de una referencia de archivo sin resolver, puede hacer clic en hello advertencia toobe de icono se le pida tooadd una ruta de acceso de búsqueda. Hola, a continuación, complemento usa esta tooresolve tooattempt de ruta de acceso de búsqueda los activos que faltan. Puede agregar cualquier número de rutas de acceso de búsqueda adicionales.

Cuando se resuelve una referencia, se muestra con un icono de luz verde:

![Recursos resueltos con un icono de luz verde](./media/batch-rendering-service/found_assets.png)

Si la escena requiere otros archivos no ha detectado ese complemento hello, puede agregar archivos o directorios adicionales. Hola de uso **agregar archivos** y **Agregar directorio** botones. Si carga una nueva escena mientras Hola complemento está abierto, ser seguro tooclick **actualizar** referencias de la escena de Hola de tooupdate.

#### <a name="upload-assets-tooan-asset-project"></a>Cargar proyecto activo de activos tooan

Cuando se envía un trabajo de procesamiento, hello hace referencia a los archivos que se muestran en hello **activos** ficha están cargado automáticamente tooAzure almacenamiento como un proyecto activo. También puede cargar archivos de recursos de hello independientemente de un trabajo de procesamiento, con hello **cargar** botón en hello **activos** nombre de proyecto de pestaña. Hola activo se especifica en hello **proyecto**campo y se denomina después del proyecto Maya actual de Hola de forma predeterminada. Cuando se cargan archivos de recursos, se conserva la estructura de archivos local de Hola. 

Una vez cargados, cualquier número de trabajos de representación puede hacer referencia a ellos. Todos los activos cargados son trabajo tooany disponibles que hace referencia el proyecto activo de hello, si no se incluyen en escena Hola. proyecto de activos de hello toochange al que hace referencia el siguiente trabajo, cambiar el nombre de Hola Hola **proyecto** campo hello **activos** ficha. Si hay archivos que se hace referencia que desee tooexclude de carga, anule la selección de ellas con botón Hola verde situada junto a la lista de Hola.

#### <a name="submit-and-monitor-hello-render-job"></a>Enviar y Hola monitor representar trabajo

Después de haber configurado el trabajo de procesamiento de Hola Hola complemento, haga clic en hello **enviar trabajo** botón en hello **enviar** ficha toosubmit Hola trabajo tooBatch:

![Enviar el trabajo de procesamiento de Hola](./media/batch-rendering-service/submit_job.png)

Puede supervisar un trabajo que está en curso de hello **trabajos** ficha en hello complemento. Seleccione un trabajo de hello lista toodisplay Hola estado actual del trabajo de Hola. También puede utilizar esta pestaña toocancel y eliminar trabajos, así como toodownload Hola salidas y los registros de representación. 

salidas de toodownload, modificar hello **genera** directorio de destino deseado de campo tooset Hola. Haga clic en icono toostart un proceso en segundo plano que supervisa el trabajo de Hola y descarga salidas cuando progrese de hello engranaje: 

![Visualización del estado del trabajo y descarga de las salidas](./media/batch-rendering-service/jobs.png)

Puede cerrar Maya sin interrumpir el proceso de descarga de Hola.

## <a name="next-steps"></a>Pasos siguientes

toolearn más información acerca de lote, consulte [ejecutar cargas de trabajo paralelos intrínsecamente con lote](batch-technical-overview.md).
