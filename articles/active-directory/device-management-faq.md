---
title: "aaaAzure administración de dispositivos de Active Directory preguntas más frecuentes | Documentos de Microsoft"
description: "Preguntas más frecuentes sobre la administración de dispositivos de Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 000eb6a930187e13cb24cf628793afd06813be23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-device-management-faq"></a><span data-ttu-id="d422d-103">Preguntas más frecuentes sobre la administración de dispositivos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d422d-103">Azure Active Directory device management FAQ</span></span>

<span data-ttu-id="d422d-104">**P: ¿puedo registrar dispositivo Hola recientemente. ¿Por qué no puedo ver dispositivo hello en mi información de usuario en hello portal de Azure?**</span><span class="sxs-lookup"><span data-stu-id="d422d-104">**Q: I registered hello device recently. Why can’t I see hello device under my user info in hello Azure portal?**</span></span>

<span data-ttu-id="d422d-105">**R:** dispositivos Windows 10 que están unidos al dominio con el registro automático de dispositivos no se muestran en la información de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="d422d-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under hello USER info.</span></span>
<span data-ttu-id="d422d-106">Debe toouse PowerShell toosee todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d422d-106">You need toouse PowerShell toosee all devices.</span></span> 

<span data-ttu-id="d422d-107">Solo hello dispositivos siguientes aparecen en información de usuario de hello:</span><span class="sxs-lookup"><span data-stu-id="d422d-107">Only hello following devices are listed under hello USER info:</span></span>

- <span data-ttu-id="d422d-108">Todos los dispositivos personales que no están unidos a una empresa</span><span class="sxs-lookup"><span data-stu-id="d422d-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="d422d-109">Todos los dispositivos que no tengan Windows 10 / Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d422d-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="d422d-110">Todos los dispositivos que no son de Windows</span><span class="sxs-lookup"><span data-stu-id="d422d-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="d422d-111">**P: ¿por qué no puedo ver todos los dispositivos de hello registrados en Azure Active Directory en hello portal de Azure?**</span><span class="sxs-lookup"><span data-stu-id="d422d-111">**Q: Why can I not see all hello devices registered in Azure Active Directory in hello Azure portal?**</span></span> 

<span data-ttu-id="d422d-112">**R:** actualmente no hay ninguna manera toosee todos los dispositivos registrados en hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="d422d-112">**A:** Currently, there is no way toosee all registered devices in hello Azure portal.</span></span> <span data-ttu-id="d422d-113">Puede usar Azure PowerShell toofind todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="d422d-113">You can use Azure PowerShell toofind all devices.</span></span> <span data-ttu-id="d422d-114">Para obtener más información, vea hello [MsolDevice Get](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="d422d-114">For more details, see hello [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

--- 

<span data-ttu-id="d422d-115">**P: ¿Cómo puedo saber qué estado de registro del dispositivo de Hola de cliente hello es?**</span><span class="sxs-lookup"><span data-stu-id="d422d-115">**Q: How do I know what hello device registration state of hello client is?**</span></span>

<span data-ttu-id="d422d-116">**R:** depende de estado de registro del dispositivo de hello:</span><span class="sxs-lookup"><span data-stu-id="d422d-116">**A:** hello device registration state depends on:</span></span>

- <span data-ttu-id="d422d-117">¿Qué dispositivo Hola</span><span class="sxs-lookup"><span data-stu-id="d422d-117">What hello device is</span></span>
- <span data-ttu-id="d422d-118">Cómo se ha registrado</span><span class="sxs-lookup"><span data-stu-id="d422d-118">How it was registered</span></span> 
- <span data-ttu-id="d422d-119">Los detalles relacionados con tooit.</span><span class="sxs-lookup"><span data-stu-id="d422d-119">Any details related tooit.</span></span> 
 

---

<span data-ttu-id="d422d-120">**P: ¿por qué es un dispositivo que he eliminado en hello Azure portal o mediante Windows PowerShell siguen apareciendo como está registrado?**</span><span class="sxs-lookup"><span data-stu-id="d422d-120">**Q: Why is a device I have deleted in hello Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="d422d-121">**R:** Se debe al diseño.</span><span class="sxs-lookup"><span data-stu-id="d422d-121">**A:** This is by design.</span></span> <span data-ttu-id="d422d-122">dispositivo de Hello no tendrá acceso tooresources en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="d422d-122">hello device will not have access tooresources in hello cloud.</span></span> <span data-ttu-id="d422d-123">Si desea tooremove Hola dispositivo y vuelva a registrar, una acción manual debe ser toobe realizada en los dispositivos de Hola.</span><span class="sxs-lookup"><span data-stu-id="d422d-123">If you want tooremove hello device and register again, a manual action must be toobe taken on hello device.</span></span> 

<span data-ttu-id="d422d-124">Para dispositivos Windows 10 y Windows Server 2016 unidos a un dominio AD local:</span><span class="sxs-lookup"><span data-stu-id="d422d-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="d422d-125">Abra el símbolo del sistema de hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="d422d-125">Open hello command prompt as an administrator.</span></span>

2.  <span data-ttu-id="d422d-126">Escriba `dsregcmd.exe /debug /leave`</span><span class="sxs-lookup"><span data-stu-id="d422d-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="d422d-127">Cierre la sesión e inicie sesión tarea programada de tootrigger Hola que registra el dispositivo de Hola de nuevo.</span><span class="sxs-lookup"><span data-stu-id="d422d-127">Sign out and sign in tootrigger hello scheduled task that registers hello device again.</span></span> 

<span data-ttu-id="d422d-128">Para otras plataformas de Windows unidas a un dominio AD local:</span><span class="sxs-lookup"><span data-stu-id="d422d-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="d422d-129">Abra el símbolo del sistema de hello como administrador.</span><span class="sxs-lookup"><span data-stu-id="d422d-129">Open hello command prompt as an administrator.</span></span>
2.  <span data-ttu-id="d422d-130">Escriba `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span><span class="sxs-lookup"><span data-stu-id="d422d-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="d422d-131">Escriba `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span><span class="sxs-lookup"><span data-stu-id="d422d-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="d422d-132">**P: ¿Por qué veo entradas duplicadas del dispositivo en Azure Portal?**</span><span class="sxs-lookup"><span data-stu-id="d422d-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="d422d-133">**R:**</span><span class="sxs-lookup"><span data-stu-id="d422d-133">**A:**</span></span>

-   <span data-ttu-id="d422d-134">Para Windows 10 y Windows Server 2016, si son varios intentos toounjoin y vuelva a unir hello mismo dispositivo, puede haber entradas duplicadas.</span><span class="sxs-lookup"><span data-stu-id="d422d-134">For Windows 10 and Windows Server 2016, if they are repeated attempts toounjoin and re-join hello same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="d422d-135">Si ha usado Agregar cuenta profesional o educativa, cada usuario de windows que usa Agregar cuenta profesional o educativa creará un nuevo registro de dispositivo con hello mismo nombre de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d422d-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with hello same device name.</span></span>

-   <span data-ttu-id="d422d-136">Otras plataformas de Windows que están en las instalaciones con el registro automático unido a un dominio de AD creará un nuevo registro de dispositivo con hello mismo nombre de dispositivo para cada usuario de dominio que inicie sesión en el dispositivo de Hola.</span><span class="sxs-lookup"><span data-stu-id="d422d-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with hello same device name for each domain user who logs into hello device.</span></span> 

-   <span data-ttu-id="d422d-137">Una máquina AADJ que se borró, volver a instalar y volver a unirse con hello mismo nombre, se mostrarán como otro registro con hello mismo nombre de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="d422d-137">An AADJ machine that has been wiped, re-installed and re-joined with hello same name, will show up as another record with hello same device name.</span></span>

---

<span data-ttu-id="d422d-138">**P: ¿por qué puede un usuario tener acceso a recursos desde un dispositivo que he deshabilitado en hello portal de Azure?**</span><span class="sxs-lookup"><span data-stu-id="d422d-138">**Q: Why can a user still access resources from a device I have disabled in hello Azure portal?**</span></span>

<span data-ttu-id="d422d-139">**R:** puede tardar hasta hora tooan para un toobe revoke aplicado.</span><span class="sxs-lookup"><span data-stu-id="d422d-139">**A:** It can take up tooan hour for a revoke toobe applied.</span></span>

>[!Note] 
><span data-ttu-id="d422d-140">Para dispositivos perdidos, se recomienda borrar Hola dispositivo tooensure que los usuarios no pueden tener acceso a dispositivo Hola.</span><span class="sxs-lookup"><span data-stu-id="d422d-140">For lost devices, we recommend wiping hello device tooensure that users cannot access hello device.</span></span> <span data-ttu-id="d422d-141">Para más información, vea [Inscribir dispositivos para administrarlos en Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span><span class="sxs-lookup"><span data-stu-id="d422d-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="d422d-142">**P: ¿Por qué mis usuarios ven un mensaje que indica que no pueden acceder desde aquí?**</span><span class="sxs-lookup"><span data-stu-id="d422d-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="d422d-143">**R:** si ha configurado determinado toorequire de reglas de acceso condicional un estado de dispositivo específico y Hola dispositivo no cumple los criterios de hello, los usuarios están bloqueados y verá este mensaje.</span><span class="sxs-lookup"><span data-stu-id="d422d-143">**A:** If you have configured certain conditional access rules toorequire a specific device state and hello device does not meet hello criteria, users are blocked and see this message.</span></span> <span data-ttu-id="d422d-144">Por favor, evaluar reglas de Hola y asegúrese de que el dispositivo hello es capaz de toomeet Hola criterios tooavoid este mensaje.</span><span class="sxs-lookup"><span data-stu-id="d422d-144">Please evaluate hello rules and ensure that hello device is able toomeet hello criteria tooavoid this message.</span></span>

---


<span data-ttu-id="d422d-145">**P: ¿puedo ver registro de dispositivo de hello en información de usuario de Hola Hola portal de Azure y puede ver el estado de hello como está registrado en el cliente de Hola. ¿He establecido la configuración correctamente para utilizar el acceso condicional?**</span><span class="sxs-lookup"><span data-stu-id="d422d-145">**Q: I see hello device record under hello USER info in hello Azure portal and can see hello state as registered on hello client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="d422d-146">**R:** registro hello de dispositivo (deviceID) y el estado en el portal de Azure Hola deben coincidir con el cliente de Hola y se cumplen los criterios de evaluación de acceso condicional.</span><span class="sxs-lookup"><span data-stu-id="d422d-146">**A:** hello device record (deviceID) and state on hello Azure portal must match hello client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="d422d-147">Para más información, vea [Introducción al Registro de dispositivos de Azure Active Directory](active-directory-device-registration.md).</span><span class="sxs-lookup"><span data-stu-id="d422d-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="d422d-148">**P: ¿por qué obtengo un mensaje de "nombre de usuario o contraseña es incorrecta" para un dispositivo recién he unido tooAzure AD?**</span><span class="sxs-lookup"><span data-stu-id="d422d-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined tooAzure AD?**</span></span>

<span data-ttu-id="d422d-149">**R:** Las razones comunes para este escenario son:</span><span class="sxs-lookup"><span data-stu-id="d422d-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="d422d-150">Las credenciales de usuario ya no son válidas.</span><span class="sxs-lookup"><span data-stu-id="d422d-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="d422d-151">El equipo es no se puede toocommunicate con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d422d-151">Your computer is unable toocommunicate with Azure Active Directory.</span></span> <span data-ttu-id="d422d-152">Compruebe si existen errores de conectividad de red.</span><span class="sxs-lookup"><span data-stu-id="d422d-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="d422d-153">no se cumplieron los requisitos previos de Azure AD Join Hola.</span><span class="sxs-lookup"><span data-stu-id="d422d-153">hello Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="d422d-154">Asegúrese de que ha seguido los pasos de Hola para [extender nube dispositivos de tooWindows 10 capacidades a través de Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d422d-154">Please ensure that you have followed hello steps for [Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="d422d-155">Los inicios de sesión federados requiere su toosupport de servidor de federación un punto de conexión activo de WS-Trust.</span><span class="sxs-lookup"><span data-stu-id="d422d-155">Federated logins requires your federation server toosupport a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="d422d-156">**P: ¿por qué veo un saludo "¡vaya!... se produjo un error!" cuando intento del cuadro de diálogo unir su PC?**</span><span class="sxs-lookup"><span data-stu-id="d422d-156">**Q: Why do I see hello “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="d422d-157">**R:** Es el resultado de configurar la inscripción de Azure Active Directory con Intune.</span><span class="sxs-lookup"><span data-stu-id="d422d-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="d422d-158">Para más información, vea [Configurar la administración de dispositivos Windows](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span><span class="sxs-lookup"><span data-stu-id="d422d-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="d422d-159">**P: ¿por qué mi toojoin intento producirá un error en un equipo aunque no aparece ninguna información de errores?**</span><span class="sxs-lookup"><span data-stu-id="d422d-159">**Q: Why did my attempt toojoin a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="d422d-160">**R:** una causa probable es que ese usuario Hola se registra en el dispositivo toohello con cuenta de administrador integrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="d422d-160">**A:** A likely cause is that hello user is logged in toohello device using hello built-in administrator account.</span></span> <span data-ttu-id="d422d-161">Cree una cuenta local diferente antes de usar el programa de instalación de Azure Active Directory Join toocomplete Hola.</span><span class="sxs-lookup"><span data-stu-id="d422d-161">Please create a different local account before using Azure Active Directory Join toocomplete hello setup.</span></span> 

---

<span data-ttu-id="d422d-162">**P: ¿dónde puedo encontrar instrucciones para el programa de instalación de Hola de registro automático de dispositivos?**</span><span class="sxs-lookup"><span data-stu-id="d422d-162">**Q: Where can I find instructions for hello setup of automatic device registration?**</span></span>

<span data-ttu-id="d422d-163">**R:** para obtener instrucciones detalladas, consulte [cómo tooconfigure el registro automático de Windows Unidos a dominios dispositivos con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="d422d-163">**A:** For detailed instructions, see [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="d422d-164">**P: ¿dónde puedo encontrar solución de problemas de información sobre el registro de hello automático de dispositivos?**</span><span class="sxs-lookup"><span data-stu-id="d422d-164">**Q: Where can I find troubleshooting information about hello automatic device registration?**</span></span>

<span data-ttu-id="d422d-165">**R:** Para consultar información sobre solución de problemas, vea:</span><span class="sxs-lookup"><span data-stu-id="d422d-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="d422d-166">Solución de problemas de registro automático de dominio unido equipos tooAzure AD – Windows 10 y Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d422d-166">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="d422d-167">Solución de problemas de registro automático de dominio unido equipos tooAzure AD para clientes de nivel inferior de Windows</span><span class="sxs-lookup"><span data-stu-id="d422d-167">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

