---
title: "Contratos de comunicación B2B: Azure Logic Apps | Microsoft Docs"
description: "Creación de contratos para que los asociados se puedan comunicar en escenarios B2B de Azure Logic Apps y Enterprise Integration Pack"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: 447ffb8e-3e91-4403-872b-2f496495899d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2016
ms.author: LADocs
ms.openlocfilehash: 7ce0860272901f3b4e4cf3d63f7361d539f64741
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="partner-agreements-for-b2b-communication-with-azure-logic-apps-and-enterprise-integration-pack"></a><span data-ttu-id="a06e1-103">Contratos de asociados para la comunicación B2B con Azure Logic Apps y Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="a06e1-103">Partner agreements for B2B communication with Azure Logic Apps and Enterprise Integration Pack</span></span>

<span data-ttu-id="a06e1-104">Los contratos son la piedra angular de las comunicaciones de negocio a negocio (B2B) que permiten a las entidades empresariales comunicarse perfectamente mediante protocolos estándar del sector.</span><span class="sxs-lookup"><span data-stu-id="a06e1-104">Agreements let business entities communicate seamlessly using industry standard protocols and are the cornerstone for business-to-business (B2B) communication.</span></span> <span data-ttu-id="a06e1-105">Al habilitar escenarios B2B para aplicaciones lógicas con Enterprise Integration Pack, un contrato es una disposición de las comunicaciones entre los socios comerciales B2B.</span><span class="sxs-lookup"><span data-stu-id="a06e1-105">When enabling B2B scenarios for logic apps with the Enterprise Integration Pack, an agreement is a communications arrangement between B2B trading partners.</span></span> <span data-ttu-id="a06e1-106">Este contrato se basa en la comunicación que los asociados desean establecer y es específico del protocolo o transporte.</span><span class="sxs-lookup"><span data-stu-id="a06e1-106">This agreement is based on the communications that the partners want to establish and is protocol or transport-specific.</span></span>

<span data-ttu-id="a06e1-107">La integración de Enterprise admite estos estándares de protocolo o transporte:</span><span class="sxs-lookup"><span data-stu-id="a06e1-107">Enterprise integration supports these protocol or transport standards:</span></span>

* [<span data-ttu-id="a06e1-108">AS2</span><span class="sxs-lookup"><span data-stu-id="a06e1-108">AS2</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="a06e1-109">X12</span><span class="sxs-lookup"><span data-stu-id="a06e1-109">X12</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="a06e1-110">EDIFACT</span><span class="sxs-lookup"><span data-stu-id="a06e1-110">EDIFACT</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="why-use-agreements"></a><span data-ttu-id="a06e1-111">Por qué usar contratos</span><span class="sxs-lookup"><span data-stu-id="a06e1-111">Why use agreements</span></span>

<span data-ttu-id="a06e1-112">Estas son algunas de las ventajas más comunes de usar contratos:</span><span class="sxs-lookup"><span data-stu-id="a06e1-112">Here are some common benefits when using agreements:</span></span>

* <span data-ttu-id="a06e1-113">Permite que distintas organizaciones y empresas puedan intercambiar información en un formato conocido.</span><span class="sxs-lookup"><span data-stu-id="a06e1-113">Enables different organizations and businesses to exchange information in a well-known format.</span></span>
* <span data-ttu-id="a06e1-114">Mejora la eficacia al realizar transacciones B2B</span><span class="sxs-lookup"><span data-stu-id="a06e1-114">Improves efficiency when conducting B2B transactions</span></span>
* <span data-ttu-id="a06e1-115">Fácil de crearlos, administrarlos y utilizarlos al crear aplicaciones de Enterprise Integration</span><span class="sxs-lookup"><span data-stu-id="a06e1-115">Easy to create, manage, and use when creating enterprise integration apps</span></span>

## <a name="how-to-create-agreements"></a><span data-ttu-id="a06e1-116">Creación de contratos</span><span class="sxs-lookup"><span data-stu-id="a06e1-116">How to create agreements</span></span>

* [<span data-ttu-id="a06e1-117">Creación de un contrato AS2</span><span class="sxs-lookup"><span data-stu-id="a06e1-117">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
* [<span data-ttu-id="a06e1-118">Creación de un contrato X12</span><span class="sxs-lookup"><span data-stu-id="a06e1-118">Create an X12 agreement</span></span>](logic-apps-enterprise-integration-x12.md)
* [<span data-ttu-id="a06e1-119">Creación de un contrato EDIFACT</span><span class="sxs-lookup"><span data-stu-id="a06e1-119">Create an EDIFACT agreement</span></span>](logic-apps-enterprise-integration-edifact.md)

## <a name="how-to-use-an-agreement"></a><span data-ttu-id="a06e1-120">Uso de contratos</span><span class="sxs-lookup"><span data-stu-id="a06e1-120">How to use an agreement</span></span>

<span data-ttu-id="a06e1-121">Puede crear [aplicaciones lógicas](logic-apps-what-are-logic-apps.md "Más información sobre Logic Apps") con funcionalidades de B2B mediante el uso de un contrato que hay creado.</span><span class="sxs-lookup"><span data-stu-id="a06e1-121">You can create [logic apps](logic-apps-what-are-logic-apps.md "Learn about Logic apps") with B2B capabilities by using an agreement that you created.</span></span>

## <a name="how-to-edit-an-agreement"></a><span data-ttu-id="a06e1-122">Edición de contratos</span><span class="sxs-lookup"><span data-stu-id="a06e1-122">How to edit an agreement</span></span>

<span data-ttu-id="a06e1-123">Puede editar cualquier acuerdo siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a06e1-123">You can edit any agreement by following these steps:</span></span>

1. <span data-ttu-id="a06e1-124">Seleccione la cuenta de integración que contiene el contrato que desea actualizar.</span><span class="sxs-lookup"><span data-stu-id="a06e1-124">Select the integration account that has the agreement you want to update.</span></span>

2. <span data-ttu-id="a06e1-125">Seleccione el icono de **contratos**.</span><span class="sxs-lookup"><span data-stu-id="a06e1-125">Choose the **Agreements** tile.</span></span>

3. <span data-ttu-id="a06e1-126">En la hoja **Contratos**, seleccione el contrato.</span><span class="sxs-lookup"><span data-stu-id="a06e1-126">On the **Agreements** blade, select the agreement.</span></span>

4. <span data-ttu-id="a06e1-127">Elija **Editar**.</span><span class="sxs-lookup"><span data-stu-id="a06e1-127">Choose **Edit**.</span></span> <span data-ttu-id="a06e1-128">Realice los cambios.</span><span class="sxs-lookup"><span data-stu-id="a06e1-128">Make your changes.</span></span>

5. <span data-ttu-id="a06e1-129">Elija **Aceptar** para guardar los cambios.</span><span class="sxs-lookup"><span data-stu-id="a06e1-129">To save your changes, choose **OK**.</span></span>

## <a name="how-to-delete-an-agreement"></a><span data-ttu-id="a06e1-130">Eliminación de una cuenta</span><span class="sxs-lookup"><span data-stu-id="a06e1-130">How to delete an agreement</span></span>

<span data-ttu-id="a06e1-131">Puede eliminar cualquier acuerdo siguiendo estos pasos:</span><span class="sxs-lookup"><span data-stu-id="a06e1-131">You can delete any agreement by following these steps:</span></span>

1. <span data-ttu-id="a06e1-132">Seleccione la cuenta de integración que contiene el contrato que desea eliminar.</span><span class="sxs-lookup"><span data-stu-id="a06e1-132">Select the integration account that has the agreement you want to delete.</span></span>
2. <span data-ttu-id="a06e1-133">Seleccione el icono de **contratos**.</span><span class="sxs-lookup"><span data-stu-id="a06e1-133">Choose the **Agreements** tile.</span></span>
3. <span data-ttu-id="a06e1-134">En la hoja **Contratos**, seleccione el contrato.</span><span class="sxs-lookup"><span data-stu-id="a06e1-134">On the **Agreements** blade, select the agreement.</span></span>
4. <span data-ttu-id="a06e1-135">Elija **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="a06e1-135">Choose **Delete**.</span></span>
5. <span data-ttu-id="a06e1-136">Confirme que desea eliminar el contrato seleccionado.</span><span class="sxs-lookup"><span data-stu-id="a06e1-136">Confirm that you want to delete the selected agreement.</span></span>

    <span data-ttu-id="a06e1-137">La hoja de contratos ya no muestra el contrato que se eliminó.</span><span class="sxs-lookup"><span data-stu-id="a06e1-137">The Agreements blade no longer shows the deleted agreement.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a06e1-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a06e1-138">Next steps</span></span>
* [<span data-ttu-id="a06e1-139">Creación de un contrato AS2</span><span class="sxs-lookup"><span data-stu-id="a06e1-139">Create an AS2 agreement</span></span>](logic-apps-enterprise-integration-as2.md)
