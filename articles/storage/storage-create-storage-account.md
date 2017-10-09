---
title: aaaHow toocreate, administrar o eliminar una cuenta de almacenamiento en hello portal de Azure | Documentos de Microsoft
description: "Crear una nueva cuenta de almacenamiento, administrar las claves de acceso de cuenta o eliminar una cuenta de almacenamiento en hello portal de Azure. Obtenga información acerca de las cuentas de almacenamiento estándar y premium."
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 87c37da0-6cc6-4d88-a330-ef2896a1531d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
f1_keywords: sql13.swb.windowsazurestorage.connect.f1
ms.date: 01/23/2017
ms.author: robinsh
ms.openlocfilehash: c11c6509e192170db4812f47c389fc1009b94daf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="about-azure-storage-accounts"></a>Acerca de las cuentas de almacenamiento de Azure
[!INCLUDE [storage-selector-portal-create-storage-account](../../includes/storage-selector-portal-create-storage-account.md)]

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

## <a name="overview"></a>Información general
Una cuenta de almacenamiento de Azure proporciona un toostore de espacio de nombres único y obtener acceso a los objetos de datos de almacenamiento de Azure. Todos los objetos de una cuenta de almacenamiento se facturan juntos como un grupo. De forma predeterminada, datos de hello en su cuenta de están disponible solo tooyou, propietario de la cuenta de hello.

[!INCLUDE [storage-account-types-include](../../includes/storage-account-types-include.md)]

## <a name="storage-account-billing"></a>Facturación de la cuenta de almacenamiento
[!INCLUDE [storage-account-billing-include](../../includes/storage-account-billing-include.md)]

> [!NOTE]
> Cuando se crea una máquina virtual de Azure, una cuenta de almacenamiento se crea automáticamente en la ubicación de implementación de hello si ya no tiene una cuenta de almacenamiento en esa ubicación. Por lo que no es necesario toofollow Hola estos pasos toocreate una cuenta de almacenamiento para los discos de máquina virtual. nombre de cuenta de almacenamiento de Hola se basará en el nombre de la máquina virtual de Hola. Vea hello [documentación de máquinas virtuales de Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) para obtener más detalles.
> 
> 

## <a name="storage-account-endpoints"></a>Extremos de la cuenta de almacenamiento
Cada objeto que se almacena en el Almacenamiento de Azure tiene una dirección URL única. formatos de nombres de cuenta de almacenamiento de Hola Hola subdominio de esa dirección. Hello combinación de nombre de subdominio y de dominio, que es el servicio de tooeach específico, forma un *extremo* para su cuenta de almacenamiento.

Por ejemplo, si la cuenta de almacenamiento se denomina *mystorageaccount*, puntos de conexión de hello predeterminados para la cuenta de almacenamiento son:

* Blob service: http://*mystorageaccount*.blob.core.windows.net
* Table service: http://*mystorageaccount*.table.core.windows.net
* Queue service: http://*mystorageaccount*.queue.core.windows.net
* Servicio de archivos: http://*mystorageaccount*.file.core.windows.net

> [!NOTE]
> Una cuenta de almacenamiento Blob solo expone el extremo de servicio de Blob de Hola.
> 
> 

dirección URL de Hello para tener acceso a un objeto en una cuenta de almacenamiento se crea mediante la anexión de ubicación del objeto de hello en el punto de conexión de hello almacenamiento cuenta toohello. Por ejemplo, una dirección de blob podría tener este formato: http://*mystorageaccount*.blob.core.windows.net/*mycontainer*/*myblob*.

También puede configurar un toouse de nombre de dominio personalizado con su cuenta de almacenamiento. En el caso de las cuentas de almacenamiento clásicas, consulte [Configurar un nombre de dominio personalizado para el punto de conexión de Almacenamiento de blobs](storage-custom-domain-name.md) para conocer más detalles. Para las cuentas de almacenamiento de administrador de recursos, esta funcionalidad no se agregó toohello [portal de Azure](https://portal.azure.com) aún, pero se puede configurar con PowerShell. Para obtener más información, vea hello [AzureRmStorageAccount conjunto](https://msdn.microsoft.com/library/mt607146.aspx) cmdlet.  

## <a name="create-a-storage-account"></a>Crear una cuenta de almacenamiento
1. Inicie sesión en toohello [portal de Azure](https://portal.azure.com).
2. En el menú del concentrador hello, seleccione **New** -> **almacenamiento** -> **cuenta de almacenamiento**.
3. Escriba un nombre para la cuenta de almacenamiento. Vea [puntos de conexión de cuenta de almacenamiento](#storage-account-endpoints) para obtener información detallada acerca de cómo nombre de cuenta de almacenamiento de hello será tooaddress usa los objetos de almacenamiento de Azure.
   
   > [!NOTE]
   > Los nombres de cuentas de almacenamiento deben tener entre 3 y 24 caracteres, y solo pueden contener números y letras minúsculas.
   > 
   > El nombre de la cuenta de almacenamiento debe ser único dentro de Azure. Hola portal de Azure se indicará si el nombre de la cuenta de almacenamiento Hola que selecciona ya está en uso.
   > 
   > 
4. Especificar toobe de modelo de implementación de hello usa: **el Administrador de recursos** o **clásico**. **El Administrador de recursos** recomienda Hola modelo de implementación. Para obtener más información, vea [Descripción de la implementación del Administrador de recursos y la implementación clásica](../azure-resource-manager/resource-manager-deployment-model.md).
   
   > [!NOTE]
   > Las cuentas de almacenamiento de BLOB solo pueden crearse mediante el modelo de implementación del Administrador de recursos de Hola.
   > 
   > 
5. Seleccionar tipo de saludo de la cuenta de almacenamiento: **de propósito General** o **almacenamiento de blobs**. **Propósito general** es Hola predeterminado.
   
    Si **de propósito General** se ha seleccionado, a continuación, especifique el nivel de rendimiento de hello: **estándar** o **Premium**. valor predeterminado de Hello es **estándar**. Para obtener más detalles sobre las cuentas de almacenamiento estándar y premium, consulte [Introducción tooMicrosoft almacenamiento de Azure](storage-introduction.md) y [almacenamiento Premium: almacenamiento de alto rendimiento para cargas de trabajo de máquina Virtual de Azure](storage-premium-storage.md).
   
    Si **almacenamiento de blobs** se ha seleccionado, a continuación, especifique el nivel de acceso de hello: **activa** o **frío**. valor predeterminado de Hello es **activa**. Consulte [Almacenamiento de blobs de Azure: niveles de acceso Esporádico y Frecuente](storage-blob-storage-tiers.md) para más información.
6. Seleccione opción de replicación de Hola Hola cuenta de almacenamiento: **LRS**, **GRS**, **RA-GRS**, o **ZRS**. valor predeterminado de Hello es **RA-GRS**. Para obtener más información sobre las opciones de replicación del Almacenamiento de Azure, consulte [Replicación de Almacenamiento de Azure](storage-redundancy.md).
7. Seleccione la suscripción de hello en que desea que la nueva cuenta de almacenamiento de toocreate Hola.
8. Especifique un nuevo grupo de recursos o seleccione un grupo de recursos existente. Para más información sobre los grupos de recursos, consulte [Información general de Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
9. Seleccione la ubicación geográfica de hello para la cuenta de almacenamiento. Consulte [Regiones de Azure](https://azure.microsoft.com/regions/#services) para más información acerca de qué servicios están disponibles en cada región.
10. Haga clic en **crear** cuenta de almacenamiento de toocreate Hola.

## <a name="manage-your-storage-account"></a>Administración de la cuenta de almacenamiento
### <a name="change-your-account-configuration"></a>Cambio de la configuración de cuenta
Después de crear la cuenta de almacenamiento, puede modificar su configuración, como el cambio de opción de replicación de hello utilizado para la cuenta de Hola o cambiar nivel de acceso de Hola para una cuenta de almacenamiento de blobs. Hola [portal de Azure](https://portal.azure.com), navegar por la cuenta de almacenamiento de tooyour, busque y haga clic en **configuración** en **configuración** tooview o cambio de configuración de la cuenta de hello.

> [!NOTE]
> Según el nivel de rendimiento de Hola que eligió al crear la cuenta de almacenamiento de hello, algunas opciones de replicación no pueden estar disponibles.
> 
> 

Cambiar la opción de replicación de hello, cambiará el precio del servicio. Consulte [Precios de Almacenamiento de Azure](https://azure.microsoft.com/pricing/details/storage/) para más información.

Para Blob cuentas de almacenamiento, cambiar el nivel de acceso de hello pueden incurrir en cargos de hello cambiar además toochanging el precio del servicio. Vea hello [cuentas de almacenamiento - precios y facturación de Blob](storage-blob-storage-tiers.md#pricing-and-billing) para obtener más detalles.

### <a name="manage-your-storage-access-keys"></a>Administración de las claves de acceso de almacenamiento
Cuando se crea una cuenta de almacenamiento, Azure genera dos claves de acceso de almacenamiento de 512 bits, que se usan para la autenticación cuando se tiene acceso a la cuenta de almacenamiento de Hola. Proporcionando dos claves de acceso de almacenamiento de Azure permite las claves de hello tooregenerate con ningún servicio de almacenamiento de tooyour de interrupción o un servicio de toothat de acceso.

> [!NOTE]
> Se recomienda no compartir con nadie las claves de acceso de almacenamiento. toopermit acceder a los recursos de toostorage sin dar las claves de acceso, puede usar un *firma de acceso compartido*. Una firma de acceso compartido proporciona acceso tooa recursos en su cuenta para un intervalo que define y con permisos de Hola que especifique. Consulte [Uso de firmas de acceso compartido (SAS)](storage-dotnet-shared-access-signature-part-1.md) para más información.
> 
> 
<a id="view-and-copy-storage-access-keys"/></a>
#### <a name="view-and-copy-storage-access-keys"></a>Visualización y copia de las claves de acceso de almacenamiento
Hola [portal de Azure](https://portal.azure.com), navegue tooyour cuenta de almacenamiento, haga clic en **toda la configuración de** y, a continuación, haga clic en **las claves de acceso** tooview, copiar y regenerar las claves de acceso de cuenta. Hola **teclas de acceso** hoja también incluye las cadenas de conexión configuradas previamente con las claves principales y secundarias que se pueden copiar toouse en sus aplicaciones.

#### <a name="regenerate-storage-access-keys"></a>Nueva generación de las claves de acceso de almacenamiento
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
2. Regenerar clave de acceso principal de hello para la cuenta de almacenamiento. En hello **teclas de acceso** hoja, haga clic en **regenerar Key1**y, a continuación, haga clic en **Sí** tooconfirm que desea toogenerate una nueva clave.
3. Actualizar las cadenas de conexión de hello en su clave de acceso principal nueva de código tooreference Hola.
4. Clave de acceso secundaria de regenerar Hola Hola igual manera.

## <a name="delete-a-storage-account"></a>Eliminar una cuenta de almacenamiento
tooremove una cuenta de almacenamiento que ya no se está usando, navegar por la cuenta de almacenamiento de toohello en hello [portal de Azure](https://portal.azure.com)y haga clic en **eliminar**. Al eliminar una cuenta de almacenamiento, eliminan toda cuenta hello, incluidos todos los datos de cuenta de hello.

> [!WARNING]
> Es imposible toorestore una cuenta de almacenamiento se eliminó o recuperar contenido de Hola que contenía antes de la eliminación. Prepararse nada tooback seguro de que desea toosave antes de eliminar la cuenta de hello. Esto también es válido para todos los recursos en la cuenta de hello: al eliminar un blob, tabla, cola o archivo, éste se eliminará permanentemente.
> 
> 

toodelete una cuenta de almacenamiento que está asociada a una máquina virtual de Azure, primero debe asegurarse de que los discos de máquina virtual que se haya eliminado. Si no elimina primero los discos de máquina virtual, a continuación, cuando intente toodelete su cuenta de almacenamiento, verá un mensaje de error similar al:

    Failed toodelete storage account <vm-storage-account-name>. Unable toodelete storage account <vm-storage-account-name>: 'Storage account <vm-storage-account-name> has some active image(s) and/or disk(s). Ensure these image(s) and/or disk(s) are removed before deleting this storage account.'.

Si cuenta de almacenamiento de hello usa el modelo de implementación de hello clásico, puede quitar el disco de máquina virtual de hello siguiendo estos pasos en hello [portal de Azure](https://manage.windowsazure.com):

1. Navegue toohello [portal de Azure clásico](https://manage.windowsazure.com).
2. Navegue toohello pestaña de máquinas virtuales.
3. Haga clic en la ficha discos del saludo.
4. Seleccione el disco de datos y luego haga clic en Eliminar disco.
5. imágenes de disco toodelete, vaya la ficha de imágenes de toohello y elimine las imágenes que se almacenan en la cuenta de hello.

Para obtener más información, vea hello [documentación de la máquina Virtual de Azure](http://azure.microsoft.com/documentation/services/virtual-machines/).

## <a name="next-steps"></a>Pasos siguientes
* [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente disponible, de Microsoft que le permite toowork visualmente con datos del almacenamiento de Azure en Windows, Mac OS y Linux.
* [Almacenamiento de blobs de Azure: niveles de acceso Esporádico y Frecuente](storage-blob-storage-tiers.md)
* [Replicación de almacenamiento de Azure](storage-redundancy.md)
* [Configuración de las cadenas de conexión de Almacenamiento de Azure](storage-configure-connection-string.md)
* [Transferencia de datos con la utilidad de línea de comandos de AzCopy Hola](storage-use-azcopy.md)
* Visite hello [Blog del equipo de almacenamiento de Azure](http://blogs.msdn.com/b/windowsazurestorage/).

