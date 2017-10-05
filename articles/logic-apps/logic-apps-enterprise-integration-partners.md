---
title: "Creación de asociados para mensajes de negocio a negocio (B2B): Azure Logic Apps | Microsoft Docs"
description: "Información sobre cómo agregar asociados a una cuenta de integración con Enterprise Integration Pack y Logic Apps"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: b179325c-a511-4c1b-9796-f7484b4f6873
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 950cb449b53f400f0f0f860caf5415bbb5212269
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="5bfcf-103">Incorporación o actualización de asociados de contratos de negocio a negocio del flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="5bfcf-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="5bfcf-104">Los asociados son entidades que participan en transacciones de negocio a negocio (B2B) e intercambian mensajes entre ellos.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="5bfcf-105">Antes de poder crear asociados que le representen a usted y a otra organización en estas transacciones, debe compartir la información que identifica y valida los mensajes enviados por cada uno.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="5bfcf-106">Después de analizar estos detalles y prepararse para comenzar la relación de negocios, podrá crear asociados en la cuenta de integración para que los represente a ambos.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-106">After you discuss these details and are ready to start your business relationship, you can create partners in your integration account to represent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="5bfcf-107">¿Qué roles tienen los asociados en la cuenta de integración?</span><span class="sxs-lookup"><span data-stu-id="5bfcf-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="5bfcf-108">Para definir los detalles acerca de los mensajes intercambiados entre los asociados, debe crear contratos entre ellos.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-108">To define details about the messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="5bfcf-109">No obstante, antes de crear uno, hay que agregar, como mínimo, dos asociados a la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-109">However, before you can create an agreement, you must have added at least two partners to your integration account.</span></span> <span data-ttu-id="5bfcf-110">La organización debe formar parte del contrato como **asociado del host**.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-110">Your organization must be part of the agreement as the **host partner**.</span></span> <span data-ttu-id="5bfcf-111">El otro asociado, o **asociado invitado**, representa la organización que intercambia mensajes con su organización.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-111">The other partner, or **guest partner** represents the organization that exchanges messages with your organization.</span></span> <span data-ttu-id="5bfcf-112">El asociado invitado puede ser otra compañía o incluso un departamento de su organización.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-112">The guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="5bfcf-113">Después de agregar a estos asociados, puede crear un contrato.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="5bfcf-114">La configuración de recepción y de envío afecta exclusivamente al partner anfitrión.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-114">Receive and Send settings are oriented from the point of view of the Hosted Partner.</span></span> <span data-ttu-id="5bfcf-115">Por ejemplo, la configuración de recepción de un contrato determina cómo el partner anfitrión recibe los mensajes enviados de un partner invitado.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-115">For example, the receive settings in an agreement determine how the hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="5bfcf-116">Del mismo modo, la configuración de envío del contrato indica cómo el partner anfitrión envía mensajes al partner invitado.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-116">Likewise, the send settings on the agreement indicate how the hosted partner sends messages to the guest partner.</span></span>

## <a name="how-to-create-a-partner"></a><span data-ttu-id="5bfcf-117">¿Cómo se crean partners?</span><span class="sxs-lookup"><span data-stu-id="5bfcf-117">How to create a partner?</span></span>

1. <span data-ttu-id="5bfcf-118">En Azure Portal, seleccione **Examinar**.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-118">In the Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="5bfcf-119">En el cuadro de búsqueda, especifique **integración** y seleccione **Integration Accounts** (Cuentas de integración) en la lista de resultados.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-119">In the filter search box, enter **integration**, then select **Integration Accounts** in the results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="5bfcf-120">Seleccione la cuenta integración en la que desea agregar a los asociados.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-120">Select the integration account where you want to add your partners.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="5bfcf-121">Seleccione el icono de **Asociados** .</span><span class="sxs-lookup"><span data-stu-id="5bfcf-121">Select the **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="5bfcf-122">En la hoja de asociados, seleccione **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-122">In the Partners blade, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="5bfcf-123">Escriba un nombre para el asociado y, a continuación, seleccione un **Calificador**.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="5bfcf-124">Finalmente, escriba un **valor** para ayudar a identificar los documentos que se incluyen en las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-124">Finally, enter a **Value** to help identify documents that come into your apps.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="5bfcf-125">Seleccione el icono de notificación de *campana* para ver el progreso del proceso de creación de asociados.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-125">To see the progress for your partner creation process, select the *bell* notification icon.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="5bfcf-126">Para confirmar que los nuevos asociados se agregaron correctamente, seleccione el icono de **Asociados**.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-126">To confirm that your new partners were successfully added, select the **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="5bfcf-127">Cuando haya seleccionado el icono de Asociados, también verá que los asociados que acaba de agregar aparecen en la hoja Asociados.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-127">After you select the Partners tile, you'll also see  newly added partners in the Partners blade.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-to-edit-existing-partners-in-your-integration-account"></a><span data-ttu-id="5bfcf-128">Edición de asociados existentes en su cuenta de integración</span><span class="sxs-lookup"><span data-stu-id="5bfcf-128">How to edit existing partners in your integration account</span></span>

1. <span data-ttu-id="5bfcf-129">Seleccione el icono de **Asociados** .</span><span class="sxs-lookup"><span data-stu-id="5bfcf-129">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="5bfcf-130">Seleccione el asociado que quiera editar cuando se abra la hoja Asociados.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-130">After the Partners blade opens, select the partner you want to edit.</span></span>
3. <span data-ttu-id="5bfcf-131">En el icono **Actualizar asociado**, realice los cambios.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-131">On the **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="5bfcf-132">Cuando haya terminado, elija **Guardar** o, para cancelar los cambios, seleccione **Descartar**.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-132">After you're done, choose **Save**, or to cancel your changes, select **Discard**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-to-delete-a-partner"></a><span data-ttu-id="5bfcf-133">¿Cómo se eliminan partners?</span><span class="sxs-lookup"><span data-stu-id="5bfcf-133">How to delete a partner</span></span>

1. <span data-ttu-id="5bfcf-134">Seleccione el icono de **Asociados** .</span><span class="sxs-lookup"><span data-stu-id="5bfcf-134">Select the **Partners** tile.</span></span>
2. <span data-ttu-id="5bfcf-135">Seleccione el asociado que desea eliminar cuando se abra la hoja Asociados.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-135">After the Partner blade opens, select the partner that you want to delete.</span></span>
3. <span data-ttu-id="5bfcf-136">Elija **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="5bfcf-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="5bfcf-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="5bfcf-137">Next steps</span></span>
* [<span data-ttu-id="5bfcf-138">Más información sobre los contratos</span><span class="sxs-lookup"><span data-stu-id="5bfcf-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Información sobre los contratos de integración de empresas")  

