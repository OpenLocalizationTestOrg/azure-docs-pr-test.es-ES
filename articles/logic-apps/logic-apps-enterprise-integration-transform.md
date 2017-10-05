---
title: "Conversión de datos XML con transformaciones: Azure Logic Apps | Microsoft Docs"
description: "Crear transformaciones o mapas para convertir datos XML de un formato a otro en las aplicaciones lógicas mediante el SDK de Enterprise Integration"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: add01429-21bc-4bab-8b23-bc76ba7d0bde
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: fb6027769377b3527b11f7831dab3bb8d7061c84
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="enterprise-integration-with-xml-transforms"></a><span data-ttu-id="9abd4-103">Integración de empresas con transformaciones XML</span><span class="sxs-lookup"><span data-stu-id="9abd4-103">Enterprise integration with XML transforms</span></span>
## <a name="overview"></a><span data-ttu-id="9abd4-104">Información general</span><span class="sxs-lookup"><span data-stu-id="9abd4-104">Overview</span></span>
<span data-ttu-id="9abd4-105">El conector de transformación de integración de empresas convierte los datos de un formato a otro.</span><span class="sxs-lookup"><span data-stu-id="9abd4-105">The Enterprise integration Transform connector converts data from one format to another format.</span></span> <span data-ttu-id="9abd4-106">Por ejemplo, puede darse el caso de que tenga un mensaje entrante en el que la fecha actual tenga el formato añoMesDía.</span><span class="sxs-lookup"><span data-stu-id="9abd4-106">For example, you may have an incoming message that contains the current date in the YearMonthDay format.</span></span> <span data-ttu-id="9abd4-107">Puede utilizar una transformación para cambiar el formato de la fecha a mesDíaAño.</span><span class="sxs-lookup"><span data-stu-id="9abd4-107">You can use a transform to reformat the date to be in the MonthDayYear format.</span></span>

## <a name="what-does-a-transform-do"></a><span data-ttu-id="9abd4-108">¿Para qué sirve una transformación?</span><span class="sxs-lookup"><span data-stu-id="9abd4-108">What does a transform do?</span></span>
<span data-ttu-id="9abd4-109">Una Transformación, que se conoce también como asignación, está formada por un esquema XML de origen (la entrada) y un esquema XML de destino (la salida).</span><span class="sxs-lookup"><span data-stu-id="9abd4-109">A Transform, which is also known as a map, consists of a Source XML schema (the input) and a Target XML schema (the output).</span></span> <span data-ttu-id="9abd4-110">Puede utilizar las diferentes funciones integradas para administrar o controlar los datos, incluidos aspectos como las manipulaciones de cadenas, las asignaciones condicionales, las expresiones aritméticas, los formateadores de tiempo y fecha e, incluso, las construcciones en bucle.</span><span class="sxs-lookup"><span data-stu-id="9abd4-110">You can use different built-in functions to help manipulate or control the data, including string manipulations, conditional assignments, arithmetic expressions, date time formatters, and even looping constructs.</span></span>

## <a name="how-to-create-a-transform"></a><span data-ttu-id="9abd4-111">¿Cómo se crea una transformación?</span><span class="sxs-lookup"><span data-stu-id="9abd4-111">How to create a transform?</span></span>
<span data-ttu-id="9abd4-112">Puede crear una asignación o una transformación mediante el [SDK de integración de empresas](https://aka.ms/vsmapsandschemas)de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9abd4-112">You can create a transform/map by using the Visual Studio [Enterprise Integration SDK](https://aka.ms/vsmapsandschemas).</span></span> <span data-ttu-id="9abd4-113">Cuando haya terminado de crear y probar la transformación, cargue la transformación en la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="9abd4-113">When you are finished creating and testing the transform, you upload the transform into your integration account.</span></span> 

## <a name="how-to-use-a-transform"></a><span data-ttu-id="9abd4-114">Procedimiento para utilizar una transformación</span><span class="sxs-lookup"><span data-stu-id="9abd4-114">How to use a transform</span></span>
<span data-ttu-id="9abd4-115">Cuando cargue la transformación o la asignación en la cuenta de integración, podrá emplearla para crear una aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="9abd4-115">After you upload the transform/map into your integration account, you can use it to create a Logic app.</span></span> <span data-ttu-id="9abd4-116">Esta ejecuta las transformaciones siempre que se desencadena la aplicación lógica (y que haya contenido de entrada que deba transformarse).</span><span class="sxs-lookup"><span data-stu-id="9abd4-116">The Logic app runs your transformations whenever the Logic app is triggered (and there is input content that needs to be transformed).</span></span>

<span data-ttu-id="9abd4-117">**Estos son los pasos para utilizar una transformación**:</span><span class="sxs-lookup"><span data-stu-id="9abd4-117">**Here are the steps to use a transform**:</span></span>

### <a name="prerequisites"></a><span data-ttu-id="9abd4-118">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="9abd4-118">Prerequisites</span></span>

* <span data-ttu-id="9abd4-119">Crear una cuenta de integración y agregarle una asignación.</span><span class="sxs-lookup"><span data-stu-id="9abd4-119">Create an integration account and add a map to it</span></span>  

<span data-ttu-id="9abd4-120">Ahora que ha tenido en cuenta los requisitos previos, tendrá que crear la Aplicación lógica:</span><span class="sxs-lookup"><span data-stu-id="9abd4-120">Now that you've taken care of the prerequisites, it's time to create your Logic app:</span></span>  

1. <span data-ttu-id="9abd4-121">Cree una aplicación lógica y [vincúlela a la cuenta de integración](../logic-apps/logic-apps-enterprise-integration-accounts.md "Aprenda a vincular una cuenta de integración a una aplicación lógica") que contenga la asignación.</span><span class="sxs-lookup"><span data-stu-id="9abd4-121">Create a Logic app and [link it to your integration account](../logic-apps/logic-apps-enterprise-integration-accounts.md "Learn to link an integration account to a Logic app") that contains the map.</span></span>
2. <span data-ttu-id="9abd4-122">Agregue un desencadenador de tipo **Solicitud** a su aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="9abd4-122">Add a **Request** trigger to your Logic app</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-1.png)    
3. <span data-ttu-id="9abd4-123">Agregue la acción **Transform XML** (Transformar XML), pero seleccione antes **Agregar una acción** </span><span class="sxs-lookup"><span data-stu-id="9abd4-123">Add the **Transform XML** action by first selecting **Add an action** </span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-2.png)   
4. <span data-ttu-id="9abd4-124">Escriba la palabra *transform* en el cuadro de búsqueda para filtrar todas las acciones por la que desee usar.</span><span class="sxs-lookup"><span data-stu-id="9abd4-124">Enter the word *transform* in the search box to filter all the actions to the one that you want to use</span></span>  
   ![](./media/logic-apps-enterprise-integration-transforms/transform-3.png)  
5. <span data-ttu-id="9abd4-125">Seleccione la acción **Transform XML** (Transformar XML)</span><span class="sxs-lookup"><span data-stu-id="9abd4-125">Select the **Transform XML** action</span></span>   
6. <span data-ttu-id="9abd4-126">Agregue el **CONTENIDO** XML que vaya a transformar.</span><span class="sxs-lookup"><span data-stu-id="9abd4-126">Add the XML **CONTENT** that you transform.</span></span> <span data-ttu-id="9abd4-127">Puede usar cualquier dato XML que reciba en la solicitud HTTP como valor de **CONTENIDO**.</span><span class="sxs-lookup"><span data-stu-id="9abd4-127">You can use any XML data you receive in the HTTP request as the **CONTENT**.</span></span> <span data-ttu-id="9abd4-128">En este ejemplo, seleccione el cuerpo de la solicitud HTTP que desencadenó la Aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="9abd4-128">In this example, select the body of the HTTP request that triggered the Logic app.</span></span>
7. <span data-ttu-id="9abd4-129">Seleccione el nombre de la **ASIGNACIÓN** que quiera usar para realizar la transformación.</span><span class="sxs-lookup"><span data-stu-id="9abd4-129">Select the name of the **MAP** that you want to use to perform the transformation.</span></span> <span data-ttu-id="9abd4-130">La asignación ya debe estar en la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="9abd4-130">The map must already be in your integration account.</span></span> <span data-ttu-id="9abd4-131">En el paso anterior, ya concedió a la Aplicación lógica acceso a la cuenta de integración que contiene la asignación.</span><span class="sxs-lookup"><span data-stu-id="9abd4-131">In an earlier step, you already gave your Logic app access to your integration account that contains your map.</span></span>      
   ![](./media/logic-apps-enterprise-integration-transforms/transform-4.png) 
8. <span data-ttu-id="9abd4-132">Guarde el trabajo</span><span class="sxs-lookup"><span data-stu-id="9abd4-132">Save your work</span></span>  
    ![](./media/logic-apps-enterprise-integration-transforms/transform-5.png) 

<span data-ttu-id="9abd4-133">En este momento, ya ha terminado de configurar su asignación.</span><span class="sxs-lookup"><span data-stu-id="9abd4-133">At this point, you are finished setting up your map.</span></span> <span data-ttu-id="9abd4-134">En una aplicación real, puede almacenar los datos transformados en una aplicación LOB como SalesForce.</span><span class="sxs-lookup"><span data-stu-id="9abd4-134">In a real world application, you may want to store the transformed data in an LOB application such as SalesForce.</span></span> <span data-ttu-id="9abd4-135">Puede agregar fácilmente una acción para enviar el resultado de la transformación a Salesforce.</span><span class="sxs-lookup"><span data-stu-id="9abd4-135">You can easily as an action to send the output of the transform to Salesforce.</span></span> 

<span data-ttu-id="9abd4-136">Ahora puede probar la transformación realizando una solicitud al punto de conexión HTTP.</span><span class="sxs-lookup"><span data-stu-id="9abd4-136">You can now test your transform by making a request to the HTTP endpoint.</span></span>  

## <a name="features-and-use-cases"></a><span data-ttu-id="9abd4-137">Características y casos de uso</span><span class="sxs-lookup"><span data-stu-id="9abd4-137">Features and use cases</span></span>
* <span data-ttu-id="9abd4-138">La transformación creada en una asignación puede ser simple, como copiar un nombre y una dirección de un documento a otro.</span><span class="sxs-lookup"><span data-stu-id="9abd4-138">The transformation created in a map can be simple, such as copying a name and address from one document to another.</span></span> <span data-ttu-id="9abd4-139">O bien puede crear transformaciones más complejas mediante las operaciones de asignación integradas.</span><span class="sxs-lookup"><span data-stu-id="9abd4-139">Or, you can create more complex transformations using the out-of-the-box map operations.</span></span>  
* <span data-ttu-id="9abd4-140">Hay varias operaciones de asignación o funciones a las que se puede acceder fácilmente, por ejemplo, cadenas, funciones de fecha hora, etc.</span><span class="sxs-lookup"><span data-stu-id="9abd4-140">Multiple map operations or functions are readily available, including strings, date time functions, and so on.</span></span>  
* <span data-ttu-id="9abd4-141">Puede realizar una copia de datos directa entre los esquemas.</span><span class="sxs-lookup"><span data-stu-id="9abd4-141">You can do a direct data copy between the schemas.</span></span> <span data-ttu-id="9abd4-142">En el Asignador que incluye el SDK, es tan sencillo como dibujar una línea que conecte los elementos del esquema de origen con sus equivalentes en el de destino.</span><span class="sxs-lookup"><span data-stu-id="9abd4-142">In the Mapper included in the SDK, this is as simple as drawing a line that connects the elements in the source schema with their counterparts in the destination schema.</span></span>  
* <span data-ttu-id="9abd4-143">Al crear una asignación, verá una representación gráfica de esta, que muestra todos los vínculos y relaciones que cree.</span><span class="sxs-lookup"><span data-stu-id="9abd4-143">When creating a map, you view a graphical representation of the map, which shows all the relationships and links you create.</span></span>
* <span data-ttu-id="9abd4-144">Utilice la característica Comprobar asignación para agregar un mensaje XML de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="9abd4-144">Use the Test Map feature to add a sample XML message.</span></span> <span data-ttu-id="9abd4-145">Con un solo clic, puede probar la asignación creada y ver el resultado generado.</span><span class="sxs-lookup"><span data-stu-id="9abd4-145">With a simple click, you can test the map you created, and see the generated output.</span></span>  
* <span data-ttu-id="9abd4-146">Cargue asignaciones que ya existan.</span><span class="sxs-lookup"><span data-stu-id="9abd4-146">Upload existing maps</span></span>  
* <span data-ttu-id="9abd4-147">Es compatible con el formato XML.</span><span class="sxs-lookup"><span data-stu-id="9abd4-147">Includes support for the XML format.</span></span>

## <a name="learn-more"></a><span data-ttu-id="9abd4-148">Más información</span><span class="sxs-lookup"><span data-stu-id="9abd4-148">Learn more</span></span>
* [<span data-ttu-id="9abd4-149">Más información sobre Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="9abd4-149">Learn more about the Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md "Información sobre Enterprise Integration Pack")  
* [<span data-ttu-id="9abd4-150">Más información sobre las asignaciones</span><span class="sxs-lookup"><span data-stu-id="9abd4-150">Learn more about maps</span></span>](../logic-apps/logic-apps-enterprise-integration-maps.md "Información sobre las asignaciones de Enterprise Integration")  

