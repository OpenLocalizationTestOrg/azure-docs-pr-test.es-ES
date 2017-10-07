---
title: aaaCreate servicios de BizTalk de Azure en hello portal de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo tooprovision o crear servicios de BizTalk de Azure en hello portal de Azure; MABS, WABS"
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
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a><span data-ttu-id="3dcbc-103">Crear servicios de BizTalk mediante Hola portal de Azure</span><span class="sxs-lookup"><span data-stu-id="3dcbc-103">Create BizTalk Services using hello Azure portal</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> <span data-ttu-id="3dcbc-104">toosign en toohello portal de Azure, necesitará una cuenta de Azure y suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-104">toosign in toohello Azure portal, you need an Azure account and Azure subscription.</span></span> <span data-ttu-id="3dcbc-105">En caso de no tener ninguna, puede crear una cuenta de evaluación gratuita en tan solo unos minutos.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-105">If you don't have an account, you can create a free trial account within a few minutes.</span></span> <span data-ttu-id="3dcbc-106">Consulte [Evaluación gratuita de Azure](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span><span class="sxs-lookup"><span data-stu-id="3dcbc-106">See [Azure Free Trial](http://go.microsoft.com/fwlink/p/?LinkID=239738).</span></span>


## <span data-ttu-id="3dcbc-107"><a name="CreateService"></a>Creación de un servicio de BizTalk</span><span class="sxs-lookup"><span data-stu-id="3dcbc-107"><a name="CreateService"></a>Create a BizTalk Service</span></span>
<span data-ttu-id="3dcbc-108">Función hello la edición que elija, no todas las configuraciones de BizTalk Service pueden estar disponibles.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-108">Depending on hello Edition you choose, not all BizTalk Service settings may be available.</span></span>

1. <span data-ttu-id="3dcbc-109">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="3dcbc-109">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="3dcbc-110">En el panel de navegación de la parte inferior de hello, seleccione **NEW**:</span><span class="sxs-lookup"><span data-stu-id="3dcbc-110">In hello bottom navigation pane, select **NEW**:</span></span>  
   <span data-ttu-id="3dcbc-111">![Seleccione el botón nuevo Hola][NEWButton]</span><span class="sxs-lookup"><span data-stu-id="3dcbc-111">![Select hello New button][NEWButton]</span></span>
3. <span data-ttu-id="3dcbc-112">Seleccione **APP SERVICES** > **SERVICIO DE BIZTALK** > **CREACIÓN PERSONALIZADA**:</span><span class="sxs-lookup"><span data-stu-id="3dcbc-112">Select **APP SERVICES** > **BIZTALK SERVICE** > **CUSTOM CREATE**:</span></span>  
   <span data-ttu-id="3dcbc-113">![Seleccione Servicio de BizTalk y seleccione Custom Create][NewBizTalkService]</span><span class="sxs-lookup"><span data-stu-id="3dcbc-113">![Select BizTalk Service and select Custom Create][NewBizTalkService]</span></span>
4. <span data-ttu-id="3dcbc-114">Escriba la configuración de servicio de BizTalk de hello:</span><span class="sxs-lookup"><span data-stu-id="3dcbc-114">Enter hello BizTalk Service settings:</span></span>
   
    <table border="1">
    <tr>
    <td><span data-ttu-id="3dcbc-115"><strong>Nombre del servicio de BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="3dcbc-115"><strong>BizTalk service name</strong></span></span></td>
    <td><span data-ttu-id="3dcbc-116">Puede escribir cualquier nombre pero sea específico.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-116">You can enter any name but be specific.</span></span> <span data-ttu-id="3dcbc-117">Estos son algunos ejemplos:</span><span class="sxs-lookup"><span data-stu-id="3dcbc-117">Some examples include:</span></span><br/><br/><span data-ttu-id="3dcbc-118">
    <em>mycompany</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="3dcbc-118">
    <em>mycompany</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="3dcbc-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="3dcbc-119">
    <em>mycompanymyapplication</em>.biztalk.windows.net</span></span><br/><span data-ttu-id="3dcbc-120">
    <em>myapplication</em>.biztalk.windows.net</span><span class="sxs-lookup"><span data-stu-id="3dcbc-120">
    <em>myapplication</em>.biztalk.windows.net</span></span><br/><br/><span data-ttu-id="3dcbc-121">". biztalk.windows.net" es nombre toohello agregadas automáticamente que especifique.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-121">".biztalk.windows.net" is automatically added toohello name you enter.</span></span> <span data-ttu-id="3dcbc-122">Esto crea una dirección URL que es usado tooaccess su BizTalk del servicio, como <strong>https://<em>myapplication</em>. biztalk.windows.net</strong>.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-122">This creates a URL that is used tooaccess your BizTalk Service, like <strong>https://<em>myapplication</em>.biztalk.windows.net</strong>.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="3dcbc-123"><strong>Edición</strong></span><span class="sxs-lookup"><span data-stu-id="3dcbc-123"><strong>Edition</strong></span></span></td>
    <td><span data-ttu-id="3dcbc-124">Si se encuentra en fase de pruebas y desarrollo de hello, elija <strong>Developer</strong>.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-124">If you are in hello testing/development phase, choose <strong>Developer</strong>.</span></span> <span data-ttu-id="3dcbc-125">Si se encuentra en fase de producción de hello, use hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">servicios de BizTalk: gráfico de ediciones</a> toodetermine si <strong>Premium</strong>, <strong>estándar</strong>, o <strong>Basic</strong>es Hola opción correcta para su escenario de negocio.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-125">If you are in hello production phase, use hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk Services: Editions Chart</a> toodetermine if <strong>Premium</strong>, <strong>Standard</strong>, or <strong>Basic</strong> is hello correct choice for your business scenario.</span></span>
    </td>
    </tr>
    <tr>
    <td><span data-ttu-id="3dcbc-126"><strong>Región</strong></span><span class="sxs-lookup"><span data-stu-id="3dcbc-126"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="3dcbc-127">Seleccione Hola región geográfica toohost su BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-127">Select hello geographic region toohost your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="3dcbc-128"><strong>URL de dominio</strong></span><span class="sxs-lookup"><span data-stu-id="3dcbc-128"><strong>Domain URL</strong></span></span></td>
    <td><span data-ttu-id="3dcbc-129"><strong>Opcional</strong>.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-129"><strong>Optional</strong>.</span></span> <span data-ttu-id="3dcbc-130">De forma predeterminada, es la dirección URL del dominio de Hola <em>YourBizTalkServiceName</em>. biztalk.windows.net.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-130">By default, hello domain URL is <em>YourBizTalkServiceName</em>.biztalk.windows.net.</span></span> <span data-ttu-id="3dcbc-131">También se puede escribir un dominio personalizado.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-131">A custom domain can also be entered.</span></span> <span data-ttu-id="3dcbc-132">Por ejemplo, si el dominio es <em>contoso</em>, puede escribir:</span><span class="sxs-lookup"><span data-stu-id="3dcbc-132">For example, if your domain is <em>contoso</em>, you can enter:</span></span> <br/><br/><span data-ttu-id="3dcbc-133">
    <em>MyCompany</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="3dcbc-133">
    <em>MyCompany</em>.contoso.com</span></span><br/><span data-ttu-id="3dcbc-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="3dcbc-134">
    <em>MyCompanyMyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="3dcbc-135">
    <em>MyApplication</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="3dcbc-135">
    <em>MyApplication</em>.contoso.com</span></span><br/><span data-ttu-id="3dcbc-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span><span class="sxs-lookup"><span data-stu-id="3dcbc-136">
    <em>YourBizTalkServiceName</em>.contoso.com</span></span><br/>
    </td>
    </tr>
    </table>
<span data-ttu-id="3dcbc-137">Seleccione la flecha siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-137">Select hello NEXT arrow.</span></span>
<span data-ttu-id="3dcbc-138">5.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-138">5.</span></span> <span data-ttu-id="3dcbc-139">Escriba Hola almacenamiento y la configuración de la base de datos:</span><span class="sxs-lookup"><span data-stu-id="3dcbc-139">Enter hello Storage and Database Settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="3dcbc-140"><strong>Cuenta de almacenamiento de supervisión y archivado</strong></span><span class="sxs-lookup"><span data-stu-id="3dcbc-140"><strong>Monitoring/Archiving storage account</strong></span></span></td>
    <td><span data-ttu-id="3dcbc-141">Seleccione una cuenta de almacenamiento existente o cree una nueva cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-141">Select an existing storage account or create a new storage account.</span></span> <br/><br/><span data-ttu-id="3dcbc-142">Si crea una nueva cuenta de almacenamiento, escriba Hola <strong>nombre de la cuenta de almacenamiento</strong>.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-142">If you create a new Storage account, enter hello <strong>Storage Account Name</strong>.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="3dcbc-143"><strong>Base de datos de seguimiento</strong></span><span class="sxs-lookup"><span data-stu-id="3dcbc-143"><strong>Tracking database</strong></span></span></td>
    <td><span data-ttu-id="3dcbc-144">Si usa una Base de datos SQL de Azure existente, no puede usarla otro Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-144">If you use an existing Azure SQL Database, it cannot be used by another BizTalk Service.</span></span> <span data-ttu-id="3dcbc-145">Necesita el nombre de inicio de sesión de Hola y la contraseña que especificó cuando se creó ese servidor de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-145">You need hello login name and password entered when that Azure SQL Database Server was created.</span></span><br/><br/><span data-ttu-id="3dcbc-146"><strong>Sugerencia</strong> crear base de datos de seguimiento de Hola y cuenta de almacenamiento de supervisión y archivado en Hola la misma región como Hola BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-146"><strong>TIP</strong> Create hello Tracking database and Monitoring/Archiving storage account in hello same region as hello BizTalk Service.</span></span></td>
    </tr>
    </table>
<span data-ttu-id="3dcbc-147">Seleccione la flecha siguiente Hola.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-147">Select hello NEXT arrow.</span></span>
<span data-ttu-id="3dcbc-148">6.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-148">6.</span></span> <span data-ttu-id="3dcbc-149">Escriba la configuración de la base de datos de hello:</span><span class="sxs-lookup"><span data-stu-id="3dcbc-149">Enter hello Database settings:</span></span>  <table border="1">
    <tr>
    <td><span data-ttu-id="3dcbc-150"><strong>Name</strong></span><span class="sxs-lookup"><span data-stu-id="3dcbc-150"><strong>Name</strong></span></span></td>
    <td><span data-ttu-id="3dcbc-151">Disponible cuando <strong>crear una nueva instancia de base de datos SQL</strong> está seleccionado en la pantalla de bienvenida anterior.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-151">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="3dcbc-152">Escriba un toobe de nombre de base de datos SQL utilizado por su BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-152">Enter a SQL Database name toobe used by your BizTalk Service.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="3dcbc-153"><strong>Servidor</strong></span><span class="sxs-lookup"><span data-stu-id="3dcbc-153"><strong>Server</strong></span></span></td>
    <td><span data-ttu-id="3dcbc-154">Disponible cuando <strong>crear una nueva instancia de base de datos SQL</strong> está seleccionado en la pantalla de bienvenida anterior.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-154">Available when <strong>Create a new SQL Database instance</strong> is selected in hello previous screen.</span></span>
    <br/><br/>
<span data-ttu-id="3dcbc-155">Seleccione un servidor de SQL Database existente o cree uno nuevo.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-155">Select an existing SQL Database Server or create a new SQL Database server.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="3dcbc-156"><strong>Nombre de inicio de sesión del servidor</strong></span><span class="sxs-lookup"><span data-stu-id="3dcbc-156"><strong>Server login name</strong></span></span></td>
    <td><span data-ttu-id="3dcbc-157">Escriba el nombre de usuario de inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-157">Enter hello login user name.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="3dcbc-158"><strong>Contraseña de inicio de sesión del servidor</strong></span><span class="sxs-lookup"><span data-stu-id="3dcbc-158"><strong>Server login password</strong></span></span></td>
    <td><span data-ttu-id="3dcbc-159">Escriba la contraseña de inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-159">Enter hello login password.</span></span></td>
    </tr>
    <tr>
    <td><span data-ttu-id="3dcbc-160"><strong>Región</strong></span><span class="sxs-lookup"><span data-stu-id="3dcbc-160"><strong>Region</strong></span></span></td>
    <td><span data-ttu-id="3dcbc-161">Disponible cuando se selecciona <strong>Crear una nueva instancia de SQL Database</strong>.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-161">Available when <strong>Create a new SQL Database instance</strong> is selected.</span></span> <span data-ttu-id="3dcbc-162">Seleccione toohost de región geográfica de hello en la base de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-162">Select hello geographic region toohost your SQL Database.</span></span></td>
    </tr>
    </table>

<span data-ttu-id="3dcbc-163">Seleccione a Hola marca de verificación toocomplete Hola asistente.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-163">Select hello check mark toocomplete hello wizard.</span></span> <span data-ttu-id="3dcbc-164">aparece el icono de progreso de Hello:</span><span class="sxs-lookup"><span data-stu-id="3dcbc-164">hello progress icon appears:</span></span>  
![El icono de progreso aparece cuando se completa][ProgressComplete]

<span data-ttu-id="3dcbc-166">Cuando haya finalizado, Hola servicio de BizTalk de Azure se haya creado y listo para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-166">When complete, hello Azure BizTalk Service is created and ready for your applications.</span></span> <span data-ttu-id="3dcbc-167">configuración predeterminada de Hello es suficientes.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-167">hello default settings are sufficient.</span></span> <span data-ttu-id="3dcbc-168">Si desea que la configuración predeterminada de toochange hello, seleccione **servicios de BIZTALK** en Hola panel de navegación izquierdo y, a continuación, seleccione su BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-168">If you want toochange hello default settings, select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span> <span data-ttu-id="3dcbc-169">Opciones de configuración adicionales se muestran en hello [pestañas panel, Monitor y escala](biztalk-dashboard-monitor-scale-tabs.md) en la parte superior de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-169">Additional settings are displayed in hello [Dashboard, Monitor, and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md) at hello top.</span></span>

<span data-ttu-id="3dcbc-170">Según el estado de Hola de hello BizTalk Service, hay algunas operaciones que no se puede completar.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-170">Depending on hello state of hello BizTalk Service, there are some operations that cannot be completed.</span></span> <span data-ttu-id="3dcbc-171">Para obtener una lista de estas operaciones, vaya demasiado[gráfico de estado de servicios de BizTalk](biztalk-service-state-chart.md).</span><span class="sxs-lookup"><span data-stu-id="3dcbc-171">For a list of these operations, go too[BizTalk Services State Chart](biztalk-service-state-chart.md).</span></span>

## <a name="post-provisioning-steps"></a><span data-ttu-id="3dcbc-172">Pasos posteriores al aprovisionamiento</span><span class="sxs-lookup"><span data-stu-id="3dcbc-172">Post-provisioning steps</span></span>
* [<span data-ttu-id="3dcbc-173">Instalar certificado de hello en un equipo local</span><span class="sxs-lookup"><span data-stu-id="3dcbc-173">Install hello certificate on a local computer</span></span>](#InstallCert)
* [<span data-ttu-id="3dcbc-174">Incorporación de un certificado listo para producción</span><span class="sxs-lookup"><span data-stu-id="3dcbc-174">Add a production-ready certificate</span></span>](#AddCert)
* [<span data-ttu-id="3dcbc-175">Obtener el espacio de nombres de Control de acceso de Hola</span><span class="sxs-lookup"><span data-stu-id="3dcbc-175">Get hello Access Control namespace</span></span>](#ACS)

#### <span data-ttu-id="3dcbc-176"><a name="InstallCert"></a>Instalar certificado de hello en un equipo local</span><span class="sxs-lookup"><span data-stu-id="3dcbc-176"><a name="InstallCert"></a>Install hello certificate on a local computer</span></span>
<span data-ttu-id="3dcbc-177">Como parte del aprovisionamiento del Servicio de BizTalk, se crea un certificado autofirmado y se asocia a su suscripción del Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-177">As part of BizTalk Service provisioning, a self-signed certificate is created and associated with your BizTalk Service subscription.</span></span> <span data-ttu-id="3dcbc-178">Debe descargar este certificado e instalarlo en los equipos desde donde se implemente aplicaciones de BizTalk Service o enviar mensajes tooa punto de conexión de BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-178">You must download this certificate and install it on computers from where you either deploy BizTalk Service applications or send messages tooa BizTalk Service endpoint.</span></span>

1. <span data-ttu-id="3dcbc-179">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="3dcbc-179">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="3dcbc-180">Seleccione **servicios de BIZTALK** en Hola panel de navegación izquierdo y, a continuación, seleccione la suscripción de BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-180">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service subscription.</span></span>
3. <span data-ttu-id="3dcbc-181">Seleccione hello **panel** ficha.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-181">Select hello **Dashboard** tab.</span></span>
4. <span data-ttu-id="3dcbc-182">Seleccione **Descargar certificado SSL**:</span><span class="sxs-lookup"><span data-stu-id="3dcbc-182">Select **Download SSL Certificate**:</span></span>  
   <span data-ttu-id="3dcbc-183">![Modificar certificado SSL][QuickGlance]</span><span class="sxs-lookup"><span data-stu-id="3dcbc-183">![Modify SSL Certificate][QuickGlance]</span></span>
5. <span data-ttu-id="3dcbc-184">Haga doble clic en el certificado de Hola y ejecutar mediante Hola Asistente tooinstall Hola de certificado.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-184">Double-click hello certificate and run through hello wizard tooinstall hello certificate.</span></span> <span data-ttu-id="3dcbc-185">Asegúrese de instalar el certificado de hello en hello **entidades emisoras de certificados raíz de confianza** almacenar.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-185">Make sure you install hello certificate under hello **Trusted Root Certificate Authorities** store.</span></span>

#### <span data-ttu-id="3dcbc-186"><a name="AddCert"></a>Incorporación de un certificado listo para producción</span><span class="sxs-lookup"><span data-stu-id="3dcbc-186"><a name="AddCert"></a>Add a production-ready certificate</span></span>
<span data-ttu-id="3dcbc-187">Hola certificado de firma automática que se crea automáticamente al crear servicios de BizTalk está diseñado para su uso en entornos de desarrollo únicamente.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-187">hello self-signed certificate that is automatically created when creating BizTalk Services is intended for use in development environments only.</span></span> <span data-ttu-id="3dcbc-188">Para escenarios de producción, reemplácelo por un certificado listo para producción.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-188">For production scenarios, replace it with a production-ready certificate.</span></span>

1. <span data-ttu-id="3dcbc-189">En hello **panel** ficha, seleccione **certificado SSL de actualización**.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-189">On hello **Dashboard** tab, select **Update SSL Certificate**.</span></span>
2. <span data-ttu-id="3dcbc-190">Examinar el certificado SSL de privado tooyour (*CertificateName*.pfx) que incluya el nombre de BizTalk Service, escriba la contraseña de hello y, a continuación, haga clic en la casilla de verificación Hola.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-190">Browse tooyour private SSL certificate (*CertificateName*.pfx) that includes your BizTalk Service name, enter hello password, and then click hello check mark.</span></span>

#### <span data-ttu-id="3dcbc-191"><a name="ACS"></a>Obtener el espacio de nombres de Control de acceso de Hola</span><span class="sxs-lookup"><span data-stu-id="3dcbc-191"><a name="ACS"></a>Get hello Access Control namespace</span></span>
1. <span data-ttu-id="3dcbc-192">Inicie sesión en toohello [portal de Azure](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="3dcbc-192">Sign in toohello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=213885).</span></span>
2. <span data-ttu-id="3dcbc-193">Seleccione **servicios de BIZTALK** en Hola panel de navegación izquierdo y, a continuación, seleccione su BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-193">Select **BIZTALK SERVICES** in hello left navigation pane, and then select your BizTalk Service.</span></span>
3. <span data-ttu-id="3dcbc-194">En la barra de tareas de hello, seleccione **información de conexión**:</span><span class="sxs-lookup"><span data-stu-id="3dcbc-194">In hello task bar, select **Connection Information**:</span></span>  
   <span data-ttu-id="3dcbc-195">![Seleccione Connection Information][ACSConnectInfo]</span><span class="sxs-lookup"><span data-stu-id="3dcbc-195">![Select Connection Information][ACSConnectInfo]</span></span>
4. <span data-ttu-id="3dcbc-196">Copiar valores de Control de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-196">Copy hello Access Control values.</span></span>

<span data-ttu-id="3dcbc-197">Cuando implementa un proyecto de servicio de BizTalk desde Visual Studio, debe escribir este espacio de nombres del servicio de control de acceso.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-197">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="3dcbc-198">espacio de nombres de Control de acceso de Hola se crea automáticamente para su BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-198">hello Access Control namespace is automatically created for your BizTalk Service.</span></span>

<span data-ttu-id="3dcbc-199">valores de Control de acceso de Hola se pueden usar con cualquier aplicación.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-199">hello Access Control values can be used with any application.</span></span> <span data-ttu-id="3dcbc-200">Cuando se crea el servicios de BizTalk de Azure, este espacio de nombres de Control de acceso controla la autenticación de hello con la implementación de BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-200">When Azure BizTalk Services is created, this Access Control namespace controls hello authentication with your BizTalk Service deployment.</span></span> <span data-ttu-id="3dcbc-201">Si desea toochange Hola suscripción o administrar el espacio de nombres de hello, seleccione **ACTIVE DIRECTORY** en Hola panel de navegación izquierdo y, a continuación, seleccione el espacio de nombres.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-201">If you want toochange hello subscription or manage hello namespace, select **ACTIVE DIRECTORY** in hello left navigation pane and then select your namespace.</span></span> <span data-ttu-id="3dcbc-202">barra de tareas de Hola enumera las opciones.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-202">hello task bar lists your options.</span></span>

<span data-ttu-id="3dcbc-203">Haga clic en **administrar** abre Hola Portal de administración de Control de acceso.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-203">Clicking **Manage** opens hello Access Control Management Portal.</span></span> <span data-ttu-id="3dcbc-204">En el Portal de administración de Control de acceso de hello, Hola usa BizTalk Service **identidades de servicio**:</span><span class="sxs-lookup"><span data-stu-id="3dcbc-204">In hello Access Control Management Portal, hello BizTalk Service uses **Service identities**:</span></span>  
<span data-ttu-id="3dcbc-205">![Identidades de servicio de ACS en hello Portal de administración de Control de acceso][ACSServiceIdentities]</span><span class="sxs-lookup"><span data-stu-id="3dcbc-205">![ACS Service Identities in hello Access Control Management Portal][ACSServiceIdentities]</span></span>

<span data-ttu-id="3dcbc-206">Hola identidad de servicio de Control de acceso es un conjunto de credenciales que permite que las aplicaciones o los clientes tooauthenticate directamente con el Control de acceso y recibir un token.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-206">hello Access Control service identity is a set of credentials that allow applications or clients tooauthenticate directly with Access Control and receive a token.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3dcbc-207">usa Hello BizTalk Service **propietario** para la identidad del servicio predeterminado Hola y Hola **contraseña** valor.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-207">hello BizTalk Service uses **Owner** for hello default service identity and hello **Password** value.</span></span> <span data-ttu-id="3dcbc-208">Si se usa el valor de clave simétrica de hello en lugar de hello valor de contraseña, hello siguiente error puede producirse.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-208">If you use hello Symmetric Key value instead of hello Password value, hello following error may occur.</span></span><br/><br/><span data-ttu-id="3dcbc-209">*No se pudo conectar la cuenta de servicio de administración de Control de acceso de toohello con hello especificada las credenciales*</span><span class="sxs-lookup"><span data-stu-id="3dcbc-209">*Could not connect toohello Access Control Management Service account with hello specified credentials*</span></span>
> 
> 

<span data-ttu-id="3dcbc-210">[Administración del espacio de nombres ACS](https://msdn.microsoft.com/library/azure/hh674478.aspx) muestra algunas directrices y recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-210">[Managing Your ACS Namespace](https://msdn.microsoft.com/library/azure/hh674478.aspx) lists some guidelines and recommendations.</span></span>

## <a name="requirements-explained"></a><span data-ttu-id="3dcbc-211">Requisitos explicados</span><span class="sxs-lookup"><span data-stu-id="3dcbc-211">Requirements explained</span></span>
<span data-ttu-id="3dcbc-212">Estos requisitos no aplican toohello edición gratuita.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-212">These requirements do not apply toohello Free Edition.</span></span>

<table border="1">
<tr bgcolor="FAF9F9">
        <td><span data-ttu-id="3dcbc-213"><strong>Lo que necesita</strong></span><span class="sxs-lookup"><span data-stu-id="3dcbc-213"><strong>What you need</strong></span></span></td>
        <td><span data-ttu-id="3dcbc-214"><strong>Por qué es necesario</strong></span><span class="sxs-lookup"><span data-stu-id="3dcbc-214"><strong>Why you need it</strong></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="3dcbc-215">Suscripción de Azure</span><span class="sxs-lookup"><span data-stu-id="3dcbc-215">Azure subscription</span></span></td>
<td><span data-ttu-id="3dcbc-216">suscripción de Hello determina quién puede iniciar sesión en toohello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-216">hello subscription determines who can sign in toohello Azure portal.</span></span> <span data-ttu-id="3dcbc-217">titular de la cuenta de Hello crea la suscripción de hello en <a HREF="https://account.windowsazure.com/Subscriptions"> suscripciones de Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-217">hello Account holder creates hello subscription at <a HREF="https://account.windowsazure.com/Subscriptions"> Azure Subscriptions</a>.</span></span>
<br/><br/>
<span data-ttu-id="3dcbc-218">Hola cuenta de Azure puede tener varias suscripciones y puede administrarse por alguien que se permite.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-218">hello Azure account can have multiple subscriptions and can be managed by anyone who is permitted.</span></span> <span data-ttu-id="3dcbc-219">Por ejemplo, el titular de la cuenta de Azure crea una suscripción denominada <em>BizTalkServiceSubscription</em> y proporciona Hola administradores de BizTalk dentro de su empresa (por ejemplo, ContosoBTSAdmins@live.com) tener acceso a toothis suscripción.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-219">For example, your Azure account holder creates a subscription named <em>BizTalkServiceSubscription</em> and gives hello BizTalk Administrators within your company (for example, ContosoBTSAdmins@live.com) access toothis subscription.</span></span> <span data-ttu-id="3dcbc-220">En este escenario, administradores de BizTalk Server Hola inicia sesión en toohello portal de Azure y tiene los servicios de hello hospedado tooall completos de administrador derechos en la suscripción de hello, incluidos los servicios de BizTalk de Azure.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-220">In this scenario, hello BizTalk Administrators sign in toohello Azure portal and have full Administrator rights tooall hello hosted services in hello subscription, including Azure BizTalk Services.</span></span> <span data-ttu-id="3dcbc-221">Administradores de BizTalk Server Hello no son titulares de la cuenta de Azure de hello y, por tanto, no tiene acceso a información de facturación de tooany.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-221">hello BizTalk Administrators are not hello Azure account holders and therefore don't have access tooany billing information.</span></span>
<br/><br/><span data-ttu-id="3dcbc-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">Administrar suscripciones y cuentas de almacenamiento en el portal de Azure hello</a> proporciona más información.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-222">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577"> Manage Subscriptions and Storage Accounts in hello Azure portal</a> provides more information.</span></span>
</td>
</tr>
<tr>
<td><span data-ttu-id="3dcbc-223">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="3dcbc-223">Azure SQL Database</span></span></td>
<td><span data-ttu-id="3dcbc-224">Almacena Hola tablas, vistas y procedimientos almacenados utilizados por BizTalk Service, incluidos los datos de seguimiento de Hola Hola.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-224">Stores hello tables, views, and stored procedures used by hello BizTalk Service, including hello Tracking data.</span></span>
<br/><br/>
<span data-ttu-id="3dcbc-225">Cuando cree un servicio de BizTalk, puede usar un servidor de Azure SQL Server existente, una Base de datos SQL de Azure existente, o bien puede crear automáticamente un servidor o una base de datos nuevos.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-225">When you create a BizTalk Service, you can use an existing Azure SQL Server, Azure SQL Database, or automatically create a new Server or Database.</span></span>
<br/><br/>
<span data-ttu-id="3dcbc-226">Hola escala de base de datos SQL se configura automáticamente.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-226">hello SQL Database scale is automatically configured.</span></span> <span data-ttu-id="3dcbc-227">Por lo general, la escala predeterminada de hello es suficiente para una BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-227">Typically, hello default scale is sufficient for a BizTalk Service.</span></span> <span data-ttu-id="3dcbc-228">Cambiar escala Hola afecta precios.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-228">Changing hello scale impacts pricing.</span></span> <span data-ttu-id="3dcbc-229">Consulte <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">Cuentas y facturación en Azure SQL Database</a>
</span><span class="sxs-lookup"><span data-stu-id="3dcbc-229">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930"> Accounts and Billing in Azure SQL Database</a>
</span></span><br/><br/><span data-ttu-id="3dcbc-230">
<strong>Notas</strong>
</span><span class="sxs-lookup"><span data-stu-id="3dcbc-230">
<strong>Notes</strong>
</span></span><br/>
<ul>
<li> <span data-ttu-id="3dcbc-231">Cuando crea una nueva Base de datos SQL o SQL Server de Azure, Servicios de Azure se habilita automáticamente.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-231">When you create a new Azure SQL Server and Database, Azure Services is automatically enabled.</span></span> <span data-ttu-id="3dcbc-232">Hola BizTalk Service requiere que los servicios de Azure habilitarse.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-232">hello BizTalk Service requires Azure Services be enabled.</span></span></li>
<li><span data-ttu-id="3dcbc-233">Si crea una nueva base de datos de SQL Azure en un servidor de SQL Azure existente, Hola reglas de firewall de hello Server no se cambian.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-233">If you create a new Azure SQL Database on an existing Azure SQL Server, hello firewall rules of hello Server are not changed.</span></span> <span data-ttu-id="3dcbc-234">Como resultado, es posible que otros servicios de Azure no se permiten las bases de datos del servidor de acceso toohello.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-234">As a result, it's possible other Azure Services are not allowed access toohello Server's databases.</span></span></li>
</ul>
</td>
</tr>
<tr>
<td><span data-ttu-id="3dcbc-235">Espacio de nombres del servicio de control de acceso de Azure</span><span class="sxs-lookup"><span data-stu-id="3dcbc-235">Azure Access Control namespace</span></span></td>
<td><span data-ttu-id="3dcbc-236">Autentica con los Servicios de BizTalk de Azure.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-236">Authenticates with Azure BizTalk Services.</span></span> <span data-ttu-id="3dcbc-237">Cuando implementa un proyecto de servicio de BizTalk desde Visual Studio, debe escribir este espacio de nombres del servicio de control de acceso.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-237">When you deploy a BizTalk Service project from Visual Studio, you enter this Access Control namespace.</span></span> <span data-ttu-id="3dcbc-238">Cuando se crea un BizTalk Service, se crea automáticamente el espacio de nombres de Control de acceso de Hola.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-238">When you create a BizTalk Service, hello Access Control namespace is automatically created.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="3dcbc-239">Cuenta de almacenamiento de Azure</span><span class="sxs-lookup"><span data-stu-id="3dcbc-239">Azure Storage account</span></span></td>
<td><span data-ttu-id="3dcbc-240">Proporciona acceso tootables, blobs y colas utilizadas por el texto siguiente Hola de BizTalk Service toosave:</span><span class="sxs-lookup"><span data-stu-id="3dcbc-240">Gives access tootables, blobs, and queues used by your BizTalk Service toosave hello following:</span></span>

<ul>
<li><span data-ttu-id="3dcbc-241">Los archivos de registro de ese Hola monitor BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-241">Log files that monitor hello BizTalk Service.</span></span> <span data-ttu-id="3dcbc-242">Hola supervisando resultados también se muestra en hello **supervisión** ficha Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-242">hello monitoring output is also displayed in hello **Monitoring** tab in hello Azure portal.</span></span></li>
<li><span data-ttu-id="3dcbc-243">Al crear un X12 o acuerdo de AS2 entre socios comerciales, puede habilitar propiedades de mensaje de Hola archivado características toostore.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-243">When creating an X12 or AS2 agreement between partners, you can enable hello Archiving feature toostore message properties.</span></span> <span data-ttu-id="3dcbc-244">Estos datos se guardan en hello cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-244">This data is saved in hello Storage account.</span></span></li>
</ul>
<br/>
<span data-ttu-id="3dcbc-245">Cuando crea un servicio de BizTalk, puede usar una cuenta de almacenamiento existente o puede crear automáticamente una nueva.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-245">When you create a BizTalk Service, you can use an existing Storage account or automatically create a new Storage account.</span></span>
<br/><br/>
<span data-ttu-id="3dcbc-246">configuración de almacenamiento predeterminada de Hello es suficientes para un BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-246">hello default Storage settings are sufficient for a BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="3dcbc-247">Cuando crea una cuenta de almacenamiento, se crean automáticamente una clave primaria y una clave secundaria.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-247">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="3dcbc-248">Estas claves controlan el acceso tooyour cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-248">These Keys control access tooyour Storage account.</span></span> <span data-ttu-id="3dcbc-249">Hola BizTalk Service usa automáticamente Hola Primary Key.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-249">hello BizTalk Service automatically uses hello Primary Key.</span></span>
<br/><br/>
<span data-ttu-id="3dcbc-250">Consulte <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">Almacenamiento</a> para más información.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-250">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671"> Storage</a> for more information.</span></span>
</td>
</tr>

<tr>
<td><span data-ttu-id="3dcbc-251">Certificado privado de SSL</span><span class="sxs-lookup"><span data-stu-id="3dcbc-251">SSL private certificate</span></span></td>
<td>
<span data-ttu-id="3dcbc-252">Cuando se crea un servicio de Azure BizTalk, también se crea una URL HTTPS que incluye su nombre de Servicio de BizTalk.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-252">When an Azure BizTalk Service is created, an HTTPS URL that includes your BizTalk Service name is also created.</span></span> <span data-ttu-id="3dcbc-253">Esta dirección URL es toouse configurada automáticamente un certificado autofirmado sólo del desarrollo.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-253">This URL is automatically configured toouse a self-signed development-only certificate.</span></span> <span data-ttu-id="3dcbc-254">Para producción, necesita un certificado SSL privado.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-254">For production, you need a private SSL certificate.</span></span>
<br/><br/><span data-ttu-id="3dcbc-255">
<strong>Información importante sobre el certificado SSL</strong>

</span><span class="sxs-lookup"><span data-stu-id="3dcbc-255">
<strong>Important SSL Certificate Information</strong>

</span></span><ul>
<li><span data-ttu-id="3dcbc-256">fecha de expiración del certificado de Hello debe ser inferior a 5 años.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-256">hello certificate expiration date must be less than 5 years.</span></span></li>
<li><span data-ttu-id="3dcbc-257">Todos los certificados privados requieren una contraseña.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-257">All private certificates require a password.</span></span> <span data-ttu-id="3dcbc-258">Apréndase esta contraseña y, como procedimiento recomendado, comparta esta contraseña con sus administradores.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-258">Know this password and as a best practice, share this password with your administrators.</span></span></li>
<li><span data-ttu-id="3dcbc-259">Los certificados autofirmados se utilizan en un entorno de prueba o de desarrollo.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-259">Self-signed certificates are used in a test/development environment.</span></span> <span data-ttu-id="3dcbc-260">Cuando se usan certificados autofirmados, importar el almacén de certificados personales de hello certificados tooyour y Hola almacén de certificados de entidades de certificación raíz de confianza.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-260">When using self-signed certificates, import hello certificate tooyour Personal certificate store and hello Trusted Root Certification Authorities certificate store.</span></span></li>
</ul>
<br/><span data-ttu-id="3dcbc-261">Cuando se envía la entidad de certificación de tooyour de solicitud certificado de producción de hello, dar Hola propiedades de certificado siguientes:</span><span class="sxs-lookup"><span data-stu-id="3dcbc-261">When sending hello production certificate request tooyour certification authority, give hello following certificate properties:</span></span>
<br/>

<ul>
<li><span data-ttu-id="3dcbc-262"><strong>Uso mejorado de clave</strong>: como mínimo, Azure BizTalk Services requiere la autenticación de servidor.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-262"><strong>Enhanced Key Usage</strong>: At a minimum, Azure BizTalk Services requires Server Authentication.</span></span></li>
<li><span data-ttu-id="3dcbc-263"><strong>Nombre común</strong>: escriba el nombre de dominio completo (FQDN) de Hola de su URL de servicio de BizTalk de Azure.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-263"><strong>Common Name</strong>: Enter hello fully qualified domain name (FQDN) of your Azure BizTalk Service URL.</span></span> <span data-ttu-id="3dcbc-264">Consulte <a HREF="#CreateService">Crear un servicio de BizTalk</a> en este artículo.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-264">See <a HREF="#CreateService">Create a BizTalk Service</a> in this article.</span></span></li>
</ul>
<br/>
<span data-ttu-id="3dcbc-265">Puede agregarse un certificado nuevo o diferente después de crea Hola BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-265">A new or different certificate can be added after hello BizTalk Service is created.</span></span>
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a><span data-ttu-id="3dcbc-266">conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="3dcbc-266">Hybrid Connections</span></span>
<span data-ttu-id="3dcbc-267">Cuando se crea un servicio de BizTalk de Azure, Hola **conexiones híbridas** pestaña está disponible:</span><span class="sxs-lookup"><span data-stu-id="3dcbc-267">When you create an Azure BizTalk Service, hello **Hybrid Connections** tab is available:</span></span>

![Pestaña Conexiones híbridas][HybridConnectionTab]

<span data-ttu-id="3dcbc-269">Las conexiones híbridas son tooconnect usado un Azure sitio Web o servicio móvil de Azure tooany local recursos que usa un puerto TCP estático, como SQL Server, MySQL, las API de Web HTTP, servicios móviles y mayoría de los servicios Web personalizados.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-269">Hybrid Connections are used tooconnect an Azure website or Azure mobile service tooany on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, Mobile Services, and most custom Web Services.</span></span>  <span data-ttu-id="3dcbc-270">Las conexiones híbridas y Hola servicio del adaptador de BizTalk son diferentes.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-270">Hybrid Connections and hello BizTalk Adapter Service are different.</span></span> <span data-ttu-id="3dcbc-271">Hola servicio del adaptador de BizTalk es el sistema de línea de negocio (LOB) de tooconnect usa servicios de BizTalk de Azure tooan local.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-271">hello BizTalk Adapter Service is used tooconnect Azure BizTalk Services tooan on-premises Line of Business (LOB) system.</span></span>

 <span data-ttu-id="3dcbc-272">Vea [conexiones híbridas](integration-hybrid-connection-overview.md) toolearn más, incluidas la creación y administración de conexiones híbridas.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-272">See [Hybrid Connections](integration-hybrid-connection-overview.md) toolearn more, including creating and managing Hybrid Connections.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3dcbc-273">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3dcbc-273">Next steps</span></span>
<span data-ttu-id="3dcbc-274">Ahora que se crea un BizTalk Service, familiarícese con hello diferentes [servicios de BizTalk: pestañas panel, Monitor y escala](biztalk-dashboard-monitor-scale-tabs.md).</span><span class="sxs-lookup"><span data-stu-id="3dcbc-274">Now that a BizTalk Service is created, familiarize yourself with hello different [BizTalk Services: Dashboard, Monitor and Scale tabs](biztalk-dashboard-monitor-scale-tabs.md).</span></span> <span data-ttu-id="3dcbc-275">Su servicio de BizTalk está listo para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="3dcbc-275">Your BizTalk Service is ready for your applications.</span></span> <span data-ttu-id="3dcbc-276">toostart crear aplicaciones, vaya demasiado[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span><span class="sxs-lookup"><span data-stu-id="3dcbc-276">toostart creating applications, go too[Azure BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=235197).</span></span>

## <a name="see-also"></a><span data-ttu-id="3dcbc-277">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="3dcbc-277">See also</span></span>
* [<span data-ttu-id="3dcbc-278">Servicios de BizTalk: Gráfico de ediciones</span><span class="sxs-lookup"><span data-stu-id="3dcbc-278">BizTalk Services: Editions Chart</span></span>](biztalk-editions-feature-chart.md)<br/>
* [<span data-ttu-id="3dcbc-279">BizTalk Services: gráfico de estado</span><span class="sxs-lookup"><span data-stu-id="3dcbc-279">BizTalk Services: State Chart</span></span>](biztalk-service-state-chart.md)<br/>
* [<span data-ttu-id="3dcbc-280">Servicios de BizTalk: copias de seguridad y restauración</span><span class="sxs-lookup"><span data-stu-id="3dcbc-280">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)<br/>
* [<span data-ttu-id="3dcbc-281">Servicios de BizTalk: limitaciones</span><span class="sxs-lookup"><span data-stu-id="3dcbc-281">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)<br/>
* [<span data-ttu-id="3dcbc-282">Servicios de BizTalk: nombre del emisor y clave del emisor</span><span class="sxs-lookup"><span data-stu-id="3dcbc-282">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)<br/>
* [<span data-ttu-id="3dcbc-283">¿Cómo puedo comenzar a utilizar Hola SDK de servicios de BizTalk de Azure</span><span class="sxs-lookup"><span data-stu-id="3dcbc-283">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [<span data-ttu-id="3dcbc-284">Conexiones híbridas</span><span class="sxs-lookup"><span data-stu-id="3dcbc-284">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
