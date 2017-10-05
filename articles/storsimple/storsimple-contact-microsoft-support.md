---
title: "Registro de un vale de soporte técnico para la serie 8000 de StorSimple | Microsoft Docs"
description: "Aprenda a crear una solicitud de soporte técnico y a iniciar una sesión de soporte técnico en su dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 2ebc20fe-f490-4749-8e43-c9fac86f1676
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/27/2017
ms.author: alkohli;anbacker
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cecc2566b432e897b5eff0c12e66598f0518ed80
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="contact-microsoft-support-for-your-storsimple"></a><span data-ttu-id="feb8b-103">Contacto con el soporte técnico de Microsoft para StorSimple</span><span class="sxs-lookup"><span data-stu-id="feb8b-103">Contact Microsoft Support for your StorSimple</span></span>
<span data-ttu-id="feb8b-104">Si tiene algún problema con la solución de Microsoft Azure StorSimple, puede crear una solicitud de servicio de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="feb8b-104">If you encounter any issues with your Microsoft Azure StorSimple solution, you can create a service request for technical support.</span></span> <span data-ttu-id="feb8b-105">En una sesión en línea con su ingeniero de soporte técnico, también deberá iniciar una sesión de soporte técnico en su dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="feb8b-105">In an online session with your support engineer, you may also need to start a support session on your StorSimple device.</span></span> <span data-ttu-id="feb8b-106">Este artículo le enseñará a:</span><span class="sxs-lookup"><span data-stu-id="feb8b-106">This article walks you through:</span></span>

* <span data-ttu-id="feb8b-107">Crear una solicitud de soporte.</span><span class="sxs-lookup"><span data-stu-id="feb8b-107">How to create a support request.</span></span>
* <span data-ttu-id="feb8b-108">Iniciar una sesión de soporte en la interfaz de Windows PowerShell del dispositivo de StorSimple.</span><span class="sxs-lookup"><span data-stu-id="feb8b-108">How to start a support session in the Windows PowerShell interface of your StorSimple device.</span></span>

<span data-ttu-id="feb8b-109">Revise la sección [Información y contratos de nivel de servicio de soporte de la serie StorSimple 8000](https://msdn.microsoft.com/library/mt433077.aspx) antes de crear una solicitud de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="feb8b-109">Review the [StorSimple 8000 Series Support SLAs and information](https://msdn.microsoft.com/library/mt433077.aspx) before you create a Support request.</span></span>

## <a name="create-a-support-request"></a><span data-ttu-id="feb8b-110">Crear una solicitud de soporte</span><span class="sxs-lookup"><span data-stu-id="feb8b-110">Create a support request</span></span>
<span data-ttu-id="feb8b-111">Lleve a cabo los siguientes pasos para crear una solicitud de soporte.</span><span class="sxs-lookup"><span data-stu-id="feb8b-111">Perform the following steps to create a support request:</span></span>

#### <a name="to-create-a-support-request"></a><span data-ttu-id="feb8b-112">Para crear una solicitud de soporte</span><span class="sxs-lookup"><span data-stu-id="feb8b-112">To create a support request</span></span>
1. <span data-ttu-id="feb8b-113">En el [Portal de Azure clásico](https://manage.windowsazure.com/), haga clic en el extremo superior derecho, en el nombre de cuenta y, a continuación, haga clic en **Póngase en contacto con el Soporte técnico de Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="feb8b-113">In the [Azure classic portal](https://manage.windowsazure.com/), in the upper right corner, click your account name and then click **Contact Microsoft Support**.</span></span>
   
    ![Ponerse en contacto con el soporte técnico de MS a través del Portal de administración](./media/storsimple-contact-microsoft-support/Ibiza1.png)
2. <span data-ttu-id="feb8b-115">Se le redirigirá al nuevo Portal de Azure (portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="feb8b-115">You will be redirected to the new Azure portal (portal.azure.com).</span></span> <span data-ttu-id="feb8b-116">Haga clic en el icono **Nueva solicitud de soporte técnico** .</span><span class="sxs-lookup"><span data-stu-id="feb8b-116">Click the **New support request** tile.</span></span>
   
    ![Ponerse en contacto con el soporte técnico de MS a través del nuevo portal](./media/storsimple-contact-microsoft-support/Ibiza2.png)
   
    <span data-ttu-id="feb8b-118">En el lado derecho de la pantalla, aparecerá el panel **Nueva solicitud de soporte técnico** .</span><span class="sxs-lookup"><span data-stu-id="feb8b-118">On the right side of the screen, the **New support request** pane appears.</span></span> 
   
    ![Panel Nueva solicitud de soporte](./media/storsimple-contact-microsoft-support/Ibiza3a.png)
3. <span data-ttu-id="feb8b-120">En el cuadro de diálogo **Aspectos básicos** , haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="feb8b-120">In the **Basics** dialog box, complete the following:</span></span>                                
   
   1. <span data-ttu-id="feb8b-121">En la lista desplegable **Tipo de problema**, seleccione **Técnico**.</span><span class="sxs-lookup"><span data-stu-id="feb8b-121">From the **Issue type** drop-down list , select **Technical**.</span></span>
   2. <span data-ttu-id="feb8b-122">Seleccione una **Suscripción** en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="feb8b-122">Select a **Subscription** from the drop-down list.</span></span>
   3. <span data-ttu-id="feb8b-123">En la lista desplegable **Servicio**, seleccione **StorSimple**.</span><span class="sxs-lookup"><span data-stu-id="feb8b-123">From the **Service** drop-down list, select **StorSimple**.</span></span> 
   4. <span data-ttu-id="feb8b-124">Seleccione un **Plan de soporte técnico** en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="feb8b-124">Select a **Support plan** from the drop-down list.</span></span> <span data-ttu-id="feb8b-125">Para habilitar el soporte técnico, debe contar con un plan de soporte técnico de pago.</span><span class="sxs-lookup"><span data-stu-id="feb8b-125">You need a paid support plan to enable Technical Support.</span></span>
4. <span data-ttu-id="feb8b-126">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="feb8b-126">Click **Next**.</span></span> <span data-ttu-id="feb8b-127">Aparecerá el cuadro de diálogo **Problema** .</span><span class="sxs-lookup"><span data-stu-id="feb8b-127">The **Problem** dialog box appears.</span></span>
   
    ![Panel Nueva solicitud de soporte](./media/storsimple-contact-microsoft-support/Ibiza5a.png) 
5. <span data-ttu-id="feb8b-129">En el cuadro de diálogo **Problema** , haga lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="feb8b-129">In the **Problem** dialog box, complete the following:</span></span>
   
   1. <span data-ttu-id="feb8b-130">Seleccione un nivel de **Gravedad** en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="feb8b-130">Select a **Severity** level from the drop-down list.</span></span>
   2. <span data-ttu-id="feb8b-131">Seleccione un **Tipo de problema** en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="feb8b-131">Select a **Problem type** from the drop-down list.</span></span>
   3. <span data-ttu-id="feb8b-132">Seleccione una **Categoría** en la lista desplegable.</span><span class="sxs-lookup"><span data-stu-id="feb8b-132">Select a **Category** from the drop-down list.</span></span> 
   4. <span data-ttu-id="feb8b-133">En el campo **Detalles** , escriba una descripción breve del problema.</span><span class="sxs-lookup"><span data-stu-id="feb8b-133">In the **Details** box, briefly describe your issue.</span></span>
   5. <span data-ttu-id="feb8b-134">En el cuadro **Período de tiempo** , indique la fecha, la hora y la zona horaria correspondiente a la aparición más reciente del problema.</span><span class="sxs-lookup"><span data-stu-id="feb8b-134">In the **Time frame** box, indicate the date, time, and time zone that corresponds to the most recent occurrence of your issue.</span></span>
   6. <span data-ttu-id="feb8b-135">En **Carga de archivos**, haga clic en el icono de carpeta para buscar el paquete de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="feb8b-135">Under **File upload**, click the folder icon to browse to your support package.</span></span>
   7. <span data-ttu-id="feb8b-136">Seleccione la casilla de verificación **Compartir información de diagnóstico** .</span><span class="sxs-lookup"><span data-stu-id="feb8b-136">Select the **Share diagnostic information** check box.</span></span>
6. <span data-ttu-id="feb8b-137">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="feb8b-137">Click **Next**.</span></span> <span data-ttu-id="feb8b-138">Aparecerá el cuadro de diálogo **Información de contacto** .</span><span class="sxs-lookup"><span data-stu-id="feb8b-138">The **Contact information** dialog box appears.</span></span>
   
    ![Panel Nueva solicitud de soporte](./media/storsimple-contact-microsoft-support/Ibiza6a.png) 
7. <span data-ttu-id="feb8b-140">Escriba la información de contacto y seleccione un método de contacto (teléfono o correo electrónico).</span><span class="sxs-lookup"><span data-stu-id="feb8b-140">Enter your contact information and select a contact method (phone or email).</span></span> 
8. <span data-ttu-id="feb8b-141">Seleccione la casilla de verificación **Guardar cambios de contacto para solicitudes futuras de soporte técnico** .</span><span class="sxs-lookup"><span data-stu-id="feb8b-141">Select the **Save contact changes for future support requests** check box.</span></span>
9. <span data-ttu-id="feb8b-142">Haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="feb8b-142">Click **Create**.</span></span>

<span data-ttu-id="feb8b-143">Una vez que ha enviado la solicitud, un ingeniero de soporte se pondrá en contacto con usted tan pronto como sea posible para procesar su solicitud.</span><span class="sxs-lookup"><span data-stu-id="feb8b-143">After you have submitted your request, a Support engineer will contact you as soon as possible to proceed with your request.</span></span>

## <a name="start-a-support-session-in-windows-powershell-for-storsimple"></a><span data-ttu-id="feb8b-144">Iniciar una sesión de soporte en Windows PowerShell para StorSimple</span><span class="sxs-lookup"><span data-stu-id="feb8b-144">Start a support session in Windows PowerShell for StorSimple</span></span>
<span data-ttu-id="feb8b-145">Para solucionar los problemas que pudiera experimentar con el dispositivo StorSimple, deberá ponerse en contacto con el equipo de soporte técnico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="feb8b-145">To troubleshoot any issues that you might experience with the StorSimple device, you will need to engage with the Microsoft Support team.</span></span> <span data-ttu-id="feb8b-146">Es posible que el soporte técnico de Microsoft necesite utilizar una sesión de soporte para iniciar sesión en su dispositivo.</span><span class="sxs-lookup"><span data-stu-id="feb8b-146">Microsoft Support may need to use a support session to log on to your device.</span></span> 

<span data-ttu-id="feb8b-147">Lleve a cabo los siguientes pasos para iniciar una sesión de soporte.</span><span class="sxs-lookup"><span data-stu-id="feb8b-147">Perform the following steps to start a support session:</span></span>

#### <a name="to-start-a-support-session"></a><span data-ttu-id="feb8b-148">Para iniciar una sesión de soporte</span><span class="sxs-lookup"><span data-stu-id="feb8b-148">To start a support session</span></span>
1. <span data-ttu-id="feb8b-149">Acceda al dispositivo directamente desde la consola serie o a través de una sesión de telnet desde un equipo remoto.</span><span class="sxs-lookup"><span data-stu-id="feb8b-149">Access the device directly by using the serial console or through a telnet session from a remote computer.</span></span> <span data-ttu-id="feb8b-150">Para ello, siga los pasos descritos en [Uso de PuTTy para conectarse a la consola serie del dispositivo](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="feb8b-150">To do this, follow the steps in [Use PuTTY to connect to the device serial console](storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span>
2. <span data-ttu-id="feb8b-151">En la sesión que se abre, presione la tecla **Intro** para obtener un símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="feb8b-151">In the session that opens, press the **Enter** key to get a command prompt.</span></span>
3. <span data-ttu-id="feb8b-152">En el menú de la consola serie, seleccione la opción 1, **iniciar sesión con acceso completo**.</span><span class="sxs-lookup"><span data-stu-id="feb8b-152">In the serial console menu, select option 1, **Log in with full access**.</span></span>
4. <span data-ttu-id="feb8b-153">En el símbolo del sistema, escriba la siguiente contraseña:</span><span class="sxs-lookup"><span data-stu-id="feb8b-153">At the prompt, type the following password:</span></span> 
   
    `Password1`
5. <span data-ttu-id="feb8b-154">En el símbolo del sistema, escriba el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="feb8b-154">At the prompt, type the following command:</span></span>
   
    `Enable-HcsSupportAccess`
6. <span data-ttu-id="feb8b-155">Aparecerá una cadena cifrada.</span><span class="sxs-lookup"><span data-stu-id="feb8b-155">An encrypted string will be presented to you.</span></span> <span data-ttu-id="feb8b-156">Copie esta cadena en un editor de texto como el Bloc de notas.</span><span class="sxs-lookup"><span data-stu-id="feb8b-156">Copy this string into a text editor such as Notepad.</span></span>
7. <span data-ttu-id="feb8b-157">Guarde esta cadena y envíela por correo electrónico al soporte técnico de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="feb8b-157">Save this string and send it in an email message to Microsoft Support.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="feb8b-158">Puede deshabilitar el acceso al soporte técnico ejecutando `Disable-HcsSupportAccess`.</span><span class="sxs-lookup"><span data-stu-id="feb8b-158">You can disable support access by running `Disable-HcsSupportAccess`.</span></span> <span data-ttu-id="feb8b-159">El dispositivo StorSimple también intenta deshabilitar el acceso al soporte técnico 8 horas después de iniciada la sesión.</span><span class="sxs-lookup"><span data-stu-id="feb8b-159">The StorSimple device will also attempt to disable support access 8 hours after the session was initiated.</span></span> <span data-ttu-id="feb8b-160">Es un procedimiento recomendado cambiar las credenciales de su dispositivo StorSimple después de una sesión de soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="feb8b-160">It is a best practice to change your StorSimple device credentials after initiating a support session.</span></span>
> 
> 

