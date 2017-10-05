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
ms.openlocfilehash: fd5988b2d4170166902bb5cc39603d4a0f83be59
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="fe96a-103">Preguntas más frecuentes acerca de Azure Active Directory Connect</span><span class="sxs-lookup"><span data-stu-id="fe96a-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="fe96a-104">Instalación general</span><span class="sxs-lookup"><span data-stu-id="fe96a-104">General installation</span></span>
<span data-ttu-id="fe96a-105">**P: ¿Funcionará la instalación si el administrador global de Azure AD tiene 2FA habilitado?**</span><span class="sxs-lookup"><span data-stu-id="fe96a-105">**Q: Will installation work if the Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="fe96a-106">Sí, con las compilaciones de febrero de 2016.</span><span class="sxs-lookup"><span data-stu-id="fe96a-106">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="fe96a-107">**P: ¿Existe alguna manera de instalar Azure AD Connect de manera desatendida?**</span><span class="sxs-lookup"><span data-stu-id="fe96a-107">**Q: Is there a way to install Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="fe96a-108">Solo se admite la instalación de Azure AD Connect mediante el Asistente para instalación.</span><span class="sxs-lookup"><span data-stu-id="fe96a-108">It is only supported to install Azure AD Connect using the installation wizard.</span></span> <span data-ttu-id="fe96a-109">No se admite la instalación silenciosa y desatendida.</span><span class="sxs-lookup"><span data-stu-id="fe96a-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="fe96a-110">**P: Tengo un bosque en el que no se puede contactar con un dominio. ¿Cómo se puede instalar Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="fe96a-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="fe96a-111">Sí, con las compilaciones de febrero de 2016.</span><span class="sxs-lookup"><span data-stu-id="fe96a-111">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="fe96a-112">**P.: ¿El agente de mantenimiento de AD DS funciona en Server Core?**</span><span class="sxs-lookup"><span data-stu-id="fe96a-112">**Q: Does the AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="fe96a-113">Sí.</span><span class="sxs-lookup"><span data-stu-id="fe96a-113">Yes.</span></span> <span data-ttu-id="fe96a-114">Después de instalar el agente, puede completar el proceso de registro mediante el siguiente cmdlet de PowerShell:</span><span class="sxs-lookup"><span data-stu-id="fe96a-114">After installing the agent, you can complete the registration process using the following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="fe96a-115">Red</span><span class="sxs-lookup"><span data-stu-id="fe96a-115">Network</span></span>
<span data-ttu-id="fe96a-116">**P: Tengo un firewall, dispositivo de red o algo más que limita las conexiones de tiempo máximo que pueden permanecer abiertas en mi red. ¿Cuál debería ser mi umbral de tiempo de espera del lado de cliente al usar Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="fe96a-116">**Q: I have a firewall, network device, or something else that limits the maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="fe96a-117">Todo el software de redes, dispositivos físicos o cualquier otra cosa que limite el tiempo máximo en que las conexiones permanecen abiertas deben usar un umbral de un mínimo de 5 minutos (300 segundos) para conectividad entre el servidor donde está instalado el cliente de Azure AD Connect y Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fe96a-117">All networking software, physical devices, or anything else that limits the maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between the server where the Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="fe96a-118">Esto también se aplica a todas las herramientas de sincronización de Microsoft Identity publicadas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="fe96a-118">This also applies to all previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="fe96a-119">**P: ¿Se admiten los dominios de una sola etiqueta (SLD)?**</span><span class="sxs-lookup"><span data-stu-id="fe96a-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="fe96a-120">No, Azure AD Connect no admite bosques/dominios locales con dominios de una sola etiqueta.</span><span class="sxs-lookup"><span data-stu-id="fe96a-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="fe96a-121">**P: ¿Se admiten los nombres de NetBios con puntos?**</span><span class="sxs-lookup"><span data-stu-id="fe96a-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="fe96a-122">No, Azure AD Connect no admite bosques/dominios locales en los que el nombre de NetBios contenga un punto "." en el nombre.</span><span class="sxs-lookup"><span data-stu-id="fe96a-122">No, Azure AD Connect does not support on-premises forests/domains where the NetBios name contains a period "." in the name.</span></span>

## <a name="federation"></a><span data-ttu-id="fe96a-123">Federación</span><span class="sxs-lookup"><span data-stu-id="fe96a-123">Federation</span></span>
<span data-ttu-id="fe96a-124">**P.: ¿Qué debo hacer si recibo un correo electrónico que me pide que renueve el certificado de Office 365?**</span><span class="sxs-lookup"><span data-stu-id="fe96a-124">**Q: What do I do if I receive an email that asking me to renew my Office 365 certificate**</span></span>  
<span data-ttu-id="fe96a-125">Siga las instrucciones que se describen en el tema de [renovación de certificados](active-directory-aadconnect-o365-certs.md) .</span><span class="sxs-lookup"><span data-stu-id="fe96a-125">Use the guidance that is outlined in the [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how to renew the certificate.</span></span>

<span data-ttu-id="fe96a-126">**P.: Tengo establecido Actualizar automáticamente el usuario de confianza para el usuario de confianza de O365. ¿Es necesario realizar alguna acción cuando se implemente automáticamente mi certificado de firma de tokens?**</span><span class="sxs-lookup"><span data-stu-id="fe96a-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have to take any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="fe96a-127">Siga las instrucciones que se describen en el artículo sobre la [renovación de certificados](active-directory-aadconnect-o365-certs.md).</span><span class="sxs-lookup"><span data-stu-id="fe96a-127">Use the guidance that is outlined in the article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="fe96a-128">Environment</span><span class="sxs-lookup"><span data-stu-id="fe96a-128">Environment</span></span>
<span data-ttu-id="fe96a-129">**P: ¿Se admite cambiar el nombre del servidor después de haber instalado Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="fe96a-129">**Q: Is it supported to rename the server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="fe96a-130">No.</span><span class="sxs-lookup"><span data-stu-id="fe96a-130">No.</span></span> <span data-ttu-id="fe96a-131">Cambiar el nombre del servidor hará que el motor de sincronización no pueda conectarse a la Base de datos SQL y el servicio no podrá iniciarse.</span><span class="sxs-lookup"><span data-stu-id="fe96a-131">Changing the server name will cause the sync engine to not be able to connect to the SQL database and the service will not be able to start.</span></span>

## <a name="identity-data"></a><span data-ttu-id="fe96a-132">Datos de identidad</span><span class="sxs-lookup"><span data-stu-id="fe96a-132">Identity data</span></span>
<span data-ttu-id="fe96a-133">**P: El atributo UPN (userPrincipalName) de Azure AD no coincide con el UPN local, ¿por qué?**</span><span class="sxs-lookup"><span data-stu-id="fe96a-133">**Q: The UPN (userPrincipalName) attribute in Azure AD does not match the on-prem UPN - why?**</span></span>  
<span data-ttu-id="fe96a-134">Consulte estos artículos:</span><span class="sxs-lookup"><span data-stu-id="fe96a-134">See these articles:</span></span>

* [<span data-ttu-id="fe96a-135">Los nombres de usuario de Office 365, Azure o Intune no coinciden con el UPN local o el identificador de inicio de sesión alternativo</span><span class="sxs-lookup"><span data-stu-id="fe96a-135">User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="fe96a-136">Los cambios no son sincronizados por la herramienta de sincronización de Azure Active Directory después de cambiar el UPN de una cuenta de usuario para usar un dominio federado diferente</span><span class="sxs-lookup"><span data-stu-id="fe96a-136">Changes aren't synced by the Azure Active Directory Sync tool after you change the UPN of a user account to use a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="fe96a-137">También puede configurar Azure AD para permitir que el motor de sincronización actualice userPrincipalName como se describe en [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md)(Características del servicio de sincronización de Azure AD Connect).</span><span class="sxs-lookup"><span data-stu-id="fe96a-137">You can also configure Azure AD to allow the sync engine to update the userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="fe96a-138">**P: ¿Se admiten las coincidencias parciales de objetos de contacto/grupo de AD local con objetos de contacto/grupo de Azure AD existentes?**</span><span class="sxs-lookup"><span data-stu-id="fe96a-138">**Q: Is it supported to soft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="fe96a-139">No, actualmente no se admite.</span><span class="sxs-lookup"><span data-stu-id="fe96a-139">No, this is currently not supported.</span></span>

<span data-ttu-id="fe96a-140">**P: ¿Se admite configurar manualmente el atributo ImmutableId en objetos de contacto/grupo de Azure AD existentes para conseguir una coincidencia exacta con los objetos de contacto/grupo de AD local?**</span><span class="sxs-lookup"><span data-stu-id="fe96a-140">**Q: Is it supported to manually set ImmutableId attribute on existing Azure AD Group/Contact objects to hard match it to on-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="fe96a-141">No, actualmente no se admite.</span><span class="sxs-lookup"><span data-stu-id="fe96a-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="fe96a-142">Configuración personalizada</span><span class="sxs-lookup"><span data-stu-id="fe96a-142">Custom configuration</span></span>
<span data-ttu-id="fe96a-143">**P: ¿Dónde se documentan los cmdlets de PowerShell para Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="fe96a-143">**Q: Where are the PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="fe96a-144">A excepción de los cmdlets documentados en este sitio, el resto de cmdlets de PowerShell que se encuentran en Azure AD Connect no se admiten para uso del cliente.</span><span class="sxs-lookup"><span data-stu-id="fe96a-144">With the exception of the cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="fe96a-145">**P.: ¿Puedo usar la característica exportación e importación del servidor de *Synchronization Service Manager* para mover la configuración entre servidores?**</span><span class="sxs-lookup"><span data-stu-id="fe96a-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* to move configuration between servers?**</span></span>  
<span data-ttu-id="fe96a-146">No.</span><span class="sxs-lookup"><span data-stu-id="fe96a-146">No.</span></span> <span data-ttu-id="fe96a-147">Esta opción no recuperará todas las opciones de configuración y no debe usarse.</span><span class="sxs-lookup"><span data-stu-id="fe96a-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="fe96a-148">En su lugar, debe usar al Asistente para crear la configuración base en el segundo servidor y utilizar el editor de reglas de sincronización para generar scripts de PowerShell para mover cualquier regla personalizada entre servidores.</span><span class="sxs-lookup"><span data-stu-id="fe96a-148">You should instead use the wizard to create the base configuration on the second server and use the sync rule editor to generate PowerShell scripts to move any custom rule between servers.</span></span> <span data-ttu-id="fe96a-149">Consulte [Migración oscilante](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="fe96a-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="fe96a-150">**P: ¿Se pueden almacenar en caché las contraseñas de la página de inicio de sesión y se puede evitar esto dado que contiene un elemento de entrada de contraseña con el atributo de autocompletar = "false"?**</span><span class="sxs-lookup"><span data-stu-id="fe96a-150">**Q: Can passwords be cached for the Azure sign-in page and can this be prevented since it contains a password input element with the autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="fe96a-151">Actualmente no admitimos la modificación de los atributos HTML del campo de entrada de contraseña, incluida la etiqueta de autocompletar.</span><span class="sxs-lookup"><span data-stu-id="fe96a-151">We currently do not support modifying the HTML attributes of the Password input field, including the autocomplete tag.</span></span> <span data-ttu-id="fe96a-152">Estamos trabajando en una característica que permitirá Javascript personalizado, por lo que podrá agregar cualquier atributo al campo de contraseña.</span><span class="sxs-lookup"><span data-stu-id="fe96a-152">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="fe96a-153">Esta solución debería estar disponible a finales de 2017.</span><span class="sxs-lookup"><span data-stu-id="fe96a-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="fe96a-154">**P: En la página de inicio de sesión de Azure, se muestran nombres de usuario de usuarios que han iniciado sesión anteriormente de forma correcta.  ¿Este comportamiento se puede desactivar?**</span><span class="sxs-lookup"><span data-stu-id="fe96a-154">**Q: On the Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="fe96a-155">Actualmente no admitimos la modificación de los atributos HTML de la página de inicio de sesión.</span><span class="sxs-lookup"><span data-stu-id="fe96a-155">We currently do not support modifying the HTML attributes of the sign-in page.</span></span> <span data-ttu-id="fe96a-156">Estamos trabajando en una característica que permitirá Javascript personalizado, por lo que podrá agregar cualquier atributo al campo de contraseña.</span><span class="sxs-lookup"><span data-stu-id="fe96a-156">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="fe96a-157">Esta solución debería estar disponible a finales de 2017.</span><span class="sxs-lookup"><span data-stu-id="fe96a-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="fe96a-158">**P: ¿Existe alguna manera de evitar las sesiones simultáneas?**</span><span class="sxs-lookup"><span data-stu-id="fe96a-158">**Q: Is there a way to prevent concurrent sessions?**</span></span></br>
<span data-ttu-id="fe96a-159">No.</span><span class="sxs-lookup"><span data-stu-id="fe96a-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="fe96a-160">Solución de problemas</span><span class="sxs-lookup"><span data-stu-id="fe96a-160">Troubleshooting</span></span>
<span data-ttu-id="fe96a-161">**P: ¿Cómo puedo obtener ayuda con Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="fe96a-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="fe96a-162">Buscar en Microsoft Knowledge Base (KB)</span><span class="sxs-lookup"><span data-stu-id="fe96a-162">Search the Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="fe96a-163">Busque en Microsoft Knowledge Base (KB) soluciones técnicas a los problemas de break-fix más comunes sobre soporte técnico de Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="fe96a-163">Search the Microsoft Knowledge Base (KB) for technical solutions to common break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="fe96a-164">Foros de Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fe96a-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="fe96a-165">Puede buscar y examinar preguntas técnicas y sus respuestas en la comunidad o realizar su propia pregunta haciendo clic [aquí](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span><span class="sxs-lookup"><span data-stu-id="fe96a-165">You can search and browse for technical questions and answers from the community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="fe96a-166">Asistencia al cliente de Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="fe96a-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="fe96a-167">Use este vínculo para obtener soporte técnico mediante el Portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fe96a-167">Use this link to get support through the Azure portal.</span></span>

