---
title: "asociados de aaaCreate para mensajes de negocio a negocio (B2B): las aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tooyour integración de tooadd asociados cuenta con hello paquete de integración empresarial y las aplicaciones lógicas"
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
ms.openlocfilehash: 8dc70a8f441fcf228ed178029dcdbac940d794b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a><span data-ttu-id="23c3d-103">Incorporación o actualización de asociados de contratos de negocio a negocio del flujo de trabajo</span><span class="sxs-lookup"><span data-stu-id="23c3d-103">Add or update partners in business-to-business agreements in your workflow</span></span>

<span data-ttu-id="23c3d-104">Los asociados son entidades que participan en transacciones de negocio a negocio (B2B) e intercambian mensajes entre ellos.</span><span class="sxs-lookup"><span data-stu-id="23c3d-104">Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other.</span></span> <span data-ttu-id="23c3d-105">Antes de poder crear asociados que le representen a usted y a otra organización en estas transacciones, debe compartir la información que identifica y valida los mensajes enviados por cada uno.</span><span class="sxs-lookup"><span data-stu-id="23c3d-105">Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other.</span></span> <span data-ttu-id="23c3d-106">Después de que analizan estos detalles y toostart preparado su relación de negocios, puede crear socios en su toorepresent de cuenta de integración que ambos.</span><span class="sxs-lookup"><span data-stu-id="23c3d-106">After you discuss these details and are ready toostart your business relationship, you can create partners in your integration account toorepresent you both.</span></span>

## <a name="what-roles-do-partners-have-in-your-integration-account"></a><span data-ttu-id="23c3d-107">¿Qué roles tienen los asociados en la cuenta de integración?</span><span class="sxs-lookup"><span data-stu-id="23c3d-107">What roles do partners have in your integration account?</span></span>

<span data-ttu-id="23c3d-108">toodefine obtener más información acerca de los mensajes de Hola intercambiados entre los asociados, crear acuerdos entre los socios.</span><span class="sxs-lookup"><span data-stu-id="23c3d-108">toodefine details about hello messages exchanged between partners, you create agreements between those partners.</span></span> <span data-ttu-id="23c3d-109">Sin embargo, antes de poder crear un acuerdo, debe haber agregado cuenta de integración de tooyour de al menos dos socios comerciales.</span><span class="sxs-lookup"><span data-stu-id="23c3d-109">However, before you can create an agreement, you must have added at least two partners tooyour integration account.</span></span> <span data-ttu-id="23c3d-110">Su organización debe formar parte del contrato de Hola Hola **socio del host**.</span><span class="sxs-lookup"><span data-stu-id="23c3d-110">Your organization must be part of hello agreement as hello **host partner**.</span></span> <span data-ttu-id="23c3d-111">Hola otro asociado o **socio invitado** representa Hola organización que intercambia mensajes con su organización.</span><span class="sxs-lookup"><span data-stu-id="23c3d-111">hello other partner, or **guest partner** represents hello organization that exchanges messages with your organization.</span></span> <span data-ttu-id="23c3d-112">Socio invitado de Hello puede ser otra compañía, o incluso un departamento de su propia organización.</span><span class="sxs-lookup"><span data-stu-id="23c3d-112">hello guest partner can be another company, or even a department in your own organization.</span></span>

<span data-ttu-id="23c3d-113">Después de agregar a estos asociados, puede crear un contrato.</span><span class="sxs-lookup"><span data-stu-id="23c3d-113">After you add these partners, you can create an agreement.</span></span>

<span data-ttu-id="23c3d-114">Recepción y configuración de envío se orientan de hello punto de vista de hello Hosted asociado.</span><span class="sxs-lookup"><span data-stu-id="23c3d-114">Receive and Send settings are oriented from hello point of view of hello Hosted Partner.</span></span> <span data-ttu-id="23c3d-115">Por ejemplo, hello configuración de recepción de un acuerdo determinar cómo asociado Hola hospedado recibe los mensajes enviados desde un socio invitado.</span><span class="sxs-lookup"><span data-stu-id="23c3d-115">For example, hello receive settings in an agreement determine how hello hosted partner receives messages sent from a guest partner.</span></span> <span data-ttu-id="23c3d-116">Del mismo modo, configuración de envío Hola acuerdo Hola indica cómo asociado Hola hospedado envía a socio invitado de toohello de mensajes.</span><span class="sxs-lookup"><span data-stu-id="23c3d-116">Likewise, hello send settings on hello agreement indicate how hello hosted partner sends messages toohello guest partner.</span></span>

## <a name="how-toocreate-a-partner"></a><span data-ttu-id="23c3d-117">¿Cómo toocreate un socio?</span><span class="sxs-lookup"><span data-stu-id="23c3d-117">How toocreate a partner?</span></span>

1. <span data-ttu-id="23c3d-118">Hola portal de Azure, seleccione **examinar**.</span><span class="sxs-lookup"><span data-stu-id="23c3d-118">In hello Azure portal, select **Browse**.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-1.png)

2. <span data-ttu-id="23c3d-119">En el cuadro de búsqueda del filtro de hello, escriba **integración**, a continuación, seleccione **cuentas de integración** en la lista de resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="23c3d-119">In hello filter search box, enter **integration**, then select **Integration Accounts** in hello results list.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-2.png)

3. <span data-ttu-id="23c3d-120">Seleccione la cuenta de integración de Hola donde desea tooadd sus socios.</span><span class="sxs-lookup"><span data-stu-id="23c3d-120">Select hello integration account where you want tooadd your partners.</span></span>

    ![](./media/logic-apps-enterprise-integration-overview/overview-3.png)

4. <span data-ttu-id="23c3d-121">Seleccione hello **socios** icono.</span><span class="sxs-lookup"><span data-stu-id="23c3d-121">Select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-1.png)

5. <span data-ttu-id="23c3d-122">En la hoja de socios de hello, elija **agregar**.</span><span class="sxs-lookup"><span data-stu-id="23c3d-122">In hello Partners blade, choose **Add**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-2.png)

6. <span data-ttu-id="23c3d-123">Escriba un nombre para el asociado y, a continuación, seleccione un **Calificador**.</span><span class="sxs-lookup"><span data-stu-id="23c3d-123">Enter a name for your partner, then select a **Qualifier**.</span></span> <span data-ttu-id="23c3d-124">Por último, especifique un **valor** toohelp identificar documentos que acompañan a las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="23c3d-124">Finally, enter a **Value** toohelp identify documents that come into your apps.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-3.png)

7. <span data-ttu-id="23c3d-125">progreso de hello toosee para el proceso de creación de socios comerciales, seleccione hello *campana* icono de notificación.</span><span class="sxs-lookup"><span data-stu-id="23c3d-125">toosee hello progress for your partner creation process, select hello *bell* notification icon.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-4.png)

8. <span data-ttu-id="23c3d-126">tooconfirm que los socios nueva estaban correctamente agregado, seleccione hello **socios** icono.</span><span class="sxs-lookup"><span data-stu-id="23c3d-126">tooconfirm that your new partners were successfully added, select hello **Partners** tile.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-5.png)

    <span data-ttu-id="23c3d-127">Después de seleccionar el icono de socios de hello, también verá recién agregados asociados en la hoja de socios de Hola.</span><span class="sxs-lookup"><span data-stu-id="23c3d-127">After you select hello Partners tile, you'll also see  newly added partners in hello Partners blade.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-tooedit-existing-partners-in-your-integration-account"></a><span data-ttu-id="23c3d-128">Cómo los partners de tooedit existente en su cuenta de integración</span><span class="sxs-lookup"><span data-stu-id="23c3d-128">How tooedit existing partners in your integration account</span></span>

1. <span data-ttu-id="23c3d-129">Seleccione hello **socios** icono.</span><span class="sxs-lookup"><span data-stu-id="23c3d-129">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="23c3d-130">Después de abre la hoja de socios de hello, seleccione a socio comercial de hello desea tooedit.</span><span class="sxs-lookup"><span data-stu-id="23c3d-130">After hello Partners blade opens, select hello partner you want tooedit.</span></span>
3. <span data-ttu-id="23c3d-131">En hello **actualización asociado** icono, realice los cambios.</span><span class="sxs-lookup"><span data-stu-id="23c3d-131">On hello **Update Partner** tile, make your changes.</span></span>
4. <span data-ttu-id="23c3d-132">Cuando haya terminado, elija **guardar**, o toocancel los cambios, seleccione **descartar**.</span><span class="sxs-lookup"><span data-stu-id="23c3d-132">After you're done, choose **Save**, or toocancel your changes, select **Discard**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-toodelete-a-partner"></a><span data-ttu-id="23c3d-133">¿Cómo toodelete un socio</span><span class="sxs-lookup"><span data-stu-id="23c3d-133">How toodelete a partner</span></span>

1. <span data-ttu-id="23c3d-134">Seleccione hello **socios** icono.</span><span class="sxs-lookup"><span data-stu-id="23c3d-134">Select hello **Partners** tile.</span></span>
2. <span data-ttu-id="23c3d-135">Después de abre la hoja de socio comercial de hello, seleccione a socio comercial de Hola que desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="23c3d-135">After hello Partner blade opens, select hello partner that you want toodelete.</span></span>
3. <span data-ttu-id="23c3d-136">Elija **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="23c3d-136">Choose **Delete**.</span></span>

    ![](./media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a><span data-ttu-id="23c3d-137">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="23c3d-137">Next steps</span></span>
* [<span data-ttu-id="23c3d-138">Más información sobre los contratos</span><span class="sxs-lookup"><span data-stu-id="23c3d-138">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Información sobre los contratos de integración de empresas")  

