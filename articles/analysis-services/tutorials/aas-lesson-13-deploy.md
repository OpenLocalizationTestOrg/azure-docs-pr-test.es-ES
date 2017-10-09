---
<span data-ttu-id="57b80-101">título: aaa "lección tutorial de Analysis Services de Azure 13: implementar | Descripción de Microsoft Docs": describe cómo del proyecto tutorial de hello toodeploy tooAzure Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="57b80-101">title: aaa"Azure Analysis Services tutorial lesson 13: Deploy | Microsoft Docs" description:  Describes how toodeploy hello tutorial project tooAzure Analysis Services.</span></span>
<span data-ttu-id="57b80-102">servicios: documentationcenter de analysis services: '' autor: minewiskan manager: erikre editor: '' etiquetas: ''</span><span class="sxs-lookup"><span data-stu-id="57b80-102">services: analysis-services documentationcenter: '' author: minewiskan manager: erikre editor: '' tags: ''</span></span>

<span data-ttu-id="57b80-103">MS.AssetId: ms.service: ms.devlang de analysis services: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 17/07/2017 ms.author: owend</span><span class="sxs-lookup"><span data-stu-id="57b80-103">ms.assetid: ms.service: analysis-services ms.devlang: NA ms.topic: get-started-article ms.tgt_pltfrm: NA ms.workload: na ms.date: 07/17/2017 ms.author: owend</span></span>
---
# <a name="lesson-13-deploy"></a><span data-ttu-id="57b80-104">Lección 13: Implementación</span><span class="sxs-lookup"><span data-stu-id="57b80-104">Lesson 13: Deploy</span></span>

[!INCLUDE[analysis-services-appliesto-aas-sql2017-later](../../../includes/analysis-services-appliesto-aas-sql2017-later.md)]

<span data-ttu-id="57b80-105">En esta lección, configurará propiedades de implementación; especificar un tooand de toodeploy de servidor de Analysis Services de Azure un nombre para el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="57b80-105">In this lesson, you configure deployment properties; specifying an Azure Analysis Services server toodeploy tooand a name for hello model.</span></span> <span data-ttu-id="57b80-106">A continuación, implemente instancia toothat de hello modelo.</span><span class="sxs-lookup"><span data-stu-id="57b80-106">You then deploy hello model toothat instance.</span></span> <span data-ttu-id="57b80-107">Después de implementa el modelo, los usuarios pueden conectarse tooit mediante el uso de una aplicación de cliente de informes.</span><span class="sxs-lookup"><span data-stu-id="57b80-107">After your model is deployed, users can connect tooit by using a reporting client application.</span></span> <span data-ttu-id="57b80-108">más información, consulte toolearn [implementar tooAzure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span><span class="sxs-lookup"><span data-stu-id="57b80-108">toolearn more, see [Deploy tooAzure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).</span></span>  
  
<span data-ttu-id="57b80-109">Estimado toocomplete de tiempo en esta lección: **5 minutos**</span><span class="sxs-lookup"><span data-stu-id="57b80-109">Estimated time toocomplete this lesson: **5 minutes**</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="57b80-110">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="57b80-110">Prerequisites</span></span>  
<span data-ttu-id="57b80-111">Este tema forma parte de un tutorial de modelado tabular, que se debe completar en orden.</span><span class="sxs-lookup"><span data-stu-id="57b80-111">This topic is part of a tabular modeling tutorial, which should be completed in order.</span></span> <span data-ttu-id="57b80-112">Antes de realizar tareas de hello en esta lección, debe haber completado la lección anterior hello: [lección 12: analizar en Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span><span class="sxs-lookup"><span data-stu-id="57b80-112">Before performing hello tasks in this lesson, you should have completed hello previous lesson: [Lesson 12: Analyze in Excel](../tutorials/aas-lesson-12-analyze-in-excel.md).</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="57b80-113">Debe tener [permisos de administrador](../analysis-services-server-admins.md) en hello remoto Analysis Services server toodeploy en orden tooit.</span><span class="sxs-lookup"><span data-stu-id="57b80-113">You must have [Administrator permissions](../analysis-services-server-admins.md) on hello remote Analysis Services server in-order toodeploy tooit.</span></span>  

> [!IMPORTANT]  
> <span data-ttu-id="57b80-114">Si instaló la base de datos de ejemplo de Hola AdventureWorksDW2014 en un servidor local de SQL, y va a implementar el servidor de Analysis Services de Azure de modelo tooan, un [puerta de enlace de datos local](../analysis-services-gateway.md) es necesario.</span><span class="sxs-lookup"><span data-stu-id="57b80-114">If you installed hello AdventureWorksDW2014 sample database on an on-premises SQL Server, and you're deploying your model tooan Azure Analysis Services server, an [On-premises data gateway](../analysis-services-gateway.md) is required.</span></span>
  
## <a name="deploy-hello-model"></a><span data-ttu-id="57b80-115">Implementar el modelo de Hola</span><span class="sxs-lookup"><span data-stu-id="57b80-115">Deploy hello model</span></span>  
  
#### <a name="tooconfigure-deployment-properties"></a><span data-ttu-id="57b80-116">propiedades de implementación de tooconfigure</span><span class="sxs-lookup"><span data-stu-id="57b80-116">tooconfigure deployment properties</span></span>  

  
1.  <span data-ttu-id="57b80-117">En **el Explorador de soluciones**, contextual hello **AW Internet Sales** del proyecto y, a continuación, haga clic en **propiedades**.</span><span class="sxs-lookup"><span data-stu-id="57b80-117">In **Solution Explorer**, right-click hello **AW Internet Sales** project, and then click **Properties**.</span></span>  
  
2.  <span data-ttu-id="57b80-118">Hola **páginas de propiedades de ventas de Internet de AW** cuadro de diálogo **el servidor de implementación**, Hola **Server** propiedad, escriba servidor completo de Hola.</span><span class="sxs-lookup"><span data-stu-id="57b80-118">In hello **AW Internet Sales Property Pages** dialog box, under **Deployment Server**, in hello **Server** property, enter hello full server.</span></span>  

    ![aas-lesson13-deploy-property](../tutorials/media/aas-lesson13-deploy-property.png)
  
3.  <span data-ttu-id="57b80-120">Hola **base de datos** propiedad, escriba **Adventure Works Internet Sales**.</span><span class="sxs-lookup"><span data-stu-id="57b80-120">In hello **Database** property, type **Adventure Works Internet Sales**.</span></span>  
  
4.  <span data-ttu-id="57b80-121">Hola **nombre del modelo** propiedad, escriba **Adventure Works Internet Sales Model**.</span><span class="sxs-lookup"><span data-stu-id="57b80-121">In hello **Model Name** property, type **Adventure Works Internet Sales Model**.</span></span>  
  
5.  <span data-ttu-id="57b80-122">Compruebe sus selecciones y, a continuación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="57b80-122">Verify your selections and then click **OK**.</span></span>  
  
#### <a name="toodeploy-hello-adventure-works-internet-sales"></a><span data-ttu-id="57b80-123">Hola toodeploy Adventure Works Internet Sales</span><span class="sxs-lookup"><span data-stu-id="57b80-123">toodeploy hello Adventure Works Internet Sales</span></span>
  
1.  <span data-ttu-id="57b80-124">En **el Explorador de soluciones**, contextual hello **AW Internet Sales** proyecto > **generar**.</span><span class="sxs-lookup"><span data-stu-id="57b80-124">In **Solution Explorer**, right-click hello **AW Internet Sales** project > **Build**.</span></span>  

2.  <span data-ttu-id="57b80-125">Menú contextual hello **AW Internet Sales** proyecto > **implementar**.</span><span class="sxs-lookup"><span data-stu-id="57b80-125">Right-click hello **AW Internet Sales** project > **Deploy**.</span></span>

    <span data-ttu-id="57b80-126">Al implementar tooAzure Analysis Services, puede ser solicitada tooenter su cuenta.</span><span class="sxs-lookup"><span data-stu-id="57b80-126">When deploying tooAzure Analysis Services, you may be prompted tooenter your account.</span></span> <span data-ttu-id="57b80-127">Escriba su cuenta profesional y la contraseña, por ejemplo nancy@adventureworks.com. Esta cuenta debe ser de administradores en el servidor de Hola.</span><span class="sxs-lookup"><span data-stu-id="57b80-127">Enter your organizational account and password, for example nancy@adventureworks.com. This account must be in Admins on hello server.</span></span>
  
    <span data-ttu-id="57b80-128">cuadro de diálogo implementar Hola aparece y muestra el estado de implementación de Hola de metadatos de Hola y cada tabla incluida en el modelo de Hola.</span><span class="sxs-lookup"><span data-stu-id="57b80-128">hello Deploy dialog box appears and displays hello deployment status of hello metadata and each table included in hello model.</span></span>  
    
    ![aas-lesson13-deploy-status](../tutorials/media/aas-lesson13-deploy-status.png)
  
3. <span data-ttu-id="57b80-130">Cuando la implementación finalice correctamente, siga adelante y haga clic en **Cerrar**.</span><span class="sxs-lookup"><span data-stu-id="57b80-130">When deployment successfully completes, go ahead and click **Close**.</span></span>  
  
## <a name="conclusion"></a><span data-ttu-id="57b80-131">Conclusión</span><span class="sxs-lookup"><span data-stu-id="57b80-131">Conclusion</span></span>  
<span data-ttu-id="57b80-132">¡Enhorabuena!</span><span class="sxs-lookup"><span data-stu-id="57b80-132">Congratulations!</span></span> <span data-ttu-id="57b80-133">Ha terminado de crear e implementar el primer modelo tabular de Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="57b80-133">You're finished authoring and deploying your first Analysis Services Tabular model.</span></span> <span data-ttu-id="57b80-134">Este tutorial ha ayudado a ayudará a completar las tareas más comunes de hello en la creación de un modelo tabular.</span><span class="sxs-lookup"><span data-stu-id="57b80-134">This tutorial has helped guide you through completing hello most common tasks in creating a tabular model.</span></span> <span data-ttu-id="57b80-135">Ahora que se implementa el modelo de ventas por Internet de Adventure Works, puede utilizar el modelo de SQL Server Management Studio toomanage Hola; crear secuencias de comandos de proceso y un plan de copia de seguridad.</span><span class="sxs-lookup"><span data-stu-id="57b80-135">Now that your Adventure Works Internet Sales model is deployed, you can use SQL Server Management Studio toomanage hello model; create process scripts and a backup plan.</span></span> <span data-ttu-id="57b80-136">Los usuarios pueden conectarse ahora también modelo toohello mediante una aplicación de cliente de informes como Microsoft Excel o Power BI.</span><span class="sxs-lookup"><span data-stu-id="57b80-136">Users can also now connect toohello model using a reporting client application such as Microsoft Excel or Power BI.</span></span>  

![aas-lesson13-ssms](../tutorials/media/aas-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a><span data-ttu-id="57b80-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="57b80-138">What's next?</span></span>
<span data-ttu-id="57b80-139">[Conexión con Power BI Desktop](../analysis-services-connect-pbi.md) </span><span class="sxs-lookup"><span data-stu-id="57b80-139">[Connect with Power BI Desktop](../analysis-services-connect-pbi.md) </span></span>  
<span data-ttu-id="57b80-140">[Lección complementaria: Seguridad dinámica](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span><span class="sxs-lookup"><span data-stu-id="57b80-140">[Supplemental Lesson - Dynamic security](../tutorials/aas-supplemental-lesson-dynamic-security.md) </span></span>  
<span data-ttu-id="57b80-141">[Lección complementaria: Filas de detalles](../tutorials/aas-supplemental-lesson-detail-rows.md) </span><span class="sxs-lookup"><span data-stu-id="57b80-141">[Supplemental Lesson - Detail rows](../tutorials/aas-supplemental-lesson-detail-rows.md) </span></span>  
[<span data-ttu-id="57b80-142">Lección complementaria: Jerarquías desiguales</span><span class="sxs-lookup"><span data-stu-id="57b80-142">Supplemental Lesson - Ragged hierarchies</span></span>](../tutorials/aas-supplemental-lesson-ragged-hierarchies.md)   
