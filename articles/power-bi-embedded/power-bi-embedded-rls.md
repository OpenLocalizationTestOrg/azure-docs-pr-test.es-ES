---
title: seguridad de nivel de aaaRow con Power BI Embedded
description: "Más información sobre la seguridad de nivel de fila con Power BI Embedded"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 7936ade5-2c75-435b-8314-ea7ca815867a
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: 384f78826ecc710cf8f101b251ae68b074f3e98b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="row-level-security-with-power-bi-embedded"></a><span data-ttu-id="96013-103">Seguridad de nivel de fila con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="96013-103">Row level security with Power BI Embedded</span></span>

<span data-ttu-id="96013-104">Seguridad de nivel de fila (RLS) puede ser datos de tooparticular de acceso de usuario de toorestrict utilizados dentro de un informe o un conjunto de datos, permitiendo varias toouse distintos usuarios Hola mismo informe al ver todos los datos diferentes.</span><span class="sxs-lookup"><span data-stu-id="96013-104">Row level security (RLS) can be used toorestrict user access tooparticular data within a report or dataset, allowing for multiple different users toouse hello same report while all seeing different data.</span></span> <span data-ttu-id="96013-105">Power BI Embedded ahora admite conjuntos de datos configurados con RLS.</span><span class="sxs-lookup"><span data-stu-id="96013-105">Power BI Embedded now supports datasets configured with RLS.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-flow-1.png)

<span data-ttu-id="96013-106">En orden tootake aprovechar RLS, es importante que comprenda los conceptos principales tres; Los usuarios, Roles y reglas.</span><span class="sxs-lookup"><span data-stu-id="96013-106">In order tootake advantage of RLS, it’s important you understand three main concepts; Users, Roles, and Rules.</span></span> <span data-ttu-id="96013-107">Profundicemos en cada uno de ellos:</span><span class="sxs-lookup"><span data-stu-id="96013-107">Let’s take a closer look at each:</span></span>

<span data-ttu-id="96013-108">**Los usuarios** : estos son los usuarios finales real de hello ver informes.</span><span class="sxs-lookup"><span data-stu-id="96013-108">**Users** –  These are hello actual end-users viewing reports.</span></span> <span data-ttu-id="96013-109">En Power BI Embedded, los usuarios se identifican por la propiedad de nombre de usuario de hello en un Token de aplicación.</span><span class="sxs-lookup"><span data-stu-id="96013-109">In Power BI Embedded, users are identified by hello username property in an App Token.</span></span>

<span data-ttu-id="96013-110">**Roles** : los usuarios pertenecen tooroles.</span><span class="sxs-lookup"><span data-stu-id="96013-110">**Roles** – Users belong tooroles.</span></span> <span data-ttu-id="96013-111">Un rol es un contenedor de reglas y se puede adoptar un nombre como "Administrador de ventas" o "Representante de ventas".</span><span class="sxs-lookup"><span data-stu-id="96013-111">A role is a container for rules and can be named something like “Sales Manager” or “Sales Rep”.</span></span> <span data-ttu-id="96013-112">En Power BI Embedded, los usuarios se identifican por la propiedad de roles de hello en un Token de aplicación.</span><span class="sxs-lookup"><span data-stu-id="96013-112">In Power BI Embedded, users are identified by hello roles property in an App Token.</span></span>

<span data-ttu-id="96013-113">**Reglas de** : Roles tienen reglas, y dichas reglas son filtros real Hola va toobe aplica toohello datos.</span><span class="sxs-lookup"><span data-stu-id="96013-113">**Rules** – Roles have rules, and those rules are hello actual filters that are going toobe applied toohello data.</span></span> <span data-ttu-id="96013-114">Esto podría ser tan simple como "Country = USA" o algo mucho más dinámico.</span><span class="sxs-lookup"><span data-stu-id="96013-114">This could be as simple as “Country = USA” or something much more dynamic.</span></span>

### <a name="example"></a><span data-ttu-id="96013-115">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="96013-115">Example</span></span>

<span data-ttu-id="96013-116">Para el resto de Hola de este artículo, le presentaremos un ejemplo de creación de RLS y, a continuación, consumir dentro de una aplicación incrustada.</span><span class="sxs-lookup"><span data-stu-id="96013-116">For hello rest of this article, we’ll provide an example of authoring RLS, and then consuming that within an embedded application.</span></span> <span data-ttu-id="96013-117">El ejemplo usa hello [ejemplo de análisis de minoristas](http://go.microsoft.com/fwlink/?LinkID=780547) archivo PBIX.</span><span class="sxs-lookup"><span data-stu-id="96013-117">Our example uses hello [Retail Analysis Sample](http://go.microsoft.com/fwlink/?LinkID=780547) PBIX file.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-scenario-2.png)

<span data-ttu-id="96013-118">Nuestro ejemplo de análisis de minoristas muestra las ventas de todos los almacenes de hello en una cadena de venta específico.</span><span class="sxs-lookup"><span data-stu-id="96013-118">Our Retail Analysis sample shows sales for all hello stores in a particular retail chain.</span></span> <span data-ttu-id="96013-119">Sin RLS, con independencia de qué distrito administrador inicia sesión y vistas hello informe, verá Hola los mismos datos.</span><span class="sxs-lookup"><span data-stu-id="96013-119">Without RLS, no matter which district manager signs in and views hello report, they’ll see hello same data.</span></span> <span data-ttu-id="96013-120">Directivos determinó que cada administrador del distrito solo debe ver hello ventas para los almacenes de hello administran y toodo esto, podemos usar RLS.</span><span class="sxs-lookup"><span data-stu-id="96013-120">Senior management has determined each district manager should only see hello sales for hello stores they manage, and toodo this, we can use RLS.</span></span>

<span data-ttu-id="96013-121">RLS se ha creado en Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="96013-121">RLS is authored in Power BI Desktop.</span></span> <span data-ttu-id="96013-122">Cuando se abren el conjunto de datos de Hola y el informe, podemos cambiar esquema Hola de toodiagram vista toosee:</span><span class="sxs-lookup"><span data-stu-id="96013-122">When hello dataset and report are opened, we can switch toodiagram view toosee hello schema:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-3.png)

<span data-ttu-id="96013-123">A continuación, presentamos unos toonotice de cosas con este esquema:</span><span class="sxs-lookup"><span data-stu-id="96013-123">Here are a few things toonotice with this schema:</span></span>

* <span data-ttu-id="96013-124">Al igual que todas las medidas, **ventas totales**, se almacenan en hello **ventas** tabla de hechos.</span><span class="sxs-lookup"><span data-stu-id="96013-124">All measures, like **Total Sales**, are stored in hello **Sales** fact table.</span></span>
* <span data-ttu-id="96013-125">Hay cuatro tablas de dimensiones adicionales relacionadas: **Item**, **Time**, **Store** y **District**.</span><span class="sxs-lookup"><span data-stu-id="96013-125">There are four additional related dimension tables: **Item**, **Time**, **Store**, and **District**.</span></span>
* <span data-ttu-id="96013-126">las flechas de Hello en las líneas de relación de hello indican qué forma filtros pueden fluir de una tabla tooanother.</span><span class="sxs-lookup"><span data-stu-id="96013-126">hello arrows on hello relationship lines indicate which way filters can flow from one table tooanother.</span></span> <span data-ttu-id="96013-127">Por ejemplo, si se coloca un filtro en **tiempo [Date]**, en el esquema actual de hello sólo debería filtrar valores en hello **ventas** tabla.</span><span class="sxs-lookup"><span data-stu-id="96013-127">For example, if a filter is placed on **Time[Date]**, in hello current schema it would only filter down values in hello **Sales** table.</span></span> <span data-ttu-id="96013-128">Ninguna otra tabla se vería afectado por este filtro debido a que todos las flechas de hello en la tabla de ventas de punto toohello de líneas de relación de Hola y no inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="96013-128">No other tables would be affected by this filter since all of hello arrows on hello relationship lines point toohello sales table and not away.</span></span>
* <span data-ttu-id="96013-129">Hola **distrito** tabla indica quién es el director de Hola para cada distrito:</span><span class="sxs-lookup"><span data-stu-id="96013-129">hello **District** table indicates who hello manager is for each district:</span></span>
  
  ![](media/power-bi-embedded-rls/pbi-embedded-rls-district-table-4.png)

<span data-ttu-id="96013-130">Basada en este esquema, si se aplica un filtro toohello **administrador del distrito** columna Hola tabla distrito y si ese filtro coincide con usuario Hola Ver informe de hello, ese filtro también filtrará hacia abajo hello **almacén**y **ventas** tooonly tablas muestran datos de ese determinado distrito manager.</span><span class="sxs-lookup"><span data-stu-id="96013-130">Based on this schema, if we apply a filter toohello **District Manager** column in hello District table, and if that filter matches hello user viewing hello report, that filter will also filter down hello **Store** and **Sales** tables tooonly show data for that particular district manager.</span></span>

<span data-ttu-id="96013-131">Este es el procedimiento:</span><span class="sxs-lookup"><span data-stu-id="96013-131">Here’s how:</span></span>

1. <span data-ttu-id="96013-132">En la pestaña de modelado de hello, haga clic en **administrar funciones**.</span><span class="sxs-lookup"><span data-stu-id="96013-132">On hello Modeling tab, click **Manage Roles**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-modeling-tab-5.png)
2. <span data-ttu-id="96013-133">Cree un nuevo rol denominado **Manager**.</span><span class="sxs-lookup"><span data-stu-id="96013-133">Create a new role called **Manager**.</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-6.png)
3. <span data-ttu-id="96013-134">Hola **distrito** tabla escriba Hola siguiente expresión de DAX: **[Administrador del distrito] = USERNAME()**</span><span class="sxs-lookup"><span data-stu-id="96013-134">In hello **District** table enter hello following DAX expression: **[District Manager] = USERNAME()**</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-manager-role-7.png)
4. <span data-ttu-id="96013-135">toomake seguro Hola reglas funcionan, en hello **modelado** , haga clic en **ver como Roles**y escriba Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="96013-135">toomake sure hello rules are working, on hello **Modeling** tab, click **View as Roles**, and then enter hello following:</span></span>  
   ![](media/power-bi-embedded-rls/pbi-embedded-rls-view-as-roles-8.png)
   
   <span data-ttu-id="96013-136">Hello informes ahora mostrará datos como si se han iniciado sesión como **Andrew Ma**.</span><span class="sxs-lookup"><span data-stu-id="96013-136">hello reports will now show data as if you were signed in as **Andrew Ma**.</span></span>

<span data-ttu-id="96013-137">Aplicar filtro hello, Hola hicimos en este caso, se filtrará hacia abajo todos los registros de hello **distrito**, **almacén**, y **ventas** tablas.</span><span class="sxs-lookup"><span data-stu-id="96013-137">Applying hello filter, hello way we did here, will filter down all records in hello **District**, **Store**, and **Sales** tables.</span></span> <span data-ttu-id="96013-138">Sin embargo, debido a la dirección del filtro hello en relaciones de hello entre **ventas** y **tiempo**, **ventas** y **elemento**y **Elemento** y **tiempo** tablas no se filtrarán hacia abajo.</span><span class="sxs-lookup"><span data-stu-id="96013-138">However, because of hello filter direction on hello relationships between **Sales** and **Time**, **Sales** and **Item**, and **Item** and **Time** tables will not be filtered down.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-9.png)

<span data-ttu-id="96013-139">Que puede ser correcto para este requisito, sin embargo, si no queremos administradores toosee elementos para los que no tengan ninguna venta, se puede activar bidireccional filtrado cruzado para hello relación y flujo de hello filtro de seguridad en ambas direcciones.</span><span class="sxs-lookup"><span data-stu-id="96013-139">That may be ok for this requirement, however, if we don’t want managers toosee items for which they don’t have any sales, we could turn on bidirectional cross-filtering for hello relationship and flow hello security filter in both directions.</span></span> <span data-ttu-id="96013-140">Esto puede hacerse mediante la edición de relación de hello entre **ventas** y **elemento**, similar a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="96013-140">This can be done by editing hello relationship between **Sales** and **Item**, like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-edit-relationship-10.png)

<span data-ttu-id="96013-141">Ahora, los filtros también pueden fluir de Hola ventas tabla toohello **elemento** tabla:</span><span class="sxs-lookup"><span data-stu-id="96013-141">Now, filters can also flow from hello Sales table toohello **Item** table:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-diagram-view-11.png)

> [!NOTE]
> <span data-ttu-id="96013-142">Si usa el modo DirectQuery para los datos, necesitará tooenable bidireccional-entre filtrado mediante la selección de estas dos opciones:</span><span class="sxs-lookup"><span data-stu-id="96013-142">If you're using DirectQuery mode for your data, you will need tooenable bidirectional-cross filtering by selecting these two options:</span></span>

1. <span data-ttu-id="96013-143">**Archivo** ->  **Opciones y configuración** -> **Características de vista previa** -> **Enable cross filtering in both directions for DirectQuery** (Habilitar filtrado cruzado en ambas direcciones para DirectQuery).</span><span class="sxs-lookup"><span data-stu-id="96013-143">**File** -> **Options and Settings** -> **Preview Features** -> **Enable cross filtering in both directions for DirectQuery**.</span></span>
2. <span data-ttu-id="96013-144">**Archivo** -> **Opciones y configuración** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode** (Permitir medida sin restricciones en el modo DirectQuery).</span><span class="sxs-lookup"><span data-stu-id="96013-144">**File** -> **Options and Settings** -> **DirectQuery** -> **Allow unrestricted measure in DirectQuery mode**.</span></span>

<span data-ttu-id="96013-145">más información sobre filtrado cruzado bidireccional, descarga hello toolearn [filtrado cruzado bidireccional en SQL Server Analysis Services 2016 y Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) notas del producto.</span><span class="sxs-lookup"><span data-stu-id="96013-145">toolearn more about bidirectional cross-filtering, download hello [Bidirectional cross-filtering in SQL Server Analysis Services 2016 and Power BI Desktop](http://download.microsoft.com/download/2/7/8/2782DF95-3E0D-40CD-BFC8-749A2882E109/Bidirectional cross-filtering in Analysis Services 2016 and Power BI.docx) whitepaper.</span></span>

<span data-ttu-id="96013-146">Esto concluye todo el trabajo de Hola que necesita toobe realiza en Power BI Desktop, pero no hay uno más parte del trabajo que necesita toobe realiza toomake Hola RLS reglas definimos trabajo en Power BI Embedded.</span><span class="sxs-lookup"><span data-stu-id="96013-146">This wraps up all hello work that needs toobe done in Power BI Desktop, but there’s one more piece of work that needs toobe done toomake hello RLS rules we defined work in Power BI Embedded.</span></span> <span data-ttu-id="96013-147">Los usuarios se autentican y autorizan mediante la aplicación y los tokens de aplicación son usado toogrant ese usuario acceso tooa Power BI Embedded informe específico.</span><span class="sxs-lookup"><span data-stu-id="96013-147">Users are authenticated and authorized by your application and App tokens are used toogrant that user access tooa specific Power BI Embedded report.</span></span> <span data-ttu-id="96013-148">Power BI Embedded no tiene información específica en quién es el usuario.</span><span class="sxs-lookup"><span data-stu-id="96013-148">Power BI Embedded doesn’t have any specific information on who your user is.</span></span> <span data-ttu-id="96013-149">Para toowork RLS, necesitará toopass algún contexto adicional como parte de su token de aplicación:</span><span class="sxs-lookup"><span data-stu-id="96013-149">For RLS toowork, you’ll need toopass some additional context as part of your app token:</span></span>

* <span data-ttu-id="96013-150">**nombre de usuario** (opcional): usar con RLS es una cadena que se puede usar toohelp identificar usuario Hola al aplicar reglas RLS.</span><span class="sxs-lookup"><span data-stu-id="96013-150">**username** (optional) – Used with RLS this is a string that can be used toohelp identify hello user when applying RLS rules.</span></span> <span data-ttu-id="96013-151">Consulte el uso de la seguridad de nivel de fila con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="96013-151">See Using Row Level Security with Power BI Embedded</span></span>
* <span data-ttu-id="96013-152">**roles** : una cadena que contiene Hola roles tooselect al aplicar las reglas de seguridad de nivel de fila.</span><span class="sxs-lookup"><span data-stu-id="96013-152">**roles** – A string containing hello roles tooselect when applying Row Level Security rules.</span></span> <span data-ttu-id="96013-153">Si se pasa más de un rol, se deben pasar como una matriz de cadenas.</span><span class="sxs-lookup"><span data-stu-id="96013-153">If passing more than one role, they should be passed as a string array.</span></span>

<span data-ttu-id="96013-154">Crear el token de hello mediante hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) método.</span><span class="sxs-lookup"><span data-stu-id="96013-154">You create hello token by using hello [CreateReportEmbedToken](https://docs.microsoft.com/dotnet/api/microsoft.powerbi.security.powerbitoken?redirectedfrom=MSDN#Microsoft_PowerBI_Security_PowerBIToken_CreateReportEmbedToken_System_String_System_String_System_String_System_DateTime_System_String_System_Collections_Generic_IEnumerable_System_String__) method.</span></span> <span data-ttu-id="96013-155">Si la propiedad de nombre de usuario de hello está presente, también debe pasar al menos un valor en roles.</span><span class="sxs-lookup"><span data-stu-id="96013-155">If hello username property is present, you must also pass at least one value in roles.</span></span>

<span data-ttu-id="96013-156">Por ejemplo, puede cambiar hello EmbedSample.</span><span class="sxs-lookup"><span data-stu-id="96013-156">For example, you could change hello EmbedSample.</span></span> <span data-ttu-id="96013-157">La línea 55 de DashboardController se puede actualizar desde</span><span class="sxs-lookup"><span data-stu-id="96013-157">DashboardController line 55 could be updated from</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id);

<span data-ttu-id="96013-158">to</span><span class="sxs-lookup"><span data-stu-id="96013-158">to</span></span>

    var embedToken = PowerBIToken.CreateReportEmbedToken(this.workspaceCollection, this.workspaceId, report.Id, "Andrew Ma", ["Manager"]);'

<span data-ttu-id="96013-159">token de la aplicación completa de Hello tendrá un aspecto similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="96013-159">hello full app token will look something like this:</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-app-token-string-12.png)

<span data-ttu-id="96013-160">Ahora, con todas las piezas de hello juntas, cuando un usuario inicia sesión en nuestra aplicación tooview este informe, solo estarán toosee capaz de datos de Hola que pueden toosee, tal como se define por la seguridad de nivel de fila.</span><span class="sxs-lookup"><span data-stu-id="96013-160">Now, with all hello pieces together, when someone logs into our application tooview this report, they’ll only be able toosee hello data that they are allowed toosee, as defined by our row-level security.</span></span>

![](media/power-bi-embedded-rls/pbi-embedded-rls-dashboard-13.png)

## <a name="see-also"></a><span data-ttu-id="96013-161">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="96013-161">See also</span></span>

[<span data-ttu-id="96013-162">Seguridad de nivel de fila</span><span class="sxs-lookup"><span data-stu-id="96013-162">Row-level security (RLS) with Power</span></span>](https://powerbi.microsoft.com/en-us/documentation/powerbi-admin-rls/)  
[<span data-ttu-id="96013-163">Autenticación y autorización con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="96013-163">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="96013-164">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="96013-164">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
<span data-ttu-id="96013-165">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) (Ejemplo de inserción de JavaScript)</span><span class="sxs-lookup"><span data-stu-id="96013-165">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/)</span></span>  
<span data-ttu-id="96013-166">¿Tiene más preguntas?</span><span class="sxs-lookup"><span data-stu-id="96013-166">More questions?</span></span> [<span data-ttu-id="96013-167">Intente Hola Comunidad de Power BI</span><span class="sxs-lookup"><span data-stu-id="96013-167">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

