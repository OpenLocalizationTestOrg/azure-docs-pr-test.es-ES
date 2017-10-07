---
title: "tooget de API de REST de hello aaaUse a trabajar con el almacén de Data Lake | Documentos de Microsoft"
description: "Use las API de REST de WebHDFS tooperform operaciones en el almacén de Data Lake"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57ac6501-cb71-4f75-82c2-acc07c562889
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: 62fce8293dfee730a61f2a3d37fc138ce7c3afdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a>Introducción al Almacén de Azure Data Lake mediante las API de REST
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [.NET SDK](data-lake-store-get-started-net-sdk.md)
> * [SDK de Java](data-lake-store-get-started-java-sdk.md)
> * [API de REST](data-lake-store-get-started-rest-api.md)
> * [CLI de Azure 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

En este artículo, aprenderá cómo toouse WebHDFS API de REST API de REST de almacén de datos Lake tooperform de cuentas y administración, así como las operaciones de sistema de archivos en el almacén de Azure Data Lake. El Almacén de Azure Data Lake expone sus propias API de REST para operaciones de administración de cuentas. Sin embargo, como el Almacén de Data Lake es compatible con el ecosistema de HDFS y Hadoop, admite el uso de las API de REST de WebHDFS para las operaciones del sistema de archivos.

> [!NOTE]
> Para obtener información detallada sobre la compatibilidad con API de REST de hello para el almacén de Data Lake, consulte [referencia de API de REST de almacén de Azure datos Lake](https://msdn.microsoft.com/library/mt693424.aspx).
> 
> 

## <a name="prerequisites"></a>Requisitos previos
* **Una suscripción de Azure**. Vea [Obtener evaluación gratuita de Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Cree una aplicación de Azure Active Directory**. Usar la aplicación de almacén de Data Lake de hello Azure AD aplicación tooauthenticate Hola con Azure AD. Hay diferentes enfoques tooauthenticate con Azure AD, que son **autenticación de usuario final** o **autenticación del servicio a servicio**. Para obtener instrucciones y obtener más información acerca de cómo tooauthenticate, consulte [autenticación de usuario final](data-lake-store-end-user-authenticate-using-active-directory.md) o [autenticación del servicio a servicio](data-lake-store-authenticate-using-active-directory.md).
* [cURL](http://curl.haxx.se/). En este artículo usa toodemonstrate cURL cómo toomake API de REST se llama con una cuenta de almacén de Data Lake.

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>¿Cómo se puede autenticar mediante Azure Active Directory?
Puede utilizar dos tooauthenticate enfoques con Azure Active Directory.

### <a name="end-user-authentication-interactive"></a>Autenticación de usuario final (interactiva)
En este escenario, aplicación hello pide toolog de usuario de hello en y se realizan todas las operaciones de hello en contexto de saludo del usuario de Hola. Realizar Hola siguiendo los pasos para la autenticación interactiva.

1. A través de la aplicación, redirigir Hola usuario toohello después de la dirección URL:
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<URI de redireccionamiento > necesita toobe codificado para su uso en una dirección URL. Por lo tanto, para https://localhost, use `https%3A%2F%2Flocalhost`).
   > 
   > 
   
    A fin de Hola de este tutorial, puede reemplazar los valores de marcador de posición de hello en dirección URL de hello anteriormente y péguelo en la barra de direcciones del explorador de web. Será redirigido tooauthenticate mediante el inicio de sesión de Azure. Una vez que ha iniciado sesión correctamente, respuesta de Hola se muestra en la barra de direcciones del explorador de Hola. respuesta de Hello será Hola siguiendo el formato siguiente:
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. Capturar el código de autorización de Hola de respuesta de Hola. Para este tutorial, puede copiar el código de autorización de Hola de barra de direcciones de hello del explorador web de Hola y páselo en hello POST solicitud toohello extremo de token, tal y como se muestra a continuación:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > En este caso, Hola \<REDIRECT-URI > no deben codificarse.
   > 
   > 
3. respuesta de Hello es un objeto JSON que contiene un token de acceso (p. ej., `"access_token": "<ACCESS_TOKEN>"`) y un token de actualización (p. ej., `"refresh_token": "<REFRESH_TOKEN>"`). La aplicación usa Hola token de acceso al obtener acceso a almacén de Azure Data Lake y tooget de token de actualización de hello otro token de acceso cuando caduca un token de acceso.
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. Cuando expira el token de acceso de hello, puede solicitar un nuevo token de acceso con el token de actualización de hello, tal y como se muestra a continuación:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

Para más información sobre la autenticación interactiva de usuarios, consulte el [flujo de concesión de un código de autorización](https://msdn.microsoft.com/library/azure/dn645542.aspx).

### <a name="service-to-service-authentication-non-interactive"></a>Autenticación de servicio a servicio (no interactiva)
En este escenario, aplicación de Hola Hola proporciona sus propias credenciales operaciones de hello tooperform. Para ello, debe emitir una solicitud POST como Hola se muestra a continuación. 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

salida de Hello de esta solicitud incluirá un token de autorización (indicado por `access-token` en la siguiente salida de Hola) que se pasará posteriormente con las llamadas de API de REST. Guarde este token de autenticación en un archivo de texto; lo necesitará más adelante en este artículo.

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

En este artículo usa hello **no interactivo** enfoque. Para obtener más información sobre no interactivo (llamadas de servicio a servicio), consulte [llamadas de tooservice utilizando las credenciales del servicio](https://msdn.microsoft.com/library/azure/dn645543.aspx).

## <a name="create-a-data-lake-store-account"></a>Crear una cuenta de Almacén de Data Lake
Esta operación se basa en la llamada de API de REST de hello definido [aquí](https://msdn.microsoft.com/library/mt694078.aspx).

Usar hello siguiente comando cURL. Reemplace **\<yourstorename>** por el nombre de Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

Hola por encima del comando, reemplace \< `REDACTED` \> con token de autorización de hello recuperar versiones anteriores. carga de la solicitud de Hola para este comando se encuentra en hello **input.json** archivo que se proporciona para hello `-d` parámetro anterior. Hola contenido del archivo de input.json hello es similar siguiente hello:

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a>Crear carpetas en una cuenta de Almacén de Data Lake
Esta operación se basa en llamada de API de REST de WebHDFS Hola definido [aquí](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).

Usar hello siguiente comando cURL. Reemplace **\<yourstorename>** por el nombre de Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

Hola por encima del comando, reemplace \< `REDACTED` \> con token de autorización de hello recuperar versiones anteriores. Este comando crea un directorio llamado **mytempdir** en la carpeta de raíz de Hola de su cuenta de almacén de Data Lake.

Debería ver una respuesta similar al siguiente si Hola operación se completa correctamente:

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a>Mostrar carpetas en una cuenta de Almacén de Data Lake
Esta operación se basa en llamada de API de REST de WebHDFS Hola definido [aquí](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).

Usar hello siguiente comando cURL. Reemplace **\<yourstorename>** por el nombre de Data Lake Store.

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

Hola por encima del comando, reemplace \< `REDACTED` \> con token de autorización de hello recuperar versiones anteriores.

Debería ver una respuesta similar al siguiente si Hola operación se completa correctamente:

    {
    "FileStatuses": {
        "FileStatus": [{
            "length": 0,
            "pathSuffix": "mytempdir",
            "type": "DIRECTORY",
            "blockSize": 268435456,
            "accessTime": 1458324719512,
            "modificationTime": 1458324719512,
            "replication": 0,
            "permission": "777",
            "owner": "NotSupportYet",
            "group": "NotSupportYet"
        }]
    }
    }

## <a name="upload-data-into-a-data-lake-store-account"></a>Cargar datos en una cuenta del Almacén de Data Lake
Esta operación se basa en llamada de API de REST de WebHDFS Hola definido [aquí](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).

Usar hello siguiente comando cURL. Reemplace **\<yourstorename>** por el nombre de Data Lake Store.

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

Hola por encima de la sintaxis **-T** parámetro es Hola ubicación del archivo de Hola que se va a cargar.

salida de Hello es siguiente de toohello similar:
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a>Leer datos de una cuenta del Almacén de Data Lake
Esta operación se basa en llamada de API de REST de WebHDFS Hola definido [aquí](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).

La lectura de datos desde una cuenta del Almacén de Data Lake es un proceso de dos pasos.

* En primer lugar enviar una solicitud GET en el punto de conexión de hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`. Esto devolverá una ubicación toosubmit Hola siguiente GET solicitud.
* A continuación, enviar solicitud de obtención de hello en el punto de conexión de hello `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`. Esto mostrará el contenido de hello del archivo hello.

Sin embargo, porque no hay ninguna diferencia en Hola parámetros de entrada entre hello en primer lugar y hello segundo paso, puede usar hello `-L` primera solicitud de parámetro toosubmit Hola. `-L`opción básicamente combina dos solicitudes en uno y hará que cURL solicitud hello en la nueva ubicación de Hola de puesta al día. Por último, se muestra la salida de hello de todas las llamadas de solicitud de hello, como se muestra a continuación. Reemplace **\<yourstorename>** por el nombre de Data Lake Store.

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

Debería ver un siguiente toohello similar de salida:

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a>Cambiar el nombre de un archivo en una cuenta del Almacén de Data Lake
Esta operación se basa en llamada de API de REST de WebHDFS Hola definido [aquí](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).

Siguiente Hola de uso cURL toorename de comando en un archivo. Reemplace **\<yourstorename>** por el nombre de Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

Debería ver un siguiente toohello similar de salida:

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a>Eliminar un archivo de una cuenta del Almacén de Data Lake
Esta operación se basa en llamada de API de REST de WebHDFS Hola definido [aquí](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).

Siguiente Hola de uso cURL toodelete de comando en un archivo. Reemplace **\<yourstorename>** por el nombre de Data Lake Store.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

Debería ver una salida similar Hola siguiente:

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a>Eliminar una cuenta del Almacén de Data Lake
Esta operación se basa en la llamada de API de REST de hello definido [aquí](https://msdn.microsoft.com/library/mt694075.aspx).

Siguiente Hola de uso cURL comando toodelete una cuenta de almacén de Data Lake. Reemplace **\<yourstorename>** por el nombre de Data Lake Store.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

Debería ver una salida similar Hola siguiente:

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a>Otras referencias
* [Abrir aplicaciones Big Data de origen que funcionan con el Almacén de Azure Data Lake](data-lake-store-compatible-oss-other-applications.md)

