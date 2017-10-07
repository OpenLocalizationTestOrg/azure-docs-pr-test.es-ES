---
title: "aaaCreate, link, eliminar o mover una cuenta de integración de aplicaciones lógicas de Azure | Documentos de Microsoft"
description: "¿Cómo toocreate una integración de la cuenta y vincular las aplicaciones lógicas tooyour"
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: d3ad9e99-a9ee-477b-81bf-0881e11e632f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: LADocs; mandia
ms.openlocfilehash: fda6c91723b3e3624ee176df112ba8b6c9800273
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-an-integration-account"></a><span data-ttu-id="37d98-103">¿Qué es una cuenta de integración?</span><span class="sxs-lookup"><span data-stu-id="37d98-103">What is an integration account?</span></span>

<span data-ttu-id="37d98-104">Una cuenta de integración permite a las aplicaciones de integración de enterprise toomanage artefactos, incluidos los esquemas, mapas, certificados, socios comerciales y acuerdos.</span><span class="sxs-lookup"><span data-stu-id="37d98-104">An integration account allows enterprise integration apps toomanage artifacts, including schemas, maps, certificates, partners and agreements.</span></span> <span data-ttu-id="37d98-105">Cualquier aplicación de integración que se crea usa un tooaccess de cuenta de integración estos esquemas, mapas, certificados y así sucesivamente.</span><span class="sxs-lookup"><span data-stu-id="37d98-105">Any integration app you create uses an integration account tooaccess these schemas, maps, certificates, and so on.</span></span>

## <a name="create-an-integration-account"></a><span data-ttu-id="37d98-106">Creación de una cuenta de integración</span><span class="sxs-lookup"><span data-stu-id="37d98-106">Create an integration account</span></span>

1.  <span data-ttu-id="37d98-107">Inicie sesión en toohello [portal de Azure](http://portal.azure.com "portal de Azure").</span><span class="sxs-lookup"><span data-stu-id="37d98-107">Sign in toohello [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="37d98-108">En el menú izquierdo de hello, seleccione **más servicios**.</span><span class="sxs-lookup"><span data-stu-id="37d98-108">From hello left menu, select **More services**.</span></span>

    ![Selección de "Más servicios"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="37d98-110">En el cuadro de búsqueda de hello, escriba "integración" para el filtro.</span><span class="sxs-lookup"><span data-stu-id="37d98-110">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="37d98-111">En la lista de resultados de hello, seleccione **cuentas de integración**.</span><span class="sxs-lookup"><span data-stu-id="37d98-111">In hello results list, select **Integration Accounts**.</span></span>

    ![Filtre por "integración", seleccione "Cuentas de integración"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="37d98-113">Hola parte superior de la página de hello, elija **agregar**.</span><span class="sxs-lookup"><span data-stu-id="37d98-113">At hello top of hello page, choose **Add**.</span></span>

    ![Elección de Agregar](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. <span data-ttu-id="37d98-115">Nombre de la cuenta de integración y seleccione Hola suscripción de Azure que desea toouse.</span><span class="sxs-lookup"><span data-stu-id="37d98-115">Name your integration account and select hello Azure subscription that you want toouse.</span></span> <span data-ttu-id="37d98-116">Puede crear un **Grupo de recursos** nuevo o seleccionar uno existente.</span><span class="sxs-lookup"><span data-stu-id="37d98-116">You can either create a new **Resource group** or select an existing resource group.</span></span> <span data-ttu-id="37d98-117">A continuación, seleccione la **Ubicación** para hospedar la cuenta de integración y el **Plan de tarifa**.</span><span class="sxs-lookup"><span data-stu-id="37d98-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span></span> 

    <span data-ttu-id="37d98-118">Cuando esté listo, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="37d98-118">When you're ready, choose **Create**.</span></span>

    ![Incorporación de los detalles de la cuenta de integración](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    <span data-ttu-id="37d98-120">Azure proporciona a su cuenta de integración en la ubicación de hello seleccionado, que debe completarse dentro de 1 minuto.</span><span class="sxs-lookup"><span data-stu-id="37d98-120">Azure provisions your integration account  in hello selected location, which should complete within 1 minute.</span></span>

5. <span data-ttu-id="37d98-121">Actualice la página de Hola.</span><span class="sxs-lookup"><span data-stu-id="37d98-121">Refresh hello page.</span></span> <span data-ttu-id="37d98-122">Verá la nueva cuenta de integración aparecer en la lista.</span><span class="sxs-lookup"><span data-stu-id="37d98-122">You see your new integration account listed.</span></span>

    ![La nueva cuenta de integración aparece en la lista](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

<span data-ttu-id="37d98-124">A continuación, vincular cuenta de hello de integración que se tooyour creado aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="37d98-124">Next, link hello integration account that you created tooyour logic app.</span></span> 

## <a name="link-an-integration-account-tooa-logic-app"></a><span data-ttu-id="37d98-125">Vincular una aplicación de la lógica de la cuenta tooa integración</span><span class="sxs-lookup"><span data-stu-id="37d98-125">Link an integration account tooa logic app</span></span>

<span data-ttu-id="37d98-126">toogive acceso a las aplicaciones lógicas toomaps, esquemas, contratos y otros artefactos de la cuenta de integración, aplicación de vínculo hello integración cuenta tooyour lógica.</span><span class="sxs-lookup"><span data-stu-id="37d98-126">toogive your logic apps access toomaps, schemas, agreements, and other artifacts in your integration account, link hello integration account tooyour logic app.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="37d98-127">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="37d98-127">Prerequisites</span></span>

* <span data-ttu-id="37d98-128">Tener una cuenta de integración</span><span class="sxs-lookup"><span data-stu-id="37d98-128">An integration account</span></span>
* <span data-ttu-id="37d98-129">Tener una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="37d98-129">A logic app</span></span>

> [!NOTE] 
> <span data-ttu-id="37d98-130">Asegurarse de que la aplicación de cuenta y la lógica de integración hello *indicarlo Azure* antes de empezar.</span><span class="sxs-lookup"><span data-stu-id="37d98-130">Make sure your integration account and logic app are in hello *same Azure location* before you begin.</span></span>


1. <span data-ttu-id="37d98-131">Hola portal de Azure, seleccione la aplicación lógica y compruebe la ubicación de la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="37d98-131">In hello Azure portal, select your logic app, and check your logic app's location.</span></span>

    ![Selección de la aplicación lógica y comprobación de la ubicación](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. <span data-ttu-id="37d98-133">En **Configuración**, seleccione **Cuenta de integración**.</span><span class="sxs-lookup"><span data-stu-id="37d98-133">Under **Settings**, select **Integration Account**.</span></span>

    ![Selección de la "Cuenta de integración"](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. <span data-ttu-id="37d98-135">De hello **seleccionar una cuenta de integración** enumerar, cuenta de integración de hello seleccione desea aplicación lógica de toolink tooyour.</span><span class="sxs-lookup"><span data-stu-id="37d98-135">From hello **Select an Integration account** list, select hello integration account you want toolink tooyour logic app.</span></span> <span data-ttu-id="37d98-136">Elija toofinish vincular, **guardar**.</span><span class="sxs-lookup"><span data-stu-id="37d98-136">toofinish linking, choose **Save**.</span></span>

    ![Selección de la cuenta de integración](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    <span data-ttu-id="37d98-138">Se recibe una notificación que muestra la integración de cuenta es la aplicación de la lógica de tooyour vinculado, y que todos los artefactos de la cuenta de integración están ahora disponibles tooyour aplicación de lógica.</span><span class="sxs-lookup"><span data-stu-id="37d98-138">You get a notification that shows your integration account is linked tooyour logic app,  and that all artifacts in your integration account are now available tooyour logic app.</span></span>

    ![Se vincula la aplicación lógica tooyour cuenta de integración](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

<span data-ttu-id="37d98-140">Ahora que su cuenta de integración es aplicación de lógica de tooyour vinculado, puede utilizar conectores de hello B2B en las aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="37d98-140">Now that your integration account is linked tooyour logic app, you can use hello B2B connectors in your logic apps.</span></span> <span data-ttu-id="37d98-141">Algunos conectores de B2B comunes incluyen validación XML, y codificación y descodificación de archivos planos.</span><span class="sxs-lookup"><span data-stu-id="37d98-141">Some common B2B connectors include XML validation and flat file encode/decode.</span></span>  

## <a name="delete-your-integration-account"></a><span data-ttu-id="37d98-142">Eliminación de la cuenta de integración</span><span class="sxs-lookup"><span data-stu-id="37d98-142">Delete your integration account</span></span>

1. <span data-ttu-id="37d98-143">Seleccione **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="37d98-143">Select **More services**.</span></span>

    ![Selección de "Más servicios"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="37d98-145">En el cuadro de búsqueda de hello, escriba "integración" para el filtro.</span><span class="sxs-lookup"><span data-stu-id="37d98-145">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="37d98-146">En la lista de resultados de hello, seleccione **cuentas de integración**.</span><span class="sxs-lookup"><span data-stu-id="37d98-146">In hello results list, select **Integration Accounts**.</span></span>

    ![Filtre por "integración", seleccione "Cuentas de integración"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="37d98-148">Seleccione la cuenta de integración de Hola que desea toodelete.</span><span class="sxs-lookup"><span data-stu-id="37d98-148">Select hello integration account that you want toodelete.</span></span>

    ![Seleccione toodelete de cuenta de integración](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. <span data-ttu-id="37d98-150">En el menú de hello, elija **eliminar**.</span><span class="sxs-lookup"><span data-stu-id="37d98-150">On hello menu, choose **Delete**.</span></span>

    ![Selección de "Eliminar"](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. <span data-ttu-id="37d98-152">Confirmar la cuenta de integración de hello toodelete choice.</span><span class="sxs-lookup"><span data-stu-id="37d98-152">Confirm your choice toodelete hello integration account.</span></span>

## <a name="move-your-integration-account"></a><span data-ttu-id="37d98-153">Movimiento de la cuenta de integración</span><span class="sxs-lookup"><span data-stu-id="37d98-153">Move your integration account</span></span>

<span data-ttu-id="37d98-154">toomove un tooanother de cuenta de integración Azure suscripción o grupo de recursos, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="37d98-154">toomove an integration account tooanother Azure subscription or resource group, follow these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37d98-155">Debe actualizar todas las secuencias de comandos toouse Hola nuevos identificadores de recursos después de mover una cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="37d98-155">You must update all scripts toouse hello new resource IDs after you move an integration account.</span></span>

1. <span data-ttu-id="37d98-156">Seleccione **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="37d98-156">Select **More services**.</span></span>

    ![Selección de "Más servicios"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="37d98-158">En el cuadro de búsqueda de hello, escriba "integración" para el filtro.</span><span class="sxs-lookup"><span data-stu-id="37d98-158">In hello search box, type "integration" for your filter.</span></span> <span data-ttu-id="37d98-159">En la lista de resultados de hello, seleccione **cuentas de integración**.</span><span class="sxs-lookup"><span data-stu-id="37d98-159">In hello results list, select **Integration Accounts**.</span></span>

    ![Filtre por "integración", seleccione "Cuentas de integración"](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. <span data-ttu-id="37d98-161">Seleccione la cuenta de integración de Hola que desea toomove.</span><span class="sxs-lookup"><span data-stu-id="37d98-161">Select hello integration account that you want toomove.</span></span> <span data-ttu-id="37d98-162">En **Configuración**, elija **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="37d98-162">Under **Settings**, choose **Properties**.</span></span>

    ![Seleccione toomove de cuenta de integración.](./media/logic-apps-enterprise-integration-accounts/move.png)

5. <span data-ttu-id="37d98-165">Cambiar el grupo de recursos de Hola o suscripción de Azure que esté asociada con su cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="37d98-165">Change hello resource group or Azure subscription that's associated with your integration account.</span></span>

    ![Elija Cambiar el grupo de recursos o Cambiar suscripción](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a><span data-ttu-id="37d98-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="37d98-167">Next Steps</span></span>
* [<span data-ttu-id="37d98-168">Más información sobre los contratos</span><span class="sxs-lookup"><span data-stu-id="37d98-168">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Información sobre los contratos de integración de empresas")  

