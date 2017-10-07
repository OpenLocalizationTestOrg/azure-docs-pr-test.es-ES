---
title: aaaOverview de base de datos de Azure para el servicio de base de datos relacional de MySQL | Documentos de Microsoft
description: "Información general de hello base de datos de Azure para el servicio de base de datos relacional de MySQL."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 08/02/2017
ms.custom: mvc
ms.openlocfilehash: f02493e2c3c38ccab408a718f98861600481812d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-database-for-mysql-service-introduction"></a><span data-ttu-id="9caa3-103">¿Qué es Azure Database for MySQL?</span><span class="sxs-lookup"><span data-stu-id="9caa3-103">What is Azure Database for MySQL?</span></span> <span data-ttu-id="9caa3-104">Introducción al servicio</span><span class="sxs-lookup"><span data-stu-id="9caa3-104">Service Introduction</span></span>
<span data-ttu-id="9caa3-105">Base de datos de Azure para MySQL es un servicio de base de datos relacional en hello basado en la nube de Microsoft [MySQL Community Edition](https://www.mysql.com/products/community/) motor de base de datos.</span><span class="sxs-lookup"><span data-stu-id="9caa3-105">Azure Database for MySQL is a relational database service in hello Microsoft cloud based on [MySQL Community Edition](https://www.mysql.com/products/community/) database engine.</span></span>  <span data-ttu-id="9caa3-106">Azure Database for MySQL ofrece lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="9caa3-106">Azure Database for MySQL delivers:</span></span>

- <span data-ttu-id="9caa3-107">Rendimiento predecible en varios niveles de servicio</span><span class="sxs-lookup"><span data-stu-id="9caa3-107">Predictable performance at multiple service levels</span></span>
- <span data-ttu-id="9caa3-108">Escalabilidad dinámica sin tiempo de inactividad de la aplicación</span><span class="sxs-lookup"><span data-stu-id="9caa3-108">Dynamic scalability with no application downtime</span></span>
- <span data-ttu-id="9caa3-109">Alta disponibilidad integrada</span><span class="sxs-lookup"><span data-stu-id="9caa3-109">Built-in high availability</span></span>
- <span data-ttu-id="9caa3-110">Protección de datos</span><span class="sxs-lookup"><span data-stu-id="9caa3-110">Data protection</span></span>

<span data-ttu-id="9caa3-111">Estas funcionalidades no requieren casi ninguna tarea de administración y todas se proporcionan sin ningún costo adicional.</span><span class="sxs-lookup"><span data-stu-id="9caa3-111">These capabilities require almost no administration, and all are provided at no additional cost.</span></span> <span data-ttu-id="9caa3-112">Le permiten toofocus en desarrollo de aplicaciones rápida y acelerar su toomarket de tiempo, en lugar de asignar un tiempo muy valioso y máquinas virtuales de toomanaging de recursos y la infraestructura.</span><span class="sxs-lookup"><span data-stu-id="9caa3-112">They allow you toofocus on rapid app development and accelerating your time toomarket, rather than allocating precious time and resources toomanaging virtual machines and infrastructure.</span></span> <span data-ttu-id="9caa3-113">Además, puede continuar toodevelop la aplicación con hello Abrir origen herramientas y plataforma de su elección y entregar con velocidad de Hola y eficacia que exige su negocio sin tener toolearn nuevas habilidades.</span><span class="sxs-lookup"><span data-stu-id="9caa3-113">In addition, you can continue toodevelop your application with hello open source tools and platform of your choice, and deliver with hello speed and efficiency your business demands without having toolearn new skills.</span></span>

![Diagrama conceptual de Azure Database for MySQL](media/overview/1-azure-db-for-mysql-conceptual-diagram.png)

<span data-ttu-id="9caa3-115">Este artículo es una introducción tooAzure base de datos de conceptos básicos de MySQL y características relacionadas tooperformance, escalabilidad y facilidad de uso, con detalles de tooexplore de vínculos.</span><span class="sxs-lookup"><span data-stu-id="9caa3-115">This article is an introduction tooAzure Database for MySQL core concepts and features related tooperformance, scalability, and manageability, with links tooexplore details.</span></span> <span data-ttu-id="9caa3-116">Consulte que estos rápida inicia tooget inició:</span><span class="sxs-lookup"><span data-stu-id="9caa3-116">See these quick starts tooget you started:</span></span>
- <span data-ttu-id="9caa3-117">[Create an Azure Database for MySQL server using Azure Portal](quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="9caa3-117">[Create an Azure Database for MySQL server using Azure portal](quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="9caa3-118">[Create an Azure Database for MySQL server using Azure CLI](quickstart-create-mysql-server-database-using-azure-cli.md) (Creación de un servidor de Azure Database for MySQL mediante la CLI de Azure)</span><span class="sxs-lookup"><span data-stu-id="9caa3-118">[Create an Azure Database for MySQL server using Azure CLI](quickstart-create-mysql-server-database-using-azure-cli.md)</span></span>

<span data-ttu-id="9caa3-119">Para ver ejemplos de la CLI de Azure, consulte:</span><span class="sxs-lookup"><span data-stu-id="9caa3-119">For a set of Azure CLI samples, see:</span></span>
- [<span data-ttu-id="9caa3-120">Ejemplos de la CLI de Azure para Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="9caa3-120">Azure CLI samples for Azure Database for MySQL</span></span>](sample-scripts-azure-cli.md)

## <a name="adjust-performance-and-scale-without-downtime"></a><span data-ttu-id="9caa3-121">Ajuste del rendimiento y escalabilidad sin tiempo de inactividad</span><span class="sxs-lookup"><span data-stu-id="9caa3-121">Adjust performance and scale without downtime</span></span>
<span data-ttu-id="9caa3-122">El servicio Azure Database for MySQL actualmente ofrece dos niveles de servicio: Básico y Estándar.</span><span class="sxs-lookup"><span data-stu-id="9caa3-122">Azure Database for MySQL service offers two service tiers: Basic and Standard.</span></span> <span data-ttu-id="9caa3-123">Cada nivel ofrece rendimiento diferentes y las cargas de trabajo de base de datos de las capacidades toosupport tooheavyweight ligera.</span><span class="sxs-lookup"><span data-stu-id="9caa3-123">Each tier offers different performance and capabilities toosupport lightweight tooheavyweight database workloads.</span></span> <span data-ttu-id="9caa3-124">Puede compilar su primera aplicación en una base de datos pequeño para unos cuantos dólares de un mes, a continuación, cambiar su tooscale de nivel de servicio con necesidades de la solución sin tiempo de inactividad.</span><span class="sxs-lookup"><span data-stu-id="9caa3-124">You can build your first app on a small database for a few dollars a month, then change your service tier tooscale with needs of your solution with no downtime.</span></span> <span data-ttu-id="9caa3-125">Escalabilidad dinámica permite su toorapidly de base de datos tootransparently responden cambiantes requerimientos de recursos.</span><span class="sxs-lookup"><span data-stu-id="9caa3-125">Dynamic scalability enables your database tootransparently respond toorapidly changing resource requirements.</span></span> <span data-ttu-id="9caa3-126">Solo paga por recursos de Hola que necesita, cuando los necesite.</span><span class="sxs-lookup"><span data-stu-id="9caa3-126">You only pay for hello resources you need, when you need them.</span></span>

## <a name="monitoring-and-alerting"></a><span data-ttu-id="9caa3-127">Supervisión y alertas</span><span class="sxs-lookup"><span data-stu-id="9caa3-127">Monitoring and alerting</span></span>
<span data-ttu-id="9caa3-128">¿Cómo sabrá Hola integral haga clic cuando marque arriba y abajo?</span><span class="sxs-lookup"><span data-stu-id="9caa3-128">How do you know hello right click-stop when you dial up and down?</span></span> <span data-ttu-id="9caa3-129">Usar la supervisión de rendimiento integrado de Hola y características, combinadas con una clasificación de rendimiento Hola basada en unidad de proceso de alertas.</span><span class="sxs-lookup"><span data-stu-id="9caa3-129">Use hello built-in performance monitoring and alerting features, combined with hello performance ratings based on Compute Unit.</span></span> <span data-ttu-id="9caa3-130">Uso de estas características, puede evaluar rápidamente impacto Hola de escalar verticalmente en función de su suscripción actual o se proyecta necesidades de rendimiento.</span><span class="sxs-lookup"><span data-stu-id="9caa3-130">Using these features, you can quickly assess hello impact of scaling up or down based on your current or project performance needs.</span></span> <span data-ttu-id="9caa3-131">Consulte [Conceptos: niveles de servicio](concepts-service-tiers.md) para más información.</span><span class="sxs-lookup"><span data-stu-id="9caa3-131">See [Concepts: Service tiers](concepts-service-tiers.md) for details.</span></span>

## <a name="keep-your-app-and-business-running"></a><span data-ttu-id="9caa3-132">Mantenimiento de la aplicación y el negocio en funcionamiento</span><span class="sxs-lookup"><span data-stu-id="9caa3-132">Keep your app and business running</span></span>
<span data-ttu-id="9caa3-133">El Acuerdo de Nivel de Servicio (SLA) de Azure, con una disponibilidad del 99,99 % líder del sector y con la tecnología de una red global de centros de datos administrados por Microsoft, ayuda a mantener las aplicaciones en funcionamiento de forma ininterrumpida.</span><span class="sxs-lookup"><span data-stu-id="9caa3-133">Azure's industry leading 99.99% availability service level agreement (SLA), powered by a global network of Microsoft-managed datacenters, helps keep your app running 24/7.</span></span> <span data-ttu-id="9caa3-134">Con cada base de datos de MySQL server, aprovechar las ventajas de seguridad integrados, tolerancia a errores y protección de datos que, en caso contrario tendría toobuy o diseño, crear y administrar.</span><span class="sxs-lookup"><span data-stu-id="9caa3-134">With every Azure Database for MySQL server, you take advantage of built-in security, fault tolerance, and data protection that you would otherwise have toobuy or design, build, and manage.</span></span> <span data-ttu-id="9caa3-135">Con la base de datos de Azure para MySQL, puede utilizar restauración a un punto en el momento toorecover tooan de un servidor de estado anteriormente, anteriores hasta 35 días.</span><span class="sxs-lookup"><span data-stu-id="9caa3-135">With Azure Database for MySQL, you can use point-in-time restore toorecover a server tooan earlier state, as far back as 35 days.</span></span>

## <a name="secure-your-data"></a><span data-ttu-id="9caa3-136">Protección de los datos</span><span class="sxs-lookup"><span data-stu-id="9caa3-136">Secure your data</span></span>
<span data-ttu-id="9caa3-137">Los servicios de bases de datos de Azure tienen una tradición de seguridad de datos que conserva Azure Database for MySQL con características que limitan el acceso, protegen los datos en reposo y en movimiento, y le ayudan a supervisar la actividad.</span><span class="sxs-lookup"><span data-stu-id="9caa3-137">Azure database services have a tradition of data security that Azure Database for MySQL upholds with features that limit access, protect data at-rest and in-motion, and help you monitor activity.</span></span> <span data-ttu-id="9caa3-138">Visite hello [centro de confianza de Azure](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx) para obtener información acerca de la seguridad de plataforma de Azure.</span><span class="sxs-lookup"><span data-stu-id="9caa3-138">Visit hello [Azure Trust Center](https://www.microsoft.com/en-us/TrustCenter/Security/default.aspx) for information about Azure's platform security.</span></span>

<span data-ttu-id="9caa3-139">Hola base de datos de Azure para servicio de MySQL usa cifrado de almacenamiento de datos en reposo.</span><span class="sxs-lookup"><span data-stu-id="9caa3-139">hello Azure Database for MySQL service uses storage encryption for data at-rest.</span></span> <span data-ttu-id="9caa3-140">Datos incluidos en las copias de seguridad, se cifran en el disco (con excepción de Hola de archivos temporales creados por el motor de Hola durante la ejecución de consultas).</span><span class="sxs-lookup"><span data-stu-id="9caa3-140">Data including backups, are encrypted on disk (with hello exception of temporary files created by hello engine while running queries).</span></span> <span data-ttu-id="9caa3-141">servicio Hello usa cifrado de AES de 256 bits que se incluye en el cifrado de almacenamiento de Azure y las claves de hello están administrado por el sistema.</span><span class="sxs-lookup"><span data-stu-id="9caa3-141">hello service uses AES 256-bit cipher that is included in Azure storage encryption, and hello keys are system managed.</span></span> <span data-ttu-id="9caa3-142">El cifrado de almacenamiento siempre está activado y no se puede deshabilitar.</span><span class="sxs-lookup"><span data-stu-id="9caa3-142">Storage encryption is always on and cannot be disabled.</span></span>

<span data-ttu-id="9caa3-143">De forma predeterminada, Hola base de datos de Azure para servicio de MySQL es configurado toorequire [seguridad de la conexión SSL](./concepts-ssl-connection-security.md) para datos en movimiento a través de red de Hola.</span><span class="sxs-lookup"><span data-stu-id="9caa3-143">By default, hello Azure Database for MySQL service is configured toorequire [SSL connection security](./concepts-ssl-connection-security.md) for data in-motion across hello network.</span></span> <span data-ttu-id="9caa3-144">Aplicar las conexiones SSL entre el servidor de base de datos y las aplicaciones cliente ayuda a protege contra los ataques de "tipo man in intermedio Hola" mediante el cifrado de flujo de datos de hello entre servidor hello y la aplicación.</span><span class="sxs-lookup"><span data-stu-id="9caa3-144">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>  <span data-ttu-id="9caa3-145">Si lo desea, puede deshabilitar requerir SSL para la conexión de servicio de base de datos de tooyour si la aplicación cliente no es compatible con la conectividad SSL.</span><span class="sxs-lookup"><span data-stu-id="9caa3-145">Optionally, you can disable requiring SSL for connecting tooyour database service if your client application does not support SSL connectivity.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9caa3-146">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="9caa3-146">Next Steps</span></span>
<span data-ttu-id="9caa3-147">Ahora que ha leer una base de datos de tooAzure de introducción para MySQL y respondía a Hola pregunta "¿Cuál es la base de datos de Azure para MySQL?", está listo para:</span><span class="sxs-lookup"><span data-stu-id="9caa3-147">Now that you've read an introduction tooAzure Database for MySQL and answered hello question "What is Azure Database for MySQL?", you're ready to:</span></span>
- <span data-ttu-id="9caa3-148">Vea Hola página para las comparaciones de costo y calculadoras de precios.</span><span class="sxs-lookup"><span data-stu-id="9caa3-148">See hello pricing page for cost comparisons and calculators.</span></span> [<span data-ttu-id="9caa3-149">Precios</span><span class="sxs-lookup"><span data-stu-id="9caa3-149">Pricing</span></span>](https://azure.microsoft.com/pricing/details/mysql/)
- <span data-ttu-id="9caa3-150">Comience por crear su primer servidor.</span><span class="sxs-lookup"><span data-stu-id="9caa3-150">Get started by creating your first server.</span></span> <span data-ttu-id="9caa3-151">[Create an Azure Database for MySQL server using Azure Portal](quickstart-create-mysql-server-database-using-azure-portal.md) (Creación de un servidor de Azure Database for MySQL mediante Azure Portal)</span><span class="sxs-lookup"><span data-stu-id="9caa3-151">[Create an Azure Database for MySQL server using Azure portal](quickstart-create-mysql-server-database-using-azure-portal.md)</span></span>
- <span data-ttu-id="9caa3-152">Compilar la primera aplicación de Python, PHP, Ruby, C\#, Java, Node.js: [bibliotecas de conectividad usan tooconnect tooAzure base de datos de MySQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="9caa3-152">Build your first app in Python, PHP, Ruby, C\#, Java, Node.js: [Connectivity libraries used tooconnect tooAzure Database for MySQL](concepts-connection-libraries.md)</span></span>