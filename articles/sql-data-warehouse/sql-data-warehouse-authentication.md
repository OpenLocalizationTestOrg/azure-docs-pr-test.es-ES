---
title: "Autenticación a Azure SQL Data Warehouse | Microsoft Docs"
description: "Autenticación de Azure Active Directory (AAD) y SQL Server a Almacenamiento de datos SQL de Azure"
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
ms.openlocfilehash: 92f48027051bc4aff4d6b8d66fdd6de81bba3657
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="authentication-to-azure-sql-data-warehouse"></a><span data-ttu-id="9d8d3-103">Autenticación a Almacenamiento de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="9d8d3-103">Authentication to Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="9d8d3-104">Información general sobre seguridad</span><span class="sxs-lookup"><span data-stu-id="9d8d3-104">Security Overview</span></span>](sql-data-warehouse-overview-manage-security.md)
> * [<span data-ttu-id="9d8d3-105">Autenticación</span><span class="sxs-lookup"><span data-stu-id="9d8d3-105">Authentication</span></span>](sql-data-warehouse-authentication.md)
> * [<span data-ttu-id="9d8d3-106">Cifrado (Portal)</span><span class="sxs-lookup"><span data-stu-id="9d8d3-106">Encryption (Portal)</span></span>](sql-data-warehouse-encryption-tde.md)
> * [<span data-ttu-id="9d8d3-107">Cifrado (T-SQL)</span><span class="sxs-lookup"><span data-stu-id="9d8d3-107">Encryption (T-SQL)</span></span>](sql-data-warehouse-encryption-tde-tsql.md)
> 
> 

<span data-ttu-id="9d8d3-108">Para conectarse a Almacenamiento de datos SQL, debe transmitir las credenciales de seguridad para realizar la autenticación.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-108">To connect to SQL Data Warehouse, you must pass in security credentials for authentication purposes.</span></span> <span data-ttu-id="9d8d3-109">Después de establecer una conexión, determinados valores de conexión se configuran como parte del establecimiento de la sesión de la consulta.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-109">Upon establishing a connection, certain connection settings are configured as part of establishing your query session.</span></span>  

<span data-ttu-id="9d8d3-110">Para obtener más información sobre la seguridad y cómo habilitar las conexiones a su almacenamiento de datos, consulte [Proteger una base de datos en SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span><span class="sxs-lookup"><span data-stu-id="9d8d3-110">For more information on security and how to enable connections to your data warehouse, see [Secure a database in SQL Data Warehouse][Secure a database in SQL Data Warehouse].</span></span>

## <a name="sql-authentication"></a><span data-ttu-id="9d8d3-111">Autenticación de SQL</span><span class="sxs-lookup"><span data-stu-id="9d8d3-111">SQL authentication</span></span>
<span data-ttu-id="9d8d3-112">Para conectarse a Almacenamiento de datos SQL, debe proporcionar la información siguiente:</span><span class="sxs-lookup"><span data-stu-id="9d8d3-112">To connect to SQL Data Warehouse, you must provide the following information:</span></span>

* <span data-ttu-id="9d8d3-113">Nombre de servidor completo</span><span class="sxs-lookup"><span data-stu-id="9d8d3-113">Fully qualified servername</span></span>
* <span data-ttu-id="9d8d3-114">Especificar la autenticación de SQL</span><span class="sxs-lookup"><span data-stu-id="9d8d3-114">Specify SQL authentication</span></span>
* <span data-ttu-id="9d8d3-115">Nombre de usuario</span><span class="sxs-lookup"><span data-stu-id="9d8d3-115">Username</span></span>
* <span data-ttu-id="9d8d3-116">Password</span><span class="sxs-lookup"><span data-stu-id="9d8d3-116">Password</span></span>
* <span data-ttu-id="9d8d3-117">Base de datos predeterminada (opcional)</span><span class="sxs-lookup"><span data-stu-id="9d8d3-117">Default database (optional)</span></span>

<span data-ttu-id="9d8d3-118">De forma predeterminada, su conexión se realiza a la base de datos *maestra* y no a su base de datos de usuario.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-118">By default your connection connects to the *master* database and not your user database.</span></span> <span data-ttu-id="9d8d3-119">Para conectarse a la base de datos de usuario puede hacer dos cosas:</span><span class="sxs-lookup"><span data-stu-id="9d8d3-119">To connect to your user database, you can choose to do one of two things:</span></span>

* <span data-ttu-id="9d8d3-120">Especificar la base de datos predeterminada al registrar el servidor con el Explorador de objetos de SQL Server en SSDT, SSMS o en la cadena de conexión de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-120">Specify the default database when registering your server with the SQL Server Object Explorer in SSDT, SSMS, or in your application connection string.</span></span> <span data-ttu-id="9d8d3-121">Por ejemplo, incluya el parámetro InitialCatalog para una conexión ODBC.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-121">For example, include the InitialCatalog parameter for an ODBC connection.</span></span>
* <span data-ttu-id="9d8d3-122">Resalte la base de datos de usuario antes de crear una sesión en SSDT.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-122">Highlight the user database before creating a session in SSDT.</span></span>

> [!NOTE]
> <span data-ttu-id="9d8d3-123">La instrucción **USE MyDatabase;** de Transact-SQL no se admite para cambiar la base de datos de una conexión.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-123">The Transact-SQL statement **USE MyDatabase;** is not supported for changing the database for a connection.</span></span> <span data-ttu-id="9d8d3-124">Para instrucciones sobre cómo conectarse a SQL Data Warehouse con SSDT, consulte el artículo [Query with Visual Studio][Query with Visual Studio] (Realización de consultas con Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="9d8d3-124">For guidance connecting to SQL Data Warehouse with SSDT, refer to the [Query with Visual Studio][Query with Visual Studio] article.</span></span>
> 
> 

## <a name="azure-active-directory-aad-authentication"></a><span data-ttu-id="9d8d3-125">Autenticación de Azure Active Directory (AAD)</span><span class="sxs-lookup"><span data-stu-id="9d8d3-125">Azure Active Directory (AAD) authentication</span></span>
<span data-ttu-id="9d8d3-126">La [autenticación de Azure Active Directory][What is Azure Active Directory] es un mecanismo de conexión a SQL Data Warehouse mediante identidades de Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9d8d3-126">[Azure Active Directory][What is Azure Active Directory] authentication is a mechanism of connecting to Microsoft Azure SQL Data Warehouse by using identities in Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="9d8d3-127">Con la autenticación de Azure Active Directory puede administrar centralmente las identidades de los usuarios de la base de datos y otros servicios de Microsoft en una ubicación central.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-127">With Azure Active Directory authentication, you can centrally manage the identities of database users and other Microsoft services in one central location.</span></span> <span data-ttu-id="9d8d3-128">La administración de identificadores central ofrece un lugar único para administrar usuarios de Almacenamiento de datos SQL y simplifica la administración de permisos.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-128">Central ID management provides a single place to manage SQL Data Warehouse users and simplifies permission management.</span></span> 

### <a name="benefits"></a><span data-ttu-id="9d8d3-129">Ventajas</span><span class="sxs-lookup"><span data-stu-id="9d8d3-129">Benefits</span></span>
<span data-ttu-id="9d8d3-130">Entre las ventajas de Azure Active Directory, se incluyen:</span><span class="sxs-lookup"><span data-stu-id="9d8d3-130">Azure Active Directory benefits include:</span></span>

* <span data-ttu-id="9d8d3-131">Proporciona una alternativa a la autenticación de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-131">Provides an alternative to SQL Server authentication.</span></span>
* <span data-ttu-id="9d8d3-132">Ayuda a detener la proliferación de identidades de usuario en los servidores de base de datos.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-132">Helps stop the proliferation of user identities across database servers.</span></span>
* <span data-ttu-id="9d8d3-133">Permite la rotación de contraseñas en un solo lugar</span><span class="sxs-lookup"><span data-stu-id="9d8d3-133">Allows password rotation in a single place</span></span>
* <span data-ttu-id="9d8d3-134">Permite administrar los permisos de la base de datos con grupos externos (AAD).</span><span class="sxs-lookup"><span data-stu-id="9d8d3-134">Manage database permissions using external (AAD) groups.</span></span>
* <span data-ttu-id="9d8d3-135">Elimina el almacenamiento de contraseñas mediante la habilitación de la autenticación integrada de Windows y otras formas de autenticación compatibles con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-135">Eliminates storing passwords by enabling integrated Windows authentication and other forms of authentication supported by Azure Active Directory.</span></span>
* <span data-ttu-id="9d8d3-136">Usa usuarios de base de datos independiente para autenticar las identidades en el nivel de base de datos.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-136">Uses contained database users to authenticate identities at the database level.</span></span>
* <span data-ttu-id="9d8d3-137">Admite la autenticación basada en token para las aplicaciones que se conectan a SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-137">Supports token-based authentication for applications connecting to SQL Data Warehouse.</span></span>
* <span data-ttu-id="9d8d3-138">Admite Multi-Factor Authentication mediante autenticación universal de Active Directory para SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-138">Supports Multi-Factor authentication through Active Directory Universal Authentication for SQL Server Management Studio.</span></span> <span data-ttu-id="9d8d3-139">Para una descripción de Multi-Factor Authentication, consulte [Compatibilidad de SSMS con Azure AD MFA con Base de datos SQL y Almacenamiento de datos SQL](../sql-database/sql-database-ssms-mfa-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9d8d3-139">For a description of Multi-Factor Authentication, see [SSMS support for Azure AD MFA with SQL Database and SQL Data Warehouse](../sql-database/sql-database-ssms-mfa-authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="9d8d3-140">Azure Active Directory todavía es relativamente nuevo y tiene algunas limitaciones.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-140">Azure Active Directory is still relatively new and has some limitations.</span></span> <span data-ttu-id="9d8d3-141">Para asegurarse de que Azure Active Directory sea una buena elección para su entorno, vea [Características y limitaciones de Azure AD][Azure AD features and limitations], específicamente las consideraciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-141">To ensure that Azure Active Directory is a good fit for your environment, see [Azure AD features and limitations][Azure AD features and limitations], specifically the Additional considerations.</span></span>
> 
> 

### <a name="configuration-steps"></a><span data-ttu-id="9d8d3-142">Pasos de configuración</span><span class="sxs-lookup"><span data-stu-id="9d8d3-142">Configuration steps</span></span>
<span data-ttu-id="9d8d3-143">Siga estos pasos para configurar la autenticación de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-143">Follow these steps to configure Azure Active Directory authentication.</span></span>

1. <span data-ttu-id="9d8d3-144">Crear y rellenar un Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-144">Create and populate an Azure Active Directory</span></span>
2. <span data-ttu-id="9d8d3-145">Opcional: asociar o cambiar el Active Directory que está asociado actualmente a la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-145">Optional: Associate or change the active directory that is currently associated with your Azure Subscription</span></span>
3. <span data-ttu-id="9d8d3-146">Crear un administrador de Azure Active Directory para Almacenamiento de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-146">Create an Azure Active Directory administrator for Azure SQL Data Warehouse.</span></span>
4. <span data-ttu-id="9d8d3-147">Configurar los equipos cliente.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-147">Configure your client computers</span></span>
5. <span data-ttu-id="9d8d3-148">Crear usuarios de base de datos independiente  en la base de datos y asignados a identidades de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-148">Create contained database users in your database mapped to Azure AD identities</span></span>
6. <span data-ttu-id="9d8d3-149">Conectarse a su almacenamiento de datos mediante identidades de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-149">Connect to your data warehouse by using Azure AD identities</span></span>

<span data-ttu-id="9d8d3-150">Actualmente los usuarios de Azure Active Directory no se muestran en el Explorador de objetos de SSDT.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-150">Currently Azure Active Directory users are not shown in SSDT Object Explorer.</span></span> <span data-ttu-id="9d8d3-151">Como solución alternativa, vea los usuarios de [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d8d3-151">As a workaround, view the users in [sys.database_principals](https://msdn.microsoft.com/library/ms187328.aspx).</span></span>

### <a name="find-the-details"></a><span data-ttu-id="9d8d3-152">Búsqueda de los detalles</span><span class="sxs-lookup"><span data-stu-id="9d8d3-152">Find the details</span></span>
* <span data-ttu-id="9d8d3-153">Los pasos para configurar y usar la autenticación de Azure Active Directory son casi idénticos para Azure SQL Database y Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-153">The steps to configure and use Azure Active Directory authentication are nearly identical for Azure SQL Database and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="9d8d3-154">Siga los pasos detallados del tema [Conexión a Base de datos SQL o a Almacenamiento de datos SQL mediante autenticación de Azure Active Directory](../sql-database/sql-database-aad-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="9d8d3-154">Follow the detailed steps in the topic [Connecting to SQL Database or SQL Data Warehouse By Using Azure Active Directory Authentication](../sql-database/sql-database-aad-authentication.md).</span></span>
* <span data-ttu-id="9d8d3-155">Cree roles de base de datos personalizados y agrégueles usuarios.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-155">Create custom database roles and add users to the roles.</span></span> <span data-ttu-id="9d8d3-156">A continuación, conceda permisos específicos a los roles.</span><span class="sxs-lookup"><span data-stu-id="9d8d3-156">Then grant granular permissions to the roles.</span></span> <span data-ttu-id="9d8d3-157">Para obtener más información, consulte [Introducción a los permisos de los motores de bases de datos](https://msdn.microsoft.com/library/mt667986.aspx).</span><span class="sxs-lookup"><span data-stu-id="9d8d3-157">For more information, see [Getting Started with Database Engine Permissions](https://msdn.microsoft.com/library/mt667986.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9d8d3-158">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9d8d3-158">Next steps</span></span>
<span data-ttu-id="9d8d3-159">Para empezar a realizar consultas en el almacenamiento de datos con Visual Studio y otras aplicaciones, consulte [Query with Visual Studio][Query with Visual Studio] (Realización de consultas con Visual Studio).</span><span class="sxs-lookup"><span data-stu-id="9d8d3-159">To start querying your data warehouse with Visual Studio and other applications, see [Query with Visual Studio][Query with Visual Studio].</span></span>

<!-- Article references -->
[Secure a database in SQL Data Warehouse]: ./sql-data-warehouse-overview-manage-security.md
[Query with Visual Studio]: ./sql-data-warehouse-query-visual-studio.md
[What is Azure Active Directory]: ../active-directory/active-directory-whatis.md
[Azure AD features and limitations]: ../sql-database/sql-database-aad-authentication.md#azure-ad-features-and-limitations
