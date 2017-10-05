---
title: "Ampliación de las funcionalidades de nube a dispositivos de Windows 10 a través de Azure Active Directory Join | Microsoft Docs"
description: "Ofrece información general detallada acerca de cómo los dispositivos de Windows 10 pueden usar Azure AD Join para registrarse en Azure Active Directory."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 0cd4942f-7d54-474e-bd12-8e6764b0d42a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: d3a3d3efe1c43caff3b8d2956c14e8c90d05d22b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="extending-cloud-capabilities-to-windows-10-devices-through-azure-active-directory-join"></a><span data-ttu-id="196be-103">Ampliación de las capacidades de nube a dispositivos de Windows 10 a través de Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="196be-103">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>
## <a name="what-is-azure-active-directory-join"></a><span data-ttu-id="196be-104">¿Qué es Azure Active Directory Join?</span><span class="sxs-lookup"><span data-stu-id="196be-104">What is Azure Active Directory Join?</span></span>
<span data-ttu-id="196be-105">Azure Active Directory Join (Azure AD) es la funcionalidad que registra un dispositivo propiedad de la empresa en Azure Active Directory para permitir su administración centralizada.</span><span class="sxs-lookup"><span data-stu-id="196be-105">Azure Active Directory Join (Azure AD Join) is the functionality that registers a company-owned device in Azure Active Directory to enable centralized management of the device.</span></span> <span data-ttu-id="196be-106">Hace posible que los usuarios, como empleados y estudiantes, puedan conectarse a la nube de la empresa mediante Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="196be-106">It makes it possible for users such as employees and students to connect to the enterprise cloud through Azure Active Directory.</span></span> <span data-ttu-id="196be-107">Esto simplifica las implementaciones de Windows y el acceso a los recursos y las aplicaciones de la organización desde cualquier dispositivo de Windows, tanto propiedad de la empresa como personal (BYOD).</span><span class="sxs-lookup"><span data-stu-id="196be-107">This enables simplified Windows deployments and access to organizational apps and resources from any Windows device, both corporate-owned and personally-owned (BYOD).</span></span>

<span data-ttu-id="196be-108">Azure AD Join está pensado para empresas que es la primera vez que operan en la nube o que solo funcionan en ella, así como pequeñas y medianas empresas que carecen de una infraestructura de Windows Server Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="196be-108">Azure AD Join is intended for enterprises that are cloud-first/cloud-only--typically small- and medium-sized businesses that do not have an on-premises Windows Server Active Directory infrastructure.</span></span> <span data-ttu-id="196be-109">Dicho esto, las grandes organizaciones también pueden usar Azure AD Join en dispositivos que no pueden unirse a un dominio de la manera tradicional (por ejemplo, los dispositivos móviles) o para usuarios que necesitan principalmente acceso a Office 365 u otras aplicaciones SaaS integradas con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="196be-109">That said, Azure AD Join can and will also be used by large organizations on devices that are incapable of doing a traditional domain join (mobile devices, for example), or for users who primarily need to access Office 365 or other SaaS apps integrated with Azure AD.</span></span>

<span data-ttu-id="196be-110">Aunque la unión a un dominio de la manera tradicional aún proporciona la mejor experiencia local para los dispositivos que admiten la unión de dominios, Azure AD Join resulta adecuado para dispositivos que no la admiten.</span><span class="sxs-lookup"><span data-stu-id="196be-110">Although the traditional domain join still offers the best on-premises experience on devices that are capable of domain joining, Azure AD Join is suitable for devices that cannot domain join.</span></span> <span data-ttu-id="196be-111">Azure AD Join también es adecuado para la administración de usuarios en la nube.</span><span class="sxs-lookup"><span data-stu-id="196be-111">Azure AD Join is also suitable for managing users in the cloud.</span></span> <span data-ttu-id="196be-112">Lo hace mediante funcionalidades de administración de dispositivos móviles, en lugar de usar herramientas de administración de dominio tradicionales, como la directiva de grupo y System Center Configuration Manager (SCCM).</span><span class="sxs-lookup"><span data-stu-id="196be-112">It does so by using mobile device management capabilities instead of by using traditional domain management tools like Group Policy and System Center Configuration Manager (SCCM).</span></span>

![Información general de los dispositivos de la empresa y personales con un entorno de Active Directory y Azure AD local](./media/active-directory-azureadjoin/active-directory-azureadjoin-overview.png)

## <a name="why-should-enterprises-adopt-azure-ad-join"></a><span data-ttu-id="196be-114">¿Por qué las empresas deberían adoptar Azure AD Join?</span><span class="sxs-lookup"><span data-stu-id="196be-114">Why should enterprises adopt Azure AD Join?</span></span>
* <span data-ttu-id="196be-115">**Empresas que operan principalmente en la nube**: si ha pasado o va a pasar a un modelo en el que piensa reducir su superficie local y desea funcionar más en la nube, Azure AD Join puede resultarle ventajoso.</span><span class="sxs-lookup"><span data-stu-id="196be-115">**Businesses that are largely in the cloud**: If you have moved or are moving to a model in which you are reducing your on-premises footprint and want to operate more in the cloud, Azure AD Join could benefit you.</span></span> <span data-ttu-id="196be-116">Quizá ha creado cuentas de Azure AD manualmente o mediante la sincronización de su entorno de Active Directory local.</span><span class="sxs-lookup"><span data-stu-id="196be-116">Maybe you have created Azure AD accounts manually or through synchronizing your on-premises Active Directory.</span></span> <span data-ttu-id="196be-117">En cualquier caso, tiene una cuenta de Azure AD y puede usarla para iniciar sesión en Windows 10.</span><span class="sxs-lookup"><span data-stu-id="196be-117">Either way, you have an account in Azure AD, and you can use it to sign in to Windows 10.</span></span> <span data-ttu-id="196be-118">Los usuarios pueden unir sus equipos a Azure AD mediante la configuración rápida (OOBE) o mediante el menú Configuración.</span><span class="sxs-lookup"><span data-stu-id="196be-118">Your users can join their computers to Azure AD through either the out-of-box experience (OOBE) or through the Settings menu.</span></span> <span data-ttu-id="196be-119">Después de unirse, los usuarios disfrutarán de un acceso de inicio de sesión único (SSO) a recursos en la nube como Office 365, tanto en sus exploradores como en las aplicaciones de Office.</span><span class="sxs-lookup"><span data-stu-id="196be-119">After joining, users will enjoy single sign-on (SSO) access to cloud resources like Office 365, either in their browsers or in Office applications.</span></span>
* <span data-ttu-id="196be-120">**Instituciones educativas**: uno de los escenarios que nos suelen comentar es que las instituciones educativas tienen dos tipos de usuarios: profesores y estudiantes.</span><span class="sxs-lookup"><span data-stu-id="196be-120">**Educational institutions**: One of the scenarios we hear about often is that educational institutions have two user types: faculty and students.</span></span> <span data-ttu-id="196be-121">A los profesores se les considera miembros más a largo plazo de la organización, por lo que es deseable crear cuentas locales para ellos.</span><span class="sxs-lookup"><span data-stu-id="196be-121">Faculty members are considered longer-term members of the organization, so creating on-premises accounts for them is desirable.</span></span> <span data-ttu-id="196be-122">Sin embargo, los estudiantes son miembros de la organización a más corto plazo y, por tanto, se pueden administrar en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="196be-122">But students are shorter-term members of the organization and thus can be managed in Azure AD.</span></span> <span data-ttu-id="196be-123">Esto significa que la escala de directorio se puede trasladar a la nube, en lugar de almacenarse localmente.</span><span class="sxs-lookup"><span data-stu-id="196be-123">This means that directory scale can be pushed to the cloud instead of stored on-premises.</span></span> <span data-ttu-id="196be-124">También significa que los alumnos podrán iniciar sesión en Windows con sus cuentas de Azure AD y obtener acceso a los recursos de Office 365, en sus exploradores o en aplicaciones de Office.</span><span class="sxs-lookup"><span data-stu-id="196be-124">It also means that students can sign in to Windows with their Azure AD accounts and get access to Office 365 resources, either in their browsers or in Office applications.</span></span>
* <span data-ttu-id="196be-125">**Negocios minoristas**: otro escenario que nos suelen comentar es su deseo de simplificar la administración de los trabajadores estacionales.</span><span class="sxs-lookup"><span data-stu-id="196be-125">**Retail businesses**: Another scenario we’ve heard about from customers is their desire to manage seasonal workers more easily.</span></span>  <span data-ttu-id="196be-126">De nuevo, las cuentas para los empleados a jornada completa y a más largo plazo se suelen crear como cuentas locales en equipos unidos a un dominio.</span><span class="sxs-lookup"><span data-stu-id="196be-126">Again, accounts for longer-term, full-time employees are usually created as on-premises accounts on domain-joined machines.</span></span> <span data-ttu-id="196be-127">Sin embargo, los trabajadores estacionales son miembros a más corto plazo de la organización, por lo que es deseable administrar sus cuentas allí donde las licencias de usuario se puedan mover más fácilmente.</span><span class="sxs-lookup"><span data-stu-id="196be-127">But seasonal workers are shorter-term members of the org, so it's desirable to manage them where user licenses can be more easily moved around.</span></span> <span data-ttu-id="196be-128">La creación de estas cuentas de usuario en la nube con licencias de Office 365 permite a estos usuarios obtener los beneficios de iniciar sesión en aplicaciones de Windows y Office con una cuenta de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="196be-128">Creating these user accounts in the cloud with Office 365 licenses allows the users to get the benefits of signing in to Windows and Office applications with an Azure AD account.</span></span> <span data-ttu-id="196be-129">Además, se mantiene más flexibilidad con sus licencias una vez que abandonan su puesto de trabajo.</span><span class="sxs-lookup"><span data-stu-id="196be-129">Meanwhile, you maintain more flexibility with their licenses after they leave.</span></span>
* <span data-ttu-id="196be-130">**Otras empresas**: aunque mantenga a los usuarios en un entorno de Active Directory local, se puede beneficiar de tener a los usuarios unidos con Azure AD.</span><span class="sxs-lookup"><span data-stu-id="196be-130">**Other businesses**: Even though you maintain users in your on-premises Active Directory, you could still benefit from having users be Azure-AD-joined.</span></span> <span data-ttu-id="196be-131">Eso es porque Azure AD ofrece una experiencia de unión simplificada, la administración eficaz de dispositivos, la inscripción automática en la administración de dispositivos móviles y el inicio de sesión único a Azure AD y los recursos locales.</span><span class="sxs-lookup"><span data-stu-id="196be-131">That's because Azure AD offers a simplified joining experience, efficient device management, automatic mobile device management enrollment, and single sign-on capability for Azure AD and on-premises resources.</span></span>  

## <a name="what-capabilities-does-azure-ad-join-offer"></a><span data-ttu-id="196be-132">¿Qué funcionalidades ofrece Azure AD Join?</span><span class="sxs-lookup"><span data-stu-id="196be-132">What capabilities does Azure AD Join offer?</span></span>
<span data-ttu-id="196be-133">Con Azure AD Join, obtendrá lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="196be-133">With Azure AD Join, you get the following:</span></span>

* <span data-ttu-id="196be-134">**Aprovisionamiento automático de dispositivos de la empresa**: con Windows 10, los usuarios pueden configurar un dispositivo completamente nuevo de forma inmediata, sin necesidad de que intervenga el departamento de TI.</span><span class="sxs-lookup"><span data-stu-id="196be-134">**Self-provisioning of corporate-owned devices**: With Windows 10, users can configure a brand new, shrink-wrapped device in the out-of-box experience, without IT involvement.</span></span>
* <span data-ttu-id="196be-135">**Compatibilidad con factores de forma modernos**: Azure AD Join funciona en dispositivos que carecen de las funcionalidades tradicionales para unirse a un dominio.</span><span class="sxs-lookup"><span data-stu-id="196be-135">**Support for modern form factors**: Azure AD Join works on devices that don’t have the traditional domain join capabilities.</span></span>  
* <span data-ttu-id="196be-136">**Posibilidad de usar cuentas de organización existentes**: los usuarios ya no necesitan crear y mantener una cuenta de Microsoft personal para obtener la mejor experiencia en los dispositivos de la empresa, como hacían con Windows 8.</span><span class="sxs-lookup"><span data-stu-id="196be-136">**Support for existing organizational accounts**: Users no longer need to create and maintain a a personal Microsoft account to get the best experience on company-issued devices, as they did with Windows 8.</span></span> <span data-ttu-id="196be-137">Ahora, pueden usar sus cuentas profesionales existentes en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="196be-137">They can use their existing work accounts in Azure AD instead.</span></span> <span data-ttu-id="196be-138">Para muchas organizaciones, esto significa básicamente que los usuarios pueden configurar e iniciar sesión en Windows con las mismas credenciales que usan para acceder a Office 365.</span><span class="sxs-lookup"><span data-stu-id="196be-138">For many organizations, this basically means that users can set up and sign in to Windows with the same credentials that they use to access Office 365.</span></span>
* <span data-ttu-id="196be-139">**Inscripción automática en administración de dispositivos móviles**: los dispositivos se pueden inscribir automáticamente en la administración de dispositivos móviles cuando se conectan a Azure AD.</span><span class="sxs-lookup"><span data-stu-id="196be-139">**Automatic mobile device management  enrollment**: Devices can be automatically enrolled in mobile device management when connected to Azure AD.</span></span> <span data-ttu-id="196be-140">Este proceso funciona con soluciones de administración de dispositivos móviles de asociados y Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="196be-140">This process works with Microsoft Intune and partner mobile device management solutions.</span></span> <span data-ttu-id="196be-141">Cuando la administración de dispositivos se realiza con Intune, los administradores de TI pueden controlar y administrar los dispositivos unidos a Azure AD junto con los dispositivos unidos a un dominio en la consola de administración de SCCM.</span><span class="sxs-lookup"><span data-stu-id="196be-141">When device management is done with Intune, IT administrators can monitor/manage Azure AD-joined devices alongside domain-joined devices in the SCCM management console.</span></span>
* <span data-ttu-id="196be-142">**Inicio de sesión único en recursos de la empresa**: los usuarios disfrutan de un inicio de sesión único desde el escritorio de Windows en las aplicaciones y los recursos en la nube, como Office 365 y miles de aplicaciones empresariales que dependen de Azure AD para la autenticación mediante [Azure AD Connect](active-directory-azureadjoin-deployment-aadjoindirect.md).</span><span class="sxs-lookup"><span data-stu-id="196be-142">**Single sign-on to company resources**: Users enjoy single sign-on from the Windows desktop to apps and resources in the cloud, such as Office 365 and thousands of business applications that rely on Azure AD for authentication through [Azure AD Connect](active-directory-azureadjoin-deployment-aadjoindirect.md).</span></span> <span data-ttu-id="196be-143">Los dispositivos de la empresa que se han unido a Azure AD también disfrutarán de SSO a recursos locales cuando el dispositivo esté en la red corporativa, y desde cualquier lugar, cuando estos recursos se expongan a través del [proxy de la aplicación de Azure AD](https://msdn.microsoft.com/library/azure/Dn768219.aspx).</span><span class="sxs-lookup"><span data-stu-id="196be-143">Corporate-owned devices that are joined to Azure AD also enjoy SSO to on-premises resources when the device is on a corporate network, and from anywhere when these resources are exposed via the [Azure AD Application Proxy](https://msdn.microsoft.com/library/azure/Dn768219.aspx).</span></span>
* <span data-ttu-id="196be-144">**Movilidad de estado del SO**: la configuración de accesibilidad, los sitios web, las contraseñas Wi-Fi y otras opciones se sincronizarán en los dispositivos de la empresa sin necesidad de una cuenta de Microsoft personal.</span><span class="sxs-lookup"><span data-stu-id="196be-144">**OS State Roaming**: Accessibility settings, websites, Wi-Fi passwords, and other settings are synchronized across corporate-owned devices without requiring a personal Microsoft account.</span></span>
* <span data-ttu-id="196be-145">**Tienda Windows preparada para la empresa**: la Tienda Windows admite la adquisición de aplicaciones y licencias con cuentas de Azure AD.</span><span class="sxs-lookup"><span data-stu-id="196be-145">**Enterprise-ready Windows Store**: The Windows Store supports app acquisition and licensing with Azure AD accounts.</span></span> <span data-ttu-id="196be-146">Las organizaciones pueden adquirir aplicaciones de licencias por volumen y ponerlas a disposición de los usuarios de su organización.</span><span class="sxs-lookup"><span data-stu-id="196be-146">Organizations can volume-license apps and make them available to the users in their organization.</span></span>

## <a name="how-do-different-devices-work-with-azure-ad-join"></a><span data-ttu-id="196be-147">¿Cómo funcionan diferentes dispositivos con Azure AD Join?</span><span class="sxs-lookup"><span data-stu-id="196be-147">How do different devices work with Azure AD Join?</span></span>
| <span data-ttu-id="196be-148">Dispositivo de la empresa (unido a un dominio local)</span><span class="sxs-lookup"><span data-stu-id="196be-148">Corporate device (joined to on-premises domain)</span></span> | <span data-ttu-id="196be-149">Dispositivo de la empresa (unido a la nube)</span><span class="sxs-lookup"><span data-stu-id="196be-149">Corporate device  (joined to the cloud)</span></span> | <span data-ttu-id="196be-150">Dispositivo personal</span><span class="sxs-lookup"><span data-stu-id="196be-150">Personal device</span></span> |
| --- | --- | --- |
| <span data-ttu-id="196be-151">Los usuarios pueden iniciar sesión en Windows con las credenciales de trabajo (como lo hacen hoy).</span><span class="sxs-lookup"><span data-stu-id="196be-151">Users can sign into Windows with work credentials (as they do today).</span></span> |<span data-ttu-id="196be-152">Los usuarios pueden iniciar sesión en Windows con las credenciales de trabajo que se administran en Azure AD.</span><span class="sxs-lookup"><span data-stu-id="196be-152">Users can sign in to Windows with work credentials that are managed in Azure AD.</span></span> <span data-ttu-id="196be-153">Esto es importante para los dispositivos corporativos en tres casos:</span><span class="sxs-lookup"><span data-stu-id="196be-153">This is relevant for corporate devices in three cases:</span></span> <ol><li><span data-ttu-id="196be-154">La organización no tiene Active Directory local (por ejemplo, una pequeña empresa).</span><span class="sxs-lookup"><span data-stu-id="196be-154">The organization doesn’t have Active Directory on premises (for example, a small business).</span></span></li><li><span data-ttu-id="196be-155">La organización no crea todas las cuentas de usuario en Active Directory (por ejemplo, las cuentas de estudiantes, consultores o trabajadores estacionales no se crean en Active Directory).</span><span class="sxs-lookup"><span data-stu-id="196be-155">The organization doesn’t create all user accounts in Active Directory (for example, accounts for students, consultants, or seasonal workers are not created in Active Directory).</span></span></li><li><span data-ttu-id="196be-156">La organización tiene dispositivos de la empresa que no se pueden unir a un dominio (local), como los teléfonos o tabletas con una SKU móvil (por ejemplo, un dispositivo secundario llevado a una fábrica o tienda).</span><span class="sxs-lookup"><span data-stu-id="196be-156">The organization has corporate devices that can’t be joined to an (on-premises) domain, like phones or tablets running a Mobile SKU (for example, a secondary device taken to a factory/retail floor).</span></span></li></ol> <span data-ttu-id="196be-157">Azure AD Join permite unir dispositivos de la empresa para organizaciones administradas y federadas.</span><span class="sxs-lookup"><span data-stu-id="196be-157">Azure AD Join supports joining of corporate devices for both managed and federated organizations.</span></span> |<span data-ttu-id="196be-158">Los usuarios inician sesión en Windows con las credenciales de su cuenta de Microsoft personal (sin cambios).</span><span class="sxs-lookup"><span data-stu-id="196be-158">Users sign in to Windows with their personal Microsoft account credentials (no change).</span></span> |
| <span data-ttu-id="196be-159">Los usuarios tienen acceso a la configuración de movilidad y la tienda Windows de la empresa.</span><span class="sxs-lookup"><span data-stu-id="196be-159">Users have access to roaming settings and the enterprise Windows Store.</span></span> <span data-ttu-id="196be-160">Estos servicios funcionan con cuentas profesionales y no requieren una cuenta de Microsoft personal.</span><span class="sxs-lookup"><span data-stu-id="196be-160">These services work with work accounts and don't require a personal Microsoft account.</span></span> <span data-ttu-id="196be-161">Esto requiere que las organizaciones conecten su entorno de Active Directory local a Azure AD.</span><span class="sxs-lookup"><span data-stu-id="196be-161">This requires organizations to connect their on-premises Active Directory to Azure AD.</span></span> |<span data-ttu-id="196be-162">Los usuarios pueden hacer la configuración de autoservicio.</span><span class="sxs-lookup"><span data-stu-id="196be-162">Users can do self-service setup.</span></span> <span data-ttu-id="196be-163">Pueden realizar la configuración rápida (FRX) mediante su cuenta profesional como alternativa a que el departamento de TI realice el aprovisionamiento de los dispositivos, aunque se admiten ambos métodos.</span><span class="sxs-lookup"><span data-stu-id="196be-163">They can go through the first-run experience (FRX) via their work account as an alternative to having IT provision the devices, although both methods are supported.</span></span> |<span data-ttu-id="196be-164">Los usuarios pueden agregar fácilmente una cuenta profesional administrada en Active Directory o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="196be-164">Users can easily add a work account that’s managed in Active Directory or Azure AD.</span></span> |
| <span data-ttu-id="196be-165">Los usuarios tienen la capacidad de SSO desde el escritorio para aplicaciones profesionales, sitios web y recursos, incluidos recursos locales y aplicaciones en la nube que usan Azure AD para la autenticación.</span><span class="sxs-lookup"><span data-stu-id="196be-165">Users have SSO ability from the desktop to work apps, websites, and resources--including both on-premises resources and cloud apps that use Azure AD for authentication.</span></span> |<span data-ttu-id="196be-166">Automáticamente, los dispositivos se registran en el directorio de empresa (Azure AD) y se inscriben en administración de dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="196be-166">Devices are automatically registered in the enterprise directory (Azure AD) and automatically enrolled in mobile device management.</span></span> <span data-ttu-id="196be-167">(Característica de Azure AD Premium).</span><span class="sxs-lookup"><span data-stu-id="196be-167">(Azure AD Premium feature).</span></span> |<span data-ttu-id="196be-168">Los usuarios tienen capacidad de SSO en las aplicaciones, los sitios web y los recursos con esta cuenta profesional.</span><span class="sxs-lookup"><span data-stu-id="196be-168">Users have SSO ability across apps and to websites/resources with this work account.</span></span> |
| <span data-ttu-id="196be-169">Los usuarios pueden agregar sus cuentas de Microsoft personales para acceder a sus imágenes y archivos personales sin afectar a los datos de la empresa.</span><span class="sxs-lookup"><span data-stu-id="196be-169">Users can add their personal Microsoft accounts to access their personal pictures and files without impacting enterprise data.</span></span> <span data-ttu-id="196be-170">(La configuración de movilidad sigue funcionando con sus cuentas profesionales). La cuenta de Microsoft permite SSO y ya no controla la movilidad de la configuración.</span><span class="sxs-lookup"><span data-stu-id="196be-170">(Roaming settings continue to work with their work accounts.) The Microsoft account enables SSO and no longer drives the roaming of settings.</span></span> |<span data-ttu-id="196be-171">Los usuarios pueden usar el autoservicio de restablecimiento de contraseña (SSPR) en winlogon, lo que significa que pueden restablecer una contraseña olvidada.</span><span class="sxs-lookup"><span data-stu-id="196be-171">Users can do a self-service password reset (SSPR) on winlogon, meaning they can reset a forgotten password.</span></span> <span data-ttu-id="196be-172">(Característica de Azure AD Premium).</span><span class="sxs-lookup"><span data-stu-id="196be-172">(Azure AD Premium feature).</span></span> |<span data-ttu-id="196be-173">Los usuarios tienen acceso a la Tienda Windows de la empresa para adquirir y utilizar aplicaciones de línea de negocio en sus dispositivos personales.</span><span class="sxs-lookup"><span data-stu-id="196be-173">Users have access to the enterprise Windows Store so that they can acquire and use line-of-business apps on their personal devices.</span></span> |

## <a name="additional-information"></a><span data-ttu-id="196be-174">Información adicional</span><span class="sxs-lookup"><span data-stu-id="196be-174">Additional information</span></span>
* [<span data-ttu-id="196be-175">Windows 10 para la empresa: formas de usar dispositivos para trabajar</span><span class="sxs-lookup"><span data-stu-id="196be-175">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="196be-176">Ampliación de las capacidades de nube a dispositivos de Windows 10 a través de Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="196be-176">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="196be-177">Autenticación de identidades sin contraseñas a través de Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="196be-177">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="196be-178">Conozca los escenarios de uso de Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="196be-178">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="196be-179">Experiencias de conexión de dispositivos unidos a un dominio a Azure AD para Windows 10</span><span class="sxs-lookup"><span data-stu-id="196be-179">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="196be-180">Configuración de Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="196be-180">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)
