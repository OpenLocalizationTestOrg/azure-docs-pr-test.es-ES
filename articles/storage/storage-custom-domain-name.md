---
title: aaaConfigure un nombre de dominio personalizado para el extremo de almacenamiento de blobs de Azure | Documentos de Microsoft
description: "Usar su propio punto de conexión de almacenamiento de Blob de nombre canónico (CNAME) toohello de hello toomap de portal de Azure en una cuenta de almacenamiento de Azure."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: aaafd8c5-eacb-49dc-8c8b-3f7011ad5e92
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: marsma
ms.openlocfilehash: 6cca6a6e1dbb69e7078df7ed11b04e8b921ec2f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-custom-domain-name-for-your-blob-storage-endpoint"></a>Configurar un nombre de dominio personalizado para el punto de conexión de Almacenamiento de blobs

Puede configurar un dominio personalizado para obtener acceso a los datos Blob en la cuenta de almacenamiento de Azure. Hola extremo predeterminado para el almacenamiento de blobs es `<storage-account-name>.blob.core.windows.net`. Si asigna un dominio y subdominio personalizados como **www.contoso.com** toohello el extremo de blob para la cuenta de almacenamiento, los usuarios pueden, a continuación, obtener acceso a datos en la cuenta de almacenamiento que utiliza ese dominio de blobs.

> [!IMPORTANT]
> Azure Storage no admite aún HTTPS con dominios personalizados de forma nativa. Actualmente se puede [utilizar blobs de tooaccess de Azure CDN Hola con dominios personalizados a través de HTTPS](./storage-https-custom-domain-cdn.md).
>

Hello tabla siguiente muestran algunas direcciones URL de ejemplo para los datos de blob que se encuentra en una cuenta de almacenamiento denominada **mystorageaccount**. dominio personalizado de Hello registrado para la cuenta de almacenamiento de hello es **www.contoso.com**:

| Tipo de recurso | Dirección URL predeterminada | URL de dominio personalizado |
| --- | --- | --- |
| Cuenta de almacenamiento | http://mystorageaccount.blob.core.windows.net | http://www.contoso.com |
| Blob |http://mystorageaccount.blob.core.windows.net/mycontainer/myblob | http://www.contoso.com/mycontainer/myblob |
| Contenedor raíz | http://mystorageaccount.blob.core.windows.net/myblob o http://mystorageaccount.blob.core.windows.net/$root/myblob| http://www.contoso.com/myblob o http://www.contoso.com/$root/myblob |

## <a name="direct-vs-intermediary-domain-mapping"></a>Asignación de dominios directa frente a intermedia

Hay dos toopoint formas el extremo de blob de toohello de dominio personalizado para su cuenta de almacenamiento: dirigir CNAME asignación y uso de hello *asverify* subdominio intermedio.

### <a name="direct-cname-mapping"></a>Asignación directa de CNAME

Hola primera y más simple, el método es toocreate un registro de nombre canónico (CNAME) que se asigna el dominio y subdominio personalizados directamente toohello blob punto de conexión. Un registro CNAME es una característica de sistema (de dominio DNS) del nombre de dominio que se asigna a un dominio de destino de tooa de dominio de origen. En este caso, dominio de origen de hello es su propio dominio y subdominio personalizados, por ejemplo *www.contoso.com*. dominio de destino de hello es su extremo de servicio Blob, por ejemplo  *mystorageaccount.BLOB.Core.Windows.NET*.

método directo Hola se trata en [registrar un dominio personalizado](#register-a-custom-domain).

### <a name="intermediary-mapping-with-asverify"></a>Asignación intermedia con *asverify*

Hola segundo método también utiliza los registros CNAME, pero primero emplea un subdominio especial reconocido por el tiempo de inactividad de Azure tooavoid: **asverify**.

proceso de Hola de asignar el extremo de blob de tooa de dominio personalizado puede dar lugar a un breve período de inactividad en el dominio de hello mientras está registrando en hello [portal de Azure](https://portal.azure.com). Si el dominio personalizado atiende actualmente una aplicación con un contrato de nivel de servicio (SLA) que requiere sin tiempo de inactividad, puede usar hello Azure *asverify* subdominio como un paso de registro intermedio. Este paso intermedio garantiza a los usuarios están tooaccess capaz de su dominio mientras tiene lugar la asignación de DNS de Hola.

método intermediario Hola se trata en [registrar un dominio personalizado con hello *asverify* subdominio](#register-a-custom-domain-using-the-asverify-subdomain).

## <a name="register-a-custom-domain"></a>Registro de un dominio personalizado
Utilice este procedimiento tooregister su dominio personalizado si no tienes preocupaciones acerca de la que se va a tooyour brevemente disponible a los usuarios de dominio de hello, o si el dominio personalizado no hospeda actualmente una aplicación.

Si su dominio personalizado es compatible actualmente con una aplicación que no puede tener ningún tiempo de inactividad, siga el procedimiento Hola descrito en [registrar un dominio personalizado con hello *asverify* subdominio](#register-a-custom-domain-using-the-asverify-subdomain).

tooconfigure un nombre de dominio personalizado, debe crear un nuevo registro CNAME en DNS. Hola registro CNAME especifica un alias para un nombre de dominio. En este caso, se asigna la dirección de Hola del extremo de almacenamiento de blobs de toohello de dominio personalizado para su cuenta de almacenamiento.

Por lo general, puede administrar la configuración de DNS de su dominio en el sitio web del registrador de su dominio. Cada registrador tiene un método similar pero ligeramente distinto para especificar un registro CNAME, pero el concepto de hello es Hola igual. Algunos paquetes de registro de dominio básico no ofrecen configuración de DNS, por lo que puede que necesite tooupgrade el paquete de registro de dominio para poder crear registro CNAME Hola.

1. Navegar por la cuenta de almacenamiento de tooyour en hello [portal de Azure](https://portal.azure.com).
1. En **servicio BLOB** en la hoja de menú de hello, seleccione **dominio personalizado** tooopen hello *dominio personalizado* hoja.
1. Inicie sesión en el sitio Web del registrador de dominios tooyour e ir a página toohello para la administración de DNS. Podría encontrarlo en una sección como **Nombre de dominio**, **DNS** o **Administración del servidor de nombres**.
1. Busque la sección de Hola para administrar registros CNAME. Puede tener una página de configuración avanzada de toogo tooan y buscar palabras hello **CNAME**, **Alias**, o **subdominios**.
1. Cree un nuevo registro CNAME y proporcione un alias de subdominio como **www** o **fotos**. A continuación, proporcione un nombre de host, que es el extremo del servicio Blob, en formato de hello **mystorageaccount.blob.core.windows.net** (donde *mystorageaccount* es Hola nombre de la cuenta de almacenamiento). toouse de nombre de host de Hello aparece en elemento #1 de hello *dominio personalizado* hoja en hello [portal de Azure](https://portal.azure.com).
1. En el cuadro de texto hello en hello *dominio personalizado* hoja en hello [portal de Azure](https://portal.azure.com), escriba Hola nombre de su dominio personalizado, incluido el subdominio Hola. Por ejemplo, si su dominio es **contoso.com** y su alias de subdominio es **www**, escriba **www.contoso.com**. Si el subdominio es **fotos**, escriba **photos.contoso.com**. Hola subdominio es *requiere*.
1. Seleccione **guardar** en hello *dominio personalizado* hoja tooregister su dominio personalizado. Si el registro de hello es correcta, verá una notificación de portal que su cuenta de almacenamiento se actualizó correctamente.

Una vez que el nuevo registro CNAME se propaga a través de DNS, los usuarios pueden ver los datos de blob mediante su dominio personalizado, siempre y cuando tienen los permisos adecuados de Hola.

## <a name="register-a-custom-domain-using-hello-asverify-subdomain"></a>Registrar un dominio personalizado con hello *asverify* subdominio
Utilice este procedimiento tooregister su dominio personalizado si el dominio personalizado atiende actualmente una aplicación con un SLA que requiere que no exista ningún tiempo de inactividad. Mediante la creación de un CNAME que apunte de `asverify.<subdomain>.<customdomain>` demasiado`asverify.<storageaccount>.blob.core.windows.net`, puede registrar previamente el dominio con Azure. A continuación, puede crear un segundo CNAME que apunte de `<subdomain>.<customdomain>` demasiado`<storageaccount>.blob.core.windows.net`, en qué momento dominio personalizado de tráfico tooyour será dirigido tooyour extremo del blob.

Hola **asverify** subdominio es un subdominio especial reconocido por Azure. Anteponiendo `asverify` tooyour propio subdominio, permite toorecognize Azure su dominio personalizado sin modificar el registro DNS de hello para el dominio de Hola. Cuando se modifica el registro DNS de hello para el dominio de hello, será extremo del blob toohello asignadas sin tiempo de inactividad.

1. Navegar por la cuenta de almacenamiento de tooyour en hello [portal de Azure](https://portal.azure.com).
1. En **servicio BLOB** en la hoja de menú de hello, seleccione **dominio personalizado** tooopen hello *dominio personalizado* hoja.
1. Inicie sesión en el sitio Web del proveedor DNS de tooyour e ir a página toohello para la administración de DNS. Podría encontrarlo en una sección como **Nombre de dominio**, **DNS** o **Administración del servidor de nombres**.
1. Busque la sección de Hola para administrar registros CNAME. Puede tener una página de configuración avanzada de toogo tooan y buscar palabras hello **CNAME**, **Alias**, o **subdominios**.
1. Crear un nuevo registro CNAME y proporcionar un alias de subdominio que incluya hello *asverify* subdominio. Por ejemplo, **asverify.www** o **asverify.fotos**. A continuación, proporcione un nombre de host, que es el extremo del servicio Blob, en formato de hello **asverify.mystorageaccount.blob.core.windows.net** (donde **mystorageaccount** es Hola nombre de la cuenta de almacenamiento). toouse de nombre de host de Hello aparece en el elemento #2 de hello *dominio personalizado* hoja en hello [portal de Azure](https://portal.azure.com).
1. En el cuadro de texto hello en hello *dominio personalizado* hoja en hello [portal de Azure](https://portal.azure.com), escriba Hola nombre de su dominio personalizado, incluido el subdominio Hola. No incluya *asverify*. Por ejemplo, si su dominio es **contoso.com** y su alias de subdominio es **www**, escriba **www.contoso.com**. Si el subdominio es **fotos**, escriba **photos.contoso.com**. subdominio hello es necesario.
1. Seleccione hello **usar validación CNAME indirecta** casilla de verificación.
1. Seleccione **guardar** en hello *dominio personalizado* hoja tooregister su dominio personalizado. Si el registro de hello es correcta, verá una notificación portal para indicar que la cuenta de almacenamiento se actualizó correctamente. En este momento, Azure, se ha comprobado su dominio personalizado pero tráfico tooyour dominio no es aún se están enrutando tooyour cuenta de almacenamiento.
1. Devolver tooyour DNS del sitio Web del proveedor y crear otro registro CNAME que asigna el punto de conexión de servicio de subdominio tooyour Blob. Por ejemplo, especificar subdominio hello como **www** o **fotos** (sin hello *asverify*), y el nombre de host de Hola  **mystorageaccount.BLOB.Core.Windows.NET** (donde **mystorageaccount** es Hola nombre de la cuenta de almacenamiento). Con este paso, el registro de hello de su dominio personalizado está completando.
1. Por último, puede eliminar el registro CNAME de hello creaste Hola contenedor **asverify** subdominio, tal y como ocurría solo como un paso intermedio.

Una vez que el nuevo registro CNAME se propaga a través de DNS, los usuarios pueden ver los datos de blob mediante su dominio personalizado, siempre y cuando tienen los permisos adecuados de Hola.

## <a name="test-your-custom-domain"></a>Prueba de un dominio personalizado

tooconfirm que el dominio personalizado está realmente asignada tooyour extremo del servicio Blob, crear un blob en un contenedor público dentro de su cuenta de almacenamiento. A continuación, en un explorador web, utilice un URI con hello siguiendo el formato blob de Hola tooaccess:

`http://<subdomain.customdomain>/<mycontainer>/<myblob>`

Por ejemplo, podría usar Hola después URI tooaccess un formulario web Forms en hello **myforms** contenedor Hola **photos.contoso.com** subdominio personalizado:

`http://photos.contoso.com/myforms/applicationform.htm`

## <a name="deregister-a-custom-domain"></a>Anulación del registro de un dominio personalizado

tooderegister un dominio personalizado para el extremo de almacenamiento Blob, utilice uno de hello procedimientos siguientes.

### <a name="azure-portal"></a>Azure Portal

Realice los siguientes pasos de hello en configuración de dominio personalizado de Hola de hello tooremove de portal de Azure:

1. Navegar por la cuenta de almacenamiento de tooyour en hello [portal de Azure](https://portal.azure.com).
1. En **servicio BLOB** en la hoja de menú de hello, seleccione **dominio personalizado** tooopen hello *dominio personalizado* hoja.
1. Contenido de borrar Hola Hola del cuadro de texto que contiene el nombre de dominio personalizado.
1. Seleccione hello **guardar** botón.

Cuando se ha quitado correctamente el dominio personalizado de hello, verá una notificación portal para indicar que la cuenta de almacenamiento se actualizó correctamente.

### <a name="azure-cli-20"></a>CLI de Azure 2.0

Hola de uso [actualización la cuenta de almacenamiento az](https://docs.microsoft.com/cli/azure/storage/account#update) CLI comando y especifique una cadena vacía (`""`) para hello `--custom-domain` argumento valor tooremove un registro de dominio personalizado.

* Formato de comando:

  ```azurecli
  az storage account update \
      --name <storage-account-name> \
      --resource-group <resource-group-name> \
      --custom-domain ""
  ```

* Ejemplo de comando:

  ```azurecli
  az storage account update \
      --name mystorageaccount \
      --resource-group myresourcegroup \
      --custom-domain ""
  ```

### <a name="powershell"></a>PowerShell

Hola de uso [conjunto AzureRmStorageAccount](/powershell/module/azurerm.storage/set-azurermstorageaccount) cmdlet de PowerShell y especifique una cadena vacía (`""`) para hello `-CustomDomainName` argumento valor tooremove un registro de dominio personalizado.

* Formato de comando:

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "<resource-group-name>" `
      -AccountName "<storage-account-name>" `
      -CustomDomainName ""
  ```

* Ejemplo de comando:

  ```powershell
  Set-AzureRmStorageAccount `
      -ResourceGroupName "myresourcegroup" `
      -AccountName "mystorageaccount" `
      -CustomDomainName ""
  ```

## <a name="next-steps"></a>Pasos siguientes
* [Asignar un punto de conexión de red de entrega contenido (CDN) de Azure de tooan de dominio personalizado](../cdn/cdn-map-content-to-custom-domain.md)
* [Uso de blobs de tooaccess de Azure CDN Hola con dominios personalizados a través de HTTPS](./storage-https-custom-domain-cdn.md)
