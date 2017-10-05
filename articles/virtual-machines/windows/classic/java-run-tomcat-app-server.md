---
title: "Ejecución de un servidor de aplicaciones Java en una máquina virtual de Azure clásico | Microsoft Docs"
description: "En este tutorial se usan los recursos creados con el modelo de implementación clásico, y se muestra cómo crear una máquina virtual Windows y configurarla para ejecutar el servidor de aplicaciones de Apache Tomcat."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 6e02f42613808bcb13c0057e9f8fcc1c02273e77
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-run-a-java-application-server-on-a-virtual-machine-created-with-the-classic-deployment-model"></a><span data-ttu-id="03505-103">Ejecución de un servidor de aplicaciones Java en una máquina virtual creada con el modelo de implementación clásico</span><span class="sxs-lookup"><span data-stu-id="03505-103">How to run a Java application server on a virtual machine created with the classic deployment model</span></span>
> [!IMPORTANT]
> <span data-ttu-id="03505-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="03505-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="03505-105">En este artículo se trata el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="03505-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="03505-106">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="03505-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="03505-107">Para obtener una plantilla de Resource Manager para implementar una aplicación web con Java 8 y Tomcat, consulte [aquí](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span><span class="sxs-lookup"><span data-stu-id="03505-107">For a Resource Manager template to deploy a webapp with Java 8 and Tomcat, see [here](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).</span></span>

<span data-ttu-id="03505-108">Con Azure, puede utilizar una máquina virtual para proporcionar funciones de servidor.</span><span class="sxs-lookup"><span data-stu-id="03505-108">With Azure, you can use a virtual machine to provide server capabilities.</span></span> <span data-ttu-id="03505-109">Por ejemplo, una máquina virtual que se ejecuta en Azure se puede configurar para hospedar un servidor de aplicaciones Java, como Apache Tomcat.</span><span class="sxs-lookup"><span data-stu-id="03505-109">As an example, a virtual machine running on Azure can be configured to host a Java application server, such as Apache Tomcat.</span></span>

<span data-ttu-id="03505-110">Después de finalizar esta guía, adquirirá una comprensión de cómo crear una máquina virtual que se ejecute en Azure y configurarla para ejecutar un servidor de aplicaciones Java.</span><span class="sxs-lookup"><span data-stu-id="03505-110">After completing this guide, you will have an understanding of how to create a virtual machine running on Azure and configure it to run a Java application server.</span></span> <span data-ttu-id="03505-111">Aprenderá a realizar las siguientes tareas:</span><span class="sxs-lookup"><span data-stu-id="03505-111">You will learn and perform the following tasks:</span></span>

* <span data-ttu-id="03505-112">Crear una máquina virtual que tenga un kit de desarrollo de Java (JDK) ya instalado.</span><span class="sxs-lookup"><span data-stu-id="03505-112">How to create a virtual machine that has a Java Development Kit (JDK) already installed.</span></span>
* <span data-ttu-id="03505-113">Iniciar sesión de manera remota en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="03505-113">How to remotely sign in to your virtual machine.</span></span>
* <span data-ttu-id="03505-114">Instalar un servidor de aplicaciones Java, Apache Tomcat, en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="03505-114">How to install a Java application server--Apache Tomcat--on your virtual machine.</span></span>
* <span data-ttu-id="03505-115">Crear un extremo para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="03505-115">How to create an endpoint for your virtual machine.</span></span>
* <span data-ttu-id="03505-116">Abrir un puerto en el firewall para el servidor de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="03505-116">How to open a port in the firewall for your application server.</span></span>

<span data-ttu-id="03505-117">Los resultados de la instalación completos cuando se ejecuta Tomcat en una máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="03505-117">The completed installation results in Tomcat running on a virtual machine.</span></span>

![Máquina virtual que ejecuta Apache Tomcat][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="to-create-a-virtual-machine"></a><span data-ttu-id="03505-119">Para crear una máquina virtual</span><span class="sxs-lookup"><span data-stu-id="03505-119">To create a virtual machine</span></span>
1. <span data-ttu-id="03505-120">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="03505-120">Sign in to the [Azure portal](https://portal.azure.com).</span></span>  
2. <span data-ttu-id="03505-121">Haga clic en **Nuevo**, en **Proceso** y, a continuación en **Ver todo** en **Aplicaciones destacadas**.</span><span class="sxs-lookup"><span data-stu-id="03505-121">Click **New**, click **Compute**, then click **See all** in the **Featured apps**.</span></span>
3. <span data-ttu-id="03505-122">Haga clic en **JDK** y en **JDK 8** en el panel **JDK**.</span><span class="sxs-lookup"><span data-stu-id="03505-122">Click **JDK**, click **JDK 8** in the **JDK** pane.</span></span>  
   <span data-ttu-id="03505-123">Las imágenes de máquina virtual que son compatibles con **JDK 6** y **JDK 7** se encuentran disponibles si dispone de aplicaciones heredadas que no están preparadas para ejecutarse en JDK 8.</span><span class="sxs-lookup"><span data-stu-id="03505-123">Virtual machine images that support **JDK 6** and **JDK 7** are available if you have legacy applications that are not ready to run in JDK 8.</span></span>
4. <span data-ttu-id="03505-124">En el panel de JDK 8, seleccione **Clásico** y, a continuación, haga clic en **Crear**.</span><span class="sxs-lookup"><span data-stu-id="03505-124">In the JDK 8 pane, select **Classic**, then click **Create**.</span></span>
5. <span data-ttu-id="03505-125">En la hoja **Básico**:</span><span class="sxs-lookup"><span data-stu-id="03505-125">In the **Basics** blade:</span></span>
   1. <span data-ttu-id="03505-126">Especifique un nombre para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="03505-126">Specify a name for the virtual machine.</span></span>
   2. <span data-ttu-id="03505-127">Escriba un nombre para el administrador en el campo **Nombre de usuario** .</span><span class="sxs-lookup"><span data-stu-id="03505-127">Enter a name for the administrator in the **User Name** field.</span></span> <span data-ttu-id="03505-128">Recuerde este nombre y la contraseña asociada que aparece en el siguiente campo.</span><span class="sxs-lookup"><span data-stu-id="03505-128">Remember this name and the associated password that follows in the next field.</span></span> <span data-ttu-id="03505-129">Las necesitará cuando inicie sesión de forma remota en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="03505-129">You need them when you remotely sign in to the virtual machine.</span></span>
   3. <span data-ttu-id="03505-130">Escriba una contraseña en el campo **New password** (Contraseña nueva) y confírmela en el campo **Confirm password** (Confirmar contraseña).</span><span class="sxs-lookup"><span data-stu-id="03505-130">Enter a password in the **New password** field, and reenter it in the **Confirm password** field.</span></span> <span data-ttu-id="03505-131">Esta es la contraseña de la cuenta de administrador.</span><span class="sxs-lookup"><span data-stu-id="03505-131">This password is for the Administrator account.</span></span>
   4. <span data-ttu-id="03505-132">Seleccione la **suscripción**adecuada.</span><span class="sxs-lookup"><span data-stu-id="03505-132">Select the appropriate **Subscription**.</span></span>
   5. <span data-ttu-id="03505-133">Para el **Grupo de recursos**, haga clic en **Crear nuevo** y especifique el nombre de un nuevo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="03505-133">For the **Resource group**, click **Create new** and enter the name of a new resource group.</span></span> <span data-ttu-id="03505-134">También puede hacer clic en **Usar existente** y seleccionar uno de los grupos de recursos disponibles.</span><span class="sxs-lookup"><span data-stu-id="03505-134">Or, click **Use existing** and select one of the available resource groups.</span></span>
   6. <span data-ttu-id="03505-135">Seleccione una ubicación en la que esté la máquina virtual, como **Centro-sur de EE. UU**.</span><span class="sxs-lookup"><span data-stu-id="03505-135">Select a location where the virtual machine resides, such as **South Central US**.</span></span>
6. <span data-ttu-id="03505-136">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="03505-136">Click **Next**.</span></span>
7. <span data-ttu-id="03505-137">En la hoja **Tamaño de la imagen de máquina virtual**, seleccione **Estándar A1** o cualquier otra imagen apropiada.</span><span class="sxs-lookup"><span data-stu-id="03505-137">In the **Virtual machine image size** blade, select **A1 Standard** or another appropriate image.</span></span>
8. <span data-ttu-id="03505-138">Haga clic en **Seleccionar**.</span><span class="sxs-lookup"><span data-stu-id="03505-138">Click **Select**.</span></span>

9. <span data-ttu-id="03505-139">En la hoja **Configuración**, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="03505-139">In the **Settings** blade, click **OK**.</span></span> <span data-ttu-id="03505-140">Puede usar los valores predeterminados proporcionados por Azure.</span><span class="sxs-lookup"><span data-stu-id="03505-140">You can use the default values provided by Azure.</span></span>  
10. <span data-ttu-id="03505-141">En la hoja **Resumen**, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="03505-141">In the **Summary** blade, click **OK**.</span></span>

## <a name="to-remotely-sign-in-to-your-virtual-machine"></a><span data-ttu-id="03505-142">Para iniciar sesión de manera remota en la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="03505-142">To remotely sign in to your virtual machine</span></span>
1. <span data-ttu-id="03505-143">Inicie sesión en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="03505-143">Log on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="03505-144">Haga clic en **Virtual Machines (clásico)**.</span><span class="sxs-lookup"><span data-stu-id="03505-144">Click **Virtual machines (classic)**.</span></span> <span data-ttu-id="03505-145">Si es necesario, haga clic en **Más servicios** en la esquina inferior izquierda en las categorías de servicio.</span><span class="sxs-lookup"><span data-stu-id="03505-145">If needed, click **More services** at the bottom left corner under the service categories.</span></span> <span data-ttu-id="03505-146">La entrada **Virtual Machines (clásico)** aparece en el grupo **Proceso**.</span><span class="sxs-lookup"><span data-stu-id="03505-146">The **Virtual machines (classic)** entry is listed in the **Compute** group.</span></span>
3. <span data-ttu-id="03505-147">Haga clic en el nombre de la máquina virtual en la que desea iniciar sesión.</span><span class="sxs-lookup"><span data-stu-id="03505-147">Click the name of the virtual machine that you want to sign in to.</span></span>
4. <span data-ttu-id="03505-148">Una vez que la máquina virtual se haya iniciado, aparecerá un menú en la parte superior del panel que permitirá las conexiones.</span><span class="sxs-lookup"><span data-stu-id="03505-148">After the virtual machine has started, a menu at the top of the pane allows connections.</span></span>
5. <span data-ttu-id="03505-149">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="03505-149">Click **Connect**.</span></span>
6. <span data-ttu-id="03505-150">Siga las indicaciones, según sea necesario, para conectarse a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="03505-150">Respond to the prompts as needed to connect to the virtual machine.</span></span> <span data-ttu-id="03505-151">Normalmente, debe guardar o abrir el archivo .rdp que contiene los detalles de conexión.</span><span class="sxs-lookup"><span data-stu-id="03505-151">Typically, you save or open the .rdp file that contains the connection details.</span></span> <span data-ttu-id="03505-152">Es posible que tenga que copiar el valor de url:port de la parte final de la primera línea del archivo .rdp y pegarlo en una aplicación remota de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="03505-152">You might have to copy the url:port as the last part of the first line of the .rdp file and paste it in a remote sign-in application.</span></span>

## <a name="to-install-a-java-application-server-on-your-virtual-machine"></a><span data-ttu-id="03505-153">Para instalar un servidor de aplicaciones Java en la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="03505-153">To install a Java application server on your virtual machine</span></span>
<span data-ttu-id="03505-154">Puede copiar un servidor de aplicaciones Java en la máquina virtual o instalarlo a través de un instalador.</span><span class="sxs-lookup"><span data-stu-id="03505-154">You can copy a Java application server to your virtual machine, or you can install a Java application server through an installer.</span></span>

<span data-ttu-id="03505-155">Este tutorial usa Tomcat como servidor de la aplicación de Java que instalar.</span><span class="sxs-lookup"><span data-stu-id="03505-155">This tutorial uses Tomcat as the Java application server to install.</span></span>

1. <span data-ttu-id="03505-156">Cuando haya iniciado sesión en la máquina virtual, abra una sesión del explorador en [Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span><span class="sxs-lookup"><span data-stu-id="03505-156">When you are signed in to your virtual machine, open a browser session to [Apache Tomcat](http://tomcat.apache.org/download-80.cgi).</span></span>
2. <span data-ttu-id="03505-157">Haga doble clic en el vínculo del **instalador del servicio de Windows de 32 bits y 64 bits**.</span><span class="sxs-lookup"><span data-stu-id="03505-157">Double-click the link for **32-bit/64-bit Windows Service Installer**.</span></span> <span data-ttu-id="03505-158">Mediante esta técnica, Tomcat se instala como servicio de Windows.</span><span class="sxs-lookup"><span data-stu-id="03505-158">By using this technique, Tomcat installs as a Windows service.</span></span>
3. <span data-ttu-id="03505-159">Cuando se le pida, elija ejecutar el instalador.</span><span class="sxs-lookup"><span data-stu-id="03505-159">When prompted, choose to run the installer.</span></span>
4. <span data-ttu-id="03505-160">En el asistente para la **instalación de Apache Tomcat** , siga las indicaciones para instalar Tomcat.</span><span class="sxs-lookup"><span data-stu-id="03505-160">Within the **Apache Tomcat Setup** wizard, follow the prompts to install Tomcat.</span></span> <span data-ttu-id="03505-161">En este tutorial, es adecuado aceptar los valores predeterminados.</span><span class="sxs-lookup"><span data-stu-id="03505-161">For the purposes of this tutorial, accepting the defaults is fine.</span></span> <span data-ttu-id="03505-162">Cuando llegue al cuadro de diálogo **Completing the Apache Tomcat Setup Wizard** (Finalización del asistente para la instalación de Apache Tomcat), si lo desea, puede activar **Run Apache Tomcat** (Ejecutar Apache Tomcat) para iniciar Tomcat ahora.</span><span class="sxs-lookup"><span data-stu-id="03505-162">When you reach the **Completing the Apache Tomcat Setup Wizard** dialog box, you can optionally check **Run Apache Tomcat** to have Tomcat start now.</span></span> <span data-ttu-id="03505-163">Haga clic en **Finalizar** para finalizar el proceso de instalación de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="03505-163">Click **Finish** to complete the Tomcat setup process.</span></span>

## <a name="to-start-tomcat"></a><span data-ttu-id="03505-164">Para iniciar Tomcat</span><span class="sxs-lookup"><span data-stu-id="03505-164">To start Tomcat</span></span>

<span data-ttu-id="03505-165">Puede iniciar manualmente Tomcat abriendo un símbolo del sistema en la máquina virtual y ejecutando el comando **net&nbsp;start&nbsp;Tomcat8**.</span><span class="sxs-lookup"><span data-stu-id="03505-165">You can manually start Tomcat by opening a command prompt on your virtual machine and running the command **net&nbsp;start&nbsp;Tomcat8**.</span></span>

<span data-ttu-id="03505-166">Una vez que se está ejecutando Tomcat, puede tener acceso a Tomcat escribiendo la dirección URL <http://localhost:8080> en el explorador de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="03505-166">Once Tomcat is running, you can access Tomcat by entering the URL <http://localhost:8080> in the virtual machine's browser.</span></span>

<span data-ttu-id="03505-167">Para ver que Tomcat se ejecuta desde máquinas externas, deberá crear un extremo y abrir un puerto.</span><span class="sxs-lookup"><span data-stu-id="03505-167">To see Tomcat running from external machines, you need to create an endpoint and open a port.</span></span>

## <a name="to-create-an-endpoint-for-your-virtual-machine"></a><span data-ttu-id="03505-168">Para crear un extremo para la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="03505-168">To create an endpoint for your virtual machine</span></span>
1. <span data-ttu-id="03505-169">Inicie sesión en el [Portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="03505-169">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="03505-170">Haga clic en **Virtual Machines (clásico)**.</span><span class="sxs-lookup"><span data-stu-id="03505-170">Click **Virtual machines (classic)**.</span></span>
3. <span data-ttu-id="03505-171">Haga clic en el nombre de la máquina virtual que ejecuta el servidor de aplicaciones Java.</span><span class="sxs-lookup"><span data-stu-id="03505-171">Click the name of the virtual machine that is running your Java application server.</span></span>
4. <span data-ttu-id="03505-172">Haga clic en **Extremos**.</span><span class="sxs-lookup"><span data-stu-id="03505-172">Click **Endpoints**.</span></span>
5. <span data-ttu-id="03505-173">Haga clic en **Agregar**.</span><span class="sxs-lookup"><span data-stu-id="03505-173">Click **Add**.</span></span>
6. <span data-ttu-id="03505-174">Aparecerá el cuadro de diálogo **Agregar punto de conexión**:</span><span class="sxs-lookup"><span data-stu-id="03505-174">In the **Add endpoint** dialog box:</span></span>
   1. <span data-ttu-id="03505-175">Especifique un nombre para el extremo; por ejemplo, **HttpIn**.</span><span class="sxs-lookup"><span data-stu-id="03505-175">Specify a name for the endpoint; for example, **HttpIn**.</span></span>
   2. <span data-ttu-id="03505-176">Seleccione **TCP** para el protocolo.</span><span class="sxs-lookup"><span data-stu-id="03505-176">Select **TCP** for the protocol.</span></span>
   3. <span data-ttu-id="03505-177">Especifique **80** para el puerto público.</span><span class="sxs-lookup"><span data-stu-id="03505-177">Specify **80** for the public port.</span></span>
   4. <span data-ttu-id="03505-178">Especifique **8080** para el puerto privado.</span><span class="sxs-lookup"><span data-stu-id="03505-178">Specify **8080** for the private port.</span></span>
   5. <span data-ttu-id="03505-179">Seleccione **Deshabilitado** para la dirección IP flotante.</span><span class="sxs-lookup"><span data-stu-id="03505-179">Select **Disabled** for the floating IP address.</span></span>
   6. <span data-ttu-id="03505-180">Deje la lista de control de acceso tal y como está.</span><span class="sxs-lookup"><span data-stu-id="03505-180">Leave the access control list as is.</span></span>
   7. <span data-ttu-id="03505-181">Haga clic en el botón **Aceptar** para cerrar el cuadro de diálogo y crear el punto de conexión.</span><span class="sxs-lookup"><span data-stu-id="03505-181">Click the **OK** button to close the dialog box and create the endpoint.</span></span>

## <a name="to-open-a-port-in-the-firewall-for-your-virtual-machine"></a><span data-ttu-id="03505-182">Para abrir un puerto en el firewall para la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="03505-182">To open a port in the firewall for your virtual machine</span></span>
1. <span data-ttu-id="03505-183">Inicie sesión en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="03505-183">Sign in to your virtual machine.</span></span>
2. <span data-ttu-id="03505-184">Haga clic en **Inicio de Windows**.</span><span class="sxs-lookup"><span data-stu-id="03505-184">Click **Windows Start**.</span></span>
3. <span data-ttu-id="03505-185">Haga clic en **Panel de control**.</span><span class="sxs-lookup"><span data-stu-id="03505-185">Click **Control Panel**.</span></span>
4. <span data-ttu-id="03505-186">Haga clic en **Sistema y seguridad**, **Firewall de Windows** y luego en **Configuración avanzada**.</span><span class="sxs-lookup"><span data-stu-id="03505-186">Click **System and Security**, click **Windows Firewall**, and then click **Advanced Settings**.</span></span>
5. <span data-ttu-id="03505-187">Haga clic en **Reglas de entrada** y después en **Nueva regla**.</span><span class="sxs-lookup"><span data-stu-id="03505-187">Click **Inbound Rules**, and then click **New Rule**.</span></span>  
   <span data-ttu-id="03505-188">![Nueva regla de entrada][NewIBRule]</span><span class="sxs-lookup"><span data-stu-id="03505-188">![New inbound rule][NewIBRule]</span></span>
6. <span data-ttu-id="03505-189">En **Tipo de regla**, seleccione **Puerto** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="03505-189">For the **Rule Type**, select **Port**, and then click **Next**.</span></span>  
   <span data-ttu-id="03505-190">![Puerto de nueva regla de entrada][NewRulePort]</span><span class="sxs-lookup"><span data-stu-id="03505-190">![New inbound rule port][NewRulePort]</span></span>
7. <span data-ttu-id="03505-191">En la pantalla **Protocolo y puertos**, seleccione **TCP**, especifique **8080** como **Puerto local específico** y luego haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="03505-191">On the **Protocol and Ports** screen, select **TCP**, specify **8080** as the **Specific local port**, and then click **Next**.</span></span>  
  <span data-ttu-id="03505-192">![Nueva regla de entrada][NewRuleProtocol]</span><span class="sxs-lookup"><span data-stu-id="03505-192">![New inbound rule ][NewRuleProtocol]</span></span>
8. <span data-ttu-id="03505-193">En la pantalla **Acción**, seleccione **Permitir la conexión** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="03505-193">On the **Action** screen, select **Allow the connection**, and then click **Next**.</span></span>
   <span data-ttu-id="03505-194">![Acción de nueva regla de entrada][NewRuleAction]</span><span class="sxs-lookup"><span data-stu-id="03505-194">![New inbound rule action][NewRuleAction]</span></span>
9. <span data-ttu-id="03505-195">En la pantalla **Perfil**, asegúrese de que **Dominio**, **Privado** y **Público** estén activados y después haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="03505-195">On the **Profile** screen, ensure that **Domain**, **Private**, and **Public** are selected, and then click **Next**.</span></span>
   <span data-ttu-id="03505-196">![Perfil de nueva regla de entrada][NewRuleProfile]</span><span class="sxs-lookup"><span data-stu-id="03505-196">![New inbound rule profile][NewRuleProfile]</span></span>
10. <span data-ttu-id="03505-197">En la pantalla **Nombre**, especifique un nombre para la regla, por ejemplo **HttpIn** (sin embargo, no es necesario que el nombre de la regla coincida con el nombre del punto de conexión) y haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="03505-197">On the **Name** screen, specify a name for the rule, such as **HttpIn** (the rule name is not required to match the endpoint name, however), and then click **Finish**.</span></span>  
    <span data-ttu-id="03505-198">![Nombre de la nueva regla de entrada][NewRuleName]</span><span class="sxs-lookup"><span data-stu-id="03505-198">![New inbound rule name][NewRuleName]</span></span>

<span data-ttu-id="03505-199">En este momento, el sitio web de Tomcat debe ser visible desde un explorador externo.</span><span class="sxs-lookup"><span data-stu-id="03505-199">At this point, your Tomcat website should be viewable from an external browser.</span></span> <span data-ttu-id="03505-200">En la ventana de dirección del explorador, escriba una dirección URL del formulario  **http://*su\_DNS\_nombre*. cloudapp.net**, donde ***su\_DNS\_nombre*** es el nombre DNS que especificó cuando creó la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="03505-200">In the browser's address window, type a URL of the form **http://*your\_DNS\_name*.cloudapp.net**, where ***your\_DNS\_name*** is the DNS name you specified when you created the virtual machine.</span></span>

## <a name="application-lifecycle-considerations"></a><span data-ttu-id="03505-201">Consideraciones acerca del ciclo de vida de las aplicaciones</span><span class="sxs-lookup"><span data-stu-id="03505-201">Application lifecycle considerations</span></span>
* <span data-ttu-id="03505-202">Puede crear su propio archivo de aplicación web (WAR) y agregarlo a la carpeta **webapps** .</span><span class="sxs-lookup"><span data-stu-id="03505-202">You could create your own web application archive (WAR) and add it to the **webapps** folder.</span></span> <span data-ttu-id="03505-203">Por ejemplo, cree un proyecto web dinámico de Java Service Page (JSP) básico y expórtelo como archivo WAR.</span><span class="sxs-lookup"><span data-stu-id="03505-203">For example, create a basic Java Service Page (JSP) dynamic web project and export it as a WAR file.</span></span> <span data-ttu-id="03505-204">A continuación, copie el archivo WAR a la carpeta **webapps** de Apache Tomcat en la máquina virtual y, a continuación, ejecútelo en un explorador.</span><span class="sxs-lookup"><span data-stu-id="03505-204">Next, copy the WAR to the Apache Tomcat **webapps** folder on the virtual machine, then run it in a browser.</span></span>
* <span data-ttu-id="03505-205">De forma predeterminada, cuando el servicio Tomcat está instalado, está configurado para iniciarse manualmente.</span><span class="sxs-lookup"><span data-stu-id="03505-205">By default when the Tomcat service is installed, it is set to start manually.</span></span> <span data-ttu-id="03505-206">Puede cambiarlo para que se inicie automáticamente mediante el complemento Servicios.</span><span class="sxs-lookup"><span data-stu-id="03505-206">You can switch it to start automatically by using the Services snap-in.</span></span> <span data-ttu-id="03505-207">Inicie el complemento Servicios, haga clic en **Inicio de Windows**, **Herramientas administrativas** y luego en **Servicios**.</span><span class="sxs-lookup"><span data-stu-id="03505-207">Start the Services snap-in by clicking **Windows Start**, **Administrative Tools**, and then **Services**.</span></span> <span data-ttu-id="03505-208">Haga doble clic en el servicio **Apache Tomcat** y establezca **Tipo de inicio** en **Automático**.</span><span class="sxs-lookup"><span data-stu-id="03505-208">Double-click the **Apache Tomcat** service and set **Startup type** to **Automatic**.</span></span>

    ![Configurar un servicio para que se inicie automáticamente][service_automatic_startup]

    <span data-ttu-id="03505-210">La ventaja de que Tomcat se inicie automáticamente es que comienza a funcionar cuando se reinicia la máquina virtual (por ejemplo, después de instalar actualizaciones de software que requieren un reinicio).</span><span class="sxs-lookup"><span data-stu-id="03505-210">The benefit of having Tomcat start automatically is that it starts running when the virtual machine is rebooted (for example, after software updates that require a reboot are installed).</span></span>

## <a name="next-steps"></a><span data-ttu-id="03505-211">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="03505-211">Next steps</span></span>
<span data-ttu-id="03505-212">Puede obtener más información sobre otros servicios (como Azure Storage, Service Bus y SQL Database) que quiera incluir con las aplicaciones de Java.</span><span class="sxs-lookup"><span data-stu-id="03505-212">You can learn about other services (such as Azure Storage, service bus, and SQL Database) that you may want to include with your Java applications.</span></span> <span data-ttu-id="03505-213">Vea la información disponible en [Centro para desarrolladores de Java](https://azure.microsoft.com/develop/java/).</span><span class="sxs-lookup"><span data-stu-id="03505-213">View the information available at the [Java Developer Center](https://azure.microsoft.com/develop/java/).</span></span>

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from the "To create an ednpoint for your virtual mache" 3/17/2017,
     to use the new portal.
6. In the **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In the **New endpoint details** dialog box:
-->
