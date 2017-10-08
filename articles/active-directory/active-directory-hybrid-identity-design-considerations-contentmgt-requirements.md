---
title: "Consideraciones de diseño de identidad de aaaAzure Active Directory híbrida - determinar los requisitos de administración de contenido | Documentos de Microsoft"
description: "Proporciona una visión general de cómo toodetermine Hola requerimientos de administración de contenido de su negocio. Normalmente cuando un usuario tiene su propio dispositivo puede tener también varias credenciales que se pueden alternar aplicación toohello correspondiente que se utiliza. Es importante toodifferentiate el contenido que se creó mediante credenciales personales frente a hello las siguieron credenciales corporativas. La solución de identidad debe ser capaz de toointeract con tooprovide de servicios de nube un experiencia perfecta toohello final de usuario mientras se garantiza su privacidad y aumentar la protección de hello contra la pérdida de datos."
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
ms.openlocfilehash: 607d366633c37b65ec5cf8ae5c64d73ca1cc96b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="determine-content-management-requirements-for-your-hybrid-identity-solution"></a><span data-ttu-id="a8d91-106">Determinación de los requisitos de administración de contenido para la solución de identidad híbrida</span><span class="sxs-lookup"><span data-stu-id="a8d91-106">Determine content management requirements for your hybrid identity solution</span></span>
<span data-ttu-id="a8d91-107">Descripción Hola administración de contenido de los requisitos de su empresa puedan dirigir afectan a la decisión sobre qué toouse de solución de identidad híbrida.</span><span class="sxs-lookup"><span data-stu-id="a8d91-107">Understanding hello content management requirements for your business may direct affect your decision on which hybrid identity solution toouse.</span></span> <span data-ttu-id="a8d91-108">Con Hola proliferación de varios dispositivos y la capacidad de Hola de usuarios toobring sus propios dispositivos ([BYOD](http://aka.ms/byodcg)), empresa Hola debe proteger sus propios datos sin embargo también debe tener privacidad del usuario intacta.</span><span class="sxs-lookup"><span data-stu-id="a8d91-108">With hello proliferation of multiple devices and hello capability of users toobring their own devices ([BYOD](http://aka.ms/byodcg)), hello company must protect its own data but it also must keep user’s privacy intact.</span></span> <span data-ttu-id="a8d91-109">Normalmente cuando un usuario tiene su propio dispositivo puede tener también varias credenciales que se pueden alternar aplicación toohello correspondiente que se utiliza.</span><span class="sxs-lookup"><span data-stu-id="a8d91-109">Usually when a user has his own device he might have also multiple credentials that will be alternating according toohello application that he uses.</span></span> <span data-ttu-id="a8d91-110">Es importante toodifferentiate el contenido que se creó mediante credenciales personales frente a hello las siguieron credenciales corporativas.</span><span class="sxs-lookup"><span data-stu-id="a8d91-110">It is important toodifferentiate what content was created using personal credentials versus hello ones created using corporate credentials.</span></span> <span data-ttu-id="a8d91-111">La solución de identidad debe ser capaz de toointeract con tooprovide de servicios de nube un experiencia perfecta toohello final de usuario mientras se garantiza su privacidad y aumentar la protección de hello contra la pérdida de datos.</span><span class="sxs-lookup"><span data-stu-id="a8d91-111">Your identity solution should be able toointeract with cloud services tooprovide a seamless experience toohello end user while ensure his privacy and increase hello protection against data leakage.</span></span> 

<span data-ttu-id="a8d91-112">La solución de identidad se aprovecharán por los diferentes controles técnicos en administración de contenido de orden tooprovide tal y como se muestra en la siguiente ilustración de hello:</span><span class="sxs-lookup"><span data-stu-id="a8d91-112">Your identity solution will be leveraged by different technical controls in order tooprovide content management as shown in hello figure below:</span></span>

![](./media/hybrid-id-design-considerations/securitycontrols.png)

<span data-ttu-id="a8d91-113">**Controles de seguridad que aprovecharán su sistema de administración de identidad**</span><span class="sxs-lookup"><span data-stu-id="a8d91-113">**Security controls that will be leveraging your identity management system**</span></span>

<span data-ttu-id="a8d91-114">En general, los requisitos de administración de contenido aprovecharán su sistema de administración de identidades en hello siguientes áreas:</span><span class="sxs-lookup"><span data-stu-id="a8d91-114">In general, content management requirements will leverage your identity management system in hello following areas:</span></span>

* <span data-ttu-id="a8d91-115">Privacidad: identificación de usuario de Hola que posee un recurso y aplicar la integridad de toomaintain de hello controles adecuados.</span><span class="sxs-lookup"><span data-stu-id="a8d91-115">Privacy: identifying hello user that owns a resource and applying hello appropriate controls toomaintain integrity.</span></span>
* <span data-ttu-id="a8d91-116">Clasificación de datos: identificar usuario Hola o de grupo y de nivel de objeto de tooan de acceso según la clasificación de tooits.</span><span class="sxs-lookup"><span data-stu-id="a8d91-116">Data Classification: identify hello user or group and level of access tooan object according tooits classification.</span></span> 
* <span data-ttu-id="a8d91-117">Protección contra la pérdida de datos: controles de seguridad responsables de proteger la pérdida de datos tooavoid deberá toointeract con la identidad del usuario de hello identidad sistema toovalidate Hola.</span><span class="sxs-lookup"><span data-stu-id="a8d91-117">Data Leakage Protection: security controls responsible for protecting data tooavoid leakage will need toointeract with hello identity system toovalidate hello user’s identity.</span></span> <span data-ttu-id="a8d91-118">Esto también es importante para los fines de seguimiento de auditoría.</span><span class="sxs-lookup"><span data-stu-id="a8d91-118">This is also important for auditing trail purpose.</span></span>

> [!NOTE]
> <span data-ttu-id="a8d91-119">Lea [Clasificación de los datos para prepararlos para la nube](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) para obtener más información sobre los procedimientos recomendados e instrucciones para la clasificación de los datos.</span><span class="sxs-lookup"><span data-stu-id="a8d91-119">Read [data classification for cloud readiness](http://download.microsoft.com/download/0/A/3/0A3BE969-85C5-4DD2-83B6-366AA71D1FE3/Data-Classification-for-Cloud-Readiness.pdf) for more information about best practices and guidelines for data classification.</span></span>
> 
> 

<span data-ttu-id="a8d91-120">Cuando planifique la solución de identidad híbrida asegurarse de esa Hola después se responden preguntas según los requisitos de la organización tooyour:</span><span class="sxs-lookup"><span data-stu-id="a8d91-120">When planning your hybrid identity solution ensure that hello following questions are answered according tooyour organization’s requirements:</span></span>

* <span data-ttu-id="a8d91-121">¿La compañía tiene controles de seguridad en lugar tooenforce privacidad de los datos?</span><span class="sxs-lookup"><span data-stu-id="a8d91-121">Does your company have security controls in place tooenforce data privacy?</span></span>
  * <span data-ttu-id="a8d91-122">¿Si es así, los controles de seguridad será capaz de toointegrate con la solución de identidad híbrida de Hola que son tooadopt continua?</span><span class="sxs-lookup"><span data-stu-id="a8d91-122">If yes, will those security controls be able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="a8d91-123">¿Usa su empresa clasificación de los datos?</span><span class="sxs-lookup"><span data-stu-id="a8d91-123">Does your company use data classification?</span></span>
  * <span data-ttu-id="a8d91-124">¿Si es así, es toointegrate capaz de hello actual de solución con la solución de identidad híbrida de Hola que son tooadopt continuo?</span><span class="sxs-lookup"><span data-stu-id="a8d91-124">If yes, is hello current solution able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="a8d91-125">¿Tiene su empresa actualmente una solución para hacer frente a la pérdida de datos?</span><span class="sxs-lookup"><span data-stu-id="a8d91-125">Does your company currently have any solution for data leakage?</span></span> 
  * <span data-ttu-id="a8d91-126">¿Si es así, es toointegrate capaz de hello actual de solución con la solución de identidad híbrida de Hola que son tooadopt continuo?</span><span class="sxs-lookup"><span data-stu-id="a8d91-126">If yes, is hello current solution able toointegrate with hello hybrid identity solution that you are going tooadopt?</span></span>
* <span data-ttu-id="a8d91-127">¿La compañía necesita tooaudit acceso tooresources?</span><span class="sxs-lookup"><span data-stu-id="a8d91-127">Does your company need tooaudit access tooresources?</span></span>
  * <span data-ttu-id="a8d91-128">En caso afirmativo, ¿para qué tipo de recursos?</span><span class="sxs-lookup"><span data-stu-id="a8d91-128">If yes, what type of resources?</span></span>
  * <span data-ttu-id="a8d91-129">En caso afirmativo, ¿qué nivel de información es necesario?</span><span class="sxs-lookup"><span data-stu-id="a8d91-129">If yes, what level of information is necessary?</span></span>
  * <span data-ttu-id="a8d91-130">¿En caso afirmativo, donde debe residir registro de auditoría de hello?</span><span class="sxs-lookup"><span data-stu-id="a8d91-130">If yes, where hello audit log must reside?</span></span> <span data-ttu-id="a8d91-131">¿Local o en la nube de hello?</span><span class="sxs-lookup"><span data-stu-id="a8d91-131">On-premises or in hello cloud?</span></span>
* <span data-ttu-id="a8d91-132">¿La compañía necesita tooencrypt los mensajes de correo electrónico que contengan datos confidenciales (números de seguridad social, números de tarjeta de crédito, etcetera)?</span><span class="sxs-lookup"><span data-stu-id="a8d91-132">Does your company need tooencrypt any emails that contain sensitive data (SSNs, credit card numbers, etc)?</span></span>
* <span data-ttu-id="a8d91-133">¿La compañía necesita tooencrypt todos los documentos o contenido compartido con socios comerciales externos?</span><span class="sxs-lookup"><span data-stu-id="a8d91-133">Does your company need tooencrypt all documents/contents shared with external business partners?</span></span>
* <span data-ttu-id="a8d91-134">¿La compañía necesita las directivas corporativas de tooenforce en ciertos tipos de mensajes de correo electrónico (sin responder a todos, no reenviar)?</span><span class="sxs-lookup"><span data-stu-id="a8d91-134">Does your company need tooenforce corporate policies on certain kinds of emails (do no reply all, do not forward)?</span></span>

> [!NOTE]
> <span data-ttu-id="a8d91-135">Hacer notas de tootake seguro de cada respuesta y entender el razonamiento de hello detrás de respuesta de Hola.</span><span class="sxs-lookup"><span data-stu-id="a8d91-135">Make sure tootake notes of each answer and understand hello rationale behind hello answer.</span></span> <span data-ttu-id="a8d91-136">[Definir la estrategia de protección de datos](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) irá Hola opciones disponibles y las ventajas y desventajas de cada opción.</span><span class="sxs-lookup"><span data-stu-id="a8d91-136">[Define Data Protection Strategy](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) will go over hello options available and advantages/disadvantages of each option.</span></span>  <span data-ttu-id="a8d91-137">Las respuestas que obtenga partir de estas preguntas le servirán para seleccionar la opción que mejor se adapte a sus necesidades empresariales.</span><span class="sxs-lookup"><span data-stu-id="a8d91-137">By having answered those questions you will select which option best suits your business needs.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="a8d91-138">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a8d91-138">Next steps</span></span>
[<span data-ttu-id="a8d91-139">Determinación de los requisitos de control de acceso</span><span class="sxs-lookup"><span data-stu-id="a8d91-139">Determine access control requirements</span></span>](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)

## <a name="see-also"></a><span data-ttu-id="a8d91-140">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="a8d91-140">See Also</span></span>
[<span data-ttu-id="a8d91-141">Información general sobre las consideraciones de diseño</span><span class="sxs-lookup"><span data-stu-id="a8d91-141">Design considerations overview</span></span>](active-directory-hybrid-identity-design-considerations-overview.md)

