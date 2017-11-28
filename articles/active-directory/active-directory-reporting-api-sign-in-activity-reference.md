---
title: "informe de actividad de aaaAzure inicio de sesión de Active Directory referencia de API | Documentos de Microsoft"
description: "Referencia de API de informe de actividad de hello en el inicio de sesión de Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ddcd9ae0-f6b7-4f13-a5e1-6cbf51a25634
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 8123f308a291503f2c61ac5de26696806c6402ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a><span data-ttu-id="e43e5-103">Referencia de la API de informes de actividad de inicio de sesión de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e43e5-103">Azure Active Directory sign-in activity report API reference</span></span>
<span data-ttu-id="e43e5-104">Este tema forma parte de una colección de temas sobre hello Azure Active Directory API de informes.</span><span class="sxs-lookup"><span data-stu-id="e43e5-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="e43e5-105">Reporting de Azure AD proporciona una API que permite los datos del informe de actividad de inicio de sesión tooaccess mediante código o herramientas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="e43e5-105">Azure AD reporting provides you with an API that enables you tooaccess sign-in activity report data using code or related tools.</span></span>
<span data-ttu-id="e43e5-106">ámbito de Hola de este tema es tooprovide, con información de referencia sobre hello **API de informes de actividad de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="e43e5-106">hello scope of this topic is tooprovide you with reference information about hello **sign-in activity report API**.</span></span>

<span data-ttu-id="e43e5-107">Consulte:</span><span class="sxs-lookup"><span data-stu-id="e43e5-107">See:</span></span>

* <span data-ttu-id="e43e5-108">[Actividades de inicio de sesión](active-directory-reporting-azure-portal.md#activity-reports) para obtener más información</span><span class="sxs-lookup"><span data-stu-id="e43e5-108">[Sign-in activities](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="e43e5-109">[Introducción a Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md) para obtener más información acerca de la API de informes de Hola.</span><span class="sxs-lookup"><span data-stu-id="e43e5-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


## <a name="who-can-access-hello-api-data"></a><span data-ttu-id="e43e5-110">¿Quién puede acceder a datos de la API de saludo?</span><span class="sxs-lookup"><span data-stu-id="e43e5-110">Who can access hello API data?</span></span>
* <span data-ttu-id="e43e5-111">Los usuarios y entidades de servicio de rol de administrador de seguridad o seguridad Reader de Hola</span><span class="sxs-lookup"><span data-stu-id="e43e5-111">Users and Service Principals in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="e43e5-112">Administradores globales</span><span class="sxs-lookup"><span data-stu-id="e43e5-112">Global Admins</span></span>
* <span data-ttu-id="e43e5-113">Cualquier aplicación que tenga autorización tooaccess Hola API (autorización de la aplicación puede ser el programa de instalación solamente basándose en el permiso del administrador Global)</span><span class="sxs-lookup"><span data-stu-id="e43e5-113">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

<span data-ttu-id="e43e5-114">acceso de tooconfigure para una aplicación tooaccess las API de seguridad tales como eventos de inicio de sesión, Hola de uso derivados de la solicitud de hello tooadd de PowerShell entidad de servicio en función de lector de seguridad de Hola</span><span class="sxs-lookup"><span data-stu-id="e43e5-114">tooconfigure access for an application tooaccess security APIs such as signin events, use hello following PowerShell tooadd hello applications Service Principal into hello Security Reader role</span></span>

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a><span data-ttu-id="e43e5-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="e43e5-115">Prerequisites</span></span>
<span data-ttu-id="e43e5-116">Hola a tooaccess este informe a través de la API de generación de informes, debe tener:</span><span class="sxs-lookup"><span data-stu-id="e43e5-116">tooaccess this report through hello reporting API, you must have:</span></span>

* <span data-ttu-id="e43e5-117">Tener una [edición de Azure Active Directory Premium P1 o P2](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="e43e5-117">An [Azure Active Directory Premium P1 or P2 edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="e43e5-118">Hola completado [API de generación de informes de requisitos previos tooaccess hello Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="e43e5-118">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="e43e5-119">Obtener acceso a las API de Hola</span><span class="sxs-lookup"><span data-stu-id="e43e5-119">Accessing hello API</span></span>
<span data-ttu-id="e43e5-120">Se puede tener acceso a esta API a través de hello [Explorador de gráficos](https://graphexplorer2.cloudapp.net) o mediante programación con, por ejemplo, PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e43e5-120">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="e43e5-121">En orden para PowerShell toocorrectly interpretar la sintaxis de filtros de OData Hola utilizada en las llamadas de REST de AAD Graph, debe usar acento grave hello (también conocido como: acento grave) carácter demasiado "carácter de escape" hello $.</span><span class="sxs-lookup"><span data-stu-id="e43e5-121">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="e43e5-122">carácter de acento grave Hola actúa como [carácter de escape de PowerShell](https://technet.microsoft.com/library/hh847755.aspx), lo que PowerShell toodo una interpretación literal de carácter de hello $ y evitar confundir como un nombre de variable de PowerShell (es decir: $filter).</span><span class="sxs-lookup"><span data-stu-id="e43e5-122">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="e43e5-123">Hola de este tema es Hola Explorador de gráficos.</span><span class="sxs-lookup"><span data-stu-id="e43e5-123">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="e43e5-124">Para ver un ejemplo de PowerShell, consulte este [script de PowerShell](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="e43e5-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="e43e5-125">Punto de conexión de API</span><span class="sxs-lookup"><span data-stu-id="e43e5-125">API Endpoint</span></span>
<span data-ttu-id="e43e5-126">Puede tener acceso a esta API con hello siguiente URI base:</span><span class="sxs-lookup"><span data-stu-id="e43e5-126">You can access this API using hello following base URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



<span data-ttu-id="e43e5-127">Debido a toohello el volumen de datos, esta API tiene un límite de un millón de registros devueltos.</span><span class="sxs-lookup"><span data-stu-id="e43e5-127">Due toohello volume of data, this API has a limit of one million returned records.</span></span> 

<span data-ttu-id="e43e5-128">Esta llamada devuelve datos de hello en lotes.</span><span class="sxs-lookup"><span data-stu-id="e43e5-128">This call returns hello data in batches.</span></span> <span data-ttu-id="e43e5-129">Cada lote tiene un máximo de 1000 registros.</span><span class="sxs-lookup"><span data-stu-id="e43e5-129">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="e43e5-130">tooget Hola siguiente lote de registros, use Hola siguiente vínculo.</span><span class="sxs-lookup"><span data-stu-id="e43e5-130">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="e43e5-131">Obtener hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) información del primer conjunto de registros devueltos de Hola.</span><span class="sxs-lookup"><span data-stu-id="e43e5-131">Get hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) information from hello first set of returned records.</span></span> <span data-ttu-id="e43e5-132">token de omisión de Hello será final Hola Hola de conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="e43e5-132">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a><span data-ttu-id="e43e5-133">Filtros admitidos</span><span class="sxs-lookup"><span data-stu-id="e43e5-133">Supported filters</span></span>
<span data-ttu-id="e43e5-134">Puede limitar número de Hola de registros devueltos por una API de llamar a en forma de un filtro.</span><span class="sxs-lookup"><span data-stu-id="e43e5-134">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="e43e5-135">Para inicio de sesión de la API se admiten datos relacionados, Hola después de filtros:</span><span class="sxs-lookup"><span data-stu-id="e43e5-135">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="e43e5-136">**$top =\<devolvió un número de registros toobe\>**  -número de hello toolimit de registros devueltos.</span><span class="sxs-lookup"><span data-stu-id="e43e5-136">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="e43e5-137">Se trata de una operación costosa.</span><span class="sxs-lookup"><span data-stu-id="e43e5-137">This is an expensive operation.</span></span> <span data-ttu-id="e43e5-138">No se debe usar este filtro si desea tooreturn miles de objetos.</span><span class="sxs-lookup"><span data-stu-id="e43e5-138">You should not use this filter if you want tooreturn thousands of objects.</span></span>  
* <span data-ttu-id="e43e5-139">**$filter =\<la instrucción de filtro\>**  -toospecify, en función de Hola de campos de filtro admitido, tipo de Hola de registros que le interesa</span><span class="sxs-lookup"><span data-stu-id="e43e5-139">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="e43e5-140">Operadores y campos de filtro compatibles</span><span class="sxs-lookup"><span data-stu-id="e43e5-140">Supported filter fields and operators</span></span>
<span data-ttu-id="e43e5-141">tipo de hello toospecify de registros que le interesa, puede crear una instrucción de filtro que puede contener uno o una combinación de hello después de los campos de filtro:</span><span class="sxs-lookup"><span data-stu-id="e43e5-141">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="e43e5-142">[signinDateTime](#signindatetime) : define una fecha o un intervalo de fechas.</span><span class="sxs-lookup"><span data-stu-id="e43e5-142">[signinDateTime](#signindatetime) - defines a date or date range</span></span>
* <span data-ttu-id="e43e5-143">[identificador de usuario](#userid) -define el identificador. del usuario de hello en función de usuario específico</span><span class="sxs-lookup"><span data-stu-id="e43e5-143">[userId](#userid) - defines a specific user based hello user's ID.</span></span>
* <span data-ttu-id="e43e5-144">[userPrincipalName](#userprincipalname) -define el nombre principal de usuario (UPN) de un usuario de hello en función de usuario específico</span><span class="sxs-lookup"><span data-stu-id="e43e5-144">[userPrincipalName](#userprincipalname) - defines a specific user based hello user's user principal name (UPN)</span></span>
* <span data-ttu-id="e43e5-145">[appId](#appid) -define el identificador de la aplicación de hello en función de aplicación específica</span><span class="sxs-lookup"><span data-stu-id="e43e5-145">[appId](#appid) - defines a specific app based hello app's ID</span></span>
* <span data-ttu-id="e43e5-146">[appDisplayName](#appdisplayname) -define el nombre para mostrar la aplicación de hello en función de aplicación específica</span><span class="sxs-lookup"><span data-stu-id="e43e5-146">[appDisplayName](#appdisplayname) - defines a specific app based hello app's display name</span></span>
* <span data-ttu-id="e43e5-147">[loginStatus](#loginStatus) -define el estado de Hola de inicios de sesión de hello (éxito o error)</span><span class="sxs-lookup"><span data-stu-id="e43e5-147">[loginStatus](#loginStatus) - defines hello status of hello logins (success / failure)</span></span>

> [!NOTE]
> <span data-ttu-id="e43e5-148">Al utilizar el Explorador de gráfico, Hola necesita toouse Hola correcto de caso para cada letra es los campos de filtro.</span><span class="sxs-lookup"><span data-stu-id="e43e5-148">When using Graph Explorer, you hello need toouse hello correct case for each letter is your filter fields.</span></span>
> 
> 

<span data-ttu-id="e43e5-149">toonarrow ámbito Hola de hello devolvió datos, puede crear combinaciones de filtros de hello compatible y campos de filtro.</span><span class="sxs-lookup"><span data-stu-id="e43e5-149">toonarrow down hello scope of hello returned data, you can build combinations of hello supported filters and filter fields.</span></span> <span data-ttu-id="e43e5-150">Por ejemplo, hello siguiente instrucción devuelve Hola top 10 registros entre el 1 de julio de 2016 y 6 de julio de 2016:</span><span class="sxs-lookup"><span data-stu-id="e43e5-150">For example, hello following statement returns hello top 10 records between July 1st 2016 and July 6th 2016:</span></span>

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a><span data-ttu-id="e43e5-151">signinDateTime</span><span class="sxs-lookup"><span data-stu-id="e43e5-151">signinDateTime</span></span>
<span data-ttu-id="e43e5-152">**Operadores compatibles**: eq, ge, le, gt y lt</span><span class="sxs-lookup"><span data-stu-id="e43e5-152">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="e43e5-153">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="e43e5-153">**Example**:</span></span>

<span data-ttu-id="e43e5-154">Uso de una fecha concreta</span><span class="sxs-lookup"><span data-stu-id="e43e5-154">Using a specific date</span></span>

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



<span data-ttu-id="e43e5-155">Uso de un intervalo de fechas</span><span class="sxs-lookup"><span data-stu-id="e43e5-155">Using a date range</span></span>    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


<span data-ttu-id="e43e5-156">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="e43e5-156">**Notes**:</span></span>

<span data-ttu-id="e43e5-157">parámetro de fecha y hora de Hello debe estar en formato de hora UTC de Hola</span><span class="sxs-lookup"><span data-stu-id="e43e5-157">hello datetime parameter should be in hello UTC format</span></span> 

- - -
### <a name="userid"></a><span data-ttu-id="e43e5-158">userId</span><span class="sxs-lookup"><span data-stu-id="e43e5-158">userId</span></span>
<span data-ttu-id="e43e5-159">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="e43e5-159">**Supported operators**: eq</span></span>

<span data-ttu-id="e43e5-160">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="e43e5-160">**Example**:</span></span>

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

<span data-ttu-id="e43e5-161">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="e43e5-161">**Notes**:</span></span>

<span data-ttu-id="e43e5-162">Hola de identificador de usuario es un valor de cadena</span><span class="sxs-lookup"><span data-stu-id="e43e5-162">hello value of userId is a string value</span></span>

- - -
### <a name="userprincipalname"></a><span data-ttu-id="e43e5-163">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="e43e5-163">userPrincipalName</span></span>
<span data-ttu-id="e43e5-164">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="e43e5-164">**Supported operators**: eq</span></span>

<span data-ttu-id="e43e5-165">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="e43e5-165">**Example**:</span></span>

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


<span data-ttu-id="e43e5-166">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="e43e5-166">**Notes**:</span></span>

<span data-ttu-id="e43e5-167">Hola de userPrincipalName es un valor de cadena</span><span class="sxs-lookup"><span data-stu-id="e43e5-167">hello value of userPrincipalName is a string value</span></span>

- - -
### <a name="appid"></a><span data-ttu-id="e43e5-168">appId</span><span class="sxs-lookup"><span data-stu-id="e43e5-168">appId</span></span>
<span data-ttu-id="e43e5-169">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="e43e5-169">**Supported operators**: eq</span></span>

<span data-ttu-id="e43e5-170">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="e43e5-170">**Example**:</span></span>

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



<span data-ttu-id="e43e5-171">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="e43e5-171">**Notes**:</span></span>

<span data-ttu-id="e43e5-172">Hola de appId es un valor de cadena</span><span class="sxs-lookup"><span data-stu-id="e43e5-172">hello value of appId is a string value</span></span>

- - -
### <a name="appdisplayname"></a><span data-ttu-id="e43e5-173">appDisplayName</span><span class="sxs-lookup"><span data-stu-id="e43e5-173">appDisplayName</span></span>
<span data-ttu-id="e43e5-174">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="e43e5-174">**Supported operators**: eq</span></span>

<span data-ttu-id="e43e5-175">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="e43e5-175">**Example**:</span></span>

    $filter=appDisplayName+eq+'Azure+Portal' 


<span data-ttu-id="e43e5-176">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="e43e5-176">**Notes**:</span></span>

<span data-ttu-id="e43e5-177">Hola de appDisplayName es un valor de cadena</span><span class="sxs-lookup"><span data-stu-id="e43e5-177">hello value of appDisplayName is a string value</span></span>

- - -
### <a name="loginstatus"></a><span data-ttu-id="e43e5-178">loginStatus</span><span class="sxs-lookup"><span data-stu-id="e43e5-178">loginStatus</span></span>
<span data-ttu-id="e43e5-179">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="e43e5-179">**Supported operators**: eq</span></span>

<span data-ttu-id="e43e5-180">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="e43e5-180">**Example**:</span></span>

    $filter=loginStatus+eq+'1'  


<span data-ttu-id="e43e5-181">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="e43e5-181">**Notes**:</span></span>

<span data-ttu-id="e43e5-182">Hay dos opciones para hello loginStatus: 0 - se ejecuta correctamente, 1 - error</span><span class="sxs-lookup"><span data-stu-id="e43e5-182">There are two options for hello loginStatus: 0 - success, 1 - failure</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="e43e5-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="e43e5-183">Next steps</span></span>
* <span data-ttu-id="e43e5-184">¿Desea toosee ejemplos de actividades de inicio de sesión filtradas?</span><span class="sxs-lookup"><span data-stu-id="e43e5-184">Do you want toosee examples for filtered sign-in activities?</span></span> <span data-ttu-id="e43e5-185">Extraer del repositorio hello [ejemplos de API de informes de actividad de inicio de sesión de Azure Active Directory](active-directory-reporting-api-sign-in-activity-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e43e5-185">Check out hello [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-samples.md).</span></span>
* <span data-ttu-id="e43e5-186">¿Desea más información acerca de la API de generación de informes de hello Azure AD tooknow?</span><span class="sxs-lookup"><span data-stu-id="e43e5-186">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="e43e5-187">Vea [Introducción a Azure Active Directory Reporting API hello](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="e43e5-187">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

