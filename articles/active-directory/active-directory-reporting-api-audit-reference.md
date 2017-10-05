---
title: "Referencia de la API de auditoría de Azure Active Directory | Microsoft Docs"
description: "Introducción a la API de auditoría de Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 44e46be8-09e5-4981-be2b-d474aaa92792
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 573e940c5390e7b990d889681eb37b73c5b253d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="c38de-103">Referencia de la API de auditoría de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c38de-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="c38de-104">Este tema forma parte de una serie de temas sobre la API de informes de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c38de-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="c38de-105">La característica de generación de informes de Azure AD proporciona una API que permite acceder a los datos de auditoría mediante el uso de código o herramientas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="c38de-105">Azure AD reporting provides you with an API that enables you to access audit data using code or related tools.</span></span>
<span data-ttu-id="c38de-106">El objetivo de este tema es ofrecer información de referencia sobre la **API de auditoría**.</span><span class="sxs-lookup"><span data-stu-id="c38de-106">The scope of this topic is to provide you with reference information about the **audit API**.</span></span>

<span data-ttu-id="c38de-107">Consulte:</span><span class="sxs-lookup"><span data-stu-id="c38de-107">See:</span></span>

* <span data-ttu-id="c38de-108">[Registros de auditoría](active-directory-reporting-azure-portal.md#activity-reports) para más información conceptual</span><span class="sxs-lookup"><span data-stu-id="c38de-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="c38de-109">[Introducción a la API de generación de informes de Azure Active Directory](active-directory-reporting-api-getting-started.md) para obtener más información sobre esta API</span><span class="sxs-lookup"><span data-stu-id="c38de-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


<span data-ttu-id="c38de-110">Si desea:</span><span class="sxs-lookup"><span data-stu-id="c38de-110">For:</span></span>

- <span data-ttu-id="c38de-111">Conocer las preguntas más frecuentes, lea nuestras [Preguntas más frecuentes](active-directory-reporting-faq.md)</span><span class="sxs-lookup"><span data-stu-id="c38de-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="c38de-112">En caso de problemas, [abra una incidencia de soporte técnico](active-directory-troubleshooting-support-howto.md)</span><span class="sxs-lookup"><span data-stu-id="c38de-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-the-data"></a><span data-ttu-id="c38de-113">¿Quién puede acceder a los datos?</span><span class="sxs-lookup"><span data-stu-id="c38de-113">Who can access the data?</span></span>
* <span data-ttu-id="c38de-114">Usuarios de los roles de administrador o lector de seguridad</span><span class="sxs-lookup"><span data-stu-id="c38de-114">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="c38de-115">Administradores globales</span><span class="sxs-lookup"><span data-stu-id="c38de-115">Global Admins</span></span>
* <span data-ttu-id="c38de-116">Cualquier aplicación que tenga autorización para acceder a la API (la autorización de aplicaciones solo puede configurarse según los permisos del administrador global).</span><span class="sxs-lookup"><span data-stu-id="c38de-116">Any app that has authorization to access the API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c38de-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="c38de-117">Prerequisites</span></span>
<span data-ttu-id="c38de-118">Para acceder a este informe a través de la API de generación de informes, debe cumplir los siguientes requisitos:</span><span class="sxs-lookup"><span data-stu-id="c38de-118">In order to access this report through the Reporting API, you must have:</span></span>

* <span data-ttu-id="c38de-119">Una [edición de Azure Active Directory gratis o superior](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="c38de-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="c38de-120">Completar los [requisitos previos para acceder a la API de generación de informes de Azure AD](active-directory-reporting-api-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="c38de-120">Completed the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-the-api"></a><span data-ttu-id="c38de-121">Acceso a la API</span><span class="sxs-lookup"><span data-stu-id="c38de-121">Accessing the API</span></span>
<span data-ttu-id="c38de-122">Puede acceder a esta API a través del [Probador de Graph](https://graphexplorer2.cloudapp.net) o mediante programación con, por ejemplo, PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c38de-122">You can either access this API through the [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="c38de-123">Para que PowerShell pueda interpretar correctamente la sintaxis de filtro de OData empleada en las llamadas a la API REST Graph de AAD, debe usar el carácter de acento grave para escapar $.</span><span class="sxs-lookup"><span data-stu-id="c38de-123">In order for PowerShell to correctly interpret the OData filter syntax used in AAD Graph REST calls, you must use the backtick (aka: grave accent) character to “escape” the $ character.</span></span> <span data-ttu-id="c38de-124">El carácter de acento grave actúa como [carácter de escape de PowerShell](https://technet.microsoft.com/library/hh847755.aspx), de modo que PowerShell puede hacer una interpretación literal del carácter $ y evitar que lo confunda con un nombre de variable de PowerShell (por ejemplo, $filter).</span><span class="sxs-lookup"><span data-stu-id="c38de-124">The backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell to do a literal interpretation of the $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="c38de-125">Este tema se centra en el Probador de Graph.</span><span class="sxs-lookup"><span data-stu-id="c38de-125">The focus of this topic is on the Graph Explorer.</span></span> <span data-ttu-id="c38de-126">Para ver un ejemplo de PowerShell, consulte este [script de PowerShell](active-directory-reporting-api-audit-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="c38de-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="c38de-127">Punto de conexión de API</span><span class="sxs-lookup"><span data-stu-id="c38de-127">API Endpoint</span></span>
<span data-ttu-id="c38de-128">Puede acceder a esta API con el siguiente URI:</span><span class="sxs-lookup"><span data-stu-id="c38de-128">You can access this API using the following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="c38de-129">No hay ningún límite en el número de registros devueltos por la API de generación de informes de Azure AD (mediante la paginación de OData).</span><span class="sxs-lookup"><span data-stu-id="c38de-129">There is no limit on the number of records returned by the Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="c38de-130">Para ver los límites de retención de los datos de informes, consulte [Directivas de retención de informes](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="c38de-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="c38de-131">Esta llamada devuelve los datos en lotes.</span><span class="sxs-lookup"><span data-stu-id="c38de-131">This call returns the data in batches.</span></span> <span data-ttu-id="c38de-132">Cada lote tiene un máximo de 1000 registros.</span><span class="sxs-lookup"><span data-stu-id="c38de-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="c38de-133">Para obtener el siguiente lote de registros, haga clic en el vínculo Siguiente.</span><span class="sxs-lookup"><span data-stu-id="c38de-133">To get the next batch of records, use the Next link.</span></span> <span data-ttu-id="c38de-134">Obtenga la información de skiptoken desde el primer conjunto de registros devueltos.</span><span class="sxs-lookup"><span data-stu-id="c38de-134">Get the skiptoken information from the first set of returned records.</span></span> <span data-ttu-id="c38de-135">El token de omisión estará al final del conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="c38de-135">The skip token will be at the end of the result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="c38de-136">Filtros admitidos</span><span class="sxs-lookup"><span data-stu-id="c38de-136">Supported filters</span></span>
<span data-ttu-id="c38de-137">Puede limitar el número de registros que se devuelven mediante una llamada de API usando un filtro.</span><span class="sxs-lookup"><span data-stu-id="c38de-137">You can narrow down the number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="c38de-138">En lo que respecta a los datos relacionados con las API de inicio de sesión, se admiten los siguientes filtros:</span><span class="sxs-lookup"><span data-stu-id="c38de-138">For sign-in API related data, the following filters are supported:</span></span>

* <span data-ttu-id="c38de-139">**$top=\<número de registros que se devolverán\>**: limita el número de registros devueltos.</span><span class="sxs-lookup"><span data-stu-id="c38de-139">**$top=\<number of records to be returned\>** - to limit the number of returned records.</span></span> <span data-ttu-id="c38de-140">Se trata de una operación costosa.</span><span class="sxs-lookup"><span data-stu-id="c38de-140">This is an expensive operation.</span></span> <span data-ttu-id="c38de-141">No debe utilizar este filtro si quiere devolver miles de objetos.</span><span class="sxs-lookup"><span data-stu-id="c38de-141">You should not use this filter if you want to return thousands of objects.</span></span>     
* <span data-ttu-id="c38de-142">**$filter=\<instrucción de filtro\>**: para especificar, en función de los campos de filtro compatibles, el tipo de registros que le interesan</span><span class="sxs-lookup"><span data-stu-id="c38de-142">**$filter=\<your filter statement\>** - to specify, on the basis of supported filter fields, the type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="c38de-143">Operadores y campos de filtro compatibles</span><span class="sxs-lookup"><span data-stu-id="c38de-143">Supported filter fields and operators</span></span>
<span data-ttu-id="c38de-144">Para especificar el tipo de registros que le interesa, puede crear una instrucción de filtro que puede contener uno o una combinación de los campos de filtro siguientes:</span><span class="sxs-lookup"><span data-stu-id="c38de-144">To specify the type of records you care about, you can build a filter statement that can contain either one or a combination of the following filter fields:</span></span>

* <span data-ttu-id="c38de-145">[activityDate](#activitydate): define una fecha o un intervalo de fechas</span><span class="sxs-lookup"><span data-stu-id="c38de-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="c38de-146">[category](#category): define la categoría por la que desea filtrar.</span><span class="sxs-lookup"><span data-stu-id="c38de-146">[category](#category) - defines the category you want to filter on.</span></span>
* <span data-ttu-id="c38de-147">[activityStatus](#activitystatus): define el estado de una actividad.</span><span class="sxs-lookup"><span data-stu-id="c38de-147">[activityStatus](#activitystatus) - defines the status of an activity</span></span>
* <span data-ttu-id="c38de-148">[activityType](#activitytype): define el tipo de una actividad</span><span class="sxs-lookup"><span data-stu-id="c38de-148">[activityType](#activitytype)  - defines the type of an activity</span></span>
* <span data-ttu-id="c38de-149">[activity](#activity): define la actividad como cadena</span><span class="sxs-lookup"><span data-stu-id="c38de-149">[activity](#activity) - defines the activity as string</span></span>  
* <span data-ttu-id="c38de-150">[actor/name](#actorname): define el actor en el formato de nombre del actor</span><span class="sxs-lookup"><span data-stu-id="c38de-150">[actor/name](#actorname) -   defines the actor in form of the actor's name</span></span>
* <span data-ttu-id="c38de-151">[actor/objectid](#actorobjectid) : define el actor en el formato del identificador del actor</span><span class="sxs-lookup"><span data-stu-id="c38de-151">[actor/objectid](#actorobjectid) - defines the actor in form of the actor's ID</span></span>   
* <span data-ttu-id="c38de-152">[actor/upn](#actorupn): define el actor en el formato de nombre principal de usuario (UPN) del actor</span><span class="sxs-lookup"><span data-stu-id="c38de-152">[actor/upn](#actorupn)  - defines the actor in form of the actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="c38de-153">[target/name](#targetname): define el destino en el formato de nombre del actor</span><span class="sxs-lookup"><span data-stu-id="c38de-153">[target/name](#targetname)  - defines the target in form of the actor's name</span></span>
* <span data-ttu-id="c38de-154">[target/objectid](#targetobjectid) : define el destino en el formato de identificador del destino</span><span class="sxs-lookup"><span data-stu-id="c38de-154">[target/objectid](#targetobjectid) - defines the target in form of the target's ID</span></span>  
* <span data-ttu-id="c38de-155">[target/upn](#targetupn) : define el actor en el formato de nombre principal de usuario del actor (UPN)</span><span class="sxs-lookup"><span data-stu-id="c38de-155">[target/upn](#targetupn) - defines the actor in form of the actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="c38de-156">activityDate</span><span class="sxs-lookup"><span data-stu-id="c38de-156">activityDate</span></span>
<span data-ttu-id="c38de-157">**Operadores compatibles**: eq, ge, le, gt y lt</span><span class="sxs-lookup"><span data-stu-id="c38de-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="c38de-158">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c38de-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="c38de-159">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="c38de-159">**Notes**:</span></span>

<span data-ttu-id="c38de-160">datetime debe estar en formato UTC.</span><span class="sxs-lookup"><span data-stu-id="c38de-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="c38de-161">categoría</span><span class="sxs-lookup"><span data-stu-id="c38de-161">category</span></span>

<span data-ttu-id="c38de-162">**Valores admitidos**:</span><span class="sxs-lookup"><span data-stu-id="c38de-162">**Supported values**:</span></span>

| <span data-ttu-id="c38de-163">Categoría</span><span class="sxs-lookup"><span data-stu-id="c38de-163">Category</span></span>                         | <span data-ttu-id="c38de-164">Valor</span><span class="sxs-lookup"><span data-stu-id="c38de-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="c38de-165">Core Directory (Directorio principal)</span><span class="sxs-lookup"><span data-stu-id="c38de-165">Core Directory</span></span>                   | <span data-ttu-id="c38de-166">Directorio</span><span class="sxs-lookup"><span data-stu-id="c38de-166">Directory</span></span> |
| <span data-ttu-id="c38de-167">Self-service Password Management (Administración de contraseñas de autorservicio)</span><span class="sxs-lookup"><span data-stu-id="c38de-167">Self-service Password Management</span></span> | <span data-ttu-id="c38de-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="c38de-168">SSPR</span></span>      |
| <span data-ttu-id="c38de-169">Self-service Group Management (Administración de grupos de autoservicio)</span><span class="sxs-lookup"><span data-stu-id="c38de-169">Self-service Group Management</span></span>    | <span data-ttu-id="c38de-170">SSGM</span><span class="sxs-lookup"><span data-stu-id="c38de-170">SSGM</span></span>      |
| <span data-ttu-id="c38de-171">Account Provisioning (Aprovisionamiento de cuentas)</span><span class="sxs-lookup"><span data-stu-id="c38de-171">Account Provisioning</span></span>             | <span data-ttu-id="c38de-172">Sync</span><span class="sxs-lookup"><span data-stu-id="c38de-172">Sync</span></span>      |
| <span data-ttu-id="c38de-173">Automated Password Rollover (Sustitución automática de contraseña)</span><span class="sxs-lookup"><span data-stu-id="c38de-173">Automated Password Rollover</span></span>      | <span data-ttu-id="c38de-174">Automated Password Rollover (Sustitución automática de contraseña)</span><span class="sxs-lookup"><span data-stu-id="c38de-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="c38de-175">Protección de identidad</span><span class="sxs-lookup"><span data-stu-id="c38de-175">Identity Protection</span></span>              | <span data-ttu-id="c38de-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="c38de-176">IdentityProtection</span></span> |
| <span data-ttu-id="c38de-177">Invited Users (Usuarios invitados)</span><span class="sxs-lookup"><span data-stu-id="c38de-177">Invited Users</span></span>                    | <span data-ttu-id="c38de-178">Invited Users (Usuarios invitados)</span><span class="sxs-lookup"><span data-stu-id="c38de-178">Invited Users</span></span> |
| <span data-ttu-id="c38de-179">MIM Service (Servicio MIM)</span><span class="sxs-lookup"><span data-stu-id="c38de-179">MIM Service</span></span>                      | <span data-ttu-id="c38de-180">MIM Service (Servicio MIM)</span><span class="sxs-lookup"><span data-stu-id="c38de-180">MIM Service</span></span> |



<span data-ttu-id="c38de-181">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="c38de-181">**Supported operators**: eq</span></span>

<span data-ttu-id="c38de-182">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c38de-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="c38de-183">activityStatus</span><span class="sxs-lookup"><span data-stu-id="c38de-183">activityStatus</span></span>

<span data-ttu-id="c38de-184">**Valores admitidos**:</span><span class="sxs-lookup"><span data-stu-id="c38de-184">**Supported values**:</span></span>

| <span data-ttu-id="c38de-185">Estado de la actividad</span><span class="sxs-lookup"><span data-stu-id="c38de-185">Activity Status</span></span> | <span data-ttu-id="c38de-186">Valor</span><span class="sxs-lookup"><span data-stu-id="c38de-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="c38de-187">Correcto</span><span class="sxs-lookup"><span data-stu-id="c38de-187">Success</span></span>         | <span data-ttu-id="c38de-188">0</span><span class="sxs-lookup"><span data-stu-id="c38de-188">0</span></span>     |
| <span data-ttu-id="c38de-189">Error</span><span class="sxs-lookup"><span data-stu-id="c38de-189">Failure</span></span>         | <span data-ttu-id="c38de-190">- 1</span><span class="sxs-lookup"><span data-stu-id="c38de-190">- 1</span></span>   |

<span data-ttu-id="c38de-191">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="c38de-191">**Supported operators**: eq</span></span>

<span data-ttu-id="c38de-192">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c38de-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="c38de-193">activityType</span><span class="sxs-lookup"><span data-stu-id="c38de-193">activityType</span></span>
<span data-ttu-id="c38de-194">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="c38de-194">**Supported operators**: eq</span></span>

<span data-ttu-id="c38de-195">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c38de-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="c38de-196">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="c38de-196">**Notes**:</span></span>

<span data-ttu-id="c38de-197">Distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="c38de-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="c38de-198">activity</span><span class="sxs-lookup"><span data-stu-id="c38de-198">activity</span></span>
<span data-ttu-id="c38de-199">**Operadores compatibles**: eq, contains y startsWith</span><span class="sxs-lookup"><span data-stu-id="c38de-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="c38de-200">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c38de-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="c38de-201">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="c38de-201">**Notes**:</span></span>

<span data-ttu-id="c38de-202">Distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="c38de-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="c38de-203">actor/name</span><span class="sxs-lookup"><span data-stu-id="c38de-203">actor/name</span></span>
<span data-ttu-id="c38de-204">**Operadores compatibles**: eq, contains y startsWith</span><span class="sxs-lookup"><span data-stu-id="c38de-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="c38de-205">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c38de-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="c38de-206">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="c38de-206">**Notes**:</span></span>

<span data-ttu-id="c38de-207">No distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="c38de-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="c38de-208">actor/objectid</span><span class="sxs-lookup"><span data-stu-id="c38de-208">actor/objectId</span></span>
<span data-ttu-id="c38de-209">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="c38de-209">**Supported operators**: eq</span></span>

<span data-ttu-id="c38de-210">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c38de-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="c38de-211">target/namde</span><span class="sxs-lookup"><span data-stu-id="c38de-211">target/name</span></span>
<span data-ttu-id="c38de-212">**Operadores compatibles**: eq, contains y startsWith</span><span class="sxs-lookup"><span data-stu-id="c38de-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="c38de-213">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c38de-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="c38de-214">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="c38de-214">**Notes**:</span></span>

<span data-ttu-id="c38de-215">No distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="c38de-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="c38de-216">target/upn</span><span class="sxs-lookup"><span data-stu-id="c38de-216">target/upn</span></span>
<span data-ttu-id="c38de-217">**Operadores compatibles**: eq y startsWith</span><span class="sxs-lookup"><span data-stu-id="c38de-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="c38de-218">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c38de-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="c38de-219">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="c38de-219">**Notes**:</span></span>

* <span data-ttu-id="c38de-220">No distingue mayúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="c38de-220">Case-insensitive</span></span>
* <span data-ttu-id="c38de-221">Al consultar Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity es preciso agregar el espacio de nombres completo</span><span class="sxs-lookup"><span data-stu-id="c38de-221">You need to add the full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="c38de-222">target/objectid</span><span class="sxs-lookup"><span data-stu-id="c38de-222">target/objectId</span></span>
<span data-ttu-id="c38de-223">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="c38de-223">**Supported operators**: eq</span></span>

<span data-ttu-id="c38de-224">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c38de-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="c38de-225">actor/upn</span><span class="sxs-lookup"><span data-stu-id="c38de-225">actor/upn</span></span>
<span data-ttu-id="c38de-226">**Operadores compatibles**: eq y startsWith</span><span class="sxs-lookup"><span data-stu-id="c38de-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="c38de-227">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="c38de-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="c38de-228">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="c38de-228">**Notes**:</span></span>

* <span data-ttu-id="c38de-229">No distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="c38de-229">Case-insensitive</span></span> 
* <span data-ttu-id="c38de-230">Debe agregar el espacio de nombres completo al consultar Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span><span class="sxs-lookup"><span data-stu-id="c38de-230">You need to add the full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="c38de-231">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="c38de-231">Next Steps</span></span>
* <span data-ttu-id="c38de-232">¿Quiere ver ejemplos de actividades del sistema filtradas?</span><span class="sxs-lookup"><span data-stu-id="c38de-232">Do you want to see examples for filtered system activities?</span></span> <span data-ttu-id="c38de-233">Consulte los [ejemplos de la API de auditoría de Azure Active Directory](active-directory-reporting-api-audit-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c38de-233">Check out the [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="c38de-234">¿Quiere obtener más información sobre la API de generación de informes de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="c38de-234">Do you want to know more about the Azure AD reporting API?</span></span> <span data-ttu-id="c38de-235">Consulte [Introducción a la API de informes de Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="c38de-235">See [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

