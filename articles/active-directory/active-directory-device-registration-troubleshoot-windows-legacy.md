---
title: "aaaTroubleshooting Hola el registro automático de dominio de Azure AD los equipos Unidos para clientes de nivel inferior de Windows | Documentos de Microsoft"
description: "Solución de problemas de registro automático de Hola de dominio de Azure AD los equipos Unidos para clientes de nivel inferior de Windows."
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
ms.openlocfilehash: 84fe666576f13de09d1eaa5692517d45a4dbeebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad-for-windows-down-level-clients"></a><span data-ttu-id="ebfba-103">Solución de problemas de registro automático de dominio unido equipos tooAzure AD para clientes de nivel inferior de Windows</span><span class="sxs-lookup"><span data-stu-id="ebfba-103">Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients</span></span> 

<span data-ttu-id="ebfba-104">Este tema es aplicable toohello solo después de los clientes:</span><span class="sxs-lookup"><span data-stu-id="ebfba-104">This topic is applicable only toohello following clients:</span></span> 

- <span data-ttu-id="ebfba-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="ebfba-105">Windows 7</span></span> 
- <span data-ttu-id="ebfba-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="ebfba-106">Windows 8.1</span></span> 
- <span data-ttu-id="ebfba-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="ebfba-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="ebfba-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="ebfba-108">Windows Server 2012</span></span> 
- <span data-ttu-id="ebfba-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="ebfba-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="ebfba-110">Para Windows 10 o Windows Server 2016, consulte [solución de problemas de registro automático de dominio unido equipos tooAzure AD – Windows 10 y Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span><span class="sxs-lookup"><span data-stu-id="ebfba-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="ebfba-111">En este tema se da por supuesto que ha configurado el registro automático de dispositivos Unidos a un dominio como se ha descrito en se describe en [cómo tooconfigure el registro automático de Windows Unidos a dominios dispositivos con Azure Active Directory](active-directory-device-registration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ebfba-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="ebfba-112">Este tema proporciona instrucciones sobre cómo tooresolve posibles problemas de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="ebfba-112">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  
<span data-ttu-id="ebfba-113">Algunos toonote cosas para resultados correcta:</span><span class="sxs-lookup"><span data-stu-id="ebfba-113">Some things toonote for successful outcomes:</span></span> 

- <span data-ttu-id="ebfba-114">El registro de estos clientes en Azure AD se realiza por usuario/dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ebfba-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="ebfba-115">Por ejemplo: si jdoe y jharnett iniciado sesión en el dispositivo toothis, se crea un registro independiente (DeviceID) para cada uno de estos usuarios en la ficha de información de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="ebfba-115">As an example: If jdoe and jharnett log in toothis device, a separate registration (DeviceID) is created for each of these users in hello USER info tab.</span></span>  

- <span data-ttu-id="ebfba-116">Es el registro de estos clientes fuera del cuadro de hello tootry configurado en el inicio de sesión o bloquear/desbloquear y podría haber un retraso de 5 minutos que esto se desencadena mediante una tarea de programador de tareas.</span><span class="sxs-lookup"><span data-stu-id="ebfba-116">Registration of these clients out of hello box is configured tootry at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="ebfba-117">Una nueva instalación de sistema operativo de Hola o anular el registro manual y volver a registrar, puede crear un nuevo registro en Azure AD y dará como resultado varias entradas en la ficha de información de usuario de Hola Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="ebfba-117">A re-install of hello operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="ebfba-118">Paso 1: Recuperar el estado de registro de hello</span><span class="sxs-lookup"><span data-stu-id="ebfba-118">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="ebfba-119">**estado de registro de hello tooverify:**</span><span class="sxs-lookup"><span data-stu-id="ebfba-119">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="ebfba-120">Hola abrir símbolo del sistema como administrador</span><span class="sxs-lookup"><span data-stu-id="ebfba-120">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="ebfba-121">Escriba `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="ebfba-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="ebfba-122">Este comando muestra un cuadro de diálogo que le proporciona más detalles acerca del estado de unión Hola.</span><span class="sxs-lookup"><span data-stu-id="ebfba-122">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="ebfba-124">Paso 2: Evaluar el estado de registro de hello</span><span class="sxs-lookup"><span data-stu-id="ebfba-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="ebfba-125">Si la combinación de hello no fue correcta, cuadro de diálogo de Hola proporciona detalles sobre el problema de Hola que se ha producido.</span><span class="sxs-lookup"><span data-stu-id="ebfba-125">If hello join was not successful, hello dialog box provides you with details about hello issue that has occured.</span></span>

<span data-ttu-id="ebfba-126">**Hola los problemas más comunes son:**</span><span class="sxs-lookup"><span data-stu-id="ebfba-126">**hello most common issues are:**</span></span>

- <span data-ttu-id="ebfba-127">Una configuración incorrecta de AD FS o Azure AD</span><span class="sxs-lookup"><span data-stu-id="ebfba-127">A misconfigured AD FS or Azure AD</span></span>

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="ebfba-129">No está registrado como un usuario de dominio</span><span class="sxs-lookup"><span data-stu-id="ebfba-129">You are not signed on as a domain user</span></span>

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="ebfba-131">Se ha alcanzado una cuota</span><span class="sxs-lookup"><span data-stu-id="ebfba-131">A quota has been reached</span></span>

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="ebfba-133">Hola el servicio no responde</span><span class="sxs-lookup"><span data-stu-id="ebfba-133">hello service is not responding</span></span> 

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="ebfba-135">También puede encontrar información de estado de hello en el registro de eventos de hello en **aplicaciones y servicios Log\Microsoft-unión**.</span><span class="sxs-lookup"><span data-stu-id="ebfba-135">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="ebfba-136">**Hola las causas más comunes para un registro de errores son:**</span><span class="sxs-lookup"><span data-stu-id="ebfba-136">**hello most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="ebfba-137">El equipo no está en la red interna de la organización de Hola o una VPN sin conexión tooan local controlador de dominio de AD.</span><span class="sxs-lookup"><span data-stu-id="ebfba-137">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="ebfba-138">Se registran en el equipo de tooyour con una cuenta de equipo local.</span><span class="sxs-lookup"><span data-stu-id="ebfba-138">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="ebfba-139">Problemas de configuración de servicio:</span><span class="sxs-lookup"><span data-stu-id="ebfba-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="ebfba-140">Hello servidor de federación ha sido configurado toosupport **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="ebfba-140">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="ebfba-141">No hay ningún objeto de punto de conexión de servicio que señala el nombre de dominio verificado de tooyour en Azure AD en bosque de AD de Hola que pertenece el equipo de Hola a.</span><span class="sxs-lookup"><span data-stu-id="ebfba-141">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="ebfba-142">Un usuario ha alcanzado el límite de Hola de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="ebfba-142">A user has reached hello limit of devices.</span></span> <span data-ttu-id="ebfba-143">Consulte Introducción al Registro de dispositivos de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ebfba-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ebfba-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ebfba-144">Next steps</span></span>

<span data-ttu-id="ebfba-145">Para obtener más información, vea hello [registro automático de dispositivos preguntas más frecuentes](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="ebfba-145">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
