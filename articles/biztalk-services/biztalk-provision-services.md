---
title: "Creación de Azure BizTalk Services en Azure Portal | Microsoft Docs"
description: "Obtenga información acerca de cómo aprovisionar o crear Servicios de BizTalk en el Portal de Azure; MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: eca77b4a82eb67e1755717bb4429f8d450a64dc5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-biztalk-services-using-the-azure-portal"></a><span data-ttu-id="a24f5-103">Creación de Servicios de BizTalk mediante el Portal de Azure</span><span class="sxs-lookup"><span data-stu-id="a24f5-103">Create BizTalk Services using the Azure portal</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> <span data-ttu-id="a24f5-104">Para iniciar sesión en el Portal de Azure, se necesita una suscripción a Azure y una cuenta de Azure.</span><span class="sxs-lookup"><span data-stu-id="a24f5-104">To sign in to the Azure portal, you need an Azure account and Azure subscription.</span></span> <span data-ttu-id="a24f5-105">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="a24f5-105">If you don't have an account, you can create a free trial account within a few minutes.</span></span> <span data-ttu-id="a24f5-106">Consulte [Evaluación gratuita de Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span><span class="sxs-lookup"><span data-stu-id="a24f5-106">See [Azure Free Trial](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span></span>


## <span data-ttu-id="a24f5-107"><a name="CreateService"></a>Creación de un servicio de BizTalk</span><span class="sxs-lookup"><span data-stu-id="a24f5-107"><a name="CreateService"></a>Create a BizTalk Service</span></span>
<span data-ttu-id="a24f5-108">En función de la edición que elija, puede que no estén disponibles todos los valores del Servicios de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a24f5-108">Depending on the Edition you choose, not all BizTalk Service settings may be available.</span></span>

1. <span data-ttu-id="a24f5-109">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="a24f5-109">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="a24f5-110">En el panel de navegación inferior, seleccione **NUEVO**:</span><span class="sxs-lookup"><span data-stu-id="a24f5-110">In the bottom navigation pane, select **NEW**:</span></span>  
   <span data-ttu-id="a24f5-111">![Seleccione el botón New][NEWButton]</span><span class="sxs-lookup"><span data-stu-id="a24f5-111">![Select the New button][NEWButton]</span></span>
3. <span data-ttu-id="a24f5-112">Seleccione **APP SERVICES** > **SERVICIO DE BIZTALK** > **CREACIÓN PERSONALIZADA**:</span><span class="sxs-lookup"><span data-stu-id="a24f5-112">Select **APP SERVICES** > **BIZTALK SERVICE** > **CUSTOM CREATE**:</span></span>  
   <span data-ttu-id="a24f5-113">![Seleccione Servicio de BizTalk y seleccione Custom Create][NewBizTalkService]</span><span class="sxs-lookup"><span data-stu-id="a24f5-113">![Select BizTalk Service and select Custom Create][NewBizTalkService]</span></span>
4. <span data-ttu-id="a24f5-114">Escriba la configuración del servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a24f5-114">Enter the BizTalk Service settings:</span></span>
   
    <table border="1">
    <tr>
    <td><span data-ttu-id="a24f5-115"><strong>Nombre del servicio de BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="a24f5-115"><strong>BizTalk service name</strong></span></span></td>
    <td><span data-ttu-id="a24f5-116">Puede escribir cualquier nombre pero sea específico.</span><span class="sxs-lookup"><span data-stu-id="a24f5-116">You can enter any name but be specific.</span></span> <span data-ttu-id="a24f5-117">Estos son algunos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="a24f5-117">Some examples include:</span></span><br/><br/><span data-ttu-id="a24f5-118">
    <em>mycompany</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="a24f5-118">
    <em>mycompany</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="a24f5-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="a24f5-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="a24f5-120">
    <em>myapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="a24f5-120">
    <em>myapplication</em>.biztalk.windows.net</span></span><br/><br/><span data-ttu-id="a24f5-121">".biztalk.windows.net" se agregará automáticamente al nombre que escriba.</span><span class="sxs-lookup"><span data-stu-id="a24f5-121">".biztalk.windows.net" is automatically added to the name you enter.</span></span> <span data-ttu-id="a24f5-122">Esto crea una dirección URL que se utiliza para tener acceso a su servicio de BizTalk, como <strong>https://<em>miaplicación</em>.biztalk.windows.net</strong>.</span><span class="sxs-lookup"><span data-stu-id="a24f5-122">This creates a URL that is used to access your BizTalk Service, like <strong>https://<em>myapplication</em>.biztalk.windows.net</strong>.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="a24f5-123"><strong>Edición</strong></span><span class="sxs-lookup"><span data-stu-id="a24f5-123"><strong>Edition</strong></span></span></td>
    <td><span data-ttu-id="a24f5-124">Si está en la fase de prueba/desarrollo, elija <strong>Developer</strong>.</span><span class="sxs-lookup"><span data-stu-id="a24f5-124">If you are in the testing/development phase, choose <strong>Developer</strong>.</span></span> <span data-ttu-id="a24f5-125">Si está en la fase de producción, use <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: gráfico de ediciones</a> para determinar si la opción correcta para su escenario de negocios es <strong>Premium</strong>, <strong>Standard</strong> o <strong>Basic</strong>.</span><span class="sxs-lookup"><span data-stu-id="a24f5-125">If you are in the production phase, use the <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: Editions Chart</a> to determine if <strong>Premium</strong>, <strong>Standard</strong>, or <strong>Basic</strong> is the correct choice for your business scenario.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="a24f5-126"><strong>Región</strong></span><span class="sxs-lookup"><span data-stu-id="a24f5-126"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="a24f5-127">Seleccione la región geográfica donde hospedar su servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a24f5-127">Select the geographic region to host your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="a24f5-128"><strong>URL de dominio</strong></span><span class="sxs-lookup"><span data-stu-id="a24f5-128"><strong>Domain URL</strong></span></span></td>
    <td><span data-ttu-id="a24f5-129"><strong>Opcional</strong>.</span><span class="sxs-lookup"><span data-stu-id="a24f5-129"><strong>Optional</strong>.</span></span> <span data-ttu-id="a24f5-130">De manera predeterminada, la dirección URL de dominio es <em>NombreDeServicioDeBizTalk</em>.biztalk.windows.net.</span><span class="sxs-lookup"><span data-stu-id="a24f5-130">By default, the domain URL is <em>YourBizTalkServiceName</em>.biztalk.windows.net.</span></span> <span data-ttu-id="a24f5-131">También se puede escribir un dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="a24f5-131">A custom domain can also be entered.</span></span> <span data-ttu-id="a24f5-132">Por ejemplo, si el dominio es <em>contoso</em>, puede escribir:</span><span class="sxs-lookup"><span data-stu-id="a24f5-132">For example, if your domain is <em>contoso</em>, you can enter:</span></span> <br/><br/><span data-ttu-id="a24f5-133">
    <em>MyCompany</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="a24f5-133">
    <em>MyCompany</em>.contoso.com</span></span><br/><span data-ttu-id="a24f5-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="a24f5-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="a24f5-135">
    <em>MyApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="a24f5-135">
    <em>MyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="a24f5-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="a24f5-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span></span><br/>
    </td>
    </tr>
    </table>
<span data-ttu-id="a24f5-137">Seleccione la flecha SIGUIENTE.</span><span class="sxs-lookup"><span data-stu-id="a24f5-137">Select the NEXT arrow.</span></span>
<span data-ttu-id="a24f5-138">5.</span><span class="sxs-lookup"><span data-stu-id="a24f5-138">5.</span></span> <span data-ttu-id="a24f5-139">Escriba la configuración de la base de datos y almacenamiento:</span><span class="sxs-lookup"><span data-stu-id="a24f5-139">Enter the Storage and Database Settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="a24f5-140"><strong>Cuenta de almacenamiento de supervisión y archivado</strong></span><span class="sxs-lookup"><span data-stu-id="a24f5-140"><strong>Monitoring/Archiving storage account</strong></span></span></td>
    <td><span data-ttu-id="a24f5-141">Seleccione una cuenta de almacenamiento existente o cree una nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a24f5-141">Select an existing storage account or create a new storage account.</span></span> <br/><br/><span data-ttu-id="a24f5-142">Si crea una nueva cuenta de almacenamiento, escriba el <strong>Nombre de cuenta de almacenamiento</strong>.</span><span class="sxs-lookup"><span data-stu-id="a24f5-142">If you create a new Storage account, enter the <strong>Storage Account Name</strong>.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="a24f5-143"><strong>Base de datos de seguimiento</strong></span><span class="sxs-lookup"><span data-stu-id="a24f5-143"><strong>Tracking database</strong></span></span></td>
    <td><span data-ttu-id="a24f5-144">Si usa una Base de datos SQL de Azure existente, no puede usarla otro Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a24f5-144">If you use an existing Azure SQL Database, it cannot be used by another BizTalk Service.</span></span> <span data-ttu-id="a24f5-145">Necesita el nombre de inicio de sesión y la contraseña especificados cuando se creó ese servidor de Base de datos SQL de Azure.</span><span class="sxs-lookup"><span data-stu-id="a24f5-145">You need the login name and password entered when that Azure SQL Database Server was created.</span></span><br/><br/><span data-ttu-id="a24f5-146"><strong>SUGERENCIA</strong> Cree la base de datos de seguimiento y la cuenta de almacenamiento de supervisión/archivado en la misma región que el Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a24f5-146"><strong>TIP</strong> Create the Tracking database and Monitoring/Archiving storage account in the same region as the BizTalk Service.</span></span></td>
    </tr>
    </table>
<span data-ttu-id="a24f5-147">Seleccione la flecha SIGUIENTE.</span><span class="sxs-lookup"><span data-stu-id="a24f5-147">Select the NEXT arrow.</span></span>
<span data-ttu-id="a24f5-148">6.</span><span class="sxs-lookup"><span data-stu-id="a24f5-148">6.</span></span> <span data-ttu-id="a24f5-149">Escriba la configuración de la base de datos:</span><span class="sxs-lookup"><span data-stu-id="a24f5-149">Enter the Database settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="a24f5-150"><strong>Name</strong></span><span class="sxs-lookup"><span data-stu-id="a24f5-150"><strong>Name</strong></span></span></td>
    <td><span data-ttu-id="a24f5-151">Disponible cuando se selecciona <strong>Crear una nueva instancia de SQL Database</strong> en la pantalla anterior.</span><span class="sxs-lookup"><span data-stu-id="a24f5-151">Available when <strong>Create a new SQL Database instance</strong> is selected in the previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="a24f5-152">Escriba el nombre de SQL Database que va a usar servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a24f5-152">Enter a SQL Database name to be used by your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="a24f5-153"><strong>Servidor</strong></span><span class="sxs-lookup"><span data-stu-id="a24f5-153"><strong>Server</strong></span></span></td>
    <td><span data-ttu-id="a24f5-154">Disponible cuando se selecciona <strong>Crear una nueva instancia de SQL Database</strong> en la pantalla anterior.</span><span class="sxs-lookup"><span data-stu-id="a24f5-154">Available when <strong>Create a new SQL Database instance</strong> is selected in the previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="a24f5-155">Seleccione un servidor de SQL Database existente o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="a24f5-155">Select an existing SQL Database Server or create a new SQL Database server.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="a24f5-156"><strong>Nombre de inicio de sesión del servidor</strong></span><span class="sxs-lookup"><span data-stu-id="a24f5-156"><strong>Server login name</strong></span></span></td>
    <td><span data-ttu-id="a24f5-157">Escriba el nombre de usuario de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="a24f5-157">Enter the login user name.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="a24f5-158"><strong>Contraseña de inicio de sesión del servidor</strong></span><span class="sxs-lookup"><span data-stu-id="a24f5-158"><strong>Server login password</strong></span></span></td>
    <td><span data-ttu-id="a24f5-159">Escriba la contraseña de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="a24f5-159">Enter the login password.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="a24f5-160"><strong>Región</strong></span><span class="sxs-lookup"><span data-stu-id="a24f5-160"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="a24f5-161">Disponible cuando se selecciona <strong>Crear una nueva instancia de SQL Database</strong>.</span><span class="sxs-lookup"><span data-stu-id="a24f5-161">Available when <strong>Create a new SQL Database instance</strong> is selected.</span></span> <span data-ttu-id="a24f5-162">Seleccione la región geográfica donde hospedar su Base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="a24f5-162">Select the geographic region to host your SQL Database.</span></span></td>
    </tr>
    </table>

<span data-ttu-id="a24f5-163">Seleccione la marca de verificación para completar el asistente.</span><span class="sxs-lookup"><span data-stu-id="a24f5-163">Select the check mark to complete the wizard.</span></span> <span data-ttu-id="a24f5-164">Aparece el icono de progreso: </span><span class="sxs-lookup"><span data-stu-id="a24f5-164">The progress icon appears:</span></span>  
![El icono de progreso aparece cuando se completa][ProgressComplete]

<span data-ttu-id="a24f5-166">Una vez que se completa, se crea un Servicio de BizTalk de Azure y queda listo para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a24f5-166">When complete, the Azure BizTalk Service is created and ready for your applications.</span></span> <span data-ttu-id="a24f5-167">La configuración predeterminada es suficiente.</span><span class="sxs-lookup"><span data-stu-id="a24f5-167">The default settings are sufficient.</span></span> <span data-ttu-id="a24f5-168">Si desea cambiar la configuración predeterminada, seleccione **SERVICIOS DE BIZTALK** en el panel de navegación que se encuentra a la izquierda y seleccione su Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a24f5-168">If you want to change the default settings, select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service.</span></span> <span data-ttu-id="a24f5-169">La configuración adicional aparece en las [pestañas Panel, Monitor y Escala](biztalk-dashboard-monitor-scale-tabs.md) de la parte superior.</span><span class="sxs-lookup"><span data-stu-id="a24f5-169">Additional settings are displayed in the [Dashboard, Monitor, and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md) at the top.</span></span>

<span data-ttu-id="a24f5-170">Según el estado del servicio de BizTalk, hay algunas operaciones que no se pueden completar.</span><span class="sxs-lookup"><span data-stu-id="a24f5-170">Depending on the state of the BizTalk Service, there are some operations that cannot be completed.</span></span> <span data-ttu-id="a24f5-171">Para ver una lista de estas operaciones, vaya al [gráfico del estado de Servicios de BizTalk](biztalk-service-state-chart.md).</span><span class="sxs-lookup"><span data-stu-id="a24f5-171">For a list of these operations, go to [BizTalk Services State Chart](biztalk-service-state-chart.md).</span></span>

## <a name="post-provisioning-steps"></a><span data-ttu-id="a24f5-172">Pasos posteriores al aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="a24f5-172">Post-provisioning steps</span></span>
* [<span data-ttu-id="a24f5-173">Instalación del certificado en un equipo local</span><span class="sxs-lookup"><span data-stu-id="a24f5-173">Install the certificate on a local computer</span></span>](#InstallCert)
* [<span data-ttu-id="a24f5-174">Incorporación de un certificado listo para producción</span><span class="sxs-lookup"><span data-stu-id="a24f5-174">Add a production-ready certificate</span></span>](#AddCert)
* [<span data-ttu-id="a24f5-175">Obtención del espacio de nombres de control de acceso</span><span class="sxs-lookup"><span data-stu-id="a24f5-175">Get the Access Control namespace</span></span>](#ACS)

#### <span data-ttu-id="a24f5-176"><a name="InstallCert"></a>Instalación del certificado en un equipo local</span><span class="sxs-lookup"><span data-stu-id="a24f5-176"><a name="InstallCert"></a>Install the certificate on a local computer</span></span>
<span data-ttu-id="a24f5-177">Como parte del aprovisionamiento del Servicio de BizTalk, se crea un certificado autofirmado y se asocia a su suscripción del Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a24f5-177">As part of BizTalk Service provisioning, a self-signed certificate is created and associated with your BizTalk Service subscription.</span></span> <span data-ttu-id="a24f5-178">Debe descargar este certificado e instalarlo en equipos desde los que implemente aplicaciones del Servicio de BizTalk o envíe mensajes a un extremo del Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a24f5-178">You must download this certificate and install it on computers from where you either deploy BizTalk Service applications or send messages to a BizTalk Service endpoint.</span></span>

1. <span data-ttu-id="a24f5-179">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="a24f5-179">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="a24f5-180">Seleccione **SERVICIOS DE BIZTALK** en el panel de navegación que se encuentra a la izquierda y, luego, seleccione su suscripción al Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a24f5-180">Select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service subscription.</span></span>
3. <span data-ttu-id="a24f5-181">Seleccione la pestaña **Panel** .</span><span class="sxs-lookup"><span data-stu-id="a24f5-181">Select the **Dashboard** tab.</span></span>
4. <span data-ttu-id="a24f5-182">Seleccione **Descargar certificado SSL**:</span><span class="sxs-lookup"><span data-stu-id="a24f5-182">Select **Download SSL Certificate**:</span></span>  
   <span data-ttu-id="a24f5-183">![Modificar certificado SSL][QuickGlance]</span><span class="sxs-lookup"><span data-stu-id="a24f5-183">![Modify SSL Certificate][QuickGlance]</span></span>
5. <span data-ttu-id="a24f5-184">Haga doble clic en el certificado y ejecute el asistente para instalar el certificado.</span><span class="sxs-lookup"><span data-stu-id="a24f5-184">Double-click the certificate and run through the wizard to install the certificate.</span></span> <span data-ttu-id="a24f5-185">Asegúrese de instalar el certificado en el almacén **Entidades de certificación raíz de confianza** .</span><span class="sxs-lookup"><span data-stu-id="a24f5-185">Make sure you install the certificate under the **Trusted Root Certificate Authorities** store.</span></span>

#### <span data-ttu-id="a24f5-186"><a name="AddCert"></a>Incorporación de un certificado listo para producción</span><span class="sxs-lookup"><span data-stu-id="a24f5-186"><a name="AddCert"></a>Add a production-ready certificate</span></span>
<span data-ttu-id="a24f5-187">El certificado autofirmado que se crea automáticamente al crear Servicios de BizTalk está pensado únicamente para entornos de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="a24f5-187">The self-signed certificate that is automatically created when creating BizTalk Services is intended for use in development environments only.</span></span> <span data-ttu-id="a24f5-188">Para escenarios de producción, reemplácelo por un certificado listo para producción.</span><span class="sxs-lookup"><span data-stu-id="a24f5-188">For production scenarios, replace it with a production-ready certificate.</span></span>

1. <span data-ttu-id="a24f5-189">En la pestaña **Panel**, seleccione **Actualizar certificado SSL**.</span><span class="sxs-lookup"><span data-stu-id="a24f5-189">On the **Dashboard** tab, select **Update SSL Certificate**.</span></span>
2. <span data-ttu-id="a24f5-190">Vaya al certificado SSL privado (*NombreCertificado*.pfx) que incluye el nombre de su Servicio de BizTalk, escriba la contraseña y haga clic en la marca.</span><span class="sxs-lookup"><span data-stu-id="a24f5-190">Browse to your private SSL certificate (*CertificateName*.pfx) that includes your BizTalk Service name, enter the password, and then click the check mark.</span></span>

#### <span data-ttu-id="a24f5-191"><a name="ACS"></a>Obtención del espacio de nombres de control de acceso</span><span class="sxs-lookup"><span data-stu-id="a24f5-191"><a name="ACS"></a>Get the Access Control namespace</span></span>
1. <span data-ttu-id="a24f5-192">Inicie sesión en el [Portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="a24f5-192">Sign in to the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="a24f5-193">Seleccione **SERVICIOS DE BIZTALK** en el panel de navegación izquierdo y, a continuación, seleccione su Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a24f5-193">Select **BIZTALK SERVICES** in the left navigation pane, and then select your BizTalk Service.</span></span>
3. <span data-ttu-id="a24f5-194">Seleccione **Información de conexión**en la barra de tareas:</span><span class="sxs-lookup"><span data-stu-id="a24f5-194">In the task bar, select **Connection Information**:</span></span>  
   <span data-ttu-id="a24f5-195">![Seleccione Connection Information][ACSConnectInfo]</span><span class="sxs-lookup"><span data-stu-id="a24f5-195">![Select Connection Information][ACSConnectInfo]</span></span>
4. <span data-ttu-id="a24f5-196">Copie los valores de control de acceso.</span><span class="sxs-lookup"><span data-stu-id="a24f5-196">Copy the Access Control values.</span></span>

<span data-ttu-id="a24f5-197">Cuando implementa un proyecto de servicio de BizTalk desde Visual Studio, debe escribir este espacio de nombres del servicio de control de acceso.</span><span class="sxs-lookup"><span data-stu-id="a24f5-197">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="a24f5-198">El espacio de nombres Control de acceso se crea automáticamente para el Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a24f5-198">The Access Control namespace is automatically created for your BizTalk Service.</span></span>

<span data-ttu-id="a24f5-199">Los valores de control de acceso se pueden utilizar con cualquier aplicación.</span><span class="sxs-lookup"><span data-stu-id="a24f5-199">The Access Control values can be used with any application.</span></span> <span data-ttu-id="a24f5-200">Una vez que se crean los Servicios de BizTalk de Azure, el espacio de nombres del servicio de control de acceso controla la autenticación con su implementación del servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a24f5-200">When Azure BizTalk Services is created, this Access Control namespace controls the authentication with your BizTalk Service deployment.</span></span> <span data-ttu-id="a24f5-201">Si desea cambiar la suscripción o administrar el espacio de nombres, seleccione **ACTIVE DIRECTORY** en el panel de navegación que se encuentra a la izquierda y, luego, seleccione el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="a24f5-201">If you want to change the subscription or manage the namespace, select **ACTIVE DIRECTORY** in the left navigation pane and then select your namespace.</span></span> <span data-ttu-id="a24f5-202">La barra de tareas muestra sus opciones.</span><span class="sxs-lookup"><span data-stu-id="a24f5-202">The task bar lists your options.</span></span>

<span data-ttu-id="a24f5-203">Haga clic en **Administrar** para abrir el Portal de administración del sistema de control de acceso.</span><span class="sxs-lookup"><span data-stu-id="a24f5-203">Clicking **Manage** opens the Access Control Management Portal.</span></span> <span data-ttu-id="a24f5-204">En el Portal de administración de Access Control, el servicio de BizTalk usa **Identidades de servicio**:</span><span class="sxs-lookup"><span data-stu-id="a24f5-204">In the Access Control Management Portal, the BizTalk Service uses **Service identities**:</span></span>  
<span data-ttu-id="a24f5-205">![Identidades de servicio de ACS en el Portal de administración del sistema de control de acceso][ACSServiceIdentities]</span><span class="sxs-lookup"><span data-stu-id="a24f5-205">![ACS Service Identities in the Access Control Management Portal][ACSServiceIdentities]</span></span>

<span data-ttu-id="a24f5-206">La identidad de servicio del control de acceso es un conjunto de credenciales que permiten que las aplicaciones o los clientes se autentiquen directamente con el control de acceso.</span><span class="sxs-lookup"><span data-stu-id="a24f5-206">The Access Control service identity is a set of credentials that allow applications or clients to authenticate directly with Access Control and receive a token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a24f5-207">El servicio de BizTalk usa el valor **Owner** para la identidad de servicio predeterminada y el valor **Password**.</span><span class="sxs-lookup"><span data-stu-id="a24f5-207">The BizTalk Service uses **Owner** for the default service identity and the **Password** value.</span></span> <span data-ttu-id="a24f5-208">Si usa el valor de Symmetric Key, en lugar del valor de Password, puede aparecer el siguiente error:</span><span class="sxs-lookup"><span data-stu-id="a24f5-208">If you use the Symmetric Key value instead of the Password value, the following error may occur.</span></span><br/><br/><span data-ttu-id="a24f5-209">*Could not connect to the Access Control Management Service account with the specified credentials*</span><span class="sxs-lookup"><span data-stu-id="a24f5-209">*Could not connect to the Access Control Management Service account with the specified credentials*</span></span>
> 
> 

<span data-ttu-id="a24f5-210">[Administración del espacio de nombres ACS](https://msdn.microsoft.com/library/azure/hh674478.aspx) muestra algunas directrices y recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="a24f5-210">[Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) lists some guidelines and recommendations.</span></span>

## <a name="requirements-explained"></a><span data-ttu-id="a24f5-211">Requisitos explicados</span><span class="sxs-lookup"><span data-stu-id="a24f5-211">Requirements explained</span></span>
<span data-ttu-id="a24f5-212">Estos requisitos no se aplican a la versión gratuita.</span><span class="sxs-lookup"><span data-stu-id="a24f5-212">These requirements do not apply to the Free Edition.</span></span>

<table border="1">
<tr bgcolor="FAF9F9">
        <td><span data-ttu-id="a24f5-213"><strong>Lo que necesita</strong></span><span class="sxs-lookup"><span data-stu-id="a24f5-213"><strong>What you need</strong></span></span></td>
        <td><span data-ttu-id="a24f5-214"><strong>Por qué es necesario</strong></span><span class="sxs-lookup"><span data-stu-id="a24f5-214"><strong>Why you need it</strong></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="a24f5-215">Suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="a24f5-215">Azure subscription</span></span></td>
<td><span data-ttu-id="a24f5-216">La suscripción determina quién puede iniciar sesión en el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="a24f5-216">The subscription determines who can sign in to the Azure portal.</span></span> <span data-ttu-id="a24f5-217">El titular de la cuenta crea la suscripción en <a HREF="https://account.windowsazure.com/Subscriptions"> Suscripciones de Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="a24f5-217">The Account holder creates the subscription at <a HREF="https://account.windowsazure.com/Subscriptions"> Azure Subscriptions</a>.</span></span>
<br/><br/>
<span data-ttu-id="a24f5-218">La cuenta de Azure puede tener varias suscripciones y la puede administrar alguien que tenga permisos.</span><span class="sxs-lookup"><span data-stu-id="a24f5-218">The Azure account can have multiple subscriptions and can be managed by anyone who is permitted.</span></span> <span data-ttu-id="a24f5-219">Por ejemplo, el titular de su cuenta de Azure crea una suscripción llamada <em>BizTalkServiceSubscription</em> y concede acceso a la misma a los administradores de BizTalk de la empresa (por ejemplo, ContosoBTSAdmins@live.com).</span><span class="sxs-lookup"><span data-stu-id="a24f5-219">For example, your Azure account holder creates a subscription named <em>BizTalkServiceSubscription</em> and gives the BizTalk Administrators within your company (for example, ContosoBTSAdmins@live.com) access to this subscription.</span></span> <span data-ttu-id="a24f5-220">En este escenario, los administradores de BizTalk inician sesión en el Portal de Azure y tienen permisos totales de administrador en todos los servicios hospedados en la suscripción, incluidos Servicios de BizTalk de Azure.</span><span class="sxs-lookup"><span data-stu-id="a24f5-220">In this scenario, the BizTalk Administrators sign in to the Azure portal and have full Administrator rights to all the hosted services in the subscription, including Azure BizTalk Services.</span></span> <span data-ttu-id="a24f5-221">Los administradores de BizTalk no son los titulares de la cuenta de Azure y, por lo tanto, no tienen acceso a información de facturación alguna.</span><span class="sxs-lookup"><span data-stu-id="a24f5-221">The BizTalk Administrators are not the Azure account holders and therefore don't have access to any billing information.</span></span>
<br/><br/><span data-ttu-id="a24f5-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Administrar cuentas, suscripciones y roles administrativos en Azure Portal</a> ofrece más información al respecto.</span><span class="sxs-lookup"><span data-stu-id="a24f5-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Manage Subscriptions and Storage Accounts in the Azure portal</a> provides more information.</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="a24f5-223">Base de datos SQL de Azure</span><span class="sxs-lookup"><span data-stu-id="a24f5-223">Azure SQL Database</span></span></td>
<td><span data-ttu-id="a24f5-224">Almacena las tablas, vistas y procedimientos almacenados que utilizan los Servicios de BizTalk de Azure, incluidos los datos de seguimiento.</span><span class="sxs-lookup"><span data-stu-id="a24f5-224">Stores the tables, views, and stored procedures used by the BizTalk Service, including the Tracking data.</span></span>
<br/><br/>
<span data-ttu-id="a24f5-225">Cuando cree un servicio de BizTalk, puede usar un servidor de Azure SQL Server existente, una Base de datos SQL de Azure existente, o bien puede crear automáticamente un servidor o una base de datos nuevos.</span><span class="sxs-lookup"><span data-stu-id="a24f5-225">When you create a BizTalk Service, you can use an existing Azure SQL Server, Azure SQL Database, or automatically create a new Server or Database.</span></span>
<br/><br/>
<span data-ttu-id="a24f5-226">La escala de Base de datos SQL se configura automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a24f5-226">The SQL Database scale is automatically configured.</span></span> <span data-ttu-id="a24f5-227">Normalmente, la escala predeterminada es suficiente para un Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a24f5-227">Typically, the default scale is sufficient for a BizTalk Service.</span></span> <span data-ttu-id="a24f5-228">El cambio de la escala puede afectar al precio.</span><span class="sxs-lookup"><span data-stu-id="a24f5-228">Changing the scale impacts pricing.</span></span> <span data-ttu-id="a24f5-229">Consulte <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">Cuentas y facturación en Azure SQL Database</a>
</span><span class="sxs-lookup"><span data-stu-id="a24f5-229">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
</span></span><br/><br/><span data-ttu-id="a24f5-230">
<strong>Notas</strong>
</span><span class="sxs-lookup"><span data-stu-id="a24f5-230">
<strong>Notes</strong>
</span></span><br/>
<ul>
<li> <span data-ttu-id="a24f5-231">Cuando crea una nueva Base de datos SQL o SQL Server de Azure, Servicios de Azure se habilita automáticamente.</span><span class="sxs-lookup"><span data-stu-id="a24f5-231">When you create a new Azure SQL Server and Database, Azure Services is automatically enabled.</span></span> <span data-ttu-id="a24f5-232">El Servicio de BizTalk requiere que los servicios de Azure estén habilitados.</span><span class="sxs-lookup"><span data-stu-id="a24f5-232">The BizTalk Service requires Azure Services be enabled.</span></span></li>
<li><span data-ttu-id="a24f5-233">Si crea una Base de datos SQL de Azure nueva en un SQL Server de Azure existente, no se cambian las reglas de firewall del servidor.</span><span class="sxs-lookup"><span data-stu-id="a24f5-233">If you create a new Azure SQL Database on an existing Azure SQL Server, the firewall rules of the Server are not changed.</span></span> <span data-ttu-id="a24f5-234">Como resultado, es posible que otros servicios de Azure no puedan tener acceso a las bases de datos del servidor.</span><span class="sxs-lookup"><span data-stu-id="a24f5-234">As a result, it's possible other Azure Services are not allowed access to the Server's databases.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="a24f5-235">Espacio de nombres del servicio de control de acceso de Azure</span><span class="sxs-lookup"><span data-stu-id="a24f5-235">Azure Access Control namespace</span></span></td>
<td><span data-ttu-id="a24f5-236">Autentica con los Servicios de BizTalk de Azure.</span><span class="sxs-lookup"><span data-stu-id="a24f5-236">Authenticates with Azure BizTalk Services.</span></span> <span data-ttu-id="a24f5-237">Cuando implementa un proyecto de servicio de BizTalk desde Visual Studio, debe escribir este espacio de nombres del servicio de control de acceso.</span><span class="sxs-lookup"><span data-stu-id="a24f5-237">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="a24f5-238">Al crear un Servicio de BizTalk, se crea automáticamente el espacio de nombres Control de acceso. </span><span class="sxs-lookup"><span data-stu-id="a24f5-238">When you create a BizTalk Service, the Access Control namespace is automatically created.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="a24f5-239">Cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="a24f5-239">Azure Storage account</span></span></td>
<td><span data-ttu-id="a24f5-240">Proporciona acceso a tablas, blobs y colas usados por su servicio de BizTalk para guardar lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="a24f5-240">Gives access to tables, blobs, and queues used by your BizTalk Service to save the following:</span></span>

<ul>
<li><span data-ttu-id="a24f5-241">Archivos de registro que supervisan el Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a24f5-241">Log files that monitor the BizTalk Service.</span></span> <span data-ttu-id="a24f5-242">El resultado de la supervisión también aparece en la pestaña **Supervisión** de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a24f5-242">The monitoring output is also displayed in the **Monitoring** tab in the Azure portal.</span></span></li>
<li><span data-ttu-id="a24f5-243">Cuando se crea un contrato X12 o AS2 entre asociados, puede habilitar la característica de archivado para almacenar propiedades de mensaje.</span><span class="sxs-lookup"><span data-stu-id="a24f5-243">When creating an X12 or AS2 agreement between partners, you can enable the Archiving feature to store message properties.</span></span> <span data-ttu-id="a24f5-244">Estos datos se guardan en la cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a24f5-244">This data is saved in the Storage account.</span></span></li>
</ul>
<br/>
<span data-ttu-id="a24f5-245">Cuando crea un servicio de BizTalk, puede usar una cuenta de almacenamiento existente o puede crear automáticamente una nueva.</span><span class="sxs-lookup"><span data-stu-id="a24f5-245">When you create a BizTalk Service, you can use an existing Storage account or automatically create a new Storage account.</span></span>
<br/><br/>
<span data-ttu-id="a24f5-246">La configuración de almacenamiento predeterminada es suficiente para un Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a24f5-246">The default Storage settings are sufficient for a BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="a24f5-247">Cuando crea una cuenta de almacenamiento, se crean automáticamente una clave primaria y una clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="a24f5-247">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="a24f5-248">Estas claves controlan el acceso a su cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="a24f5-248">These Keys control access to your Storage account.</span></span> <span data-ttu-id="a24f5-249">El servicio de BizTalk utiliza automáticamente la clave principal.</span><span class="sxs-lookup"><span data-stu-id="a24f5-249">The BizTalk Service automatically uses the Primary Key.</span></span>
<br/><br/>
<span data-ttu-id="a24f5-250">Consulte <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Almacenamiento</a> para más información.</span><span class="sxs-lookup"><span data-stu-id="a24f5-250">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a> for more information.</span></span>
</td>
</tr>

<tr>
<td><span data-ttu-id="a24f5-251">Certificado privado de SSL</span><span class="sxs-lookup"><span data-stu-id="a24f5-251">SSL private certificate</span></span></td>
<td>
<span data-ttu-id="a24f5-252">Cuando se crea un servicio de Azure BizTalk, también se crea una URL HTTPS que incluye su nombre de Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a24f5-252">When an Azure BizTalk Service is created, an HTTPS URL that includes your BizTalk Service name is also created.</span></span> <span data-ttu-id="a24f5-253">Esta URL se configura automáticamente para usar un certificado solo de desarrollo autofirmado.</span><span class="sxs-lookup"><span data-stu-id="a24f5-253">This URL is automatically configured to use a self-signed development-only certificate.</span></span> <span data-ttu-id="a24f5-254">Para producción, necesita un certificado SSL privado.</span><span class="sxs-lookup"><span data-stu-id="a24f5-254">For production, you need a private SSL certificate.</span></span>
<br/><br/><span data-ttu-id="a24f5-255">
<strong>Información importante sobre el certificado SSL</strong>

</span><span class="sxs-lookup"><span data-stu-id="a24f5-255">
<strong>Important SSL Certificate Information</strong>

</span></span><ul>
<li><span data-ttu-id="a24f5-256">La fecha de caducidad del certificado debe ser menor a cinco años.</span><span class="sxs-lookup"><span data-stu-id="a24f5-256">The certificate expiration date must be less than 5 years.</span></span></li>
<li><span data-ttu-id="a24f5-257">Todos los certificados privados requieren una contraseña.</span><span class="sxs-lookup"><span data-stu-id="a24f5-257">All private certificates require a password.</span></span> <span data-ttu-id="a24f5-258">Apréndase esta contraseña y, como procedimiento recomendado, comparta esta contraseña con sus administradores.</span><span class="sxs-lookup"><span data-stu-id="a24f5-258">Know this password and as a best practice, share this password with your administrators.</span></span></li>
<li><span data-ttu-id="a24f5-259">Los certificados autofirmados se utilizan en un entorno de prueba o de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="a24f5-259">Self-signed certificates are used in a test/development environment.</span></span> <span data-ttu-id="a24f5-260">Cuando utilice certificados autofirmados, importe el certificado a su almacén personal de certificados y al almacén de certificados de las entidades de certificación raíz de confianza.</span><span class="sxs-lookup"><span data-stu-id="a24f5-260">When using self-signed certificates, import the certificate to your Personal certificate store and the Trusted Root Certification Authorities certificate store.</span></span></li>
</ul>
<br/><span data-ttu-id="a24f5-261">Cuando envíe la solicitud de certificado de producción a su entidad de certificación, proporcione las siguientes propiedades del certificado:</span><span class="sxs-lookup"><span data-stu-id="a24f5-261">When sending the production certificate request to your certification authority, give the following certificate properties:</span></span>
<br/>

<ul>
<li><span data-ttu-id="a24f5-262"><strong>Uso mejorado de clave</strong>: como mínimo, Azure BizTalk Services requiere la autenticación de servidor.</span><span class="sxs-lookup"><span data-stu-id="a24f5-262"><strong>Enhanced Key Usage</strong>: At a minimum, Azure BizTalk Services requires Server Authentication.</span></span></li>
<li><span data-ttu-id="a24f5-263"><strong>Nombre común</strong>: escriba el nombre de dominio completo (FQDN) de la dirección URL de Azure BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="a24f5-263"><strong>Common Name</strong>: Enter the fully qualified domain name (FQDN) of your Azure BizTalk Service URL.</span></span> <span data-ttu-id="a24f5-264">Consulte <a HREF="#CreateService">Crear un servicio de BizTalk</a> en este artículo.</span><span class="sxs-lookup"><span data-stu-id="a24f5-264">See <a HREF="#CreateService">Create a BizTalk Service</a> in this article.</span></span></li>
</ul>
<br/>
<span data-ttu-id="a24f5-265">Es posible agregar un certificado nuevo o distinto después de crear el servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="a24f5-265">A new or different certificate can be added after the BizTalk Service is created.</span></span>
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting to any location.--->



## <a name="hybrid-connections"></a><span data-ttu-id="a24f5-266">conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="a24f5-266">Hybrid Connections</span></span>
<span data-ttu-id="a24f5-267">Cuando cree un Servicio de BizTalk de Azure, la pestaña **Conexiones híbridas** estará disponible:</span><span class="sxs-lookup"><span data-stu-id="a24f5-267">When you create an Azure BizTalk Service, the **Hybrid Connections** tab is available:</span></span>

![Pestaña Conexiones híbridas][HybridConnectionTab]

<span data-ttu-id="a24f5-269">Las conexiones híbridas se usan para conectar un sitio web de Azure o un servicio móvil de Azure a cualquier recurso local que usa un puerto TCP estático, como SQL Server, MySQL, API web HTTP, Servicios móviles y la mayoría de los servicios web personalizados.</span><span class="sxs-lookup"><span data-stu-id="a24f5-269">Hybrid Connections are used to connect an Azure website or Azure mobile service to any on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, Mobile Services, and most custom Web Services.</span></span>  <span data-ttu-id="a24f5-270">Las conexiones híbridas y el servicio de adaptador de BizTalk son diferentes.</span><span class="sxs-lookup"><span data-stu-id="a24f5-270">Hybrid Connections and the BizTalk Adapter Service are different.</span></span> <span data-ttu-id="a24f5-271">El Servicio de adaptador de BizTalk se usa para conectar los Servicios de BizTalk de Azure a un sistema de línea de negocio (LOB) local.</span><span class="sxs-lookup"><span data-stu-id="a24f5-271">The BizTalk Adapter Service is used to connect Azure BizTalk Services to an on-premises Line of Business (LOB) system.</span></span>

 <span data-ttu-id="a24f5-272">Vea [Conexiones híbridas](integration-hybrid-connection-overview.md) para obtener más información, incluida la creación y la administración de conexiones híbridas.</span><span class="sxs-lookup"><span data-stu-id="a24f5-272">See [Hybrid Connections](integration-hybrid-connection-overview.md) to learn more, including creating and managing Hybrid Connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a24f5-273">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a24f5-273">Next steps</span></span>
<span data-ttu-id="a24f5-274">Ahora que se crea un servicio de BizTalk, familiarícese con [Servicios de BizTalk: pestañas Panel, Monitor y Escala](biztalk-dashboard-monitor-scale-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="a24f5-274">Now that a BizTalk Service is created, familiarize yourself with the different [BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md).</span></span> <span data-ttu-id="a24f5-275">Su servicio de BizTalk está listo para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="a24f5-275">Your BizTalk Service is ready for your applications.</span></span> <span data-ttu-id="a24f5-276">Para comenzar a crear aplicaciones, vaya a [Servicios de BizTalk de Azure](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="a24f5-276">To start creating applications, go to [Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="a24f5-277">Consulte también</span><span class="sxs-lookup"><span data-stu-id="a24f5-277">See also</span></span>
* [<span data-ttu-id="a24f5-278">Servicios de BizTalk: Gráfico de ediciones</span><span class="sxs-lookup"><span data-stu-id="a24f5-278">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)<br/>
* [<span data-ttu-id="a24f5-279">BizTalk Services: gráfico de estado</span><span class="sxs-lookup"><span data-stu-id="a24f5-279">BizTalk Services: State Chart</span></span>](biztalk-service-state-chart.md)<br/>
* [<span data-ttu-id="a24f5-280">Servicios de BizTalk: copias de seguridad y restauración</span><span class="sxs-lookup"><span data-stu-id="a24f5-280">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)<br/>
* [<span data-ttu-id="a24f5-281">Servicios de BizTalk: limitaciones</span><span class="sxs-lookup"><span data-stu-id="a24f5-281">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)<br/>
* [<span data-ttu-id="a24f5-282">Servicios de BizTalk: nombre del emisor y clave del emisor</span><span class="sxs-lookup"><span data-stu-id="a24f5-282">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)<br/>
* [<span data-ttu-id="a24f5-283">¿Cómo puedo comenzar a utilizar el SDK de Servicios de BizTalk de Azure?</span><span class="sxs-lookup"><span data-stu-id="a24f5-283">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="a24f5-284">Conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="a24f5-284">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
