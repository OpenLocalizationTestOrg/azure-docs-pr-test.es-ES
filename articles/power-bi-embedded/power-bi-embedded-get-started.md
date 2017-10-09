---
title: aaaGet a trabajar con Microsoft Power BI Embedded
description: "Power BI Embedded, agregar informes interactivos de Power BI a la aplicación de inteligencia empresarial"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 4787cf44-5d1c-4bc3-b3fd-bf396e5c1176
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 03/11/2017
ms.author: asaxton
ms.openlocfilehash: ebb550cb4eba761dde3c23e4dd0314fc885817e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-microsoft-power-bi-embedded"></a><span data-ttu-id="3f463-103">Introducción a Microsoft Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="3f463-103">Get started with Microsoft Power BI Embedded</span></span>

<span data-ttu-id="3f463-104">**Power BI Embedded** es un servicio de Azure ese tooadd de los desarrolladores de aplicaciones permite informes interactivos Power BI en sus propias aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3f463-104">**Power BI Embedded** is an Azure service that enables application developers tooadd interactive Power BI reports into their own applications.</span></span> <span data-ttu-id="3f463-105">**Power BI Embedded** funciona con aplicaciones existentes sin necesidad de cambiar el diseño o cambiar los usuarios de manera Hola iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="3f463-105">**Power BI Embedded** works with existing applications without needing redesign or changing hello way users sign in.</span></span>

<span data-ttu-id="3f463-106">Recursos para **Microsoft Power BI Embedded** se aprovisionan mediante hello [API de Azure ARM](https://msdn.microsoft.com/library/mt712306.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f463-106">Resources for **Microsoft Power BI Embedded** are provisioned through hello [Azure ARM APIs](https://msdn.microsoft.com/library/mt712306.aspx).</span></span> <span data-ttu-id="3f463-107">En este caso, es el recurso Hola se aprovisiona un **colección de área de trabajo de Power BI**.</span><span class="sxs-lookup"><span data-stu-id="3f463-107">In this case, hello resource you provision is a **Power BI Workspace Collection**.</span></span>

![](media/power-bi-embedded-get-started/introduction.png)

## <a name="create-a-workspace-collection"></a><span data-ttu-id="3f463-108">Creación de una colección de áreas de trabajo</span><span class="sxs-lookup"><span data-stu-id="3f463-108">Create a workspace collection</span></span>

<span data-ttu-id="3f463-109">A **colección de área de trabajo** es el recurso de Azure de nivel superior de Hola y un contenedor para el contenido de Hola que se incrustarán en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f463-109">A **Workspace Collection** is hello top-level Azure resource and a container for hello content that will be embedded in your application.</span></span> <span data-ttu-id="3f463-110">Las **colecciones de áreas de trabajo** se pueden crear de dos maneras:</span><span class="sxs-lookup"><span data-stu-id="3f463-110">A **Workspace Collection** can be created in two ways::</span></span>

* <span data-ttu-id="3f463-111">Manualmente mediante Hola Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3f463-111">Manually using hello Azure Portal</span></span>
* <span data-ttu-id="3f463-112">Mediante programación con hello las API Manager(ARM) de recursos de Azure</span><span class="sxs-lookup"><span data-stu-id="3f463-112">Programmatically using hello Azure Resource Manager(ARM) APIs</span></span>

<span data-ttu-id="3f463-113">Analicemos Hola pasos toobuild una **colección de área de trabajo** utilizando Hola Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3f463-113">Let's walk through hello steps toobuild a **Workspace Collection** using hello Azure Portal.</span></span>

1. <span data-ttu-id="3f463-114">Abra el **Portal de Azure**, [http://portal.azure.com](http://portal.azure.com), e inicie sesión.</span><span class="sxs-lookup"><span data-stu-id="3f463-114">Open and sign into **Azure Portal**: [http://portal.azure.com](http://portal.azure.com).</span></span>
2. <span data-ttu-id="3f463-115">Haga clic en **+ nuevo** en el panel superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f463-115">Click **+ New** on hello top panel.</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-1.png)
3. <span data-ttu-id="3f463-116">En **Datos y análisis**, haga clic en **Power BI Embedded**.</span><span class="sxs-lookup"><span data-stu-id="3f463-116">Under **Data + Analytics** click **Power BI Embedded**.</span></span>
4. <span data-ttu-id="3f463-117">En hello **hoja de la colección de área de trabajo**, escriba información de hello necesario.</span><span class="sxs-lookup"><span data-stu-id="3f463-117">On hello **Workspace Collection Blade**, enter hello required information.</span></span> <span data-ttu-id="3f463-118">En **Precios**, consulte los [precios de Power BI Embedded](http://go.microsoft.com/fwlink/?LinkID=760527).</span><span class="sxs-lookup"><span data-stu-id="3f463-118">For **Pricing**, see [Power BI Embedded pricing](http://go.microsoft.com/fwlink/?LinkID=760527).</span></span>
   
   ![](media/power-bi-embedded-get-started/create-workspace-2.png)
5. <span data-ttu-id="3f463-119">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="3f463-119">Click **Create**.</span></span>

<span data-ttu-id="3f463-120">Hola **colección de área de trabajo** tardará tooprovision unos instantes.</span><span class="sxs-lookup"><span data-stu-id="3f463-120">hello **Workspace Collection** will take a few moments tooprovision.</span></span> <span data-ttu-id="3f463-121">Cuando haya completado, se le dirigirá toohello **hoja de la colección de área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="3f463-121">When completed, you'll be taken toohello **Workspace Collection Blade**.</span></span>

   ![](media/power-bi-embedded-get-started/create-workspace-3.png)

<span data-ttu-id="3f463-122">Hola **hoja de creación** contiene información de Hola que necesita toocall Hola API creen áreas de trabajo y que implemente contenido toothem.</span><span class="sxs-lookup"><span data-stu-id="3f463-122">hello **Creation Blade** contains hello information you need toocall hello APIs that create workspaces and deploy content toothem.</span></span>

<a name="view-access-keys"/>

## <a name="view-power-bi-api-access-keys"></a><span data-ttu-id="3f463-123">Visualización de las claves de acceso de API de Power BI</span><span class="sxs-lookup"><span data-stu-id="3f463-123">View Power BI API access keys</span></span>

<span data-ttu-id="3f463-124">Uno de hello más importante fragmentos de información necesaria toocall Hola API de REST de Power BI son hello **teclas de acceso**.</span><span class="sxs-lookup"><span data-stu-id="3f463-124">One of hello most important pieces of information needed toocall hello Power BI REST APIs are hello **Access Keys**.</span></span> <span data-ttu-id="3f463-125">Se trata de hello toogenerate usado **tokens de aplicación** que son utilizado tooauthenticate las solicitudes de API.</span><span class="sxs-lookup"><span data-stu-id="3f463-125">These are used toogenerate hello **app tokens** that are used tooauthenticate your API requests.</span></span> <span data-ttu-id="3f463-126">tooview su **teclas de acceso**, haga clic en **teclas de acceso** en hello **hoja de configuración**.</span><span class="sxs-lookup"><span data-stu-id="3f463-126">tooview your **Access Keys**, click **Access Keys** on hello **Settings Blade**.</span></span> <span data-ttu-id="3f463-127">Para más información sobre los **tokens de aplicación**, consulte [Autenticación y autorización con Power BI Embedded](power-bi-embedded-app-token-flow.md).</span><span class="sxs-lookup"><span data-stu-id="3f463-127">For more about **app tokens**, see [Authenticating and authorizing with Power BI Embedded](power-bi-embedded-app-token-flow.md).</span></span>

   ![](media/power-bi-embedded-get-started/access-keys.png)

<span data-ttu-id="3f463-128">Verá que tiene dos claves.</span><span class="sxs-lookup"><span data-stu-id="3f463-128">You'll'notice that you have two keys.</span></span>

   ![](media/power-bi-embedded-get-started/access-keys-2.png)

<span data-ttu-id="3f463-129">Copie estas claves y almacénelas de forma segura en la aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f463-129">Copy these keys and store them securely in your application.</span></span> <span data-ttu-id="3f463-130">Es muy importante tratar estas claves como lo haría con una contraseña, ya que le proporcionan acceso tooall Hola contenido en su **colección de área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="3f463-130">It's very important that you treat these keys as you would a password, because they'll provide access tooall hello content in your **Workspace Collection**.</span></span>

<span data-ttu-id="3f463-131">Aunque se muestran dos claves, solo se necesita una cada vez.</span><span class="sxs-lookup"><span data-stu-id="3f463-131">While two keys are listed, only one key is needed at a particular time.</span></span> <span data-ttu-id="3f463-132">segunda clave de Hola se proporciona de manera que puede regenerar periódicamente las claves sin interrumpir el servicio de acceso toohello.</span><span class="sxs-lookup"><span data-stu-id="3f463-132">hello second key is provided so you can periodically regenerate keys without interrupting access toohello service.</span></span>

<span data-ttu-id="3f463-133">Ahora que tiene una instancia de Power BI para la aplicación y las **claves de acceso**, puede importar un informe en la propia aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f463-133">Now that you have an instance of Power BI for your application, and **Access Keys**, you can import a report into your own app.</span></span> <span data-ttu-id="3f463-134">Antes de aprender a cómo tooimport un informe, la siguiente sección de hello describe tooembed creación de conjuntos de datos e informes de Power BI en una aplicación.</span><span class="sxs-lookup"><span data-stu-id="3f463-134">Before you learn how tooimport a report, hello next section describes creating Power BI datasets and reports tooembed into an app.</span></span>

## <a name="working-with-workspaces"></a><span data-ttu-id="3f463-135">Trabajo con áreas de trabajo</span><span class="sxs-lookup"><span data-stu-id="3f463-135">Working with workspaces</span></span>

<span data-ttu-id="3f463-136">Después de haber creado la colección de área de trabajo, deberá toocreate un área de trabajo que hospedará los informes y conjuntos de datos.</span><span class="sxs-lookup"><span data-stu-id="3f463-136">After you have created your workspace collection, you will need toocreate a workspace that will house your reports and datasets.</span></span> <span data-ttu-id="3f463-137">toocreate un área de trabajo, deberá hello toouse [API de REST de área de trabajo de Post](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f463-137">toocreate a workspace, you will need toouse hello [Post Worksapce REST API](https://msdn.microsoft.com/library/azure/mt711503.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-tooembed-into-an-app-using-power-bi-desktop"></a><span data-ttu-id="3f463-138">Crear tooembed de conjuntos de datos e informes de Power BI en una aplicación con Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="3f463-138">Create Power BI datasets and reports tooembed into an app using Power BI Desktop</span></span>

<span data-ttu-id="3f463-139">Ahora que ha creado una instancia de Power BI para su aplicación y tiene **teclas de acceso**, necesitará los conjuntos de datos de toocreate Hola Power BI e informes que desea tooembed.</span><span class="sxs-lookup"><span data-stu-id="3f463-139">Now that you have created an instance of Power BI for your application, and have **Access Keys**, you will need toocreate hello Power BI datasets and reports that you want tooembed.</span></span> <span data-ttu-id="3f463-140">Los conjuntos de datos y los informes se pueden crear con **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="3f463-140">Datasets and reports can be created by using **Power BI Desktop**.</span></span> <span data-ttu-id="3f463-141">Puede descargar [Power BI Desktop gratis](https://go.microsoft.com/fwlink/?LinkId=521662).</span><span class="sxs-lookup"><span data-stu-id="3f463-141">You can download [Power BI Desktop for free](https://go.microsoft.com/fwlink/?LinkId=521662).</span></span> <span data-ttu-id="3f463-142">O bien, tooquickly empezar a trabajar, puede descargar hello [PBIX de ejemplo de análisis de minoristas](http://go.microsoft.com/fwlink/?LinkID=780547).</span><span class="sxs-lookup"><span data-stu-id="3f463-142">Or, tooquickly get started, you can download hello [Retail Analysis Sample PBIX](http://go.microsoft.com/fwlink/?LinkID=780547).</span></span>

> [!NOTE]
> <span data-ttu-id="3f463-143">más información acerca de cómo toolearn toouse **Power BI Desktop**, consulte [Introducción a Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span><span class="sxs-lookup"><span data-stu-id="3f463-143">toolearn more about how toouse **Power BI Desktop**, see [Getting Started with Power BI Desktop](https://powerbi.microsoft.com/guided-learning/powerbi-learning-0-2-get-started-power-bi-desktop).</span></span>

<span data-ttu-id="3f463-144">Con **Power BI Desktop**, conectar tooyour origen de datos mediante la importación de una copia de datos de hello en **Power BI Desktop** o conectar directamente toohello de datos de origen mediante **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="3f463-144">With **Power BI Desktop**, you connect tooyour data source by importing a copy of hello data into **Power BI Desktop** or connecting directly toohello data source using **DirectQuery**.</span></span>

<span data-ttu-id="3f463-145">Estas son Hola diferencias entre el uso de **importación** y **DirectQuery**.</span><span class="sxs-lookup"><span data-stu-id="3f463-145">Here are hello differences between using **Import** and **DirectQuery**.</span></span>

| <span data-ttu-id="3f463-146">Importación</span><span class="sxs-lookup"><span data-stu-id="3f463-146">Import</span></span> | <span data-ttu-id="3f463-147">DirectQuery</span><span class="sxs-lookup"><span data-stu-id="3f463-147">DirectQuery</span></span> |
| --- | --- |
| <span data-ttu-id="3f463-148">Las tablas, las columnas y los *datos* se importan o se copian en **Power BI Desktop**.</span><span class="sxs-lookup"><span data-stu-id="3f463-148">Tables, columns, *and data* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="3f463-149">Cuando se trabaja con visualizaciones, **Power BI Desktop** consulta una copia de datos de Hola.</span><span class="sxs-lookup"><span data-stu-id="3f463-149">As you work with visualizations, **Power BI Desktop** queries a copy of hello data.</span></span> <span data-ttu-id="3f463-150">toosee los cambios de datos subyacente toohello se produjo, debe actualizar o importar un completo actual conjunto de datos nuevo.</span><span class="sxs-lookup"><span data-stu-id="3f463-150">toosee any changes that occurred toohello underlying data, you must refresh, or import, a complete, current dataset again.</span></span> |<span data-ttu-id="3f463-151">En *Power BI Desktop* , solo se importan o copian **tablas y columnas**.</span><span class="sxs-lookup"><span data-stu-id="3f463-151">Only *tables and columns* are imported or copied into **Power BI Desktop**.</span></span> <span data-ttu-id="3f463-152">Cuando se trabaja con visualizaciones, **Power BI Desktop** consultas Hola el origen de datos subyacente, lo que significa que siempre está viendo los datos actuales.</span><span class="sxs-lookup"><span data-stu-id="3f463-152">As you work with visualizations, **Power BI Desktop** queries hello underlying data source, which means you're always viewing current data.</span></span> |

<span data-ttu-id="3f463-153">Para obtener más información sobre el origen de datos de conexión tooa, consulte [Conectar origen de datos de tooa](power-bi-embedded-connect-datasource.md).</span><span class="sxs-lookup"><span data-stu-id="3f463-153">For more about connecting tooa data source, see [Connect tooa data source](power-bi-embedded-connect-datasource.md).</span></span>

<span data-ttu-id="3f463-154">Cuando guarde el trabajo en **Power BI Desktop**, se creará un archivo PBIX.</span><span class="sxs-lookup"><span data-stu-id="3f463-154">After you save your work in **Power BI Desktop**, a PBIX file is created.</span></span> <span data-ttu-id="3f463-155">Este archivo contiene el informe.</span><span class="sxs-lookup"><span data-stu-id="3f463-155">This file contains your report.</span></span> <span data-ttu-id="3f463-156">Además, si importa Hola de datos contiene PBIX Hola conjunto de datos completo, o si utiliza **DirectQuery**, hello PBIX contiene solo un esquema de conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="3f463-156">In addition, if you import data hello PBIX contains hello complete dataset, or if you use **DirectQuery**, hello PBIX contains just a dataset schema.</span></span> <span data-ttu-id="3f463-157">Implementar mediante programación hello PBIX en el área de trabajo con hello [API de importación de Power BI](https://msdn.microsoft.com/library/mt711504.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f463-157">You programmatically deploy hello PBIX into your workspace using hello [Power BI Import API](https://msdn.microsoft.com/library/mt711504.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="3f463-158">**Power BI Embedded** tiene adicionales API toochange Hola servidor y base de datos que el conjunto de datos está señalando tooand conjunto una credencial de cuenta de servicio que Hola conjunto de datos usará la base de datos de tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="3f463-158">**Power BI Embedded** has additional APIs toochange hello server and database that your dataset is pointing tooand set a service account credential that hello dataset will use tooconnect tooyour database.</span></span> <span data-ttu-id="3f463-159">Consulte [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) y [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx) (Revisión de origen de datos de puerta de enlace).</span><span class="sxs-lookup"><span data-stu-id="3f463-159">See [Post SetAllConnections](https://msdn.microsoft.com/library/mt711505.aspx) and [Patch Gateway Datasource](https://msdn.microsoft.com/library/mt711498.aspx).</span></span>

## <a name="create-power-bi-datasets-and-reports-using-apis"></a><span data-ttu-id="3f463-160">Creación de conjuntos de datos e informes de Power BI con las API</span><span class="sxs-lookup"><span data-stu-id="3f463-160">Create Power BI datasets and reports using APIs</span></span>

### <a name="datsets"></a><span data-ttu-id="3f463-161">Conjuntos de datos</span><span class="sxs-lookup"><span data-stu-id="3f463-161">Datsets</span></span>

<span data-ttu-id="3f463-162">Puede crear conjuntos de datos en Power BI Embedded mediante Hola API de REST.</span><span class="sxs-lookup"><span data-stu-id="3f463-162">You can create datasets within Power BI Embedded using hello REST API.</span></span> <span data-ttu-id="3f463-163">Luego, puede insertar datos en el conjunto de datos.</span><span class="sxs-lookup"><span data-stu-id="3f463-163">You can then push data into your dataset.</span></span> <span data-ttu-id="3f463-164">Esto le permite toowork con datos sin necesidad de Hola de Power BI Desktop.</span><span class="sxs-lookup"><span data-stu-id="3f463-164">This allows you toowork with data without hello need of Power BI Desktop.</span></span> <span data-ttu-id="3f463-165">Para más información, consulte [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx) (Publicación de conjuntos de datos).</span><span class="sxs-lookup"><span data-stu-id="3f463-165">For more information, see [Post Datasets](https://msdn.microsoft.com/library/azure/mt778875.aspx).</span></span>

### <a name="reports"></a><span data-ttu-id="3f463-166">Informes</span><span class="sxs-lookup"><span data-stu-id="3f463-166">Reports</span></span>

<span data-ttu-id="3f463-167">Puede crear un informe desde un conjunto de datos directamente en la aplicación con hello API de JavaScript.</span><span class="sxs-lookup"><span data-stu-id="3f463-167">You can create a report from a dataset directly in your application using hello JavaScript API.</span></span> <span data-ttu-id="3f463-168">Para más información, consulte [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Creación de un nuevo informe a partir de un conjunto de datos en Power BI Embedded).</span><span class="sxs-lookup"><span data-stu-id="3f463-168">For more information, see [Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="3f463-169">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="3f463-169">See Also</span></span>

[<span data-ttu-id="3f463-170">Get started with Microsoft Power BI Embedded sample (Introducción a Microsoft Power BI Embedded: ejemplo)</span><span class="sxs-lookup"><span data-stu-id="3f463-170">Get started with sample</span></span>](power-bi-embedded-get-started-sample.md)  
[<span data-ttu-id="3f463-171">Autenticación y autorización con Power BI Embedded</span><span class="sxs-lookup"><span data-stu-id="3f463-171">Authenticating and authorizing in Power BI Embedded</span></span>](power-bi-embedded-app-token-flow.md)  
[<span data-ttu-id="3f463-172">Inserción de un informe</span><span class="sxs-lookup"><span data-stu-id="3f463-172">Embed a report</span></span>](power-bi-embedded-embed-report.md)  
<span data-ttu-id="3f463-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md) (Creación de un nuevo informe a partir de un conjunto de datos en Power BI Embedded) 
[Save reports](power-bi-embedded-save-reports.md) (Guardar informes)</span><span class="sxs-lookup"><span data-stu-id="3f463-173">[Create a new report from a dataset in Power BI Embedded](power-bi-embedded-create-report-from-dataset.md)
[Save reports](power-bi-embedded-save-reports.md)</span></span>  
[<span data-ttu-id="3f463-174">Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="3f463-174">Power BI Desktop</span></span>](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)  
<span data-ttu-id="3f463-175">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/) (Ejemplo de inserción de JavaScript)</span><span class="sxs-lookup"><span data-stu-id="3f463-175">[JavaScript Embed Sample](https://microsoft.github.io/PowerBI-JavaScript/demo/)</span></span>  
<span data-ttu-id="3f463-176">¿Tiene más preguntas?</span><span class="sxs-lookup"><span data-stu-id="3f463-176">More questions?</span></span> [<span data-ttu-id="3f463-177">Intente Hola Comunidad de Power BI</span><span class="sxs-lookup"><span data-stu-id="3f463-177">Try hello Power BI Community</span></span>](http://community.powerbi.com/)

