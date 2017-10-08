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
# <a name="tutorial-web-app-with-a-multi-tenant-database-using-entity-framework-and-row-level-security"></a>Tutorial: Creación de una aplicación web con una base de datos multiempresa mediante Entity Framework y la seguridad de nivel de fila
Este tutorial muestra cómo toobuild de varios inquilinos web app con un "[base de datos compartida, esquema compartido](https://msdn.microsoft.com/library/aa479086.aspx)" modelo de inquilinos, mediante Entity Framework y [seguridad de nivel de fila](https://msdn.microsoft.com/library/dn765131.aspx). En este modelo, una sola base de datos contiene datos de muchos inquilinos, y cada fila de cada tabla está asociada a un "identificador de inquilino". Seguridad de nivel de fila (RLS), una nueva característica de base de datos de SQL Azure, es usado tooprevent inquilinos tengan acceso a datos de todas las demás. Esto requiere solo una único, pequeño cambio toohello la aplicación. ¡¡¡¡Centralizando la lógica de acceso inquilino de Hola de hello base de datos, RLS simplifica el código de la aplicación hello y reduce el riesgo de hello accidental de pérdida de datos entre los inquilinos.

Comenzaremos con la aplicación de hello simple póngase en contacto con el Administrador de [crear una aplicación de MVP de ASP.NET con la autenticación y la base de datos SQL e implementar tooAzure servicio de aplicaciones](web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database.md). Derecho ahora, aplicación hello permite toosee de todos los usuarios (inquilinos) todos los contactos:

![Aplicación de Contact Manager antes de habilitar RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-Before.png)

Con tan solo unos pequeños cambios, se agregará compatibilidad para varios inquilinos, para que los usuarios puede toosee sólo Hola los contactos que pertenecen toothem.

## <a name="step-1-add-an-interceptor-class-in-hello-application-tooset-hello-sessioncontext"></a>Paso 1: Agregar una clase de Interceptor Hola tooset de aplicación hello SESSION_CONTEXT
Hay un cambio de aplicación es necesario toomake. Dado que todos los usuarios de aplicación conectarán toohello base de datos mediante Hola misma cadena de conexión (es decir, mismo inicio de sesión SQL), actualmente no hay ninguna manera de que un tooknow de directivas RLS que el usuario debe utilizar un filtro para. Este enfoque es muy habitual en aplicaciones web porque habilita la agrupación de conexiones eficaz, pero significa que necesitamos otra manera tooidentify Hola actual usuario de la aplicación de base de datos de Hola. Hello solución es toohave Hola aplicación conjunto un par clave-valor para Hola UserId actual en hello [SESSION_CONTEXT](https://msdn.microsoft.com/library/mt590806) inmediatamente después de abrir una conexión, antes ejecuta ninguna de las consultas. SESSION_CONTEXT es un almacén de clave y valor de ámbito de sesión y nuestra directiva RLS usará Hola UserId almacenado en ella usuario actual de tooidentify Hola.

Agregaremos una [interceptor](https://msdn.microsoft.com/data/dn469464.aspx) (en concreto, un [DbConnectionInterceptor](https://msdn.microsoft.com/library/system.data.entity.infrastructure.interception.idbconnectioninterceptor)), una característica nueva en Entity Framework (EF) 6, conjunto de tooautomatically Hola UserId actual en hello SESSION_CONTEXT mediante la ejecución de un Instrucción de T-SQL siempre que EF abre una conexión.

1. Abra el proyecto de ContactManager de hello en Visual Studio.
2. Haga doble clic en la carpeta de modelos de Hola Hola el Explorador de soluciones y elija Agregar > clase.
3. Clase nueva Hola el nombre "SessionContextInterceptor.cs" y haga clic en Agregar.
4. Reemplace el contenido de Hola de SessionContextInterceptor.cs con el siguiente código de hello.

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

Que es el cambio de aplicación solo de hello necesario. Continúe y generar y publicar la aplicación hello.

## <a name="step-2-add-a-userid-column-toohello-database-schema"></a>Paso 2: Agregar un esquema de base de datos de toohello de columna de identificador de usuario
A continuación, necesitamos tooadd un tooassociate de tabla de contactos de UserId columna toohello cada fila con un usuario (inquilino). Se modificará el esquema de hello directamente en la base de datos de hello, para que no tengamos tooinclude este campo en nuestro modelo de datos EF.

Conectar directamente, toohello base de datos mediante SQL Server Management Studio o Visual Studio y, a continuación, ejecute hello después de T-SQL:

```
ALTER TABLE Contacts ADD UserId nvarchar(128)
    DEFAULT CAST(SESSION_CONTEXT(N'UserId') AS nvarchar(128))
```

Esto agrega una tabla de contactos de toohello de columna de identificador de usuario. Usamos Hola nvarchar (128) datos tipo toomatch Hola que identificadores de usuario almacenados en la tabla de hello AspNetUsers, y se crea una restricción DEFAULT que establecerá automáticamente hello UserId para las filas recién insertadas toobe Hola UserId almacenado actualmente en SESSION_CONTEXT.

Ahora Hola tabla tiene este aspecto:

![Tabla Contactos de SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-Contacts.png)

Cuando se crean nuevos contactos, le asignarán automáticamente Hola corregir UserId. Con fines de demostración, sin embargo, vamos a asignar a algunos de estos tooan contactos existentes existente de usuario.

Si ha creado a determinados usuarios en la aplicación hello ya (p. ej., uso local, Google o Facebook cuentas), podrá verlas en la tabla de AspNetUsers Hola. En la siguiente captura de pantalla de hello, hay solo un usuario hasta ahora.

![Tabla AspNetUsers de SSMS](./media/web-sites-dotnet-entity-framework-row-level-security/SSMS-AspNetUsers.png)

Hola copia Id. de user1@contoso.comy péguela en la instrucción de hello T-SQL siguiente. Ejecute esta instrucción tooassociate tres de hello contactos con este identificador de usuario.

```
UPDATE Contacts SET UserId = '19bc9b0d-28dd-4510-bd5e-d6b6d445f511'
WHERE ContactId IN (1, 2, 5)
```

## <a name="step-3-create-a-row-level-security-policy-in-hello-database"></a>Paso 3: Crear una directiva de seguridad de nivel de fila en la base de datos de Hola
Hola último paso es toocreate una directiva de seguridad que utiliza Hola UserId en SESSION_CONTEXT tooautomatically filtro Hola resultados devueltos por las consultas.

Mientras sigue conectado toohello de base de datos, ejecute hello después de T-SQL:

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

Este código hace tres cosas. En primer lugar, se crea un esquema nuevo como un procedimiento recomendado para centralizar y limitar el acceso toohello RLS objetos. A continuación, crea una función de predicado que devolverá '1' cuando Hola UserId de una fila coincide con hello UserId en SESSION_CONTEXT. Por último, crea una directiva de seguridad que agregue esta función como predicado de filtro y de bloqueo en la tabla de contactos de Hola. predicado de filtro de Hello provoca tooreturn consultas solo las filas que pertenecen el usuario actual toohello; predicado block que Hola actúa como una aplicación de protección tooprevent hello alguna vez accidentalmente inserte una fila por usuario equivocada Hola.

Ahora ejecute la aplicación hello e inicie sesión como user1@contoso.com. Ahora, este usuario ve únicamente los contactos de hello asignamos toothis UserId:

![Aplicación de Contact Manager antes de habilitar RLS](./media/web-sites-dotnet-entity-framework-row-level-security/ContactManagerApp-After.png)

toovalidate este aún más, intente registrar un usuario nuevo. No verán ningún contacto, porque no se han asignado toothem. Si crea un nuevo contacto, se le asignará toothem y sólo estarán toosee capaz de él.

## <a name="next-steps"></a>Pasos siguientes
Eso es todo. aplicación de Hello simple póngase en contacto con el administrador web se ha convertido en uno que cada usuario tiene su propia lista de contactos de varios inquilinos. Mediante la seguridad de nivel de fila, nos hemos evitar complejidad Hola de aplicar la lógica de acceso de inquilino en el código de aplicación. Esta transparencia permite toofocus de aplicación hello en el problema en cuestión de hello empresariales reales, y también reduce el riesgo de Hola de pérdida accidental de datos como aplicación hello código base del crece.

Este tutorial tiene solo un Hola arañado superficie de lo que es posible con RLS. Por ejemplo, es posible toohave más sofisticada o la lógica de acceso granular y su posible toostore Hola algo más que un identificador de usuario actual en hello SESSION_CONTEXT. También es posible demasiado[integrar RLS con bibliotecas de cliente de herramientas de base de datos elástica hello](../sql-database/sql-database-elastic-tools-multi-tenant-row-level-security.md) toosupport particiones de varios inquilinos en una capa de datos de escala horizontal.

Más allá de estas posibilidades, también trabajamos toomake RLS aún mejor. Si tiene alguna pregunta, ideas y las cosas que le gustaría toosee, háganoslo saber en comentarios de Hola. Agradecemos su participación.

