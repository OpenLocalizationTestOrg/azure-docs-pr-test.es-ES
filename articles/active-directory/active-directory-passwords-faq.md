---
title: "Preguntas más frecuentes: SSPR de Azure AD | Microsoft Docs"
description: "Preguntas más frecuentes sobre autoservicio de restablecimiento de contraseña de Azure AD"
services: active-directory
keywords: "Administración de contraseñas de Active Directory, administración de contraseñas, autoservicio de restablecimiento de contraseña de Azure AD"
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: b3fab99ff9fab5bc67fa70113dc5b06fac775b09
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="8c25f-104">Preguntas más frecuentes sobre la administración de contraseñas</span><span class="sxs-lookup"><span data-stu-id="8c25f-104">Password management frequently asked questions</span></span>

<span data-ttu-id="8c25f-105">A continuación se indican algunas de las preguntas más frecuentes sobre todos los aspectos relacionados con el restablecimiento de contraseñas.</span><span class="sxs-lookup"><span data-stu-id="8c25f-105">The following are some frequently asked questions for all things related to password reset.</span></span>

<span data-ttu-id="8c25f-106">Si tiene alguna pregunta general sobre Azure AD y el autoservicio de restablecimiento de contraseña y no encuentra una respuesta aquí, puede pedir ayuda a la comunidad en los [foros de Azure AD](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span><span class="sxs-lookup"><span data-stu-id="8c25f-106">If you have a general question about Azure AD and self-service password reset, that is not answered here, you can ask the community for assistance on the [Azure Ad forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="8c25f-107">Los miembros de la comunidad están formados por ingenieros, jefes de producto, MVP y profesionales de TI.</span><span class="sxs-lookup"><span data-stu-id="8c25f-107">Members of the community include Engineers, Product Managers, MVPs, and fellow IT Professionals.</span></span>

<span data-ttu-id="8c25f-108">Estas preguntas más frecuentes se dividen en las siguientes secciones:</span><span class="sxs-lookup"><span data-stu-id="8c25f-108">This FAQ is split into the following sections:</span></span>

* [<span data-ttu-id="8c25f-109">**Preguntas sobre el registro de restablecimiento de contraseña**</span><span class="sxs-lookup"><span data-stu-id="8c25f-109">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="8c25f-110">**Preguntas sobre el restablecimiento de contraseña**</span><span class="sxs-lookup"><span data-stu-id="8c25f-110">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="8c25f-111">**Preguntas sobre el cambio de contraseña**</span><span class="sxs-lookup"><span data-stu-id="8c25f-111">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="8c25f-112">**Preguntas sobre los informes de la administración de contraseñas**</span><span class="sxs-lookup"><span data-stu-id="8c25f-112">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="8c25f-113">**Preguntas sobre la escritura diferida de contraseñas**</span><span class="sxs-lookup"><span data-stu-id="8c25f-113">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="8c25f-114">Registro de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="8c25f-114">Password reset registration</span></span>
* <span data-ttu-id="8c25f-115">**P: ¿Mis usuarios pueden registrar sus propios datos de restablecimiento de contraseña?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-115">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="8c25f-116">**R:** Sí, siempre que el restablecimiento de contraseña esté habilitado y que los usuarios cuenten con licencia, pueden ir al portal de Registro de restablecimiento de contraseña en http://aka.ms/ssprsetup para registrar la información de autenticación.</span><span class="sxs-lookup"><span data-stu-id="8c25f-116">**A:** Yes, as long as password reset is enabled and they are licensed, they can go to the Password Reset Registration portal at http://aka.ms/ssprsetup to register their authentication information.</span></span> <span data-ttu-id="8c25f-117">Para registrarse, los usuarios también pueden ir al panel de acceso en http://myapps.microsoft.com, hacer clic en la pestaña de perfil y en la opción Registrarme para restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="8c25f-117">Users can also register by going to the access panel at http://myapps.microsoft.com, clicking the profile tab, and clicking the Register for Password Reset option.</span></span>
  >
  >
* <span data-ttu-id="8c25f-118">**P: ¿Puedo definir los datos de restablecimiento de contraseña en nombre de mis usuarios?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-118">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="8c25f-119">**R:** Sí, puede hacerlo en Azure AD Connect, PowerShell, [Azure Portal](https://portal.azure.com) o el Portal de administración de Office.</span><span class="sxs-lookup"><span data-stu-id="8c25f-119">**A:** Yes, you can do so with Azure AD Connect, PowerShell, the [Azure portal](https://portal.azure.com), or the Office Admin portal.</span></span> <span data-ttu-id="8c25f-120">Para más información, vea el artículo [Datos usados en el autoservicio de restablecimiento de contraseña de Azure AD](active-directory-passwords-data.md).</span><span class="sxs-lookup"><span data-stu-id="8c25f-120">For more information, see the article [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md).</span></span>
  >
  >
* <span data-ttu-id="8c25f-121">**P: ¿Puedo sincronizar localmente los datos de las preguntas de seguridad?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-121">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="8c25f-122">**R.:** No es posible hacerlo actualmente.</span><span class="sxs-lookup"><span data-stu-id="8c25f-122">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="8c25f-123">**P: ¿Mis usuarios pueden registrar datos de manera tal que otros usuarios no puedan verlos?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-123">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="8c25f-124">**R:** Sí, cuando los usuarios registran datos a través del portal de Registro de restablecimiento de contraseña, se guardan en campos de autenticación privados que solo son visibles para los administradores globales y para el propio usuario.</span><span class="sxs-lookup"><span data-stu-id="8c25f-124">**A:** Yes, when users register data using the Password Reset Registration Portal it is saved into private authentication fields that are only visible by Global Administrators and the user.</span></span>
    >
    > [!NOTE]
    > <span data-ttu-id="8c25f-125">Si una **cuenta de administrador de Azure** registra su número de teléfono de autenticación, este también se rellena en el campo de teléfono móvil y está visible.</span><span class="sxs-lookup"><span data-stu-id="8c25f-125">If an **Azure Administrator account** registers their authentication phone number it is also populated into the mobile phone field and is visible.</span></span>
    >
  >
  >
* <span data-ttu-id="8c25f-126">**P: ¿Mis usuarios necesitan registrarse antes de poder usar el restablecimiento de contraseña?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-126">**Q:  Do my users have to be registered before they can use password reset?**</span></span>

  > <span data-ttu-id="8c25f-127">**R:** No. Si define información de autenticación suficiente en nombre de sus usuarios, estos no tienen que registrarse.</span><span class="sxs-lookup"><span data-stu-id="8c25f-127">**A:** No, if you define enough authentication information on their behalf, users do not have to register.</span></span> <span data-ttu-id="8c25f-128">El restablecimiento de contraseña funciona siempre que tenga datos con formato correcto almacenados en los campos adecuados del directorio.</span><span class="sxs-lookup"><span data-stu-id="8c25f-128">Password reset works as long as you have properly formatted data stored in the appropriate fields in the directory.</span></span>
  >
  >
* <span data-ttu-id="8c25f-129">**P: ¿Puedo sincronizar o definir los campos Teléfono de autenticación, Correo electrónico de autenticación o Teléfono de autenticación alternativo en nombre de mis usuarios?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-129">**Q:  Can I synchronize or set the Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="8c25f-130">**R.:** No es posible hacerlo actualmente.</span><span class="sxs-lookup"><span data-stu-id="8c25f-130">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="8c25f-131">**P: ¿Cómo sabe el portal de registro cuáles son las opciones que tiene que mostrar a mis usuarios?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-131">**Q:  How does the registration portal know which options to show my users?**</span></span>

  > <span data-ttu-id="8c25f-132">**R:** En el portal de registro de restablecimiento de contraseña solo se muestran las opciones habilitadas para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="8c25f-132">**A:** The password reset registration portal only shows the options that you have enabled for your users.</span></span> <span data-ttu-id="8c25f-133">Estas opciones se encuentran en la sección Políticas para restablecer la contraseña del usuario en la pestaña Configurar del directorio.</span><span class="sxs-lookup"><span data-stu-id="8c25f-133">These options are found under the User Password Reset Policy section of your directory’s Configure tab.</span></span> <span data-ttu-id="8c25f-134">Por ejemplo, esto significa que, si no habilita las preguntas de seguridad, los usuarios no pueden registrarse para obtener esa opción.</span><span class="sxs-lookup"><span data-stu-id="8c25f-134">For example, this means that if you do not enable security questions, then users are not able to register for that option.</span></span>
  >
  >
* <span data-ttu-id="8c25f-135">**P: ¿Cuándo se considera que un usuario está registrado?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-135">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="8c25f-136">**R:** Se considera que un usuario está registrado en SSPR si ha registrado al menos el **Número de métodos requeridos para el restablecimiento** establecido en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8c25f-136">**A:** A user is considered registered for SSPR when they have registered at least the **Number of methods required to reset** that you have set in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >
## <a name="password-reset"></a><span data-ttu-id="8c25f-137">Restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="8c25f-137">Password reset</span></span>
* <span data-ttu-id="8c25f-138">**P: ¿Cuánto tiempo tengo que esperar para recibir un correo electrónico, un SMS o una llamada telefónica para el restablecimiento de contraseña?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-138">**Q:  How long should I wait to receive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="8c25f-139">**R:** Los correos electrónicos, los mensajes SMS y las llamadas telefónicas deberían llegar en un minuto; lo normal sería que tardaran entre 5 y 20 segundos.</span><span class="sxs-lookup"><span data-stu-id="8c25f-139">**A:** Email, SMS messages, and phone calls should arrive in under one minute, with the normal case being 5-20 seconds.</span></span>
    ><span data-ttu-id="8c25f-140">Si no recibe la notificación en este período de tiempo:</span><span class="sxs-lookup"><span data-stu-id="8c25f-140">If you do not receive the notification in this time frame:</span></span>
        > * <span data-ttu-id="8c25f-141">Compruebe la carpeta de correo no deseado.</span><span class="sxs-lookup"><span data-stu-id="8c25f-141">Check your junk folder.</span></span>
        > * <span data-ttu-id="8c25f-142">Compruebe que el número o el correo electrónico de contacto son los que espera.</span><span class="sxs-lookup"><span data-stu-id="8c25f-142">Check the number or email being contacted is the one you expect.</span></span>
        > * <span data-ttu-id="8c25f-143">Compruebe que los datos de autenticación del directorio tienen el formato correcto.</span><span class="sxs-lookup"><span data-stu-id="8c25f-143">Check the authentication data in the directory is correctly formatted.</span></span>
                >     * <span data-ttu-id="8c25f-144">Ejemplo: "+1 4255551234" o "user@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="8c25f-144">Example: "+1 4255551234" or "user@contoso.com"</span></span>
  >
  >
* <span data-ttu-id="8c25f-145">**P: ¿Qué idiomas admite el restablecimiento de contraseña?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-145">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="8c25f-146">**R:** La interfaz de usuario del restablecimiento de contraseña, los mensajes SMS y las llamadas de voz están localizados en los mismos idiomas que admite Office 365.</span><span class="sxs-lookup"><span data-stu-id="8c25f-146">**A:** The password reset UI, SMS messages, and voice calls are localized in the same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="8c25f-147">**P: ¿En qué partes de la experiencia de restablecimiento de contraseña aparece mi marca si defino la personalización de marca de mi organización en la pestaña de configuración del directorio?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-147">**Q:  What parts of the password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="8c25f-148">**R:** El portal de restablecimiento de contraseña muestra el logotipo de su organización y también le permite configurar el vínculo Póngase en contacto con el administrador para dirigirlo a una dirección URL o a un correo electrónico personalizado.</span><span class="sxs-lookup"><span data-stu-id="8c25f-148">**A:** The password reset portal shows your organizational logo and allows you to configure the Contact your administrator link to point to a custom email or URL.</span></span> <span data-ttu-id="8c25f-149">Todo correo electrónico enviado por el proceso de restablecimiento de contraseña incluye el logotipo, los colores y el nombre de su organización en el cuerpo del correo electrónico y se personaliza a partir del nombre.</span><span class="sxs-lookup"><span data-stu-id="8c25f-149">Any email that gets sent by password reset includes your organization’s logo, colors, name in the body of the email, and customized from name.</span></span>
  >
  >
* <span data-ttu-id="8c25f-150">**P: ¿Cómo puedo informar a mis usuarios sobre dónde tienen que ir para restablecer sus contraseñas?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-150">**Q:  How can I educate my users about where to go to reset their passwords?**</span></span>

  > <span data-ttu-id="8c25f-151">**R:** Puede enviar a los usuarios directamente a https://passwordreset.microsoftonline.com, o bien puede indicarles que hagan clic en el vínculo **¿No puede acceder a su cuenta?** en cualquier página de inicio de sesión educativa o profesional.</span><span class="sxs-lookup"><span data-stu-id="8c25f-151">**A:** You can send your users to https://passwordreset.microsoftonline.com directly, or you can instruct them to click the **Can’t access your account link** found on any Work or School sign-in page.</span></span> <span data-ttu-id="8c25f-152">También puede publicar estos vínculos en un lugar al que los usuarios puedan acceder con facilidad.</span><span class="sxs-lookup"><span data-stu-id="8c25f-152">You can also publish these links in a place easily accessible to your users.</span></span>
  >
  >
* <span data-ttu-id="8c25f-153">**P: ¿Puedo usar esta página desde un dispositivo móvil?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-153">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="8c25f-154">**R.:** Sí, esta página funciona en dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="8c25f-154">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="8c25f-155">**P: ¿Se admite el desbloqueo de cuentas locales de Active Directory cuando los usuarios restablecen sus contraseñas?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-155">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="8c25f-156">**R:** Sí, cuando un usuario restablece la contraseña y se ha implementado la escritura diferida de contraseñas mediante Azure AD Connect, esa cuenta de usuario se desbloquea automáticamente al restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="8c25f-156">**A:** Yes, when a user resets their password and password writeback has been deployed using Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="8c25f-157">**P: ¿Cómo puedo integrar directamente el restablecimiento de contraseña en la experiencia de inicio de sesión de escritorio de mi usuario?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-157">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="8c25f-158">**R:** Si es cliente de Azure AD Premium, puede instalar Microsoft Identity Manager sin costo adicional e implementar la solución de restablecimiento de contraseña local quera satisfacer este requisito.</span><span class="sxs-lookup"><span data-stu-id="8c25f-158">**A:** If you are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy the on-premises password reset solution to meet this requirement.</span></span>
  >
  >
* <span data-ttu-id="8c25f-159">**P: ¿Puedo establecer distintas preguntas de seguridad para diferentes configuraciones regionales?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-159">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="8c25f-160">**R.:** No es posible hacerlo actualmente.</span><span class="sxs-lookup"><span data-stu-id="8c25f-160">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="8c25f-161">**P: ¿Cuántas preguntas podemos configurar en la opción de autenticación Preguntas de seguridad?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-161">**Q:  How many questions can we configure for the Security Questions authentication option?**</span></span>

  > <span data-ttu-id="8c25f-162">**R:** Puede configurar hasta 20 preguntas de seguridad personalizadas en [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="8c25f-162">**A:** You can configure up to 20 custom security questions in the [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="8c25f-163">**P: ¿Qué longitud pueden tener las preguntas de seguridad?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-163">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="8c25f-164">**R.:** Las preguntas de seguridad pueden tener entre 3 y 200 caracteres.</span><span class="sxs-lookup"><span data-stu-id="8c25f-164">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="8c25f-165">**P: ¿Qué longitud pueden tener las respuestas a las preguntas de seguridad?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-165">**Q:  How long may answers to security questions be?**</span></span>

  > <span data-ttu-id="8c25f-166">**R.:** Las respuestas pueden tener entre 3 y 40 caracteres.</span><span class="sxs-lookup"><span data-stu-id="8c25f-166">**A:** Answers may be 3 to 40 characters long.</span></span>
  >
  >
* <span data-ttu-id="8c25f-167">**P: ¿Se rechazarán las respuestas duplicadas a las preguntas de seguridad?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-167">**Q:  Are duplicate answers to security questions rejected?**</span></span>

  > <span data-ttu-id="8c25f-168">**R.:** Sí, rechazaremos las respuestas duplicadas a las preguntas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="8c25f-168">**A:** Yes, we reject duplicate answers to security questions.</span></span>
  >
  >
* <span data-ttu-id="8c25f-169">**P: ¿Puede un usuario registrar la misma pregunta de seguridad más de una vez?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-169">**Q:  May a user register the same security question more than once?**</span></span>

  > <span data-ttu-id="8c25f-170">**R:** No. Una vez que un usuario registra una pregunta específica, no puede registrar esa pregunta por segunda vez.</span><span class="sxs-lookup"><span data-stu-id="8c25f-170">**A:** No, once a user registers a particular question, they may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="8c25f-171">**P: ¿Es posible establecer un límite mínimo de preguntas de seguridad para registro y restablecimiento?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-171">**Q:  Is it possible to set a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="8c25f-172">**R.:** Sí, es posible establecer un límite para el registro y otro para el restablecimiento.</span><span class="sxs-lookup"><span data-stu-id="8c25f-172">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="8c25f-173">Es posible que se requieran entre 3 y 5 preguntas para el registro y entre 3 y 5 para el restablecimiento.</span><span class="sxs-lookup"><span data-stu-id="8c25f-173">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="8c25f-174">**P: Si un usuario ha registrado más del número máximo de preguntas necesarias para el restablecimiento, ¿cómo se seleccionan las preguntas de seguridad durante el proceso de restablecimiento?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-174">**Q:  If a user has registered more than the maximum number of questions required to reset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="8c25f-175">**R:** De manera aleatoria se seleccionan N preguntas de seguridad del número total de preguntas para las cuales se ha registrado un usuario, donde N es el **Número de preguntas necesarias para el restablecimiento**.</span><span class="sxs-lookup"><span data-stu-id="8c25f-175">**A:** N security questions are selected at random out of the total number of questions a user has registered for, where N is the **Number of questions required to reset**.</span></span> <span data-ttu-id="8c25f-176">Por ejemplo, si un usuario tiene registradas 5 preguntas de seguridad, pero solo se requieren 3 para el restablecimiento, 3 de esas 5 se seleccionan de manera aleatoria y se presentan en el momento del restablecimiento.</span><span class="sxs-lookup"><span data-stu-id="8c25f-176">For example, if a user has 5 security questions registered, but only 3 are required to reset, 3 of the 5 are selected randomly and presented at reset.</span></span> <span data-ttu-id="8c25f-177">Si el usuario se equivoca al responder las preguntas, el proceso de selección vuelve a ejecutarse para evitar la repetición (hammering) de las preguntas.</span><span class="sxs-lookup"><span data-stu-id="8c25f-177">If the user gets the answers to the questions wrong, the selection process reoccurs to prevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="8c25f-178">**P: ¿Es posible evitar que los usuarios intenten restablecer la contraseña muchas veces en un período de tiempo breve?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-178">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="8c25f-179">**R:** Sí, existen características de seguridad integradas en el restablecimiento de contraseña a fin de ofrecer protección frente al uso indebido.</span><span class="sxs-lookup"><span data-stu-id="8c25f-179">**A:** Yes, there are security features built into password reset to protect from misuse.</span></span> <span data-ttu-id="8c25f-180">Los usuarios solo pueden intentar 5 restablecimientos de contraseña en un período de una hora antes de que se les bloquee durante 24 horas.</span><span class="sxs-lookup"><span data-stu-id="8c25f-180">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="8c25f-181">Los usuarios solo pueden intentar validar un número de teléfono 5 veces dentro de una hora antes de que se les bloquee durante 24 horas.</span><span class="sxs-lookup"><span data-stu-id="8c25f-181">Users may only try to validate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="8c25f-182">Los usuarios solo pueden intentar un método de autenticación 5 veces dentro de una hora antes de que se les bloquee durante 24 horas.</span><span class="sxs-lookup"><span data-stu-id="8c25f-182">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="8c25f-183">**P: ¿Durante cuánto tiempo es válido el código de acceso de un solo uso que recibe por correo electrónico o mensaje SMS?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-183">**Q:  For how long are the email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="8c25f-184">**R.:** La duración de la sesión de restablecimiento de contraseña es de 105 minutos.</span><span class="sxs-lookup"><span data-stu-id="8c25f-184">**A:** The session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="8c25f-185">Desde el principio de la operación de restablecimiento de contraseña, el usuario tiene 105 minutos para restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="8c25f-185">From the beginning of the password reset operation, the user has 105 minutes to reset their password.</span></span> <span data-ttu-id="8c25f-186">El código de acceso de un solo uso que recibe por correo electrónico o mensaje SMS no es válido después de este período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="8c25f-186">The email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="8c25f-187">Cambio de contraseña</span><span class="sxs-lookup"><span data-stu-id="8c25f-187">Password change</span></span>
* <span data-ttu-id="8c25f-188">**P: ¿Dónde deberían ir los usuarios para cambiar las contraseñas?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-188">**Q:  Where should my users go to change their passwords?**</span></span>

  > <span data-ttu-id="8c25f-189">**R:** Los usuarios pueden cambiar sus contraseñas en cualquier lugar en que vean su icono o imagen de perfil (como en la esquina superior derecha de las experiencias de [Office 365](https://portal.office.com) o el [Panel de acceso](https://myapps.microsoft.com)).</span><span class="sxs-lookup"><span data-stu-id="8c25f-189">**A:** Users may change their passwords anywhere they see their profile picture or icon (like in the upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="8c25f-190">Los usuarios pueden cambiar las contraseñas en la [página de perfil del Panel de acceso](https://account.activedirectory.windowsazure.com/r#/profile).</span><span class="sxs-lookup"><span data-stu-id="8c25f-190">Users may change their passwords from the [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="8c25f-191">Los usuarios también deben cambiar automáticamente sus contraseñas en la pantalla de inicio de sesión de Azure AD en caso de que hayan expirado.</span><span class="sxs-lookup"><span data-stu-id="8c25f-191">Users may also be asked to change their passwords automatically at the Azure AD sign-in screen if their passwords have expired.</span></span> <span data-ttu-id="8c25f-192">Por último, los usuarios pueden navegar directamente al [portal de cambio de contraseñas de Azure AD](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) si desean cambiar las contraseñas.</span><span class="sxs-lookup"><span data-stu-id="8c25f-192">Finally, users may navigate to the [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish to change their passwords.</span></span>
  >
  >
* <span data-ttu-id="8c25f-193">**P: ¿Los usuarios pueden recibir una notificación en el Portal de Office cuando expira la contraseña local?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-193">**Q:  Can my users be notified in the Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="8c25f-194">**R:** esto es posible actualmente si usa ADFS y sigue estas instrucciones: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396) (Envío de notificaciones de directiva de contraseña con ADFS).</span><span class="sxs-lookup"><span data-stu-id="8c25f-194">**A:** This is possible today if you are using ADFS by following the instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="8c25f-195">Esto no es posible hoy si usa la sincronización de hash de contraseña.</span><span class="sxs-lookup"><span data-stu-id="8c25f-195">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="8c25f-196">Esto se debe a que no sincronizamos las directivas de contraseña en el entorno local, por lo que no es posible publicar notificaciones de expiración en las experiencias en la nube.</span><span class="sxs-lookup"><span data-stu-id="8c25f-196">This is because we do not sync password policies from on-premises, so it is not possible for us to post expiry notifications to cloud experiences.</span></span> <span data-ttu-id="8c25f-197">En cualquier caso, también es posible [notificar a los usuarios cuyas contraseñas están a punto de expirar a través de PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c25f-197">In either case, it is also possible to [notify users whose passwords are about to expire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="8c25f-198">Informes de administración de contraseñas</span><span class="sxs-lookup"><span data-stu-id="8c25f-198">Password management reports</span></span>
* <span data-ttu-id="8c25f-199">**P: ¿Cuánto tiempo demoran en aparecer los datos en los informes de la administración de contraseñas?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-199">**Q:  How long does it take for data to show up on the password management reports?**</span></span>

  > <span data-ttu-id="8c25f-200">**R.:** Los datos deben aparecer en los informes de la administración de contraseñas en un plazo de entre 5 y 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="8c25f-200">**A:** Data should appear on the password management reports within 5-10 minutes.</span></span> <span data-ttu-id="8c25f-201">En algunas instancias, es posible que demoren hasta una hora en aparecer.</span><span class="sxs-lookup"><span data-stu-id="8c25f-201">It some instances it may take up to an hour to appear.</span></span>
  >
  >
* <span data-ttu-id="8c25f-202">**P: ¿Cómo puedo filtrar los informes de administración de contraseñas?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-202">**Q:  How can I filter the password management reports?**</span></span>

  > <span data-ttu-id="8c25f-203">**R:** Para filtrar los informes de administración de contraseñas, haga clic en la lupa pequeña que aparece en el extremo derecho de las etiquetas de columna, cerca de la parte superior del informe.</span><span class="sxs-lookup"><span data-stu-id="8c25f-203">**A:** You can filter the password management reports by clicking the small magnifying glass to the extreme right of the column labels, near the top of the report.</span></span> <span data-ttu-id="8c25f-204">Si desea realizar un filtrado más completo, puede descargar el informe a Excel y crear una tabla dinámica.</span><span class="sxs-lookup"><span data-stu-id="8c25f-204">If you want to do richer filtering, you can download the report to excel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="8c25f-205">**P: ¿Cuál es el número máximo de eventos que se almacenan en los informes de administración de contraseñas?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-205">**Q: What is the maximum number of events are stored in the password management reports?**</span></span>

  > <span data-ttu-id="8c25f-206">**R:** Hasta 75 000 eventos de restablecimiento de contraseña o de registro de restablecimiento de contraseña se almacenan en los informes de administración de contraseñas, los que abarcan hasta los últimos 30 días.</span><span class="sxs-lookup"><span data-stu-id="8c25f-206">**A:** Up to 75,000 password reset or password reset registration events are stored in the password management reports, spanning back up to 30 days.</span></span>  <span data-ttu-id="8c25f-207">Estamos trabajando para ampliar este número e incluir más eventos.</span><span class="sxs-lookup"><span data-stu-id="8c25f-207">We are working to expand this number to include more events.</span></span>
  >
  >
* <span data-ttu-id="8c25f-208">**P: ¿Hasta cuándo se remontan los informes de administración de contraseñas?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-208">**Q:  How far back do the password management reports go?**</span></span>

  > <span data-ttu-id="8c25f-209">**R.:** Los informes de administración de contraseñas muestran las operaciones generadas dentro de los últimos 30 días.</span><span class="sxs-lookup"><span data-stu-id="8c25f-209">**A:** The password management reports show operations occurring within the last 30 days.</span></span> <span data-ttu-id="8c25f-210">Por ahora, si desea archivar estos datos, puede descargar periódicamente los informes y guardarlos en una ubicación independiente.</span><span class="sxs-lookup"><span data-stu-id="8c25f-210">For now, if you need to archive this data, you can download the reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="8c25f-211">**P: ¿Existe un número máximo de filas que pueden aparecer en los informes de administración de contraseñas?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-211">**Q:  Is there a maximum number of rows that can appear on the password management reports?**</span></span>

  > <span data-ttu-id="8c25f-212">**R.:** Sí, pueden aparecer 75 000 filas como máximo en cualquiera de los informes de administración de contraseñas, tanto si se muestran en la interfaz de usuario o se descargan.</span><span class="sxs-lookup"><span data-stu-id="8c25f-212">**A:** Yes, a maximum of 75,000 rows may appear on either of the password management reports, whether they are being shown in the UI or being downloaded.</span></span>
  >
  >
* <span data-ttu-id="8c25f-213">**P: ¿Existe una API para acceder a los datos de informes de registro o de restablecimiento de contraseña?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-213">**Q:  Is there an API to access the password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="8c25f-214">**R:** Sí, consulte la documentación siguiente para saber cómo puede tener acceso al flujo de datos de informes de restablecimiento de contraseña.</span><span class="sxs-lookup"><span data-stu-id="8c25f-214">**A:** Yes, see the following documentation to learn how you can access the password reset reporting data stream.</span></span>  <span data-ttu-id="8c25f-215">[Obtenga información sobre cómo tener acceso a los eventos de informes de restablecimiento de contraseña mediante programación](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span><span class="sxs-lookup"><span data-stu-id="8c25f-215">[Learn how to access password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="8c25f-216">Escritura diferida de contraseñas</span><span class="sxs-lookup"><span data-stu-id="8c25f-216">Password writeback</span></span>
* <span data-ttu-id="8c25f-217">**P: ¿Cómo funciona la escritura diferida de contraseñas en segundo plano?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-217">**Q:  How does password writeback work behind the scenes?**</span></span>

  > <span data-ttu-id="8c25f-218">**R:** Consulte [Funcionamiento de la escritura diferida de contraseñas](active-directory-passwords-writeback.md) para obtener una explicación de lo que ocurre cuando se habilita la escritura diferida de contraseñas, además de cómo fluyen los datos por el sistema para volver al entorno local.</span><span class="sxs-lookup"><span data-stu-id="8c25f-218">**A:** See [How password writeback works](active-directory-passwords-writeback.md) for an explanation of what happens when you enable password writeback, and how data flows through the system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="8c25f-219">**P: ¿Cuánto tarda en funcionar la escritura diferida de contraseñas?  ¿Existe un retraso en la sincronización, como ocurre con la sincronización de hash de contraseña?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-219">**Q:  How long does password writeback take to work?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="8c25f-220">**R.:** La escritura diferida de contraseñas es inmediata.</span><span class="sxs-lookup"><span data-stu-id="8c25f-220">**A:** Password writeback is instant.</span></span> <span data-ttu-id="8c25f-221">Se trata de una canalización sincrónica que funciona radicalmente distinto a la sincronización de hash de contraseña.</span><span class="sxs-lookup"><span data-stu-id="8c25f-221">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="8c25f-222">La escritura diferida de contraseñas permite que los usuarios obtengan comentarios en tiempo real sobre el éxito de su operación de cambio o restablecimiento de contraseña.</span><span class="sxs-lookup"><span data-stu-id="8c25f-222">Password writeback allows users to get real-time feedback about the success of their password reset or change operation.</span></span> <span data-ttu-id="8c25f-223">El tiempo promedio para la escritura diferida correcta de una contraseña es de menos de 500 ms.</span><span class="sxs-lookup"><span data-stu-id="8c25f-223">The average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="8c25f-224">**P: Si mi cuenta local está deshabilitada, ¿en qué afecta a mi acceso y a mi cuenta en la nube?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-224">**Q:  If my on-premises account is disabled, how is my cloud account/access affected?**</span></span>

  > <span data-ttu-id="8c25f-225">**R:** Si el identificador local está deshabilitado, el acceso y el identificador de la nube también se deshabilitarán durante el próximo intervalo de sincronización a través de AAD Connect, que tiene lugar cada 30 minutos de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="8c25f-225">**A:** If your on-premises ID is disabled, your cloud ID/access will also be disabled at the next sync interval via AAD Connect byt default this is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="8c25f-226">**P: Si mi cuenta local está restringida por una directiva de contraseñas de Active Directory local, ¿SSPR se atiene a esta directiva si cambio la contraseña?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-226">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change the password?**</span></span>

  > <span data-ttu-id="8c25f-227">**R:** Sí, SSPR se basa y se rige en virtud de la directiva de contraseñas de AD local, incluidas la directiva de contraseñas de dominio típica de AD y cualquier directiva de contraseña muy específica orientada a un usuario determinado.</span><span class="sxs-lookup"><span data-stu-id="8c25f-227">**A:** Yes, SSPR relies on and abides by the on-premises AD password policy, including typical AD domain password policy, as well as any defined fine grained password policies targeted to a given user.</span></span>
  >
  >
* <span data-ttu-id="8c25f-228">**P: ¿Para qué tipos de cuentas funciona la escritura diferida de contraseñas?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-228">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="8c25f-229">**R:** La escritura diferida de contraseñas funciona para usuarios federados y usuarios con sincronización de hash de contraseña.</span><span class="sxs-lookup"><span data-stu-id="8c25f-229">**A:** Password writeback works for Federated and Password Hash Synchronized users.</span></span>
  >
  >
* <span data-ttu-id="8c25f-230">**P: ¿La escritura diferida de contraseñas aplica las directivas de contraseñas de mi dominio?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-230">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="8c25f-231">**R:** Sí, la escritura diferida de contraseñas aplica la vigencia, el historial, la complejidad y los filtros de contraseñas, además de cualquier otra restricción que pueda aplicar sobre las contraseñas en su dominio local.</span><span class="sxs-lookup"><span data-stu-id="8c25f-231">**A:** Yes, password writeback enforces password age, history, complexity, filters, and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="8c25f-232">**P: ¿Es segura la escritura diferida de contraseñas?  ¿Cómo puedo estar seguro de no ser víctima del ataque de un hacker?**</span><span class="sxs-lookup"><span data-stu-id="8c25f-232">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="8c25f-233">**R:** Sí, la escritura diferida de contraseñas es segura.</span><span class="sxs-lookup"><span data-stu-id="8c25f-233">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="8c25f-234">Para más información sobre los cuatro niveles de seguridad que implementa el servicio de escritura diferida de contraseñas, consulte la sección [Modelo de seguridad de la escritura diferida de contraseñas](active-directory-passwords-writeback.md#password-writeback-security-model) en Funcionamiento de la escritura diferida de contraseñas.</span><span class="sxs-lookup"><span data-stu-id="8c25f-234">To read more about the four layers of security implemented by the password writeback service, check out the [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) section in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="8c25f-235">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="8c25f-235">Next steps</span></span>

<span data-ttu-id="8c25f-236">Los vínculos siguientes proporcionan información adicional sobre el restablecimiento de contraseñas con Azure AD:</span><span class="sxs-lookup"><span data-stu-id="8c25f-236">The following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="8c25f-237">[**Inicio rápido**](active-directory-passwords-getting-started.md): preparativos para el autoservicio de administración de contraseñas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c25f-237">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="8c25f-238">[**Licencias**](active-directory-passwords-licensing.md): configuración de licencias de Azure AD</span><span class="sxs-lookup"><span data-stu-id="8c25f-238">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="8c25f-239">[**Datos**](active-directory-passwords-data.md): información sobre los datos necesarios y cómo se usan para administrar contraseñas</span><span class="sxs-lookup"><span data-stu-id="8c25f-239">[**Data**](active-directory-passwords-data.md) - Understand the data that is required and how it is used for password management</span></span>
* <span data-ttu-id="8c25f-240">[**Implementación**](active-directory-passwords-best-practices.md): planee e implemente SSPR en sus usuarios mediante las instrucciones que se encuentran aquí.</span><span class="sxs-lookup"><span data-stu-id="8c25f-240">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR to your users using the guidance found here</span></span>
* <span data-ttu-id="8c25f-241">[**Personalización**](active-directory-passwords-customize.md): personalización de la experiencia de SSPR para la empresa</span><span class="sxs-lookup"><span data-stu-id="8c25f-241">[**Customize**](active-directory-passwords-customize.md) - Customize the look and feel of the SSPR experience for your company.</span></span>
* <span data-ttu-id="8c25f-242">[**Informes**](active-directory-passwords-reporting.md): detectan si los usuarios acceden a la funcionalidad de SSPR, cuándo lo hacen y dónde.</span><span class="sxs-lookup"><span data-stu-id="8c25f-242">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="8c25f-243">[**Directiva**](active-directory-passwords-policy.md): información sobre las directivas de contraseñas de Azure AD y cómo establecerlas</span><span class="sxs-lookup"><span data-stu-id="8c25f-243">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="8c25f-244">[**Escritura diferida de contraseñas**](active-directory-passwords-writeback.md): cómo funciona la escritura diferida de contraseñas con el directorio local</span><span class="sxs-lookup"><span data-stu-id="8c25f-244">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="8c25f-245">[**Artículo técnico de profundización**](active-directory-passwords-how-it-works.md): más información para comprender el funcionamiento de la administración de contraseñas</span><span class="sxs-lookup"><span data-stu-id="8c25f-245">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind the curtain to understand how it works</span></span>
* <span data-ttu-id="8c25f-246">[**Solución de problemas**](active-directory-passwords-troubleshoot.md): información para resolver problemas habituales de SSPR</span><span class="sxs-lookup"><span data-stu-id="8c25f-246">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how to resolve common issues that we see with SSPR</span></span>
