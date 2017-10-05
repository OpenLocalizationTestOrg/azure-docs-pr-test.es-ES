---
title: Uso del paquete de contenido de Power BI de Azure Active Directory | Microsoft Docs
description: Aprenda a usar el paquete de contenido de Power BI de Azure Active Directory.
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5c642bb814a279756e8391f12fdc86b6ec0b4a8f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-the-azure-active-directory-power-bi-content-pack"></a><span data-ttu-id="a68d3-103">Uso del paquete de contenido de Power BI de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a68d3-103">How to use the Azure Active Directory Power BI Content Pack</span></span>

<span data-ttu-id="a68d3-104">Comprender cómo los usuarios adoptan y usan las características de Azure Active Directory es fundamental para un administrador de TI.</span><span class="sxs-lookup"><span data-stu-id="a68d3-104">Understanding how your users adopt and use Azure Active Directory features is critical for you as an IT admin.</span></span> <span data-ttu-id="a68d3-105">Permite planear la infraestructura de TI y la comunicación para aumentar la utilización y sacar el máximo partido de las características de AAD.</span><span class="sxs-lookup"><span data-stu-id="a68d3-105">It allows you to plan your IT infrastructure and communication to increase usage and to get the most out of AAD features.</span></span> <span data-ttu-id="a68d3-106">El paquete de contenido de Power BI para Azure Active Directory ofrece la capacidad de analizar con mayor profundidad los datos para comprender cómo puede usarlos para recopilar información más completa sobre qué sucede con su entorno Azure Active Directory para las diversas funcionalidades de las que depende en gran medida.</span><span class="sxs-lookup"><span data-stu-id="a68d3-106">Power BI Content Pack for Azure Active Directory gives you the ability to further analyze your data to understand how you can use this data to gather richer insights into what’s going on with their Azure Active Directory for the various capabilities you heavily rely on.</span></span>  <span data-ttu-id="a68d3-107">Con la integración de las API de Azure Active Directory en Power BI, puede descargar fácilmente los paquetes de contenido pregenerados y obtener información sobre todas las actividades dentro de su entorno Azure Active Directory por medio de la completa experiencia de visualización que Power BI ofrece.</span><span class="sxs-lookup"><span data-stu-id="a68d3-107">With the integration of Azure Active Directory APIs into Power BI, you can easily download the pre-built content packs and gain insights to all the activities within your Azure Active Directory using rich visualization experience Power BI offers.</span></span> <span data-ttu-id="a68d3-108">Puede crear su propio panel y compartirlo fácilmente con cualquier persona de su organización.</span><span class="sxs-lookup"><span data-stu-id="a68d3-108">You can create your own dashboard and share it easily with anyone in your organization.</span></span> 

<span data-ttu-id="a68d3-109">En este tema se proporcionan instrucciones paso a paso para instalar y usar el paquete de contenido en su entorno.</span><span class="sxs-lookup"><span data-stu-id="a68d3-109">This topic provides you with step-by-step instructions on how to install and use the content pack in your environment.</span></span>

## <a name="installation"></a><span data-ttu-id="a68d3-110">Instalación</span><span class="sxs-lookup"><span data-stu-id="a68d3-110">Installation</span></span>  

<span data-ttu-id="a68d3-111">**Para instalar el paquete de contenido de Power BI:**</span><span class="sxs-lookup"><span data-stu-id="a68d3-111">**To install the Power BI Content Pack:**</span></span>

1. <span data-ttu-id="a68d3-112">Inicie sesión en [Power BI](https://app.powerbi.com/groups/me/getdata/services) con su cuenta de Power BI (es la misma que la de Office 365 o Azure AD).</span><span class="sxs-lookup"><span data-stu-id="a68d3-112">Log into [Power BI](https://app.powerbi.com/groups/me/getdata/services) with your Power BI Account (this is the same account as your O365 or Azure AD Account).</span></span>

2. <span data-ttu-id="a68d3-113">En la parte inferior del panel de navegación izquierdo, seleccione **Obtener datos**.</span><span class="sxs-lookup"><span data-stu-id="a68d3-113">At the bottom of the left navigation pane, select **Get Data**.</span></span>

    ![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/01.png)
 
3. <span data-ttu-id="a68d3-115">En el cuadro **Servicios**, haga clic en **Obtener**.</span><span class="sxs-lookup"><span data-stu-id="a68d3-115">In the **Services** box, click **Get**.</span></span>
   
    ![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/02.png)

4.  <span data-ttu-id="a68d3-117">Busque **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="a68d3-117">Search for **Azure Active Directory**.</span></span>

    ![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/03.png)
 
5.  <span data-ttu-id="a68d3-119">Cuando se le solicite, escriba su identificador de inquilino de Azure AD y haga clic en **Siguiente**.</span><span class="sxs-lookup"><span data-stu-id="a68d3-119">When prompted, type your Azure AD Tenant ID, and then click **Next**.</span></span>

    > [!TIP] 
    > <span data-ttu-id="a68d3-120">Una forma rápida de obtener el identificador del inquilino de Office 365 o Azure AD es iniciar sesión en el portal de Azure AD, profundizar en el directorio y copiar el identificador de la siguiente dirección URL: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ActiveDirectoryExtension/Directory/<tenantid>/directoryQuickStart</span><span class="sxs-lookup"><span data-stu-id="a68d3-120">A quick way to get the Tenant Id for your Office 365 / Azure AD tenant is to login to the Azure AD Portal, drill down to the directory and copy the ID from the following URL: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ActiveDirectoryExtension/Directory/<tenantid>/directoryQuickStart</span></span>

    ![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/04.png) 

6.  <span data-ttu-id="a68d3-122">Haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="a68d3-122">Click **Sign-in**.</span></span> 
 
    ![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/05.png) 



7.  <span data-ttu-id="a68d3-124">Escriba su nombre de usuario y contraseña, y haga clic en **Iniciar sesión**.</span><span class="sxs-lookup"><span data-stu-id="a68d3-124">Enter your username and password, and then click **Sign in**.</span></span>
 
    ![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/06.png) 

8.  <span data-ttu-id="a68d3-126">En el cuadro de diálogo de consentimiento de la aplicación, haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="a68d3-126">On the app consent dialog, click **Accept**.</span></span>
 
9.  <span data-ttu-id="a68d3-127">Cuando se haya creado el panel de registros de actividad de Azure Active Directory, haga clic en él.</span><span class="sxs-lookup"><span data-stu-id="a68d3-127">When your Azure Active Directory Activity logs dashboard has been created, click it.</span></span>
 
    ![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/08.png) 

## <a name="what-can-i-do-with-this-content-pack"></a><span data-ttu-id="a68d3-129">¿Qué puedo hacer con este paquete de contenido?</span><span class="sxs-lookup"><span data-stu-id="a68d3-129">What can I do with this content pack?</span></span>

<span data-ttu-id="a68d3-130">Antes de explicar qué puede hacer con este paquete de contenido, aquí tiene un breve resumen de los distintos informes que incluye el paquete de contenido.</span><span class="sxs-lookup"><span data-stu-id="a68d3-130">Before we jump into what you can do with this content pack, here’s quick preview of the various reports in the content pack.</span></span> <span data-ttu-id="a68d3-131">Los datos de los informes cubren los **últimos 30 días**.</span><span class="sxs-lookup"><span data-stu-id="a68d3-131">Report data goes back to the **last 30 days**.</span></span>

### <a name="reports-included-in-this-version-of-azure-active-directory-logs-content-pack"></a><span data-ttu-id="a68d3-132">Informes incluidos en esta versión del paquete de contenido de registros de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a68d3-132">Reports included in this version of Azure Active Directory logs Content Pack</span></span>

<span data-ttu-id="a68d3-133">**Informe de utilización y tendencias de aplicaciones**: obtenga información sobre las aplicaciones que se usan en su organización y cuáles se usan más y cuándo.</span><span class="sxs-lookup"><span data-stu-id="a68d3-133">**App Usage and Trend report**:  Get insights into the apps used in your organization and which ones are being used the most and when.</span></span> <span data-ttu-id="a68d3-134">Este informe se puede usar para recopilar información sobre cómo se usa una aplicación que acabe de implementar en su organización o para averiguar qué aplicaciones son populares.</span><span class="sxs-lookup"><span data-stu-id="a68d3-134">You can use this report to gather insights into how an app you recently rolled out in your organization is being used or find out which apps are popular.</span></span> <span data-ttu-id="a68d3-135">Al hacerlo, puede mejorar la utilización si ve si no se usa la aplicación.</span><span class="sxs-lookup"><span data-stu-id="a68d3-135">By doing this, you can improve usage if you see if the app is not being used.</span></span>

<span data-ttu-id="a68d3-136">**Inicios de sesión por ubicación y usuarios**: obtenga información sobre todos los inicios de sesión llevados a cabo con la identidad de Azure y sobre la identidad de los usuarios.</span><span class="sxs-lookup"><span data-stu-id="a68d3-136">**Sign-ins by location and users**: Get insights into all the sign-ins performed using Azure Identity and gives insights into the identity of the users.</span></span> <span data-ttu-id="a68d3-137">Con esto, puede profundizar en los inicios de sesión individuales y responder a preguntas como:</span><span class="sxs-lookup"><span data-stu-id="a68d3-137">With this, you can dig deeper into individual sign-ins and answer questions like:</span></span>

- <span data-ttu-id="a68d3-138">¿Desde dónde inició sesión este usuario?</span><span class="sxs-lookup"><span data-stu-id="a68d3-138">From where did this user sign-ins?</span></span>
- <span data-ttu-id="a68d3-139">¿Qué usuario tiene la mayor cantidad de inicios de sesión y desde dónde inicia sesión?</span><span class="sxs-lookup"><span data-stu-id="a68d3-139">Which user has the most sign-ins and where do they sign-in from?</span></span> 
- <span data-ttu-id="a68d3-140">¿Fue el inicio de sesión correcto?</span><span class="sxs-lookup"><span data-stu-id="a68d3-140">Was the sign-in successful?</span></span>  
 
<span data-ttu-id="a68d3-141">Para profundizar en los detalles, haga clic en una fecha o ubicación concretas.</span><span class="sxs-lookup"><span data-stu-id="a68d3-141">You can drill into details by clicking on a specific date or location.</span></span>

<span data-ttu-id="a68d3-142">**Usuarios únicos por aplicación**: obtenga una vista de todos los usuarios únicos de una aplicación determinada.</span><span class="sxs-lookup"><span data-stu-id="a68d3-142">**Unique users per app**:  Get a view of all unique users using a given app.</span></span> <span data-ttu-id="a68d3-143">Esto incluye solo los usuarios que hayan iniciado sesión "*correctamente*" en una aplicación.</span><span class="sxs-lookup"><span data-stu-id="a68d3-143">This includes only users who have “*successfully*” signed into an application.</span></span>

<span data-ttu-id="a68d3-144">**Inicios de sesión de dispositivo**: obtenga una vista del tipo de sistema operativo y los exploradores que los usuarios están utilizando en su organización con información detallada sobre los usuarios, lo que incluye:</span><span class="sxs-lookup"><span data-stu-id="a68d3-144">**Device sign-ins**: Get a view of the type of OS and browsers are being used by users in your organization with detailed information on the users including:</span></span>

- <span data-ttu-id="a68d3-145">User Name</span><span class="sxs-lookup"><span data-stu-id="a68d3-145">User Name</span></span>
- <span data-ttu-id="a68d3-146">Dirección IP</span><span class="sxs-lookup"><span data-stu-id="a68d3-146">IP Address</span></span>
- <span data-ttu-id="a68d3-147">Ubicación</span><span class="sxs-lookup"><span data-stu-id="a68d3-147">Location</span></span> 
- <span data-ttu-id="a68d3-148">Estado de inicio de sesión</span><span class="sxs-lookup"><span data-stu-id="a68d3-148">Sign-in status</span></span> 

<span data-ttu-id="a68d3-149">Con este informe, puede comprender los diversos perfiles de dispositivo usados dentro de su organización y determinar directivas de dispositivo en función de lo que se use.</span><span class="sxs-lookup"><span data-stu-id="a68d3-149">With this report, you can understand the various device profiles used within your organization and determine device policies based on what’s used</span></span>

<span data-ttu-id="a68d3-150">**Embudo de SSPR**: obtenga una descripción de cómo se llevan a cabo los restablecimientos de contraseña en su organización.</span><span class="sxs-lookup"><span data-stu-id="a68d3-150">**SSPR Funnel**: Get an understanding on how password resets are being done in your organization.</span></span> <span data-ttu-id="a68d3-151">Eche un vistazo a cuántos restablecimientos de contraseña se intentaron con la herramienta SSPR y cuántos se realizaron correctamente.</span><span class="sxs-lookup"><span data-stu-id="a68d3-151">Get a peek into how many password resets were attempted through the SSPR tool and how many of them were successful.</span></span> <span data-ttu-id="a68d3-152">Profundice más en los restablecimientos de contraseña con error mediante el embudo de SSPR y comprenda por qué se produjeron determinados errores.</span><span class="sxs-lookup"><span data-stu-id="a68d3-152">Dig deeper into the Password resets failure using the SSPR funnel and understand why certain failures occurred.</span></span> <span data-ttu-id="a68d3-153">Este informe ofrece una visión más detallada de cómo se usa la herramienta SSPR dentro de su organización para que pueda tomar las decisiones correctas.</span><span class="sxs-lookup"><span data-stu-id="a68d3-153">This report gives a deeper understanding of how the SSPR tool is used within your organization so you can make the right decisions.</span></span>

## <a name="customizing-azure-ad-activity-content-pack"></a><span data-ttu-id="a68d3-154">Personalización del paquete de contenido de actividad de Azure AD</span><span class="sxs-lookup"><span data-stu-id="a68d3-154">Customizing Azure AD Activity content pack</span></span>

<span data-ttu-id="a68d3-155">**Cambio de la visualización**: para cambiar la visualización de un informe, haga clic en **Editar informe** y seleccione la visualización que desee.</span><span class="sxs-lookup"><span data-stu-id="a68d3-155">**Change Visualization**:  You can change a report visualization by clicking **Edit Report** and select the visualization you want.</span></span>
 
![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/09.png) 
 
![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/10.png) 

<span data-ttu-id="a68d3-158">**Inclusión de campos adicionales**: puede agregar un campo al informe o quitarlo seleccionando el objeto visual que desea agregar o quitar en el campo.</span><span class="sxs-lookup"><span data-stu-id="a68d3-158">**Include additional fields**:  You can add a field to the report or remove it by selecting the visual to which you want to add/remove the field.</span></span> <span data-ttu-id="a68d3-159">En el ejemplo siguiente, se agrega el campo "Estado de inicio de sesión" a la vista de tabla.</span><span class="sxs-lookup"><span data-stu-id="a68d3-159">In the example below, I am adding “sign-in status” field to the table view.</span></span> 
 
![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/11.png) 

<span data-ttu-id="a68d3-161">**Anclado de visualizaciones al panel**: puede personalizar el panel e incluir sus propias visualizaciones en el informe y anclarlo al panel.</span><span class="sxs-lookup"><span data-stu-id="a68d3-161">**Pin visualizations to your dashboard**:  You can customize your dashboard and include your own visualizations to the report and pin it to the dashboard.</span></span> <span data-ttu-id="a68d3-162">En el ejemplo siguiente, se agrega un filtro nuevo denominado "Estado de inicio de sesión" y se incluye en el informe.</span><span class="sxs-lookup"><span data-stu-id="a68d3-162">In the example below, I added a new filter called “Sign-in Status” and included it in the report.</span></span> <span data-ttu-id="a68d3-163">También se cambia la visualización de gráfico de barras a gráfico de líneas y se puede anclar este nuevo objeto visual al panel.</span><span class="sxs-lookup"><span data-stu-id="a68d3-163">I also changed the visualization from bar chart to a line chart and can pin this new visual to the dashboard.</span></span>

![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/12.png) 

![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/13.png) 
 

 


<span data-ttu-id="a68d3-166">**Compartir su panel**: una vez que haya creado el contenido que desea, puede compartir el panel con los usuarios de su organización.</span><span class="sxs-lookup"><span data-stu-id="a68d3-166">**Sharing your dashboard**: Once you have created the content you want, you can share the dashboard with the users in your organization.</span></span> <span data-ttu-id="a68d3-167">Recuerde que, una vez que comparta el informe, pueden ver los campos que haya seleccionado en el informe.</span><span class="sxs-lookup"><span data-stu-id="a68d3-167">Please remember that once you share the report, they can see the fields you have selected in the report.</span></span>
 
![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/14.png) 



## <a name="scheduling-a-daily-refresh-of-your-power-bi-report"></a><span data-ttu-id="a68d3-169">Programación de una actualización diaria de su informe de Power BI</span><span class="sxs-lookup"><span data-stu-id="a68d3-169">Scheduling a daily refresh of your Power BI report</span></span>

<span data-ttu-id="a68d3-170">Para programar una actualización diaria de su informe de Power BI, vaya a **Conjuntos de datos > Configuración > Programar actualización** y configúrelo como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="a68d3-170">To schedule a daily refresh of your Power BI report, go to **Datasets > Settings > Schedule Refresh** and set it as shown below.</span></span>
 
![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/15.png) 

## <a name="updating-to-newer-version-of-content-pack"></a><span data-ttu-id="a68d3-172">Actualización a una versión más reciente del paquete de contenido</span><span class="sxs-lookup"><span data-stu-id="a68d3-172">Updating to newer version of content pack</span></span>

<span data-ttu-id="a68d3-173">Si desea actualizar el paquete de contenido para obtener una versión más reciente:</span><span class="sxs-lookup"><span data-stu-id="a68d3-173">If you want to update your content pack to get a newer version:</span></span>

- <span data-ttu-id="a68d3-174">Descargue el nuevo paquete de contenido y configúrelo según las instrucciones de este artículo.</span><span class="sxs-lookup"><span data-stu-id="a68d3-174">Download the new content pack and set it up as per instructions listed in this article.</span></span>

- <span data-ttu-id="a68d3-175">Una vez configurado, vaya a **Origen de datos > Configuración > Credenciales de origen de datos** y vuelva a escribir sus credenciales, tal y como se muestra a continuación.</span><span class="sxs-lookup"><span data-stu-id="a68d3-175">Once you have set it up, go to **Data Source > Settings > Data source credentials** and re-enter your credentials as shown below</span></span>

    ![Paquete de contenido de Power BI de Azure Active Directory](./media/active-directory-reporting-power-bi-content-pack-how-to/16.png) 

<span data-ttu-id="a68d3-177">Tan pronto como la nueva versión del paquete de contenido esté funcionando, puede quitar la versión anterior, si es necesario, eliminando los informes subyacentes y los conjuntos de datos asociados con ese paquete de contenido.</span><span class="sxs-lookup"><span data-stu-id="a68d3-177">As soon as the new version of the content pack is working, you can remove the old version if needed by deleting the underlying reports and datasets associated with that content pack.</span></span>

## <a name="still-having-issues"></a><span data-ttu-id="a68d3-178">¿Sigue teniendo problemas?</span><span class="sxs-lookup"><span data-stu-id="a68d3-178">Still having issues?</span></span> 

<span data-ttu-id="a68d3-179">Consulte nuestra [guía de solución de problemas](active-directory-reporting-troubleshoot-content-pack.md).</span><span class="sxs-lookup"><span data-stu-id="a68d3-179">Check out our [troubleshooting guide](active-directory-reporting-troubleshoot-content-pack.md).</span></span> <span data-ttu-id="a68d3-180">Para obtener ayuda general con Power BI, visite estos [artículos de Ayuda](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).</span><span class="sxs-lookup"><span data-stu-id="a68d3-180">For general help with Power BI, check out these [help articles](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).</span></span>
 

## <a name="next-steps"></a><span data-ttu-id="a68d3-181">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a68d3-181">Next steps</span></span>

<span data-ttu-id="a68d3-182">Para obtener información general sobre los informes, consulte [Informes de Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a68d3-182">For an overview of reporting, see the [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>
