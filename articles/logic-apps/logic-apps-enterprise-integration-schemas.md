---
title: "Esquemas para la validación de XML: Azure Logic Apps | Microsoft Docs"
description: "Validación de documentos XML con esquemas para Azure Logic Apps y Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 56c5846c-5d8c-4ad4-9652-60b07aa8fc3b
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/29/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 4f58a587c1f10aea1cee89e46fa9ec340e0d21c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-the-enterprise-integration-pack"></a><span data-ttu-id="be1ef-103">Validación de documentos XML con esquemas para Azure Logic Apps y Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="be1ef-103">Validate XML with schemas for Azure Logic Apps and the Enterprise Integration Pack</span></span>

<span data-ttu-id="be1ef-104">Los esquemas permiten confirmar que los documentos XML recibidos son válidos y que contienen los datos esperados en un formato predefinido.</span><span class="sxs-lookup"><span data-stu-id="be1ef-104">Schemas confirm that the XML documents you receive are valid and have the expected data in a predefined format.</span></span> <span data-ttu-id="be1ef-105">Los esquemas también ayudan a validar los mensajes que se intercambian en un escenario B2B.</span><span class="sxs-lookup"><span data-stu-id="be1ef-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span></span>

## <a name="add-a-schema"></a><span data-ttu-id="be1ef-106">Agregar un esquema</span><span class="sxs-lookup"><span data-stu-id="be1ef-106">Add a schema</span></span>

1. <span data-ttu-id="be1ef-107">En Azure Portal, seleccione **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="be1ef-107">In the Azure portal, select **More services**.</span></span>

    ![Azure Portal, "Más servicios"](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. <span data-ttu-id="be1ef-109">En el cuadro de búsqueda, especifique **integración** y seleccione **Integration Accounts** (Cuentas de integración) en la lista de resultados.</span><span class="sxs-lookup"><span data-stu-id="be1ef-109">In the filter search box, enter **integration**, and select **Integration Accounts** from the results list.</span></span>

    ![Cuadro de búsqueda](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. <span data-ttu-id="be1ef-111">Seleccione la **cuenta integración** en la que vaya a agregar el esquema.</span><span class="sxs-lookup"><span data-stu-id="be1ef-111">Select the **integration account** where you want to add the schema.</span></span>

    ![Lista de cuentas de integración](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. <span data-ttu-id="be1ef-113">Seleccione el icono de **Esquemas**.</span><span class="sxs-lookup"><span data-stu-id="be1ef-113">Choose the **Schemas** tile.</span></span>

    ![Cuenta de integración de ejemplo, "Esquemas"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a><span data-ttu-id="be1ef-115">Incorporación de un archivo de esquema inferior a 2 MB</span><span class="sxs-lookup"><span data-stu-id="be1ef-115">Add a schema file smaller than 2 MB</span></span>

1. <span data-ttu-id="be1ef-116">En la hoja **Esquemas** que se abre (de los pasos anteriores), elija **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="be1ef-116">In the **Schemas** blade that opens (from the preceding steps), choose **Add**.</span></span>

    ![Hoja de esquemas, "Agregar"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. <span data-ttu-id="be1ef-118">Escriba un nombre para el esquema.</span><span class="sxs-lookup"><span data-stu-id="be1ef-118">Enter a name for your schema.</span></span> <span data-ttu-id="be1ef-119">Para cargar el archivo de esquema, seleccione el icono de carpeta junto al cuadro de texto **Esquema**.</span><span class="sxs-lookup"><span data-stu-id="be1ef-119">Upload the schema file by selecting the folder icon next to the **Schema** box.</span></span> <span data-ttu-id="be1ef-120">Cuando termine el proceso de carga, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="be1ef-120">After the upload process completes, select **OK**.</span></span>

    ![Captura de pantalla de "Agregar esquema" con "Archivo pequeño" resaltado](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-to-8-mb-maximum"></a><span data-ttu-id="be1ef-122">Incorporación de un archivo de esquema superior a 2 MB (hasta un máximo de 8 MB)</span><span class="sxs-lookup"><span data-stu-id="be1ef-122">Add a schema file larger than 2 MB (up to 8 MB maximum)</span></span>

<span data-ttu-id="be1ef-123">Estos pasos difieren en función del nivel de acceso del contenedor de blob: **Público** o **Sin acceso anónimo**.</span><span class="sxs-lookup"><span data-stu-id="be1ef-123">These steps differ based on the blob container access level: **Public** or **No anonymous access**.</span></span>

<span data-ttu-id="be1ef-124">**Para determinar este nivel de acceso**</span><span class="sxs-lookup"><span data-stu-id="be1ef-124">**To determine this access level**</span></span>

1.  <span data-ttu-id="be1ef-125">Abra el **Explorador de Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="be1ef-125">Open **Azure Storage Explorer**.</span></span> 

2.  <span data-ttu-id="be1ef-126">En **Contenedores de blob**, seleccione el contenedor de blob que desee.</span><span class="sxs-lookup"><span data-stu-id="be1ef-126">Under **Blob Containers**, select the blob container you want.</span></span> 

3.  <span data-ttu-id="be1ef-127">Seleccione **Seguridad**, **Nivel de acceso**.</span><span class="sxs-lookup"><span data-stu-id="be1ef-127">Select **Security**, **Access Level**.</span></span>

<span data-ttu-id="be1ef-128">Si el nivel de acceso de seguridad de blob es **Público**, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="be1ef-128">If the blob security access level is **Public**, follow these steps.</span></span>

![Explorador de Azure Storage, con "Contenedores de blob", "Seguridad" y "Público" resaltados](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. <span data-ttu-id="be1ef-130">Cargue el esquema en la cuenta de almacenamiento y copie el URI.</span><span class="sxs-lookup"><span data-stu-id="be1ef-130">Upload the schema to your storage account, and copy the URI.</span></span>

    ![Cuenta de almacenamiento con URI resaltado](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. <span data-ttu-id="be1ef-132">En **Agregar esquema**, seleccione **Archivo grande** y proporcione el URI en el cuadro de texto **URI de contenido**.</span><span class="sxs-lookup"><span data-stu-id="be1ef-132">In **Add Schema**, select **Large file**, and provide the URI in the **Content URI** text box.</span></span>

    ![Esquemas con el botón "Agregar" y "Archivo grande" resaltados](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

<span data-ttu-id="be1ef-134">Si el nivel de acceso de seguridad de blob es **Sin acceso anónimo**, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="be1ef-134">If the blob security access level is **No anonymous access**, follow these steps.</span></span>

![Explorador de Azure Storage, con "Contenedores de blob", "Seguridad" y "Sin acceso anónimo" resaltados](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. <span data-ttu-id="be1ef-136">Cargue el esquema en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="be1ef-136">Upload the schema to your storage account.</span></span>

    ![Cuenta de almacenamiento](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. <span data-ttu-id="be1ef-138">Genere una firma de acceso compartido para el esquema.</span><span class="sxs-lookup"><span data-stu-id="be1ef-138">Generate a shared access signature for the schema.</span></span>

    ![Cuenta de almacenamiento con la ficha firmas de acceso compartido resaltada](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. <span data-ttu-id="be1ef-140">En **Agregar esquema**, seleccione **Archivo grande** y proporcione el URI de firma de acceso compartido en el cuadro de texto **URI de contenido**.</span><span class="sxs-lookup"><span data-stu-id="be1ef-140">In **Add Schema**, select **Large file**, and provide the shared access signature URI in the **Content URI** text box.</span></span>

    ![Esquemas con el botón "Agregar" y "Archivo grande" resaltados](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. <span data-ttu-id="be1ef-142">En la hoja **Esquemas** de la cuenta de integración debería ver ahora el esquema recién agregado.</span><span class="sxs-lookup"><span data-stu-id="be1ef-142">In the **Schemas** blade of your integration account, your newly added schema should appear.</span></span>

    ![Cuenta de integración con "Esquemas" y el nuevo esquema resaltados](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a><span data-ttu-id="be1ef-144">Editar esquemas</span><span class="sxs-lookup"><span data-stu-id="be1ef-144">Edit schemas</span></span>

1. <span data-ttu-id="be1ef-145">Seleccione el icono de **Esquemas**.</span><span class="sxs-lookup"><span data-stu-id="be1ef-145">Choose the **Schemas** tile.</span></span>

2. <span data-ttu-id="be1ef-146">Cuando se abra la hoja **Esquemas**, seleccione el esquema que desea editar.</span><span class="sxs-lookup"><span data-stu-id="be1ef-146">After the **Schemas** blade opens, select the schema that you want to edit.</span></span>

3. <span data-ttu-id="be1ef-147">En la hoja **Esquemas**, seleccione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="be1ef-147">On the **Schemas** blade, choose **Edit**.</span></span>

    ![Hoja de esquemas](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. <span data-ttu-id="be1ef-149">Seleccione el archivo de esquemas que desea editar y, a continuación, seleccione **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="be1ef-149">Select the schema file that you want to edit, then select **Open**.</span></span>

    ![Abrir archivo de esquema que desea editar](media/logic-apps-enterprise-integration-schemas/edit-31.png)

<span data-ttu-id="be1ef-151">Azure muestra un mensaje que indica que el esquema se ha cargado correctamente.</span><span class="sxs-lookup"><span data-stu-id="be1ef-151">Azure shows a message that the schema uploaded successfully.</span></span>

## <a name="delete-schemas"></a><span data-ttu-id="be1ef-152">Eliminar esquemas</span><span class="sxs-lookup"><span data-stu-id="be1ef-152">Delete schemas</span></span>

1. <span data-ttu-id="be1ef-153">Seleccione el icono de **Esquemas**.</span><span class="sxs-lookup"><span data-stu-id="be1ef-153">Choose the **Schemas** tile.</span></span>

2. <span data-ttu-id="be1ef-154">Cuando se abra la hoja **Esquemas**, seleccione el esquema que desea eliminar.</span><span class="sxs-lookup"><span data-stu-id="be1ef-154">After the **Schemas** blade opens, select the schema you want to delete.</span></span>

3. <span data-ttu-id="be1ef-155">En la hoja **Esquemas**, seleccione **Editar**.</span><span class="sxs-lookup"><span data-stu-id="be1ef-155">On the **Schemas** blade, choose **Delete**.</span></span>

    ![Hoja de esquemas](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. <span data-ttu-id="be1ef-157">Para confirmar que desea eliminar el contrato seleccionado, elija **Sí**.</span><span class="sxs-lookup"><span data-stu-id="be1ef-157">To confirm that you want to delete the selected schema, choose **Yes**.</span></span>

    ![Mensaje de confirmación para "Eliminar esquema"](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    <span data-ttu-id="be1ef-159">En la hoja **Esquemas**, la lista de esquemas se actualiza y ya no incluye el esquema que ha eliminado.</span><span class="sxs-lookup"><span data-stu-id="be1ef-159">In the **Schemas** blade, the schema list refreshes  and no longer includes the schema that you deleted.</span></span>

    ![La cuenta de integración con "Esquemas" resaltado](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a><span data-ttu-id="be1ef-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="be1ef-161">Next steps</span></span>
* <span data-ttu-id="be1ef-162">[Más información sobre Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Información sobre Enterprise Integration Pack").</span><span class="sxs-lookup"><span data-stu-id="be1ef-162">[Learn more about the Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about the enterprise integration pack").</span></span>  

