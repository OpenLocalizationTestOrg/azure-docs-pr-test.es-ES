---
title: "Consideraciones sobre el diseño de identidad híbrida de Azure Active Directory: determinación de los requisitos de administración de contenido| Microsoft Docs"
description: "Se proporciona información detallada sobre cómo determinar los requisitos de administración de contenido de su empresa. Normalmente, cuando un usuario tiene su propio dispositivo lo habitual es que tenga más varias credenciales que se irán alternando según la aplicación que use. Es importante distinguir qué contenido se creó con las credenciales personales frente al que se creó con las credenciales corporativas. La solución de identidad debe ser capaz de interactuar con los servicios en la nube a fin de proporcionar al usuario final una experiencia sin fisuras, y al mismo tiempo asegurar su privacidad y aumentar la protección frente a la pérdida de datos."
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: dd1ef776-db4d-4ab8-9761-2adaa5a4f004
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 840de1e1fcba74285788d51d8f544375f0affa77
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/03/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="a1d6d-106">Determinación de los requisitos de administración de contenido para la solución de identidad híbrida</span><span class="sxs-lookup"><span data-stu-id="a1d6d-106">Determine content management requirements for your hybrid identity solution</span></span>
<span data-ttu-id="a1d6d-107">Comprender los requisitos de administración de contenido de su empresa puede afectar directamente a su decisión sobre la solución de identidad híbrida que es mejor usar.</span><span class="sxs-lookup"><span data-stu-id="a1d6d-107">Understanding the content management requirements for your business may direct affect your decision on which hybrid identity solution to use.</span></span> <span data-ttu-id="a1d6d-108">Con la proliferación de tantos dispositivos y la posibilidad de que los usuarios traigan los suyos propios ([BYOD](http://aka.ms/byodcg)), la empresa debe proteger sus propios datos, pero también mantener intacta la privacidad del usuario.</span><span class="sxs-lookup"><span data-stu-id="a1d6d-108">With the proliferation of multiple devices and the capability of users to bring their own devices ([BYOD](http://aka.ms/byodcg)), the company must protect its own data but it also must keep user’s privacy intact.</span></span> <span data-ttu-id="a1d6d-109">Normalmente, cuando un usuario tiene su propio dispositivo lo habitual es que tenga más varias credenciales que se irán alternando según la aplicación que use.</span><span class="sxs-lookup"><span data-stu-id="a1d6d-109">Usually when a user has his own device he might have also multiple credentials that will be alternating according to the application that he uses.</span></span> <span data-ttu-id="a1d6d-110">Es importante distinguir qué contenido se creó con las credenciales personales frente al que se creó con las credenciales corporativas.</span><span class="sxs-lookup"><span data-stu-id="a1d6d-110">It is important to differentiate what content was created using personal credentials versus the ones created using corporate credentials.</span></span> <span data-ttu-id="a1d6d-111">La solución de identidad debe ser capaz de interactuar con los servicios en la nube a fin de proporcionar al usuario final una experiencia sin fisuras, y al mismo tiempo asegurar su privacidad y aumentar la protección frente a la pérdida de datos.</span><span class="sxs-lookup"><span data-stu-id="a1d6d-111">Your identity solution should be able to interact with cloud services to provide a seamless experience to the end user while ensure his privacy and increase the protection against data leakage.</span></span> 

<span data-ttu-id="a1d6d-112">Diferentes controles técnicos aprovecharán la solución de identidad para proporcionar administración de contenido, como se muestra en la siguiente ilustración:</span><span class="sxs-lookup"><span data-stu-id="a1d6d-112">Your identity solution will be leveraged by different technical controls in order to provide content management as shown in the figure below:</span></span>

![](./media/hybrid-id-design-considerations/securitycontrols.png)

<span data-ttu-id="a1d6d-113">**Controles de seguridad que aprovecharán su sistema de administración de identidad**</span><span class="sxs-lookup"><span data-stu-id="a1d6d-113">**Security controls that will be leveraging your identity management system**</span></span>

<span data-ttu-id="a1d6d-114">En general, los requisitos de administración de contenido aprovecharán su sistema de administración de identidad en las áreas siguientes:</span><span class="sxs-lookup"><span data-stu-id="a1d6d-114">In general, content management requirements will leverage your identity management system in the following areas:</span></span>

* <span data-ttu-id="a1d6d-115">Privacidad: identificarán al usuario propietario de un recurso y aplicarán los controles adecuados para mantener la integridad.</span><span class="sxs-lookup"><span data-stu-id="a1d6d-115">Privacy: identifying the user that owns a resource and applying the appropriate controls to maintain integrity.</span></span>
* <span data-ttu-id="a1d6d-116">Clasificación de datos: identificarán al usuario o grupo y el nivel de acceso a un objeto en función de su clasificación.</span><span class="sxs-lookup"><span data-stu-id="a1d6d-116">Data Classification: identify the user or group and level of access to an object according to its classification.</span></span> 
* <span data-ttu-id="a1d6d-117">Protección contra pérdida de datos: los controles de seguridad responsables de la protección de los datos deberán interactuar con el sistema de identidad para validar la identidad del usuario a fin de evitar la pérdida de estos datos.</span><span class="sxs-lookup"><span data-stu-id="a1d6d-117">Data Leakage Protection: security controls responsible for protecting data to avoid leakage will need to interact with the identity system to validate the user’s identity.</span></span> <span data-ttu-id="a1d6d-118">Esto también es importante para los fines de seguimiento de auditoría.</span><span class="sxs-lookup"><span data-stu-id="a1d6d-118">This is also important for auditing trail purpose.</span></span>

> [!NOTE]
> <span data-ttu-id="a1d6d-119">Lea [Clasificación de los datos para prepararlos para la nube](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) para obtener más información sobre los procedimientos recomendados e instrucciones para la clasificación de los datos.</span><span class="sxs-lookup"><span data-stu-id="a1d6d-119">Read [data classification for cloud readiness](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) for more information about best practices and guidelines for data classification.</span></span>
> 
> 

<span data-ttu-id="a1d6d-120">Al planear la solución de identidad híbrida, asegúrese de que puede responder a las siguientes preguntas según los requisitos de su organización:</span><span class="sxs-lookup"><span data-stu-id="a1d6d-120">When planning your hybrid identity solution ensure that the following questions are answered according to your organization’s requirements:</span></span>

* <span data-ttu-id="a1d6d-121">¿Tiene su empresa controles de seguridad para aplicar la privacidad de los datos?</span><span class="sxs-lookup"><span data-stu-id="a1d6d-121">Does your company have security controls in place to enforce data privacy?</span></span>
  * <span data-ttu-id="a1d6d-122">En caso afirmativo, ¿podrán integrarse esos controles de seguridad con la solución de identidad híbrida que va a adoptar?</span><span class="sxs-lookup"><span data-stu-id="a1d6d-122">If yes, will those security controls be able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="a1d6d-123">¿Usa su empresa clasificación de los datos?</span><span class="sxs-lookup"><span data-stu-id="a1d6d-123">Does your company use data classification?</span></span>
  * <span data-ttu-id="a1d6d-124">En caso afirmativo, ¿se puede integrar la solución actual con la solución de identidad híbrida que va a adoptar?</span><span class="sxs-lookup"><span data-stu-id="a1d6d-124">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="a1d6d-125">¿Tiene su empresa actualmente una solución para hacer frente a la pérdida de datos?</span><span class="sxs-lookup"><span data-stu-id="a1d6d-125">Does your company currently have any solution for data leakage?</span></span> 
  * <span data-ttu-id="a1d6d-126">En caso afirmativo, ¿se puede integrar la solución actual con la solución de identidad híbrida que va a adoptar?</span><span class="sxs-lookup"><span data-stu-id="a1d6d-126">If yes, is the current solution able to integrate with the hybrid identity solution that you are going to adopt?</span></span>
* <span data-ttu-id="a1d6d-127">¿Necesita su empresa auditar el acceso a los recursos?</span><span class="sxs-lookup"><span data-stu-id="a1d6d-127">Does your company need to audit access to resources?</span></span>
  * <span data-ttu-id="a1d6d-128">En caso afirmativo, ¿para qué tipo de recursos?</span><span class="sxs-lookup"><span data-stu-id="a1d6d-128">If yes, what type of resources?</span></span>
  * <span data-ttu-id="a1d6d-129">En caso afirmativo, ¿qué nivel de información es necesario?</span><span class="sxs-lookup"><span data-stu-id="a1d6d-129">If yes, what level of information is necessary?</span></span>
  * <span data-ttu-id="a1d6d-130">En caso afirmativo, ¿dónde debe residir el registro de auditoría?</span><span class="sxs-lookup"><span data-stu-id="a1d6d-130">If yes, where the audit log must reside?</span></span> <span data-ttu-id="a1d6d-131">¿En el entorno local o en la nube?</span><span class="sxs-lookup"><span data-stu-id="a1d6d-131">On-premises or in the cloud?</span></span>
* <span data-ttu-id="a1d6d-132">¿Necesita su empresa cifrar los mensajes de correo electrónico que contienen datos confidenciales (números de seguridad social, números de tarjeta de crédito, etc.)?</span><span class="sxs-lookup"><span data-stu-id="a1d6d-132">Does your company need to encrypt any emails that contain sensitive data (SSNs, credit card numbers, etc)?</span></span>
* <span data-ttu-id="a1d6d-133">¿Necesita su empresa cifrar todos los documentos o contenidos compartidos con socios comerciales externos?</span><span class="sxs-lookup"><span data-stu-id="a1d6d-133">Does your company need to encrypt all documents/contents shared with external business partners?</span></span>
* <span data-ttu-id="a1d6d-134">¿Necesita su empresa aplicar directivas corporativas en determinadas clases de correos electrónicos (no responder a todos, no reenvíar)?</span><span class="sxs-lookup"><span data-stu-id="a1d6d-134">Does your company need to enforce corporate policies on certain kinds of emails (do no reply all, do not forward)?</span></span>

> [!NOTE]
> <span data-ttu-id="a1d6d-135">Asegúrese de anotar cada respuesta y de que comprende las razones que se esconden detrás.</span><span class="sxs-lookup"><span data-stu-id="a1d6d-135">Make sure to take notes of each answer and understand the rationale behind the answer.</span></span> <span data-ttu-id="a1d6d-136">[Definición de la estrategia de protección de datos](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) se recorren las opciones disponibles y las ventajas y desventajas de cada una.</span><span class="sxs-lookup"><span data-stu-id="a1d6d-136">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over the options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="a1d6d-137">Las respuestas que obtenga partir de estas preguntas le servirán para seleccionar la opción que mejor se adapte a sus necesidades empresariales.</span><span class="sxs-lookup"><span data-stu-id="a1d6d-137">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a1d6d-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a1d6d-138">Next steps</span></span>
[<span data-ttu-id="a1d6d-139">Determinación de los requisitos de control de acceso</span><span class="sxs-lookup"><span data-stu-id="a1d6d-139">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a><span data-ttu-id="a1d6d-140">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="a1d6d-140">See Also</span></span>
[<span data-ttu-id="a1d6d-141">Información general sobre las consideraciones de diseño</span><span class="sxs-lookup"><span data-stu-id="a1d6d-141">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

