---
title: "aaaSchemas para la validación de XML: las aplicaciones lógicas de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 87cf92741e10ff7cccd260f27442909e34928903
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="validate-xml-with-schemas-for-azure-logic-apps-and-hello-enterprise-integration-pack"></a><span data-ttu-id="f0656-103">Validar XML con esquemas de hello paquete de integración empresarial y las aplicaciones lógicas de Azure</span><span class="sxs-lookup"><span data-stu-id="f0656-103">Validate XML with schemas for Azure Logic Apps and hello Enterprise Integration Pack</span></span>

<span data-ttu-id="f0656-104">Esquemas confirmación que documentos XML de hello que recibirá son válidos y que han Hola esperado datos en un formato predefinido.</span><span class="sxs-lookup"><span data-stu-id="f0656-104">Schemas confirm that hello XML documents you receive are valid and have hello expected data in a predefined format.</span></span> <span data-ttu-id="f0656-105">Los esquemas también ayudan a validar los mensajes que se intercambian en un escenario B2B.</span><span class="sxs-lookup"><span data-stu-id="f0656-105">Schemas also help validate messages that are exchanged in a B2B scenario.</span></span>

## <a name="add-a-schema"></a><span data-ttu-id="f0656-106">Agregar un esquema</span><span class="sxs-lookup"><span data-stu-id="f0656-106">Add a schema</span></span>

1. <span data-ttu-id="f0656-107">Hola portal de Azure, seleccione **más servicios**.</span><span class="sxs-lookup"><span data-stu-id="f0656-107">In hello Azure portal, select **More services**.</span></span>

    ![Azure Portal, "Más servicios"](media/logic-apps-enterprise-integration-schemas/overview-11.png)

2. <span data-ttu-id="f0656-109">En el cuadro de búsqueda del filtro de hello, escriba **integración**y seleccione **cuentas de integración** desde la lista de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0656-109">In hello filter search box, enter **integration**, and select **Integration Accounts** from hello results list.</span></span>

    ![Cuadro de búsqueda](media/logic-apps-enterprise-integration-schemas/overview-21.png)

3. <span data-ttu-id="f0656-111">Seleccione hello **cuenta integración** donde desea que el esquema de hello tooadd.</span><span class="sxs-lookup"><span data-stu-id="f0656-111">Select hello **integration account** where you want tooadd hello schema.</span></span>

    ![Lista de cuentas de integración](media/logic-apps-enterprise-integration-schemas/overview-31.png)

4. <span data-ttu-id="f0656-113">Elija hello **esquemas** icono.</span><span class="sxs-lookup"><span data-stu-id="f0656-113">Choose hello **Schemas** tile.</span></span>

    ![Cuenta de integración de ejemplo, "Esquemas"](media/logic-apps-enterprise-integration-schemas/schema-11.png)

### <a name="add-a-schema-file-smaller-than-2-mb"></a><span data-ttu-id="f0656-115">Incorporación de un archivo de esquema inferior a 2 MB</span><span class="sxs-lookup"><span data-stu-id="f0656-115">Add a schema file smaller than 2 MB</span></span>

1. <span data-ttu-id="f0656-116">Hola **esquemas** hoja que se abre (de Hola pasos anteriores), elija **agregar**.</span><span class="sxs-lookup"><span data-stu-id="f0656-116">In hello **Schemas** blade that opens (from hello preceding steps), choose **Add**.</span></span>

    ![Hoja de esquemas, "Agregar"](media/logic-apps-enterprise-integration-schemas/schema-21.png)

2. <span data-ttu-id="f0656-118">Escriba un nombre para el esquema.</span><span class="sxs-lookup"><span data-stu-id="f0656-118">Enter a name for your schema.</span></span> <span data-ttu-id="f0656-119">Cargar archivo de esquema de hello seleccionando el icono de carpeta hello toohello siguiente **esquema** cuadro.</span><span class="sxs-lookup"><span data-stu-id="f0656-119">Upload hello schema file by selecting hello folder icon next toohello **Schema** box.</span></span> <span data-ttu-id="f0656-120">Una vez completado el proceso de carga de hello, seleccione **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="f0656-120">After hello upload process completes, select **OK**.</span></span>

    ![Captura de pantalla de "Agregar esquema" con "Archivo pequeño" resaltado](media/logic-apps-enterprise-integration-schemas/schema-31.png)

### <a name="add-a-schema-file-larger-than-2-mb-up-too8-mb-maximum"></a><span data-ttu-id="f0656-122">Agregar un archivo de esquema superior a 2 MB (arriba too8 MB como máximo)</span><span class="sxs-lookup"><span data-stu-id="f0656-122">Add a schema file larger than 2 MB (up too8 MB maximum)</span></span>

<span data-ttu-id="f0656-123">Estos pasos varían en función de nivel de acceso de contenedor de blob de hello: **público** o **ningún acceso anónimo**.</span><span class="sxs-lookup"><span data-stu-id="f0656-123">These steps differ based on hello blob container access level: **Public** or **No anonymous access**.</span></span>

<span data-ttu-id="f0656-124">**toodetermine este nivel de acceso**</span><span class="sxs-lookup"><span data-stu-id="f0656-124">**toodetermine this access level**</span></span>

1.  <span data-ttu-id="f0656-125">Abra el **Explorador de Azure Storage**.</span><span class="sxs-lookup"><span data-stu-id="f0656-125">Open **Azure Storage Explorer**.</span></span> 

2.  <span data-ttu-id="f0656-126">En **contenedores de blobs**, seleccione contenedor de blobs de Hola que desee.</span><span class="sxs-lookup"><span data-stu-id="f0656-126">Under **Blob Containers**, select hello blob container you want.</span></span> 

3.  <span data-ttu-id="f0656-127">Seleccione **Seguridad**, **Nivel de acceso**.</span><span class="sxs-lookup"><span data-stu-id="f0656-127">Select **Security**, **Access Level**.</span></span>

<span data-ttu-id="f0656-128">Si es el nivel de acceso de seguridad de blob de hello **público**, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="f0656-128">If hello blob security access level is **Public**, follow these steps.</span></span>

![Explorador de Azure Storage, con "Contenedores de blob", "Seguridad" y "Público" resaltados](media/logic-apps-enterprise-integration-schemas/blob-public.png)

1. <span data-ttu-id="f0656-130">Cargar la cuenta de almacenamiento de hello esquema tooyour y copie Hola URI.</span><span class="sxs-lookup"><span data-stu-id="f0656-130">Upload hello schema tooyour storage account, and copy hello URI.</span></span>

    ![Cuenta de almacenamiento con URI resaltado](media/logic-apps-enterprise-integration-schemas/schema-blob.png)

2. <span data-ttu-id="f0656-132">En **Agregar esquema**, seleccione **archivo grande**y proporcionar Hola URI Hola **contenido URI** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="f0656-132">In **Add Schema**, select **Large file**, and provide hello URI in hello **Content URI** text box.</span></span>

    ![Esquemas con el botón "Agregar" y "Archivo grande" resaltados](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

<span data-ttu-id="f0656-134">Si es el nivel de acceso de seguridad de blob de hello **ningún acceso anónimo**, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="f0656-134">If hello blob security access level is **No anonymous access**, follow these steps.</span></span>

![Explorador de Azure Storage, con "Contenedores de blob", "Seguridad" y "Sin acceso anónimo" resaltados](media/logic-apps-enterprise-integration-schemas/blob-1.png)

1. <span data-ttu-id="f0656-136">Cargar la cuenta de almacenamiento de hello esquema tooyour.</span><span class="sxs-lookup"><span data-stu-id="f0656-136">Upload hello schema tooyour storage account.</span></span>

    ![Cuenta de almacenamiento](media/logic-apps-enterprise-integration-schemas/blob-3.png)

2. <span data-ttu-id="f0656-138">Generar una firma de acceso compartido para el esquema de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0656-138">Generate a shared access signature for hello schema.</span></span>

    ![Cuenta de almacenamiento con la ficha firmas de acceso compartido resaltada](media/logic-apps-enterprise-integration-schemas/blob-2.png)

3. <span data-ttu-id="f0656-140">En **Agregar esquema**, seleccione **archivo grande**y proporcione la firma de acceso compartido de hello URI Hola **contenido URI** cuadro de texto.</span><span class="sxs-lookup"><span data-stu-id="f0656-140">In **Add Schema**, select **Large file**, and provide hello shared access signature URI in hello **Content URI** text box.</span></span>

    ![Esquemas con el botón "Agregar" y "Archivo grande" resaltados](media/logic-apps-enterprise-integration-schemas/schema-largefile.png)

4. <span data-ttu-id="f0656-142">Hola **esquemas** hoja de la cuenta de integración, debe aparecer en el esquema recién agregado.</span><span class="sxs-lookup"><span data-stu-id="f0656-142">In hello **Schemas** blade of your integration account, your newly added schema should appear.</span></span>

    ![La cuenta de integración, con "Esquemas" y el esquema nuevo de hello resaltado](media/logic-apps-enterprise-integration-schemas/schema-41.png)

## <a name="edit-schemas"></a><span data-ttu-id="f0656-144">Editar esquemas</span><span class="sxs-lookup"><span data-stu-id="f0656-144">Edit schemas</span></span>

1. <span data-ttu-id="f0656-145">Elija hello **esquemas** icono.</span><span class="sxs-lookup"><span data-stu-id="f0656-145">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="f0656-146">Después de hello **esquemas** hoja se abre, esquema de hello select que desea tooedit.</span><span class="sxs-lookup"><span data-stu-id="f0656-146">After hello **Schemas** blade opens, select hello schema that you want tooedit.</span></span>

3. <span data-ttu-id="f0656-147">En hello **esquemas** hoja, elija **editar**.</span><span class="sxs-lookup"><span data-stu-id="f0656-147">On hello **Schemas** blade, choose **Edit**.</span></span>

    ![Hoja de esquemas](media/logic-apps-enterprise-integration-schemas/edit-12.png)

4. <span data-ttu-id="f0656-149">Archivo de esquema de hello SELECT que desee tooedit, a continuación, seleccione **abiertos**.</span><span class="sxs-lookup"><span data-stu-id="f0656-149">Select hello schema file that you want tooedit, then select **Open**.</span></span>

    ![Abrir esquema archivo tooedit](media/logic-apps-enterprise-integration-schemas/edit-31.png)

<span data-ttu-id="f0656-151">Azure muestra un mensaje que Hola esquema se cargó correctamente.</span><span class="sxs-lookup"><span data-stu-id="f0656-151">Azure shows a message that hello schema uploaded successfully.</span></span>

## <a name="delete-schemas"></a><span data-ttu-id="f0656-152">Eliminar esquemas</span><span class="sxs-lookup"><span data-stu-id="f0656-152">Delete schemas</span></span>

1. <span data-ttu-id="f0656-153">Elija hello **esquemas** icono.</span><span class="sxs-lookup"><span data-stu-id="f0656-153">Choose hello **Schemas** tile.</span></span>

2. <span data-ttu-id="f0656-154">Después de hello **esquemas** hoja se abre, esquema de hello seleccione desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="f0656-154">After hello **Schemas** blade opens, select hello schema you want toodelete.</span></span>

3. <span data-ttu-id="f0656-155">En hello **esquemas** hoja, elija **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="f0656-155">On hello **Schemas** blade, choose **Delete**.</span></span>

    ![Hoja de esquemas](media/logic-apps-enterprise-integration-schemas/delete-12.png)

4. <span data-ttu-id="f0656-157">tooconfirm que desea toodelete Hola selecciona esquema, elija **Sí**.</span><span class="sxs-lookup"><span data-stu-id="f0656-157">tooconfirm that you want toodelete hello selected schema, choose **Yes**.</span></span>

    ![Mensaje de confirmación para "Eliminar esquema"](media/logic-apps-enterprise-integration-schemas/delete-21.png)

    <span data-ttu-id="f0656-159">Hola **esquemas** hoja, la lista de esquemas de hello actualiza y ya no incluye el esquema de Hola que eliminó.</span><span class="sxs-lookup"><span data-stu-id="f0656-159">In hello **Schemas** blade, hello schema list refreshes  and no longer includes hello schema that you deleted.</span></span>

    ![La cuenta de integración con "Esquemas" resaltado](media/logic-apps-enterprise-integration-schemas/delete-31.png)

## <a name="next-steps"></a><span data-ttu-id="f0656-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f0656-161">Next steps</span></span>
* <span data-ttu-id="f0656-162">[Obtener más información sobre Hola paquete de integración empresarial](logic-apps-enterprise-integration-overview.md "Obtenga más información sobre el paquete de integración empresarial hello").</span><span class="sxs-lookup"><span data-stu-id="f0656-162">[Learn more about hello Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about hello enterprise integration pack").</span></span>  

