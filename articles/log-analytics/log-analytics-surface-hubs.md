---
title: "Supervisión de Surface Hub con Azure Log Analytics | Microsoft Docs"
description: "Use la solución Surface Hub para realizar un seguimiento del estado de sus dispositivos con esta solución y comprender cómo se están utilizando."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 8b4e56bc-2d4f-4648-a236-16e9e732ebef
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b6ecd0d09589fec85c1633f528afc1165c346b7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="monitor-surface-hubs-with-log-analytics-to-track-their-health"></a><span data-ttu-id="633c3-103">Supervisión de Surface Hubs con Log Analytics para realizar un seguimiento de su estado</span><span class="sxs-lookup"><span data-stu-id="633c3-103">Monitor Surface Hubs with Log Analytics to track their health</span></span>

![Símbolo de Surface Hub](./media/log-analytics-surface-hubs/surface-hub-symbol.png)

<span data-ttu-id="633c3-105">Este artículo describe cómo puede usar la solución Surface Hub en Log Analytics para supervisar los dispositivos Microsoft Surface Hub con Microsoft Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="633c3-105">This article describes how you can use the Surface Hub solution in Log Analytics to monitor Microsoft Surface Hub devices with the Microsoft Operations Management Suite (OMS).</span></span> <span data-ttu-id="633c3-106">Log Analytics ayuda a realizar un seguimiento del estado de sus dispositivos con esta solución y comprender cómo se están utilizando.</span><span class="sxs-lookup"><span data-stu-id="633c3-106">Log Analytics helps you track the health of your Surface Hubs as well as understand how they are being used.</span></span>

<span data-ttu-id="633c3-107">Cada dispositivo Surface Hub tiene el agente de supervisión de Microsoft instalado.</span><span class="sxs-lookup"><span data-stu-id="633c3-107">Each Surface Hub has the Microsoft Monitoring Agent installed.</span></span> <span data-ttu-id="633c3-108">A través del agente se pueden enviar datos desde Surface Hub a OMS.</span><span class="sxs-lookup"><span data-stu-id="633c3-108">Its through the agent that you can send data from your Surface Hub to OMS.</span></span> <span data-ttu-id="633c3-109">Los archivos de registro se leen desde los dispositivos Surface Hub y se envían al servicio de OMS.</span><span class="sxs-lookup"><span data-stu-id="633c3-109">Log files are read from your Surface Hubs and are then are sent to the OMS service.</span></span> <span data-ttu-id="633c3-110">Los problemas (por ejemplo, que los servidores estén sin conexión, el calendario no se sincronice o la cuenta del dispositivo no pueda iniciar sesión en Skype) se muestran en OMS en el panel de Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="633c3-110">Issues like servers being offline, the calendar not syncing, or if the device account is unable to log into Skype are shown in OMS in the Surface Hub dashboard.</span></span> <span data-ttu-id="633c3-111">Mediante el uso de los datos en el panel, puede identificar los dispositivos que no se están ejecutando o que tienen otros problemas, así como, posiblemente aplicar correcciones para los problemas detectados.</span><span class="sxs-lookup"><span data-stu-id="633c3-111">By using the data in the dashboard, you can identify devices that are not running, or that are having other problems, and potentially apply fixes for the detected issues.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="633c3-112">Instalación y configuración de la solución</span><span class="sxs-lookup"><span data-stu-id="633c3-112">Installing and configuring the solution</span></span>
<span data-ttu-id="633c3-113">Utilice la siguiente información para instalar y configurar la solución.</span><span class="sxs-lookup"><span data-stu-id="633c3-113">Use the following information to install and configure the solution.</span></span> <span data-ttu-id="633c3-114">Para administrar sus dispositivos Surface Hub desde Microsoft Operations Management Suite (OMS), necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="633c3-114">In order to manage your Surface Hubs from the Microsoft Operations Management Suite (OMS), you'll need the following:</span></span>

* <span data-ttu-id="633c3-115">Una suscripción válida a [OMS](http://www.microsoft.com/oms).</span><span class="sxs-lookup"><span data-stu-id="633c3-115">A valid subscription to [OMS](http://www.microsoft.com/oms).</span></span>
* <span data-ttu-id="633c3-116">Un nivel de [suscripción a OMS](https://azure.microsoft.com/pricing/details/log-analytics/) que será admita el número de dispositivos que quiera supervisar.</span><span class="sxs-lookup"><span data-stu-id="633c3-116">An [OMS subscription](https://azure.microsoft.com/pricing/details/log-analytics/) level that will support the number of devices you want to monitor.</span></span> <span data-ttu-id="633c3-117">Los precios de OMS varían en función de cuántos dispositivos inscritos haya y de la cantidad de datos que se procesen.</span><span class="sxs-lookup"><span data-stu-id="633c3-117">OMS pricing varies depending on how many devices are enrolled, and how much data it processes.</span></span> <span data-ttu-id="633c3-118">Deberá tener esto en cuenta al planear la implementación de Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="633c3-118">You'll want to take this into consideration when planning your Surface Hub rollout.</span></span>

<span data-ttu-id="633c3-119">Después, agregará una suscripción de OMS a su suscripción de Microsoft Azure existente o creará una nueva área de trabajo directamente a través del portal de OMS.</span><span class="sxs-lookup"><span data-stu-id="633c3-119">Next, you will either add an OMS subscription to your existing Microsoft Azure subscription or create a new workspace directly through the OMS portal.</span></span> <span data-ttu-id="633c3-120">Las instrucciones detalladas para usar cualquiera de estos métodos se encuentran en el artículo de [introducción a Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="633c3-120">Detailed instructions for using either method is at [Get started with Log Analytics](log-analytics-get-started.md).</span></span> <span data-ttu-id="633c3-121">Una vez configurada la suscripción de OMS, hay dos formas de inscribir dispositivos Surface Hub:</span><span class="sxs-lookup"><span data-stu-id="633c3-121">Once the OMS subscription is set up, there are two ways to enroll your Surface Hub devices:</span></span>

* <span data-ttu-id="633c3-122">Automáticamente mediante Intune</span><span class="sxs-lookup"><span data-stu-id="633c3-122">Automatically through Intune</span></span>
* <span data-ttu-id="633c3-123">Manualmente a través de la aplicación **Configuración** del dispositivo Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="633c3-123">Manually through **Settings** on your Surface Hub device.</span></span>

## <a name="set-up-monitoring"></a><span data-ttu-id="633c3-124">Configuración de la supervisión</span><span class="sxs-lookup"><span data-stu-id="633c3-124">Set up monitoring</span></span>
<span data-ttu-id="633c3-125">Puede supervisar el estado y la actividad de su dispositivo Surface Hub usando Log Analytics de OMS.</span><span class="sxs-lookup"><span data-stu-id="633c3-125">You can monitor the health and activity of your Surface Hub using Log Analytics in OMS.</span></span> <span data-ttu-id="633c3-126">Puede inscribir el dispositivo Surface Hub en OMS mediante Intune o localmente con **Configuración** de Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="633c3-126">You can enroll the Surface Hub in OMS by using Intune, or locally by using **Settings** on the Surface Hub.</span></span>

## <a name="connect-surface-hubs-to-oms-through-intune"></a><span data-ttu-id="633c3-127">Conexión de dispositivos Surface Hub a OMS mediante Intune</span><span class="sxs-lookup"><span data-stu-id="633c3-127">Connect Surface Hubs to OMS through Intune</span></span>
<span data-ttu-id="633c3-128">Necesitará el identificador de área de trabajo y la clave de área de trabajo del área de trabajo de OMS que va a administrar sus dispositivos Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="633c3-128">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="633c3-129">Puede obtenerlos desde el portal de OMS.</span><span class="sxs-lookup"><span data-stu-id="633c3-129">You can get those from the OMS portal.</span></span>

<span data-ttu-id="633c3-130">Intune es un producto de Microsoft que permite administrar de forma centralizada la configuración de OMS que se aplica a uno o varios de los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="633c3-130">Intune is a Microsoft product that allows you to centrally manage the OMS configuration settings that are applied to one or more of your devices.</span></span> <span data-ttu-id="633c3-131">Siga estos pasos para configurar los dispositivos mediante Intune:</span><span class="sxs-lookup"><span data-stu-id="633c3-131">Follow these steps to configure your devices through Intune:</span></span>

1. <span data-ttu-id="633c3-132">Inicie sesión en Intune.</span><span class="sxs-lookup"><span data-stu-id="633c3-132">Sign in to Intune.</span></span>
2. <span data-ttu-id="633c3-133">Vaya a **Configuración** > **Orígenes conectados**.</span><span class="sxs-lookup"><span data-stu-id="633c3-133">Navigate to **Settings** > **Connected Sources**.</span></span>
3. <span data-ttu-id="633c3-134">Cree o edite una directiva basada en la plantilla de Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="633c3-134">Create or edit a policy based on the Surface Hub template.</span></span>
4. <span data-ttu-id="633c3-135">Vaya a la sección de OMS (Azure Operational Insights) de la directiva y agregue el *identificador de área de trabajo* y la *clave de área de trabajo* a la directiva.</span><span class="sxs-lookup"><span data-stu-id="633c3-135">Navigate to the OMS (Azure Operational Insights) section of the policy, and add the *Workspace ID* and *Workspace Key* to the policy.</span></span>
5. <span data-ttu-id="633c3-136">Guarde la directiva.</span><span class="sxs-lookup"><span data-stu-id="633c3-136">Save the policy.</span></span>
6. <span data-ttu-id="633c3-137">Asocia la directiva con el grupo de dispositivos adecuado.</span><span class="sxs-lookup"><span data-stu-id="633c3-137">Associate the policy with the appropriate group of devices.</span></span>

   ![Directiva de Intune](./media/log-analytics-surface-hubs/intune.png)

<span data-ttu-id="633c3-139">Después, Intune sincroniza la configuración de OMS con los dispositivos en el grupo de destino, con lo que se inscriben en el área de trabajo de OMS.</span><span class="sxs-lookup"><span data-stu-id="633c3-139">Intune then syncs the OMS settings with the devices in the target group, enrolling them in your OMS workspace.</span></span>

## <a name="connect-surface-hubs-to-oms-using-the-settings-app"></a><span data-ttu-id="633c3-140">Conexión de los dispositivos Surface Hub a OMS a través de la aplicación Configuración</span><span class="sxs-lookup"><span data-stu-id="633c3-140">Connect Surface Hubs to OMS using the Settings app</span></span>
<span data-ttu-id="633c3-141">Necesitará el identificador de área de trabajo y la clave de área de trabajo del área de trabajo de OMS que va a administrar sus dispositivos Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="633c3-141">You'll need the workspace ID and workspace key for the OMS workspace that will manage your Surface Hubs.</span></span> <span data-ttu-id="633c3-142">Puede obtenerlos desde el portal de OMS.</span><span class="sxs-lookup"><span data-stu-id="633c3-142">You can get those from the OMS portal.</span></span>

<span data-ttu-id="633c3-143">Si no usa Intune para administrar su entorno, puede inscribir dispositivos manualmente con **Configuración** en cada dispositivo Surface Hub:</span><span class="sxs-lookup"><span data-stu-id="633c3-143">If you don't use Intune to manage your environment, you can enroll devices manually through **Settings** on each Surface Hub:</span></span>

1. <span data-ttu-id="633c3-144">En Surface Hub, abra **Configuración**.</span><span class="sxs-lookup"><span data-stu-id="633c3-144">From your Surface Hub, open **Settings**.</span></span>
2. <span data-ttu-id="633c3-145">Escriba las credenciales de administrador de dispositivos cuando se le solicite.</span><span class="sxs-lookup"><span data-stu-id="633c3-145">Enter the device admin credentials when prompted.</span></span>
3. <span data-ttu-id="633c3-146">Haga clic en **Este dispositivo** y, en **Supervisión**, haga clic en **Configure OMS Settings** (Configuración de OMS).</span><span class="sxs-lookup"><span data-stu-id="633c3-146">Click **This device**, and the under **Monitoring**, click **Configure OMS Settings**.</span></span>
4. <span data-ttu-id="633c3-147">Seleccione **Habilitar supervisión**.</span><span class="sxs-lookup"><span data-stu-id="633c3-147">Select **Enable monitoring**.</span></span>
5. <span data-ttu-id="633c3-148">En el cuadro de diálogo de configuración de OMS, escriba el **identificador de área de trabajo** y escriba la **clave de área de trabajo**.</span><span class="sxs-lookup"><span data-stu-id="633c3-148">In the OMS settings dialog, type the **Workspace ID** and type the **Workspace Key**.</span></span>  
   <span data-ttu-id="633c3-149">![settings](./media/log-analytics-surface-hubs/settings.png)</span><span class="sxs-lookup"><span data-stu-id="633c3-149">![settings](./media/log-analytics-surface-hubs/settings.png)</span></span>
6. <span data-ttu-id="633c3-150">Haga clic en **Aceptar** para completar la configuración.</span><span class="sxs-lookup"><span data-stu-id="633c3-150">Click **OK** to complete the configuration.</span></span>

<span data-ttu-id="633c3-151">Aparecerá una confirmación que indica si la configuración de OMS se aplicó correctamente en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="633c3-151">A confirmation appears telling you whether or not the OMS configuration was successfully applied to the device.</span></span> <span data-ttu-id="633c3-152">Si es así, aparecerá un mensaje que indica que el agente se ha conectado correctamente al servicio de OMS.</span><span class="sxs-lookup"><span data-stu-id="633c3-152">If it was, a message appears stating that the agent successfully connected to the OMS service.</span></span> <span data-ttu-id="633c3-153">El dispositivo comienza a enviar datos a OMS, donde puede verlos y utilizarlos.</span><span class="sxs-lookup"><span data-stu-id="633c3-153">The device then starts sending data to OMS where you can view and act on it.</span></span>

## <a name="monitor-surface-hubs"></a><span data-ttu-id="633c3-154">Supervisión de dispositivos Surface Hub</span><span class="sxs-lookup"><span data-stu-id="633c3-154">Monitor Surface Hubs</span></span>
<span data-ttu-id="633c3-155">La supervisión de los dispositivos Surface Hubs con OMS es muy similar a la de todos los demás dispositivos inscritos.</span><span class="sxs-lookup"><span data-stu-id="633c3-155">Monitoring your Surface Hubs using OMS is much like monitoring any other enrolled devices.</span></span>

1. <span data-ttu-id="633c3-156">Inicie sesión en el portal de OMS.</span><span class="sxs-lookup"><span data-stu-id="633c3-156">Sign in to the OMS portal.</span></span>
2. <span data-ttu-id="633c3-157">Desplácese hasta el panel de paquete de solución Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="633c3-157">Navigate to the Surface Hub solution pack dashboard.</span></span>
3. <span data-ttu-id="633c3-158">Se muestra el estado del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="633c3-158">Your device's health is displayed.</span></span>

   ![Panel de Surface Hub](./media/log-analytics-surface-hubs/surface-hub-dashboard.png)

<span data-ttu-id="633c3-160">Puede crear [alertas](log-analytics-alerts.md) en función de las búsquedas de registros existentes o personalizadas.</span><span class="sxs-lookup"><span data-stu-id="633c3-160">You can create [alerts](log-analytics-alerts.md) based on existing or custom log searches.</span></span> <span data-ttu-id="633c3-161">Con los datos que recopile OMS de los dispositivos Surface Hub, puede buscar problemas y generar alertas sobre las condiciones que defina para sus dispositivos.</span><span class="sxs-lookup"><span data-stu-id="633c3-161">Using the data the OMS collects from your Surface Hubs, you can search for issues and alert on the conditions that you define for your devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="633c3-162">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="633c3-162">Next steps</span></span>
* <span data-ttu-id="633c3-163">Use [Búsquedas de registros en Log Analytics](log-analytics-log-searches.md) para ver datos detallados de Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="633c3-163">Use [Log searches in Log Analytics](log-analytics-log-searches.md) to view detailed Surface Hub data.</span></span>
* <span data-ttu-id="633c3-164">Cree [alertas](log-analytics-alerts.md) para recibir una notificación cuando se produzcan problemas con Surface Hub.</span><span class="sxs-lookup"><span data-stu-id="633c3-164">Create [alerts](log-analytics-alerts.md) to notify you when issues occur with your Surface Hubs.</span></span>
