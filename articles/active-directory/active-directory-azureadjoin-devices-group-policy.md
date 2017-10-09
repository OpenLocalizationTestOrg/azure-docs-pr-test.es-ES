---
title: experimenta aaaConnect dispositivos Unidos a dominio tooAzure AD para Windows 10 | Documentos de Microsoft
description: "Explica cómo los administradores pueden configurar la red de empresa de directiva de grupo tooenable dispositivos toobe toohello Unidos a un dominio."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 2ff29f3e-5325-4f43-9baa-6ae8d6bad3e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 9766aa702352dea2ecad3a9a0bdf8d3286ee6d91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="connect-domain-joined-devices-tooazure-ad-for-windows-10-experiences"></a><span data-ttu-id="769ba-103">Conectar dispositivos Unidos a dominio tooAzure AD para experiencias de Windows 10</span><span class="sxs-lookup"><span data-stu-id="769ba-103">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>
<span data-ttu-id="769ba-104">Unión a un dominio es organizaciones de forma tradicional de hello han conectado dispositivos para el trabajo de hello en los últimos 15 años y mucho más.</span><span class="sxs-lookup"><span data-stu-id="769ba-104">Domain join is hello traditional way organizations have connected devices for work for hello last 15 years and more.</span></span> <span data-ttu-id="769ba-105">Ha habilitado toosign de usuarios en los dispositivos tootheir mediante el uso de su trabajo de Windows Server Active Directory (Active Directory) o escolares y permitido toofully de TI administran estos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="769ba-105">It has enabled users toosign in tootheir devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT toofully manage these devices.</span></span> <span data-ttu-id="769ba-106">Las organizaciones suelen basarse en métodos tooprovision dispositivos toousers de creación de imágenes y generalmente se utiliza System Center Configuration Manager (SCCM) o directiva de grupo toomanage ellos.</span><span class="sxs-lookup"><span data-stu-id="769ba-106">Organizations typically rely on imaging methods tooprovision devices toousers and generally use System Center Configuration Manager (SCCM) or Group Policy toomanage them.</span></span>


<span data-ttu-id="769ba-107">Unión a un dominio de Windows 10 proporciona Hola después ventajas después de conectar dispositivos tooAzure Active Directory (Azure AD):</span><span class="sxs-lookup"><span data-stu-id="769ba-107">Domain join in Windows 10 provides you with hello following benefits after you connect devices tooAzure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="769ba-108">Inicio de sesión (SSO) tooAzure AD recursos individuales desde cualquier lugar</span><span class="sxs-lookup"><span data-stu-id="769ba-108">Single sign-on (SSO) tooAzure AD resources from anywhere</span></span>
* <span data-ttu-id="769ba-109">Obtener acceso a enterprise toohello tienda Windows mediante el uso de trabajo o escuela cuentas (no requerida ninguna cuenta de Microsoft)</span><span class="sxs-lookup"><span data-stu-id="769ba-109">Access toohello enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="769ba-110">Movilidad de las configuraciones de usuario conforme a la empresa entre dispositivos que usan cuentas profesionales o educativas (sin necesidad de una cuenta Microsoft)</span><span class="sxs-lookup"><span data-stu-id="769ba-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="769ba-111">Autenticación segura y práctico inicio de sesión para cuentas profesionales o educativas con Windows Hello para empresas y Windows Hello</span><span class="sxs-lookup"><span data-stu-id="769ba-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="769ba-112">Capacidad toorestrict acceso solo toodevices que cumplen con la configuración de directiva de grupo de organización de dispositivo</span><span class="sxs-lookup"><span data-stu-id="769ba-112">Ability toorestrict access only toodevices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="769ba-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="769ba-113">Prerequisites</span></span>
<span data-ttu-id="769ba-114">Unión a un dominio continúa toobe útil.</span><span class="sxs-lookup"><span data-stu-id="769ba-114">Domain join continues toobe useful.</span></span> <span data-ttu-id="769ba-115">Sin embargo, los beneficios de hello Azure AD tooget de SSO, itinerancia de configuración con o cuentas, educativas y tener acceso a almacén tooWindows con trabajo cuentas profesionales o educativas, necesitará Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="769ba-115">However, tooget hello Azure AD benefits of SSO, roaming of settings with work or school accounts, and access tooWindows Store with work or school accounts, you will need hello following:</span></span>

* <span data-ttu-id="769ba-116">Suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="769ba-116">Azure AD subscription</span></span>
* <span data-ttu-id="769ba-117">Azure AD Connect tooextend hello tooAzure directory AD local</span><span class="sxs-lookup"><span data-stu-id="769ba-117">Azure AD Connect tooextend hello on-premises directory tooAzure AD</span></span>
* <span data-ttu-id="769ba-118">Directiva que ha establecido tooconnect dispositivos Unidos a dominio tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="769ba-118">Policy that's set tooconnect domain-joined devices tooAzure AD</span></span>
* <span data-ttu-id="769ba-119">Compilación de Windows 10 (compilación 10551 o posterior) en los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="769ba-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="769ba-120">tooenable Windows Hello para empresas y Windows Hello, también necesitará siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="769ba-120">tooenable Windows Hello for Business and Windows Hello, you will also need hello following:</span></span>

- <span data-ttu-id="769ba-121">**Infraestructura de clave pública (PKI)** para la emisión de certificados de usuario.</span><span class="sxs-lookup"><span data-stu-id="769ba-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="769ba-122">**Rama actual de System Center Configuration Manager** -necesita tooinstall versión 1606 o superior.</span><span class="sxs-lookup"><span data-stu-id="769ba-122">**System Center Configuration Manager Current Branch** - You need tooinstall version 1606 or better.</span></span>  
<span data-ttu-id="769ba-123">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="769ba-123">For more information, see:</span></span> 
    - [<span data-ttu-id="769ba-124">Documentación de System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="769ba-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="769ba-125">Blog del equipo de System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="769ba-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="769ba-126">Configuración de Windows Hello para empresas en System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="769ba-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="769ba-127">Como un requisito de implementación de PKI toohello alternativo, puede hacer siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="769ba-127">As an alternative toohello PKI deployment requirement, you can do hello following:</span></span>

* <span data-ttu-id="769ba-128">Tener algunos controladores de dominio con los Servicios de dominio de Active Directory para Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="769ba-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="769ba-129">tooenable acceso condicional, puede crear configuraciones de directiva de grupo que permitir que los dispositivos Unidos a un toodomain de acceso con sin implementaciones adicionales.</span><span class="sxs-lookup"><span data-stu-id="769ba-129">tooenable conditional access, you can create Group Policy settings that allow access toodomain-joined devices with no additional deployments.</span></span> <span data-ttu-id="769ba-130">toomanage control de acceso basado en cumplimiento de dispositivo de hello, necesitará la siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="769ba-130">toomanage access control based on compliance of hello device, you will need hello following:</span></span>

* <span data-ttu-id="769ba-131">Rama actual de System Center Configuration Manager (1606 o posterior) para escenarios de Windows Hello para empresas</span><span class="sxs-lookup"><span data-stu-id="769ba-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="769ba-132">Instrucciones de implementación</span><span class="sxs-lookup"><span data-stu-id="769ba-132">Deployment instructions</span></span>

<span data-ttu-id="769ba-133">toodeploy, siga los pasos de hello enumerados en [cómo tooconfigure el registro automático de Windows Unidos a dominios dispositivos con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span><span class="sxs-lookup"><span data-stu-id="769ba-133">toodeploy, follow hello steps listed in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="769ba-134">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="769ba-134">Next step</span></span>
* [<span data-ttu-id="769ba-135">Windows 10 para empresa hello: dispositivos de toouse de formas de trabajo</span><span class="sxs-lookup"><span data-stu-id="769ba-135">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="769ba-136">Extender nube dispositivos de tooWindows 10 capacidades a través de Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="769ba-136">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="769ba-137">Conozca los escenarios de uso de Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="769ba-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="769ba-138">Conectar dispositivos Unidos a dominio tooAzure AD para experiencias de Windows 10</span><span class="sxs-lookup"><span data-stu-id="769ba-138">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="769ba-139">Configuración de Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="769ba-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

