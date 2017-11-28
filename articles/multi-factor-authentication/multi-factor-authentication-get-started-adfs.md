---
title: "comprobación de paso aaaTwo y AD FS - MFA de Azure | Documentos de Microsoft"
description: "Se trata de una página de autenticación multifactor de Azure de Hola que describe cómo se inicia tooget con MFA de Azure y AD FS."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 44fbba68-6cf9-46c1-a9df-736580b68ae3
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/23/2017
ms.author: kgremban
ms.openlocfilehash: 7c1c925039d3cb753ba60e286168e5869faeae4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-multi-factor-authentication-and-active-directory-federation-services"></a><span data-ttu-id="04bd7-103">Introducción a Azure Multi-Factor Authentication y a los Servicios de federación de Active Directory</span><span class="sxs-lookup"><span data-stu-id="04bd7-103">Getting started with Azure Multi-Factor Authentication and Active Directory Federation Services</span></span>
<span data-ttu-id="04bd7-104"><center>![Nube](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span><span class="sxs-lookup"><span data-stu-id="04bd7-104"><center>![Cloud](./media/multi-factor-authentication-get-started-adfs/adfs.png)</center></span></span>

<span data-ttu-id="04bd7-105">Si su organización ha federado su Active Directory local con Azure Active Directory mediante AD FS, tiene a su disposición dos opciones para usar Azure Multi-Factor Authentication.</span><span class="sxs-lookup"><span data-stu-id="04bd7-105">If your organization has federated your on-premises Active Directory with Azure Active Directory using AD FS, there are two options for using Azure Multi-Factor Authentication.</span></span>

* <span data-ttu-id="04bd7-106">Recursos de nube seguros a través del uso de Azure Multi-Factor Authentication o los Servicios de federación de Active Directory</span><span class="sxs-lookup"><span data-stu-id="04bd7-106">Secure cloud resources using Azure Multi-Factor Authentication or Active Directory Federation Services</span></span>
* <span data-ttu-id="04bd7-107">Protección de recursos en la nube y locales mediante Servidor Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="04bd7-107">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server</span></span>

<span data-ttu-id="04bd7-108">Hello en la tabla siguiente resume la experiencia de comprobación de hello entre la protección de recursos con la autenticación multifactor Azure y AD FS</span><span class="sxs-lookup"><span data-stu-id="04bd7-108">hello following table summarizes hello verification experience between securing resources with Azure Multi-Factor Authentication and AD FS</span></span>

| <span data-ttu-id="04bd7-109">Experiencia de verificación: aplicaciones basadas en explorador</span><span class="sxs-lookup"><span data-stu-id="04bd7-109">Verification Experience - Browser-based Apps</span></span> | <span data-ttu-id="04bd7-110">Experiencia de verificación: aplicaciones no basadas en explorador</span><span class="sxs-lookup"><span data-stu-id="04bd7-110">Verification Experience - Non-Browser-based Apps</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="04bd7-111">Protección de recursos de Azure AD con Azure Multi-Factor Authentication</span><span class="sxs-lookup"><span data-stu-id="04bd7-111">Securing Azure AD resources using Azure Multi-Factor Authentication</span></span> |<li><span data-ttu-id="04bd7-112">primer paso de verificación Hola se realiza localmente utilizando AD FS.</span><span class="sxs-lookup"><span data-stu-id="04bd7-112">hello first verification step is performed on-premises using AD FS.</span></span></li> <li><span data-ttu-id="04bd7-113">Hola segundo paso es un método basado en teléfono que se llevan a cabo mediante la autenticación de nube.</span><span class="sxs-lookup"><span data-stu-id="04bd7-113">hello second step is a phone-based method carried out using cloud authentication.</span></span></li> |
| <span data-ttu-id="04bd7-114">Protección de los recursos de Azure AD mediante los servicios de federación de Active Directory</span><span class="sxs-lookup"><span data-stu-id="04bd7-114">Securing Azure AD resources using Active Directory Federation Services</span></span> |<li><span data-ttu-id="04bd7-115">primer paso de verificación Hola se realiza localmente utilizando AD FS.</span><span class="sxs-lookup"><span data-stu-id="04bd7-115">hello first verification step is performed on-premises using AD FS.</span></span></li><li><span data-ttu-id="04bd7-116">Hola segundo paso es realiza localmente respondiendo a una notificación de Hola.</span><span class="sxs-lookup"><span data-stu-id="04bd7-116">hello second step is performed on-premises by honoring hello claim.</span></span></li> |

<span data-ttu-id="04bd7-117">Advertencias sobre las contraseñas de aplicación para usuarios federados:</span><span class="sxs-lookup"><span data-stu-id="04bd7-117">Caveats with app passwords for federated users:</span></span>

* <span data-ttu-id="04bd7-118">Las contraseña de aplicación se comprueban mediante autenticación en la nube y, por lo tanto, omiten las federaciones.</span><span class="sxs-lookup"><span data-stu-id="04bd7-118">App passwords are verified using cloud authentication, so they bypass federation.</span></span> <span data-ttu-id="04bd7-119">La federación solo se usa activamente al configurar una contraseña de aplicación.</span><span class="sxs-lookup"><span data-stu-id="04bd7-119">Federation is only actively used when setting up an app password.</span></span>
* <span data-ttu-id="04bd7-120">La configuración del control de acceso de cliente local no se cumple con las contraseñas de aplicación.</span><span class="sxs-lookup"><span data-stu-id="04bd7-120">On-premises Client Access Control settings are not honored by app passwords.</span></span>
* <span data-ttu-id="04bd7-121">Se pierde la capacidad de registro de autenticación local para las contraseñas de aplicación.</span><span class="sxs-lookup"><span data-stu-id="04bd7-121">You lose on-premises authentication-logging capability for app passwords.</span></span>
* <span data-ttu-id="04bd7-122">La deshabilitación o eliminación de cuenta puede tardar horas toothree para sincronización de directorios, lo que se retrasa la deshabilitación o eliminación de contraseñas de aplicación en la identidad de nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="04bd7-122">Account disable/deletion may take up toothree hours for directory sync, delaying disable/deletion of app passwords in hello cloud identity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="04bd7-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="04bd7-123">Next steps</span></span>
<span data-ttu-id="04bd7-124">Para obtener información sobre cómo configurar la autenticación multifactor Azure u Hola servidor Azure Multi-factor Authentication con AD FS, vea Hola siguientes artículos:</span><span class="sxs-lookup"><span data-stu-id="04bd7-124">For information on setting up either Azure Multi-Factor Authentication or hello Azure Multi-Factor Authentication Server with AD FS, see hello following articles:</span></span>

* [<span data-ttu-id="04bd7-125">Protección de recursos en la nube con Azure Multi-Factor Authentication y AD FS</span><span class="sxs-lookup"><span data-stu-id="04bd7-125">Secure cloud resources using Azure Multi-Factor Authentication and AD FS</span></span>](multi-factor-authentication-get-started-adfs-cloud.md)
* [<span data-ttu-id="04bd7-126">Protección de recursos en la nube y locales mediante Servidor Azure Multi-Factor Authentication con Windows Server 2012 R2 AD FS</span><span class="sxs-lookup"><span data-stu-id="04bd7-126">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with Windows Server 2012 R2 AD FS</span></span>](multi-factor-authentication-get-started-adfs-w2k12.md)
* [<span data-ttu-id="04bd7-127">Protección de recursos en la nube y locales mediante Servidor Azure Multi-Factor Authentication con AD FS 2.0</span><span class="sxs-lookup"><span data-stu-id="04bd7-127">Secure cloud and on-premises resources using Azure Multi-Factor Authentication Server with AD FS 2.0</span></span>](multi-factor-authentication-get-started-adfs-adfs2.md)
