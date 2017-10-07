---
title: aaaOverview del lote de Azure para desarrolladores | Documentos de Microsoft
description: "Obtenga información acerca de las características de Hola de servicio por lotes de Hola y sus API desde la perspectiva del desarrollo."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 416b95f8-2d7b-4111-8012-679b0f60d204
ms.service: batch
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 06/28/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3da9d82572b28d05d1923166bd08c26725ca3316
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="develop-large-scale-parallel-compute-solutions-with-batch"></a>Desarrollo de soluciones de procesos paralelos a gran escala con Batch

En esta información general de componentes principales de Hola de hello servicio Azure Batch, se describen las características de servicio principal de Hola y recursos que los desarrolladores de lote pueden usar paralelas a gran escala toobuild soluciones de proceso.

Si está desarrollando una aplicación distribuida de cálculo o de servicio que emite directa [API de REST] [ batch_rest_api] llamadas o si está usando uno de hello [SDK de lote](batch-apis-tools.md#azure-accounts-for-batch-development), va a utilizar muchos de los recursos de Hola y características que se describen en este artículo.

> [!TIP]
> Para un nivel más alto Introducción toohello servicio por lotes, vea [conceptos básicos de Azure Batch](batch-technical-overview.md).
>
>

## <a name="batch-service-workflow"></a>Flujo de trabajo del servicio Batch
Hello siguiente flujo de trabajo de alto nivel es típico de casi todas las aplicaciones y servicios que utilizan el servicio de lote de hello para el procesamiento de las cargas de trabajo paralelas:

1. Cargar hello **archivos de datos** que desea tooprocess tooan [el almacenamiento de Azure] [ azure_storage] cuenta. Lote incluye compatibilidad integrada para acceder al almacenamiento de blobs de Azure y sus tareas pueden descargar estos archivos demasiado[nodos de proceso](#compute-node) cuando se ejecutan las tareas de Hola.
2. Cargar hello **archivos de la aplicación** que se ejecutarán las tareas. Estos archivos pueden ser archivos binarios o secuencias de comandos y sus dependencias y se ejecutan las tareas de hello en los trabajos. Las tareas pueden descargar estos archivos desde su cuenta de almacenamiento, o puede usar hello [paquetes de aplicación](#application-packages) característica de lote para la implementación y administración de aplicaciones.
3. Cree un [grupo](#pool) de nodos de proceso. Cuando se crea un grupo, especifique número Hola de nodos de proceso para el grupo de hello, su tamaño y el sistema operativo de Hola. Cuando se ejecuta cada tarea en el trabajo, se le asigna tooexecute en uno de los nodos de hello en el grupo.
4. Creación de un [trabajo](#job). Un trabajo administra una colección de tareas. Asociar cada grupo específico de tooa de trabajo donde se ejecutarán las tareas de la tarea.
5. Agregar [tareas](#task) toohello trabajo. Cada tarea ejecuta la aplicación hello o script que ha cargado los archivos de datos de hello tooprocess descarga desde la cuenta de almacenamiento. Dado que cada tarea se completa, puede cargar su almacenamiento tooAzure de salida.
6. Supervisar el progreso del trabajo y recuperar el resultado de la tarea de Hola desde el almacenamiento de Azure.

Hello las secciones siguientes tratan estas y Hola otros recursos de proceso por lotes que permiten su escenario de cálculo distribuido.

> [!NOTE]
> Necesita un [cuenta de lote](#account) toouse Hola servicio por lotes. Casi todas las soluciones de Batch usan una cuenta de [Azure Storage][azure_storage] para el almacenamiento y la recuperación de archivos. Lote actualmente admite solo hello **general** tipo de cuenta de almacenamiento, tal como se describe en el paso 5 de [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) en [cuentas de almacenamiento de Azure sobre](../storage/common/storage-create-storage-account.md).
>
>

## <a name="batch-service-resources"></a>Recursos del servicio Batch
Algunos de hello después de recursos, cuentas, calculan nodos, grupos, los trabajos y tareas--necesarios por todas las soluciones que utilizan el servicio de lote de Hola. Otros, como las programaciones de los trabajos y los paquetes de aplicación, son características útiles, pero opcionales.

* [Cuenta](#account)
* [Nodo de ejecución](#compute-node)
* [Grupo](#pool)
* [Trabajo](#job)

  * [Programaciones del trabajo](#scheduled-jobs)
* [Task](#task)

  * [Tarea de inicio](#start-task)
  * [Tareas del Administrador de trabajos](#job-manager-task)
  * [Tareas de preparación y liberación de trabajos](#job-preparation-and-release-tasks)
  * [Tarea de instancias múltiples (MPI)](#multi-instance-tasks)
  * [Dependencias de las tareas](#task-dependencies)
* [Paquetes de aplicación](#application-packages)

## <a name="account"></a>Cuenta
Una cuenta de lote es una entidad identificada de forma única dentro de hello servicio por lotes. Todo el procesamiento se asocia con una cuenta de Batch.

Puede crear una cuenta de Azure Batch con hello [portal de Azure](batch-account-create-portal.md) o mediante programación, como con hello [biblioteca .NET de administración de lotes](batch-management-dotnet.md). Al crear la cuenta de hello, puede asociar una cuenta de almacenamiento de Azure.

### <a name="pool-allocation-mode"></a>Modo de asignación de grupos

Cuando se crea una cuenta de Batch, puede especificar cómo se asignan los [grupos](#pool) de nodos de proceso. Puede elegir tooallocate grupos de nodos de cálculo en una suscripción administrada por lote de Azure, o se puede asignar en su propia suscripción. Hola *modo de asignación de grupo de* propiedad de cuenta de hello determina donde se asignan grupos. 

toodecide agrupación toouse de modo de asignación, tenga en cuenta que mejor se adapte a su escenario:

* **Servicio de lote**: servicio por lotes es el modo de asignación de grupo predeterminado hello, y en el que se asignan grupos entre bastidores de hello en suscripciones de Azure administrados. Tenga en cuenta estos puntos clave sobre el modo de asignación de grupo de hello servicio por lotes:

    - modo de asignación de grupo de servicio por lotes de Hello es compatible con grupos de servicio en la nube y máquinas virtuales.
    - modo de asignación de grupo de servicio por lotes Hello admite tanto la autenticación de clave compartida o [autenticación de Azure Active Directory](batch-aad-auth.md) (Azure AD). 
    - Puede usar los nodos de proceso dedicado o de baja prioridad en grupos que se asignan a modo de asignación de grupo de servicio por lotes de Hola.
    - No utilice el modo de asignación de grupo de servicio por lotes de hello si tiene previsto toocreate grupos de máquina virtual de Azure de imágenes de máquina virtual personalizadas, o si tiene previsto toouse una red virtual. Crear su cuenta con el modo de asignación de grupo de suscripción de usuario de hello en su lugar.
    - Se deben crear grupos de máquina virtual aprovisionados en una cuenta creada con el modo de asignación de grupo de servicio por lotes de Hola desde [máquinas virtuales de Azure Marketplace] [ vm_marketplace] imágenes.

* **Suscripción de usuario**: con el modo de asignación de grupo de suscripción de usuario de hello, se asignan grupos de proceso por lotes en hello suscripción de Azure donde se crea la cuenta de hello. Tenga en cuenta estos puntos clave sobre el modo de asignación de grupo de hello suscripción de usuario:
     
    - modo de asignación de grupo de suscripción de usuario de Hello admite sólo los grupos de máquina Virtual. No admite grupos de Cloud Services.
    - grupos de máquina Virtual de toocreate de imágenes de máquina virtual o una red virtual toouse personalizado con los grupos de máquina Virtual, debe utilizar el modo de asignación de grupo de suscripción de usuario Hola.  
    - Debe usar [autenticación de Azure Active Directory](batch-aad-auth.md) con los grupos que se asignan en la suscripción de usuario de Hola. 
    - Debe configurar un almacén de claves de Azure para su cuenta de lote si el modo de asignación de grupo de Hola se establece tooUser suscripción. 
    - Puede usar los nodos de cálculo solo dedicado en grupos en una cuenta creada con el modo de asignación de grupo de suscripción de usuario de Hola. No se admiten nodos de prioridad baja.
    - Se pueden crear grupos de máquina virtual que se aprovisiona en una cuenta con el modo de asignación de grupo de suscripción de usuario de Hola desde [máquinas virtuales de Azure Marketplace] [ vm_marketplace] imágenes o a una personalizada imágenes que proporcionar.

Hello en la tabla siguiente compara los modos de asignación de grupo de servicio por lotes y suscripción de usuario Hola.

| **Modo de asignación de grupos**                 | **Servicio Batch**                                                                                       | **Suscripción de usuario**                                                              |
|-------------------------------------------|---------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------|
| **Los grupos se asignan en**               | Una suscripción administrada por Azure                                                                           | suscripción de usuario de Hello en qué Hola lote se crea la cuenta                        |
| **Configuraciones admitidas**             | <ul><li>Configuración de servicio en la nube</li><li>Configuración de máquina virtual (Linux y Windows)</li></ul> | <ul><li>Configuración de máquina virtual (Linux y Windows)</li></ul>                |
| **Imágenes de máquina virtual admitidas**                  | <ul><li>Imágenes de Azure Marketplace</li></ul>                                                              | <ul><li>Imágenes de Azure Marketplace</li><li>Imágenes personalizadas</li></ul>                   |
| **Tipos de nodo de proceso admitidos**         | <ul><li>Nodos dedicados</li><li>Nodos de prioridad baja</li></ul>                                            | <ul><li>Nodos dedicados</li></ul>                                                  |
| **Autenticación admitida**             | <ul><li>Clave compartida</li><li>Azure AD</li></ul>                                                           | <ul><li>Azure AD</li></ul>                                                         |
| **Azure Key Vault requerido**             | No                                                                                                      | Sí                                                                                |
| **Cuota de núcleos**                           | Determinado por la cuota de núcleos de Batch                                                                          | Determinado por la cuota de núcleos de la suscripción                                              |
| **Compatibilidad con redes virtuales de Azure** | Grupos creados con hello configuración del servicio de nube                                                      | Grupos creados con hello configuración de máquina Virtual                               |
| **Modelo de implementación de red virtual admitido**      | Redes virtuales creadas con el modelo de implementación clásico                                                             | Redes virtuales creadas con el modelo de implementación clásica de Hola o administrador de recursos de Azure |

## <a name="azure-storage-account"></a>Cuenta de almacenamiento de Azure

La mayoría de las soluciones de Batch usan Azure Storage para almacenar los archivos de recursos y los archivos de salida.  

Lote admite actualmente el único tipo de cuenta de almacenamiento general de hello, tal como se describe en el paso 5 de [crear una cuenta de almacenamiento](../storage/common/storage-create-storage-account.md#create-a-storage-account) en [cuentas de almacenamiento de Azure sobre](../storage/common/storage-create-storage-account.md). Las tareas de Batch (incluidas las tareas estándar, las de inicio, las de preparación de trabajos y las de liberación de trabajos) deben especificar archivos de recursos que residan en cuentas de almacenamiento de uso general.


## <a name="compute-node"></a>Nodo de proceso
Un nodo de proceso es una máquina virtual de Azure (VM) o la máquina virtual que está dedicado tooprocessing una parte de la carga de trabajo de la aplicación de servicio de nube. tamaño de Hola de un nodo determina número Hola de núcleos de CPU, capacidad de memoria y tamaño del sistema de archivos local que se asigna el nodo toohello. Puede crear grupos de nodos de Windows o Linux mediante el uso de servicios de nube de Azure, imágenes de hello [máquinas virtuales de Azure Marketplace][vm_marketplace], o imágenes personalizadas que prepare. Vea a continuación hello [grupo](#pool) sección para obtener más información acerca de estas opciones.

Nodos pueden ejecutar cualquier archivo ejecutable o script que es compatible con el entorno de sistema operativo de hello del nodo de Hola. Esto incluye scripts \*.exe, \*.cmd, \*.bat y de PowerShell para Windows, además de archivos binarios y scripts de shell y de Python para Linux.

Todos los nodos de proceso en Batch también incluyen:

* Una [estructura de carpetas](#files-and-directories) estándar y [variables de entorno](#environment-settings-for-tasks) asociadas, disponibles para que las tareas hagan referencia a ellas.
* **Firewall** los valores que están configurados toocontrol acceso.
* [Acceso remoto](#connecting-to-compute-nodes) tooboth Windows (Protocolo de escritorio remoto (RDP)) y nodos de Linux (Shell seguro (SSH)).

## <a name="pool"></a>grupo
Un grupo es una colección de nodos en la que se ejecuta la aplicación. grupo de Hola puede crearse manualmente por el usuario o automáticamente por hello servicio por lotes cuando se especifica Hola trabajo toobe realizada. Puede crear y administrar un grupo que cumpla los requisitos de recursos de saludo de la aplicación. Puede usarse un grupo solo por cuenta de lote de hello en el que se creó. Una cuenta de Batch puede tener más de un grupo.

Grupos de lote de Azure se basan en la plataforma de proceso de Azure de hello principal. Proporcionan asignación a gran escala, instalación de la aplicación, la distribución de datos, la supervisión del estado y ajuste flexible del número de Hola de nodos de proceso dentro de un grupo de ([escalado](#scaling-compute-resources)).

Todos los nodos que se agregan el grupo de tooa se asignan un nombre único y una dirección IP. Cuando se quita un nodo de un grupo, se perderán los cambios que se realizan archivos o sistema operativo de toohello y su nombre y dirección IP se liberan para su uso futuro. Cuando un nodo abandona un grupo, su vigencia finaliza.

Cuando se crea un grupo, puede especificar Hola siguientes atributos. Algunas opciones de configuración difieren, según el modo de asignación de grupo de Hola de hello lote [cuenta](#account):

- Sistema operativo y versión de nodo de proceso
- Tipo de nodo de proceso y número de nodos de destino
- Tamaño de los nodos de cálculo de Hola
- Directiva de escalado
- Directiva de programación de tareas
- Estado de comunicación para nodos de proceso
- Tareas de inicio para nodos de proceso
- paquetes de aplicación
- Network configuration (Configuración de red)

Cada una de estas configuraciones se describe con más detalle en las secciones siguientes de Hola.

> [!IMPORTANT]
> Cuentas de lote creadas con el modo de asignación de grupo de servicio por lotes de hello tienen una cuota predeterminada que limita el número de Hola de núcleos en una cuenta de lote. número de Hola de núcleos corresponde toohello número de nodos de cálculo. Puede encontrar las cuotas predeterminadas de hello e instrucciones sobre cómo demasiado[aumentar una cuota](batch-quota-limit.md#increase-a-quota) en [las cuotas y límites de hello servicio Azure Batch](batch-quota-limit.md). Si el grupo no es conseguir su número de destino de nodos, cuota de núcleos de hello podría ser motivo de Hola.
>
>Las cuentas de lote creadas con el modo de asignación de grupo de suscripción de usuario de hello no ver las cuotas del servicio de lote de Hola. En su lugar, comparten en hello cuota de núcleos de hello especifica la suscripción. Para más información, consulte [Límites de Virtual Machines](../azure-subscription-service-limits.md#virtual-machines-limits) en [Límites, cuotas y restricciones de suscripción y servicios de Microsoft Azure](../azure-subscription-service-limits.md).
>
>

### <a name="compute-node-operating-system-and-version"></a>Sistema operativo y versión de nodo de proceso

Cuando se crea un grupo de lote, puede especificar configuración de máquina virtual de Azure de Hola y el tipo de Hola de desea toorun en cada nodo de proceso en el grupo de Hola de sistema operativo. Hola dos tipos de configuraciones disponibles en lote son:

- Hola **configuración de máquina Virtual**, que especifica ese grupo Hola está formada por máquinas virtuales de Azure. Estas máquinas virtuales pueden crearse a partir de imágenes de Linux o Windows. 

    Cuando se crea un grupo en función de la configuración de máquina Virtual de hello, debe especificar no solo Hola tamaño de nodos de Hola y el origen de Hola de hello imágenes que se utilizan toocreate ellos, sino también hello **referencia de la imagen de máquina virtual** hello y Lote **agente nodo SKU** toobe instalado en nodos de Hola. Para más información sobre cómo especificar estas propiedades del grupo, consulte [Aprovisionamiento de nodos de proceso de Linux en grupos del servicio Azure Batch](batch-linux-nodes.md).

- Hola **configuración de servicios de nube**, que especifica ese grupo Hola consta de los nodos de servicios de nube de Azure. Cloud Services proporciona *solo* nodos de proceso Windows.

    Se enumeran los sistemas operativos disponibles para los grupos de configuración de servicios de nube de Hola [versiones del SO invitado de Azure y la matriz de compatibilidad SDK](../cloud-services/cloud-services-guestos-update-matrix.md). Cuando se crea un grupo que contiene los nodos de servicios en la nube, necesita toospecify tamaño de nodo de Hola y su *familia del SO*. Servicios en la nube son tooAzure implementado más rápidamente que las máquinas virtuales que ejecutan Windows. Si desea grupos de nodos de proceso Windows, es posible que Cloud Services proporcione una mejora en el rendimiento en términos de tiempo de implementación.

    * Hola *familia del SO* también determina qué versiones de .NET se instalan con hello SO.
    * Como con roles de trabajo dentro de los servicios de nube, puede especificar un *versión del sistema operativo* (para obtener más información sobre los roles de trabajo, vea hello [más información sobre los servicios de nube](../cloud-services/cloud-services-choose-me.md#tell-me-about-cloud-services) sección Hola [servicios en la nube información general sobre](../cloud-services/cloud-services-choose-me.md)).
    * Como con roles de trabajo, es recomendable que especifique `*` para hello *versión del sistema operativo* para que los nodos de Hola se actualizan automáticamente y no hay ningún trabajo necesario toocater toonewly publican versiones. caso de uso principal de Hola para seleccionar una versión específica del sistema operativo es tooensure compatibilidad de las aplicaciones, lo que permite la compatibilidad con versiones anteriores toobe prueba realizada antes de permitir Hola versión toobe actualizado. Después de la validación, Hola *versión del sistema operativo* para grupo de hello puede actualizarse y se puede instalar la nueva imagen del SO Hola--las tareas en ejecución se interrumpirá y poner en cola.

Cuando se crea un grupo, necesita tooselect Hola adecuado **nodeAgentSkuId**, en función de hello SO de la imagen base de Hola de su disco duro virtual. Puede obtener una asignación de tootheir de identificadores de SKU de agente de nodo disponible referencias de imagen del sistema operativo que realiza la llamada hello [los SKU de agente compatible de nodo de lista](https://docs.microsoft.com/rest/api/batchservice/list-supported-node-agent-skus) operación.

Vea hello [cuenta](#account) sección para obtener información acerca de cómo establecer el modo de asignación de grupo de hello cuando se crea una cuenta de lote.

#### <a name="custom-images-for-virtual-machine-pools"></a>Imágenes personalizadas de grupos de máquinas virtuales

toouse un grupos de máquina Virtual tooprovision de imagen personalizada, crear su cuenta de lote con el modo de asignación de grupo de suscripción de usuario de Hola. Con este modo, se asignan a grupos de proceso por lotes en una suscripción de Hola donde reside la cuenta de hello. Vea hello [cuenta](#account) sección para obtener información acerca de cómo establecer el modo de asignación de grupo de hello cuando se crea una cuenta de lote.

toouse una imagen personalizada, deberá imagen de hello tooprepare generalizándola. Para obtener información acerca de cómo preparar imágenes personalizadas de Linux desde máquinas virtuales de Azure, consulte [capturar un toouse de máquina virtual de Linux de Azure como una plantilla de](../virtual-machines/linux/capture-image-nodejs.md). Para más información acerca de cómo preparar imágenes de Windows personalizadas a partir de máquinas virtuales de Azure, consulte [Crear imágenes de máquina virtual personalizadas con Azure PowerShell](../virtual-machines/windows/tutorial-custom-images.md). 

> [!IMPORTANT]
> Al preparar la imagen personalizada, tenga en siguiente Hola de cuenta:
> - Asegurarse de esa imagen del sistema operativo base Hola usar tooprovision las agrupaciones de lote no se cualquiera previamente instalado las extensiones de Azure, como la extensión de Script personalizado de Hola. Si la imagen de hello contiene una extensión previamente instalada, Azure puede encontrar problemas implementar Hola máquina virtual.
> - Asegúrese de que esa imagen del sistema operativo base Hola que proporcionan usa Hola unidad temporal de forma predeterminada, tal y como hello agente de nodo de lote actualmente espera como unidad temporal predeterminada Hola.
>
>

toocreate un grupo de configuración de máquina Virtual con una imagen personalizada, necesitará uno o cuentas de almacenamiento de Azure estándar más toostore las imágenes de disco duro virtual personalizadas. Las imágenes personalizadas se almacenan como blobs. tooreference personalizado imágenes cuando se crea un grupo, especifique Hola URI de blobs de disco duro virtual de imagen personalizada de Hola para hello [osDisk](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_osdisk) propiedad de hello [virtualMachineConfiguration](https://docs.microsoft.com/rest/api/batchservice/add-a-pool-to-an-account#bk_vmconf) propiedad.

Asegúrese de que las cuentas de almacenamiento cumplen Hola siguiendo criterios:   

- blobs de disco duro virtual de imagen personalizada hello contenedores necesitan toobe en las cuentas de almacenamiento de Hola Hola misma suscripción como Hola cuenta de lote (suscripción de usuario de hello).
- Hola especifica cuentas de almacenamiento necesitan toobe Hola misma región que Hola cuenta de lote.
- Actualmente, solo se admiten las cuentas de almacenamiento estándar de uso general. Almacenamiento Premium de Azure se admitirán en futuras Hola.
- Puede especificar una cuenta de almacenamiento con varios blobs VHD personalizados o varias cuentas de almacenamiento, que tenga cada una un único blob. Le recomendamos que toouse cuentas de almacenamiento varios tooget un mejor rendimiento.
- Un blob de disco duro virtual de imagen personalizado único puede admitir hasta 20 instancias de máquina virtual de Windows o too40 que instancias de VM de Linux. Necesitará toocreate copias de grupos de toocreate blob Hola de disco duro virtual con más máquinas virtuales. Por ejemplo, un grupo con 200 máquinas virtuales de Windows necesita 10 únicos blobs de disco duro virtual especificados para hello **osDisk** propiedad.

toocreate un grupo desde una imagen personalizada con hello portal de Azure:

1. Navegar por cuenta de lote tooyour Hola portal de Azure.
2. En hello **configuración** hoja, seleccione hello **grupos** elemento de menú.
3. En hello **grupos** hoja, seleccione hello **agregar** comando; Hola **Agregar grupo** hoja se mostrarán.
4. Seleccione **imagen personalizada (Linux y Windows)** de hello **tipo de imagen** lista desplegable. portal de Hello muestra hello **imagen personalizada** selector. Elija uno o más VHD de Hola Hola de contenedor y haga clic en mismo **seleccione** botón. 
    Se agregará compatibilidad con varios discos duros virtuales de diferentes cuentas de almacenamiento y los contenedores diferentes en hello futuras.
5. Seleccione Hola correcto **Publisher/oferta/Sku** para los VHD personalizados, seleccione Hola deseado **Caching** modo y, a continuación, rellene todos Hola otros parámetros para el grupo de Hola.
6. toocheck si un grupo se basa en una imagen personalizada, vea hello **sistema operativo** propiedad en la sección de resumen de recursos de Hola de hello **grupo** hoja. valor de Hola de esta propiedad debe ser **imagen de VM personalizada**.
7. Todos los VHD personalizados asociados a un grupo se muestran en el grupo de hello **propiedades** hoja.

### <a name="compute-node-type-and-target-number-of-nodes"></a>Tipo de nodo de proceso y número de nodos de destino

Cuando se crea un grupo, puede especificar qué tipos de nodos de cálculo que desee y Hola número de destino para cada uno. Hola dos tipos de nodos de ejecución son:

- **Nodos de proceso dedicados.** Los nodos de proceso dedicados están reservados para las cargas de trabajo que usted tenga. Son más caros que los nodos de prioridad baja, pero se garantiza que se ve relegado toonever.

- **Nodos de proceso de prioridad baja.** Nodos de prioridad baja sacar partido de exceso de capacidad en Azure toorun las cargas de trabajo por lotes. Los nodos de prioridad baja son menos costosos por hora que los nodos dedicados y habilitan las cargas de trabajo que requieren una gran potencia de proceso. Para obtener más información, vea [Use low-priority VMs with Batch](batch-low-pri-vms.md) (Usar máquinas virtuales de prioridad baja con Batch).

    Los nodos de proceso de prioridad baja pueden verse reemplazados cuando Azure no tiene una capacidad sobrante suficiente. Si un nodo se ve relegado durante la ejecución de tareas, tareas de hello son poner en cola y vuelva a ejecutar una vez que un nodo de proceso vuelve a estar disponible. Nodos de prioridad baja son una buena opción para las cargas de trabajo en tiempo de finalización del trabajo de hello es flexible y trabajo Hola se distribuye entre muchos nodos. Antes de decidir toouse nodos de prioridad baja para su escenario, asegúrese de que ningún trabajo perdido debido toopreemption será toorecreate mínima y sencilla.

    Nodos de proceso de prioridad baja solo están disponibles para las cuentas de lote creadas con el modo de asignación de grupo Hola establecido demasiado**servicio por lotes**.

Puede tener ambos nodos de cálculo de prioridad baja y dedicado en hello mismo grupo. Cada tipo de nodo &mdash; prioridad baja y dedicado &mdash; tiene su propia configuración de destino para el que se puede especificar el número de hello deseado de nodos. 
    
número de nodos de proceso Hello es tooas que se hace referencia una *destino* porque, en algunas situaciones, el grupo no alcancen número deseado de Hola de nodos. Por ejemplo, un grupo no puede lograr destino Hola si alcanza hello [cuota de núcleos](batch-quota-limit.md) para el lote de la cuenta en primer lugar. O bien, grupo de hello no podría lograr destino Hola si ha aplicado una escala automática grupo toohello fórmulas que limita el número máximo de Hola de nodos.

Para obtener información sobre los precios de los nodos de proceso de prioridad baja y dedicados, vea [Precios de Batch](https://azure.microsoft.com/pricing/details/batch/).

### <a name="size-of-hello-compute-nodes"></a>Tamaño de los nodos de cálculo de Hola

**configuración de Servicios en la nube** aparecen en [Tamaños de los servicios en la nube](../cloud-services/cloud-services-sizes-specs.md). Batch admite todos los tamaños de Cloud Services excepto `ExtraSmall`, `STANDARD_A1_V2` y `STANDARD_A2_V2`.

Los tamaños de los nodos de proceso de la **configuración de máquina virtual** se muestran en [Tamaños de las máquinas virtuales Linux en Azure](../virtual-machines/linux/sizes.md) y [Tamaños de las máquinas virtuales Windows en Azure](../virtual-machines/windows/sizes.md). Batch admite todos los tamaños de máquina virtual de Azure excepto `STANDARD_A0` y aquellos con Premium Storage (series `STANDARD_GS`, `STANDARD_DS` y `STANDARD_DSV2`).

Al seleccionar un tamaño de nodo de proceso, considere la posibilidad de hello características y requisitos de las aplicaciones de Hola que se va a ejecutar en nodos de Hola. Aspectos como si la aplicación hello es multiproceso y la cantidad de memoria que consume puede ayudar a determinan tamaño de nodo de hello más adecuado y rentable. Es habitual tooselect un tamaño de nodo suponiendo que una tarea se ejecutará en un nodo a la vez. Sin embargo, es posible toohave varias tareas (y, por tanto, varias instancias de aplicación) [ejecutar en paralelo](batch-parallel-node-tasks.md) en nodos de ejecución durante la ejecución del trabajo. En este caso, es común toochoose una petición de hello aumentado más grande de tooaccommodate tamaño de nodo de ejecución de tareas paralelas. Para más información, consulte [Directiva de programación de tareas](#task-scheduling-policy).

Todos los nodos de hello en un grupo son Hola mismo tamaño. Si piensa toorun aplicaciones con diferentes requisitos de sistema y niveles de carga, se recomienda que utilice grupos distintos.

### <a name="scaling-policy"></a>Directiva de escalado

Para las cargas de trabajo dinámicos, puede escribir y aplicar un [fórmula de escalado automático](#scaling-compute-resources) tooa grupo. Hola servicio por lotes se evalúa como la fórmula y ajusta Hola número de nodos dentro de grupo de hello en función de diversos grupo, trabajo y los parámetros de tareas que se pueden especificar periódicamente.

### <a name="task-scheduling-policy"></a>Directiva de programación de tareas

Hola [máximo de tareas por nodo](batch-parallel-node-tasks.md) opción de configuración determina el número máximo de Hola de tareas que se pueden ejecutar en paralelo en cada nodo de proceso en el grupo de Hola.

configuración predeterminada de Hello especifica que una tarea a la vez que se ejecuta en un nodo, pero existen escenarios donde resulta beneficioso toohave dos o más tareas que se ejecuta en un nodo al mismo tiempo. Vea hello [escenario de ejemplo](batch-parallel-node-tasks.md#example-scenario) en hello [tareas simultáneas nodo](batch-parallel-node-tasks.md) toosee artículo cómo puede beneficiarse de varias tareas por nodo.

También puede especificar un *tipo de relleno* que determina si distribuye uniformemente tareas Hola a todos los nodos en un grupo de lote o módulos de cada nodo con el número máximo de Hola de tareas antes de asignar el nodo de tooanother de tareas.

### <a name="communication-status-for-compute-nodes"></a>Estado de comunicación para nodos de proceso

En la mayoría de los escenarios, las tareas funcionan de forma independiente y no es necesario toocommunicate entre sí. Sin embargo, hay algunas aplicaciones en las que las tareas deben comunicarse, como en los [escenarios MPI](batch-mpi.md).

Puede configurar un grupo tooallow **la comunicación entre nodos**, para que puedan comunicarse nodos dentro de un grupo en tiempo de ejecución. Cuando se habilita la comunicación entre nodos, los nodos en grupos de configuración de Cloud Services pueden comunicarse entre sí en los puertos superiores a 1100, mientras que los grupos de configuración de máquina virtual no restringen el tráfico en ningún puerto.

Tenga en cuenta que habilitar la comunicación entre nodos también afecta la colocación de Hola de nodos de hello en los clústeres y puede limitar el número máximo de Hola de nodos en un grupo debido a restricciones de implementación. Si la aplicación no requiere la comunicación entre nodos, Hola servicio por lotes puede asignar a un número potencialmente grande de nodos toohello grupo de clústeres distintos muchas y tooenable de centros de datos mayor potencia de procesamiento en paralelo.

### <a name="start-tasks-for-compute-nodes"></a>Tareas de inicio para nodos de proceso

Hola opcional *Iniciar tarea* se ejecuta en cada nodo, ese nodo une a grupo de Hola y se reinicia cada vez que un nodo o se restablece la imagen inicial. tarea de inicio de Hello es especialmente útil para preparar los nodos de proceso para la ejecución de Hola de tareas, como la instalación de aplicaciones de Hola que las tareas se ejecutan en nodos de proceso de Hola.

### <a name="application-packages"></a>paquetes de aplicación

Puede especificar [paquetes de aplicación](#application-packages) toodeploy toohello nodos de cálculo en el grupo de Hola. Paquetes de aplicación proporcionan implementación simplificada y control de versiones de aplicaciones de Hola que se ejecutan las tareas. Los paquetes de aplicación que se especifiquen para un grupo se instalarán en todos los nodos que se unan al grupo cada vez que un nodo se reinicie o se restablezca la imagen inicial.

> [!NOTE]
> Los paquetes de aplicaciones se admiten en todos los grupos de Batch creados después del 5 de julio de 2017. Ahora se admiten en los grupos de lote creados entre el 10 de marzo de 2016 y 5 de julio de 2017 solo si se creó el grupo de hello mediante una configuración del servicio de nube. Los grupos de lote creados too10 anteriores de marzo de 2016 son compatibles con los paquetes de aplicaciones. Para obtener más información sobre el uso de la aplicación paquetes toodeploy los nodos de proceso por lotes de tooyour de aplicaciones, consulte [implementar aplicaciones toocompute nodos con paquetes de aplicaciones de lote](batch-application-packages.md).
>
>

### <a name="network-configuration"></a>Network configuration (Configuración de red)

Puede especificar las subredes Hola de un Azure [red virtual (VNet)](../virtual-network/virtual-networks-overview.md) en proceso del grupo de qué Hola deben crearse los nodos. Vea hello [configuración del grupo de red](#pool-network-configuration) sección para obtener más información.


## <a name="job"></a>Trabajo
Un trabajo es una colección de tareas. Administra cómo se realiza el cálculo por sus tareas en los nodos de proceso de hello en un grupo.

* trabajo de Hello especifica hello **grupo** en qué hello es toobe ejecutar el trabajo. Puede crear un grupo para cada trabajo o usar uno solo para muchos de ellos. Puede crear un grupo para cada trabajo asociado con una programación de trabajo o para todos los trabajos asociados con ella.
* Puede especificar una **prioridad del trabajo**opcional. Cuando se envía un trabajo con una prioridad más alta que los trabajos que están actualmente en curso, se insertan tareas hello para el trabajo de prioridad más alta de hello en cola de Hola por delante de las tareas para los trabajos de menor prioridad Hola. No adelantarán a las tareas de trabajos de prioridad más baja que ya estén en ejecución.
* Puede usar trabajo **restricciones** toospecify ciertos límites para los trabajos:

    Puede establecer un **wallclock máximo tiempo**, de modo que si un trabajo se ejecuta durante más tiempo máximo wallclock de Hola que se especifica, se terminan trabajo hello y todas sus tareas.

    Batch puede detectar tareas con errores y después volver a intentarlas. Puede especificar hello **número máximo de reintentos de tarea** como una restricción, incluso si una tarea es *siempre* o *nunca* vuelve a intentar. Volver a intentar una tarea significa que la tarea hello toobe poner en cola, vuelva a ejecutar.
* La aplicación cliente puede agregar trabajo tooa de tareas, o puede especificar un [tarea del Administrador de trabajos](#job-manager-task). Una tarea del Administrador de trabajo contiene información de Hola que es necesario toocreate Hola requiere tareas de un trabajo, con la tarea del Administrador de trabajos de Hola que se ejecute en uno de hello nodos de cálculo en el grupo de Hola. Hello tarea del Administrador de trabajos se trata específicamente por lote--está en la cola en cuanto trabajo Hola se crea y se reinicia si se produce un error. Es una tarea del Administrador de trabajos *requiere* para los trabajos creados por un [la programación del trabajo](#scheduled-jobs) porque es Hola únicas forma toodefine Hola tareas antes de que se crea una instancia de trabajo de Hola.
* De forma predeterminada, trabajos permanecen en estado activo de hello cuando complete todas las tareas de trabajo de Hola. Puede cambiar este comportamiento para que hello trabajo finalizará automáticamente cuando complete todas las tareas de trabajo de Hola. Conjunto Hola trabajo **onAllTasksComplete** propiedad ([OnAllTasksComplete] [ net_onalltaskscomplete] en .NET de lote) demasiado*terminatejob* tooautomatically terminar el trabajo de hello cuando todas sus tareas están en estado de hello completado.

    Tenga en cuenta que el servicio por lotes Hola considera que un trabajo con *no* toohave tareas completado todas sus tareas. Por lo tanto, esta opción se utiliza normalmente con una [tarea del administrador de trabajos](#job-manager-task). Si desea que la terminación de trabajo automática toouse sin un administrador de trabajos, debe establecer inicialmente un nuevo trabajo **onAllTasksComplete** propiedad demasiado*noaction*, a continuación, establezca demasiado*terminatejob* solo después de que haya terminado de agregar tareas toohello trabajo.

### <a name="job-priority"></a>prioridad del trabajo
Puede asignar un toojobs de prioridad que se crean en el lote. Hola servicio por lotes usa el valor de prioridad de Hola de hello toodetermine Hola de órdenes de programación de trabajos en una cuenta (Esto no es toobe confundirse con un [trabajo programado](#scheduled-jobs)). los valores de prioridad de Hello comprendidos entre -1000 too1000, con -1000 Hola de prioridad más baja y 1000 está Hola más alto. prioridad de hello tooupdate de un trabajo, llamada hello [actualizar propiedades de Hola de un trabajo] [ rest_update_job] operación (REST de lote), o modificar hello [CloudJob.Priority] [ net_cloudjob_priority] propiedad (lote. NET).

Dentro de hello misma cuenta, mayor prioridad trabajos tienen la prioridad de programación a través de los trabajos con prioridad inferior. Un trabajo con un valor de prioridad mayor en una cuenta no tiene precedencia de programación sobre otro trabajo con un valor de prioridad inferior de una cuenta diferente.

La programación de trabajos entre los grupos es independiente. Entre grupos diferentes, no se garantiza que un trabajo con una prioridad más alta se programe antes si el grupo asociado tiene pocos nodos inactivos. Hola mismo grupo, los trabajos con hello mismo nivel de prioridad tienen la misma probabilidad de estar programado.

### <a name="scheduled-jobs"></a>Scheduled jobs
[Programaciones de trabajos] [ rest_job_schedules] habilitar los trabajos recurrentes toocreate dentro de hello servicio por lotes. Una programación de trabajo especifica cuando los trabajos e incluye especificaciones de Hola para hello trabajos toobe ejecutar toorun. Puede especificar cuánto tiempo duración Hola de programación de hello--y cuando programación Hola está en vigor, y con qué frecuencia se crean trabajos durante Hola programado período.

## <a name="task"></a>Tarea
Una tarea es una unidad de cálculo que está asociada con un trabajo. Se ejecuta en un nodo. Las tareas se asignan tooa nodo para su ejecución, o se ponen en cola hasta que un nodo deja de estar disponible. En términos simples, una tarea ejecuta uno o más programas o scripts en un proceso nodo tooperform Hola trabajo que necesita.

Cuando crea una tarea, puede especificar:

* Hola **línea de comandos** para la tarea hello. Se trata de línea de comandos de Hola que se ejecuta la aplicación o el script en el nodo de proceso de Hola.

    Es importante toonote que Hola de línea de comandos no se ejecute en un shell. Por lo tanto, forma nativa no puede aprovechar las características de shell como [variable de entorno](#environment-settings-for-tasks) expansión (Esto incluye hello `PATH`). tootake provecho de estas características, debe invocar shell hello en línea de comandos de hello: por ejemplo, iniciando `cmd.exe` en nodos de Windows o `/bin/sh` en Linux:

    `cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

    `/bin/sh -c MyTaskApplication $MY_ENV_VAR`

    Si las tareas deben toorun una aplicación o un script que no esté en Hola del nodo `PATH` o hacer referencia a variables de entorno, invoque shell Hola explícitamente en la línea de comandos de tarea de Hola.
* **Archivos de recursos** que contienen hello toobe de datos procesado. Estos archivos son nodo toohello copia de forma automática desde el almacenamiento de blobs en una cuenta de almacenamiento de Azure de propósito general antes de que se ejecuta la línea de comandos de la tarea hello. Para obtener más información, consulte las secciones de hello [tarea de inicio](#start-task) y [archivos y directorios](#files-and-directories).
* Hola **variables de entorno** que son requeridos por la aplicación. Para obtener más información, vea hello [configuración del entorno para tareas](#environment-settings-for-tasks) sección.
* Hola **restricciones** bajo qué Hola debe ejecutar la tarea. Por ejemplo, las restricciones incluyen el tiempo máximo de hello esa tarea Hola se permite toorun, número máximo de Hola de veces que se debe reintentar una tarea fallida, y el tiempo máximo de Hola que se conservan los archivos en el directorio de trabajo de la tarea hello.
* **Paquetes de aplicación** toodeploy toohello en qué Hola está programada toorun tarea de nodo de proceso. [Paquetes de aplicación](#application-packages) proporcionar implementación simplificada y control de versiones de aplicaciones de Hola que se ejecutan las tareas. Paquetes de aplicación de nivel de tarea son especialmente útiles en entornos de grupo compartido, donde distintos trabajos que se ejecutan en un grupo y no se elimina el grupo de hello cuando se completa un trabajo. Si el trabajo tiene menos tareas que los nodos de grupo de hello, paquetes de aplicaciones de la tarea pueden minimizar la transferencia de datos ya que la aplicación está implementada toohello solo nodos que se ejecutan las tareas.

Además tootasks definir tooperform cálculo en un nodo, Hola después tareas especiales también se proporciona Hola servicio por lotes:

* [Tarea de inicio](#start-task)
* [Tareas del Administrador de trabajos](#job-manager-task)
* [Tareas de preparación y liberación de trabajos](#job-preparation-and-release-tasks)
* [Tareas de instancias múltiples (MPI)](#multi-instance-tasks)
* [Dependencias de las tareas](#task-dependencies)

### <a name="start-task"></a>Tarea de inicio
Asociando un **Iniciar tarea** con un grupo, puede preparar Hola OE de sus nodos. Por ejemplo, puede realizar acciones tales como instalar aplicaciones de Hola que se ejecutan las tareas o iniciar procesos en segundo plano. tarea de inicio de Hola se ejecuta cada vez que inicia un nodo, mientras permanece en el grupo de hello--primero incluso cuando el nodo de hello es agregar grupo toohello y cuando se reinicia o restablece la imagen inicial.

Una ventaja principal de la tarea de inicio de hello es que puede contener toda información de Hola que sea necesario tooconfigure de un nodo de proceso e instalar aplicaciones de Hola que son necesarias para la ejecución de la tarea. Por lo tanto, es tan simple como especificar el número de nodos de destino nuevo Hola aumentar Hola número de nodos en un grupo. tarea de inicio de Hello proporciona información de Hola de servicio de lote de Hola que es necesario tooconfigure Hola nuevos nodos y llegar a ellos listo para aceptar las tareas.

Como con cualquier tarea del lote de Azure, puede especificar una lista de **archivos de recursos** en [el almacenamiento de Azure][azure_storage], además tooa **línea de comandos** toobe ejecutar. servicio de lote de Hello nodo de toohello de archivos de recursos de Hola la primera copia del almacenamiento de Azure y, a continuación, ejecuta la línea de comandos de Hola. Para una tarea de inicio de grupo, lista de archivos de Hola normalmente contiene la aplicación de la tarea de hello y sus dependencias.

Sin embargo, tarea de inicio de hello podría incluir también toobe de datos de referencia utilizado por todas las tareas que se ejecutan en nodos de proceso de Hola. Por ejemplo, puede realizar la línea de comandos de una tarea de inicio una `robocopy` operación toocopy archivos de la aplicación (que se especificaron como archivos de recursos y descargan nodo toohello) de hello iniciar la tarea [directorio de trabajo](#files-and-directories) toohello [carpeta compartida](#files-and-directories), y, a continuación, ejecute un archivo MSI o `setup.exe`.

Es conveniente normalmente hello toowait de servicio de lote para toocomplete de tarea de inicio de hello antes de considerar Hola tareas listo toobe asignado de nodo, pero puede configurarlo.

Si se produce un error en una tarea de inicio en un nodo de proceso, a continuación, hello estado del nodo de Hola se tooreflect actualizada Hola error, y nodo hello no está asignado a las tareas. Una tarea de inicio puede producir un error si hay un problema de copiar sus archivos de recursos de almacenamiento, o si el proceso de hello ejecutado por su línea de comandos devuelve un código de salida distinto de cero.

Si agrega o actualiza la tarea de inicio de hello para un grupo existente, debe reiniciar el equipo de sus nodos de proceso para hello inicio tarea toobe aplica toohello nodos.

>[!NOTE]
> Hello tamaño total de una tarea de inicio debe ser menor o igual too32768 caracteres, incluidos los archivos de recursos y las variables de entorno. tooensure que la tarea de inicio cumple este requisito, puede usar uno de estos dos enfoques:
>
> 1. Puede utilizar aplicaciones de toodistribute de paquetes de aplicación o datos en cada nodo en el grupo de lote. Para obtener más información acerca de los paquetes de aplicación, consulte [implementar aplicaciones toocompute nodos con paquetes de aplicaciones de lote](batch-application-packages.md).
> 2. Puede crear manualmente un archivo comprimido que contenga los archivos de aplicación. Cargue el almacenamiento de archivo comprimido tooAzure como un blob. Especificar el archivo de hello zip como un archivo de recursos para la tarea de inicio. Antes de ejecutar línea de comandos de hello para la tarea de inicio, descomprima el archivo hello desde línea de comandos de Hola. 
>
>    archivo de hello toounzip, puede usar Hola archivar la herramienta de su elección. Necesitará la herramienta de hello tooinclude que usar archive de hello toounzip como un archivo de recursos para la tarea de inicio de Hola.
>
>

### <a name="job-manager-task"></a>Tareas del Administrador de trabajos
Normalmente, se utiliza un **tarea del Administrador de trabajos** toocontrol o monitor de trabajo de ejecución, por ejemplo, toocreate y enviar tareas de Hola para un trabajo, determinar toorun tareas adicionales y determinar cuándo el trabajo ha finalizado. Sin embargo, una tarea del Administrador de trabajos no es actividades toothese restringido. Es una tarea completa que puede realizar todas las acciones que se requieren para el trabajo de Hola. Por ejemplo, una tarea del Administrador de trabajos puede descargar un archivo que se especifica como un parámetro, analizar Hola contenido de ese archivo y enviar tareas adicionales en función de dicho contenido.

Una tarea del administrador de trabajos se inicia antes que cualquier otra. Proporciona Hola siguientes características:

* Automáticamente se envía como una tarea por hello servicio por lotes cuando se crea el trabajo de Hola.
* Se está programada tooexecute antes de hello otras tareas de un trabajo.
* Su nodo asociado es toobe última hello quitado de un grupo al grupo de hello es que se producen reducciones.
* Su terminación puede ser toohello relacionados de finalización de todas las tareas de trabajo de Hola.
* Una tarea del Administrador de trabajos tiene prioridad más alta de hello cuando necesita toobe reiniciar. Si no hay un nodo inactivo, Hola servicio por lotes puede terminarse uno de hello otras tareas en ejecución en sala de hello grupo toomake para toorun de tareas de administrador de trabajos de Hola.
* Una tarea del Administrador de trabajo en un trabajo no tiene prioridad sobre las tareas de Hola de otros trabajos. Entre trabajos, solo se tienen en cuenta las prioridades de nivel de trabajo.

### <a name="job-preparation-and-release-tasks"></a>Tareas de preparación y liberación de trabajos
El servicio Batch proporciona la tarea de preparación del trabajo para la configuración de ejecución previa al trabajo. Tareas de liberación del trabajo para el mantenimiento o la limpieza posteriores al trabajo.

* **Tareas de preparación del trabajo**: una tarea de preparación de trabajo se ejecuta en todos los nodos de proceso que son tareas programadas toorun, antes de cualquier Hola se ejecutan otras tareas de trabajo. Puede usar un datos de toocopy de tareas de preparación de trabajo que se comparten entre todas las tareas, pero es trabajo toohello único, por ejemplo.
* **Tarea de liberación del trabajo**: cuando haya finalizado un trabajo, una tarea de liberación del trabajo se ejecuta en cada nodo de grupo de Hola que ejecuta al menos una tarea. Puede utilizar un trabajo versión toodelete datos de la tarea que se copian en la tarea de preparación del trabajo de Hola o toocompress y la carga de datos del registro diagnóstico, por ejemplo.

Ambos preparación del trabajo y tareas de versión permiten toospecify un toorun de línea de comandos cuando se invoca la tarea hello. Las tareas ofrecen características tales como descarga de archivos, ejecución con elevación de privilegios, variables de entorno personalizadas, duración máxima de ejecución, número de reintentos y tiempo de retención de archivo.

Para obtener más información sobre las tareas de preparación y liberación del trabajo, consulte [Ejecución de las tareas de preparación y realización de trabajos en los nodos de proceso de Azure Batch](batch-job-prep-release.md).

### <a name="multi-instance-task"></a>Tarea de instancias múltiples
A [tareas varias instancias](batch-mpi.md) es una tarea que esté configurado toorun en más de un nodo de ejecución al mismo tiempo. Con las tareas de varias instancias, puede habilitar el alto rendimiento informáticos escenarios que requieren un grupo de nodos de proceso que asignan juntos tooprocess una carga de trabajo única (como pasar interfaz mensajes (MPI)).

Para obtener una explicación detallada sobre cómo ejecutar trabajos de MPI en lote mediante el uso de la biblioteca de .NET de lotes de hello, visite [varias instancias de uso tareas toorun las aplicaciones de interfaz de paso de mensajes (MPI) en Azure Batch](batch-mpi.md).

### <a name="task-dependencies"></a>Dependencias de las tareas
[Las dependencias entre tareas](batch-task-dependencies.md), como Hola nombre indica, le permiten toospecify que depende una tarea en la realización de Hola de otras tareas antes de su ejecución. Esta característica proporciona compatibilidad para situaciones en que una tarea "nivel inferior" consume salida de hello de una tarea "precede en la cadena"--o cuando una tarea de nivel superior realiza algunas operaciones de inicialización que requiere una tarea de nivel inferior. toouse esta característica, debe primero las dependencias de tareas habilitar en el proceso por lotes. A continuación, para cada tarea que depende de otro (o muchos otros), especifique las tareas de Hola que depende de dicha tarea.

Con las dependencias de tareas, puede configurar escenarios como Hola siguiente:

* *taskB* depende de *taskA* (la ejecución de *taskB* no se iniciará hasta que *taskA* se haya completado).
* *taskC* depende de *taskA* y *taskB*.
* *taskD* depende de un intervalo de tareas, como las tareas de *1* a *10*, antes de ejecutarse.

Extraer del repositorio [tareas dependencias en Azure Batch](batch-task-dependencies.md) hello y [TaskDependencies] [ github_sample_taskdeps] código de ejemplo de Hola [ejemplos de lote de azure] [ github_samples] Repositorio de GitHub para más información detallada sobre esta característica.

## <a name="environment-settings-for-tasks"></a>Configuración del entorno para las tareas
Cada tarea ejecutada por hello servicio por lotes tiene variables de tooenvironment de acceso que establece en nodos de proceso. Esto incluye las variables de entorno definidas por hello servicio por lotes ([definido por el servicio][msdn_env_vars]) y las variables de entorno personalizado que se pueden definir para las tareas. las aplicaciones de Hola y secuencias de comandos que se ejecutan las tareas tienen acceso a variables de entorno de toothese durante la ejecución.

Se pueden establecer variables de entorno personalizado en el nivel de tarea o trabajo de hello rellenando hello *configuración del entorno* propiedad para estas entidades. Por ejemplo, vea hello [agregar un trabajo de tarea tooa] [ rest_add_task] operación (API de REST de lote) o hello [CloudTask.EnvironmentSettings] [ net_cloudtask_env] y [ CloudJob.CommonEnvironmentSettings] [ net_job_env] propiedades en .NET de lote.

La aplicación de cliente o servicio puede obtener variables de entorno de una tarea, definido por el servicio y personalizadas, mediante el uso de hello [obtener información acerca de una tarea] [ rest_get_task_info] operación (REST de lote) o mediante el acceso a Hola [CloudTask.EnvironmentSettings] [ net_cloudtask_env] propiedad (lote. NET). Pueden tener acceso a estos procesos que se ejecutan en un nodo de proceso y otras variables de entorno en el nodo de hello, por ejemplo, mediante el uso de Hola familiarizado `%VARIABLE_NAME%` (Windows) o `$VARIABLE_NAME` sintaxis (Linux).

Puede encontrar una lista completa de las variables de entorno definidas por el servicio en [Compute node environment variables][msdn_env_vars] (Variables de entorno en los nodos de proceso).

## <a name="files-and-directories"></a>Archivos y directorios
Cada tarea tiene un *directorio de trabajo* en el que se crean ninguno o más archivos y directorios. Este directorio de trabajo puede utilizarse para almacenar programa Hola ejecutada por la tarea hello, datos de Hola que procesa, y Hola de salida del procesamiento de Hola que lleva a cabo. Usuario de la tarea de hello propiedad todos los archivos y directorios de una tarea.

Hola servicio por lotes expone una parte del sistema de archivos de hello en un nodo como hello *directorio raíz*. Tareas pueden tener acceso a directorio raíz de hello haciendo referencia a hello `AZ_BATCH_NODE_ROOT_DIR` variable de entorno. Para obtener más información sobre el uso de variables de entorno, consulte [Configuración del entorno para las tareas](#environment-settings-for-tasks).

directorio raíz de Hello contiene Hola siguiendo la estructura de directorios:

![Estructura de directorio de nodo de proceso][1]

* **compartido**: este directorio proporciona acceso de lectura/escritura demasiado*todos los* tareas que se ejecutan en un nodo. Cualquier tarea que se ejecuta en el nodo de hello puede crear, leer, actualizar y eliminar archivos en este directorio. Tareas pueden tener acceso a este directorio haciendo referencia a hello `AZ_BATCH_NODE_SHARED_DIR` variable de entorno.
* **startup**: una tarea de inicio usa este directorio como directorio de trabajo. Todos los archivos de Hola que son nodos de toohello descargado por la tarea de inicio de Hola se almacenan aquí. tarea de inicio de Hello puede crear, leer, actualizar y eliminar archivos en este directorio. Tareas pueden tener acceso a este directorio haciendo referencia a hello `AZ_BATCH_NODE_STARTUP_DIR` variable de entorno.
* **Tareas**: se crea un directorio para cada tarea que se ejecuta en el nodo de Hola. Se tiene acceso haciendo referencia a hello `AZ_BATCH_TASK_DIR` variable de entorno.

    Dentro de cada directorio de la tarea, Hola servicio por lotes crea un directorio de trabajo (`wd`) cuya ruta de acceso único especificado por hello `AZ_BATCH_TASK_WORKING_DIR` variable de entorno. Este directorio proporciona la tarea de toohello de acceso de lectura/escritura. tarea Hello puede crear, leer, actualizar y eliminar archivos en este directorio. Este directorio se conserva en función de hello *RetentionTime* restricción que se especifica para la tarea hello.

    `stdout.txt`y `stderr.txt`: estos archivos se escriben toohello carpeta de tareas durante la ejecución de Hola de tarea hello.

> [!IMPORTANT]
> Cuando se quita un nodo de grupo de hello, *todos los* de Hola se quitan los archivos que se almacenan en el nodo de Hola.
>
>

## <a name="application-packages"></a>paquetes de aplicación
Hola [paquetes de aplicación](batch-application-packages.md) característica proporciona una administración sencilla y la implementación de aplicaciones de nodos de proceso de toohello en los grupos. Puede cargar y administrar varias versiones del programa Hola a las aplicaciones se ejecutan las tareas, incluidos sus archivos binarios y archivos auxiliares. A continuación, se puede implementar automáticamente una o varias de estas aplicaciones toohello nodos de cálculo en el grupo.

Puede especificar los paquetes de aplicación en el nivel de grupo y tarea de Hola. Cuando se especifican que los paquetes de aplicación de grupo, aplicación hello es nodo tooevery implementado en el grupo de Hola. Al especificar los paquetes de aplicación de tareas, aplicación hello es implementado toonodes única que están programado toorun al menos una de las tareas del trabajo de hello, justo antes de Hola se ejecuta la línea de comandos de la tarea.

Identificadores de lote Hola detalles sobre cómo trabajar con el almacenamiento de Azure toostore los paquetes de aplicaciones e implementación toocompute nodos, por lo que se puede simplificar la sobrecarga de administración y su código.

toofind más información acerca de la característica de paquete de aplicación Hola, visite [implementar aplicaciones toocompute nodos con paquetes de aplicaciones de lote](batch-application-packages.md).

> [!NOTE]
> Si agrega tooan de paquetes de aplicación de grupo *existente* grupo, debe reiniciar el equipo de sus nodos de proceso para los paquetes de aplicación hello toobe implementa toohello nodos.
>
>

## <a name="pool-and-compute-node-lifetime"></a>Vigencia de grupo y nodo de proceso
Al diseñar la solución de lote de Azure, tiene toomake una decisión de diseño acerca de cómo y cuando se crean grupos y cuánto tiempo nodos dentro de esos grupos se mantienen a disposición de proceso.

En un extremo del espectro de hello, puede crear un grupo para cada trabajo que se envía y eliminar grupo Hola tan pronto como las tareas finalizan la ejecución. Esto maximiza el uso porque solo se asignan nodos hello cuando sea preciso y apagar en cuanto están inactivas. Aunque esto significa que trabajo Hola debe esperar Hola nodos toobe asignado, es importante toonote que las tareas están programadas para ejecutarse en cuanto nodos existen individualmente, asignado y Hola se completó la tarea de inicio. Lote *no* espere a que todos los nodos dentro de un grupo están disponibles antes de asignar tareas toohello nodos. Esto garantiza la utilización máxima de todos los nodos disponibles.

En hello otro extremo del espectro de hello, si tiene trabajos iniciar inmediatamente es la prioridad más alta de hello, puede crear un grupo de antemano y disponer de sus nodos antes de que los trabajos se envían. En este escenario, las tareas se pueden iniciar inmediatamente, pero nodos podrían permanecen inactivos mientras se esperaba para ellos toobe asignado.

Normalmente, se utiliza un enfoque combinado para controlar una carga variable, pero en curso. Puede tener un grupo que se envían a varios trabajos, pero pueden escalar el número de Hola de nodos hacia arriba o hacia abajo según la carga de trabajo de toohello (vea [ajuste de escala en los recursos informáticos](#scaling-compute-resources) Hola siguiente sección). Puede realizar esto de manera reactiva, según la carga actual o de forma anticipada si se puede predecir la carga.

## <a name="virtual-network-vnet-and-firewall-configuration"></a>Configuración de red virtual y de firewall 

Cuando se aprovisiona un conjunto de nodos de proceso de Azure Batch, puede asociar el grupo de hello con una subred de un Azure [red virtual (VNet)](../virtual-network/virtual-networks-overview.md). toolearn más acerca de cómo crear una red virtual con subredes, vea [crear una red virtual de Azure con subredes](../virtual-network/virtual-networks-create-vnet-arm-pportal.md). 

 * Hola red virtual asociada a un grupo debe ser:

   * En hello Azure mismo **región** como Hola cuenta de lote de Azure.
   * En Hola mismo **suscripción** como Hola cuenta de lote de Azure.

* tipo de Hola de red virtual admitida depende de cómo se asignan grupos de hello cuenta de lote:

    - Si el modo de asignación de grupo de Hola para su cuenta de lote se establece tooBatch servicio, entonces puede asignar una toopools única red virtual creados con hello **configuración de servicios de nube**. Además, Hola especifica la que red virtual debe crearse con el modelo de implementación clásica de Hola. No se admiten redes virtuales creadas con el modelo de implementación de hello Azure Resource Manager.
 
    - Si el modo de asignación de grupo de Hola para su cuenta de lote se establece tooUser suscripción, entonces puede asignar una toopools única red virtual creados con hello **configuración de máquina Virtual**. Los grupos creados con hello **configuración del servicio de nube** no son compatibles. Hola que red virtual asociado puede crearse con el modelo de implementación de Azure Resource Manager Hola o modelo de implementación clásica de Hola.

    Para una tabla que resume la compatibilidad de red virtual, según el modo de asignación de toopool, vea hello [modo de asignación de grupo](#pool-allocation-mode) sección.

* Si el modo de asignación de grupo de Hola para su cuenta de lote se establece tooBatch servicio, debe proporcionar permisos para hello tooaccess principal del servicio de lote Hola red virtual. Hola red virtual debe asignar Hola [Classic Virtual Machine Contributor Role-Based Access Control (RBAC)](https://azure.microsoft.com/documentation/articles/role-based-access-built-in-roles/#classic-virtual-machine-contributor) entidad de servicio de rol toohello por lotes. Si Hola especificado no se ha proporcionado el rol RBAC, servicio de lote de hello devuelve 400 (solicitud incorrecta). rol de hello tooadd Hola portal de Azure:

    1. Seleccione hello **red virtual**, a continuación, **(de índices IAM) de control de acceso** > **Roles** > **colaborador de la máquina Virtual**  >  **Agregar**.
    2. En hello **agregar permisos** hoja, seleccione hello **colaborador de la máquina Virtual** rol.
    3. En hello **agregar permisos** hoja, busque Hola API de lote. Buscar cada una de estas cadenas a su vez hasta que encuentre Hola API:
        1. **MicrosoftAzureBatch**.
        2. **Microsoft Azure Batch**. Los inquilinos más recientes de Azure AD pueden utilizar este nombre.
        3. **ddbf3205-c6bd-46ae-8127-60eb93363864** es Id. de Hola para hello API de lote. 
    3. Seleccione Hola entidad de servicio de API de lote. 
    4. Haga clic en **Guardar**.

        ![Asignar la entidad de servicio de tooBatch de rol de colaborador de VM](./media/batch-api-basics/iam-add-role.png)


* Hola especifica la subred debe disponer de suficiente libre **direcciones IP** tooaccommodate Hola número total de nodos de destino; es decir, Hola suma de hello `targetDedicatedNodes` y `targetLowPriorityNodes` propiedades del grupo de Hola. Si subred hello no tiene suficientes direcciones IP libres, Hola servicio por lotes parcialmente asigna los nodos de proceso de hello en el grupo de Hola y devuelve un error de cambio de tamaño.

* Hola especificado subred debe permitir la comunicación de toobe de servicio de lote de hello tooschedule capaz de tareas en los nodos de proceso de Hola. Si los nodos de proceso de comunicación toohello denegado por un **grupo de seguridad de red (NSG)** asociada Hola de red virtual, Hola servicio por lotes establece el estado de Hola Hola de nodos de ejecución demasiado**inutilizable**.

* Si Hola especifica la red virtual esté asociada **grupos de seguridad de red (NSG)** o un **firewall**, a continuación, algunos puertos de sistema reservado deben estar habilitados para las comunicaciones entrantes:

- Para los grupos creados con una configuración de máquina virtual, habilite los puertos 29876 y 29877, así como el puerto 22 para Linux y el 3389 para Windows. 
- Para los grupos creados con una configuración de servicio en la nube, habilite los puertos 10100, 20100 y 30100. 
- Habilite las conexiones salientes tooAzure almacenamiento en el puerto 443. Además, asegúrese de que todos los servidores DNS personalizados que dan servicio a red virtual pueden resolver el punto de conexión de Azure Storage. En concreto, una dirección URL de formulario de hello `<account>.table.core.windows.net` debe poderse resolver.

    Hello tabla siguiente describen Hola puertos que necesite tooenable para grupos que ha creado con la configuración de máquina virtual de Hola entrantes:

    |    Puertos de destino    |    Dirección IP de origen      |    ¿Agrega Batch los grupos de seguridad de red?    |    ¿Es necesario para toobe de máquina virtual puede usar?    |    Acción del usuario   |
    |---------------------------|---------------------------|----------------------------|-------------------------------------|-----------------------|
    |    <ul><li>Para los grupos creados con la configuración de máquina virtual de hello: 29876, 29877</li><li>Para los grupos creados con la configuración del servicio de nube de hello: 10100, 20100, 30100</li></ul>         |    Solo direcciones IP de rol de servicio de Batch |    Sí. Lote agrega NSG a nivel de Hola de red tooVMs de interfaces (NIC) que están conectados. Estos grupos de seguridad de red permiten el tráfico únicamente desde las direcciones IP de rol de servicio de Batch. Incluso si abrir estos puertos para hello todo el sitio web, obtener bloqueará el tráfico de hello en hello NIC. |    Sí  |  No es necesario toospecify un NSG, como proceso por lotes permite únicamente las direcciones IP de lote. <br /><br /> Sin embargo, si lo hace, asegúrese de que estos puertos estén abiertos al tráfico entrante. <br /><br /> Si especifica * como hello IP de origen en el NSG, lote agrega todavía NSG en nivel de Hola de tooVMs NIC conectada. |
    |    3389, 22               |    Equipos de usuario que utiliza para la depuración, para que pueda acceder remotamente Hola VM.    |    No                                    |    No                     |    Agregue los NSG si desea toohello de acceso remoto (RDP/SSH) toopermit máquina virtual.   |                 

    Hello en la tabla siguiente describe el puerto de salida de hello que necesita tooenable toopermit acceso tooAzure almacenamiento:

    |    Puertos de salida    |    Destino    |    ¿Agrega Batch los grupos de seguridad de red?    |    ¿Es necesario para toobe de máquina virtual puede usar?    |    Acción del usuario    |
    |------------------------|-------------------|----------------------------|-------------------------------------|------------------------|
    |    443    |    Azure Storage    |    No    |    Sí    |    Si agrega los NSG, a continuación, asegúrese de que este puerto está abierto toooutbound tráfico.    |


## <a name="scaling-compute-resources"></a>Escalado de recursos de proceso
Con [el escalado automático](batch-automatic-scaling.md), puede tener el servicio por lotes Hola ajuste dinámicamente el número de Hola de nodos de proceso en un grupo según toohello carga de trabajo y recursos de uso actual de su escenario de proceso. Esto le permite toolower Hola costo total de la aplicación en ejecución mediante el uso de recursos de hello solo necesita y los que liberar a no es necesario.

Para habilitar el escalado automático, escriba una [fórmula de escalado automático](batch-automatic-scaling.md#automatic-scaling-formulas) y asóciela con un grupo. Hola servicio por lotes utiliza número de destino de Hola Hola toodetermine fórmulas de nodos en el grupo de Hola para hello siguiente escala intervalo (es decir, un intervalo que se puede configurar). Puede especificar valores de escalado automático de Hola para un grupo cuando se crea o habilitar el ajuste de escala en un grupo más adelante. También puede actualizar Hola ajuste de escala en configuración en un grupo de ajuste de escala-habilitado.

Por ejemplo, quizás un trabajo requiere que se envía a un gran número de toobe de tareas que se ejecuta. Puede asignar un grupo de escalado toohello fórmulas que ajusta Hola número de nodos de grupo, Hola basado en número actual de Hola de tareas en cola y la tasa de finalización de Hola de tareas de hello en el trabajo de Hola. Hola servicio por lotes periódicamente evalúa la fórmula de Hola y cambia el tamaño de bloque de hello, en función de la carga de trabajo y las otras opciones de fórmulas. servicio de Hello agrega nodos según sea necesario cuando hay un gran número de tareas en cola y quita los nodos cuando no hay ninguna tarea en cola o se está ejecutando.

Una fórmula de escala se puede basar en hello siguientes métricas:

* **Las métricas de tiempo** se basan en las estadísticas recopiladas cada cinco minutos en hello especificar número de horas.
* **Métricas de recursos** : se basan en el uso de CPU, ancho de banda y memoria y en el número de nodos.
* **Métricas de tareas**: se basan en el estado de la tarea, como *Activa* (en cola), *En ejecución* o *Completada*.

Cuando el escalado automático reduce el número de Hola de nodos de proceso en un grupo, debe tener en cuenta cómo toohandle tareas que se ejecutan en tiempo de presentación del programa Hola a reducir la operación. tooaccommodate este, lote proporciona una *opción de cancelación de asignación de nodo* que se pueden incluir en las fórmulas. Por ejemplo, puede especificar que las tareas en ejecución se detiene inmediatamente, detiene inmediatamente y, a continuación, poner en cola para su ejecución en otro nodo o permiten toofinish antes de nodo de Hola se quita del grupo de Hola.

Para obtener más información sobre cómo escalar automáticamente una aplicación, consulte [Escalado automático de nodos de proceso en un grupo de Azure Batch](batch-automatic-scaling.md).

> [!TIP]
> toomaximize utilización de recursos de proceso, establecer el número de destino de Hola de nodos toozero final Hola de un trabajo, pero permitir la ejecución de tareas toofinish.
>
>

## <a name="security-with-certificates"></a>Seguridad con certificados
Normalmente debe toouse certificados al cifrar o descifrar información confidencial para tareas como clave de Hola para un [cuenta de almacenamiento de Azure][azure_storage]. toosupport esto, puede instalar certificados en los nodos. Secretos cifrados se pasan tootasks a través de los parámetros de línea de comandos o insertados en uno de los recursos de tareas de Hola y certificados Hola instalado pueden ser toodecrypt usado ellos.

Usar hello [agregar certificado] [ rest_add_cert] operación (REST de lote) o [CertificateOperations.CreateCertificate] [ net_create_cert] método (por lotes. NET) tooadd una cuenta de lote tooa de certificado. A continuación, puede asociar certificados de hello con un grupo nuevo o existente. Cuando un certificado está asociado a un grupo, Hola servicio por lotes instala el certificado de hello en cada nodo de grupo de Hola. Hola servicio por lotes instala los certificados apropiados de hello cuando se inicia el nodo de hello, antes de iniciar las tareas (incluida la tarea de inicio de Hola y de tarea del Administrador de trabajos).

Si agrega certificados tooan *existente* grupo, debe reiniciar el equipo de sus nodos de proceso Hola certificados toobe aplica toohello nodos.

## <a name="error-handling"></a>Control de errores
Le resultará necesario toohandle errores de tarea y de aplicación dentro de la solución de lote.

### <a name="task-failure-handling"></a>Control de errores de tareas
Los errores de las tareas se incluyen en estas categorías:

* **Errores de procesamiento previo**

    Si una tarea produce un error toostart, un error previa al procesamiento se establece para la tarea hello.  

    Errores de procesamiento previo puede producirse si han movido los archivos de recursos de la tarea de hello, Hola cuenta de almacenamiento ya no está disponible o se encontró otro problema que ha impedido Hola correcta operación de copia de archivos toohello nodo.

* **Errores de carga de archivos**

    Si la carga de archivos que se especifican para una tarea falla por alguna razón, un error de carga de archivo está establecido para la tarea hello.

    Archivo de carga pueden producirse errores si hello SAS proporcionada acceso al almacenamiento de Azure no es válido o no proporciona permisos de escritura, si la cuenta de almacenamiento de hello ya no está disponible, o si otro problema se ha encontrado que impedía Hola copia correcta de los archivos de nodo de Hola.    

* **Errores de aplicación**

    También puede producir un error de proceso de Hola que se especifica mediante la línea de comandos de la tarea hello. Hello proceso se considera toohave error al proceso de Hola que es ejecutado por la tarea hello devuelve un código de salida distinto de cero (vea *códigos de salida de tarea* en la sección siguiente de hello).

    Errores de aplicación, puede configurar por lotes tarea tooautomatically reintento hello tooa un número especificado de veces.

* **Errores de restricción**

    Puede definir una restricción que especifica Hola duración de ejecución máximo para un trabajo o tarea, hello *maxWallClockTime*. Esto puede ser útil para finalizar las tareas que no cumplan tooprogress.

    Cuando se ha superado el período de tiempo máximo de hello, tarea hello está marcado como *completado*, pero el código de salida de hello se establece demasiado`0xC000013A` hello y *schedulingError* campo está marcado como `{ category:"ServerError", code="TaskEnded"}`.

### <a name="debugging-application-failures"></a>Depuración de errores de aplicación
* `stderr` y `stdout`

    Durante la ejecución, una aplicación podría generar resultados de diagnóstico que puede usar tootroubleshoot problemas. Como se mencionó en hello en la sección anterior [archivos y directorios](#files-and-directories), Hola servicio por lotes escribe la salida estándar y el error estándar de salida demasiado`stdout.txt` y `stderr.txt` nodo de ejecución de archivos en el directorio de la tarea de hello en Hola. Puede utilizar Hola portal de Azure o uno de toodownload del SDK de lote de hello estos archivos. Por ejemplo, puede recuperar estos y otros archivos para solucionar problemas mediante el uso de [ComputeNode.GetNodeFile] [ net_getfile_node] y [CloudTask.GetNodeFile] [ net_getfile_task] de biblioteca de .NET de lote de Hola.

* **Códigos de salida de la tarea**

    Como se mencionó anteriormente, una tarea se marcará como incorrecta Hola servicio por lotes si el proceso de Hola que es ejecutado por la tarea hello devuelve un código de salida distinto de cero. Cuando una tarea ejecuta un proceso, lote rellena la propiedad de código de salida de la tarea hello con hello *devolver código de proceso de hello*. Es importante toonote que código de salida de una tarea es **no** determinado por hello servicio por lotes. Código de salida de una tarea viene determinado por el propio proceso Hola o sistema operativo de hello en el proceso de Hola que ejecuta.

### <a name="accounting-for-task-failures-or-interruptions"></a>Consideraciones sobre errores o interrupciones
En ocasiones, las tareas pueden presentar errores o interrumpirse. Hello propia aplicación de tareas podría producir un error, podría reiniciarse en qué Hola se ejecuta la tarea de nodo de Hola o nodo Hola podría quitarse de grupo de Hola durante una operación de cambio de tamaño si hello desasignación directiva del grupo conjunto tooremove nodos inmediatamente sin tener que esperar toofinish de tareas. En todos los casos, tarea hello puede ser automáticamente poner en cola por lotes para su ejecución en otro nodo.

También es posible que un toocause problema intermitente toohang de una tarea o tomar tooexecute demasiado larga. Puede establecer el intervalo de ejecución máximo de saludo para una tarea. Si se supera el intervalo de ejecución máximo de hello, Hola servicio por lotes interrumpe la aplicación de la tarea de hello.

### <a name="connecting-toocompute-nodes"></a>Conectando los nodos toocompute
Puede realizar la depuración y solución de problemas mediante la firma de forma remota en el nodo de proceso de tooa adicionales. Puede usar hello toodownload portal Azure un archivo de protocolo de escritorio remoto (RDP) para los nodos de Windows y obtener información de conexión de Secure Shell (SSH) para los nodos de Linux. También puede hacerlo mediante el uso de hello las API de lote: por ejemplo, con [.NET de lotes] [ net_rdpfile] o [lote Python](batch-linux-nodes.md#connect-to-linux-nodes-using-ssh).

> [!IMPORTANT]
> nodo de tooa tooconnect a través de RDP o SSH, primero debe crear un usuario en el nodo de Hola. toodo esto, puede usar hello portal de Azure, [agregar un nodo de tooa de cuenta de usuario] [ rest_create_user] mediante la API de REST de lote de hello, llamar hello [ComputeNode.CreateComputeNodeUser] [ net_create_user] método en .NET de lote o llamada hello [add_user] [ py_add_user] método hello lote Python módulo.
>
>

### <a name="troubleshooting-problematic-compute-nodes"></a>Solución de problemas de nodos de proceso problemáticos
En situaciones donde algunas de las tareas se producen errores, la aplicación de cliente de proceso por lotes o el servicio puede examinar los metadatos de Hola de hello no se pudo tareas tooidentify un nodo que. Cada nodo de un grupo tiene un identificador único y nodo de hello en el que se ejecuta una tarea se incluye en los metadatos de la tarea de Hola. Una vez que haya identificado un "nodo problemático", puede llevar a cabo varias acciones con él:

* **Reinicie el nodo de hello** ([REST][rest_reboot] | [.NET][net_reboot])

    A veces puede borrar reiniciar nodo Hola latentes problemas como los procesos bloqueados o se ha bloqueado. Tenga en cuenta que si el grupo utiliza una tarea de inicio o el trabajo utiliza una tarea de preparación del trabajo, se ejecutan cuando se reinicia el nodo de Hola.
* **Restablecer imagen inicial de nodo de hello** ([REST][rest_reimage] | [.NET][net_reimage])

    Esto vuelve a instalar sistema operativo de hello en el nodo de Hola. Al igual que con un nodo se reinicie, inicie tareas y tareas de preparación del trabajo se vuelva a ejecutar después de que se ha renovado nodo Hola.
* **Quitar nodo Hola de grupo de hello** ([REST][rest_remove] | [.NET][net_remove])

    A veces resulta toocompletely es necesario quitar un nodo Hola de grupo de Hola.
* **Deshabilitar la programación de tareas en el nodo de hello** ([REST][rest_offline] | [.NET][net_offline])

    Esto eficazmente toma Hola nodo sin conexión para que no hay otras tareas se asignan tooit, pero permite Hola nodo tooremain se está ejecutando y en grupo de Hola. Esto le permite tooperform seguir investigando a causa de Hola de errores de hello sin perder los datos de la tarea fallida de Hola y sin nodo de hello provocando errores de tareas adicionales. Por ejemplo, puede deshabilitar la programación de tareas en el nodo de hello, a continuación, [iniciar una sesión remota](#connecting-to-compute-nodes) tooexamine Hola registros de eventos del nodo o realizar otra solución de problemas. Una vez que finalice la investigación, a continuación, puede poner en línea el nodo de hello habilitando la programación de tareas ([REST][rest_online] | [.NET] [ net_online]), o uno de hello realizar otras acciones que se analizaron anteriormente.

> [!IMPORTANT]
> Con cada acción que se describe en esta sección, reiniciar, restablecer la imagen inicial, quitar y deshabilitar la programación de tareas, es capaz de toospecify cómo se administran las tareas en ejecución actualmente en el nodo de hello cuando se realiza la acción de Hola. Por ejemplo, al deshabilitar programación de tareas en un nodo mediante el uso de biblioteca de cliente de .NET de lotes de hello, puede especificar un [DisableComputeNodeSchedulingOption] [ net_offline_option] toospecify de valor de enumeración si demasiado**Terminate** tareas en ejecución, **poner** para programar en otros nodos, o permitir la ejecución de tareas toocomplete antes de realizar la acción de hello (**TaskCompletion**).
>
>

## <a name="next-steps"></a>Pasos siguientes
* Obtenga información acerca de hello [herramientas y API de lote](batch-apis-tools.md) disponibles para la creación de soluciones de lote.
* Guiará a través de una aplicación de proceso por lotes de ejemplo paso a paso en [empezar a trabajar con hello biblioteca de Azure Batch para .NET](batch-dotnet-get-started.md). También hay un [versión de Python](batch-python-tutorial.md) nodos de proceso de tutorial de Hola que se ejecuta una carga de trabajo en Linux.
* Descargar y generar hello [Explorer lote] [ github_batchexplorer] proyecto de ejemplo para su uso mientras desarrolla sus soluciones de lote. Hola explorador por lotes puede realizar siguiente hello y mucho más:

  * Supervisar y manipular grupos, trabajos y tareas dentro de su cuenta de Batch
  * Descargar `stdout.txt`, `stderr.txt`, y otros archivos de los nodos
  * Crear usuarios en los nodos y descargar archivos RDP para el inicio de sesión remoto.
* Obtenga información acerca de cómo demasiado[crear grupos de nodos de proceso de Linux](batch-linux-nodes.md).
* Visite hello [foro de Azure Batch] [ batch_forum] en MSDN. Foro de Hello es conveniente colocar tooask preguntas, si solo se desea obtener la información o es un experto en uso por lotes.

[1]: ./media/batch-api-basics/node-folder-structure.png

[azure_storage]: https://azure.microsoft.com/services/storage/
[batch_forum]: https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurebatch
[cloud_service_sizes]: ../cloud-services/cloud-services-sizes-specs.md
[msmpi]: https://msdn.microsoft.com/library/bb524831.aspx
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_sample_taskdeps]:  https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/TaskDependencies
[github_batchexplorer]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/BatchExplorer
[batch_net_api]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[msdn_env_vars]: https://msdn.microsoft.com/library/azure/mt743623.aspx
[net_cloudjob_jobmanagertask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobmanagertask.aspx
[net_cloudjob_priority]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.priority.aspx
[net_cloudpool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx
[net_cloudtask_env]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.environmentsettings.aspx
[net_create_cert]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.createcertificate.aspx
[net_create_user]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.createcomputenodeuser.aspx
[net_getfile_node]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.getnodefile.aspx
[net_getfile_task]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.getnodefile.aspx
[net_job_env]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.commonenvironmentsettings.aspx
[net_multiinstancesettings]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.multiinstancesettings.aspx
[net_onalltaskscomplete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.onalltaskscomplete.aspx
[net_rdp]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.getrdpfile.aspx
[net_reboot]: https://msdn.microsoft.com/library/azure/mt631495.aspx
[net_reimage]: https://msdn.microsoft.com/library/azure/mt631496.aspx
[net_remove]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.removefrompoolasync.aspx
[net_offline]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.disableschedulingasync.aspx
[net_online]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenode.enableschedulingasync.aspx
[net_offline_option]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.common.disablecomputenodeschedulingoption.aspx
[net_rdpfile]: https://msdn.microsoft.com/library/azure/Mt272127.aspx
[vnet]: https://msdn.microsoft.com/library/azure/dn820174.aspx#bk_netconf

[py_add_user]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.ComputeNodeOperations.add_user

[batch_rest_api]: https://msdn.microsoft.com/library/azure/Dn820158.aspx
[rest_add_job]: https://msdn.microsoft.com/library/azure/mt282178.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[rest_add_cert]: https://msdn.microsoft.com/library/azure/dn820169.aspx
[rest_add_task]: https://msdn.microsoft.com/library/azure/dn820105.aspx
[rest_create_user]: https://msdn.microsoft.com/library/azure/dn820137.aspx
[rest_get_task_info]: https://msdn.microsoft.com/library/azure/dn820133.aspx
[rest_job_schedules]: https://msdn.microsoft.com/library/azure/mt282179.aspx
[rest_multiinstance]: https://msdn.microsoft.com/library/azure/mt637905.aspx
[rest_multiinstancesettings]: https://msdn.microsoft.com/library/azure/dn820105.aspx#multiInstanceSettings
[rest_update_job]: https://msdn.microsoft.com/library/azure/dn820162.aspx
[rest_rdp]: https://msdn.microsoft.com/library/azure/dn820120.aspx
[rest_reboot]: https://msdn.microsoft.com/library/azure/dn820171.aspx
[rest_reimage]: https://msdn.microsoft.com/library/azure/dn820157.aspx
[rest_remove]: https://msdn.microsoft.com/library/azure/dn820194.aspx
[rest_offline]: https://msdn.microsoft.com/library/azure/mt637904.aspx
[rest_online]: https://msdn.microsoft.com/library/azure/mt637907.aspx

[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
