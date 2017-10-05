---
title: "Referencia de la API de informes de actividad de inicio de sesión de Azure Active Directory | Microsoft Docs"
description: "Referencia de la API de informes de actividad de inicio de sesión de Azure Active Directory"
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
ms.openlocfilehash: d83f1a899ba38dab2c1c1661adede87db6f88c20
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a><span data-ttu-id="320b4-103">Referencia de la API de informes de actividad de inicio de sesión de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="320b4-103">Azure Active Directory sign-in activity report API reference</span></span>
<span data-ttu-id="320b4-104">Este tema forma parte de una serie de temas sobre la API de informes de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="320b4-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="320b4-105">La característica de generación de informes de Azure AD proporciona una API que permite acceder a los datos de informes de actividades de inicio de sesión mediante el uso de código o herramientas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="320b4-105">Azure AD reporting provides you with an API that enables you to access sign-in activity report data using code or related tools.</span></span>
<span data-ttu-id="320b4-106">El objetivo de este tema es ofrecer información de referencia sobre la **API de informes de actividad de inicio de sesión**.</span><span class="sxs-lookup"><span data-stu-id="320b4-106">The scope of this topic is to provide you with reference information about the **sign-in activity report API**.</span></span>

<span data-ttu-id="320b4-107">Consulte:</span><span class="sxs-lookup"><span data-stu-id="320b4-107">See:</span></span>

* <span data-ttu-id="320b4-108">[Actividades de inicio de sesión](active-directory-reporting-azure-portal.md#activity-reports) para obtener más información</span><span class="sxs-lookup"><span data-stu-id="320b4-108">[Sign-in activities](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="320b4-109">[Introducción a la API de generación de informes de Azure Active Directory](active-directory-reporting-api-getting-started.md) para obtener más información sobre esta API</span><span class="sxs-lookup"><span data-stu-id="320b4-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


## <a name="who-can-access-the-api-data"></a><span data-ttu-id="320b4-110">¿Quién puede acceder a los datos de la API?</span><span class="sxs-lookup"><span data-stu-id="320b4-110">Who can access the API data?</span></span>
* <span data-ttu-id="320b4-111">Usuarios y entidades de seguridad de los roles de administrador o lector de seguridad</span><span class="sxs-lookup"><span data-stu-id="320b4-111">Users and Service Principals in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="320b4-112">Administradores globales</span><span class="sxs-lookup"><span data-stu-id="320b4-112">Global Admins</span></span>
* <span data-ttu-id="320b4-113">Cualquier aplicación que tenga autorización para acceder a la API (la autorización de aplicaciones solo puede configurarse según los permisos del administrador global).</span><span class="sxs-lookup"><span data-stu-id="320b4-113">Any app that has authorization to access the API (app authorization can be setup only based on Global Admin’s permission)</span></span>

<span data-ttu-id="320b4-114">Para configurar el acceso a fin de que una aplicación tenga acceso a API de seguridad tales como eventos de inicio de sesión, use el siguiente PowerShell para agregar la entidad de servicio de las aplicaciones al rol de lector de seguridad</span><span class="sxs-lookup"><span data-stu-id="320b4-114">To configure access for an application to access security APIs such as signin events, use the following PowerShell to add the applications Service Principal into the Security Reader role</span></span>

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a><span data-ttu-id="320b4-115">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="320b4-115">Prerequisites</span></span>
<span data-ttu-id="320b4-116">Para acceder a este informe a través de la API de generación de informes, debe cumplir los siguientes requisitos:</span><span class="sxs-lookup"><span data-stu-id="320b4-116">To access this report through the reporting API, you must have:</span></span>

* <span data-ttu-id="320b4-117">Tener una [edición de Azure Active Directory Premium P1 o P2](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="320b4-117">An [Azure Active Directory Premium P1 or P2 edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="320b4-118">Completar los [requisitos previos para acceder a la API de generación de informes de Azure AD](active-directory-reporting-api-prerequisites.md)</span><span class="sxs-lookup"><span data-stu-id="320b4-118">Completed the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-the-api"></a><span data-ttu-id="320b4-119">Acceso a la API</span><span class="sxs-lookup"><span data-stu-id="320b4-119">Accessing the API</span></span>
<span data-ttu-id="320b4-120">Puede acceder a esta API a través del [Probador de Graph](https://graphexplorer2.cloudapp.net) o mediante programación con, por ejemplo, PowerShell.</span><span class="sxs-lookup"><span data-stu-id="320b4-120">You can either access this API through the [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="320b4-121">Para que PowerShell pueda interpretar correctamente la sintaxis de filtro de OData empleada en las llamadas a la API REST Graph de AAD, debe usar el carácter de acento grave para escapar $.</span><span class="sxs-lookup"><span data-stu-id="320b4-121">In order for PowerShell to correctly interpret the OData filter syntax used in AAD Graph REST calls, you must use the backtick (aka: grave accent) character to “escape” the $ character.</span></span> <span data-ttu-id="320b4-122">El carácter de acento grave actúa como [carácter de escape de PowerShell](https://technet.microsoft.com/library/hh847755.aspx), de modo que PowerShell puede hacer una interpretación literal del carácter $ y evitar que lo confunda con un nombre de variable de PowerShell (por ejemplo, $filter).</span><span class="sxs-lookup"><span data-stu-id="320b4-122">The backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell to do a literal interpretation of the $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="320b4-123">Este tema se centra en el Probador de Graph.</span><span class="sxs-lookup"><span data-stu-id="320b4-123">The focus of this topic is on the Graph Explorer.</span></span> <span data-ttu-id="320b4-124">Para ver un ejemplo de PowerShell, consulte este [script de PowerShell](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="320b4-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="320b4-125">Punto de conexión de API</span><span class="sxs-lookup"><span data-stu-id="320b4-125">API Endpoint</span></span>
<span data-ttu-id="320b4-126">Puede acceder a esta API con el siguiente URI base:</span><span class="sxs-lookup"><span data-stu-id="320b4-126">You can access this API using the following base URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



<span data-ttu-id="320b4-127">Debido al volumen de datos, esta API tiene un límite de un millón de registros devueltos.</span><span class="sxs-lookup"><span data-stu-id="320b4-127">Due to the volume of data, this API has a limit of one million returned records.</span></span> 

<span data-ttu-id="320b4-128">Esta llamada devuelve los datos en lotes.</span><span class="sxs-lookup"><span data-stu-id="320b4-128">This call returns the data in batches.</span></span> <span data-ttu-id="320b4-129">Cada lote tiene un máximo de 1000 registros.</span><span class="sxs-lookup"><span data-stu-id="320b4-129">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="320b4-130">Para obtener el siguiente lote de registros, haga clic en el vínculo Siguiente.</span><span class="sxs-lookup"><span data-stu-id="320b4-130">To get the next batch of records, use the Next link.</span></span> <span data-ttu-id="320b4-131">Obtenga la información de [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) desde el primer conjunto de registros devueltos.</span><span class="sxs-lookup"><span data-stu-id="320b4-131">Get the [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) information from the first set of returned records.</span></span> <span data-ttu-id="320b4-132">El token de omisión estará al final del conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="320b4-132">The skip token will be at the end of the result set.</span></span>  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a><span data-ttu-id="320b4-133">Filtros admitidos</span><span class="sxs-lookup"><span data-stu-id="320b4-133">Supported filters</span></span>
<span data-ttu-id="320b4-134">Puede limitar el número de registros que se devuelven mediante una llamada de API usando un filtro.</span><span class="sxs-lookup"><span data-stu-id="320b4-134">You can narrow down the number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="320b4-135">En lo que respecta a los datos relacionados con las API de inicio de sesión, se admiten los siguientes filtros:</span><span class="sxs-lookup"><span data-stu-id="320b4-135">For sign-in API related data, the following filters are supported:</span></span>

* <span data-ttu-id="320b4-136">**$top=\<número de registros que se devolverán\>**: limita el número de registros devueltos.</span><span class="sxs-lookup"><span data-stu-id="320b4-136">**$top=\<number of records to be returned\>** - to limit the number of returned records.</span></span> <span data-ttu-id="320b4-137">Se trata de una operación costosa.</span><span class="sxs-lookup"><span data-stu-id="320b4-137">This is an expensive operation.</span></span> <span data-ttu-id="320b4-138">No debe utilizar este filtro si quiere devolver miles de objetos.</span><span class="sxs-lookup"><span data-stu-id="320b4-138">You should not use this filter if you want to return thousands of objects.</span></span>  
* <span data-ttu-id="320b4-139">**$filter=\<instrucción de filtro\>**: para especificar, en función de los campos de filtro compatibles, el tipo de registros que le interesan</span><span class="sxs-lookup"><span data-stu-id="320b4-139">**$filter=\<your filter statement\>** - to specify, on the basis of supported filter fields, the type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="320b4-140">Operadores y campos de filtro compatibles</span><span class="sxs-lookup"><span data-stu-id="320b4-140">Supported filter fields and operators</span></span>
<span data-ttu-id="320b4-141">Para especificar el tipo de registros que le interesa, puede crear una instrucción de filtro que puede contener uno o una combinación de los campos de filtro siguientes:</span><span class="sxs-lookup"><span data-stu-id="320b4-141">To specify the type of records you care about, you can build a filter statement that can contain either one or a combination of the following filter fields:</span></span>

* <span data-ttu-id="320b4-142">[signinDateTime](#signindatetime) : define una fecha o un intervalo de fechas.</span><span class="sxs-lookup"><span data-stu-id="320b4-142">[signinDateTime](#signindatetime) - defines a date or date range</span></span>
* <span data-ttu-id="320b4-143">[userId](#userid) : define un determinado usuario según su identificador.</span><span class="sxs-lookup"><span data-stu-id="320b4-143">[userId](#userid) - defines a specific user based the user's ID.</span></span>
* <span data-ttu-id="320b4-144">[userPrincipalName](#userprincipalname) : define un determinado usuario según el nombre principal del usuario (UPN).</span><span class="sxs-lookup"><span data-stu-id="320b4-144">[userPrincipalName](#userprincipalname) - defines a specific user based the user's user principal name (UPN)</span></span>
* <span data-ttu-id="320b4-145">[appId](#appid) : define una determinada aplicación según el identificador de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="320b4-145">[appId](#appid) - defines a specific app based the app's ID</span></span>
* <span data-ttu-id="320b4-146">[appDisplayName](#appdisplayname) : define una determinada aplicación según el nombre para mostrar de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="320b4-146">[appDisplayName](#appdisplayname) - defines a specific app based the app's display name</span></span>
* <span data-ttu-id="320b4-147">[loginStatus](#loginStatus) : define el estado de los inicios de sesión (success o failure).</span><span class="sxs-lookup"><span data-stu-id="320b4-147">[loginStatus](#loginStatus) - defines the status of the logins (success / failure)</span></span>

> [!NOTE]
> <span data-ttu-id="320b4-148">Al utilizar el Probador de Graph, tenga en cuenta que los campos de filtro distinguen mayúsculas y minúsculas.</span><span class="sxs-lookup"><span data-stu-id="320b4-148">When using Graph Explorer, you the need to use the correct case for each letter is your filter fields.</span></span>
> 
> 

<span data-ttu-id="320b4-149">Para limitar el ámbito de los datos devueltos, puede crear combinaciones de los filtros y campos de filtro disponibles.</span><span class="sxs-lookup"><span data-stu-id="320b4-149">To narrow down the scope of the returned data, you can build combinations of the supported filters and filter fields.</span></span> <span data-ttu-id="320b4-150">Por ejemplo, la siguiente instrucción devuelve los 10 principales registros entre el 1 y el 6 de julio de 2016:</span><span class="sxs-lookup"><span data-stu-id="320b4-150">For example, the following statement returns the top 10 records between July 1st 2016 and July 6th 2016:</span></span>

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a><span data-ttu-id="320b4-151">signinDateTime</span><span class="sxs-lookup"><span data-stu-id="320b4-151">signinDateTime</span></span>
<span data-ttu-id="320b4-152">**Operadores compatibles**: eq, ge, le, gt y lt</span><span class="sxs-lookup"><span data-stu-id="320b4-152">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="320b4-153">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="320b4-153">**Example**:</span></span>

<span data-ttu-id="320b4-154">Uso de una fecha concreta</span><span class="sxs-lookup"><span data-stu-id="320b4-154">Using a specific date</span></span>

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



<span data-ttu-id="320b4-155">Uso de un intervalo de fechas</span><span class="sxs-lookup"><span data-stu-id="320b4-155">Using a date range</span></span>    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


<span data-ttu-id="320b4-156">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="320b4-156">**Notes**:</span></span>

<span data-ttu-id="320b4-157">El parámetro datetime debe estar en formato UTC</span><span class="sxs-lookup"><span data-stu-id="320b4-157">The datetime parameter should be in the UTC format</span></span> 

- - -
### <a name="userid"></a><span data-ttu-id="320b4-158">userId</span><span class="sxs-lookup"><span data-stu-id="320b4-158">userId</span></span>
<span data-ttu-id="320b4-159">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="320b4-159">**Supported operators**: eq</span></span>

<span data-ttu-id="320b4-160">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="320b4-160">**Example**:</span></span>

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

<span data-ttu-id="320b4-161">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="320b4-161">**Notes**:</span></span>

<span data-ttu-id="320b4-162">El valor de userId es un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="320b4-162">The value of userId is a string value</span></span>

- - -
### <a name="userprincipalname"></a><span data-ttu-id="320b4-163">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="320b4-163">userPrincipalName</span></span>
<span data-ttu-id="320b4-164">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="320b4-164">**Supported operators**: eq</span></span>

<span data-ttu-id="320b4-165">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="320b4-165">**Example**:</span></span>

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


<span data-ttu-id="320b4-166">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="320b4-166">**Notes**:</span></span>

<span data-ttu-id="320b4-167">El valor de userPrincipalName es un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="320b4-167">The value of userPrincipalName is a string value</span></span>

- - -
### <a name="appid"></a><span data-ttu-id="320b4-168">appId</span><span class="sxs-lookup"><span data-stu-id="320b4-168">appId</span></span>
<span data-ttu-id="320b4-169">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="320b4-169">**Supported operators**: eq</span></span>

<span data-ttu-id="320b4-170">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="320b4-170">**Example**:</span></span>

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



<span data-ttu-id="320b4-171">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="320b4-171">**Notes**:</span></span>

<span data-ttu-id="320b4-172">El valor de appId es un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="320b4-172">The value of appId is a string value</span></span>

- - -
### <a name="appdisplayname"></a><span data-ttu-id="320b4-173">appDisplayName</span><span class="sxs-lookup"><span data-stu-id="320b4-173">appDisplayName</span></span>
<span data-ttu-id="320b4-174">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="320b4-174">**Supported operators**: eq</span></span>

<span data-ttu-id="320b4-175">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="320b4-175">**Example**:</span></span>

    $filter=appDisplayName+eq+'Azure+Portal' 


<span data-ttu-id="320b4-176">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="320b4-176">**Notes**:</span></span>

<span data-ttu-id="320b4-177">El valor de appDisplayName es un valor de cadena.</span><span class="sxs-lookup"><span data-stu-id="320b4-177">The value of appDisplayName is a string value</span></span>

- - -
### <a name="loginstatus"></a><span data-ttu-id="320b4-178">loginStatus</span><span class="sxs-lookup"><span data-stu-id="320b4-178">loginStatus</span></span>
<span data-ttu-id="320b4-179">**Operadores compatibles**: eq</span><span class="sxs-lookup"><span data-stu-id="320b4-179">**Supported operators**: eq</span></span>

<span data-ttu-id="320b4-180">**Ejemplo**:</span><span class="sxs-lookup"><span data-stu-id="320b4-180">**Example**:</span></span>

    $filter=loginStatus+eq+'1'  


<span data-ttu-id="320b4-181">**Notas**:</span><span class="sxs-lookup"><span data-stu-id="320b4-181">**Notes**:</span></span>

<span data-ttu-id="320b4-182">Hay dos opciones para loginStatus: 0: success; 1: failure</span><span class="sxs-lookup"><span data-stu-id="320b4-182">There are two options for the loginStatus: 0 - success, 1 - failure</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="320b4-183">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="320b4-183">Next steps</span></span>
* <span data-ttu-id="320b4-184">¿Quiere ver ejemplos de actividades de inicio de sesión filtradas?</span><span class="sxs-lookup"><span data-stu-id="320b4-184">Do you want to see examples for filtered sign-in activities?</span></span> <span data-ttu-id="320b4-185">Consulte [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-samples.md)(Ejemplos de API de informes de actividad de inicio de sesión de Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="320b4-185">Check out the [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-samples.md).</span></span>
* <span data-ttu-id="320b4-186">¿Quiere obtener más información sobre la API de generación de informes de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="320b4-186">Do you want to know more about the Azure AD reporting API?</span></span> <span data-ttu-id="320b4-187">Consulte [Introducción a la API de informes de Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="320b4-187">See [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

