---
title: aaaProtect datos personales con el centro de seguridad de Azure | Documentos de Microsoft
description: "protección de datos personales mediante Azure Security Center"
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
ms.date: 08/24/2017
ms.author: barclayn
ms.custom: 
ms.openlocfilehash: 8e2c893d13318392f47fa912089d52618f9e7b45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="protect-personal-data-from-breaches-and-attacks-azure-security-center"></a><span data-ttu-id="edb51-103">Protección de datos personales frente a infracciones de seguridad y ataques: Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="edb51-103">Protect personal data from breaches and attacks: Azure Security Center</span></span>

<span data-ttu-id="edb51-104">Este artículo le ayudará a entender cómo incumple toouse Azure Security Center tooprotect de los datos personal y ataques.</span><span class="sxs-lookup"><span data-stu-id="edb51-104">This article will help you understand how toouse Azure Security Center tooprotect personal data from breaches and attacks.</span></span>

## <a name="scenario"></a><span data-ttu-id="edb51-105">Escenario</span><span class="sxs-lookup"><span data-stu-id="edb51-105">Scenario</span></span> 

<span data-ttu-id="edb51-106">Una empresa cruise grandes, con sede en Estados Unidos, Hola está ampliando sus itinerarios toooffer de operaciones en hello Mediterráneo y Mar Báltico, así como Hola británicas.</span><span class="sxs-lookup"><span data-stu-id="edb51-106">A large cruise company, headquartered in hello United States, is expanding its operations toooffer itineraries in hello Mediterranean, and Baltic seas, as well as hello British Isles.</span></span> <span data-ttu-id="edb51-107">toohelp en los esfuerzos, ha adquirido varias líneas cruise más pequeñas con sede en Italia, Alemania, Dinamarca y Hola inglés del Reino Unido</span><span class="sxs-lookup"><span data-stu-id="edb51-107">toohelp in those efforts, it has acquired several smaller cruise lines based in Italy, Germany, Denmark, and hello U.K.</span></span>

<span data-ttu-id="edb51-108">la compañía de Hello utiliza los datos corporativos de Microsoft Azure toostore en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="edb51-108">hello company uses Microsoft Azure toostore corporate data in hello cloud.</span></span> <span data-ttu-id="edb51-109">Esto incluye información de identificación personal como nombres, direcciones, números de teléfono e información de la tarjeta de crédito.</span><span class="sxs-lookup"><span data-stu-id="edb51-109">This includes personal identifiable information such as names, addresses, phone numbers, and credit card information.</span></span> <span data-ttu-id="edb51-110">También incluye información de recursos humanos como:</span><span class="sxs-lookup"><span data-stu-id="edb51-110">It also includes Human Resources information such as:</span></span>

- <span data-ttu-id="edb51-111">Direcciones</span><span class="sxs-lookup"><span data-stu-id="edb51-111">Addresses</span></span>
- <span data-ttu-id="edb51-112">Números de teléfono</span><span class="sxs-lookup"><span data-stu-id="edb51-112">Phone numbers</span></span>
- <span data-ttu-id="edb51-113">Números de identificación fiscal</span><span class="sxs-lookup"><span data-stu-id="edb51-113">Tax identification numbers</span></span>
- <span data-ttu-id="edb51-114">Información médica</span><span class="sxs-lookup"><span data-stu-id="edb51-114">Medical information</span></span>

<span data-ttu-id="edb51-115">línea de Hello cruise también mantiene una base de datos grande de miembros del programa de recompensa y fidelidad.</span><span class="sxs-lookup"><span data-stu-id="edb51-115">hello cruise line also maintains a large database of reward and loyalty program members.</span></span> <span data-ttu-id="edb51-116">Red de Hola de acceso de los empleados corporativos de oficinas remotas y la Agencia de viajes de la compañía de Hola ubicados en todo Hola a todos tienen acceso a recursos de empresa de toosome.</span><span class="sxs-lookup"><span data-stu-id="edb51-116">Corporate employees access hello network from hello company’s remote offices and travel agents located around hello world have access toosome company resources.</span></span>
<span data-ttu-id="edb51-117">Datos personales pasan a través de la red de hello entre estas ubicaciones y el centro de datos de Microsoft de Hola.</span><span class="sxs-lookup"><span data-stu-id="edb51-117">Personal data travels across hello network between these locations and hello Microsoft data center.</span></span>

## <a name="problem-statement"></a><span data-ttu-id="edb51-118">Declaración del problema</span><span class="sxs-lookup"><span data-stu-id="edb51-118">Problem statement</span></span>

<span data-ttu-id="edb51-119">empresa Hola está preocupa por la amenaza de Hola de ataques en sus recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="edb51-119">hello company is concerned about hello threat of attacks on their Azure resources.</span></span> <span data-ttu-id="edb51-120">Desean tooprevent exposición de las personas toounauthorized de datos personales de los empleados y los clientes.</span><span class="sxs-lookup"><span data-stu-id="edb51-120">They want tooprevent exposure of customers’ and employees’ personal data toounauthorized persons.</span></span> <span data-ttu-id="edb51-121">Desea obtener instrucciones sobre la prevención y respuesta o corrección, así como un modo eficaz toomonitor hello en curso la seguridad de sus recursos de nube.</span><span class="sxs-lookup"><span data-stu-id="edb51-121">They want guidance on both prevention and response/remediation, as well as an effective way toomonitor hello ongoing security of their cloud resources.</span></span>
<span data-ttu-id="edb51-122">Necesita una línea de defensa sólida contra los atacantes sofisticados y organizados que hay en la actualidad.</span><span class="sxs-lookup"><span data-stu-id="edb51-122">They need a strong line of defense against today’s sophisticated and organized attackers.</span></span>

## <a name="company-goal"></a><span data-ttu-id="edb51-123">Objetivo de la empresa</span><span class="sxs-lookup"><span data-stu-id="edb51-123">Company goal</span></span>

<span data-ttu-id="edb51-124">Uno de los objetivos de la compañía de hello es privacidad de hello tooensure de los datos personales de los empleados y los clientes mediante la protección contra amenazas.</span><span class="sxs-lookup"><span data-stu-id="edb51-124">One of hello company’s goals is tooensure hello privacy of customers’ and employees’ personal data by protecting it from threats.</span></span> <span data-ttu-id="edb51-125">Uno de sus objetivos es toorespond inmediatamente toosigns de infracción toomitigate Hola impacto.</span><span class="sxs-lookup"><span data-stu-id="edb51-125">One of their goals is toorespond immediately toosigns of breach toomitigate hello impact.</span></span> <span data-ttu-id="edb51-126">Necesita una manera de tooassess Hola estado actual de la seguridad, identificar las configuraciones vulnerables y corregirlas.</span><span class="sxs-lookup"><span data-stu-id="edb51-126">It requires a way tooassess hello current state of security, identify vulnerable configurations, and remediate them.</span></span>

## <a name="solutions"></a><span data-ttu-id="edb51-127">Soluciones</span><span class="sxs-lookup"><span data-stu-id="edb51-127">Solutions</span></span>

<span data-ttu-id="edb51-128">Microsoft Azure Security Center (ASC) proporciona una solución integrada de supervisión de la seguridad y administración de directivas.</span><span class="sxs-lookup"><span data-stu-id="edb51-128">Microsoft Azure Security Center (ASC) provides an integrated security monitoring and policy management solution.</span></span> <span data-ttu-id="edb51-129">Ofrece las funcionalidades sencillas y eficaces de prevención, detección y respuesta ante amenazas.</span><span class="sxs-lookup"><span data-stu-id="edb51-129">It delivers easy-to-use and effective threat prevention, detection, and response capabilities.</span></span>

### <a name="prevention"></a><span data-ttu-id="edb51-130">Prevención</span><span class="sxs-lookup"><span data-stu-id="edb51-130">Prevention</span></span>

<span data-ttu-id="edb51-131">ASC le ayuda a evitar infracciones habilitando las directivas de seguridad tooset, proporcionan acceso just-in-time e implementar las recomendaciones de seguridad.</span><span class="sxs-lookup"><span data-stu-id="edb51-131">ASC helps you prevent breaches by enabling you tooset security policies, provide just-in-time access, and implement security recommendations.</span></span>

<span data-ttu-id="edb51-132">Una directiva de seguridad define el conjunto de Hola de controles que se recomienda para los recursos dentro de hello especificado suscripción.</span><span class="sxs-lookup"><span data-stu-id="edb51-132">A security policy defines hello set of controls recommended for resources within hello specified subscription.</span></span> <span data-ttu-id="edb51-133">Justo a tiempo acceso puede ser usado toolock hacia abajo el tráfico entrante tooyour máquinas virtuales de Azure, lo que reduce la exposición tooattacks.</span><span class="sxs-lookup"><span data-stu-id="edb51-133">Just in time access can be used toolock down inbound traffic tooyour Azure VMs, reducing exposure tooattacks.</span></span> <span data-ttu-id="edb51-134">Recomendaciones de seguridad se crean ASC después de analizar el estado de seguridad de Hola de los recursos de Azure.</span><span class="sxs-lookup"><span data-stu-id="edb51-134">Security recommendations are created by ASC after analyzing hello security state of your Azure resources.</span></span>

#### <a name="how-do-i-set-security-policies-in-asc"></a><span data-ttu-id="edb51-135">¿Cómo se pueden establecer directivas de seguridad en ASC?</span><span class="sxs-lookup"><span data-stu-id="edb51-135">How do I set security policies in ASC?</span></span>

<span data-ttu-id="edb51-136">Puede configurar directivas de seguridad para cada suscripción.</span><span class="sxs-lookup"><span data-stu-id="edb51-136">You can configure security policies for each subscription.</span></span> <span data-ttu-id="edb51-137">toomodify una directiva de seguridad, debe ser propietario o colaborador de esa suscripción.</span><span class="sxs-lookup"><span data-stu-id="edb51-137">toomodify a security policy, you must be an owner or contributor of that subscription.</span></span> <span data-ttu-id="edb51-138">Hola portal de Azure, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="edb51-138">In hello Azure portal, do hello following:</span></span>

1. <span data-ttu-id="edb51-139">Seleccione **directiva** en el panel de hello ASC.</span><span class="sxs-lookup"><span data-stu-id="edb51-139">Select **Policy** in hello ASC dashboard.</span></span>

2. <span data-ttu-id="edb51-140">Seleccione la suscripción de hello en el que desea que Directiva de hello tooenable.</span><span class="sxs-lookup"><span data-stu-id="edb51-140">Select hello subscription on which you want tooenable hello policy.</span></span>

3. <span data-ttu-id="edb51-141">Elija **directivas de prevención** tooconfigure directivas por suscripción.</span><span class="sxs-lookup"><span data-stu-id="edb51-141">Choose **Prevention policy** tooconfigure policies per subscription.</span></span> <span data-ttu-id="edb51-142">**Recopilar datos de máquinas virtuales** debe establecerse demasiado**en.**</span><span class="sxs-lookup"><span data-stu-id="edb51-142">**Collect data from virtual machines** should be set too**On.**</span></span>

4. <span data-ttu-id="edb51-143">Hola **directivas de prevención** opciones, seleccionadas **en** recomendaciones de seguridad de hello tooenable que son relevantes para la suscripción de Hola.</span><span class="sxs-lookup"><span data-stu-id="edb51-143">In hello **Prevention policy** options, select **On** tooenable hello security recommendations that are relevant for hello subscription.</span></span>

![](media/protect-personal-data-azure-security-center/prevention-policy.png)

<span data-ttu-id="edb51-144">Para obtener más instrucciones y una explicación de cada una de las recomendaciones de la directiva de Hola que se pueden habilitar, consulte [establecer directivas de seguridad de Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span><span class="sxs-lookup"><span data-stu-id="edb51-144">For more detailed instructions and an explanation of each of hello policy recommendations that can be enabled, see [Set security policies in Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-policies#set-security-policies).</span></span>

#### <a name="how-do-i-configure-just-in-time-access-jit"></a><span data-ttu-id="edb51-145">¿Cómo se puede configurar el acceso Just-In-Time (JIT)?</span><span class="sxs-lookup"><span data-stu-id="edb51-145">How do I configure Just in Time Access (JIT)?</span></span>

<span data-ttu-id="edb51-146">Cuando JIT está habilitada, el centro de seguridad para bloquear el tráfico entrante tooyour máquinas virtuales de Azure mediante la creación de una regla de NSG.</span><span class="sxs-lookup"><span data-stu-id="edb51-146">When JIT is enabled, Security Center locks down inbound traffic tooyour Azure VMs by creating an NSG rule.</span></span> <span data-ttu-id="edb51-147">Seleccionar puertos hello en hello VM toowhich se bloqueará el tráfico entrante hacia abajo.</span><span class="sxs-lookup"><span data-stu-id="edb51-147">You select hello ports on hello VM toowhich inbound traffic will be locked down.</span></span> <span data-ttu-id="edb51-148">toouse JIT acceso, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="edb51-148">toouse JIT access, do hello following:</span></span>

1. <span data-ttu-id="edb51-149">Seleccione hello **en el icono de acceso VM de tiempo** en la hoja de hello ASC.</span><span class="sxs-lookup"><span data-stu-id="edb51-149">Select hello **Just in time VM access tile** on hello ASC blade.</span></span>

2. <span data-ttu-id="edb51-150">Seleccione hello **recomendado** ficha.</span><span class="sxs-lookup"><span data-stu-id="edb51-150">Select hello **Recommended** tab.</span></span>

3. <span data-ttu-id="edb51-151">En **máquinas virtuales**, seleccione hello las máquinas virtuales que desea tooenable.</span><span class="sxs-lookup"><span data-stu-id="edb51-151">Under **VMs**, select hello VMs that you want tooenable.</span></span> <span data-ttu-id="edb51-152">Esto coloca una máquina virtual de tooa siguiente marca de verificación.</span><span class="sxs-lookup"><span data-stu-id="edb51-152">This puts a checkmark next tooa VM.</span></span> 
4. <span data-ttu-id="edb51-153">Seleccione **Habilitar JIT** en VM.</span><span class="sxs-lookup"><span data-stu-id="edb51-153">Select **Enable JIT** on VMs.</span></span>
5. <span data-ttu-id="edb51-154">Seleccione **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="edb51-154">Select **Save**.</span></span>

<span data-ttu-id="edb51-155">A continuación, puede ver los puertos predeterminados de Hola que ASC recomienda al estar habilitado para JIT.</span><span class="sxs-lookup"><span data-stu-id="edb51-155">Then you can see hello default ports that ASC recommends being enabled for JIT.</span></span> <span data-ttu-id="edb51-156">También puede agregar y configurar un puerto nuevo en el que desea tooenable Hola justo a tiempo la solución.</span><span class="sxs-lookup"><span data-stu-id="edb51-156">You can also add and configure a new port on which you want tooenable hello just in time solution.</span></span> <span data-ttu-id="edb51-157">Hola **en el acceso en tiempo de máquina virtual** icono Hola centro de seguridad muestra el número de Hola de máquinas virtuales configuradas para el acceso JIT.</span><span class="sxs-lookup"><span data-stu-id="edb51-157">hello **Just in time VM access** tile in hello Security Center shows hello number of VMs configured for JIT access.</span></span> <span data-ttu-id="edb51-158">También muestra hello número de solicitudes de acceso autorizado a realizadas en hello última semana.</span><span class="sxs-lookup"><span data-stu-id="edb51-158">It also shows hello number of approved access requests made in hello last week.</span></span>

![](media/protect-personal-data-azure-security-center/jit-vm.png)

<span data-ttu-id="edb51-159">Para obtener instrucciones sobre cómo toodo esto, y ver información adicional sobre sólo en el acceso de tiempo, [administrar el acceso de máquina virtual con justo a tiempo.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span><span class="sxs-lookup"><span data-stu-id="edb51-159">For instructions on how toodo this, and additional information about Just in Time access, see [Manage virtual machine access using just in time.](https://docs.microsoft.com/azure/security-center/security-center-just-in-time)</span></span>

#### <a name="how-do-i-implement-asc-security-recommendations"></a><span data-ttu-id="edb51-160">¿Cómo se pueden implementar recomendaciones de seguridad de ASC?</span><span class="sxs-lookup"><span data-stu-id="edb51-160">How do I implement ASC security recommendations?</span></span>

<span data-ttu-id="edb51-161">Cuando el Centro de seguridad identifica vulnerabilidades de seguridad potenciales, crea recomendaciones.</span><span class="sxs-lookup"><span data-stu-id="edb51-161">When Security Center identifies potential security vulnerabilities, it creates recommendations.</span></span> <span data-ttu-id="edb51-162">recomendaciones de Hello guiarle por proceso de Hola de configuración de controles de Hola que sea necesitado.</span><span class="sxs-lookup"><span data-stu-id="edb51-162">hello recommendations guide you through hello process of configuring hello needed controls.</span></span> 
1. <span data-ttu-id="edb51-163">Seleccione hello **recomendaciones** icono Panel de hello ASC.</span><span class="sxs-lookup"><span data-stu-id="edb51-163">Select hello **Recommendations** tile on hello ASC dashboard.</span></span>

2. <span data-ttu-id="edb51-164">Ver recomendaciones de hello, que se muestran en un formato de tabla, donde cada línea representa una recomendación.</span><span class="sxs-lookup"><span data-stu-id="edb51-164">View hello recommendations, which are shown in a table format where each line represents one recommendation.</span></span>

3. <span data-ttu-id="edb51-165">recomendaciones de toofilter, seleccione **filtro** y seleccionar valores de gravedad y el estado de hello desea toosee.</span><span class="sxs-lookup"><span data-stu-id="edb51-165">toofilter recommendations, select **Filter** and select hello severity and state values you wish toosee.</span></span>

4. <span data-ttu-id="edb51-166">toodismiss una recomendación que no es aplicable, puede haga clic y seleccione **descartar.**</span><span class="sxs-lookup"><span data-stu-id="edb51-166">toodismiss a recommendation that is not applicable, you can right click and select **Dismiss.**</span></span>

5. <span data-ttu-id="edb51-167">Evalúe qué recomendación debería aplicarse primero.</span><span class="sxs-lookup"><span data-stu-id="edb51-167">Evaluate which recommendation should be applied first.</span></span>

6. <span data-ttu-id="edb51-168">Aplicar recomendaciones de hello en orden de prioridad.</span><span class="sxs-lookup"><span data-stu-id="edb51-168">Apply hello recommendations in order of priority.</span></span>

<span data-ttu-id="edb51-169">Para obtener una lista de posibles recomendaciones y procedimientos paso a paso acerca de cómo tooapply cada uno, vea [administrar las recomendaciones de seguridad en el centro de seguridad de Azure.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span><span class="sxs-lookup"><span data-stu-id="edb51-169">For a list of possible recommendations and walk-throughs on how tooapply each, see [Managing security recommendations in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-recommendations)</span></span>

### <a name="detection-and-response"></a><span data-ttu-id="edb51-170">Detección y respuesta</span><span class="sxs-lookup"><span data-stu-id="edb51-170">Detection and Response</span></span>

<span data-ttu-id="edb51-171">Detección y respuesta van juntas, como se desee toorespond tan pronto como sea posible después de que se detecta una amenaza.</span><span class="sxs-lookup"><span data-stu-id="edb51-171">Detection and response go together, as you want toorespond as quickly as possible after a threat is detected.</span></span>
<span data-ttu-id="edb51-172">La detección de amenazas ASC funciona mediante la recopilación automáticamente información de seguridad de los recursos de Azure, red de Hola y soluciones de socios conectados.</span><span class="sxs-lookup"><span data-stu-id="edb51-172">ASC threat detection works by automatically collecting security information from your Azure resources, hello network, and connected partner solutions.</span></span> <span data-ttu-id="edb51-173">ASC es capaz de actualizar rápidamente los algoritmos de detección a medida que los atacantes idean nuevos y más sofisticados ataques de seguridad.</span><span class="sxs-lookup"><span data-stu-id="edb51-173">ASC can rapidly update its detection algorithms as attackers release new and increasingly sophisticated exploits.</span></span> <span data-ttu-id="edb51-174">Para obtener información más detallada sobre cómo funciona la detección de amenazas de ASC, consulte [Funcionalidades de detección de Azure Security Center](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span><span class="sxs-lookup"><span data-stu-id="edb51-174">For more detailed information on how ASC’s threat detection works, see [Azure Security Center detection capabilities](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities).</span></span>

#### <a name="how-do-i-manage-and-respond-toosecurity-alerts"></a><span data-ttu-id="edb51-175">¿Cómo administrar y responder a alertas de toosecurity?</span><span class="sxs-lookup"><span data-stu-id="edb51-175">How do I manage and respond toosecurity alerts?</span></span>

<span data-ttu-id="edb51-176">Se muestra una lista de alertas de seguridad con prioridades en el centro de seguridad junto con hello información que necesita tooquickly investigar el problema de Hola.</span><span class="sxs-lookup"><span data-stu-id="edb51-176">A list of prioritized security alerts is shown in Security Center along with hello information you need tooquickly investigate hello problem.</span></span> <span data-ttu-id="edb51-177">Centro de seguridad también incluye recomendaciones sobre cómo tooremediate un ataque.</span><span class="sxs-lookup"><span data-stu-id="edb51-177">Security Center also includes recommendations for how tooremediate an attack.</span></span> <span data-ttu-id="edb51-178">toomanage la seguridad de alertas, hacer Hola después de:</span><span class="sxs-lookup"><span data-stu-id="edb51-178">toomanage your security alerts, do hello following:</span></span>

1. <span data-ttu-id="edb51-179">Seleccione hello **alertas de seguridad** el icono Panel de hello ASC.</span><span class="sxs-lookup"><span data-stu-id="edb51-179">Select hello **Security alerts** tile in hello ASC dashboard.</span></span> <span data-ttu-id="edb51-180">Aquí verá detalles de cada alerta.</span><span class="sxs-lookup"><span data-stu-id="edb51-180">This shows details for each alert.</span></span>

2. <span data-ttu-id="edb51-181">alertas de toofilter basadas en fecha, el estado y la gravedad, seleccione **filtro** y, a continuación, seleccione los valores de hello que desee toosee.</span><span class="sxs-lookup"><span data-stu-id="edb51-181">toofilter alerts based on date, state, and severity, select **Filter** and then select hello values you want toosee.</span></span>

3. <span data-ttu-id="edb51-182">toorespond tooan alerta, selecciónelo y revise la información de hello, seleccione recurso Hola que fuera atacado.</span><span class="sxs-lookup"><span data-stu-id="edb51-182">toorespond tooan alert, select it and review hello information, then select hello resource that was attacked.</span></span>

4. <span data-ttu-id="edb51-183">Hola **descripción** campo, podrá ver detalles, incluidas las actualizaciones recomendadas.</span><span class="sxs-lookup"><span data-stu-id="edb51-183">In hello **Description** field, you’ll see details, including recommended remediation.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts.png)

<span data-ttu-id="edb51-184">Para obtener más instrucciones sobre las alertas de toosecurity responde, consulte [toosecurity de administración y de que responda las alertas en el centro de seguridad de Azure.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span><span class="sxs-lookup"><span data-stu-id="edb51-184">For more detailed instructions on responding toosecurity alerts, see [Managing and responding toosecurity alerts in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts)</span></span>

<span data-ttu-id="edb51-185">Para obtener ayuda en la investigación de alertas de seguridad, empresa Hola puede integrar las alertas ASC con su propia solución SIEM, con [integración de Azure registro](https://aka.ms/AzLog).</span><span class="sxs-lookup"><span data-stu-id="edb51-185">For further help in investigating security alerts, hello company can integrate ASC alerts with its own SIEM solution, using [Azure Log Integration](https://aka.ms/AzLog).</span></span>

#### <a name="how-do-i-manage-security-incidents"></a><span data-ttu-id="edb51-186">¿Cómo se pueden administrar incidentes de seguridad?</span><span class="sxs-lookup"><span data-stu-id="edb51-186">How do I manage security incidents?</span></span>

<span data-ttu-id="edb51-187">En ASC, un incidente de seguridad es la suma de todas las alertas de un recurso que se alinean con patrones de cadenas de eliminación.</span><span class="sxs-lookup"><span data-stu-id="edb51-187">In ASC, a security incident is an aggregation of all alerts for a resource that align with kill chain patterns.</span></span> <span data-ttu-id="edb51-188">Un incidente revelará lista Hola de alertas relacionadas, lo que permite tooobtain obtener más información sobre cada repetición.</span><span class="sxs-lookup"><span data-stu-id="edb51-188">An Incident will reveal hello list of related alerts, which enables you tooobtain more information about each occurrence.</span></span> <span data-ttu-id="edb51-189">Incidentes aparecen en Hola icono de alertas de seguridad y de hoja.</span><span class="sxs-lookup"><span data-stu-id="edb51-189">Incidents appear in hello Security Alerts tile and blade.</span></span>

<span data-ttu-id="edb51-190">tooreview y administrar incidentes de seguridad, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="edb51-190">tooreview and manage security incidents, do hello following:</span></span>

1. <span data-ttu-id="edb51-191">Seleccione hello **alertas de seguridad** icono.</span><span class="sxs-lookup"><span data-stu-id="edb51-191">Select hello **Security alerts** tile.</span></span> <span data-ttu-id="edb51-192">Si se detecta un incidente de seguridad, aparecerá en el gráfico de alertas de seguridad de Hola.</span><span class="sxs-lookup"><span data-stu-id="edb51-192">if a security incident is detected, it will appear under hello security alerts graph.</span></span> <span data-ttu-id="edb51-193">Tendrá un icono distinto de otras alertas.</span><span class="sxs-lookup"><span data-stu-id="edb51-193">It will have an icon that’s different from other alerts.</span></span>

2. <span data-ttu-id="edb51-194">Seleccione toosee incidentes hello más detalles sobre este incidente de seguridad.</span><span class="sxs-lookup"><span data-stu-id="edb51-194">Select hello incident toosee more details about this security incident.</span></span> <span data-ttu-id="edb51-195">Detalles adicionales incluyen su descripción completa, su gravedad, su estado actual, Hola atacada recursos, los pasos de corrección de Hola de incidente de Hola y Hola alertas que se incluyeron en este incidente.</span><span class="sxs-lookup"><span data-stu-id="edb51-195">Additional details include its full description, its severity, its current state, hello attacked resource, hello remediation steps for hello incident, and hello alerts that were included in this incident.</span></span>

<span data-ttu-id="edb51-196">Puede filtrar toosee **incidentes solo**, **alertas solo**, o **ambos**.</span><span class="sxs-lookup"><span data-stu-id="edb51-196">You can filter toosee **incidents only**, **alerts only**, or **both**.</span></span>

#### <a name="how-do-i-access-hello-threat-intelligence-report"></a><span data-ttu-id="edb51-197">¿Cómo obtengo acceso Hola informes de inteligencia de amenazas?</span><span class="sxs-lookup"><span data-stu-id="edb51-197">How do I access hello Threat Intelligence Report?</span></span>

<span data-ttu-id="edb51-198">ASC analiza la información frente a amenazas de tooidentify de varios orígenes.</span><span class="sxs-lookup"><span data-stu-id="edb51-198">ASC analyzes information from multiple sources tooidentify threats.</span></span> <span data-ttu-id="edb51-199">los equipos de respuesta a incidentes de tooassist investigación y corregir las amenazas, centro de seguridad incluye un informe de inteligencia de amenazas que contiene información sobre la amenaza de Hola que se detectó.</span><span class="sxs-lookup"><span data-stu-id="edb51-199">tooassist incident response teams investigate and remediate threats, Security Center includes a threat intelligence report that contains information about hello threat that was detected.</span></span>

<span data-ttu-id="edb51-200">Security Center tiene tres tipos de informes de amenazas, que pueden variar por ataque.</span><span class="sxs-lookup"><span data-stu-id="edb51-200">Security Center has three types of threat reports, which can vary per attack.</span></span>
<span data-ttu-id="edb51-201">informes de Hello disponibles son:</span><span class="sxs-lookup"><span data-stu-id="edb51-201">hello reports available are:</span></span>

- <span data-ttu-id="edb51-202">Informe de grupo de actividad: proporciona información detallada sobre los atacantes, sus objetivos y las tácticas que emplean.</span><span class="sxs-lookup"><span data-stu-id="edb51-202">Activity Group Report: provides deep dives into attackers, their objectives and tactics.</span></span>

- <span data-ttu-id="edb51-203">Informe de campaña: se centra en los detalles de campañas de ataque específicas.</span><span class="sxs-lookup"><span data-stu-id="edb51-203">Campaign Report: focuses on details of specific attack campaigns.</span></span>

- <span data-ttu-id="edb51-204">Informe de resumen de amenaza: cubre todos los elementos de informes de dos anteriores Hola.</span><span class="sxs-lookup"><span data-stu-id="edb51-204">Threat Summary Report: covers all items in hello previous two reports.</span></span>

<span data-ttu-id="edb51-205">Este tipo de información es muy útil durante el proceso de respuesta a incidentes de hello, que existe un origen de hello toounderstand de investigación en curso de ataque de hello, Hola motivaciones del atacante, y qué toomitigate toodo este problema en adelante.</span><span class="sxs-lookup"><span data-stu-id="edb51-205">This type of information is very useful during hello incident response process, where there is an ongoing investigation toounderstand hello source of hello attack, hello attacker’s motivations, and what toodo toomitigate this issue moving forward.</span></span>

1. <span data-ttu-id="edb51-206">tooaccess Hola inteligencia sobre amenazas de informes, Hola siguientes:</span><span class="sxs-lookup"><span data-stu-id="edb51-206">tooaccess hello threat intelligence report, do hello following:</span></span>

2. <span data-ttu-id="edb51-207">Seleccione hello **alertas de seguridad** icono Panel de hello ASC.</span><span class="sxs-lookup"><span data-stu-id="edb51-207">Select hello **Security alerts** tile on hello ASC dashboard.</span></span>

3. <span data-ttu-id="edb51-208">Seleccionar alerta de seguridad de hello para el que desea tooobtain obtener más información.</span><span class="sxs-lookup"><span data-stu-id="edb51-208">Select hello security alert for which you want tooobtain more information.</span></span>

4. <span data-ttu-id="edb51-209">Hola **informes** , a continuación, haga clic en informe de inteligencia de amenazas de hello vínculo toohello.</span><span class="sxs-lookup"><span data-stu-id="edb51-209">In hello **Reports** field, click hello link toohello threat intelligence report.</span></span>

5. <span data-ttu-id="edb51-210">Se abrirá el archivo PDF de hello, que puede descargar.</span><span class="sxs-lookup"><span data-stu-id="edb51-210">This will open hello PDF file, which you can download.</span></span>

![](media/protect-personal-data-azure-security-center/security-alerts-suspicious-process.png)

<span data-ttu-id="edb51-211">Para obtener información adicional acerca de hello informe de inteligencia de amenazas ASC, consulte [informe de inteligencia de amenaza del centro de seguridad de Azure.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span><span class="sxs-lookup"><span data-stu-id="edb51-211">For additional information about hello ASC threat intelligence report, see [Azure Security Center Threat Intelligence Report.](https://docs.microsoft.com/azure/security-center/security-center-threat-report)</span></span>

### <a name="assessment"></a><span data-ttu-id="edb51-212">Evaluación</span><span class="sxs-lookup"><span data-stu-id="edb51-212">Assessment</span></span>

<span data-ttu-id="edb51-213">toohelp con pruebas, la evaluación y la evaluación de la postura de seguridad, ASC proporciona para evaluación de vulnerabilidad integrado con Qualys agentes en la nube, como parte de su componente de recomendaciones de la máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="edb51-213">toohelp with testing, assessment and evaluation of your security posture, ASC provides for integrated vulnerability assessment with Qualys cloud agents, as a part of its virtual machine recommendations component.</span></span>

<span data-ttu-id="edb51-214">Hola Qualys agente informes vulnerabilidad datos toohello Qualys plataforma de administración, que, a continuación, envía una vulnerabilidad y datos de supervisión de estado tooASC de nuevo.</span><span class="sxs-lookup"><span data-stu-id="edb51-214">hello Qualys agent reports vulnerability data toohello Qualys management platform, which then sends vulnerability and health monitoring data back tooASC.</span></span> <span data-ttu-id="edb51-215">Hola tooadd recomendación se muestra una solución de evaluación de vulnerabilidad en hello **recomendaciones** hoja en el panel de hello ASC.</span><span class="sxs-lookup"><span data-stu-id="edb51-215">hello recommendation tooadd a vulnerability assessment solution is displayed in hello **Recommendations** blade on hello ASC dashboard.</span></span>

<span data-ttu-id="edb51-216">Después de instala la solución de evaluación de vulnerabilidades de hello en destino Hola VM, exámenes de centro de seguridad Hola VM toodetect e identifican las vulnerabilidades de sistema y de aplicación.</span><span class="sxs-lookup"><span data-stu-id="edb51-216">After hello vulnerability assessment solution is installed on hello target VM, Security Center scans hello VM toodetect and identify system and application vulnerabilities.</span></span> <span data-ttu-id="edb51-217">Detecta problemas se muestran bajo hello **recomendaciones de máquinas virtuales** opción.</span><span class="sxs-lookup"><span data-stu-id="edb51-217">Detected issues are shown under hello **Virtual Machines Recommendations** option.</span></span>

#### <a name="how-do-i-implement-a-vulnerability-assessment-solution"></a><span data-ttu-id="edb51-218">¿Cómo se puede implementar una solución de evaluación de vulnerabilidades?</span><span class="sxs-lookup"><span data-stu-id="edb51-218">How do I implement a vulnerability assessment solution?</span></span> 

<span data-ttu-id="edb51-219">Si una máquina virtual aún no tiene implementada una solución de evaluación de vulnerabilidades integrada, Security Center recomienda su instalación.</span><span class="sxs-lookup"><span data-stu-id="edb51-219">If a Virtual Machine does not have an integrated vulnerability assessment solution already deployed, Security Center recommends that it be installed.</span></span>

1. <span data-ttu-id="edb51-220">En panel ASC hello, en hello **recomendaciones** hoja, seleccione **agregar una solución de evaluación de vulnerabilidad.**</span><span class="sxs-lookup"><span data-stu-id="edb51-220">In hello ASC dashboard, on hello **Recommendations** blade, select **Add a vulnerability assessment solution.**</span></span>

2. <span data-ttu-id="edb51-221">Seleccione las máquinas virtuales de Hola donde desea que la solución de evaluación de vulnerabilidades de hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="edb51-221">Select hello VMs where you want tooinstall hello vulnerability assessment solution.</span></span>

3. <span data-ttu-id="edb51-222">Haga clic en **Instalar en las máquinas virtuales de [número de].**</span><span class="sxs-lookup"><span data-stu-id="edb51-222">Click on **Install on [number of] VMs.**</span></span>

4. <span data-ttu-id="edb51-223">Seleccione una solución de socios de hello Azure Marketplace, o bajo **usar una solución existente,** seleccione **Qualys.**</span><span class="sxs-lookup"><span data-stu-id="edb51-223">Select a partner solution in hello Azure Marketplace, or under **Use existing solution,** select **Qualys.**</span></span>

5. <span data-ttu-id="edb51-224">Puede activar la configuración de actualización automática de Hola o desactivar en hello **soluciones de socios** hoja.</span><span class="sxs-lookup"><span data-stu-id="edb51-224">You can turn hello auto update settings on or off in hello **Partner Solutions** blade.</span></span>

<span data-ttu-id="edb51-225">Para obtener más instrucciones sobre cómo tooimplement una solución de evaluación de vulnerabilidad, consulte [evaluación de vulnerabilidad en el centro de seguridad de Azure.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span><span class="sxs-lookup"><span data-stu-id="edb51-225">For further instructions on how tooimplement a vulnerability assessment solution, see [Vulnerability Assessment in Azure Security Center.](https://docs.microsoft.com/azure/security-center/security-center-vulnerability-assessment-recommendations)</span></span>

## <a name="next-steps"></a><span data-ttu-id="edb51-226">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="edb51-226">Next steps</span></span>

- [<span data-ttu-id="edb51-227">Guía de inicio rápido de Azure Security Center</span><span class="sxs-lookup"><span data-stu-id="edb51-227">Azure Security Center quick start guide</span></span>](https://docs.microsoft.com/azure/security-center/security-center-get-started)

- [<span data-ttu-id="edb51-228">Introducción tooAzure centro de seguridad</span><span class="sxs-lookup"><span data-stu-id="edb51-228">Introduction tooAzure Security Center</span></span>](https://docs.microsoft.com/azure/security-center/security-center-intro)

- [<span data-ttu-id="edb51-229">Integración de las alertas de Azure Security Center con la integración de registro de Azure</span><span class="sxs-lookup"><span data-stu-id="edb51-229">Integrating Azure Security Center alerts with Azure log integration</span></span>](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration)

- <span data-ttu-id="edb51-230">[Boost Azure Security Center with Integrated Vulnerability Assessment](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/) (Potenciación de Azure Security Center con la evaluación de vulnerabilidades integrada)</span><span class="sxs-lookup"><span data-stu-id="edb51-230">[Boost Azure Security Center with Integrated Vulnerability Assessment](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/16/boost-azure-security-center-with-integrated-vulnerability-assessment/)</span></span>
