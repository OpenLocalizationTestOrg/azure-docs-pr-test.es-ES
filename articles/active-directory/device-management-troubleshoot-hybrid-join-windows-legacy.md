---
title: "aaaTroubleshooting híbrido Azure Active Directory unido a dispositivos de nivel inferior | Documentos de Microsoft"
description: "Solución de problemas de dispositivos híbridos de nivel inferior unidos a Azure Active Directory"
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
ms.openlocfilehash: edd56b89579fac6b427732902284ad9c568b87b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-down-level-devices"></a><span data-ttu-id="fb5e6-103">Solución de problemas de dispositivos híbridos de nivel inferior unidos a Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fb5e6-103">Troubleshooting hybrid Azure Active Directory joined down-level devices</span></span> 

<span data-ttu-id="fb5e6-104">Este tema es aplicable toohello solo después de dispositivos:</span><span class="sxs-lookup"><span data-stu-id="fb5e6-104">This topic is applicable only toohello following devices:</span></span> 

- <span data-ttu-id="fb5e6-105">Windows 7</span><span class="sxs-lookup"><span data-stu-id="fb5e6-105">Windows 7</span></span> 
- <span data-ttu-id="fb5e6-106">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="fb5e6-106">Windows 8.1</span></span> 
- <span data-ttu-id="fb5e6-107">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="fb5e6-107">Windows Server 2008 R2</span></span> 
- <span data-ttu-id="fb5e6-108">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="fb5e6-108">Windows Server 2012</span></span> 
- <span data-ttu-id="fb5e6-109">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="fb5e6-109">Windows Server 2012 R2</span></span> 
 

<span data-ttu-id="fb5e6-110">Para Windows 10 o Windows Server 2016, consulte [Solución de problemas de dispositivos híbridos de Windows 10 y Windows Server 2016 unidos a Azure Active Directory](device-management-troubleshoot-hybrid-join-windows-current.md).</span><span class="sxs-lookup"><span data-stu-id="fb5e6-110">For Windows 10 or Windows Server 2016, see [Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices](device-management-troubleshoot-hybrid-join-windows-current.md).</span></span>

<span data-ttu-id="fb5e6-111">En este tema se da por supuesto que tiene [dispositivos Unidos a un híbrido configurado Azure Active Directory](device-management-hybrid-azuread-joined-devices-setup.md) hello toosupport los escenarios siguientes:</span><span class="sxs-lookup"><span data-stu-id="fb5e6-111">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="fb5e6-112">Acceso condicional basado en dispositivos</span><span class="sxs-lookup"><span data-stu-id="fb5e6-112">Device-based conditional access</span></span>

- [<span data-ttu-id="fb5e6-113">Perfiles móviles de empresa</span><span class="sxs-lookup"><span data-stu-id="fb5e6-113">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="fb5e6-114">Windows Hello para empresas</span><span class="sxs-lookup"><span data-stu-id="fb5e6-114">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md) 





<span data-ttu-id="fb5e6-115">Este tema proporciona instrucciones sobre cómo tooresolve posibles problemas de solución de problemas.</span><span class="sxs-lookup"><span data-stu-id="fb5e6-115">This topic provides you with troubleshooting guidance on how tooresolve potential issues.</span></span>  

<span data-ttu-id="fb5e6-116">**Qué debería saber:**</span><span class="sxs-lookup"><span data-stu-id="fb5e6-116">**What you should know:**</span></span> 

- <span data-ttu-id="fb5e6-117">número máximo de Hola de dispositivos por usuario está centrado en los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="fb5e6-117">hello maximum number of devices per user is device-centric.</span></span> <span data-ttu-id="fb5e6-118">Por ejemplo, si *jdoe* y *jharnett* dispositivo de inicio de sesión tooa, se crea un registro independiente (DeviceID) para cada uno de ellos en hello **usuario** ficha información.</span><span class="sxs-lookup"><span data-stu-id="fb5e6-118">For example, if *jdoe* and *jharnett* sign-in tooa device, a separate registration (DeviceID) is created for each of them in hello **USER** info tab.</span></span>  

- <span data-ttu-id="fb5e6-119">Hola registro inicial / combinación de dispositivos es tooperform configurado un intento de inicio de sesión o bloquear / desbloquear.</span><span class="sxs-lookup"><span data-stu-id="fb5e6-119">hello initial registration / join of devices is configured tooperform an attempt at either logon or lock / unlock.</span></span> <span data-ttu-id="fb5e6-120">Podría haber un retraso de 5 minutos desencadenado por una tarea de programador de tareas.</span><span class="sxs-lookup"><span data-stu-id="fb5e6-120">There could be 5-minute delay triggered by a task scheduler task.</span></span> 

- <span data-ttu-id="fb5e6-121">Una reinstalación del sistema operativo de Hola o un manual unregister y vuelva a registrar pueden crear un nuevo registro en Azure AD y da como resultado varias entradas en la ficha de información de usuario de hello en Hola portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="fb5e6-121">A reinstall of hello operating system or a manual unregister and re-register may create a new registration on Azure AD and results in multiple entries under hello USER info tab in hello Azure portal.</span></span> 


## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="fb5e6-122">Paso 1: Recuperar el estado de registro de hello</span><span class="sxs-lookup"><span data-stu-id="fb5e6-122">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="fb5e6-123">**estado de registro de hello tooverify:**</span><span class="sxs-lookup"><span data-stu-id="fb5e6-123">**tooverify hello registration status:**</span></span>  

1. <span data-ttu-id="fb5e6-124">Hola abrir símbolo del sistema como administrador</span><span class="sxs-lookup"><span data-stu-id="fb5e6-124">Open hello command prompt as an administrator</span></span> 

2. <span data-ttu-id="fb5e6-125">Escriba `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span><span class="sxs-lookup"><span data-stu-id="fb5e6-125">Type `"%programFiles%\Microsoft Workplace Join\autoworkplace.exe /i"`</span></span>

<span data-ttu-id="fb5e6-126">Este comando muestra un cuadro de diálogo que le proporciona más detalles acerca del estado de unión Hola.</span><span class="sxs-lookup"><span data-stu-id="fb5e6-126">This command displays a dialog box that provides you with more details about hello join status.</span></span>

![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/01.png)


## <a name="step-2-evaluate-hello-hybrid-azure-ad-join-status"></a><span data-ttu-id="fb5e6-128">Paso 2: Evaluar el estado de unión de Azure AD de hello híbrida</span><span class="sxs-lookup"><span data-stu-id="fb5e6-128">Step 2: Evaluate hello hybrid Azure AD join status</span></span> 

<span data-ttu-id="fb5e6-129">Si la combinación de Azure AD de hello híbrida no fue correcta, cuadro de diálogo de hello proporciona detalles sobre el problema de Hola que se ha producido.</span><span class="sxs-lookup"><span data-stu-id="fb5e6-129">If hello hybrid Azure AD join was not successful, hello dialog box provides you with details about hello issue that has occurred.</span></span>

<span data-ttu-id="fb5e6-130">**Hola los problemas más comunes son:**</span><span class="sxs-lookup"><span data-stu-id="fb5e6-130">**hello most common issues are:**</span></span>

- <span data-ttu-id="fb5e6-131">Una configuración incorrecta de AD FS o Azure AD</span><span class="sxs-lookup"><span data-stu-id="fb5e6-131">A misconfigured AD FS or Azure AD</span></span>

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/02.png)

- <span data-ttu-id="fb5e6-133">No está registrado como un usuario de dominio</span><span class="sxs-lookup"><span data-stu-id="fb5e6-133">You are not signed on as a domain user</span></span>

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/03.png)

- <span data-ttu-id="fb5e6-135">Se ha alcanzado una cuota</span><span class="sxs-lookup"><span data-stu-id="fb5e6-135">A quota has been reached</span></span>

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/04.png)

- <span data-ttu-id="fb5e6-137">Hola el servicio no responde</span><span class="sxs-lookup"><span data-stu-id="fb5e6-137">hello service is not responding</span></span> 

    ![Workplace Join for Windows](./media/active-directory-device-registration-troubleshoot-windows-legacy/05.png)

<span data-ttu-id="fb5e6-139">También puede encontrar información de estado de hello en el registro de eventos de hello en **aplicaciones y servicios Log\Microsoft-unión**.</span><span class="sxs-lookup"><span data-stu-id="fb5e6-139">You can also find hello status information in hello event log under **Applications and Services Log\Microsoft-Workplace Join**.</span></span>
  
<span data-ttu-id="fb5e6-140">**Hola las causas más comunes para una combinación de Azure AD errores híbrida son:**</span><span class="sxs-lookup"><span data-stu-id="fb5e6-140">**hello most common causes for a failed hybrid Azure AD join are:**</span></span> 

- <span data-ttu-id="fb5e6-141">El equipo no está en la red interna de la organización de Hola o una VPN sin conexión tooan local controlador de dominio de AD.</span><span class="sxs-lookup"><span data-stu-id="fb5e6-141">Your computer is not on hello organization’s internal network or a VPN without connection tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="fb5e6-142">Se registran en el equipo de tooyour con una cuenta de equipo local.</span><span class="sxs-lookup"><span data-stu-id="fb5e6-142">You are logged on tooyour computer with a local computer account.</span></span> 

- <span data-ttu-id="fb5e6-143">Problemas de configuración de servicio:</span><span class="sxs-lookup"><span data-stu-id="fb5e6-143">Service configuration issues:</span></span> 

  - <span data-ttu-id="fb5e6-144">Hello servidor de federación ha sido configurado toosupport **WIAORMULTIAUTHN**.</span><span class="sxs-lookup"><span data-stu-id="fb5e6-144">hello federation server has been configured toosupport **WIAORMULTIAUTHN**.</span></span> 

  - <span data-ttu-id="fb5e6-145">No hay ningún objeto de punto de conexión de servicio que señala el nombre de dominio verificado de tooyour en Azure AD en bosque de AD de Hola que pertenece el equipo de Hola a.</span><span class="sxs-lookup"><span data-stu-id="fb5e6-145">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to.</span></span>

  - <span data-ttu-id="fb5e6-146">Un usuario ha alcanzado el límite de Hola de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="fb5e6-146">A user has reached hello limit of devices.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="fb5e6-147">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="fb5e6-147">Next steps</span></span>

<span data-ttu-id="fb5e6-148">Si tiene preguntas, consulte hello [preguntas más frecuentes sobre la administración de dispositivos](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="fb5e6-148">For questions, see hello [device management FAQ](device-management-faq.md)</span></span>  
