---
title: aaaDeploy IDE EHP7 SP3 de SAP para SAP ERP 6.0 en Azure | Documentos de Microsoft
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
ms.openlocfilehash: 26d88c7b48a91d35602464c4f89ca7a30502c4b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a><span data-ttu-id="5553b-103">Implementación de SAP IDES EHP7 SP3 para SAP ERP 6.0 en Azure</span><span class="sxs-lookup"><span data-stu-id="5553b-103">Deploy SAP IDES EHP7 SP3 for SAP ERP 6.0 on Azure</span></span>
<span data-ttu-id="5553b-104">Este artículo se describe cómo toodeploy una SAP sistema IDE que se ejecuta con SQL Server y el sistema operativo de Windows hello en Azure a través de hello biblioteca de dispositivo de nube de SAP (SAP CAL) 3.0.</span><span class="sxs-lookup"><span data-stu-id="5553b-104">This article describes how toodeploy an SAP IDES system running with SQL Server and hello Windows operating system on Azure via hello SAP Cloud Appliance Library (SAP CAL) 3.0.</span></span> <span data-ttu-id="5553b-105">capturas de pantalla de Hello muestran el proceso paso a paso de Hola.</span><span class="sxs-lookup"><span data-stu-id="5553b-105">hello screenshots show hello step-by-step process.</span></span> <span data-ttu-id="5553b-106">toodeploy otra solución, siga Hola los mismos pasos.</span><span class="sxs-lookup"><span data-stu-id="5553b-106">toodeploy a different solution, follow hello same steps.</span></span>

<span data-ttu-id="5553b-107">toostart con hello CAL de SAP, vaya toohello [biblioteca de dispositivo de nube de SAP](https://cal.sap.com/) sitio Web.</span><span class="sxs-lookup"><span data-stu-id="5553b-107">toostart with hello SAP CAL, go toohello [SAP Cloud Appliance Library](https://cal.sap.com/) website.</span></span> <span data-ttu-id="5553b-108">SAP también tiene un blog sobre Hola nuevo [SAP en la nube Appliance biblioteca 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span><span class="sxs-lookup"><span data-stu-id="5553b-108">SAP also has a blog about hello new [SAP Cloud Appliance Library 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).</span></span> 

> [!NOTE]
<span data-ttu-id="5553b-109">Tal y como del 29 de mayo de 2017, puede usar el modelo de implementación de Azure Resource Manager hello además preferido menor toohello de implementación clásica modelo toodeploy Hola CAL de SAP.</span><span class="sxs-lookup"><span data-stu-id="5553b-109">As of May 29, 2017, you can use hello Azure Resource Manager deployment model in addition toohello less-preferred classic deployment model toodeploy hello SAP CAL.</span></span> <span data-ttu-id="5553b-110">Se recomienda que use el nuevo modelo de implementación de administrador de recursos hello y pasar por alto el modelo de implementación clásica de Hola.</span><span class="sxs-lookup"><span data-stu-id="5553b-110">We recommend that you use hello new Resource Manager deployment model and disregard hello classic deployment model.</span></span>

<span data-ttu-id="5553b-111">Si ha creado una cuenta de CAL de SAP que utiliza el modelo clásico de hello, *necesita toocreate otra cuenta de CAL de SAP*.</span><span class="sxs-lookup"><span data-stu-id="5553b-111">If you already created an SAP CAL account that uses hello classic model, *you need toocreate another SAP CAL account*.</span></span> <span data-ttu-id="5553b-112">Esta cuenta debe tooexclusively implementar en Azure mediante el modelo de administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5553b-112">This account needs tooexclusively deploy into Azure by using hello Resource Manager model.</span></span>

<span data-ttu-id="5553b-113">Después de iniciar sesión en toohello CAL de SAP, primera página de hello normalmente le toohello **soluciones** página.</span><span class="sxs-lookup"><span data-stu-id="5553b-113">After you sign in toohello SAP CAL, hello first page usually leads you toohello **Solutions** page.</span></span> <span data-ttu-id="5553b-114">soluciones de Hello ofrecidas en hello CAL de SAP se aumentan continuamente, por lo que tendrá que tooscroll un poco toofind Hola solución.</span><span class="sxs-lookup"><span data-stu-id="5553b-114">hello solutions offered on hello SAP CAL are steadily increasing, so you might need tooscroll quite a bit toofind hello solution you want.</span></span> <span data-ttu-id="5553b-115">solución de IDE de SAP basados en Windows de Hello resaltado que está disponible exclusivamente en Azure demuestra el proceso de implementación de hello:</span><span class="sxs-lookup"><span data-stu-id="5553b-115">hello highlighted Windows-based SAP IDES solution that is available exclusively on Azure demonstrates hello deployment process:</span></span>

![Soluciones de SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-hello-sap-cal"></a><span data-ttu-id="5553b-117">Crear una cuenta de hello CAL de SAP</span><span class="sxs-lookup"><span data-stu-id="5553b-117">Create an account in hello SAP CAL</span></span>
1. <span data-ttu-id="5553b-118">toosign en toohello CAL de SAP para hello primera vez, utilice el usuario S SAP u otro usuario registrado con SAP.</span><span class="sxs-lookup"><span data-stu-id="5553b-118">toosign in toohello SAP CAL for hello first time, use your SAP S-User or other user registered with SAP.</span></span> <span data-ttu-id="5553b-119">A continuación, defina una cuenta de CAL de SAP que se usa por dispositivos de toodeploy Hola CAL de SAP en Azure.</span><span class="sxs-lookup"><span data-stu-id="5553b-119">Then define an SAP CAL account that is used by hello SAP CAL toodeploy appliances on Azure.</span></span> <span data-ttu-id="5553b-120">En la definición de la cuenta de hello, necesitará:</span><span class="sxs-lookup"><span data-stu-id="5553b-120">In hello account definition, you need to:</span></span>

    <span data-ttu-id="5553b-121">a.</span><span class="sxs-lookup"><span data-stu-id="5553b-121">a.</span></span> <span data-ttu-id="5553b-122">Seleccione el modelo de implementación de hello en Azure (Administrador de recursos o estándar).</span><span class="sxs-lookup"><span data-stu-id="5553b-122">Select hello deployment model on Azure (Resource Manager or classic).</span></span>

    <span data-ttu-id="5553b-123">b.</span><span class="sxs-lookup"><span data-stu-id="5553b-123">b.</span></span> <span data-ttu-id="5553b-124">Especifique la suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="5553b-124">Enter your Azure subscription.</span></span> <span data-ttu-id="5553b-125">Puede asignarse a una cuenta de SAP CAL tooone suscripción solo.</span><span class="sxs-lookup"><span data-stu-id="5553b-125">An SAP CAL account can be assigned tooone subscription only.</span></span> <span data-ttu-id="5553b-126">Si necesita más de una suscripción, deberá toocreate otra cuenta de CAL de SAP.</span><span class="sxs-lookup"><span data-stu-id="5553b-126">If you need more than one subscription, you need toocreate another SAP CAL account.</span></span>
    
    <span data-ttu-id="5553b-127">c.</span><span class="sxs-lookup"><span data-stu-id="5553b-127">c.</span></span> <span data-ttu-id="5553b-128">Dar permiso toodeploy de hello CAL de SAP en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="5553b-128">Give hello SAP CAL permission toodeploy into your Azure subscription.</span></span>

    > [!NOTE]
    <span data-ttu-id="5553b-129">pasos siguientes Hola muestran cómo cuenta toocreate una CAL de SAP para las implementaciones del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="5553b-129">hello next steps show how toocreate an SAP CAL account for Resource Manager deployments.</span></span> <span data-ttu-id="5553b-130">Si ya tiene una cuenta de CAL de SAP que sea el modelo de implementación clásica toohello vinculado, se *necesita* toofollow estos toocreate pasos una nueva cuenta de CAL de SAP.</span><span class="sxs-lookup"><span data-stu-id="5553b-130">If you already have an SAP CAL account that is linked toohello classic deployment model, you *need* toofollow these steps toocreate a new SAP CAL account.</span></span> <span data-ttu-id="5553b-131">nueva cuenta de CAL de SAP Hola debe toodeploy en el modelo de administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5553b-131">hello new SAP CAL account needs toodeploy in hello Resource Manager model.</span></span>

2. <span data-ttu-id="5553b-132">toocreate una nueva CAL de SAP de la cuenta, hello **cuentas** página muestra dos opciones de Azure:</span><span class="sxs-lookup"><span data-stu-id="5553b-132">toocreate a new SAP CAL account, hello **Accounts** page shows two choices for Azure:</span></span> 

    <span data-ttu-id="5553b-133">a.</span><span class="sxs-lookup"><span data-stu-id="5553b-133">a.</span></span> <span data-ttu-id="5553b-134">**Microsoft Azure (clásica)** es el modelo de implementación clásica de Hola y ya no se prefiere.</span><span class="sxs-lookup"><span data-stu-id="5553b-134">**Microsoft Azure (classic)** is hello classic deployment model and is no longer preferred.</span></span>

    <span data-ttu-id="5553b-135">b.</span><span class="sxs-lookup"><span data-stu-id="5553b-135">b.</span></span> <span data-ttu-id="5553b-136">**Microsoft Azure** es Hola nuevo modelo de implementación de administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="5553b-136">**Microsoft Azure** is hello new Resource Manager deployment model.</span></span>

    ![Cuentas de SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    <span data-ttu-id="5553b-138">Seleccione toodeploy en el modelo del Administrador de recursos de hello, **Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="5553b-138">toodeploy in hello Resource Manager model, select **Microsoft Azure**.</span></span>

    ![Cuentas de SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. <span data-ttu-id="5553b-140">Escriba hello Azure **Id. de suscripción** que pueden encontrarse en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="5553b-140">Enter hello Azure **Subscription ID** that can be found on hello Azure portal.</span></span> 

    ![Identificador de suscripción de SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. <span data-ttu-id="5553b-142">tooauthorize Hola SAP CAL toodeploy en hello suscripción de Azure ha definido, haga clic en **Authorize**.</span><span class="sxs-lookup"><span data-stu-id="5553b-142">tooauthorize hello SAP CAL toodeploy into hello Azure subscription you defined, click **Authorize**.</span></span> <span data-ttu-id="5553b-143">Hola después de la página aparece en la pestaña de explorador hello:</span><span class="sxs-lookup"><span data-stu-id="5553b-143">hello following page appears in hello browser tab:</span></span>

    ![Inicio de sesión de servicios en la nube de Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. <span data-ttu-id="5553b-145">Si aparece más de un usuario, elija la cuenta de Microsoft de Hola que está vinculado toobe hello coadministrator de hello Azure suscripción que ha seleccionado.</span><span class="sxs-lookup"><span data-stu-id="5553b-145">If more than one user is listed, choose hello Microsoft account that is linked toobe hello coadministrator of hello Azure subscription you selected.</span></span> <span data-ttu-id="5553b-146">Hola después de la página aparece en la pestaña de explorador hello:</span><span class="sxs-lookup"><span data-stu-id="5553b-146">hello following page appears in hello browser tab:</span></span>

    ![Confirmación de servicios en la nube de Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. <span data-ttu-id="5553b-148">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="5553b-148">Click **Accept**.</span></span> <span data-ttu-id="5553b-149">Si es correcta la autorización de hello, vuelve a mostrar hello definición de la cuenta de CAL de SAP.</span><span class="sxs-lookup"><span data-stu-id="5553b-149">If hello authorization is successful, hello SAP CAL account definition displays again.</span></span> <span data-ttu-id="5553b-150">Después de unos minutos, un mensaje confirmará que el proceso de autorización de hello fue correcta.</span><span class="sxs-lookup"><span data-stu-id="5553b-150">After a short time, a message confirms that hello authorization process was successful.</span></span>

7. <span data-ttu-id="5553b-151">Hola tooassign recién creado tooyour de cuenta SAP CAL de usuario, escriba su **Id. de usuario** en Hola Hola derecho cuadro de texto y haga clic en **agregar**.</span><span class="sxs-lookup"><span data-stu-id="5553b-151">tooassign hello newly created SAP CAL account tooyour user, enter your **User ID** in hello text box on hello right and click **Add**.</span></span> 

    ![Asociación de cuenta toouser](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. <span data-ttu-id="5553b-153">tooassociate su cuenta con usuario Hola que usas toosign en toohello CAL de SAP, haga clic en **revisión**.</span><span class="sxs-lookup"><span data-stu-id="5553b-153">tooassociate your account with hello user that you use toosign in toohello SAP CAL, click **Review**.</span></span> 

9. <span data-ttu-id="5553b-154">asociación de hello toocreate entre el usuario y la cuenta de CAL de SAP de hello recién creado, haga clic en **crear**.</span><span class="sxs-lookup"><span data-stu-id="5553b-154">toocreate hello association between your user and hello newly created SAP CAL account, click **Create**.</span></span>

    ![Asociación de tooaccount de usuario](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

<span data-ttu-id="5553b-156">Ha creado correctamente una cuenta de SAP CAL que puede:</span><span class="sxs-lookup"><span data-stu-id="5553b-156">You successfully created an SAP CAL account that is able to:</span></span>

- <span data-ttu-id="5553b-157">Utilice el modelo de implementación del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5553b-157">Use hello Resource Manager deployment model.</span></span>
- <span data-ttu-id="5553b-158">Implementar sistemas de SAP en su suscripción a Azure.</span><span class="sxs-lookup"><span data-stu-id="5553b-158">Deploy SAP systems into your Azure subscription.</span></span>

> [!NOTE]
<span data-ttu-id="5553b-159">Para poder implementar soluciones SAP IDE Hola basadas en Windows y SQL Server, puede que tenga toosign hacia arriba para una suscripción de CAL de SAP.</span><span class="sxs-lookup"><span data-stu-id="5553b-159">Before you can deploy hello SAP IDES solution based on Windows and SQL Server, you might need toosign up for an SAP CAL subscription.</span></span> <span data-ttu-id="5553b-160">En caso contrario, podría aparecen solución hello como **bloqueado** en la página de información general de Hola.</span><span class="sxs-lookup"><span data-stu-id="5553b-160">Otherwise, hello solution might show up as **Locked** on hello overview page.</span></span>

### <a name="deploy-a-solution"></a><span data-ttu-id="5553b-161">Implementación de una solución</span><span class="sxs-lookup"><span data-stu-id="5553b-161">Deploy a solution</span></span>
1. <span data-ttu-id="5553b-162">Después de configurar una cuenta de CAL de SAP, seleccione **Hola solución SAP IDE en Windows y SQL Server** solución.</span><span class="sxs-lookup"><span data-stu-id="5553b-162">After you set up an SAP CAL account, select **hello SAP IDES solution on Windows and SQL Server** solution.</span></span> <span data-ttu-id="5553b-163">Haga clic en **crear instancia**y confirme las condiciones de uso y los términos de Hola.</span><span class="sxs-lookup"><span data-stu-id="5553b-163">Click **Create Instance**, and confirm hello usage and terms conditions.</span></span> 

2. <span data-ttu-id="5553b-164">En hello **modo básico: crear instancia** página, necesita:</span><span class="sxs-lookup"><span data-stu-id="5553b-164">On hello **Basic Mode: Create Instance** page, you need to:</span></span>

    <span data-ttu-id="5553b-165">a.</span><span class="sxs-lookup"><span data-stu-id="5553b-165">a.</span></span> <span data-ttu-id="5553b-166">Especificar en **Name** el nombre de la instancia.</span><span class="sxs-lookup"><span data-stu-id="5553b-166">Enter an instance **Name**.</span></span>

    <span data-ttu-id="5553b-167">b.</span><span class="sxs-lookup"><span data-stu-id="5553b-167">b.</span></span> <span data-ttu-id="5553b-168">Seleccionar una **región** de Azure.</span><span class="sxs-lookup"><span data-stu-id="5553b-168">Select an Azure **Region**.</span></span> <span data-ttu-id="5553b-169">Puede que tenga un tooget de suscripción de CAL de SAP que ofrece varias regiones de Azure.</span><span class="sxs-lookup"><span data-stu-id="5553b-169">You might need an SAP CAL subscription tooget multiple Azure regions offered.</span></span>

    <span data-ttu-id="5553b-170">c.</span><span class="sxs-lookup"><span data-stu-id="5553b-170">c.</span></span>  <span data-ttu-id="5553b-171">Escriba master hello **contraseña** para la solución de hello, tal como se muestra:</span><span class="sxs-lookup"><span data-stu-id="5553b-171">Enter hello master **Password** for hello solution, as shown:</span></span>

    ![SAP CAL, Modo básico: crear instancia](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. <span data-ttu-id="5553b-173">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="5553b-173">Click **Create**.</span></span> <span data-ttu-id="5553b-174">Más tarde, según el tamaño de Hola y la complejidad de solución de hello (Hola CAL de SAP proporciona una estimación), Hola estado se muestra como activo y preparado para su uso:</span><span class="sxs-lookup"><span data-stu-id="5553b-174">After some time, depending on hello size and complexity of hello solution (hello SAP CAL provides an estimate), hello status is shown as active and ready for use:</span></span> 

    ![Instancias de SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. <span data-ttu-id="5553b-176">grupo de recursos de toofind hello y todos los objetos que se crearon Hola CAL de SAP, vaya toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="5553b-176">toofind hello resource group and all its objects that were created by hello SAP CAL, go toohello Azure portal.</span></span> <span data-ttu-id="5553b-177">máquina virtual de Hello puede encontrarse a partir de hello mismo nombre que se proporcionó en hello CAL de SAP de la instancia.</span><span class="sxs-lookup"><span data-stu-id="5553b-177">hello virtual machine can be found starting with hello same instance name that was given in hello SAP CAL.</span></span>

    ![Objetos del grupo de recursos](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. <span data-ttu-id="5553b-179">En el portal de SAP CAL hello, toohello implementado instancias y haga clic en **conectar**.</span><span class="sxs-lookup"><span data-stu-id="5553b-179">On hello SAP CAL portal, go toohello deployed instances and click **Connect**.</span></span> <span data-ttu-id="5553b-180">Hola después de la ventana emergente aparece:</span><span class="sxs-lookup"><span data-stu-id="5553b-180">hello following pop-up window appears:</span></span> 

    ![Conectar toohello instancia](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. <span data-ttu-id="5553b-182">Para poder usar uno de hello opciones tooconnect toohello implementado sistemas, haga clic en **Getting Started Guide**.</span><span class="sxs-lookup"><span data-stu-id="5553b-182">Before you can use one of hello options tooconnect toohello deployed systems, click **Getting Started Guide**.</span></span> <span data-ttu-id="5553b-183">nombres de la documentación de Hola Hola a los usuarios para cada uno de los métodos de conectividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="5553b-183">hello documentation names hello users for each of hello connectivity methods.</span></span> <span data-ttu-id="5553b-184">las contraseñas de Hola para los usuarios se establecen toohello contraseña maestra que ha definido al principio de Hola Hola del proceso de implementación.</span><span class="sxs-lookup"><span data-stu-id="5553b-184">hello passwords for those users are set toohello master password you defined at hello beginning of hello deployment process.</span></span> <span data-ttu-id="5553b-185">En la documentación de hello, otros usuarios más funcionales se muestran con sus contraseñas, que se pueden usar toosign en toohello implementa el sistema.</span><span class="sxs-lookup"><span data-stu-id="5553b-185">In hello documentation, other more functional users are listed with their passwords, which you can use toosign in toohello deployed system.</span></span>

    ![Documentación de bienvenida de SAP](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

<span data-ttu-id="5553b-187">En unas pocas horas, un sistema SAP IDES en buen estado se implementa en Azure.</span><span class="sxs-lookup"><span data-stu-id="5553b-187">Within a few hours, a healthy SAP IDES system is deployed in Azure.</span></span>

<span data-ttu-id="5553b-188">Si ha adquirido una suscripción de CAL de SAP, SAP admite totalmente las implementaciones a través de hello CAL de SAP en Azure.</span><span class="sxs-lookup"><span data-stu-id="5553b-188">If you bought an SAP CAL subscription, SAP fully supports deployments through hello SAP CAL on Azure.</span></span> <span data-ttu-id="5553b-189">cola de soporte técnico de Hello es BC-VCM-CAL.</span><span class="sxs-lookup"><span data-stu-id="5553b-189">hello support queue is BC-VCM-CAL.</span></span>

