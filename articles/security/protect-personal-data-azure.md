---
title: aaaProtect datos personales en Microsoft Azure | Documentos de Microsoft
description: "En primer lugar el artículo en una serie de artículos toohelp usar datos personales tooprotect de Azure"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/22/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: cbffd3872552cbd0f12539535898c41ecf7789e8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-in-microsoft-azure"></a><span data-ttu-id="a222f-103">Protección de datos personales en Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="a222f-103">Protect personal data in Microsoft Azure</span></span>

<span data-ttu-id="a222f-104">En este artículo se presenta una serie de artículos que le ayudarán a utilizar seguridad de Azure tecnologías y servicios tooprotect datos personales.</span><span class="sxs-lookup"><span data-stu-id="a222f-104">This article introduces a series of articles that help you use Azure security technologies and services tooprotect personal data.</span></span> <span data-ttu-id="a222f-105">Se trata de un requisito clave para muchas iniciativas de gobierno y cumplimiento corporativas y del sector.</span><span class="sxs-lookup"><span data-stu-id="a222f-105">This is a key requirement for many corporate and industry compliance and governance initiatives.</span></span> <span data-ttu-id="a222f-106">escenario de Hello, objetivos de empresa y de instrucción de problema se incluyen aquí.</span><span class="sxs-lookup"><span data-stu-id="a222f-106">hello scenario, problem statement and company goals are included here.</span></span>

## <a name="scenario-and-problem-statement"></a><span data-ttu-id="a222f-107">Escenario y declaración del problema</span><span class="sxs-lookup"><span data-stu-id="a222f-107">Scenario and problem statement</span></span>

<span data-ttu-id="a222f-108">Una empresa cruise grandes, con sede en Estados Unidos de hello, está ampliando sus itinerarios toooffer de operaciones en Hola Mediterráneo, Adriático y Mar Báltico, así como Hola británicas.</span><span class="sxs-lookup"><span data-stu-id="a222f-108">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, Adriatic, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="a222f-109">toosupport los esfuerzos, ha adquirido varias líneas cruise más pequeñas que encuentre en Italia, Alemania, Dinamarca y Hola inglés del Reino Unido</span><span class="sxs-lookup"><span data-stu-id="a222f-109">toosupport those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark and hello U.K.</span></span>

<span data-ttu-id="a222f-110">la compañía de Hello utiliza los datos corporativos de Microsoft Azure toostore en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="a222f-110">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="a222f-111">Esto puede incluir empleado o la información de cliente, como:</span><span class="sxs-lookup"><span data-stu-id="a222f-111">This may include employee and/or customer information such as:</span></span>

- <span data-ttu-id="a222f-112">direcciones</span><span class="sxs-lookup"><span data-stu-id="a222f-112">addresses</span></span>
- <span data-ttu-id="a222f-113">números de teléfono</span><span class="sxs-lookup"><span data-stu-id="a222f-113">phone numbers</span></span>
- <span data-ttu-id="a222f-114">números de identificación fiscal</span><span class="sxs-lookup"><span data-stu-id="a222f-114">tax identification numbers</span></span>
- <span data-ttu-id="a222f-115">Información médica</span><span class="sxs-lookup"><span data-stu-id="a222f-115">medical information</span></span>
- <span data-ttu-id="a222f-116">información de tarjeta de crédito</span><span class="sxs-lookup"><span data-stu-id="a222f-116">credit card information</span></span>

<span data-ttu-id="a222f-117">empresa Hola debe proteger la privacidad de Hola de datos de clientes y empleados asegurándose de departamentos de toothose accesible de datos que lo necesiten.</span><span class="sxs-lookup"><span data-stu-id="a222f-117">hello company must protect hello privacy of employee and customer data while making data accessible toothose departments that need it.</span></span> <span data-ttu-id="a222f-118">(por ejemplo, los departamentos de nóminas y reservas).</span><span class="sxs-lookup"><span data-stu-id="a222f-118">(such as payroll and reservations departments)</span></span>

## <a name="company-goals"></a><span data-ttu-id="a222f-119">Objetivos de la empresa</span><span class="sxs-lookup"><span data-stu-id="a222f-119">Company goals</span></span> 

- <span data-ttu-id="a222f-120">Los orígenes de datos que contienen datos personales están cifrados si residen en el almacenamiento en nube.</span><span class="sxs-lookup"><span data-stu-id="a222f-120">Data sources that contain personal data are encrypted when residing in cloud storage.</span></span>

- <span data-ttu-id="a222f-121">Datos personales que se transfieren desde una ubicación tooanother se cifran mientras en tránsito.</span><span class="sxs-lookup"><span data-stu-id="a222f-121">Personal data that is transferred from one location tooanother is encrypted while in-transit.</span></span> <span data-ttu-id="a222f-122">Esto es cierto si los datos de Hola se transmiten a través de la red virtual de Hola o a través de Internet de hello entre el centro de datos corporativo de Hola y Hola nube de Azure.</span><span class="sxs-lookup"><span data-stu-id="a222f-122">This is true if hello data is traveling across hello virtual network or across hello Internet between hello corporate datacenter and hello Azure cloud.</span></span>

- <span data-ttu-id="a222f-123">Sólidas tecnologías de control de acceso y administración de identidades protegen la confidencialidad e integridad de los datos personales frente al acceso no autorizado.</span><span class="sxs-lookup"><span data-stu-id="a222f-123">Confidentiality and integrity of personal data is protected from unauthorized access by strong identity management and access control technologies.</span></span>

- <span data-ttu-id="a222f-124">Los datos personales están protegidos contra su exposición a través de una infracción de seguridad de los mismos mediante la supervisión de vulnerabilidades y amenazas.</span><span class="sxs-lookup"><span data-stu-id="a222f-124">Personal data is protected from exposure via data breach via monitoring for vulnerabilities and threats.</span></span>

- <span data-ttu-id="a222f-125">Hello estado de seguridad de los servicios de Azure que almacenan o transmiten datos personales se evalúa toobetter de oportunidades de tooidentify proteger los datos personales.</span><span class="sxs-lookup"><span data-stu-id="a222f-125">hello security state of Azure services that store or transmit personal data is assessed tooidentify opportunities toobetter protect personal data.</span></span>

## <a name="data-protection-guidance"></a><span data-ttu-id="a222f-126">Guía de protección de datos</span><span class="sxs-lookup"><span data-stu-id="a222f-126">Data protection guidance</span></span>

<span data-ttu-id="a222f-127">Hola siguientes artículos contiene tooguidance cómo técnica que le ayudará a alcanzar los objetivos de protección de datos personales de hello mencionados anteriormente:</span><span class="sxs-lookup"><span data-stu-id="a222f-127">hello following articles contain technical how-tooguidance that will help you attain hello personal data protection goals listed above:</span></span>

- [<span data-ttu-id="a222f-128">Tecnologías de cifrado de Azure</span><span class="sxs-lookup"><span data-stu-id="a222f-128">Azure encryption technologies</span></span>](protect-personal-data-at-rest.md)

- [<span data-ttu-id="a222f-129">Tecnologías de cifrado de Azure</span><span class="sxs-lookup"><span data-stu-id="a222f-129">Azure encryption technologies</span></span>](protect-personal-data-in-transit-encryption.md)

- [<span data-ttu-id="a222f-130">Azure identity and access technologies (Tecnologías de identidad y acceso de Azure)</span><span class="sxs-lookup"><span data-stu-id="a222f-130">Azure identity and access technologies</span></span>](protect-personal-data-identity-access-controls.md)

- [<span data-ttu-id="a222f-131">Azure network security technologies (Tecnologías de Azure Network Security)</span><span class="sxs-lookup"><span data-stu-id="a222f-131">Azure network security technologies</span></span>](protect-personal-data-network-security.md)

- [<span data-ttu-id="a222f-132">Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="a222f-132">Azure Security Center</span></span>](protect-personal-data-azure-security-center.md)



## <a name="next-steps"></a><span data-ttu-id="a222f-133">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="a222f-133">Next steps</span></span>

- [<span data-ttu-id="a222f-134">Sitio de información de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="a222f-134">Azure Security Information Site</span></span>](https://aka.ms/AzureSecInfo)

- [<span data-ttu-id="a222f-135">Microsoft Trust Center</span><span class="sxs-lookup"><span data-stu-id="a222f-135">Microsoft Trust Center</span></span>](https://www.microsoft.com/TrustCenter/default.aspx)

- [<span data-ttu-id="a222f-136">Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="a222f-136">Azure Security Center</span></span>](https://azure.microsoft.com/services/security-center/)

- [<span data-ttu-id="a222f-137">Blog del equipo de seguridad de Azure</span><span class="sxs-lookup"><span data-stu-id="a222f-137">Azure Security Team Blog</span></span>](https://www.azuresecurityorg)

- [<span data-ttu-id="a222f-138">Azure.com Blog - Security (Blog de Azure.com: seguridad)</span><span class="sxs-lookup"><span data-stu-id="a222f-138">Azure.com Blog - Security</span></span>](https://azure.microsoft.com/blog/topics/security/)
