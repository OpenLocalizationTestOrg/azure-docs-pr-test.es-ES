---
title: "Tutorial: Creación de una aplicación web con una base de datos multiempresa mediante Entity Framework y la seguridad de nivel de fila"
description: "Aprenda a desarrollar una aplicación web de ASP.NET MVC 5 con un back-end de Base de datos SQL multiempresa, mediante Entity Framework y la seguridad de nivel de fila."
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
ms.openlocfilehash: ba1bb3d84b462dfebbb2564569517d7336bf54fd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a><span data-ttu-id="4da75-103">Tutorial: Creación de una aplicación web con una base de datos multiempresa mediante Entity Framework y la seguridad de nivel de fila</span><span class="sxs-lookup"><span data-stu-id="4da75-103">Tutorial: Web app with a multi-tenant database using Entity Framework and Row-Level Security</span></span>
<span data-ttu-id="4da75-104">En este tutorial se muestra cómo crear una aplicación web multiempresa con un modelo de arrendamiento "[base de datos compartida, esquema compartido](https://msdn.microsoft.com/library/aa479086.aspx)", con Entity Framework y la [seguridad de nivel de fila](https://msdn.microsoft.com/library/dn765131.aspx).</span><span class="sxs-lookup"><span data-stu-id="4da75-104">This tutorial shows how to build a multi-tenant web app with a "[shared database, shared schema](https://msdn.microsoft.com/library/aa479086.aspx)" tenancy model, using Entity Framework and [Row-Level Security](https://msdn.microsoft.com/library/dn765131.aspx).</span></span> <span data-ttu-id="4da75-105">En este modelo, una sola base de datos contiene datos de muchos inquilinos, y cada fila de cada tabla está asociada a un "identificador de inquilino".</span><span class="sxs-lookup"><span data-stu-id="4da75-105">In this model, a single database contains data for many tenants, and each row in each table is associated with a "Tenant ID."</span></span> <span data-ttu-id="4da75-106">La seguridad de nivel de fila (RLS), una nueva característica de Base de datos SQL de Azure, se usa para impedir que los inquilinos obtengan acceso a los datos de los demás inquilinos.</span><span class="sxs-lookup"><span data-stu-id="4da75-106">Row-Level Security (RLS), a new feature for Azure SQL Database, is used to prevent tenants from accessing each other's data.</span></span> <span data-ttu-id="4da75-107">Para ello solo es necesario realizar un pequeño cambio en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4da75-107">This requires just a single, small change to the application.</span></span> <span data-ttu-id="4da75-108">Al centralizar la lógica de acceso del inquilino dentro de la propia base de datos, RLS simplifica el código de la aplicación y reduce el riesgo de pérdidas accidentales de los datos entre los inquilinos.</span><span class="sxs-lookup"><span data-stu-id="4da75-108">By centralizing the tenant access logic within the database itself, RLS simplifies the application code and reduces the risk of accidental data leakage between tenants.</span></span>

<span data-ttu-id="4da75-109">Vamos a comenzar con la aplicación sencilla de Contact Manager de la sección [Creación de una aplicación de ASP.NET MVP con autenticación y Base de datos SQL e implementación en el Servicio de aplicaciones de Azure](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span><span class="sxs-lookup"><span data-stu-id="4da75-109">Let's start with the simple Contact Manager application from [Create an ASP.NET MVP app with auth and SQL DB and deploy to Azure App Service](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md).</span></span> <span data-ttu-id="4da75-110">Ahora mismo, la aplicación permite a todos los usuarios (inquilinos) ver todos los contactos:</span><span class="sxs-lookup"><span data-stu-id="4da75-110">Right now, the application allows all users (tenants) to see all contacts:</span></span>

![Aplicación de Contact Manager antes de habilitar RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

<span data-ttu-id="4da75-112">Con solo algunos pequeños cambios, agregaremos compatibilidad con multiempresa, de forma que los usuarios solo podrán ver los contactos que les pertenecen.</span><span class="sxs-lookup"><span data-stu-id="4da75-112">With just a few small changes, we will add support for multi-tenancy, so that users are able to see only the contacts that belong to them.</span></span>

## <a name="step-1-add-an-interceptor-class-in-the-application-to-set-the-sessioncontext"></a><span data-ttu-id="4da75-113">Paso 1: Incorporación de una clase de Interceptor en la aplicación para establecer el valor de SESSION_CONTEXT</span><span class="sxs-lookup"><span data-stu-id="4da75-113">Step 1: Add an Interceptor class in the application to set the SESSION_CONTEXT</span></span>
<span data-ttu-id="4da75-114">Solo tenemos que realizar un cambio en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4da75-114">There is one application change we need to make.</span></span> <span data-ttu-id="4da75-115">Puesto que todos los usuarios de la aplicación se conectan a la base de datos con la misma cadena de conexión (es decir, el mismo inicio de sesión SQL), no hay actualmente ninguna forma de que una directiva RSL sepa por qué usuario se debería filtrar.</span><span class="sxs-lookup"><span data-stu-id="4da75-115">Because all application users connect to the database using the same connection string (i.e. same SQL login), there is currently no way for an RLS policy to know which user it should filter for.</span></span> <span data-ttu-id="4da75-116">Este enfoque es muy común en las aplicaciones web porque permite la agrupación eficaz de conexiones, pero significa que necesitamos otra manera de identificar al usuario actual de la aplicación dentro de la base de datos.</span><span class="sxs-lookup"><span data-stu-id="4da75-116">This approach is very common in web applications because it enables efficient connection pooling, but it means we need another way to identify the current application user within the database.</span></span> <span data-ttu-id="4da75-117">La solución consiste en que la aplicación establezca un par de clave-valor para el UserId actual en [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) inmediatamente después de abrir una conexión y antes de ejecutar una consulta.</span><span class="sxs-lookup"><span data-stu-id="4da75-117">The solution is to have the application set a key-value pair for the current UserId in the [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) immediately after opening a connection, before it executes any queries.</span></span> <span data-ttu-id="4da75-118">SESSION_CONTEXT es un almacén de pares de clave-valor con ámbito de sesión, y nuestra política RLS usará el UserId almacenado en él para identificar al usuario actual.</span><span class="sxs-lookup"><span data-stu-id="4da75-118">SESSION_CONTEXT is a session-scoped key-value store, and our RLS policy will use the UserId stored in it to identify the current user.</span></span>

<span data-ttu-id="4da75-119">Agregaremos un [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (en concreto [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), una nueva característica de Entity Framework (EF) 6, para establecer automáticamente el UserId actual en SESSION_CONTEXT ejecutando una instrucción T-SQL cuando EF abra una conexión.</span><span class="sxs-lookup"><span data-stu-id="4da75-119">We will add an [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (in particular, a [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), a new feature in Entity Framework (EF) 6, to automatically set the current UserId in the SESSION_CONTEXT by executing a T-SQL statement whenever EF opens a connection.</span></span>

1. <span data-ttu-id="4da75-120">Abra el proyecto ContactManager en Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4da75-120">Open the ContactManager project in Visual Studio.</span></span>
2. <span data-ttu-id="4da75-121">Haga clic con el botón derecho en la carpeta Modelos en el Explorador de soluciones y seleccione Agregar > Clase.</span><span class="sxs-lookup"><span data-stu-id="4da75-121">Right-click on the Models folder in the Solution Explorer, and choose Add > Class.</span></span>
3. <span data-ttu-id="4da75-122">Asigne a la nueva clase el nombre "SessionContextInterceptor.cs" y haga clic en Agregar.</span><span class="sxs-lookup"><span data-stu-id="4da75-122">Name the new class "SessionContextInterceptor.cs" and click Add.</span></span>
4. <span data-ttu-id="4da75-123">Reemplace el contenido de SessionContextInterceptor.cs por el código siguiente.</span><span class="sxs-lookup"><span data-stu-id="4da75-123">Replace the contents of SessionContextInterceptor.cs with the following code.</span></span>

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
            // Set SESSION_CONTEXT to current UserId whenever EF opens a connection
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

<span data-ttu-id="4da75-124">Este es el único cambio que precisa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4da75-124">That's the only application change required.</span></span> <span data-ttu-id="4da75-125">Siga adelante y compile y publique la aplicación.</span><span class="sxs-lookup"><span data-stu-id="4da75-125">Go ahead and build and publish the application.</span></span>

## <a name="step-2-add-a-userid-column-to-the-database-schema"></a><span data-ttu-id="4da75-126">Paso 2: Incorporación de una columna UserId al esquema de base de datos</span><span class="sxs-lookup"><span data-stu-id="4da75-126">Step 2: Add a UserId column to the database schema</span></span>
<span data-ttu-id="4da75-127">A continuación, debemos agregar una columna UserId a la tabla Contactos para asociar cada fila a un usuario (inquilino).</span><span class="sxs-lookup"><span data-stu-id="4da75-127">Next, we need to add a UserId column to the Contacts table to associate each row with a user (tenant).</span></span> <span data-ttu-id="4da75-128">Modificaremos el esquema directamente en la base de datos, por lo que no tenemos que incluir este campo en nuestro modelo de datos de EF.</span><span class="sxs-lookup"><span data-stu-id="4da75-128">We will alter the schema directly in the database, so that we don't have to include this field in our EF data model.</span></span>

<span data-ttu-id="4da75-129">Conéctese a la base de datos directamente, mediante SQL Server Management Studio o Visual Studio, y luego ejecute la siguiente instrucción T-SQL:</span><span class="sxs-lookup"><span data-stu-id="4da75-129">Connect to the database directly, using either SQL Server Management Studio or Visual Studio, and then execute the following T-SQL:</span></span>

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

<span data-ttu-id="4da75-130">Se agrega una columna UserId a la tabla Contactos.</span><span class="sxs-lookup"><span data-stu-id="4da75-130">This adds a UserId column to the Contacts table.</span></span> <span data-ttu-id="4da75-131">Usamos el tipo de datos nvarchar (128) para que coincidan los UserId almacenados en la tabla AspNetUsers y creamos una restricción DEFAULT que establece automáticamente  que el UserId de las filas recién insertadas sea el UserId almacenado actualmente en SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="4da75-131">We use the nvarchar(128) data type to match the UserIds stored in the AspNetUsers table, and we create a DEFAULT constraint that will automatically set the UserId for newly inserted rows to be the UserId currently stored in SESSION_CONTEXT.</span></span>

<span data-ttu-id="4da75-132">Ahora la tabla tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="4da75-132">Now the table looks like this:</span></span>

![Tabla Contactos de SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

<span data-ttu-id="4da75-134">Cuando se creen nuevos contactos, se les asignará automáticamente el UserId correcto.</span><span class="sxs-lookup"><span data-stu-id="4da75-134">When new contacts are created, they'll automatically be assigned the correct UserId.</span></span> <span data-ttu-id="4da75-135">No obstante, con fines de demostración, vamos a asignar algunos de estos contactos existentes a un usuario existente.</span><span class="sxs-lookup"><span data-stu-id="4da75-135">For demo purposes, however, let's assign a few of these existing contacts to an existing user.</span></span>

<span data-ttu-id="4da75-136">Si ya ha creado unos cuantos usuarios en la aplicación (por ejemplo, mediante cuentas locales, de Google o de Facebook), los verá en la tabla AspNetUsers.</span><span class="sxs-lookup"><span data-stu-id="4da75-136">If you've created a few users in the application already (e.g., using local, Google, or Facebook accounts), you'll see them in the AspNetUsers table.</span></span> <span data-ttu-id="4da75-137">En la siguiente captura de pantalla, hasta el momento solo hay un usuario.</span><span class="sxs-lookup"><span data-stu-id="4da75-137">In the screenshot below, there is only one user so far.</span></span>

![Tabla AspNetUsers de SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

<span data-ttu-id="4da75-139">Copie el identificador de user1@contoso.com y péguelo en la siguiente instrucción T-SQL.</span><span class="sxs-lookup"><span data-stu-id="4da75-139">Copy the Id for user1@contoso.com, and paste it into the T-SQL statement below.</span></span> <span data-ttu-id="4da75-140">Ejecute esta instrucción para asociar tres de los contactos con este UserId.</span><span class="sxs-lookup"><span data-stu-id="4da75-140">Execute this statement to associate three of the Contacts with this UserId.</span></span>

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-the-database"></a><span data-ttu-id="4da75-141">Paso 3: Creación de una directiva de seguridad de nivel de fila en la base de datos</span><span class="sxs-lookup"><span data-stu-id="4da75-141">Step 3: Create a Row-Level Security policy in the database</span></span>
<span data-ttu-id="4da75-142">El paso final consiste en crear una directiva de seguridad que use el UserId de SESSION_CONTEXT para filtrar automáticamente los resultados devueltos por las consultas.</span><span class="sxs-lookup"><span data-stu-id="4da75-142">The final step is to create a security policy that uses the UserId in SESSION_CONTEXT to automatically filter the results returned by queries.</span></span>

<span data-ttu-id="4da75-143">Mientras sigue conectado a la base de datos, ejecute la siguiente instrucción T-SQL:</span><span class="sxs-lookup"><span data-stu-id="4da75-143">While still connected to the database, execute the following T-SQL:</span></span>

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

<span data-ttu-id="4da75-144">Este código hace tres cosas.</span><span class="sxs-lookup"><span data-stu-id="4da75-144">This code does three things.</span></span> <span data-ttu-id="4da75-145">En primer lugar, crea un nuevo esquema como procedimiento recomendado para centralizar y limitar el acceso a los objetos RLS.</span><span class="sxs-lookup"><span data-stu-id="4da75-145">First, it creates a new schema as a best practice for centralizing and limiting access to the RLS objects.</span></span> <span data-ttu-id="4da75-146">A continuación, crea una función de predicado que devolverá '1' cuando el UserId de una fila coincide con el UserId de SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="4da75-146">Next, it creates a predicate function that will return '1' when the UserId of a row matches the UserId in SESSION_CONTEXT.</span></span> <span data-ttu-id="4da75-147">Finalmente, crea una directiva de seguridad que agrega esta función como un predicado de filtro y bloqueo en la tabla Contactos.</span><span class="sxs-lookup"><span data-stu-id="4da75-147">Finally, it creates a security policy that adds this function as both a filter and block predicate on the Contacts table.</span></span> <span data-ttu-id="4da75-148">El predicado de filtro hace que las consultas solo devuelvan las filas que pertenecen al usuario actual, y el predicado de bloqueo actúa como salvaguarda para impedir que la aplicación inserte por accidente una fila para el usuario incorrecto.</span><span class="sxs-lookup"><span data-stu-id="4da75-148">The filter predicate causes queries to return only rows that belong to the current user, and the block predicate acts as a safeguard to prevent the application from ever accidentally inserting a row for the wrong user.</span></span>

<span data-ttu-id="4da75-149">Ejecute ahora la aplicación e inicie sesión como user1@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="4da75-149">Now run the application, and sign in as user1@contoso.com.</span></span> <span data-ttu-id="4da75-150">Ahora este usuario solo ve los contactos que se asignaron anteriormente a este UserId:</span><span class="sxs-lookup"><span data-stu-id="4da75-150">This user now sees only the Contacts we assigned to this UserId earlier:</span></span>

![Aplicación de Contact Manager antes de habilitar RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

<span data-ttu-id="4da75-152">Para validar esto aún más, intente registrar un nuevo usuario.</span><span class="sxs-lookup"><span data-stu-id="4da75-152">To validate this further, try registering a new user.</span></span> <span data-ttu-id="4da75-153">Este usuario no verá ningún contacto, ya que no se le ha asignado ninguno.</span><span class="sxs-lookup"><span data-stu-id="4da75-153">They will see no contacts, because none have been assigned to them.</span></span> <span data-ttu-id="4da75-154">Si dicho usuario crea un nuevo contacto, se le asignará a él, y solo él podrá verlo.</span><span class="sxs-lookup"><span data-stu-id="4da75-154">If they create a new contact, it will be assigned to them, and only they will be able to see it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4da75-155">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="4da75-155">Next steps</span></span>
<span data-ttu-id="4da75-156">Eso es todo.</span><span class="sxs-lookup"><span data-stu-id="4da75-156">That's it!</span></span> <span data-ttu-id="4da75-157">La aplicación web sencilla de Contact Manager se ha convertido en una aplicación multiempresa donde cada usuario tiene su propia lista de contactos.</span><span class="sxs-lookup"><span data-stu-id="4da75-157">The simple Contact Manager web app has been converted into a multi-tenant one where each user has its own contact list.</span></span> <span data-ttu-id="4da75-158">Mediante la seguridad de nivel de fila, hemos evitado la complejidad de aplicar lógica de acceso de inquilino a nuestro código de aplicación.</span><span class="sxs-lookup"><span data-stu-id="4da75-158">By using Row-Level Security, we've avoided the complexity of enforcing tenant access logic in our application code.</span></span> <span data-ttu-id="4da75-159">Esta transparencia permite a la aplicación centrarse en el problema empresarial real entre manos, y también reduce el riesgo de pérdida accidental de datos cuando el código base de la aplicación crece.</span><span class="sxs-lookup"><span data-stu-id="4da75-159">This transparency allows the application to focus on the real business problem at hand, and it also reduces the risk of accidentally leaking data as the application's codebase grows.</span></span>

<span data-ttu-id="4da75-160">En este tutorial solo se ha mostrado una mínima parte de lo que se puede hacer con RLS.</span><span class="sxs-lookup"><span data-stu-id="4da75-160">This tutorial has only scratched the surface of what's possible with RLS.</span></span> <span data-ttu-id="4da75-161">Por ejemplo, se puede tener una lógica de acceso más sofisticada o granular, y es posible almacenar más valores que únicamente el UserId de SESSION_CONTEXT.</span><span class="sxs-lookup"><span data-stu-id="4da75-161">For instance, it's possible to have more sophisticated or granular access logic, and it's possible to store more than just the current UserId in the SESSION_CONTEXT.</span></span> <span data-ttu-id="4da75-162">También es posible [integrar RLS con las bibliotecas de cliente de herramientas de base de datos elástica](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) para permitir particiones multiempresa en una capa de datos de escalado horizontal.</span><span class="sxs-lookup"><span data-stu-id="4da75-162">It's also possible to [integrate RLS with the elastic database tools client libraries](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) to support multi-tenant shards in a scale-out data tier.</span></span>

<span data-ttu-id="4da75-163">Al margen de estas posibilidades, también estamos trabajando para mejorar RLS más incluso.</span><span class="sxs-lookup"><span data-stu-id="4da75-163">Beyond these possibilities, we're also working to make RLS even better.</span></span> <span data-ttu-id="4da75-164">Si tiene alguna pregunta, idea o cosas que le gustaría ver, háganos llegar sus comentarios.</span><span class="sxs-lookup"><span data-stu-id="4da75-164">If you have any questions, ideas, or things you'd like to see, please let us know in the comments.</span></span> <span data-ttu-id="4da75-165">Agradecemos su participación.</span><span class="sxs-lookup"><span data-stu-id="4da75-165">We appreciate your feedback!</span></span>

