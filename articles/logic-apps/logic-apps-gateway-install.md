---
title: puerta de enlace de aaaInstall local datos - Azure Logic Apps | Documentos de Microsoft
description: "Antes de acceder a orígenes de datos de forma local, instalar la puerta de enlace de datos de hello en local para la transferencia de datos rápidamente y cifrado entre los orígenes de datos de forma local y las aplicaciones lógicas"
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
ms.openlocfilehash: 01386a904d856ff545f2eca8eb1b008dcdc08574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-on-premises-data-gateway-for-azure-logic-apps"></a><span data-ttu-id="dd34e-104">Hola de instalación local puerta de enlace de datos para las aplicaciones lógicas de Azure</span><span class="sxs-lookup"><span data-stu-id="dd34e-104">Install hello on-premises data gateway for Azure Logic Apps</span></span>

<span data-ttu-id="dd34e-105">Antes de que las aplicaciones lógicas pueden tener acceso a orígenes de datos de forma local, debe instalar y configurar la puerta de enlace de datos de hello en local.</span><span class="sxs-lookup"><span data-stu-id="dd34e-105">Before your logic apps can access data sources on premises, you must install and set up hello on-premises data gateway.</span></span> <span data-ttu-id="dd34e-106">puerta de enlace de Hello actúa como un puente que permite el cifrado entre los sistemas locales y las aplicaciones lógicas y transferencia de datos rápidamente.</span><span class="sxs-lookup"><span data-stu-id="dd34e-106">hello gateway acts as a bridge that provides quick data transfer and encryption between on-premises systems and your logic apps.</span></span> <span data-ttu-id="dd34e-107">puerta de enlace de Hello transmite datos desde orígenes locales en los canales cifrados a través de hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="dd34e-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="dd34e-108">Todo el tráfico se origina como proteger el tráfico saliente desde el agente de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd34e-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="dd34e-109">Obtenga más información sobre [cómo funciona la puerta de enlace de datos de hello](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="dd34e-109">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

<span data-ttu-id="dd34e-110">puerta de enlace de Hello es compatible con orígenes de datos de las conexiones toothese local:</span><span class="sxs-lookup"><span data-stu-id="dd34e-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="dd34e-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="dd34e-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="dd34e-112">DB2</span><span class="sxs-lookup"><span data-stu-id="dd34e-112">DB2</span></span>  
*   <span data-ttu-id="dd34e-113">Sistema de archivos</span><span class="sxs-lookup"><span data-stu-id="dd34e-113">File System</span></span>
*   <span data-ttu-id="dd34e-114">Informix</span><span class="sxs-lookup"><span data-stu-id="dd34e-114">Informix</span></span>
*   <span data-ttu-id="dd34e-115">MQ</span><span class="sxs-lookup"><span data-stu-id="dd34e-115">MQ</span></span>
*   <span data-ttu-id="dd34e-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="dd34e-116">MySQL</span></span>
*   <span data-ttu-id="dd34e-117">Base de datos de Oracle</span><span class="sxs-lookup"><span data-stu-id="dd34e-117">Oracle Database</span></span>
*   <span data-ttu-id="dd34e-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="dd34e-118">PostgreSQL</span></span>
*   <span data-ttu-id="dd34e-119">Servidor de aplicaciones de SAP</span><span class="sxs-lookup"><span data-stu-id="dd34e-119">SAP Application Server</span></span> 
*   <span data-ttu-id="dd34e-120">Servidor de mensajes de SAP</span><span class="sxs-lookup"><span data-stu-id="dd34e-120">SAP Message Server</span></span>
*   <span data-ttu-id="dd34e-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="dd34e-121">SharePoint</span></span>
*   <span data-ttu-id="dd34e-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="dd34e-122">SQL Server</span></span>
*   <span data-ttu-id="dd34e-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="dd34e-123">Teradata</span></span>

<span data-ttu-id="dd34e-124">Estos pasos muestra cómo toofirst instalación Hola local puerta de enlace de datos antes de [establecer una conexión entre la puerta de enlace de Hola y las aplicaciones lógicas](./logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="dd34e-124">These steps show how toofirst install hello on-premises data gateway before you [set up a connection between hello gateway and your logic apps](./logic-apps-gateway-connection.md).</span></span> <span data-ttu-id="dd34e-125">Para obtener más información sobre las conexiones admitidas, consulte [Conectores para Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="dd34e-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span> 

<span data-ttu-id="dd34e-126">Para obtener información acerca de cómo toouse Hola puerta de enlace con otros servicios, vea estos artículos:</span><span class="sxs-lookup"><span data-stu-id="dd34e-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="dd34e-127">Puerta de enlace de datos local de Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="dd34e-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="dd34e-128">Puerta de enlace de datos local de Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="dd34e-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="dd34e-129">Puerta de enlace de datos local de Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="dd34e-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="dd34e-130">Administración de una puerta de enlace de datos local en Microsoft PowerApps</span><span class="sxs-lookup"><span data-stu-id="dd34e-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a><span data-ttu-id="dd34e-131">Requisitos</span><span class="sxs-lookup"><span data-stu-id="dd34e-131">Requirements</span></span>

<span data-ttu-id="dd34e-132">**Mínimos**:</span><span class="sxs-lookup"><span data-stu-id="dd34e-132">**Minimum**:</span></span>

* <span data-ttu-id="dd34e-133">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="dd34e-133">.NET 4.5 Framework</span></span>
* <span data-ttu-id="dd34e-134">versión de 64 bits de Windows 7 o Windows Server 2008 R2 (o posterior)</span><span class="sxs-lookup"><span data-stu-id="dd34e-134">64-bit version of Windows 7 or Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="dd34e-135">**Recomendaciones**:</span><span class="sxs-lookup"><span data-stu-id="dd34e-135">**Recommended**:</span></span>

* <span data-ttu-id="dd34e-136">CPU de 8 núcleos</span><span class="sxs-lookup"><span data-stu-id="dd34e-136">8 Core CPU</span></span>
* <span data-ttu-id="dd34e-137">8 GB de memoria</span><span class="sxs-lookup"><span data-stu-id="dd34e-137">8 GB Memory</span></span>
* <span data-ttu-id="dd34e-138">versión de 64 bits de Windows 2012 R2 (o posterior)</span><span class="sxs-lookup"><span data-stu-id="dd34e-138">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="dd34e-139">**Consideraciones importantes**:</span><span class="sxs-lookup"><span data-stu-id="dd34e-139">**Important considerations**:</span></span>

* <span data-ttu-id="dd34e-140">Hola de instalación local de puerta de enlace de datos solo en un equipo local.</span><span class="sxs-lookup"><span data-stu-id="dd34e-140">Install hello on-premises data gateway only on a local computer.</span></span>
<span data-ttu-id="dd34e-141">No se puede instalar la puerta de enlace de hello en un controlador de dominio.</span><span class="sxs-lookup"><span data-stu-id="dd34e-141">You can't install hello gateway on a domain controller.</span></span>

   > [!TIP]
   > <span data-ttu-id="dd34e-142">No tiene puerta de enlace de tooinstall hello en hello mismo equipo que el origen de datos.</span><span class="sxs-lookup"><span data-stu-id="dd34e-142">You don't have tooinstall hello gateway on hello same computer as your data source.</span></span> <span data-ttu-id="dd34e-143">latencia de toominimize, puede instalar puerta de enlace de hello más próximo como origen de datos de tooyour posible, o en hello mismo equipo, suponiendo que tenga permisos.</span><span class="sxs-lookup"><span data-stu-id="dd34e-143">toominimize latency, you can install hello gateway as close as possible tooyour data source, or on hello same computer, assuming that you have permissions.</span></span>

* <span data-ttu-id="dd34e-144">No instale la puerta de enlace de hello en un equipo que se desactiva, deja de toosleep o no se conecta toohello Internet porque no se puede ejecutar la puerta de enlace de hello en esas circunstancias.</span><span class="sxs-lookup"><span data-stu-id="dd34e-144">Don't install hello gateway on a computer that turns off, goes toosleep, or doesn't connect toohello Internet because hello gateway can't run under those circumstances.</span></span> <span data-ttu-id="dd34e-145">Además, el rendimiento de la puerta de enlace podría verse afectado en una red inalámbrica.</span><span class="sxs-lookup"><span data-stu-id="dd34e-145">Also, gateway performance might suffer over a wireless network.</span></span>

* <span data-ttu-id="dd34e-146">Durante la instalación, debe iniciar sesión con una [cuenta profesional o educativa](https://docs.microsoft.com/azure/active-directory/sign-up-organization) que está administrada por Azure Active Directory (Azure AD), no una cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dd34e-146">During installation, you must sign in with a [work or school account](https://docs.microsoft.com/azure/active-directory/sign-up-organization) that's managed by Azure Active Directory (Azure AD), not a Microsoft account.</span></span> 

  <span data-ttu-id="dd34e-147">Tiene toouse Hola mismo trabajo o escuela hello más tarde en Azure de cuenta portal al crear y asociar un recurso de puerta de enlace con la instalación de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="dd34e-147">You have toouse hello same work or school account later in hello Azure portal when you create and associate a gateway resource with your gateway installation.</span></span> <span data-ttu-id="dd34e-148">A continuación, seleccione este recurso de puerta de enlace al crear conexión Hola entre el origen de datos lógica hello y aplicaciones locales.</span><span class="sxs-lookup"><span data-stu-id="dd34e-148">You then select this gateway resource when you create hello connection between your logic app and hello on-premises data source.</span></span> [<span data-ttu-id="dd34e-149">¿Por qué debo usar una cuenta profesional o educativa de Azure AD?</span><span class="sxs-lookup"><span data-stu-id="dd34e-149">Why must I use an Azure AD work or school account?</span></span>](#why-azure-work-school-account)

  > [!TIP]
  > <span data-ttu-id="dd34e-150">Si se suscribió a una oferta de Office 365 y no proporcionó su correo electrónico profesional real, la dirección de inicio de sesión podría tener un aspecto similar al siguiente: jeff@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="dd34e-150">If you signed up for an Office 365 offering and didn't supply your actual work email, your sign-in address might look like jeff@contoso.onmicrosoft.com.</span></span> 

* <span data-ttu-id="dd34e-151">Si tiene una puerta de enlace existente que configura con un instalador que es anterior a la versión 14.16.6317.4, no se puede cambiar la ubicación de la puerta de enlace Installer más reciente de ejecución Hola.</span><span class="sxs-lookup"><span data-stu-id="dd34e-151">If you have an existing gateway that you set up with an installer that's earlier than version 14.16.6317.4, you can't change your gateway's location by running hello latest installer.</span></span> <span data-ttu-id="dd34e-152">Sin embargo, puede usar hello más reciente instalador tooset una nueva puerta de enlace con la ubicación de Hola que desea en su lugar.</span><span class="sxs-lookup"><span data-stu-id="dd34e-152">However, you can use hello latest installer tooset up a new gateway with hello location that you want instead.</span></span>
  
  <span data-ttu-id="dd34e-153">Si tiene un instalador de puerta de enlace que es anterior a la versión 14.16.6317.4, pero no ha instalado la puerta de enlace, puede descargar y utilice el instalador de hello más reciente.</span><span class="sxs-lookup"><span data-stu-id="dd34e-153">If you have a gateway installer that's earlier than version 14.16.6317.4, but you haven't installed your gateway yet, you can download and use hello latest installer.</span></span>

<a name="install-gateway"></a>

## <a name="install-hello-data-gateway"></a><span data-ttu-id="dd34e-154">Instalar la puerta de enlace de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="dd34e-154">Install hello data gateway</span></span>

1.  <span data-ttu-id="dd34e-155">[Descargue y ejecute el instalador de puerta de enlace de hello en un equipo local](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="dd34e-155">[Download and run hello gateway installer on a local computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span></span>

2. <span data-ttu-id="dd34e-156">Revise y acepte los términos de Hola de uso y declaración de privacidad.</span><span class="sxs-lookup"><span data-stu-id="dd34e-156">Review and accept hello terms of use and privacy statement.</span></span>

3. <span data-ttu-id="dd34e-157">Especifique la ruta de acceso de hello en el equipo local donde desea que la puerta de enlace de tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="dd34e-157">Specify hello path on your local computer where you want tooinstall hello gateway.</span></span>

4. <span data-ttu-id="dd34e-158">Cuando se le solicite, inicie sesión con su cuenta profesional o educativa de Azure, no con una cuenta de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="dd34e-158">When prompted, sign in with your Azure work or school account, not a Microsoft account.</span></span>

   ![Inicio de sesión con una cuenta profesional o educativa de Azure](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. <span data-ttu-id="dd34e-160">Registrar la puerta de enlace instalada con hello [servicio de nube de puerta de enlace](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="dd34e-160">Now register your installed gateway with hello [gateway cloud service](#gateway-cloud-service).</span></span> <span data-ttu-id="dd34e-161">Elija **Registrar una nueva puerta de enlace en este equipo**.</span><span class="sxs-lookup"><span data-stu-id="dd34e-161">Choose **Register a new gateway on this computer**.</span></span>

   <span data-ttu-id="dd34e-162">servicio de nube de puerta de enlace de Hello cifra y almacena sus credenciales de origen de datos y los detalles de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="dd34e-162">hello gateway cloud service encrypts and stores your data source credentials and gateway details.</span></span> 
   <span data-ttu-id="dd34e-163">servicio de Hello también enruta las consultas y los resultados entre la aplicación lógica, puerta de enlace de datos de hello en local y el origen de datos de forma local.</span><span class="sxs-lookup"><span data-stu-id="dd34e-163">hello service also routes queries and their results between your logic app, hello on-premises data gateway, and your data source on premises.</span></span>

6. <span data-ttu-id="dd34e-164">Especifique un nombre para la instalación de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="dd34e-164">Provide a name for your gateway installation.</span></span> <span data-ttu-id="dd34e-165">Cree una clave de recuperación y luego confírmela.</span><span class="sxs-lookup"><span data-stu-id="dd34e-165">Create a recovery key, then confirm your recovery key.</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="dd34e-166">La clave de recuperación debe contener al menos ocho caracteres.</span><span class="sxs-lookup"><span data-stu-id="dd34e-166">Your recovery key must contain at least eight characters.</span></span> <span data-ttu-id="dd34e-167">Asegúrese de guardar y mantenga la clave de hello en un lugar seguro.</span><span class="sxs-lookup"><span data-stu-id="dd34e-167">Make sure that you save and keep hello key in a safe place.</span></span> <span data-ttu-id="dd34e-168">También necesitará esta clave cuando se desea toomigrate, restaurar o tomar a través de una puerta de enlace existente.</span><span class="sxs-lookup"><span data-stu-id="dd34e-168">You also need this key when you want toomigrate, restore, or take over an existing gateway.</span></span>

   1. <span data-ttu-id="dd34e-169">Elija la región de toochange Hola predeterminados para el servicio de nube de puerta de enlace de Hola y utilizados por la instalación de puerta de enlace, Service Bus de Azure **cambiar región**.</span><span class="sxs-lookup"><span data-stu-id="dd34e-169">toochange hello default region for hello gateway cloud service and Azure Service Bus used by your gateway installation, choose **Change Region**.</span></span>

      ![Cambio de región](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      <span data-ttu-id="dd34e-171">Hola predeterminado Hola región está asociado con el inquilino de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="dd34e-171">hello default region is hello region associated with your Azure AD tenant.</span></span>

   2. <span data-ttu-id="dd34e-172">En el siguiente panel hello, abra hello **Seleccionar región** demasiado elija una región diferente.</span><span class="sxs-lookup"><span data-stu-id="dd34e-172">On hello next pane, open hello **Select Region** too choose a different region.</span></span>

      ![Seleccione otra región.](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      <span data-ttu-id="dd34e-174">Por ejemplo, podría seleccionar Hola misma región que la aplicación lógica o, por lo que puede reducir la latencia del origen de datos de local de hello seleccione región más cercanas tooyour.</span><span class="sxs-lookup"><span data-stu-id="dd34e-174">For example, you might select hello same region as your logic app, or select hello region closest tooyour on-premises data source so you can reduce latency.</span></span> <span data-ttu-id="dd34e-175">El recurso de puerta de enlace y la aplicación lógica pueden tener ubicaciones distintas.</span><span class="sxs-lookup"><span data-stu-id="dd34e-175">Your gateway resource and logic app can have different locations.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="dd34e-176">No puede cambiar esta región después de la instalación.</span><span class="sxs-lookup"><span data-stu-id="dd34e-176">You can't change this region after installation.</span></span> <span data-ttu-id="dd34e-177">Esta región también determina y restringe la ubicación de Hola donde puede crear Hola recursos de Azure para la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="dd34e-177">This region also determines and restricts hello location where you can create hello Azure resource for your gateway.</span></span> <span data-ttu-id="dd34e-178">Por lo que cuando se crea el recurso de puerta de enlace de Azure, asegúrese de que ubicación del recurso Hola coincide con región Hola que seleccionó durante la instalación de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="dd34e-178">So when you create your gateway resource in Azure, make sure that hello resource location matches hello region that you selected during gateway installation.</span></span>
      > 
      > <span data-ttu-id="dd34e-179">Si desea toouse una región distinta para la puerta de enlace más adelante, debe configurar una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="dd34e-179">If you want toouse a different region for your gateway later, you must set up a new gateway.</span></span>

   3. <span data-ttu-id="dd34e-180">Cuando esté listo, elija **Hecho**.</span><span class="sxs-lookup"><span data-stu-id="dd34e-180">When you're ready, choose **Done**.</span></span>

7. <span data-ttu-id="dd34e-181">Ahora siga estos pasos en hello portal de Azure para que pueda [crear un recurso de Azure para la puerta de enlace](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="dd34e-181">Now follow these steps in hello Azure portal so you can [create an Azure resource for your gateway](../logic-apps/logic-apps-gateway-connection.md).</span></span> 

<span data-ttu-id="dd34e-182">Obtenga más información sobre [cómo funciona la puerta de enlace de datos de hello](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="dd34e-182">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a><span data-ttu-id="dd34e-183">Migrar, restaurar o controlar una puerta de enlace existente</span><span class="sxs-lookup"><span data-stu-id="dd34e-183">Migrate, restore, or take over an existing gateway</span></span>

<span data-ttu-id="dd34e-184">tooperform estas tareas, debe tener la clave de recuperación de Hola que se especificó cuando se instaló la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd34e-184">tooperform these tasks, you must have hello recovery key that was specified when hello gateway was installed.</span></span>

1. <span data-ttu-id="dd34e-185">En el menú Inicio del equipo, elija **Puerta de enlace de datos locales**.</span><span class="sxs-lookup"><span data-stu-id="dd34e-185">From your computer's Start menu, choose **On-premises data gateway**.</span></span>

2. <span data-ttu-id="dd34e-186">Después de hello instalador se abre, inicie sesión con hello mismo Azure trabajar o cuenta organizativa que antes eran usa puerta de enlace de tooinstall Hola.</span><span class="sxs-lookup"><span data-stu-id="dd34e-186">After hello installer opens, sign in with hello same Azure work or school account that was previously used tooinstall hello gateway.</span></span>

3. <span data-ttu-id="dd34e-187">Elija **Migrar, restaurar o controlar una puerta de enlace existente**.</span><span class="sxs-lookup"><span data-stu-id="dd34e-187">Choose **Migrate, restore, or take over an existing gateway**.</span></span>

4. <span data-ttu-id="dd34e-188">Proporcione la clave de nombre y la recuperación de Hola para puerta de enlace de Hola que desee toomigrate, restaurar o sustituir sobre.</span><span class="sxs-lookup"><span data-stu-id="dd34e-188">Provide hello name and recovery key for hello gateway that you want toomigrate, restore, or take over.</span></span>

<a name="restart-gateway"></a>
## <a name="restart-hello-gateway"></a><span data-ttu-id="dd34e-189">Reinicie la puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="dd34e-189">Restart hello gateway</span></span>

<span data-ttu-id="dd34e-190">puerta de enlace de Hola se ejecuta como un servicio de Windows.</span><span class="sxs-lookup"><span data-stu-id="dd34e-190">hello gateway runs as a Windows service.</span></span> <span data-ttu-id="dd34e-191">Como cualquier otro servicio de Windows, puede iniciar y detener servicio Hola de varias maneras.</span><span class="sxs-lookup"><span data-stu-id="dd34e-191">Like any other Windows service, you can start and stop hello service in multiple ways.</span></span> <span data-ttu-id="dd34e-192">Por ejemplo, puede abrir un símbolo del sistema con permisos elevados en el equipo de Hola donde se ejecuta la puerta de enlace de Hola y ejecutar cualquiera de estos comandos:</span><span class="sxs-lookup"><span data-stu-id="dd34e-192">For example, you can open a command prompt with elevated permissions on hello computer where hello gateway is running, and run either these commands:</span></span>

* <span data-ttu-id="dd34e-193">servicio de hello toostop, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="dd34e-193">toostop hello service, run this command:</span></span>
  
    `net stop PBIEgwService`

* <span data-ttu-id="dd34e-194">servicio de hello toostart, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="dd34e-194">toostart hello service, run this command:</span></span>
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a><span data-ttu-id="dd34e-195">Cuenta de servicio de Windows</span><span class="sxs-lookup"><span data-stu-id="dd34e-195">Windows service account</span></span>

<span data-ttu-id="dd34e-196">puerta de enlace de datos de Hello local se configura toouse `NT SERVICE\PBIEgwService` para Windows hello credenciales de inicio de sesión del servicio.</span><span class="sxs-lookup"><span data-stu-id="dd34e-196">hello on-premises data gateway is set up toouse `NT SERVICE\PBIEgwService` for hello Windows service logon credentials.</span></span> <span data-ttu-id="dd34e-197">De forma predeterminada, puerta de enlace de hello tiene "Hola iniciar sesión como servicio" directamente para la máquina de Hola donde se instala la puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd34e-197">By default, hello gateway has hello "Log on as a service" right for hello machine where you install hello gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="dd34e-198">Hola cuenta de servicio de Windows difiere de cuenta de hello usada para conectarse a orígenes de datos locales de tooon y de hello Azure trabajo o cuenta organizativa utiliza toosign en servicios de toocloud.</span><span class="sxs-lookup"><span data-stu-id="dd34e-198">hello Windows service account differs from hello account used for connecting tooon-premises data sources, and from hello Azure work or school account used toosign in toocloud services.</span></span>

## <a name="configure-a-firewall-or-proxy"></a><span data-ttu-id="dd34e-199">Configuración de un firewall o proxy</span><span class="sxs-lookup"><span data-stu-id="dd34e-199">Configure a firewall or proxy</span></span>

<span data-ttu-id="dd34e-200">puerta de enlace de Hello crea una conexión de salida demasiado [Service Bus de Azure](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="dd34e-200">hello gateway creates an outbound connection too [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="dd34e-201">información de proxy de tooprovide para la puerta de enlace, consulte [configurar el proxy](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span><span class="sxs-lookup"><span data-stu-id="dd34e-201">tooprovide proxy information for your gateway, see [Configure proxy settings](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span></span>

<span data-ttu-id="dd34e-202">toocheck si el firewall o proxy, puede bloquear las conexiones, confirmar si su equipo puede conectar realmente toohello hello y internet [Service Bus de Azure](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="dd34e-202">toocheck whether your firewall, or proxy, might block connections, confirm whether your machine can actually connect toohello internet and hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="dd34e-203">Desde un símbolo del sistema de PowerShell, ejecute este comando:</span><span class="sxs-lookup"><span data-stu-id="dd34e-203">From a PowerShell prompt, run this command:</span></span>

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> <span data-ttu-id="dd34e-204">Este comando sólo comprueba la conectividad de red y conectividad toohello Service Bus de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd34e-204">This command only tests network connectivity and connectivity toohello Azure Service Bus.</span></span> <span data-ttu-id="dd34e-205">Por lo que el comando hello no tiene nada toodo con puerta de enlace de Hola o un servicio de nube de puerta de enlace de Hola que cifra y almacena sus credenciales y detalles de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="dd34e-205">So hello command doesn't have anything toodo with hello gateway or hello gateway cloud service that encrypts and stores your credentials and gateway details.</span></span> 
>
> <span data-ttu-id="dd34e-206">Además, este comando solo está disponible en Windows Server 2012 R2 o posterior y Windows 8.1 o posterior.</span><span class="sxs-lookup"><span data-stu-id="dd34e-206">Also, this command is only available on Windows Server 2012 R2 or later, and Windows 8.1 or later.</span></span> <span data-ttu-id="dd34e-207">En versiones anteriores del sistema operativo, puede usar Telnet demasiado probar la conectividad.</span><span class="sxs-lookup"><span data-stu-id="dd34e-207">On earlier OS versions, you can use Telnet too test connectivity.</span></span> <span data-ttu-id="dd34e-208">Obtenga más información sobre [Azure Service Bus y soluciones híbridas](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="dd34e-208">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

<span data-ttu-id="dd34e-209">Los resultados deberían ser ejemplo toothis similar:</span><span class="sxs-lookup"><span data-stu-id="dd34e-209">Your results should look similar toothis example:</span></span>

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

<span data-ttu-id="dd34e-210">Si **TcpTestSucceeded** no está establecido demasiado**True**, puede estar bloqueado por un firewall.</span><span class="sxs-lookup"><span data-stu-id="dd34e-210">If **TcpTestSucceeded** is not set too**True**, you might be blocked by a firewall.</span></span> <span data-ttu-id="dd34e-211">Si lo desea, toobe completa, sustituir hello **ComputerName** y **puerto** valores con valores de hello aparecen bajo [configurar puertos](#configure-ports) en este tema.</span><span class="sxs-lookup"><span data-stu-id="dd34e-211">If you want toobe comprehensive, substitute hello **ComputerName** and **Port** values with hello values listed under [Configure ports](#configure-ports) in this topic.</span></span>

<span data-ttu-id="dd34e-212">firewall de Hello también podría bloquear las conexiones que Hola que Service Bus de Azure hace toohello centros de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd34e-212">hello firewall might also block connections that hello Azure Service Bus makes toohello Azure datacenters.</span></span> <span data-ttu-id="dd34e-213">Si se produce esta situación, aprobar (desbloquear) todas Hola direcciones IP para esos centros de datos en su región.</span><span class="sxs-lookup"><span data-stu-id="dd34e-213">If this scenario happens, approve (unblock) all hello IP addresses for those datacenters in your region.</span></span> <span data-ttu-id="dd34e-214">Para esas direcciones IP, [lista de direcciones aquí de get hello Azure IP](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="dd34e-214">For those IP addresses, [get hello Azure IP addresses list here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

## <a name="configure-ports"></a><span data-ttu-id="dd34e-215">Configuración de los puertos</span><span class="sxs-lookup"><span data-stu-id="dd34e-215">Configure ports</span></span>

<span data-ttu-id="dd34e-216">puerta de enlace de Hello crea una conexión de salida demasiado[Service Bus de Azure](https://azure.microsoft.com/services/service-bus/) y se comunica en los puertos de salida: TCP 443 (valor predeterminado), 5671, 5672 y 9350 a 9354.</span><span class="sxs-lookup"><span data-stu-id="dd34e-216">hello gateway creates an outbound connection too[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) and communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span> <span data-ttu-id="dd34e-217">puerta de enlace de Hello no requiere puertos de entrada.</span><span class="sxs-lookup"><span data-stu-id="dd34e-217">hello gateway doesn't require inbound ports.</span></span> <span data-ttu-id="dd34e-218">Obtenga más información sobre [Azure Service Bus y soluciones híbridas](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="dd34e-218">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

| <span data-ttu-id="dd34e-219">NOMBRES DE DOMINIO</span><span class="sxs-lookup"><span data-stu-id="dd34e-219">DOMAIN NAMES</span></span> | <span data-ttu-id="dd34e-220">PUERTOS DE SALIDA</span><span class="sxs-lookup"><span data-stu-id="dd34e-220">OUTBOUND PORTS</span></span> | <span data-ttu-id="dd34e-221">DESCRIPCIÓN</span><span class="sxs-lookup"><span data-stu-id="dd34e-221">DESCRIPTION</span></span> |
| --- | --- | --- |
| <span data-ttu-id="dd34e-222">*. analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="dd34e-222">*.analysis.windows.net</span></span> | <span data-ttu-id="dd34e-223">443</span><span class="sxs-lookup"><span data-stu-id="dd34e-223">443</span></span> | <span data-ttu-id="dd34e-224">HTTPS</span><span class="sxs-lookup"><span data-stu-id="dd34e-224">HTTPS</span></span> | 
| <span data-ttu-id="dd34e-225">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="dd34e-225">*.login.windows.net</span></span> | <span data-ttu-id="dd34e-226">443</span><span class="sxs-lookup"><span data-stu-id="dd34e-226">443</span></span> | <span data-ttu-id="dd34e-227">HTTPS</span><span class="sxs-lookup"><span data-stu-id="dd34e-227">HTTPS</span></span> | 
| <span data-ttu-id="dd34e-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="dd34e-228">*.servicebus.windows.net</span></span> | <span data-ttu-id="dd34e-229">5671-5672</span><span class="sxs-lookup"><span data-stu-id="dd34e-229">5671-5672</span></span> | <span data-ttu-id="dd34e-230">Advanced Message Queuing Protocol (AMQP)</span><span class="sxs-lookup"><span data-stu-id="dd34e-230">Advanced Message Queuing Protocol (AMQP)</span></span> | 
| <span data-ttu-id="dd34e-231">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="dd34e-231">*.servicebus.windows.net</span></span> | <span data-ttu-id="dd34e-232">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="dd34e-232">443, 9350-9354</span></span> | <span data-ttu-id="dd34e-233">Agentes de escucha en Service Bus Relay sobre TCP (requiere 443 para la adquisición del token de Access Control)</span><span class="sxs-lookup"><span data-stu-id="dd34e-233">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> | 
| <span data-ttu-id="dd34e-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="dd34e-234">*.frontend.clouddatahub.net</span></span> | <span data-ttu-id="dd34e-235">443</span><span class="sxs-lookup"><span data-stu-id="dd34e-235">443</span></span> | <span data-ttu-id="dd34e-236">HTTPS</span><span class="sxs-lookup"><span data-stu-id="dd34e-236">HTTPS</span></span> | 
| <span data-ttu-id="dd34e-237">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="dd34e-237">*.core.windows.net</span></span> | <span data-ttu-id="dd34e-238">443</span><span class="sxs-lookup"><span data-stu-id="dd34e-238">443</span></span> | <span data-ttu-id="dd34e-239">HTTPS</span><span class="sxs-lookup"><span data-stu-id="dd34e-239">HTTPS</span></span> | 
| <span data-ttu-id="dd34e-240">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="dd34e-240">login.microsoftonline.com</span></span> | <span data-ttu-id="dd34e-241">443</span><span class="sxs-lookup"><span data-stu-id="dd34e-241">443</span></span> | <span data-ttu-id="dd34e-242">HTTPS</span><span class="sxs-lookup"><span data-stu-id="dd34e-242">HTTPS</span></span> | 
| <span data-ttu-id="dd34e-243">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="dd34e-243">*.msftncsi.com</span></span> | <span data-ttu-id="dd34e-244">443</span><span class="sxs-lookup"><span data-stu-id="dd34e-244">443</span></span> | <span data-ttu-id="dd34e-245">Usar tootest conectividad a internet cuando puerta de enlace de hello es inaccesible por hello servicio Power BI.</span><span class="sxs-lookup"><span data-stu-id="dd34e-245">Used tootest internet connectivity when hello gateway is unreachable by hello Power BI service.</span></span> | 

<span data-ttu-id="dd34e-246">Si tiene direcciones IP de tooapprove en lugar de dominios de hello, puede descargar y usar hello [lista de intervalos de direcciones IP de centro de datos de Azure de Microsoft](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="dd34e-246">If you have tooapprove IP addresses instead of hello domains, you can download and use hello [Microsoft Azure Datacenter IP ranges list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="dd34e-247">En algunos casos, las conexiones de Bus de servicio de Azure de Hola se realizan con la dirección IP en lugar de nombres de dominio completo.</span><span class="sxs-lookup"><span data-stu-id="dd34e-247">In some cases, hello Azure Service Bus connections are made with IP Address rather than fully qualified domain names.</span></span>

<a name="gateway-cloud-service"></a>
## <a name="how-does-hello-data-gateway-work"></a><span data-ttu-id="dd34e-248">¿Cómo funciona la puerta de enlace de datos de hello?</span><span class="sxs-lookup"><span data-stu-id="dd34e-248">How does hello data gateway work?</span></span>

<span data-ttu-id="dd34e-249">puerta de enlace de datos de Hello facilita la comunicación rápida y segura entre la lógica de aplicación, servicio de nube de puerta de enlace de Hola y el origen de datos local.</span><span class="sxs-lookup"><span data-stu-id="dd34e-249">hello data gateway facilitates quick and secure communication between your logic app, hello gateway cloud service, and your on-premises data source.</span></span> 

![diagram-for-on-premises-data-gateway-flow](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

<span data-ttu-id="dd34e-251">Por lo que cuando el usuario hello en la nube de hello interactúa con un elemento que se ha conectado tooyour local de origen de datos:</span><span class="sxs-lookup"><span data-stu-id="dd34e-251">So when hello user in hello cloud interacts with an element that's connected tooyour on-premises data source:</span></span>

1. <span data-ttu-id="dd34e-252">servicio de nube de puerta de enlace de Hola crea una consulta, junto con las credenciales de hello cifrada para el origen de datos de hello y envía la cola de toohello de consulta de Hola para hello tooprocess de puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="dd34e-252">hello gateway cloud service creates a query, along with hello encrypted credentials for hello data source, and sends hello query toohello queue for hello gateway tooprocess.</span></span>

2. <span data-ttu-id="dd34e-253">servicio de nube de puerta de enlace de Hello analiza la consulta de Hola e inserta Hola solicitud toohello Service Bus de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd34e-253">hello gateway cloud service analyzes hello query and pushes hello request toohello Azure Service Bus.</span></span>

3. <span data-ttu-id="dd34e-254">puerta de enlace de datos de Hello local sondea hello Azure Service Bus para las solicitudes pendientes.</span><span class="sxs-lookup"><span data-stu-id="dd34e-254">hello on-premises data gateway polls hello Azure Service Bus for pending requests.</span></span>

4. <span data-ttu-id="dd34e-255">puerta de enlace de Hello obtiene Hola consulta, descifra las credenciales de Hola y conecta el origen de datos de toohello con esas credenciales.</span><span class="sxs-lookup"><span data-stu-id="dd34e-255">hello gateway gets hello query, decrypts hello credentials, and connects toohello data source with those credentials.</span></span>

5. <span data-ttu-id="dd34e-256">puerta de enlace de Hello envía Hola consultar toohello origen de datos para su ejecución.</span><span class="sxs-lookup"><span data-stu-id="dd34e-256">hello gateway sends hello query toohello data source for execution.</span></span>

6. <span data-ttu-id="dd34e-257">resultados de Hola se envían desde el origen de datos de hello, puerta de enlace de toohello atrás y, a continuación, servicio de nube de puerta de enlace de toohello.</span><span class="sxs-lookup"><span data-stu-id="dd34e-257">hello results are sent from hello data source, back toohello gateway, and then toohello gateway cloud service.</span></span> <span data-ttu-id="dd34e-258">Hello servicio de nube de puerta de enlace, a continuación, usa los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd34e-258">hello gateway cloud service then uses hello results.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="dd34e-259">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="dd34e-259">Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="dd34e-260">General</span><span class="sxs-lookup"><span data-stu-id="dd34e-260">General</span></span>

<span data-ttu-id="dd34e-261">**Preguntas**: ¿necesito una puerta de enlace para los orígenes de datos en la nube de hello, como SQL Azure?</span><span class="sxs-lookup"><span data-stu-id="dd34e-261">**Q**: Do I need a gateway for data sources in hello cloud, such as SQL Azure?</span></span> <br/><span data-ttu-id="dd34e-262">
**R:** No.</span><span class="sxs-lookup"><span data-stu-id="dd34e-262">
**A**: No.</span></span> <span data-ttu-id="dd34e-263">Una puerta de enlace conecta a orígenes de datos de tooon locales solo.</span><span class="sxs-lookup"><span data-stu-id="dd34e-263">A gateway connects tooon-premises data sources only.</span></span>

<span data-ttu-id="dd34e-264">**¿Preguntas**: puerta de enlace de hello tiene toobe instalado en hello mismo equipo como origen de datos de hello?</span><span class="sxs-lookup"><span data-stu-id="dd34e-264">**Q**: Does hello gateway have toobe installed on hello same machine as hello data source?</span></span> <br/><span data-ttu-id="dd34e-265">
**R:** No.</span><span class="sxs-lookup"><span data-stu-id="dd34e-265">
**A**: No.</span></span> <span data-ttu-id="dd34e-266">puerta de enlace de Hello conecta toohello origen de datos usando la información de conexión de Hola que proporcionó.</span><span class="sxs-lookup"><span data-stu-id="dd34e-266">hello gateway connects toohello data source using hello connection information that was provided.</span></span> <span data-ttu-id="dd34e-267">Considere la posibilidad de puerta de enlace de hello como una aplicación de cliente en este sentido.</span><span class="sxs-lookup"><span data-stu-id="dd34e-267">Consider hello gateway as a client application in this sense.</span></span> <span data-ttu-id="dd34e-268">puerta de enlace de Hello solo necesita Hola capacidad tooconnect toohello nombre del servidor que se proporcionó.</span><span class="sxs-lookup"><span data-stu-id="dd34e-268">hello gateway just needs hello capability tooconnect toohello server name that was provided.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="dd34e-269">**Preguntas**: ¿por qué debo utiliza un trabajo de Azure o toosign de cuenta en la escuela?</span><span class="sxs-lookup"><span data-stu-id="dd34e-269">**Q**: Why must I use an Azure work or school account toosign in?</span></span> <br/><span data-ttu-id="dd34e-270">
**Un**: solo puede usar un trabajo de Azure o educativa cuenta cuando se instala la puerta de enlace de datos de hello en local.</span><span class="sxs-lookup"><span data-stu-id="dd34e-270">
**A**: You can only use an Azure work or school account when you install hello on-premises data gateway.</span></span> <span data-ttu-id="dd34e-271">Su cuenta de inicio de sesión se almacena en un inquilino administrado por Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="dd34e-271">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="dd34e-272">Por lo general, nombre principal de la cuenta de Azure AD usuario (UPN) coincide con dirección de correo electrónico de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd34e-272">Usually, your Azure AD account's user principal name (UPN) matches hello email address.</span></span>

<span data-ttu-id="dd34e-273">**P**: ¿Dónde se almacenan mis credenciales?</span><span class="sxs-lookup"><span data-stu-id="dd34e-273">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="dd34e-274">
**Un**: credenciales de Hola que especifique para un origen de datos se cifran y almacenan en el servicio de nube de puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd34e-274">
**A**: hello credentials that you enter for a data source are encrypted and stored in hello gateway cloud service.</span></span> <span data-ttu-id="dd34e-275">las credenciales de Hola se descifran en la puerta de enlace de datos de hello en local.</span><span class="sxs-lookup"><span data-stu-id="dd34e-275">hello credentials are decrypted at hello on-premises data gateway.</span></span>

<span data-ttu-id="dd34e-276">**P**: ¿Hay algún requisito con respecto al ancho de banda de red?</span><span class="sxs-lookup"><span data-stu-id="dd34e-276">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="dd34e-277">
**R**: Se recomienda que la conexión de red tenga buen rendimiento.</span><span class="sxs-lookup"><span data-stu-id="dd34e-277">
**A**: We recommend that your network connection has good throughput.</span></span> <span data-ttu-id="dd34e-278">Cada entorno es diferente y cantidad de Hola de datos que se envían afecta a los resultados de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd34e-278">Every environment is different, and hello amount of data being sent affects hello results.</span></span> <span data-ttu-id="dd34e-279">Usar ExpressRoute puede ayudar a tooguarantee un nivel de rendimiento entre hello centros de datos de Azure y local.</span><span class="sxs-lookup"><span data-stu-id="dd34e-279">Using ExpressRoute could help tooguarantee a level of throughput between on-premises and hello Azure datacenters.</span></span>
<span data-ttu-id="dd34e-280">Puede usar Hola herramienta de otro fabricante Azure Speed Test aplicación toohelp medidor su rendimiento.</span><span class="sxs-lookup"><span data-stu-id="dd34e-280">You can use hello third-party tool Azure Speed Test app toohelp gauge your throughput.</span></span>

<span data-ttu-id="dd34e-281">**Preguntas**: ¿qué es la latencia de Hola para consultas tooa datos de origen en ejecución de puerta de enlace de hello?</span><span class="sxs-lookup"><span data-stu-id="dd34e-281">**Q**: What is hello latency for running queries tooa data source from hello gateway?</span></span> <span data-ttu-id="dd34e-282">¿Cuál es la mejor arquitectura de hello?</span><span class="sxs-lookup"><span data-stu-id="dd34e-282">What is hello best architecture?</span></span> <br/><span data-ttu-id="dd34e-283">
**Un**: latencia de red tooreduce, puerta de enlace de instalación hello como origen de datos de toohello cerrar como sea posible.</span><span class="sxs-lookup"><span data-stu-id="dd34e-283">
**A**: tooreduce network latency, install hello gateway as close toohello data source as possible.</span></span> <span data-ttu-id="dd34e-284">Si puede instalar la puerta de enlace de hello en el origen de datos real de hello, esta proximidad reduce la latencia de hello introducida.</span><span class="sxs-lookup"><span data-stu-id="dd34e-284">If you can install hello gateway on hello actual data source, this proximity minimizes hello latency introduced.</span></span> <span data-ttu-id="dd34e-285">Considere la posibilidad de centros de datos de hello demasiado.</span><span class="sxs-lookup"><span data-stu-id="dd34e-285">Consider hello datacenters too.</span></span> <span data-ttu-id="dd34e-286">Por ejemplo, si el servicio usa el centro de datos de hello oeste de Estados Unidos y tiene SQL Server hospedado en una máquina virtual de Azure, la VM de Azure deben estar en hello West US demasiado.</span><span class="sxs-lookup"><span data-stu-id="dd34e-286">For example, if your service uses hello West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in hello West US too.</span></span> <span data-ttu-id="dd34e-287">Esta proximidad reduce la latencia y evita los cargos de salida en hello VM de Azure.</span><span class="sxs-lookup"><span data-stu-id="dd34e-287">This proximity minimizes latency and avoids egress charges on hello Azure VM.</span></span>

<span data-ttu-id="dd34e-288">**Preguntas**: ¿de qué resultados enviados toohello atrás en la nube?</span><span class="sxs-lookup"><span data-stu-id="dd34e-288">**Q**: How are results sent back toohello cloud?</span></span> <br/><span data-ttu-id="dd34e-289">
**Un**: los resultados se envían a través de hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="dd34e-289">
**A**: Results are sent through hello Azure Service Bus.</span></span>

<span data-ttu-id="dd34e-290">**Preguntas**: ¿hay ninguna puerta de enlace de toohello de las conexiones entrantes de nube de hello?</span><span class="sxs-lookup"><span data-stu-id="dd34e-290">**Q**: Are there any inbound connections toohello gateway from hello cloud?</span></span> <br/><span data-ttu-id="dd34e-291">
**R:** No.</span><span class="sxs-lookup"><span data-stu-id="dd34e-291">
**A**: No.</span></span> <span data-ttu-id="dd34e-292">puerta de enlace de Hello utiliza conexiones salientes tooAzure Bus de servicio.</span><span class="sxs-lookup"><span data-stu-id="dd34e-292">hello gateway uses outbound connections tooAzure Service Bus.</span></span>

<span data-ttu-id="dd34e-293">**P**: ¿Qué sucede si bloqueo las conexiones de salida?</span><span class="sxs-lookup"><span data-stu-id="dd34e-293">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="dd34e-294">¿Qué necesito tooopen?</span><span class="sxs-lookup"><span data-stu-id="dd34e-294">What do I need tooopen?</span></span> <br/><span data-ttu-id="dd34e-295">
**Un**: ver los puertos de Hola y hosts que Hola usos de la puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="dd34e-295">
**A**: See hello ports and hosts that hello gateway uses.</span></span>

<span data-ttu-id="dd34e-296">**¿Preguntas**: lo que se denomina el servicio de Windows de hello real?</span><span class="sxs-lookup"><span data-stu-id="dd34e-296">**Q**: What is hello actual Windows service called?</span></span><br/><span data-ttu-id="dd34e-297">
**Un**: en servicios, puerta de enlace de Hola se denomina servicio Power BI Enterprise Gateway.</span><span class="sxs-lookup"><span data-stu-id="dd34e-297">
**A**: In Services, hello gateway is called Power BI Enterprise Gateway Service.</span></span>

<span data-ttu-id="dd34e-298">**¿Preguntas**: Hola a servicio de Windows de puerta de enlace que se ejecutan con una cuenta de Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="dd34e-298">**Q**: Can hello gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="dd34e-299">
**R:** No.</span><span class="sxs-lookup"><span data-stu-id="dd34e-299">
**A**: No.</span></span> <span data-ttu-id="dd34e-300">Hola servicio de Windows debe tener una cuenta de Windows válida.</span><span class="sxs-lookup"><span data-stu-id="dd34e-300">hello Windows service must have a valid Windows account.</span></span> <span data-ttu-id="dd34e-301">De forma predeterminada, el servicio de Hola se ejecuta con hello SID de servicio, NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="dd34e-301">By default, hello service runs with hello Service SID, NT SERVICE\PBIEgwService.</span></span>

### <a name="high-availability-and-disaster-recovery"></a><span data-ttu-id="dd34e-302">Alta disponibilidad y recuperación ante desastres</span><span class="sxs-lookup"><span data-stu-id="dd34e-302">High availability and disaster recovery</span></span>

<span data-ttu-id="dd34e-303">**P**: ¿Cuáles son las opciones de recuperación ante desastres disponibles?</span><span class="sxs-lookup"><span data-stu-id="dd34e-303">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="dd34e-304">
**Un**: puede usar toorestore de clave de recuperación de Hola o mover una puerta de enlace.</span><span class="sxs-lookup"><span data-stu-id="dd34e-304">
**A**: You can use hello recovery key toorestore or move a gateway.</span></span> <span data-ttu-id="dd34e-305">Cuando se instala la puerta de enlace de hello, especifique la clave de recuperación de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd34e-305">When you install hello gateway, specify hello recovery key.</span></span>

<span data-ttu-id="dd34e-306">**Preguntas**: ¿cuál es la ventaja de Hola de clave de recuperación de hello?</span><span class="sxs-lookup"><span data-stu-id="dd34e-306">**Q**: What is hello benefit of hello recovery key?</span></span> <br/><span data-ttu-id="dd34e-307">
**Un**: clave de recuperación de hello proporciona una manera toomigrate o recuperar la configuración de puerta de enlace después de un desastre.</span><span class="sxs-lookup"><span data-stu-id="dd34e-307">
**A**: hello recovery key provides a way toomigrate or recover your gateway settings after a disaster.</span></span>

<span data-ttu-id="dd34e-308">**Preguntas**: ¿existen planes para habilitar escenarios de alta disponibilidad con puerta de enlace de hello?</span><span class="sxs-lookup"><span data-stu-id="dd34e-308">**Q**: Are there any plans for enabling high availability scenarios with hello gateway?</span></span> <br/><span data-ttu-id="dd34e-309">
**Un**: estos escenarios se encuentran en la guía básica de hello, pero aún no tenemos una escala de tiempo.</span><span class="sxs-lookup"><span data-stu-id="dd34e-309">
**A**: These scenarios are on hello roadmap, but we don't have a timeline yet.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="dd34e-310">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="dd34e-310">Troubleshooting</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

<span data-ttu-id="dd34e-311">**Preguntas**: ¿Cómo puedo ver las consultas que se están enviando el origen de datos local de toohello?</span><span class="sxs-lookup"><span data-stu-id="dd34e-311">**Q**: How can I see what queries are being sent toohello on-premises data source?</span></span> <br/><span data-ttu-id="dd34e-312">
**Un**: para habilitar el seguimiento de la consulta, que incluye las consultas de Hola que se envían.</span><span class="sxs-lookup"><span data-stu-id="dd34e-312">
**A**: You can enable query tracing, which includes hello queries that are sent.</span></span> <span data-ttu-id="dd34e-313">Recuerde consulta toochange remontarse toohello valor original cuando haya finalizado la solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="dd34e-313">Remember toochange query tracing back toohello original value when done troubleshooting.</span></span> <span data-ttu-id="dd34e-314">Si lo deja activado, crea registros de mayor tamaño.</span><span class="sxs-lookup"><span data-stu-id="dd34e-314">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="dd34e-315">También puede examinar las herramientas de que dispone su origen de datos para el seguimiento de consultas.</span><span class="sxs-lookup"><span data-stu-id="dd34e-315">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="dd34e-316">Por ejemplo, puede utilizar Eventos extendidos o SQL Profiler en SQL Server y Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="dd34e-316">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="dd34e-317">**¿Preguntas**: donde se encuentran los registros de puerta de enlace de hello?</span><span class="sxs-lookup"><span data-stu-id="dd34e-317">**Q**: Where are hello gateway logs?</span></span> <br/><span data-ttu-id="dd34e-318">
**R**: Consulte la sección Herramientas de este mismo tema.</span><span class="sxs-lookup"><span data-stu-id="dd34e-318">
**A**: See Tools later in this topic.</span></span>

### <a name="update-toohello-latest-version"></a><span data-ttu-id="dd34e-319">Actualizar la versión más reciente de toohello</span><span class="sxs-lookup"><span data-stu-id="dd34e-319">Update toohello latest version</span></span>

<span data-ttu-id="dd34e-320">Muchos problemas pueden surgir cuando la versión de la puerta de enlace de Hola quede anticuado.</span><span class="sxs-lookup"><span data-stu-id="dd34e-320">Many issues can surface when hello gateway version becomes outdated.</span></span> <span data-ttu-id="dd34e-321">Como buena práctica general, asegúrese de utilizar la versión más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd34e-321">As good general practice, make sure that you use hello latest version.</span></span> <span data-ttu-id="dd34e-322">Si no ha actualizado la puerta de enlace de Hola durante un mes o más, podría pensar en instalar la versión más reciente de Hola de puerta de enlace de Hola y vea si puede reproducir el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd34e-322">If you haven't updated hello gateway for a month or longer, you might consider installing hello latest version of hello gateway, and see if you can reproduce hello issue.</span></span>

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="dd34e-323">Error: No se pudo tooadd toogroup de usuario.</span><span class="sxs-lookup"><span data-stu-id="dd34e-323">Error: Failed tooadd user toogroup.</span></span> <span data-ttu-id="dd34e-324">(Usuarios del registro de rendimiento de-2147463168 PBIEgwService)</span><span class="sxs-lookup"><span data-stu-id="dd34e-324">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="dd34e-325">Podría obtener este error si intentas puerta de enlace de tooinstall hello en un controlador de dominio que no es compatible.</span><span class="sxs-lookup"><span data-stu-id="dd34e-325">You might get this error if you try tooinstall hello gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="dd34e-326">Asegúrese de que implemente la puerta de enlace de hello en un equipo que no es un controlador de dominio.</span><span class="sxs-lookup"><span data-stu-id="dd34e-326">Make sure that you deploy hello gateway on a machine that isn't a domain controller.</span></span>

## <a name="tools"></a><span data-ttu-id="dd34e-327">Herramientas</span><span class="sxs-lookup"><span data-stu-id="dd34e-327">Tools</span></span>

### <a name="collect-logs-from-hello-gateway-configurer"></a><span data-ttu-id="dd34e-328">Recopilar registros de configurer de puerta de enlace de Hola</span><span class="sxs-lookup"><span data-stu-id="dd34e-328">Collect logs from hello gateway configurer</span></span>

<span data-ttu-id="dd34e-329">Puede recopilar varios registros para puerta de enlace de Hola.</span><span class="sxs-lookup"><span data-stu-id="dd34e-329">You can collect several logs for hello gateway.</span></span> <span data-ttu-id="dd34e-330">Siempre se inician con registros de Hola!</span><span class="sxs-lookup"><span data-stu-id="dd34e-330">Always start with hello logs!</span></span>

#### <a name="installer-logs"></a><span data-ttu-id="dd34e-331">Registros del instalador</span><span class="sxs-lookup"><span data-stu-id="dd34e-331">Installer logs</span></span>

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a><span data-ttu-id="dd34e-332">Registros de configuración</span><span class="sxs-lookup"><span data-stu-id="dd34e-332">Configuration logs</span></span>

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="dd34e-333">Registros del servicio de puerta de enlace empresarial</span><span class="sxs-lookup"><span data-stu-id="dd34e-333">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a><span data-ttu-id="dd34e-334">Registros de eventos</span><span class="sxs-lookup"><span data-stu-id="dd34e-334">Event logs</span></span>

<span data-ttu-id="dd34e-335">Puede encontrar registros de Data Management Gateway y PowerBIGateway en hello **registros de aplicaciones y servicios**.</span><span class="sxs-lookup"><span data-stu-id="dd34e-335">You can find hello Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>

### <a name="fiddler-trace"></a><span data-ttu-id="dd34e-336">Seguimiento de Fiddler</span><span class="sxs-lookup"><span data-stu-id="dd34e-336">Fiddler Trace</span></span>

<span data-ttu-id="dd34e-337">[Fiddler](http://www.telerik.com/fiddler) es una herramienta gratuita de Telerik que supervisa el tráfico HTTP.</span><span class="sxs-lookup"><span data-stu-id="dd34e-337">[Fiddler](http://www.telerik.com/fiddler) is a free tool from Telerik that monitors HTTP traffic.</span></span> <span data-ttu-id="dd34e-338">Puede ver este tráfico mediante el servicio de Power BI desde el equipo cliente de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="dd34e-338">You can see this traffic with hello Power BI service from hello client machine.</span></span> <span data-ttu-id="dd34e-339">Este servicio puede mostrar errores y otra información relacionada.</span><span class="sxs-lookup"><span data-stu-id="dd34e-339">This service might show errors and other related information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dd34e-340">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="dd34e-340">Next steps</span></span>
    
* [<span data-ttu-id="dd34e-341">Conectar datos tooon locales desde las aplicaciones lógicas</span><span class="sxs-lookup"><span data-stu-id="dd34e-341">Connect tooon-premises data from logic apps</span></span>](../logic-apps/logic-apps-gateway-connection.md)
* [<span data-ttu-id="dd34e-342">Características de Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="dd34e-342">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="dd34e-343">Conectores para Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="dd34e-343">Connectors for Azure Logic Apps</span></span>](../connectors/apis-list.md)
