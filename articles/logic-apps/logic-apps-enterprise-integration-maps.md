---
title: "Transformación de XML con mapas XSLT: Azure Logic Apps | Microsoft Docs"
description: "Incorporación de mapas XSLT para transformar datos XML con Azure Logic Apps y Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 90f5cfc4-46b2-4ef7-8ac4-486bb0e3f289
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 4445a84a6c6425110e7d705019a28b5cc5447046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-maps-for-xml-data-transform"></a><span data-ttu-id="146cc-103">Incorporación de mapas para la transformación de datos XML</span><span class="sxs-lookup"><span data-stu-id="146cc-103">Add maps for XML data transform</span></span>

<span data-ttu-id="146cc-104">Enterprise Integration utiliza mapas para transformar datos XML de un formato a otro.</span><span class="sxs-lookup"><span data-stu-id="146cc-104">Enterprise integration uses maps to transform XML data between formats.</span></span> <span data-ttu-id="146cc-105">Un mapa es un documento XML que define qué datos de un documento deben transformarse en otro formato.</span><span class="sxs-lookup"><span data-stu-id="146cc-105">A map is an XML document that defines the data in a document that should be transformed into another format.</span></span> 

## <a name="why-use-maps"></a><span data-ttu-id="146cc-106">¿Por qué se utilizan las asignaciones?</span><span class="sxs-lookup"><span data-stu-id="146cc-106">Why use maps?</span></span>

<span data-ttu-id="146cc-107">Suponga que recibe periódicamente pedidos o facturas B2B de clientes que usen el formato de fecha AAAMMDD.</span><span class="sxs-lookup"><span data-stu-id="146cc-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses the YYYMMDD format for dates.</span></span> <span data-ttu-id="146cc-108">Sin embargo, en su organización, las fechas se almacenan en el formato MMDDAAA.</span><span class="sxs-lookup"><span data-stu-id="146cc-108">However, in your organization, you store dates in the MMDDYYY format.</span></span> <span data-ttu-id="146cc-109">Puede usar una asignación para *transformar* el formato de fecha AAAMMDD en MMDDAAA antes de almacenar los detalles de los pedidos o las facturas en la base de datos de actividades de clientes.</span><span class="sxs-lookup"><span data-stu-id="146cc-109">You can use a map to *transform* the YYYMMDD date format into the MMDDYYY before storing the order or invoice details in your customer activity database.</span></span>

## <a name="how-do-i-create-a-map"></a><span data-ttu-id="146cc-110">¿Cómo se crea un mapa?</span><span class="sxs-lookup"><span data-stu-id="146cc-110">How do I create a map?</span></span>

<span data-ttu-id="146cc-111">Puede crear proyectos de integración de BizTalk con [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Información sobre Enterprise Integration Pack") para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="146cc-111">You can create BizTalk Integration projects with the [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack") for Visual Studio 2015.</span></span> <span data-ttu-id="146cc-112">Posteriormente, puede crear un archivo de mapa de Integration que le permite mostrar en un mapa los elementos entre dos archivos de esquema XML.</span><span class="sxs-lookup"><span data-stu-id="146cc-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span></span> <span data-ttu-id="146cc-113">Después de compilar este proyecto, obtendrá un documento XSLT.</span><span class="sxs-lookup"><span data-stu-id="146cc-113">After you build this project, you will have an XSLT document.</span></span>

## <a name="how-do-i-add-a-map"></a><span data-ttu-id="146cc-114">¿Cómo se puede agregar un mapa?</span><span class="sxs-lookup"><span data-stu-id="146cc-114">How do I add a map?</span></span>

1. <span data-ttu-id="146cc-115">En Azure Portal, seleccione **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="146cc-115">In the Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="146cc-116">En el cuadro de búsqueda, especifique **integración** y seleccione **Integration Accounts** (Cuentas de integración) en la lista de resultados.</span><span class="sxs-lookup"><span data-stu-id="146cc-116">In the filter search box, enter **integration**, then select **Integration Accounts** from the results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="146cc-117">Seleccione la cuenta integración en la que vaya a agregar el mapa.</span><span class="sxs-lookup"><span data-stu-id="146cc-117">Select the integration account where you want to add the map.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="146cc-118">Seleccione el icono de **Mapas**.</span><span class="sxs-lookup"><span data-stu-id="146cc-118">Select the **Maps** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. <span data-ttu-id="146cc-119">Una vez que se abre la hoja de mapas, elija **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="146cc-119">After the Maps blade opens, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. <span data-ttu-id="146cc-120">Escriba un **nombre** para el mapa.</span><span class="sxs-lookup"><span data-stu-id="146cc-120">Enter a **Name** for your map.</span></span> <span data-ttu-id="146cc-121">Para cargar el archivo de mapa, seleccione el icono de carpeta de la derecha del cuadro de texto **Mapa**.</span><span class="sxs-lookup"><span data-stu-id="146cc-121">To upload the map file, choose the folder icon on the right side of the **Map** text box.</span></span> <span data-ttu-id="146cc-122">Cuando termine el proceso de carga, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="146cc-122">After the upload process completes, choose **OK**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. <span data-ttu-id="146cc-123">Después de que Azure agregue el mapa a la cuenta de integración, obtendrá un mensaje en la pantalla que muestra si se ha agregado el archivo de mapa o no.</span><span class="sxs-lookup"><span data-stu-id="146cc-123">After Azure adds the map to your integration account, you get an onscreen message that shows whether your map file was added or not.</span></span> <span data-ttu-id="146cc-124">Después de obtener este mensaje, elija el icono de **mapas** para que pueda ver el mapa recién agregado.</span><span class="sxs-lookup"><span data-stu-id="146cc-124">After you get this message, choose the **Maps** tile so you can view the newly added map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a><span data-ttu-id="146cc-125">¿Cómo se puede editar un mapa?</span><span class="sxs-lookup"><span data-stu-id="146cc-125">How do I edit a map?</span></span>

<span data-ttu-id="146cc-126">Debe cargar un nuevo archivo de mapa con los cambios que desee.</span><span class="sxs-lookup"><span data-stu-id="146cc-126">You must upload a new map file with the changes that you want.</span></span> <span data-ttu-id="146cc-127">En primer lugar, puede descargar el mapa para editarlo.</span><span class="sxs-lookup"><span data-stu-id="146cc-127">You can first download the map for editing.</span></span>

<span data-ttu-id="146cc-128">Siga estos pasos para cargar un nuevo mapa que reemplace el que ya existe.</span><span class="sxs-lookup"><span data-stu-id="146cc-128">To upload a new map that replaces the existing map, follow these steps.</span></span>

1. <span data-ttu-id="146cc-129">Seleccione el icono de **Mapas**.</span><span class="sxs-lookup"><span data-stu-id="146cc-129">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="146cc-130">Una vez que se abra la hoja de mapas, seleccione el mapa que desea editar.</span><span class="sxs-lookup"><span data-stu-id="146cc-130">After the Maps blade opens, select the map that you want to edit.</span></span>

3. <span data-ttu-id="146cc-131">En la hoja de **mapas**, elija **Actualizar**.</span><span class="sxs-lookup"><span data-stu-id="146cc-131">On the **Maps** blade, choose **Update**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. <span data-ttu-id="146cc-132">En el selector de archivos, seleccione el archivo de mapa que desea cargar y haga clic en **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="146cc-132">In the file picker, select the map file that you want to upload, then select **Open**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-to-delete-a-map"></a><span data-ttu-id="146cc-133">¿Cómo se eliminan asignaciones?</span><span class="sxs-lookup"><span data-stu-id="146cc-133">How to delete a map?</span></span>

1. <span data-ttu-id="146cc-134">Seleccione el icono de **Mapas**.</span><span class="sxs-lookup"><span data-stu-id="146cc-134">Choose the **Maps** tile.</span></span>

2. <span data-ttu-id="146cc-135">Una vez que se abra la hoja de mapas, seleccione el mapa que desea eliminar.</span><span class="sxs-lookup"><span data-stu-id="146cc-135">After the Maps blade opens, select the map you want to delete.</span></span>

3. <span data-ttu-id="146cc-136">Elija **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="146cc-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. <span data-ttu-id="146cc-137">Confirme que desea eliminar el mapa.</span><span class="sxs-lookup"><span data-stu-id="146cc-137">Confirm that you want to delete the map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a><span data-ttu-id="146cc-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="146cc-138">Next Steps</span></span>
* [<span data-ttu-id="146cc-139">Más información sobre Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="146cc-139">Learn more about the Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Información sobre Enterprise Integration Pack")  
* [<span data-ttu-id="146cc-140">Más información sobre los contratos</span><span class="sxs-lookup"><span data-stu-id="146cc-140">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Información sobre los contratos de integración de empresas")  
* [<span data-ttu-id="146cc-141">Más información sobre las transformaciones</span><span class="sxs-lookup"><span data-stu-id="146cc-141">Learn more about transforms</span></span>](logic-apps-enterprise-integration-transform.md "Información sobre las transformaciones de integración empresarial")  

