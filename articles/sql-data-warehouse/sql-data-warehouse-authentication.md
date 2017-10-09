---
title: aaaAuthentication tooAzure almacenamiento de datos SQL | Documentos de Microsoft
description: Azure Active Directory (AAD) y SQL Server authentication tooAzure almacenamiento de datos SQL.
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
tags: 
ms.assetid: fefaaa75-2d0c-4e5d-aadb-410342d1ad73
ms.service: sql-data-warehouse
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.custom: security
ms.date: 03/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 66673ce1d4761243755254c8f64de1078a0ea82e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-tooazure-sql-data-warehouse"></a><span data-ttu-id="89af4-103">Autenticación tooAzure almacenamiento de datos SQL</span><span class="sxs-lookup"><span data-stu-id="89af4-103">Authentication tooAzure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="89af4-104">Información general sobre seguridad</span><span class="sxs-lookup"><span data-stu-id="89af4-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="89af4-105">Autenticación</span><span class="sxs-lookup"><span data-stu-id="89af4-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="89af4-106">Cifrado (Portal)</span><span class="sxs-lookup"><span data-stu-id="89af4-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="89af4-107">Cifrado (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="89af4-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="89af4-108">tooconnect tooSQL almacenamiento de datos, debe pasar las credenciales de seguridad para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="89af4-108">tooconnect tooSQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="89af4-109">Después de establecer una conexión, determinados valores de conexión se configuran como parte del establecimiento de la sesión de la consulta.</span><span class="sxs-lookup"><span data-stu-id="89af4-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="89af4-110">Para obtener más información sobre la seguridad y cómo tooenable almacenamiento de datos de las conexiones tooyour, consulte [proteger una base de datos en el almacén de datos de SQL][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="89af4-110">For more information on security and how tooenable connections tooyour data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="89af4-111">Autenticación de SQL</span><span class="sxs-lookup"><span data-stu-id="89af4-111">SQL authentication</span></span>
<span data-ttu-id="89af4-112">tooconnect tooSQL almacenamiento de datos, debe proporcionar Hola siguiente información:</span><span class="sxs-lookup"><span data-stu-id="89af4-112">tooconnect tooSQL Data Warehouse, you must provide hello following information:</span></span>

* <span data-ttu-id="89af4-113">Nombre de servidor completo</span><span class="sxs-lookup"><span data-stu-id="89af4-113">Fully qualified servername</span></span>
* <span data-ttu-id="89af4-114">Especificar la autenticación de SQL</span><span class="sxs-lookup"><span data-stu-id="89af4-114">Specify SQL authentication</span></span>
* <span data-ttu-id="89af4-115">Nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="89af4-115">Username</span></span>
* <span data-ttu-id="89af4-116">Password</span><span class="sxs-lookup"><span data-stu-id="89af4-116">Password</span></span>
* <span data-ttu-id="89af4-117">Base de datos predeterminada (opcional)</span><span class="sxs-lookup"><span data-stu-id="89af4-117">Default database (optional)</span></span>

<span data-ttu-id="89af4-118">De forma predeterminada la conexión conecta toohello *maestro* base de datos y no la base de datos de usuario.</span><span class="sxs-lookup"><span data-stu-id="89af4-118">By default your connection connects toohello *master* database and not your user database.</span></span> <span data-ttu-id="89af4-119">base de datos de usuario de tooyour tooconnect, puede elegir toodo una de estas dos cosas:</span><span class="sxs-lookup"><span data-stu-id="89af4-119">tooconnect tooyour user database, you can choose toodo one of two things:</span></span>

* <span data-ttu-id="89af4-120">Especificar base de datos de hello predeterminada al registrar el servidor con el Explorador de objetos de SQL Server en SSDT, SSMS, o en la cadena de conexión de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="89af4-120">Specify hello default database when registering your server with hello SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="89af4-121">Por ejemplo, incluir parámetro InitialCatalog de hello para una conexión ODBC.</span><span class="sxs-lookup"><span data-stu-id="89af4-121">For example, include hello InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="89af4-122">Resalte la base de datos de usuario de hello antes de crear una sesión en SSDT.</span><span class="sxs-lookup"><span data-stu-id="89af4-122">Highlight hello user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="89af4-123">Hola instrucción Transact-SQL **uso MyDatabase;** no se admite para cambiar base de datos de Hola para una conexión.</span><span class="sxs-lookup"><span data-stu-id="89af4-123">hello Transact-SQL statement **USE MyDatabase;** is not supported for changing hello database for a connection.</span></span> <span data-ttu-id="89af4-124">Para obtener instrucciones conectar tooSQL almacenamiento de datos con SSDT, consulte toohello [consulta con Visual Studio] [ Query with Visual Studio] artículo.</span><span class="sxs-lookup"><span data-stu-id="89af4-124">For guidance connecting tooSQL Data Warehouse with SSDT, refer toohello [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="89af4-125">Autenticación de Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="89af4-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="89af4-126">[Azure Active Directory] [ What is Azure Active Directory] autenticación es un mecanismo de conexión tooMicrosoft almacenamiento de datos de SQL Azure mediante el uso de identidades en Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="89af4-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting tooMicrosoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="89af4-127">Con la autenticación de Azure Active Directory, puede administrar de forma centralizada las identidades de Hola de usuarios de base de datos y otros servicios de Microsoft en una ubicación central.</span><span class="sxs-lookup"><span data-stu-id="89af4-127">With Azure Active Directory authentication, you can centrally manage hello identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="89af4-128">Administración del identificador central proporciona un único lugar a los usuarios de almacenamiento de datos SQL de toomanage y simplifica la administración de permisos.</span><span class="sxs-lookup"><span data-stu-id="89af4-128">Central ID management provides a single place toomanage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="89af4-129">Ventajas</span><span class="sxs-lookup"><span data-stu-id="89af4-129">Benefits</span></span>
<span data-ttu-id="89af4-130">Entre las ventajas de Azure Active Directory, se incluyen:</span><span class="sxs-lookup"><span data-stu-id="89af4-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="89af4-131">Proporciona una autenticación del servidor tooSQL alternativo.</span><span class="sxs-lookup"><span data-stu-id="89af4-131">Provides an alternative tooSQL Server authentication.</span></span>
* <span data-ttu-id="89af4-132">Ayuda a detener la proliferación de Hola de identidades de usuario entre los servidores de base de datos.</span><span class="sxs-lookup"><span data-stu-id="89af4-132">Helps stop hello proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="89af4-133">Permite la rotación de contraseñas en un solo lugar</span><span class="sxs-lookup"><span data-stu-id="89af4-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="89af4-134">Permite administrar los permisos de la base de datos con grupos externos (AAD).</span><span class="sxs-lookup"><span data-stu-id="89af4-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="89af4-135">Elimina el almacenamiento de contraseñas mediante la habilitación de la autenticación integrada de Windows y otras formas de autenticación compatibles con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="89af4-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="89af4-136">Usa contenido tooauthenticate identidades de los usuarios de base de datos en el nivel de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="89af4-136">Uses contained database users tooauthenticate identities at hello database level.</span></span>
* <span data-ttu-id="89af4-137">Admite la autenticación basada en autorización token de aplicaciones que se conectan tooSQL almacenamiento de datos.</span><span class="sxs-lookup"><span data-stu-id="89af4-137">Supports token-based authentication for applications connecting tooSQL Data Warehouse.</span></span>
* <span data-ttu-id="89af4-138">Admite Multi-Factor Authentication mediante autenticación universal de Active Directory para SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="89af4-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="89af4-139">Para una descripción de Multi-Factor Authentication, consulte [Compatibilidad de SSMS con Azure AD MFA con Base de datos SQL y Almacenamiento de datos SQL](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="89af4-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="89af4-140">Azure Active Directory todavía es relativamente nuevo y tiene algunas limitaciones.</span><span class="sxs-lookup"><span data-stu-id="89af4-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="89af4-141">tooensure que Azure Active Directory es una buena elección para su entorno, consulte [características de Azure AD y limitaciones][Azure AD features and limitations], concretamente Hola consideraciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="89af4-141">tooensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically hello Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="89af4-142">Pasos de configuración</span><span class="sxs-lookup"><span data-stu-id="89af4-142">Configuration steps</span></span>
<span data-ttu-id="89af4-143">Siga estos autenticación de Azure Active Directory tooconfigure pasos.</span><span class="sxs-lookup"><span data-stu-id="89af4-143">Follow these steps tooconfigure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="89af4-144">Crear y rellenar un Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="89af4-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="89af4-145">Opcional: Asociar o cambiar Hola active directory que está asociada actualmente con la suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="89af4-145">Optional: Associate or change hello active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="89af4-146">Crear un administrador de Azure Active Directory para Almacenamiento de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="89af4-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="89af4-147">Configurar los equipos cliente.</span><span class="sxs-lookup"><span data-stu-id="89af4-147">Configure your client computers</span></span>
5. <span data-ttu-id="89af4-148">Crear usuarios de base de datos independiente en la base de datos asignado tooAzure identidades de AD</span><span class="sxs-lookup"><span data-stu-id="89af4-148">Create contained database users in your database mapped tooAzure AD identities</span></span>
6. <span data-ttu-id="89af4-149">Conectar almacenamiento de datos de tooyour mediante identidades de Azure AD</span><span class="sxs-lookup"><span data-stu-id="89af4-149">Connect tooyour data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="89af4-150">Actualmente los usuarios de Azure Active Directory no se muestran en el Explorador de objetos de SSDT.</span><span class="sxs-lookup"><span data-stu-id="89af4-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="89af4-151">Como alternativa, ver los usuarios de hello en [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span><span class="sxs-lookup"><span data-stu-id="89af4-151">As a workaround, view hello users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-hello-details"></a><span data-ttu-id="89af4-152">Conocer los detalles de Hola</span><span class="sxs-lookup"><span data-stu-id="89af4-152">Find hello details</span></span>
* <span data-ttu-id="89af4-153">autenticación de Azure Active Directory de tooconfigure y el uso de los pasos de Hello son casi idénticos para la base de datos de SQL Azure y almacenamiento de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="89af4-153">hello steps tooconfigure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="89af4-154">Siga Hola detallan los pasos en el tema de hello [tooSQL de conexión base de datos o SQL datos almacenamiento mediante Azure Active Directory autenticación](../sql-database/sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="89af4-154">Follow hello detailed steps in hello topic [Connecting tooSQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="89af4-155">Crear roles de base de datos personalizada y agregue usuarios toohello funciones.</span><span class="sxs-lookup"><span data-stu-id="89af4-155">Create custom database roles and add users toohello roles.</span></span> <span data-ttu-id="89af4-156">A continuación, conceder permisos granulares toohello roles.</span><span class="sxs-lookup"><span data-stu-id="89af4-156">Then grant granular permissions toohello roles.</span></span> <span data-ttu-id="89af4-157">Para obtener más información, consulte [Introducción a los permisos de los motores de bases de datos](https://msdn.microsoft.com/library/mt667986.aspx).</span><span class="sxs-lookup"><span data-stu-id="89af4-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="89af4-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="89af4-158">Next steps</span></span>
<span data-ttu-id="89af4-159">toostart consultar el almacenamiento de datos con Visual Studio y otras aplicaciones, consulte [consulta con Visual Studio][Query with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="89af4-159">toostart querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
