---
title: "auditoría de Active Directory aaaAzure referencia de API | Documentos de Microsoft"
description: "¿Cómo tooget partió Hola API de auditoría de Azure Active Directory"
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
ms.openlocfilehash: 5f33b62ede9be445f35704739e328580dc454368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="3e46e-103">Referencia de la API de auditoría de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3e46e-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="3e46e-104">Este tema forma parte de una colección de temas sobre hello Azure Active Directory API de informes.</span><span class="sxs-lookup"><span data-stu-id="3e46e-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="3e46e-105">Reporting de Azure AD proporciona una API que permite los datos de auditoría tooaccess mediante código o herramientas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="3e46e-105">Azure AD reporting provides you with an API that enables you tooaccess audit data using code or related tools.</span></span>
<span data-ttu-id="3e46e-106">ámbito de Hola de este tema es tooprovide, con información de referencia sobre hello **API de auditoría**.</span><span class="sxs-lookup"><span data-stu-id="3e46e-106">hello scope of this topic is tooprovide you with reference information about hello **audit API**.</span></span>

<span data-ttu-id="3e46e-107">Consulte:</span><span class="sxs-lookup"><span data-stu-id="3e46e-107">See:</span></span>

* <span data-ttu-id="3e46e-108">[Registros de auditoría](active-directory-reporting-azure-portal.md#activity-reports) para más información conceptual</span><span class="sxs-lookup"><span data-stu-id="3e46e-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="3e46e-109">[Introducción a Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md) para obtener más información acerca de la API de informes de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e46e-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


<span data-ttu-id="3e46e-110">Si desea:</span><span class="sxs-lookup"><span data-stu-id="3e46e-110">For:</span></span>

- <span data-ttu-id="3e46e-111">Conocer las preguntas más frecuentes, lea nuestras [Preguntas más frecuentes](active-directory-reporting-faq.md)</span><span class="sxs-lookup"><span data-stu-id="3e46e-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="3e46e-112">En caso de problemas, [abra una incidencia de soporte técnico](active-directory-troubleshooting-support-howto.md)</span><span class="sxs-lookup"><span data-stu-id="3e46e-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-hello-data"></a><span data-ttu-id="3e46e-113">¿Quién puede tener acceso a datos de hello?</span><span class="sxs-lookup"><span data-stu-id="3e46e-113">Who can access hello data?</span></span>
* <span data-ttu-id="3e46e-114">Usuarios de rol de administrador de seguridad o seguridad lector Hola</span><span class="sxs-lookup"><span data-stu-id="3e46e-114">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="3e46e-115">Administradores globales</span><span class="sxs-lookup"><span data-stu-id="3e46e-115">Global Admins</span></span>
* <span data-ttu-id="3e46e-116">Cualquier aplicación que tenga autorización tooaccess Hola API (autorización de la aplicación puede ser el programa de instalación solamente basándose en el permiso del administrador Global)</span><span class="sxs-lookup"><span data-stu-id="3e46e-116">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3e46e-117">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="3e46e-117">Prerequisites</span></span>
<span data-ttu-id="3e46e-118">En este informe a través de tooaccess de orden Hola API de informes, debe tener:</span><span class="sxs-lookup"><span data-stu-id="3e46e-118">In order tooaccess this report through hello Reporting API, you must have:</span></span>

* <span data-ttu-id="3e46e-119">Una [edición de Azure Active Directory gratis o superior](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="3e46e-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="3e46e-120">Hola completado [API de generación de informes de requisitos previos tooaccess hello Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="3e46e-120">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="3e46e-121">Obtener acceso a las API de Hola</span><span class="sxs-lookup"><span data-stu-id="3e46e-121">Accessing hello API</span></span>
<span data-ttu-id="3e46e-122">Se puede tener acceso a esta API a través de hello [Explorador de gráficos](https://graphexplorer2.cloudapp.net) o mediante programación con, por ejemplo, PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3e46e-122">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="3e46e-123">En orden para PowerShell toocorrectly interpretar la sintaxis de filtros de OData Hola utilizada en las llamadas de REST de AAD Graph, debe usar acento grave hello (también conocido como: acento grave) carácter demasiado "carácter de escape" hello $.</span><span class="sxs-lookup"><span data-stu-id="3e46e-123">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="3e46e-124">carácter de acento grave Hola actúa como [carácter de escape de PowerShell](https://technet.microsoft.com/library/hh847755.aspx), lo que PowerShell toodo una interpretación literal de carácter de hello $ y evitar confundir como un nombre de variable de PowerShell (es decir: $filter).</span><span class="sxs-lookup"><span data-stu-id="3e46e-124">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="3e46e-125">Hola de este tema es Hola Explorador de gráficos.</span><span class="sxs-lookup"><span data-stu-id="3e46e-125">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="3e46e-126">Para ver un ejemplo de PowerShell, consulte este [script de PowerShell](active-directory-reporting-api-audit-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="3e46e-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="3e46e-127">Punto de conexión de API</span><span class="sxs-lookup"><span data-stu-id="3e46e-127">API Endpoint</span></span>
<span data-ttu-id="3e46e-128">Puede tener acceso a esta API con hello siguiente URI:</span><span class="sxs-lookup"><span data-stu-id="3e46e-128">You can access this API using hello following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="3e46e-129">No hay ningún límite en hello número de registros devueltos por la API de auditoría de hello Azure AD (uso de la paginación de OData).</span><span class="sxs-lookup"><span data-stu-id="3e46e-129">There is no limit on hello number of records returned by hello Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="3e46e-130">Para ver los límites de retención de los datos de informes, consulte [Directivas de retención de informes](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="3e46e-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="3e46e-131">Esta llamada devuelve datos de hello en lotes.</span><span class="sxs-lookup"><span data-stu-id="3e46e-131">This call returns hello data in batches.</span></span> <span data-ttu-id="3e46e-132">Cada lote tiene un máximo de 1000 registros.</span><span class="sxs-lookup"><span data-stu-id="3e46e-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="3e46e-133">tooget Hola siguiente lote de registros, use Hola siguiente vínculo.</span><span class="sxs-lookup"><span data-stu-id="3e46e-133">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="3e46e-134">Obtener información de skiptoken de hello del primer conjunto de registros devueltos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3e46e-134">Get hello skiptoken information from hello first set of returned records.</span></span> <span data-ttu-id="3e46e-135">token de omisión de Hello será final Hola Hola de conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="3e46e-135">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="3e46e-136">Filtros admitidos</span><span class="sxs-lookup"><span data-stu-id="3e46e-136">Supported filters</span></span>
<span data-ttu-id="3e46e-137">Puede limitar número de Hola de registros devueltos por una API de llamar a en forma de un filtro.</span><span class="sxs-lookup"><span data-stu-id="3e46e-137">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="3e46e-138">Para inicio de sesión de la API se admiten datos relacionados, Hola después de filtros:</span><span class="sxs-lookup"><span data-stu-id="3e46e-138">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="3e46e-139">**$top =\<devolvió un número de registros toobe\>**  -número de hello toolimit de registros devueltos.</span><span class="sxs-lookup"><span data-stu-id="3e46e-139">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="3e46e-140">Se trata de una operación costosa.</span><span class="sxs-lookup"><span data-stu-id="3e46e-140">This is an expensive operation.</span></span> <span data-ttu-id="3e46e-141">No se debe usar este filtro si desea tooreturn miles de objetos.</span><span class="sxs-lookup"><span data-stu-id="3e46e-141">You should not use this filter if you want tooreturn thousands of objects.</span></span>     
* <span data-ttu-id="3e46e-142">**$filter =\<la instrucción de filtro\>**  -toospecify, en función de Hola de campos de filtro admitido, tipo de Hola de registros que le interesa</span><span class="sxs-lookup"><span data-stu-id="3e46e-142">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="3e46e-143">Operadores y campos de filtro compatibles</span><span class="sxs-lookup"><span data-stu-id="3e46e-143">Supported filter fields and operators</span></span>
<span data-ttu-id="3e46e-144">tipo de hello toospecify de registros que le interesa, puede crear una instrucción de filtro que puede contener uno o una combinación de hello después de los campos de filtro:</span><span class="sxs-lookup"><span data-stu-id="3e46e-144">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="3e46e-145">[activityDate](#activitydate): define una fecha o un intervalo de fechas</span><span class="sxs-lookup"><span data-stu-id="3e46e-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="3e46e-146">[categoría](#category) -define la categoría de hello en la que desee toofilter.</span><span class="sxs-lookup"><span data-stu-id="3e46e-146">[category](#category) - defines hello category you want toofilter on.</span></span>
* <span data-ttu-id="3e46e-147">[activityStatus](#activitystatus) -define el estado de saludo de una actividad</span><span class="sxs-lookup"><span data-stu-id="3e46e-147">[activityStatus](#activitystatus) - defines hello status of an activity</span></span>
* <span data-ttu-id="3e46e-148">[activityType](#activitytype) -define el tipo de saludo de una actividad</span><span class="sxs-lookup"><span data-stu-id="3e46e-148">[activityType](#activitytype)  - defines hello type of an activity</span></span>
* <span data-ttu-id="3e46e-149">[actividad](#activity) -define actividad hello como cadena</span><span class="sxs-lookup"><span data-stu-id="3e46e-149">[activity](#activity) - defines hello activity as string</span></span>  
* <span data-ttu-id="3e46e-150">[nombre delactor/](#actorname) -define actor hello en formato de nombre del actor Hola</span><span class="sxs-lookup"><span data-stu-id="3e46e-150">[actor/name](#actorname) -   defines hello actor in form of hello actor's name</span></span>
* <span data-ttu-id="3e46e-151">[actor/objectid](#actorobjectid) -define actores de Hola en formato de Id. de actor Hola</span><span class="sxs-lookup"><span data-stu-id="3e46e-151">[actor/objectid](#actorobjectid) - defines hello actor in form of hello actor's ID</span></span>   
* <span data-ttu-id="3e46e-152">[actor/upn](#actorupn) -define actores hello en formato de nombre principal de usuario del actor hello (UPN)</span><span class="sxs-lookup"><span data-stu-id="3e46e-152">[actor/upn](#actorupn)  - defines hello actor in form of hello actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="3e46e-153">[nombre dedestino/](#targetname) -define el destino de hello en forma de nombre del actor Hola</span><span class="sxs-lookup"><span data-stu-id="3e46e-153">[target/name](#targetname)  - defines hello target in form of hello actor's name</span></span>
* <span data-ttu-id="3e46e-154">[destino/objectid](#targetobjectid) -define el destino de hello en forma de identificador del destino de Hola</span><span class="sxs-lookup"><span data-stu-id="3e46e-154">[target/objectid](#targetobjectid) - defines hello target in form of hello target's ID</span></span>  
* <span data-ttu-id="3e46e-155">[destino/upn](#targetupn) -define actores hello en formato de nombre principal de usuario del actor hello (UPN)</span><span class="sxs-lookup"><span data-stu-id="3e46e-155">[target/upn](#targetupn) - defines hello actor in form of hello actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="3e46e-156">activityDate</span><span class="sxs-lookup"><span data-stu-id="3e46e-156">activityDate</span></span>
<span data-ttu-id="3e46e-157">**Operadores compatibles**: eq, ge, le, gt y lt</span><span class="sxs-lookup"><span data-stu-id="3e46e-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="3e46e-158">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="3e46e-159">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-159">**Notes**:</span></span>

<span data-ttu-id="3e46e-160">datetime debe estar en formato UTC.</span><span class="sxs-lookup"><span data-stu-id="3e46e-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="3e46e-161">categoría</span><span class="sxs-lookup"><span data-stu-id="3e46e-161">category</span></span>

<span data-ttu-id="3e46e-162">**Valores admitidos**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-162">**Supported values**:</span></span>

| <span data-ttu-id="3e46e-163">Categoría</span><span class="sxs-lookup"><span data-stu-id="3e46e-163">Category</span></span>                         | <span data-ttu-id="3e46e-164">Valor</span><span class="sxs-lookup"><span data-stu-id="3e46e-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="3e46e-165">Core Directory (Directorio principal)</span><span class="sxs-lookup"><span data-stu-id="3e46e-165">Core Directory</span></span>                   | <span data-ttu-id="3e46e-166">Directorio</span><span class="sxs-lookup"><span data-stu-id="3e46e-166">Directory</span></span> |
| <span data-ttu-id="3e46e-167">Self-service Password Management (Administración de contraseñas de autorservicio)</span><span class="sxs-lookup"><span data-stu-id="3e46e-167">Self-service Password Management</span></span> | <span data-ttu-id="3e46e-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="3e46e-168">SSPR</span></span>      |
| <span data-ttu-id="3e46e-169">Self-service Group Management (Administración de grupos de autoservicio)</span><span class="sxs-lookup"><span data-stu-id="3e46e-169">Self-service Group Management</span></span>    | <span data-ttu-id="3e46e-170">SSGM</span><span class="sxs-lookup"><span data-stu-id="3e46e-170">SSGM</span></span>      |
| <span data-ttu-id="3e46e-171">Account Provisioning (Aprovisionamiento de cuentas)</span><span class="sxs-lookup"><span data-stu-id="3e46e-171">Account Provisioning</span></span>             | <span data-ttu-id="3e46e-172">Sync</span><span class="sxs-lookup"><span data-stu-id="3e46e-172">Sync</span></span>      |
| <span data-ttu-id="3e46e-173">Automated Password Rollover (Sustitución automática de contraseña)</span><span class="sxs-lookup"><span data-stu-id="3e46e-173">Automated Password Rollover</span></span>      | <span data-ttu-id="3e46e-174">Automated Password Rollover (Sustitución automática de contraseña)</span><span class="sxs-lookup"><span data-stu-id="3e46e-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="3e46e-175">Protección de identidad</span><span class="sxs-lookup"><span data-stu-id="3e46e-175">Identity Protection</span></span>              | <span data-ttu-id="3e46e-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="3e46e-176">IdentityProtection</span></span> |
| <span data-ttu-id="3e46e-177">Invited Users (Usuarios invitados)</span><span class="sxs-lookup"><span data-stu-id="3e46e-177">Invited Users</span></span>                    | <span data-ttu-id="3e46e-178">Invited Users (Usuarios invitados)</span><span class="sxs-lookup"><span data-stu-id="3e46e-178">Invited Users</span></span> |
| <span data-ttu-id="3e46e-179">MIM Service (Servicio MIM)</span><span class="sxs-lookup"><span data-stu-id="3e46e-179">MIM Service</span></span>                      | <span data-ttu-id="3e46e-180">MIM Service (Servicio MIM)</span><span class="sxs-lookup"><span data-stu-id="3e46e-180">MIM Service</span></span> |



<span data-ttu-id="3e46e-181">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="3e46e-181">**Supported operators**: eq</span></span>

<span data-ttu-id="3e46e-182">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="3e46e-183">activityStatus</span><span class="sxs-lookup"><span data-stu-id="3e46e-183">activityStatus</span></span>

<span data-ttu-id="3e46e-184">**Valores admitidos**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-184">**Supported values**:</span></span>

| <span data-ttu-id="3e46e-185">Estado de la actividad</span><span class="sxs-lookup"><span data-stu-id="3e46e-185">Activity Status</span></span> | <span data-ttu-id="3e46e-186">Valor</span><span class="sxs-lookup"><span data-stu-id="3e46e-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="3e46e-187">Correcto</span><span class="sxs-lookup"><span data-stu-id="3e46e-187">Success</span></span>         | <span data-ttu-id="3e46e-188">0</span><span class="sxs-lookup"><span data-stu-id="3e46e-188">0</span></span>     |
| <span data-ttu-id="3e46e-189">Error</span><span class="sxs-lookup"><span data-stu-id="3e46e-189">Failure</span></span>         | <span data-ttu-id="3e46e-190">- 1</span><span class="sxs-lookup"><span data-stu-id="3e46e-190">- 1</span></span>   |

<span data-ttu-id="3e46e-191">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="3e46e-191">**Supported operators**: eq</span></span>

<span data-ttu-id="3e46e-192">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="3e46e-193">activityType</span><span class="sxs-lookup"><span data-stu-id="3e46e-193">activityType</span></span>
<span data-ttu-id="3e46e-194">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="3e46e-194">**Supported operators**: eq</span></span>

<span data-ttu-id="3e46e-195">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="3e46e-196">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-196">**Notes**:</span></span>

<span data-ttu-id="3e46e-197">Distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="3e46e-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="3e46e-198">activity</span><span class="sxs-lookup"><span data-stu-id="3e46e-198">activity</span></span>
<span data-ttu-id="3e46e-199">**Operadores compatibles**: eq, contains y startsWith</span><span class="sxs-lookup"><span data-stu-id="3e46e-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="3e46e-200">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="3e46e-201">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-201">**Notes**:</span></span>

<span data-ttu-id="3e46e-202">Distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="3e46e-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="3e46e-203">actor/name</span><span class="sxs-lookup"><span data-stu-id="3e46e-203">actor/name</span></span>
<span data-ttu-id="3e46e-204">**Operadores compatibles**: eq, contains y startsWith</span><span class="sxs-lookup"><span data-stu-id="3e46e-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="3e46e-205">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="3e46e-206">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-206">**Notes**:</span></span>

<span data-ttu-id="3e46e-207">No distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="3e46e-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="3e46e-208">actor/objectid</span><span class="sxs-lookup"><span data-stu-id="3e46e-208">actor/objectId</span></span>
<span data-ttu-id="3e46e-209">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="3e46e-209">**Supported operators**: eq</span></span>

<span data-ttu-id="3e46e-210">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="3e46e-211">target/namde</span><span class="sxs-lookup"><span data-stu-id="3e46e-211">target/name</span></span>
<span data-ttu-id="3e46e-212">**Operadores compatibles**: eq, contains y startsWith</span><span class="sxs-lookup"><span data-stu-id="3e46e-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="3e46e-213">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="3e46e-214">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-214">**Notes**:</span></span>

<span data-ttu-id="3e46e-215">No distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="3e46e-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="3e46e-216">target/upn</span><span class="sxs-lookup"><span data-stu-id="3e46e-216">target/upn</span></span>
<span data-ttu-id="3e46e-217">**Operadores compatibles**: eq y startsWith</span><span class="sxs-lookup"><span data-stu-id="3e46e-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="3e46e-218">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="3e46e-219">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-219">**Notes**:</span></span>

* <span data-ttu-id="3e46e-220">No distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="3e46e-220">Case-insensitive</span></span>
* <span data-ttu-id="3e46e-221">Se necesita espacio de nombres completo de tooadd Hola consultar Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span><span class="sxs-lookup"><span data-stu-id="3e46e-221">You need tooadd hello full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="3e46e-222">target/objectid</span><span class="sxs-lookup"><span data-stu-id="3e46e-222">target/objectId</span></span>
<span data-ttu-id="3e46e-223">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="3e46e-223">**Supported operators**: eq</span></span>

<span data-ttu-id="3e46e-224">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="3e46e-225">actor/upn</span><span class="sxs-lookup"><span data-stu-id="3e46e-225">actor/upn</span></span>
<span data-ttu-id="3e46e-226">**Operadores compatibles**: eq y startsWith</span><span class="sxs-lookup"><span data-stu-id="3e46e-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="3e46e-227">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="3e46e-228">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="3e46e-228">**Notes**:</span></span>

* <span data-ttu-id="3e46e-229">No distingue mayúsculas de minúsculas.</span><span class="sxs-lookup"><span data-stu-id="3e46e-229">Case-insensitive</span></span> 
* <span data-ttu-id="3e46e-230">Se necesita espacio de nombres completo de tooadd Hola consultar Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span><span class="sxs-lookup"><span data-stu-id="3e46e-230">You need tooadd hello full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="3e46e-231">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3e46e-231">Next Steps</span></span>
* <span data-ttu-id="3e46e-232">¿Desea toosee ejemplos para las actividades de filtrado de sistema?</span><span class="sxs-lookup"><span data-stu-id="3e46e-232">Do you want toosee examples for filtered system activities?</span></span> <span data-ttu-id="3e46e-233">Extraer del repositorio hello [ejemplos de API de auditoría de Azure Active Directory](active-directory-reporting-api-audit-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3e46e-233">Check out hello [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="3e46e-234">¿Desea más información acerca de la API de generación de informes de hello Azure AD tooknow?</span><span class="sxs-lookup"><span data-stu-id="3e46e-234">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="3e46e-235">Vea [Introducción a Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="3e46e-235">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

