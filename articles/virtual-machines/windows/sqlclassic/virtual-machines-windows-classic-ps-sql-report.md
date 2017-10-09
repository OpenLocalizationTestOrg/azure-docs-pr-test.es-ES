---
title: "aaaUse PowerShell tooCreate una máquina virtual con unas Native Mode Report Server | Documentos de Microsoft"
description: "Este tema describe y le guía a través de la implementación de Hola y configuración de un servidor de informes de modo nativo de SQL Server Reporting Services en una máquina Virtual de Azure. "
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
ms.openlocfilehash: e7791199c87dff106132f1535da12de40a8dbc9c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocreate-an-azure-vm-with-a-native-mode-report-server"></a><span data-ttu-id="da45d-103">Usar PowerShell tooCreate un Azure VM con un modo de servidor de informes nativo</span><span class="sxs-lookup"><span data-stu-id="da45d-103">Use PowerShell tooCreate an Azure VM With a Native Mode Report Server</span></span>
> [!IMPORTANT] 
> <span data-ttu-id="da45d-104">Azure tiene dos modelos de implementación diferentes para crear recursos y trabajar con ellos: [Resource Manager y el clásico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="da45d-104">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="da45d-105">Este artículo tratan con modelo de implementación de hello clásico.</span><span class="sxs-lookup"><span data-stu-id="da45d-105">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="da45d-106">Microsoft recomienda que más nuevas implementaciones de usar el modelo del Administrador de recursos de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-106">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="da45d-107">Este tema describe y le guía a través de la implementación de Hola y configuración de un servidor de informes de modo nativo de SQL Server Reporting Services en una máquina Virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="da45d-107">This topic describes and walks you through hello deployment and configuration of a SQL Server Reporting Services native mode report server in an Azure Virtual Machine.</span></span> <span data-ttu-id="da45d-108">Hola pasos de este documento, use una combinación de máquina virtual de pasos manuales toocreate hello y una secuencia de comandos de Windows PowerShell tooconfigure Reporting Services en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="da45d-108">hello steps in this document use a combination of manual steps toocreate hello virtual machine and a Windows PowerShell script tooconfigure Reporting Services on hello VM.</span></span> <span data-ttu-id="da45d-109">script de configuración de Hello incluye abrir un puerto de firewall para HTTP o HTTPs.</span><span class="sxs-lookup"><span data-stu-id="da45d-109">hello configuration script includes opening a firewall port for HTTP or HTTPs.</span></span>

> [!NOTE]
> <span data-ttu-id="da45d-110">Si no es necesario que **HTTPS** en el servidor de informes de hello, **omita el paso 2**.</span><span class="sxs-lookup"><span data-stu-id="da45d-110">If you do not require **HTTPS** on hello report server, **skip step 2**.</span></span>
> 
> <span data-ttu-id="da45d-111">Después de crear Hola VM en el paso 1, vaya toohello sección usar script tooconfigure Hola servidor de informes y HTTP.</span><span class="sxs-lookup"><span data-stu-id="da45d-111">After creating hello VM in step 1, go toohello section Use script tooconfigure hello report server and HTTP.</span></span> <span data-ttu-id="da45d-112">Después de ejecutar script de Hola, servidor de informes de hello es toouse listo.</span><span class="sxs-lookup"><span data-stu-id="da45d-112">After you run hello script, hello report server is ready toouse.</span></span>

## <a name="prerequisites-and-assumptions"></a><span data-ttu-id="da45d-113">Requisitos previos y suposiciones</span><span class="sxs-lookup"><span data-stu-id="da45d-113">Prerequisites and Assumptions</span></span>
* <span data-ttu-id="da45d-114">**Suscripción de Azure**: Compruebe el número de Hola de núcleos disponibles en su suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="da45d-114">**Azure Subscription**: Verify hello number of cores available in your Azure Subscription.</span></span> <span data-ttu-id="da45d-115">Si creas Hola recomendada tamaño de memoria virtual **A3**, necesita **4** núcleos disponibles.</span><span class="sxs-lookup"><span data-stu-id="da45d-115">If you create hello recommended VM size of **A3**, you need **4** available cores.</span></span> <span data-ttu-id="da45d-116">Si usa un tamaño de máquina virtual de **A2**, necesita **2** núcleos disponibles.</span><span class="sxs-lookup"><span data-stu-id="da45d-116">If you use a VM size of **A2**, you need **2** available cores.</span></span>
  
  * <span data-ttu-id="da45d-117">límite de núcleos de hello tooverify de su suscripción, Hola portal de Azure clásico, haga clic en configuración en el panel izquierdo de hello y, a continuación, haga clic en uso en el menú superior Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-117">tooverify hello core limit of your subscription, in hello Azure classic portal, click SETTINGS in hello left pane and then Click USAGE in hello top menu.</span></span>
  * <span data-ttu-id="da45d-118">cuota de núcleos de hello tooincrease, póngase en contacto con [soporte técnico de Azure](https://azure.microsoft.com/support/options/).</span><span class="sxs-lookup"><span data-stu-id="da45d-118">tooincrease hello core quota, contact [Azure Support](https://azure.microsoft.com/support/options/).</span></span> <span data-ttu-id="da45d-119">Para obtener más información sobre el tamaño de la máquina virtual, consulte [Tamaños de máquinas virtuales para Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="da45d-119">For VM size information, see [Virtual Machine Sizes for Azure](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
* <span data-ttu-id="da45d-120">**Script de Windows PowerShell**: tema Hola se da por supuesto que tiene conocimientos prácticos básicos de Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="da45d-120">**Windows PowerShell Scripting**: hello topic assumes that you have a basic working knowledge of Windows PowerShell.</span></span> <span data-ttu-id="da45d-121">Para obtener más información sobre cómo usar Windows PowerShell, vea Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="da45d-121">For more information about using Windows PowerShell, see hello following:</span></span>
  
  * [<span data-ttu-id="da45d-122">Inicio de Windows PowerShell en Windows Server</span><span class="sxs-lookup"><span data-stu-id="da45d-122">Starting Windows PowerShell on Windows Server</span></span>](https://technet.microsoft.com/library/hh847814.aspx)
  * [<span data-ttu-id="da45d-123">Introducción a Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="da45d-123">Getting Started with Windows PowerShell</span></span>](https://technet.microsoft.com/library/hh857337.aspx)

## <a name="step-1-provision-an-azure-virtual-machine"></a><span data-ttu-id="da45d-124">Paso 1: Aprovisionar una máquina virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="da45d-124">Step 1: Provision an Azure Virtual Machine</span></span>
1. <span data-ttu-id="da45d-125">Examinar toohello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="da45d-125">Browse toohello Azure classic portal.</span></span>
2. <span data-ttu-id="da45d-126">Haga clic en **máquinas virtuales** en el panel izquierdo de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-126">Click **Virtual Machines** in hello left pane.</span></span>
   
    ![máquinas virtuales de microsoft azure](./media/virtual-machines-windows-classic-ps-sql-report/IC660124.gif)
3. <span data-ttu-id="da45d-128">Haga clic en **Nuevo**.</span><span class="sxs-lookup"><span data-stu-id="da45d-128">Click **New**.</span></span>
   
    ![botón nuevo](./media/virtual-machines-windows-classic-ps-sql-report/IC692019.gif)
4. <span data-ttu-id="da45d-130">Haga clic en **De la galería**.</span><span class="sxs-lookup"><span data-stu-id="da45d-130">Click **From Gallery**.</span></span>
   
    ![nueva máquina virtual de la galería](./media/virtual-machines-windows-classic-ps-sql-report/IC692020.gif)
5. <span data-ttu-id="da45d-132">Haga clic en **SQL Server 2014 RTM Standard: Windows Server 2012 R2** y, a continuación, haga clic en hello flecha toocontinue.</span><span class="sxs-lookup"><span data-stu-id="da45d-132">Click **SQL Server 2014 RTM Standard – Windows Server 2012 R2** and then click hello arrow toocontinue.</span></span>
   
    ![Siguiente](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
   
    <span data-ttu-id="da45d-134">Si necesita datos de Reporting Services de hello controlada por la característica de suscripciones, elija **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span><span class="sxs-lookup"><span data-stu-id="da45d-134">If you need hello Reporting Services data driven subscriptions feature, choose **SQL Server 2014 RTM Enterprise – Windows Server 2012 R2**.</span></span> <span data-ttu-id="da45d-135">Para obtener más información sobre las ediciones de SQL Server y compatibilidad con las características, vea [características compatibles con las ediciones de SQL Server 2012 hello](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span><span class="sxs-lookup"><span data-stu-id="da45d-135">For more information on SQL Server editions and feature support, see [Features Supported by hello Editions of SQL Server 2012](https://msdn.microsoft.com/library/cc645993.aspx#Reporting).</span></span>
6. <span data-ttu-id="da45d-136">En hello **configuración de máquina Virtual** página, edite Hola siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="da45d-136">On hello **Virtual machine configuration** page, edit hello following fields:</span></span>
   
   * <span data-ttu-id="da45d-137">Si hay más de un **versión fecha**, seleccione Hola versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="da45d-137">If there is more than one **VERSION RELEASE DATE**, select hello most recent version.</span></span>
   * <span data-ttu-id="da45d-138">**Nombre de máquina virtual**: nombre de la máquina de hello también se utiliza en la siguiente página de configuración de hello como nombre DNS del servicio de nube de hello predeterminado.</span><span class="sxs-lookup"><span data-stu-id="da45d-138">**Virtual Machine Name**: hello machine name is also used on hello next configuration page as hello default Cloud Service DNS name.</span></span> <span data-ttu-id="da45d-139">nombre DNS de Hello debe ser único en hello servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="da45d-139">hello DNS name must be unique across hello Azure service.</span></span> <span data-ttu-id="da45d-140">Considere la posibilidad de configurar Hola VM con un nombre de equipo que describe qué Hola máquina virtual se utiliza para.</span><span class="sxs-lookup"><span data-stu-id="da45d-140">Consider configuring hello VM with a computer name that describes what hello VM is used for.</span></span> <span data-ttu-id="da45d-141">Por ejemplo, ssrsnativecloud.</span><span class="sxs-lookup"><span data-stu-id="da45d-141">For example ssrsnativecloud.</span></span>
   * <span data-ttu-id="da45d-142">**Nivel**: estándar</span><span class="sxs-lookup"><span data-stu-id="da45d-142">**Tier**: Standard</span></span>
   * <span data-ttu-id="da45d-143">**Tamaño: A3** recomienda Hola tamaño de máquina virtual para las cargas de trabajo de SQL Server.</span><span class="sxs-lookup"><span data-stu-id="da45d-143">**Size:A3** is hello recommended VM size for SQL Server workloads.</span></span> <span data-ttu-id="da45d-144">Si una máquina virtual solo se utiliza como un servidor de informes, un tamaño A2 es suficiente a menos que el servidor de informes de hello experimente una carga de trabajo grande.</span><span class="sxs-lookup"><span data-stu-id="da45d-144">If a VM is only used as a report server, a VM size of A2 is sufficient unless hello report server experiences a large workload.</span></span> <span data-ttu-id="da45d-145">Para más información sobre precios de máquinas virtuales, consulte [Precios de Máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="da45d-145">For VM pricing information, see [Virtual Machines Pricing](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>
   * <span data-ttu-id="da45d-146">**Nuevo nombre de usuario**: nombre de Hola que proporcione se crea como un administrador en hello VM.</span><span class="sxs-lookup"><span data-stu-id="da45d-146">**New User Name**: hello name you provide is created as an administrator on hello VM.</span></span>
   * <span data-ttu-id="da45d-147">**Nueva contraseña** y **Confirmar**.</span><span class="sxs-lookup"><span data-stu-id="da45d-147">**New Password** and **confirm**.</span></span> <span data-ttu-id="da45d-148">Esta contraseña se usa para la nueva cuenta de administrador de Hola y se recomienda que utilice una contraseña segura.</span><span class="sxs-lookup"><span data-stu-id="da45d-148">This password is used for hello new administrator account and it is recommended you use a strong password.</span></span>
   * <span data-ttu-id="da45d-149">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="da45d-149">Click **Next**.</span></span> <span data-ttu-id="da45d-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span><span class="sxs-lookup"><span data-stu-id="da45d-150">![next](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)</span></span>
7. <span data-ttu-id="da45d-151">En la página siguiente de hello, edite Hola siguientes campos:</span><span class="sxs-lookup"><span data-stu-id="da45d-151">On hello next page, edit hello following fields:</span></span>
   
   * <span data-ttu-id="da45d-152">**Servicio en la nube**: seleccione **Crear un nuevo servicio en la nube**.</span><span class="sxs-lookup"><span data-stu-id="da45d-152">**Cloud Service**: select **Create a new Cloud Service**.</span></span>
   * <span data-ttu-id="da45d-153">**Nombre DNS del servicio de nube**: se trata de nombre DNS público de Hola de hello servicio de nube que está asociado con hello VM.</span><span class="sxs-lookup"><span data-stu-id="da45d-153">**Cloud Service DNS Name**: This is hello public DNS name of hello Cloud Service that is associated with hello VM.</span></span> <span data-ttu-id="da45d-154">Hola predeterminado es nombre hello que escribió para el nombre de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-154">hello default name is hello name you typed in for hello VM name.</span></span> <span data-ttu-id="da45d-155">Si en pasos posteriores del tema de hello, crear un certificado SSL de confianza y, a continuación, se utiliza el nombre DNS de Hola valor Hola Hola "**emitido para**" del certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-155">If in later steps of hello topic, you create a trusted SSL certificate and then hello DNS name is used for hello value of hello “**Issued to**” of hello certificate.</span></span>
   * <span data-ttu-id="da45d-156">**Afinidad de la región/grupo/red Virtual**: elija Hola región más cercana tooyour a los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="da45d-156">**Region/Affinity Group/Virtual Network**: Choose hello region closest tooyour end users.</span></span>
   * <span data-ttu-id="da45d-157">**Cuenta de almacenamiento**: use una cuenta de almacenamiento generada automáticamente</span><span class="sxs-lookup"><span data-stu-id="da45d-157">**Storage Account**: Use an automatically generated storage account.</span></span>
   * <span data-ttu-id="da45d-158">**Conjunto de disponibilidad**: ninguno.</span><span class="sxs-lookup"><span data-stu-id="da45d-158">**Availability Set**: None.</span></span>
   * <span data-ttu-id="da45d-159">**Los puntos de conexión** mantener hello **escritorio remoto** y **PowerShell** puntos de conexión y, a continuación, agregue el extremo HTTP o HTTPS, dependiendo de su entorno.</span><span class="sxs-lookup"><span data-stu-id="da45d-159">**ENDPOINTS** Keep hello **Remote Desktop** and **PowerShell** endpoints and then add either an HTTP or HTTPS endpoint, depending on your environment.</span></span>
     
     * <span data-ttu-id="da45d-160">**HTTP**: Hola predeterminadas son puertos públicos y privados **80**.</span><span class="sxs-lookup"><span data-stu-id="da45d-160">**HTTP**: hello default public and private ports are **80**.</span></span> <span data-ttu-id="da45d-161">Tenga en cuenta que si utiliza un puerto privado distinto de 80, modifique **$HTTPport = 80** en secuencia de comandos de hello http.</span><span class="sxs-lookup"><span data-stu-id="da45d-161">Note that if you use a private port other than 80, modify **$HTTPport = 80** in hello http script.</span></span>
     * <span data-ttu-id="da45d-162">**HTTPS**: Hola predeterminadas son puertos públicos y privados **443**.</span><span class="sxs-lookup"><span data-stu-id="da45d-162">**HTTPS**: hello default public and private ports are **443**.</span></span> <span data-ttu-id="da45d-163">Una práctica recomendada de seguridad es el puerto privado de toochange hello y configurar su hello y firewall informes servidor toouse Hola privado puerto.</span><span class="sxs-lookup"><span data-stu-id="da45d-163">A security best practice is toochange hello private port and configure your firewall and hello report server toouse hello private port.</span></span> <span data-ttu-id="da45d-164">Para obtener más información sobre los puntos de conexión, vea [cómo tooSet la comunicación con una máquina Virtual](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="da45d-164">For more information on endpoints, see [How tooSet Up Communication with a Virtual Machine](../classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span> <span data-ttu-id="da45d-165">Tenga en cuenta que si utiliza un puerto distinto de 443, cambie el parámetro hello **$HTTPsport = 443** Hola script HTTPS.</span><span class="sxs-lookup"><span data-stu-id="da45d-165">Note that if you use a port other than 443, change hello parameter **$HTTPsport = 443** in hello HTTPS script.</span></span>
   * <span data-ttu-id="da45d-166">Haga clic en Siguiente.</span><span class="sxs-lookup"><span data-stu-id="da45d-166">Click next .</span></span> ![Siguiente](./media/virtual-machines-windows-classic-ps-sql-report/IC692021.gif)
8. <span data-ttu-id="da45d-168">En hello última página del Asistente de hello, mantenga el valor predeterminado de hello **instalar agente de máquina virtual de hello** seleccionado.</span><span class="sxs-lookup"><span data-stu-id="da45d-168">On hello last page of hello wizard, keep hello default **Install hello VM agent** selected.</span></span> <span data-ttu-id="da45d-169">Hello pasos de este tema no utilizar agente de máquina virtual de hello pero si piensa tookeep esta máquina virtual, agente de VM de Hola y las extensiones le permitirá tooenhance visitará CM.</span><span class="sxs-lookup"><span data-stu-id="da45d-169">hello steps in this topic do not utilize hello VM agent but if you plan tookeep this VM, hello VM agent and extensions will allow you tooenhance he CM.</span></span>  <span data-ttu-id="da45d-170">Para obtener más información sobre el agente de máquina virtual de hello, consulte [agente de máquina virtual y extensiones – parte 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span><span class="sxs-lookup"><span data-stu-id="da45d-170">For more information on hello VM agent, see [VM Agent and Extensions – Part 1](https://azure.microsoft.com/blog/2014/04/11/vm-agent-and-extensions-part-1/).</span></span> <span data-ttu-id="da45d-171">Uno de anuncio de Hola predeterminado extensiones instaladas ejecutando es extensión "BGINFO" de Hola que se muestra en el escritorio de la máquina virtual de hello, espacio de la unidad de información del sistema, como la dirección IP interna y free.</span><span class="sxs-lookup"><span data-stu-id="da45d-171">One of hello default extensions installed ad running is hello “BGINFO” extension that displays on hello VM desktop, system information such as internal IP and free drive space.</span></span>
9. <span data-ttu-id="da45d-172">Haga clic en Completo.</span><span class="sxs-lookup"><span data-stu-id="da45d-172">Click complete .</span></span> ![Aceptar](./media/virtual-machines-windows-classic-ps-sql-report/IC660122.gif)
10. <span data-ttu-id="da45d-174">Hola **estado** de hello VM se muestra como **iniciando (aprovisionamiento)** durante el proceso de aprovisionamiento de hello y, a continuación, se muestra como **ejecuta** cuando Hola máquina virtual se ha aprovisionado y listo toouse.</span><span class="sxs-lookup"><span data-stu-id="da45d-174">hello **Status** of hello VM displays as **Starting (Provisioning)** during hello provision process and then displays as **Running** when hello VM is provisioned and ready toouse.</span></span>

## <a name="step-2-create-a-server-certificate"></a><span data-ttu-id="da45d-175">Paso 2: Crear un certificado de servidor</span><span class="sxs-lookup"><span data-stu-id="da45d-175">Step 2: Create a Server Certificate</span></span>
> [!NOTE]
> <span data-ttu-id="da45d-176">Si no se requiere HTTPS en el servidor de informes de hello, puede **omita el paso 2** y vaya sección toohello **usar HTTP y el servidor de informes de script tooconfigure hello**.</span><span class="sxs-lookup"><span data-stu-id="da45d-176">If you do not require HTTPS on hello report server, you can **skip step 2** and go toohello section **Use script tooconfigure hello report server and HTTP**.</span></span> <span data-ttu-id="da45d-177">Use Hola HTTP script tooquickly configurar servidor de informes de Hola y el informe de hello servidor será toouse listo.</span><span class="sxs-lookup"><span data-stu-id="da45d-177">Use hello HTTP script tooquickly configure hello report server and hello report server will be ready toouse.</span></span>

<span data-ttu-id="da45d-178">En orden toouse HTTPS en hello VM, necesita un certificado SSL de confianza.</span><span class="sxs-lookup"><span data-stu-id="da45d-178">In order toouse HTTPS on hello VM, you need a trusted SSL certificate.</span></span> <span data-ttu-id="da45d-179">Según el escenario, puede usar uno de hello siguiendo dos métodos:</span><span class="sxs-lookup"><span data-stu-id="da45d-179">Depending on your scenario, you can use one of hello following two methods:</span></span>

* <span data-ttu-id="da45d-180">Un certificado SSL válido emitido por una entidad de certificación (CA) y de confianza de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="da45d-180">A valid SSL certificate issued by a Certification Authority (CA) and trusted by Microsoft.</span></span> <span data-ttu-id="da45d-181">los certificados de CA raíz de Hello son necesario toobe distribuida a través de hello programa de certificados raíz de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="da45d-181">hello CA root certificates are required toobe distributed via hello Microsoft Root Certificate Program.</span></span> <span data-ttu-id="da45d-182">Para obtener más información acerca de este programa, consulte [Windows y el programa de certificados de Windows Phone 8 SSL raíz (miembro de CA)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) y [Introducción toohello programa de certificados raíz de Microsoft](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span><span class="sxs-lookup"><span data-stu-id="da45d-182">For more information about this program, see [Windows and Windows Phone 8 SSL Root Certificate Program (Member CAs)](http://social.technet.microsoft.com/wiki/contents/articles/14215.windows-and-windows-phone-8-ssl-root-certificate-program-member-cas.aspx) and [Introduction toohello Microsoft Root Certificate Program](http://social.technet.microsoft.com/wiki/contents/articles/3281.introduction-to-the-microsoft-root-certificate-program.aspx).</span></span>
* <span data-ttu-id="da45d-183">Un certificado autofirmado.</span><span class="sxs-lookup"><span data-stu-id="da45d-183">A self-signed certificate.</span></span> <span data-ttu-id="da45d-184">No se recomiendan los certificados autofirmados para entornos de producción.</span><span class="sxs-lookup"><span data-stu-id="da45d-184">Self-signed certificates are not recommended for production environments.</span></span>

### <a name="toouse-a-certificate-created-by-a-trusted-certificate-authority-ca"></a><span data-ttu-id="da45d-185">toouse un certificado creado por una entidad de confianza de certificados (CA)</span><span class="sxs-lookup"><span data-stu-id="da45d-185">toouse a certificate created by a trusted Certificate Authority (CA)</span></span>
1. <span data-ttu-id="da45d-186">**Solicitar un certificado de servidor para el sitio Web de Hola de una entidad de certificación**.</span><span class="sxs-lookup"><span data-stu-id="da45d-186">**Request a server certificate for hello website from a certification authority**.</span></span> 
   
    <span data-ttu-id="da45d-187">Hola Asistente para certificados de servidor Web puede usar cualquier toogenerate un archivo de solicitud de certificado (Certreq.txt) que envía tooa entidad emisora de certificados, o toogenerate una solicitud para una entidad de certificación en línea.</span><span class="sxs-lookup"><span data-stu-id="da45d-187">You can use hello Web Server Certificate Wizard either toogenerate a certificate request file (Certreq.txt) that you send tooa certification authority, or toogenerate a request for an online certification authority.</span></span> <span data-ttu-id="da45d-188">Por ejemplo, los Servicios de certificados de Microsoft en Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="da45d-188">For example, Microsoft Certificate Services in Windows Server 2012.</span></span> <span data-ttu-id="da45d-189">Según el nivel de Hola de garantía de identificación proporcionado por el certificado de servidor, es la solicitud de varios días, meses tooseveral para tooapprove de entidad de certificación de Hola y envíe un archivo de certificado.</span><span class="sxs-lookup"><span data-stu-id="da45d-189">Depending on hello level of identification assurance offered by your server certificate, it is several days tooseveral months for hello certification authority tooapprove your request and send you a certificate file.</span></span> 
   
    <span data-ttu-id="da45d-190">Para obtener más información sobre las solicitudes de certificados de servidor, vea Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="da45d-190">For more information about requesting a server certificates, see hello following:</span></span> 
   
   * <span data-ttu-id="da45d-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span><span class="sxs-lookup"><span data-stu-id="da45d-191">Use [Certreq](https://technet.microsoft.com/library/cc725793.aspx), [Certreq](https://technet.microsoft.com/library/cc725793.aspx).</span></span>
   * <span data-ttu-id="da45d-192">TooAdminister de herramientas de seguridad Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="da45d-192">Security Tools tooAdminister Windows Server 2012.</span></span>
     
     [<span data-ttu-id="da45d-193">Herramientas de seguridad tooAdminister Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="da45d-193">Security Tools tooAdminister Windows Server 2012</span></span>](https://technet.microsoft.com/library/jj730960.aspx)
     
     > [!NOTE]
     > <span data-ttu-id="da45d-194">Hola **emitido para** campo de hello confianza certificado SSL debe ser Hola igual como hello **nombre de DNS del servicio de nube** que usó para Hola nueva máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="da45d-194">hello **issued to** field of hello trusted SSL certificate should be hello same as hello **Cloud Service DNS NAME** you used for hello new VM.</span></span>

2. <span data-ttu-id="da45d-195">**Instalar certificado de servidor de hello en el servidor Web de hello**.</span><span class="sxs-lookup"><span data-stu-id="da45d-195">**Install hello server certificate on hello Web server**.</span></span> <span data-ttu-id="da45d-196">servidor Web de Hello en este caso es hello VM que Hola de hosts de servidor de informes y se crea el sitio Web de Hola en pasos posteriores cuando se configura Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="da45d-196">hello Web server in this case is hello VM that hosts hello report server and hello website is created in later steps when you configure Reporting Services.</span></span> <span data-ttu-id="da45d-197">Para obtener más información acerca de cómo instalar certificado de servidor hello en el servidor Web de hello utilizando el complemento MMC de certificados de hello, consulte [instalar un certificado de servidor](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="da45d-197">For more information about installing hello server certificate on hello Web server by using hello Certificate MMC snap-in, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
    <span data-ttu-id="da45d-198">Si desea que el script de Hola toouse incluido con este tema, el servidor de informes de tooconfigure hello, Hola valor de certificados de hello **huella digital** es necesario que un parámetro de script de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-198">If you want toouse hello script included with this topic, tooconfigure hello report server, hello value of hello certificates **Thumbprint** is required as a parameter of hello script.</span></span> <span data-ttu-id="da45d-199">Vea Hola próxima sección para obtener más información sobre cómo tooobtain Hola huella digital del certificado de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-199">See hello next section for details on how tooobtain hello thumbprint of hello certificate.</span></span>
3. <span data-ttu-id="da45d-200">Asignar al servidor de informes de hello server certificado toohello.</span><span class="sxs-lookup"><span data-stu-id="da45d-200">Assign hello server certificate toohello report server.</span></span> <span data-ttu-id="da45d-201">asignación de Hola se completa en la sección siguiente de hello cuando se configura el servidor de informes de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-201">hello assignment is completed in hello next section when you configure hello report server.</span></span>

### <a name="toouse-hello-virtual-machines-self-signed-certificate"></a><span data-ttu-id="da45d-202">Hola toouse certificado autofirmado de máquinas virtuales</span><span class="sxs-lookup"><span data-stu-id="da45d-202">toouse hello Virtual Machines Self-signed Certificate</span></span>
<span data-ttu-id="da45d-203">Un certificado autofirmado se creó en hello VM cuando Hola VM se haya proporcionado.</span><span class="sxs-lookup"><span data-stu-id="da45d-203">A self-signed certificate was created on hello VM when hello VM was provisioned.</span></span> <span data-ttu-id="da45d-204">certificado de Hello tiene Hola mismo nombre como nombre DNS de VM de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-204">hello certificate has hello same name as hello VM DNS name.</span></span> <span data-ttu-id="da45d-205">En errores de certificado de orden tooavoid, es necesario dicho certificado hello es de confianza en hello propia máquina virtual y también para todos los usuarios del sitio de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-205">In order tooavoid certificate errors, it is required that hello certificate is trusted on hello VM itself, and also by all users of hello site.</span></span>

1. <span data-ttu-id="da45d-206">tootrust Hola CA raíz del certificado de hello en hello VM Local, agregue Hola certificado toohello **entidades de certificación raíz de confianza**.</span><span class="sxs-lookup"><span data-stu-id="da45d-206">tootrust hello root CA of hello certificate on hello Local VM, add hello certificate toohello **Trusted Root Certification Authorities**.</span></span> <span data-ttu-id="da45d-207">Hola aquí te mostramos un resumen de pasos de hello necesarios.</span><span class="sxs-lookup"><span data-stu-id="da45d-207">hello following is a summary of hello steps required.</span></span> <span data-ttu-id="da45d-208">Para obtener instrucciones detalladas sobre cómo tootrust Hola entidad emisora de certificados, consulte [instalar un certificado de servidor](https://technet.microsoft.com/library/cc740068).</span><span class="sxs-lookup"><span data-stu-id="da45d-208">For detailed steps on how tootrust hello CA, see [Install a Server Certificate](https://technet.microsoft.com/library/cc740068).</span></span>
   
   1. <span data-ttu-id="da45d-209">En hello portal de Azure clásico, seleccione Hola máquina virtual y haga clic en conectar.</span><span class="sxs-lookup"><span data-stu-id="da45d-209">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="da45d-210">Según la configuración del explorador, es posible que toosave solicitada un archivo .rdp para la conexión toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="da45d-210">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
      
       ![conectar máquina virtual de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="da45d-212">Usar el nombre de VM de hello usuario, nombre de usuario y contraseña que configuró cuando creaste Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="da45d-212">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
      
       <span data-ttu-id="da45d-213">Por ejemplo, en Hola después de la imagen, nombre de la máquina virtual de hello es **ssrsnativecloud** y es el nombre de usuario de hello **testuser**.</span><span class="sxs-lookup"><span data-stu-id="da45d-213">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
      
       ![el inicio de sesión incluye la máquina virtual](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
   2. <span data-ttu-id="da45d-215">Ejecute mmc.exe.</span><span class="sxs-lookup"><span data-stu-id="da45d-215">Run mmc.exe.</span></span> <span data-ttu-id="da45d-216">Para obtener más información, consulte [Cómo: ver certificados con hello complemento MMC](https://msdn.microsoft.com/library/ms788967.aspx).</span><span class="sxs-lookup"><span data-stu-id="da45d-216">For more information, see [How to: View Certificates with hello MMC Snap-in](https://msdn.microsoft.com/library/ms788967.aspx).</span></span>
   3. <span data-ttu-id="da45d-217">En la aplicación de consola de hello **archivo** menú, agregar hello **certificados** complemento, seleccione **cuenta de equipo** cuando se le pida y, a continuación, haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="da45d-217">In hello console application **File** menu, add hello **Certificates** snap-in, select **Computer Account** when prompted, and then click **Next**.</span></span>
   4. <span data-ttu-id="da45d-218">Seleccione **equipo Local** toomanage y, a continuación, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="da45d-218">Select **Local Computer** toomanage and then click **Finish**.</span></span>
   5. <span data-ttu-id="da45d-219">Haga clic en **Aceptar** y, a continuación, expanda hello **certificados - Personal** nodos y, a continuación, haga clic en **certificados**.</span><span class="sxs-lookup"><span data-stu-id="da45d-219">Click **Ok** and then expand hello **Certificates -Personal** nodes and then click **Certificates**.</span></span> <span data-ttu-id="da45d-220">se denomina nombre de DNS de Hola de hello VM Hello certificado y termina con **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="da45d-220">hello certificate is named after hello DNS name of hello VM and ends with **cloudapp.net**.</span></span> <span data-ttu-id="da45d-221">Haga clic en el nombre del certificado de Hola y haga clic en **copia**.</span><span class="sxs-lookup"><span data-stu-id="da45d-221">Right-click hello certificate name and click **Copy**.</span></span>
   6. <span data-ttu-id="da45d-222">Expanda hello **entidades de certificación raíz de confianza** nodo y, a continuación, haga **certificados** y, a continuación, haga clic en **pegar**.</span><span class="sxs-lookup"><span data-stu-id="da45d-222">Expand hello **Trusted Root Certification Authorities** node and then right-click **Certificates** and then click **Paste**.</span></span>
   7. <span data-ttu-id="da45d-223">toovalidate, doble haga clic en el nombre del certificado Hola bajo **entidades de certificación raíz de confianza** y compruebe que no hay ningún error y puede ver el certificado.</span><span class="sxs-lookup"><span data-stu-id="da45d-223">toovalidate, double click on hello certificate name under **Trusted Root Certification Authorities** and verify that there are no errors and you see your certificate.</span></span> <span data-ttu-id="da45d-224">Si desea que toouse Hola HTTPS script incluido con este tema, el servidor de informes de tooconfigure hello, Hola valor de certificados de hello **huella digital** es necesario que un parámetro de script de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-224">If you want toouse hello HTTPS script included with this topic, tooconfigure hello report server, hello value of hello certificates **Thumbprint** is required as a parameter of hello script.</span></span> <span data-ttu-id="da45d-225">**valor de huella digital de hello tooget**, complete Hola siguiente.</span><span class="sxs-lookup"><span data-stu-id="da45d-225">**tooget hello thumbprint value**, complete hello following.</span></span> <span data-ttu-id="da45d-226">También hay una huella digital de PowerShell ejemplo tooretrieve hello en sección [usar HTTPS y servidor de informes de script tooconfigure Hola](#use-script-to-configure-the-report-server-and-HTTPS).</span><span class="sxs-lookup"><span data-stu-id="da45d-226">There is also a PowerShell sample tooretrieve hello thumbprint in section [Use script tooconfigure hello report server and HTTPS](#use-script-to-configure-the-report-server-and-HTTPS).</span></span>
      
      1. <span data-ttu-id="da45d-227">Haga doble clic en el nombre de Hola Hola del certificado de, por ejemplo ssrsnativecloud.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="da45d-227">Double-click hello name of hello certificate, for example ssrsnativecloud.cloudapp.net.</span></span>
      2. <span data-ttu-id="da45d-228">Haga clic en hello **detalles** ficha.</span><span class="sxs-lookup"><span data-stu-id="da45d-228">Click hello **Details** tab.</span></span>
      3. <span data-ttu-id="da45d-229">Haga clic en **Huella digital**.</span><span class="sxs-lookup"><span data-stu-id="da45d-229">Click **Thumbprint**.</span></span> <span data-ttu-id="da45d-230">valor de Hola de huella digital de Hola se muestra en el campo de detalles de hello, por ejemplo a6 08 3C df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9C 2c fb 2f.</span><span class="sxs-lookup"><span data-stu-id="da45d-230">hello value of hello thumbprint is displayed in hello details field, for example ‎a6 08 3c df f9 0b f7 e3 7c 25 ed a4 ed 7e ac 91 9c 2c fb 2f.</span></span>
      4. <span data-ttu-id="da45d-231">Copie la huella digital de Hola y guardar el valor de Hola para más tarde o editar script de Hola ahora.</span><span class="sxs-lookup"><span data-stu-id="da45d-231">Copy hello thumbprint and save hello value for later or edit hello script now.</span></span>
      5. <span data-ttu-id="da45d-232">(*) Antes de ejecutar script de Hola, quite los espacios de hello entre pares de Hola de valores.</span><span class="sxs-lookup"><span data-stu-id="da45d-232">(*) Before you run hello script, remove hello spaces in between hello pairs of values.</span></span> <span data-ttu-id="da45d-233">Por ejemplo la huella digital de Hola que se indicó antes ahora sería a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span><span class="sxs-lookup"><span data-stu-id="da45d-233">For example hello thumbprint noted before would now be ‎a6083cdff90bf7e37c25eda4ed7eac919c2cfb2f.</span></span>
      6. <span data-ttu-id="da45d-234">Asignar al servidor de informes de hello server certificado toohello.</span><span class="sxs-lookup"><span data-stu-id="da45d-234">Assign hello server certificate toohello report server.</span></span> <span data-ttu-id="da45d-235">asignación de Hola se completa en la sección siguiente de hello cuando se configura el servidor de informes de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-235">hello assignment is completed in hello next section when you configure hello report server.</span></span>

<span data-ttu-id="da45d-236">Si usas un certificado SSL autofirmado, nombre de hello en el certificado de Hola ya coincide con hostname Hola de hello VM.</span><span class="sxs-lookup"><span data-stu-id="da45d-236">If you are using a self-signed SSL certificate, hello name on hello certificate already matches hello hostname of hello VM.</span></span> <span data-ttu-id="da45d-237">Por lo tanto, Hola DNS de la máquina de hello ya está registrado globalmente y puede tener acceso desde cualquier cliente.</span><span class="sxs-lookup"><span data-stu-id="da45d-237">Therefore, hello DNS of hello machine is already registered globally and can be accessed from any client.</span></span>

## <a name="step-3-configure-hello-report-server"></a><span data-ttu-id="da45d-238">Paso 3: Configurar el servidor de informes de Hola</span><span class="sxs-lookup"><span data-stu-id="da45d-238">Step 3: Configure hello Report Server</span></span>
<span data-ttu-id="da45d-239">En esta sección se explica cómo configurar Hola VM como un servidor de informes de modo nativo de Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="da45d-239">This section walks you through configuring hello VM as a Reporting Services native mode report server.</span></span> <span data-ttu-id="da45d-240">Puede usar uno de hello después el servidor de informes de métodos tooconfigure hello:</span><span class="sxs-lookup"><span data-stu-id="da45d-240">You can use one of hello following methods tooconfigure hello report server:</span></span>

* <span data-ttu-id="da45d-241">Servidor de informes de uso Hola script tooconfigure Hola</span><span class="sxs-lookup"><span data-stu-id="da45d-241">Use hello script tooconfigure hello report server</span></span>
* <span data-ttu-id="da45d-242">Hola tooConfigure use el Administrador de configuración del servidor de informes.</span><span class="sxs-lookup"><span data-stu-id="da45d-242">Use Configuration Manager tooConfigure hello Report Server.</span></span>

<span data-ttu-id="da45d-243">Para obtener pasos más detallada, vea la sección de hello [toohello conectar Máquina Virtual e inicie Hola Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span><span class="sxs-lookup"><span data-stu-id="da45d-243">For more detailed steps, see hello section [Connect toohello Virtual Machine and Start hello Reporting Services Configuration Manager](virtual-machines-windows-classic-ps-sql-bi.md#connect-to-the-virtual-machine-and-start-the-reporting-services-configuration-manager).</span></span>

<span data-ttu-id="da45d-244">**Nota sobre la autenticación:** Hola método de autenticación recomendado no es autenticación de Windows y autenticación de Reporting Services de hello predeterminada.</span><span class="sxs-lookup"><span data-stu-id="da45d-244">**Authentication Note:** Windows authentication is hello recommended authentication method and it is hello default Reporting Services authentication.</span></span> <span data-ttu-id="da45d-245">Solo los usuarios que se configuran en hello VM pueden tener acceso a Reporting Services y asignan tooReporting roles de servicios.</span><span class="sxs-lookup"><span data-stu-id="da45d-245">Only users that are configured on hello VM can access Reporting Services and assigned tooReporting Services roles.</span></span>

### <a name="use-script-tooconfigure-hello-report-server-and-http"></a><span data-ttu-id="da45d-246">Servidor de informes de uso script tooconfigure hello y HTTP</span><span class="sxs-lookup"><span data-stu-id="da45d-246">Use script tooconfigure hello report server and HTTP</span></span>
<span data-ttu-id="da45d-247">toouse Hola Windows PowerShell script tooconfigure Hola servidor de informes, Hola completa pasos.</span><span class="sxs-lookup"><span data-stu-id="da45d-247">toouse hello Windows PowerShell script tooconfigure hello report server, complete hello following steps.</span></span> <span data-ttu-id="da45d-248">configuración de Hello incluye HTTP y HTTPS no:</span><span class="sxs-lookup"><span data-stu-id="da45d-248">hello configuration includes HTTP, not HTTPS:</span></span>

1. <span data-ttu-id="da45d-249">En hello portal de Azure clásico, seleccione Hola máquina virtual y haga clic en conectar.</span><span class="sxs-lookup"><span data-stu-id="da45d-249">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="da45d-250">Según la configuración del explorador, es posible que toosave solicitada un archivo .rdp para la conexión toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="da45d-250">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
   
    ![conectar máquina virtual de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="da45d-252">Usar el nombre de VM de hello usuario, nombre de usuario y contraseña que configuró cuando creaste Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="da45d-252">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
   
    <span data-ttu-id="da45d-253">Por ejemplo, en Hola después de la imagen, nombre de la máquina virtual de hello es **ssrsnativecloud** y es el nombre de usuario de hello **testuser**.</span><span class="sxs-lookup"><span data-stu-id="da45d-253">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
   
    ![el inicio de sesión incluye la máquina virtual](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="da45d-255">En hello VM, abra **Windows PowerShell ISE** con privilegios administrativos.</span><span class="sxs-lookup"><span data-stu-id="da45d-255">On hello VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="da45d-256">Hola PowerShell ISE se instala de forma predeterminada en Windows server 2012.</span><span class="sxs-lookup"><span data-stu-id="da45d-256">hello PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="da45d-257">Se recomienda que usar hello ISE en lugar de una ventana estándar de Windows PowerShell, por lo que puede pegar el script de Hola en hello ISE, modificar el script de Hola y, a continuación, ejecute el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-257">It is recommended you use hello ISE instead of a standard Windows PowerShell window so that you can paste hello script into hello ISE, modify hello script, and then run hello script.</span></span>
3. <span data-ttu-id="da45d-258">En Windows PowerShell ISE, haga clic en hello **vista** menú y, a continuación, haga clic en **Mostrar panel de scripts**.</span><span class="sxs-lookup"><span data-stu-id="da45d-258">In Windows PowerShell ISE, click hello **View** menu and then click **Show Script Pane**.</span></span>
4. <span data-ttu-id="da45d-259">Hola siguiente secuencia de comandos de copiar y pegar el script de Hola en panel de scripts de Windows PowerShell ISE Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-259">Copy hello following script, and paste hello script into hello Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures a Native mode report server without HTTPS
        $ErrorActionPreference = "Stop"
   
        $server = $env:COMPUTERNAME
        $HTTPport = 80 # change hello value if you used a different port for hello private HTTP endpoint when hello VM was created.
   
        ## Set PowerShell execution policy toobe able toorun scripts
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
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Report Server Configuration Steps
   
        ## Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
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
   
        ## Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS              ## this automatically changes toosqlserver provider
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
   
        ## Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
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
5. <span data-ttu-id="da45d-260">Si ha creado Hola VM con un puerto HTTP distinto de 80, modifique el parámetro de hello $HTTPport = 80.</span><span class="sxs-lookup"><span data-stu-id="da45d-260">If you created hello VM with an HTTP port other than 80, modify hello parameter $HTTPport = 80.</span></span>
6. <span data-ttu-id="da45d-261">script de Hola está configurado actualmente para Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="da45d-261">hello script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="da45d-262">Si desea que toorun Hola script para Reporting Services, modificar parte de la versión de Hola del espacio de nombres de toohello de ruta de acceso de hello demasiado "v11", en la instrucción de hello Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="da45d-262">If you want toorun hello script for  Reporting Services, modify hello version portion of hello path toohello namespace too“v11”, on hello Get-WmiObject statement.</span></span>
7. <span data-ttu-id="da45d-263">Ejecutar script de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-263">Run hello script.</span></span>

<span data-ttu-id="da45d-264">**Validación**: tooverify que Hola funcionalidad del servidor de informes básica funciona, vea hello [Compruebe la configuración de hello](#verify-the-configuration) sección más adelante en este tema.</span><span class="sxs-lookup"><span data-stu-id="da45d-264">**Validation**: tooverify that hello basic report server functionality is working, see hello [Verify hello configuration](#verify-the-configuration) section later in this topic.</span></span>

### <a name="use-script-tooconfigure-hello-report-server-and-https"></a><span data-ttu-id="da45d-265">Servidor de informes de uso script tooconfigure hello y HTTPS</span><span class="sxs-lookup"><span data-stu-id="da45d-265">Use script tooconfigure hello report server and HTTPS</span></span>
<span data-ttu-id="da45d-266">toouse Windows PowerShell tooconfigure Hola servidor de informes, Hola completa pasos.</span><span class="sxs-lookup"><span data-stu-id="da45d-266">toouse Windows PowerShell tooconfigure hello report server, complete hello following steps.</span></span> <span data-ttu-id="da45d-267">configuración de Hello incluye HTTPS y no HTTP.</span><span class="sxs-lookup"><span data-stu-id="da45d-267">hello configuration includes HTTPS, not HTTP.</span></span>

1. <span data-ttu-id="da45d-268">En hello portal de Azure clásico, seleccione Hola máquina virtual y haga clic en conectar.</span><span class="sxs-lookup"><span data-stu-id="da45d-268">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="da45d-269">Según la configuración del explorador, es posible que toosave solicitada un archivo .rdp para la conexión toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="da45d-269">Depending on your browser configuration, you may be prompted toosave an .rdp file for connecting toohello VM.</span></span>
   
    ![conectar máquina virtual de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif) <span data-ttu-id="da45d-271">Usar el nombre de VM de hello usuario, nombre de usuario y contraseña que configuró cuando creaste Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="da45d-271">Use hello user VM name, user name and password you configured when you created hello VM.</span></span> 
   
    <span data-ttu-id="da45d-272">Por ejemplo, en Hola después de la imagen, nombre de la máquina virtual de hello es **ssrsnativecloud** y es el nombre de usuario de hello **testuser**.</span><span class="sxs-lookup"><span data-stu-id="da45d-272">For example, in hello following image, hello VM name is **ssrsnativecloud** and hello user name is **testuser**.</span></span>
   
    ![el inicio de sesión incluye la máquina virtual](./media/virtual-machines-windows-classic-ps-sql-report/IC764111.png)
2. <span data-ttu-id="da45d-274">En hello VM, abra **Windows PowerShell ISE** con privilegios administrativos.</span><span class="sxs-lookup"><span data-stu-id="da45d-274">On hello VM, open **Windows PowerShell ISE** with administrative privileges.</span></span> <span data-ttu-id="da45d-275">Hola PowerShell ISE se instala de forma predeterminada en Windows server 2012.</span><span class="sxs-lookup"><span data-stu-id="da45d-275">hello PowerShell ISE is installed by default on Windows server 2012.</span></span> <span data-ttu-id="da45d-276">Se recomienda que usar hello ISE en lugar de una ventana estándar de Windows PowerShell, por lo que puede pegar el script de Hola en hello ISE, modificar el script de Hola y, a continuación, ejecute el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-276">It is recommended you use hello ISE instead of a standard Windows PowerShell window so that you can paste hello script into hello ISE, modify hello script, and then run hello script.</span></span>
3. <span data-ttu-id="da45d-277">tooenable ejecutar secuencias de comandos, ejecute hello siguiente comando de Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="da45d-277">tooenable running scripts, run hello following Windows PowerShell command:</span></span>
   
        Set-ExecutionPolicy RemoteSigned
   
    <span data-ttu-id="da45d-278">A continuación, puede ejecutar Hola después de la directiva de Hola tooverify:</span><span class="sxs-lookup"><span data-stu-id="da45d-278">You can then run hello following tooverify hello policy:</span></span>
   
        Get-ExecutionPolicy
4. <span data-ttu-id="da45d-279">En **Windows PowerShell ISE**, haga clic en hello **vista** menú y, a continuación, haga clic en **Mostrar panel de scripts**.</span><span class="sxs-lookup"><span data-stu-id="da45d-279">In **Windows PowerShell ISE**, click hello **View** menu and then click **Show Script Pane**.</span></span>
5. <span data-ttu-id="da45d-280">Copie Hola siguiente script y péguelo en el panel de scripts de Windows PowerShell ISE Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-280">Copy hello following script and paste it into hello Windows PowerShell ISE script pane.</span></span>
   
        ## This script configures hello report server, including HTTPS
        $ErrorActionPreference = "Stop"
        $httpsport=443 # modify if you used a different port number when hello HTTPS endpoint was created.
   
        # You can run hello following command tooget (.cloudapp.net certificates) so you can copy hello thumbprint / certificate hash
        #dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
        #
        # hello certifacte hash is a REQUIRED parameter
        $certificatehash="" 
        # hello certificate hash should not contain spaces
   
        if ($certificatehash.Length -lt 1) 
        {
            write-error "certificatehash is a required parameter"
        } 
        # Certificates should be all lower case
        $certificatehash=$certificatehash.ToLower()
        $server = $env:COMPUTERNAME
        # If hello certificate is not a wildcard certificate, comment out hello following line, and enable hello full $DNSNAme reference.
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
   
        write-host "hello script will use $DNSNameAndPort as hello DNS name and port" 
   
        ## Register for MSReportServer_ConfigurationSetting
        ## Change hello version portion of hello path too"v11" toouse hello script for SQL Server 2012
        $RSObject = Get-WmiObject -class "MSReportServer_ConfigurationSetting" -namespace "root\Microsoft\SqlServer\ReportServer\RS_MSSQLSERVER\v12\Admin"
   
        ## Reporting Services Report Server Configuration Steps
   
        ## 1. Setting hello web service URL ##
        write-host -foregroundcolor green "Setting hello web service URL"
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
   
        ## 2. Setting hello Database ##
        write-host -foregroundcolor green "Setting hello Database"
        write-host -foregroundcolor green ">>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>"
        $time=Get-Date
        write-host -foregroundcolor DarkGray $time
   
        ## GenerateDatabaseScript - for creating hello database
            write-host "Calling GenerateDatabaseCreationScript for database $dbName"
            $r = $RSObject.GenerateDatabaseCreationScript($dbName,1033,$false)
            CheckResult $r "GenerateDatabaseCreationScript"
            $script = $r.Script
   
        ## Execute sql script toocreate hello database
            write-host 'Executing Database Creation Script'
            $savedcvd = Get-Location
            Import-Module SQLPS                    ## this automatically changes toosqlserver provider
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
   
        ## 3. Setting hello Report Manager URL ##
   
        write-host -foregroundcolor green "Setting hello Report Manager URL"
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
6. <span data-ttu-id="da45d-281">Modificar hello **$certificatehash** parámetro hello script:</span><span class="sxs-lookup"><span data-stu-id="da45d-281">Modify hello **$certificatehash** parameter in hello script:</span></span>
   
   * <span data-ttu-id="da45d-282">Se trata de un parámetro **obligatorio** .</span><span class="sxs-lookup"><span data-stu-id="da45d-282">This is a **required** parameter.</span></span> <span data-ttu-id="da45d-283">Si no ha guardado el valor de certificado de Hola de los pasos anteriores de hello, use uno de hello siguiendo el valor de hash del certificado de métodos toocopy Hola de huella digital de certificados de Hola.:</span><span class="sxs-lookup"><span data-stu-id="da45d-283">If you did not save hello certificate value from hello previous steps, use one of hello following methods toocopy hello certificate hash value from hello certificates thumbprint.:</span></span>
     
       <span data-ttu-id="da45d-284">En hello VM, abra Windows PowerShell ISE y ejecute hello siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="da45d-284">On hello VM, open Windows PowerShell ISE and run hello following command:</span></span>
     
           dir cert:\LocalMachine -rec | Select-Object * | where {$_.issuer -like "*cloudapp*" -and $_.pspath -like "*root*"} | select dnsnamelist, thumbprint, issuer
     
       <span data-ttu-id="da45d-285">salida de Hello tendrá un aspecto similar a continuación toohello.</span><span class="sxs-lookup"><span data-stu-id="da45d-285">hello output will look similar toohello following.</span></span> <span data-ttu-id="da45d-286">Si el script de Hola devuelve una línea en blanco, Hola VM no tiene un certificado configurado por ejemplo, vea la sección de hello [toouse Hola certificado autofirmado de máquinas virtuales](#to-use-the-virtual-machines-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="da45d-286">If hello script returns a blank line, hello VM does not have a certificate configured for example, see hello section [toouse hello Virtual Machines Self-signed Certificate](#to-use-the-virtual-machines-self-signed-certificate).</span></span>
     
     <span data-ttu-id="da45d-287">OR</span><span class="sxs-lookup"><span data-stu-id="da45d-287">OR</span></span>
   * <span data-ttu-id="da45d-288">Hola máquina virtual, ejecute mmc.exe y, a continuación, agregar Hola **certificados** complemento.</span><span class="sxs-lookup"><span data-stu-id="da45d-288">On hello VM Run mmc.exe and then add hello **Certificates** snap-in.</span></span>
   * <span data-ttu-id="da45d-289">En hello **entidades emisoras de certificados raíz de confianza** haga doble clic en el nombre del certificado.</span><span class="sxs-lookup"><span data-stu-id="da45d-289">Under hello **Trusted Root Certificate Authorities** node double-click your certificate name.</span></span> <span data-ttu-id="da45d-290">Si utilizas un certificado autofirmado de Hola de hello VM, el certificado de Hola se denomina nombre de DNS de Hola de hello VM y termina con **cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="da45d-290">If you are using hello self-signed certificate of hello VM, hello certificate is named after hello DNS name of hello VM and ends with **cloudapp.net**.</span></span>
   * <span data-ttu-id="da45d-291">Haga clic en hello **detalles** ficha.</span><span class="sxs-lookup"><span data-stu-id="da45d-291">Click hello **Details** tab.</span></span>
   * <span data-ttu-id="da45d-292">Haga clic en **Huella digital**.</span><span class="sxs-lookup"><span data-stu-id="da45d-292">Click **Thumbprint**.</span></span> <span data-ttu-id="da45d-293">valor de Hola de huella digital de Hola se muestra en el campo de detalles de hello, por ejemplo af 11 60 b6 4b 28 8 d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span><span class="sxs-lookup"><span data-stu-id="da45d-293">hello value of hello thumbprint is displayed in hello details field, for example af 11 60 b6 4b 28 8d 89 0a 82 12 ff 6b a9 c3 66 4f 31 90 48</span></span>
   * <span data-ttu-id="da45d-294">**Antes de ejecutar script de Hola**, quitar Hola espacios entre los pares de Hola de valores.</span><span class="sxs-lookup"><span data-stu-id="da45d-294">**Before you run hello script**, remove hello spaces in between hello pairs of values.</span></span> <span data-ttu-id="da45d-295">Por ejemplo, af1160b64b288d890a8212ff6ba9c3664f319048.</span><span class="sxs-lookup"><span data-stu-id="da45d-295">For example af1160b64b288d890a8212ff6ba9c3664f319048</span></span>
7. <span data-ttu-id="da45d-296">Modificar hello **$httpsport** parámetro:</span><span class="sxs-lookup"><span data-stu-id="da45d-296">Modify hello **$httpsport** parameter:</span></span> 
   
   * <span data-ttu-id="da45d-297">Si utiliza el puerto 443 para el punto de conexión de hello HTTPS, no deberá tooupdate este parámetro en el script de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-297">If you used port 443 for hello HTTPS endpoint, then you do not need tooupdate this parameter in hello script.</span></span> <span data-ttu-id="da45d-298">En caso contrario, use valor del puerto Hola seleccionado al configurar extremo privado HTTPS de hello en hello VM.</span><span class="sxs-lookup"><span data-stu-id="da45d-298">Otherwise use hello port value you selected when you configured hello HTTPS private endpoint on hello VM.</span></span>
8. <span data-ttu-id="da45d-299">Modificar hello **$DNSName** parámetro:</span><span class="sxs-lookup"><span data-stu-id="da45d-299">Modify hello **$DNSName** parameter:</span></span> 
   
   * <span data-ttu-id="da45d-300">script de Hola está configurado para un certificado comodín $DNSName = "+".</span><span class="sxs-lookup"><span data-stu-id="da45d-300">hello script is configured for a wild card certificate $DNSName="+".</span></span> <span data-ttu-id="da45d-301">Si lo no hace ningún tooconfigure desee para un enlace de certificado comodín, comente $DNSName = "+"y habilitar Hola después de la línea, la referencia de $DNSNAme completa de hello, ## $DNSName="$server.cloudapp.net".</span><span class="sxs-lookup"><span data-stu-id="da45d-301">If you do no want tooconfigure for a wildcard certificate binding, comment out $DNSName="+" and enable hello following line, hello full $DNSNAme reference, ##$DNSName="$server.cloudapp.net".</span></span>
     
       <span data-ttu-id="da45d-302">Cambie el valor de hello $DNSName si no desea que nombre DNS de la máquina virtual de toouse Hola para Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="da45d-302">Change hello $DNSName value if you do not want toouse hello virtual machine’s DNS name for Reporting Services.</span></span> <span data-ttu-id="da45d-303">Si usa el parámetro hello, certificado hello también debe usar este nombre y registrar nombre hello globalmente en un servidor DNS.</span><span class="sxs-lookup"><span data-stu-id="da45d-303">If you use hello parameter, hello certificate must also use this name and you register hello name globally on a DNS server.</span></span>
9. <span data-ttu-id="da45d-304">script de Hola está configurado actualmente para Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="da45d-304">hello script is currently configured for  Reporting Services.</span></span> <span data-ttu-id="da45d-305">Si desea que toorun Hola script para Reporting Services, modificar parte de la versión de Hola del espacio de nombres de toohello de ruta de acceso de hello demasiado "v11", en la instrucción de hello Get-WmiObject.</span><span class="sxs-lookup"><span data-stu-id="da45d-305">If you want toorun hello script for  Reporting Services, modify hello version portion of hello path toohello namespace too“v11”, on hello Get-WmiObject statement.</span></span>
10. <span data-ttu-id="da45d-306">Ejecutar script de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-306">Run hello script.</span></span>

<span data-ttu-id="da45d-307">**Validación**: tooverify que Hola funcionalidad del servidor de informes básica funciona, vea hello [Compruebe la configuración de hello](#verify-the-connection) sección más adelante en este tema.</span><span class="sxs-lookup"><span data-stu-id="da45d-307">**Validation**: tooverify that hello basic report server functionality is working, see hello [Verify hello configuration](#verify-the-connection) section later in this topic.</span></span> <span data-ttu-id="da45d-308">enlace de certificado de hello tooverify abra un símbolo del sistema con privilegios administrativos y, a continuación, ejecute el siguiente comando de Hola:</span><span class="sxs-lookup"><span data-stu-id="da45d-308">tooverify hello certificate binding open a command prompt with administrative privileges, and then run hello following command:</span></span>

    netsh http show sslcert

<span data-ttu-id="da45d-309">resultado de Hello incluirá siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="da45d-309">hello result will include hello following:</span></span>

    IP:port                      : 0.0.0.0:443

    Certificate Hash             : f98adf786994c1e4a153f53fe20f94210267d0e7

### <a name="use-configuration-manager-tooconfigure-hello-report-server"></a><span data-ttu-id="da45d-310">Hola tooConfigure use el Administrador de configuración del servidor de informes</span><span class="sxs-lookup"><span data-stu-id="da45d-310">Use Configuration Manager tooConfigure hello Report Server</span></span>
<span data-ttu-id="da45d-311">Si no desea toorun tooconfigure de secuencia de comandos de PowerShell Hola Forms Hola el servidor de informes, siga los pasos de hello en esta sección toouse Hola modo nativo configuration manager tooconfigure Hola servidor de Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="da45d-311">If you do not want toorun hello PowerShell script tooconfigure hello report server, follow hello steps in this section toouse hello Reporting Services native mode configuration manager tooconfigure hello report server.</span></span>

1. <span data-ttu-id="da45d-312">En hello portal de Azure clásico, seleccione Hola máquina virtual y haga clic en conectar.</span><span class="sxs-lookup"><span data-stu-id="da45d-312">From hello Azure classic portal, select hello VM and click connect.</span></span> <span data-ttu-id="da45d-313">Usar el nombre de usuario de Hola y la contraseña que configuró al crear Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="da45d-313">Use hello user name and password you configured when you created hello VM.</span></span>
   
    ![conectar máquina virtual de tooazure](./media/virtual-machines-windows-classic-ps-sql-report/IC650112.gif)
2. <span data-ttu-id="da45d-315">Ejecute Windows update e instale las actualizaciones toohello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="da45d-315">Run Windows update and install updates toohello VM.</span></span> <span data-ttu-id="da45d-316">Si se requiere un reinicio de hello VM, reiniciar Hola VM y vuelva a conectar toohello VM de hello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="da45d-316">If a restart of hello VM is required, restart hello VM and reconnect toohello VM from hello Azure classic portal.</span></span>
3. <span data-ttu-id="da45d-317">En el menú de inicio de hello en hello VM, escriba **Reporting Services** y abra **Reporting Services Configuration Manager**.</span><span class="sxs-lookup"><span data-stu-id="da45d-317">From hello Start menu on hello VM, type **Reporting Services** and open **Reporting Services Configuration Manager**.</span></span>
4. <span data-ttu-id="da45d-318">Deje los valores predeterminados de Hola para **nombre del servidor** y **instancia del servidor de informes**.</span><span class="sxs-lookup"><span data-stu-id="da45d-318">Leave hello default values for **Server Name** and **Report Server Instance**.</span></span> <span data-ttu-id="da45d-319">Haga clic en **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="da45d-319">Click **Connect**.</span></span>
5. <span data-ttu-id="da45d-320">En el panel izquierdo de hello, haga clic en **dirección URL del servicio Web**.</span><span class="sxs-lookup"><span data-stu-id="da45d-320">In hello left pane, click **Web Service URL**.</span></span>
6. <span data-ttu-id="da45d-321">De forma predeterminada, RS está configurado para el puerto 80 HTTP con la IP "Todas asignadas".</span><span class="sxs-lookup"><span data-stu-id="da45d-321">By default, RS is configured for HTTP port 80 with IP “All Assigned”.</span></span> <span data-ttu-id="da45d-322">tooadd HTTPS:</span><span class="sxs-lookup"><span data-stu-id="da45d-322">tooadd HTTPS:</span></span>
   
   1. <span data-ttu-id="da45d-323">En **certificado SSL**: certificado Hola seleccione desee toouse, por ejemplo [nombre de VM]. cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="da45d-323">In **SSL Certificate**: select hello certificate you want toouse, for example [VM name].cloudapp.net.</span></span> <span data-ttu-id="da45d-324">Si no aparece ningún certificado, vea la sección de hello **paso 2: crear un certificado de servidor** para obtener información sobre cómo tooinstall y confianza Hola certificado en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="da45d-324">If no certificates are listed, see hello section **Step 2: Create a Server Certificate** for information on how tooinstall and trust hello certificate on hello VM.</span></span>
   2. <span data-ttu-id="da45d-325">En **Puerto SSL**: elija 443.</span><span class="sxs-lookup"><span data-stu-id="da45d-325">Under **SSL Port**: choose 443.</span></span> <span data-ttu-id="da45d-326">Si configuró el extremo privado HTTPS de Hola Hola VM con otro puerto privado, usar ese valor aquí.</span><span class="sxs-lookup"><span data-stu-id="da45d-326">If you configured hello HTTPS private endpoint in hello VM with a different private port, use that value here.</span></span>
   3. <span data-ttu-id="da45d-327">Haga clic en **aplicar** y espere Hola operación toocomplete.</span><span class="sxs-lookup"><span data-stu-id="da45d-327">Click **Apply** and wait for hello operation toocomplete.</span></span>
7. <span data-ttu-id="da45d-328">En el panel izquierdo de hello, haga clic en **base de datos**.</span><span class="sxs-lookup"><span data-stu-id="da45d-328">In hello left pane, click **Database**.</span></span>
   
   1. <span data-ttu-id="da45d-329">Haga clic en **Cambiar base de datos**.</span><span class="sxs-lookup"><span data-stu-id="da45d-329">Click **Change Databas**e.</span></span>
   2. <span data-ttu-id="da45d-330">Haga clic en **Crear una nueva base de datos del servidor de informes** y luego en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="da45d-330">Click **Create a new report server database** and then click **Next**.</span></span>
   3. <span data-ttu-id="da45d-331">Deje Hola predeterminado **nombre del servidor**: Hola VM puede llamar y dejar predeterminado hello **tipo de autenticación** como **usuario actual** : **laseguridadintegrada**.</span><span class="sxs-lookup"><span data-stu-id="da45d-331">Leave hello default **Server Name**: as hello VM name and leave hello default **Authentication Type** as **Current User** – **Integrated Security**.</span></span> <span data-ttu-id="da45d-332">Haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="da45d-332">Click **Next**.</span></span>
   4. <span data-ttu-id="da45d-333">Deje Hola predeterminado **nombre de base de datos** como **ReportServer** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="da45d-333">Leave hello default **Database Name** as **ReportServer** and click **Next**.</span></span>
   5. <span data-ttu-id="da45d-334">Deje Hola predeterminado **tipo de autenticación** como **credenciales del servicio** y haga clic en **siguiente**.</span><span class="sxs-lookup"><span data-stu-id="da45d-334">Leave hello default **Authentication Type** as **Service Credentials** and click **Next**.</span></span>
   6. <span data-ttu-id="da45d-335">Haga clic en **siguiente** en hello **resumen** página.</span><span class="sxs-lookup"><span data-stu-id="da45d-335">Click **Next** on hello **Summary** page.</span></span>
   7. <span data-ttu-id="da45d-336">Una vez completada la configuración de hello, haga clic en **finalizar**.</span><span class="sxs-lookup"><span data-stu-id="da45d-336">When hello configuration is complete, click **Finish**.</span></span>
8. <span data-ttu-id="da45d-337">En el panel izquierdo de hello, haga clic en **Report Manager URL**.</span><span class="sxs-lookup"><span data-stu-id="da45d-337">In hello left pane, click **Report Manager URL**.</span></span> <span data-ttu-id="da45d-338">Deje Hola predeterminado **directorio Virtual** como **informes** y haga clic en **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="da45d-338">Leave hello default **Virtual Directory** as **Reports** and click **Apply**.</span></span>
9. <span data-ttu-id="da45d-339">Haga clic en **Exit** tooclose Hola Reporting Services Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="da45d-339">Click **Exit** tooclose hello Reporting Services Configuration Manager.</span></span>

## <a name="step-4-open-windows-firewall-port"></a><span data-ttu-id="da45d-340">Paso 4: abrir el puerto de Firewall de Windows</span><span class="sxs-lookup"><span data-stu-id="da45d-340">Step 4: Open Windows Firewall Port</span></span>
> [!NOTE]
> <span data-ttu-id="da45d-341">Si ha usado uno Hola scripts tooconfigure Hola servidor de informes, puede omitir esta sección.</span><span class="sxs-lookup"><span data-stu-id="da45d-341">If you used one of hello scripts tooconfigure hello report server, you can skip this section.</span></span> <span data-ttu-id="da45d-342">script de Hola incluye un puerto de firewall de paso tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-342">hello script included a step tooopen hello firewall port.</span></span> <span data-ttu-id="da45d-343">valor predeterminado de Hello era el puerto 80 para HTTP y el puerto 443 para HTTPS.</span><span class="sxs-lookup"><span data-stu-id="da45d-343">hello default was port 80 for HTTP and port 443 for HTTPS.</span></span>
> 
> 

<span data-ttu-id="da45d-344">tooconnect remotamente tooReport Manager u Hola de informes es necesario Server en la máquina virtual de hello, un extremo TCP en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="da45d-344">tooconnect remotely tooReport Manager or hello Report Server on hello virtual machine, a TCP Endpoint is required on hello VM.</span></span> <span data-ttu-id="da45d-345">Es hello tooopen necesario mismo número de puerto en firewall de la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-345">It is required tooopen hello same port in hello VM’s firewall.</span></span> <span data-ttu-id="da45d-346">Hola extremo se creó cuando se aprovisionó Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="da45d-346">hello endpoint was created when hello VM was provisioned.</span></span>

<span data-ttu-id="da45d-347">Esta sección proporciona información básica sobre cómo tooopen Hola puerto de firewall.</span><span class="sxs-lookup"><span data-stu-id="da45d-347">This section provides basic information on how tooopen hello firewall port.</span></span> <span data-ttu-id="da45d-348">Para más información, consulte [Configurar un firewall para el acceso del Servidor de informes](https://technet.microsoft.com/library/bb934283.aspx)</span><span class="sxs-lookup"><span data-stu-id="da45d-348">For more information, see [Configure a Firewall for Report Server Access](https://technet.microsoft.com/library/bb934283.aspx)</span></span>

> [!NOTE]
> <span data-ttu-id="da45d-349">Si utiliza el servidor de informes de hello script tooconfigure hello, puede omitir esta sección.</span><span class="sxs-lookup"><span data-stu-id="da45d-349">If you used hello script tooconfigure hello report server, you can skip this section.</span></span> <span data-ttu-id="da45d-350">script de Hola incluye un puerto de firewall de paso tooopen Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-350">hello script included a step tooopen hello firewall port.</span></span>
> 
> 

<span data-ttu-id="da45d-351">Si configura un puerto privado para HTTPS distinto de 443, modifique Hola siguiente secuencia de comandos de forma adecuada.</span><span class="sxs-lookup"><span data-stu-id="da45d-351">If you configured a private port for HTTPS other than 443, modify hello following script appropriately.</span></span> <span data-ttu-id="da45d-352">puerto de tooopen **443** en hello Firewall de Windows, realice el siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="da45d-352">tooopen port **443** on hello Windows Firewall, complete hello following:</span></span>

1. <span data-ttu-id="da45d-353">Abra la ventana de Windows PowerShell con privilegios administrativos.</span><span class="sxs-lookup"><span data-stu-id="da45d-353">Open a Windows PowerShell window with administrative privileges.</span></span>
2. <span data-ttu-id="da45d-354">Si usa un puerto distinto de 443 al configurar el punto de conexión de hello HTTPS en hello VM, actualizar el puerto de Hola Hola siguiente comando y, a continuación, ejecute el comando de hello:</span><span class="sxs-lookup"><span data-stu-id="da45d-354">If you used a port other than 443 when you configured hello HTTPS endpoint on hello VM, update hello port in hello following command and then run hello command:</span></span>
   
        New-NetFirewallRule -DisplayName “Report Server (TCP on port 443)” -Direction Inbound –Protocol TCP –LocalPort 443
3. <span data-ttu-id="da45d-355">Una vez completado el comando de hello, **Aceptar** se muestra en el símbolo del sistema Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-355">When hello command completes, **Ok** is displayed in hello command prompt.</span></span>

<span data-ttu-id="da45d-356">tooverify que se abre el puerto de hello, abra una ventana de Windows PowerShell y ejecución Hola siguiente comando:</span><span class="sxs-lookup"><span data-stu-id="da45d-356">tooverify that hello port is opened, open a Windows PowerShell window and run hello following command:</span></span>

    get-netfirewallrule | where {$_.displayname -like "*report*"} | select displayname,enabled,action

## <a name="verify-hello-configuration"></a><span data-ttu-id="da45d-357">Comprobar la configuración de Hola</span><span class="sxs-lookup"><span data-stu-id="da45d-357">Verify hello configuration</span></span>
<span data-ttu-id="da45d-358">tooverify que la funcionalidad del servidor de informes básica hello ahora funciona, abra el explorador con privilegios administrativos y, a continuación, examinar toohello siguiente URL del Administrador de informes de ad de servidor de informes:</span><span class="sxs-lookup"><span data-stu-id="da45d-358">tooverify that hello basic report server functionality is now working, open your browser with administrative privileges and then browse toohello following report server ad report manager URLS:</span></span>

* <span data-ttu-id="da45d-359">En hello VM, busque toohello dirección URL del servidor de informes:</span><span class="sxs-lookup"><span data-stu-id="da45d-359">On hello VM, browse toohello report server URL:</span></span>
  
        http://localhost/reportserver
* <span data-ttu-id="da45d-360">En hello VM, busque toohello dirección URL del Administrador de informes:</span><span class="sxs-lookup"><span data-stu-id="da45d-360">On hello VM, browse toohello report manger URL:</span></span>
  
        http://localhost/Reports
* <span data-ttu-id="da45d-361">Desde el equipo local, busque toohello **remoto** Administrador de informes en hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="da45d-361">From your local computer, browse toohello **remote** report Manager on hello VM.</span></span> <span data-ttu-id="da45d-362">Actualice el nombre DNS de Hola Hola siguiente ejemplo según corresponda.</span><span class="sxs-lookup"><span data-stu-id="da45d-362">Update hello DNS name in hello following example as appropriate.</span></span> <span data-ttu-id="da45d-363">Cuando se le pida una contraseña, utilice credenciales de administrador de Hola que creó cuando se aprovisionó Hola máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="da45d-363">When prompted for a password, use hello administrator credentials you created when hello VM was provisioned.</span></span> <span data-ttu-id="da45d-364">nombre de usuario de Hello es Hola [dominio]\[nombre de usuario] formato, donde dominio hello es el nombre de equipo para la máquina virtual de hello, por ejemplo ssrsnativecloud\testuser.</span><span class="sxs-lookup"><span data-stu-id="da45d-364">hello user name is in hello [Domain]\[user name] format, where hello domain is hello VM computer name, for example ssrsnativecloud\testuser.</span></span> <span data-ttu-id="da45d-365">Si no usa HTTP**S**, quitar hello **s** en dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-365">If you are not using HTTP**S**, remove hello **s** in hello URL.</span></span> <span data-ttu-id="da45d-366">Vea Hola próxima sección para obtener información sobre cómo crear usuarios adicionales en la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="da45d-366">See hello next section for information on creating additional users on VM.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/Reports
* <span data-ttu-id="da45d-367">Desde el equipo local, busque toohello dirección URL del servidor de informes remoto.</span><span class="sxs-lookup"><span data-stu-id="da45d-367">From your local computer, browse toohello remote report server URL.</span></span> <span data-ttu-id="da45d-368">Actualice el nombre DNS de Hola Hola siguiente ejemplo según corresponda.</span><span class="sxs-lookup"><span data-stu-id="da45d-368">Update hello DNS name in hello following example as appropriate.</span></span> <span data-ttu-id="da45d-369">Si no usa HTTP, quite Hola s en la dirección URL de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-369">If you are not using HTTPS, remove hello s in hello URL.</span></span>
  
        https://ssrsnativecloud.cloudapp.net/ReportServer

## <a name="create-users-and-assign-roles"></a><span data-ttu-id="da45d-370">Crear usuarios y asignar roles</span><span class="sxs-lookup"><span data-stu-id="da45d-370">Create Users and Assign Roles</span></span>
<span data-ttu-id="da45d-371">Después de configurar y verificar Hola el servidor de informes, una tarea administrativa común es toocreate uno o más usuarios y asignar usuarios tooReporting las funciones de servicios.</span><span class="sxs-lookup"><span data-stu-id="da45d-371">After configuring and verifying hello report server, a common administrative task is toocreate one or more users and assign users tooReporting Services roles.</span></span> <span data-ttu-id="da45d-372">Para obtener más información, vea Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="da45d-372">For more information, see hello following:</span></span>

* [<span data-ttu-id="da45d-373">Crear una cuenta de usuarios local</span><span class="sxs-lookup"><span data-stu-id="da45d-373">Create a local user account</span></span>](https://technet.microsoft.com/library/cc770642.aspx)
* <span data-ttu-id="da45d-374">[Conceder acceso de usuario tooa el servidor de informes (Administrador de informes)](https://msdn.microsoft.com/library/ms156034.aspx))</span><span class="sxs-lookup"><span data-stu-id="da45d-374">[Grant User Access tooa Report Server (Report Manager)](https://msdn.microsoft.com/library/ms156034.aspx))</span></span>
* [<span data-ttu-id="da45d-375">Crear y administrar asignaciones de roles</span><span class="sxs-lookup"><span data-stu-id="da45d-375">Create and Manage Role Assignments</span></span>](https://msdn.microsoft.com/library/ms155843.aspx)

## <a name="toocreate-and-publish-reports-toohello-azure-virtual-machine"></a><span data-ttu-id="da45d-376">tooCreate y publicar informes toohello Máquina Virtual de Azure</span><span class="sxs-lookup"><span data-stu-id="da45d-376">tooCreate and Publish Reports toohello Azure Virtual Machine</span></span>
<span data-ttu-id="da45d-377">Hello tabla siguiente resume algunas de hello opciones toopublish disponibles los informes existentes desde un servidor de informes de toohello de equipo local hospedado en hello Máquina Virtual de Microsoft Azure:</span><span class="sxs-lookup"><span data-stu-id="da45d-377">hello following table summarizes some of hello options available toopublish existing reports from an on-premises computer toohello report server hosted on hello Microsoft Azure Virtual Machine:</span></span>

* <span data-ttu-id="da45d-378">**Script RS.exe**: utilice RS.exe script toocopy elementos del informe y tooyour de servidor de informes existente Máquina Virtual de Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="da45d-378">**RS.exe script**: Use RS.exe script toocopy report items from and existing report server tooyour Microsoft Azure Virtual Machine.</span></span> <span data-ttu-id="da45d-379">Para obtener más información, vea la sección Hola "tooNative de modo nativo: modo de máquina Virtual de Microsoft Azure" en [Sample Reporting Services rs.exe Script tooMigrate contenido entre servidores de informes](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="da45d-379">For more information, see hello section “Native mode tooNative Mode – Microsoft Azure Virtual Machine” in [Sample Reporting Services rs.exe Script tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>
* <span data-ttu-id="da45d-380">**Generador de informes**: máquina virtual de hello incluye Hola click-una vez versión del generador de informes de Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="da45d-380">**Report Builder**: hello virtual machine includes hello click-once version of Microsoft SQL Server Report Builder.</span></span> <span data-ttu-id="da45d-381">Hola de generador de informes de toostart primera vez en la máquina virtual de hello:</span><span class="sxs-lookup"><span data-stu-id="da45d-381">toostart Report builder hello first time on hello virtual machine:</span></span>
  
  1. <span data-ttu-id="da45d-382">Inicie el explorador con privilegios administrativos.</span><span class="sxs-lookup"><span data-stu-id="da45d-382">Start your browser with administrative privileges.</span></span>
  2. <span data-ttu-id="da45d-383">Busque el Administrador de tooreport en la máquina virtual de Hola y haga clic en **Report Builder** en cinta de opciones de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-383">Browse tooreport manager on hello virtual machine and click **Report Builder**  in hello ribbon.</span></span>
     
     <span data-ttu-id="da45d-384">Para más información, consulte [Instalar, desinstalar y asistencia del Generador de informes](https://technet.microsoft.com/library/dd207038.aspx).</span><span class="sxs-lookup"><span data-stu-id="da45d-384">For more information, see [Installing, Uninstalling, and Supporting Report Builder](https://technet.microsoft.com/library/dd207038.aspx).</span></span>
* <span data-ttu-id="da45d-385">**SQL Server Data Tools: Máquina virtual**: si creaste Hola VM con SQL Server 2012, SQL Server Data Tools se instala en la máquina virtual de Hola y puede ser usado toocreate **proyectos de servidor de informes** e informes acerca de hello virtual máquina.</span><span class="sxs-lookup"><span data-stu-id="da45d-385">**SQL Server Data Tools: VM**:  If you created hello VM with SQL Server 2012, then SQL Server Data Tools is installed on hello virtual machine and can be used toocreate **Report Server Projects** and reports on hello virtual machine.</span></span> <span data-ttu-id="da45d-386">Herramientas de datos de SQL Server puede publicar el servidor de informes de toohello Hola informes en la máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-386">SQL Server Data Tools can publish hello reports toohello report server on hello virtual machine.</span></span>
  
    <span data-ttu-id="da45d-387">Si ha creado Hola VM con SQL server 2014, puede instalar a SQL Server Data Tools - BI para visual Studio.</span><span class="sxs-lookup"><span data-stu-id="da45d-387">If you created hello VM with SQL server 2014, you can install SQL Server Data Tools- BI for visual Studio.</span></span> <span data-ttu-id="da45d-388">Para obtener más información, vea Hola siguiente:</span><span class="sxs-lookup"><span data-stu-id="da45d-388">For more information, see hello following:</span></span>
  
  * [<span data-ttu-id="da45d-389">Microsoft SQL Server Data Tools - Business Intelligence para Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="da45d-389">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2013</span></span>](https://www.microsoft.com/download/details.aspx?id=42313)
  * [<span data-ttu-id="da45d-390">Microsoft SQL Server Data Tools - Business Intelligence para Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="da45d-390">Microsoft SQL Server Data Tools - Business Intelligence for Visual Studio 2012</span></span>](https://www.microsoft.com/download/details.aspx?id=36843)
  * [<span data-ttu-id="da45d-391">SQL Server Data Tools y SQL Server Business Intelligence (SSDT-BI)</span><span class="sxs-lookup"><span data-stu-id="da45d-391">SQL Server Data Tools and SQL Server Business Intelligence (SSDT-BI)</span></span>](http://curah.microsoft.com/30004/sql-server-data-tools-ssdt-and-sql-server-business-intelligence)
* <span data-ttu-id="da45d-392">**SQL Server Data Tools: remoto**: en el equipo local, cree un proyecto de Reporting Services en SQL Server Data Tools que contenga informes de Reporting Services.</span><span class="sxs-lookup"><span data-stu-id="da45d-392">**SQL Server Data Tools: Remote**:  On your local computer, create a Reporting Services project in SQL Server Data Tools that contains Reporting Services reports.</span></span> <span data-ttu-id="da45d-393">Configurar URL de servicio web de hello proyecto tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="da45d-393">Configure hello project tooconnect toohello web service URL.</span></span>
  
    ![propiedades del proyecto de ssdt para proyecto SSRS](./media/virtual-machines-windows-classic-ps-sql-report/IC650114.gif)
* <span data-ttu-id="da45d-395">**Usar script**: usar el contenido del servidor de informes de toocopy de secuencia de comandos.</span><span class="sxs-lookup"><span data-stu-id="da45d-395">**Use script**: Use script toocopy report server content.</span></span> <span data-ttu-id="da45d-396">Para obtener más información, consulte [Sample Reporting Services rs.exe Script tooMigrate contenido entre servidores de informes](https://msdn.microsoft.com/library/dn531017.aspx).</span><span class="sxs-lookup"><span data-stu-id="da45d-396">For more information, see [Sample Reporting Services rs.exe Script tooMigrate Content between Report Servers](https://msdn.microsoft.com/library/dn531017.aspx).</span></span>

## <a name="minimize-cost-if-you-are-not-using-hello-vm"></a><span data-ttu-id="da45d-397">Minimizar el costo si no usas Hola VM</span><span class="sxs-lookup"><span data-stu-id="da45d-397">Minimize cost if you are not using hello VM</span></span>
> [!NOTE]
> <span data-ttu-id="da45d-398">toominimize cargos para las máquinas virtuales de Azure cuando no esté en uso, apague Hola VM desde el portal de Azure clásico Hola.</span><span class="sxs-lookup"><span data-stu-id="da45d-398">toominimize charges for your Azure Virtual Machines when not in use, shut down hello VM from hello Azure classic portal.</span></span> <span data-ttu-id="da45d-399">Si utiliza opciones de energía de Windows hello dentro de un tooshut VM hacia abajo Hola VM, se sigue cobrando Hola mismo importe para hello máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="da45d-399">If you use hello Windows power options inside a VM tooshut down hello VM, you are still charged hello same amount for hello VM.</span></span> <span data-ttu-id="da45d-400">tooreduce se aplicarán cargos, necesita tooshut hacia abajo Hola VM Hola portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="da45d-400">tooreduce charges, you need tooshut down hello VM in hello Azure classic portal.</span></span> <span data-ttu-id="da45d-401">Si ya no necesita Hola VM, recuerde toodelete Hola VM y Hola cargos de almacenamiento de tooavoid de archivos .vhd asociado. Para obtener más información, vea la sección de preguntas más frecuentes de hello en [detalles de precios de máquinas virtuales](https://azure.microsoft.com/pricing/details/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="da45d-401">If you no longer need hello VM, remember toodelete hello VM and hello associated .vhd files tooavoid storage charges.For more information, see hello FAQ section at [Virtual Machines Pricing Details](https://azure.microsoft.com/pricing/details/virtual-machines/).</span></span>

## <a name="more-information"></a><span data-ttu-id="da45d-402">Más información</span><span class="sxs-lookup"><span data-stu-id="da45d-402">More Information</span></span>
### <a name="resources"></a><span data-ttu-id="da45d-403">Recursos</span><span class="sxs-lookup"><span data-stu-id="da45d-403">Resources</span></span>
* <span data-ttu-id="da45d-404">Para consultar contenido similar relacionados con la implementación de servidor único de tooa de SQL Server Business Intelligence y SharePoint 2013, vea [tooCreate de usar Windows PowerShell una máquina virtual de Azure con SQL Server BI y SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span><span class="sxs-lookup"><span data-stu-id="da45d-404">For similar content related tooa single server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Use Windows PowerShell tooCreate an Azure VM With SQL Server BI and SharePoint 2013](https://msdn.microsoft.com/library/azure/dn385843.aspx).</span></span>
* <span data-ttu-id="da45d-405">Para tooa relacionado de contenido similar consulte implementación de varios servidores de SQL Server Business Intelligence y SharePoint 2013, [implementar SQL Server Business Intelligence en máquinas virtuales Azure](https://msdn.microsoft.com/library/dn321998.aspx).</span><span class="sxs-lookup"><span data-stu-id="da45d-405">For similar content related tooa multi-server deployment of SQL Server Business Intelligence and SharePoint 2013, see [Deploy SQL Server Business Intelligence in Azure Virtual Machines](https://msdn.microsoft.com/library/dn321998.aspx).</span></span>
* <span data-ttu-id="da45d-406">Para obtener información General relacionadas toodeployments de SQL Server Business Intelligence en máquinas de virtuales de Azure, consulte [SQL Server Business Intelligence en máquinas virtuales Azure](virtual-machines-windows-classic-ps-sql-bi.md).</span><span class="sxs-lookup"><span data-stu-id="da45d-406">For General information related toodeployments of SQL Server Business Intelligence in Azure Virtual Machines, see [SQL Server Business Intelligence in Azure Virtual Machines](virtual-machines-windows-classic-ps-sql-bi.md).</span></span>
* <span data-ttu-id="da45d-407">Para obtener más información sobre el costo de hello del proceso de Azure, consulte la ficha de máquinas virtuales de Hola de [Calculadora de precios de Azure](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span><span class="sxs-lookup"><span data-stu-id="da45d-407">For more information about hello cost of Azure compute charges, see hello Virtual Machines tab of [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?scenario=virtual-machines).</span></span>

### <a name="community-content"></a><span data-ttu-id="da45d-408">Contenido de la Comunidad</span><span class="sxs-lookup"><span data-stu-id="da45d-408">Community Content</span></span>
* <span data-ttu-id="da45d-409">Para obtener instrucciones paso a paso sobre cómo toocreate un modo nativo de Reporting Services servidor de informes sin utilizar script, consulte [hospedar SQL Reporting Service en la máquina Virtual Azure](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span><span class="sxs-lookup"><span data-stu-id="da45d-409">For step by step instructions on how toocreate a Reporting Services Native mode report server without using script, see [Hosting SQL Reporting Service on Azure Virtual Machine](http://adititechnologiesblog.blogspot.in/2012/07/hosting-sql-reporting-service-on-azure.html).</span></span>

### <a name="links-tooother-resources-for-sql-server-in-azure-vms"></a><span data-ttu-id="da45d-410">Recursos de tooother de vínculos para SQL Server en máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="da45d-410">Links tooother resources for SQL Server in Azure VMs</span></span>
[<span data-ttu-id="da45d-411">Información general sobre SQL Server en máquinas virtuales de Azure</span><span class="sxs-lookup"><span data-stu-id="da45d-411">SQL Server on Azure Virtual Machines Overview</span></span>](../sql/virtual-machines-windows-sql-server-iaas-overview.md)

