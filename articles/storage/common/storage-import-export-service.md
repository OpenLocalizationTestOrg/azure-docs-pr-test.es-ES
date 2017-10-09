---
title: "aaaUsing importación/exportación de Azure tootransfer datos tooand del almacenamiento de blobs | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toocreate importar y exportar los trabajos en hello portal de Azure para transferir datos tooand de almacenamiento de blobs."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 668f53f2-f5a4-48b5-9369-88ec5ea05eb5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2017
ms.author: muralikk
ms.openlocfilehash: 0be486a4badf2127b4613f3e9664e4cd308d3298
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-microsoft-azure-importexport-service-tootransfer-data-tooblob-storage"></a>Usar el almacenamiento de hello importación y exportación de Microsoft Azure service tootransfer datos tooblob
Hola servicio de importación y exportación de Azure permite toosecurely transfieren grandes cantidades de almacenamiento de blobs de datos tooAzure por el centro de datos de Azure de tooan de envío unidades de disco duro. También puede utilizar estos datos de tootransfer de servicio de unidades de disco de toohard de almacenamiento de blobs de Azure y enviar al sitio local tooyour. Este servicio es adecuado en situaciones donde desee tootransfer varios terabytes (TB) de tooor de datos de Azure, pero cargar o descargar a través de red de hello es factible debido toolimited ancho de banda o alto de los costos de red.

servicio de Hello requiere que las unidades de disco duro debe ser BitLocker cifrada por razones de seguridad de Hola de los datos. Hola service admite ambos Hola clásico y el Administrador de recursos de Azure almacenamiento cuentas (niveles estándar y frío) presentes en todas las regiones de Hola de Azure pública. Debes enviar tooone de unidades de disco duro de ubicaciones de hello admitida especificado más adelante en este artículo.

En este artículo, aprenderá más acerca de servicio de importación y exportación de Azure de Hola y cómo tooship unidades de disco para copiar la tooand de datos de almacenamiento de blobs de Azure.

## <a name="when-should-i-use-hello-azure-importexport-service"></a>¿Cuándo debo usar servicio de importación y exportación de Azure de hello?
Considere la posibilidad de usar el servicio de importación y exportación de Azure al cargar o descargar datos a través de red de hello es demasiado lento, o bien obtener el ancho de banda de red adicional es costo prohibitivo.

Puede utilizar este servicio en los siguientes escenarios:

* Migrar datos en la nube toohello: mover grandes cantidades de datos tooAzure de forma rápida y rentable.
* La distribución de contenido: enviar rápidamente datos tooyour sitios de cliente.
* Copia de seguridad: Realizar copias de seguridad de su toostore de datos local en el almacenamiento de blobs de Azure.
* Recuperación de datos: recuperar gran cantidad de datos almacenados en almacenamiento de blobs y recibirlo de ubicación de tooyour local.

## <a name="prerequisites"></a>Requisitos previos
En esta sección se enumeran Hola requisitos previos necesarios toouse este servicio. Revíselos detenidamente antes de enviar sus unidades.

### <a name="storage-account"></a>Cuenta de almacenamiento
Debe tener una suscripción de Azure y una o varias cuentas toouse Hola importación y exportación de servicio de almacenamiento. Cada trabajo puede ser usado tootransfer tooor de datos de una cuenta de almacenamiento. Dicho de otra forma, un trabajo de importación y exportación no puede abarcar varias cuentas de almacenamiento. Para obtener información acerca de cómo crear una nueva cuenta de almacenamiento, consulte [cómo tooCreate una cuenta de almacenamiento](storage-create-storage-account.md#create-a-storage-account).

### <a name="blob-types"></a>Tipos de blobs
Puede usar datos de importación y exportación de Azure servicio toocopy demasiado**bloque** blobs o **página** blobs. Y a la inversa, solo puede exportar blobs **en bloque**, **en páginas** o **en anexos** de Azure Storage mediante este servicio.

### <a name="job"></a>Trabajo
proceso de hello toobegin de la importación de tooor exportar desde almacenamiento de blobs, primero cree un trabajo. Un trabajo puede ser un trabajo de importación o un trabajo de exportación:

* Cree un trabajo de importación cuando desee que los datos de tootransfer tener tooblobs local en su cuenta de almacenamiento de Azure.
* Crear un trabajo de exportación cuando desee que los datos de tootransfer actualmente almacenados como blobs en las unidades de toohard de cuenta de almacenamiento que son enviados tooyou.s cuando se crea un trabajo, notificar Hola importación y exportación de servicio que enviará uno o más estricta unidades tooan Azure Centro de datos.

* En el caso de un trabajo de importación, enviará las unidades de disco duro que contengan los datos.
* Si es un trabajo de exportación, enviará las unidades de disco duro vacías.
* Puede distribuir una too10 unidades de disco duro por trabajo.

Puede crear una importación o exportación de trabajo mediante el portal de Azure de Hola o hello [API de REST de importación y exportación de almacenamiento de Azure](/rest/api/storageimportexport).

### <a name="waimportexport-tool"></a>Herramienta WAImportExport
primer paso de Hola para crear un **importar** trabajo es tooprepare las unidades de disco que se van a enviar para la importación. tooprepare las unidades de disco, debe conectar ejecución hello herramienta WAImportExport en el servidor local de Hola y tooa de servidor local. Esta herramienta WAImportExport facilita la copia de la unidad de datos toohello, cifrado de datos de hello en unidad de hello con BitLocker y generar archivos de diario de unidad de Hola.

archivos de diario de Hello almacenan información básica sobre su trabajo y la unidad de disco como número de serie de unidad y el nombre de la cuenta de almacenamiento. Este archivo de diario no se almacena en la unidad de Hola. Se utiliza durante la creación del trabajo de importación. Más adelante en este artículo se proporcionan pasos detallados sobre la creación del trabajo.

Hola WAImportExport herramienta solo es compatible con el sistema operativo de Windows de 64 bits. Vea hello [sistema operativo](#operating-system) sección para versiones específicas de sistema operativo compatible.

Descargar Hola la versión más reciente de hello [herramienta WAImportExport](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExportV2.zip). Para obtener más detalles sobre el uso de hello herramienta WAImportExport, vea hello [Using Hola herramienta WAImportExport](storage-import-export-tool-how-to.md).

>[!NOTE]
>**Versión anterior:** puede [descargar WAImportExpot V1](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip) versión de Hola herramienta y consulte demasiado[Guía de uso de WAImportExpot V1](storage-import-export-tool-how-to-v1.md). Versión de WAImportExpot V1 de herramienta de hello proporcionan compatibilidad para **preparación de discos al datos ya están escritos previamente toohello disco**. También necesitará toouse WAImportExpot V1 herramienta si Hola solo una clave disponible es la clave SAS.

>

### <a name="hard-disk-drives"></a>Unidades de disco duro
2,5 solo se admite SSD o 2,5" o 3,5" SATA II o disco duro interno de III para su uso con el servicio de importación/exportación de Hola. Un único trabajo de importación/exportacón puede tener un máximo de 10 unidades HDD/SSD, y cada una de ellas puede tener cualquier tamaño. Gran número de unidades de disco puede abarcar varios trabajos y no hay ningún límite en el número de Hola de trabajos que se pueden crear. 

Para los trabajos de importación, se procesarán solo Hola primer volumen de datos en la unidad de Hola. volumen de datos de Hello debe estar formateado con NTFS.

> [!IMPORTANT]
> Este servicio no admite unidades de disco duro externas que incorporen un adaptador USB integrado. Además, no se puede usar el disco de hello dentro de hello mayúsculas y minúsculas de un disco duro externo; No enviar unidades de disco duro externos.
> 
> 

A continuación se muestra que una lista de adaptadores USB externos utiliza toocopy datos toointernal unidades de disco duro. Anker 68UPSATAA-02BU Anker 68UPSHHDS-BU Startech SATADOCK22UE Orico 6628SUS3-C-BK (serie 6628) Base de acoplamiento de unidad de disco duro externa SATA de intercambio directo Thermaltake BlacX (USB 2.0 y eSATA)

### <a name="encryption"></a>Cifrado
datos de Hello en unidad de hello deben cifrarse con cifrado de unidad BitLocker. Así estarán protegidos mientras se encuentren en tránsito.

Para los trabajos de importación, hay cifrado de dos maneras tooperform Hola. Hola primera manera es la opción de Hola de toospecify cuando se usa el archivo CSV de conjunto de datos mientras se ejecuta la herramienta WAImportExport de Hola durante la preparación de la unidad. Hola segunda manera es el cifrado de BitLocker de tooenable manualmente en la unidad de Hola y especificar la clave de cifrado de Hola en hello driveset CSV cuando se ejecuta la línea de comandos de herramienta WAImportExport durante la preparación de unidad.

Para los trabajos de exportación, después de los datos copiados toohello unidades, servicio Hola cifrará unidad hello mediante BitLocker antes de enviarlo tooyou atrás. clave de cifrado de Hola se proporcionarán tooyou a través de hello portal de Azure.  

### <a name="operating-system"></a>Sistema operativo
Puede usar uno de hello después de 64 bits sistemas operativos tooprepare Hola unidad de disco duro con hello herramienta WAImportExport antes de enviar Hola unidad tooAzure:

Windows 7 Enterprise, Windows 7 Ultimate, Windows 8 Pro, Windows 8 Enterprise, Windows 8.1 Pro, Windows 8.1 Enterprise, Windows 10<sup>1</sup>, Windows Server 2008 R2, Windows Server 2012 y Windows Server 2012 R2. Todos estos sistemas operativos admiten el cifrado de unidad BitLocker.

### <a name="locations"></a>Ubicaciones
Hola servicio de importación y exportación de Azure es compatible con copia tooand de datos de todas las cuentas de almacenamiento de Azure pública. Puede distribuir tooone de unidades de disco duro de hello ubicaciones siguientes. Si la cuenta de almacenamiento está en una ubicación pública de Azure que no se especifica en este caso, se proporcionará una ubicación de envío alternativas al crear Hola trabajo mediante Hola portal de Azure u Hola API de REST de importación y exportación.

Ubicaciones de envío admitidas:

* Este de EE. UU.
* Oeste de EE. UU.
* Este de EE. UU. 2
* Oeste de EE. UU. 2
* Central EE. UU.:
* Centro-Norte de EE. UU
* Centro-Sur de EE. UU
* Centro occidental de EE.UU.
* Europa del Norte
* Europa occidental
* Asia oriental
* Sudeste asiático
* Australia Oriental
* Sudeste de Australia
* Oeste de Japón
* Este de Japón
* India Central
* Sur de la India
* Oeste de la India
* Centro de Canadá
* Este de Canadá
* Sur de Brasil
* Corea Central
* Gobierno de EE. UU. - Virginia
* Gobierno de EE. UU. - Iowa
* Departamento de Defensa de EE. UU. Este
* Departamento de Defensa de EE. UU. Centro
* Este de China
* Norte de China
* Sur del Reino Unido 2

### <a name="shipping"></a>Envío
**Trasvase de las unidades de centro de datos de toohello:**

Cuando se crea un trabajo de importación o exportación, se le proporcionará que una dirección de envío de uno de hello admite ubicaciones tooship las unidades de disco. Hola irección proporcionado dependerá de ubicación de saludo de la cuenta de almacenamiento, pero no puede ser igual Hola como la ubicación de la cuenta de almacenamiento.

Puede utilizar operadores como FedEx, DHL, SAI (UPS) u Hola US Postal Service tooship su toohello unidades dirección de envío.

**Unidades de envío desde el centro de datos de hello:**

Cuando se crea un trabajo de importación o exportación, debe proporcionar una dirección de devolución para Microsoft toouse cuando una copia de trasvase de las unidades de hello una vez completado el trabajo. Asegúrese de que proporcionar una dirección de remite válida tooavoid retrasos en el procesamiento.

Puede usar el operador de su elección en el disco duro Hola de orden tooforward directa. operador de Hello debe tener seguimiento adecuado en la cadena de custodia de orden toomaintain. También debe proporcionar a un transportista FedEx o DHL válido toobe de número de cuenta utilizada por Microsoft para enviar atrás en unidades de disco Hola. Un número de cuenta FedEx es necesario para enviar las unidades de disco de hello Estados Unidos y ubicaciones en Europa. En DHL, se requiere un número de cuenta para devolver las unidades enviadas desde Asia y Australia. Puede crear una cuenta de [FedEx](http://www.fedex.com/us/oadr/) (para EE. UU. y Europa) o [DHL](http://www.dhl.com/) (Asia y Australia) si no tiene una. Si ya tiene un número de cuenta de uno de estos transportistas, compruebe que sea válido.

En la entrega de los paquetes, debe seguir los términos de hello en [condiciones de servicio de Microsoft Azure](https://azure.microsoft.com/support/legal/services-terms/).

> [!IMPORTANT]
> Tenga en cuenta que los medios físicos de Hola que se entregan pueden requerir fronteras internacionales toocross. Usted es responsable de asegurarse de que el medio físico y los datos se importado o exportados con arreglo a las leyes de Hola. Antes de enviar un medio físico hello, consulte con su tooverify asesores que los medios y los datos pueden ser legalmente centro de datos enviados toohello identificado. Esto le ayudará a tooensure que llega a Microsoft de manera oportuna. Por ejemplo, cualquier paquete que cruce fronteras internacionales necesita un toobe factura comercial, así como paquetes de saludo (excepto si cruzar las fronteras dentro de la Unión Europea). Puede imprimir una copia rellena de factura comercial de Hola desde el sitio Web de transportista. Algunos ejemplos de factura comercial son la [factura comercial de DHL](http://invoice-template.com/wp-content/uploads/dhl-commercial-invoice-template.pdf) y la [factura comercial de FedEx](http://images.fedex.com/downloads/shared/shipdocuments/blankforms/commercialinvoice.pdf). Asegúrese de que Microsoft no se ha indicado como exportador Hola.
> 
> 

## <a name="how-does-hello-azure-importexport-service-work"></a>¿Cómo funciona Hola servicio de importación y exportación de Azure?
Puede transferir datos entre el sitio local y el almacenamiento de blobs de Azure mediante el servicio de importación y exportación de hello mediante la creación de trabajos y centro de datos de Azure de unidades de disco duro tooan de envío. Cada unidad de disco duro que se envía está asociada a un único trabajo. Cada trabajo está asociado a una única cuenta de almacenamiento. Hola de revisión [sección de requisitos previos](#pre-requisites) cuidadosamente toolearn sobre características de Hola de este servicio admitido como blob tipos, los tipos de disco, ubicaciones y envío.

En esta sección, se describen en un Hola de nivel alto pasos para importar y exportar los trabajos. Más adelante en hello [sección de inicio rápido](#quick-start), se proporcionan instrucciones paso a paso toocreate una importación y exportación de trabajo.

### <a name="inside-an-import-job"></a>Dentro de un trabajo de importación
En un nivel superior, un trabajo de importación implica Hola pasos:

* Determinar Hola datos toobe importado y Hola número de unidades que se necesita.
* Identificar la ubicación del blob de destino de Hola para los datos de almacenamiento de blobs.
* Usar hello herramienta WAImportExport toocopy su tooone de datos o más unidades de disco duro y cifrarlos con BitLocker.
* Crear un trabajo de importación en la cuenta de almacenamiento de destino mediante el portal de Azure de Hola u Hola API de REST de importación y exportación. Si usa Hola portal de Azure, cargar archivos de diario de unidad de Hola.
* Proporcionar remite de Hola y transportista cuenta número toobe utilizada para el envío Hola unidades back-tooyou.
* Toohello de unidades de disco duro de envío Hola proporcionada durante la creación del trabajo de dirección de envío.
* Actualizar entrega Hola seguimiento número en detalles del trabajo de importación de Hola y enviar el trabajo de importación de Hola.
* Las unidades se reciben y procesan en el centro de datos de Azure Hola.
* Las unidades se suministran mediante el operador cuenta toohello remite proporcionado en el trabajo de importación de Hola.
  
    ![Figura 1: Importación de flujos de trabajo](./media/storage-import-export-service/importjob.png)

### <a name="inside-an-export-job"></a>Dentro de un trabajo de exportación
En un nivel superior, un trabajo de exportación implica Hola pasos:

* Determinar Hola datos toobe exportado y Hola número de unidades que se necesita.
* Identificar blobs de origen de Hola o rutas de acceso de contenedor de los datos en almacenamiento de blobs.
* Crear un trabajo de exportación en la cuenta de almacenamiento de origen mediante el portal de Azure de Hola u Hola API de REST de importación y exportación.
* Especificar Hola blobs de origen o trabajo de exportación de las rutas de acceso de contenedor de los datos en Hola.
* Prever Hola devuelto dirección y transportista cuenta el número de toobe utilizada para el envío Hola unidades back-tooyou.
* Toohello de unidades de disco duro de envío Hola proporcionada durante la creación del trabajo de dirección de envío.
* Actualizar entrega Hola seguimiento número en detalles del trabajo de exportación de Hola y enviar el trabajo de exportación de Hola.
* unidades de Hola se reciben y procesan en el centro de datos de Azure Hola.
* Hola unidades cifradas con BitLocker; Hola claves están disponibles a través de hello portal de Azure.  
* Hola unidades se suministran con el transportista cuenta toohello remite proporcionado en el trabajo de importación de Hola.
  
    ![Figura 2: Exportación de flujos de trabajo](./media/storage-import-export-service/exportjob.png)

### <a name="viewing-your-job-and-drive-status"></a>Visualización del estado del trabajo y de la unidad
Puede realizar un seguimiento de estado de saludo de la importación o trabajos de exportación de hello portal de Azure. Haga clic en hello **importación/exportación** ficha. Aparecerá una lista de los trabajos en la página de Hola.

![Visualización del estado del trabajo](./media/storage-import-export-service/jobstate.png)

Verá uno de hello después de Estados de trabajo dependiendo de dónde se encuentra la unidad en proceso de Hola.

| Estado del trabajo | Descripción |
|:--- |:--- |
| Creating | Después de crea un trabajo, su estado se establece tooCreating. Mientras se está en el trabajo de hello en estado de creación de hello, hello servicio de importación/exportación supone Hola unidades no han sido enviados toohello centro de datos. Un trabajo puede permanecer en estado de creación de hello para tootwo semanas, después de que este se eliminará automáticamente por el servicio de Hola. |
| Envío | Después de enviar el paquete, debe actualizar Hola información de seguimiento en hello portal de Azure.  Trabajo de hello Esto convertirá en "Shipping". Hola trabajo permanecerá en estado de envío de Hola para tootwo semanas. 
| Received | Después de que todas las unidades se han recibido en el centro de datos de hello, se establecerá el estado del trabajo de hello toohello recibidos. |
| Transferring | Una vez como mínimo una unidad ha comenzado el procesamiento, se establecerá el estado del trabajo de hello toohello transferir. Ver estados de unidad de hello sección para obtener información detallada. |
| Packaging | Cuando todas las unidades de procesamiento han completado, el trabajo de Hola se colocarán en estado de empaquetado de hello hasta que las unidades de hello son enviado tooyou back. |
| Completed | Una vez todas las unidades se han enviado toohello back-cliente, si se ha completado el trabajo de hello sin errores, a continuación, Hola se establecerá toohello estado completado. trabajo de Hola se eliminarán automáticamente después de 90 días en hello estado completado. |
| Closed | Una vez todas las unidades se han enviado toohello back-cliente, si ha habido algún error durante el procesamiento de Hola de trabajo de hello, a continuación, Hola se establecerá toohello cerrarlos. trabajo de Hola se eliminarán automáticamente después de 90 días en estado cerrado Hola. |

tabla Hola siguiente describe el ciclo de vida de Hola de una unidad de disco individual durante su transición a través de un trabajo de importación o exportación. Hola estado actual de cada unidad en un trabajo ahora es visible desde el portal de Azure Hola.
Hello siguiente tabla describe cada estado que puede pasar cada unidad en un trabajo.

| Estado de la unidad | Descripción |
|:--- |:--- |
| Specified | Para un trabajo de importación, cuando se crea el trabajo de Hola de hello portal de Azure, estado inicial de Hola para una unidad es Hola Specified estado. Para un trabajo de exportación, ya que no se especifica ninguna unidad cuando se crea el trabajo de hello, Hola inicial para las unidades estado es Hola recibidos. |
| Received | unidad de Hello cambia toohello recibidos estado al operador de servicio de importación y exportación de hello ha procesado las unidades de Hola que se han recibido de hello trasvase de empresa para un trabajo de importación. Para un trabajo de exportación, Hola inicial para las unidades estado es Hola recibidos. |
| NeverReceived | unidad de disco de Hello pasará toohello NeverReceived estado cuando llega el paquete de saludo de un trabajo pero paquete hello no contiene la unidad de Hola. También puede mover una unidad a este estado si han pasado dos semanas ya que Hola servicio ha recibido información de envío de hello, pero paquete Hola aún no ha llegado al centro de datos de Hola. |
| Transferring | Una unidad moverá toohello transferir estado al servicio Hola comienza tootransfer datos de hello unidad tooWindows almacenamiento de Azure. |
| Completed | Una unidad de disco pasará toohello estado completado al servicio de hello haya transferido correctamente todos los datos de hello sin errores.
| CompletedMoreInfo | Una unidad de disco pasará toohello CompletedMoreInfo estado al servicio de hello haya encontrado algún problema mientras copiaba datos desde o unidad de toohello. Hola información puede incluir errores, advertencias o mensajes informativos sobre sobrescribir blobs.
| ShippedBack | unidad de disco de Hello pasará toohello ShippedBack estado cuando se ha enviado desde la dirección de retorno de toohello de hello datos centro de nuevo. |

Esta imagen de hello portal de Azure muestra el estado de la unidad de Hola de un trabajo de ejemplo:

![Visualización de estado de la unidad](./media/storage-import-export-service/drivestate.png)

Hello tabla siguiente describen los Estados de error de unidad de Hola y las acciones de hello realizadas para cada estado.

| Estado de la unidad | Evento | Resolución y paso siguiente |
|:--- |:--- |:--- |
| NeverReceived | Una unidad que está marcada como NeverReceived (porque no se recibió como parte de envío del trabajo de hello) llega en otro envío. | equipo de operaciones de Hello moverá Hola unidad toohello estado recibido. |
| N/D | Una unidad que no forma parte de cualquier trabajo llega al centro de datos de hello como parte de otro trabajo. | unidad de Hola se marcará como una unidad de disco adicional y se devolverá al cliente de toohello cuando se completa el trabajo de hello asociado con el paquete original Hola. |

### <a name="time-tooprocess-job"></a>Trabajo de temporizador tooprocess
cantidad de Hola de tiempo que tarda tooprocess un trabajo de importación y exportación depende de distintos factores, como la hora de envío, tipo de trabajo, escriba y el tamaño de Hola datos copiados y Hola tamaño de los discos de hello proporcionado. Hola servicio de importación/exportación no tiene un SLA, pero después de que se reciben los discos de hello servicio Hola esfuerza toocomplete Hola copia en 7 días too10. Puede usar progreso del trabajo de hello API de REST tootrack hello más estrechamente. Hay una porcentaje completa del parámetro en hello operación enumerar trabajos que se da una indicación de progreso de la copia. Contacto toous si necesita un toocomplete de estimación de un trabajo de importación y exportación crítica de tiempo.

### <a name="pricing"></a>Precios
**Cuota de manipulación de unidades**

Existe una cuota de manipulación por cada unidad procesada como parte del trabajo de importación o exportación. Ver detalles de hello en hello [precios de importación y exportación de Azure](https://azure.microsoft.com/pricing/details/storage-import-export/).

**Gastos de envío**

Al enviar las unidades tooAzure, usted paga Hola transportista del envío toohello costo de envío. Cuando Microsoft devuelve Hola unidades tooyou, Hola gastos de envío se cobra cuenta del transportista toohello que proporciona al momento de hello de la creación de trabajo.

**Costos de transacción**

La importación de datos en Blob Storage no tiene ningún costo de transacción asociado. los cargos de salida estándar de Hello son aplicables cuando se exportan datos desde almacenamiento de blobs. Para más información sobre los costos de transacción, consulte [Detalles de precios de Transferencias de datos](https://azure.microsoft.com/pricing/details/data-transfers/)

## <a name="quick-start"></a>Inicio rápido
En esta sección se proporcionan instrucciones paso a paso para crear trabajos de importación y exportación. Asegúrese de que cumple todos hello [requisitos previos](#pre-requisites) antes de continuar.

> [!IMPORTANT]
> servicio Hello es compatible con una cuenta de almacenamiento estándar por importar o exportar un trabajo y no admite cuentas de almacenamiento premium. 
> 
> 
## <a name="create-an-import-job"></a>Crear un trabajo de importación
Crear un tooyour de datos de importación trabajo toocopy cuenta de almacenamiento de Azure desde discos duros enviar uno o más unidades de disco que contiene el centro de datos toohello datos especificados. trabajo de importación Hello comunica detalles sobre las unidades de disco duro, toobe de datos que copia, cuenta de almacenamiento de destino y el servicio de importación y exportación de toohello de información de envío. El proceso de creación de un trabajo de importación consta de tres pasos. En primer lugar, prepare las unidades mediante la herramienta WAImportExport de Hola. En segundo lugar, envíe un trabajo de importación mediante Hola portal de Azure. En tercer lugar, se distribuye Hola unidades toohello proporcionada durante Hola de creación y actualización de trabajo, información de envío en los detalles del trabajo de dirección de envío.   

### <a name="prepare-your-drives"></a>Preparación de las unidades
Hola primer paso al importar datos mediante el servicio de importación y exportación de hello es tooprepare sus unidades mediante la herramienta WAImportExport de Hola. Siga estos pasos hello tooprepare las unidades de disco.

1. Identificar Hola datos toobe importado. Podría tratarse de directorios y archivos independientes en el servidor local de Hola o un recurso compartido de red.  
2. Determinar el número de Hola de unidades que debe según el tamaño total de datos de Hola. Adquirir unidades de disco duro SATA II y III de hello requerido número de 2,5 SSD 2,5" o 3,5".
3. Identificar la cuenta de almacenamiento de destino de hello, contenedor, directorios virtuales y blobs.
4.  Determinar los directorios de hello y/o archivos independientes que serán copiados tooeach unidad de disco duro.
5.  Crear Hola archivos CSV para el conjunto de datos y driveset.
    
    **Archivo CSV de conjunto de datos**
    
    A continuación se muestra un ejemplo de archivo CSV de conjunto de datos:
    
    ```
    BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
    "F:\50M_original\100M_1.csv.txt","containername/100M_1.csv.txt",BlockBlob,rename,"None",None
    "F:\50M_original\","containername/",BlockBlob,rename,"None",None 
    ```
   
    Hola ejemplo anterior, 100M_1.csv.txt será toohello copiada raíz del contenedor de hello denominado "containername". Si el nombre de contenedor de Hola "containername" no existe, se creará uno. Todos los archivos y carpetas bajo 50M_original será toocontainername de copia de forma recursiva. Se mantendrá la estructura de carpetas.

    Obtenga más información sobre [preparar el archivo CSV de hello dataset](storage-import-export-tool-preparing-hard-drives-import.md#prepare-the-dataset-csv-file).
    
    **Recuerde**: de forma predeterminada, se importarán los datos de hello como Blobs en bloques. Puede usar datos de hello BlobType tooimport del valor del campo como un BLOB de página. Por ejemplo, si va a importar archivos VHD que se van a montar como discos en una máquina virtual de Azure, debe importarlos como blobs en páginas.

    **Archivo CSV de conjunto de unidades**

    valor de Hola de driveset Hola marca es un archivo CSV que contiene la lista de hello discos toowhich Hola de letras de unidad se asignan en orden para hello herramienta toocorrectly lista de selección Hola de toobe discos preparado. 

    A continuación se muestra el ejemplo de Hola del archivo CSV de driveset:
    
    ```
    DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
    G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
    H,Format,SilentMode,Encrypt,
    ```

    Hola ejemplo anterior, se supone que se han conectado dos discos y volúmenes NTFS básicos con letra de volumen G:\ y H:\ se han creado. herramienta de Hello formateará y cifrar el disco Hola que hospeda H:\ y no formatear ni cifrar disco Hola hospedaje volumen G:\.

    Obtenga más información sobre [preparar el archivo CSV de hello driveset](storage-import-export-tool-preparing-hard-drives-import.md#prepare-initialdriveset-or-additionaldriveset-csv-file).

6.  Hola de uso [herramienta WAImportExport](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) toocopy su tooone de datos o más unidades de disco duro.
7.  Puede especificar "Encrypt" en el campo de cifrado drivset CSV tooenable cifrado de BitLocker en la unidad de disco duro de Hola. Como alternativa, también puede habilitar el cifrado de BitLocker manualmente en la unidad de disco duro de Hola y especificar "AlreadyEncrypted" y especificar la clave de hello en hello driveset CSV mientras se ejecuta la herramienta de Hola.

8. No modifique los datos de hello en unidades de disco duro de Hola o un archivo de diario de hello después de completar la preparación del disco.

> [!IMPORTANT]
> Cada unidad de disco duro que prepare generará un archivo del diario. Al crear trabajo de importación de hello mediante Hola portal de Azure, debe cargar todos los archivos de diario de Hola de unidades de Hola que forman parte de ese trabajo de importación. Las unidades sin archivos de diario no se procesarán.
> 
>

A continuación son comandos de Hola y ejemplos para preparar la unidad de disco duro de hello utilizando herramienta WAImportExport.

Herramienta WAImportExport comando PrepImport para hello en primer lugar copie directorios de sesión toocopy o archivos con una nueva sesión de copia:

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] [/sk:<StorageAccountKey>] [/silentmode] [/InitialDriveSet:<driveset.csv>] DataSet:<dataset.csv>
```

**Ejemplo 1 de importación**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

En orden demasiado**agregar más unidades**, uno puede crear un nuevo archivo driveset y ejecute el comando de hello como sigue. Para copia posteriores sesiones toohello diferentes unidades de disco a la especificada en el archivo .csv de InitialDriveset, especificar un nuevo archivo CSV de driveset y proporcionarlo como un parámetro de valor toohello "AdditionalDriveSet". Hola de uso **mismo archivo diario** nombre y proporcionar una **nuevo identificador de sesión**. formato de Hello del archivo AdditionalDriveset CSV es el mismo que el formato de InitialDriveSet.

```
WAImportExport.exe PrepImport /j:<JournalFile> /id:<SessionId> /AdditionalDriveSet:<driveset.csv>
```

**Ejemplo 2 de importación**
```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3  /AdditionalDriveSet:driveset-2.csv
```

En orden tooadd datos adicionales toohello driveset mismo, herramienta WAImportExport comando PrepImport puede llamarse para copia posteriores sesiones toocopy adicionales o directorio de archivos: de copia posteriores sesiones toohello unidades de disco duro mismo especificado en InitialDriveset .csv, especifique hello **mismo archivo diario** nombre y proporcionar una **nuevo identificador de sesión**; no hay ninguna clave de cuenta de almacenamiento de necesidad tooprovide Hola.

```
WAImportExport PrepImport /j:<JournalFile> /id:<SessionId> /j:<JournalFile> /id:<SessionId> [/logdir:<LogDirectory>] DataSet:<dataset.csv>
```

**Ejemplo 3 de importación**

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

Ver más detalles acerca de cómo utilizar la herramienta WAImportExport de hello en [preparación de unidades de disco duro para la importación de](storage-import-export-tool-preparing-hard-drives-import.md).

Además, consulte toohello [unidades de disco duro de tooprepare de flujo de trabajo para un trabajo de importación de ejemplo](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md) para obtener instrucciones paso a paso detalladas.  

### <a name="create-hello-import-job"></a>Crear trabajo de importación de Hola
1. Una vez que ha preparado el disco, navegar por la cuenta de almacenamiento tooyour Hola portal de Azure y ver Hola panel. En **Vista rápida**, haga clic en **Crear un trabajo de importación**. Revise los pasos de Hola y seleccione Hola casilla tooindicate que ha preparado el disco y que tiene el archivo de diario de unidad de hello disponible.
2. En el paso 1, proporcionar información de contacto para hello responsable de este trabajo de importación y una dirección de remite válida. Si desea que los datos de registro detallado de toosave de trabajo de importación de hello, compruebe la opción de hello demasiado**guardar Hola registro detallado en mi contenedor de blobs 'waimportexport'**.
3. En el paso 2, cargar archivos de diario de unidad de hello obtenida durante el paso de preparación de unidad de Hola. Necesitará un archivo de tooupload para cada unidad que haya preparado.
   
   ![Creación del trabajo de importación - Paso 3](./media/storage-import-export-service/import-job-03.png)
4. En el paso 3, escriba un nombre descriptivo para el trabajo de importación de Hola. Tenga en cuenta que nombre hello puede contener solo letras minúsculas, números, guiones y caracteres de subrayado, debe empezar por una letra y no puede contener espacios. Va a utilizar nombre de hello elija tootrack los trabajos mientras están en curso y una vez que se completen.
   
   A continuación, seleccione la región del centro de datos de lista de Hola. región del centro de datos de Hola indicará datos saludo del centro y dirección toowhich debe enviar el paquete. Consulte las P+F de Hola a continuación para obtener más información.
5. En el paso 4, seleccione el transportista de devolución de lista de Hola y escriba el número de cuenta del transportista. Microsoft usará esta cuenta tooship Hola unidades atrás tooyou una vez completado el trabajo de importación.
   
   Si tiene el número de seguimiento, seleccione el transportista de entrega de la lista de Hola y escriba el número de seguimiento.
   
   Si no tiene un seguimiento número todavía, elija **proporcionaré mi información de envío para este trabajo de importación una vez que haya enviado mi paquete**, a continuación, complete el proceso de importación de Hola.
6. devolver el número de seguimiento después de que ha enviado el paquete de tooenter toohello **importación/exportación** página de la cuenta de almacenamiento en hello portal de Azure, seleccione el trabajo de lista de Hola y elija **información de envío**. Navegar por el Asistente de Hola y escriba el número de seguimiento en el paso 2.
   
    Si no se actualiza Hola número de seguimiento en 2 semanas de creación de trabajo de hello, trabajo Hola expirará.
   
    Si el trabajo de hello está en estado de creación, envío o transferencia de hello, también puede actualizar el número de cuenta del transportista en el paso 2 del Asistente para Hola. Una vez que el trabajo de hello está en estado de empaquetado de hello, no se puede actualizar el número de cuenta del transportista para ese trabajo.
7. Puede realizar un seguimiento del progreso de trabajo en el panel del portal Hola. Vea lo que significa cada estado del trabajo en la sección anterior de Hola por [ver el estado del trabajo](#viewing-your-job-status).

## <a name="create-an-export-job"></a>Crear un trabajo de exportación
Crear un hello de toonotify de trabajo de exportación de servicio de importación y exportación que deberá enviar uno o del centro de datos de toohello de más unidades de disco vacías para que se pueden exportar datos desde las unidades de toohello de cuenta de almacenamiento y las unidades de hello, a continuación, enviaban tooyou.

### <a name="prepare-your-drives"></a>Preparación de las unidades
Para preparar las unidades para el trabajo de exportación, se recomienda realizar las siguientes comprobaciones previas:

1. Compruebe el número de Hola de discos necesarios mediante el comando de la herramienta de hello WAImportExport PreviewExport. Para más información, consulte [Vista previa de uso de disco para un trabajo de exportación](https://msdn.microsoft.com/library/azure/dn722414.aspx). Le ayuda a obtener una vista previa de uso de la unidad para los blobs de Hola que seleccionó, basándose en hello tamaño de unidades de hello va toouse.
2. Compruebe que se puede leer o escribir toohello unidad de disco duro que se enviarán para trabajo de exportación de Hola.

### <a name="create-hello-export-job"></a>Crear trabajo de exportación de Hola
1. toocreate un trabajo de exportación, navegar por la cuenta de almacenamiento tooyour Hola portal de Azure y ver Hola panel. En **vista rápida**, haga clic en **crear un trabajo de exportación de** y continúe con el Asistente de Hola.
2. En el paso 2, proporcionar información de contacto para hello responsable de este trabajo de exportación. Si desea que los datos de registro detallado de toosave de trabajo de exportación de hello, compruebe la opción de hello demasiado**guardar Hola registro detallado en mi contenedor de blobs 'waimportexport'**.
3. En el paso 3, especifique qué blob de datos que se va tooexport desde su espacio de almacenamiento cuenta tooyour de unidad o unidades. Puede elegir tooexport todos los datos de blob de cuenta de almacenamiento de hello, o puede especificar que los blobs o conjuntos de tooexport de blobs.
   
   toospecify un tooexport blob, use hello **es igual a** selector y especifique el blob de toohello de ruta de acceso relativa de hello, empezando por el nombre del contenedor de Hola. Use *$root* contenedor raíz de toospecify Hola.
   
   toospecify todos los blobs a partir de un prefijo, use hello **empieza por** selector y especifique el prefijo de hello, comenzar con una barra diagonal '/'. prefijo de Hello puede ser el prefijo de hello del nombre de contenedor de hello, nombre de contenedor completa de Hola o nombre del contenedor completa de hello seguido por el prefijo de Hola de nombre de blob de Hola.
   
   Hello en la tabla siguiente muestra ejemplos de rutas de acceso de blob válido:
   
   | Selector | Ruta del blob | Description |
   | --- | --- | --- |
   | Empieza por |/ |Exporta todos los blobs en la cuenta de almacenamiento de Hola |
   | Empieza por |/$root/ |Exporta todos los blobs en el contenedor raíz de Hola |
   | Empieza por |/book |Exporta todos los blobs de cualquier contenedor que empiecen por el prefijo **book** |
   | Empieza por |/music/ |Exporta todos los blobs del contenedor **music** |
   | Empieza por |/music/love |Exporta todos los blobs del contenedor **music** que empiecen por el prefijo **love**. |
   | Igual demasiado|$root/logo.bmp |Blob de exportaciones **logo.bmp** en el contenedor raíz de Hola |
   | Igual demasiado|videos/story.mp4 |Exporta el blob **story.mp4** del contenedor **videos** |
   
   Debe proporcionar rutas de acceso de blob de hello en los formatos válidos tooavoid errores durante el procesamiento, como se muestra en esta captura de pantalla.
   
   ![Creación del trabajo de exportación - Paso 3](./media/storage-import-export-service/export-job-03.png)
4. En el paso 4, escriba un nombre descriptivo para el trabajo de exportación de Hola. nombre de Hola que especifique puede contener solo letras minúsculas, números, guiones y caracteres de subrayado, debe empezar por una letra y no puede contener espacios.
   
   región del centro de datos Hola indicará toowhich de centro de datos de hello debe enviar el paquete. Consulte las P+F de Hola a continuación para obtener más información.
5. En el paso 5, seleccione el transportista de devolución de lista de Hola y escriba el número de cuenta del transportista. Microsoft usará esta cuenta tooship tooyou una vez completado el trabajo de exportación realizar copias de las unidades de disco.
   
   Si tiene el número de seguimiento, seleccione el transportista de entrega de la lista de Hola y escriba el número de seguimiento.
   
   Si no tiene un seguimiento número todavía, elija **proporcionaré mi información de envío para este trabajo de exportación una vez que haya enviado mi paquete**, a continuación, complete el proceso de exportación de Hola.
6. devolver el número de seguimiento después de que ha enviado el paquete de tooenter toohello **importación/exportación** página de la cuenta de almacenamiento en hello portal de Azure, seleccione el trabajo de lista de Hola y elija **información de envío**. Navegar por el Asistente de Hola y escriba el número de seguimiento en el paso 2.
   
    Si no se actualiza Hola número de seguimiento en 2 semanas de creación de trabajo de hello, trabajo Hola expirará.
   
    Si el trabajo de hello está en estado de creación, envío o transferencia de hello, también puede actualizar el número de cuenta del transportista en el paso 2 del Asistente para Hola. Una vez que el trabajo de hello está en estado de empaquetado de hello, no se puede actualizar el número de cuenta del transportista para ese trabajo.
   
   > [!NOTE]
   > Si Hola blob toobe exporta está en uso en el momento de Hola de copiar unidad toohard, servicio de importación y exportación de Azure tendrá una instantánea de hello blob y copia Hola instantánea.
   > 
   > 
7. Puede realizar un seguimiento del progreso de trabajo en panel de Hola Hola portal de Azure. Vea lo que significa cada estado del trabajo en la sección anterior de hello en "ver el estado del trabajo".
8. Después de recibir las unidades de hello con los datos exportados, puede ver y copiar las claves de BitLocker Hola generadas por servicio de hello para la unidad. Navegar por la cuenta de almacenamiento tooyour Hola portal de Azure y haga clic en ficha de importación y exportación de Hola. Seleccione el trabajo de exportación de lista de Hola y haga clic en botón Ver claves de Hola. las claves de BitLocker de Hello aparecen como se muestra a continuación:
   
   ![Visualización de claves de BitLocker de un trabajo de exportación](./media/storage-import-export-service/export-job-bitlocker-keys.png)

Vaya a través de la sección de preguntas más frecuentes de Hola a continuación tal y como lo abordan los problemas más comunes de Hola clientes encuentran al usar este servicio.

## <a name="frequently-asked-questions"></a>Preguntas más frecuentes

**¿Puedo copiar almacenamiento de archivos de Azure mediante el servicio de importación y exportación de hello?**

No, Hola servicio de importación y exportación de Azure solo admite Blobs en bloques y Blobs en páginas. No se admiten todos los demás tipos de almacenamiento, lo que incluye Azure File Storage, Table Storage y Queue Storage.

**¿Está disponible para las suscripciones de CSP servicio de importación y exportación de Azure de hello?**

No, el servicio Azure Import/Export no admite suscripciones a CSP.

**¿Se puede omitir la preparación de unidad de Hola para un trabajo de importación o ¿se puede preparar una unidad sin necesidad de copiar?**

Cualquier unidad que desea que tooship para la importación de datos debe estar preparada mediante la herramienta WAImportExport de Azure de Hola. Debe usar la unidad de hello WAImportExport herramienta toocopy datos toohello.

**¿Necesito tooperform cualquier preparación de disco al crear un trabajo de exportación?**

No, pero se recomiendan algunas comprobaciones previas. Compruebe el número de Hola de discos necesarios mediante el comando de la herramienta de hello WAImportExport PreviewExport. Para más información, consulte [Vista previa de uso de disco para un trabajo de exportación](https://msdn.microsoft.com/library/azure/dn722414.aspx). Le ayuda a obtener una vista previa de uso de la unidad para los blobs de Hola que seleccionó, basándose en hello tamaño de unidades de hello va toouse. También compruebe que puede leer de y escritura toohello unidad de disco duro que se enviarán para hello trabajo de exportación.

**¿Qué ocurre si se envía accidentalmente una unidad de disco duro que no se ajusta toohello admite requisitos?**

Centro de datos de Azure Hola devolverá unidad Hola que no se ajusta toohello admitido requisitos tooyou. Si sólo algunas de las unidades de hello en el paquete de Hola cumplen los requisitos de compatibilidad de hello, esas unidades se procesarán y se devolverán las unidades de Hola que no cumplen los requisitos de hello tooyou.

**¿Puedo cancelar un trabajo?**

Puede cancelar un trabajo si el estado es Creating o Shipping.

**¿Cuánto puedo ver estado de Hola de trabajos completados en hello portal de Azure?**

Puede ver estado de saludo de los trabajos completados para los días de too90. Los trabajos completados se eliminarán una vez transcurrido ese plazo.

**Si desea tooimport o exportación más de 10 unidades, ¿qué debo hacer?**

Una importación o exportación trabajo puede hacer referencia solo 10 unidades en un único trabajo de servicio de importación/exportación de Hola. Si desea tooship más de 10 unidades, puede crear varios trabajos. Las unidades que están asociadas con hello mismo trabajo debe distribuirse juntas en Hola mismo paquete.
Microsoft ofrece orientación y asistencia cuando la capacidad de datos abarca varios trabajos de importación en disco. Para más información, póngase en contacto con bulkimport@microsoft.com.

**¿Hola Hola unidades de formato de servicio antes de devolverlos?**

No. Todas las unidades están cifradas con BitLocker.

**¿Puedo adquirir unidades de Microsoft para los trabajos de importación y exportación?**

No. Necesitará tooship sus propias unidades tanto para importación y exportación los trabajos.

** ¿Cómo puedo acceder a los datos importados por este servicio**

se pueden tener acceso a datos de Hello en su cuenta de almacenamiento de Azure a través del Portal de Azure de Hola o mediante una herramienta independiente denominado Explorador de almacenamiento. https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-manage-with-storage-explorer 

**Una vez completado el trabajo de importación de Hola, ¿qué mis datos aspecto tendrá en cuenta de almacenamiento de hello? ¿Se conservará la jerarquía de directorios?**

Al preparar una unidad de disco duro para un trabajo de importación, el destino de Hola se especifica por campo de DstBlobPathOrPrefix hello en el conjunto de datos CSV. Este es el contenedor de destino de hello en toowhich de cuenta de almacenamiento Hola se copian los datos de la unidad de disco duro de Hola. Dentro de este contenedor de destino, los directorios virtuales se crean para las carpetas de la unidad de disco duro de Hola y blobs se crean para los archivos. 

**¿Si la unidad de hello tiene archivos que ya existen en mi cuenta de almacenamiento, servicio de hello sobrescribirá los blobs existentes en mi cuenta de almacenamiento?**

Al preparar la unidad de hello, puede especificar si los archivos de destino de Hola se deben sobrescribir o pasa por alto mediante el campo de hello en el archivo CSV de conjunto de datos llamado a la disposición: < cambiar el nombre | sobrescribir no | sobrescribir >. De forma predeterminada, el servicio de Hola se cambie el nombre de los nuevos archivos de hello en lugar de sobrescribir blobs existentes.

**¿Es la herramienta WAImportExport de hello compatible con sistemas operativos de 32 bits?**
No. Hola WAImportExport herramienta solo es compatible con sistemas operativos de Windows de 64 bits. Consulte la sección de sistemas operativos toohello Hola [requisitos previos](#pre-requisites) para obtener una lista completa de las versiones compatibles de sistema operativo.

**¿Debo incluir algo distinto de la unidad de disco duro de hello en Mi paquete?**

Envíe solo las unidades de disco duro. No incluya elementos como cables de alimentación o cables USB.

**¿Es necesario tooship Mis discos con FedEx o DHL?**

Puede distribuir el centro de datos de las unidades toohello con cualquier operador conocido como FedEx, DHL, SAI (UPS) o US Postal Service. Sin embargo, para hello envío unidades tooyou atrás desde el centro de datos de hello, debe proporcionar un número de cuenta de FedEx Hola Estados Unidos y Europa, o un número de cuenta DHL en hello Asia y regiones de Australia.

**¿Existe alguna restricción internacional en el envío de las unidades?**

Tenga en cuenta que los medios físicos de Hola que se entregan pueden requerir fronteras internacionales toocross. Usted es responsable de asegurarse de que el medio físico y los datos se importado o exportados con arreglo a las leyes de Hola. Antes de enviar un medio físico hello, consulte con su tooverify asesores que los medios y los datos pueden ser legalmente centro de datos enviados toohello identificado. Esto le ayudará a tooensure que llega a Microsoft de manera oportuna.

**Cuando se crea un trabajo, Hola dirección de envío es una ubicación que sea diferente de la ubicación de la cuenta de almacenamiento. ¿qué debo hacer?**

Algunas ubicaciones de la cuenta de almacenamiento son asignada tooalternate ubicaciones de envío. Previamente ubicaciones de envío disponible también pueden ser ubicaciones de tooalternate temporalmente asignadas. Compruebe siempre Hola proporcionada durante la creación de trabajo antes de enviar las unidades de disco de dirección de envío.

**Al enviar la unidad, operador de hello solicita Hola datos center contacto dirección y número de teléfono. ¿Qué debo proporcionar?**

Hola, número de teléfono y DC dirección se proporciona como parte de la creación del trabajo.

**¿Puedo usar buzones de PST de toocopy del servicio de importación y exportación de Hola y tooO365 de datos de SharePoint?**

Consulte demasiado[archivos PST de importación o tooOffice de datos de SharePoint 365](https://technet.microsoft.com/library/ms.o365.cc.ingestionhelp.aspx).

**¿Puedo usar toocopy de servicio de importación y exportación de hello Mi servicio de copia de seguridad de Azure de las copias de seguridad sin conexión toohello?**

Consulte demasiado[flujo de trabajo de copia de seguridad sin conexión en copia de seguridad de Azure](../../backup/backup-azure-backup-import-export.md).

**¿Qué es números máximos Hola de unidad de disco duro para en un solo envío?**

Puede ser cualquier número de unidades de disco duro en un solo envío y si los discos de hello pertenecen toomultiple trabajos se recomienda demasiado un) tienen discos Hola etiquetados con nombres de trabajo correspondiente Hola. b) trabajos de Hola de actualización con un número de seguimiento lleva el sufijo de -1, etcetera-2.
  
**¿Qué es hello máximo Blob en bloques y tamaño de Blob de página admitido por la importación y exportación de disco?**

El tamaño máximo aproximado de blobs en bloques admitido es de 4,768 TB o 5.000.000 MB.
El tamaño máximo de blobs en páginas es de 1 TB.

**¿Admite el servicio Import/Export el cifrado AES 256?**

Servicio de importación y exportación de Azure de forma predeterminada se cifra con el cifrado de bitlocker de AES 128, pero puede ser mayor tooAES 256 mediante manualmente cifrado con bitlocker antes de que se copian los datos. 

Si usa [WAImportExpot V1](http://download.microsoft.com/download/0/C/D/0CD6ABA7-024F-4202-91A0-CE2656DCE413/WaImportExportV1.zip), a continuación se muestra un comando de ejemplo.
```
WAImportExport PrepImport /sk:<StorageAccountKey> /csas:<ContainerSas> /t: <TargetDriveLetter> [/format] [/silentmode] [/encrypt] [/bk:<BitLockerKey>] [/logdir:<LogDirectory>] /j:<JournalFile> /id:<SessionId> /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory> [/Disposition:<Disposition>] [/BlobType:<BlockBlob|PageBlob>] [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>] 
```
Si usa [herramienta WAImportExport](http://download.microsoft.com/download/3/6/B/36BFF22A-91C3-4DFC-8717-7567D37D64C5/WAImportExport.zip) especifique "AlreadyEncrypted" y proporcione la clave de hello en hello driveset CSV.
```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
G,AlreadyFormatted,SilentMode,AlreadyEncrypted,060456-014509-132033-080300-252615-584177-672089-411631 |
```
## <a name="next-steps"></a>Pasos siguientes

* [Configurar la herramienta WAImportExport de Hola](storage-import-export-tool-how-to.md)
* [Transferencia de datos con la utilidad de línea de comandos de AzCopy Hola](storage-use-azcopy.md)
* [Ejemplo de API de REST de Azure Import/Export](https://azure.microsoft.com/documentation/samples/storage-dotnet-import-export-job-management/)

