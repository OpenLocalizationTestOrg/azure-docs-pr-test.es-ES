---
title: "aaaDeploy 4HANA/S de SAP o BW/4HANA en una máquina virtual de Azure | Documentos de Microsoft"
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
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a><span data-ttu-id="2eac7-103">Implementación de SAP S/4HANA o BW/4HANA en Azure</span><span class="sxs-lookup"><span data-stu-id="2eac7-103">Deploy SAP S/4HANA or BW/4HANA on Azure</span></span>
<span data-ttu-id="2eac7-104">Este artículo describe cómo toodeploy S/4HANA en Azure mediante el uso de Hola biblioteca de dispositivo de nube de SAP (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="2eac7-104">This article describes how toodeploy S/4HANA on Azure by using hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="2eac7-105">toodeploy otras soluciones basadas en SAP HANA, por ejemplo, BW/4HANA, siguen Hola mismos pasos.</span><span class="sxs-lookup"><span data-stu-id="2eac7-105">toodeploy other SAP HANA-based solutions, such as BW/4HANA, follow hello same steps.</span></span>

> [!NOTE]
<span data-ttu-id="2eac7-106">Para obtener más información acerca de hello CAL de SAP, visite toohello [biblioteca de dispositivo de nube de SAP](https://cal.sap.com/) sitio Web.</span><span class="sxs-lookup"><span data-stu-id="2eac7-106">For more information about hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="2eac7-107">SAP tiene también un blog sobre hello [SAP en la nube Appliance biblioteca 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="2eac7-107">SAP also has a blog about hello [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span>

> [!NOTE]
<span data-ttu-id="2eac7-108">Tal y como del 29 de mayo de 2017, puede usar el modelo de implementación de Azure Resource Manager hello además preferido menor toohello de implementación clásica modelo toodeploy Hola CAL de SAP.</span><span class="sxs-lookup"><span data-stu-id="2eac7-108">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="2eac7-109">Se recomienda que use el nuevo modelo de implementación de administrador de recursos hello y pasar por alto el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="2eac7-109">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

## <a name="step-by-step-process-toodeploy-hello-solution"></a><span data-ttu-id="2eac7-110">Solución de hello toodeploy proceso paso a paso</span><span class="sxs-lookup"><span data-stu-id="2eac7-110">Step-by-step process toodeploy hello solution</span></span>

<span data-ttu-id="2eac7-111">Hola sigue la secuencia de capturas de pantalla muestra cómo toodeploy S/4HANA en Azure mediante el uso de Hola CAL de SAP.</span><span class="sxs-lookup"><span data-stu-id="2eac7-111">hello following sequence of screenshots shows you how toodeploy S/4HANA on Azure by using hello SAP CAL.</span></span> <span data-ttu-id="2eac7-112">proceso de Hello funciona Hola igual en otras soluciones, como BW/4HANA.</span><span class="sxs-lookup"><span data-stu-id="2eac7-112">hello process works hello same way for other solutions, such as BW/4HANA.</span></span>

<span data-ttu-id="2eac7-113">Hola **soluciones** página muestra algunas de hello soluciones basadas en SAP HANA de CAL disponibles en Azure.</span><span class="sxs-lookup"><span data-stu-id="2eac7-113">hello **Solutions** page shows some of hello SAP CAL HANA-based solutions available on Azure.</span></span> <span data-ttu-id="2eac7-114">**SAP S/4HANA 1610 FPS01, dispositivo Fully-Activated** está en la fila de hello central:</span><span class="sxs-lookup"><span data-stu-id="2eac7-114">**SAP S/4HANA 1610 FPS01, Fully-Activated Appliance** is in hello middle row:</span></span>

![Soluciones de SAP CAL](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="2eac7-116">Crear una cuenta de hello CAL de SAP</span><span class="sxs-lookup"><span data-stu-id="2eac7-116">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="2eac7-117">toosign en toohello CAL de SAP para hello primera vez, utilice el usuario S SAP u otro usuario registrado con SAP.</span><span class="sxs-lookup"><span data-stu-id="2eac7-117">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="2eac7-118">A continuación, defina una cuenta de CAL de SAP que se usa por dispositivos de toodeploy Hola CAL de SAP en Azure.</span><span class="sxs-lookup"><span data-stu-id="2eac7-118">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="2eac7-119">En la definición de la cuenta de hello, necesitará:</span><span class="sxs-lookup"><span data-stu-id="2eac7-119">In hello account definition, you need to:</span></span>

    <span data-ttu-id="2eac7-120">a.</span><span class="sxs-lookup"><span data-stu-id="2eac7-120">a.</span></span> <span data-ttu-id="2eac7-121">Seleccione el modelo de implementación de hello en Azure (Administrador de recursos o estándar).</span><span class="sxs-lookup"><span data-stu-id="2eac7-121">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="2eac7-122">b.</span><span class="sxs-lookup"><span data-stu-id="2eac7-122">b.</span></span> <span data-ttu-id="2eac7-123">Especifique la suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="2eac7-123">Enter your Azure subscription.</span></span> <span data-ttu-id="2eac7-124">Puede asignarse a una cuenta de SAP CAL tooone suscripción solo.</span><span class="sxs-lookup"><span data-stu-id="2eac7-124">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="2eac7-125">Si necesita más de una suscripción, deberá toocreate otra cuenta de CAL de SAP.</span><span class="sxs-lookup"><span data-stu-id="2eac7-125">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>

    <span data-ttu-id="2eac7-126">c.</span><span class="sxs-lookup"><span data-stu-id="2eac7-126">c.</span></span> <span data-ttu-id="2eac7-127">Dar permiso toodeploy de hello CAL de SAP en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="2eac7-127">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="2eac7-128">pasos siguientes Hola muestran cómo cuenta toocreate una CAL de SAP para las implementaciones del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="2eac7-128">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="2eac7-129">Si ya tiene una cuenta de CAL de SAP que sea el modelo de implementación clásica toohello vinculado, se *necesita* toofollow estos toocreate pasos una nueva cuenta de CAL de SAP.</span><span class="sxs-lookup"><span data-stu-id="2eac7-129">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="2eac7-130">nueva cuenta de CAL de SAP Hola debe toodeploy en el modelo de administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2eac7-130">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="2eac7-131">Cree una nueva cuenta de SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="2eac7-131">Create a new SAP CAL account.</span></span> <span data-ttu-id="2eac7-132">Hola **cuentas** página muestra tres opciones de Azure:</span><span class="sxs-lookup"><span data-stu-id="2eac7-132">hello **Accounts** page shows three choices for Azure:</span></span> 

    <span data-ttu-id="2eac7-133">a.</span><span class="sxs-lookup"><span data-stu-id="2eac7-133">a.</span></span> <span data-ttu-id="2eac7-134">**Microsoft Azure (clásica)** es el modelo de implementación clásica de Hola y ya no se prefiere.</span><span class="sxs-lookup"><span data-stu-id="2eac7-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="2eac7-135">b.</span><span class="sxs-lookup"><span data-stu-id="2eac7-135">b.</span></span> <span data-ttu-id="2eac7-136">**Microsoft Azure** es Hola nuevo modelo de implementación de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="2eac7-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    <span data-ttu-id="2eac7-137">c.</span><span class="sxs-lookup"><span data-stu-id="2eac7-137">c.</span></span> <span data-ttu-id="2eac7-138">**Windows Azure operado por 21Vianet** es una opción en China que usa el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="2eac7-138">**Windows Azure operated by 21Vianet** is an option in China that uses hello classic deployment model.</span></span>

    <span data-ttu-id="2eac7-139">Seleccione toodeploy en el modelo del Administrador de recursos de hello, **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="2eac7-139">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Detalles de la cuenta de SAP CAL](./media/cal-s4h/s4h-pic-2a.png)

3. <span data-ttu-id="2eac7-141">Escriba hello Azure **Id. de suscripción** que pueden encontrarse en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="2eac7-141">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span>

   ![Cuentas de SAP CAL](./media/cal-s4h/s4h-pic3c.png)

4. <span data-ttu-id="2eac7-143">tooauthorize Hola SAP CAL toodeploy en hello suscripción de Azure ha definido, haga clic en **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="2eac7-143">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="2eac7-144">Hola después de la página aparece en la pestaña de explorador hello:</span><span class="sxs-lookup"><span data-stu-id="2eac7-144">hello following page appears in hello browser tab:</span></span>

   ![Inicio de sesión de servicios en la nube de Internet Explorer](./media/cal-s4h/s4h-pic4c.png)

5. <span data-ttu-id="2eac7-146">Si aparece más de un usuario, elija la cuenta de Microsoft de Hola que está vinculado toobe hello coadministrator de hello Azure suscripción que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="2eac7-146">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="2eac7-147">Hola después de la página aparece en la pestaña de explorador hello:</span><span class="sxs-lookup"><span data-stu-id="2eac7-147">hello following page appears in hello browser tab:</span></span>

   ![Confirmación de servicios en la nube de Internet Explorer](./media/cal-s4h/s4h-pic5a.png)

6. <span data-ttu-id="2eac7-149">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2eac7-149">Click **Accept**.</span></span> <span data-ttu-id="2eac7-150">Si es correcta la autorización de hello, vuelve a mostrar hello definición de la cuenta de CAL de SAP.</span><span class="sxs-lookup"><span data-stu-id="2eac7-150">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="2eac7-151">Después de unos minutos, un mensaje confirmará que el proceso de autorización de hello fue correcta.</span><span class="sxs-lookup"><span data-stu-id="2eac7-151">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="2eac7-152">Hola tooassign recién creado tooyour de cuenta SAP CAL de usuario, escriba su **Id. de usuario** en Hola Hola derecho cuadro de texto y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="2eac7-152">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span>

   ![Asociación de cuenta toouser](./media/cal-s4h/s4h-pic8a.png)

8. <span data-ttu-id="2eac7-154">tooassociate su cuenta con usuario Hola que usas toosign en toohello CAL de SAP, haga clic en **revisión**.</span><span class="sxs-lookup"><span data-stu-id="2eac7-154">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 
 
9. <span data-ttu-id="2eac7-155">asociación de hello toocreate entre el usuario y la cuenta de CAL de SAP de hello recién creado, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="2eac7-155">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

   ![Asociación de cuenta de usuario tooSAP CAL](./media/cal-s4h/s4h-pic9b.png)

<span data-ttu-id="2eac7-157">Ha creado correctamente una cuenta de SAP CAL que puede:</span><span class="sxs-lookup"><span data-stu-id="2eac7-157">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="2eac7-158">Utilice el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="2eac7-158">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="2eac7-159">Implementar sistemas de SAP en su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="2eac7-159">Deploy SAP systems into your Azure subscription.</span></span>

<span data-ttu-id="2eac7-160">Ahora puede iniciar toodeploy S/4HANA en su suscripción de usuario en Azure.</span><span class="sxs-lookup"><span data-stu-id="2eac7-160">Now you can start toodeploy S/4HANA into your user subscription in Azure.</span></span>

> [!NOTE]
<span data-ttu-id="2eac7-161">Antes de continuar, determine si dispone de cuotas de núcleos de Azure para máquinas virtuales de la serie H de Azure.</span><span class="sxs-lookup"><span data-stu-id="2eac7-161">Before you continue, determine whether you have Azure core quotas for Azure H-Series VMs.</span></span> <span data-ttu-id="2eac7-162">En el momento de hello, Hola CAL de SAP usa H-Series máquinas virtuales de Azure toodeploy algunas de las soluciones basadas en SAP HANA de Hola.</span><span class="sxs-lookup"><span data-stu-id="2eac7-162">At hello moment, hello SAP CAL uses H-Series VMs of Azure toodeploy some of hello SAP HANA-based solutions.</span></span> <span data-ttu-id="2eac7-163">Su suscripción de Azure podría no tener ninguna cuota de núcleos para la serie H.</span><span class="sxs-lookup"><span data-stu-id="2eac7-163">Your Azure subscription might not have any H-Series core quotas for H-Series.</span></span> <span data-ttu-id="2eac7-164">Si es así, tendrá que tooget de soporte técnico de Azure toocontact una cuota de núcleos de al menos 16 H-Series.</span><span class="sxs-lookup"><span data-stu-id="2eac7-164">If so, you might need toocontact Azure support tooget a quota of at least 16 H-Series cores.</span></span>

> [!NOTE]
<span data-ttu-id="2eac7-165">Al implementar una solución en Azure en hello CAL de SAP, es posible que puede elegir solo una región de Azure.</span><span class="sxs-lookup"><span data-stu-id="2eac7-165">When you deploy a solution on Azure in hello SAP CAL, you might find that you can choose only one Azure region.</span></span> <span data-ttu-id="2eac7-166">toodeploy en regiones de Azure que no sea de hello uno sugeridos por hello CAL de SAP, deberá toopurchase una suscripción de CAL de SAP.</span><span class="sxs-lookup"><span data-stu-id="2eac7-166">toodeploy into Azure regions other than hello one suggested by hello SAP CAL, you need toopurchase a CAL subscription from SAP.</span></span> <span data-ttu-id="2eac7-167">También tendrá que tooopen un mensaje con SAP toohave su toodeliver de cuenta habilitada CAL en regiones de Azure que no sea de Hola que se sugieren inicialmente.</span><span class="sxs-lookup"><span data-stu-id="2eac7-167">You also might need tooopen a message with SAP toohave your CAL account enabled toodeliver into Azure regions other than hello ones initially suggested.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="2eac7-168">Implementación de una solución</span><span class="sxs-lookup"><span data-stu-id="2eac7-168">Deploy a solution</span></span>

<span data-ttu-id="2eac7-169">Vamos a implementar una solución de hello **soluciones** página de hello CAL de SAP.</span><span class="sxs-lookup"><span data-stu-id="2eac7-169">Let's deploy a solution from hello **Solutions** page of hello SAP CAL.</span></span> <span data-ttu-id="2eac7-170">Hola CAL de SAP tiene dos toodeploy de secuencias:</span><span class="sxs-lookup"><span data-stu-id="2eac7-170">hello SAP CAL has two sequences toodeploy:</span></span>

- <span data-ttu-id="2eac7-171">Una secuencia básica que utiliza una página toodefine Hola sistema toobe implementado</span><span class="sxs-lookup"><span data-stu-id="2eac7-171">A basic sequence that uses one page toodefine hello system toobe deployed</span></span>
- <span data-ttu-id="2eac7-172">Una secuencia avanzada que le ofrece varias opciones en relación al tamaño de las máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="2eac7-172">An advanced sequence that gives you certain choices on VM sizes</span></span> 

<span data-ttu-id="2eac7-173">Se muestra aquí toodeployment de ruta de acceso básico de Hola.</span><span class="sxs-lookup"><span data-stu-id="2eac7-173">We demonstrate hello basic path toodeployment here.</span></span>

1. <span data-ttu-id="2eac7-174">En hello **detalles de la cuenta** página, necesita:</span><span class="sxs-lookup"><span data-stu-id="2eac7-174">On hello **Account Details** page, you need to:</span></span>

    <span data-ttu-id="2eac7-175">a.</span><span class="sxs-lookup"><span data-stu-id="2eac7-175">a.</span></span> <span data-ttu-id="2eac7-176">Seleccionar una cuenta de SAP CAL.</span><span class="sxs-lookup"><span data-stu-id="2eac7-176">Select an SAP CAL account.</span></span> <span data-ttu-id="2eac7-177">(Utilice una cuenta que sea toodeploy asociado con el modelo de implementación del Administrador de recursos de hello).</span><span class="sxs-lookup"><span data-stu-id="2eac7-177">(Use an account that is associated toodeploy with hello Resource Manager deployment model.)</span></span>

    <span data-ttu-id="2eac7-178">b.</span><span class="sxs-lookup"><span data-stu-id="2eac7-178">b.</span></span> <span data-ttu-id="2eac7-179">Especificar en **Name** el nombre de la instancia.</span><span class="sxs-lookup"><span data-stu-id="2eac7-179">Enter an instance **Name**.</span></span>

    <span data-ttu-id="2eac7-180">c.</span><span class="sxs-lookup"><span data-stu-id="2eac7-180">c.</span></span> <span data-ttu-id="2eac7-181">Seleccionar una **región** de Azure.</span><span class="sxs-lookup"><span data-stu-id="2eac7-181">Select an Azure **Region**.</span></span> <span data-ttu-id="2eac7-182">Hola CAL de SAP sugiere una región.</span><span class="sxs-lookup"><span data-stu-id="2eac7-182">hello SAP CAL suggests a region.</span></span> <span data-ttu-id="2eac7-183">Si necesita otra región de Azure y no tiene una suscripción de CAL de SAP, deberá tooorder una CAL de suscripción con SAP.</span><span class="sxs-lookup"><span data-stu-id="2eac7-183">If you need another Azure region and you don't have an SAP CAL subscription, you need tooorder a CAL subscription with SAP.</span></span>

    <span data-ttu-id="2eac7-184">d.</span><span class="sxs-lookup"><span data-stu-id="2eac7-184">d.</span></span> <span data-ttu-id="2eac7-185">Escriba un patrón **contraseña** para la solución de Hola de ocho o nueve caracteres.</span><span class="sxs-lookup"><span data-stu-id="2eac7-185">Enter a master **Password** for hello solution of eight or nine characters.</span></span> <span data-ttu-id="2eac7-186">Hola contraseña se usa para los administradores de Hola de diferentes componentes de Hola.</span><span class="sxs-lookup"><span data-stu-id="2eac7-186">hello password is used for hello administrators of hello different components.</span></span>

   ![SAP CAL, Modo básico: crear instancia](./media/cal-s4h/s4h-pic10a.png)

2. <span data-ttu-id="2eac7-188">Haga clic en **crear**y en el cuadro de mensaje de Hola que aparece, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2eac7-188">Click **Create**, and in hello message box that appears, click **OK**.</span></span>

   ![Tamaños de máquinas virtuales que admite SAP CAL](./media/cal-s4h/s4h-pic10b.png)

3. <span data-ttu-id="2eac7-190">Hola **clave privada** cuadro de diálogo, haga clic en **almacén** clave privada de toostore Hola Hola CAL de SAP.</span><span class="sxs-lookup"><span data-stu-id="2eac7-190">In hello **Private Key** dialog box, click **Store** toostore hello private key in hello SAP CAL.</span></span> <span data-ttu-id="2eac7-191">Haga clic en protección con contraseña de clave privada de hello, toouse **descargar**.</span><span class="sxs-lookup"><span data-stu-id="2eac7-191">toouse password protection for hello private key, click **Download**.</span></span> 

   ![Clave privada de SAP CAL](./media/cal-s4h/s4h-pic10c.png)

4. <span data-ttu-id="2eac7-193">Hola de lectura SAP CAL **advertencia** el mensaje y haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="2eac7-193">Read hello SAP CAL **Warning** message, and click **OK**.</span></span>

   ![Advertencia de SAP CAL](./media/cal-s4h/s4h-pic10d.png)

    <span data-ttu-id="2eac7-195">Ahora la implementación de hello tiene lugar.</span><span class="sxs-lookup"><span data-stu-id="2eac7-195">Now hello deployment takes place.</span></span> <span data-ttu-id="2eac7-196">Más tarde, según el tamaño de Hola y la complejidad de solución de hello (Hola CAL de SAP proporciona una estimación), Hola estado se muestra como activo y preparado para su uso.</span><span class="sxs-lookup"><span data-stu-id="2eac7-196">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use.</span></span>

5. <span data-ttu-id="2eac7-197">recopilados con las máquinas virtuales de toofind Hola Hola otros recursos asociados en un grupo de recursos, vaya toohello portal de Azure:</span><span class="sxs-lookup"><span data-stu-id="2eac7-197">toofind hello virtual machines collected with hello other associated resources in one resource group, go toohello Azure portal:</span></span> 

   ![Objetos de CAL de SAP implementados en el nuevo portal de Hola](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. <span data-ttu-id="2eac7-199">En el portal de SAP CAL hello, estado de hello aparece como **Active**.</span><span class="sxs-lookup"><span data-stu-id="2eac7-199">On hello SAP CAL portal, hello status appears as **Active**.</span></span> <span data-ttu-id="2eac7-200">solución de toohello tooconnect, haga clic en **conectar**.</span><span class="sxs-lookup"><span data-stu-id="2eac7-200">tooconnect toohello solution, click **Connect**.</span></span> <span data-ttu-id="2eac7-201">Se implementan diferentes componentes de diferentes opciones tooconnect toohello dentro de esta solución.</span><span class="sxs-lookup"><span data-stu-id="2eac7-201">Different options tooconnect toohello different components are deployed within this solution.</span></span>

   ![Instancias de SAP CAL](./media/cal-s4h/active_solution.png)

7. <span data-ttu-id="2eac7-203">Para poder usar uno de hello opciones tooconnect toohello implementado sistemas, haga clic en **Getting Started Guide**.</span><span class="sxs-lookup"><span data-stu-id="2eac7-203">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> 

   ![Conectar toohello instancia](./media/cal-s4h/connect_to_solution.png)

    <span data-ttu-id="2eac7-205">nombres de la documentación de Hola Hola a los usuarios para cada uno de los métodos de conectividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="2eac7-205">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="2eac7-206">las contraseñas de Hola para los usuarios se establecen toohello contraseña maestra que ha definido al principio de Hola Hola del proceso de implementación.</span><span class="sxs-lookup"><span data-stu-id="2eac7-206">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="2eac7-207">En la documentación de hello, otros usuarios más funcionales se muestran con sus contraseñas, que se pueden usar toosign en toohello implementa el sistema.</span><span class="sxs-lookup"><span data-stu-id="2eac7-207">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span> 

    <span data-ttu-id="2eac7-208">Por ejemplo, si usas Hola GUI de SAP está preinstalado en la máquina de escritorio remoto de Windows hello, Hola sistema S/4 podría ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="2eac7-208">For example, if you use hello SAP GUI that's preinstalled on hello Windows Remote Desktop machine, hello S/4 system might look like this:</span></span>

   ![SM50 Hola preinstalado GUI de SAP](./media/cal-s4h/gui_sm50.png)

    <span data-ttu-id="2eac7-210">O bien, si usas hello DBACockpit, instancia Hola podría ser similar al siguiente:</span><span class="sxs-lookup"><span data-stu-id="2eac7-210">Or if you use hello DBACockpit, hello instance might look like this:</span></span>

   ![SM50 Hola DBACockpit GUI de SAP](./media/cal-s4h/dbacockpit.png)

<span data-ttu-id="2eac7-212">En unas horas, una aplicación SAP S/4 correcta se implementa en Azure.</span><span class="sxs-lookup"><span data-stu-id="2eac7-212">Within a few hours, a healthy SAP S/4 appliance is deployed in Azure.</span></span>

<span data-ttu-id="2eac7-213">Si ha adquirido una suscripción de CAL de SAP, SAP admite totalmente las implementaciones a través de hello CAL de SAP en Azure.</span><span class="sxs-lookup"><span data-stu-id="2eac7-213">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="2eac7-214">cola de soporte técnico de Hello es BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="2eac7-214">hello support queue is BC-VCM-CAL.</span></span>







