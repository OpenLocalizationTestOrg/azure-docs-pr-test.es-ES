---
title: "Preguntas más frecuentes sobre el registro automático de dispositivos de Azure Active Directory | Microsoft Docs"
description: "Preguntas más frecuentes sobre el registro automático de dispositivos con Azure Active Directory."
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
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 29751239ae2a26cd7b07ddd0d8a8e706d4056b68
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-automatic-device-registration-faq"></a><span data-ttu-id="85de3-103">Preguntas más frecuentes sobre el registro automático de dispositivos de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="85de3-103">Azure Active Directory automatic device registration FAQ</span></span>

<span data-ttu-id="85de3-104">**P: He registrado el dispositivo hace poco. ¿Por qué no puedo ver el dispositivo en la información del usuario en Azure Portal?**</span><span class="sxs-lookup"><span data-stu-id="85de3-104">**Q: I registered the device recently. Why can’t I see the device under my user info in the Azure portal?**</span></span>

<span data-ttu-id="85de3-105">**R:** Los dispositivos Windows 10 unidos a un dominio mediante el registro automático de dispositivos no aparecen en la información del USUARIO.</span><span class="sxs-lookup"><span data-stu-id="85de3-105">**A:** Windows 10 devices that are domain-joined with automatic device registration do not show up under the USER info.</span></span>
<span data-ttu-id="85de3-106">Debe usar PowerShell para ver todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="85de3-106">You need to use PowerShell to see all devices.</span></span> 

<span data-ttu-id="85de3-107">Solo los dispositivos siguientes aparecen en la información del USUARIO:</span><span class="sxs-lookup"><span data-stu-id="85de3-107">Only the following devices are listed under the USER info:</span></span>

- <span data-ttu-id="85de3-108">Todos los dispositivos personales que no están unidos a una empresa</span><span class="sxs-lookup"><span data-stu-id="85de3-108">All personal devices that are not enterprise joined</span></span> 
- <span data-ttu-id="85de3-109">Todos los dispositivos que no tengan Windows 10 / Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="85de3-109">All non-Windows 10 / Windows Server 2016</span></span> 
- <span data-ttu-id="85de3-110">Todos los dispositivos que no son de Windows</span><span class="sxs-lookup"><span data-stu-id="85de3-110">All non-Windows devices</span></span> 

---

<span data-ttu-id="85de3-111">**P: ¿Por qué no puedo ver en Azure Portal todos los dispositivos registrados en Azure Active Directory?**</span><span class="sxs-lookup"><span data-stu-id="85de3-111">**Q: Why can I not see all the devices registered in Azure Active Directory in the Azure portal?**</span></span> 

<span data-ttu-id="85de3-112">**R:** Actualmente, no hay ninguna forma de ver todos los dispositivos registrados en Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="85de3-112">**A:** Currently, there is no way to see all registered devices in the Azure portal.</span></span> <span data-ttu-id="85de3-113">Puede usar Azure PowerShell para buscar todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="85de3-113">You can use Azure PowerShell to find all devices.</span></span> <span data-ttu-id="85de3-114">Para más información, vea el cmdlet [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0).</span><span class="sxs-lookup"><span data-stu-id="85de3-114">For more details, see the [Get-MsolDevice](/powershell/module/msonline/get-msoldevice?view=azureadps-1.0) cmdlet.</span></span>

--- 

<span data-ttu-id="85de3-115">**P: ¿Cómo puedo saber cuál es el estado de registro del dispositivo del cliente?**</span><span class="sxs-lookup"><span data-stu-id="85de3-115">**Q: How do I know what the device registration state of the client is?**</span></span>

<span data-ttu-id="85de3-116">**R:** El estado de registro del dispositivo depende de:</span><span class="sxs-lookup"><span data-stu-id="85de3-116">**A:** The device registration state depends on:</span></span>

- <span data-ttu-id="85de3-117">De qué dispositivo se trata</span><span class="sxs-lookup"><span data-stu-id="85de3-117">What the device is</span></span>
- <span data-ttu-id="85de3-118">Cómo se ha registrado</span><span class="sxs-lookup"><span data-stu-id="85de3-118">How it was registered</span></span> 
- <span data-ttu-id="85de3-119">Los detalles relacionados con él</span><span class="sxs-lookup"><span data-stu-id="85de3-119">Any details related to it.</span></span> 
 

---

<span data-ttu-id="85de3-120">**P: ¿Por qué aún aparece registrado un dispositivo que ya he eliminado de Azure Portal o con Windows PowerShell?**</span><span class="sxs-lookup"><span data-stu-id="85de3-120">**Q: Why is a device I have deleted in the Azure portal or using Windows PowerShell still listed as registered?**</span></span>

<span data-ttu-id="85de3-121">**R:** Se debe al diseño.</span><span class="sxs-lookup"><span data-stu-id="85de3-121">**A:** This is by design.</span></span> <span data-ttu-id="85de3-122">El dispositivo no puede acceder a los recursos en la nube.</span><span class="sxs-lookup"><span data-stu-id="85de3-122">The device will not have access to resources in the cloud.</span></span> <span data-ttu-id="85de3-123">Si desea quitar el dispositivo y registrarlo de nuevo, es necesario realizar una acción manual en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="85de3-123">If you want to remove the device and register again, a manual action must be to be taken on the device.</span></span> 

<span data-ttu-id="85de3-124">Para dispositivos Windows 10 y Windows Server 2016 unidos a un dominio AD local:</span><span class="sxs-lookup"><span data-stu-id="85de3-124">For Windows 10 and Windows Server 2016 that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="85de3-125">Abra el símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="85de3-125">Open the command prompt as an administrator.</span></span>

2.  <span data-ttu-id="85de3-126">Escriba `dsregcmd.exe /debug /leave`</span><span class="sxs-lookup"><span data-stu-id="85de3-126">Type `dsregcmd.exe /debug /leave`</span></span>

3.  <span data-ttu-id="85de3-127">Cierre la sesión y luego iníciela para desencadenar la tarea programada que registra de nuevo el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="85de3-127">Sign out and sign in to trigger the scheduled task that registers the device again.</span></span> 

<span data-ttu-id="85de3-128">Para otras plataformas de Windows unidas a un dominio AD local:</span><span class="sxs-lookup"><span data-stu-id="85de3-128">For other Windows platforms that are on-premises AD domain-joined:</span></span>

1.  <span data-ttu-id="85de3-129">Abra el símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="85de3-129">Open the command prompt as an administrator.</span></span>
2.  <span data-ttu-id="85de3-130">Escriba `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span><span class="sxs-lookup"><span data-stu-id="85de3-130">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /l"`.</span></span>
3.  <span data-ttu-id="85de3-131">Escriba `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span><span class="sxs-lookup"><span data-stu-id="85de3-131">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /j"`.</span></span>

---

<span data-ttu-id="85de3-132">**P: ¿Por qué veo entradas duplicadas del dispositivo en Azure Portal?**</span><span class="sxs-lookup"><span data-stu-id="85de3-132">**Q: Why do I see duplicate device entries in Azure portal?**</span></span>

<span data-ttu-id="85de3-133">**R:**</span><span class="sxs-lookup"><span data-stu-id="85de3-133">**A:**</span></span>

-   <span data-ttu-id="85de3-134">Para Windows 10 y Windows Server 2016, si se dan varios intentos para desunir y volver a unir el mismo dispositivo, pueden aparecer entradas duplicadas.</span><span class="sxs-lookup"><span data-stu-id="85de3-134">For Windows 10 and Windows Server 2016, if they are repeated attempts to unjoin and re-join the same device, there might be duplicate entries.</span></span> 

-   <span data-ttu-id="85de3-135">Si ha usado Agregar cuenta profesional o educativa, cada usuario de Windows que usa Agregar cuenta profesional o educativa creará un nuevo registro de dispositivo con el mismo nombre de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="85de3-135">If you have used Add Work or School Account, each windows user who uses Add Work or School Account will create a new device record with the same device name.</span></span>

-   <span data-ttu-id="85de3-136">Otras plataformas de Windows unidas a un dominio AD local con el registro automático crearán un nuevo registro de dispositivo con el mismo nombre de dispositivo para cada usuario del dominio registrado en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="85de3-136">Other Windows platforms that are on-premises AD domain-joined using automatic registration will create a new device record with the same device name for each domain user who logs into the device.</span></span> 

-   <span data-ttu-id="85de3-137">Una máquina AADJ que se ha borrado, se ha vuelto a instalar y se ha vuelto a unir con el mismo nombre, aparece como otro registro con el mismo nombre de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="85de3-137">An AADJ machine that has been wiped, re-installed and re-joined with the same name, will show up as another record with the same device name.</span></span>

---

<span data-ttu-id="85de3-138">**P: ¿Por qué puede un usuario tener acceso a recursos desde un dispositivo que he deshabilitado en Azure Portal?**</span><span class="sxs-lookup"><span data-stu-id="85de3-138">**Q: Why can a user still access resources from a device I have disabled in the Azure portal?**</span></span>

<span data-ttu-id="85de3-139">**R:** Una revocación puede tardar hasta una hora en aplicarse.</span><span class="sxs-lookup"><span data-stu-id="85de3-139">**A:** It can take up to an hour for a revoke to be applied.</span></span>

>[!Note] 
><span data-ttu-id="85de3-140">Para dispositivos perdidos, se recomienda borrar el dispositivo para asegurarse de que los usuarios no pueden acceder a él.</span><span class="sxs-lookup"><span data-stu-id="85de3-140">For lost devices, we recommend wiping the device to ensure that users cannot access the device.</span></span> <span data-ttu-id="85de3-141">Para más información, vea [Inscribir dispositivos para administrarlos en Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span><span class="sxs-lookup"><span data-stu-id="85de3-141">For more details, see [Enroll devices for management in Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).</span></span> 


---

<span data-ttu-id="85de3-142">**P: ¿Por qué mis usuarios ven un mensaje que indica que no pueden acceder desde aquí?**</span><span class="sxs-lookup"><span data-stu-id="85de3-142">**Q: Why do my users see “You can’t get there from here”?**</span></span>

<span data-ttu-id="85de3-143">**R:** Si ha configurado determinadas reglas de acceso condicional para requerir un estado de dispositivo específico y el dispositivo no cumple los criterios, a los usuarios se les bloquea y ven este mensaje.</span><span class="sxs-lookup"><span data-stu-id="85de3-143">**A:** If you have configured certain conditional access rules to require a specific device state and the device does not meet the criteria, users are blocked and see this message.</span></span> <span data-ttu-id="85de3-144">Evalúe las reglas y asegúrese de que el dispositivo pueda cumplir los criterios para evitar ese mensaje.</span><span class="sxs-lookup"><span data-stu-id="85de3-144">Please evaluate the rules and ensure that the device is able to meet the criteria to avoid this message.</span></span>

---


<span data-ttu-id="85de3-145">**P: Puedo ver el registro del dispositivo en la información del USUARIO en Azure Portal y puedo ver el estado como registrado en el cliente. ¿He establecido la configuración correctamente para utilizar el acceso condicional?**</span><span class="sxs-lookup"><span data-stu-id="85de3-145">**Q: I see the device record under the USER info in the Azure portal and can see the state as registered on the client. Am I setup correctly for using conditional access?**</span></span>

<span data-ttu-id="85de3-146">**R:** El registro del dispositivo (Id. de dispositivo) y el estado que aparece en Azure Portal deben coincidir con el cliente y cumplir todos los criterios de evaluación establecidos para el acceso condicional.</span><span class="sxs-lookup"><span data-stu-id="85de3-146">**A:** The device record (deviceID) and state on the Azure portal must match the client and meet any evaluation criteria for conditional access.</span></span> <span data-ttu-id="85de3-147">Para más información, vea [Introducción al Registro de dispositivos de Azure Active Directory](active-directory-device-registration.md).</span><span class="sxs-lookup"><span data-stu-id="85de3-147">For more details, see [Get started with Azure Active Directory Device Registration](active-directory-device-registration.md).</span></span>

---

<span data-ttu-id="85de3-148">**P: ¿Por qué me aparece el mensaje “El nombre de usuario o la contraseña no son correctos” para un dispositivo que ya he unido a Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="85de3-148">**Q: Why do I get a "username or password is incorrect" message for a device I have just joined to Azure AD?**</span></span>

<span data-ttu-id="85de3-149">**R:** Las razones comunes para este escenario son:</span><span class="sxs-lookup"><span data-stu-id="85de3-149">**A:** Common reasons for this scenario are:</span></span>

- <span data-ttu-id="85de3-150">Las credenciales de usuario ya no son válidas.</span><span class="sxs-lookup"><span data-stu-id="85de3-150">Your user credentials are no longer valid.</span></span>

- <span data-ttu-id="85de3-151">El equipo no puede comunicarse con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="85de3-151">Your computer is unable to communicate with Azure Active Directory.</span></span> <span data-ttu-id="85de3-152">Compruebe si existen errores de conectividad de red.</span><span class="sxs-lookup"><span data-stu-id="85de3-152">Check for any network connectivity issues.</span></span>

- <span data-ttu-id="85de3-153">No se han cumplido los requisitos previos para Azure AD Join.</span><span class="sxs-lookup"><span data-stu-id="85de3-153">The Azure AD Join pre-requisites were not met.</span></span> <span data-ttu-id="85de3-154">Asegúrese de que haya seguido los pasos para la [Ampliación de las capacidades de nube a dispositivos de Windows 10 a través de Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span><span class="sxs-lookup"><span data-stu-id="85de3-154">Please ensure that you have followed the steps for [Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join](active-directory-azureadjoin-overview.md).</span></span>  

- <span data-ttu-id="85de3-155">Los inicios de sesión federados requieren que el servidor de federación admita un punto de conexión activo de WS-Trust.</span><span class="sxs-lookup"><span data-stu-id="85de3-155">Federated logins requires your federation server to support a WS-Trust active endpoint.</span></span> 

---

<span data-ttu-id="85de3-156">**P: ¿Por qué me aparece un cuadro de diálogo que indica que se ha producido un error cuando intento unir mi equipo?**</span><span class="sxs-lookup"><span data-stu-id="85de3-156">**Q: Why do I see the “Oops… an error occurred!" dialog when I try do join my PC?**</span></span>

<span data-ttu-id="85de3-157">**R:** Es el resultado de configurar la inscripción de Azure Active Directory con Intune.</span><span class="sxs-lookup"><span data-stu-id="85de3-157">**A:** This is a result of setting up Azure Active Directory enrollment with Intune.</span></span> <span data-ttu-id="85de3-158">Para más información, vea [Configurar la administración de dispositivos Windows](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span><span class="sxs-lookup"><span data-stu-id="85de3-158">For more details, see [Set up Windows device management](https://docs.microsoft.com/intune/deploy-use/set-up-windows-device-management-with-microsoft-intune#azure-active-directory-enrollment).</span></span>  

---

<span data-ttu-id="85de3-159">**P: ¿Por qué se produce un error al intentar unir mi equipo a pesar de que no he obtenido información sobre el error?**</span><span class="sxs-lookup"><span data-stu-id="85de3-159">**Q: Why did my attempt to join a PC fail although I didn't get any error information?**</span></span>

<span data-ttu-id="85de3-160">**R:** Puede deberse a que el usuario ha iniciado sesión en el dispositivo con la cuenta de administrador integrada.</span><span class="sxs-lookup"><span data-stu-id="85de3-160">**A:** A likely cause is that the user is logged in to the device using the built-in administrator account.</span></span> <span data-ttu-id="85de3-161">Cree una cuenta local distinta antes de usar Azure Active Directory Join para completar la instalación.</span><span class="sxs-lookup"><span data-stu-id="85de3-161">Please create a different local account before using Azure Active Directory Join to complete the setup.</span></span> 

---

<span data-ttu-id="85de3-162">**P: ¿Dónde puedo encontrar instrucciones para la configuración de registro automático de dispositivos?**</span><span class="sxs-lookup"><span data-stu-id="85de3-162">**Q: Where can I find instructions for the setup of automatic device registration?**</span></span>

<span data-ttu-id="85de3-163">**R:** Para ver instrucciones detalladas, consulte [Configuración del registro automático de dispositivos unidos a un dominio de Windows con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="85de3-163">**A:** For detailed instructions, see [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

---

<span data-ttu-id="85de3-164">**P: ¿Dónde puedo encontrar información para solucionar problemas con el registro automático de dispositivos?**</span><span class="sxs-lookup"><span data-stu-id="85de3-164">**Q: Where can I find troubleshooting information about the automatic device registration?**</span></span>

<span data-ttu-id="85de3-165">**R:** Para consultar información sobre solución de problemas, vea:</span><span class="sxs-lookup"><span data-stu-id="85de3-165">**A:** For troubleshooting information, see:</span></span>

- [<span data-ttu-id="85de3-166">Solución de problemas de registro automático de equipos unidos a un dominio en Azure AD: Windows 10 y Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="85de3-166">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)

- [<span data-ttu-id="85de3-167">Solución de problemas de registro automático de equipos unidos a un dominio en Azure AD para clientes de nivel inferior de Windows</span><span class="sxs-lookup"><span data-stu-id="85de3-167">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
 
---

