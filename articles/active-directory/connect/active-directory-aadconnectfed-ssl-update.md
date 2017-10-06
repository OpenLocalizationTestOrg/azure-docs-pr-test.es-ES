---
title: "Azure AD Connect: Certificado actualización Hola SSL para una granja de servidores de servicios de federación de Active Directory (AD FS) | Documentos de Microsoft"
description: Este documento detalles Hola pasos tooupdate Hola certificado SSL de una granja de AD FS mediante el uso de Azure AD Connect.
services: active-directory
keywords: "azure ad connect, actualizar ssl de adfs, actualizar certificado de adfs, cambiar certificado de adfs, nuevo certificado de adfs, certificado de adfs, actualizar certificado ssl de adfs, actualizar certificado ssl de adfs, configurar certificado ssl de adfs, adfs, ssl, certificado, certificado de comunicación de servicio de adfs, actualizar federación, configurar federación, aad connect"
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: bce7f75aab83b6abacb8472a6895054d137e10e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="update-hello-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a><span data-ttu-id="303ef-104">Actualiza el certificado SSL de Hola para una granja de servidores de servicios de federación de Active Directory (AD FS)</span><span class="sxs-lookup"><span data-stu-id="303ef-104">Update hello SSL certificate for an Active Directory Federation Services (AD FS) farm</span></span>

## <a name="overview"></a><span data-ttu-id="303ef-105">Información general</span><span class="sxs-lookup"><span data-stu-id="303ef-105">Overview</span></span>
<span data-ttu-id="303ef-106">Este artículo describe cómo se puede usar certificado SSL de Azure AD Connect tooupdate hello en una granja de servidores de servicios de federación de Active Directory (AD FS).</span><span class="sxs-lookup"><span data-stu-id="303ef-106">This article describes how you can use Azure AD Connect tooupdate hello SSL certificate for an Active Directory Federation Services (AD FS) farm.</span></span> <span data-ttu-id="303ef-107">Puede usar certificado de hello Azure AD Connect herramienta tooeasily actualización Hola SSL de granja de servidores de hello AD FS aunque Hola inicio de sesión en método de usuario seleccionado no está AD FS.</span><span class="sxs-lookup"><span data-stu-id="303ef-107">You can use hello Azure AD Connect tool tooeasily update hello SSL certificate for hello AD FS farm even if hello user sign-in method selected is not AD FS.</span></span>

<span data-ttu-id="303ef-108">Puede realizar toda la operación de actualización de certificado SSL para la granja de servidores de hello AD FS a través de todos los servidores de Proxy de aplicación Web (WAP) en tres pasos sencillos y federación hello:</span><span class="sxs-lookup"><span data-stu-id="303ef-108">You can perform hello whole operation of updating SSL certificate for hello AD FS farm across all federation and Web Application Proxy (WAP) servers in three simple steps:</span></span>

![Tres pasos](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
><span data-ttu-id="303ef-110">toolearn más información acerca de los certificados usados por AD FS, consulte [descripción de los certificados usados por AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span><span class="sxs-lookup"><span data-stu-id="303ef-110">toolearn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="303ef-111">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="303ef-111">Prerequisites</span></span>

* <span data-ttu-id="303ef-112">**Granja de AD FS**: asegúrese de que la granja de AD FS se base en Windows Server 2012 R2 o una versión posterior.</span><span class="sxs-lookup"><span data-stu-id="303ef-112">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span></span>
* <span data-ttu-id="303ef-113">**Azure AD Connect**: asegúrese de que Hola versión de Azure AD Connect es 1.1.443.0 o posterior.</span><span class="sxs-lookup"><span data-stu-id="303ef-113">**Azure AD Connect**: Ensure that hello version of Azure AD Connect is 1.1.443.0 or later.</span></span> <span data-ttu-id="303ef-114">Va a utilizar la tarea hello **actualización AD el certificado SSL FS**.</span><span class="sxs-lookup"><span data-stu-id="303ef-114">You'll use hello task **Update AD FS SSL certificate**.</span></span>

![Tarea de actualización de SSL](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a><span data-ttu-id="303ef-116">Paso 1: Proporcionar información de la granja de AD FS</span><span class="sxs-lookup"><span data-stu-id="303ef-116">Step 1: Provide AD FS farm information</span></span>

<span data-ttu-id="303ef-117">Azure AD Connect intenta automáticamente tooobtain información acerca de la granja de servidores de hello AD FS:</span><span class="sxs-lookup"><span data-stu-id="303ef-117">Azure AD Connect attempts tooobtain information about hello AD FS farm automatically by:</span></span>
1. <span data-ttu-id="303ef-118">Consultar información de la granja de servidores de Hola de AD FS (Windows Server 2016 o posterior).</span><span class="sxs-lookup"><span data-stu-id="303ef-118">Querying hello farm information from AD FS (Windows Server 2016 or later).</span></span>
2. <span data-ttu-id="303ef-119">Hacer referencia a información de Hola de ejecuciones anteriores, que se almacenan de forma local con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="303ef-119">Referencing hello information from previous runs, which are stored locally with Azure AD Connect.</span></span>

<span data-ttu-id="303ef-120">Puede modificar la lista de Hola de servidores que se muestran agregando o quitando hello tooreflect Hola actual configuración de servidores de granja de servidores de hello AD FS.</span><span class="sxs-lookup"><span data-stu-id="303ef-120">You can modify hello list of servers that are displayed by adding or removing hello servers tooreflect hello current configuration of hello AD FS farm.</span></span> <span data-ttu-id="303ef-121">Tan pronto como se proporciona la información del servidor hello, Azure AD Connect muestra conectividad de Hola y el estado de certificados SSL actual.</span><span class="sxs-lookup"><span data-stu-id="303ef-121">As soon as hello server information is provided, Azure AD Connect displays hello connectivity and current SSL certificate status.</span></span>

![Información del servidor de AD FS](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

<span data-ttu-id="303ef-123">Si la lista de hello contiene un servidor que ya no forma parte de la granja de servidores de hello AD FS, haga clic en **quitar** toodelete servidor de hello en lista de Hola de servidores en la granja de servidores de AD FS.</span><span class="sxs-lookup"><span data-stu-id="303ef-123">If hello list contains a server that's no longer part of hello AD FS farm, click **Remove** toodelete hello server from hello list of servers in your AD FS farm.</span></span>

![Servidor sin conexión en la lista](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> <span data-ttu-id="303ef-125">Quitar un servidor de la lista de Hola de servidores de AD FS de granja de servidores en Azure AD Connect es una operación local y las actualizaciones de Hola información de hello granja de AD FS que Azure AD Connect mantiene localmente.</span><span class="sxs-lookup"><span data-stu-id="303ef-125">Removing a server from hello list of servers for an AD FS farm in Azure AD Connect is a local operation and updates hello information for hello AD FS farm that Azure AD Connect maintains locally.</span></span> <span data-ttu-id="303ef-126">Azure AD Connect no modifica la configuración de hello en AD FS tooreflect Hola cambio.</span><span class="sxs-lookup"><span data-stu-id="303ef-126">Azure AD Connect doesn't modify hello configuration on AD FS tooreflect hello change.</span></span>    

## <a name="step-2-provide-a-new-ssl-certificate"></a><span data-ttu-id="303ef-127">Paso 2: Proporcionar el nuevo certificado SSL</span><span class="sxs-lookup"><span data-stu-id="303ef-127">Step 2: Provide a new SSL certificate</span></span>

<span data-ttu-id="303ef-128">Cuando haya confirmado información Hola acerca de los servidores de la granja de servidores de AD FS, Azure AD Connect solicita nuevo certificado SSL de Hola.</span><span class="sxs-lookup"><span data-stu-id="303ef-128">After you've confirmed hello information about AD FS farm servers, Azure AD Connect asks for hello new SSL certificate.</span></span> <span data-ttu-id="303ef-129">Proporcione una protección por contraseña PFX toocontinue Hola instalación del certificado.</span><span class="sxs-lookup"><span data-stu-id="303ef-129">Provide a password-protected PFX certificate toocontinue hello installation.</span></span>

![Certificado SSL](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

<span data-ttu-id="303ef-131">Después de proporcionar el certificado de hello, Azure AD Connect pasa por una serie de requisitos previos.</span><span class="sxs-lookup"><span data-stu-id="303ef-131">After you provide hello certificate, Azure AD Connect goes through a series of prerequisites.</span></span> <span data-ttu-id="303ef-132">Comprobar Hola certificado tooensure que Hola certificado es correcto para la granja de servidores de AD FS hello:</span><span class="sxs-lookup"><span data-stu-id="303ef-132">Verify hello certificate tooensure that hello certificate is correct for hello AD FS farm:</span></span>

-   <span data-ttu-id="303ef-133">Hello nombre de asunto de nombre/alternativo de sujeto de certificado de hello es Hola igual como nombre de servicio de federación de hello, o es un certificado comodín.</span><span class="sxs-lookup"><span data-stu-id="303ef-133">hello subject name/alternate subject name for hello certificate is either hello same as hello federation service name, or it's a wildcard certificate.</span></span>
-   <span data-ttu-id="303ef-134">certificado de Hello es válido durante más de 30 días.</span><span class="sxs-lookup"><span data-stu-id="303ef-134">hello certificate is valid for more than 30 days.</span></span>
-   <span data-ttu-id="303ef-135">cadena de confianza del certificado de Hello es válido.</span><span class="sxs-lookup"><span data-stu-id="303ef-135">hello certificate trust chain is valid.</span></span>
-   <span data-ttu-id="303ef-136">certificado de Hello está protegido con contraseña.</span><span class="sxs-lookup"><span data-stu-id="303ef-136">hello certificate is password protected.</span></span>

## <a name="step-3-select-servers-for-hello-update"></a><span data-ttu-id="303ef-137">Paso 3: Seleccione los servidores de actualización de Hola</span><span class="sxs-lookup"><span data-stu-id="303ef-137">Step 3: Select servers for hello update</span></span>

<span data-ttu-id="303ef-138">En el paso siguiente de hello, seleccione servidores de Hola que necesitan toohave Hola SSL certificado actualizado.</span><span class="sxs-lookup"><span data-stu-id="303ef-138">In hello next step, select hello servers that need toohave hello SSL certificate updated.</span></span> <span data-ttu-id="303ef-139">Actualización de hello no se puede seleccionar los servidores que están sin conexión.</span><span class="sxs-lookup"><span data-stu-id="303ef-139">Servers that are offline can't be selected for hello update.</span></span>

![Seleccione los servidores tooupdate](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

<span data-ttu-id="303ef-141">Después de completar la configuración de hello, Azure AD Connect muestra mensajes de Hola que indica el estado de saludo de la actualización de Hola y proporciona un inicio de sesión de AD FS hello tooverify de opción.</span><span class="sxs-lookup"><span data-stu-id="303ef-141">After you complete hello configuration, Azure AD Connect displays hello message that indicates hello status of hello update and provides an option tooverify hello AD FS sign-in.</span></span>

![Configuración completada](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a><span data-ttu-id="303ef-143">Preguntas más frecuentes</span><span class="sxs-lookup"><span data-stu-id="303ef-143">FAQs</span></span>

* <span data-ttu-id="303ef-144">**¿Qué debe ser el nombre de asunto Hola del certificado de Hola Hola nuevo certificado de SSL de AD FS?**</span><span class="sxs-lookup"><span data-stu-id="303ef-144">**What should be hello subject name of hello certificate for hello new AD FS SSL certificate?**</span></span>

    <span data-ttu-id="303ef-145">Azure AD Connect comprueba si Hola sujeto alternativo de nombre/nombre del firmante Hola certificado contiene nombre de servicio de federación de Hola.</span><span class="sxs-lookup"><span data-stu-id="303ef-145">Azure AD Connect checks if hello subject name/alternate subject name of hello certificate contains hello federation service name.</span></span> <span data-ttu-id="303ef-146">Por ejemplo, si el nombre de servicio de federación es fs.contoso.com, el nombre de sujeto alternativo/nombre de sujeto de hello debe ser fs.contoso.com.  También se aceptan certificados comodín.</span><span class="sxs-lookup"><span data-stu-id="303ef-146">For example, if your federation service name is fs.contoso.com, hello subject name/alternate subject name must be fs.contoso.com.  Wildcard certificates are also accepted.</span></span>

* <span data-ttu-id="303ef-147">**¿Por qué se me pide las credenciales de nuevo en la página del servidor WAP Hola?**</span><span class="sxs-lookup"><span data-stu-id="303ef-147">**Why am I asked for credentials again on hello WAP server page?**</span></span>

    <span data-ttu-id="303ef-148">Si las credenciales de Hola que proporcione para conectarse a servidores de FS tooAD también no tienen los servidores WAP Hola privilegio toomanage hello, Azure AD Connect pide las credenciales que tienen privilegios administrativos en los servidores WAP Hola.</span><span class="sxs-lookup"><span data-stu-id="303ef-148">If hello credentials you provide for connecting tooAD FS servers don't also have hello privilege toomanage hello WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on hello WAP servers.</span></span>

* <span data-ttu-id="303ef-149">**servidor de Hola se muestra como sin conexión. ¿qué debo hacer?**</span><span class="sxs-lookup"><span data-stu-id="303ef-149">**hello server is shown as offline. What should I do?**</span></span>

    <span data-ttu-id="303ef-150">Azure AD Connect no puede realizar cualquier operación si Hola servidor está sin conexión.</span><span class="sxs-lookup"><span data-stu-id="303ef-150">Azure AD Connect can't perform any operation if hello server is offline.</span></span> <span data-ttu-id="303ef-151">Si Hola servidor forma parte de hello granja de AD FS, a continuación, compruebe el servidor de toohello de conectividad de Hola.</span><span class="sxs-lookup"><span data-stu-id="303ef-151">If hello server is part of hello AD FS farm, then check hello connectivity toohello server.</span></span> <span data-ttu-id="303ef-152">Después de resolver el problema de hello, presione Hola actualizar icono tooupdate Hola estado Asistente Hola.</span><span class="sxs-lookup"><span data-stu-id="303ef-152">After you've resolved hello issue, press hello refresh icon tooupdate hello status in hello wizard.</span></span> <span data-ttu-id="303ef-153">Si el servidor de hello formaba parte de hello granja anteriormente pero ahora ya no existe, haga clic en **quitar** toodelete de lista de Hola de servidores que se conectan de Azure AD mantiene.</span><span class="sxs-lookup"><span data-stu-id="303ef-153">If hello server was part of hello farm earlier but now no longer exists, click **Remove** toodelete it from hello list of servers that Azure AD Connect maintains.</span></span> <span data-ttu-id="303ef-154">Quitar servidor hello en lista de hello en Azure AD Connect no altera Hola configuración de AD FS propio.</span><span class="sxs-lookup"><span data-stu-id="303ef-154">Removing hello server from hello list in Azure AD Connect doesn't alter hello AD FS configuration itself.</span></span> <span data-ttu-id="303ef-155">Si usa AD FS en Windows Server 2016 o posterior, sigue siendo de servidor hello en los valores de configuración de Hola y se mostrará nuevo hello vuela hello tarea se ejecuta.</span><span class="sxs-lookup"><span data-stu-id="303ef-155">If you're using AD FS in Windows Server 2016 or later, hello server remains in hello configuration settings and will be shown again hello next time hello task is run.</span></span>

* <span data-ttu-id="303ef-156">**¿Se puede actualizar un subconjunto de Mis servidores de granja de servidores con un certificado SSL nuevo Hola?**</span><span class="sxs-lookup"><span data-stu-id="303ef-156">**Can I update a subset of my farm servers with hello new SSL certificate?**</span></span>

    <span data-ttu-id="303ef-157">Sí.</span><span class="sxs-lookup"><span data-stu-id="303ef-157">Yes.</span></span> <span data-ttu-id="303ef-158">Siempre puede ejecutar la tarea hello **certificado SSL de actualización** nuevo Hola de tooupdate servidores restantes.</span><span class="sxs-lookup"><span data-stu-id="303ef-158">You can always run hello task **Update SSL Certificate** again tooupdate hello remaining servers.</span></span> <span data-ttu-id="303ef-159">En hello **actualización de certificados de servidores seleccionados para SSL** página, puede ordenar la lista Hola de servidores en **fecha de expiración de SSL** tooeasily acceder a servidores de Hola que aún no se actualizó.</span><span class="sxs-lookup"><span data-stu-id="303ef-159">On hello **Select servers for SSL certificate update** page, you can sort hello list of servers on **SSL Expiry date** tooeasily access hello servers that aren't updated yet.</span></span>

* <span data-ttu-id="303ef-160">**Quita servidor de Hola Hola anterior que se ejecuta, pero se sigue que se muestra como sin conexión y se muestra en la página de hello AD FS servidores. ¿Por qué es servidor de sin conexión de hello estando disponibles incluso después de que quitó?**</span><span class="sxs-lookup"><span data-stu-id="303ef-160">**I removed hello server in hello previous run, but it's still being shown as offline and listed on hello AD FS Servers page. Why is hello offline server still there even after I removed it?**</span></span>

    <span data-ttu-id="303ef-161">Quitar servidor hello en lista de hello en Azure AD Connect no quitarlo en hello configuración de AD FS.</span><span class="sxs-lookup"><span data-stu-id="303ef-161">Removing hello server from hello list in Azure AD Connect doesn't remove it in hello AD FS configuration.</span></span> <span data-ttu-id="303ef-162">AD FS (Windows Server 2016 o posterior) para toda la información acerca de la granja de servidores de hello hace referencia a Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="303ef-162">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about hello farm.</span></span> <span data-ttu-id="303ef-163">Si servidor hello sigue estando presente en hello configuración de AD FS, se enumerarán en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="303ef-163">If hello server is still present in hello AD FS configuration, it will be listed back in hello list.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="303ef-164">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="303ef-164">Next steps</span></span>

- [<span data-ttu-id="303ef-165">Azure AD Connect y la federación</span><span class="sxs-lookup"><span data-stu-id="303ef-165">Azure AD Connect and federation</span></span>](active-directory-aadconnectfed-whatis.md)
- [<span data-ttu-id="303ef-166">Servicios de federación de Active Directory y personalización con Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="303ef-166">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)
