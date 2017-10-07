---
title: "Active Directory Reporting preguntas más frecuentes sobre aaaAzure | Documentos de Microsoft"
description: "Preguntas más frecuentes sobre informes de Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 534da0b1-7858-4167-9986-7a62fbd10439
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: be65a05574ea3b5b190cd02a96b211c571ba70bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-faq"></a><span data-ttu-id="e140a-103">Preguntas más frecuentes sobre informes de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e140a-103">Azure Active Directory reporting FAQ</span></span>

<span data-ttu-id="e140a-104">Este artículo incluye toofrequently respuestas preguntas frecuentes (P+f) sobre los informes de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e140a-104">This article includes answers toofrequently asked questions (FAQs) about Azure Active Directory reporting.</span></span>  
<span data-ttu-id="e140a-105">Para más información, vea [Informes de Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e140a-105">For more details, see [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span> 

<span data-ttu-id="e140a-106">**P: ¿cuál es la retención de datos de Hola para los registros de actividad (auditoría y los inicios de sesión) en hello portal de Azure?**</span><span class="sxs-lookup"><span data-stu-id="e140a-106">**Q: What is hello data retention for activity logs (Audit and Sign-ins) in hello Azure portal?**</span></span> 

<span data-ttu-id="e140a-107">**R:** proporcionamos 7 días de datos para nuestros clientes libres y cambiando tooan Azure AD Premium 1 o 2 Premium licencia, puede tener acceso a datos para los días de too30.</span><span class="sxs-lookup"><span data-stu-id="e140a-107">**A:** We provide 7 days of data for our free customers and by switching tooan Azure AD Premium 1 or Premium 2 license, you can access data for up too30 days.</span></span> <span data-ttu-id="e140a-108">Para obtener más información sobre la retención, vea [Directivas de retención de informes de Azure Active Directory](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="e140a-108">For more details on retention, see [Azure Active Directory report retention policies](active-directory-reporting-retention.md)</span></span>

--- 

<span data-ttu-id="e140a-109">**P: ¿cuánto tiempo tarda hasta que ven los datos de actividad de hello después de que se ha completado una tarea?**</span><span class="sxs-lookup"><span data-stu-id="e140a-109">**Q: How long does it take until I can see hello Activity data after I have completed my task?**</span></span>

<span data-ttu-id="e140a-110">**R:** registros de auditoría de actividad con una latencia comprendido entre 15 minutos tooan hora.</span><span class="sxs-lookup"><span data-stu-id="e140a-110">**A:** Audit activity logs have a latency ranging from 15 mins tooan hour.</span></span> <span data-ttu-id="e140a-111">Registros de actividad de inicio de sesión con una latencia comprendido entre 15 minutos para la mayoría de los registros y too2 horas para una serie de registros.</span><span class="sxs-lookup"><span data-stu-id="e140a-111">Sign-in activity logs have a latency ranging from 15 mins for most records and up too2 hours for a few records.</span></span>

---

<span data-ttu-id="e140a-112">**P: ¿necesito toobe que una actividad de administrador global toosee hello inicia una sesión Hola Portal de Azure o tooget datos a través de hello API?**</span><span class="sxs-lookup"><span data-stu-id="e140a-112">**Q: Do I need toobe a global admin toosee hello activity logs in hello Azure Portal or tooget data through hello API?**</span></span>

<span data-ttu-id="e140a-113">**R**: No.</span><span class="sxs-lookup"><span data-stu-id="e140a-113">**A:** No.</span></span> <span data-ttu-id="e140a-114">Puede ser un **lector de seguridad**, un **Administrador de seguridad** o un **administrador Global** toosee datos en el Portal de Azure o accediendo a través de hello API de informes.</span><span class="sxs-lookup"><span data-stu-id="e140a-114">You can either be a **Security Reader**, a **Security Admin** or a **Global Admin** toosee reporting data in Azure Portal or by accessing it through hello API.</span></span>

---

<span data-ttu-id="e140a-115">**P: ¿puedo obtener información de registro de actividad de Office 365 a través de hello portal de Azure?**</span><span class="sxs-lookup"><span data-stu-id="e140a-115">**Q: Can I get Office 365 activity log information through hello Azure portal?**</span></span>

<span data-ttu-id="e140a-116">**R:** aunque actividad de Office 365 y recurso compartido de registros de actividad de Azure AD muchos recursos de directorio de hello, si desea que una vista completa de Hola registros de actividad de Office 365, debe pasar la información de registro de actividad de Office 365 tooget de toohello centro de administración de Office 365.</span><span class="sxs-lookup"><span data-stu-id="e140a-116">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of hello directory resources, if you want a full view of hello Office 365 activity logs, you should go toohello Office 365 Admin Center tooget Office 365 Activity log information.</span></span>

---


<span data-ttu-id="e140a-117">**P: ¿qué es la API utilizo tooget información acerca de los registros de actividad de Office 365?**</span><span class="sxs-lookup"><span data-stu-id="e140a-117">**Q: Which APIs do I use tooget information about Office 365 Activity logs?**</span></span>

<span data-ttu-id="e140a-118">**R:** uso Hola API de administración de Office 365 tooaccess Hola [registros de actividad de Office 365 a través de una API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span><span class="sxs-lookup"><span data-stu-id="e140a-118">**A:** Use hello Office 365 Management APIs tooaccess hello [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span></span>

---

<span data-ttu-id="e140a-119">**P: ¿Cuántos registros puedo descargar de Azure Portal?**</span><span class="sxs-lookup"><span data-stu-id="e140a-119">**Q: How many records I can download from Azure portal?**</span></span>

<span data-ttu-id="e140a-120">**R:** puede descargar los registros de too120K de hello portal de Azure.</span><span class="sxs-lookup"><span data-stu-id="e140a-120">**A:** You can download up too120K records from hello Azure portal.</span></span> <span data-ttu-id="e140a-121">Hola registros se ordenan por *más reciente* y de forma predeterminada, se obtienen los registros de hello K más reciente de 120.</span><span class="sxs-lookup"><span data-stu-id="e140a-121">hello records are sorted by *most recent* and by default, you get hello most recent 120K records.</span></span> 

---

<span data-ttu-id="e140a-122">**P: ¿cuántos registros se pueden consultar a través de las actividades de hello API?**</span><span class="sxs-lookup"><span data-stu-id="e140a-122">**Q: How many records can I query through hello activities API?**</span></span>

<span data-ttu-id="e140a-123">**R:** puede consultar los registros de millones de too1 (si no utiliza el operador top de hello, que ordena el registro de hello más reciente).</span><span class="sxs-lookup"><span data-stu-id="e140a-123">**A:** You can query up too1 million records (if you don’t use hello top operator, which sorts hello record by most recent).</span></span> <span data-ttu-id="e140a-124">Si usa el operador de "top" Hola, puede consultar los registros de too500K.</span><span class="sxs-lookup"><span data-stu-id="e140a-124">If you do use hello “top” operator, you can query up too500K records.</span></span> <span data-ttu-id="e140a-125">Puede encontrar las consultas de ejemplo de cómo toouse Hola API aquí [aquí](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="e140a-125">You can find sample queries on how toouse hello API here [here](active-directory-reporting-api-getting-started.md).</span></span>

---

<span data-ttu-id="e140a-126">**P: ¿Cómo puedo obtener una licencia Premium?**</span><span class="sxs-lookup"><span data-stu-id="e140a-126">**Q: How do I get a premium license?**</span></span>

<span data-ttu-id="e140a-127">**R:** vea [Introducción a Azure Active Directory Premium](active-directory-get-started-premium.md) para una pregunta de toothis de respuesta.</span><span class="sxs-lookup"><span data-stu-id="e140a-127">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer toothis question.</span></span>

---

<span data-ttu-id="e140a-128">**P: ¿Cuándo se deberían ver los datos de actividades después de obtener una licencia Premium?**</span><span class="sxs-lookup"><span data-stu-id="e140a-128">**Q: How soon should I see activities data after getting a premium license?**</span></span>

<span data-ttu-id="e140a-129">**R:** si ya tiene datos de las actividades como una licencia gratuita, a continuación, puede ver Hola los mismos datos.</span><span class="sxs-lookup"><span data-stu-id="e140a-129">**A:** If you already have activities data as a free license, then you can see hello same data.</span></span> <span data-ttu-id="e140a-130">Si no tiene ningún dato, tardará uno o dos días.</span><span class="sxs-lookup"><span data-stu-id="e140a-130">If you don’t have any data, then it will take one or two days.</span></span>

---

<span data-ttu-id="e140a-131">**P: ¿Puedo ver los datos del último mes después de obtener una licencia de Azure AD Premium?**</span><span class="sxs-lookup"><span data-stu-id="e140a-131">**Q: Do I see last month's data after getting an Azure AD premium license?**</span></span>

<span data-ttu-id="e140a-132">**R:** si ha cambiado recientemente tooa Premium versión (incluida una versión de prueba), puede ver los datos de too7 días inicialmente.</span><span class="sxs-lookup"><span data-stu-id="e140a-132">**A:** If you have recently switched tooa Premium version (including a trial version), you can see data up too7 days initially.</span></span> <span data-ttu-id="e140a-133">Cuando se acumulan datos, verá los too30 días.</span><span class="sxs-lookup"><span data-stu-id="e140a-133">When data accumulates, you will see up too30 days.</span></span>

---

<span data-ttu-id="e140a-134">**P: ¿hay un evento de riesgo en la protección de identidad pero no veo un inicio de sesión correspondiente en hello todos los inicios de sesión. ¿Es normal?**</span><span class="sxs-lookup"><span data-stu-id="e140a-134">**Q: There is a risk event in Identity Protection but I’m not seeing corresponding sign-in in hello all sign-ins. Is this expected?**</span></span>

<span data-ttu-id="e140a-135">**R:** Sí, Identity Protection evalúa el riesgo de todos los flujos de autenticación si es interactivo o no interactivo.</span><span class="sxs-lookup"><span data-stu-id="e140a-135">**A:** Yes, Identity Protection evaluates risk for all authentication flows whether if be interactive or non-interactive.</span></span> <span data-ttu-id="e140a-136">Sin embargo, el único informe de todos los inicios de sesión muestra hello solo inicios de sesión interactivos.</span><span class="sxs-lookup"><span data-stu-id="e140a-136">However, all sign-ins only report shows only hello interactive sign-ins.</span></span>

---

<span data-ttu-id="e140a-137">**P: ¿Cómo puedo descargar informes de "Usuarios marcan para su riesgo" hello en el portal de Azure?**</span><span class="sxs-lookup"><span data-stu-id="e140a-137">**Q: How can I download hello “Users flagged for risk” report in Azure portal?**</span></span>

<span data-ttu-id="e140a-138">**R:** toodownload de opción de hello *usuarios marcan para su riesgo* pronto se agregará el informe.</span><span class="sxs-lookup"><span data-stu-id="e140a-138">**A:** hello option toodownload *Users flagged for risk* report will be added soon.</span></span>

---

<span data-ttu-id="e140a-139">**P: ¿cómo saber por qué un inicio de sesión o un usuario se marcó arriesgado Hola portal de Azure?**</span><span class="sxs-lookup"><span data-stu-id="e140a-139">**Q: How do I know why a sign-in or a user was flagged risky in hello Azure portal?**</span></span>

<span data-ttu-id="e140a-140">**R:** clientes de edición Premium pueden obtener más información sobre Hola subyacente eventos de riesgo, haga clic en usuario de hello en "Usuarios marcan para su riesgo" o haciendo clic en "Arriesgados inicios de sesión de" Hola.</span><span class="sxs-lookup"><span data-stu-id="e140a-140">**A:** Premium edition customers can learn more about hello underlying risk events by clicking on hello user in “Users flagged for risk” or by clicking on hello “Risky sign-ins”.</span></span> <span data-ttu-id="e140a-141">Los clientes de edición gratuita y básica obtener usuarios en riesgo de toosee hello e inicios de sesión sin Hola subyacente información sobre eventos de riesgo.</span><span class="sxs-lookup"><span data-stu-id="e140a-141">Free and Basic edition customers get toosee hello at-risk users and sign-ins without hello underlying risk event information.</span></span>

---

<span data-ttu-id="e140a-142">**P: ¿cómo se calculan las direcciones IP en inicios de sesión de Hola y el informe de inicios de sesión riesgo?**</span><span class="sxs-lookup"><span data-stu-id="e140a-142">**Q: How are IP addresses calculated in hello sign-ins and risky sign-ins report??**</span></span>

<span data-ttu-id="e140a-143">**R:** direcciones IP se emiten de forma que no hay ninguna conexión definitiva entre una dirección IP y dónde se encuentran físicamente equipo del Hola con esa dirección.</span><span class="sxs-lookup"><span data-stu-id="e140a-143">**A:** IP addresses are issued in such a way that there is no definitive connection between an IP address and where hello computer with that address is physically located.</span></span> <span data-ttu-id="e140a-144">Esto se complica por factores como proveedores de dispositivos móviles y las redes privadas virtuales emitir las direcciones IP de grupos centrales a menudo muy lejos de donde se usa realmente el dispositivo de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="e140a-144">This is complicated by factors such as mobile providers and VPNs issuing IP addresses from central pools often very far from where hello client device is actually used.</span></span> <span data-ttu-id="e140a-145">Dados Hola anterior, la conversión de ubicación física del tooa de dirección IP es un esfuerzo en función de seguimientos, datos del registro, busque inversa SAI (UPS) y otra información.</span><span class="sxs-lookup"><span data-stu-id="e140a-145">Given hello above, converting IP address tooa physical location is a best effort based on traces, registry data, reverse look ups and other information.</span></span> 

---
