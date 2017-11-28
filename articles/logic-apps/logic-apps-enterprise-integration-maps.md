---
title: aaaTransform XML con XSLT mapas - Azure Logic Apps | Documentos de Microsoft
description: "Agregar que XSLT asigna los datos XML de tootransform con hello paquete de integración empresarial y las aplicaciones lógicas de Azure"
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
ms.openlocfilehash: 720e6f988b8542136dfcc402c3c463fcfb2f23cf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-maps-for-xml-data-transform"></a><span data-ttu-id="fa80a-103">Incorporación de mapas para la transformación de datos XML</span><span class="sxs-lookup"><span data-stu-id="fa80a-103">Add maps for XML data transform</span></span>

<span data-ttu-id="fa80a-104">Usos de la integración de Enterprise asigna datos XML de tootransform entre los formatos.</span><span class="sxs-lookup"><span data-stu-id="fa80a-104">Enterprise integration uses maps tootransform XML data between formats.</span></span> <span data-ttu-id="fa80a-105">Un mapa es un documento XML que define los datos de hello en un documento que debería transformarse en otro formato.</span><span class="sxs-lookup"><span data-stu-id="fa80a-105">A map is an XML document that defines hello data in a document that should be transformed into another format.</span></span> 

## <a name="why-use-maps"></a><span data-ttu-id="fa80a-106">¿Por qué se utilizan las asignaciones?</span><span class="sxs-lookup"><span data-stu-id="fa80a-106">Why use maps?</span></span>

<span data-ttu-id="fa80a-107">Suponga que recibe con regularidad B2B pedidos o facturas de un cliente que utiliza el formato YYYMMDD de Hola para las fechas.</span><span class="sxs-lookup"><span data-stu-id="fa80a-107">Suppose that you regularly receive B2B orders or invoices from a customer who uses hello YYYMMDD format for dates.</span></span> <span data-ttu-id="fa80a-108">Sin embargo, en su organización, almacenar fechas en formato MMDDYYY Hola.</span><span class="sxs-lookup"><span data-stu-id="fa80a-108">However, in your organization, you store dates in hello MMDDYYY format.</span></span> <span data-ttu-id="fa80a-109">Puede usar una asignación demasiado*transformar* formato de fecha de hello YYYMMDD en hello MMDDYYY antes de almacenar los detalles de pedido o factura de hello en la base de datos de la actividad del cliente.</span><span class="sxs-lookup"><span data-stu-id="fa80a-109">You can use a map too*transform* hello YYYMMDD date format into hello MMDDYYY before storing hello order or invoice details in your customer activity database.</span></span>

## <a name="how-do-i-create-a-map"></a><span data-ttu-id="fa80a-110">¿Cómo se crea un mapa?</span><span class="sxs-lookup"><span data-stu-id="fa80a-110">How do I create a map?</span></span>

<span data-ttu-id="fa80a-111">Puede crear proyectos de integración de BizTalk con hello [paquete de integración empresarial](logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial hello") para Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="fa80a-111">You can create BizTalk Integration projects with hello [Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about hello enterprise integration pack") for Visual Studio 2015.</span></span> <span data-ttu-id="fa80a-112">Posteriormente, puede crear un archivo de mapa de Integration que le permite mostrar en un mapa los elementos entre dos archivos de esquema XML.</span><span class="sxs-lookup"><span data-stu-id="fa80a-112">You can then create an Integration Map file that lets you visually map items between two XML schema files.</span></span> <span data-ttu-id="fa80a-113">Después de compilar este proyecto, obtendrá un documento XSLT.</span><span class="sxs-lookup"><span data-stu-id="fa80a-113">After you build this project, you will have an XSLT document.</span></span>

## <a name="how-do-i-add-a-map"></a><span data-ttu-id="fa80a-114">¿Cómo se puede agregar un mapa?</span><span class="sxs-lookup"><span data-stu-id="fa80a-114">How do I add a map?</span></span>

1. <span data-ttu-id="fa80a-115">Hola portal de Azure, seleccione **examinar**.</span><span class="sxs-lookup"><span data-stu-id="fa80a-115">In hello Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="fa80a-116">En el cuadro de búsqueda del filtro de hello, escriba **integración**, a continuación, seleccione **cuentas de integración** desde la lista de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="fa80a-116">In hello filter search box, enter **integration**, then select **Integration Accounts** from hello results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="fa80a-117">Seleccione la cuenta de integración de Hola donde desea que el mapa de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="fa80a-117">Select hello integration account where you want tooadd hello map.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="fa80a-118">Seleccione hello **mapas** icono.</span><span class="sxs-lookup"><span data-stu-id="fa80a-118">Select hello **Maps** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-1.png)

5. <span data-ttu-id="fa80a-119">Después de abre la hoja de mapas de hello, elija **agregar**.</span><span class="sxs-lookup"><span data-stu-id="fa80a-119">After hello Maps blade opens, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-2.png)  

6. <span data-ttu-id="fa80a-120">Escriba un **nombre** para el mapa.</span><span class="sxs-lookup"><span data-stu-id="fa80a-120">Enter a **Name** for your map.</span></span> <span data-ttu-id="fa80a-121">mapa de hello tooupload de archivos, elija el icono de carpeta de hello en hello derecha de hello **mapa** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="fa80a-121">tooupload hello map file, choose hello folder icon on hello right side of hello **Map** text box.</span></span> <span data-ttu-id="fa80a-122">Una vez completado el proceso de carga de hello, elija **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="fa80a-122">After hello upload process completes, choose **OK**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-3.png)

7. <span data-ttu-id="fa80a-123">Después de Azure agrega la cuenta de integración de hello mapa tooyour, obtendrá un mensaje en la pantalla que muestra si se ha agregado el archivo de asignación o no.</span><span class="sxs-lookup"><span data-stu-id="fa80a-123">After Azure adds hello map tooyour integration account, you get an onscreen message that shows whether your map file was added or not.</span></span> <span data-ttu-id="fa80a-124">Después de obtener este mensaje, elija hello **mapas** mosaico para que pueda ver Hola recién agregado asignación.</span><span class="sxs-lookup"><span data-stu-id="fa80a-124">After you get this message, choose hello **Maps** tile so you can view hello newly added map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/map-4.png)

## <a name="how-do-i-edit-a-map"></a><span data-ttu-id="fa80a-125">¿Cómo se puede editar un mapa?</span><span class="sxs-lookup"><span data-stu-id="fa80a-125">How do I edit a map?</span></span>

<span data-ttu-id="fa80a-126">Debe cargar un nuevo archivo de asignación con cambios de Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="fa80a-126">You must upload a new map file with hello changes that you want.</span></span> <span data-ttu-id="fa80a-127">En primer lugar, puede descargar mapa Hola para su edición.</span><span class="sxs-lookup"><span data-stu-id="fa80a-127">You can first download hello map for editing.</span></span>

<span data-ttu-id="fa80a-128">tooupload un mapa nuevo que reemplaza la asignación existente de hello, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="fa80a-128">tooupload a new map that replaces hello existing map, follow these steps.</span></span>

1. <span data-ttu-id="fa80a-129">Elija hello **mapas** icono.</span><span class="sxs-lookup"><span data-stu-id="fa80a-129">Choose hello **Maps** tile.</span></span>

2. <span data-ttu-id="fa80a-130">Después de abre la hoja de mapas de hello, seleccione asignación de Hola que desea tooedit.</span><span class="sxs-lookup"><span data-stu-id="fa80a-130">After hello Maps blade opens, select hello map that you want tooedit.</span></span>

3. <span data-ttu-id="fa80a-131">En hello **mapas** hoja, elija **actualización**.</span><span class="sxs-lookup"><span data-stu-id="fa80a-131">On hello **Maps** blade, choose **Update**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-1.png)

4. <span data-ttu-id="fa80a-132">En el selector de archivos de hello, seleccione archivo de mapa de Hola que desee tooupload, a continuación, seleccione **abiertos**.</span><span class="sxs-lookup"><span data-stu-id="fa80a-132">In hello file picker, select hello map file that you want tooupload, then select **Open**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/edit-2.png)

## <a name="how-toodelete-a-map"></a><span data-ttu-id="fa80a-133">¿Cómo toodelete un mapa?</span><span class="sxs-lookup"><span data-stu-id="fa80a-133">How toodelete a map?</span></span>

1. <span data-ttu-id="fa80a-134">Elija hello **mapas** icono.</span><span class="sxs-lookup"><span data-stu-id="fa80a-134">Choose hello **Maps** tile.</span></span>

2. <span data-ttu-id="fa80a-135">Después de abre la hoja de mapas de hello, seleccione asignación de hello desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="fa80a-135">After hello Maps blade opens, select hello map you want toodelete.</span></span>

3. <span data-ttu-id="fa80a-136">Elija **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="fa80a-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete.png)

4. <span data-ttu-id="fa80a-137">Confirme que desea que el mapa de hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="fa80a-137">Confirm that you want toodelete hello map.</span></span>

    ![](./media/logic-apps-enterprise-integration-maps/delete-confirmation-1.png)

## <a name="next-steps"></a><span data-ttu-id="fa80a-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fa80a-138">Next Steps</span></span>
* [<span data-ttu-id="fa80a-139">Obtener más información sobre Hola paquete de integración empresarial</span><span class="sxs-lookup"><span data-stu-id="fa80a-139">Learn more about hello Enterprise Integration Pack</span></span>](logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial")  
* [<span data-ttu-id="fa80a-140">Más información sobre los contratos</span><span class="sxs-lookup"><span data-stu-id="fa80a-140">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Información sobre los contratos de integración de empresas")  
* [<span data-ttu-id="fa80a-141">Más información sobre las transformaciones</span><span class="sxs-lookup"><span data-stu-id="fa80a-141">Learn more about transforms</span></span>](logic-apps-enterprise-integration-transform.md "Información sobre las transformaciones de integración empresarial")  

