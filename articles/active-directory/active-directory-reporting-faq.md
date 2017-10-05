---
title: "Preguntas más frecuentes sobre informes de Azure Active Directory | Microsoft Docs"
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
ms.openlocfilehash: accf292f70bf0eafdefc00c3feeaf8e346605401
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-active-directory-reporting-faq"></a><span data-ttu-id="299df-103">Preguntas más frecuentes sobre informes de Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="299df-103">Azure Active Directory reporting FAQ</span></span>

<span data-ttu-id="299df-104">Este artículo incluye respuestas a preguntas más frecuentes (P+F) sobre los informes de Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="299df-104">This article includes answers to frequently asked questions (FAQs) about Azure Active Directory reporting.</span></span>  
<span data-ttu-id="299df-105">Para más información, vea [Informes de Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="299df-105">For more details, see [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span> 

<span data-ttu-id="299df-106">**P: ¿Cuál es la retención de datos de los registros de actividad (auditoría e inicios de sesión) en Azure Portal?**</span><span class="sxs-lookup"><span data-stu-id="299df-106">**Q: What is the data retention for activity logs (Audit and Sign-ins) in the Azure portal?**</span></span> 

<span data-ttu-id="299df-107">**R:** Se proporcionan 7 días de retención de datos para los clientes con suscripción gratuita, pero si cambian a una licencia de Azure AD Premium 1 o Premium 2, pueden acceder a los datos durante un período máximo de 30 días.</span><span class="sxs-lookup"><span data-stu-id="299df-107">**A:** We provide 7 days of data for our free customers and by switching to an Azure AD Premium 1 or Premium 2 license, you can access data for up to 30 days.</span></span> <span data-ttu-id="299df-108">Para obtener más información sobre la retención, vea [Directivas de retención de informes de Azure Active Directory](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="299df-108">For more details on retention, see [Azure Active Directory report retention policies](active-directory-reporting-retention.md)</span></span>

--- 

<span data-ttu-id="299df-109">**P: ¿Cuánto tiempo debo esperar para poder ver los datos de actividad después de haber completado una tarea?**</span><span class="sxs-lookup"><span data-stu-id="299df-109">**Q: How long does it take until I can see the Activity data after I have completed my task?**</span></span>

<span data-ttu-id="299df-110">**R:** Los registros de actividad de auditoría tienen una latencia que oscila entre 15 minutos y una hora.</span><span class="sxs-lookup"><span data-stu-id="299df-110">**A:** Audit activity logs have a latency ranging from 15 mins to an hour.</span></span> <span data-ttu-id="299df-111">Los registros de actividad de inicio de sesión tienen una latencia comprendida entre 15 minutos para la mayoría de los registros y hasta 2 horas para una serie de registros.</span><span class="sxs-lookup"><span data-stu-id="299df-111">Sign-in activity logs have a latency ranging from 15 mins for most records and up to 2 hours for a few records.</span></span>

---

<span data-ttu-id="299df-112">**P: ¿Necesito ser un administrador global para consultar los registros de actividad en Azure Portal o para obtener datos a través de la API?**</span><span class="sxs-lookup"><span data-stu-id="299df-112">**Q: Do I need to be a global admin to see the activity logs in the Azure Portal or to get data through the API?**</span></span>

<span data-ttu-id="299df-113">**R**: No.</span><span class="sxs-lookup"><span data-stu-id="299df-113">**A:** No.</span></span> <span data-ttu-id="299df-114">Puede ser un **Lector de seguridad**, un **Administrador de seguridad** o un **Administrador global** para ver datos en Azure Portal o para acceder a ellos con la API.</span><span class="sxs-lookup"><span data-stu-id="299df-114">You can either be a **Security Reader**, a **Security Admin** or a **Global Admin** to see reporting data in Azure Portal or by accessing it through the API.</span></span>

---

<span data-ttu-id="299df-115">**P: ¿Puedo obtener información del registro de actividad de Office 365 a través de Azure Portal?**</span><span class="sxs-lookup"><span data-stu-id="299df-115">**Q: Can I get Office 365 activity log information through the Azure portal?**</span></span>

<span data-ttu-id="299df-116">**R:** Aunque los registros de actividad de Office 365 y Azure AD comparten mucho de los recursos del directorio, si desea obtener una vista completa de los registros de actividad de Office 365, debe ir al Centro de administración de Office 365 para obtener la información del registro de actividad de Office 365.</span><span class="sxs-lookup"><span data-stu-id="299df-116">**A:** Even though Office 365 activity and Azure AD activity logs share a lot of the directory resources, if you want a full view of the Office 365 activity logs, you should go to the Office 365 Admin Center to get Office 365 Activity log information.</span></span>

---


<span data-ttu-id="299df-117">**P: ¿Qué API utilizo para obtener información sobre los registros de actividad de Office 365?**</span><span class="sxs-lookup"><span data-stu-id="299df-117">**Q: Which APIs do I use to get information about Office 365 Activity logs?**</span></span>

<span data-ttu-id="299df-118">**R:** Use las API de Administración de Office 365 para acceder a los [registros de actividad de Office 365 a través de una API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span><span class="sxs-lookup"><span data-stu-id="299df-118">**A:** Use the Office 365 Management APIs to access the [Office 365 Activity logs through an API](https://msdn.microsoft.com/office-365/office-365-managment-apis-overview).</span></span>

---

<span data-ttu-id="299df-119">**P: ¿Cuántos registros puedo descargar de Azure Portal?**</span><span class="sxs-lookup"><span data-stu-id="299df-119">**Q: How many records I can download from Azure portal?**</span></span>

<span data-ttu-id="299df-120">**R:** Puede descargar hasta 120 000 registros de Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="299df-120">**A:** You can download up to 120K records from the Azure portal.</span></span> <span data-ttu-id="299df-121">Los registros se ordenan a partir de los *más recientes* y, de forma predeterminada, se obtienen los últimos 120 000 registros.</span><span class="sxs-lookup"><span data-stu-id="299df-121">The records are sorted by *most recent* and by default, you get the most recent 120K records.</span></span> 

---

<span data-ttu-id="299df-122">**P: ¿Cuántos registros puedo consultar a través de las API de actividades?**</span><span class="sxs-lookup"><span data-stu-id="299df-122">**Q: How many records can I query through the activities API?**</span></span>

<span data-ttu-id="299df-123">**R:** Puede consultar hasta un millón de registros (si no usa el operador TOP, que ordena los registros a partir del más reciente).</span><span class="sxs-lookup"><span data-stu-id="299df-123">**A:** You can query up to 1 million records (if you don’t use the top operator, which sorts the record by most recent).</span></span> <span data-ttu-id="299df-124">Si usa el operador "top", puede consultar hasta 500 000 registros.</span><span class="sxs-lookup"><span data-stu-id="299df-124">If you do use the “top” operator, you can query up to 500K records.</span></span> <span data-ttu-id="299df-125">Puede encontrar las consultas de ejemplo sobre cómo usar la API [aquí](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="299df-125">You can find sample queries on how to use the API here [here](active-directory-reporting-api-getting-started.md).</span></span>

---

<span data-ttu-id="299df-126">**P: ¿Cómo puedo obtener una licencia Premium?**</span><span class="sxs-lookup"><span data-stu-id="299df-126">**Q: How do I get a premium license?**</span></span>

<span data-ttu-id="299df-127">**R:** Vea [Introducción a Azure Active Directory Premium](active-directory-get-started-premium.md) para obtener una respuesta a esta pregunta.</span><span class="sxs-lookup"><span data-stu-id="299df-127">**A:** See [Getting started with Azure Active Directory Premium](active-directory-get-started-premium.md) for an answer to this question.</span></span>

---

<span data-ttu-id="299df-128">**P: ¿Cuándo se deberían ver los datos de actividades después de obtener una licencia Premium?**</span><span class="sxs-lookup"><span data-stu-id="299df-128">**Q: How soon should I see activities data after getting a premium license?**</span></span>

<span data-ttu-id="299df-129">**R:** Si dispone ya de datos de actividades como una licencia gratuita, entonces puede ver los mismos datos.</span><span class="sxs-lookup"><span data-stu-id="299df-129">**A:** If you already have activities data as a free license, then you can see the same data.</span></span> <span data-ttu-id="299df-130">Si no tiene ningún dato, tardará uno o dos días.</span><span class="sxs-lookup"><span data-stu-id="299df-130">If you don’t have any data, then it will take one or two days.</span></span>

---

<span data-ttu-id="299df-131">**P: ¿Puedo ver los datos del último mes después de obtener una licencia de Azure AD Premium?**</span><span class="sxs-lookup"><span data-stu-id="299df-131">**Q: Do I see last month's data after getting an Azure AD premium license?**</span></span>

<span data-ttu-id="299df-132">**R:** Si ha cambiado recientemente a una versión Premium (incluida una versión de prueba), inicialmente, puede ver datos de hasta siete días.</span><span class="sxs-lookup"><span data-stu-id="299df-132">**A:** If you have recently switched to a Premium version (including a trial version), you can see data up to 7 days initially.</span></span> <span data-ttu-id="299df-133">Cuando se acumulan datos, verá hasta 30 días.</span><span class="sxs-lookup"><span data-stu-id="299df-133">When data accumulates, you will see up to 30 days.</span></span>

---

<span data-ttu-id="299df-134">**P: Hay un evento de riesgo en Identity Protection, pero no veo el inicio de sesión correspondiente en todos los inicios de sesión. ¿Es normal?**</span><span class="sxs-lookup"><span data-stu-id="299df-134">**Q: There is a risk event in Identity Protection but I’m not seeing corresponding sign-in in the all sign-ins. Is this expected?**</span></span>

<span data-ttu-id="299df-135">**R:** Sí, Identity Protection evalúa el riesgo de todos los flujos de autenticación si es interactivo o no interactivo.</span><span class="sxs-lookup"><span data-stu-id="299df-135">**A:** Yes, Identity Protection evaluates risk for all authentication flows whether if be interactive or non-interactive.</span></span> <span data-ttu-id="299df-136">Sin embargo, el informe únicamente de todos los inicios de sesión muestra los inicios de sesión interactivos.</span><span class="sxs-lookup"><span data-stu-id="299df-136">However, all sign-ins only report shows only the interactive sign-ins.</span></span>

---

<span data-ttu-id="299df-137">**P: ¿Cómo puedo descargar el informe Usuarios marcados en riesgo en Azure Portal?**</span><span class="sxs-lookup"><span data-stu-id="299df-137">**Q: How can I download the “Users flagged for risk” report in Azure portal?**</span></span>

<span data-ttu-id="299df-138">**R:**: La opción para descargar el informe *Usuarios marcados en riesgo* se agregará próximamente.</span><span class="sxs-lookup"><span data-stu-id="299df-138">**A:** The option to download *Users flagged for risk* report will be added soon.</span></span>

---

<span data-ttu-id="299df-139">**P: ¿Cómo puedo sé por qué un inicio de sesión o un usuario se marcó como en riesgo en Azure Portal?**</span><span class="sxs-lookup"><span data-stu-id="299df-139">**Q: How do I know why a sign-in or a user was flagged risky in the Azure portal?**</span></span>

<span data-ttu-id="299df-140">**R:**: Los clientes de la edición Premium pueden obtener más información sobre los eventos de riesgos subyacentes haciendo clic en el usuario en "Usuarios marcados en riesgo" o haciendo clic en "Inicios de sesión en riesgo".</span><span class="sxs-lookup"><span data-stu-id="299df-140">**A:** Premium edition customers can learn more about the underlying risk events by clicking on the user in “Users flagged for risk” or by clicking on the “Risky sign-ins”.</span></span> <span data-ttu-id="299df-141">Los clientes de edición gratuita y básica pueden ver los inicios de sesión y usuarios en riesgo sin la información de eventos de riesgo subyacentes.</span><span class="sxs-lookup"><span data-stu-id="299df-141">Free and Basic edition customers get to see the at-risk users and sign-ins without the underlying risk event information.</span></span>

---

<span data-ttu-id="299df-142">**P: ¿Cómo se calculan las direcciones IP en los inicios de sesión y en el informe de inicios de sesión de riesgo?**</span><span class="sxs-lookup"><span data-stu-id="299df-142">**Q: How are IP addresses calculated in the sign-ins and risky sign-ins report??**</span></span>

<span data-ttu-id="299df-143">**R:** Las direcciones IP se emiten de forma que no haya ninguna conexión definitiva entre una dirección IP y donde se encuentre físicamente el equipo con esa dirección.</span><span class="sxs-lookup"><span data-stu-id="299df-143">**A:** IP addresses are issued in such a way that there is no definitive connection between an IP address and where the computer with that address is physically located.</span></span> <span data-ttu-id="299df-144">Esto se complica por factores tales como proveedores de dispositivos móviles y VPN que emiten direcciones IP desde grupos centrales, a menudo muy lejos de donde se usa realmente el dispositivo del cliente.</span><span class="sxs-lookup"><span data-stu-id="299df-144">This is complicated by factors such as mobile providers and VPNs issuing IP addresses from central pools often very far from where the client device is actually used.</span></span> <span data-ttu-id="299df-145">Dado lo anterior, la conversión de la dirección IP en una ubicación física es un esfuerzo notable basado en seguimientos, datos de registro, búsquedas inversas y otra información.</span><span class="sxs-lookup"><span data-stu-id="299df-145">Given the above, converting IP address to a physical location is a best effort based on traces, registry data, reverse look ups and other information.</span></span> 

---
