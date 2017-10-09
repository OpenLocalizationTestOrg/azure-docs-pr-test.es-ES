---
title: "administración de toodevice aaaIntroduction en Azure Active Directory | Documentos de Microsoft"
description: "Obtenga información acerca de cómo la administración de dispositivos puede ayudarle tooget control sobre los dispositivos de Hola que tengan acceso a recursos en su entorno."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: e2fc0a3e8d00dc69cf01db9074e34427e396cfcf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toodevice-management-in-azure-active-directory"></a><span data-ttu-id="675a9-103">Administración de toodevice de introducción en Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="675a9-103">Introduction toodevice management in Azure Active Directory</span></span>

<span data-ttu-id="675a9-104">En un mundo móvil en primer lugar, basado en la nube, Azure Active Directory (Azure AD) permite toodevices de inicio de sesión único, las aplicaciones y servicios desde cualquier lugar.</span><span class="sxs-lookup"><span data-stu-id="675a9-104">In a mobile-first, cloud-first world, Azure Active Directory (Azure AD) enables single sign-on toodevices, apps, and services from anywhere.</span></span> <span data-ttu-id="675a9-105">Con la proliferación de Hola de dispositivos - incluidos Bring Your Own Device (BYOD), profesionales de TI se enfrentan dos objetivos opuestos:</span><span class="sxs-lookup"><span data-stu-id="675a9-105">With hello proliferation of devices - including Bring Your Own Device (BYOD), IT professionals are faced with two opposing goals:</span></span>

- <span data-ttu-id="675a9-106">Capacitar a toobe de los usuarios finales de hello productivo, donde y cuando</span><span class="sxs-lookup"><span data-stu-id="675a9-106">Empower hello end users toobe productive wherever and whenever</span></span>
- <span data-ttu-id="675a9-107">Proteger los activos corporativos hello en cualquier momento</span><span class="sxs-lookup"><span data-stu-id="675a9-107">Protect hello corporate assets at any time</span></span>

<span data-ttu-id="675a9-108">A través de dispositivos, los usuarios están obteniendo acceso tooyour los activos corporativos.</span><span class="sxs-lookup"><span data-stu-id="675a9-108">Through devices, your users are getting access tooyour corporate assets.</span></span> <span data-ttu-id="675a9-109">tooprotect los activos corporativos, como un administrador de TI, desea que un control toohave sobre estos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="675a9-109">tooprotect your corporate assets, as an IT administrator, you want toohave control over these devices.</span></span> <span data-ttu-id="675a9-110">Esto le permite toomake seguro de que los usuarios se obtiene acceso a los recursos desde dispositivos que cumplen los estándares de seguridad y cumplimiento de normas.</span><span class="sxs-lookup"><span data-stu-id="675a9-110">This enables you toomake sure that your users are accessing your resources from devices that meet your standards for security and compliance.</span></span> 

<span data-ttu-id="675a9-111">Administración de dispositivos también es base hello [acceso condicional basado en dispositivo](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="675a9-111">Device management is also hello foundation for [device-based conditional access](active-directory-conditional-access-policy-connected-applications.md).</span></span> <span data-ttu-id="675a9-112">Con el acceso condicional basado en dispositivos, puede asegurarse de que solo es posible con tooresources en su entorno de acceso de confianza para dispositivos.</span><span class="sxs-lookup"><span data-stu-id="675a9-112">With device-based conditional access, you can ensure that access tooresources in your environment is only possible with trusted devices.</span></span>   

<span data-ttu-id="675a9-113">En este tema se explica cómo funciona la administración de dispositivos en Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="675a9-113">This topic explains how device management in Azure Active Directory works.</span></span>

## <a name="getting-devices-under-hello-control-of-azure-ad"></a><span data-ttu-id="675a9-114">Dispositivos bajo el control de Hola de Azure AD</span><span class="sxs-lookup"><span data-stu-id="675a9-114">Getting devices under hello control of Azure AD</span></span>

<span data-ttu-id="675a9-115">tooget un dispositivo bajo el control de Hola de Azure AD, tienes dos opciones:</span><span class="sxs-lookup"><span data-stu-id="675a9-115">tooget a device under hello control of Azure AD, you have two options:</span></span>

- <span data-ttu-id="675a9-116">Registro</span><span class="sxs-lookup"><span data-stu-id="675a9-116">Registering</span></span> 
- <span data-ttu-id="675a9-117">Unión</span><span class="sxs-lookup"><span data-stu-id="675a9-117">Joining</span></span>

<span data-ttu-id="675a9-118">**Registrar** un tooAzure dispositivo AD permite toomanage identidad del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="675a9-118">**Registering** a device tooAzure AD enables you toomanage a device’s identity.</span></span> <span data-ttu-id="675a9-119">Cuando se registra un dispositivo, el registro de dispositivos de Azure AD proporciona dispositivo Hola con una identidad que es usado tooauthenticate Hola dispositivo cuando un usuario inicia sesión tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="675a9-119">When a device is registered, Azure AD device registration provides hello device with an identity that is used tooauthenticate hello device when a user signs-in tooAzure AD.</span></span> <span data-ttu-id="675a9-120">Puede usar Hola identidad tooenable o deshabilitar un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="675a9-120">You can use hello identity tooenable or disable a device.</span></span>

<span data-ttu-id="675a9-121">Cuando se combina con una solución de management(MDM) de dispositivos móviles como Microsoft Intune, los atributos de dispositivo de hello en Azure AD se actualizan con información adicional sobre el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="675a9-121">When combined with a mobile device management(MDM) solution such as Microsoft Intune, hello device attributes in Azure AD are updated with additional information about hello device.</span></span> <span data-ttu-id="675a9-122">Esto permite que las reglas de acceso condicional de toocreate que exijan el acceso desde dispositivos toomeet los estándares de seguridad y cumplimiento de normas.</span><span class="sxs-lookup"><span data-stu-id="675a9-122">This allows you toocreate conditional access rules that enforce access from devices toomeet your standards for security and compliance.</span></span> <span data-ttu-id="675a9-123">Para más información sobre la inscripción de dispositivos de Microsoft Intune, consulte el artículo sobre cómo inscribir dispositivos para su administración en Intune.</span><span class="sxs-lookup"><span data-stu-id="675a9-123">For more information on enrolling devices in Microsoft Intune, see Enroll devices for management in Intune .</span></span>

<span data-ttu-id="675a9-124">**Combinar** un dispositivo es un tooregistering de extensión un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="675a9-124">**Joining** a device is an extension tooregistering a device.</span></span> <span data-ttu-id="675a9-125">Esto significa, le proporciona todos los beneficios de Hola de registrar un dispositivo y en suma toothis, también cambia el estado local Hola de un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="675a9-125">This means, it provides you with all hello benefits of registering a device and in addition toothis, it also changes hello local state of a device.</span></span> <span data-ttu-id="675a9-126">Cambiar el estado local de hello permite que el dispositivo de toosign en tooa de los usuarios mediante una organización cuenta profesional o educativa en lugar de una cuenta personal.</span><span class="sxs-lookup"><span data-stu-id="675a9-126">Changing hello local state enables your users toosign-in tooa device using an organizational work or school account instead of a personal account.</span></span>

## <a name="azure-ad-registered-devices"></a><span data-ttu-id="675a9-127">Dispositivos registrados en Azure AD</span><span class="sxs-lookup"><span data-stu-id="675a9-127">Azure AD registered devices</span></span>   

<span data-ttu-id="675a9-128">objetivo de dispositivos de Azure AD registrado Hello es tooprovide con soporte para hello **Bring Your Own Device (BYOD)** escenario.</span><span class="sxs-lookup"><span data-stu-id="675a9-128">hello goal of Azure AD registered devices is tooprovide you with support for hello **Bring Your Own Device (BYOD)** scenario.</span></span> <span data-ttu-id="675a9-129">En este escenario, el usuario puede acceder a los recursos controlados de Azure Active Directory de su organización con un dispositivo personal.</span><span class="sxs-lookup"><span data-stu-id="675a9-129">In this scenario, a user can access your organization’s Azure Active Directory controlled resources using a personal device.</span></span>  

![Dispositivos registrados en Azure AD](./media/device-management-introduction/03.png)

<span data-ttu-id="675a9-131">acceso de Hola se basa en una cuenta profesional o educativa que se ha introducido en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="675a9-131">hello access is based on a work or school account that has been entered on hello device.</span></span>  
<span data-ttu-id="675a9-132">Por ejemplo, Windows 10 permite a los usuarios tooadd un trabajo o escuela cuenta tooa PC, Tablet PC o teléfono.</span><span class="sxs-lookup"><span data-stu-id="675a9-132">For example, Windows 10 enables users tooadd a work or school account tooa personal computer, tablet, or phone.</span></span>  
<span data-ttu-id="675a9-133">Cuando un usuario ha agregado un trabajo o la cuenta organizativa, el dispositivo Hola está registrado con Azure AD y opcionalmente inscritos en el sistema de administración (MDM) de dispositivo móvil de Hola que su organización ha configurado.</span><span class="sxs-lookup"><span data-stu-id="675a9-133">When a user has added a work or school account, hello device is registered with Azure AD and optionally enrolled in hello mobile device management (MDM) system that your organization has configured.</span></span> <span data-ttu-id="675a9-134">Los usuarios de su organización pueden agregar un trabajo o educativa cómodamente dispositivo personal tooa de cuenta:</span><span class="sxs-lookup"><span data-stu-id="675a9-134">Your organization’s users can add a work or school account tooa personal device conveniently:</span></span>

- <span data-ttu-id="675a9-135">Al obtener acceso a una aplicación de trabajo para hello es la primera vez</span><span class="sxs-lookup"><span data-stu-id="675a9-135">When accessing a work application for hello first time</span></span>
- <span data-ttu-id="675a9-136">Manualmente a través de hello **configuración** menú en caso de hello de Windows 10</span><span class="sxs-lookup"><span data-stu-id="675a9-136">Manually via hello **Settings** menu in hello case of Windows 10</span></span> 

<span data-ttu-id="675a9-137">Puede configurar dispositivos registrados en Azure AD para Windows 10, iOS, Android y macOS.</span><span class="sxs-lookup"><span data-stu-id="675a9-137">You can configure Azure AD registered devices for Windows 10, iOS, Android and macOS.</span></span>

## <a name="azure-ad-joined-devices"></a><span data-ttu-id="675a9-138">Dispositivos unidos a Azure AD</span><span class="sxs-lookup"><span data-stu-id="675a9-138">Azure AD joined devices</span></span>

<span data-ttu-id="675a9-139">objetivo de Hola de dispositivos de Azure AD Unido es toosimplify:</span><span class="sxs-lookup"><span data-stu-id="675a9-139">hello goal of Azure AD joined devices is toosimplify:</span></span>

- <span data-ttu-id="675a9-140">Las implementaciones de Windows de los dispositivos de trabajo</span><span class="sxs-lookup"><span data-stu-id="675a9-140">Windows deployments of work-owned devices</span></span> 
- <span data-ttu-id="675a9-141">Acceso tooorganizational aplicaciones y recursos desde cualquier dispositivo de Windows</span><span class="sxs-lookup"><span data-stu-id="675a9-141">Access tooorganizational apps and resources from any Windows device</span></span>

![Dispositivos registrados en Azure AD](./media/device-management-introduction/02.png)


<span data-ttu-id="675a9-143">Estos objetivos se llevan a cabo proporcionando a los usuarios una experiencia de autoservicio para dispositivos propiedad de trabajo bajo el control de Hola de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="675a9-143">These goals are accomplished by providing your users with a self-service experience for getting work-owned devices under hello control of Azure AD.</span></span>  
<span data-ttu-id="675a9-144">La **unión a Azure AD** está pensada para aquellas organizaciones en las que la nube es prioritaria y exclusiva.</span><span class="sxs-lookup"><span data-stu-id="675a9-144">**Azure AD Join** is intended for organizations that are cloud-first / cloud-only.</span></span> <span data-ttu-id="675a9-145">Son por lo general pequeñas y medianas empresas que carecen de una infraestructura de Windows Server Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="675a9-145">These are typically small- and medium-sized businesses that do not have an on-premises Windows Server Active Directory infrastructure.</span></span> 

<span data-ttu-id="675a9-146">Implementación de dispositivos de Azure AD unido le ofrece Hola siguientes ventajas:</span><span class="sxs-lookup"><span data-stu-id="675a9-146">Implementing Azure AD joined devices provides you with hello following benefits:</span></span>

- <span data-ttu-id="675a9-147">**Inicio de sesión único (SSO)** tooyour Azure administra servicios y aplicaciones SaaS.</span><span class="sxs-lookup"><span data-stu-id="675a9-147">**Single-Sign-On (SSO)** tooyour Azure managed SaaS apps and services.</span></span> <span data-ttu-id="675a9-148">Los usuarios no ven mensajes de autenticación adicionales al acceder a los recursos de trabajo.</span><span class="sxs-lookup"><span data-stu-id="675a9-148">Your users don’t see additional authentication prompts when accessing work resources.</span></span> <span data-ttu-id="675a9-149">Hola funcionalidad SSO es incluso cuando no están conectados toohello red de dominio disponible.</span><span class="sxs-lookup"><span data-stu-id="675a9-149">hello SSO functionality is even when they are not connected toohello domain network available.</span></span>

- <span data-ttu-id="675a9-150">**Itinerancia de las configuraciones de usuario** conforme a la empresa entre dispositivos unidos.</span><span class="sxs-lookup"><span data-stu-id="675a9-150">**Enterprise compliant roaming** of user settings across joined devices.</span></span> <span data-ttu-id="675a9-151">Los usuarios no tienen una configuración de toosee de la cuenta (por ejemplo, Hotmail) de Microsoft tooconnect en todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="675a9-151">Users don’t need tooconnect a Microsoft account (for example, Hotmail) toosee settings across devices.</span></span>

- <span data-ttu-id="675a9-152">**Acceso tooWindows tienda para empresas** con cuenta de AD.</span><span class="sxs-lookup"><span data-stu-id="675a9-152">**Access tooWindows Store for Business** using AD account.</span></span> <span data-ttu-id="675a9-153">Los usuarios pueden elegir entre un inventario de aplicaciones seleccionadas previamente por organización Hola.</span><span class="sxs-lookup"><span data-stu-id="675a9-153">Your users can choose from an inventory of applications pre-selected by hello organization.</span></span>

- <span data-ttu-id="675a9-154">**Windows Hello** compatibilidad para los recursos de toowork un acceso seguro y práctico.</span><span class="sxs-lookup"><span data-stu-id="675a9-154">**Windows Hello** support for secure and convenient access toowork resources.</span></span>

- <span data-ttu-id="675a9-155">**Restricción del acceso** tooapps de solo los dispositivos que cumplen las directivas de cumplimiento.</span><span class="sxs-lookup"><span data-stu-id="675a9-155">**Restriction of access** tooapps from only devices that meet compliance policy.</span></span>

<span data-ttu-id="675a9-156">Aunque la unión a Azure AD esté pensada principalmente para aquellas organizaciones que no tengan una infraestructura de Windows Server Active Directory local, sin duda se puede utilizar también en escenarios donde:</span><span class="sxs-lookup"><span data-stu-id="675a9-156">While Azure AD join is primarily intended for organizations that do not have an on-premises Windows Server Active Directory infrastructure, you can certainly also use it in scenarios where:</span></span>

- <span data-ttu-id="675a9-157">No puede usar una combinación de dominio local, por ejemplo, si necesita tooget dispositivos móviles como tabletas y teléfonos bajo control.</span><span class="sxs-lookup"><span data-stu-id="675a9-157">You can’t use an on-premises domain join, for example, if you need tooget mobile devices such as tablets and phones under control.</span></span>

- <span data-ttu-id="675a9-158">Los usuarios necesitan principalmente tooaccess Office 365 u otras aplicaciones de SaaS integradas con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="675a9-158">Your users primarily need tooaccess Office 365 or other SaaS apps integrated with Azure AD.</span></span>

- <span data-ttu-id="675a9-159">Desea toomanage un grupo de usuarios en Azure AD en lugar de en Active Directory.</span><span class="sxs-lookup"><span data-stu-id="675a9-159">You want toomanage a group of users in Azure AD instead of in Active Directory.</span></span> <span data-ttu-id="675a9-160">Puede aplicar, por ejemplo, los trabajadores tooseasonal, contratistas o estudiantes.</span><span class="sxs-lookup"><span data-stu-id="675a9-160">This can apply, for example, tooseasonal workers, contractors, or students.</span></span>

- <span data-ttu-id="675a9-161">Desea tooprovide unión capacidades tooworkers en oficinas de sucursales remotas con la infraestructura local limitada.</span><span class="sxs-lookup"><span data-stu-id="675a9-161">You want tooprovide joining capabilities tooworkers in remote branch offices with limited on-premises infrastructure.</span></span>

<span data-ttu-id="675a9-162">Puede configurar dispositivos unidos a Azure AD para dispositivos Windows 10.</span><span class="sxs-lookup"><span data-stu-id="675a9-162">You can configure Azure AD joined devices for Windows 10 devices.</span></span>


## <a name="hybrid-azure-ad-joined-devices"></a><span data-ttu-id="675a9-163">Dispositivos híbridos unidos a Azure AD</span><span class="sxs-lookup"><span data-stu-id="675a9-163">Hybrid Azure AD joined devices</span></span>

<span data-ttu-id="675a9-164">Para más de una década, muchas organizaciones han utilizado Hola dominio combinación tootheir local Active Directory tooenable:</span><span class="sxs-lookup"><span data-stu-id="675a9-164">For more than a decade, many organizations have used hello domain join tootheir on-premises Active Directory tooenable:</span></span>

- <span data-ttu-id="675a9-165">TI departamentos toomanage trabajo dispositivos corporativos desde una ubicación central.</span><span class="sxs-lookup"><span data-stu-id="675a9-165">IT departments toomanage work-owned devices from a central location.</span></span>

- <span data-ttu-id="675a9-166">Toosign de usuarios en los dispositivos tootheir con su Active Directory cuentas profesionales o educativas.</span><span class="sxs-lookup"><span data-stu-id="675a9-166">Users toosign in tootheir devices with their Active Directory work or school accounts.</span></span> 

<span data-ttu-id="675a9-167">Por lo general, las organizaciones con una superficie local dependen de dispositivos de tooprovision de métodos de imágenes y a menudo usan **System Center Configuration Manager (SCCM)** o **(GP) de directiva de grupo** toomanage ellos.</span><span class="sxs-lookup"><span data-stu-id="675a9-167">Typically, organizations with an on-premises footprint rely on imaging methods tooprovision devices, and they often use **System Center Configuration Manager (SCCM)** or **group policy (GP)** toomanage them.</span></span>

<span data-ttu-id="675a9-168">Si su entorno tiene un servidor local superficie de AD y también desea que aprovechan las capacidades de hello proporcionadas por Azure Active Directory, puede implementar dispositivos de Azure AD unido híbrida.</span><span class="sxs-lookup"><span data-stu-id="675a9-168">If your environment has an on-premises AD footprint and you also want benefit from hello capabilities provided by Azure Active Directory, you can implement hybrid Azure AD joined devices.</span></span> <span data-ttu-id="675a9-169">Se trata de dispositivos que son ambos, tooyour unido a Active Directory local y Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="675a9-169">These are devices that are both, joined tooyour on-premises Active Directory and your Azure Active Directory.</span></span>

![Dispositivos registrados en Azure AD](./media/device-management-introduction/01.png)


<span data-ttu-id="675a9-171">Debe usar dispositivos híbridos unidos a Azure AD si:</span><span class="sxs-lookup"><span data-stu-id="675a9-171">You should use Azure AD hybrid joined devices if:</span></span>

- <span data-ttu-id="675a9-172">Tiene dispositivos de implementada toothese de aplicaciones de Win32 que usan NTLM o Kerberos.</span><span class="sxs-lookup"><span data-stu-id="675a9-172">You have Win32 apps deployed toothese devices that use NTLM / Kerberos.</span></span>

- <span data-ttu-id="675a9-173">Necesita GP o SCCM / dispositivos de toomanage de DCM.</span><span class="sxs-lookup"><span data-stu-id="675a9-173">You require GP or SCCM / DCM toomanage devices.</span></span>

- <span data-ttu-id="675a9-174">Desea que los toocontinue toouse imágenes soluciones tooconfigure dispositivos para los empleados.</span><span class="sxs-lookup"><span data-stu-id="675a9-174">You want toocontinue toouse imaging solutions tooconfigure devices for your employees.</span></span>

<span data-ttu-id="675a9-175">Puede configurar dispositivos híbridos unidos a Azure AD para Windows 10 y dispositivos de nivel inferior como Windows 8 y Windows 7.</span><span class="sxs-lookup"><span data-stu-id="675a9-175">You can configure Hybrid Azure AD joined devices for Windows 10 and down-level devices such as Windows 8 and Windows 7.</span></span>

## <a name="summary"></a><span data-ttu-id="675a9-176">Resumen</span><span class="sxs-lookup"><span data-stu-id="675a9-176">Summary</span></span>

<span data-ttu-id="675a9-177">Con la administración de dispositivos en Azure AD, puede:</span><span class="sxs-lookup"><span data-stu-id="675a9-177">With device management in Azure AD, you can:</span></span> 

- <span data-ttu-id="675a9-178">Simplificar el proceso de Hola de someter a dispositivos de control de Hola de Azure AD</span><span class="sxs-lookup"><span data-stu-id="675a9-178">Simplify hello process of bringing devices under hello control of Azure AD</span></span>

- <span data-ttu-id="675a9-179">Proporcionar a los usuarios con toouse fácil acceso tooyour recursos de una organización basada en la nube</span><span class="sxs-lookup"><span data-stu-id="675a9-179">Provide your users with an easy toouse access tooyour organization’s cloud-based resources</span></span>

<span data-ttu-id="675a9-180">Como regla general, debe utilizar:</span><span class="sxs-lookup"><span data-stu-id="675a9-180">As a rule of a thumb, you should use:</span></span>

- <span data-ttu-id="675a9-181">Dispositivos registrados en Azure AD para dispositivos personales</span><span class="sxs-lookup"><span data-stu-id="675a9-181">Azure AD registered devices for personal devices</span></span>

- <span data-ttu-id="675a9-182">Azure AD unido dispositivos para dispositivos que no están unidos a un tooan AD local</span><span class="sxs-lookup"><span data-stu-id="675a9-182">Azure AD joined devices for devices that are not joined tooan on-premises AD</span></span> 

- <span data-ttu-id="675a9-183">Híbrido Azure AD unido dispositivos para dispositivos que están unidos a un tooan AD local</span><span class="sxs-lookup"><span data-stu-id="675a9-183">Hybrid Azure AD joined devices for devices that are joined tooan on-premises AD</span></span>     




## <a name="next-steps"></a><span data-ttu-id="675a9-184">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="675a9-184">Next steps</span></span>

- <span data-ttu-id="675a9-185">información general sobre cómo dispositivo toomanage en hello Azure portal, vea tooget [administrar los dispositivos con hello portal de Azure](device-management-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="675a9-185">tooget an overview of how toomanage device in hello Azure portal, see [managing devices using hello Azure portal](device-management-azure-portal.md)</span></span>

- <span data-ttu-id="675a9-186">toolearn más sobre el acceso condicional basado en dispositivos, consulte [configurar directivas de acceso condicional basado en dispositivos de Azure Active Directory](active-directory-conditional-access-policy-connected-applications.md).</span><span class="sxs-lookup"><span data-stu-id="675a9-186">toolearn more about device-based conditional access, see [configure Azure Active Directory device-based conditional access policies](active-directory-conditional-access-policy-connected-applications.md).</span></span>

- <span data-ttu-id="675a9-187">dispositivos de Azure AD unirse de toosetup híbrido, consulte [cómo tooconfigure híbrida Azure Active Directory dispositivos Unidos a un](device-management-hybrid-azuread-joined-devices-setup.md).</span><span class="sxs-lookup"><span data-stu-id="675a9-187">toosetup hybrid Azure AD joined devices, see [how tooconfigure hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md).</span></span>


