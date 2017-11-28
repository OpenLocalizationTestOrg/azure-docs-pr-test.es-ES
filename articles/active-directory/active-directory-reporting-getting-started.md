---
title: "Introducción a los informes de Azure Active Directory | Microsoft Docs"
description: Listas de Hola varios informes disponibles en los informes de Azure Active Directory
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 7ac99919-8df5-4424-9298-fc7c025ba949
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: f47875708398391dd7f3efdc56a741fdba273b76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a><span data-ttu-id="181ba-103">Introducción a los informes de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="181ba-103">Getting started with Azure Active Directory Reporting</span></span>
## <a name="what-it-is"></a><span data-ttu-id="181ba-104">¿Qué es?</span><span class="sxs-lookup"><span data-stu-id="181ba-104">What it is</span></span>
<span data-ttu-id="181ba-105">Azure Active Directory (Azure AD) incluye informes de seguridad, actividad y auditoría para el directorio.</span><span class="sxs-lookup"><span data-stu-id="181ba-105">Azure Active Directory (Azure AD) includes security, activity, and audit reports for your directory.</span></span> <span data-ttu-id="181ba-106">Presentamos una lista de informes de hello incluidas:</span><span class="sxs-lookup"><span data-stu-id="181ba-106">Here's a list of hello reports included:</span></span>

### <a name="security-reports"></a><span data-ttu-id="181ba-107">Informes de seguridad</span><span class="sxs-lookup"><span data-stu-id="181ba-107">Security reports</span></span>
* <span data-ttu-id="181ba-108">Inicios de sesión desde orígenes desconocidos</span><span class="sxs-lookup"><span data-stu-id="181ba-108">Sign-ins from unknown sources</span></span>
* <span data-ttu-id="181ba-109">Inicios de sesión tras varios errores</span><span class="sxs-lookup"><span data-stu-id="181ba-109">Sign-ins after multiple failures</span></span>
* <span data-ttu-id="181ba-110">Inicios de sesión desde varias ubicaciones geográficas</span><span class="sxs-lookup"><span data-stu-id="181ba-110">Sign-ins from multiple geographies</span></span>
* <span data-ttu-id="181ba-111">Inicios de sesión desde direcciones IP con actividad sospechosa</span><span class="sxs-lookup"><span data-stu-id="181ba-111">Sign-ins from IP addresses with suspicious activity</span></span>
* <span data-ttu-id="181ba-112">Actividad de inicio de sesión irregular</span><span class="sxs-lookup"><span data-stu-id="181ba-112">Irregular sign-in activity</span></span>
* <span data-ttu-id="181ba-113">Inicios de sesión desde dispositivos posiblemente infectados</span><span class="sxs-lookup"><span data-stu-id="181ba-113">Sign-ins from possibly infected devices</span></span>
* <span data-ttu-id="181ba-114">Usuarios con actividad de inicio de sesión anómala</span><span class="sxs-lookup"><span data-stu-id="181ba-114">Users with anomalous sign-in activity</span></span>

### <a name="activity-reports"></a><span data-ttu-id="181ba-115">Informes de actividad</span><span class="sxs-lookup"><span data-stu-id="181ba-115">Activity reports</span></span>
* <span data-ttu-id="181ba-116">Uso de la aplicación: resumen</span><span class="sxs-lookup"><span data-stu-id="181ba-116">Application usage: summary</span></span>
* <span data-ttu-id="181ba-117">Uso de la aplicación: detallado</span><span class="sxs-lookup"><span data-stu-id="181ba-117">Application usage: detailed</span></span>
* <span data-ttu-id="181ba-118">Panel de la aplicación</span><span class="sxs-lookup"><span data-stu-id="181ba-118">Application dashboard</span></span>
* <span data-ttu-id="181ba-119">Errores de aprovisionamiento de cuentas</span><span class="sxs-lookup"><span data-stu-id="181ba-119">Account provisioning errors</span></span>
* <span data-ttu-id="181ba-120">Dispositivos de usuario individuales</span><span class="sxs-lookup"><span data-stu-id="181ba-120">Individual user devices</span></span>
* <span data-ttu-id="181ba-121">Actividad de usuario individual</span><span class="sxs-lookup"><span data-stu-id="181ba-121">Individual user Activity</span></span>
* <span data-ttu-id="181ba-122">Informe de actividad de grupos</span><span class="sxs-lookup"><span data-stu-id="181ba-122">Groups activity report</span></span>
* <span data-ttu-id="181ba-123">Informe de actividad de registro de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="181ba-123">Password Reset Registration Activity Report</span></span>
* <span data-ttu-id="181ba-124">Actividad de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="181ba-124">Password reset activity</span></span>

### <a name="audit-reports"></a><span data-ttu-id="181ba-125">Informes de auditoría</span><span class="sxs-lookup"><span data-stu-id="181ba-125">Audit reports</span></span>
* <span data-ttu-id="181ba-126">Informe de auditoría de directorio</span><span class="sxs-lookup"><span data-stu-id="181ba-126">Directory audit report</span></span>

> [!TIP]
> <span data-ttu-id="181ba-127">Para obtener más documentación sobre informes de Azure AD, vea [Visualización de los informes de acceso y uso](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="181ba-127">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="how-it-works"></a><span data-ttu-id="181ba-128">Cómo funciona</span><span class="sxs-lookup"><span data-stu-id="181ba-128">How it works</span></span>
### <a name="reporting-pipeline"></a><span data-ttu-id="181ba-129">Canalización de informes</span><span class="sxs-lookup"><span data-stu-id="181ba-129">Reporting pipeline</span></span>
<span data-ttu-id="181ba-130">canalización informes de Hello consta de tres pasos principales.</span><span class="sxs-lookup"><span data-stu-id="181ba-130">hello reporting pipeline consists of three main steps.</span></span> <span data-ttu-id="181ba-131">Cada vez que un usuario inicia sesión o se realiza una autenticación, ocurre lo siguiente de hello:</span><span class="sxs-lookup"><span data-stu-id="181ba-131">Every time a user signs in, or an authentication is made, hello following happens:</span></span>

* <span data-ttu-id="181ba-132">En primer lugar, se autentica el usuario de hello (correcta o incorrectamente) y Hola resultado se almacena en las bases de datos del servicio de Azure Active Directory de Hola.</span><span class="sxs-lookup"><span data-stu-id="181ba-132">First, hello user is authenticated (successfully or unsuccessfully), and hello result is stored in hello Azure Active Directory service databases.</span></span>
* <span data-ttu-id="181ba-133">En intervalos regulares, se procesan todos los inicios de sesión recientes.</span><span class="sxs-lookup"><span data-stu-id="181ba-133">At regular intervals, all recent sign ins are processed.</span></span> <span data-ttu-id="181ba-134">En este momento, la seguridad y los algoritmos de actividades anómalas buscan todos los inicios de sesión recientes en busca de actividad sospechosa.</span><span class="sxs-lookup"><span data-stu-id="181ba-134">At this point, our security and anomalous activity algorithms are searching all recent sign ins for suspicious activity.</span></span>
* <span data-ttu-id="181ba-135">Después del procesamiento, Hola informes anota, almacenado en memoria caché y sirve de hello portal de Azure clásico.</span><span class="sxs-lookup"><span data-stu-id="181ba-135">After processing, hello reports are written, cached, and served in hello Azure classic portal.</span></span>

### <a name="report-generation-times"></a><span data-ttu-id="181ba-136">Tiempos de generación de informes</span><span class="sxs-lookup"><span data-stu-id="181ba-136">Report generation times</span></span>
<span data-ttu-id="181ba-137">Pagar toohello gran volumen de autenticaciones y el inicio de sesión que inicios procesan por hello plataforma de Azure AD, hello más reciente inicios de sesión procesados son, por término medio, una hora anteriores.</span><span class="sxs-lookup"><span data-stu-id="181ba-137">Due toohello large volume of authentications and sign ins processed by hello Azure AD platform, hello most recent sign-ins processed are, on average, one hour old.</span></span> <span data-ttu-id="181ba-138">En raras ocasiones, puede llevar hasta too8 horas tooprocess hello más reciente inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="181ba-138">In rare cases, it may take up too8 hours tooprocess hello most recent sign-ins.</span></span>

<span data-ttu-id="181ba-139">Puede encontrar iniciar sesión más reciente de hello procesado mediante el examen de texto de Ayuda de hello en parte superior de Hola de cada informe.</span><span class="sxs-lookup"><span data-stu-id="181ba-139">You can find hello most recent processed sign-in by examining hello help text at hello top of each report.</span></span>

![Texto de ayuda en parte superior de Hola de cada informe](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> <span data-ttu-id="181ba-141">Para obtener más documentación sobre informes de Azure AD, vea [Visualización de los informes de acceso y uso](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="181ba-141">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="getting-started"></a><span data-ttu-id="181ba-142">Introducción</span><span class="sxs-lookup"><span data-stu-id="181ba-142">Getting started</span></span>
### <a name="sign-into-hello-azure-classic-portal"></a><span data-ttu-id="181ba-143">Inicie sesión en hello portal de Azure clásico</span><span class="sxs-lookup"><span data-stu-id="181ba-143">Sign into hello Azure classic portal</span></span>
<span data-ttu-id="181ba-144">En primer lugar, deberá toosign en hello [portal de Azure clásico](https://manage.windowsazure.com) como administrador global o de cumplimiento de normas.</span><span class="sxs-lookup"><span data-stu-id="181ba-144">First, you'll need toosign into hello [Azure classic portal](https://manage.windowsazure.com)  as a global or compliance administrator.</span></span> <span data-ttu-id="181ba-145">También debe ser un administrador de servicios de suscripción de Azure o Coadministrador o usar Hola "acceso tooAzure AD" suscripción de Azure.</span><span class="sxs-lookup"><span data-stu-id="181ba-145">You must also be an Azure subscription service administrator or co-administrator, or be using hello "Access tooAzure AD" Azure subscription.</span></span>

### <a name="navigate-tooreports"></a><span data-ttu-id="181ba-146">Navegue tooReports</span><span class="sxs-lookup"><span data-stu-id="181ba-146">Navigate tooReports</span></span>
<span data-ttu-id="181ba-147">tooview informes, navegue toohello ficha de informes en parte superior de Hola de su directorio.</span><span class="sxs-lookup"><span data-stu-id="181ba-147">tooview Reports, navigate toohello Reports tab at hello top of your directory.</span></span>

<span data-ttu-id="181ba-148">Si se trata de la primera vez que ver los informes de hello, necesitará cuadro de diálogo de tooagree tooa para poder ver los informes de Hola.</span><span class="sxs-lookup"><span data-stu-id="181ba-148">If this is your first time viewing hello reports, you'll need tooagree tooa dialog box before you can view hello reports.</span></span> <span data-ttu-id="181ba-149">Se trata de tooensure que es aceptable para que los administradores de su organización tooview estos datos, lo cual pueden considerarse información privada en algunos países.</span><span class="sxs-lookup"><span data-stu-id="181ba-149">This is tooensure that it's acceptable for admins in your organization tooview this data, which may be considered private information in some countries.</span></span>

![Cuadro de diálogo](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a><span data-ttu-id="181ba-151">Exploración de cada informe</span><span class="sxs-lookup"><span data-stu-id="181ba-151">Explore each report</span></span>
<span data-ttu-id="181ba-152">Navegue a cada informe toosee Hola de datos que se recopilan y procesan Hola inicios de sesión.</span><span class="sxs-lookup"><span data-stu-id="181ba-152">Navigate into each report toosee hello data being collected and hello sign-ins processed.</span></span> <span data-ttu-id="181ba-153">Puede encontrar un [lista de todos los informes de hello aquí](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="181ba-153">You can find a [list of all hello reports here](active-directory-reporting-guide.md).</span></span>

![Todos los informes](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-hello-reports-as-csv"></a><span data-ttu-id="181ba-155">Descargar informes de hello como CSV</span><span class="sxs-lookup"><span data-stu-id="181ba-155">Download hello reports as CSV</span></span>
<span data-ttu-id="181ba-156">Cada informe se puede descargar como un archivo CSV (valores separados por comas).</span><span class="sxs-lookup"><span data-stu-id="181ba-156">Each report can be downloaded as a CSV (comma-separated value) file.</span></span> <span data-ttu-id="181ba-157">Puede utilizar estos archivos en Excel, Power BI o programas toofurther analizar los datos de análisis de terceros.</span><span class="sxs-lookup"><span data-stu-id="181ba-157">You can use these files in Excel, PowerBI or third-party analysis programs toofurther analyze your data.</span></span>

<span data-ttu-id="181ba-158">toodownload cualquier informe como CSV, navegar por toohello informe y haga clic en "Descargar" en la parte inferior de Hola.</span><span class="sxs-lookup"><span data-stu-id="181ba-158">toodownload any report as a CSV, navigate toohello report and click "Download" at hello bottom.</span></span>

![Botón Descargar](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> <span data-ttu-id="181ba-160">Para obtener más documentación sobre informes de Azure AD, vea [Visualización de los informes de acceso y uso](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="181ba-160">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="181ba-161">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="181ba-161">Next steps</span></span>
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a><span data-ttu-id="181ba-162">Personalización de las alertas para la actividad de inicio de sesión anómala</span><span class="sxs-lookup"><span data-stu-id="181ba-162">Customize alerts for anomalous sign in activity</span></span>
<span data-ttu-id="181ba-163">Navegue toohello "Configurar" pestaña del directorio.</span><span class="sxs-lookup"><span data-stu-id="181ba-163">Navigate toohello "Configure" tab of your directory.</span></span>

<span data-ttu-id="181ba-164">Desplácese toohello sección de "Notificaciones".</span><span class="sxs-lookup"><span data-stu-id="181ba-164">Scroll toohello "Notifications" section.</span></span>

<span data-ttu-id="181ba-165">Habilitar o deshabilitar la sección "Notificaciones de correo electrónico de inicios de sesión anómalos" de Hola.</span><span class="sxs-lookup"><span data-stu-id="181ba-165">Enable or disable hello "Email Notifications of Anomalous sign-ins" section.</span></span>

![Hola sección notificaciones](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-hello-azure-ad-reporting-api"></a><span data-ttu-id="181ba-167">Integrar con hello API Reporting de Azure AD</span><span class="sxs-lookup"><span data-stu-id="181ba-167">Integrate with hello Azure AD Reporting API</span></span>
<span data-ttu-id="181ba-168">Vea [Introducción a Hola API Reporting](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="181ba-168">See [Getting started with hello Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

### <a name="engage-multi-factor-authentication-on-users"></a><span data-ttu-id="181ba-169">Uso de Multi-Factor Authentication en usuarios</span><span class="sxs-lookup"><span data-stu-id="181ba-169">Engage Multi-Factor Authentication on users</span></span>
<span data-ttu-id="181ba-170">Seleccione un usuario en un informe.</span><span class="sxs-lookup"><span data-stu-id="181ba-170">Select a user in a report.</span></span>

<span data-ttu-id="181ba-171">Haga clic en el botón de "Habilitar MFA" de hello en parte inferior de Hola de pantalla de bienvenida.</span><span class="sxs-lookup"><span data-stu-id="181ba-171">Click hello "Enable MFA" button at hello bottom of hello screen.</span></span>

![botón de la autenticación multifactor de Hello final Hola de pantalla de bienvenida](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> <span data-ttu-id="181ba-173">Para obtener más documentación sobre informes de Azure AD, vea [Visualización de los informes de acceso y uso](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="181ba-173">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

## <a name="learn-more"></a><span data-ttu-id="181ba-174">Más información</span><span class="sxs-lookup"><span data-stu-id="181ba-174">Learn more</span></span>
### <a name="audit-events"></a><span data-ttu-id="181ba-175">Eventos de auditoría</span><span class="sxs-lookup"><span data-stu-id="181ba-175">Audit events</span></span>
<span data-ttu-id="181ba-176">Obtenga información acerca de qué eventos se auditan en el directorio de hello en [Azure Active Directory informar de eventos de auditoría](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="181ba-176">Learn about what events are audited in hello directory in [Azure Active Directory Reporting Audit Events](active-directory-reporting-audit-events.md).</span></span>

### <a name="api-integration"></a><span data-ttu-id="181ba-177">Integración de la API</span><span class="sxs-lookup"><span data-stu-id="181ba-177">API Integration</span></span>
<span data-ttu-id="181ba-178">Vea [Introducción a Hola API Reporting](active-directory-reporting-api-getting-started.md) hello y [documentación de referencia de API](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span><span class="sxs-lookup"><span data-stu-id="181ba-178">See [Getting started with hello Reporting API](active-directory-reporting-api-getting-started.md) and hello [API reference documentation](https://msdn.microsoft.com/library/azure/mt126081.aspx).</span></span>

### <a name="get-in-touch"></a><span data-ttu-id="181ba-179">Ponerse en contacto</span><span class="sxs-lookup"><span data-stu-id="181ba-179">Get in touch</span></span>
<span data-ttu-id="181ba-180">Envíe un correo electrónico a [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) para trasmitir sus comentarios, solicitar ayuda o plantear las preguntas que tenga.</span><span class="sxs-lookup"><span data-stu-id="181ba-180">Email [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) for feedback, help, or any questions you might have.</span></span>

> [!TIP]
> <span data-ttu-id="181ba-181">Para obtener más documentación sobre informes de Azure AD, vea [Visualización de los informes de acceso y uso](active-directory-view-access-usage-reports.md).</span><span class="sxs-lookup"><span data-stu-id="181ba-181">For more documentation on Azure AD Reporting, check out [View your access and usage reports](active-directory-view-access-usage-reports.md).</span></span>
> 
> 

