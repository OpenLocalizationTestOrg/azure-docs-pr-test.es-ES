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
# <a name="securing-access-tooazure-cosmos-db-data"></a><span data-ttu-id="94d38-103">Proteger los datos de base de datos de Cosmos tooAzure de acceso</span><span class="sxs-lookup"><span data-stu-id="94d38-103">Securing access tooAzure Cosmos DB data</span></span>
<span data-ttu-id="94d38-104">Este artículo proporciona información general de protección de toodata de acceso almacenada en [base de datos de Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="94d38-104">This article provides an overview of securing access toodata stored in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

<span data-ttu-id="94d38-105">Base de datos de Azure Cosmos usa dos tipos de claves tooauthenticate usuarios y proporcionan acceso a los datos tooits y recursos.</span><span class="sxs-lookup"><span data-stu-id="94d38-105">Azure Cosmos DB uses two types of keys tooauthenticate users and provide access tooits data and resources.</span></span> 

|<span data-ttu-id="94d38-106">Tipo de clave</span><span class="sxs-lookup"><span data-stu-id="94d38-106">Key type</span></span>|<span data-ttu-id="94d38-107">Recursos</span><span class="sxs-lookup"><span data-stu-id="94d38-107">Resources</span></span>|
|---|---|
|[<span data-ttu-id="94d38-108">Claves maestras</span><span class="sxs-lookup"><span data-stu-id="94d38-108">Master keys</span></span>](#master-keys) |<span data-ttu-id="94d38-109">Se utilizan para los recursos administrativos: cuentas de base de datos, bases de datos, usuarios y permisos</span><span class="sxs-lookup"><span data-stu-id="94d38-109">Used for administrative resources: database accounts, databases, users, and permissions</span></span>|
|[<span data-ttu-id="94d38-110">Tokens de recursos</span><span class="sxs-lookup"><span data-stu-id="94d38-110">Resource tokens</span></span>](#resource-tokens)|<span data-ttu-id="94d38-111">Se usan para recursos de aplicaciones: colecciones, documentos, datos adjuntos, procedimientos almacenados, desencadenadores y UDF</span><span class="sxs-lookup"><span data-stu-id="94d38-111">Used for application resources: collections, documents, attachments, stored procedures, triggers, and UDFs</span></span>|

<a id="master-keys"></a>

## <a name="master-keys"></a><span data-ttu-id="94d38-112">Claves maestras</span><span class="sxs-lookup"><span data-stu-id="94d38-112">Master keys</span></span> 

<span data-ttu-id="94d38-113">Claves maestras de proporcionar acceso toohello todos los recursos administrativos de hello para la cuenta de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d38-113">Master keys provide access toohello all hello administrative resources for hello database account.</span></span> <span data-ttu-id="94d38-114">Claves maestras:</span><span class="sxs-lookup"><span data-stu-id="94d38-114">Master keys:</span></span>  
- <span data-ttu-id="94d38-115">Proporcionar acceso tooaccounts, las bases de datos, los usuarios y permisos.</span><span class="sxs-lookup"><span data-stu-id="94d38-115">Provide access tooaccounts, databases, users, and permissions.</span></span> 
- <span data-ttu-id="94d38-116">No puede ser usado tooprovide acceso granular toocollections y documentos.</span><span class="sxs-lookup"><span data-stu-id="94d38-116">Cannot be used tooprovide granular access toocollections and documents.</span></span>
- <span data-ttu-id="94d38-117">Se crean durante la creación de hello de una cuenta.</span><span class="sxs-lookup"><span data-stu-id="94d38-117">Are created during hello creation of an account.</span></span>
- <span data-ttu-id="94d38-118">Se pueden regenerar en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="94d38-118">Can be regenerated at any time.</span></span>

<span data-ttu-id="94d38-119">Cada cuenta consta de dos claves maestras: una principal y una secundaria.</span><span class="sxs-lookup"><span data-stu-id="94d38-119">Each account consists of two Master keys: a primary key and secondary key.</span></span> <span data-ttu-id="94d38-120">Hola de claves duales sirve para que se puede volver a generar o revertir las claves, que proporcionan datos y cuenta de acceso continuo de tooyour.</span><span class="sxs-lookup"><span data-stu-id="94d38-120">hello purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access tooyour account and data.</span></span> 

<span data-ttu-id="94d38-121">En suma toohello dos claves de maestro de cuenta de base de datos de Cosmos Hola, hay dos claves de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="94d38-121">In addition toohello two master keys for hello Cosmos DB account, there are two read-only keys.</span></span> <span data-ttu-id="94d38-122">Estas claves de solo lectura sólo permiten operaciones de lectura en la cuenta de hello.</span><span class="sxs-lookup"><span data-stu-id="94d38-122">These read-only keys only allow read operations on hello account.</span></span> <span data-ttu-id="94d38-123">Claves de solo lectura no proporcionan acceso tooread recursos de permisos.</span><span class="sxs-lookup"><span data-stu-id="94d38-123">Read-only keys do not provide access tooread permissions resources.</span></span>

<span data-ttu-id="94d38-124">Objeto principal, secundario, de solo lectura y las claves maestras de lectura y escritura se pueden recuperar y volver a generar con hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="94d38-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using hello Azure portal.</span></span> <span data-ttu-id="94d38-125">Para ver instrucciones al respecto, consulte [Visualización, copia y regeneración de las claves de acceso](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="94d38-125">For instructions, see [View, copy, and regenerate access keys](manage-account.md#keys).</span></span>

![Control de acceso (de índices IAM) en el portal de Azure: demostrar la seguridad de base de datos NoSQL Hola](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

<span data-ttu-id="94d38-127">proceso de Hola de rotación de la clave maestra es simple.</span><span class="sxs-lookup"><span data-stu-id="94d38-127">hello process of rotating your master key is simple.</span></span> <span data-ttu-id="94d38-128">Vaya a toohello tooretrieve portal Azure la clave secundaria, reemplace la clave principal con la clave secundaria de la aplicación y, luego, rotar la clave principal de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="94d38-128">Navigate toohello Azure portal tooretrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate hello primary key in hello Azure portal.</span></span>

![Rotación de claves maestras en el portal de Azure: demostrar la seguridad de base de datos NoSQL Hola](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-toouse-a-master-key"></a><span data-ttu-id="94d38-130">Código de ejemplo toouse una clave maestra</span><span class="sxs-lookup"><span data-stu-id="94d38-130">Code sample toouse a master key</span></span>

<span data-ttu-id="94d38-131">Hello ejemplo de código siguiente muestra cómo toouse una base de datos de Cosmos un DocumentClient de tooinstantiate de punto de conexión y la clave maestra de la cuenta y crear una base de datos.</span><span class="sxs-lookup"><span data-stu-id="94d38-131">hello following code sample illustrates how toouse a Cosmos DB account endpoint and master key tooinstantiate a DocumentClient and create a database.</span></span> 

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

## <a name="resource-tokens"></a><span data-ttu-id="94d38-132">Tokens de recursos</span><span class="sxs-lookup"><span data-stu-id="94d38-132">Resource tokens</span></span>

<span data-ttu-id="94d38-133">Tokens de recursos proporcionan acceso a recursos de la aplicación toohello dentro de una base de datos.</span><span class="sxs-lookup"><span data-stu-id="94d38-133">Resource tokens provide access toohello application resources within a database.</span></span> <span data-ttu-id="94d38-134">Los tokens de recursos:</span><span class="sxs-lookup"><span data-stu-id="94d38-134">Resource tokens:</span></span>
- <span data-ttu-id="94d38-135">Proporcionar acceso toospecific colecciones, las claves de partición, documentos, datos adjuntos, procedimientos almacenados, desencadenadores y UDF.</span><span class="sxs-lookup"><span data-stu-id="94d38-135">Provide access toospecific collections, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span></span>
- <span data-ttu-id="94d38-136">Se crean cuando un [usuario](#users) se concede [permisos](#permissions) tooa de recurso específico.</span><span class="sxs-lookup"><span data-stu-id="94d38-136">Are created when a [user](#users) is granted [permissions](#permissions) tooa specific resource.</span></span>
- <span data-ttu-id="94d38-137">Se vuelven a crear cuando una llamada POST, GET o PUT aplica una acción a un recurso de permiso.</span><span class="sxs-lookup"><span data-stu-id="94d38-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span></span>
- <span data-ttu-id="94d38-138">Usar un token de recurso de hash construido específicamente para el permiso, recursos y usuario Hola.</span><span class="sxs-lookup"><span data-stu-id="94d38-138">Use a hash resource token specifically constructed for hello user, resource, and permission.</span></span>
- <span data-ttu-id="94d38-139">Está limitado por un período de validez personalizable.</span><span class="sxs-lookup"><span data-stu-id="94d38-139">Are time bound with a customizable validity period.</span></span> <span data-ttu-id="94d38-140">intervalo de tiempo válido de Hello predeterminado es una hora.</span><span class="sxs-lookup"><span data-stu-id="94d38-140">hello default valid timespan is one hour.</span></span> <span data-ttu-id="94d38-141">Duración del token, sin embargo, se puede especificar explícitamente, seguridad tooa máximo de cinco horas.</span><span class="sxs-lookup"><span data-stu-id="94d38-141">Token lifetime, however, may be explicitly specified, up tooa maximum of five hours.</span></span>
- <span data-ttu-id="94d38-142">Proporcionar un seguro toogiving alternativo out Hola master key.</span><span class="sxs-lookup"><span data-stu-id="94d38-142">Provide a safe alternative toogiving out hello master key.</span></span> 
- <span data-ttu-id="94d38-143">Habilitar clientes tooread, escritura y recursos de eliminación de cuenta de base de datos de Cosmos Hola según los permisos de toohello que se ha permitido.</span><span class="sxs-lookup"><span data-stu-id="94d38-143">Enable clients tooread, write, and delete resources in hello Cosmos DB account according toohello permissions they've been granted.</span></span>

<span data-ttu-id="94d38-144">Puede usar un token de recurso (mediante la creación de usuarios de base de datos de Cosmos y permisos) cuando desee tooprovide tooresources de acceso en la base de datos de Cosmos cuenta tooa cliente que no es de confianza con la clave maestra de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d38-144">You can use a resource token (by creating Cosmos DB users and permissions) when you want tooprovide access tooresources in your Cosmos DB account tooa client that cannot be trusted with hello master key.</span></span>  

<span data-ttu-id="94d38-145">Tokens de recursos de COSMOS DB proporcionan una alternativa segura que permite a clientes tooread, escritura y eliminación recursos en su cuenta de base de datos de Cosmos según se le ha concedido los permisos toohello y sin necesidad de un patrón de cualquiera o leen la clave única.</span><span class="sxs-lookup"><span data-stu-id="94d38-145">Cosmos DB resource tokens provide a safe alternative that enables clients tooread, write, and delete resources in your Cosmos DB account according toohello permissions you've granted, and without need for either a master or read only key.</span></span>

<span data-ttu-id="94d38-146">Este es un modelo de diseño típico mediante el cual pueden solicita, genera y entrega tooclients tokens de recursos:</span><span class="sxs-lookup"><span data-stu-id="94d38-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered tooclients:</span></span>

1. <span data-ttu-id="94d38-147">Un servicio de nivel intermedio se configura tooserve un fotos del usuario tooshare aplicaciones móviles.</span><span class="sxs-lookup"><span data-stu-id="94d38-147">A mid-tier service is set up tooserve a mobile application tooshare user photos.</span></span> 
2. <span data-ttu-id="94d38-148">servicio de nivel intermedio de Hello posee clave maestra de Hola de hello cuenta de base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="94d38-148">hello mid-tier service possesses hello master key of hello Cosmos DB account.</span></span>
3. <span data-ttu-id="94d38-149">aplicación de fotografía de Hola se instala en dispositivos móviles del usuario final.</span><span class="sxs-lookup"><span data-stu-id="94d38-149">hello photo app is installed on end-user mobile devices.</span></span> 
4. <span data-ttu-id="94d38-150">Inicio de sesión, aplicación de fotografía de hello establece la identidad de Hola de usuario de hello con servicio de capa intermedia de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d38-150">On login, hello photo app establishes hello identity of hello user with hello mid-tier service.</span></span> <span data-ttu-id="94d38-151">Este mecanismo de establecimiento de identidad es simplemente una aplicación toohello.</span><span class="sxs-lookup"><span data-stu-id="94d38-151">This mechanism of identity establishment is purely up toohello application.</span></span>
5. <span data-ttu-id="94d38-152">Una vez establecida la identidad de hello, servicio de capa intermedia de hello solicita permisos basados en la identidad de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d38-152">Once hello identity is established, hello mid-tier service requests permissions based on hello identity.</span></span>
6. <span data-ttu-id="94d38-153">servicio de nivel intermedio de Hello envía una aplicación de teléfono de token toohello atrás de recursos.</span><span class="sxs-lookup"><span data-stu-id="94d38-153">hello mid-tier service sends a resource token back toohello phone app.</span></span>
7. <span data-ttu-id="94d38-154">aplicación de teléfono de Hello puede continuar toouse hello toodirectly token acceso DB Cosmos de recursos con permisos de hello definidos por el token de recurso de Hola y para intervalo de saludo permitido por el token de recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d38-154">hello phone app can continue toouse hello resource token toodirectly access Cosmos DB resources with hello permissions defined by hello resource token and for hello interval allowed by hello resource token.</span></span> 
8. <span data-ttu-id="94d38-155">Cuando expira el token de recurso de hello, las solicitudes posteriores reciben una excepción 401 no autorizado.</span><span class="sxs-lookup"><span data-stu-id="94d38-155">When hello resource token expires, subsequent requests receive a 401 unauthorized exception.</span></span>  <span data-ttu-id="94d38-156">En este momento, aplicación de teléfono de hello vuelve a establece la identidad de Hola y solicita un nuevo token de recurso.</span><span class="sxs-lookup"><span data-stu-id="94d38-156">At this point, hello phone app re-establishes hello identity and requests a new resource token.</span></span>

    ![Flujo de trabajo de tokens de recursos de Azure Cosmos DB](./media/secure-access-to-data/resourcekeyworkflow.png)

<span data-ttu-id="94d38-158">Administración y generación de tokens de recursos se controla mediante bibliotecas de cliente de base de datos de Cosmos nativas Hola; Sin embargo, si utiliza REST debe construir los encabezados de solicitud/autenticación Hola.</span><span class="sxs-lookup"><span data-stu-id="94d38-158">Resource token generation and management is handled by hello native Cosmos DB client libraries; however, if you use REST you must construct hello request/authentication headers.</span></span> <span data-ttu-id="94d38-159">Para obtener más información acerca de cómo crear encabezados de autenticación para REST, consulte [el Control de acceso en los recursos de base de datos de Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) o hello [código fuente de nuestro SDK](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span><span class="sxs-lookup"><span data-stu-id="94d38-159">For more information on creating authentication headers for REST, see [Access Control on Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) or hello [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span></span>

<span data-ttu-id="94d38-160">Para un ejemplo de un servicio de nivel intermedio utiliza toogenerate o un agente de tokens de recursos, vea hello [ResourceTokenBroker aplicación](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span><span class="sxs-lookup"><span data-stu-id="94d38-160">For an example of a middle tier service used toogenerate or broker resource tokens, see hello [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span></span>

<a id="users"></a>

## <a name="users"></a><span data-ttu-id="94d38-161">Usuarios</span><span class="sxs-lookup"><span data-stu-id="94d38-161">Users</span></span>
<span data-ttu-id="94d38-162">Los usuarios de Cosmos DB están asociados con una base de datos de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="94d38-162">Cosmos DB users are associated with a Cosmos DB database.</span></span>  <span data-ttu-id="94d38-163">Cada base de datos puede contener cero, o más, usuarios de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="94d38-163">Each database can contain zero or more Cosmos DB users.</span></span>  <span data-ttu-id="94d38-164">Hola siguiendo el ejemplo de código muestra cómo toocreate un recurso de usuario de base de datos de Cosmos.</span><span class="sxs-lookup"><span data-stu-id="94d38-164">hello following code sample shows how toocreate a Cosmos DB user resource.</span></span>

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> <span data-ttu-id="94d38-165">Cada usuario de base de datos de Cosmos tiene una propiedad de PermissionsLink que puede ser usado tooretrieve Hola lista de [permisos](#permissions) asociado Hola usuario.</span><span class="sxs-lookup"><span data-stu-id="94d38-165">Each Cosmos DB user has a PermissionsLink property that can be used tooretrieve hello list of [permissions](#permissions) associated with hello user.</span></span>
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a><span data-ttu-id="94d38-166">Permisos</span><span class="sxs-lookup"><span data-stu-id="94d38-166">Permissions</span></span>
<span data-ttu-id="94d38-167">Un recurso de permiso de Cosmos DB se asocia a un usuario de dicha base de datos.</span><span class="sxs-lookup"><span data-stu-id="94d38-167">A Cosmos DB permission resource is associated with a Cosmos DB user.</span></span>  <span data-ttu-id="94d38-168">Cada usuario puede contener cero o más permisos de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="94d38-168">Each user may contain zero or more Cosmos DB permissions.</span></span>  <span data-ttu-id="94d38-169">Un recurso de permiso proporciona el token de seguridad de acceso tooa que Hola necesidades de los usuarios al intentar tooaccess un recurso de aplicación específica.</span><span class="sxs-lookup"><span data-stu-id="94d38-169">A permission resource provides access tooa security token that hello user needs when trying tooaccess a specific application resource.</span></span>
<span data-ttu-id="94d38-170">Hay dos niveles de acceso disponibles que puede proporcionar un recurso de permiso:</span><span class="sxs-lookup"><span data-stu-id="94d38-170">There are two available access levels that may be provided by a permission resource:</span></span>

* <span data-ttu-id="94d38-171">All: usuario de hello tiene permisos completos en el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d38-171">All: hello user has full permission on hello resource.</span></span>
* <span data-ttu-id="94d38-172">Lectura: usuario Hola solo puede leer el contenido de hello del recurso de hello, pero no puede realizar escritura, actualización o las operaciones de eliminación en el recurso de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d38-172">Read: hello user can only read hello contents of hello resource but cannot perform write, update, or delete operations on hello resource.</span></span>

> [!NOTE]
> <span data-ttu-id="94d38-173">En orden toorun Cosmos DB procedimientos almacenados Hola usuario debe tener Hola todos los permisos en la colección de hello en qué Hola se ejecutará el procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="94d38-173">In order toorun Cosmos DB stored procedures hello user must have hello All permission on hello collection in which hello stored procedure will be run.</span></span>
> 
> 

### <a name="code-sample-toocreate-permission"></a><span data-ttu-id="94d38-174">Permiso de toocreate de ejemplo de código</span><span class="sxs-lookup"><span data-stu-id="94d38-174">Code sample toocreate permission</span></span>

<span data-ttu-id="94d38-175">Hello ejemplo de código siguiente muestra cómo toocreate un recurso de permiso de lectura Hola token de recurso del recurso de permiso de Hola y asociar permisos Hola Hola [usuario](#users) creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="94d38-175">hello following code sample shows how toocreate a permission resource, read hello resource token of hello permission resource, and associate hello permissions with hello [user](#users) created above.</span></span>

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

<span data-ttu-id="94d38-176">Si ha especificado que una clave de partición para la colección, a continuación, permiso de Hola para los recursos de la colección, documentos y datos adjuntos también debe incluir Hola ResourcePartitionKey en suma toohello ResourceLink.</span><span class="sxs-lookup"><span data-stu-id="94d38-176">If you have specified a partition key for your collection, then hello permission for collection, document, and attachment resources must also include hello ResourcePartitionKey in addition toohello ResourceLink.</span></span>

### <a name="code-sample-tooread-permissions-for-user"></a><span data-ttu-id="94d38-177">Permisos de tooread de ejemplo de código de usuario</span><span class="sxs-lookup"><span data-stu-id="94d38-177">Code sample tooread permissions for user</span></span>

<span data-ttu-id="94d38-178">tooeasily obtener todos los recursos de permiso asociados a un usuario determinado, base de datos de Cosmos pone a disposición un permiso de fuentes de distribución para cada objeto de usuario.</span><span class="sxs-lookup"><span data-stu-id="94d38-178">tooeasily obtain all permission resources associated with a particular user, Cosmos DB makes available a permission feed for each user object.</span></span>  <span data-ttu-id="94d38-179">Hello fragmento de código siguiente muestra cómo construir una lista de permisos permiso de hello tooretrieve asociado usuario Hola creado anteriormente y crear instancias de un nuevo DocumentClient en nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="94d38-179">hello following code snippet shows how tooretrieve hello permission associated with hello user created above, construct a permission list, and instantiate a new DocumentClient on behalf of hello user.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="94d38-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="94d38-180">Next steps</span></span>
* <span data-ttu-id="94d38-181">toolearn más información acerca de la seguridad de la base de datos de base de datos de Cosmos, consulte [DB Cosmos: seguridad de base de datos](database-security.md).</span><span class="sxs-lookup"><span data-stu-id="94d38-181">toolearn more about Cosmos DB database security, see [Cosmos DB: Database security](database-security.md).</span></span>
* <span data-ttu-id="94d38-182">toolearn acerca de cómo administrar las claves maestras y de solo lectura, vea [cómo toomanage una cuenta de base de datos de Azure Cosmos](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="94d38-182">toolearn about managing master and read-only keys, see [How toomanage an Azure Cosmos DB account](manage-account.md#keys).</span></span>
* <span data-ttu-id="94d38-183">toolearn cómo ver los tokens de autorización de la base de datos de Azure Cosmos de tooconstruct, [el Control de acceso en los recursos de base de datos de Azure Cosmos](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span><span class="sxs-lookup"><span data-stu-id="94d38-183">toolearn how tooconstruct Azure Cosmos DB authorization tokens, see [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span></span>
