---
title: "Información sobre la protección del acceso a los datos de Azure Cosmos DB | Microsoft Docs"
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
ms.openlocfilehash: 383e04f91eec2f465b381ce30f2d6d24c488b731
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="securing-access-to-azure-cosmos-db-data"></a><span data-ttu-id="77df7-103">Protección del acceso a los datos de Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="77df7-103">Securing access to Azure Cosmos DB data</span></span>
<span data-ttu-id="77df7-104">En este artículo se proporciona información general sobre la protección del acceso a los datos almacenados en [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="77df7-104">This article provides an overview of securing access to data stored in [Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

<span data-ttu-id="77df7-105">Azure Cosmos DB usa dos tipos de claves para autenticar usuarios y proporcionar acceso a sus datos y recursos.</span><span class="sxs-lookup"><span data-stu-id="77df7-105">Azure Cosmos DB uses two types of keys to authenticate users and provide access to its data and resources.</span></span> 

|<span data-ttu-id="77df7-106">Tipo de clave</span><span class="sxs-lookup"><span data-stu-id="77df7-106">Key type</span></span>|<span data-ttu-id="77df7-107">Recursos</span><span class="sxs-lookup"><span data-stu-id="77df7-107">Resources</span></span>|
|---|---|
|[<span data-ttu-id="77df7-108">Claves maestras</span><span class="sxs-lookup"><span data-stu-id="77df7-108">Master keys</span></span>](#master-keys) |<span data-ttu-id="77df7-109">Se utilizan para los recursos administrativos: cuentas de base de datos, bases de datos, usuarios y permisos</span><span class="sxs-lookup"><span data-stu-id="77df7-109">Used for administrative resources: database accounts, databases, users, and permissions</span></span>|
|[<span data-ttu-id="77df7-110">Tokens de recursos</span><span class="sxs-lookup"><span data-stu-id="77df7-110">Resource tokens</span></span>](#resource-tokens)|<span data-ttu-id="77df7-111">Se usan para recursos de aplicaciones: colecciones, documentos, datos adjuntos, procedimientos almacenados, desencadenadores y UDF</span><span class="sxs-lookup"><span data-stu-id="77df7-111">Used for application resources: collections, documents, attachments, stored procedures, triggers, and UDFs</span></span>|

<a id="master-keys"></a>

## <a name="master-keys"></a><span data-ttu-id="77df7-112">Claves maestras</span><span class="sxs-lookup"><span data-stu-id="77df7-112">Master keys</span></span> 

<span data-ttu-id="77df7-113">Las claves maestras proporcionan acceso a todos los recursos administrativos de la cuenta de base de datos.</span><span class="sxs-lookup"><span data-stu-id="77df7-113">Master keys provide access to the all the administrative resources for the database account.</span></span> <span data-ttu-id="77df7-114">Claves maestras:</span><span class="sxs-lookup"><span data-stu-id="77df7-114">Master keys:</span></span>  
- <span data-ttu-id="77df7-115">Proporcionan acceso a cuentas, bases de datos, usuarios y permisos.</span><span class="sxs-lookup"><span data-stu-id="77df7-115">Provide access to accounts, databases, users, and permissions.</span></span> 
- <span data-ttu-id="77df7-116">No se pueden usar para proporcionar acceso granular a colecciones y documentos.</span><span class="sxs-lookup"><span data-stu-id="77df7-116">Cannot be used to provide granular access to collections and documents.</span></span>
- <span data-ttu-id="77df7-117">Se crean durante la creación de una cuenta.</span><span class="sxs-lookup"><span data-stu-id="77df7-117">Are created during the creation of an account.</span></span>
- <span data-ttu-id="77df7-118">Se pueden regenerar en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="77df7-118">Can be regenerated at any time.</span></span>

<span data-ttu-id="77df7-119">Cada cuenta consta de dos claves maestras: una principal y una secundaria.</span><span class="sxs-lookup"><span data-stu-id="77df7-119">Each account consists of two Master keys: a primary key and secondary key.</span></span> <span data-ttu-id="77df7-120">El fin de las claves dobles es que pueda regenerar, o distribuir claves, lo que proporciona un acceso continuo a su cuenta y sus datos.</span><span class="sxs-lookup"><span data-stu-id="77df7-120">The purpose of dual keys is so that you can regenerate, or roll keys, providing continuous access to your account and data.</span></span> 

<span data-ttu-id="77df7-121">Además de las dos claves maestras de la cuenta de Cosmos DB, hay dos claves de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="77df7-121">In addition to the two master keys for the Cosmos DB account, there are two read-only keys.</span></span> <span data-ttu-id="77df7-122">Estas claves de solo lectura permiten operaciones de lectura en la cuenta.</span><span class="sxs-lookup"><span data-stu-id="77df7-122">These read-only keys only allow read operations on the account.</span></span> <span data-ttu-id="77df7-123">Las claves de solo lectura no proporcionan acceso a los recursos de los permisos de lectura.</span><span class="sxs-lookup"><span data-stu-id="77df7-123">Read-only keys do not provide access to read permissions resources.</span></span>

<span data-ttu-id="77df7-124">Las claves maestras principal, secundaria, de solo lectura y de lectura y escritura se pueden recuperar y volver a generar desde Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="77df7-124">Primary, secondary, read only, and read-write master keys can be retrieved and regenerated using the Azure portal.</span></span> <span data-ttu-id="77df7-125">Para ver instrucciones al respecto, consulte [Visualización, copia y regeneración de las claves de acceso](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="77df7-125">For instructions, see [View, copy, and regenerate access keys](manage-account.md#keys).</span></span>

![Control de acceso (IAM) en Azure Portal: demostración de la seguridad de bases de datos NoSQL](./media/secure-access-to-data/nosql-database-security-master-key-portal.png)

<span data-ttu-id="77df7-127">El proceso de rotación de la clave maestra es simple.</span><span class="sxs-lookup"><span data-stu-id="77df7-127">The process of rotating your master key is simple.</span></span> <span data-ttu-id="77df7-128">Navegue hasta Azure Portal para recuperar la clave secundaria, reemplace la clave principal por la clave secundaria en la aplicación y, finalmente, rote la clave principal en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="77df7-128">Navigate to the Azure portal to retrieve your secondary key, then replace your primary key with your secondary key in your application, then rotate the primary key in the Azure portal.</span></span>

![Rotación de la clave maestra en Azure Portal: demostración de la seguridad de bases de datos NoSQL](./media/secure-access-to-data/nosql-database-security-master-key-rotate-workflow.png)

### <a name="code-sample-to-use-a-master-key"></a><span data-ttu-id="77df7-130">Ejemplo de código para usar una clave maestra</span><span class="sxs-lookup"><span data-stu-id="77df7-130">Code sample to use a master key</span></span>

<span data-ttu-id="77df7-131">El fragmento de código de ejemplo ilustra cómo usar un punto de conexión y la clave maestra de la cuenta de Cosmos DB para crear una instancia de DocumentClient y una base de datos.</span><span class="sxs-lookup"><span data-stu-id="77df7-131">The following code sample illustrates how to use a Cosmos DB account endpoint and master key to instantiate a DocumentClient and create a database.</span></span> 

```csharp
//Read the Azure Cosmos DB endpointUrl and authorization keys from config.
//These values are available from the Azure portal on the Azure Cosmos DB account blade under "Keys".
//NB > Keep these values in a safe and secure location. Together they provide Administrative access to your DocDB account.

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

## <a name="resource-tokens"></a><span data-ttu-id="77df7-132">Tokens de recursos</span><span class="sxs-lookup"><span data-stu-id="77df7-132">Resource tokens</span></span>

<span data-ttu-id="77df7-133">Los tokens de recursos proporcionan acceso a los recursos de la aplicación en una base de datos.</span><span class="sxs-lookup"><span data-stu-id="77df7-133">Resource tokens provide access to the application resources within a database.</span></span> <span data-ttu-id="77df7-134">Los tokens de recursos:</span><span class="sxs-lookup"><span data-stu-id="77df7-134">Resource tokens:</span></span>
- <span data-ttu-id="77df7-135">Proporcionan acceso a colecciones, claves de partición, documentos, datos adjuntos, procedimientos almacenados, desencadenadores y UDF concretos.</span><span class="sxs-lookup"><span data-stu-id="77df7-135">Provide access to specific collections, partition keys, documents, attachments, stored procedures, triggers, and UDFs.</span></span>
- <span data-ttu-id="77df7-136">Se crean cuando a un [usuario](#users) se le conceden [permisos](#permissions) para un recurso concreto.</span><span class="sxs-lookup"><span data-stu-id="77df7-136">Are created when a [user](#users) is granted [permissions](#permissions) to a specific resource.</span></span>
- <span data-ttu-id="77df7-137">Se vuelven a crear cuando una llamada POST, GET o PUT aplica una acción a un recurso de permiso.</span><span class="sxs-lookup"><span data-stu-id="77df7-137">Are recreated when a permission resource is acted upon on by POST, GET, or PUT call.</span></span>
- <span data-ttu-id="77df7-138">Usan un token de recurso de hash construido específicamente para el usuario, el recurso y el permiso.</span><span class="sxs-lookup"><span data-stu-id="77df7-138">Use a hash resource token specifically constructed for the user, resource, and permission.</span></span>
- <span data-ttu-id="77df7-139">Está limitado por un período de validez personalizable.</span><span class="sxs-lookup"><span data-stu-id="77df7-139">Are time bound with a customizable validity period.</span></span> <span data-ttu-id="77df7-140">El intervalo de tiempo válido predeterminado es una hora.</span><span class="sxs-lookup"><span data-stu-id="77df7-140">The default valid timespan is one hour.</span></span> <span data-ttu-id="77df7-141">Sin embargo, la vigencia del token puede especificarse explícitamente hasta un máximo de cinco horas.</span><span class="sxs-lookup"><span data-stu-id="77df7-141">Token lifetime, however, may be explicitly specified, up to a maximum of five hours.</span></span>
- <span data-ttu-id="77df7-142">Proporcionan una alternativa segura a proporcionar la clave maestra.</span><span class="sxs-lookup"><span data-stu-id="77df7-142">Provide a safe alternative to giving out the master key.</span></span> 
- <span data-ttu-id="77df7-143">Permiten que los clientes lean, escriban y eliminen recursos de la cuenta de Cosmos DB en función de los permisos que se les haya otorgado.</span><span class="sxs-lookup"><span data-stu-id="77df7-143">Enable clients to read, write, and delete resources in the Cosmos DB account according to the permissions they've been granted.</span></span>

<span data-ttu-id="77df7-144">Si desea proporcionar acceso a los recursos de su cuenta de Cosmos DB a un cliente que no es de confianza con la clave maestra, puede usar un token de recurso (mediante la creación de usuarios y permisos de Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="77df7-144">You can use a resource token (by creating Cosmos DB users and permissions) when you want to provide access to resources in your Cosmos DB account to a client that cannot be trusted with the master key.</span></span>  

<span data-ttu-id="77df7-145">Los tokens de recurso de Cosmos DB ofrecen una alternativa segura que permite a los clientes leer, escribir y eliminar recursos de la cuenta de Cosmos DB en función de los permisos que se les hayan concedido y sin necesidad de una clave maestra o de solo lectura.</span><span class="sxs-lookup"><span data-stu-id="77df7-145">Cosmos DB resource tokens provide a safe alternative that enables clients to read, write, and delete resources in your Cosmos DB account according to the permissions you've granted, and without need for either a master or read only key.</span></span>

<span data-ttu-id="77df7-146">Este es un patrón de diseño típico para solicitar, generar y entregar tokens de recursos a los clientes:</span><span class="sxs-lookup"><span data-stu-id="77df7-146">Here is a typical design pattern whereby resource tokens may be requested, generated, and delivered to clients:</span></span>

1. <span data-ttu-id="77df7-147">Se configura un servicio de nivel intermedio para que una aplicación móvil pueda usarlo para compartir fotos del usuario.</span><span class="sxs-lookup"><span data-stu-id="77df7-147">A mid-tier service is set up to serve a mobile application to share user photos.</span></span> 
2. <span data-ttu-id="77df7-148">Dicho servicio tiene la clave maestra de la cuenta de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="77df7-148">The mid-tier service possesses the master key of the Cosmos DB account.</span></span>
3. <span data-ttu-id="77df7-149">La aplicación fotográfica se instala en los dispositivos móviles de los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="77df7-149">The photo app is installed on end-user mobile devices.</span></span> 
4. <span data-ttu-id="77df7-150">Al iniciar sesión, dicha aplicación establece la identidad del usuario con el servicio de nivel intermedio.</span><span class="sxs-lookup"><span data-stu-id="77df7-150">On login, the photo app establishes the identity of the user with the mid-tier service.</span></span> <span data-ttu-id="77df7-151">Este mecanismo de establecimiento de identidad depende únicamente de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="77df7-151">This mechanism of identity establishment is purely up to the application.</span></span>
5. <span data-ttu-id="77df7-152">Una vez establecida la identidad, el servicio de nivel intermedio solicita permisos en función de esta.</span><span class="sxs-lookup"><span data-stu-id="77df7-152">Once the identity is established, the mid-tier service requests permissions based on the identity.</span></span>
6. <span data-ttu-id="77df7-153">El servicio de nivel intermedio reenvía un token de recurso a la aplicación de teléfono.</span><span class="sxs-lookup"><span data-stu-id="77df7-153">The mid-tier service sends a resource token back to the phone app.</span></span>
7. <span data-ttu-id="77df7-154">La aplicación de teléfono puede seguir usando el token de recurso para obtener acceso directo a los recursos de Cosmos DB con los permisos definidos por el token de recurso y para el intervalo permitido por dicho token.</span><span class="sxs-lookup"><span data-stu-id="77df7-154">The phone app can continue to use the resource token to directly access Cosmos DB resources with the permissions defined by the resource token and for the interval allowed by the resource token.</span></span> 
8. <span data-ttu-id="77df7-155">Cuando el token de recurso expira, las solicitudes posteriores reciben un mensaje 401 de excepción no autorizada.</span><span class="sxs-lookup"><span data-stu-id="77df7-155">When the resource token expires, subsequent requests receive a 401 unauthorized exception.</span></span>  <span data-ttu-id="77df7-156">En este punto, la aplicación de teléfono restablece la identidad y solicita un nuevo token de recurso.</span><span class="sxs-lookup"><span data-stu-id="77df7-156">At this point, the phone app re-establishes the identity and requests a new resource token.</span></span>

    ![Flujo de trabajo de tokens de recursos de Azure Cosmos DB](./media/secure-access-to-data/resourcekeyworkflow.png)

<span data-ttu-id="77df7-158">La generación y administración de los tokens de recursos las controlan las bibliotecas de cliente de Cosmos DB nativas; sin embargo, si se usa REST, debe construir los encabezados de solicitud o autenticación.</span><span class="sxs-lookup"><span data-stu-id="77df7-158">Resource token generation and management is handled by the native Cosmos DB client libraries; however, if you use REST you must construct the request/authentication headers.</span></span> <span data-ttu-id="77df7-159">Para más información acerca de cómo crear encabezados de autenticación para REST, consulte [Access Control on Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) (Control de acceso en recursos de Cosmos DB) o [el código fuente de nuestros SDK](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span><span class="sxs-lookup"><span data-stu-id="77df7-159">For more information on creating authentication headers for REST, see [Access Control on Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) or the [source code for our SDKs](https://github.com/Azure/azure-documentdb-node/blob/master/source/lib/auth.js).</span></span>

<span data-ttu-id="77df7-160">Para ver un ejemplo de un servicio de nivel intermedio que se usa para generarlo o los tokens de recursos del agente, consulte la [aplicación ResourceTokenBroker](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span><span class="sxs-lookup"><span data-stu-id="77df7-160">For an example of a middle tier service used to generate or broker resource tokens, see the [ResourceTokenBroker app](https://github.com/Azure/azure-documentdb-dotnet/tree/master/samples/xamarin/UserItems/ResourceTokenBroker/ResourceTokenBroker/Controllers).</span></span>

<a id="users"></a>

## <a name="users"></a><span data-ttu-id="77df7-161">Usuarios</span><span class="sxs-lookup"><span data-stu-id="77df7-161">Users</span></span>
<span data-ttu-id="77df7-162">Los usuarios de Cosmos DB están asociados con una base de datos de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="77df7-162">Cosmos DB users are associated with a Cosmos DB database.</span></span>  <span data-ttu-id="77df7-163">Cada base de datos puede contener cero, o más, usuarios de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="77df7-163">Each database can contain zero or more Cosmos DB users.</span></span>  <span data-ttu-id="77df7-164">El siguiente código de ejemplo muestra cómo crear un recurso de usuario de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="77df7-164">The following code sample shows how to create a Cosmos DB user resource.</span></span>

```csharp
//Create a user.
User docUser = new User
{
    Id = "mobileuser"
};

docUser = await client.CreateUserAsync(UriFactory.CreateDatabaseUri("db"), docUser);
```

> [!NOTE]
> <span data-ttu-id="77df7-165">Cada usuario de Cosmos DB tiene una propiedad PermissionsLink que se puede usar para recuperar la lista de [permisos](#permissions) asociados al usuario.</span><span class="sxs-lookup"><span data-stu-id="77df7-165">Each Cosmos DB user has a PermissionsLink property that can be used to retrieve the list of [permissions](#permissions) associated with the user.</span></span>
> 
> 

<a id="permissions"></a>

## <a name="permissions"></a><span data-ttu-id="77df7-166">Permisos</span><span class="sxs-lookup"><span data-stu-id="77df7-166">Permissions</span></span>
<span data-ttu-id="77df7-167">Un recurso de permiso de Cosmos DB se asocia a un usuario de dicha base de datos.</span><span class="sxs-lookup"><span data-stu-id="77df7-167">A Cosmos DB permission resource is associated with a Cosmos DB user.</span></span>  <span data-ttu-id="77df7-168">Cada usuario puede contener cero o más permisos de Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="77df7-168">Each user may contain zero or more Cosmos DB permissions.</span></span>  <span data-ttu-id="77df7-169">Un recurso de permiso proporciona acceso a un token de seguridad que el usuario necesita al intentar obtener acceso a un recurso de aplicación específico.</span><span class="sxs-lookup"><span data-stu-id="77df7-169">A permission resource provides access to a security token that the user needs when trying to access a specific application resource.</span></span>
<span data-ttu-id="77df7-170">Hay dos niveles de acceso disponibles que puede proporcionar un recurso de permiso:</span><span class="sxs-lookup"><span data-stu-id="77df7-170">There are two available access levels that may be provided by a permission resource:</span></span>

* <span data-ttu-id="77df7-171">Todo: el usuario tiene pleno permiso en el recurso.</span><span class="sxs-lookup"><span data-stu-id="77df7-171">All: The user has full permission on the resource.</span></span>
* <span data-ttu-id="77df7-172">Lectura: el usuario solo puede leer el contenido del recurso, pero no realizar operaciones de escritura, actualización o eliminación en este.</span><span class="sxs-lookup"><span data-stu-id="77df7-172">Read: The user can only read the contents of the resource but cannot perform write, update, or delete operations on the resource.</span></span>

> [!NOTE]
> <span data-ttu-id="77df7-173">Para ejecutar procedimientos almacenados de Cosmos DB, el usuario debe tener el permiso Todo en la colección donde se va a ejecutar el procedimiento almacenado.</span><span class="sxs-lookup"><span data-stu-id="77df7-173">In order to run Cosmos DB stored procedures the user must have the All permission on the collection in which the stored procedure will be run.</span></span>
> 
> 

### <a name="code-sample-to-create-permission"></a><span data-ttu-id="77df7-174">Ejemplo de código para crear permisos</span><span class="sxs-lookup"><span data-stu-id="77df7-174">Code sample to create permission</span></span>

<span data-ttu-id="77df7-175">El código de ejemplo siguiente muestra cómo crear un recurso de permisos, leer el token de dicho recurso y asociar los permisos al [usuario](#users) creado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="77df7-175">The following code sample shows how to create a permission resource, read the resource token of the permission resource, and associate the permissions with the [user](#users) created above.</span></span>

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

<span data-ttu-id="77df7-176">Si ha especificado una clave de partición para la colección y, después, el permiso para los recursos de la colección, de los documentos y de los datos adjuntos también debe incluir la clave ResourcePartitionKey, además de ResourceLink.</span><span class="sxs-lookup"><span data-stu-id="77df7-176">If you have specified a partition key for your collection, then the permission for collection, document, and attachment resources must also include the ResourcePartitionKey in addition to the ResourceLink.</span></span>

### <a name="code-sample-to-read-permissions-for-user"></a><span data-ttu-id="77df7-177">Ejemplo de código para los permisos de lectura del usuario</span><span class="sxs-lookup"><span data-stu-id="77df7-177">Code sample to read permissions for user</span></span>

<span data-ttu-id="77df7-178">Para obtener fácilmente todos los recursos de permisos asociados a un usuario concreto, Cosmos DB dispone de una fuente de permisos para cada objeto de usuario.</span><span class="sxs-lookup"><span data-stu-id="77df7-178">To easily obtain all permission resources associated with a particular user, Cosmos DB makes available a permission feed for each user object.</span></span>  <span data-ttu-id="77df7-179">El fragmento de código siguiente muestra cómo recuperar el permiso asociado al usuario creado anteriormente, construir una lista de permisos y crear instancias de un nuevo elemento DocumentClient en nombre del usuario.</span><span class="sxs-lookup"><span data-stu-id="77df7-179">The following code snippet shows how to retrieve the permission associated with the user created above, construct a permission list, and instantiate a new DocumentClient on behalf of the user.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="77df7-180">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="77df7-180">Next steps</span></span>
* <span data-ttu-id="77df7-181">Para más información acerca de la seguridad de las bases de datos de Cosmos DB, consulte [Cosmos DB: Database security](database-security.md) (Cosmos DB: seguridad de bases de datos).</span><span class="sxs-lookup"><span data-stu-id="77df7-181">To learn more about Cosmos DB database security, see [Cosmos DB: Database security](database-security.md).</span></span>
* <span data-ttu-id="77df7-182">Para información sobre cómo administrar las claves maestra y de solo lectura, consulte [Administración de una cuenta de Azure Cosmos DB](manage-account.md#keys).</span><span class="sxs-lookup"><span data-stu-id="77df7-182">To learn about managing master and read-only keys, see [How to manage an Azure Cosmos DB account](manage-account.md#keys).</span></span>
* <span data-ttu-id="77df7-183">Para aprender a construir tokens de autorización de Azure Cosmos DB, consulte [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources) (Control de acceso en recursos de Azure Cosmos DB).</span><span class="sxs-lookup"><span data-stu-id="77df7-183">To learn how to construct Azure Cosmos DB authorization tokens, see [Access Control on Azure Cosmos DB Resources](https://docs.microsoft.com/rest/api/documentdb/access-control-on-documentdb-resources).</span></span>
