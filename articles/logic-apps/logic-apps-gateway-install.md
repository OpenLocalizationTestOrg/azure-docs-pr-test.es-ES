---
title: "Instalación de una puerta de enlace de datos local: Azure Logic Apps | Microsoft Docs"
description: "Antes de obtener acceso a orígenes de datos locales, instale la puerta de enlace de datos local para obtener cifrado y transferencia de datos más rápidos entre orígenes de datos locales y aplicaciones lógicas."
keywords: "obtener acceso a datos, local, transferencia de datos, cifrado, orígenes de datos"
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 34e68ae7d35019848b35c785a2715ec458dc6e73
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="install-the-on-premises-data-gateway-for-azure-logic-apps"></a><span data-ttu-id="535c2-104">Instalación de la puerta de enlace de datos local para Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="535c2-104">Install the on-premises data gateway for Azure Logic Apps</span></span>

<span data-ttu-id="535c2-105">Para que las aplicaciones lógicas puedan obtener acceso a orígenes de datos locales, debe instalar y configurar la puerta de enlace de datos local.</span><span class="sxs-lookup"><span data-stu-id="535c2-105">Before your logic apps can access data sources on premises, you must install and set up the on-premises data gateway.</span></span> <span data-ttu-id="535c2-106">La puerta de enlace actúa como un puente que permite la transferencia de datos y el cifrado entre sistemas locales y las aplicaciones lógicas.</span><span class="sxs-lookup"><span data-stu-id="535c2-106">The gateway acts as a bridge that provides quick data transfer and encryption between on-premises systems and your logic apps.</span></span> <span data-ttu-id="535c2-107">La puerta de enlace retransmite datos desde orígenes locales en canales cifrados hasta Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="535c2-107">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="535c2-108">Todo el tráfico se origina como tráfico de salida seguro desde el agente de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="535c2-108">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="535c2-109">Más información sobre [cómo funciona la puerta de enlace de datos](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="535c2-109">Learn more about [how the data gateway works](#gateway-cloud-service).</span></span>

<span data-ttu-id="535c2-110">La puerta de enlace admite conexiones a estos orígenes de datos locales:</span><span class="sxs-lookup"><span data-stu-id="535c2-110">The gateway supports connections to these data sources on premises:</span></span>

*   <span data-ttu-id="535c2-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="535c2-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="535c2-112">DB2</span><span class="sxs-lookup"><span data-stu-id="535c2-112">DB2</span></span>  
*   <span data-ttu-id="535c2-113">Sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="535c2-113">File System</span></span>
*   <span data-ttu-id="535c2-114">Informix</span><span class="sxs-lookup"><span data-stu-id="535c2-114">Informix</span></span>
*   <span data-ttu-id="535c2-115">MQ</span><span class="sxs-lookup"><span data-stu-id="535c2-115">MQ</span></span>
*   <span data-ttu-id="535c2-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="535c2-116">MySQL</span></span>
*   <span data-ttu-id="535c2-117">Base de datos de Oracle</span><span class="sxs-lookup"><span data-stu-id="535c2-117">Oracle Database</span></span>
*   <span data-ttu-id="535c2-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="535c2-118">PostgreSQL</span></span>
*   <span data-ttu-id="535c2-119">Servidor de aplicaciones de SAP</span><span class="sxs-lookup"><span data-stu-id="535c2-119">SAP Application Server</span></span> 
*   <span data-ttu-id="535c2-120">Servidor de mensajes de SAP</span><span class="sxs-lookup"><span data-stu-id="535c2-120">SAP Message Server</span></span>
*   <span data-ttu-id="535c2-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="535c2-121">SharePoint</span></span>
*   <span data-ttu-id="535c2-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="535c2-122">SQL Server</span></span>
*   <span data-ttu-id="535c2-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="535c2-123">Teradata</span></span>

<span data-ttu-id="535c2-124">En estos pasos se muestra cómo instalar en primer lugar la puerta de enlace de datos local antes de [configurar una conexión entre la puerta de enlace y las aplicaciones lógicas](./logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="535c2-124">These steps show how to first install the on-premises data gateway before you [set up a connection between the gateway and your logic apps](./logic-apps-gateway-connection.md).</span></span> <span data-ttu-id="535c2-125">Para obtener más información sobre las conexiones admitidas, consulte [Conectores para Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="535c2-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span> 

<span data-ttu-id="535c2-126">Para información sobre cómo usar la puerta de enlace con otros servicios, consulte estos artículos:</span><span class="sxs-lookup"><span data-stu-id="535c2-126">For information about how to use the gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="535c2-127">Puerta de enlace de datos local de Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="535c2-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="535c2-128">Puerta de enlace de datos local de Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="535c2-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="535c2-129">Puerta de enlace de datos local de Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="535c2-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="535c2-130">Administración de una puerta de enlace de datos local en Microsoft PowerApps</span><span class="sxs-lookup"><span data-stu-id="535c2-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a><span data-ttu-id="535c2-131">Requisitos</span><span class="sxs-lookup"><span data-stu-id="535c2-131">Requirements</span></span>

<span data-ttu-id="535c2-132">**Mínimos**:</span><span class="sxs-lookup"><span data-stu-id="535c2-132">**Minimum**:</span></span>

* <span data-ttu-id="535c2-133">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="535c2-133">.NET 4.5 Framework</span></span>
* <span data-ttu-id="535c2-134">versión de 64 bits de Windows 7 o Windows Server 2008 R2 (o posterior)</span><span class="sxs-lookup"><span data-stu-id="535c2-134">64-bit version of Windows 7 or Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="535c2-135">**Recomendaciones**:</span><span class="sxs-lookup"><span data-stu-id="535c2-135">**Recommended**:</span></span>

* <span data-ttu-id="535c2-136">CPU de 8 núcleos</span><span class="sxs-lookup"><span data-stu-id="535c2-136">8 Core CPU</span></span>
* <span data-ttu-id="535c2-137">8 GB de memoria</span><span class="sxs-lookup"><span data-stu-id="535c2-137">8 GB Memory</span></span>
* <span data-ttu-id="535c2-138">versión de 64 bits de Windows 2012 R2 (o posterior)</span><span class="sxs-lookup"><span data-stu-id="535c2-138">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="535c2-139">**Consideraciones importantes**:</span><span class="sxs-lookup"><span data-stu-id="535c2-139">**Important considerations**:</span></span>

* <span data-ttu-id="535c2-140">Instale la puerta de enlace de datos local únicamente en un equipo local.</span><span class="sxs-lookup"><span data-stu-id="535c2-140">Install the on-premises data gateway only on a local computer.</span></span>
<span data-ttu-id="535c2-141">No puede instalarla en un controlador de dominio.</span><span class="sxs-lookup"><span data-stu-id="535c2-141">You can't install the gateway on a domain controller.</span></span>

   > [!TIP]
   > <span data-ttu-id="535c2-142">No tiene que instalar la puerta de enlace en el mismo equipo que el origen de datos.</span><span class="sxs-lookup"><span data-stu-id="535c2-142">You don't have to install the gateway on the same computer as your data source.</span></span> <span data-ttu-id="535c2-143">Para minimizar la latencia, puede instalar la puerta de enlace lo más cerca posible del origen de datos o en el mismo equipo, suponiendo que tiene los permisos necesarios.</span><span class="sxs-lookup"><span data-stu-id="535c2-143">To minimize latency, you can install the gateway as close as possible to your data source, or on the same computer, assuming that you have permissions.</span></span>

* <span data-ttu-id="535c2-144">No instale la puerta de enlace en un equipo que se apague, que entre en suspensión o que no se conecte a Internet, ya que no se puede ejecutar la puerta de enlace en esas circunstancias.</span><span class="sxs-lookup"><span data-stu-id="535c2-144">Don't install the gateway on a computer that turns off, goes to sleep, or doesn't connect to the Internet because the gateway can't run under those circumstances.</span></span> <span data-ttu-id="535c2-145">Además, el rendimiento de la puerta de enlace podría verse afectado en una red inalámbrica.</span><span class="sxs-lookup"><span data-stu-id="535c2-145">Also, gateway performance might suffer over a wireless network.</span></span>

* <span data-ttu-id="535c2-146">Durante la instalación, debe iniciar sesión con una [cuenta profesional o educativa](https://docs.microsoft.com/azure/active-directory/sign-up-organization) que está administrada por Azure Active Directory (Azure AD), no una cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="535c2-146">During installation, you must sign in with a [work or school account](https://docs.microsoft.com/azure/active-directory/sign-up-organization) that's managed by Azure Active Directory (Azure AD), not a Microsoft account.</span></span> 

  <span data-ttu-id="535c2-147">Tiene que usar la misma cuenta profesional o educativa más adelante en Azure Portal al crear un recurso de puerta de enlace y asociarlo a la instalación de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="535c2-147">You have to use the same work or school account later in the Azure portal when you create and associate a gateway resource with your gateway installation.</span></span> <span data-ttu-id="535c2-148">Este recurso de puerta de enlace se selecciona después al crear la conexión entre la aplicación lógica y el origen de datos local.</span><span class="sxs-lookup"><span data-stu-id="535c2-148">You then select this gateway resource when you create the connection between your logic app and the on-premises data source.</span></span> [<span data-ttu-id="535c2-149">¿Por qué debo usar una cuenta profesional o educativa de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="535c2-149">Why must I use an Azure AD work or school account?</span></span>](#why-azure-work-school-account)

  > [!TIP]
  > <span data-ttu-id="535c2-150">Si se suscribió a una oferta de Office 365 y no proporcionó su correo electrónico profesional real, la dirección de inicio de sesión podría tener un aspecto similar al siguiente: jeff@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="535c2-150">If you signed up for an Office 365 offering and didn't supply your actual work email, your sign-in address might look like jeff@contoso.onmicrosoft.com.</span></span> 

* <span data-ttu-id="535c2-151">Si tiene una puerta de enlace existente que configuró con un instalador que es anterior a la versión 14.16.6317.4, no puede cambiar la ubicación de la puerta de enlace ejecutando el programa de instalación más reciente.</span><span class="sxs-lookup"><span data-stu-id="535c2-151">If you have an existing gateway that you set up with an installer that's earlier than version 14.16.6317.4, you can't change your gateway's location by running the latest installer.</span></span> <span data-ttu-id="535c2-152">Sin embargo, puede usar el programa de instalación más reciente para instalar una puerta de enlace nueva con la ubicación que quiere en su lugar.</span><span class="sxs-lookup"><span data-stu-id="535c2-152">However, you can use the latest installer to set up a new gateway with the location that you want instead.</span></span>
  
  <span data-ttu-id="535c2-153">Si tiene un instalador de puerta de enlace que es anterior a la versión 14.16.6317.4, pero no ha instalado la puerta de enlace todavía, puede descargar y usar el programa de instalación más reciente.</span><span class="sxs-lookup"><span data-stu-id="535c2-153">If you have a gateway installer that's earlier than version 14.16.6317.4, but you haven't installed your gateway yet, you can download and use the latest installer.</span></span>

<a name="install-gateway"></a>

## <a name="install-the-data-gateway"></a><span data-ttu-id="535c2-154">Instalación de la puerta de enlace de datos</span><span class="sxs-lookup"><span data-stu-id="535c2-154">Install the data gateway</span></span>

1.  <span data-ttu-id="535c2-155">[Descargue y ejecute el programa de instalación de la puerta de enlace en un equipo local](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="535c2-155">[Download and run the gateway installer on a local computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span></span>

2. <span data-ttu-id="535c2-156">Revise y acepte las condiciones de uso y la declaración de privacidad.</span><span class="sxs-lookup"><span data-stu-id="535c2-156">Review and accept the terms of use and privacy statement.</span></span>

3. <span data-ttu-id="535c2-157">Especifique la ruta de acceso en el equipo local donde quiere instalar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="535c2-157">Specify the path on your local computer where you want to install the gateway.</span></span>

4. <span data-ttu-id="535c2-158">Cuando se le solicite, inicie sesión con su cuenta profesional o educativa de Azure, no con una cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="535c2-158">When prompted, sign in with your Azure work or school account, not a Microsoft account.</span></span>

   ![Inicio de sesión con una cuenta profesional o educativa de Azure](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. <span data-ttu-id="535c2-160">Registre ahora la puerta de enlace instalada con el [servicio en la nube de la puerta de enlace](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="535c2-160">Now register your installed gateway with the [gateway cloud service](#gateway-cloud-service).</span></span> <span data-ttu-id="535c2-161">Elija **Registrar una nueva puerta de enlace en este equipo**.</span><span class="sxs-lookup"><span data-stu-id="535c2-161">Choose **Register a new gateway on this computer**.</span></span>

   <span data-ttu-id="535c2-162">El servicio en la nube de la puerta de enlace cifra y almacena los detalles de la puerta de enlace y las credenciales del origen de datos.</span><span class="sxs-lookup"><span data-stu-id="535c2-162">The gateway cloud service encrypts and stores your data source credentials and gateway details.</span></span> 
   <span data-ttu-id="535c2-163">El servicio también enruta las consultas y sus resultados entre la aplicación lógica, la puerta de enlace de datos local y el origen de datos local.</span><span class="sxs-lookup"><span data-stu-id="535c2-163">The service also routes queries and their results between your logic app, the on-premises data gateway, and your data source on premises.</span></span>

6. <span data-ttu-id="535c2-164">Especifique un nombre para la instalación de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="535c2-164">Provide a name for your gateway installation.</span></span> <span data-ttu-id="535c2-165">Cree una clave de recuperación y luego confírmela.</span><span class="sxs-lookup"><span data-stu-id="535c2-165">Create a recovery key, then confirm your recovery key.</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="535c2-166">La clave de recuperación debe contener al menos ocho caracteres.</span><span class="sxs-lookup"><span data-stu-id="535c2-166">Your recovery key must contain at least eight characters.</span></span> <span data-ttu-id="535c2-167">Asegúrese de guardar y conservar la clave en un lugar seguro.</span><span class="sxs-lookup"><span data-stu-id="535c2-167">Make sure that you save and keep the key in a safe place.</span></span> <span data-ttu-id="535c2-168">También necesita esta clave cuando quiera migrar, restaurar o controlar una puerta de enlace existente.</span><span class="sxs-lookup"><span data-stu-id="535c2-168">You also need this key when you want to migrate, restore, or take over an existing gateway.</span></span>

   1. <span data-ttu-id="535c2-169">Para cambiar la región predeterminada del servicio en la nube de la puerta de enlace y de Azure Service Bus que usa la instalación de la puerta de enlace, elija **Cambiar región**.</span><span class="sxs-lookup"><span data-stu-id="535c2-169">To change the default region for the gateway cloud service and Azure Service Bus used by your gateway installation, choose **Change Region**.</span></span>

      ![Cambio de región](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      <span data-ttu-id="535c2-171">La región predeterminada es la asociada al inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="535c2-171">The default region is the region associated with your Azure AD tenant.</span></span>

   2. <span data-ttu-id="535c2-172">En el panel siguiente, abra **Seleccionar región** para elegir otra región.</span><span class="sxs-lookup"><span data-stu-id="535c2-172">On the next pane, open the **Select Region** to choose a different region.</span></span>

      ![Seleccione otra región.](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      <span data-ttu-id="535c2-174">Por ejemplo, puede seleccionar la misma región que la aplicación lógica o la región más cercana al origen de datos local para reducir la latencia.</span><span class="sxs-lookup"><span data-stu-id="535c2-174">For example, you might select the same region as your logic app, or select the region closest to your on-premises data source so you can reduce latency.</span></span> <span data-ttu-id="535c2-175">El recurso de puerta de enlace y la aplicación lógica pueden tener ubicaciones distintas.</span><span class="sxs-lookup"><span data-stu-id="535c2-175">Your gateway resource and logic app can have different locations.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="535c2-176">No puede cambiar esta región después de la instalación.</span><span class="sxs-lookup"><span data-stu-id="535c2-176">You can't change this region after installation.</span></span> <span data-ttu-id="535c2-177">Esta región también determina y restringe la ubicación en la que puede crear el recurso de Azure para la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="535c2-177">This region also determines and restricts the location where you can create the Azure resource for your gateway.</span></span> <span data-ttu-id="535c2-178">De modo que, al crear el recurso de puerta de enlace en Azure, asegúrese de que la ubicación del recurso coincide con la región que seleccionó durante la instalación de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="535c2-178">So when you create your gateway resource in Azure, make sure that the resource location matches the region that you selected during gateway installation.</span></span>
      > 
      > <span data-ttu-id="535c2-179">Si quiere usar una región distinta para la puerta de enlace más adelante, debe configurar una puerta de enlace nueva.</span><span class="sxs-lookup"><span data-stu-id="535c2-179">If you want to use a different region for your gateway later, you must set up a new gateway.</span></span>

   3. <span data-ttu-id="535c2-180">Cuando esté listo, elija **Hecho**.</span><span class="sxs-lookup"><span data-stu-id="535c2-180">When you're ready, choose **Done**.</span></span>

7. <span data-ttu-id="535c2-181">Ahora, siga estos pasos en Azure Portal para [crear un recurso de Azure para la puerta de enlace](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="535c2-181">Now follow these steps in the Azure portal so you can [create an Azure resource for your gateway](../logic-apps/logic-apps-gateway-connection.md).</span></span> 

<span data-ttu-id="535c2-182">Más información sobre [cómo funciona la puerta de enlace de datos](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="535c2-182">Learn more about [how the data gateway works](#gateway-cloud-service).</span></span>

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a><span data-ttu-id="535c2-183">Migrar, restaurar o controlar una puerta de enlace existente</span><span class="sxs-lookup"><span data-stu-id="535c2-183">Migrate, restore, or take over an existing gateway</span></span>

<span data-ttu-id="535c2-184">Para llevar a cabo estas tareas, debe tener la clave de recuperación que se especificó cuando se instaló la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="535c2-184">To perform these tasks, you must have the recovery key that was specified when the gateway was installed.</span></span>

1. <span data-ttu-id="535c2-185">En el menú Inicio del equipo, elija **Puerta de enlace de datos locales**.</span><span class="sxs-lookup"><span data-stu-id="535c2-185">From your computer's Start menu, choose **On-premises data gateway**.</span></span>

2. <span data-ttu-id="535c2-186">Cuando se abra el instalador, inicie sesión con la misma cuenta profesional o educativa de Azure que se usó anteriormente para instalar la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="535c2-186">After the installer opens, sign in with the same Azure work or school account that was previously used to install the gateway.</span></span>

3. <span data-ttu-id="535c2-187">Elija **Migrar, restaurar o controlar una puerta de enlace existente**.</span><span class="sxs-lookup"><span data-stu-id="535c2-187">Choose **Migrate, restore, or take over an existing gateway**.</span></span>

4. <span data-ttu-id="535c2-188">Especifique la clave de recuperación para la puerta de enlace que quiere migrar, restaurar o controlar.</span><span class="sxs-lookup"><span data-stu-id="535c2-188">Provide the name and recovery key for the gateway that you want to migrate, restore, or take over.</span></span>

<a name="restart-gateway"></a>
## <a name="restart-the-gateway"></a><span data-ttu-id="535c2-189">Reinicio de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="535c2-189">Restart the gateway</span></span>

<span data-ttu-id="535c2-190">La puerta de enlace se ejecuta como un servicio de Windows.</span><span class="sxs-lookup"><span data-stu-id="535c2-190">The gateway runs as a Windows service.</span></span> <span data-ttu-id="535c2-191">Al igual que con cualquier otro servicio de Windows, puede iniciar y detener el servicio de varias maneras.</span><span class="sxs-lookup"><span data-stu-id="535c2-191">Like any other Windows service, you can start and stop the service in multiple ways.</span></span> <span data-ttu-id="535c2-192">Por ejemplo, puede abrir un símbolo del sistema con permisos elevados en el equipo en el que se ejecuta la puerta de enlace y ejecutar cualquiera de estos comandos:</span><span class="sxs-lookup"><span data-stu-id="535c2-192">For example, you can open a command prompt with elevated permissions on the computer where the gateway is running, and run either these commands:</span></span>

* <span data-ttu-id="535c2-193">Para detener el servicio, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="535c2-193">To stop the service, run this command:</span></span>
  
    `net stop PBIEgwService`

* <span data-ttu-id="535c2-194">Para iniciar el servicio, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="535c2-194">To start the service, run this command:</span></span>
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a><span data-ttu-id="535c2-195">Cuenta de servicio de Windows</span><span class="sxs-lookup"><span data-stu-id="535c2-195">Windows service account</span></span>

<span data-ttu-id="535c2-196">La puerta de enlace de datos local está configurada para usar `NT SERVICE\PBIEgwService` para las credenciales de inicio de sesión del servicio de Windows.</span><span class="sxs-lookup"><span data-stu-id="535c2-196">The on-premises data gateway is set up to use `NT SERVICE\PBIEgwService` for the Windows service logon credentials.</span></span> <span data-ttu-id="535c2-197">De forma predeterminada, la puerta de enlace tiene el derecho "Iniciar sesión como servicio" en la máquina donde se instala la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="535c2-197">By default, the gateway has the "Log on as a service" right for the machine where you install the gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="535c2-198">Esta cuenta de servicio de Windows no es la misma que se usa para conectarse a orígenes de datos locales, ni la cuenta profesional o educativa de Azure que se usa para iniciar sesión en servicios en la nube.</span><span class="sxs-lookup"><span data-stu-id="535c2-198">The Windows service account differs from the account used for connecting to on-premises data sources, and from the Azure work or school account used to sign in to cloud services.</span></span>

## <a name="configure-a-firewall-or-proxy"></a><span data-ttu-id="535c2-199">Configuración de un firewall o proxy</span><span class="sxs-lookup"><span data-stu-id="535c2-199">Configure a firewall or proxy</span></span>

<span data-ttu-id="535c2-200">La puerta de enlace crea una conexión de salida a [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="535c2-200">The gateway creates an outbound connection to [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="535c2-201">Para proporcionar información del proxy para la puerta de enlace, consulte [Configuración de proxy](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span><span class="sxs-lookup"><span data-stu-id="535c2-201">To provide proxy information for your gateway, see [Configure proxy settings](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span></span>

<span data-ttu-id="535c2-202">Para comprobar si el firewall o el proxy puede bloquear conexiones, confirme si el equipo puede conectarse realmente a Internet y a [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="535c2-202">To check whether your firewall, or proxy, might block connections, confirm whether your machine can actually connect to the internet and the [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="535c2-203">Desde un símbolo del sistema de PowerShell, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="535c2-203">From a PowerShell prompt, run this command:</span></span>

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> <span data-ttu-id="535c2-204">Este comando solo comprueba la conectividad de red y la conectividad a Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="535c2-204">This command only tests network connectivity and connectivity to the Azure Service Bus.</span></span> <span data-ttu-id="535c2-205">Por lo tanto, el comando no tiene nada que ver con la puerta de enlace ni con el servicio en la nube de la puerta de enlace que cifra y almacena las credenciales y los detalles de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="535c2-205">So the command doesn't have anything to do with the gateway or the gateway cloud service that encrypts and stores your credentials and gateway details.</span></span> 
>
> <span data-ttu-id="535c2-206">Además, este comando solo está disponible en Windows Server 2012 R2 o posterior y Windows 8.1 o posterior.</span><span class="sxs-lookup"><span data-stu-id="535c2-206">Also, this command is only available on Windows Server 2012 R2 or later, and Windows 8.1 or later.</span></span> <span data-ttu-id="535c2-207">En versiones anteriores del sistema operativo, puede usar Telnet para probar la conectividad.</span><span class="sxs-lookup"><span data-stu-id="535c2-207">On earlier OS versions, you can use Telnet to test connectivity.</span></span> <span data-ttu-id="535c2-208">Obtenga más información sobre [Azure Service Bus y soluciones híbridas](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="535c2-208">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

<span data-ttu-id="535c2-209">Los resultados deben ser parecidos a los del ejemplo siguiente:</span><span class="sxs-lookup"><span data-stu-id="535c2-209">Your results should look similar to this example:</span></span>

```text
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

<span data-ttu-id="535c2-210">Si el valor de **TcpTestSucceeded** no es **True**, podría estar bloqueado por un firewall.</span><span class="sxs-lookup"><span data-stu-id="535c2-210">If **TcpTestSucceeded** is not set to **True**, you might be blocked by a firewall.</span></span> <span data-ttu-id="535c2-211">Si quiere ser detallado, sustituya los valores de **ComputerName** y **Port** por los que aparecen en [Configuración de los puertos](#configure-ports) en este tema.</span><span class="sxs-lookup"><span data-stu-id="535c2-211">If you want to be comprehensive, substitute the **ComputerName** and **Port** values with the values listed under [Configure ports](#configure-ports) in this topic.</span></span>

<span data-ttu-id="535c2-212">El firewall también podría estar bloqueando las conexiones de Azure Service Bus con los centros de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="535c2-212">The firewall might also block connections that the Azure Service Bus makes to the Azure datacenters.</span></span> <span data-ttu-id="535c2-213">Si se produce este escenario, apruebe (desbloquee) todas las direcciones IP de esos centros de datos en su región.</span><span class="sxs-lookup"><span data-stu-id="535c2-213">If this scenario happens, approve (unblock) all the IP addresses for those datacenters in your region.</span></span> <span data-ttu-id="535c2-214">Para esas direcciones IP, puede [obtener la lista de direcciones IP de Azure aquí](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="535c2-214">For those IP addresses, [get the Azure IP addresses list here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

## <a name="configure-ports"></a><span data-ttu-id="535c2-215">Configuración de los puertos</span><span class="sxs-lookup"><span data-stu-id="535c2-215">Configure ports</span></span>

<span data-ttu-id="535c2-216">La puerta de enlace crea una conexión de salida a [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) y se comunica en los puertos de salida: TCP 443 (predeterminado), 5671, 5672 y del 9350 al 9354.</span><span class="sxs-lookup"><span data-stu-id="535c2-216">The gateway creates an outbound connection to [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) and communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span> <span data-ttu-id="535c2-217">La puerta de enlace no requiere puertos de entrada.</span><span class="sxs-lookup"><span data-stu-id="535c2-217">The gateway doesn't require inbound ports.</span></span> <span data-ttu-id="535c2-218">Obtenga más información sobre [Azure Service Bus y soluciones híbridas](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="535c2-218">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

| <span data-ttu-id="535c2-219">NOMBRES DE DOMINIO</span><span class="sxs-lookup"><span data-stu-id="535c2-219">DOMAIN NAMES</span></span> | <span data-ttu-id="535c2-220">PUERTOS DE SALIDA</span><span class="sxs-lookup"><span data-stu-id="535c2-220">OUTBOUND PORTS</span></span> | <span data-ttu-id="535c2-221">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="535c2-221">DESCRIPTION</span></span> |
| --- | --- | --- |
| <span data-ttu-id="535c2-222">*. analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="535c2-222">*.analysis.windows.net</span></span> | <span data-ttu-id="535c2-223">443</span><span class="sxs-lookup"><span data-stu-id="535c2-223">443</span></span> | <span data-ttu-id="535c2-224">HTTPS</span><span class="sxs-lookup"><span data-stu-id="535c2-224">HTTPS</span></span> | 
| <span data-ttu-id="535c2-225">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="535c2-225">*.login.windows.net</span></span> | <span data-ttu-id="535c2-226">443</span><span class="sxs-lookup"><span data-stu-id="535c2-226">443</span></span> | <span data-ttu-id="535c2-227">HTTPS</span><span class="sxs-lookup"><span data-stu-id="535c2-227">HTTPS</span></span> | 
| <span data-ttu-id="535c2-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="535c2-228">*.servicebus.windows.net</span></span> | <span data-ttu-id="535c2-229">5671-5672</span><span class="sxs-lookup"><span data-stu-id="535c2-229">5671-5672</span></span> | <span data-ttu-id="535c2-230">Advanced Message Queuing Protocol (AMQP)</span><span class="sxs-lookup"><span data-stu-id="535c2-230">Advanced Message Queuing Protocol (AMQP)</span></span> | 
| <span data-ttu-id="535c2-231">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="535c2-231">*.servicebus.windows.net</span></span> | <span data-ttu-id="535c2-232">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="535c2-232">443, 9350-9354</span></span> | <span data-ttu-id="535c2-233">Agentes de escucha en Service Bus Relay sobre TCP (requiere 443 para la adquisición del token de Access Control)</span><span class="sxs-lookup"><span data-stu-id="535c2-233">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> | 
| <span data-ttu-id="535c2-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="535c2-234">*.frontend.clouddatahub.net</span></span> | <span data-ttu-id="535c2-235">443</span><span class="sxs-lookup"><span data-stu-id="535c2-235">443</span></span> | <span data-ttu-id="535c2-236">HTTPS</span><span class="sxs-lookup"><span data-stu-id="535c2-236">HTTPS</span></span> | 
| <span data-ttu-id="535c2-237">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="535c2-237">*.core.windows.net</span></span> | <span data-ttu-id="535c2-238">443</span><span class="sxs-lookup"><span data-stu-id="535c2-238">443</span></span> | <span data-ttu-id="535c2-239">HTTPS</span><span class="sxs-lookup"><span data-stu-id="535c2-239">HTTPS</span></span> | 
| <span data-ttu-id="535c2-240">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="535c2-240">login.microsoftonline.com</span></span> | <span data-ttu-id="535c2-241">443</span><span class="sxs-lookup"><span data-stu-id="535c2-241">443</span></span> | <span data-ttu-id="535c2-242">HTTPS</span><span class="sxs-lookup"><span data-stu-id="535c2-242">HTTPS</span></span> | 
| <span data-ttu-id="535c2-243">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="535c2-243">*.msftncsi.com</span></span> | <span data-ttu-id="535c2-244">443</span><span class="sxs-lookup"><span data-stu-id="535c2-244">443</span></span> | <span data-ttu-id="535c2-245">Se utiliza para probar la conectividad a Internet cuando el servicio Power BI no puede acceder a la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="535c2-245">Used to test internet connectivity when the gateway is unreachable by the Power BI service.</span></span> | 

<span data-ttu-id="535c2-246">Si tiene que aprobar direcciones IP en lugar de los dominios, puede descargar y usar la [lista de intervalos IP de Microsoft Azure Datacenter](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="535c2-246">If you have to approve IP addresses instead of the domains, you can download and use the [Microsoft Azure Datacenter IP ranges list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="535c2-247">En algunos casos, las conexiones a Azure Service Bus se realizarán con la dirección IP en lugar de con nombres de dominio completos.</span><span class="sxs-lookup"><span data-stu-id="535c2-247">In some cases, the Azure Service Bus connections are made with IP Address rather than fully qualified domain names.</span></span>

<a name="gateway-cloud-service"></a>
## <a name="how-does-the-data-gateway-work"></a><span data-ttu-id="535c2-248">¿Cómo funciona la puerta de enlace de datos?</span><span class="sxs-lookup"><span data-stu-id="535c2-248">How does the data gateway work?</span></span>

<span data-ttu-id="535c2-249">La puerta de enlace de datos facilita la comunicación rápida y segura entre la aplicación lógica, el servicio en la nube de la puerta de enlace y el origen de datos local.</span><span class="sxs-lookup"><span data-stu-id="535c2-249">The data gateway facilitates quick and secure communication between your logic app, the gateway cloud service, and your on-premises data source.</span></span> 

![diagram-for-on-premises-data-gateway-flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

<span data-ttu-id="535c2-251">Por lo tanto, cuando el usuario en la nube interactúa con un elemento conectado a un origen de datos local, sucede lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="535c2-251">So when the user in the cloud interacts with an element that's connected to your on-premises data source:</span></span>

1. <span data-ttu-id="535c2-252">El servicio en la nube de la puerta de enlace crea una consulta, junto con las credenciales cifradas del origen de datos y la envía a la cola de la puerta de enlace por procesar.</span><span class="sxs-lookup"><span data-stu-id="535c2-252">The gateway cloud service creates a query, along with the encrypted credentials for the data source, and sends the query to the queue for the gateway to process.</span></span>

2. <span data-ttu-id="535c2-253">El servicio en la nube de la puerta de enlace analiza la consulta e inserta la solicitud en la instancia de Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="535c2-253">The gateway cloud service analyzes the query and pushes the request to the Azure Service Bus.</span></span>

3. <span data-ttu-id="535c2-254">La puerta de enlace de datos local sondea el bus de servicio de Azure en busca de solicitudes pendientes.</span><span class="sxs-lookup"><span data-stu-id="535c2-254">The on-premises data gateway polls the Azure Service Bus for pending requests.</span></span>

4. <span data-ttu-id="535c2-255">La puerta de enlace obtiene la consulta, descifra las credenciales y se conecta al origen de datos con ellas.</span><span class="sxs-lookup"><span data-stu-id="535c2-255">The gateway gets the query, decrypts the credentials, and connects to the data source with those credentials.</span></span>

5. <span data-ttu-id="535c2-256">La puerta de enlace envía la consulta al origen de datos para su ejecución.</span><span class="sxs-lookup"><span data-stu-id="535c2-256">The gateway sends the query to the data source for execution.</span></span>

6. <span data-ttu-id="535c2-257">Los resultados se envían desde el origen de datos, de vuelta a la puerta de enlace y, después, al servicio en la nube de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="535c2-257">The results are sent from the data source, back to the gateway, and then to the gateway cloud service.</span></span> <span data-ttu-id="535c2-258">Seguidamente, el servicio en la nube de la puerta de enlace usa los resultados.</span><span class="sxs-lookup"><span data-stu-id="535c2-258">The gateway cloud service then uses the results.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="535c2-259">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="535c2-259">Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="535c2-260">General</span><span class="sxs-lookup"><span data-stu-id="535c2-260">General</span></span>

<span data-ttu-id="535c2-261">**P**: ¿Necesito una puerta de enlace para los orígenes de datos en la nube como, por ejemplo, SQL Azure?</span><span class="sxs-lookup"><span data-stu-id="535c2-261">**Q**: Do I need a gateway for data sources in the cloud, such as SQL Azure?</span></span> <br/><span data-ttu-id="535c2-262">
**R:** No.</span><span class="sxs-lookup"><span data-stu-id="535c2-262">
**A**: No.</span></span> <span data-ttu-id="535c2-263">Las puertas de enlace se conectan únicamente a orígenes de datos locales.</span><span class="sxs-lookup"><span data-stu-id="535c2-263">A gateway connects to on-premises data sources only.</span></span>

<span data-ttu-id="535c2-264">**P**: ¿La puerta de enlace debe estar instalada en la misma máquina que el origen de datos?</span><span class="sxs-lookup"><span data-stu-id="535c2-264">**Q**: Does the gateway have to be installed on the same machine as the data source?</span></span> <br/><span data-ttu-id="535c2-265">
**R:** No.</span><span class="sxs-lookup"><span data-stu-id="535c2-265">
**A**: No.</span></span> <span data-ttu-id="535c2-266">La puerta de enlace se conecta al origen de datos mediante la información de conexión que se proporcionó.</span><span class="sxs-lookup"><span data-stu-id="535c2-266">The gateway connects to the data source using the connection information that was provided.</span></span> <span data-ttu-id="535c2-267">Considere la puerta de enlace como una aplicación cliente en este sentido.</span><span class="sxs-lookup"><span data-stu-id="535c2-267">Consider the gateway as a client application in this sense.</span></span> <span data-ttu-id="535c2-268">La puerta de enlace solo necesita la funcionalidad para conectarse al nombre de servidor que se proporcionó.</span><span class="sxs-lookup"><span data-stu-id="535c2-268">The gateway just needs the capability to connect to the server name that was provided.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="535c2-269">**P**: ¿Por qué debo usar una cuenta profesional o educativa de Azure para iniciar sesión?</span><span class="sxs-lookup"><span data-stu-id="535c2-269">**Q**: Why must I use an Azure work or school account to sign in?</span></span> <br/><span data-ttu-id="535c2-270">
**R**: Solo puede usar una cuenta profesional o educativa de Azure al instalar la puerta de enlace de datos local.</span><span class="sxs-lookup"><span data-stu-id="535c2-270">
**A**: You can only use an Azure work or school account when you install the on-premises data gateway.</span></span> <span data-ttu-id="535c2-271">Su cuenta de inicio de sesión se almacena en un inquilino administrado por Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="535c2-271">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="535c2-272">Por lo general, el nombre principal de usuario (UPN) de la cuenta de Azure AD coincide con la dirección de correo electrónico.</span><span class="sxs-lookup"><span data-stu-id="535c2-272">Usually, your Azure AD account's user principal name (UPN) matches the email address.</span></span>

<span data-ttu-id="535c2-273">**P**: ¿Dónde se almacenan mis credenciales?</span><span class="sxs-lookup"><span data-stu-id="535c2-273">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="535c2-274">
**R**: Las credenciales que especifique para un origen de datos se cifran y almacenan en el servicio en la nube de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="535c2-274">
**A**: The credentials that you enter for a data source are encrypted and stored in the gateway cloud service.</span></span> <span data-ttu-id="535c2-275">Las credenciales se descifran en la puerta de enlace de datos local.</span><span class="sxs-lookup"><span data-stu-id="535c2-275">The credentials are decrypted at the on-premises data gateway.</span></span>

<span data-ttu-id="535c2-276">**P**: ¿Hay algún requisito con respecto al ancho de banda de red?</span><span class="sxs-lookup"><span data-stu-id="535c2-276">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="535c2-277">
**R**: Se recomienda que la conexión de red tenga buen rendimiento.</span><span class="sxs-lookup"><span data-stu-id="535c2-277">
**A**: We recommend that your network connection has good throughput.</span></span> <span data-ttu-id="535c2-278">Cada entorno es diferente, y la cantidad de datos que se envíe afecta a los resultados.</span><span class="sxs-lookup"><span data-stu-id="535c2-278">Every environment is different, and the amount of data being sent affects the results.</span></span> <span data-ttu-id="535c2-279">Si usa ExpressRoute, podrá ayudar a garantizar un nivel de rendimiento entre los centros de datos locales y los de Azure.</span><span class="sxs-lookup"><span data-stu-id="535c2-279">Using ExpressRoute could help to guarantee a level of throughput between on-premises and the Azure datacenters.</span></span>
<span data-ttu-id="535c2-280">Puede usar la aplicación Azure Speed Test (desarrollada por un tercero) para medir su rendimiento.</span><span class="sxs-lookup"><span data-stu-id="535c2-280">You can use the third-party tool Azure Speed Test app to help gauge your throughput.</span></span>

<span data-ttu-id="535c2-281">**P**: ¿cuál es la latencia para la ejecución de consultas en un origen de datos desde la puerta de enlace?</span><span class="sxs-lookup"><span data-stu-id="535c2-281">**Q**: What is the latency for running queries to a data source from the gateway?</span></span> <span data-ttu-id="535c2-282">¿Cuál es la mejor arquitectura?</span><span class="sxs-lookup"><span data-stu-id="535c2-282">What is the best architecture?</span></span> <br/><span data-ttu-id="535c2-283">
**R**: Para reducir la latencia de red, instale la puerta de enlace lo más cerca posible del origen de datos.</span><span class="sxs-lookup"><span data-stu-id="535c2-283">
**A**: To reduce network latency, install the gateway as close to the data source as possible.</span></span> <span data-ttu-id="535c2-284">Si puede instalar la puerta de enlace en el propio origen de datos, esta proximidad minimizará la latencia introducida.</span><span class="sxs-lookup"><span data-stu-id="535c2-284">If you can install the gateway on the actual data source, this proximity minimizes the latency introduced.</span></span> <span data-ttu-id="535c2-285">Tenga en cuenta también los centros de datos.</span><span class="sxs-lookup"><span data-stu-id="535c2-285">Consider the datacenters too.</span></span> <span data-ttu-id="535c2-286">Por ejemplo, si el servicio usa el centro de datos del oeste de EE. UU. y tiene SQL Server hospedado en una máquina virtual de Azure, esta debería encontrarse también en el oeste de EE. UU.</span><span class="sxs-lookup"><span data-stu-id="535c2-286">For example, if your service uses the West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in the West US too.</span></span> <span data-ttu-id="535c2-287">Esta proximidad minimiza la latencia y evita los cargos de salida en la máquina virtual de Azure.</span><span class="sxs-lookup"><span data-stu-id="535c2-287">This proximity minimizes latency and avoids egress charges on the Azure VM.</span></span>

<span data-ttu-id="535c2-288">**P**: ¿Cómo se devuelven los resultados a la nube?</span><span class="sxs-lookup"><span data-stu-id="535c2-288">**Q**: How are results sent back to the cloud?</span></span> <br/><span data-ttu-id="535c2-289">
**R**: Los resultados se envían a través de Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="535c2-289">
**A**: Results are sent through the Azure Service Bus.</span></span>

<span data-ttu-id="535c2-290">**P**: ¿Hay alguna conexión de entrada a la puerta de enlace desde la nube?</span><span class="sxs-lookup"><span data-stu-id="535c2-290">**Q**: Are there any inbound connections to the gateway from the cloud?</span></span> <br/><span data-ttu-id="535c2-291">
**R:** No.</span><span class="sxs-lookup"><span data-stu-id="535c2-291">
**A**: No.</span></span> <span data-ttu-id="535c2-292">La puerta de enlace usa conexiones de salida al bus de servicio de Azure.</span><span class="sxs-lookup"><span data-stu-id="535c2-292">The gateway uses outbound connections to Azure Service Bus.</span></span>

<span data-ttu-id="535c2-293">**P**: ¿Qué sucede si bloqueo las conexiones de salida?</span><span class="sxs-lookup"><span data-stu-id="535c2-293">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="535c2-294">¿Qué tengo que abrir?</span><span class="sxs-lookup"><span data-stu-id="535c2-294">What do I need to open?</span></span> <br/><span data-ttu-id="535c2-295">
**R**: Consulte los puertos y los hosts que usa la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="535c2-295">
**A**: See the ports and hosts that the gateway uses.</span></span>

<span data-ttu-id="535c2-296">**P**: ¿Cómo se llama el servicio real de Windows?</span><span class="sxs-lookup"><span data-stu-id="535c2-296">**Q**: What is the actual Windows service called?</span></span><br/><span data-ttu-id="535c2-297">
**R**: En los servicios, la puerta de enlace se llama Servicio Power BI Enterprise Gateway.</span><span class="sxs-lookup"><span data-stu-id="535c2-297">
**A**: In Services, the gateway is called Power BI Enterprise Gateway Service.</span></span>

<span data-ttu-id="535c2-298">**P**: ¿Se puede ejecutar el servicio de Windows de puerta de enlace con una cuenta de Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="535c2-298">**Q**: Can the gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="535c2-299">
**R:** No.</span><span class="sxs-lookup"><span data-stu-id="535c2-299">
**A**: No.</span></span> <span data-ttu-id="535c2-300">El servicio de Windows debe tener una cuenta de Windows válida.</span><span class="sxs-lookup"><span data-stu-id="535c2-300">The Windows service must have a valid Windows account.</span></span> <span data-ttu-id="535c2-301">De forma predeterminada, el servicio se ejecuta con el SID de servicio NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="535c2-301">By default, the service runs with the Service SID, NT SERVICE\PBIEgwService.</span></span>

### <a name="high-availability-and-disaster-recovery"></a><span data-ttu-id="535c2-302">Alta disponibilidad y recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="535c2-302">High availability and disaster recovery</span></span>

<span data-ttu-id="535c2-303">**P**: ¿Cuáles son las opciones de recuperación ante desastres disponibles?</span><span class="sxs-lookup"><span data-stu-id="535c2-303">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="535c2-304">
**R**: Puede usar la clave de recuperación para restaurar o mover una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="535c2-304">
**A**: You can use the recovery key to restore or move a gateway.</span></span> <span data-ttu-id="535c2-305">Cuando instale la puerta de enlace, especifique la clave de recuperación.</span><span class="sxs-lookup"><span data-stu-id="535c2-305">When you install the gateway, specify the recovery key.</span></span>

<span data-ttu-id="535c2-306">**P**: ¿Qué ventaja aporta la clave de recuperación?</span><span class="sxs-lookup"><span data-stu-id="535c2-306">**Q**: What is the benefit of the recovery key?</span></span> <br/><span data-ttu-id="535c2-307">
**R**: La clave de recuperación proporciona una forma de migrar o recuperar la configuración de la puerta de enlace después de un desastre.</span><span class="sxs-lookup"><span data-stu-id="535c2-307">
**A**: The recovery key provides a way to migrate or recover your gateway settings after a disaster.</span></span>

<span data-ttu-id="535c2-308">**P**: ¿Hay algún plan para habilitar escenarios de alta disponibilidad con la puerta de enlace?</span><span class="sxs-lookup"><span data-stu-id="535c2-308">**Q**: Are there any plans for enabling high availability scenarios with the gateway?</span></span> <br/><span data-ttu-id="535c2-309">
**R**: Estos escenarios figuran en nuestra agenda, pero aún no tenemos una escala de tiempo.</span><span class="sxs-lookup"><span data-stu-id="535c2-309">
**A**: These scenarios are on the roadmap, but we don't have a timeline yet.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="535c2-310">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="535c2-310">Troubleshooting</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

<span data-ttu-id="535c2-311">**P**: ¿Cómo se pueden ver las consultas que se envían al origen de datos local?</span><span class="sxs-lookup"><span data-stu-id="535c2-311">**Q**: How can I see what queries are being sent to the on-premises data source?</span></span> <br/><span data-ttu-id="535c2-312">
**R**: Puede habilitar el seguimiento de consultas, que incluye las consultas que se envían.</span><span class="sxs-lookup"><span data-stu-id="535c2-312">
**A**: You can enable query tracing, which includes the queries that are sent.</span></span> <span data-ttu-id="535c2-313">No olvide devolver el seguimiento de consultas al valor original cuando haya terminado de solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="535c2-313">Remember to change query tracing back to the original value when done troubleshooting.</span></span> <span data-ttu-id="535c2-314">Si lo deja activado, crea registros de mayor tamaño.</span><span class="sxs-lookup"><span data-stu-id="535c2-314">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="535c2-315">También puede examinar las herramientas de que dispone su origen de datos para el seguimiento de consultas.</span><span class="sxs-lookup"><span data-stu-id="535c2-315">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="535c2-316">Por ejemplo, puede utilizar Eventos extendidos o SQL Profiler en SQL Server y Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="535c2-316">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="535c2-317">**P**: ¿Dónde están los registros de la puerta de enlace?</span><span class="sxs-lookup"><span data-stu-id="535c2-317">**Q**: Where are the gateway logs?</span></span> <br/><span data-ttu-id="535c2-318">
**R**: Consulte la sección Herramientas de este mismo tema.</span><span class="sxs-lookup"><span data-stu-id="535c2-318">
**A**: See Tools later in this topic.</span></span>

### <a name="update-to-the-latest-version"></a><span data-ttu-id="535c2-319">Actualización a la versión más reciente</span><span class="sxs-lookup"><span data-stu-id="535c2-319">Update to the latest version</span></span>

<span data-ttu-id="535c2-320">Pueden surgir muchos problemas cuando la versión de la puerta de enlace deja de estar actualizada.</span><span class="sxs-lookup"><span data-stu-id="535c2-320">Many issues can surface when the gateway version becomes outdated.</span></span> <span data-ttu-id="535c2-321">Como buena práctica general, asegúrese de que está usando la versión más reciente.</span><span class="sxs-lookup"><span data-stu-id="535c2-321">As good general practice, make sure that you use the latest version.</span></span> <span data-ttu-id="535c2-322">Si no ha actualizado la puerta de enlace durante un mes o más, debería plantearse instalar su versión más reciente y comprobar si puede reproducir el problema.</span><span class="sxs-lookup"><span data-stu-id="535c2-322">If you haven't updated the gateway for a month or longer, you might consider installing the latest version of the gateway, and see if you can reproduce the issue.</span></span>

### <a name="error-failed-to-add-user-to-group--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="535c2-323">Error: Error al agregar el usuario al grupo.</span><span class="sxs-lookup"><span data-stu-id="535c2-323">Error: Failed to add user to group.</span></span> <span data-ttu-id="535c2-324">(Usuarios del registro de rendimiento de-2147463168 PBIEgwService)</span><span class="sxs-lookup"><span data-stu-id="535c2-324">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="535c2-325">Es posible que reciba este error si intenta instalar la puerta de enlace en un controlador de dominio, lo cual no se admite.</span><span class="sxs-lookup"><span data-stu-id="535c2-325">You might get this error if you try to install the gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="535c2-326">Asegúrese de implementar la puerta de enlace en una máquina que no sea un controlador de dominio.</span><span class="sxs-lookup"><span data-stu-id="535c2-326">Make sure that you deploy the gateway on a machine that isn't a domain controller.</span></span>

## <a name="tools"></a><span data-ttu-id="535c2-327">Herramientas</span><span class="sxs-lookup"><span data-stu-id="535c2-327">Tools</span></span>

### <a name="collect-logs-from-the-gateway-configurer"></a><span data-ttu-id="535c2-328">Recopilación de registros desde el configurador de la puerta de enlace</span><span class="sxs-lookup"><span data-stu-id="535c2-328">Collect logs from the gateway configurer</span></span>

<span data-ttu-id="535c2-329">Puede recopilar varios registros de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="535c2-329">You can collect several logs for the gateway.</span></span> <span data-ttu-id="535c2-330">¡Empiece siempre por los registros!</span><span class="sxs-lookup"><span data-stu-id="535c2-330">Always start with the logs!</span></span>

#### <a name="installer-logs"></a><span data-ttu-id="535c2-331">Registros del instalador</span><span class="sxs-lookup"><span data-stu-id="535c2-331">Installer logs</span></span>

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a><span data-ttu-id="535c2-332">Registros de configuración</span><span class="sxs-lookup"><span data-stu-id="535c2-332">Configuration logs</span></span>

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="535c2-333">Registros del servicio de puerta de enlace empresarial</span><span class="sxs-lookup"><span data-stu-id="535c2-333">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a><span data-ttu-id="535c2-334">Registros de eventos</span><span class="sxs-lookup"><span data-stu-id="535c2-334">Event logs</span></span>

<span data-ttu-id="535c2-335">Puede encontrar los registros de Data Management Gateway y PowerBIGateway en **Registros de aplicaciones y servicios**.</span><span class="sxs-lookup"><span data-stu-id="535c2-335">You can find the Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>

### <a name="fiddler-trace"></a><span data-ttu-id="535c2-336">Seguimiento de Fiddler</span><span class="sxs-lookup"><span data-stu-id="535c2-336">Fiddler Trace</span></span>

<span data-ttu-id="535c2-337">[Fiddler](http://www.telerik.com/fiddler) es una herramienta gratuita de Telerik que supervisa el tráfico HTTP.</span><span class="sxs-lookup"><span data-stu-id="535c2-337">[Fiddler](http://www.telerik.com/fiddler) is a free tool from Telerik that monitors HTTP traffic.</span></span> <span data-ttu-id="535c2-338">Puede ver este tráfico con el servicio Power BI desde la máquina cliente.</span><span class="sxs-lookup"><span data-stu-id="535c2-338">You can see this traffic with the Power BI service from the client machine.</span></span> <span data-ttu-id="535c2-339">Este servicio puede mostrar errores y otra información relacionada.</span><span class="sxs-lookup"><span data-stu-id="535c2-339">This service might show errors and other related information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="535c2-340">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="535c2-340">Next steps</span></span>
    
* [<span data-ttu-id="535c2-341">Conexión a datos locales desde aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="535c2-341">Connect to on-premises data from logic apps</span></span>](../logic-apps/logic-apps-gateway-connection.md)
* [<span data-ttu-id="535c2-342">Características de Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="535c2-342">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="535c2-343">Conectores para Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="535c2-343">Connectors for Azure Logic Apps</span></span>](../connectors/apis-list.md)
