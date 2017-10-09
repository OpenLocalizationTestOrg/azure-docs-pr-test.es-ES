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
ms.openlocfilehash: d04a9efeb3b35421aa605cadb2aa25f656a4d515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="password-management-frequently-asked-questions"></a><span data-ttu-id="cd750-104">Preguntas más frecuentes sobre la administración de contraseñas</span><span class="sxs-lookup"><span data-stu-id="cd750-104">Password management frequently asked questions</span></span>

<span data-ttu-id="cd750-105">Hola siguientes es algunas preguntas frecuentes para todos los aspectos relacionados con toopassword restablecer.</span><span class="sxs-lookup"><span data-stu-id="cd750-105">hello following are some frequently asked questions for all things related toopassword reset.</span></span>

<span data-ttu-id="cd750-106">Si tiene alguna pregunta sobre Azure AD general y una contraseña de autoservicio de restablecimiento, que no se trata aquí, puede pedir Comunidad Hola para obtener ayuda en hello [foros de Azure Ad](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span><span class="sxs-lookup"><span data-stu-id="cd750-106">If you have a general question about Azure AD and self-service password reset, that is not answered here, you can ask hello community for assistance on hello [Azure Ad forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=WindowsAzureAD).</span></span> <span data-ttu-id="cd750-107">Los miembros de la Comunidad de hello incluyen ingenieros, directores de producto, MVP y colegas profesionales de TI.</span><span class="sxs-lookup"><span data-stu-id="cd750-107">Members of hello community include Engineers, Product Managers, MVPs, and fellow IT Professionals.</span></span>

<span data-ttu-id="cd750-108">Estas preguntas más frecuentes se dividen en hello las secciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="cd750-108">This FAQ is split into hello following sections:</span></span>

* [<span data-ttu-id="cd750-109">**Preguntas sobre el registro de restablecimiento de contraseña**</span><span class="sxs-lookup"><span data-stu-id="cd750-109">**Questions about Password Reset Registration**</span></span>](#password-reset-registration)
* [<span data-ttu-id="cd750-110">**Preguntas sobre el restablecimiento de contraseña**</span><span class="sxs-lookup"><span data-stu-id="cd750-110">**Questions about Password Reset**</span></span>](#password-reset)
* [<span data-ttu-id="cd750-111">**Preguntas sobre el cambio de contraseña**</span><span class="sxs-lookup"><span data-stu-id="cd750-111">**Questions about Password Change**</span></span>](#password-change)
* [<span data-ttu-id="cd750-112">**Preguntas sobre los informes de la administración de contraseñas**</span><span class="sxs-lookup"><span data-stu-id="cd750-112">**Questions about password management Reports**</span></span>](#password-management-reports)
* [<span data-ttu-id="cd750-113">**Preguntas sobre la escritura diferida de contraseñas**</span><span class="sxs-lookup"><span data-stu-id="cd750-113">**Questions about password writeback**</span></span>](#password-writeback)

## <a name="password-reset-registration"></a><span data-ttu-id="cd750-114">Registro de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="cd750-114">Password reset registration</span></span>
* <span data-ttu-id="cd750-115">**P: ¿Mis usuarios pueden registrar sus propios datos de restablecimiento de contraseña?**</span><span class="sxs-lookup"><span data-stu-id="cd750-115">**Q:  Can my users register their own password reset data?**</span></span>

  > <span data-ttu-id="cd750-116">**R:** Sí, siempre y cuando se habilita el restablecimiento de contraseña y cuenten con licencia, pueden ir toohello portal de registro de restablecimiento de contraseña en http://aka.ms/ssprsetup tooregister su información de autenticación.</span><span class="sxs-lookup"><span data-stu-id="cd750-116">**A:** Yes, as long as password reset is enabled and they are licensed, they can go toohello Password Reset Registration portal at http://aka.ms/ssprsetup tooregister their authentication information.</span></span> <span data-ttu-id="cd750-117">Los usuarios también pueden registrarse va de panel de acceso de toohello en http://myapps.microsoft.com, haga clic en la ficha perfil de Hola y haga clic en hello registrar para la opción de restablecimiento de contraseña.</span><span class="sxs-lookup"><span data-stu-id="cd750-117">Users can also register by going toohello access panel at http://myapps.microsoft.com, clicking hello profile tab, and clicking hello Register for Password Reset option.</span></span>
  >
  >
* <span data-ttu-id="cd750-118">**P: ¿Puedo definir los datos de restablecimiento de contraseña en nombre de mis usuarios?**</span><span class="sxs-lookup"><span data-stu-id="cd750-118">**Q:  Can I define password reset data on behalf of my users?**</span></span>

  > <span data-ttu-id="cd750-119">**R:** Sí, puede hacerlo con Azure AD Connect, PowerShell, hello [portal de Azure](https://portal.azure.com), o el portal de administración de Office de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd750-119">**A:** Yes, you can do so with Azure AD Connect, PowerShell, hello [Azure portal](https://portal.azure.com), or hello Office Admin portal.</span></span> <span data-ttu-id="cd750-120">Para obtener más información, vea el artículo de hello [datos usados por Azure AD autoservicio de restablecimiento de contraseña](active-directory-passwords-data.md).</span><span class="sxs-lookup"><span data-stu-id="cd750-120">For more information, see hello article [Data used by Azure AD Self-Service Password Reset](active-directory-passwords-data.md).</span></span>
  >
  >
* <span data-ttu-id="cd750-121">**P: ¿Puedo sincronizar localmente los datos de las preguntas de seguridad?**</span><span class="sxs-lookup"><span data-stu-id="cd750-121">**Q:  Can I synchronize data for security questions from on premises?**</span></span>

  > <span data-ttu-id="cd750-122">**R.:** No es posible hacerlo actualmente.</span><span class="sxs-lookup"><span data-stu-id="cd750-122">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="cd750-123">**P: ¿Mis usuarios pueden registrar datos de manera tal que otros usuarios no puedan verlos?**</span><span class="sxs-lookup"><span data-stu-id="cd750-123">**Q:  Can my users register data in such a way that other users cannot see this data?**</span></span>

  > <span data-ttu-id="cd750-124">**R:** Sí, cuando un usuario registra datos mediante Hola se guarda la Portal de registro de restablecimiento de contraseña en los campos privados de autenticación que solo están visibles por los administradores globales y Hola por el usuario.</span><span class="sxs-lookup"><span data-stu-id="cd750-124">**A:** Yes, when users register data using hello Password Reset Registration Portal it is saved into private authentication fields that are only visible by Global Administrators and hello user.</span></span>
    >
    > [!NOTE]
    > <span data-ttu-id="cd750-125">Si un **cuenta de administrador de Azure** registra el número de teléfono de autenticación que también se rellena en el campo de teléfono móvil de Hola y es visible.</span><span class="sxs-lookup"><span data-stu-id="cd750-125">If an **Azure Administrator account** registers their authentication phone number it is also populated into hello mobile phone field and is visible.</span></span>
    >
  >
  >
* <span data-ttu-id="cd750-126">**P: ¿Mis usuarios tienen toobe registrado para poder usar el restablecimiento de contraseña?**</span><span class="sxs-lookup"><span data-stu-id="cd750-126">**Q:  Do my users have toobe registered before they can use password reset?**</span></span>

  > <span data-ttu-id="cd750-127">**R:** No, si define suficiente información de autenticación en su nombre, los usuarios no tienen tooregister.</span><span class="sxs-lookup"><span data-stu-id="cd750-127">**A:** No, if you define enough authentication information on their behalf, users do not have tooregister.</span></span> <span data-ttu-id="cd750-128">Restablecimiento de contraseña funciona como correctamente ha aplicado formato a los datos almacenados en los campos correspondientes de hello en el directorio de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd750-128">Password reset works as long as you have properly formatted data stored in hello appropriate fields in hello directory.</span></span>
  >
  >
* <span data-ttu-id="cd750-129">**P: ¿puedo sincronizar o establecer los campos de teléfono de autenticación, correo electrónico de autenticación o teléfono de autenticación alternativo de hello en nombre de Mis usuarios?**</span><span class="sxs-lookup"><span data-stu-id="cd750-129">**Q:  Can I synchronize or set hello Authentication Phone, Authentication Email or Alternate Authentication Phone fields on behalf of my users?**</span></span>

  > <span data-ttu-id="cd750-130">**R.:** No es posible hacerlo actualmente.</span><span class="sxs-lookup"><span data-stu-id="cd750-130">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="cd750-131">**P: ¿cómo portal de registro de hello sabe qué tooshow opciones Mis usuarios?**</span><span class="sxs-lookup"><span data-stu-id="cd750-131">**Q:  How does hello registration portal know which options tooshow my users?**</span></span>

  > <span data-ttu-id="cd750-132">**R:** portal de registro de restablecimiento de contraseña de hello solo muestra Hola opciones que ha habilitado para los usuarios.</span><span class="sxs-lookup"><span data-stu-id="cd750-132">**A:** hello password reset registration portal only shows hello options that you have enabled for your users.</span></span> <span data-ttu-id="cd750-133">Estas opciones se encuentran en hello sección Directiva de restablecimiento de contraseña de usuario de la ficha configurar de su directorio. Por ejemplo, esto significa que si no habilita preguntas de seguridad, a continuación, los usuarios no son tooregister capaz de esa opción.</span><span class="sxs-lookup"><span data-stu-id="cd750-133">These options are found under hello User Password Reset Policy section of your directory’s Configure tab. For example, this means that if you do not enable security questions, then users are not able tooregister for that option.</span></span>
  >
  >
* <span data-ttu-id="cd750-134">**P: ¿Cuándo se considera que un usuario está registrado?**</span><span class="sxs-lookup"><span data-stu-id="cd750-134">**Q:  When is a user considered registered?**</span></span>

  > <span data-ttu-id="cd750-135">**R:** se considera que un usuario se registra para SSPR cuando se hayan registrado al menos Hola **número de métodos necesarios tooreset** que haya establecido en hello [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cd750-135">**A:** A user is considered registered for SSPR when they have registered at least hello **Number of methods required tooreset** that you have set in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
## <a name="password-reset"></a><span data-ttu-id="cd750-136">Restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="cd750-136">Password reset</span></span>
* <span data-ttu-id="cd750-137">**P: ¿Cuánto debo esperar tooreceive un correo electrónico, SMS o llamada de teléfono de restablecimiento de contraseña?**</span><span class="sxs-lookup"><span data-stu-id="cd750-137">**Q:  How long should I wait tooreceive an email, SMS, or phone call from password reset?**</span></span>

  > <span data-ttu-id="cd750-138">**R:** correo electrónico, mensajes SMS, y llamadas telefónicas deben llegar en menos de un minuto, con hello habitual es que tarden 5 y 20 segundos.</span><span class="sxs-lookup"><span data-stu-id="cd750-138">**A:** Email, SMS messages, and phone calls should arrive in under one minute, with hello normal case being 5-20 seconds.</span></span>
    ><span data-ttu-id="cd750-139">Si no se reciben una notificación de hello en este período de tiempo:</span><span class="sxs-lookup"><span data-stu-id="cd750-139">If you do not receive hello notification in this time frame:</span></span>
        > * <span data-ttu-id="cd750-140">Compruebe la carpeta de correo no deseado.</span><span class="sxs-lookup"><span data-stu-id="cd750-140">Check your junk folder.</span></span>
        > * <span data-ttu-id="cd750-141">Compruebe el número de Hola o correo electrónico contactado es hello uno que espera.</span><span class="sxs-lookup"><span data-stu-id="cd750-141">Check hello number or email being contacted is hello one you expect.</span></span>
        > * <span data-ttu-id="cd750-142">Compruebe los datos de autenticación de hello en el directorio de hello tiene el formato correcto.</span><span class="sxs-lookup"><span data-stu-id="cd750-142">Check hello authentication data in hello directory is correctly formatted.</span></span>
                >     * <span data-ttu-id="cd750-143">Ejemplo: "+1 4255551234" o "user@contoso.com"</span><span class="sxs-lookup"><span data-stu-id="cd750-143">Example: "+1 4255551234" or "user@contoso.com"</span></span>
  >
  >
* <span data-ttu-id="cd750-144">**P: ¿Qué idiomas admite el restablecimiento de contraseña?**</span><span class="sxs-lookup"><span data-stu-id="cd750-144">**Q:  What languages are supported by password reset?**</span></span>

  > <span data-ttu-id="cd750-145">**R:** Hola de interfaz de usuario de restablecimiento de contraseña, mensajes SMS y voz llamadas están localizadas en hello mismos idiomas que se admiten en Office 365.</span><span class="sxs-lookup"><span data-stu-id="cd750-145">**A:** hello password reset UI, SMS messages, and voice calls are localized in hello same languages that are supported in Office 365.</span></span>
  >
  >
* <span data-ttu-id="cd750-146">**P: ¿qué partes de la experiencia de restablecimiento de contraseña de hello obtengan marca cuando establezco organizativa de personalización de marca en mi directorio de la pestaña de configuración?**</span><span class="sxs-lookup"><span data-stu-id="cd750-146">**Q:  What parts of hello password reset experience get branded when I set organizational branding in my directory’s configure tab?**</span></span>

  > <span data-ttu-id="cd750-147">**R:** portal de restablecimiento de contraseña de hello muestra el logotipo de su organización y le permite tooconfigure Hola póngase en contacto con su administrador vínculo toopoint tooa correo electrónico personalizadas o dirección URL.</span><span class="sxs-lookup"><span data-stu-id="cd750-147">**A:** hello password reset portal shows your organizational logo and allows you tooconfigure hello Contact your administrator link toopoint tooa custom email or URL.</span></span> <span data-ttu-id="cd750-148">Cualquier correo electrónico que se envía a través de restablecimiento de contraseña incluye el logotipo de su organización, colores, el nombre de cuerpo de saludo de correo electrónico de Hola y personalizada a partir del nombre.</span><span class="sxs-lookup"><span data-stu-id="cd750-148">Any email that gets sent by password reset includes your organization’s logo, colors, name in hello body of hello email, and customized from name.</span></span>
  >
  >
* <span data-ttu-id="cd750-149">**P: ¿Cómo puedo informar a Mis usuarios sobre dónde toogo tooreset sus contraseñas?**</span><span class="sxs-lookup"><span data-stu-id="cd750-149">**Q:  How can I educate my users about where toogo tooreset their passwords?**</span></span>

  > <span data-ttu-id="cd750-150">**R:** puede enviar su toohttps://passwordreset.microsoftonline.com a los usuarios directamente, o puede indicar hello tooclick **no se puede tener acceso a su vínculo de la cuenta** se encuentra en cualquier página de inicio de sesión de trabajo o centro educativo.</span><span class="sxs-lookup"><span data-stu-id="cd750-150">**A:** You can send your users toohttps://passwordreset.microsoftonline.com directly, or you can instruct them tooclick hello **Can’t access your account link** found on any Work or School sign-in page.</span></span> <span data-ttu-id="cd750-151">También puede publicar estos vínculos en un tooyour fácilmente accesible de contexto a los usuarios.</span><span class="sxs-lookup"><span data-stu-id="cd750-151">You can also publish these links in a place easily accessible tooyour users.</span></span>
  >
  >
* <span data-ttu-id="cd750-152">**P: ¿Puedo usar esta página desde un dispositivo móvil?**</span><span class="sxs-lookup"><span data-stu-id="cd750-152">**Q:  Can I use this page from a mobile device?**</span></span>

  > <span data-ttu-id="cd750-153">**R.:** Sí, esta página funciona en dispositivos móviles.</span><span class="sxs-lookup"><span data-stu-id="cd750-153">**A:** Yes, this page works on mobile devices.</span></span>
  >
  >
* <span data-ttu-id="cd750-154">**P: ¿Se admite el desbloqueo de cuentas locales de Active Directory cuando los usuarios restablecen sus contraseñas?**</span><span class="sxs-lookup"><span data-stu-id="cd750-154">**Q:  Do you support unlocking local active directory accounts when users reset their passwords?**</span></span>

  > <span data-ttu-id="cd750-155">**R:** Sí, cuando un usuario restablece la contraseña y se ha implementado la escritura diferida de contraseñas mediante Azure AD Connect, esa cuenta de usuario se desbloquea automáticamente al restablecer la contraseña.</span><span class="sxs-lookup"><span data-stu-id="cd750-155">**A:** Yes, when a user resets their password and password writeback has been deployed using Azure AD Connect, that user’s account is automatically unlocked when they reset their password.</span></span>
  >
  >
* <span data-ttu-id="cd750-156">**P: ¿Cómo puedo integrar directamente el restablecimiento de contraseña en la experiencia de inicio de sesión de escritorio de mi usuario?**</span><span class="sxs-lookup"><span data-stu-id="cd750-156">**Q:  How can I integrate password reset directly into my user’s desktop sign-in experience?**</span></span>

  > <span data-ttu-id="cd750-157">**R:** si es un cliente de Azure AD Premium, puede instalar Microsoft Identity Manager sin ningún costo adicional e implementar Hola local contraseña restablecimiento solución toomeet este requisito.</span><span class="sxs-lookup"><span data-stu-id="cd750-157">**A:** If you are an Azure AD Premium customer, you can install Microsoft Identity Manager at no additional cost and deploy hello on-premises password reset solution toomeet this requirement.</span></span>
  >
  >
* <span data-ttu-id="cd750-158">**P: ¿Puedo establecer distintas preguntas de seguridad para diferentes configuraciones regionales?**</span><span class="sxs-lookup"><span data-stu-id="cd750-158">**Q:  Can I set different security questions for different locales?**</span></span>

  > <span data-ttu-id="cd750-159">**R.:** No es posible hacerlo actualmente.</span><span class="sxs-lookup"><span data-stu-id="cd750-159">**A:** This is not possible today.</span></span>
  >
  >
* <span data-ttu-id="cd750-160">**P: ¿cuántas preguntas se pueden configurar para la opción de autenticación de preguntas de seguridad de hello?**</span><span class="sxs-lookup"><span data-stu-id="cd750-160">**Q:  How many questions can we configure for hello Security Questions authentication option?**</span></span>

  > <span data-ttu-id="cd750-161">**R:** puede configurar las preguntas de seguridad personalizado too20 Hola [portal de Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cd750-161">**A:** You can configure up too20 custom security questions in hello [Azure portal](https://portal.azure.com).</span></span>
  >
  >
* <span data-ttu-id="cd750-162">**P: ¿Qué longitud pueden tener las preguntas de seguridad?**</span><span class="sxs-lookup"><span data-stu-id="cd750-162">**Q:  How long may security questions be?**</span></span>

  > <span data-ttu-id="cd750-163">**R.:** Las preguntas de seguridad pueden tener entre 3 y 200 caracteres.</span><span class="sxs-lookup"><span data-stu-id="cd750-163">**A:** Security questions may be between 3 and 200 characters long.</span></span>
  >
  >
* <span data-ttu-id="cd750-164">**P: ¿cuánto tiempo puede respuestas toosecurity preguntas?**</span><span class="sxs-lookup"><span data-stu-id="cd750-164">**Q:  How long may answers toosecurity questions be?**</span></span>

  > <span data-ttu-id="cd750-165">**R:** respuestas pueden tener 3 caracteres too40.</span><span class="sxs-lookup"><span data-stu-id="cd750-165">**A:** Answers may be 3 too40 characters long.</span></span>
  >
  >
* <span data-ttu-id="cd750-166">**P: ¿se rechazan respuestas duplicadas toosecurity preguntas?**</span><span class="sxs-lookup"><span data-stu-id="cd750-166">**Q:  Are duplicate answers toosecurity questions rejected?**</span></span>

  > <span data-ttu-id="cd750-167">**R:** Sí, se rechazan respuestas duplicadas toosecurity preguntas.</span><span class="sxs-lookup"><span data-stu-id="cd750-167">**A:** Yes, we reject duplicate answers toosecurity questions.</span></span>
  >
  >
* <span data-ttu-id="cd750-168">**P: ¿puede un registro de usuario Hola misma pregunta de seguridad más de una vez?**</span><span class="sxs-lookup"><span data-stu-id="cd750-168">**Q:  May a user register hello same security question more than once?**</span></span>

  > <span data-ttu-id="cd750-169">**R:** No. Una vez que un usuario registra una pregunta específica, no puede registrar esa pregunta por segunda vez.</span><span class="sxs-lookup"><span data-stu-id="cd750-169">**A:** No, once a user registers a particular question, they may not register for that question a second time.</span></span>
  >
  >
* <span data-ttu-id="cd750-170">**P: ¿es posible tooset un límite mínimo de preguntas de seguridad de registro y restablecimiento?**</span><span class="sxs-lookup"><span data-stu-id="cd750-170">**Q:  Is it possible tooset a minimum limit of security questions for registration and reset?**</span></span>

  > <span data-ttu-id="cd750-171">**R.:** Sí, es posible establecer un límite para el registro y otro para el restablecimiento.</span><span class="sxs-lookup"><span data-stu-id="cd750-171">**A:** Yes, one limit can be set for registration and another for reset.</span></span> <span data-ttu-id="cd750-172">Es posible que se requieran entre 3 y 5 preguntas para el registro y entre 3 y 5 para el restablecimiento.</span><span class="sxs-lookup"><span data-stu-id="cd750-172">3-5 security questions may be required for registration and 3-5 may be required for reset.</span></span>
  >
  >
* <span data-ttu-id="cd750-173">**P: si un usuario ha registrado más Hola número máximo de preguntas necesario tooreset, ¿cómo se seleccionan las preguntas de seguridad durante el restablecimiento?**</span><span class="sxs-lookup"><span data-stu-id="cd750-173">**Q:  If a user has registered more than hello maximum number of questions required tooreset, how are security questions selected during reset?**</span></span>

  > <span data-ttu-id="cd750-174">**R:** seguridad N preguntas se seleccionan aleatoriamente fuera del número total de Hola de preguntas que un usuario ha registrado, donde N es hello **número de preguntas necesario tooreset**.</span><span class="sxs-lookup"><span data-stu-id="cd750-174">**A:** N security questions are selected at random out of hello total number of questions a user has registered for, where N is hello **Number of questions required tooreset**.</span></span> <span data-ttu-id="cd750-175">Por ejemplo, si un usuario tiene 5 preguntas de seguridad registrados, pero sólo 3 son necesario tooreset, 3 de hello 5 se selecciona aleatoriamente y presentadas en el restablecimiento.</span><span class="sxs-lookup"><span data-stu-id="cd750-175">For example, if a user has 5 security questions registered, but only 3 are required tooreset, 3 of hello 5 are selected randomly and presented at reset.</span></span> <span data-ttu-id="cd750-176">Si Hola usuario recibe respuestas de hello toohello preguntas incorrecto, el proceso de selección de hello vuelve a suceder tooprevent ataques por repetición.</span><span class="sxs-lookup"><span data-stu-id="cd750-176">If hello user gets hello answers toohello questions wrong, hello selection process reoccurs tooprevent question hammering.</span></span>
  >
  >
* <span data-ttu-id="cd750-177">**P: ¿Es posible evitar que los usuarios intenten restablecer la contraseña muchas veces en un período de tiempo breve?**</span><span class="sxs-lookup"><span data-stu-id="cd750-177">**Q:  Do you prevent users from attempting password reset many times in a short time period?**</span></span>

  > <span data-ttu-id="cd750-178">**R:** Sí, hay características de seguridad integradas en tooprotect de restablecimiento de contraseña de uso indebido.</span><span class="sxs-lookup"><span data-stu-id="cd750-178">**A:** Yes, there are security features built into password reset tooprotect from misuse.</span></span> <span data-ttu-id="cd750-179">Los usuarios solo pueden intentar 5 restablecimientos de contraseña en un período de una hora antes de que se les bloquee durante 24 horas.</span><span class="sxs-lookup"><span data-stu-id="cd750-179">Users may only try 5 password reset attempts within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="cd750-180">Los usuarios solo pueden probar toovalidate un número de teléfono 5 veces en una hora antes de que se bloquee durante 24 horas.</span><span class="sxs-lookup"><span data-stu-id="cd750-180">Users may only try toovalidate a phone number 5 times within an hour before being locked out for 24 hours.</span></span> <span data-ttu-id="cd750-181">Los usuarios solo pueden intentar un método de autenticación 5 veces dentro de una hora antes de que se les bloquee durante 24 horas.</span><span class="sxs-lookup"><span data-stu-id="cd750-181">Users may only try a single authentication method 5 times within an hour before being locked out for 24 hours.</span></span>
  >
  >
* <span data-ttu-id="cd750-182">**P: ¿durante cuánto tiempo son código de acceso de un solo uso de SMS y correo electrónico de hello válidos?**</span><span class="sxs-lookup"><span data-stu-id="cd750-182">**Q:  For how long are hello email and SMS one-time passcode valid?**</span></span>

  > <span data-ttu-id="cd750-183">**R:** Hola duración de la sesión para restablecer la contraseña es 105 minutos.</span><span class="sxs-lookup"><span data-stu-id="cd750-183">**A:** hello session lifetime for password reset is 105 minutes.</span></span> <span data-ttu-id="cd750-184">Desde principio Hola de hello operación de restablecimiento de contraseña, usuario de hello tiene 105 minutos tooreset su contraseña.</span><span class="sxs-lookup"><span data-stu-id="cd750-184">From hello beginning of hello password reset operation, hello user has 105 minutes tooreset their password.</span></span> <span data-ttu-id="cd750-185">Hello código de acceso de un solo uso de SMS y correo electrónico no son válidos después de que expire este período de tiempo.</span><span class="sxs-lookup"><span data-stu-id="cd750-185">hello email and SMS one-time passcode are invalid after this time period expires.</span></span>
  >
  >

## <a name="password-change"></a><span data-ttu-id="cd750-186">Cambio de contraseña</span><span class="sxs-lookup"><span data-stu-id="cd750-186">Password change</span></span>
* <span data-ttu-id="cd750-187">**P: ¿dónde deberían Mis usuarios ir toochange sus contraseñas?**</span><span class="sxs-lookup"><span data-stu-id="cd750-187">**Q:  Where should my users go toochange their passwords?**</span></span>

  > <span data-ttu-id="cd750-188">**R:** a los usuarios pueden cambiar sus contraseñas en cualquier lugar vean su imagen de perfil o el icono (al igual que en hello superior derecho de sus [Office 365](https://portal.office.com) o [Panel de acceso](https://myapps.microsoft.com) experiencias.</span><span class="sxs-lookup"><span data-stu-id="cd750-188">**A:** Users may change their passwords anywhere they see their profile picture or icon (like in hello upper right corner of their [Office 365](https://portal.office.com) or [Access Panel](https://myapps.microsoft.com) experiences.</span></span> <span data-ttu-id="cd750-189">Los usuarios pueden cambiar sus contraseñas de hello [página del Panel de acceso de perfil](https://account.activedirectory.windowsazure.com/r#/profile).</span><span class="sxs-lookup"><span data-stu-id="cd750-189">Users may change their passwords from hello [Access Panel profile page](https://account.activedirectory.windowsazure.com/r#/profile).</span></span> <span data-ttu-id="cd750-190">Los usuarios también pueden ser más frecuentes toochange sus contraseñas automáticamente en la pantalla de inicio de sesión de bienvenida Azure AD si sus contraseñas han caducado.</span><span class="sxs-lookup"><span data-stu-id="cd750-190">Users may also be asked toochange their passwords automatically at hello Azure AD sign-in screen if their passwords have expired.</span></span> <span data-ttu-id="cd750-191">Por último, los usuarios pueden navegar toohello [Portal de cambio de contraseña de Azure AD](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directamente si lo desean toochange sus contraseñas.</span><span class="sxs-lookup"><span data-stu-id="cd750-191">Finally, users may navigate toohello [Azure AD Password Change Portal](https://account.activedirectory.windowsazure.com/ChangePassword.aspx) directly if they wish toochange their passwords.</span></span>
  >
  >
* <span data-ttu-id="cd750-192">**P: ¿pueden mis usuarios se notificará en hello Portal de Office cuando expira la contraseña local?**</span><span class="sxs-lookup"><span data-stu-id="cd750-192">**Q:  Can my users be notified in hello Office Portal when their on-premises password expires?**</span></span>

  > <span data-ttu-id="cd750-193">**R:** esto es posible hoy si utilizas AD FS siguiendo las instrucciones de hello aquí: [enviar notificaciones de directiva de contraseña con ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span><span class="sxs-lookup"><span data-stu-id="cd750-193">**A:** This is possible today if you are using ADFS by following hello instructions here: [Sending Password Policy Claims with ADFS](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configure-ad-fs-to-send-password-expiry-claims?f=255&MSPPError=-2147217396).</span></span> <span data-ttu-id="cd750-194">Esto no es posible hoy si usa la sincronización de hash de contraseña.</span><span class="sxs-lookup"><span data-stu-id="cd750-194">If you are using password hash synchronization, this is not possible today.</span></span> <span data-ttu-id="cd750-195">Esto es porque no se sincronizar directivas de contraseña local, por lo que no es posible que nos toocloud de notificaciones de expiración toopost experiencias.</span><span class="sxs-lookup"><span data-stu-id="cd750-195">This is because we do not sync password policies from on-premises, so it is not possible for us toopost expiry notifications toocloud experiences.</span></span> <span data-ttu-id="cd750-196">En cualquier caso, también es posible demasiado[notificar a los usuarios cuyas contraseñas están sobre tooexpire mediante PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span><span class="sxs-lookup"><span data-stu-id="cd750-196">In either case, it is also possible too[notify users whose passwords are about tooexpire by using PowerShell](https://social.technet.microsoft.com/wiki/contents/articles/23313.notify-active-directory-users-about-password-expiry-using-powershell.aspx).</span></span>
  >
  >

## <a name="password-management-reports"></a><span data-ttu-id="cd750-197">Informes de administración de contraseñas</span><span class="sxs-lookup"><span data-stu-id="cd750-197">Password management reports</span></span>
* <span data-ttu-id="cd750-198">**P: ¿cuánto tarda para datos tooshow seguridad en informes de administración de contraseñas de hello?**</span><span class="sxs-lookup"><span data-stu-id="cd750-198">**Q:  How long does it take for data tooshow up on hello password management reports?**</span></span>

  > <span data-ttu-id="cd750-199">**R:** los datos aparecerán en informes de administración de contraseñas de hello en entre 5 y 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="cd750-199">**A:** Data should appear on hello password management reports within 5-10 minutes.</span></span> <span data-ttu-id="cd750-200">Algunas instancias pueden tardar hasta tooan hora tooappear.</span><span class="sxs-lookup"><span data-stu-id="cd750-200">It some instances it may take up tooan hour tooappear.</span></span>
  >
  >
* <span data-ttu-id="cd750-201">**P: ¿Cómo puedo filtrar los informes de administración de contraseñas de hello?**</span><span class="sxs-lookup"><span data-stu-id="cd750-201">**Q:  How can I filter hello password management reports?**</span></span>

  > <span data-ttu-id="cd750-202">**R:** puede filtrar los informes de administración de contraseñas de hello haciendo clic en hello lupa pequeña toohello derecha de las etiquetas de columna de hello, cerca de parte superior de Hola de informe de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd750-202">**A:** You can filter hello password management reports by clicking hello small magnifying glass toohello extreme right of hello column labels, near hello top of hello report.</span></span> <span data-ttu-id="cd750-203">Si desea toodo de filtrado exhaustivo, puede descargar Hola informe tooexcel y crear una tabla dinámica.</span><span class="sxs-lookup"><span data-stu-id="cd750-203">If you want toodo richer filtering, you can download hello report tooexcel and create a pivot table.</span></span>
  >
  >
* <span data-ttu-id="cd750-204">**P: ¿cuál es el número máximo de Hola de eventos se almacenan en los informes de administración de contraseñas de hello?**</span><span class="sxs-lookup"><span data-stu-id="cd750-204">**Q: What is hello maximum number of events are stored in hello password management reports?**</span></span>

  > <span data-ttu-id="cd750-205">**R:** seguridad too75, 000 contraseña contraseña o restablecimiento del registro los eventos de restablecimiento se almacenan en informes de administración de contraseñas de hello, expansión de copia de seguridad too30 días.</span><span class="sxs-lookup"><span data-stu-id="cd750-205">**A:** Up too75,000 password reset or password reset registration events are stored in hello password management reports, spanning back up too30 days.</span></span>  <span data-ttu-id="cd750-206">Estamos trabajando tooexpand este número tooinclude más eventos.</span><span class="sxs-lookup"><span data-stu-id="cd750-206">We are working tooexpand this number tooinclude more events.</span></span>
  >
  >
* <span data-ttu-id="cd750-207">**P: ¿cómo lejos vaya Hola informes de administración de contraseñas?**</span><span class="sxs-lookup"><span data-stu-id="cd750-207">**Q:  How far back do hello password management reports go?**</span></span>

  > <span data-ttu-id="cd750-208">**R:** administración de contraseñas de hello informa de las operaciones de presentación que se producen en hello últimos 30 días.</span><span class="sxs-lookup"><span data-stu-id="cd750-208">**A:** hello password management reports show operations occurring within hello last 30 days.</span></span> <span data-ttu-id="cd750-209">Por ahora, si necesita tooarchive estos datos, puede descargar informes de hello periódicamente y guardarlos en una ubicación diferente.</span><span class="sxs-lookup"><span data-stu-id="cd750-209">For now, if you need tooarchive this data, you can download hello reports periodically and save them in a separate location.</span></span>
  >
  >
* <span data-ttu-id="cd750-210">**P: ¿existe un número máximo de filas que pueden aparecer en informes de administración de contraseñas de hello?**</span><span class="sxs-lookup"><span data-stu-id="cd750-210">**Q:  Is there a maximum number of rows that can appear on hello password management reports?**</span></span>

  > <span data-ttu-id="cd750-211">**R:** Sí, un máximo de 75.000 filas puede aparecer en cualquiera de los informes de administración de contraseñas de hello, si se muestran en Hola interfaz de usuario o que se va a descargar.</span><span class="sxs-lookup"><span data-stu-id="cd750-211">**A:** Yes, a maximum of 75,000 rows may appear on either of hello password management reports, whether they are being shown in hello UI or being downloaded.</span></span>
  >
  >
* <span data-ttu-id="cd750-212">**P: ¿existe una tooaccess API Hola contraseña restablecimiento o registro de datos de informes?**</span><span class="sxs-lookup"><span data-stu-id="cd750-212">**Q:  Is there an API tooaccess hello password reset or registration reporting data?**</span></span>

  > <span data-ttu-id="cd750-213">**R:** Sí, vea Hola siguientes documentación toolearn cómo puede tener acceso a contraseñas de hello restablecer flujo de datos de informes.</span><span class="sxs-lookup"><span data-stu-id="cd750-213">**A:** Yes, see hello following documentation toolearn how you can access hello password reset reporting data stream.</span></span>  <span data-ttu-id="cd750-214">[Obtenga información acerca de cómo tooaccess de restablecimiento de contraseña eventos de informe mediante programación](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span><span class="sxs-lookup"><span data-stu-id="cd750-214">[Learn how tooaccess password reset reporting events programmatically](https://msdn.microsoft.com/library/azure/mt126081.aspx#BKMK_SsprActivityEvent).</span></span>
  >
  >

## <a name="password-writeback"></a><span data-ttu-id="cd750-215">Escritura diferida de contraseñas</span><span class="sxs-lookup"><span data-stu-id="cd750-215">Password writeback</span></span>
* <span data-ttu-id="cd750-216">**P: ¿cómo funciona la escritura diferida de contraseñas entre bastidores de hello?**</span><span class="sxs-lookup"><span data-stu-id="cd750-216">**Q:  How does password writeback work behind hello scenes?**</span></span>

  > <span data-ttu-id="cd750-217">**R:** vea [cómo funciona la escritura diferida de contraseñas](active-directory-passwords-writeback.md) para obtener una explicación de lo que ocurre cuando se habilita la escritura diferida de contraseñas y cómo fluyen los datos a través del sistema de hello en el entorno local.</span><span class="sxs-lookup"><span data-stu-id="cd750-217">**A:** See [How password writeback works](active-directory-passwords-writeback.md) for an explanation of what happens when you enable password writeback, and how data flows through hello system back into your on-premises environment.</span></span>
  >
  >
* <span data-ttu-id="cd750-218">**P: ¿cuánto tiempo tarda la escritura diferida de contraseñas la toowork?  ¿Existe un retraso en la sincronización, como ocurre con la sincronización de hash de contraseña?**</span><span class="sxs-lookup"><span data-stu-id="cd750-218">**Q:  How long does password writeback take toowork?  Is there a synchronization delay like with password hash sync?**</span></span>

  > <span data-ttu-id="cd750-219">**R.:** La escritura diferida de contraseñas es inmediata.</span><span class="sxs-lookup"><span data-stu-id="cd750-219">**A:** Password writeback is instant.</span></span> <span data-ttu-id="cd750-220">Se trata de una canalización sincrónica que funciona radicalmente distinto a la sincronización de hash de contraseña.</span><span class="sxs-lookup"><span data-stu-id="cd750-220">It is a synchronous pipeline that works fundamentally differently than password hash synchronization.</span></span> <span data-ttu-id="cd750-221">Escritura diferida de contraseñas permite a los usuarios tooget comentarios en tiempo real sobre la correcta de Hola de su contraseña restablecer o cambiar la operación.</span><span class="sxs-lookup"><span data-stu-id="cd750-221">Password writeback allows users tooget real-time feedback about hello success of their password reset or change operation.</span></span> <span data-ttu-id="cd750-222">tiempo medio de Hola para una reescritura de una contraseña correcta es inferior a 500 ms..</span><span class="sxs-lookup"><span data-stu-id="cd750-222">hello average time for a successful writeback of a password is under 500 ms.</span></span>
  >
  >
* <span data-ttu-id="cd750-223">**P: Si mi cuenta local está deshabilitada, ¿en qué afecta a mi acceso y a mi cuenta en la nube?**</span><span class="sxs-lookup"><span data-stu-id="cd750-223">**Q:  If my on-premises account is disabled, how is my cloud account/access affected?**</span></span>

  > <span data-ttu-id="cd750-224">**R:** si el identificador local está deshabilitado, la nube de identificador/acceso también se deshabilitará al siguiente intervalo de sincronización Hola a través de la conexión de AAD byt de forma predeterminada se trata cada 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="cd750-224">**A:** If your on-premises ID is disabled, your cloud ID/access will also be disabled at hello next sync interval via AAD Connect byt default this is every 30 minutes.</span></span>
  >
  >
* <span data-ttu-id="cd750-225">**¿P: si mi cuenta local está restringido por una directiva de contraseña de Active Directory local, SSPR obedecen a esta directiva cuando se cambia la contraseña de hello?**</span><span class="sxs-lookup"><span data-stu-id="cd750-225">**Q:  If my on-premises account is constrained by an on-premises Active Directory password policy, does SSPR obey this policy when I change hello password?**</span></span>

  > <span data-ttu-id="cd750-226">**R:** Sí, SSPR se basa en y se rige por directiva de contraseñas de AD, incluida la directiva de contraseñas de dominio de AD típica, así como las directivas de contraseña específica definida como destino tooa dado usuario a local de Hola.</span><span class="sxs-lookup"><span data-stu-id="cd750-226">**A:** Yes, SSPR relies on and abides by hello on-premises AD password policy, including typical AD domain password policy, as well as any defined fine grained password policies targeted tooa given user.</span></span>
  >
  >
* <span data-ttu-id="cd750-227">**P: ¿Para qué tipos de cuentas funciona la escritura diferida de contraseñas?**</span><span class="sxs-lookup"><span data-stu-id="cd750-227">**Q:  What types of accounts does password writeback work for?**</span></span>

  > <span data-ttu-id="cd750-228">**R:** La escritura diferida de contraseñas funciona para usuarios federados y usuarios con sincronización de hash de contraseña.</span><span class="sxs-lookup"><span data-stu-id="cd750-228">**A:** Password writeback works for Federated and Password Hash Synchronized users.</span></span>
  >
  >
* <span data-ttu-id="cd750-229">**P: ¿La escritura diferida de contraseñas aplica las directivas de contraseñas de mi dominio?**</span><span class="sxs-lookup"><span data-stu-id="cd750-229">**Q:  Does password writeback enforce my domain’s password policies?**</span></span>

  > <span data-ttu-id="cd750-230">**R:** Sí, la escritura diferida de contraseñas aplica la vigencia, el historial, la complejidad y los filtros de contraseñas, además de cualquier otra restricción que pueda aplicar sobre las contraseñas en su dominio local.</span><span class="sxs-lookup"><span data-stu-id="cd750-230">**A:** Yes, password writeback enforces password age, history, complexity, filters, and any other restriction you may put in place on passwords in your local domain.</span></span>
  >
  >
* <span data-ttu-id="cd750-231">**P: ¿Es segura la escritura diferida de contraseñas?  ¿Cómo puedo estar seguro de no ser víctima del ataque de un hacker?**</span><span class="sxs-lookup"><span data-stu-id="cd750-231">**Q:  Is password writeback secure?  How can I be sure I won’t get hacked?**</span></span>

  > <span data-ttu-id="cd750-232">**R:** Sí, la escritura diferida de contraseñas es segura.</span><span class="sxs-lookup"><span data-stu-id="cd750-232">**A:** Yes, password writeback is secure.</span></span> <span data-ttu-id="cd750-233">tooread más información acerca de las capas de hello cuatro de seguridad implementado por el servicio de escritura diferida de contraseña de hello, desproteger hello [modelo de seguridad de escritura diferida de contraseñas](active-directory-passwords-writeback.md#password-writeback-security-model) sección en cómo funciona la escritura diferida de contraseñas.</span><span class="sxs-lookup"><span data-stu-id="cd750-233">tooread more about hello four layers of security implemented by hello password writeback service, check out hello [Password writeback security model](active-directory-passwords-writeback.md#password-writeback-security-model) section in How password writeback works.</span></span>
  >
  >

## <a name="next-steps"></a><span data-ttu-id="cd750-234">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="cd750-234">Next steps</span></span>

<span data-ttu-id="cd750-235">Hola siguientes vínculos proporciona más información sobre el uso de Azure AD de restablecimiento de contraseña</span><span class="sxs-lookup"><span data-stu-id="cd750-235">hello following links provide additional information regarding password reset using Azure AD</span></span>

* <span data-ttu-id="cd750-236">[**Inicio rápido**](active-directory-passwords-getting-started.md): preparativos para el autoservicio de administración de contraseñas de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd750-236">[**Quick Start**](active-directory-passwords-getting-started.md) - Get up and running with Azure AD self service password management</span></span> 
* <span data-ttu-id="cd750-237">[**Licencias**](active-directory-passwords-licensing.md): configuración de licencias de Azure AD</span><span class="sxs-lookup"><span data-stu-id="cd750-237">[**Licensing**](active-directory-passwords-licensing.md) - Configure your Azure AD Licensing</span></span>
* <span data-ttu-id="cd750-238">[**Datos** ](active-directory-passwords-data.md) : comprender los datos de Hola que es necesarios y cómo se utiliza para la administración de contraseñas</span><span class="sxs-lookup"><span data-stu-id="cd750-238">[**Data**](active-directory-passwords-data.md) - Understand hello data that is required and how it is used for password management</span></span>
* <span data-ttu-id="cd750-239">[**Implementación** ](active-directory-passwords-best-practices.md) -planear e implementar a los usuarios de Autoservicio tooyour usando la orientación de hello encontrar aquí</span><span class="sxs-lookup"><span data-stu-id="cd750-239">[**Rollout**](active-directory-passwords-best-practices.md) - Plan and deploy SSPR tooyour users using hello guidance found here</span></span>
* <span data-ttu-id="cd750-240">[**Personalizar** ](active-directory-passwords-customize.md) -personalizar Hola apariencia y funcionamiento del programa Hola a la experiencia de Autoservicio de su empresa.</span><span class="sxs-lookup"><span data-stu-id="cd750-240">[**Customize**](active-directory-passwords-customize.md) - Customize hello look and feel of hello SSPR experience for your company.</span></span>
* <span data-ttu-id="cd750-241">[**Informes**](active-directory-passwords-reporting.md): detectan si los usuarios acceden a la funcionalidad de SSPR, cuándo lo hacen y dónde.</span><span class="sxs-lookup"><span data-stu-id="cd750-241">[**Reporting**](active-directory-passwords-reporting.md) - Discover if, when, and where your users are accessing SSPR functionality</span></span>
* <span data-ttu-id="cd750-242">[**Directiva**](active-directory-passwords-policy.md): información sobre las directivas de contraseñas de Azure AD y cómo establecerlas</span><span class="sxs-lookup"><span data-stu-id="cd750-242">[**Policy**](active-directory-passwords-policy.md) - Understand and set Azure AD password policies</span></span>
* <span data-ttu-id="cd750-243">[**Escritura diferida de contraseñas**](active-directory-passwords-writeback.md): cómo funciona la escritura diferida de contraseñas con el directorio local</span><span class="sxs-lookup"><span data-stu-id="cd750-243">[**Password Writeback**](active-directory-passwords-writeback.md) - How does password writeback work with your on-premises directory</span></span>
* <span data-ttu-id="cd750-244">[**Profundización técnica** ](active-directory-passwords-how-it-works.md) -ir detrás de hello cortina toounderstand cómo funciona</span><span class="sxs-lookup"><span data-stu-id="cd750-244">[**Technical Deep Dive**](active-directory-passwords-how-it-works.md) - Go behind hello curtain toounderstand how it works</span></span>
* <span data-ttu-id="cd750-245">[**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Obtenga información acerca de cómo problemas comunes de tooresolve que vemos con SSPR</span><span class="sxs-lookup"><span data-stu-id="cd750-245">[**Troubleshoot**](active-directory-passwords-troubleshoot.md) - Learn how tooresolve common issues that we see with SSPR</span></span>
