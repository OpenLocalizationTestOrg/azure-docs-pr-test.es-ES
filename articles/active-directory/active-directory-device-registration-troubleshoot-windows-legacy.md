---
title: "Solución de problemas de registro automático de equipos unidos a un dominio Azure AD para clientes de nivel inferior de Windows | Microsoft Docs"
description: "Solución de problemas de registro automático de equipos unidos a un dominio Azure AD para clientes de nivel inferior de Windows."
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
ms.openlocfilehash: a7c8ef4c59c53c21258f0c61963d8f994a3946ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad-for-windows-down-level-clients"></a><span data-ttu-id="3065b-103">Solución de problemas de registro automático de equipos unidos a un dominio en Azure AD para clientes de nivel inferior de Windows</span><span class="sxs-lookup"><span data-stu-id="3065b-103">Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients</span></span> 

<span data-ttu-id="3065b-104">Este tema solo es aplicable a los siguientes clientes:</span><span class="sxs-lookup"><span data-stu-id="3065b-104">This topic is applicable only to the following clients:</span></span> 

- <span data-ttu-id="3065b-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="3065b-105">Windows 7</span></span> 
- <span data-ttu-id="3065b-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="3065b-106">Windows 8.1</span></span> 
- <span data-ttu-id="3065b-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="3065b-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="3065b-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="3065b-108">Windows Server 2012</span></span> 
- <span data-ttu-id="3065b-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3065b-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="3065b-110">Para Windows 10 o Windows Server 2016, consulte [Solución de problemas de registro automático de equipos unidos a un dominio Azure AD para Windows 10 y Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span><span class="sxs-lookup"><span data-stu-id="3065b-110">For Windows 10 or Windows Server 2016, see [Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016](active-directory-device-registration-troubleshoot-windows.md).</span></span>

<span data-ttu-id="3065b-111">En este tema se supone que ha configurado el registro automático de dispositivos unidos a un dominio como se describe en [Configuración del registro automático de dispositivos unidos a un dominio de Windows con Azure Active Directory](active-directory-device-registration-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3065b-111">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md).</span></span>
 
<span data-ttu-id="3065b-112">En este tema se proporcionan instrucciones sobre cómo resolver problemas potenciales.</span><span class="sxs-lookup"><span data-stu-id="3065b-112">This topic provides you with troubleshooting guidance on how to resolve potential issues.</span></span>  
<span data-ttu-id="3065b-113">Algunos aspectos que se deben tener en cuenta para obtener buenos resultados:</span><span class="sxs-lookup"><span data-stu-id="3065b-113">Some things to note for successful outcomes:</span></span> 

- <span data-ttu-id="3065b-114">El registro de estos clientes en Azure AD se realiza por usuario/dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3065b-114">Registration of these clients on Azure AD is per user/device.</span></span> <span data-ttu-id="3065b-115">Por ejemplo: si jdoe y jharnett inician sesión en este dispositivo, se crea un registro independiente (Id. de dispositivo) para cada uno de estos usuarios en la pestaña de información de USUARIO.</span><span class="sxs-lookup"><span data-stu-id="3065b-115">As an example: If jdoe and jharnett log in to this device, a separate registration (DeviceID) is created for each of these users in the USER info tab.</span></span>  

- <span data-ttu-id="3065b-116">El registro de estos clientes predeterminados se configura para probar el inicio de sesión o el bloqueo/desbloqueo, y se puede experimentar un retraso de 5 minutos que se desencadena con la tarea del Programador de tareas.</span><span class="sxs-lookup"><span data-stu-id="3065b-116">Registration of these clients out of the box is configured to try at either logon or lock/unlock and there could be 5-minute delay that this is triggered using a Task Scheduler task.</span></span> 

- <span data-ttu-id="3065b-117">La reinstalación del sistema operativo o la anulación del registro y el nuevo registro de forma manual pueden crear un nuevo registro en Azure AD y generar varias entradas en la pestaña de información de USUARIO de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="3065b-117">A re-install of the operating system or a manual un-register and re-register may create a new registration on Azure AD and will result in multiple entries under the USER info tab in the Azure portal.</span></span> 


## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="3065b-118">Paso 1: Recuperar el estado del registro</span><span class="sxs-lookup"><span data-stu-id="3065b-118">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="3065b-119">**Para verificar el estado del registro:**</span><span class="sxs-lookup"><span data-stu-id="3065b-119">**To verify the registration status:**</span></span>  

1. <span data-ttu-id="3065b-120">Abra el símbolo del sistema como administrador.</span><span class="sxs-lookup"><span data-stu-id="3065b-120">Open the command prompt as an administrator</span></span> 

2. <span data-ttu-id="3065b-121">Escriba `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="3065b-121">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="3065b-122">Este comando muestra un cuadro de diálogo que proporciona más detalles sobre el estado de la unión.</span><span class="sxs-lookup"><span data-stu-id="3065b-122">This command displays a dialog box that provides you with more details about the join status.</span></span>

![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="3065b-124">Paso 2: Evaluar el estado del registro</span><span class="sxs-lookup"><span data-stu-id="3065b-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="3065b-125">Si la unión no se realiza correctamente, el cuadro de diálogo proporciona detalles sobre el problema que se ha producido.</span><span class="sxs-lookup"><span data-stu-id="3065b-125">If the join was not successful, the dialog box provides you with details about the issue that has occured.</span></span>

<span data-ttu-id="3065b-126">**Los problemas más comunes son:**</span><span class="sxs-lookup"><span data-stu-id="3065b-126">**The most common issues are:**</span></span>

- <span data-ttu-id="3065b-127">Una configuración incorrecta de AD FS o Azure AD</span><span class="sxs-lookup"><span data-stu-id="3065b-127">A misconfigured AD FS or Azure AD</span></span>

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="3065b-129">No está registrado como un usuario de dominio</span><span class="sxs-lookup"><span data-stu-id="3065b-129">You are not signed on as a domain user</span></span>

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="3065b-131">Se ha alcanzado una cuota</span><span class="sxs-lookup"><span data-stu-id="3065b-131">A quota has been reached</span></span>

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="3065b-133">El servicio no responde</span><span class="sxs-lookup"><span data-stu-id="3065b-133">The service is not responding</span></span> 

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="3065b-135">También puede encontrar la información de estado en el registro de eventos en **Registros de aplicaciones y servicios\Microsoft-Workplace Join**.</span><span class="sxs-lookup"><span data-stu-id="3065b-135">You can also find the status information in the event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="3065b-136">**Las causas más comunes del error de un registro son:**</span><span class="sxs-lookup"><span data-stu-id="3065b-136">**The most common causes for a failed registration are:**</span></span> 

- <span data-ttu-id="3065b-137">El equipo no está en la red interna de la organización o en una VPN sin conexión a una implementación local del controlador de dominio de AD.</span><span class="sxs-lookup"><span data-stu-id="3065b-137">Your computer is not on the organization’s internal network or a VPN without connection to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="3065b-138">Ha iniciado sesión en el equipo con una cuenta del equipo local.</span><span class="sxs-lookup"><span data-stu-id="3065b-138">You are logged on to your computer with a local computer account.</span></span> 

- <span data-ttu-id="3065b-139">Problemas de configuración de servicio:</span><span class="sxs-lookup"><span data-stu-id="3065b-139">Service configuration issues:</span></span> 

  - <span data-ttu-id="3065b-140">El servidor de federación se ha configurado para admitir **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="3065b-140">The federation server has been configured to support **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="3065b-141">No hay ningún objeto de punto de conexión de servicio que haga referencia a su nombre de dominio comprobado en Azure AD en el bosque de AD al que pertenece el equipo.</span><span class="sxs-lookup"><span data-stu-id="3065b-141">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to.</span></span>

  - <span data-ttu-id="3065b-142">Un usuario ha alcanzado el límite de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="3065b-142">A user has reached the limit of devices.</span></span> <span data-ttu-id="3065b-143">Consulte Introducción al Registro de dispositivos de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3065b-143">Please see Get Started with Azure Active Directory Device Registration.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3065b-144">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="3065b-144">Next steps</span></span>

<span data-ttu-id="3065b-145">Para más información, vea [Preguntas más frecuentes sobre el registro automático de dispositivos](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="3065b-145">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
