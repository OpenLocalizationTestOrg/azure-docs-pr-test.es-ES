---
title: "Administración de usuarios y roles de base de datos en Azure Analysis Services | Microsoft Docs"
description: "Obtenga información sobre cómo administrar usuarios y roles de base de datos en un servidor de Analysis Services en Azure."
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
ms.openlocfilehash: d0bc7d7514f111b4bbde33bd60ae21264bd797fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="manage-database-roles-and-users"></a><span data-ttu-id="d79e5-103">Administración de usuarios y roles de base de datos</span><span class="sxs-lookup"><span data-stu-id="d79e5-103">Manage database roles and users</span></span>

<span data-ttu-id="d79e5-104">En el nivel de base de datos modelo, todos los usuarios deben pertenecer a un rol.</span><span class="sxs-lookup"><span data-stu-id="d79e5-104">At the model database level, all users must belong to a role.</span></span> <span data-ttu-id="d79e5-105">Los roles definen a los usuarios con permisos concretos para la base de datos modelo.</span><span class="sxs-lookup"><span data-stu-id="d79e5-105">Roles define users with particular permissions for the model database.</span></span> <span data-ttu-id="d79e5-106">Cualquier usuario o grupo de seguridad que se agregue a un rol debe tener una cuenta en un inquilino de Azure AD en la misma suscripción que el servidor.</span><span class="sxs-lookup"><span data-stu-id="d79e5-106">Any user or security group added to a role must have an account in an Azure AD tenant in the same subscription as the server.</span></span>

<span data-ttu-id="d79e5-107">La forma en que se definen los roles es distinta en función de la herramienta que se usa, pero el efecto es el mismo.</span><span class="sxs-lookup"><span data-stu-id="d79e5-107">How you define roles is different depending on the tool you use, but the effect is the same.</span></span>

<span data-ttu-id="d79e5-108">Los permisos de los roles incluyen:</span><span class="sxs-lookup"><span data-stu-id="d79e5-108">Role permissions include:</span></span>
*  <span data-ttu-id="d79e5-109">**Administrador**: usuarios con permisos totales para la base de datos.</span><span class="sxs-lookup"><span data-stu-id="d79e5-109">**Administrator** - Users have full permissions for the database.</span></span> <span data-ttu-id="d79e5-110">Los roles de base de datos con permisos de administrador son distintos de los administradores de servidor.</span><span class="sxs-lookup"><span data-stu-id="d79e5-110">Database roles with Administrator permissions are different from server administrators.</span></span>
*  <span data-ttu-id="d79e5-111">**Proceso**: usuarios que se pueden conectar a la base de datos y realizan operaciones de proceso en ella, además de analizar los datos de base de datos modelo.</span><span class="sxs-lookup"><span data-stu-id="d79e5-111">**Process** - Users can connect to and perform process operations on the database, and analyze model database data.</span></span>
*  <span data-ttu-id="d79e5-112">**Lectura**: usuarios que pueden usar una aplicación cliente para conectarse a los datos de una base de datos modelo y analizarlo.</span><span class="sxs-lookup"><span data-stu-id="d79e5-112">**Read** -  Users can use a client application to connect to and analyze model database data.</span></span>

<span data-ttu-id="d79e5-113">Cuando se crea un proyecto de modelo tabular, crea roles y agrega usuarios o grupos a esos roles mediante el Administrador de roles de SSDT.</span><span class="sxs-lookup"><span data-stu-id="d79e5-113">When creating a tabular model project, you create roles and add users or groups to those roles by using Role Manager in SSDT.</span></span> <span data-ttu-id="d79e5-114">Cuando se implementa en un servidor, se usa SSMS, [cmdlets de PowerShell para Analysis Services](https://msdn.microsoft.com/library/hh758425.aspx) o [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) para agregar o quitar roles de miembros de usuario.</span><span class="sxs-lookup"><span data-stu-id="d79e5-114">When deployed to a server, you use SSMS, [Analysis Services PowerShell cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), or [Tabular Model Scripting Language](https://msdn.microsoft.com/library/mt614797.aspx) (TMSL) to add or remove roles and user members.</span></span>

## <a name="to-add-or-manage-roles-and-users-in-ssdt"></a><span data-ttu-id="d79e5-115">Para agregar o administrar roles y usuarios en SSDT</span><span class="sxs-lookup"><span data-stu-id="d79e5-115">To add or manage roles and users in SSDT</span></span>  
  
1.  <span data-ttu-id="d79e5-116">En SSDT > **Explorador de modelos tabulares**, haga clic con el botón derecho en **Roles**.</span><span class="sxs-lookup"><span data-stu-id="d79e5-116">In SSDT > **Tabular Model Explorer**, right-click **Roles**.</span></span>  
  
2.  <span data-ttu-id="d79e5-117">En **Administrador de roles**, haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="d79e5-117">In **Role Manager**, click **New**.</span></span>  
  
3.  <span data-ttu-id="d79e5-118">Escriba un nombre para el rol.</span><span class="sxs-lookup"><span data-stu-id="d79e5-118">Type a name for the role.</span></span>  
  
     <span data-ttu-id="d79e5-119">De manera predeterminada, el nombre del rol predeterminado se enumera de manera incremental para cada rol nuevo.</span><span class="sxs-lookup"><span data-stu-id="d79e5-119">By default, the name of the default role is incrementally numbered for each new role.</span></span> <span data-ttu-id="d79e5-120">Se recomienda que escriba un nombre que identifique de forma clara el tipo de miembro, por ejemplo, Administrador financiero o Especialistas en recursos humanos.</span><span class="sxs-lookup"><span data-stu-id="d79e5-120">It's recommended you type a name that clearly identifies the member type, for example, Finance Managers or Human Resources Specialists.</span></span>  
  
4.  <span data-ttu-id="d79e5-121">Seleccione uno de estos permisos:</span><span class="sxs-lookup"><span data-stu-id="d79e5-121">Select one of the following permissions:</span></span>  
  
    |<span data-ttu-id="d79e5-122">Permiso</span><span class="sxs-lookup"><span data-stu-id="d79e5-122">Permission</span></span>|<span data-ttu-id="d79e5-123">Descripción</span><span class="sxs-lookup"><span data-stu-id="d79e5-123">Description</span></span>|  
    |----------------|-----------------|  
    |<span data-ttu-id="d79e5-124">**None**</span><span class="sxs-lookup"><span data-stu-id="d79e5-124">**None**</span></span>|<span data-ttu-id="d79e5-125">Los miembros no pueden modificar el esquema de modelo ni tampoco consultar datos.</span><span class="sxs-lookup"><span data-stu-id="d79e5-125">Members cannot modify the model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="d79e5-126">**Lectura**</span><span class="sxs-lookup"><span data-stu-id="d79e5-126">**Read**</span></span>|<span data-ttu-id="d79e5-127">Los miembros pueden consultar datos (según los filtros de fila), pero no pueden modificar el esquema de modelo.</span><span class="sxs-lookup"><span data-stu-id="d79e5-127">Members can query data (based on row filters) but cannot modify the model schema.</span></span>|  
    |<span data-ttu-id="d79e5-128">**Lectura y proceso**</span><span class="sxs-lookup"><span data-stu-id="d79e5-128">**Read and Process**</span></span>|<span data-ttu-id="d79e5-129">Los miembros pueden consultar datos (según los filtros de nivel de fila) y ejecutar las operaciones Procesar y Procesar todo, pero no pueden modificar el esquema de modelo.</span><span class="sxs-lookup"><span data-stu-id="d79e5-129">Members can query data (based on row-level filters) and run Process and Process All operations, but cannot modify the model schema.</span></span>|  
    |<span data-ttu-id="d79e5-130">**Proceso**</span><span class="sxs-lookup"><span data-stu-id="d79e5-130">**Process**</span></span>|<span data-ttu-id="d79e5-131">Los modelos pueden ejecutar las operaciones Procesar y Procesar todo.</span><span class="sxs-lookup"><span data-stu-id="d79e5-131">Members can run Process and Process All operations.</span></span> <span data-ttu-id="d79e5-132">No pueden modificar el esquema de modelo ni pueden consultar datos.</span><span class="sxs-lookup"><span data-stu-id="d79e5-132">Cannot modify the model schema and cannot query data.</span></span>|  
    |<span data-ttu-id="d79e5-133">**Administrador**</span><span class="sxs-lookup"><span data-stu-id="d79e5-133">**Administrator**</span></span>|<span data-ttu-id="d79e5-134">Los miembros pueden modificar el esquema de modelo y consultar todos los datos.</span><span class="sxs-lookup"><span data-stu-id="d79e5-134">Members can modify the model schema and query all data.</span></span>|   
  
5.  <span data-ttu-id="d79e5-135">Si el rol que crea tiene permiso de Lectura o Lectura y proceso, puede agregar filtros de fila mediante una fórmula DAX.</span><span class="sxs-lookup"><span data-stu-id="d79e5-135">If the role you are creating has Read or Read and Process permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="d79e5-136">Haga clic en la pestaña **Filtros de fila**, seleccione una tabla y, luego, haga clic en el campo **Filtro DAX** y escriba una fórmula DAX.</span><span class="sxs-lookup"><span data-stu-id="d79e5-136">Click the **Row Filters** tab, then select a table, then click the **DAX Filter** field, and then type a DAX formula.</span></span>
  
6.  <span data-ttu-id="d79e5-137">Haga clic en **Miembros** > **Agregar externo**.</span><span class="sxs-lookup"><span data-stu-id="d79e5-137">Click **Members** > **Add External**.</span></span>  
  
8.  <span data-ttu-id="d79e5-138">En **Agregar miembro externo**, escriba usuarios o grupos en Azure AD del inquilino por dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="d79e5-138">In **Add External Member**, enter users or groups in your tenant Azure AD by email address.</span></span> <span data-ttu-id="d79e5-139">Una vez que hace clic en Aceptar y cierra el Administrador de roles, los roles y los miembros de rol aparecen en el Explorador de modelos tabulares.</span><span class="sxs-lookup"><span data-stu-id="d79e5-139">After you click OK and close Role Manager, roles and role members appear in Tabular Model Explorer.</span></span> 
 
     ![Roles y usuarios en el Explorador de modelos tabulares](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. <span data-ttu-id="d79e5-141">Implemente el servidor de Azure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="d79e5-141">Deploy to your Azure Analysis Services server.</span></span>


## <a name="to-add-or-manage-roles-and-users-in-ssms"></a><span data-ttu-id="d79e5-142">Para agregar o administrar roles y usuarios en SSMS</span><span class="sxs-lookup"><span data-stu-id="d79e5-142">To add or manage roles and users in SSMS</span></span>
<span data-ttu-id="d79e5-143">Para agregar roles y usuarios a una base de datos modelo implementada, debe estar conectado al servidor como administrador del servidor y ya debe tener un rol de base de datos con permisos de administrador.</span><span class="sxs-lookup"><span data-stu-id="d79e5-143">To add roles and users to a deployed model database, you must be connected to the server as a Server administrator or already in a database role with administrator permissions.</span></span>

1. <span data-ttu-id="d79e5-144">En el Explorador de objetos, haga clic con el botón derecho en **Rol** > **Nuevo rol**.</span><span class="sxs-lookup"><span data-stu-id="d79e5-144">In Object Exporer, right-click **Roles** > **New Role**.</span></span>

2. <span data-ttu-id="d79e5-145">En **Crear rol**, escriba un nombre de rol y su descripción.</span><span class="sxs-lookup"><span data-stu-id="d79e5-145">In **Create Role**, enter a role name and description.</span></span>

3. <span data-ttu-id="d79e5-146">Seleccione un permiso.</span><span class="sxs-lookup"><span data-stu-id="d79e5-146">Select a permission.</span></span>
   |<span data-ttu-id="d79e5-147">Permiso</span><span class="sxs-lookup"><span data-stu-id="d79e5-147">Permission</span></span>|<span data-ttu-id="d79e5-148">Descripción</span><span class="sxs-lookup"><span data-stu-id="d79e5-148">Description</span></span>|  
   |----------------|-----------------|  
   |<span data-ttu-id="d79e5-149">**Control total (administrador)**</span><span class="sxs-lookup"><span data-stu-id="d79e5-149">**Full control (Administrator)**</span></span>|<span data-ttu-id="d79e5-150">Los miembros pueden modificar el esquema modelo, el proceso y pueden consultar todos los datos.</span><span class="sxs-lookup"><span data-stu-id="d79e5-150">Members can modify the model schema, process, and can query all data.</span></span>| 
   |<span data-ttu-id="d79e5-151">**Proceso de una base de datos**</span><span class="sxs-lookup"><span data-stu-id="d79e5-151">**Process database**</span></span>|<span data-ttu-id="d79e5-152">Los modelos pueden ejecutar las operaciones Procesar y Procesar todo.</span><span class="sxs-lookup"><span data-stu-id="d79e5-152">Members can run Process and Process All operations.</span></span> <span data-ttu-id="d79e5-153">No pueden modificar el esquema de modelo ni pueden consultar datos.</span><span class="sxs-lookup"><span data-stu-id="d79e5-153">Cannot modify the model schema and cannot query data.</span></span>|  
   |<span data-ttu-id="d79e5-154">**Lectura**</span><span class="sxs-lookup"><span data-stu-id="d79e5-154">**Read**</span></span>|<span data-ttu-id="d79e5-155">Los miembros pueden consultar datos (según los filtros de fila), pero no pueden modificar el esquema de modelo.</span><span class="sxs-lookup"><span data-stu-id="d79e5-155">Members can query data (based on row filters) but cannot modify the model schema.</span></span>|  
  
4. <span data-ttu-id="d79e5-156">Haga clic en **Pertenencia** y, luego, escriba un usuario o grupo en Azure AD del inquilino por dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="d79e5-156">Click **Membership**, then enter a user or group in your tenant Azure AD by email address.</span></span>

     ![Agregar usuario](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. <span data-ttu-id="d79e5-158">Si el rol que crea tiene permiso de lectura, puede agregar filtros de fila mediante una fórmula DAX.</span><span class="sxs-lookup"><span data-stu-id="d79e5-158">If the role you are creating has Read permission, you can add row filters by using a DAX formula.</span></span> <span data-ttu-id="d79e5-159">Haga clic en **Filtros de fila**, seleccione una tabla y, luego, escriba una fórmula DAX en el campo **Filtro DAX**.</span><span class="sxs-lookup"><span data-stu-id="d79e5-159">Click **Row Filters**, select a table, and then type a DAX formula in the **DAX Filter** field.</span></span> 

## <a name="to-add-roles-and-users-by-using-a-tmsl-script"></a><span data-ttu-id="d79e5-160">Para agregar roles y usuarios mediante un script de TMSL</span><span class="sxs-lookup"><span data-stu-id="d79e5-160">To add roles and users by using a TMSL script</span></span>
<span data-ttu-id="d79e5-161">Puede ejecutar un script de TMSL en la ventana XMLA en SSMS o mediante PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d79e5-161">You can run a TMSL script in the XMLA window in SSMS or by using PowerShell.</span></span> <span data-ttu-id="d79e5-162">Use el comando [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) y el objeto [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl).</span><span class="sxs-lookup"><span data-stu-id="d79e5-162">Use the [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) command and the [Roles](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.</span></span>

<span data-ttu-id="d79e5-163">**Script TMSL de ejemplo**</span><span class="sxs-lookup"><span data-stu-id="d79e5-163">**Sample TMSL script**</span></span>

<span data-ttu-id="d79e5-164">En este ejemplo, se agrega un grupo y un usuario externo de B2B al rol de analista con permisos de lectura para la base de datos de SalesBI.</span><span class="sxs-lookup"><span data-stu-id="d79e5-164">In this sample, a B2B external user and a group are added to the Analyst role with Read permissions for the SalesBI database.</span></span> <span data-ttu-id="d79e5-165">Tanto el usuario externo como el grupo deben encontrarse en el mismo Azure AD de inquilino.</span><span class="sxs-lookup"><span data-stu-id="d79e5-165">Both the external user and group must be in same tenant Azure AD.</span></span>

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users to query the model",
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

## <a name="to-add-roles-and-users-by-using-powershell"></a><span data-ttu-id="d79e5-166">Para agregar roles y usuarios mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="d79e5-166">To add roles and users by using PowerShell</span></span>
<span data-ttu-id="d79e5-167">El módulo [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) proporciona cmdlets de administración de base de datos específicos de la tarea y el cmdlet Invoke-ASCmd de uso general que acepta un script o una consulta de Tabular Model Scripting Language (TMSL).</span><span class="sxs-lookup"><span data-stu-id="d79e5-167">The [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module provides task-specific database management cmdlets and the general-purpose Invoke-ASCmd cmdlet that accepts a Tabular Model Scripting Language (TMSL) query or script.</span></span> <span data-ttu-id="d79e5-168">Los cmdlets siguientes se usan para administrar usuarios y roles de base de datos.</span><span class="sxs-lookup"><span data-stu-id="d79e5-168">The following cmdlets are used for managing database roles and users.</span></span>
  
|<span data-ttu-id="d79e5-169">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="d79e5-169">Cmdlet</span></span>|<span data-ttu-id="d79e5-170">Descripción</span><span class="sxs-lookup"><span data-stu-id="d79e5-170">Description</span></span>|
|------------|-----------------| 
|[<span data-ttu-id="d79e5-171">Add-RoleMember</span><span class="sxs-lookup"><span data-stu-id="d79e5-171">Add-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510167.aspx)|<span data-ttu-id="d79e5-172">Agrega un miembro a un rol de base de datos.</span><span class="sxs-lookup"><span data-stu-id="d79e5-172">Add a member to a database role.</span></span>| 
|[<span data-ttu-id="d79e5-173">Remove-RoleMember</span><span class="sxs-lookup"><span data-stu-id="d79e5-173">Remove-RoleMember</span></span>](https://msdn.microsoft.com/library/hh510173.aspx)|<span data-ttu-id="d79e5-174">Quita un miembro de un rol de base de datos.</span><span class="sxs-lookup"><span data-stu-id="d79e5-174">Remove a member from a database role.</span></span>|   
|[<span data-ttu-id="d79e5-175">Invoke-ASCmd</span><span class="sxs-lookup"><span data-stu-id="d79e5-175">Invoke-ASCmd</span></span>](https://msdn.microsoft.com/library/hh479579.aspx)|<span data-ttu-id="d79e5-176">Ejecuta un script de TMSL.</span><span class="sxs-lookup"><span data-stu-id="d79e5-176">Execute a TMSL script.</span></span>|

## <a name="row-filters"></a><span data-ttu-id="d79e5-177">Filtros de fila</span><span class="sxs-lookup"><span data-stu-id="d79e5-177">Row filters</span></span>  
<span data-ttu-id="d79e5-178">Los filtros de fila definen las filas de una tabla que los miembros de un rol determinado pueden consultar.</span><span class="sxs-lookup"><span data-stu-id="d79e5-178">Row filters define which rows in a table can be queried by members of a particular role.</span></span> <span data-ttu-id="d79e5-179">Los filtros de fila están definidos para cada tabla en un modelo mediante fórmulas DAX.</span><span class="sxs-lookup"><span data-stu-id="d79e5-179">Row filters are defined for each table in a model by using DAX formulas.</span></span>  
  
<span data-ttu-id="d79e5-180">Los filtros de fila solo se pueden definir para los roles con permisos de lectura y lectura y proceso.</span><span class="sxs-lookup"><span data-stu-id="d79e5-180">Row filters can be defined only for roles with Read and Read and Process permissions.</span></span> <span data-ttu-id="d79e5-181">De manera predeterminada, si no hay definido un filtro de fila para una tabla determinada, los miembros pueden consultar todas las filas de la tabla a menos que el filtrado cruzado se aplique desde otra tabla.</span><span class="sxs-lookup"><span data-stu-id="d79e5-181">By default, if a row filter is not defined for a particular table, members  can query all rows in the table unless cross-filtering applies from another table.</span></span>
  
 <span data-ttu-id="d79e5-182">Los filtros de fila requieren una fórmula DAX, que se debe evaluar con un valor TRUE o FALSE, para definir las filas a las que pueden consultar los miembros de ese rol determinado.</span><span class="sxs-lookup"><span data-stu-id="d79e5-182">Row filters require a DAX formula, which must evaluate to a TRUE/FALSE value, to define the rows that can be queried by members of that particular role.</span></span> <span data-ttu-id="d79e5-183">No es posible consultar filas que no están incluidas en la fórmula DAX.</span><span class="sxs-lookup"><span data-stu-id="d79e5-183">Rows not included in the DAX formula cannot be queried.</span></span> <span data-ttu-id="d79e5-184">Por ejemplo, en la tabla Cliente con la siguiente expresión de filtros de fila siguiente, *=Customers [Country] = "USA"*, los miembros del rol Ventas solo pueden ver los clientes en los Estados Unidos.</span><span class="sxs-lookup"><span data-stu-id="d79e5-184">For example, the Customers table with the following row filters expression, *=Customers [Country] = “USA”*, members of the Sales role can only see customers in the USA.</span></span>  
  
<span data-ttu-id="d79e5-185">Los filtros de fila se aplican a las rilas especificadas y a las filas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="d79e5-185">Row filters apply to the specified rows and related rows.</span></span> <span data-ttu-id="d79e5-186">Cuando una tabla tiene varias relaciones, los filtros aplican seguridad para la relación activa.</span><span class="sxs-lookup"><span data-stu-id="d79e5-186">When a table has multiple relationships, filters apply security for the relationship that is active.</span></span> <span data-ttu-id="d79e5-187">Los filtros de fila forman una intersección con otros filtros de fila definidos para las tablas relacionadas, por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="d79e5-187">Row filters are intersected with other row filers defined for related tables, for example:</span></span>  
  
|<span data-ttu-id="d79e5-188">Tabla</span><span class="sxs-lookup"><span data-stu-id="d79e5-188">Table</span></span>|<span data-ttu-id="d79e5-189">Expresión DAX</span><span class="sxs-lookup"><span data-stu-id="d79e5-189">DAX expression</span></span>|  
|-----------|--------------------|  
|<span data-ttu-id="d79e5-190">Region</span><span class="sxs-lookup"><span data-stu-id="d79e5-190">Region</span></span>|<span data-ttu-id="d79e5-191">=Region[Country]="EE. UU."</span><span class="sxs-lookup"><span data-stu-id="d79e5-191">=Region[Country]=”USA”</span></span>|  
|<span data-ttu-id="d79e5-192">ProductCategory</span><span class="sxs-lookup"><span data-stu-id="d79e5-192">ProductCategory</span></span>|<span data-ttu-id="d79e5-193">=ProductCategory[Name]="Bicicletas"</span><span class="sxs-lookup"><span data-stu-id="d79e5-193">=ProductCategory[Name]=”Bicycles”</span></span>|  
|<span data-ttu-id="d79e5-194">Transacciones</span><span class="sxs-lookup"><span data-stu-id="d79e5-194">Transactions</span></span>|<span data-ttu-id="d79e5-195">=Transactions[Year]=2016</span><span class="sxs-lookup"><span data-stu-id="d79e5-195">=Transactions[Year]=2016</span></span>|  
  
 <span data-ttu-id="d79e5-196">El efecto neto es que los miembros pueden consultar filas de datos cuando el cliente se encuentra en EE. UU., la categoría de producto es "bicicletas" y el año es 2016.</span><span class="sxs-lookup"><span data-stu-id="d79e5-196">The net effect is members can query rows of data where the customer is in the USA, the product category is bicycles, and the year is 2016.</span></span> <span data-ttu-id="d79e5-197">Los usuarios no pueden consultar transacciones fuera de los EE. UU., transacciones que no sean bicicletas o transacciones que no se hayan realizado el 2016, a menos que sean miembro de otro rol que conceda estos permisos.</span><span class="sxs-lookup"><span data-stu-id="d79e5-197">Users cannot query transactions outside of the USA, transactions that are not bicycles, or transactions not in 2016 unless they are a member of another role that grants these permissions.</span></span>
  
 <span data-ttu-id="d79e5-198">Puede usar el filtro, *=FALSE()*, para denegar el acceso a todas las filas de una tabla completa.</span><span class="sxs-lookup"><span data-stu-id="d79e5-198">You can use the filter, *=FALSE()*, to deny access to all rows for an entire table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d79e5-199">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="d79e5-199">Next steps</span></span>
  <span data-ttu-id="d79e5-200">[Administración de administradores del servidor](analysis-services-server-admins.md) </span><span class="sxs-lookup"><span data-stu-id="d79e5-200">[Manage server administrators](analysis-services-server-admins.md) </span></span>  
  [<span data-ttu-id="d79e5-201">Administración de Azure Analysis Services con PowerShell</span><span class="sxs-lookup"><span data-stu-id="d79e5-201">Manage Azure Analysis Services with PowerShell</span></span>](analysis-services-powershell.md)  
  [<span data-ttu-id="d79e5-202">Referencia Tabular Model Scripting Language (TMSL)</span><span class="sxs-lookup"><span data-stu-id="d79e5-202">Tabular Model Scripting Language (TMSL) Reference</span></span>](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

