---
title: aaaLearn sobre verificacion de MFA de Azure | Documentos de Microsoft
description: "¿Qué es la autenticación multifactor Azure, ¿por qué usar MFA, obtener más información sobre el cliente de la autenticación multifactor de Hola y Hola métodos y diferentes versiones disponibles. "
keywords: "Introducción tooMFA, información general de mfa, ¿qué es mfa"
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
ms.openlocfilehash: a91b8d6941d2b6ce72a789a97c57e10e594e7ada
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-multi-factor-authentication"></a><span data-ttu-id="ce3d9-104">¿Qué es Azure Multi-Factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="ce3d9-104">What is Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="ce3d9-105">Verificación en dos pasos es un método de autenticación que requiere más de un método de comprobación y agrega una segunda capa crítica de inicios de sesión de seguridad toouser y las transacciones.</span><span class="sxs-lookup"><span data-stu-id="ce3d9-105">Two-step verification is a method of authentication that requires more than one verification method and adds a critical second layer of security toouser sign-ins and transactions.</span></span> <span data-ttu-id="ce3d9-106">Funciona solicitando dos o más de hello siguiendo métodos de comprobación:</span><span class="sxs-lookup"><span data-stu-id="ce3d9-106">It works by requiring any two or more of hello following verification methods:</span></span>

* <span data-ttu-id="ce3d9-107">Un elemento que conoce (normalmente una contraseña).</span><span class="sxs-lookup"><span data-stu-id="ce3d9-107">Something you know (typically a password)</span></span>
* <span data-ttu-id="ce3d9-108">Un elemento del que dispone (un dispositivo de confianza que no se puede duplicar con facilidad, como un teléfono).</span><span class="sxs-lookup"><span data-stu-id="ce3d9-108">Something you have (a trusted device that is not easily duplicated, like a phone)</span></span>
* <span data-ttu-id="ce3d9-109">Un elemento físico que le identifica (biométrica).</span><span class="sxs-lookup"><span data-stu-id="ce3d9-109">Something you are (biometrics)</span></span>

<span data-ttu-id="ce3d9-110"><center>![Nombre de usuario y contraseña](./media/multi-factor-authentication/pword.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificados](./media/multi-factor-authentication/phone.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smartphone](./media/multi-factor-authentication/hware.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Tarjeta inteligente](./media/multi-factor-authentication/smart.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Tarjeta inteligente virtual](./media/multi-factor-authentication/vsmart.png)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Nombre de usuario y contraseña](./media/multi-factor-authentication/cert.png)</center></span><span class="sxs-lookup"><span data-stu-id="ce3d9-110"><center>![Username and Password](./media/multi-factor-authentication/pword.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Certificates](./media/multi-factor-authentication/phone.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Phone](./media/multi-factor-authentication/hware.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Smart Card](./media/multi-factor-authentication/smart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Virtual Smart Card](./media/multi-factor-authentication/vsmart.png) &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Username and Password](./media/multi-factor-authentication/cert.png)</center></span></span>

<span data-ttu-id="ce3d9-111">Azure Multi-Factor Authentication (MFA) es la solución de Microsoft de comprobación de dos pasos.</span><span class="sxs-lookup"><span data-stu-id="ce3d9-111">Azure Multi-Factor Authentication (MFA) is Microsoft's two-step verification solution.</span></span> <span data-ttu-id="ce3d9-112">Azure MFA ayuda a proteger acceso toodata y las aplicaciones al tiempo que satisface la demanda de los usuarios de un proceso de inicio de sesión simple.</span><span class="sxs-lookup"><span data-stu-id="ce3d9-112">Azure MFA helps safeguard access toodata and applications while meeting user demand for a simple sign-in process.</span></span> <span data-ttu-id="ce3d9-113">Ofrece una autenticación segura a través de una gran variedad de métodos de comprobación (como la comprobación mediante llamadas telefónicas, mensajes de texto o aplicaciones móviles).</span><span class="sxs-lookup"><span data-stu-id="ce3d9-113">It delivers strong authentication via a range of verification methods, including phone call, text message, or mobile app verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/WA-MFA-Overview/player]
>
>

## <a name="why-use-azure-multi-factor-authentication"></a><span data-ttu-id="ce3d9-114">¿Por qué usar Azure Multi-Factor Authentication?</span><span class="sxs-lookup"><span data-stu-id="ce3d9-114">Why use Azure Multi-Factor Authentication?</span></span>
<span data-ttu-id="ce3d9-115">Hoy en día, ahora más que nunca, las personas están cada vez más conectadas.</span><span class="sxs-lookup"><span data-stu-id="ce3d9-115">Today, more than ever, people are increasingly connected.</span></span> <span data-ttu-id="ce3d9-116">Con los smartphones, tabletas, equipos portátiles y equipos, personas tienen varias opciones diferentes acerca de cómo va a tooconnect y permanecer conectados en cualquier momento.</span><span class="sxs-lookup"><span data-stu-id="ce3d9-116">With smart phones, tablets, laptops, and PCs, people have several different options on how they are going tooconnect and stay connected at any time.</span></span> <span data-ttu-id="ce3d9-117">Pueden acceder a sus cuentas y las aplicaciones desde cualquier lugar, lo que significa que pueden ser más productivos y atender mejor a sus clientes.</span><span class="sxs-lookup"><span data-stu-id="ce3d9-117">People can access their accounts and applications from anywhere, which means that they can get more work done and serve their customers better.</span></span>

<span data-ttu-id="ce3d9-118">La autenticación multifactor Azure es una sencilla toouse, escalable, y solución confiable que proporciona un segundo método de autenticación para que los usuarios siempre están protegidos.</span><span class="sxs-lookup"><span data-stu-id="ce3d9-118">Azure Multi-Factor Authentication is an easy toouse, scalable, and reliable solution that provides a second method of authentication so your users are always protected.</span></span>

| ![TooUse fácil](./media/multi-factor-authentication/simple.png) | ![Escalable](./media/multi-factor-authentication/scalable.png) | ![Siempre protegido](./media/multi-factor-authentication/protected.png) | ![Confiable](./media/multi-factor-authentication/reliable.png) |
|:---:|:---:|:---:|:---:|
| <span data-ttu-id="ce3d9-123">**Toouse fácil**</span><span class="sxs-lookup"><span data-stu-id="ce3d9-123">**Easy toouse**</span></span> |<span data-ttu-id="ce3d9-124">**Escalable**</span><span class="sxs-lookup"><span data-stu-id="ce3d9-124">**Scalable**</span></span> |<span data-ttu-id="ce3d9-125">**Siempre protegido**</span><span class="sxs-lookup"><span data-stu-id="ce3d9-125">**Always Protected**</span></span> |<span data-ttu-id="ce3d9-126">**Confiable**</span><span class="sxs-lookup"><span data-stu-id="ce3d9-126">**Reliable**</span></span> |

* <span data-ttu-id="ce3d9-127">**Fácil tooUse** -Azure la autenticación multifactor está tooset simple seguridad y el uso.</span><span class="sxs-lookup"><span data-stu-id="ce3d9-127">**Easy tooUse** - Azure Multi-Factor Authentication is simple tooset up and use.</span></span> <span data-ttu-id="ce3d9-128">Hello obtener protección adicional que se incluye con la autenticación multifactor Azure permite a los usuarios toomanage sus propios dispositivos.</span><span class="sxs-lookup"><span data-stu-id="ce3d9-128">hello extra protection that comes with Azure Multi-Factor Authentication allows users toomanage their own devices.</span></span> <span data-ttu-id="ce3d9-129">Y lo mejor de todo es que en muchos casos se puede configurar con unos pocos clics.</span><span class="sxs-lookup"><span data-stu-id="ce3d9-129">Best of all, in many instances it can be set up with just a few simple clicks.</span></span>
* <span data-ttu-id="ce3d9-130">**Escalable** -la autenticación multifactor Azure usa la energía de Hola de nube de Hola y se integra con sus instalaciones de AD y aplicaciones personalizadas.</span><span class="sxs-lookup"><span data-stu-id="ce3d9-130">**Scalable** - Azure Multi-Factor Authentication uses hello power of hello cloud and integrates with your on-premises AD and custom apps.</span></span> <span data-ttu-id="ce3d9-131">Esta protección se ha ampliado incluso tooyour escenarios de gran volumen, una importancia decisiva.</span><span class="sxs-lookup"><span data-stu-id="ce3d9-131">This protection is even extended tooyour high-volume, mission-critical scenarios.</span></span>
* <span data-ttu-id="ce3d9-132">**Siempre protegido** -la autenticación multifactor Azure proporciona una autenticación segura con hello más altos estándares del sector.</span><span class="sxs-lookup"><span data-stu-id="ce3d9-132">**Always Protected** - Azure Multi-Factor Authentication provides strong authentication using hello highest industry standards.</span></span>
* <span data-ttu-id="ce3d9-133">**Confiable** : se garantiza la disponibilidad del 99,9% de Azure Multi-Factor Authenticaton.</span><span class="sxs-lookup"><span data-stu-id="ce3d9-133">**Reliable** - We guarantee 99.9% availability of Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="ce3d9-134">Hello servicio se considera no disponible cuando no puede tooreceive o proceso de solicitudes de comprobación para la comprobación de dos pasos de Hola.</span><span class="sxs-lookup"><span data-stu-id="ce3d9-134">hello service is considered unavailable when it is unable tooreceive or process verification requests for hello two-step verification.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Windows-Azure-Multi-Factor-Authentication/player]


## <a name="next-steps"></a><span data-ttu-id="ce3d9-135">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="ce3d9-135">Next steps</span></span>

- <span data-ttu-id="ce3d9-136">Lea [Cómo funciona Azure Multi-Factor Authentication](multi-factor-authentication-how-it-works.md).</span><span class="sxs-lookup"><span data-stu-id="ce3d9-136">Learn about [how Azure Multi-Factor Authentication works](multi-factor-authentication-how-it-works.md)</span></span>

- <span data-ttu-id="ce3d9-137">Hola diferentes que conozca [versiones y los métodos de consumo para la autenticación multifactor de Azure](multi-factor-authentication-versions-plans.md)</span><span class="sxs-lookup"><span data-stu-id="ce3d9-137">Read about hello different [versions and consumption methods for Azure Multi-Factor Authentication](multi-factor-authentication-versions-plans.md)</span></span>
