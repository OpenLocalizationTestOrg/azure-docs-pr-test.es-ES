---
title: "aaaConfigure una cadena de conexión para el almacenamiento de Azure | Documentos de Microsoft"
description: "Configure una cadena de conexión para una cuenta de Azure Storage. Una cadena de conexión contiene información de hello necesarios tooauthenticate tener acceso a cuenta de almacenamiento de tooa desde la aplicación en tiempo de ejecución."
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: ecb0acb5-90a9-4eb2-93e6-e9860eda5e53
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: marsma
ms.openlocfilehash: 80c38a6f8f0d4f06b99e7c487647b984e01d1772
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-storage-connection-strings"></a>Configuración de las cadenas de conexión de Azure Storage

Una cadena de conexión incluye información de autenticación de hello necesaria para los datos de tooaccess de aplicación de una cuenta de almacenamiento de Azure en tiempo de ejecución. Las cadenas de conexión se pueden configurar para:

* Conectar toohello emulador de almacenamiento de Azure.
* Acceder a la cuenta de Azure Storage.
* Acceder a recursos especificados en Azure a través de una firma de acceso compartido (SAS).

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

## <a name="storing-your-connection-string"></a>Almacenamiento de la cadena de conexión
La aplicación necesita la cadena de conexión de hello tooaccess en tiempo de ejecución tooauthenticate las solicitudes realizadas tooAzure almacenamiento. Tiene varias opciones para almacenar una cadena de conexión:

* Una aplicación en ejecución en el escritorio de Hola o en un dispositivo puede almacenar la cadena de conexión de hello en un **app.config** o **web.config** archivo. Agregar toohello de cadena de conexión de hello **AppSettings** sección en estos archivos.
* Una aplicación que se ejecuta en un servicio de nube de Azure puede almacenar la cadena de conexión de Hola Hola [archivo de esquema (.cscfg) de configuración de servicio de Azure](https://msdn.microsoft.com/library/ee758710.aspx). Agregar toohello de cadena de conexión de hello **ConfigurationSettings** sección del archivo de configuración de servicio de Hola.
* La cadena de conexión se puede usar directamente en el código. Sin embargo, es aconsejable que en la mayoría de los escenarios se recomienda almacenar la cadena de configuración en un archivo de configuración.

Almacenamiento de la cadena de conexión en un archivo de configuración hace que tooswitch de cadena de conexión tooupdate fácil Hola entre el emulador de almacenamiento de hello y una cuenta de almacenamiento de Azure en la nube de Hola. Entorno de destino tooyour toopoint de cadena de la conexión de Hola de tooedit bastará.

Puede usar hello [Administrador de configuración de Microsoft Azure](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/) tooaccess la cadena de conexión en tiempo de ejecución, independientemente de donde se está ejecutando la aplicación.

## <a name="create-a-connection-string-for-hello-storage-emulator"></a>Crear una cadena de conexión para el emulador de almacenamiento de Hola
[!INCLUDE [storage-emulator-connection-string-include](../../includes/storage-emulator-connection-string-include.md)]

Para obtener más información acerca del emulador de almacenamiento de hello, consulte [usar el emulador de almacenamiento de Azure de Hola para desarrollo y pruebas](storage-use-emulator.md).

## <a name="create-a-connection-string-for-an-azure-storage-account"></a>Creación de una cadena de conexión para una cuenta de Azure Storage
toocreate una cadena de conexión para la cuenta de almacenamiento de Azure, dar formato a siguiente Hola de uso. Indicar si desea que tooconnect toohello cuenta de almacenamiento a través de HTTPS (recomendado) o HTTP, reemplace `myAccountName` con el nombre de hello de la cuenta de almacenamiento y reemplace `myAccountKey` con su clave de acceso de cuenta:

`DefaultEndpointsProtocol=[http|https];AccountName=myAccountName;AccountKey=myAccountKey`

Por ejemplo, la cadena de conexión podría ser similar a la siguiente:

`DefaultEndpointsProtocol=https;AccountName=storagesample;AccountKey=<account-key>`

Aunque Azure Storage admite HTTP y HTTPS en una cadena de conexión, *se recomienda encarecidamente utilizar HTTPS*.

> [!TIP]
> Puede encontrar cadenas de conexión de la cuenta de almacenamiento en hello [portal de Azure](https://portal.azure.com). Navegue demasiado**configuración** > **las claves de acceso** en cadenas de conexión de la cuenta de almacenamiento menú hoja toosee para las claves de acceso principal y secundaria.
>

## <a name="create-a-connection-string-using-a-shared-access-signature"></a>Creación de una cadena de conexión con una firma de acceso compartido
[!INCLUDE [storage-use-sas-in-connection-string-include](../../includes/storage-use-sas-in-connection-string-include.md)]

## <a name="create-a-connection-string-for-an-explicit-storage-endpoint"></a>Creación de una cadena de conexión para un punto de conexión de Storage explícito
Puede especificar los extremos de servicio explícito en la cadena de conexión en lugar de usar puntos de conexión de hello predeterminados. toocreate una cadena de conexión que especifica un extremo explícito, especificar extremo de servicio completo de Hola para cada servicio, incluida la especificación del protocolo de hello (HTTPS (recomendado) o HTTP), en hello siguiendo el formato:

```
DefaultEndpointsProtocol=[http|https];
BlobEndpoint=myBlobEndpoint;
FileEndpoint=myFileEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
AccountName=myAccountName;
AccountKey=myAccountKey
```

Un escenario donde puedes toospecify un extremo explícito es cuando se ha asignado su tooa de punto de conexión de almacenamiento de blobs [dominio personalizado](storage-custom-domain-name.md). En ese caso, puede especificar un punto de conexión personalizado para Blob Storage en la cadena de conexión. También puede especificar extremos predeterminados de Hola para hello otros servicios si la aplicación usa.

Este es un ejemplo de una cadena de conexión que especifica un extremo explícito para hello servicio Blob:

```
# Blob endpoint only
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
AccountName=storagesample;
AccountKey=<account-key>
```

Este ejemplo especifica los extremos explícitos para todos los servicios, incluido un dominio personalizado para hello servicio Blob:

```
# All service endpoints
DefaultEndpointsProtocol=https;
BlobEndpoint=http://www.mydomain.com;
FileEndpoint=https://myaccount.file.core.windows.net;
QueueEndpoint=https://myaccount.queue.core.windows.net;
TableEndpoint=https://myaccount.table.core.windows.net;
AccountName=storagesample;
AccountKey=<account-key>
```

valores de punto de conexión de Hello en una cadena de conexión son solicitudes de Hola de tooconstruct usa servicios de almacenamiento de información de URI toohello y dictan el formato de Hola de los URI que se devolvió el código de tooyour.

Si ha asignado un dominio personalizado de almacenamiento extremo tooa y omite ese punto de conexión de una cadena de conexión, no será capaz de toouse esa conexión cadena tooaccess datos en dicho servicio desde el código.

> [!IMPORTANT]
> Los valores del punto de conexión de servicio de las cadenas de conexión deben ser identificadores URI con el formato correcto, entre los que se incluyen `https://` (recomendado) o `http://`. Dado que el almacenamiento de Azure todavía no admite HTTPS para dominios personalizados, *debe* especificar `http://` para cualquier extremo URI que señala tooa de dominio personalizado.
>

### <a name="create-a-connection-string-with-an-endpoint-suffix"></a>Creación de una cadena de conexión con el sufijo de un punto de conexión
toocreate una cadena de conexión para un servicio de almacenamiento en regiones o instancias sin el sufijo de punto de conexión diferente, como para China de Azure o Azure Government, Hola uso siguiendo el formato de cadena de conexión. Indicar si desea que tooconnect toohello cuenta de almacenamiento a través de HTTPS (recomendado) o HTTP, reemplace `myAccountName` con el nombre de saludo de la cuenta de almacenamiento, reemplace `myAccountKey` con su clave de acceso de cuenta y reemplace `mySuffix` con hello URI sufijo:

```
DefaultEndpointsProtocol=[http|https];
AccountName=myAccountName;
AccountKey=myAccountKey;
EndpointSuffix=mySuffix;
```

Este es un ejemplo de cadena de conexión para los servicios de Storage en Azure China:

```
DefaultEndpointsProtocol=https;
AccountName=storagesample;
AccountKey=<account-key>;
EndpointSuffix=core.chinacloudapi.cn;
```

## <a name="parsing-a-connection-string"></a>Análisis de una cadena de conexión
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="next-steps"></a>Pasos siguientes
* [Usar el emulador de almacenamiento de Azure de Hola para desarrollo y pruebas](storage-use-emulator.md)
* [Exploradores de Azure Storage](storage-explorers.md)
* [Uso de Firmas de acceso compartido (SAS)](storage-dotnet-shared-access-signature-part-1.md)

