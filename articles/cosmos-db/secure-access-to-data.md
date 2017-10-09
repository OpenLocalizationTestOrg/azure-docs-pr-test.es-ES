---
title: "aaaLearn cómo toosecure tener acceso a toodata en la base de datos de Azure Cosmos | Documentos de Microsoft"
description: "Obtenga información sobre los conceptos de control de acceso en Azure Cosmos DB, incluidas las claves maestras, las claves de solo lectura, los usuarios y los permisos."
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 8641225d-e839-4ba6-a6fd-d6314ae3a51c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: mimig
ms.openlocfilehash: fef7f8e14b488f6ceab0f2aa279a1e99d4416f08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-cosmos-db-data"></a>Proteger los datos de base de datos de Cosmos tooAzure de acceso
Este artículo proporciona información general de protección de toodata de acceso almacenada en [base de datos de Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).

Base de datos de Azure Cosmos usa dos tipos de claves tooauthenticate usuarios y proporcionan acceso a los datos tooits y recursos. 

|Tipo de clave|Recursos|
|---|---|
|[Claves maestras](#master-keys) |Se utilizan para los recursos administrativos: cuentas de base de datos, bases de datos, usuarios y permisos|
|[Tokens de recursos](#resource-tokens)|Se usan para recursos de aplicaciones: colecciones, documentos, datos adjuntos, procedimientos almacenados, desencadenadores y UDF|

<a id="master-keys"></a>

## <a name="master-keys"></a>Claves maestras 

Claves maestras de proporcionar acceso toohello todos los recursos administrativos de hello para la cuenta de base de datos de Hola. Claves maestras:  
- Proporcionar acceso tooaccounts, las bases de datos, los usuarios y permisos. 
- No puede ser usado tooprovide acceso granular toocollections y documentos.
- Se crean durante la creación de hello de una cuenta.
- Se pueden regenerar en cualquier momento.

Cada cuenta consta de dos claves maestras: una principal y una secundaria. Hola de claves duales sirve para que se puede volver a generar o revertir las claves, que proporcionan datos y cuenta de acceso continuo de tooyour. 

En suma toohello dos claves de maestro de cuenta de base de datos de Cosmos Hola, hay dos claves de solo lectura. Estas claves de solo lectura sólo permiten operaciones de lectura en la cuenta de hello. Claves de solo lectura no proporcionan acceso tooread recursos de permisos.

Objeto principal, secundario, de solo lectura y las claves maestras de lectura y escritura se pueden recuperar y volver a generar con hello portal de Azure. Para ver instrucciones al respecto, consulte [Visualización, copia y regeneración de las claves de acceso](manage-account.md#keys).

![Control de acceso (de índices IAM) en el portal de Azure: demostrar la seguridad de base de datos NoSQL Hola](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

proceso de Hola de rotación de la clave maestra es simple. Vaya a toohello tooretrieve portal Azure la clave secundaria, reemplace la clave principal con la clave secundaria de la aplicación y, luego, rotar la clave principal de Hola Hola portal de Azure.

![Rotación de claves maestras en el portal de Azure: demostrar la seguridad de base de datos NoSQL Hola](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-toouse-a-master-key"></a>Código de ejemplo toouse una clave maestra

Hello ejemplo de código siguiente muestra cómo toouse una base de datos de Cosmos un DocumentClient de tooinstantiate de punto de conexión y la clave maestra de la cuenta y crear una base de datos. 

```csharp
//Read hello Azure Cosmos DB endpointUrl and authorization keys from config.
//These values are available from hello Azure portal on hello Azure Cosmos DB account blade under "Keys".
//NB > Keep these values in a safe and secure location. Together they provide Administrative access tooyour DocDB account.

private static readonly string endpointUrl = ConfigurationManager.AppSettings["EndPointUrl"];
private static readonly SecureString authorizationKey = ToSecureString(ConfigurationManager.AppSettings["AuthorizationKey"]);

client = new DocumentClient(new Uri(endpointUrl), authorizationKey);

// Create Database
Database database = await client.CreateDatabaseAsync(
    new Database
    {
        Id = databaseName
    });
```

<a id="resource-tokens"></a>

## <a name="resource-tokens"></a>Tokens de recursos

Tokens de recursos proporcionan acceso a recursos de la aplicación toohello dentro de una base de datos. Los tokens de recursos:
- Proporcionar acceso toospecific colecciones, las claves de partición, documentos, datos adjuntos, procedimientos almacenados, desencadenadores y UDF.
- Se crean cuando un [usuario](#users) se concede [permisos](#permissions) tooa de recurso específico.
- Se vuelven a crear cuando una llamada POST, GET o PUT aplica una acción a un recurso de permiso.
- Usar un token de recurso de hash construido específicamente para el permiso, recursos y usuario Hola.
- Está limitado por un período de validez personalizable. intervalo de tiempo válido de Hello predeterminado es una hora. Duración del token, sin embargo, se puede especificar explícitamente, seguridad tooa máximo de cinco horas.
- Proporcionar un seguro toogiving alternativo out Hola master key. 
- Habilitar clientes tooread, escritura y recursos de eliminación de cuenta de base de datos de Cosmos Hola según los permisos de toohello que se ha permitido.

Puede usar un token de recurso (mediante la creación de usuarios de base de datos de Cosmos y permisos) cuando desee tooprovide tooresources de acceso en la base de datos de Cosmos cuenta tooa cliente que no es de confianza con la clave maestra de Hola.  

Tokens de recursos de COSMOS DB proporcionan una alternativa segura que permite a clientes tooread, escritura y eliminación recursos en su cuenta de base de datos de Cosmos según se le ha concedido los permisos toohello y sin necesidad de un patrón de cualquiera o leen la clave única.

Este es un modelo de diseño típico mediante el cual pueden solicita, genera y entrega tooclients tokens de recursos:

1. Un servicio de nivel intermedio se configura tooserve un fotos del usuario tooshare aplicaciones móviles. 
2. servicio de nivel intermedio de Hello posee clave maestra de Hola de hello cuenta de base de datos de Cosmos.
3. aplicación de fotografía de Hola se instala en dispositivos móviles del usuario final. 
4. Inicio de sesión, aplicación de fotografía de hello establece la identidad de Hola de usuario de hello con servicio de capa intermedia de Hola. Este mecanismo de establecimiento de identidad es simplemente una aplicación toohello.
5. Una vez establecida la identidad de hello, servicio de capa intermedia de hello solicita permisos basados en la identidad de Hola.
6. servicio de nivel intermedio de Hello envía una aplicación de teléfono de token toohello atrás de recursos.
7. aplicación de teléfono de Hello puede continuar toouse hello toodirectly token acceso DB Cosmos de recursos con permisos de hello definidos por el token de recurso de Hola y para intervalo de saludo permitido por el token de recurso de Hola. 
8. Cuando expira el token de recurso de hello, las solicitudes posteriores reciben una excepción 401 no autorizado.  En este momento, aplicación de teléfono de hello vuelve a establece la identidad de Hola y solicita un nuevo token de recurso.

    ![Flujo de trabajo de tokens de recursos de Azure Cosmos DB](./media/secure-access-to-data/resourcekeyworkflow.png)

Administración y generación de tokens de recursos se controla mediante bibliotecas de cliente de base de datos de Cosmos nativas Hola; Sin embargo, si utiliza REST debe construir los encabezados de solicitud/autenticación Hola. Para obtener más información acerca de cómo crear encabezados de autenticación para REST, consulte [el Control de acceso en los recursos de base de datos de Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) o hello [código fuente de nuestro SDK](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).

Para un ejemplo de un servicio de nivel intermedio utiliza toogenerate o un agente de tokens de recursos, vea hello [ResourceTokenBroker aplicación](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).

<a id="users"></a>

## <a name="users"></a>Usuarios
Los usuarios de Cosmos DB están asociados con una base de datos de Cosmos DB.  Cada base de datos puede contener cero, o más, usuarios de Cosmos DB.  Hola siguiendo el ejemplo de código muestra cómo toocreate un recurso de usuario de base de datos de Cosmos.

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> Cada usuario de base de datos de Cosmos tiene una propiedad de PermissionsLink que puede ser usado tooretrieve Hola lista de [permisos](#permissions) asociado Hola usuario.
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a>Permisos
Un recurso de permiso de Cosmos DB se asocia a un usuario de dicha base de datos.  Cada usuario puede contener cero o más permisos de Cosmos DB.  Un recurso de permiso proporciona el token de seguridad de acceso tooa que Hola necesidades de los usuarios al intentar tooaccess un recurso de aplicación específica.
Hay dos niveles de acceso disponibles que puede proporcionar un recurso de permiso:

* All: usuario de hello tiene permisos completos en el recurso de Hola.
* Lectura: usuario Hola solo puede leer el contenido de hello del recurso de hello, pero no puede realizar escritura, actualización o las operaciones de eliminación en el recurso de Hola.

> [!NOTE]
> En orden toorun Cosmos DB procedimientos almacenados Hola usuario debe tener Hola todos los permisos en la colección de hello en qué Hola se ejecutará el procedimiento almacenado.
> 
> 

### <a name="code-sample-toocreate-permission"></a>Permiso de toocreate de ejemplo de código

Hello ejemplo de código siguiente muestra cómo toocreate un recurso de permiso de lectura Hola token de recurso del recurso de permiso de Hola y asociar permisos Hola Hola [usuario](#users) creado anteriormente.

```csharp
// Create a permission.
Permission docPermission = new Permission
{
    PermissionMode = PermissionMode.Read,
    ResourceLink = documentCollection.SelfLink,
    Id = "readperm"
};
  
docPermission = await client.CreatePermissionAsync(UriFactory.CreateUserUri("db", "user"), docPermission);
Console.WriteLine(docPermission.Id + " has token of: " + docPermission.Token);
```

Si ha especificado que una clave de partición para la colección, a continuación, permiso de Hola para los recursos de la colección, documentos y datos adjuntos también debe incluir Hola ResourcePartitionKey en suma toohello ResourceLink.

### <a name="code-sample-tooread-permissions-for-user"></a>Permisos de tooread de ejemplo de código de usuario

tooeasily obtener todos los recursos de permiso asociados a un usuario determinado, base de datos de Cosmos pone a disposición un permiso de fuentes de distribución para cada objeto de usuario.  Hello fragmento de código siguiente muestra cómo construir una lista de permisos permiso de hello tooretrieve asociado usuario Hola creado anteriormente y crear instancias de un nuevo DocumentClient en nombre de usuario de Hola.

```csharp
//Read a permission feed.
FeedResponse<Permission> permFeed = await client.ReadPermissionFeedAsync(
  UriFactory.CreateUserUri("db", "myUser"));
 List<Permission> permList = new List<Permission>();

foreach (Permission perm in permFeed)
{
    permList.Add(perm);
}

DocumentClient userClient = new DocumentClient(new Uri(endpointUrl), permList);
```

## <a name="next-steps"></a>Pasos siguientes
* toolearn más información acerca de la seguridad de la base de datos de base de datos de Cosmos, consulte [DB Cosmos: seguridad de base de datos](database-security.md).
* toolearn acerca de cómo administrar las claves maestras y de solo lectura, vea [cómo toomanage una cuenta de base de datos de Azure Cosmos](manage-account.md#keys).
* toolearn cómo ver los tokens de autorización de la base de datos de Azure Cosmos de tooconstruct, [el Control de acceso en los recursos de base de datos de Azure Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).
