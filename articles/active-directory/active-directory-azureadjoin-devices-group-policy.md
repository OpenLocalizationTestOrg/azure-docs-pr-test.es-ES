---
title: "Experiencias de conexión de dispositivos unidos a un dominio a Azure AD para Windows 10 | Microsoft Docs"
description: "Explica cómo los administradores pueden configurar directivas de grupo para permitir que los dispositivos se unan mediante dominio a la red empresarial."
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
ms.openlocfilehash: 9c91579d20bb84701f6d0b97d944728c84044adf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="connect-domain-joined-devices-to-azure-ad-for-windows-10-experiences"></a><span data-ttu-id="281bc-103">Experiencias de conexión de dispositivos unidos a un dominio a Azure AD para Windows 10</span><span class="sxs-lookup"><span data-stu-id="281bc-103">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>
<span data-ttu-id="281bc-104">Durante los últimos 15 años o más, las organizaciones emplean el método tradicional de unirse a un dominio para que los dispositivos conectados funcionen.</span><span class="sxs-lookup"><span data-stu-id="281bc-104">Domain join is the traditional way organizations have connected devices for work for the last 15 years and more.</span></span> <span data-ttu-id="281bc-105">Esto ha hecho posible que los usuarios inicien sesión en sus dispositivos con sus cuentas profesionales o educativas de Windows Server Active Directory (Active Directory) y que los administradores de TI puedan administrar esos dispositivos por completo.</span><span class="sxs-lookup"><span data-stu-id="281bc-105">It has enabled users to sign in to their devices by using their Windows Server Active Directory (Active Directory) work or school accounts and allowed IT to fully manage these devices.</span></span> <span data-ttu-id="281bc-106">Las organizaciones suelen confían en los métodos de creación de imágenes para aprovisionar los dispositivos de los usuarios y usan generalmente System Center Configuration Manager (SCCM) o la directiva de grupo para administrarlos.</span><span class="sxs-lookup"><span data-stu-id="281bc-106">Organizations typically rely on imaging methods to provision devices to users and generally use System Center Configuration Manager (SCCM) or Group Policy to manage them.</span></span>


<span data-ttu-id="281bc-107">Unirse a un dominio en Windows 10 proporciona las siguientes ventajas después de haber conectado los dispositivos a Azure Active Directory (Azure AD):</span><span class="sxs-lookup"><span data-stu-id="281bc-107">Domain join in Windows 10 provides you with the following benefits after you connect devices to Azure Active Directory (Azure AD):</span></span>

* <span data-ttu-id="281bc-108">Inicio de sesión único (SSO) a los recursos de Azure AD desde cualquier lugar</span><span class="sxs-lookup"><span data-stu-id="281bc-108">Single sign-on (SSO) to Azure AD resources from anywhere</span></span>
* <span data-ttu-id="281bc-109">Acceso a la Tienda Windows para empresas mediante cuentas profesionales o educativas (sin necesidad de una cuenta Microsoft)</span><span class="sxs-lookup"><span data-stu-id="281bc-109">Access to the enterprise Windows Store by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="281bc-110">Movilidad de las configuraciones de usuario conforme a la empresa entre dispositivos que usan cuentas profesionales o educativas (sin necesidad de una cuenta Microsoft)</span><span class="sxs-lookup"><span data-stu-id="281bc-110">Enterprise-compliant roaming of user settings across devices by using work or school accounts (no Microsoft account required)</span></span>
* <span data-ttu-id="281bc-111">Autenticación segura y práctico inicio de sesión para cuentas profesionales o educativas con Windows Hello para empresas y Windows Hello</span><span class="sxs-lookup"><span data-stu-id="281bc-111">Strong authentication and convenient sign-in for work or school accounts with Windows Hello for Business and Windows Hello</span></span>
* <span data-ttu-id="281bc-112">Posibilidad de limitar el acceso únicamente a los dispositivos que cumplan con la configuración de la directiva de grupo para los dispositivos de la organización</span><span class="sxs-lookup"><span data-stu-id="281bc-112">Ability to restrict access only to devices that comply with organizational device Group Policy settings</span></span>

## <a name="prerequisites"></a><span data-ttu-id="281bc-113">Requisitos previos</span><span class="sxs-lookup"><span data-stu-id="281bc-113">Prerequisites</span></span>
<span data-ttu-id="281bc-114">Unirse a un dominio sigue resultando útil.</span><span class="sxs-lookup"><span data-stu-id="281bc-114">Domain join continues to be useful.</span></span> <span data-ttu-id="281bc-115">Sin embargo, para disfrutar de los beneficios de Azure AD respecto del inicio de sesión único, la movilidad de la configuración con las cuentas profesionales o educativas y el acceso a la Tienda Windows con las cuentas profesionales o educativas, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="281bc-115">However, to get the Azure AD benefits of SSO, roaming of settings with work or school accounts, and access to Windows Store with work or school accounts, you will need the following:</span></span>

* <span data-ttu-id="281bc-116">Suscripción de Azure AD</span><span class="sxs-lookup"><span data-stu-id="281bc-116">Azure AD subscription</span></span>
* <span data-ttu-id="281bc-117">Azure AD Connect para ampliar el directorio local a Azure AD</span><span class="sxs-lookup"><span data-stu-id="281bc-117">Azure AD Connect to extend the on-premises directory to Azure AD</span></span>
* <span data-ttu-id="281bc-118">Establecimiento de la directiva para conectar los dispositivos unidos a un dominio a Azure AD</span><span class="sxs-lookup"><span data-stu-id="281bc-118">Policy that's set to connect domain-joined devices to Azure AD</span></span>
* <span data-ttu-id="281bc-119">Compilación de Windows 10 (compilación 10551 o posterior) en los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="281bc-119">Windows 10 build (build 10551 or newer) for devices</span></span>

<span data-ttu-id="281bc-120">Para habilitar Windows Hello para empresas y Windows Hello, también necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="281bc-120">To enable Windows Hello for Business and Windows Hello, you will also need the following:</span></span>

- <span data-ttu-id="281bc-121">**Infraestructura de clave pública (PKI)** para la emisión de certificados de usuario.</span><span class="sxs-lookup"><span data-stu-id="281bc-121">**Public key infrastructure (PKI)** for user certificates issuance.</span></span>

- <span data-ttu-id="281bc-122">**Rama actual de System Center Configuration Manager**: debe instalar la versión 1606 o superior.</span><span class="sxs-lookup"><span data-stu-id="281bc-122">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span></span>  
<span data-ttu-id="281bc-123">Para más información, consulte:</span><span class="sxs-lookup"><span data-stu-id="281bc-123">For more information, see:</span></span> 
    - [<span data-ttu-id="281bc-124">Documentación de System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="281bc-124">Documentation for System Center Configuration Manager</span></span>](https://technet.microsoft.com/library/mt346023.aspx)
    - [<span data-ttu-id="281bc-125">Blog del equipo de System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="281bc-125">System Center Configuration Manager Team Blog</span></span>](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx)
    - [<span data-ttu-id="281bc-126">Configuración de Windows Hello para empresas en System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="281bc-126">Windows Hello for Business settings in System Center Configuration Manager</span></span>](https://docs.microsoft.com/sccm/protect/deploy-use/windows-hello-for-business-settings)

<span data-ttu-id="281bc-127">Como alternativa al requisito de implementación de PKI, puede hacer lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="281bc-127">As an alternative to the PKI deployment requirement, you can do the following:</span></span>

* <span data-ttu-id="281bc-128">Tener algunos controladores de dominio con los Servicios de dominio de Active Directory para Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="281bc-128">Have a few domain controllers with Windows Server 2016 Active Directory Domain Services.</span></span>

<span data-ttu-id="281bc-129">Para habilitar el acceso condicional, puede crear una configuración de directiva de grupo que permita el acceso a dispositivos unidos a un dominio sin ninguna implementación adicional.</span><span class="sxs-lookup"><span data-stu-id="281bc-129">To enable conditional access, you can create Group Policy settings that allow access to domain-joined devices with no additional deployments.</span></span> <span data-ttu-id="281bc-130">Para administrar el control de acceso basado en el cumplimiento del dispositivo, necesitará lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="281bc-130">To manage access control based on compliance of the device, you will need the following:</span></span>

* <span data-ttu-id="281bc-131">Rama actual de System Center Configuration Manager (1606 o posterior) para escenarios de Windows Hello para empresas</span><span class="sxs-lookup"><span data-stu-id="281bc-131">System Center Configuration Manager Current Branch (1606 or later) for Windows Hello for Business scenarios</span></span>

## <a name="deployment-instructions"></a><span data-ttu-id="281bc-132">Instrucciones de implementación</span><span class="sxs-lookup"><span data-stu-id="281bc-132">Deployment instructions</span></span>

<span data-ttu-id="281bc-133">Para implementar, siga los pasos de [Configuración del registro automático de dispositivos unidos a un dominio de Windows con Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md).</span><span class="sxs-lookup"><span data-stu-id="281bc-133">To deploy, follow the steps listed in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-conditional-access-automatic-device-registration-setup.md)</span></span>

## <a name="next-step"></a><span data-ttu-id="281bc-134">Paso siguiente</span><span class="sxs-lookup"><span data-stu-id="281bc-134">Next step</span></span>
* [<span data-ttu-id="281bc-135">Windows 10 para la empresa: formas de usar dispositivos para trabajar</span><span class="sxs-lookup"><span data-stu-id="281bc-135">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="281bc-136">Ampliación de las capacidades de nube a dispositivos de Windows 10 a través de Azure Active Directory Join</span><span class="sxs-lookup"><span data-stu-id="281bc-136">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="281bc-137">Conozca los escenarios de uso de Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="281bc-137">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="281bc-138">Experiencias de conexión de dispositivos unidos a un dominio a Azure AD para Windows 10</span><span class="sxs-lookup"><span data-stu-id="281bc-138">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="281bc-139">Configuración de Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="281bc-139">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

