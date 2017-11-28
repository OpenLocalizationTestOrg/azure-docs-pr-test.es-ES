---
title: roles y usuarios de Azure Analysis Services de base de datos aaaManage | Documentos de Microsoft
description: "Obtenga información acerca de cómo toomanage y bases de datos roles a los usuarios en un servidor de Analysis Services en Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2ad069a6bcce11bc43347625cb32ec400d48af18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-database-roles-and-users"></a><span data-ttu-id="3b9fb-103">Administración de usuarios y roles de base de datos</span><span class="sxs-lookup"><span data-stu-id="3b9fb-103">Manage database roles and users</span></span>

<span data-ttu-id="3b9fb-104">En el nivel de base de datos de modelo de hello, todos los usuarios deben pertenecer tooa rol.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-104">At hello model database level, all users must belong tooa role.</span></span> <span data-ttu-id="3b9fb-105">Los roles definen los usuarios con permisos concretos para la base de datos de modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-105">Roles define users with particular permissions for hello model database.</span></span> <span data-ttu-id="3b9fb-106">Cualquier usuario o grupo de seguridad agrega rol tooa debe tener una cuenta en un inquilino de Azure AD en hello misma suscripción como servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-106">Any user or security group added tooa role must have an account in an Azure AD tenant in hello same subscription as hello server.</span></span>

<span data-ttu-id="3b9fb-107">Cómo definir roles es diferente dependiendo de herramienta de Hola que se usa, pero efecto hello es Hola igual.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-107">How you define roles is different depending on hello tool you use, but hello effect is hello same.</span></span>

<span data-ttu-id="3b9fb-108">Los permisos de los roles incluyen:</span><span class="sxs-lookup"><span data-stu-id="3b9fb-108">Role permissions include:</span></span>
*  <span data-ttu-id="3b9fb-109">**Administrador** -los usuarios tienen permisos completos para la base de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-109">**Administrator** - Users have full permissions for hello database.</span></span> <span data-ttu-id="3b9fb-110">Los roles de base de datos con permisos de administrador son distintos de los administradores de servidor.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-110">Database roles with Administrator permissions are different from server administrators.</span></span>
*  <span data-ttu-id="3b9fb-111">**Proceso** -los usuarios pueden conectarse tooand realizar operaciones de proceso en la base de datos de Hola y analizar los datos de la base de datos de modelo.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-111">**Process** - Users can connect tooand perform process operations on hello database, and analyze model database data.</span></span>
*  <span data-ttu-id="3b9fb-112">**Lectura** -los usuarios pueden utilizar un cliente de aplicación tooconnect tooand analizar los datos de la base de datos de modelo.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-112">**Read** -  Users can use a client application tooconnect tooand analyze model database data.</span></span>

<span data-ttu-id="3b9fb-113">Al crear un proyecto de modelo tabular, crea roles y agrega usuarios o grupos de roles de toothose mediante Administrador de roles de SSDT.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-113">When creating a tabular model project, you create roles and add users or groups toothose roles by using Role Manager in SSDT.</span></span> <span data-ttu-id="3b9fb-114">Cuando servidor tooa implementada, se usa SSMS, [cmdlets de Analysis Services PowerShell](https://msdn.microsoft.com/library/hh758425.aspx), o [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) tooadd (TMSL) o quitar roles y miembros de usuario.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-114">When deployed tooa server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) tooadd or remove roles and user members.</span></span>

## <a name="tooadd-or-manage-roles-and-users-in-ssdt"></a><span data-ttu-id="3b9fb-115">tooadd o administrar roles y usuarios en SSDT</span><span class="sxs-lookup"><span data-stu-id="3b9fb-115">tooadd or manage roles and users in SSDT</span></span>  
  
1.  <span data-ttu-id="3b9fb-116">En SSDT > **Explorador de modelos tabulares**, haga clic con el botón derecho en **Roles**.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-116">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span></span>  
  
2.  <span data-ttu-id="3b9fb-117">En **Administrador de roles**, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-117">In **Role Manager**, click **New**.</span></span>  
  
3.  <span data-ttu-id="3b9fb-118">Escriba un nombre para el rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-118">Type a name for hello role.</span></span>  
  
     <span data-ttu-id="3b9fb-119">De forma predeterminada, nombre Hola de rol predeterminado de Hola se incrementará numéricamente para cada nuevo rol.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-119">By default, hello name of hello default role is incrementally numbered for each new role.</span></span> <span data-ttu-id="3b9fb-120">Se recomienda que escribir un nombre que identifique claramente el tipo de miembro de hello, por ejemplo, administradores financieros o especialistas en recursos humanos.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-120">It's recommended you type a name that clearly identifies hello member type, for example, Finance Managers or Human Resources Specialists.</span></span>  
  
4.  <span data-ttu-id="3b9fb-121">Seleccione uno de los siguientes permisos de hello:</span><span class="sxs-lookup"><span data-stu-id="3b9fb-121">Select one of hello following permissions:</span></span>  
  
    |<span data-ttu-id="3b9fb-122">Permiso</span><span class="sxs-lookup"><span data-stu-id="3b9fb-122">Permission</span></span>|<span data-ttu-id="3b9fb-123">Descripción</span><span class="sxs-lookup"><span data-stu-id="3b9fb-123">Description</span></span>|  
    |----------------|-----------------|  
    |<span data-ttu-id="3b9fb-124">**None**</span><span class="sxs-lookup"><span data-stu-id="3b9fb-124">**None**</span></span>|<span data-ttu-id="3b9fb-125">Los miembros no pueden modificar el esquema del modelo hello y no pueden consultar los datos.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-125">Members cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="3b9fb-126">**Lectura**</span><span class="sxs-lookup"><span data-stu-id="3b9fb-126">**Read**</span></span>|<span data-ttu-id="3b9fb-127">Los miembros pueden consultar datos (según los filtros de fila) pero no pueden modificar el esquema del modelo Hola.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-127">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="3b9fb-128">**Lectura y proceso**</span><span class="sxs-lookup"><span data-stu-id="3b9fb-128">**Read and Process**</span></span>|<span data-ttu-id="3b9fb-129">Los miembros pueden consultar datos (en función de filtros de nivel de fila) y las operaciones de procesar y procesar todo de ejecución, pero no pueden modificar el esquema del modelo Hola.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-129">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify hello model schema.</span></span>|  
    |<span data-ttu-id="3b9fb-130">**Proceso**</span><span class="sxs-lookup"><span data-stu-id="3b9fb-130">**Process**</span></span>|<span data-ttu-id="3b9fb-131">Los modelos pueden ejecutar las operaciones Procesar y Procesar todo.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-131">Members can run Process and Process All operations.</span></span> <span data-ttu-id="3b9fb-132">No se puede modificar el esquema del modelo hello y no se puede consultar los datos.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-132">Cannot modify hello model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="3b9fb-133">**Administrador**</span><span class="sxs-lookup"><span data-stu-id="3b9fb-133">**Administrator**</span></span>|<span data-ttu-id="3b9fb-134">Los miembros pueden modificar el esquema del modelo de Hola y consultar todos los datos.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-134">Members can modify hello model schema and query all data.</span></span>|   
  
5.  <span data-ttu-id="3b9fb-135">Si el rol de hello es crear ha leído o permiso de lectura y procesamiento, puede agregar filtros de fila mediante una fórmula DAX.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-135">If hello role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="3b9fb-136">Haga clic en hello **filtros de fila** ficha, seleccione una tabla y, luego, haga clic en hello **filtro DAX** campo y, a continuación, escriba una fórmula DAX.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-136">Click hello **Row Filters** tab, then select a table, then click hello **DAX Filter** field, and then type a DAX formula.</span></span>
  
6.  <span data-ttu-id="3b9fb-137">Haga clic en **Miembros** > **Agregar externo**.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-137">Click **Members** > **Add External**.</span></span>  
  
8.  <span data-ttu-id="3b9fb-138">En **Agregar miembro externo**, escriba usuarios o grupos en Azure AD del inquilino por dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-138">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span></span> <span data-ttu-id="3b9fb-139">Una vez que hace clic en Aceptar y cierra el Administrador de roles, los roles y los miembros de rol aparecen en el Explorador de modelos tabulares.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-139">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span></span> 
 
     ![Roles y usuarios en el Explorador de modelos tabulares](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. <span data-ttu-id="3b9fb-141">Implementar el servidor de Analysis Services de Azure tooyour.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-141">Deploy tooyour Azure Analysis Services server.</span></span>


## <a name="tooadd-or-manage-roles-and-users-in-ssms"></a><span data-ttu-id="3b9fb-142">tooadd o administrar roles y usuarios en SSMS</span><span class="sxs-lookup"><span data-stu-id="3b9fb-142">tooadd or manage roles and users in SSMS</span></span>
<span data-ttu-id="3b9fb-143">tooadd roles y usuarios tooa implementado la base de datos de modelo, debe ser servidor toohello conectado como administrador del servidor o que ya esté en un rol de base de datos con permisos de administrador.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-143">tooadd roles and users tooa deployed model database, you must be connected toohello server as a Server administrator or already in a database role with administrator permissions.</span></span>

1. <span data-ttu-id="3b9fb-144">En el Explorador de objetos, haga clic con el botón derecho en **Rol** > **Nuevo rol**.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-144">In Object Exporer, right-click **Roles** > **New Role**.</span></span>

2. <span data-ttu-id="3b9fb-145">En **Crear rol**, escriba un nombre de rol y su descripción.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-145">In **Create Role**, enter a role name and description.</span></span>

3. <span data-ttu-id="3b9fb-146">Seleccione un permiso.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-146">Select a permission.</span></span>
   |<span data-ttu-id="3b9fb-147">Permiso</span><span class="sxs-lookup"><span data-stu-id="3b9fb-147">Permission</span></span>|<span data-ttu-id="3b9fb-148">Descripción</span><span class="sxs-lookup"><span data-stu-id="3b9fb-148">Description</span></span>|  
   |----------------|-----------------|  
   |<span data-ttu-id="3b9fb-149">**Control total (administrador)**</span><span class="sxs-lookup"><span data-stu-id="3b9fb-149">**Full control (Administrator)**</span></span>|<span data-ttu-id="3b9fb-150">Los miembros pueden modificar el esquema de modelo de hello, procesar y puede consultar todos los datos.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-150">Members can modify hello model schema, process, and can query all data.</span></span>| 
   |<span data-ttu-id="3b9fb-151">**Proceso de una base de datos**</span><span class="sxs-lookup"><span data-stu-id="3b9fb-151">**Process database**</span></span>|<span data-ttu-id="3b9fb-152">Los modelos pueden ejecutar las operaciones Procesar y Procesar todo.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-152">Members can run Process and Process All operations.</span></span> <span data-ttu-id="3b9fb-153">No se puede modificar el esquema del modelo hello y no se puede consultar los datos.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-153">Cannot modify hello model schema and cannot query data.</span></span>|  
   |<span data-ttu-id="3b9fb-154">**Lectura**</span><span class="sxs-lookup"><span data-stu-id="3b9fb-154">**Read**</span></span>|<span data-ttu-id="3b9fb-155">Los miembros pueden consultar datos (según los filtros de fila) pero no pueden modificar el esquema del modelo Hola.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-155">Members can query data (based on row filters) but cannot modify hello model schema.</span></span>|  
  
4. <span data-ttu-id="3b9fb-156">Haga clic en **Pertenencia** y, luego, escriba un usuario o grupo en Azure AD del inquilino por dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-156">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span></span>

     ![Agregar usuario](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. <span data-ttu-id="3b9fb-158">Si el rol de Hola que está creando tiene permiso de lectura, puede agregar filtros de fila mediante una fórmula DAX.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-158">If hello role you are creating has Read permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="3b9fb-159">Haga clic en **filtros de fila**, seleccione una tabla y, a continuación, escriba una fórmula DAX en hello **filtro DAX** campo.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-159">Click **Row Filters**, select a table, and then type a DAX formula in hello **DAX Filter** field.</span></span> 

## <a name="tooadd-roles-and-users-by-using-a-tmsl-script"></a><span data-ttu-id="3b9fb-160">tooadd roles y usuarios mediante un script TMSL</span><span class="sxs-lookup"><span data-stu-id="3b9fb-160">tooadd roles and users by using a TMSL script</span></span>
<span data-ttu-id="3b9fb-161">Puede ejecutar un script TMSL en la ventana XMLA de hello en SSMS o mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-161">You can run a TMSL script in hello XMLA window in SSMS or by using PowerShell.</span></span> <span data-ttu-id="3b9fb-162">Hola de uso [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) hello y comando [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) objeto.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-162">Use hello [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and hello [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span></span>

<span data-ttu-id="3b9fb-163">**Script TMSL de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="3b9fb-163">**Sample TMSL script**</span></span>

<span data-ttu-id="3b9fb-164">En este ejemplo, un usuario externo B2B y un grupo se agregan toohello de función de analista con permisos de lectura para la base de datos de hello SalesBI.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-164">In this sample, a B2B external user and a group are added toohello Analyst role with Read permissions for hello SalesBI database.</span></span> <span data-ttu-id="3b9fb-165">Ambos Hola usuario externo y grupo debe estar en el mismo inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-165">Both hello external user and group must be in same tenant Azure AD.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users tooquery hello model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="tooadd-roles-and-users-by-using-powershell"></a><span data-ttu-id="3b9fb-166">tooadd roles y usuarios con PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b9fb-166">tooadd roles and users by using PowerShell</span></span>
<span data-ttu-id="3b9fb-167">Hola [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) módulo proporciona la base de datos específica de la tarea de administración hello y cmdlets de uso general cmdlet Invoke-ASCmd que acepta un script o consulta de Tabular Model Scripting Language (TMSL).</span><span class="sxs-lookup"><span data-stu-id="3b9fb-167">hello [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and hello general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="3b9fb-168">Hola siguientes cmdlets se usa para administrar usuarios y roles de base de datos.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-168">hello following cmdlets are used for managing database roles and users.</span></span>
  
|<span data-ttu-id="3b9fb-169">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="3b9fb-169">Cmdlet</span></span>|<span data-ttu-id="3b9fb-170">Descripción</span><span class="sxs-lookup"><span data-stu-id="3b9fb-170">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="3b9fb-171">Add-RoleMember</span><span class="sxs-lookup"><span data-stu-id="3b9fb-171">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="3b9fb-172">Agregar un rol de base de datos de miembro tooa.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-172">Add a member tooa database role.</span></span>| 
|[<span data-ttu-id="3b9fb-173">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="3b9fb-173">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="3b9fb-174">Quita un miembro de un rol de base de datos.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-174">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="3b9fb-175">Invoke-ASCmd</span><span class="sxs-lookup"><span data-stu-id="3b9fb-175">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="3b9fb-176">Ejecuta un script de TMSL.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-176">Execute a TMSL script.</span></span>|

## <a name="row-filters"></a><span data-ttu-id="3b9fb-177">Filtros de fila</span><span class="sxs-lookup"><span data-stu-id="3b9fb-177">Row filters</span></span>  
<span data-ttu-id="3b9fb-178">Los filtros de fila definen las filas de una tabla que los miembros de un rol determinado pueden consultar.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-178">Row filters define which rows in a table can be queried by members of a particular role.</span></span> <span data-ttu-id="3b9fb-179">Los filtros de fila están definidos para cada tabla en un modelo mediante fórmulas DAX.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-179">Row filters are defined for each table in a model by using DAX formulas.</span></span>  
  
<span data-ttu-id="3b9fb-180">Los filtros de fila solo se pueden definir para los roles con permisos de lectura y lectura y proceso.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-180">Row filters can be defined only for roles with Read and Read and Process permissions.</span></span> <span data-ttu-id="3b9fb-181">De forma predeterminada, si no se define un filtro de fila para una tabla determinada, los miembros pueden consultar todas las filas de tabla de Hola a menos que el filtrado cruzado se aplica de otra tabla.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-181">By default, if a row filter is not defined for a particular table, members  can query all rows in hello table unless cross-filtering applies from another table.</span></span>
  
 <span data-ttu-id="3b9fb-182">Los filtros de fila requieren una fórmula DAX, que se debe evaluar tooa valor TRUE/FALSE, filas de hello toodefine que pueden ser consultadas por los miembros de ese rol concreto.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-182">Row filters require a DAX formula, which must evaluate tooa TRUE/FALSE value, toodefine hello rows that can be queried by members of that particular role.</span></span> <span data-ttu-id="3b9fb-183">No se puede consultar las filas no incluidas en hello fórmula DAX.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-183">Rows not included in hello DAX formula cannot be queried.</span></span> <span data-ttu-id="3b9fb-184">Por ejemplo, Hola tabla Customers con la siguiente expresión de filtros de fila, de hello *= clientes [Country] = "EE"*, los miembros del rol de ventas de hello solo pueden ver los clientes de Estados Unidos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-184">For example, hello Customers table with hello following row filters expression, *=Customers [Country] = “USA”*, members of hello Sales role can only see customers in hello USA.</span></span>  
  
<span data-ttu-id="3b9fb-185">Aplicar filtros de fila toohello especificada filas y filas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-185">Row filters apply toohello specified rows and related rows.</span></span> <span data-ttu-id="3b9fb-186">Si una tabla tiene varias relaciones, los filtros aplican seguridad para la relación de Hola que está activo.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-186">When a table has multiple relationships, filters apply security for hello relationship that is active.</span></span> <span data-ttu-id="3b9fb-187">Los filtros de fila forman una intersección con otros filtros de fila definidos para las tablas relacionadas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="3b9fb-187">Row filters are intersected with other row filers defined for related tables, for example:</span></span>  
  
|<span data-ttu-id="3b9fb-188">Tabla</span><span class="sxs-lookup"><span data-stu-id="3b9fb-188">Table</span></span>|<span data-ttu-id="3b9fb-189">Expresión DAX</span><span class="sxs-lookup"><span data-stu-id="3b9fb-189">DAX expression</span></span>|  
|-----------|--------------------|  
|<span data-ttu-id="3b9fb-190">Region</span><span class="sxs-lookup"><span data-stu-id="3b9fb-190">Region</span></span>|<span data-ttu-id="3b9fb-191">=Region[Country]="EE. UU."</span><span class="sxs-lookup"><span data-stu-id="3b9fb-191">=Region[Country]=”USA”</span></span>|  
|<span data-ttu-id="3b9fb-192">ProductCategory</span><span class="sxs-lookup"><span data-stu-id="3b9fb-192">ProductCategory</span></span>|<span data-ttu-id="3b9fb-193">=ProductCategory[Name]="Bicicletas"</span><span class="sxs-lookup"><span data-stu-id="3b9fb-193">=ProductCategory[Name]=”Bicycles”</span></span>|  
|<span data-ttu-id="3b9fb-194">Transacciones</span><span class="sxs-lookup"><span data-stu-id="3b9fb-194">Transactions</span></span>|<span data-ttu-id="3b9fb-195">=Transactions[Year]=2016</span><span class="sxs-lookup"><span data-stu-id="3b9fb-195">=Transactions[Year]=2016</span></span>|  
  
 <span data-ttu-id="3b9fb-196">efecto neto de Hello es miembros pueden consultar filas de datos donde es cliente de hello en Estados Unidos de hello, Hola categoría de producto sea bicycles y año de hello es 2016.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-196">hello net effect is members can query rows of data where hello customer is in hello USA, hello product category is bicycles, and hello year is 2016.</span></span> <span data-ttu-id="3b9fb-197">Los usuarios no pueden consultar las transacciones fuera de Estados Unidos de hello, las transacciones que no cumplan o transacciones no están en 2016 a menos que sean miembro de otro rol que les conceda estos permisos.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-197">Users cannot query transactions outside of hello USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span></span>
  
 <span data-ttu-id="3b9fb-198">Puede utilizar el filtro de hello, *=FALSE()*, toodeny filas de tooall de acceso para una tabla completa.</span><span class="sxs-lookup"><span data-stu-id="3b9fb-198">You can use hello filter, *=FALSE()*, toodeny access tooall rows for an entire table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b9fb-199">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3b9fb-199">Next steps</span></span>
  <span data-ttu-id="3b9fb-200">[Administración de administradores del servidor](analysis-services-server-admins.md) </span><span class="sxs-lookup"><span data-stu-id="3b9fb-200">[Manage server administrators](analysis-services-server-admins.md) </span></span>  
  [<span data-ttu-id="3b9fb-201">Administración de Azure Analysis Services con PowerShell</span><span class="sxs-lookup"><span data-stu-id="3b9fb-201">Manage Azure Analysis Services with PowerShell</span></span>](analysis-services-powershell.md)  
  [<span data-ttu-id="3b9fb-202">Referencia Tabular Model Scripting Language (TMSL)</span><span class="sxs-lookup"><span data-stu-id="3b9fb-202">Tabular Model Scripting Language (TMSL) Reference</span></span>](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

