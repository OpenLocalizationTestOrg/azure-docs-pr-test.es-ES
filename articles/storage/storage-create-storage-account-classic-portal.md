---
title: "aaaHow toocreate, administrar o eliminar una cuenta de almacenamiento en hello portal de Azure clásico | Documentos de Microsoft"
description: "Crear una nueva cuenta de almacenamiento, administrar las claves de acceso de cuenta o eliminar una cuenta de almacenamiento en hello portal de Azure. Obtenga información acerca de las cuentas de almacenamiento estándar y premium."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 5e4f4360-3f81-4d63-a0b1-e7771b67af11
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: 6ee2359e02c7c9e9c111e1fc87a6160bb8b785b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a>Acerca de las cuentas de almacenamiento de Azure
[!INCLUDE [storage-selector-portal-create-storage-account](../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-try-azure-tools](../../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Información general
Un deja de cuenta de almacenamiento de Azure se accede a los servicios de Azure Blob, cola, tabla y archivo de toohello en el almacenamiento de Azure. La cuenta de almacenamiento proporciona Hola espacio de nombres único para los objetos de datos de almacenamiento de Azure. De forma predeterminada, datos de hello en su cuenta de están disponible solo tooyou, propietario de la cuenta de hello.

Existen dos tipos de cuentas de almacenamiento:

* Una cuenta de almacenamiento estándar incluye el almacenamiento de blobs, tablas, colas y archivos.
* Una cuenta de almacenamiento premium actualmente solo admite los discos de máquinas virtuales de Azure. Consulte [Almacenamiento premium: almacenamiento de alto rendimiento para cargas de trabajo de máquinas virtuales de Azure](storage-premium-storage.md) para una información general detallada del Almacenamiento premium.

## <a name="storage-account-billing"></a>Facturación de la cuenta de almacenamiento
El uso de Almacenamiento de Azure se le factura según su cuenta de almacenamiento. Los costos de almacenamiento se basan en cuatro factores: capacidad de almacenamiento, esquema de replicación, transacciones de almacenamiento y salida de datos.

* Capacidad de almacenamiento refiere toohow mucho de la cobertura de la cuenta de almacenamiento que usa datos toostore. costo de Hello almacenar simplemente los datos se determina por la cantidad de datos se almacenan y cómo se ha replicado.
* La replicación determina cuántas copias de los datos se conservan al mismo tiempo, y en qué ubicaciones.
* Las transacciones hacen referencia tooall lectura y tooAzure almacenamiento de las operaciones de escritura.
* Salida de datos hace referencia toodata transferido fuera de una región de Azure. Cuando se tiene acceso a datos hello en su cuenta de almacenamiento por una aplicación que no se está ejecutando en Hola misma región, si aplicación es un servicio de nube o algún otro tipo de aplicación, a continuación, se le cobrará por la salida de datos. (Para los servicios de Azure, que puede seguir pasos toogroup sus datos y servicios en hello mismos datos centros tooreduce o eliminar los cargos de salida de datos.)  

Hola [precios de almacenamiento de Azure](https://azure.microsoft.com/pricing/details/storage) página proporciona información detallada de precios para la capacidad de almacenamiento, replicación y transacciones. Hola [detalles de precios de transferencias de datos](https://azure.microsoft.com/pricing/details/data-transfers/) página proporciona información detallada de precios para la salida de datos.

Para obtener más información acerca de los objetivos de capacidad y rendimiento de la cuenta de almacenamiento, consulte [Objetivos de escalabilidad y rendimiento de Almacenamiento de Azure](storage-scalability-targets.md).

> [!NOTE]
> Cuando se crea una máquina virtual de Azure, una cuenta de almacenamiento se crea automáticamente en la ubicación de implementación de hello si ya no tiene una cuenta de almacenamiento en esa ubicación. Por lo que no es necesario toofollow Hola estos pasos toocreate una cuenta de almacenamiento para los discos de máquina virtual. nombre de cuenta de almacenamiento de Hola se basará en el nombre de la máquina virtual de Hola. Vea hello [documentación de máquinas virtuales de Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) para obtener más detalles.
> 
> 

## <a name="create-a-storage-account"></a>Crear una cuenta de almacenamiento
1. Inicie sesión en toohello [Portal clásico de Azure](https://manage.windowsazure.com).
2. Haga clic en **New** en barra de tareas de hello en parte inferior de Hola de página Hola. Elija **Servicios de datos** | **Almacenamiento** y haga clic en **Creación rápida**.
   
    ![Nueva cuenta de almacenamiento](./media/storage-create-storage-account-classic-portal/storage_NewStorageAccount.png)
3. En **Dirección URL**, escriba un nombre para la cuenta de almacenamiento.
   
   > [!NOTE]
   > Los nombres de cuentas de almacenamiento deben tener entre 3 y 24 caracteres, y solo pueden contener números y letras minúsculas.
   > 
   > El nombre de la cuenta de almacenamiento debe ser único dentro de Azure. Hola Portal clásico de Azure se indicará si selecciona nombre de cuenta de almacenamiento de hello ya está en uso.
   > 
   > 
   
    Vea [puntos de conexión de cuenta de almacenamiento](#storage-account-endpoints) a continuación para obtener información detallada acerca de cómo nombre de cuenta de almacenamiento de hello será tooaddress usa los objetos de almacenamiento de Azure.
4. En **ubicación/grupo de afinidad**, seleccione una ubicación para la cuenta de almacenamiento es cerrar clientes tooyou o tooyour. Si los datos de la cuenta de almacenamiento se obtendrá acceso desde otro servicio de Azure, como una máquina virtual de Azure o un servicio de nube, puede que desee tooselect un grupo de afinidad de hello lista toogroup su cuenta de almacenamiento en hello mismo centro de datos con otros servicios de Azure que está usando tooimprove rendimiento y reducir los costos.
   
    Tenga en cuenta que debe seleccionar un grupo de afinidad cuando se crea la cuenta de almacenamiento. No se puede mover un grupo de afinidad de tooan cuenta existente. Para obtener información sobre los grupos de afinidad, consulte [Coubicación de servicios con un grupo de afinidad](#service-co-location-with-an-affinity-group) que se muestra a continuación.
   
   > [!IMPORTANT]
   > toodetermine qué ubicaciones están disponibles para su suscripción, puede llamar a hello [enumerar todos los proveedores de recursos](https://msdn.microsoft.com/library/azure/dn790524.aspx) operación. proveedores de toolist desde PowerShell, llame a [AzureLocation Get](https://msdn.microsoft.com/library/azure/dn757693.aspx). Desde. NET, use hello [lista](https://msdn.microsoft.com/library/azure/microsoft.azure.management.resources.provideroperationsextensions.list.aspx) método de hello ProviderOperationsExtensions clase.
   > 
   > Además, consulte [Regiones de Azure](https://azure.microsoft.com/regions/#services) para obtener más información acerca de qué servicios están disponibles en la región.
   > 
   > 
5. Si tiene más de una suscripción de Azure, Hola **suscripción** campo se muestra. En **suscripción**, escriba Hola suscripción de Azure que desee toouse Hola cuenta de almacenamiento.
6. En **replicación**, seleccione Hola nivel deseado de replicación para la cuenta de almacenamiento. Hola recomienda la opción de replicación es la replicación con redundancia geográfica, que proporciona la máxima durabilidad de los datos. Para obtener más información sobre las opciones de replicación del Almacenamiento de Azure, consulte [Replicación de Almacenamiento de Azure](storage-redundancy.md).
7. Haga clic en **Crear cuenta de almacenamiento**.
   
    La cuenta de almacenamiento puede tardar unos toocreate minutos. estado de hello toocheck, puede supervisar las notificaciones de hello en parte inferior de Hola de hello Portal clásico de Azure. Una vez creada la cuenta de almacenamiento de hello, la nueva cuenta de almacenamiento tiene **Online** estado y está listo para su uso.

![Página de almacenamiento](./media/storage-create-storage-account-classic-portal/Storage_StoragePage.png)

### <a name="storage-account-endpoints"></a>Puntos de conexión de cuenta de almacenamiento
Cada objeto que se almacena en el Almacenamiento de Azure tiene una dirección URL única. formatos de nombres de cuenta de almacenamiento de Hola Hola subdominio de esa dirección. Hello combinación de nombre de subdominio y de dominio, que es el servicio de tooeach específico, forma un *extremo* para su cuenta de almacenamiento.

Por ejemplo, si la cuenta de almacenamiento se denomina *mystorageaccount*, puntos de conexión de hello predeterminados para la cuenta de almacenamiento son:

* Blob service: http://*mystorageaccount*.blob.core.windows.net
* Table service: http://*mystorageaccount*.table.core.windows.net
* Queue service: http://*mystorageaccount*.queue.core.windows.net
* Servicio de archivos: http://*mystorageaccount*.file.core.windows.net

Puede ver los puntos de conexión de hello para la cuenta de almacenamiento en panel de almacenamiento Hola Hola [Portal clásico de Azure](https://manage.windowsazure.com) una vez creada la cuenta de hello.

dirección URL de Hello para tener acceso a un objeto en una cuenta de almacenamiento se crea mediante la anexión de ubicación del objeto de hello en el punto de conexión de hello almacenamiento cuenta toohello. Por ejemplo, una dirección de blob podría tener este formato: http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*.

También puede configurar un toouse de nombre de dominio personalizado con su cuenta de almacenamiento. Consulte [Configurar un nombre de dominio personalizado para el punto de conexión de Almacenamiento de blobs](storage-custom-domain-name.md) para conocer más detalles.

### <a name="service-co-location-with-an-affinity-group"></a>Coubicación de servicios con un grupo de afinidad
Un *grupo de afinidad* es un grupo geográfico de los servicios de Azure y máquinas virtuales con la cuenta de almacenamiento de Azure. Un grupo de afinidad puede mejorar el rendimiento del servicio al ubicar las cargas de trabajo de equipo en hello mismos datos del centro o cerca de audiencia de usuarios de destino de Hola. Además, sin facturación cargos de salida cuando se tiene acceso a datos en una cuenta de almacenamiento de otro servicio que forma parte del programa Hola mismo grupo de afinidad.

> [!NOTE]
> toocreate un grupo de afinidad, abra hello <b>configuración</b> área de hello [Portal clásico de Azure](https://manage.windowsazure.com), haga clic en <b>grupos de afinidad</b>y, a continuación, haga clic en <b>agregar un grupo de afinidad</b> o hello <b>agregar</b> botón. También puede crear y administrar grupos de afinidad mediante Hola API de administración de servicios de Azure. Consulte <a href="http://msdn.microsoft.com/library/azure/ee460798.aspx">Operaciones en grupos de afinidad</a> para obtener más información.
> 
> 

## <a name="view-copy-and-regenerate-storage-access-keys"></a>Vista, copia y regeneración de las claves de acceso de almacenamiento
Cuando se crea una cuenta de almacenamiento, Azure genera dos claves de acceso de almacenamiento de 512 bits, que se usan para la autenticación cuando se tiene acceso a la cuenta de almacenamiento de Hola. Proporcionando dos claves de acceso de almacenamiento de Azure permite las claves de hello tooregenerate con ningún servicio de almacenamiento de tooyour de interrupción o un servicio de toothat de acceso.

> [!NOTE]
> Se recomienda no compartir con nadie las claves de acceso de almacenamiento. toopermit acceder a los recursos de toostorage sin dar las claves de acceso, puede usar un *firma de acceso compartido*. Una firma de acceso compartido proporciona acceso tooa recursos en su cuenta para un intervalo que define y con permisos de Hola que especifique. Consulte [Uso de firmas de acceso compartido (SAS)](storage-dotnet-shared-access-signature-part-1.md) para más información.
> 
> 

Hola [Portal clásico de Azure](https://manage.windowsazure.com), use **administrar claves** en el panel de Hola o hello **almacenamiento** página tooview, copiar y claves de acceso de almacenamiento de hello regenerar que se usan tooaccess Hola servicios Blob, tabla y cola.

### <a name="copy-a-storage-access-key"></a>Copia de una clave de acceso de almacenamiento
Puede usar **administrar claves** toocopy un toouse clave de acceso de almacenamiento en una cadena de conexión. cadena de conexión de Hello requiere nombre de cuenta de almacenamiento de hello y una clave toouse en la autenticación. Para obtener información acerca de cómo configurar conexión cadenas tooaccess servicios de almacenamiento de Azure, consulte [configurar cadenas de conexión de almacenamiento de Azure](storage-configure-connection-string.md).

1. Hola [Portal clásico de Azure](https://manage.windowsazure.com), haga clic en **almacenamiento**y, a continuación, haga clic en nombre de Hola de panel de hello almacenamiento cuenta tooopen Hola.
2. Haga clic en **Administrar claves**.
   
     **Administrar claves de acceso** .
   
    ![Managekeys](./media/storage-create-storage-account-classic-portal/Storage_ManageKeys.png)
3. toocopy una tecla de acceso de almacenamiento, texto de la tecla Hola select. A continuación, haga clic con el botón derecho y haga clic en **Copiar**.

### <a name="regenerate-storage-access-keys"></a>Nueva generación de las claves de acceso de almacenamiento
Le recomendamos que cambie las teclas de acceso de hello tooyour cuenta de almacenamiento, periódicamente toohelp proteger las conexiones de almacenamiento. Se asignan dos claves de acceso para que pueda mantener cuenta de almacenamiento de las conexiones toohello mediante una clave de acceso mientras se regenera Hola otra clave de acceso.

> [!WARNING]
> Volver a generar las claves de acceso puede afectar a los servicios en Azure, así como sus propias aplicaciones que dependen de la cuenta de almacenamiento de Hola. Todos los clientes que usan cuenta de almacenamiento de hello acceso tooaccess clave Hola deben ser clave nueva de hello toouse actualizada.
> 
> 

**Servicios multimedia** -si tiene servicios de multimedia que dependen de la cuenta de almacenamiento, deben volver a sincronizar las claves de acceso de hello con su servicio multimedia después de regenerar claves de Hola.

**Aplicaciones** : si tiene aplicaciones web o servicios en la nube esa cuenta de almacenamiento de uso hello, perderá las conexiones de hello si vuelve a generar las claves, a menos que poner las claves. 

**Exploradores de almacenamiento** : Si usas cualquiera [las aplicaciones de explorador de almacenamiento](storage-explorers.md), seguramente necesitará la clave de almacenamiento de hello tooupdate dichas aplicaciones usan.

Este es el proceso de Hola para rotar las claves de acceso de almacenamiento:

1. Actualizar las cadenas de conexión de hello en su clave de acceso secundaria de hello tooreference aplicación de código de cuenta de almacenamiento de Hola.
2. Regenerar clave de acceso principal de hello para la cuenta de almacenamiento. Hola [Portal clásico de Azure](https://manage.windowsazure.com), desde el panel de Hola o hello **configurar** página, haga clic en **administrar claves**. Haga clic en **regenerar** en Hola clave de acceso principal y, a continuación, haga clic en **Sí** tooconfirm que desea toogenerate una nueva clave.
3. Actualizar las cadenas de conexión de hello en su clave de acceso principal nueva de código tooreference Hola.
4. Regenerar clave de acceso secundaria de Hola.

## <a name="delete-a-storage-account"></a>Eliminar una cuenta de almacenamiento
una cuenta de almacenamiento que ya no se está usando, use tooremove **eliminar** en el panel de Hola o hello **configurar** página. **Eliminar** eliminaciones Hola cuenta de almacenamiento en su totalidad, incluidos todos Hola blobs, tablas y colas de cuenta de hello.

> [!WARNING]
> Es imposible toorestore una cuenta de almacenamiento se eliminó o recuperar contenido de Hola que contenía antes de la eliminación. Prepararse nada tooback seguro de que desea toosave antes de eliminar la cuenta de hello. Esto también es válido para todos los recursos en la cuenta de hello: al eliminar un blob, tabla, cola o archivo, éste se eliminará permanentemente.
> 
> Si la cuenta de almacenamiento contiene archivos de disco duro virtual para una máquina virtual de Azure, debe eliminar todas las imágenes y discos que usan los archivos de disco duro virtual antes de poder eliminar la cuenta de almacenamiento de Hola. En primer lugar, detener la máquina virtual de hello si se está ejecutando y, a continuación, elimínelo. discos toodelete, navegue toohello **discos** pestaña y eliminar los discos no existe. imágenes de toodelete, navegue toohello **imágenes** pestaña y elimine las imágenes que se almacenan en la cuenta de hello.
> 
> 

1. Hola [Portal clásico de Azure](https://manage.windowsazure.com), haga clic en **almacenamiento**.
2. Haga clic en cualquier entrada de cuenta de almacenamiento de hello excepto nombre hello y, a continuación, haga clic en **eliminar**.
   
     -O bien-
   
    Haga clic en nombre de Hola de panel de Hola de tooopen de cuentas de almacenamiento de hello y, a continuación, haga clic en **eliminar**.
3. Haga clic en **Sí** tooconfirm que desea que la cuenta de almacenamiento de toodelete Hola.

## <a name="next-steps"></a>Pasos siguientes
* toolearn más sobre el almacenamiento de Azure, vea hello [documentación del almacenamiento de Azure](https://azure.microsoft.com/documentation/services/storage/).
* Visite hello [Blog del equipo de almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/).
* [Transferencia de datos con la utilidad de línea de comandos de AzCopy Hola](storage-use-azcopy.md)

