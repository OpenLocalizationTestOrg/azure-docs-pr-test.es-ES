---
title: "Información acerca de la verificación en dos pasos de Azure MFA | Microsoft Docs"
description: "En este tema se explica qué es Azure Multi-factor Authentication, por qué usar MFA, aporta más información sobre el cliente de Multi-Factor Authentication y los distintos métodos y versiones disponibles. "
keywords: "introducción a MFA, introducción general a mfa, qué es mfa"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: c40d7a34-1274-4496-96b0-784850c06e9b
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/03/2017
ms.author: kgremban
ms.openlocfilehash: 7334ab5b278c3339fdbc2e363fd5c609604d3e14
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a><span data-ttu-id="28abd-104">¿Qué es Azure Multi-Factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="28abd-104">What is Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="28abd-105">La verificación en dos pasos es un método de autenticación que requiere más de un método de comprobación y agrega un segundo nivel importante de seguridad crítico a las transacciones e inicios de sesión del usuario.</span><span class="sxs-lookup"><span data-stu-id="28abd-105">Two-step verification is a method of authentication that requires more than one verification method and adds a critical second layer of security to user sign-ins and transactions.</span></span> <span data-ttu-id="28abd-106">Funciona mediante la solicitud de dos o más de los siguientes métodos de verificación:</span><span class="sxs-lookup"><span data-stu-id="28abd-106">It works by requiring any two or more of the following verification methods:</span></span>

* <span data-ttu-id="28abd-107">Un elemento que conoce (normalmente una contraseña).</span><span class="sxs-lookup"><span data-stu-id="28abd-107">Something you know (typically a password)</span></span>
* <span data-ttu-id="28abd-108">Un elemento del que dispone (un dispositivo de confianza que no se puede duplicar con facilidad, como un teléfono).</span><span class="sxs-lookup"><span data-stu-id="28abd-108">Something you have (a trusted device that is not easily duplicated, like a phone)</span></span>
* <span data-ttu-id="28abd-109">Un elemento físico que le identifica (biométrica).</span><span class="sxs-lookup"><span data-stu-id="28abd-109">Something you are (biometrics)</span></span>

<span data-ttu-id="28abd-110"><center>![Nombre de usuario y contraseña](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificados](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smartphone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Tarjeta inteligente](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Tarjeta inteligente virtual](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Nombre de usuario y contraseña](./media/multi-factor-authentication/cert.png)</center></span><span class="sxs-lookup"><span data-stu-id="28abd-110"><center>![Username and Password](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificates](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Phone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Card](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Virtual Smart Card](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Username and Password](./media/multi-factor-authentication/cert.png)</center></span></span>

<span data-ttu-id="28abd-111">Azure Multi-Factor Authentication (MFA) es la solución de Microsoft de comprobación de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="28abd-111">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span></span> <span data-ttu-id="28abd-112">Azure MFA ayuda a proteger el acceso a los datos y las aplicaciones, al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple.</span><span class="sxs-lookup"><span data-stu-id="28abd-112">Azure MFA helps safeguard access to data and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="28abd-113">Ofrece una autenticación segura a través de una gran variedad de métodos de comprobación (como la comprobación mediante llamadas telefónicas, mensajes de texto o aplicaciones móviles).</span><span class="sxs-lookup"><span data-stu-id="28abd-113">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a><span data-ttu-id="28abd-114">¿Por qué usar Azure Multi-Factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="28abd-114">Why use Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="28abd-115">Hoy en día, ahora más que nunca, las personas están cada vez más conectadas.</span><span class="sxs-lookup"><span data-stu-id="28abd-115">Today, more than ever, people are increasingly connected.</span></span> <span data-ttu-id="28abd-116">Con los smartphones, tabletas, equipos portátiles y equipos de sobremesa, las personas tienen varias opciones para conectarse y permanecer conectados en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="28abd-116">With smart phones, tablets, laptops, and PCs, people have several different options on how they are going to connect and stay connected at any time.</span></span> <span data-ttu-id="28abd-117">Pueden acceder a sus cuentas y las aplicaciones desde cualquier lugar, lo que significa que pueden ser más productivos y atender mejor a sus clientes.</span><span class="sxs-lookup"><span data-stu-id="28abd-117">People can access their accounts and applications from anywhere, which means that they can get more work done and serve their customers better.</span></span>

<span data-ttu-id="28abd-118">Azure Multi-Factor Authentication es una solución fácil de usar, escalable y confiable que proporciona un segundo método de autenticación para que los usuarios siempre estén protegidos.</span><span class="sxs-lookup"><span data-stu-id="28abd-118">Azure Multi-Factor Authentication is an easy to use, scalable, and reliable solution that provides a second method of authentication so your users are always protected.</span></span>

| ![Fácil de usar](./media/multi-factor-authentication/simple.png) | ![Escalable](./media/multi-factor-authentication/scalable.png) | ![Siempre protegido](./media/multi-factor-authentication/protected.png) | ![Confiable](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| <span data-ttu-id="28abd-123">**Fácil de usar**</span><span class="sxs-lookup"><span data-stu-id="28abd-123">**Easy to use**</span></span> |<span data-ttu-id="28abd-124">**Escalable**</span><span class="sxs-lookup"><span data-stu-id="28abd-124">**Scalable**</span></span> |<span data-ttu-id="28abd-125">**Siempre protegido**</span><span class="sxs-lookup"><span data-stu-id="28abd-125">**Always Protected**</span></span> |<span data-ttu-id="28abd-126">**Confiable**</span><span class="sxs-lookup"><span data-stu-id="28abd-126">**Reliable**</span></span> |

* <span data-ttu-id="28abd-127">**Fácil de usar** : Azure Multi-Factor Authenticaton es fácil de configurar y utilizar.</span><span class="sxs-lookup"><span data-stu-id="28abd-127">**Easy to Use** - Azure Multi-Factor Authentication is simple to set up and use.</span></span> <span data-ttu-id="28abd-128">La protección adicional que se incluye con Azure Multi-Factor Authentication permite a los usuarios administrar sus propios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="28abd-128">The extra protection that comes with Azure Multi-Factor Authentication allows users to manage their own devices.</span></span> <span data-ttu-id="28abd-129">Y lo mejor de todo es que en muchos casos se puede configurar con unos pocos clics.</span><span class="sxs-lookup"><span data-stu-id="28abd-129">Best of all, in many instances it can be set up with just a few simple clicks.</span></span>
* <span data-ttu-id="28abd-130">**Escalable** : Azure Multi-Factor Authenticaton utiliza la potencia de la nube y se integra con la instancia local de Active Directory y aplicaciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="28abd-130">**Scalable** - Azure Multi-Factor Authentication uses the power of the cloud and integrates with your on-premises AD and custom apps.</span></span> <span data-ttu-id="28abd-131">Esta protección se extiende incluso a los escenarios críticos de gran volumen.</span><span class="sxs-lookup"><span data-stu-id="28abd-131">This protection is even extended to your high-volume, mission-critical scenarios.</span></span>
* <span data-ttu-id="28abd-132">**Siempre protegido** Azure Multi-Factor Authenticaton ofrece autenticación segura mediante los más elevados estándares del sector.</span><span class="sxs-lookup"><span data-stu-id="28abd-132">**Always Protected** - Azure Multi-Factor Authentication provides strong authentication using the highest industry standards.</span></span>
* <span data-ttu-id="28abd-133">**Confiable** : se garantiza la disponibilidad del 99,9% de Azure Multi-Factor Authenticaton.</span><span class="sxs-lookup"><span data-stu-id="28abd-133">**Reliable** - We guarantee 99.9% availability of Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="28abd-134">Se considera que el servicio no está disponible cuando no puede recibir ni procesar las solicitudes de comprobación para la comprobación en dos pasos.</span><span class="sxs-lookup"><span data-stu-id="28abd-134">The service is considered unavailable when it is unable to receive or process verification requests for the two-step verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a><span data-ttu-id="28abd-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="28abd-135">Next steps</span></span>

- <span data-ttu-id="28abd-136">Lea [Cómo funciona Azure Multi-Factor Authentication](multi-factor-authentication-how-it-works.md).</span><span class="sxs-lookup"><span data-stu-id="28abd-136">Learn about [how Azure Multi-Factor Authentication works](multi-factor-authentication-how-it-works.md)</span></span>

- <span data-ttu-id="28abd-137">Obtenga información sobre las diferentes [versiones y métodos de utilización de Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md).</span><span class="sxs-lookup"><span data-stu-id="28abd-137">Read about the different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>
