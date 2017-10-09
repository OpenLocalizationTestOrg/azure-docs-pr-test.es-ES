---
title: "aaaCreate identidad de aplicación de Azure con CLI de Azure | Documentos de Microsoft"
description: "Describe cómo controlan toouse CLI de Azure toocreate una aplicación de Azure Active Directory y entidad de servicio y lo acceso tooresources a través del acceso basado en roles. Muestra cómo tooauthenticate aplicación con una contraseña o un certificado."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 0d693ec801d4f4d6c24ec420580776e73014b325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-cli-toocreate-a-service-principal-tooaccess-resources"></a>Usar una entidad de seguridad tooaccess los recursos del servicio de toocreate de CLI de Azure

Cuando haya una aplicación o un script que necesita tooaccess recursos, puede configurar una identidad para la aplicación hello y autenticar la aplicación hello con sus propias credenciales. Esta identidad se conoce como una entidad de servicio. Este enfoque le permite:

* Asignar permisos de identidad de aplicación de toohello que son diferentes de sus propios permisos. Normalmente, estos permisos son tooexactly restringido qué aplicación hello necesita toodo.
* Usar un certificado para la autenticación al ejecutar un script desatendido.

Este artículo muestra cómo toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset seguridad un toorun de aplicación en sus propias credenciales y la identidad. Instalar la versión más reciente de Hola de [Azure CLI 1.0](../cli-install-nodejs.md) toomake que su entorno coincide con los ejemplos de hello en este artículo.

## <a name="required-permissions"></a>Permisos necesarios
toocomplete en este tema, debe tener permisos suficientes en Azure Active Directory y la suscripción de Azure. En concreto, debe ser capaz de toocreate una aplicación en Azure Active Directory hello y asignar Hola servicio principal tooa rol. 

Hola más fácil manera toocheck si su cuenta tiene los permisos adecuados es a través del portal de Hola. Consulte [Comprobación de los permisos necesarios en el portal](resource-group-create-service-principal-portal.md#required-permissions).

Ahora, continuar tooa sección para cada uno [contraseña](#create-service-principal-with-password) o [certificado](#create-service-principal-with-certificate) autenticación.

## <a name="create-service-principal-with-password"></a>Creación de entidad de servicio con contraseña
En esta sección, realice Hola pasos toocreate Hola aplicación de AD con una contraseña y asignar la entidad de servicio de toohello de rol de lector de Hola.

1. Inicie sesión en la cuenta de tooyour.
   
   ```azurecli
   azure login
   ```
2. toocreate una identidad de aplicación proporcionan Hola nombre de aplicación hello y una contraseña, como se muestra en el siguiente comando de hello:
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   se devuelve la nueva entidad de servicio Hola. Hola Id. de objeto es necesario al conceder permisos. guid de Hello aparece con hello nombres principales de servicio es necesario al iniciar sesión. Este guid es hello mismo valor que el identificador de la aplicación hello. En las aplicaciones de ejemplo de Hola, este valor es que se hace referencia tooas Hola `Client ID`. 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. Conceder permisos de entidad de seguridad de servicio de hello en su suscripción. En este ejemplo, agregar rol lector de hello servicio toohello principal, que concede permiso tooread todos los recursos de suscripción de Hola. Para obtener información sobre otros roles, consulte [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md). Para el parámetro objectid de hello, proporcionar Hola Id. de objeto que utilizó al crear la aplicación hello. Antes de ejecutar este comando, debe permitir un poco Hola nuevo servicio principal toopropagate a lo largo de Azure Active Directory. Si estos comandos se ejecutan manualmente, lo habitual es que haya transcurrido suficiente tiempo entre las tareas. En una secuencia de comandos, debe agregar una toosleep paso entre los comandos de hello (como `sleep 15`). Si ve que Hola de error que indica que principal no existe en el directorio de hello, vuelva a ejecutar el comando Hola.
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
Eso es todo. La aplicación de AD y la entidad de servicio ya están configuradas. sección de Hello siguiente muestra cómo toolog con hello de credenciales a través de la CLI de Azure. Si desea toouse credencial de hello en la aplicación de código, no es necesario toocontinue con este tema. También puede avanzar toohello [aplicaciones de ejemplo](#sample-applications) para obtener ejemplos de inicio de sesión con el identificador de la aplicación y la contraseña. 

### <a name="provide-credentials-through-azure-cli"></a>Proporcionar credenciales a través de la CLI de Azure
Ahora, debe toolog en como operaciones de tooperform aplicación Hola.

1. Siempre que inicie sesión como una entidad de servicio, necesita Id. de inquilino de hello tooprovide del directorio de hello para la aplicación de AD. Un inquilino es una instancia de Azure Active Directory. tooretrieve Hola Id. de inquilino de su suscripción autenticado actualmente, use:
   
   ```azurecli
   azure account show
   ```
   
   Que devuelve:
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     Si necesita Id. de inquilino de hello tooget de otra suscripción, utilice Hola siguiente comando:
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. Si necesita toouse de Id. de cliente de tooretrieve hello para iniciar sesión, use:
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     Hola toouse de valor para el registro es guid Hola aparecen en los nombres principales de servicio de Hola.
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. Inicie sesión como entidad de servicio de Hola.
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    Le solicitará contraseña de Hola. Proporcione la contraseña de Hola que especificó al crear la aplicación hello AD.
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

Ahora está autenticado como entidad de seguridad de servicio de Hola Hola principal de servicio que ha creado.

Como alternativa, puede invocar operaciones de REST de toolog de línea de comandos de hello en. De respuesta de autenticación de hello, puede recuperar el token de acceso de Hola para su uso con otras operaciones. Para obtener un ejemplo de recuperación de token de acceso de hello mediante la invocación de operaciones REST, consulte [generar un Token de acceso](resource-manager-rest-api.md#generating-an-access-token).

## <a name="create-service-principal-with-certificate"></a>Creación de entidad de servicio con certificado
En esta sección, realice los pasos de hello para:

* Creación de un certificado autofirmado.
* crear Hola aplicación AD con certificado de Hola y entidad de servicio de Hola
* asignar la entidad de servicio de toohello de rol de lector de Hola

toocomplete estos pasos, debe tener [OpenSSL](http://www.openssl.org/) instalado.

1. Creación de un certificado autofirmado.
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. Hola anterior paso crea dos archivos: privkey.pem y cert.pem. Combinar las claves públicas y privadas de hello en un único archivo.

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. Abra hello **examplecert.pem** de archivos y busque secuencia larga de Hola de caracteres entre **---BEGIN CERTIFICATE---** y **---END CERTIFICATE---**. Copiar datos del certificado Hola. Estos datos se pasan como un parámetro al crear Hola entidad de servicio.

4. Inicie sesión en la cuenta de tooyour.

   ```azurecli
   azure login
   ```
5. entidad de servicio de toocreate hello, proporcione el nombre de Hola de aplicación hello y datos de certificados de hello, tal y como se muestra en el siguiente comando de hello:
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   se devuelve la nueva entidad de servicio Hola. Hola Id. de objeto es necesario al conceder permisos. guid de Hello aparece con hello nombres principales de servicio es necesario al iniciar sesión. Este guid es hello mismo valor que el identificador de la aplicación hello. En las aplicaciones de ejemplo de Hola, este valor es que se hace referencia tooas Hola identificador de cliente. 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. Conceder permisos de entidad de seguridad de servicio de hello en su suscripción. En este ejemplo, agregar rol lector de hello servicio toohello principal, que concede permiso tooread todos los recursos de suscripción de Hola. Para obtener información sobre otros roles, consulte [RBAC: Roles integrados](../active-directory/role-based-access-built-in-roles.md). Para el parámetro objectid de hello, proporcionar Hola Id. de objeto que utilizó al crear la aplicación hello. Antes de ejecutar este comando, debe permitir un poco Hola nuevo servicio principal toopropagate a lo largo de Azure Active Directory. Si estos comandos se ejecutan manualmente, lo habitual es que haya transcurrido suficiente tiempo entre las tareas. En una secuencia de comandos, debe agregar una toosleep paso entre los comandos de hello (como `sleep 15`). Si ve que Hola de error que indica que principal no existe en el directorio de hello, vuelva a ejecutar el comando Hola.
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a>Proporcionar un certificado a través de un script automatizado de la CLI de Azure
Ahora, debe toolog en como operaciones de tooperform aplicación Hola.

1. Siempre que inicie sesión como una entidad de servicio, necesita Id. de inquilino de hello tooprovide del directorio de hello para la aplicación de AD. Un inquilino es una instancia de Azure Active Directory. tooretrieve Hola Id. de inquilino de su suscripción autenticado actualmente, use:
   
   ```azurecli
   azure account show
   ```
   
   Que devuelve:
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   Si necesita Id. de inquilino de hello tooget de otra suscripción, utilice Hola siguiente comando:
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. tooretrieve Hola huella digital del certificado y quite los caracteres que no necesite, use:
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   De este modo, se devuelve un valor de huella digital similar al siguiente:
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. Si necesita toouse de Id. de cliente de tooretrieve hello para iniciar sesión, use:
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   Hola toouse de valor para el registro es guid Hola aparecen en los nombres principales de servicio de Hola.
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. Inicie sesión como entidad de servicio de Hola.
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

Ahora está autenticado como entidad de servicio Hola para hello aplicación de Azure Active Directory que creó.

## <a name="change-credentials"></a>Cambio de credenciales

toochange Hola credenciales para una aplicación de AD, ya sea debido a un riesgo de seguridad o una expiración de la credencial, use `azure ad app set`.

toochange una contraseña, use:

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

toochange un valor de certificado, use:

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a>Depurar

Puede encontrar Hola siguientes errores al crear a una entidad de servicio:

* **"Authentication_Unauthorized"** o **"ninguna suscripción encontrado en el contexto de Hola".** -Ve este error cuando la cuenta no tiene hello [los permisos necesarios](#required-permissions) en hello Azure Active Directory tooregister una aplicación. Por lo general, este error aparece cuando los usuarios administradores de Azure Active Directory son los únicos que pueden registrar las aplicaciones y la cuenta no es de un administrador. Pida a su administrador tooeither asignar rol Administrador tooan o tooenable usuarios tooregister aplicaciones.

* Su cuenta **"no tiene autorización tooperform acción 'Microsoft.Authorization/roleAssignments/write' sobre el ámbito '/ subscriptions / {guid}'."**  -Verá este error cuando su cuenta no tiene suficiente tooassign permisos una identidad de tooan de rol. Pida el tooadd de administrador de suscripción rol Administrador de acceso tooUser.

## <a name="sample-applications"></a>Aplicaciones de ejemplo
Para obtener información sobre cómo iniciar sesión como aplicación Hola a través de distintas plataformas, vea:

* [.NET](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [Java](/java/azure/java-sdk-azure-authenticate)
* [Node.js](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [Python](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [Ruby](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a>Pasos siguientes
* Para obtener instrucciones detalladas sobre cómo integrar una aplicación en Azure para administrar recursos, vea [tooauthorization de guía del desarrollador con hello API de Azure Resource Manager](resource-manager-api-authentication.md).
* tooget obtener más información sobre el uso de certificados y la CLI de Azure, vea [autenticación basada en certificados con entidades de seguridad de servicio de Azure desde la línea de comandos de Linux](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx). 
* Para obtener una lista de las acciones disponibles que puede otorgar o denegar toousers, consulte [las operaciones de proveedor de recursos del Administrador de recursos de Azure](../active-directory/role-based-access-control-resource-provider-operations.md).
