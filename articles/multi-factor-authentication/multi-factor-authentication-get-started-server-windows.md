---
title: "aaaWindows autenticación y el servidor de MFA de Azure | Documentos de Microsoft"
description: "Se trata de una página de autenticación multifactor de Azure de Hola que te ayudará a implementar la autenticación de Windows y el servidor de autenticación multifactor de Azure."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 19a4043f-c4ce-43c0-80e7-2548ee92cb74
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/06/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 0fc38fd751966bf883d4eae7c48055988922af80
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a><span data-ttu-id="9b237-103">Servidor de Autenticación de Windows y Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="9b237-103">Windows Authentication and Azure Multi-Factor Authentication Server</span></span>
<span data-ttu-id="9b237-104">Utilice sección de autenticación de Windows hello de hello tooenable de servidor de autenticación multifactor de Azure y configurar la autenticación de Windows para las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9b237-104">Use hello Windows Authentication section of hello Azure Multi-Factor Authentication Server tooenable and configure Windows authentication for applications.</span></span> <span data-ttu-id="9b237-105">Antes de configurar la autenticación de Windows, tenga Hola lista en la cuenta siguiente:</span><span class="sxs-lookup"><span data-stu-id="9b237-105">Before you set up Windows Authentication, keep hello following list in mind:</span></span>

* <span data-ttu-id="9b237-106">Después de la instalación, reinicie hello Azure la autenticación multifactor para el efecto de tootake de servicios de Terminal Server.</span><span class="sxs-lookup"><span data-stu-id="9b237-106">After setup, reboot hello Azure Multi-Factor Authentication for Terminal Services tootake effect.</span></span>
* <span data-ttu-id="9b237-107">Si se comprueba 'Coincidencia de usuario requieren la autenticación multifactor Azure' y no está en la lista de usuarios de hello, no será capaz de toolog en la máquina de hello después del reinicio.</span><span class="sxs-lookup"><span data-stu-id="9b237-107">If ‘Require Azure Multi-Factor Authentication user match’ is checked and you are not in hello user list, you will not be able toolog into hello machine after reboot.</span></span>
* <span data-ttu-id="9b237-108">Direcciones IP depende de si aplicación hello puede proporcionar la dirección IP del cliente con la autenticación de Hola Hola de confianza.</span><span class="sxs-lookup"><span data-stu-id="9b237-108">Trusted IPs is dependent on whether hello application can provide hello client IP with hello authentication.</span></span> <span data-ttu-id="9b237-109">Actualmente solo se admite Terminal Services.</span><span class="sxs-lookup"><span data-stu-id="9b237-109">Currently only Terminal Services is supported.</span></span>  

> [!NOTE]
> <span data-ttu-id="9b237-110">Esta característica no está admitida toosecure Terminal Services en Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="9b237-110">This feature is not supported toosecure Terminal Services on Windows Server 2012 R2.</span></span>

## <a name="toosecure-an-application-with-windows-authentication-use-hello-following-procedure"></a><span data-ttu-id="9b237-111">toosecure una aplicación con la autenticación de Windows, siguiendo el procedimiento de Hola de uso.</span><span class="sxs-lookup"><span data-stu-id="9b237-111">toosecure an application with Windows Authentication, use hello following procedure.</span></span>
1. <span data-ttu-id="9b237-112">Haga clic en icono de autenticación de Windows hello Hola servidor Azure Multi-factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="9b237-112">In hello Azure Multi-Factor Authentication Server click hello Windows Authentication icon.</span></span>
   <span data-ttu-id="9b237-113">![Autenticación de Windows](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span><span class="sxs-lookup"><span data-stu-id="9b237-113">![Windows Authentication](./media/multi-factor-authentication-get-started-server-windows/windowsauth.png)</span></span>
2. <span data-ttu-id="9b237-114">Comprobar hello **habilitar la autenticación de Windows** casilla de verificación.</span><span class="sxs-lookup"><span data-stu-id="9b237-114">Check hello **Enable Windows Authentication** checkbox.</span></span> <span data-ttu-id="9b237-115">De forma predeterminada, esta casilla está desmarcada.</span><span class="sxs-lookup"><span data-stu-id="9b237-115">By default, this box is unchecked.</span></span>
3. <span data-ttu-id="9b237-116">pestaña de aplicaciones de Hello permite Hola administrador tooconfigure una o más aplicaciones para la autenticación de Windows.</span><span class="sxs-lookup"><span data-stu-id="9b237-116">hello Applications tab allows hello administrator tooconfigure one or more applications for Windows Authentication.</span></span>
4. <span data-ttu-id="9b237-117">Seleccione un servidor o una aplicación: especifique si el servidor o la aplicación hello está habilitada.</span><span class="sxs-lookup"><span data-stu-id="9b237-117">Select a server or application – specify whether hello server/application is enabled.</span></span> <span data-ttu-id="9b237-118">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9b237-118">Click **OK**.</span></span>
5. <span data-ttu-id="9b237-119">Haga clic en **Agregar...**</span><span class="sxs-lookup"><span data-stu-id="9b237-119">Click **Add…**</span></span>
6. <span data-ttu-id="9b237-120">pestaña de IP de confianza de Hello permite tooskip Azure Multi-factor Authentication para sesiones de Windows que se originan de direcciones IP específicas.</span><span class="sxs-lookup"><span data-stu-id="9b237-120">hello Trusted IPs tab allows you tooskip Azure Multi-Factor Authentication for Windows sessions originating from specific IPs.</span></span> <span data-ttu-id="9b237-121">Por ejemplo, si los empleados usan la aplicación hello desde office hello y desde casa, puede decidir que no desea que sus teléfonos suenen para Azure Multi-factor Authentication mientras se encuentran en office Hola.</span><span class="sxs-lookup"><span data-stu-id="9b237-121">For example, if employees use hello application from hello office and from home, you may decide you don't want their phones ringing for Azure Multi-Factor Authentication while at hello office.</span></span> <span data-ttu-id="9b237-122">Para ello, especificaría subred de la oficina de hello como entrada de IP de confianza.</span><span class="sxs-lookup"><span data-stu-id="9b237-122">For this, you would specify hello office subnet as Trusted IPs entry.</span></span>
7. <span data-ttu-id="9b237-123">Haga clic en **Agregar...**</span><span class="sxs-lookup"><span data-stu-id="9b237-123">Click **Add…**</span></span>
8. <span data-ttu-id="9b237-124">Seleccione **IP única** si desea que tooskip una única dirección IP.</span><span class="sxs-lookup"><span data-stu-id="9b237-124">Select **Single IP** if you would like tooskip a single IP address.</span></span>
9. <span data-ttu-id="9b237-125">Seleccione **intervalo de IP** si desea que tooskip todo un intervalo de IP.</span><span class="sxs-lookup"><span data-stu-id="9b237-125">Select **IP Range** if you would like tooskip an entire IP range.</span></span> <span data-ttu-id="9b237-126">Ejemplo 10.63.193.1-10.63.193.100.</span><span class="sxs-lookup"><span data-stu-id="9b237-126">Example 10.63.193.1-10.63.193.100.</span></span>
10. <span data-ttu-id="9b237-127">Seleccione **subred** si desea que toospecify un intervalo de direcciones IP mediante la notación de subred.</span><span class="sxs-lookup"><span data-stu-id="9b237-127">Select **Subnet** if you would like toospecify a range of IPs using subnet notation.</span></span> <span data-ttu-id="9b237-128">Escriba Hola dirección IP inicial y seleccione Hola máscara de red adecuada de la lista desplegable de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b237-128">Enter hello subnet's starting IP and pick hello appropriate netmask from hello drop-down list.</span></span>
11. <span data-ttu-id="9b237-129">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="9b237-129">Click **OK**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9b237-130">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9b237-130">Next steps</span></span>

- [<span data-ttu-id="9b237-131">Configuración de dispositivos de VPN de terceros para el servidor Azure MFA</span><span class="sxs-lookup"><span data-stu-id="9b237-131">Configure third-party VPN appliances for Azure MFA Server</span></span>](multi-factor-authentication-advanced-vpn-configurations.md)

- [<span data-ttu-id="9b237-132">Aumentar la infraestructura de autenticación existente con hello extensión NPS para Azure MFA</span><span class="sxs-lookup"><span data-stu-id="9b237-132">Augment your existing authentication infrastructure with hello NPS extension for Azure MFA</span></span>](multi-factor-authentication-nps-extension.md)
