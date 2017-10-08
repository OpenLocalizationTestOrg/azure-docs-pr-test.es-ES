---
title: "Tutorial: Creación de una aplicación web con una base de datos multiempresa mediante Entity Framework y la seguridad de nivel de fila"
description: "Obtenga información acerca de cómo toodevelop un 5 de MVC de ASP.NET web app con la base de datos SQL backent, mediante Entity Framework y seguridad de nivel de fila de varios inquilinos."
metakeywords: azure asp.net mvc entity framework multi tenant row level security rls sql database
services: app-service\web
documentationcenter: .net
manager: jeffreyg
author: tmullaney
ms.assetid: 8fdc47a5-6fc3-4d29-ab6a-33e79f50699f
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 04/25/2016
ms.author: thmullan
ms.openlocfilehash: 1b715e01807032c3f6497c374ce427dd762af141
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a><span data-ttu-id="9fd2d-103">Tutorial: Creación de una aplicación web con una base de datos multiempresa mediante Entity Framework y la seguridad de nivel de fila</span><span class="sxs-lookup"><span data-stu-id="9fd2d-103">Tutorial: Web app with a multi-tenant database using Entity Framework and Row-Level Security</span></span>
<span data-ttu-id="9fd2d-104">Este tutorial muestra cómo toobuild de varios inquilinos web app con un "[base de datos compartida, esquema compartido](https://msdn.microsoft.com/library/aa479086.aspx)" modelo de inquilinos, mediante Entity Framework y [seguridad de nivel de fila](https://msdn.microsoft.com/library/dn765131.aspx).</span><span class="sxs-lookup"><span data-stu-id="9fd2d-104">This tutorial shows how toobuild a multi-tenant web app with a "[shared database, shared schema](https://msdn.microsoft.com/library/aa479086.aspx)" tenancy model, using Entity Framework and [Row-Level Security](https://msdn.microsoft.com/library/dn765131.aspx).</span></span> <span data-ttu-id="9fd2d-105">En este modelo, una sola base de datos contiene datos de muchos inquilinos, y cada fila de cada tabla está asociada a un "identificador de inquilino".</span><span class="sxs-lookup"><span data-stu-id="9fd2d-105">In this model, a single database contains data for many tenants, and each row in each table is associated with a "Tenant ID."</span></span> <span data-ttu-id="9fd2d-106">Seguridad de nivel de fila (RLS), una nueva característica de base de datos de SQL Azure, es usado tooprevent inquilinos tengan acceso a datos de todas las demás.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-106">Row-Level Security (RLS), a new feature for Azure SQL Database, is used tooprevent tenants from accessing each other's data.</span></span> <span data-ttu-id="9fd2d-107">Esto requiere solo una único, pequeño cambio toohello la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-107">This requires just a single, small change toohello application.</span></span> <span data-ttu-id="9fd2d-108">¡¡¡¡Centralizando la lógica de acceso inquilino de Hola de hello base de datos, RLS simplifica el código de la aplicación hello y reduce el riesgo de hello accidental de pérdida de datos entre los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-108">By centralizing hello tenant access logic within hello database itself, RLS simplifies hello application code and reduces hello risk of accidental data leakage between tenants.</span></span>

<span data-ttu-id="9fd2d-109">Comenzaremos con la aplicación de hello simple póngase en contacto con el Administrador de [crear una aplicación de MVP de ASP.NET con la autenticación y la base de datos SQL e implementar tooAzure servicio de aplicaciones](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="9fd2d-109">Let's start with hello simple Contact Manager application from [Create an ASP.NET MVP app with auth and SQL DB and deploy tooAzure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span> <span data-ttu-id="9fd2d-110">Derecho ahora, aplicación hello permite toosee de todos los usuarios (inquilinos) todos los contactos:</span><span class="sxs-lookup"><span data-stu-id="9fd2d-110">Right now, hello application allows all users (tenants) toosee all contacts:</span></span>

![Aplicación de Contact Manager antes de habilitar RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

<span data-ttu-id="9fd2d-112">Con tan solo unos pequeños cambios, se agregará compatibilidad para varios inquilinos, para que los usuarios puede toosee sólo Hola los contactos que pertenecen toothem.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-112">With just a few small changes, we will add support for multi-tenancy, so that users are able toosee only hello contacts that belong toothem.</span></span>

## <a name="step-1-add-an-interceptor-class-in-hello-application-tooset-hello-sessioncontext"></a><span data-ttu-id="9fd2d-113">Paso 1: Agregar una clase de Interceptor Hola tooset de aplicación hello SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="9fd2d-113">Step 1: Add an Interceptor class in hello application tooset hello SESSION_CONTEXT</span></span>
<span data-ttu-id="9fd2d-114">Hay un cambio de aplicación es necesario toomake.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-114">There is one application change we need toomake.</span></span> <span data-ttu-id="9fd2d-115">Dado que todos los usuarios de aplicación conectarán toohello base de datos mediante Hola misma cadena de conexión (es decir, mismo inicio de sesión SQL), actualmente no hay ninguna manera de que un tooknow de directivas RLS que el usuario debe utilizar un filtro para.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-115">Because all application users connect toohello database using hello same connection string (i.e. same SQL login), there is currently no way for an RLS policy tooknow which user it should filter for.</span></span> <span data-ttu-id="9fd2d-116">Este enfoque es muy habitual en aplicaciones web porque habilita la agrupación de conexiones eficaz, pero significa que necesitamos otra manera tooidentify Hola actual usuario de la aplicación de base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-116">This approach is very common in web applications because it enables efficient connection pooling, but it means we need another way tooidentify hello current application user within hello database.</span></span> <span data-ttu-id="9fd2d-117">Hello solución es toohave Hola aplicación conjunto un par clave-valor para Hola UserId actual en hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) inmediatamente después de abrir una conexión, antes ejecuta ninguna de las consultas.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-117">hello solution is toohave hello application set a key-value pair for hello current UserId in hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediately after opening a connection, before it executes any queries.</span></span> <span data-ttu-id="9fd2d-118">SESSION_CONTEXT es un almacén de clave y valor de ámbito de sesión y nuestra directiva RLS usará Hola UserId almacenado en ella usuario actual de tooidentify Hola.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-118">SESSION_CONTEXT is a session-scoped key-value store, and our RLS policy will use hello UserId stored in it tooidentify hello current user.</span></span>

<span data-ttu-id="9fd2d-119">Agregaremos una [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (en concreto, un [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), una característica nueva en Entity Framework (EF) 6, conjunto de tooautomatically Hola UserId actual en hello SESSION_CONTEXT mediante la ejecución de un Instrucción de T-SQL siempre que EF abre una conexión.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-119">We will add an [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (in particular, a [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), a new feature in Entity Framework (EF) 6, tooautomatically set hello current UserId in hello SESSION_CONTEXT by executing a T-SQL statement whenever EF opens a connection.</span></span>

1. <span data-ttu-id="9fd2d-120">Abra el proyecto de ContactManager de hello en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-120">Open hello ContactManager project in Visual Studio.</span></span>
2. <span data-ttu-id="9fd2d-121">Haga doble clic en la carpeta de modelos de Hola Hola el Explorador de soluciones y elija Agregar > clase.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-121">Right-click on hello Models folder in hello Solution Explorer, and choose Add > Class.</span></span>
3. <span data-ttu-id="9fd2d-122">Clase nueva Hola el nombre "SessionContextInterceptor.cs" y haga clic en Agregar.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-122">Name hello new class "SessionContextInterceptor.cs" and click Add.</span></span>
4. <span data-ttu-id="9fd2d-123">Reemplace el contenido de Hola de SessionContextInterceptor.cs con el siguiente código de hello.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-123">Replace hello contents of SessionContextInterceptor.cs with hello following code.</span></span>

```
using System;
using System.Collections.Generic;
using System.Linq;
using System.Web;
using System.Data.Common;
using System.Data.Entity;
using System.Data.Entity.Infrastructure.Interception;
using Microsoft.AspNet.Identity;

namespace ContactManager.Models
{
    public class SessionContextInterceptor : IDbConnectionInterceptor
    {
        public void Opened(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
            // Set SESSION_CONTEXT toocurrent UserId whenever EF opens a connection
            try
            {
                var userId = System.Web.HttpContext.Current.User.Identity.GetUserId();
                if (userId != null)
                {
                    DbCommand cmd = connection.CreateCommand();
                    cmd.CommandText = "EXEC sp_set_session_context @key=N'UserId', @value=@UserId";
                    DbParameter param = cmd.CreateParameter();
                    param.ParameterName = "@UserId";
                    param.Value = userId;
                    cmd.Parameters.Add(param);
                    cmd.ExecuteNonQuery();
                }
            }
            catch (System.NullReferenceException)
            {
                // If no user is logged in, leave SESSION_CONTEXT null (all rows will be filtered)
            }
        }

        public void Opening(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void BeganTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void BeginningTransaction(DbConnection connection, BeginTransactionInterceptionContext interceptionContext)
        {
        }

        public void Closed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Closing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void ConnectionStringGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSet(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionStringSetting(DbConnection connection, DbConnectionPropertyInterceptionContext<string> interceptionContext)
        {
        }

        public void ConnectionTimeoutGetting(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void ConnectionTimeoutGot(DbConnection connection, DbConnectionInterceptionContext<int> interceptionContext)
        {
        }

        public void DataSourceGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DataSourceGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void DatabaseGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void Disposed(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void Disposing(DbConnection connection, DbConnectionInterceptionContext interceptionContext)
        {
        }

        public void EnlistedTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void EnlistingTransaction(DbConnection connection, EnlistTransactionInterceptionContext interceptionContext)
        {
        }

        public void ServerVersionGetting(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void ServerVersionGot(DbConnection connection, DbConnectionInterceptionContext<string> interceptionContext)
        {
        }

        public void StateGetting(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }

        public void StateGot(DbConnection connection, DbConnectionInterceptionContext<System.Data.ConnectionState> interceptionContext)
        {
        }
    }

    public class SessionContextConfiguration : DbConfiguration
    {
        public SessionContextConfiguration()
        {
            AddInterceptor(new SessionContextInterceptor());
        }
    }
}
```

<span data-ttu-id="9fd2d-124">Que es el cambio de aplicación solo de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-124">That's hello only application change required.</span></span> <span data-ttu-id="9fd2d-125">Continúe y generar y publicar la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-125">Go ahead and build and publish hello application.</span></span>

## <a name="step-2-add-a-userid-column-toohello-database-schema"></a><span data-ttu-id="9fd2d-126">Paso 2: Agregar un esquema de base de datos de toohello de columna de identificador de usuario</span><span class="sxs-lookup"><span data-stu-id="9fd2d-126">Step 2: Add a UserId column toohello database schema</span></span>
<span data-ttu-id="9fd2d-127">A continuación, necesitamos tooadd un tooassociate de tabla de contactos de UserId columna toohello cada fila con un usuario (inquilino).</span><span class="sxs-lookup"><span data-stu-id="9fd2d-127">Next, we need tooadd a UserId column toohello Contacts table tooassociate each row with a user (tenant).</span></span> <span data-ttu-id="9fd2d-128">Se modificará el esquema de hello directamente en la base de datos de hello, para que no tengamos tooinclude este campo en nuestro modelo de datos EF.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-128">We will alter hello schema directly in hello database, so that we don't have tooinclude this field in our EF data model.</span></span>

<span data-ttu-id="9fd2d-129">Conectar directamente, toohello base de datos mediante SQL Server Management Studio o Visual Studio y, a continuación, ejecute hello después de T-SQL:</span><span class="sxs-lookup"><span data-stu-id="9fd2d-129">Connect toohello database directly, using either SQL Server Management Studio or Visual Studio, and then execute hello following T-SQL:</span></span>

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

<span data-ttu-id="9fd2d-130">Esto agrega una tabla de contactos de toohello de columna de identificador de usuario.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-130">This adds a UserId column toohello Contacts table.</span></span> <span data-ttu-id="9fd2d-131">Usamos Hola nvarchar (128) datos tipo toomatch Hola que identificadores de usuario almacenados en la tabla de hello AspNetUsers, y se crea una restricción DEFAULT que establecerá automáticamente hello UserId para las filas recién insertadas toobe Hola UserId almacenado actualmente en SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-131">We use hello nvarchar(128) data type toomatch hello UserIds stored in hello AspNetUsers table, and we create a DEFAULT constraint that will automatically set hello UserId for newly inserted rows toobe hello UserId currently stored in SESSION_CONTEXT.</span></span>

<span data-ttu-id="9fd2d-132">Ahora Hola tabla tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="9fd2d-132">Now hello table looks like this:</span></span>

![Tabla Contactos de SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

<span data-ttu-id="9fd2d-134">Cuando se crean nuevos contactos, le asignarán automáticamente Hola corregir UserId.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-134">When new contacts are created, they'll automatically be assigned hello correct UserId.</span></span> <span data-ttu-id="9fd2d-135">Con fines de demostración, sin embargo, vamos a asignar a algunos de estos tooan contactos existentes existente de usuario.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-135">For demo purposes, however, let's assign a few of these existing contacts tooan existing user.</span></span>

<span data-ttu-id="9fd2d-136">Si ha creado a determinados usuarios en la aplicación hello ya (p. ej., uso local, Google o Facebook cuentas), podrá verlas en la tabla de AspNetUsers Hola.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-136">If you've created a few users in hello application already (e.g., using local, Google, or Facebook accounts), you'll see them in hello AspNetUsers table.</span></span> <span data-ttu-id="9fd2d-137">En la siguiente captura de pantalla de hello, hay solo un usuario hasta ahora.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-137">In hello screenshot below, there is only one user so far.</span></span>

![Tabla AspNetUsers de SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

<span data-ttu-id="9fd2d-139">Hola copia Id. de user1@contoso.comy péguela en la instrucción de hello T-SQL siguiente.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-139">Copy hello Id for user1@contoso.com, and paste it into hello T-SQL statement below.</span></span> <span data-ttu-id="9fd2d-140">Ejecute esta instrucción tooassociate tres de hello contactos con este identificador de usuario.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-140">Execute this statement tooassociate three of hello Contacts with this UserId.</span></span>

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-hello-database"></a><span data-ttu-id="9fd2d-141">Paso 3: Crear una directiva de seguridad de nivel de fila en la base de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="9fd2d-141">Step 3: Create a Row-Level Security policy in hello database</span></span>
<span data-ttu-id="9fd2d-142">Hola último paso es toocreate una directiva de seguridad que utiliza Hola UserId en SESSION_CONTEXT tooautomatically filtro Hola resultados devueltos por las consultas.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-142">hello final step is toocreate a security policy that uses hello UserId in SESSION_CONTEXT tooautomatically filter hello results returned by queries.</span></span>

<span data-ttu-id="9fd2d-143">Mientras sigue conectado toohello de base de datos, ejecute hello después de T-SQL:</span><span class="sxs-lookup"><span data-stu-id="9fd2d-143">While still connected toohello database, execute hello following T-SQL:</span></span>

```
CREATE SCHEMA Security
go

CREATE FUNCTION Security.userAccessPredicate(@UserId nvarchar(128))
    RETURNS TABLE
    WITH SCHEMABINDING
AS
    RETURN SELECT 1 AS accessResult
    WHERE @UserId = CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
go

CREATE SECURITY POLICY Security.userSecurityPolicy
    ADD FILTER PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts,
    ADD BLOCK PREDICATE Security.userAccessPredicate(UserId) ON dbo.Contacts
go

```

<span data-ttu-id="9fd2d-144">Este código hace tres cosas.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-144">This code does three things.</span></span> <span data-ttu-id="9fd2d-145">En primer lugar, se crea un esquema nuevo como un procedimiento recomendado para centralizar y limitar el acceso toohello RLS objetos.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-145">First, it creates a new schema as a best practice for centralizing and limiting access toohello RLS objects.</span></span> <span data-ttu-id="9fd2d-146">A continuación, crea una función de predicado que devolverá '1' cuando Hola UserId de una fila coincide con hello UserId en SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-146">Next, it creates a predicate function that will return '1' when hello UserId of a row matches hello UserId in SESSION_CONTEXT.</span></span> <span data-ttu-id="9fd2d-147">Por último, crea una directiva de seguridad que agregue esta función como predicado de filtro y de bloqueo en la tabla de contactos de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-147">Finally, it creates a security policy that adds this function as both a filter and block predicate on hello Contacts table.</span></span> <span data-ttu-id="9fd2d-148">predicado de filtro de Hello provoca tooreturn consultas solo las filas que pertenecen el usuario actual toohello; predicado block que Hola actúa como una aplicación de protección tooprevent hello alguna vez accidentalmente inserte una fila por usuario equivocada Hola.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-148">hello filter predicate causes queries tooreturn only rows that belong toohello current user, and hello block predicate acts as a safeguard tooprevent hello application from ever accidentally inserting a row for hello wrong user.</span></span>

<span data-ttu-id="9fd2d-149">Ahora ejecute la aplicación hello e inicie sesión como user1@contoso.com. Ahora, este usuario ve únicamente los contactos de hello asignamos toothis UserId:</span><span class="sxs-lookup"><span data-stu-id="9fd2d-149">Now run hello application, and sign in as user1@contoso.com. This user now sees only hello Contacts we assigned toothis UserId earlier:</span></span>

![Aplicación de Contact Manager antes de habilitar RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

<span data-ttu-id="9fd2d-151">toovalidate este aún más, intente registrar un usuario nuevo.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-151">toovalidate this further, try registering a new user.</span></span> <span data-ttu-id="9fd2d-152">No verán ningún contacto, porque no se han asignado toothem.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-152">They will see no contacts, because none have been assigned toothem.</span></span> <span data-ttu-id="9fd2d-153">Si crea un nuevo contacto, se le asignará toothem y sólo estarán toosee capaz de él.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-153">If they create a new contact, it will be assigned toothem, and only they will be able toosee it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9fd2d-154">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9fd2d-154">Next steps</span></span>
<span data-ttu-id="9fd2d-155">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-155">That's it!</span></span> <span data-ttu-id="9fd2d-156">aplicación de Hello simple póngase en contacto con el administrador web se ha convertido en uno que cada usuario tiene su propia lista de contactos de varios inquilinos.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-156">hello simple Contact Manager web app has been converted into a multi-tenant one where each user has its own contact list.</span></span> <span data-ttu-id="9fd2d-157">Mediante la seguridad de nivel de fila, nos hemos evitar complejidad Hola de aplicar la lógica de acceso de inquilino en el código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-157">By using Row-Level Security, we've avoided hello complexity of enforcing tenant access logic in our application code.</span></span> <span data-ttu-id="9fd2d-158">Esta transparencia permite toofocus de aplicación hello en el problema en cuestión de hello empresariales reales, y también reduce el riesgo de Hola de pérdida accidental de datos como aplicación hello código base del crece.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-158">This transparency allows hello application toofocus on hello real business problem at hand, and it also reduces hello risk of accidentally leaking data as hello application's codebase grows.</span></span>

<span data-ttu-id="9fd2d-159">Este tutorial tiene solo un Hola arañado superficie de lo que es posible con RLS.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-159">This tutorial has only scratched hello surface of what's possible with RLS.</span></span> <span data-ttu-id="9fd2d-160">Por ejemplo, es posible toohave más sofisticada o la lógica de acceso granular y su posible toostore Hola algo más que un identificador de usuario actual en hello SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-160">For instance, it's possible toohave more sophisticated or granular access logic, and it's possible toostore more than just hello current UserId in hello SESSION_CONTEXT.</span></span> <span data-ttu-id="9fd2d-161">También es posible demasiado[integrar RLS con bibliotecas de cliente de herramientas de base de datos elástica hello](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport particiones de varios inquilinos en una capa de datos de escala horizontal.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-161">It's also possible too[integrate RLS with hello elastic database tools client libraries](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport multi-tenant shards in a scale-out data tier.</span></span>

<span data-ttu-id="9fd2d-162">Más allá de estas posibilidades, también trabajamos toomake RLS aún mejor.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-162">Beyond these possibilities, we're also working toomake RLS even better.</span></span> <span data-ttu-id="9fd2d-163">Si tiene alguna pregunta, ideas y las cosas que le gustaría toosee, háganoslo saber en comentarios de Hola.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-163">If you have any questions, ideas, or things you'd like toosee, please let us know in hello comments.</span></span> <span data-ttu-id="9fd2d-164">Agradecemos su participación.</span><span class="sxs-lookup"><span data-stu-id="9fd2d-164">We appreciate your feedback!</span></span>

