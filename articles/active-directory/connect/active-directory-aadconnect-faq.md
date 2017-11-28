---
title: "Azure Active Directory Connect: Preguntas más frecuentes (P+F) | Microsoft Docs"
description: "Esta página contiene las preguntas más frecuentes sobre Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="7b2ae-103">Preguntas más frecuentes acerca de Azure Active Directory Connect</span><span class="sxs-lookup"><span data-stu-id="7b2ae-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="7b2ae-104">Instalación general</span><span class="sxs-lookup"><span data-stu-id="7b2ae-104">General installation</span></span>
<span data-ttu-id="7b2ae-105">**P: ¿instalación funcionará si Hola administrador Global de Azure AD tiene 2FA habilitado?**</span><span class="sxs-lookup"><span data-stu-id="7b2ae-105">**Q: Will installation work if hello Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="7b2ae-106">Con las compilaciones de Hola de febrero de 2016, esto se admite.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-106">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="7b2ae-107">**P: ¿existe una tooinstall de manera desatendida de Connect de Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="7b2ae-107">**Q: Is there a way tooinstall Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="7b2ae-108">Es sólo compatible tooinstall Azure AD Connect con el Asistente para la instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-108">It is only supported tooinstall Azure AD Connect using hello installation wizard.</span></span> <span data-ttu-id="7b2ae-109">No se admite la instalación silenciosa y desatendida.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="7b2ae-110">**P: Tengo un bosque en el que no se puede contactar con un dominio. ¿Cómo se puede instalar Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="7b2ae-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="7b2ae-111">Con las compilaciones de Hola de febrero de 2016, esto se admite.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-111">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="7b2ae-112">**P: ¿Hola trabajo de agente de mantenimiento de AD DS en server core?**</span><span class="sxs-lookup"><span data-stu-id="7b2ae-112">**Q: Does hello AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="7b2ae-113">Sí.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-113">Yes.</span></span> <span data-ttu-id="7b2ae-114">Después de instalar el agente de hello, puede completar el proceso de registro de hello mediante Hola siguiente cmdlet de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="7b2ae-114">After installing hello agent, you can complete hello registration process using hello following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="7b2ae-115">Red</span><span class="sxs-lookup"><span data-stu-id="7b2ae-115">Network</span></span>
<span data-ttu-id="7b2ae-116">**P: tengo un firewall, el dispositivo de red, o algo más que limita las conexiones de tiempo máximo de hello puede permanecer abierto en la red. ¿Cuál debería ser mi umbral de tiempo de espera del lado de cliente al usar Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="7b2ae-116">**Q: I have a firewall, network device, or something else that limits hello maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="7b2ae-117">Todo el software de red, dispositivos físicos o cualquier otra cosa que pueden permanecer abiertas las conexiones de tiempo máximo de hello debe usar un umbral de al menos 5 minutos (300 segundos) para la conectividad entre los límites Hola servidor hello Azure AD Connect cliente está instalado y Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-117">All networking software, physical devices, or anything else that limits hello maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between hello server where hello Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="7b2ae-118">Esto también aplica la herramienta de sincronización de Microsoft Identity tooall que anteriormente se publicó.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-118">This also applies tooall previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="7b2ae-119">**P: ¿Se admiten los dominios de una sola etiqueta (SLD)?**</span><span class="sxs-lookup"><span data-stu-id="7b2ae-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="7b2ae-120"> No, Azure AD Connect no admite bosques/dominios locales con dominios de una sola etiqueta.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="7b2ae-121">**P: ¿Se admiten los nombres de NetBios con puntos?**</span><span class="sxs-lookup"><span data-stu-id="7b2ae-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="7b2ae-122">No, Azure AD Connect no admite local bosques o dominios donde el nombre de NetBios de hello contiene un punto "." en nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-122">No, Azure AD Connect does not support on-premises forests/domains where hello NetBios name contains a period "." in hello name.</span></span>

## <a name="federation"></a><span data-ttu-id="7b2ae-123">Federación</span><span class="sxs-lookup"><span data-stu-id="7b2ae-123">Federation</span></span>
<span data-ttu-id="7b2ae-124">**P: ¿qué debo hacer si se recibe un correo electrónico que me pide toorenew mi certificado de Office 365**</span><span class="sxs-lookup"><span data-stu-id="7b2ae-124">**Q: What do I do if I receive an email that asking me toorenew my Office 365 certificate**</span></span>  
<span data-ttu-id="7b2ae-125">Utilizar la Guía de hello descrito en hello [renovar certificados](active-directory-aadconnect-o365-certs.md) tema acerca de cómo toorenew Hola certificado.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-125">Use hello guidance that is outlined in hello [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how toorenew hello certificate.</span></span>

<span data-ttu-id="7b2ae-126">**P.: Tengo establecido Actualizar automáticamente el usuario de confianza para el usuario de confianza de O365. ¿Tengo tootake ninguna acción cuando se sustituye el token de certificado de firma automáticamente?**</span><span class="sxs-lookup"><span data-stu-id="7b2ae-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have tootake any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="7b2ae-127">Utilizar la Guía de Hola que se describe en el artículo de hello [renovar certificados](active-directory-aadconnect-o365-certs.md).</span><span class="sxs-lookup"><span data-stu-id="7b2ae-127">Use hello guidance that is outlined in hello article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="7b2ae-128">Environment</span><span class="sxs-lookup"><span data-stu-id="7b2ae-128">Environment</span></span>
<span data-ttu-id="7b2ae-129">**P: ¿es sólo admitido toorename Hola server después de que se ha instalado Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="7b2ae-129">**Q: Is it supported toorename hello server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="7b2ae-130">No.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-130">No.</span></span> <span data-ttu-id="7b2ae-131">Cambiar el nombre de servidor hello será causa Hola sincronización motor toonot base de datos SQL puede tooconnect toohello y servicio hello no será capaz de toostart.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-131">Changing hello server name will cause hello sync engine toonot be able tooconnect toohello SQL database and hello service will not be able toostart.</span></span>

## <a name="identity-data"></a><span data-ttu-id="7b2ae-132">Datos de identidad</span><span class="sxs-lookup"><span data-stu-id="7b2ae-132">Identity data</span></span>
<span data-ttu-id="7b2ae-133">**P: no coincide con el atributo UPN (userPrincipalName) hello en Azure AD Hola UPN local: ¿por qué?**</span><span class="sxs-lookup"><span data-stu-id="7b2ae-133">**Q: hello UPN (userPrincipalName) attribute in Azure AD does not match hello on-prem UPN - why?**</span></span>  
<span data-ttu-id="7b2ae-134"> Consulte estos artículos:</span><span class="sxs-lookup"><span data-stu-id="7b2ae-134">See these articles:</span></span>

* [<span data-ttu-id="7b2ae-135">Nombres de usuario no coinciden en Office 365, Azure ni Intune Hola UPN local o Id. de inicio de sesión alternativo</span><span class="sxs-lookup"><span data-stu-id="7b2ae-135">User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="7b2ae-136">Los cambios no se sincronizan mediante la herramienta de sincronización de Azure Active Directory Hola después de cambiar Hola UPN de un toouse de cuenta de usuario un dominio federado diferente</span><span class="sxs-lookup"><span data-stu-id="7b2ae-136">Changes aren't synced by hello Azure Active Directory Sync tool after you change hello UPN of a user account toouse a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="7b2ae-137">También puede configurar Azure AD tooallow Hola sincronización motor tooupdate Hola userPrincipalName tal y como se describe en [características del servicio de sincronización de Azure AD Connect](active-directory-aadconnectsyncservice-features.md).</span><span class="sxs-lookup"><span data-stu-id="7b2ae-137">You can also configure Azure AD tooallow hello sync engine tooupdate hello userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="7b2ae-138">**P: ¿son compatible toosoft coincidencia locales objetos de grupo o contacto de AD con objetos de grupo o contacto de Azure AD existente?**</span><span class="sxs-lookup"><span data-stu-id="7b2ae-138">**Q: Is it supported toosoft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="7b2ae-139">No, actualmente no se admite.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-139">No, this is currently not supported.</span></span>

<span data-ttu-id="7b2ae-140">**P: ¿es toomanually de TI admitida establece el atributo de ImmutableId en Azure AD grupo o contacto existente objetos toohard coincidir local tooon objetos de grupo o contacto de AD?**</span><span class="sxs-lookup"><span data-stu-id="7b2ae-140">**Q: Is it supported toomanually set ImmutableId attribute on existing Azure AD Group/Contact objects toohard match it tooon-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="7b2ae-141">No, actualmente no se admite.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="7b2ae-142">Configuración personalizada</span><span class="sxs-lookup"><span data-stu-id="7b2ae-142">Custom configuration</span></span>
<span data-ttu-id="7b2ae-143">**P: ¿dónde son Hola cmdlets de PowerShell para Azure AD Connect documentado?**</span><span class="sxs-lookup"><span data-stu-id="7b2ae-143">**Q: Where are hello PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="7b2ae-144">Con excepción de Hola de cmdlets de hello documentados en este sitio, no se admiten otros cmdlets de PowerShell que se encuentra en Azure AD Connect para uso del cliente.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-144">With hello exception of hello cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="7b2ae-145">**P: ¿puedo usar la "Importación / servidor de exportación de servidor" se encuentra en *Synchronization Service Manager* toomove configuración entre servidores?**</span><span class="sxs-lookup"><span data-stu-id="7b2ae-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* toomove configuration between servers?**</span></span>  
<span data-ttu-id="7b2ae-146">No.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-146">No.</span></span> <span data-ttu-id="7b2ae-147">Esta opción no recuperará todas las opciones de configuración y no debe usarse.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="7b2ae-148">En su lugar debe usar configuración básica de hello Asistente toocreate hello en el segundo servidor de Hola y usar reglas de sincronización Hola editor toogenerate PowerShell scripts toomove cualquier regla personalizada entre servidores.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-148">You should instead use hello wizard toocreate hello base configuration on hello second server and use hello sync rule editor toogenerate PowerShell scripts toomove any custom rule between servers.</span></span> <span data-ttu-id="7b2ae-149">Consulte [Migración oscilante](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="7b2ae-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="7b2ae-150">**P: ¿pueden las contraseñas almacenarse en caché para la página de Hola de inicio de sesión Azure y esto se puede evitar que porque contiene un elemento input de contraseña con Autocompletar hello = "false" atributo?**</span><span class="sxs-lookup"><span data-stu-id="7b2ae-150">**Q: Can passwords be cached for hello Azure sign-in page and can this be prevented since it contains a password input element with hello autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="7b2ae-151">Actualmente no admitimos modificación Hola de atributos HTML del campo de entrada de contraseña hello, incluyendo Hola Autocompletar etiqueta.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-151">We currently do not support modifying hello HTML attributes of hello Password input field, including hello autocomplete tag.</span></span> <span data-ttu-id="7b2ae-152">Actualmente estamos trabajando en una característica que le permitirá para Javascript personalizado que le permitirá tooadd cualquier campo de contraseña de toohello de atributo.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-152">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="7b2ae-153">Esta solución debería estar disponible a finales de 2017.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="7b2ae-154">**P: ¿en hello Azure página de inicio de sesión, se muestran los nombres de usuario para los usuarios que previamente han iniciado sesión correctamente.  ¿Este comportamiento se puede desactivar?**</span><span class="sxs-lookup"><span data-stu-id="7b2ae-154">**Q: On hello Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="7b2ae-155">Actualmente no admitimos modificación Hola de atributos HTML de la página de inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-155">We currently do not support modifying hello HTML attributes of hello sign-in page.</span></span> <span data-ttu-id="7b2ae-156">Actualmente estamos trabajando en una característica que le permitirá para Javascript personalizado que le permitirá tooadd cualquier campo de contraseña de toohello de atributo.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-156">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="7b2ae-157">Esta solución debería estar disponible a finales de 2017.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="7b2ae-158">**P: ¿existe una manera tooprevent sesiones simultáneas?**</span><span class="sxs-lookup"><span data-stu-id="7b2ae-158">**Q: Is there a way tooprevent concurrent sessions?**</span></span></br>
<span data-ttu-id="7b2ae-159">No.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="7b2ae-160">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="7b2ae-160">Troubleshooting</span></span>
<span data-ttu-id="7b2ae-161">**P: ¿Cómo puedo obtener ayuda con Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="7b2ae-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="7b2ae-162">Buscar Hola Microsoft Knowledge Base (KB)</span><span class="sxs-lookup"><span data-stu-id="7b2ae-162">Search hello Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="7b2ae-163">Busque en Microsoft Knowledge Base (KB) de Hola para problemas de soluciones técnicas toocommon break-fix en línea sobre la compatibilidad con Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-163">Search hello Microsoft Knowledge Base (KB) for technical solutions toocommon break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="7b2ae-164">Foros de Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7b2ae-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="7b2ae-165">Puede buscar y examinar para technical preguntas y respuestas de la Comunidad de Hola o Formula su pregunta haciendo clic en [aquí](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span><span class="sxs-lookup"><span data-stu-id="7b2ae-165">You can search and browse for technical questions and answers from hello community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="7b2ae-166">Asistencia al cliente de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="7b2ae-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="7b2ae-167">Use esta compatibilidad de tooget de vínculo a través de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="7b2ae-167">Use this link tooget support through hello Azure portal.</span></span>

