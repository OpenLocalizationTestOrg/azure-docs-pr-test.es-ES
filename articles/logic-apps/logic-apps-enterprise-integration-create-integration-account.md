---
title: "Creación, vinculación, eliminación o movimiento de una cuenta de integración en Azure Logic Apps | Microsoft Docs"
description: "Creación de una cuenta de integración y vinculación de la misma a Logic Apps"
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
ms.openlocfilehash: 716e7b5bab8725dea0fd2b760d0e46e8e892c5b4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-an-integration-account"></a><span data-ttu-id="1a219-103">¿Qué es una cuenta de integración?</span><span class="sxs-lookup"><span data-stu-id="1a219-103">What is an integration account?</span></span>

<span data-ttu-id="1a219-104">Una cuenta de integración permite a las aplicaciones de integración empresarial administrar artefactos, incluidos esquemas, asignaciones, certificados, asociados y contratos.</span><span class="sxs-lookup"><span data-stu-id="1a219-104">An integration account allows enterprise integration apps to manage artifacts, including schemas, maps, certificates, partners and agreements.</span></span> <span data-ttu-id="1a219-105">Cualquier aplicación de integración que se crea, utiliza una cuenta de integración para tener acceso a estos esquemas, mapas, certificados, etc.</span><span class="sxs-lookup"><span data-stu-id="1a219-105">Any integration app you create uses an integration account to access these schemas, maps, certificates, and so on.</span></span>

## <a name="create-an-integration-account"></a><span data-ttu-id="1a219-106">Creación de una cuenta de integración</span><span class="sxs-lookup"><span data-stu-id="1a219-106">Create an integration account</span></span>

1.  <span data-ttu-id="1a219-107">Inicie sesión en [Azure Portal](http://portal.azure.com "Azure Portal").</span><span class="sxs-lookup"><span data-stu-id="1a219-107">Sign in to the [Azure portal](http://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="1a219-108">En el menú izquierdo, seleccione **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="1a219-108">From the left menu, select **More services**.</span></span>

    ![Selección de "Más servicios"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="1a219-110">En el cuadro de búsqueda, escriba "integración" como filtro.</span><span class="sxs-lookup"><span data-stu-id="1a219-110">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="1a219-111">En la lista de resultados, seleccione **Cuentas de integración**.</span><span class="sxs-lookup"><span data-stu-id="1a219-111">In the results list, select **Integration Accounts**.</span></span>

    ![Filtre por "integración", seleccione "Cuentas de integración"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="1a219-113">En la parte superior de la página, elija **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="1a219-113">At the top of the page, choose **Add**.</span></span>

    ![Elección de Agregar](./media/logic-apps-enterprise-integration-accounts/account-3.png)

4. <span data-ttu-id="1a219-115">Dele un nombre a la cuenta de integración y seleccione la suscripción de Azure que desee utilizar.</span><span class="sxs-lookup"><span data-stu-id="1a219-115">Name your integration account and select the Azure subscription that you want to use.</span></span> <span data-ttu-id="1a219-116">Puede crear un **Grupo de recursos** nuevo o seleccionar uno existente.</span><span class="sxs-lookup"><span data-stu-id="1a219-116">You can either create a new **Resource group** or select an existing resource group.</span></span> <span data-ttu-id="1a219-117">A continuación, seleccione la **Ubicación** para hospedar la cuenta de integración y el **Plan de tarifa**.</span><span class="sxs-lookup"><span data-stu-id="1a219-117">Then select a **Location** for hosting your integration account and a **Pricing Tier**.</span></span> 

    <span data-ttu-id="1a219-118">Cuando esté listo, seleccione **Crear**.</span><span class="sxs-lookup"><span data-stu-id="1a219-118">When you're ready, choose **Create**.</span></span>

    ![Incorporación de los detalles de la cuenta de integración](./media/logic-apps-enterprise-integration-accounts/account-4.png)

    <span data-ttu-id="1a219-120">Azure aprovisionará la cuenta de integración en la ubicación seleccionada, lo cual tardará un minuto como mucho.</span><span class="sxs-lookup"><span data-stu-id="1a219-120">Azure provisions your integration account  in the selected location, which should complete within 1 minute.</span></span>

5. <span data-ttu-id="1a219-121">Actualice la página.</span><span class="sxs-lookup"><span data-stu-id="1a219-121">Refresh the page.</span></span> <span data-ttu-id="1a219-122">Verá la nueva cuenta de integración aparecer en la lista.</span><span class="sxs-lookup"><span data-stu-id="1a219-122">You see your new integration account listed.</span></span>

    ![La nueva cuenta de integración aparece en la lista](./media/logic-apps-enterprise-integration-accounts/account-5.png) 

<span data-ttu-id="1a219-124">A continuación, vincule la cuenta de integración que acaba de crear a la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="1a219-124">Next, link the integration account that you created to your logic app.</span></span> 

## <a name="link-an-integration-account-to-a-logic-app"></a><span data-ttu-id="1a219-125">Vinculación de una cuenta de integración a una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="1a219-125">Link an integration account to a logic app</span></span>

<span data-ttu-id="1a219-126">Para que las aplicaciones lógicas puedan acceder a las asignaciones, los esquemas, los contratos y otros artefactos de la cuenta de integración, vincule esta última a la aplicación lógica.</span><span class="sxs-lookup"><span data-stu-id="1a219-126">To give your logic apps access to maps, schemas, agreements, and other artifacts in your integration account, link the integration account to your logic app.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="1a219-127">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="1a219-127">Prerequisites</span></span>

* <span data-ttu-id="1a219-128">Tener una cuenta de integración</span><span class="sxs-lookup"><span data-stu-id="1a219-128">An integration account</span></span>
* <span data-ttu-id="1a219-129">Tener una aplicación lógica</span><span class="sxs-lookup"><span data-stu-id="1a219-129">A logic app</span></span>

> [!NOTE] 
> <span data-ttu-id="1a219-130">Antes de empezar, asegúrese de que la cuenta de integración y la aplicación lógica se encuentran en la *misma ubicación de Azure*.</span><span class="sxs-lookup"><span data-stu-id="1a219-130">Make sure your integration account and logic app are in the *same Azure location* before you begin.</span></span>


1. <span data-ttu-id="1a219-131">En Azure Portal, seleccione la aplicación lógica y compruebe su ubicación.</span><span class="sxs-lookup"><span data-stu-id="1a219-131">In the Azure portal, select your logic app, and check your logic app's location.</span></span>

    ![Selección de la aplicación lógica y comprobación de la ubicación](./media/logic-apps-enterprise-integration-accounts/linkaccount-1.png)

2. <span data-ttu-id="1a219-133">En **Configuración**, seleccione **Cuenta de integración**.</span><span class="sxs-lookup"><span data-stu-id="1a219-133">Under **Settings**, select **Integration Account**.</span></span>

    ![Selección de la "Cuenta de integración"](./media/logic-apps-enterprise-integration-accounts/linkaccount-2.png)

3. <span data-ttu-id="1a219-135">Seleccione la cuenta de integración que desee vincular a la aplicación de la lista **Seleccione una cuenta de integración**.</span><span class="sxs-lookup"><span data-stu-id="1a219-135">From the **Select an Integration account** list, select the integration account you want to link to your logic app.</span></span> <span data-ttu-id="1a219-136">Para terminar de vinculación, elija **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="1a219-136">To finish linking, choose **Save**.</span></span>

    ![Selección de la cuenta de integración](./media/logic-apps-enterprise-integration-accounts/linkaccount-3.png)

    <span data-ttu-id="1a219-138">Recibirá una notificación de la vinculación de la cuenta de integración a la aplicación lógica y de que esta tiene ahora todos los artefactos de la cuenta de integración disponibles.</span><span class="sxs-lookup"><span data-stu-id="1a219-138">You get a notification that shows your integration account is linked to your logic app,  and that all artifacts in your integration account are now available to your logic app.</span></span>

    ![Aplicación lógica vinculada a la cuenta de integración](./media/logic-apps-enterprise-integration-accounts/linkaccount-5.png)

<span data-ttu-id="1a219-140">Ahora que la cuenta de integración está vinculada a la aplicación lógica, puede usar los conectores de B2B en las aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="1a219-140">Now that your integration account is linked to your logic app, you can use the B2B connectors in your logic apps.</span></span> <span data-ttu-id="1a219-141">Algunos conectores de B2B comunes incluyen validación XML, y codificación y descodificación de archivos planos.</span><span class="sxs-lookup"><span data-stu-id="1a219-141">Some common B2B connectors include XML validation and flat file encode/decode.</span></span>  

## <a name="delete-your-integration-account"></a><span data-ttu-id="1a219-142">Eliminación de la cuenta de integración</span><span class="sxs-lookup"><span data-stu-id="1a219-142">Delete your integration account</span></span>

1. <span data-ttu-id="1a219-143">Seleccione **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="1a219-143">Select **More services**.</span></span>

    ![Selección de "Más servicios"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="1a219-145">En el cuadro de búsqueda, escriba "integración" como filtro.</span><span class="sxs-lookup"><span data-stu-id="1a219-145">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="1a219-146">En la lista de resultados, seleccione **Cuentas de integración**.</span><span class="sxs-lookup"><span data-stu-id="1a219-146">In the results list, select **Integration Accounts**.</span></span>

    ![Filtre por "integración", seleccione "Cuentas de integración"](./media/logic-apps-enterprise-integration-accounts/account-2.png)  

3. <span data-ttu-id="1a219-148">Seleccione la cuenta de integración que desee eliminar.</span><span class="sxs-lookup"><span data-stu-id="1a219-148">Select the integration account that you want to delete.</span></span>

    ![Selección de la cuenta de integración que se va a eliminar](./media/logic-apps-enterprise-integration-accounts/account-5.png)

4. <span data-ttu-id="1a219-150">En el menú, elija **Eliminar**.</span><span class="sxs-lookup"><span data-stu-id="1a219-150">On the menu, choose **Delete**.</span></span>

    ![Selección de "Eliminar"](./media/logic-apps-enterprise-integration-accounts/delete.png)

5. <span data-ttu-id="1a219-152">Confirme que desea eliminar la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="1a219-152">Confirm your choice to delete the integration account.</span></span>

## <a name="move-your-integration-account"></a><span data-ttu-id="1a219-153">Movimiento de la cuenta de integración</span><span class="sxs-lookup"><span data-stu-id="1a219-153">Move your integration account</span></span>

<span data-ttu-id="1a219-154">Para mover una cuenta de integración a otro grupo de recursos o suscripción de Azure, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="1a219-154">To move an integration account to another Azure subscription or resource group, follow these steps.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a219-155">Después de mover una cuenta de integración tiene que actualizar todos los scripts para utilizar los nuevos identificadores de recurso.</span><span class="sxs-lookup"><span data-stu-id="1a219-155">You must update all scripts to use the new resource IDs after you move an integration account.</span></span>

1. <span data-ttu-id="1a219-156">Seleccione **Más servicios**.</span><span class="sxs-lookup"><span data-stu-id="1a219-156">Select **More services**.</span></span>

    ![Selección de "Más servicios"](./media/logic-apps-enterprise-integration-accounts/account-1.png)

2. <span data-ttu-id="1a219-158">En el cuadro de búsqueda, escriba "integración" como filtro.</span><span class="sxs-lookup"><span data-stu-id="1a219-158">In the search box, type "integration" for your filter.</span></span> <span data-ttu-id="1a219-159">En la lista de resultados, seleccione **Cuentas de integración**.</span><span class="sxs-lookup"><span data-stu-id="1a219-159">In the results list, select **Integration Accounts**.</span></span>

    ![Filtre por "integración", seleccione "Cuentas de integración"](./media/logic-apps-enterprise-integration-accounts/account-2.png)

3. <span data-ttu-id="1a219-161">Seleccione la cuenta de integración que desee mover.</span><span class="sxs-lookup"><span data-stu-id="1a219-161">Select the integration account that you want to move.</span></span> <span data-ttu-id="1a219-162">En **Configuración**, elija **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="1a219-162">Under **Settings**, choose **Properties**.</span></span>

    ![Seleccione de la cuenta de integración que va a mover.](./media/logic-apps-enterprise-integration-accounts/move.png)

5. <span data-ttu-id="1a219-165">Cambie el grupo de recursos o la suscripción de Azure asociados a la cuenta de integración.</span><span class="sxs-lookup"><span data-stu-id="1a219-165">Change the resource group or Azure subscription that's associated with your integration account.</span></span>

    ![Elija Cambiar el grupo de recursos o Cambiar suscripción](./media/logic-apps-enterprise-integration-accounts/move-2.png)

## <a name="next-steps"></a><span data-ttu-id="1a219-167">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="1a219-167">Next Steps</span></span>
* [<span data-ttu-id="1a219-168">Más información sobre los contratos</span><span class="sxs-lookup"><span data-stu-id="1a219-168">Learn more about agreements</span></span>](../logic-apps/logic-apps-enterprise-integration-agreements.md "Información sobre los contratos de integración de empresas")  

