---
title: "Uso de PowerShell para crear una máquina virtual de Azure con un servidor de informes en modo nativo | Microsoft Docs"
description: "En este tema se describe y se le guiará por la implementación y la configuración de un servidor de informes de modo nativo de SQL Server Reporting Services en una máquina virtual de Azure. "
services: virtual-machines-windows
documentationcenter: na
author: guyinacube
manager: erikre
editor: monicar
tags: azure-service-management
ms.assetid: 553af55b-d02e-4e32-904c-682bfa20fa0f
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/11/2017
ms.author: asaxton
ms.openlocfilehash: 5e5c11251cd316e8161dbe362b300be76927ac01
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="use-powershell-to-create-an-azure-vm-with-a-native-mode-report-server"></a><span data-ttu-id="47335-103">Usar PowerShell para crear una máquina virtual de Azure con un servidor de informes en modo nativo</span><span class="sxs-lookup"><span data-stu-id="47335-103">Use PowerShell to Create an Azure VM With a Native Mode Report Server</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="47335-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="47335-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="47335-105">En este artículo se trata el modelo de implementación clásico.</span><span class="sxs-lookup"><span data-stu-id="47335-105">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="47335-106">Microsoft recomienda que las implementaciones más recientes usen el modelo del Administrador de recursos.</span><span class="sxs-lookup"><span data-stu-id="47335-106">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="47335-107">En este tema se describe y se le guiará por la implementación y la configuración de un servidor de informes de modo nativo de SQL Server Reporting Services en una máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="47335-107">This topic describes and walks you through the deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine.</span></span> <span data-ttu-id="47335-108">Los pasos de este documento usan una combinación de pasos manuales para crear la máquina virtual y un script de Windows PowerShell para configurar Reporting Services en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-108">The steps in this document use a combination of manual steps to create the virtual machine and a Windows PowerShell script to configure Reporting Services on the VM.</span></span> <span data-ttu-id="47335-109">El script de configuración incluye la apertura de un puerto de firewall para HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="47335-109">The configuration script includes opening a firewall port for HTTP or HTTPs.</span></span>

> [!NOTE]
> <span data-ttu-id="47335-110">Si no necesita **HTTPS** en el servidor de informes, **omita el paso 2**.</span><span class="sxs-lookup"><span data-stu-id="47335-110">If you do not require **HTTPS** on the report server, **skip step 2**.</span></span>
> 
> <span data-ttu-id="47335-111">Después de crear la máquina virtual en el paso 1, vaya a la sección Usar script para configurar el HTTP y el servidor de informes.</span><span class="sxs-lookup"><span data-stu-id="47335-111">After creating the VM in step 1, go to the section Use script to configure the report server and HTTP.</span></span> <span data-ttu-id="47335-112">Después de ejecutar el script, el servidor de informes estará listo para su uso.</span><span class="sxs-lookup"><span data-stu-id="47335-112">After you run the script, the report server is ready to use.</span></span>

## <a name="prerequisites-and-assumptions"></a><span data-ttu-id="47335-113">Requisitos previos y suposiciones</span><span class="sxs-lookup"><span data-stu-id="47335-113">Prerequisites and Assumptions</span></span>
* <span data-ttu-id="47335-114">**Suscripción de Azure**: compruebe el número de núcleos disponibles en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="47335-114">**Azure Subscription**: Verify the number of cores available in your Azure Subscription.</span></span> <span data-ttu-id="47335-115">Si crea el tamaño recomendado de máquina virtual de **A3**, necesita **4** núcleos disponibles.</span><span class="sxs-lookup"><span data-stu-id="47335-115">If you create the recommended VM size of **A3**, you need **4** available cores.</span></span> <span data-ttu-id="47335-116">Si usa un tamaño de máquina virtual de **A2**, necesita **2** núcleos disponibles.</span><span class="sxs-lookup"><span data-stu-id="47335-116">If you use a VM size of **A2**, you need **2** available cores.</span></span>
  
  * <span data-ttu-id="47335-117">Para comprobar el límite de núcleos de su suscripción, en el Portal de Azure clásico, haga clic en CONFIGURACIÓN en el panel izquierdo y luego en USO en el menú superior.</span><span class="sxs-lookup"><span data-stu-id="47335-117">To verify the core limit of your subscription, in the Azure classic portal, click SETTINGS in the left pane and then Click USAGE in the top menu.</span></span>
  * <span data-ttu-id="47335-118">Para aumentar la cuota de núcleos, póngase en contacto con el [soporte técnico de Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="47335-118">To increase the core quota, contact [Azure Support](https://azure.microsoft.com/support/options/).</span></span> <span data-ttu-id="47335-119">Para obtener más información sobre el tamaño de la máquina virtual, consulte [Tamaños de máquinas virtuales para Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="47335-119">For VM size information, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="47335-120">**Scripting de Windows PowerShell**: en el tema se supone que cuenta con conocimientos prácticos básicos de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="47335-120">**Windows PowerShell Scripting**: The topic assumes that you have a basic working knowledge of Windows PowerShell.</span></span> <span data-ttu-id="47335-121">Para obtener más información sobre el uso de Windows PowerShell, vea lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="47335-121">For more information about using Windows PowerShell, see the following:</span></span>
  
  * [<span data-ttu-id="47335-122">Inicio de Windows PowerShell en Windows Server</span><span class="sxs-lookup"><span data-stu-id="47335-122">Starting Windows PowerShell on Windows Server</span></span>](https://technet.microsoft.com/library/hh847814.aspx)
  * [<span data-ttu-id="47335-123">Introducción a Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="47335-123">Getting Started with Windows PowerShell</span></span>](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a><span data-ttu-id="47335-124">Paso 1: Aprovisionar una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="47335-124">Step 1: Provision an Azure Virtual Machine</span></span>
1. <span data-ttu-id="47335-125">Vaya al Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="47335-125">Browse to the Azure classic portal.</span></span>
2. <span data-ttu-id="47335-126">Haga clic en **Máquinas virtuales** en el panel izquierdo.</span><span class="sxs-lookup"><span data-stu-id="47335-126">Click **Virtual Machines** in the left pane.</span></span>
   
    ![máquinas virtuales de microsoft azure](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. <span data-ttu-id="47335-128">Haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="47335-128">Click **New**.</span></span>
   
    ![botón nuevo](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. <span data-ttu-id="47335-130">Haga clic en **De la galería**.</span><span class="sxs-lookup"><span data-stu-id="47335-130">Click **From Gallery**.</span></span>
   
    ![nueva máquina virtual de la galería](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. <span data-ttu-id="47335-132">Haga clic en **SQL Server 2014 RTM Standard: Windows Server 2012 R2** y luego en la flecha para continuar.</span><span class="sxs-lookup"><span data-stu-id="47335-132">Click **SQL Server 2014 RTM Standard – Windows Server 2012 R2** and then click the arrow to continue.</span></span>
   
    ![Siguiente](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    <span data-ttu-id="47335-134">Si necesita la característica de suscripciones controladas por datos de Reporting Services, elija **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span><span class="sxs-lookup"><span data-stu-id="47335-134">If you need the Reporting Services data driven subscriptions feature, choose **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span></span> <span data-ttu-id="47335-135">Para más información sobre las ediciones de SQL Server y la compatibilidad de características, consulte [Características admitidas por las ediciones de SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span><span class="sxs-lookup"><span data-stu-id="47335-135">For more information on SQL Server editions and feature support, see [Features Supported by the Editions of SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span></span>
6. <span data-ttu-id="47335-136">En la página **Configuración de la máquina virtual** , edite los siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="47335-136">On the **Virtual machine configuration** page, edit the following fields:</span></span>
   
   * <span data-ttu-id="47335-137">Si hay más de una **FECHA DE LANZAMIENTO DE LA VERSIÓN**, seleccione la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="47335-137">If there is more than one **VERSION RELEASE DATE**, select the most recent version.</span></span>
   * <span data-ttu-id="47335-138">**Nombre de máquina virtual**: el nombre de la máquina también se usa en la siguiente página de configuración como el nombre DNS del servicio en la nube predeterminado.</span><span class="sxs-lookup"><span data-stu-id="47335-138">**Virtual Machine Name**: The machine name is also used on the next configuration page as the default Cloud Service DNS name.</span></span> <span data-ttu-id="47335-139">El nombre DNS debe ser único en el servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="47335-139">The DNS name must be unique across the Azure service.</span></span> <span data-ttu-id="47335-140">Considere la posibilidad de configurar la máquina virtual con un nombre de equipo que describa para qué se usa la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-140">Consider configuring the VM with a computer name that describes what the VM is used for.</span></span> <span data-ttu-id="47335-141">Por ejemplo, ssrsnativecloud.</span><span class="sxs-lookup"><span data-stu-id="47335-141">For example ssrsnativecloud.</span></span>
   * <span data-ttu-id="47335-142">**Nivel**: estándar</span><span class="sxs-lookup"><span data-stu-id="47335-142">**Tier**: Standard</span></span>
   * <span data-ttu-id="47335-143">**Tamaño: A3** es el tamaño de máquina virtual recomendado para cargas de trabajo de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="47335-143">**Size:A3** is the recommended VM size for SQL Server workloads.</span></span> <span data-ttu-id="47335-144">Si una máquina virtual solo se usa como servidor de informes, un tamaño de A2 es suficiente a menos que el servidor de informes experimente una gran carga de trabajo.</span><span class="sxs-lookup"><span data-stu-id="47335-144">If a VM is only used as a report server, a VM size of A2 is sufficient unless the report server experiences a large workload.</span></span> <span data-ttu-id="47335-145">Para más información sobre precios de máquinas virtuales, consulte [Precios de Máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="47335-145">For VM pricing information, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
   * <span data-ttu-id="47335-146">**Nuevo nombre de usuario**: el nombre que ofrece se crea como administrador en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-146">**New User Name**: the name you provide is created as an administrator on the VM.</span></span>
   * <span data-ttu-id="47335-147">**Nueva contraseña** y **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="47335-147">**New Password** and **confirm**.</span></span> <span data-ttu-id="47335-148">Esta contraseña se usa para la nueva cuenta de administrador y se recomienda usar una contraseña segura.</span><span class="sxs-lookup"><span data-stu-id="47335-148">This password is used for the new administrator account and it is recommended you use a strong password.</span></span>
   * <span data-ttu-id="47335-149">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="47335-149">Click **Next**.</span></span> <span data-ttu-id="47335-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span><span class="sxs-lookup"><span data-stu-id="47335-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span></span>
7. <span data-ttu-id="47335-151">En la página siguiente, edite los siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="47335-151">On the next page, edit the following fields:</span></span>
   
   * <span data-ttu-id="47335-152">**Servicio en la nube**: seleccione **Crear un nuevo servicio en la nube**.</span><span class="sxs-lookup"><span data-stu-id="47335-152">**Cloud Service**: select **Create a new Cloud Service**.</span></span>
   * <span data-ttu-id="47335-153">**Nombre DNS de servicio en la nube**: este es el nombre DNS público del servicio en la nube que está asociado a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-153">**Cloud Service DNS Name**: This is the public DNS name of the Cloud Service that is associated with the VM.</span></span> <span data-ttu-id="47335-154">El nombre predeterminado es el nombre que escribió para el nombre de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-154">The default name is the name you typed in for the VM name.</span></span> <span data-ttu-id="47335-155">Si se encuentra en pasos posteriores del tema, crea un certificado SSL de confianza y se usa el nombre DNS para el valor de "**Emitido a**" del certificado.</span><span class="sxs-lookup"><span data-stu-id="47335-155">If in later steps of the topic, you create a trusted SSL certificate and then the DNS name is used for the value of the “**Issued to**” of the certificate.</span></span>
   * <span data-ttu-id="47335-156">**Región/grupo de afinidad/red virtual**: elija la región más cercana a sus usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="47335-156">**Region/Affinity Group/Virtual Network**: Choose the region closest to your end users.</span></span>
   * <span data-ttu-id="47335-157">**Cuenta de almacenamiento**: use una cuenta de almacenamiento generada automáticamente</span><span class="sxs-lookup"><span data-stu-id="47335-157">**Storage Account**: Use an automatically generated storage account.</span></span>
   * <span data-ttu-id="47335-158">**Conjunto de disponibilidad**: ninguno.</span><span class="sxs-lookup"><span data-stu-id="47335-158">**Availability Set**: None.</span></span>
   * <span data-ttu-id="47335-159">**PUNTOS DE CONEXIÓN** Mantenga los puntos de conexión **Escritorio remoto** y **PowerShell** y después agregue un punto de conexión HTTP o HTTPS, en función del entorno.</span><span class="sxs-lookup"><span data-stu-id="47335-159">**ENDPOINTS** Keep the **Remote Desktop** and **PowerShell** endpoints and then add either an HTTP or HTTPS endpoint, depending on your environment.</span></span>
     
     * <span data-ttu-id="47335-160">**HTTP**: los puertos públicos y privados predeterminados son **80**.</span><span class="sxs-lookup"><span data-stu-id="47335-160">**HTTP**: The default public and private ports are **80**.</span></span> <span data-ttu-id="47335-161">Tenga en cuenta que si usa un puerto privado distinto de 80, tendrá que modificar **$HTTPport = 80** en el script de http.</span><span class="sxs-lookup"><span data-stu-id="47335-161">Note that if you use a private port other than 80, modify **$HTTPport = 80** in the http script.</span></span>
     * <span data-ttu-id="47335-162">**HTTPS**: los puertos públicos y privados predeterminados son **443**.</span><span class="sxs-lookup"><span data-stu-id="47335-162">**HTTPS**: The default public and private ports are **443**.</span></span> <span data-ttu-id="47335-163">Una práctica recomendada de seguridad consiste en cambiar el puerto privado y configurar el firewall y el servidor de informes para usar el puerto privado.</span><span class="sxs-lookup"><span data-stu-id="47335-163">A security best practice is to change the private port and configure your firewall and the report server to use the private port.</span></span> <span data-ttu-id="47335-164">Para más información sobre los puntos de conexión, consulte [Configuración de extremos en una máquina virtual](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="47335-164">For more information on endpoints, see [How to Set Up Communication with a Virtual Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="47335-165">Tenga en cuenta que si usa un puerto distinto de 443, debe cambiar el parámetro **$HTTPsport = 443** en el script de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="47335-165">Note that if you use a port other than 443, change the parameter **$HTTPsport = 443** in the HTTPS script.</span></span>
   * <span data-ttu-id="47335-166">Haga clic en Siguiente.</span><span class="sxs-lookup"><span data-stu-id="47335-166">Click next .</span></span> ![Siguiente](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. <span data-ttu-id="47335-168">En la última página del asistente, mantenga el valor predeterminado de **Instalar el agente de VM** seleccionado.</span><span class="sxs-lookup"><span data-stu-id="47335-168">On the last page of the wizard, keep the default **Install the VM agent** selected.</span></span> <span data-ttu-id="47335-169">Los pasos descritos en este tema no usan al agente de máquina virtual, pero si piensa mantener esta máquina virtual, el agente de máquina virtual y las extensiones le permitirán mejorar la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-169">The steps in this topic do not utilize the VM agent but if you plan to keep this VM, the VM agent and extensions will allow you to enhance he CM.</span></span>  <span data-ttu-id="47335-170">Para más información sobre el agente de máquina virtual, consulte [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span><span class="sxs-lookup"><span data-stu-id="47335-170">For more information on the VM agent, see [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span></span> <span data-ttu-id="47335-171">Una de las extensiones predeterminadas instaladas y en ejecución es la extensión "BGINFO" que se muestra en el escritorio de la máquina virtual, información del sistema como la dirección IP interna y el espacio libre en disco.</span><span class="sxs-lookup"><span data-stu-id="47335-171">One of the default extensions installed ad running is the “BGINFO” extension that displays on the VM desktop, system information such as internal IP and free drive space.</span></span>
9. <span data-ttu-id="47335-172">Haga clic en Completo.</span><span class="sxs-lookup"><span data-stu-id="47335-172">Click complete .</span></span> ![Aceptar](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. <span data-ttu-id="47335-174">El **estado** de la máquina virtual se muestra como **Iniciando (aprovisionamiento)** durante el proceso de aprovisionamiento y luego se muestra como **En ejecución** cuando la máquina virtual está aprovisionada y lista para usarse.</span><span class="sxs-lookup"><span data-stu-id="47335-174">The **Status** of the VM displays as **Starting (Provisioning)** during the provision process and then displays as **Running** when the VM is provisioned and ready to use.</span></span>

## <a name="step-2-create-a-server-certificate"></a><span data-ttu-id="47335-175">Paso 2: Crear un certificado de servidor</span><span class="sxs-lookup"><span data-stu-id="47335-175">Step 2: Create a Server Certificate</span></span>
> [!NOTE]
> <span data-ttu-id="47335-176">Si no requiere HTTPS en el servidor de informes, puede **omitir el paso 2** e ir a la sección **Uso del script para configurar el servidor de informes y HTTP**.</span><span class="sxs-lookup"><span data-stu-id="47335-176">If you do not require HTTPS on the report server, you can **skip step 2** and go to the section **Use script to configure the report server and HTTP**.</span></span> <span data-ttu-id="47335-177">Use el script de HTTP para configurar rápidamente el servidor de informes y el servidor de informes estará listo para su uso.</span><span class="sxs-lookup"><span data-stu-id="47335-177">Use the HTTP script to quickly configure the report server and the report server will be ready to use.</span></span>

<span data-ttu-id="47335-178">Para usar HTTPS en la máquina virtual, necesitará un certificado SSL de confianza.</span><span class="sxs-lookup"><span data-stu-id="47335-178">In order to use HTTPS on the VM, you need a trusted SSL certificate.</span></span> <span data-ttu-id="47335-179">Según el escenario, puede usar uno de los dos métodos siguientes:</span><span class="sxs-lookup"><span data-stu-id="47335-179">Depending on your scenario, you can use one of the following two methods:</span></span>

* <span data-ttu-id="47335-180">Un certificado SSL válido emitido por una entidad de certificación (CA) y de confianza de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="47335-180">A valid SSL certificate issued by a Certification Authority (CA) and trusted by Microsoft.</span></span> <span data-ttu-id="47335-181">Se requiere la distribución de los certificados raíz de CA mediante el programa de certificados raíz de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="47335-181">The CA root certificates are required to be distributed via the Microsoft Root Certificate Program.</span></span> <span data-ttu-id="47335-182">Para más información sobre este programa, consulte [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) (Programas de certificados raíz SSL de Windows y Windows Phone) (CA miembros) e [Introduction to The Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx) (Introducción al Programa de certificados raíz de Microsoft).</span><span class="sxs-lookup"><span data-stu-id="47335-182">For more information about this program, see [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) and [Introduction to The Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span></span>
* <span data-ttu-id="47335-183">Un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="47335-183">A self-signed certificate.</span></span> <span data-ttu-id="47335-184">No se recomiendan los certificados autofirmados para entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="47335-184">Self-signed certificates are not recommended for production environments.</span></span>

### <a name="to-use-a-certificate-created-by-a-trusted-certificate-authority-ca"></a><span data-ttu-id="47335-185">Para usar un certificado creado por una entidad de certificación (CA) de confianza</span><span class="sxs-lookup"><span data-stu-id="47335-185">To use a certificate created by a trusted Certificate Authority (CA)</span></span>
1. <span data-ttu-id="47335-186">**Solicitar un certificado de servidor para el sitio web desde una entidad de certificación**.</span><span class="sxs-lookup"><span data-stu-id="47335-186">**Request a server certificate for the website from a certification authority**.</span></span> 
   
    <span data-ttu-id="47335-187">Puede utilizar el Asistente para certificados de servidor Web para generar un archivo de solicitud de certificado (Certreq.txt) que se envía a una entidad de certificación o para generar una solicitud para una entidad de certificación en línea.</span><span class="sxs-lookup"><span data-stu-id="47335-187">You can use the Web Server Certificate Wizard either to generate a certificate request file (Certreq.txt) that you send to a certification authority, or to generate a request for an online certification authority.</span></span> <span data-ttu-id="47335-188">Por ejemplo, los Servicios de certificados de Microsoft en Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="47335-188">For example, Microsoft Certificate Services in Windows Server 2012.</span></span> <span data-ttu-id="47335-189">Según el nivel de garantía de identificación ofrecido por el certificado del servidor, se tarda entre varios días o varios meses en que la entidad de certificación apruebe su solicitud y le envíe un archivo de certificado.</span><span class="sxs-lookup"><span data-stu-id="47335-189">Depending on the level of identification assurance offered by your server certificate, it is several days to several months for the certification authority to approve your request and send you a certificate file.</span></span> 
   
    <span data-ttu-id="47335-190">Para obtener más información sobre la solicitud de certificados a un servidor, vea lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="47335-190">For more information about requesting a server certificates, see the following:</span></span> 
   
   * <span data-ttu-id="47335-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span><span class="sxs-lookup"><span data-stu-id="47335-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span></span>
   * <span data-ttu-id="47335-192">Herramientas de seguridad para administrar Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="47335-192">Security Tools to Administer Windows Server 2012.</span></span>
     
     [<span data-ttu-id="47335-193">Herramientas de seguridad para administrar Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="47335-193">Security Tools to Administer Windows Server 2012</span></span>](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > <span data-ttu-id="47335-194">El campo **Emitido a** del certificado SSL de confianza debe ser el mismo que el **nombre DNS de servicio en la nube** que usó para la nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-194">The **issued to** field of the trusted SSL certificate should be the same as the **Cloud Service DNS NAME** you used for the new VM.</span></span>

2. <span data-ttu-id="47335-195">**Instale el certificado de servidor en el servidor web**.</span><span class="sxs-lookup"><span data-stu-id="47335-195">**Install the server certificate on the Web server**.</span></span> <span data-ttu-id="47335-196">En este caso, el servidor web es la máquina virtual que hospeda el servidor de informes y el sitio web se crea en pasos posteriores al configurar Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="47335-196">The Web server in this case is the VM that hosts the report server and the website is created in later steps when you configure Reporting Services.</span></span> <span data-ttu-id="47335-197">Para obtener más información sobre la instalación del certificado de servidor en el servidor web mediante el complemento MMC de certificado, consulte [Instalar un certificado de servidor](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="47335-197">For more information about installing the server certificate on the Web server by using the Certificate MMC snap-in, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
    <span data-ttu-id="47335-198">Si quiere usar el script incluido con este tema, para configurar el servidor de informes, se requiere el valor de los certificados **Huella digital** como parámetro del script.</span><span class="sxs-lookup"><span data-stu-id="47335-198">If you want to use the script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span></span> <span data-ttu-id="47335-199">Vea la sección siguiente para obtener más información sobre cómo obtener la huella digital del certificado.</span><span class="sxs-lookup"><span data-stu-id="47335-199">See the next section for details on how to obtain the thumbprint of the certificate.</span></span>
3. <span data-ttu-id="47335-200">Asigne el certificado de servidor al servidor de informes.</span><span class="sxs-lookup"><span data-stu-id="47335-200">Assign the server certificate to the report server.</span></span> <span data-ttu-id="47335-201">La asignación se completa en la sección siguiente al configurar el servidor de informes.</span><span class="sxs-lookup"><span data-stu-id="47335-201">The assignment is completed in the next section when you configure the report server.</span></span>

### <a name="to-use-the-virtual-machines-self-signed-certificate"></a><span data-ttu-id="47335-202">Para usar el certificado autofirmado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="47335-202">To use the Virtual Machines Self-signed Certificate</span></span>
<span data-ttu-id="47335-203">Se creó un certificado autofirmado en la máquina virtual cuando se aprovisionó la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-203">A self-signed certificate was created on the VM when the VM was provisioned.</span></span> <span data-ttu-id="47335-204">El certificado tiene el mismo nombre que el nombre de DNS de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-204">The certificate has the same name as the VM DNS name.</span></span> <span data-ttu-id="47335-205">Para evitar errores de certificado, es necesario que el certificado sea de confianza en la propia máquina virtual y también de la confianza de todos los usuarios del sitio.</span><span class="sxs-lookup"><span data-stu-id="47335-205">In order to avoid certificate errors, it is required that the certificate is trusted on the VM itself, and also by all users of the site.</span></span>

1. <span data-ttu-id="47335-206">Para confiar en la entidad de certificación raíz del certificado en la máquina virtual local, agregue el certificado a las **Entidades de certificación raíz de confianza**.</span><span class="sxs-lookup"><span data-stu-id="47335-206">To trust the root CA of the certificate on the Local VM, add the certificate to the **Trusted Root Certification Authorities**.</span></span> <span data-ttu-id="47335-207">A continuación se encuentra un resumen de los pasos necesarios.</span><span class="sxs-lookup"><span data-stu-id="47335-207">The following is a summary of the steps required.</span></span> <span data-ttu-id="47335-208">Para obtener pasos detallados sobre cómo confiar en la entidad de certificación, consulte [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="47335-208">For detailed steps on how to trust the CA, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
   1. <span data-ttu-id="47335-209">En el Portal de Azure clásico, seleccione la máquina virtual y haga clic en Conectar.</span><span class="sxs-lookup"><span data-stu-id="47335-209">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="47335-210">En función de la configuración del explorador, es posible que se le solicite guardar un archivo .rdp para conectarse a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-210">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
      
       ![conectarse a máquina virtual de azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="47335-212">Use el nombre de la máquina virtual del usuario, el nombre de usuario y la contraseña que configuró al crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-212">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
      
       <span data-ttu-id="47335-213">Por ejemplo, en la siguiente imagen, el nombre de la máquina virtual es **ssrsnativecloud** y el nombre del usuario es **testuser**.</span><span class="sxs-lookup"><span data-stu-id="47335-213">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
      
       ![el inicio de sesión incluye la máquina virtual](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. <span data-ttu-id="47335-215">Ejecute mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="47335-215">Run mmc.exe.</span></span> <span data-ttu-id="47335-216">Para más información, consulte [Visualización de certificados con el complemento MMC](https://msdn.microsoft.com/library/ms788967.aspx).</span><span class="sxs-lookup"><span data-stu-id="47335-216">For more information, see [How to: View Certificates with the MMC Snap-in](https://msdn.microsoft.com/library/ms788967.aspx).</span></span>
   3. <span data-ttu-id="47335-217">En el menú de la aplicación de consola **Archivo**, agregue el complemento **Certificados**, seleccione **Cuenta de equipo** cuando se le pida y luego haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="47335-217">In the console application **File** menu, add the **Certificates** snap-in, select **Computer Account** when prompted, and then click **Next**.</span></span>
   4. <span data-ttu-id="47335-218">Seleccione **Equipo local** para administrar y luego haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="47335-218">Select **Local Computer** to manage and then click **Finish**.</span></span>
   5. <span data-ttu-id="47335-219">Haga clic en **Aceptar** y expanda los nodos **Certificados - Personal**; luego haga clic en **Certificados**.</span><span class="sxs-lookup"><span data-stu-id="47335-219">Click **Ok** and then expand the **Certificates -Personal** nodes and then click **Certificates**.</span></span> <span data-ttu-id="47335-220">El certificado toma el nombre DNS de la máquina virtual y agrega **cloudapp.net**al final.</span><span class="sxs-lookup"><span data-stu-id="47335-220">The certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span></span> <span data-ttu-id="47335-221">Haga clic con el botón derecho en el nombre del certificado y haga clic en **Copiar**.</span><span class="sxs-lookup"><span data-stu-id="47335-221">Right-click the certificate name and click **Copy**.</span></span>
   6. <span data-ttu-id="47335-222">Expanda el nodo **Entidades de certificación raíz de confianza**, haga clic con el botón derecho en **Certificados** y luego haga clic en **Pegar**.</span><span class="sxs-lookup"><span data-stu-id="47335-222">Expand the **Trusted Root Certification Authorities** node and then right-click **Certificates** and then click **Paste**.</span></span>
   7. <span data-ttu-id="47335-223">Para validar, haga doble clic en el nombre del certificado en **Entidades de certificación raíz de confianza** y compruebe que no haya ningún error; de este modo, verá el certificado.</span><span class="sxs-lookup"><span data-stu-id="47335-223">To validate, double click on the certificate name under **Trusted Root Certification Authorities** and verify that there are no errors and you see your certificate.</span></span> <span data-ttu-id="47335-224">Si quiere usar el script de HTTPS incluido con este tema, para configurar el servidor de informes se requiere el valor de la **huella digital** de los certificados como parámetro del script.</span><span class="sxs-lookup"><span data-stu-id="47335-224">If you want to use the HTTPS script included with this topic, to configure the report server, the value of the certificates **Thumbprint** is required as a parameter of the script.</span></span> <span data-ttu-id="47335-225">**Para obtener el valor de la huella digital**, complete los pasos siguientes.</span><span class="sxs-lookup"><span data-stu-id="47335-225">**To get the thumbprint value**, complete the following.</span></span> <span data-ttu-id="47335-226">También hay un ejemplo de PowerShell para recuperar la huella digital en la sección [Usar el script para configurar el servidor de informes y HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span><span class="sxs-lookup"><span data-stu-id="47335-226">There is also a PowerShell sample to retrieve the thumbprint in section [Use script to configure the report server and HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span></span>
      
      1. <span data-ttu-id="47335-227">Haga doble clic en el nombre del certificado, por ejemplo, ssrsnativecloud.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="47335-227">Double-click the name of the certificate, for example ssrsnativecloud.cloudapp.net.</span></span>
      2. <span data-ttu-id="47335-228">Haga clic en la pestaña **Detalles** .</span><span class="sxs-lookup"><span data-stu-id="47335-228">Click the **Details** tab.</span></span>
      3. <span data-ttu-id="47335-229">Haga clic en **Huella digital**.</span><span class="sxs-lookup"><span data-stu-id="47335-229">Click **Thumbprint**.</span></span> <span data-ttu-id="47335-230">El valor de la huella digital se muestra en el campo de detalles, por ejemplo, ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span><span class="sxs-lookup"><span data-stu-id="47335-230">The value of the thumbprint is displayed in the details field, for example ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span></span>
      4. <span data-ttu-id="47335-231">Copie la huella digital y guarde el valor para más adelante o edite el script ahora.</span><span class="sxs-lookup"><span data-stu-id="47335-231">Copy the thumbprint and save the value for later or edit the script now.</span></span>
      5. <span data-ttu-id="47335-232">(*) Antes de ejecutar el script, quite los espacios entre los pares de valores.</span><span class="sxs-lookup"><span data-stu-id="47335-232">(*) Before you run the script, remove the spaces in between the pairs of values.</span></span> <span data-ttu-id="47335-233">Por ejemplo, la huella digital que se ha indicado antes ahora sería ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span><span class="sxs-lookup"><span data-stu-id="47335-233">For example the thumbprint noted before would now be ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span></span>
      6. <span data-ttu-id="47335-234">Asigne el certificado de servidor al servidor de informes.</span><span class="sxs-lookup"><span data-stu-id="47335-234">Assign the server certificate to the report server.</span></span> <span data-ttu-id="47335-235">La asignación se completa en la sección siguiente al configurar el servidor de informes.</span><span class="sxs-lookup"><span data-stu-id="47335-235">The assignment is completed in the next section when you configure the report server.</span></span>

<span data-ttu-id="47335-236">Si está usando un certificado SSL autofirmado, el nombre del certificado ya coincide con el nombre de host de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-236">If you are using a self-signed SSL certificate, the name on the certificate already matches the hostname of the VM.</span></span> <span data-ttu-id="47335-237">Por lo tanto, el DNS de la máquina ya está registrado globalmente y se puede obtener acceso a él desde cualquier cliente.</span><span class="sxs-lookup"><span data-stu-id="47335-237">Therefore, the DNS of the machine is already registered globally and can be accessed from any client.</span></span>

## <a name="step-3-configure-the-report-server"></a><span data-ttu-id="47335-238">Paso 3: configurar el Servidor de informes</span><span class="sxs-lookup"><span data-stu-id="47335-238">Step 3: Configure the Report Server</span></span>
<span data-ttu-id="47335-239">En esta sección se explica cómo configurar la máquina virtual como servidor de informes de modo nativo de Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="47335-239">This section walks you through configuring the VM as a Reporting Services native mode report server.</span></span> <span data-ttu-id="47335-240">Puede usar uno de los métodos siguientes para configurar el servidor de informes:</span><span class="sxs-lookup"><span data-stu-id="47335-240">You can use one of the following methods to configure the report server:</span></span>

* <span data-ttu-id="47335-241">Use el script para configurar el servidor de informes</span><span class="sxs-lookup"><span data-stu-id="47335-241">Use the script to configure the report server</span></span>
* <span data-ttu-id="47335-242">Use el Administrador de configuración para configurar el servidor de informes.</span><span class="sxs-lookup"><span data-stu-id="47335-242">Use Configuration Manager to Configure the Report Server.</span></span>

<span data-ttu-id="47335-243">Para ver pasos más detallados, consulte la sección [Conectarse a la máquina virtual e iniciar el Administrador de configuración de Reporting Services](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="47335-243">For more detailed steps, see the section [Connect to the Virtual Machine and Start the Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span></span>

<span data-ttu-id="47335-244">**Nota de autenticación:** la autenticación de Windows es el método de autenticación recomendado y es la autenticación predeterminada de Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="47335-244">**Authentication Note:** Windows authentication is the recommended authentication method and it is the default Reporting Services authentication.</span></span> <span data-ttu-id="47335-245">Solo los usuarios que están configurados en la máquina virtual pueden obtener acceso a Reporting Services y asignarse a los roles de Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="47335-245">Only users that are configured on the VM can access Reporting Services and assigned to Reporting Services roles.</span></span>

### <a name="use-script-to-configure-the-report-server-and-http"></a><span data-ttu-id="47335-246">Uso del script para configurar el servidor de informes y HTTP</span><span class="sxs-lookup"><span data-stu-id="47335-246">Use script to configure the report server and HTTP</span></span>
<span data-ttu-id="47335-247">Para usar el script de Windows PowerShell para configurar el servidor de informes, complete los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="47335-247">To use the Windows PowerShell script to configure the report server, complete the following steps.</span></span> <span data-ttu-id="47335-248">La configuración incluye HTTP, no HTTPS:</span><span class="sxs-lookup"><span data-stu-id="47335-248">The configuration includes HTTP, not HTTPS:</span></span>

1. <span data-ttu-id="47335-249">En el Portal de Azure clásico, seleccione la máquina virtual y haga clic en Conectar.</span><span class="sxs-lookup"><span data-stu-id="47335-249">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="47335-250">En función de la configuración del explorador, es posible que se le solicite guardar un archivo .rdp para conectarse a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-250">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
   
    ![conectarse a máquina virtual de azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="47335-252">Use el nombre de la máquina virtual del usuario, el nombre de usuario y la contraseña que configuró al crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-252">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
   
    <span data-ttu-id="47335-253">Por ejemplo, en la siguiente imagen, el nombre de la máquina virtual es **ssrsnativecloud** y el nombre del usuario es **testuser**.</span><span class="sxs-lookup"><span data-stu-id="47335-253">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
   
    ![el inicio de sesión incluye la máquina virtual](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="47335-255">En la máquina virtual, abra **Windows PowerShell ISE** con privilegios administrativos.</span><span class="sxs-lookup"><span data-stu-id="47335-255">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="47335-256">El PowerShell ISE se instala de forma predeterminada en Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="47335-256">The PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="47335-257">Se recomienda utilizar el ISE en lugar de una ventana de Windows PowerShell estándar, por lo que puede pegar el script en el ISE, modificar el script y luego ejecutar el script.</span><span class="sxs-lookup"><span data-stu-id="47335-257">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span></span>
3. <span data-ttu-id="47335-258">En Windows PowerShell ISE, haga clic en el menú **Vista** y luego haga clic en **Mostrar panel de scripts**.</span><span class="sxs-lookup"><span data-stu-id="47335-258">In Windows PowerShell ISE, click the **View** menu and then click **Show Script Pane**.</span></span>
4. <span data-ttu-id="47335-259">Copie el siguiente script y pegue el script en el panel de scripts de Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="47335-259">Copy the following script, and paste the script into the Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change the value if you used a different port for the private HTTP endpoint when the VM was created.
   
        ## Set PowerShell execution policy to be able to run scripts
        Set-ExecutionPolicy RemoteSigned -Force
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change the version portion of the path to "v11" to use the script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting the web service URL ##
        write-host -foregroundcolor green "Setting the web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port $HTTPport (for local usage)
            write-host "Calling ReserveURL port $HTTPport"
            $r = $RSObject.ReserveURL('ReportServerWebService',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportServer port $HTTPport" 
   
        ## Setting the Database ##
        write-host -foregroundcolor green "Setting the Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating the database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script to create the database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes to sqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## Setting the Report Manager URL ##
   
        write-host -foregroundcolor green "Setting the Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port $HTTPport
            write-host "Calling ReserveURL for ReportManager, port $HTTPport"
            $r = $RSObject.ReserveURL('ReportManager',"http://+:$HTTPport",1033)
            CheckResult $r "ReserveURL for ReportManager port $HTTPport"
   
        write-host -foregroundcolor green "Open Firewall port for $HTTPport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $HTTPport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $HTTPport)” -Direction Inbound –Protocol TCP –LocalPort $HTTPport
            write-host "Added rule Report Server (TCP on port $HTTPport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
5. <span data-ttu-id="47335-260">Si ha creado la máquina virtual con un puerto HTTP distinto de 80, modifique el parámetro $HTTPport = 80.</span><span class="sxs-lookup"><span data-stu-id="47335-260">If you created the VM with an HTTP port other than 80, modify the parameter $HTTPport = 80.</span></span>
6. <span data-ttu-id="47335-261">El script está configurado actualmente para Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="47335-261">The script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="47335-262">Si quiere ejecutar el script para Reporting Services, modifique la parte de la versión de la ruta de acceso al espacio de nombres "v11", en la instrucción Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="47335-262">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span></span>
7. <span data-ttu-id="47335-263">Ejecute el script.</span><span class="sxs-lookup"><span data-stu-id="47335-263">Run the script.</span></span>

<span data-ttu-id="47335-264">**Validación**: para comprobar que la funcionalidad del servidor de informes básica es correcta, vea la sección [Comprobar la configuración](#verify-the-configuration) más adelante en este tema.</span><span class="sxs-lookup"><span data-stu-id="47335-264">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-configuration) section later in this topic.</span></span>

### <a name="use-script-to-configure-the-report-server-and-https"></a><span data-ttu-id="47335-265">Usar el script para configurar el servidor de informes y HTTPS</span><span class="sxs-lookup"><span data-stu-id="47335-265">Use script to configure the report server and HTTPS</span></span>
<span data-ttu-id="47335-266">Para usar Windows PowerShell para configurar el servidor de informes, complete los siguientes pasos.</span><span class="sxs-lookup"><span data-stu-id="47335-266">To use Windows PowerShell to configure the report server, complete the following steps.</span></span> <span data-ttu-id="47335-267">La configuración incluye HTTPS, no HTTP.</span><span class="sxs-lookup"><span data-stu-id="47335-267">The configuration includes HTTPS, not HTTP.</span></span>

1. <span data-ttu-id="47335-268">En el Portal de Azure clásico, seleccione la máquina virtual y haga clic en Conectar.</span><span class="sxs-lookup"><span data-stu-id="47335-268">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="47335-269">En función de la configuración del explorador, es posible que se le solicite guardar un archivo .rdp para conectarse a la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-269">Depending on your browser configuration, you may be prompted to save an .rdp file for connecting to the VM.</span></span>
   
    ![conectarse a máquina virtual de azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="47335-271">Use el nombre de la máquina virtual del usuario, el nombre de usuario y la contraseña que configuró al crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-271">Use the user VM name, user name and password you configured when you created the VM.</span></span> 
   
    <span data-ttu-id="47335-272">Por ejemplo, en la siguiente imagen, el nombre de la máquina virtual es **ssrsnativecloud** y el nombre del usuario es **testuser**.</span><span class="sxs-lookup"><span data-stu-id="47335-272">For example, in the following image, the VM name is **ssrsnativecloud** and the user name is **testuser**.</span></span>
   
    ![el inicio de sesión incluye la máquina virtual](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="47335-274">En la máquina virtual, abra **Windows PowerShell ISE** con privilegios administrativos.</span><span class="sxs-lookup"><span data-stu-id="47335-274">On the VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="47335-275">El PowerShell ISE se instala de forma predeterminada en Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="47335-275">The PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="47335-276">Se recomienda utilizar el ISE en lugar de una ventana de Windows PowerShell estándar, por lo que puede pegar el script en el ISE, modificar el script y luego ejecutar el script.</span><span class="sxs-lookup"><span data-stu-id="47335-276">It is recommended you use the ISE instead of a standard Windows PowerShell window so that you can paste the script into the ISE, modify the script, and then run the script.</span></span>
3. <span data-ttu-id="47335-277">Para habilitar la ejecución de scripts, ejecute el siguiente comando de Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="47335-277">To enable running scripts, run the following Windows PowerShell command:</span></span>
   
        Set-ExecutionPolicy RemoteSigned
   
    <span data-ttu-id="47335-278">Luego puede ejecutar lo siguiente para comprobar la directiva:</span><span class="sxs-lookup"><span data-stu-id="47335-278">You can then run the following to verify the policy:</span></span>
   
        Get-ExecutionPolicy
4. <span data-ttu-id="47335-279">En **Windows PowerShell ISE**, haga clic en el menú **Vista** y luego haga clic en **Mostrar panel de scripts**.</span><span class="sxs-lookup"><span data-stu-id="47335-279">In **Windows PowerShell ISE**, click the **View** menu and then click **Show Script Pane**.</span></span>
5. <span data-ttu-id="47335-280">Copie el siguiente script y péguelo en el panel de scripts de Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="47335-280">Copy the following script and paste it into the Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures the report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when the HTTPS endpoint was created.
   
        # You can run the following command to get (.cloudapp.net certificates) so you can copy the thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # The certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # the certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If the certificate is not a wildcard certificate, comment out the following line, and enable the full $DNSNAme reference.
        $DNSName="+"
        #$DNSName="$server.cloudapp.net"
        $DNSNameAndPort = $DNSName + ":$httpsport"
   
        ## Utility method for verifying an operation's result
        function CheckResult
        {
            param($wmi_result, $actionname)
            if ($wmi_result.HRESULT -ne 0) {
                write-error "$actionname failed. Error from WMI: $($wmi_result.Error)"
            }
        }
   
        $starttime=Get-Date
        write-host -foregroundcolor DarkGray $starttime StartTime
   
        ## ReportServer Database name - this can be changed if needed
        $dbName='ReportServer'
   
        write-host "The script will use $DNSNameAndPort as the DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change the version portion of the path to "v11" to use the script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting the web service URL ##
        write-host -foregroundcolor green "Setting the web service URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for ReportServer site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportServerWebService','ReportServer',1033)
            CheckResult $r "SetVirtualDirectory for ReportServer"
   
        ## ReserveURL for ReportServerWebService - port 80 (for local usage)
            write-host 'Calling ReserveURL port 80'
            $r = $RSObject.ReserveURL('ReportServerWebService','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportServer port 80" 
   
        ## ReserveURL for ReportServerWebService - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportServerWebService',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportServer port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportServerWebService port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport, with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportServerWebService',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportServer port $httpsport" 
   
        ## 2. Setting the Database ##
        write-host -foregroundcolor green "Setting the Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating the database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script to create the database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes to sqlserver provider
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## GenerateGrantRightsScript 
            $DBUser = "NT Service\ReportServer"
            write-host "Calling GenerateDatabaseRightsScript with user $DBUser"
            $r = $RSObject.GenerateDatabaseRightsScript($DBUser,$dbName,$false,$true)
            CheckResult $r "GenerateDatabaseRightsScript"
            $script = $r.Script
   
        ## Execute grant rights script
            write-host 'Executing Database Rights Script'
            $savedcvd = Get-Location
            cd sqlserver:\
            Invoke-SqlCmd -Query $script
            Set-Location $savedcvd
   
        ## SetDBConnection - uses Windows Service (type 2), username is ignored
            write-host "Calling SetDatabaseConnection server $server, DB $dbName"
            $r = $RSObject.SetDatabaseConnection($server,$dbName,2,'','')
            CheckResult $r "SetDatabaseConnection"  
   
        ## 3. Setting the Report Manager URL ##
   
        write-host -foregroundcolor green "Setting the Report Manager URL"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## SetVirtualDirectory for Reports (Report Manager) site
            write-host 'Calling SetVirtualDirectory'
            $r = $RSObject.SetVirtualDirectory('ReportManager','Reports',1033)
            CheckResult $r "SetVirtualDirectory"
   
        ## ReserveURL for ReportManager  - port 80
            write-host 'Calling ReserveURL for ReportManager, port 80'
            $r = $RSObject.ReserveURL('ReportManager','http://+:80',1033)
            CheckResult $r "ReserveURL for ReportManager port 80"
   
        ## ReserveURL for ReportManager - port $httpsport
            write-host "Calling ReserveURL port $httpsport, for URL: https://$DNSNameAndPort"
            $r = $RSObject.ReserveURL('ReportManager',"https://$DNSNameAndPort",1033)
            CheckResult $r "ReserveURL for ReportManager port $httpsport" 
   
        ## CreateSSLCertificateBinding for ReportManager port $httpsport
            write-host "Calling CreateSSLCertificateBinding port $httpsport with certificate hash: $certificatehash"
            $r = $RSObject.CreateSSLCertificateBinding('ReportManager',$certificatehash,'0.0.0.0',$httpsport,1033)
            CheckResult $r "CreateSSLCertificateBinding for ReportManager port $httpsport" 
   
        write-host -foregroundcolor green "Open Firewall port for $httpsport"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## Open Firewall port for $httpsport
            New-NetFirewallRule -DisplayName “Report Server (TCP on port $httpsport)” -Direction Inbound –Protocol TCP –LocalPort $httpsport
            write-host "Added rule Report Server (TCP on port $httpsport) in Windows Firewall"
   
        write-host 'Operations completed, Report Server is ready'
        write-host -foregroundcolor DarkGray $starttime StartTime
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
6. <span data-ttu-id="47335-281">Modifique el parámetro **$certificatehash** en el script:</span><span class="sxs-lookup"><span data-stu-id="47335-281">Modify the **$certificatehash** parameter in the script:</span></span>
   
   * <span data-ttu-id="47335-282">Se trata de un parámetro **obligatorio** .</span><span class="sxs-lookup"><span data-stu-id="47335-282">This is a **required** parameter.</span></span> <span data-ttu-id="47335-283">Si no ha guardado el valor de certificado de los pasos anteriores, use uno de los siguientes métodos para copiar el valor hash del certificado de la huella digital de certificados:</span><span class="sxs-lookup"><span data-stu-id="47335-283">If you did not save the certificate value from the previous steps, use one of the following methods to copy the certificate hash value from the certificates thumbprint.:</span></span>
     
       <span data-ttu-id="47335-284">En la máquina virtual, abra Windows PowerShell ISE y ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="47335-284">On the VM, open Windows PowerShell ISE and run the following command:</span></span>
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       <span data-ttu-id="47335-285">El resultado será similar al siguiente.</span><span class="sxs-lookup"><span data-stu-id="47335-285">The output will look similar to the following.</span></span> <span data-ttu-id="47335-286">Si el script devuelve una línea en blanco, la máquina virtual no tiene un certificado configurado; por ejemplo, consulte la sección [Para usar el certificado autofirmado de máquinas virtuales](#to-use-the-virtual-machines-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="47335-286">If the script returns a blank line, the VM does not have a certificate configured for example, see the section [To use the Virtual Machines Self-signed Certificate](#to-use-the-virtual-machines-self-signed-certificate).</span></span>
     
     <span data-ttu-id="47335-287">OR</span><span class="sxs-lookup"><span data-stu-id="47335-287">OR</span></span>
   * <span data-ttu-id="47335-288">En la máquina virtual, ejecute mmc.exe y luego agregue el complemento **Certificados** .</span><span class="sxs-lookup"><span data-stu-id="47335-288">On the VM Run mmc.exe and then add the **Certificates** snap-in.</span></span>
   * <span data-ttu-id="47335-289">En el nodo **Entidades de certificación raíz de confianza** , haga doble clic en el nombre del certificado.</span><span class="sxs-lookup"><span data-stu-id="47335-289">Under the **Trusted Root Certificate Authorities** node double-click your certificate name.</span></span> <span data-ttu-id="47335-290">Si está usando el certificado autofirmado de la máquina virtual, el certificado toma el nombre DNS de la máquina virtual y finaliza con **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="47335-290">If you are using the self-signed certificate of the VM, the certificate is named after the DNS name of the VM and ends with **cloudapp.net**.</span></span>
   * <span data-ttu-id="47335-291">Haga clic en la pestaña **Detalles** .</span><span class="sxs-lookup"><span data-stu-id="47335-291">Click the **Details** tab.</span></span>
   * <span data-ttu-id="47335-292">Haga clic en **Huella digital**.</span><span class="sxs-lookup"><span data-stu-id="47335-292">Click **Thumbprint**.</span></span> <span data-ttu-id="47335-293">El valor de la huella digital se muestra en el campo de detalles, por ejemplo, af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48.</span><span class="sxs-lookup"><span data-stu-id="47335-293">The value of the thumbprint is displayed in the details field, for example af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span></span>
   * <span data-ttu-id="47335-294">**Antes de ejecutar el script**, quite los espacios entre los pares de valores.</span><span class="sxs-lookup"><span data-stu-id="47335-294">**Before you run the script**, remove the spaces in between the pairs of values.</span></span> <span data-ttu-id="47335-295">Por ejemplo, af1160b64b288d890a8212ff6ba9c3664f319048.</span><span class="sxs-lookup"><span data-stu-id="47335-295">For example af1160b64b288d890a8212ff6ba9c3664f319048</span></span>
7. <span data-ttu-id="47335-296">Modifique el parámetro **$httpsport** :</span><span class="sxs-lookup"><span data-stu-id="47335-296">Modify the **$httpsport** parameter:</span></span> 
   
   * <span data-ttu-id="47335-297">Si usa el puerto 443 para el extremo HTTPS, no necesita actualizar este parámetro en el script.</span><span class="sxs-lookup"><span data-stu-id="47335-297">If you used port 443 for the HTTPS endpoint, then you do not need to update this parameter in the script.</span></span> <span data-ttu-id="47335-298">En caso contrario, use el valor de puerto que ha seleccionado al configurar el extremo privado de HTTPS en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-298">Otherwise use the port value you selected when you configured the HTTPS private endpoint on the VM.</span></span>
8. <span data-ttu-id="47335-299">Modifique el parámetro **$DNSName** :</span><span class="sxs-lookup"><span data-stu-id="47335-299">Modify the **$DNSName** parameter:</span></span> 
   
   * <span data-ttu-id="47335-300">El script se configura para un certificado comodín $DNSName="+".</span><span class="sxs-lookup"><span data-stu-id="47335-300">The script is configured for a wild card certificate $DNSName="+".</span></span> <span data-ttu-id="47335-301">Si no que quiere configurar para un enlace de certificado comodín, comente $DNSName ="+" y habilitar la siguiente línea, la referencia $DNSNAme completa, $DNSName="$server.cloudapp.net ##".</span><span class="sxs-lookup"><span data-stu-id="47335-301">If you do no want to configure for a wildcard certificate binding, comment out $DNSName="+" and enable the following line, the full $DNSNAme reference, ##$DNSName="$server.cloudapp.net".</span></span>
     
       <span data-ttu-id="47335-302">Cambie el valor de $DNSName si no quiere usar el nombre DNS de la máquina virtual para Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="47335-302">Change the $DNSName value if you do not want to use the virtual machine’s DNS name for Reporting Services.</span></span> <span data-ttu-id="47335-303">Si usa el parámetro, el certificado también debe usar este nombre y registrar el nombre globalmente en un servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="47335-303">If you use the parameter, the certificate must also use this name and you register the name globally on a DNS server.</span></span>
9. <span data-ttu-id="47335-304">El script está configurado actualmente para Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="47335-304">The script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="47335-305">Si quiere ejecutar el script para Reporting Services, modifique la parte de la versión de la ruta de acceso al espacio de nombres "v11", en la instrucción Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="47335-305">If you want to run the script for  Reporting Services, modify the version portion of the path to the namespace to “v11”, on the Get-WmiObject statement.</span></span>
10. <span data-ttu-id="47335-306">Ejecute el script.</span><span class="sxs-lookup"><span data-stu-id="47335-306">Run the script.</span></span>

<span data-ttu-id="47335-307">**Validación**: para comprobar que la funcionalidad del servidor de informes básica es correcta, vea la sección [Comprobar la configuración](#verify-the-connection) más adelante en este tema.</span><span class="sxs-lookup"><span data-stu-id="47335-307">**Validation**: To verify that the basic report server functionality is working, see the [Verify the configuration](#verify-the-connection) section later in this topic.</span></span> <span data-ttu-id="47335-308">Para comprobar el enlace de certificado, abra un símbolo del sistema con privilegios administrativos y luego ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="47335-308">To verify the certificate binding open a command prompt with administrative privileges, and then run the following command:</span></span>

    netsh http show sslcert

<span data-ttu-id="47335-309">El resultado incluirá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="47335-309">The result will include the following:</span></span>

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-to-configure-the-report-server"></a><span data-ttu-id="47335-310">Usar el Administrador de configuración para configurar el Servidor de informes</span><span class="sxs-lookup"><span data-stu-id="47335-310">Use Configuration Manager to Configure the Report Server</span></span>
<span data-ttu-id="47335-311">Si no quiere ejecutar el script de PowerShell para configurar el servidor de informes, siga los pasos de esta sección para usar el administrador de configuración del modo nativo de Reporting Services para configurar el servidor de informes.</span><span class="sxs-lookup"><span data-stu-id="47335-311">If you do not want to run the PowerShell script to configure the report server, follow the steps in this section to use the Reporting Services native mode configuration manager to configure the report server.</span></span>

1. <span data-ttu-id="47335-312">En el Portal de Azure clásico, seleccione la máquina virtual y haga clic en Conectar.</span><span class="sxs-lookup"><span data-stu-id="47335-312">From the Azure classic portal, select the VM and click connect.</span></span> <span data-ttu-id="47335-313">Use el nombre de usuario y la contraseña que configuró al crear la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-313">Use the user name and password you configured when you created the VM.</span></span>
   
    ![conectarse a máquina virtual de azure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. <span data-ttu-id="47335-315">Ejecute Windows Update e instale las actualizaciones en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-315">Run Windows update and install updates to the VM.</span></span> <span data-ttu-id="47335-316">Si se requiere un reinicio de la máquina virtual, reinicie la máquina virtual y vuelva a conectarse a la máquina virtual desde el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="47335-316">If a restart of the VM is required, restart the VM and reconnect to the VM from the Azure classic portal.</span></span>
3. <span data-ttu-id="47335-317">En el menú Inicio de la máquina virtual, escriba **Reporting Services** y abra el **Administrador de configuración de Reporting Services**.</span><span class="sxs-lookup"><span data-stu-id="47335-317">From the Start menu on the VM, type **Reporting Services** and open **Reporting Services Configuration Manager**.</span></span>
4. <span data-ttu-id="47335-318">Deje los valores predeterminados para **Nombre del servidor** e **Instancia del servidor de informes**.</span><span class="sxs-lookup"><span data-stu-id="47335-318">Leave the default values for **Server Name** and **Report Server Instance**.</span></span> <span data-ttu-id="47335-319">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="47335-319">Click **Connect**.</span></span>
5. <span data-ttu-id="47335-320">En el panel izquierdo, haga clic en **URL de servicio web**.</span><span class="sxs-lookup"><span data-stu-id="47335-320">In the left pane, click **Web Service URL**.</span></span>
6. <span data-ttu-id="47335-321">De forma predeterminada, RS está configurado para el puerto 80 HTTP con la IP "Todas asignadas".</span><span class="sxs-lookup"><span data-stu-id="47335-321">By default, RS is configured for HTTP port 80 with IP “All Assigned”.</span></span> <span data-ttu-id="47335-322">Para agregar HTTPS:</span><span class="sxs-lookup"><span data-stu-id="47335-322">To add HTTPS:</span></span>
   
   1. <span data-ttu-id="47335-323">En **Certificado SSL**, seleccione el certificado que quiere usar, por ejemplo, [nombre de máquina virtual].cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="47335-323">In **SSL Certificate**: select the certificate you want to use, for example [VM name].cloudapp.net.</span></span> <span data-ttu-id="47335-324">Si no aparece ningún certificado, consulte la sección **Paso 2: crear un certificado de servidor** para más información sobre cómo instalar y confiar en el certificado en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-324">If no certificates are listed, see the section **Step 2: Create a Server Certificate** for information on how to install and trust the certificate on the VM.</span></span>
   2. <span data-ttu-id="47335-325">En **Puerto SSL**: elija 443.</span><span class="sxs-lookup"><span data-stu-id="47335-325">Under **SSL Port**: choose 443.</span></span> <span data-ttu-id="47335-326">Si ha configurado el extremo privado HTTPS en la máquina virtual con otro puerto privado, use ese valor aquí.</span><span class="sxs-lookup"><span data-stu-id="47335-326">If you configured the HTTPS private endpoint in the VM with a different private port, use that value here.</span></span>
   3. <span data-ttu-id="47335-327">Haga clic en **Aplicar** y espere a que finalice la operación.</span><span class="sxs-lookup"><span data-stu-id="47335-327">Click **Apply** and wait for the operation to complete.</span></span>
7. <span data-ttu-id="47335-328">En el panel izquierdo, haga clic en **Base de datos**.</span><span class="sxs-lookup"><span data-stu-id="47335-328">In the left pane, click **Database**.</span></span>
   
   1. <span data-ttu-id="47335-329">Haga clic en **Cambiar base de datos**.</span><span class="sxs-lookup"><span data-stu-id="47335-329">Click **Change Databas**e.</span></span>
   2. <span data-ttu-id="47335-330">Haga clic en **Crear una nueva base de datos del servidor de informes** y luego en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="47335-330">Click **Create a new report server database** and then click **Next**.</span></span>
   3. <span data-ttu-id="47335-331">Deje el valor de **nombre de servidor** predeterminado como el nombre de la máquina virtual y deje el valor de **tipo de autenticación** predeterminado como **Usuario actual** – **Seguridad integrada**.</span><span class="sxs-lookup"><span data-stu-id="47335-331">Leave the default **Server Name**: as the VM name and leave the default **Authentication Type** as **Current User** – **Integrated Security**.</span></span> <span data-ttu-id="47335-332">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="47335-332">Click **Next**.</span></span>
   4. <span data-ttu-id="47335-333">Deje el **nombre de base de datos** predeterminado como **ReportServer** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="47335-333">Leave the default **Database Name** as **ReportServer** and click **Next**.</span></span>
   5. <span data-ttu-id="47335-334">Deje el valor de **Tipo de autenticación** predeterminado como **Credenciales de servicio** y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="47335-334">Leave the default **Authentication Type** as **Service Credentials** and click **Next**.</span></span>
   6. <span data-ttu-id="47335-335">Haga clic en **Siguiente** on the **Resumen** .</span><span class="sxs-lookup"><span data-stu-id="47335-335">Click **Next** on the **Summary** page.</span></span>
   7. <span data-ttu-id="47335-336">Cuando haya completado la configuración, haga clic en **Finalizar**.</span><span class="sxs-lookup"><span data-stu-id="47335-336">When the configuration is complete, click **Finish**.</span></span>
8. <span data-ttu-id="47335-337">En el panel izquierdo, haga clic en **URL de Administrador de informes**.</span><span class="sxs-lookup"><span data-stu-id="47335-337">In the left pane, click **Report Manager URL**.</span></span> <span data-ttu-id="47335-338">Deje el valor de **Directorio virtual** predeterminado como **Informes** y haga clic en **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="47335-338">Leave the default **Virtual Directory** as **Reports** and click **Apply**.</span></span>
9. <span data-ttu-id="47335-339">Haga clic en **Salir** para cerrar el Administrador de configuración de Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="47335-339">Click **Exit** to close the Reporting Services Configuration Manager.</span></span>

## <a name="step-4-open-windows-firewall-port"></a><span data-ttu-id="47335-340">Paso 4: abrir el puerto de Firewall de Windows</span><span class="sxs-lookup"><span data-stu-id="47335-340">Step 4: Open Windows Firewall Port</span></span>
> [!NOTE]
> <span data-ttu-id="47335-341">Si ha usado uno de los scripts para configurar el servidor de informes, puede omitir esta sección.</span><span class="sxs-lookup"><span data-stu-id="47335-341">If you used one of the scripts to configure the report server, you can skip this section.</span></span> <span data-ttu-id="47335-342">El script incluía un paso para abrir el puerto de firewall.</span><span class="sxs-lookup"><span data-stu-id="47335-342">The script included a step to open the firewall port.</span></span> <span data-ttu-id="47335-343">El valor predeterminado era el puerto 80 para HTTP y el puerto 443 para HTTPS.</span><span class="sxs-lookup"><span data-stu-id="47335-343">The default was port 80 for HTTP and port 443 for HTTPS.</span></span>
> 
> 

<span data-ttu-id="47335-344">Para conectarse de forma remota al Administrador de informes o al Servidor de informes en la máquina virtual, se requiere un extremo TCP en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-344">To connect remotely to Report Manager or the Report Server on the virtual machine, a TCP Endpoint is required on the VM.</span></span> <span data-ttu-id="47335-345">Se requiere abrir el mismo puerto en el firewall de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-345">It is required to open the same port in the VM’s firewall.</span></span> <span data-ttu-id="47335-346">El extremo se creó cuando se aprovisionó la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-346">The endpoint was created when the VM was provisioned.</span></span>

<span data-ttu-id="47335-347">En esta sección se ofrece información básica sobre cómo abrir el puerto de firewall.</span><span class="sxs-lookup"><span data-stu-id="47335-347">This section provides basic information on how to open the firewall port.</span></span> <span data-ttu-id="47335-348">Para más información, consulte [Configurar un firewall para el acceso del Servidor de informes](https://technet.microsoft.com/library/bb934283.aspx)</span><span class="sxs-lookup"><span data-stu-id="47335-348">For more information, see [Configure a Firewall for Report Server Access](https://technet.microsoft.com/library/bb934283.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="47335-349">Si ha usado el script para configurar el servidor de informes, puede omitir esta sección.</span><span class="sxs-lookup"><span data-stu-id="47335-349">If you used the script to configure the report server, you can skip this section.</span></span> <span data-ttu-id="47335-350">El script incluía un paso para abrir el puerto de firewall.</span><span class="sxs-lookup"><span data-stu-id="47335-350">The script included a step to open the firewall port.</span></span>
> 
> 

<span data-ttu-id="47335-351">Si configuró un puerto privado para HTTPS distinto de 443, modifique el siguiente script correctamente.</span><span class="sxs-lookup"><span data-stu-id="47335-351">If you configured a private port for HTTPS other than 443, modify the following script appropriately.</span></span> <span data-ttu-id="47335-352">Para abrir el puerto **443** en el Firewall de Windows, realice los pasos siguientes:</span><span class="sxs-lookup"><span data-stu-id="47335-352">To open port **443** on the Windows Firewall, complete the following:</span></span>

1. <span data-ttu-id="47335-353">Abra la ventana de Windows PowerShell con privilegios administrativos.</span><span class="sxs-lookup"><span data-stu-id="47335-353">Open a Windows PowerShell window with administrative privileges.</span></span>
2. <span data-ttu-id="47335-354">Si ha usado un puerto distinto de 443 al configurar el extremo HTTPS en la máquina virtual, actualice el puerto en el siguiente comando y luego ejecute el comando:</span><span class="sxs-lookup"><span data-stu-id="47335-354">If you used a port other than 443 when you configured the HTTPS endpoint on the VM, update the port in the following command and then run the command:</span></span>
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. <span data-ttu-id="47335-355">Cuando finalice el comando, aparece **Aceptar** en el símbolo del sistema.</span><span class="sxs-lookup"><span data-stu-id="47335-355">When the command completes, **Ok** is displayed in the command prompt.</span></span>

<span data-ttu-id="47335-356">Para comprobar que se abre el puerto, abra una ventana de Windows PowerShell y ejecute el siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="47335-356">To verify that the port is opened, open a Windows PowerShell window and run the following command:</span></span>

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-the-configuration"></a><span data-ttu-id="47335-357">Comprobar la configuración</span><span class="sxs-lookup"><span data-stu-id="47335-357">Verify the configuration</span></span>
<span data-ttu-id="47335-358">Para comprobar que la funcionalidad del servidor de informes básica funciona, abra su explorador con privilegios administrativos y luego vaya hasta las siguientes URL del administrador de informes y del servidor de informes:</span><span class="sxs-lookup"><span data-stu-id="47335-358">To verify that the basic report server functionality is now working, open your browser with administrative privileges and then browse to the following report server ad report manager URLS:</span></span>

* <span data-ttu-id="47335-359">En la máquina virtual, examine hasta la dirección URL del servidor de informes:</span><span class="sxs-lookup"><span data-stu-id="47335-359">On the VM, browse to the report server URL:</span></span>
  
        http://localhost/reportserver
* <span data-ttu-id="47335-360">En la máquina virtual, examine hasta la dirección URL del administrador de informes:</span><span class="sxs-lookup"><span data-stu-id="47335-360">On the VM, browse to the report manger URL:</span></span>
  
        http://localhost/Reports
* <span data-ttu-id="47335-361">Desde el equipo local, vaya al Administrador de informes **remoto** en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-361">From your local computer, browse to the **remote** report Manager on the VM.</span></span> <span data-ttu-id="47335-362">Actualice el nombre DNS en el ejemplo siguiente, según corresponda.</span><span class="sxs-lookup"><span data-stu-id="47335-362">Update the DNS name in the following example as appropriate.</span></span> <span data-ttu-id="47335-363">Cuando se le pida una contraseña, use las credenciales de administrador que creó cuando se aprovisionó la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-363">When prompted for a password, use the administrator credentials you created when the VM was provisioned.</span></span> <span data-ttu-id="47335-364">El nombre de usuario se encuentra en el formato [Dominio]\[nombre de usuario], donde el dominio es el nombre de equipo de la máquina virtual, por ejemplo, ssrsnativecloud\testuser.</span><span class="sxs-lookup"><span data-stu-id="47335-364">The user name is in the [Domain]\[user name] format, where the domain is the VM computer name, for example ssrsnativecloud\testuser.</span></span> <span data-ttu-id="47335-365">Si no está usando HTTP**S**, quite la **s** de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="47335-365">If you are not using HTTP**S**, remove the **s** in the URL.</span></span> <span data-ttu-id="47335-366">Vea la siguiente sección para obtener información sobre cómo crear usuarios adicionales en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-366">See the next section for information on creating additional users on VM.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/Reports
* <span data-ttu-id="47335-367">Desde el equipo local, vaya a la URL del servidor de informes remoto.</span><span class="sxs-lookup"><span data-stu-id="47335-367">From your local computer, browse to the remote report server URL.</span></span> <span data-ttu-id="47335-368">Actualice el nombre DNS en el ejemplo siguiente, según corresponda.</span><span class="sxs-lookup"><span data-stu-id="47335-368">Update the DNS name in the following example as appropriate.</span></span> <span data-ttu-id="47335-369">Si no está usando HTTPS, quite la s de la dirección URL.</span><span class="sxs-lookup"><span data-stu-id="47335-369">If you are not using HTTPS, remove the s in the URL.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a><span data-ttu-id="47335-370">Crear usuarios y asignar roles</span><span class="sxs-lookup"><span data-stu-id="47335-370">Create Users and Assign Roles</span></span>
<span data-ttu-id="47335-371">Después de configurar y comprobar el servidor de informes, una tarea administrativa común es crear uno o más usuarios y asignar usuarios a roles de Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="47335-371">After configuring and verifying the report server, a common administrative task is to create one or more users and assign users to Reporting Services roles.</span></span> <span data-ttu-id="47335-372">Para obtener más información, consulte los temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="47335-372">For more information, see the following:</span></span>

* [<span data-ttu-id="47335-373">Crear una cuenta de usuarios local</span><span class="sxs-lookup"><span data-stu-id="47335-373">Create a local user account</span></span>](https://technet.microsoft.com/library/cc770642.aspx)
* <span data-ttu-id="47335-374">[Conceder a un usuario acceso a un servidor de informes (Administrador de informes)](https://msdn.microsoft.com/library/ms156034.aspx)</span><span class="sxs-lookup"><span data-stu-id="47335-374">[Grant User Access to a Report Server (Report Manager)](https://msdn.microsoft.com/library/ms156034.aspx))</span></span>
* [<span data-ttu-id="47335-375">Crear y administrar asignaciones de roles</span><span class="sxs-lookup"><span data-stu-id="47335-375">Create and Manage Role Assignments</span></span>](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="to-create-and-publish-reports-to-the-azure-virtual-machine"></a><span data-ttu-id="47335-376">Para crear y publicar informes en la máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="47335-376">To Create and Publish Reports to the Azure Virtual Machine</span></span>
<span data-ttu-id="47335-377">En la tabla siguiente se resumen algunas de las opciones disponibles para publicar los informes existentes desde un equipo local al servidor de informes hospedados en la máquina virtual de Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="47335-377">The following table summarizes some of the options available to publish existing reports from an on-premises computer to the report server hosted on the Microsoft Azure Virtual Machine:</span></span>

* <span data-ttu-id="47335-378">**Script de RS.exe**: use el script de RS.exe para copiar elementos de informes desde la máquina virtual de Microsoft Azure y el servidor de informes existente en ella.</span><span class="sxs-lookup"><span data-stu-id="47335-378">**RS.exe script**: Use RS.exe script to copy report items from and existing report server to your Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="47335-379">Para más información, consulte la sección "Modo nativo a modo nativo: máquina virtual de Microsoft Azure" en [Script de rs.exe de Reporting Services de ejemplo para migrar contenido entre servidores de informes](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="47335-379">For more information, see the section “Native mode to Native Mode – Microsoft Azure Virtual Machine” in [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>
* <span data-ttu-id="47335-380">**Generador de informes**: la máquina virtual incluye la versión de un solo clic del Generador de informes de Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="47335-380">**Report Builder**: The virtual machine includes the click-once version of Microsoft SQL Server Report Builder.</span></span> <span data-ttu-id="47335-381">Para iniciar el Generador de informes por primera vez en la máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="47335-381">To start Report builder the first time on the virtual machine:</span></span>
  
  1. <span data-ttu-id="47335-382">Inicie el explorador con privilegios administrativos.</span><span class="sxs-lookup"><span data-stu-id="47335-382">Start your browser with administrative privileges.</span></span>
  2. <span data-ttu-id="47335-383">Vaya hasta el administrador de informes en la máquina virtual y haga clic en el **Generador de informes** en la cinta de opciones.</span><span class="sxs-lookup"><span data-stu-id="47335-383">Browse to report manager on the virtual machine and click **Report Builder**  in the ribbon.</span></span>
     
     <span data-ttu-id="47335-384">Para más información, consulte [Instalar, desinstalar y asistencia del Generador de informes](https://technet.microsoft.com/library/dd207038.aspx).</span><span class="sxs-lookup"><span data-stu-id="47335-384">For more information, see [Installing, Uninstalling, and Supporting Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span></span>
* <span data-ttu-id="47335-385">**SQL Server Data Tools: máquina virtual** si ha creado la máquina virtual con SQL Server 2012, SQL Server Data Tools se instala en la máquina virtual y se puede usar para crear **proyectos del Servidor de informes** e informes en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-385">**SQL Server Data Tools: VM**:  If you created the VM with SQL Server 2012, then SQL Server Data Tools is installed on the virtual machine and can be used to create **Report Server Projects** and reports on the virtual machine.</span></span> <span data-ttu-id="47335-386">SQL Server Data Tools puede publicar los informes en el servidor de informes en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-386">SQL Server Data Tools can publish the reports to the report server on the virtual machine.</span></span>
  
    <span data-ttu-id="47335-387">Si ha creado la máquina virtual con SQL server 2014, puede instalar SQL Server Data Tools- BI para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="47335-387">If you created the VM with SQL server 2014, you can install SQL Server Data Tools- BI for visual Studio.</span></span> <span data-ttu-id="47335-388">Para obtener más información, consulte los temas siguientes:</span><span class="sxs-lookup"><span data-stu-id="47335-388">For more information, see the following:</span></span>
  
  * [<span data-ttu-id="47335-389">Microsoft SQL Server Data Tools - Business Intelligence para Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="47335-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span></span>](https://www.microsoft.com/download/details.aspx?id=42313)
  * [<span data-ttu-id="47335-390">Microsoft SQL Server Data Tools - Business Intelligence para Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="47335-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=36843)
  * [<span data-ttu-id="47335-391">SQL Server Data Tools y SQL Server Business Intelligence (SSDT-BI)</span><span class="sxs-lookup"><span data-stu-id="47335-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span></span>](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* <span data-ttu-id="47335-392">**SQL Server Data Tools: remoto**: en el equipo local, cree un proyecto de Reporting Services en SQL Server Data Tools que contenga informes de Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="47335-392">**SQL Server Data Tools: Remote**:  On your local computer, create a Reporting Services project in SQL Server Data Tools that contains Reporting Services reports.</span></span> <span data-ttu-id="47335-393">Configure el proyecto para que se conecte a la dirección URL del servicio web.</span><span class="sxs-lookup"><span data-stu-id="47335-393">Configure the project to connect to the web service URL.</span></span>
  
    ![propiedades del proyecto de ssdt para proyecto SSRS](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* <span data-ttu-id="47335-395">**Usar script**: use el script para copiar el contenido del servidor de informes.</span><span class="sxs-lookup"><span data-stu-id="47335-395">**Use script**: Use script to copy report server content.</span></span> <span data-ttu-id="47335-396">Para obtener más información, vea [Script de rs.exe de Reporting Services de ejemplo para migrar contenido entre servidores de informes](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="47335-396">For more information, see [Sample Reporting Services rs.exe Script to Migrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>

## <a name="minimize-cost-if-you-are-not-using-the-vm"></a><span data-ttu-id="47335-397">Minimizar el costo si no está usando la máquina virtual</span><span class="sxs-lookup"><span data-stu-id="47335-397">Minimize cost if you are not using the VM</span></span>
> [!NOTE]
> <span data-ttu-id="47335-398">Para minimizar los costos de las máquinas virtuales de Azure cuando no estén en uso, apague la máquina virtual desde el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="47335-398">To minimize charges for your Azure Virtual Machines when not in use, shut down the VM from the Azure classic portal.</span></span> <span data-ttu-id="47335-399">Si usa las opciones de energía de Windows dentro de una máquina virtual para apagar la máquina virtual, se le seguirá cobrando el mismo importe para la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="47335-399">If you use the Windows power options inside a VM to shut down the VM, you are still charged the same amount for the VM.</span></span> <span data-ttu-id="47335-400">Para reducir los costos, deberá apagar la máquina virtual en el Portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="47335-400">To reduce charges, you need to shut down the VM in the Azure classic portal.</span></span> <span data-ttu-id="47335-401">Si ya no necesita la máquina virtual, recuerde eliminar la máquina virtual y los archivos .vhd asociados para evitar costos de almacenamiento. Para más información, consulte la sección de preguntas más frecuentes en [Detalles de precios de máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="47335-401">If you no longer need the VM, remember to delete the VM and the associated .vhd files to avoid storage charges.For more information, see the FAQ section at [Virtual Machines Pricing Details](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>

## <a name="more-information"></a><span data-ttu-id="47335-402">Más información</span><span class="sxs-lookup"><span data-stu-id="47335-402">More Information</span></span>
### <a name="resources"></a><span data-ttu-id="47335-403">Recursos</span><span class="sxs-lookup"><span data-stu-id="47335-403">Resources</span></span>
* <span data-ttu-id="47335-404">Para consultar contenido similar relacionado con una implementación de servidor único de SQL Server Business Intelligence y SharePoint 2013, consulte [Usar Windows PowerShell para crear una máquina virtual de Azure con SQL Server BI y SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span><span class="sxs-lookup"><span data-stu-id="47335-404">For similar content related to a single server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Use Windows PowerShell to Create an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span></span>
* <span data-ttu-id="47335-405">Para consultar contenido similar relacionado con una implementación de varios servidores de SQL Server Business Intelligence y SharePoint 2013, consulte [Implementar SQL Server Business Intelligence en máquinas virtuales de Azure](https://msdn.microsoft.com/library/dn321998.aspx).</span><span class="sxs-lookup"><span data-stu-id="47335-405">For similar content related to a multi-server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span></span>
* <span data-ttu-id="47335-406">Para consultar información similar relacionada con implementaciones de SQL Server Business Intelligence en Máquinas virtuales de Azure, consulte [SQL Server Business Intelligence en Máquinas virtuales de Azure](virtual-machines-windows-classic-ps-sql-bi.md).</span><span class="sxs-lookup"><span data-stu-id="47335-406">For General information related to deployments of SQL Server Business Intelligence in Azure Virtual Machines, see [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span></span>
* <span data-ttu-id="47335-407">Para más información sobre el costo de procesos de Azure, consulte la pestaña Máquinas virtuales de la [Calculadora de precios de Azure](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="47335-407">For more information about the cost of Azure compute charges, see the Virtual Machines tab of [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span></span>

### <a name="community-content"></a><span data-ttu-id="47335-408">Contenido de la Comunidad</span><span class="sxs-lookup"><span data-stu-id="47335-408">Community Content</span></span>
* <span data-ttu-id="47335-409">Para ver instrucciones paso a paso sobre cómo crear un servidor de informes de modo nativo de Reporting Services sin usar el script, consulte [Hospedar el servicio de SQL Reporting en la máquina virtual de Azure](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span><span class="sxs-lookup"><span data-stu-id="47335-409">For step by step instructions on how to create a Reporting Services Native mode report server without using script, see [Hosting SQL Reporting Service on Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span></span>

### <a name="links-to-other-resources-for-sql-server-in-azure-vms"></a><span data-ttu-id="47335-410">Vínculos a otros recursos para SQL Server en máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="47335-410">Links to other resources for SQL Server in Azure VMs</span></span>
[<span data-ttu-id="47335-411">Información general sobre SQL Server en máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="47335-411">SQL Server on Azure Virtual Machines Overview</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

