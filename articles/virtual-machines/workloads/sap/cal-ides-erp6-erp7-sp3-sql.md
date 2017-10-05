---
title: "Implementación de SAP IDES EHP7 SP3 para SAP ERP 6.0 en Azure | Microsoft Docs"
description: "Implementación de SAP IDES EHP7 SP3 para SAP ERP 6.0 en Azure"
services: virtual-machines-windows
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 626c1523-1026-478f-bd8a-22c83b869231
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 09/16/2016
ms.author: hermannd
ms.openlocfilehash: 91eed294077ff72d0760018b10c98f32db88f3be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a><span data-ttu-id="4d7e5-103">Implementación de SAP IDES EHP7 SP3 para SAP ERP 6.0 en Azure</span><span class="sxs-lookup"><span data-stu-id="4d7e5-103">Deploy SAP IDES EHP7 SP3 for SAP ERP 6.0 on Azure</span></span>
<span data-ttu-id="4d7e5-104">En este artículo se describe cómo implementar un sistema SAP IDES que se ejecuta con SQL Server y el sistema operativo Windows en Azure por medio de SAP Cloud Appliance Library (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-104">This article describes how to deploy an SAP IDES system running with SQL Server and the Windows operating system on Azure via the SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="4d7e5-105">Las capturas de pantalla muestran el proceso paso a paso.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-105">The screenshots show the step-by-step process.</span></span> <span data-ttu-id="4d7e5-106">Para implementar otra solución, siga los mismos pasos.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-106">To deploy a different solution, follow the same steps.</span></span>

<span data-ttu-id="4d7e5-107">Para empezar con SAP CAL, vaya al sitio web de [SAP Cloud Appliance Library](https://cal.sap.com/).</span><span class="sxs-lookup"><span data-stu-id="4d7e5-107">To start with the SAP CAL, go to the [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="4d7e5-108">SAP también tiene un blog acerca de [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="4d7e5-108">SAP also has a blog about the new [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span> 

> [!NOTE]
<span data-ttu-id="4d7e5-109">A partir del 29 de mayo de 2017 puede usar el modelo de implementación mediante Azure Resource Manager, además del modelo de implementación clásico, que se usa menos, para implementar SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-109">As of May 29, 2017, you can use the Azure Resource Manager deployment model in addition to the less-preferred classic deployment model to deploy the SAP CAL.</span></span> <span data-ttu-id="4d7e5-110">Se recomienda usar el nuevo modelo de implementación mediante Resource Manager, en lugar del modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-110">We recommend that you use the new Resource Manager deployment model and disregard the classic deployment model.</span></span>

<span data-ttu-id="4d7e5-111">Si ya ha creado una cuenta de SAP CAL que utiliza el modelo clásico, *debe crear otra*.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-111">If you already created an SAP CAL account that uses the classic model, *you need to create another SAP CAL account*.</span></span> <span data-ttu-id="4d7e5-112">Dicha cuenta se debe implementar exclusivamente en Azure mediante el modelo de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-112">This account needs to exclusively deploy into Azure by using the Resource Manager model.</span></span>

<span data-ttu-id="4d7e5-113">Después de iniciar sesión SAP CAL, la primera página normalmente conducir a la página de **soluciones**.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-113">After you sign in to the SAP CAL, the first page usually leads you to the **Solutions** page.</span></span> <span data-ttu-id="4d7e5-114">El número de soluciones que se ofrecen en SAP CAL aumenta continuamente, por lo que es posible que deba desplazarse un poco para encontrar la solución que desea.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-114">The solutions offered on the SAP CAL are steadily increasing, so you might need to scroll quite a bit to find the solution you want.</span></span> <span data-ttu-id="4d7e5-115">La SAP IDES para Windows resaltada que está disponible exclusivamente en Azure muestra el proceso de implementación:</span><span class="sxs-lookup"><span data-stu-id="4d7e5-115">The highlighted Windows-based SAP IDES solution that is available exclusively on Azure demonstrates the deployment process:</span></span>

![Soluciones de SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-the-sap-cal"></a><span data-ttu-id="4d7e5-117">Creación de una cuenta en SAP CAL</span><span class="sxs-lookup"><span data-stu-id="4d7e5-117">Create an account in the SAP CAL</span></span>
1. <span data-ttu-id="4d7e5-118">La primera vez que inicie sesión en SAP CAL, utilice S-User de SAP, o cualquier otro usuario registrado de SAP.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-118">To sign in to the SAP CAL for the first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="4d7e5-119">A continuación, defina una cuenta de SAP CAL que SAP CAL use para implementar aplicaciones en Azure.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-119">Then define an SAP CAL account that is used by the SAP CAL to deploy appliances on Azure.</span></span> <span data-ttu-id="4d7e5-120">En la definición de la cuenta, debe:</span><span class="sxs-lookup"><span data-stu-id="4d7e5-120">In the account definition, you need to:</span></span>

    <span data-ttu-id="4d7e5-121">a.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-121">a.</span></span> <span data-ttu-id="4d7e5-122">Seleccione el modelo de implementación en Azure (Resource Manager o clásico).</span><span class="sxs-lookup"><span data-stu-id="4d7e5-122">Select the deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="4d7e5-123">b.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-123">b.</span></span> <span data-ttu-id="4d7e5-124">Especifique la suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-124">Enter your Azure subscription.</span></span> <span data-ttu-id="4d7e5-125">Una cuenta de SAP CAL no se puede asignar a más de una suscripción.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-125">An SAP CAL account can be assigned to one subscription only.</span></span> <span data-ttu-id="4d7e5-126">Si necesita más de una suscripción, debe crear otra cuenta de SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-126">If you need more than one subscription, you need to create another SAP CAL account.</span></span>
    
    <span data-ttu-id="4d7e5-127">c.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-127">c.</span></span> <span data-ttu-id="4d7e5-128">Conceda el permiso de SAP CAL para realizar la implementación en la suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-128">Give the SAP CAL permission to deploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="4d7e5-129">Los pasos siguientes muestran cómo crear una cuenta de SAP CAL para las implementaciones mediante Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-129">The next steps show how to create an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="4d7e5-130">Si ya tiene una cuenta de SAP CAL vinculada al modelo de implementación clásico, *tendrá que* seguir estos pasos para crear una cuenta de SAP CAL nueva.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-130">If you already have an SAP CAL account that is linked to the classic deployment model, you *need* to follow these steps to create a new SAP CAL account.</span></span> <span data-ttu-id="4d7e5-131">La nueva cuenta de SAP CAL se tiene que implementar mediante el modelo de Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-131">The new SAP CAL account needs to deploy in the Resource Manager model.</span></span>

2. <span data-ttu-id="4d7e5-132">Para crear una nueva cuenta de SAP CAL, la página **Accounts** (Cuentas) muestra dos opciones para Azure:</span><span class="sxs-lookup"><span data-stu-id="4d7e5-132">To create a new SAP CAL account, the **Accounts** page shows two choices for Azure:</span></span> 

    <span data-ttu-id="4d7e5-133">a.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-133">a.</span></span> <span data-ttu-id="4d7e5-134">**Microsoft Azure (classic)** es el modelo de implementación clásico y ya no se suele usar.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-134">**Microsoft Azure (classic)** is the classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="4d7e5-135">b.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-135">b.</span></span> <span data-ttu-id="4d7e5-136">**Microsoft Azure** es el nuevo modelo de implementación mediante Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-136">**Microsoft Azure** is the new Resource Manager deployment model.</span></span>

    ![Cuentas de SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    <span data-ttu-id="4d7e5-138">Para implementar mediante el modelo de Resource Manager, seleccione **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-138">To deploy in the Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Cuentas de SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. <span data-ttu-id="4d7e5-140">En el campo **Suscription ID**, especifique el identificador de suscripción de Azure, que se puede encontrar en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-140">Enter the Azure **Subscription ID** that can be found on the Azure portal.</span></span> 

    ![Identificador de suscripción de SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. <span data-ttu-id="4d7e5-142">Para autorizar que SAP CAL se implemente en la suscripción de Azure que ha definido, haga clic en **Authorize** (Autorizar).</span><span class="sxs-lookup"><span data-stu-id="4d7e5-142">To authorize the SAP CAL to deploy into the Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="4d7e5-143">La siguiente página aparecerá en la pestaña del explorador:</span><span class="sxs-lookup"><span data-stu-id="4d7e5-143">The following page appears in the browser tab:</span></span>

    ![Inicio de sesión de servicios en la nube de Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. <span data-ttu-id="4d7e5-145">Si se enumera más de un usuario, elija la cuenta de Microsoft vinculada para ser el coadministrador de la suscripción de Azure que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-145">If more than one user is listed, choose the Microsoft account that is linked to be the coadministrator of the Azure subscription you selected.</span></span> <span data-ttu-id="4d7e5-146">La siguiente página aparecerá en la pestaña del explorador:</span><span class="sxs-lookup"><span data-stu-id="4d7e5-146">The following page appears in the browser tab:</span></span>

    ![Confirmación de servicios en la nube de Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. <span data-ttu-id="4d7e5-148">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-148">Click **Accept**.</span></span> <span data-ttu-id="4d7e5-149">Si la autorización es correcta, vuelve a mostrarse la definición de la cuenta de SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-149">If the authorization is successful, the SAP CAL account definition displays again.</span></span> <span data-ttu-id="4d7e5-150">Poco después, un mensaje confirma que el proceso de autorización se ha realizado correctamente.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-150">After a short time, a message confirms that the authorization process was successful.</span></span>

7. <span data-ttu-id="4d7e5-151">Para asignar la cuenta de SAP CAL recién creada al usuario, escriba en el cuadro de texto de la derecha su **identificador de usuario** y haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-151">To assign the newly created SAP CAL account to your user, enter your **User ID** in the text box on the right and click **Add**.</span></span> 

    ![Asociación de cuenta a usuario](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. <span data-ttu-id="4d7e5-153">Para asociar una cuenta con el usuario que utiliza para iniciar sesión en SAP CAL, haga clic en **Review** (Revisar).</span><span class="sxs-lookup"><span data-stu-id="4d7e5-153">To associate your account with the user that you use to sign in to the SAP CAL, click **Review**.</span></span> 

9. <span data-ttu-id="4d7e5-154">Para crear la asociación entre el usuario y la cuenta de SAP CAL recién creada, haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="4d7e5-154">To create the association between your user and the newly created SAP CAL account, click **Create**.</span></span>

    ![Asociación de usuario a cuenta](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

<span data-ttu-id="4d7e5-156">Ha creado correctamente una cuenta de SAP CAL que puede:</span><span class="sxs-lookup"><span data-stu-id="4d7e5-156">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="4d7e5-157">Usar el modelo de implementación mediante Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-157">Use the Resource Manager deployment model.</span></span>
- <span data-ttu-id="4d7e5-158">Implementar sistemas de SAP en su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-158">Deploy SAP systems into your Azure subscription.</span></span>

> [!NOTE]
<span data-ttu-id="4d7e5-159">Para poder implementar la solución SAP IDES para Windows y SQL Server, es preciso registrarse para obtener una suscripción de SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-159">Before you can deploy the SAP IDES solution based on Windows and SQL Server, you might need to sign up for an SAP CAL subscription.</span></span> <span data-ttu-id="4d7e5-160">Si no se hace, la solución podría aparecer como **Locked** (Bloqueado) en la página de información general.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-160">Otherwise, the solution might show up as **Locked** on the overview page.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="4d7e5-161">Implementación de una solución</span><span class="sxs-lookup"><span data-stu-id="4d7e5-161">Deploy a solution</span></span>
1. <span data-ttu-id="4d7e5-162">Después de configurar una cuenta de SAP CAL, seleccione **La solución SAP IDES en Windows y la solución SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-162">After you set up an SAP CAL account, select **The SAP IDES solution on Windows and SQL Server** solution.</span></span> <span data-ttu-id="4d7e5-163">Haga clic en **Create Instance** (Crear instancia) y confirme las condiciones de uso.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-163">Click **Create Instance**, and confirm the usage and terms conditions.</span></span> 

2. <span data-ttu-id="4d7e5-164">En la página **Basic Mode: Create Instance** (Modo básico: crear instancia), tiene que:</span><span class="sxs-lookup"><span data-stu-id="4d7e5-164">On the **Basic Mode: Create Instance** page, you need to:</span></span>

    <span data-ttu-id="4d7e5-165">a.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-165">a.</span></span> <span data-ttu-id="4d7e5-166">Especificar en **Name** el nombre de la instancia.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-166">Enter an instance **Name**.</span></span>

    <span data-ttu-id="4d7e5-167">b.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-167">b.</span></span> <span data-ttu-id="4d7e5-168">Seleccionar una **región** de Azure.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-168">Select an Azure **Region**.</span></span> <span data-ttu-id="4d7e5-169">Para poder elegir entre varias regiones de Azure, puede que necesite tener una suscripción a SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-169">You might need an SAP CAL subscription to get multiple Azure regions offered.</span></span>

    <span data-ttu-id="4d7e5-170">c.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-170">c.</span></span>  <span data-ttu-id="4d7e5-171">Escribir en **Master Password** la contraseña maestra de la solución, como se muestra:</span><span class="sxs-lookup"><span data-stu-id="4d7e5-171">Enter the master **Password** for the solution, as shown:</span></span>

    ![SAP CAL, Modo básico: crear instancia](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. <span data-ttu-id="4d7e5-173">Haga clic en **Create** (Crear).</span><span class="sxs-lookup"><span data-stu-id="4d7e5-173">Click **Create**.</span></span> <span data-ttu-id="4d7e5-174">Después de un tiempo, y en función del tamaño y la complejidad de la solución (SAP CAL ofrece una estimación), el estado pasa mostrarse como activo y listo para usarse:</span><span class="sxs-lookup"><span data-stu-id="4d7e5-174">After some time, depending on the size and complexity of the solution (the SAP CAL provides an estimate), the status is shown as active and ready for use:</span></span> 

    ![Instancias de SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. <span data-ttu-id="4d7e5-176">Para buscar el grupo de recursos y todos los objetos que SAP CAL ha creado, vaya Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-176">To find the resource group and all its objects that were created by the SAP CAL, go to the Azure portal.</span></span> <span data-ttu-id="4d7e5-177">Se puede ver que la máquina virtual se inicia con el mismo nombre de instancia que se proporcionó en SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-177">The virtual machine can be found starting with the same instance name that was given in the SAP CAL.</span></span>

    ![Objetos del grupo de recursos](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. <span data-ttu-id="4d7e5-179">En el portal de SAP CAL, vaya a las instancias implementadas y haga clic en **Connect** (Conectar).</span><span class="sxs-lookup"><span data-stu-id="4d7e5-179">On the SAP CAL portal, go to the deployed instances and click **Connect**.</span></span> <span data-ttu-id="4d7e5-180">Aparece la siguiente ventana emergente:</span><span class="sxs-lookup"><span data-stu-id="4d7e5-180">The following pop-up window appears:</span></span> 

    ![Conectarse a la instancia](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. <span data-ttu-id="4d7e5-182">Para poder usar una de las opciones para conectarse a los sistemas implementados, haga clic en **Guía de introducción**.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-182">Before you can use one of the options to connect to the deployed systems, click **Getting Started Guide**.</span></span> <span data-ttu-id="4d7e5-183">La documentación asigna los nombres de los usuarios en cada uno de los métodos de conectividad.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-183">The documentation names the users for each of the connectivity methods.</span></span> <span data-ttu-id="4d7e5-184">Las contraseñas de dichos usuarios se establecen en la contraseña maestra que se definió al comienzo del proceso de implementación.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-184">The passwords for those users are set to the master password you defined at the beginning of the deployment process.</span></span> <span data-ttu-id="4d7e5-185">En la documentación, otros usuarios más funcionales se enumeran junto con sus contraseñas, que se pueden usar para iniciar sesión en el sistema implementado.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-185">In the documentation, other more functional users are listed with their passwords, which you can use to sign in to the deployed system.</span></span>

    ![Documentación de bienvenida de SAP](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

<span data-ttu-id="4d7e5-187">En unas pocas horas, un sistema SAP IDES en buen estado se implementa en Azure.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-187">Within a few hours, a healthy SAP IDES system is deployed in Azure.</span></span>

<span data-ttu-id="4d7e5-188">Si ha adquirido una suscripción a SAP CAL, SAP admite totalmente implementaciones a través de SAP CAL en Azure.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-188">If you bought an SAP CAL subscription, SAP fully supports deployments through the SAP CAL on Azure.</span></span> <span data-ttu-id="4d7e5-189">La cola de compatibilidad es BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="4d7e5-189">The support queue is BC-VCM-CAL.</span></span>

