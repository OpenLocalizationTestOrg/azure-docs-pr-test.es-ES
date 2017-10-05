---
title: "Implementación de SAP S/4 HANA o BW/4 HANA en una máquina virtual de Azure | Microsoft Docs"
description: "Implementación de SAP S/4HANA o BW/4HANA en una máquina virtual de Azure"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 4788fa14a6c49d39b5a3096a69b6738f4a5d8cca
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a><span data-ttu-id="59bae-103">Implementación de SAP S/4HANA o BW/4HANA en Azure</span><span class="sxs-lookup"><span data-stu-id="59bae-103">Deploy SAP S/4HANA or BW/4HANA on Azure</span></span>
<span data-ttu-id="59bae-104">En este artículo se describe cómo implementar S/4HANA en Azure por medio de SAP Cloud Appliance Library (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="59bae-104">This article describes how to deploy S/4HANA on Azure by using the SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="59bae-105">Para implementar otras soluciones basadas en SAP HANA, por ejemplo, BW/4HANA, siga los mismos pasos.</span><span class="sxs-lookup"><span data-stu-id="59bae-105">To deploy other SAP HANA-based solutions, such as BW/4HANA, follow the same steps.</span></span>

> [!NOTE]
<span data-ttu-id="59bae-106">Para más información sobre SAP CAL, vaya al sitio web de [SAP Cloud Appliance Library](https://cal.sap.com/).</span><span class="sxs-lookup"><span data-stu-id="59bae-106">For more information about the SAP CAL, go to the [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="59bae-107">SAP también tiene un blog acerca de [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="59bae-107">SAP also has a blog about the [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span>

> [!NOTE]
<span data-ttu-id="59bae-108">A partir del 29 de mayo de 2017 puede usar el modelo de implementación mediante Azure Resource Manager, además del modelo de implementación clásico, que se usa menos, para implementar SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="59bae-108">As of May 29, 2017, you can use the Azure Resource Manager deployment model in addition to the less-preferred classic deployment model to deploy the SAP CAL.</span></span> <span data-ttu-id="59bae-109">Se recomienda usar el nuevo modelo de implementación mediante Resource Manager, en lugar del modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="59bae-109">We recommend that you use the new Resource Manager deployment model and disregard the classic deployment model.</span></span>

## <a name="step-by-step-process-to-deploy-the-solution"></a><span data-ttu-id="59bae-110">Proceso paso a paso para implementar la solución</span><span class="sxs-lookup"><span data-stu-id="59bae-110">Step-by-step process to deploy the solution</span></span>

<span data-ttu-id="59bae-111">La siguiente secuencia de capturas de pantalla muestra cómo implementar S/4HANA en Azure mediante la solución SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="59bae-111">The following sequence of screenshots shows you how to deploy S/4HANA on Azure by using the SAP CAL.</span></span> <span data-ttu-id="59bae-112">El proceso funciona del mismo modo para otras soluciones como BW/4HANA.</span><span class="sxs-lookup"><span data-stu-id="59bae-112">The process works the same way for other solutions, such as BW/4HANA.</span></span>

<span data-ttu-id="59bae-113">La página **Soluciones** muestra algunas de las soluciones basadas en SAP CAL HANA disponibles en Azure.</span><span class="sxs-lookup"><span data-stu-id="59bae-113">The **Solutions** page shows some of the SAP CAL HANA-based solutions available on Azure.</span></span> <span data-ttu-id="59bae-114">**SAP S/4HANA 1610 FPS01, aplicación completamente activada** está en la fila central:</span><span class="sxs-lookup"><span data-stu-id="59bae-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Appliance** is in the middle row:</span></span>

![Soluciones de SAP CAL](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-the-sap-cal"></a><span data-ttu-id="59bae-116">Creación de una cuenta en SAP CAL</span><span class="sxs-lookup"><span data-stu-id="59bae-116">Create an account in the SAP CAL</span></span>
1. <span data-ttu-id="59bae-117">La primera vez que inicie sesión en SAP CAL, utilice S-User de SAP, o cualquier otro usuario registrado de SAP.</span><span class="sxs-lookup"><span data-stu-id="59bae-117">To sign in to the SAP CAL for the first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="59bae-118">A continuación, defina una cuenta de SAP CAL que SAP CAL use para implementar aplicaciones en Azure.</span><span class="sxs-lookup"><span data-stu-id="59bae-118">Then define an SAP CAL account that is used by the SAP CAL to deploy appliances on Azure.</span></span> <span data-ttu-id="59bae-119">En la definición de la cuenta, debe:</span><span class="sxs-lookup"><span data-stu-id="59bae-119">In the account definition, you need to:</span></span>

    <span data-ttu-id="59bae-120">a.</span><span class="sxs-lookup"><span data-stu-id="59bae-120">a.</span></span> <span data-ttu-id="59bae-121">Seleccione el modelo de implementación en Azure (Resource Manager o clásico).</span><span class="sxs-lookup"><span data-stu-id="59bae-121">Select the deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="59bae-122">b.</span><span class="sxs-lookup"><span data-stu-id="59bae-122">b.</span></span> <span data-ttu-id="59bae-123">Especifique la suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="59bae-123">Enter your Azure subscription.</span></span> <span data-ttu-id="59bae-124">Una cuenta de SAP CAL no se puede asignar a más de una suscripción.</span><span class="sxs-lookup"><span data-stu-id="59bae-124">An SAP CAL account can be assigned to one subscription only.</span></span> <span data-ttu-id="59bae-125">Si necesita más de una suscripción, debe crear otra cuenta de SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="59bae-125">If you need more than one subscription, you need to create another SAP CAL account.</span></span>

    <span data-ttu-id="59bae-126">c.</span><span class="sxs-lookup"><span data-stu-id="59bae-126">c.</span></span> <span data-ttu-id="59bae-127">Conceda el permiso de SAP CAL para realizar la implementación en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="59bae-127">Give the SAP CAL permission to deploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="59bae-128">Los pasos siguientes muestran cómo crear una cuenta de SAP CAL para las implementaciones mediante Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="59bae-128">The next steps show how to create an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="59bae-129">Si ya tiene una cuenta de SAP CAL vinculada al modelo de implementación clásico, *tendrá que* seguir estos pasos para crear una cuenta de SAP CAL nueva.</span><span class="sxs-lookup"><span data-stu-id="59bae-129">If you already have an SAP CAL account that is linked to the classic deployment model, you *need* to follow these steps to create a new SAP CAL account.</span></span> <span data-ttu-id="59bae-130">La nueva cuenta de SAP CAL se tiene que implementar mediante el modelo de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="59bae-130">The new SAP CAL account needs to deploy in the Resource Manager model.</span></span>

2. <span data-ttu-id="59bae-131">Cree una nueva cuenta de SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="59bae-131">Create a new SAP CAL account.</span></span> <span data-ttu-id="59bae-132">La página **Cuentas** muestra tres opciones de Azure:</span><span class="sxs-lookup"><span data-stu-id="59bae-132">The **Accounts** page shows three choices for Azure:</span></span> 

    <span data-ttu-id="59bae-133">a.</span><span class="sxs-lookup"><span data-stu-id="59bae-133">a.</span></span> <span data-ttu-id="59bae-134">**Microsoft Azure (classic)** es el modelo de implementación clásico y ya no se suele usar.</span><span class="sxs-lookup"><span data-stu-id="59bae-134">**Microsoft Azure (classic)** is the classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="59bae-135">b.</span><span class="sxs-lookup"><span data-stu-id="59bae-135">b.</span></span> <span data-ttu-id="59bae-136">**Microsoft Azure** es el nuevo modelo de implementación mediante Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="59bae-136">**Microsoft Azure** is the new Resource Manager deployment model.</span></span>

    <span data-ttu-id="59bae-137">c.</span><span class="sxs-lookup"><span data-stu-id="59bae-137">c.</span></span> <span data-ttu-id="59bae-138">**Windows Azure operado por 21Vianet** es una opción en China que usa el modelo de implementación clásica.</span><span class="sxs-lookup"><span data-stu-id="59bae-138">**Windows Azure operated by 21Vianet** is an option in China that uses the classic deployment model.</span></span>

    <span data-ttu-id="59bae-139">Para implementar mediante el modelo de Resource Manager, seleccione **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="59bae-139">To deploy in the Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Detalles de la cuenta de SAP CAL](./media/cal-s4h/s4h-pic-2a.png)

3. <span data-ttu-id="59bae-141">En el campo **Suscription ID**, especifique el identificador de suscripción de Azure, que se puede encontrar en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="59bae-141">Enter the Azure **Subscription ID** that can be found on the Azure portal.</span></span>

   ![Cuentas de SAP CAL](./media/cal-s4h/s4h-pic3c.png)

4. <span data-ttu-id="59bae-143">Para autorizar que SAP CAL se implemente en la suscripción de Azure que ha definido, haga clic en **Authorize** (Autorizar).</span><span class="sxs-lookup"><span data-stu-id="59bae-143">To authorize the SAP CAL to deploy into the Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="59bae-144">La siguiente página aparecerá en la pestaña del explorador:</span><span class="sxs-lookup"><span data-stu-id="59bae-144">The following page appears in the browser tab:</span></span>

   ![Inicio de sesión de servicios en la nube de Internet Explorer](./media/cal-s4h/s4h-pic4c.png)

5. <span data-ttu-id="59bae-146">Si se enumera más de un usuario, elija la cuenta de Microsoft vinculada para ser el coadministrador de la suscripción de Azure que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="59bae-146">If more than one user is listed, choose the Microsoft account that is linked to be the coadministrator of the Azure subscription you selected.</span></span> <span data-ttu-id="59bae-147">La siguiente página aparecerá en la pestaña del explorador:</span><span class="sxs-lookup"><span data-stu-id="59bae-147">The following page appears in the browser tab:</span></span>

   ![Confirmación de servicios en la nube de Internet Explorer](./media/cal-s4h/s4h-pic5a.png)

6. <span data-ttu-id="59bae-149">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="59bae-149">Click **Accept**.</span></span> <span data-ttu-id="59bae-150">Si la autorización es correcta, vuelve a mostrarse la definición de la cuenta de SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="59bae-150">If the authorization is successful, the SAP CAL account definition displays again.</span></span> <span data-ttu-id="59bae-151">Poco después, un mensaje confirma que el proceso de autorización se ha realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="59bae-151">After a short time, a message confirms that the authorization process was successful.</span></span>

7. <span data-ttu-id="59bae-152">Para asignar la cuenta de SAP CAL recién creada al usuario, escriba en el cuadro de texto de la derecha su **identificador de usuario** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="59bae-152">To assign the newly created SAP CAL account to your user, enter your **User ID** in the text box on the right and click **Add**.</span></span>

   ![Asociación de cuenta a usuario](./media/cal-s4h/s4h-pic8a.png)

8. <span data-ttu-id="59bae-154">Para asociar una cuenta con el usuario que utiliza para iniciar sesión en SAP CAL, haga clic en **Review** (Revisar).</span><span class="sxs-lookup"><span data-stu-id="59bae-154">To associate your account with the user that you use to sign in to the SAP CAL, click **Review**.</span></span> 
 
9. <span data-ttu-id="59bae-155">Para crear la asociación entre el usuario y la cuenta de SAP CAL recién creada, haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="59bae-155">To create the association between your user and the newly created SAP CAL account, click **Create**.</span></span>

   ![Asociación de usuario a cuenta de SAP CAL](./media/cal-s4h/s4h-pic9b.png)

<span data-ttu-id="59bae-157">Ha creado correctamente una cuenta de SAP CAL que puede:</span><span class="sxs-lookup"><span data-stu-id="59bae-157">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="59bae-158">Usar el modelo de implementación mediante Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="59bae-158">Use the Resource Manager deployment model.</span></span>
- <span data-ttu-id="59bae-159">Implementar sistemas de SAP en su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="59bae-159">Deploy SAP systems into your Azure subscription.</span></span>

<span data-ttu-id="59bae-160">Ya puede empezar a implementar S/4HANA en su suscripción de usuario en Azure.</span><span class="sxs-lookup"><span data-stu-id="59bae-160">Now you can start to deploy S/4HANA into your user subscription in Azure.</span></span>

> [!NOTE]
<span data-ttu-id="59bae-161">Antes de continuar, determine si dispone de cuotas de núcleos de Azure para máquinas virtuales de la serie H de Azure.</span><span class="sxs-lookup"><span data-stu-id="59bae-161">Before you continue, determine whether you have Azure core quotas for Azure H-Series VMs.</span></span> <span data-ttu-id="59bae-162">En este momento, SAP CAL usa máquinas virtuales de la serie H de Azure para implementar algunas de las soluciones basadas en SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="59bae-162">At the moment, the SAP CAL uses H-Series VMs of Azure to deploy some of the SAP HANA-based solutions.</span></span> <span data-ttu-id="59bae-163">Su suscripción de Azure podría no tener ninguna cuota de núcleos para la serie H.</span><span class="sxs-lookup"><span data-stu-id="59bae-163">Your Azure subscription might not have any H-Series core quotas for H-Series.</span></span> <span data-ttu-id="59bae-164">Si es así, tendrá que ponerse en contacto con el soporte técnico de Azure para obtener una cuota de al menos 16 núcleos de la serie H.</span><span class="sxs-lookup"><span data-stu-id="59bae-164">If so, you might need to contact Azure support to get a quota of at least 16 H-Series cores.</span></span>

> [!NOTE]
<span data-ttu-id="59bae-165">Al implementar una solución de Azure en SAP CAL, es posible que solo pueda elegir una región de Azure.</span><span class="sxs-lookup"><span data-stu-id="59bae-165">When you deploy a solution on Azure in the SAP CAL, you might find that you can choose only one Azure region.</span></span> <span data-ttu-id="59bae-166">Para implementar en otras regiones de Azure distintas a la que sugiere SAP CAL, debe adquirir una suscripción de CAL desde SAP.</span><span class="sxs-lookup"><span data-stu-id="59bae-166">To deploy into Azure regions other than the one suggested by the SAP CAL, you need to purchase a CAL subscription from SAP.</span></span> <span data-ttu-id="59bae-167">Es posible que también necesite abrir un mensaje con SAP para habilitar su cuenta de CAL para entregar en regiones de Azure distintas de las que se sugirieron inicialmente.</span><span class="sxs-lookup"><span data-stu-id="59bae-167">You also might need to open a message with SAP to have your CAL account enabled to deliver into Azure regions other than the ones initially suggested.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="59bae-168">Implementación de una solución</span><span class="sxs-lookup"><span data-stu-id="59bae-168">Deploy a solution</span></span>

<span data-ttu-id="59bae-169">Vamos a implementar una solución desde la página **Soluciones** de SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="59bae-169">Let's deploy a solution from the **Solutions** page of the SAP CAL.</span></span> <span data-ttu-id="59bae-170">SAP CAL tiene dos secuencias para implementar:</span><span class="sxs-lookup"><span data-stu-id="59bae-170">The SAP CAL has two sequences to deploy:</span></span>

- <span data-ttu-id="59bae-171">Una secuencia básica que utiliza una página para definir el sistema que se va a implementar</span><span class="sxs-lookup"><span data-stu-id="59bae-171">A basic sequence that uses one page to define the system to be deployed</span></span>
- <span data-ttu-id="59bae-172">Una secuencia avanzada que le ofrece varias opciones en relación al tamaño de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="59bae-172">An advanced sequence that gives you certain choices on VM sizes</span></span> 

<span data-ttu-id="59bae-173">Aquí se muestra la ruta de acceso básica a la implementación.</span><span class="sxs-lookup"><span data-stu-id="59bae-173">We demonstrate the basic path to deployment here.</span></span>

1. <span data-ttu-id="59bae-174">En la página **Detalles de la cuenta**, debe:</span><span class="sxs-lookup"><span data-stu-id="59bae-174">On the **Account Details** page, you need to:</span></span>

    <span data-ttu-id="59bae-175">a.</span><span class="sxs-lookup"><span data-stu-id="59bae-175">a.</span></span> <span data-ttu-id="59bae-176">Seleccionar una cuenta de SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="59bae-176">Select an SAP CAL account.</span></span> <span data-ttu-id="59bae-177">(Utilice una cuenta asociada para implementar con el modelo de implementación de Resource Manager).</span><span class="sxs-lookup"><span data-stu-id="59bae-177">(Use an account that is associated to deploy with the Resource Manager deployment model.)</span></span>

    <span data-ttu-id="59bae-178">b.</span><span class="sxs-lookup"><span data-stu-id="59bae-178">b.</span></span> <span data-ttu-id="59bae-179">Especificar en **Name** el nombre de la instancia.</span><span class="sxs-lookup"><span data-stu-id="59bae-179">Enter an instance **Name**.</span></span>

    <span data-ttu-id="59bae-180">c.</span><span class="sxs-lookup"><span data-stu-id="59bae-180">c.</span></span> <span data-ttu-id="59bae-181">Seleccionar una **región** de Azure.</span><span class="sxs-lookup"><span data-stu-id="59bae-181">Select an Azure **Region**.</span></span> <span data-ttu-id="59bae-182">SAP CAL sugiere una región.</span><span class="sxs-lookup"><span data-stu-id="59bae-182">The SAP CAL suggests a region.</span></span> <span data-ttu-id="59bae-183">Si necesita otra región de Azure y no tiene una suscripción de SAP CAL, deberá solicitar una suscripción de CAL con SAP.</span><span class="sxs-lookup"><span data-stu-id="59bae-183">If you need another Azure region and you don't have an SAP CAL subscription, you need to order a CAL subscription with SAP.</span></span>

    <span data-ttu-id="59bae-184">d.</span><span class="sxs-lookup"><span data-stu-id="59bae-184">d.</span></span> <span data-ttu-id="59bae-185">Escriba una **contraseña** maestra para la solución que contenga ocho o nueve caracteres.</span><span class="sxs-lookup"><span data-stu-id="59bae-185">Enter a master **Password** for the solution of eight or nine characters.</span></span> <span data-ttu-id="59bae-186">La contraseña se usa para los administradores de los distintos componentes.</span><span class="sxs-lookup"><span data-stu-id="59bae-186">The password is used for the administrators of the different components.</span></span>

   ![SAP CAL, Modo básico: crear instancia](./media/cal-s4h/s4h-pic10a.png)

2. <span data-ttu-id="59bae-188">Haga clic en **Crear** y, en el cuadro de mensaje que aparece, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="59bae-188">Click **Create**, and in the message box that appears, click **OK**.</span></span>

   ![Tamaños de máquinas virtuales que admite SAP CAL](./media/cal-s4h/s4h-pic10b.png)

3. <span data-ttu-id="59bae-190">En el cuadro de diálogo **Clave privada**, haga clic en **Almacenar** para almacenar la clave privada en SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="59bae-190">In the **Private Key** dialog box, click **Store** to store the private key in the SAP CAL.</span></span> <span data-ttu-id="59bae-191">Para usar la protección con contraseña para la clave privada, haga clic en **Descargar**.</span><span class="sxs-lookup"><span data-stu-id="59bae-191">To use password protection for the private key, click **Download**.</span></span> 

   ![Clave privada de SAP CAL](./media/cal-s4h/s4h-pic10c.png)

4. <span data-ttu-id="59bae-193">Lea el mensaje de **advertencia** de SAP CAL y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="59bae-193">Read the SAP CAL **Warning** message, and click **OK**.</span></span>

   ![Advertencia de SAP CAL](./media/cal-s4h/s4h-pic10d.png)

    <span data-ttu-id="59bae-195">Ahora se realizará la implementación.</span><span class="sxs-lookup"><span data-stu-id="59bae-195">Now the deployment takes place.</span></span> <span data-ttu-id="59bae-196">Después de un tiempo, y en función del tamaño y la complejidad de la solución (SAP CAL ofrece una estimación), el estado pasa a mostrarse como activo y listo para usarse.</span><span class="sxs-lookup"><span data-stu-id="59bae-196">After some time, depending on the size and complexity of the solution (the SAP CAL provides an estimate), the status is shown as active and ready for use.</span></span>

5. <span data-ttu-id="59bae-197">Para buscar las máquinas virtuales que se recopilan con los demás recursos asociados de un grupo de recursos, vaya a Azure Portal:</span><span class="sxs-lookup"><span data-stu-id="59bae-197">To find the virtual machines collected with the other associated resources in one resource group, go to the Azure portal:</span></span> 

   ![Objetos de SAP CAL implementados en el nuevo portal](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. <span data-ttu-id="59bae-199">En el portal de SAP CAL, el estado aparece como **Activo**.</span><span class="sxs-lookup"><span data-stu-id="59bae-199">On the SAP CAL portal, the status appears as **Active**.</span></span> <span data-ttu-id="59bae-200">Para conectarse a la solución, haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="59bae-200">To connect to the solution, click **Connect**.</span></span> <span data-ttu-id="59bae-201">Se implementan diferentes opciones para conectarse a los distintos componentes en esta solución.</span><span class="sxs-lookup"><span data-stu-id="59bae-201">Different options to connect to the different components are deployed within this solution.</span></span>

   ![Instancias de SAP CAL](./media/cal-s4h/active_solution.png)

7. <span data-ttu-id="59bae-203">Para poder usar una de las opciones para conectarse a los sistemas implementados, haga clic en **Guía de introducción**.</span><span class="sxs-lookup"><span data-stu-id="59bae-203">Before you can use one of the options to connect to the deployed systems, click **Getting Started Guide**.</span></span> 

   ![Conectarse a la instancia](./media/cal-s4h/connect_to_solution.png)

    <span data-ttu-id="59bae-205">La documentación asigna los nombres de los usuarios en cada uno de los métodos de conectividad.</span><span class="sxs-lookup"><span data-stu-id="59bae-205">The documentation names the users for each of the connectivity methods.</span></span> <span data-ttu-id="59bae-206">Las contraseñas de dichos usuarios se establecen en la contraseña maestra que se definió al comienzo del proceso de implementación.</span><span class="sxs-lookup"><span data-stu-id="59bae-206">The passwords for those users are set to the master password you defined at the beginning of the deployment process.</span></span> <span data-ttu-id="59bae-207">En la documentación, otros usuarios más funcionales se enumeran junto con sus contraseñas, que se pueden usar para iniciar sesión en el sistema implementado.</span><span class="sxs-lookup"><span data-stu-id="59bae-207">In the documentation, other more functional users are listed with their passwords, which you can use to sign in to the deployed system.</span></span> 

    <span data-ttu-id="59bae-208">Por ejemplo, si utiliza la GUI de SAP que está preinstalada en la máquina del Escritorio remoto de Windows, puede que el sistema S/4 sea parecido al siguiente:</span><span class="sxs-lookup"><span data-stu-id="59bae-208">For example, if you use the SAP GUI that's preinstalled on the Windows Remote Desktop machine, the S/4 system might look like this:</span></span>

   ![SM50 en la GUI de SAP preinstalada](./media/cal-s4h/gui_sm50.png)

    <span data-ttu-id="59bae-210">O bien, si utiliza DBACockpit, puede que la instancia se parezca a la siguiente:</span><span class="sxs-lookup"><span data-stu-id="59bae-210">Or if you use the DBACockpit, the instance might look like this:</span></span>

   ![SM50 en la GUI de SAP de DBACockpit](./media/cal-s4h/dbacockpit.png)

<span data-ttu-id="59bae-212">En unas horas, una aplicación SAP S/4 correcta se implementa en Azure.</span><span class="sxs-lookup"><span data-stu-id="59bae-212">Within a few hours, a healthy SAP S/4 appliance is deployed in Azure.</span></span>

<span data-ttu-id="59bae-213">Si ha adquirido una suscripción a SAP CAL, SAP admite totalmente implementaciones a través de SAP CAL en Azure.</span><span class="sxs-lookup"><span data-stu-id="59bae-213">If you bought an SAP CAL subscription, SAP fully supports deployments through the SAP CAL on Azure.</span></span> <span data-ttu-id="59bae-214">La cola de compatibilidad es BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="59bae-214">The support queue is BC-VCM-CAL.</span></span>







