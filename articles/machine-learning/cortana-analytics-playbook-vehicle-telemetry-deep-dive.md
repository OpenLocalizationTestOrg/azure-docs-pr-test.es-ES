---
title: "aaaDeep profundizar en mantenimiento de vehículo de predecir y dirigir hábitos - Azure | Documentos de Microsoft"
description: "Usar funciones de Hola de toogain en tiempo real y predicción visión de inteligencia de Cortana en el estado del vehículo y dirigir hábitos."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: d8866fa6-aba6-40e5-b3b3-33057393c1a8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: ba1448a5081762292561f904d9ec54617c9a5330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-hello-solution"></a><span data-ttu-id="a9342-103">Guía de solución de análisis de telemetría de vehículo: profundización en soluciones de Hola</span><span class="sxs-lookup"><span data-stu-id="a9342-103">Vehicle telemetry analytics solution playbook: deep dive into hello solution</span></span>
<span data-ttu-id="a9342-104">Esto **menú** vincula toohello secciones de esta guía:</span><span class="sxs-lookup"><span data-stu-id="a9342-104">This **menu** links toohello sections of this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="a9342-105">Esta sección detalla en cada una de las fases de hello representados en hello arquitectura de la solución con instrucciones y punteros para la personalización.</span><span class="sxs-lookup"><span data-stu-id="a9342-105">This section drills down into each of hello stages depicted in hello Solution Architecture with instructions and pointers for customization.</span></span> 

## <a name="data-sources"></a><span data-ttu-id="a9342-106">Orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="a9342-106">Data Sources</span></span>
<span data-ttu-id="a9342-107">solución de Hello utiliza dos orígenes de datos diferentes:</span><span class="sxs-lookup"><span data-stu-id="a9342-107">hello solution uses two different data sources:</span></span>

* <span data-ttu-id="a9342-108">**conjunto de datos de señales de vehículo y diagnósticos simulados** y</span><span class="sxs-lookup"><span data-stu-id="a9342-108">**simulated vehicle signals and diagnostic dataset** and</span></span> 
* <span data-ttu-id="a9342-109">**catálogo de vehículo**</span><span class="sxs-lookup"><span data-stu-id="a9342-109">**vehicle catalog**</span></span>

<span data-ttu-id="a9342-110">Se incluye un simulador telemático del vehículo como parte de esta solución.</span><span class="sxs-lookup"><span data-stu-id="a9342-110">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="a9342-111">Se emite información de diagnóstico y se indica el estado de toohello correspondiente del vehículo hello y toohello automóvil patrón en un momento dado en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="a9342-111">It emits diagnostic information and signals corresponding toohello state of hello vehicle and toohello driving pattern at a given point in time.</span></span> <span data-ttu-id="a9342-112">Haga clic en [vehículo telemáticas simulador](http://go.microsoft.com/fwlink/?LinkId=717075) hello toodownload **solución de Visual Studio de vehículo telemáticas simulador** para las personalizaciones en función de sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="a9342-112">Click [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) toodownload hello **Vehicle Telematics Simulator Visual Studio Solution** for customizations based on your requirements.</span></span> <span data-ttu-id="a9342-113">catálogo de vehículo Hello contiene un conjunto de datos de referencia con una asignación de toomodel Niv.</span><span class="sxs-lookup"><span data-stu-id="a9342-113">hello vehicle catalog contains a reference dataset with a VIN toomodel mapping.</span></span>

![Simulador telemático de vehículo](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

<span data-ttu-id="a9342-115">*Ilustración 1: Simulador telemático de vehículo*</span><span class="sxs-lookup"><span data-stu-id="a9342-115">*Figure 1 – Vehicle Telematics Simulator*</span></span>

<span data-ttu-id="a9342-116">Se trata de un conjunto de datos con formato JSON que contiene Hola después de esquema.</span><span class="sxs-lookup"><span data-stu-id="a9342-116">This is a JSON-formatted dataset that contains hello following schema.</span></span>

| <span data-ttu-id="a9342-117">Columna</span><span class="sxs-lookup"><span data-stu-id="a9342-117">Column</span></span> | <span data-ttu-id="a9342-118">Description</span><span class="sxs-lookup"><span data-stu-id="a9342-118">Description</span></span> | <span data-ttu-id="a9342-119">Valores</span><span class="sxs-lookup"><span data-stu-id="a9342-119">Values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a9342-120">VIN</span><span class="sxs-lookup"><span data-stu-id="a9342-120">VIN</span></span> |<span data-ttu-id="a9342-121">Número de identificación del vehículo generado de forma aleatoria</span><span class="sxs-lookup"><span data-stu-id="a9342-121">Randomly generated Vehicle Identification Number</span></span> |<span data-ttu-id="a9342-122">Se obtiene a partir de una lista maestra de 10.000 números de identificación de vehículo generados de forma aleatoria.</span><span class="sxs-lookup"><span data-stu-id="a9342-122">This is obtained from a master list of 10,000 randomly generated vehicle identification numbers.</span></span> |
| <span data-ttu-id="a9342-123">Outside temperature</span><span class="sxs-lookup"><span data-stu-id="a9342-123">Outside temperature</span></span> |<span data-ttu-id="a9342-124">Hola fuera temperatura donde está impulsando vehículo Hola</span><span class="sxs-lookup"><span data-stu-id="a9342-124">hello outside temperature where hello vehicle is driving</span></span> |<span data-ttu-id="a9342-125">Número generado al azar de 0 a 100</span><span class="sxs-lookup"><span data-stu-id="a9342-125">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="a9342-126">Engine temperature</span><span class="sxs-lookup"><span data-stu-id="a9342-126">Engine temperature</span></span> |<span data-ttu-id="a9342-127">temperatura del motor Hola de vehículo Hola</span><span class="sxs-lookup"><span data-stu-id="a9342-127">hello engine temperature of hello vehicle</span></span> |<span data-ttu-id="a9342-128">Número generado al azar de 0 a 500</span><span class="sxs-lookup"><span data-stu-id="a9342-128">Randomly generated number from 0-500</span></span> |
| <span data-ttu-id="a9342-129">Velocidad</span><span class="sxs-lookup"><span data-stu-id="a9342-129">Speed</span></span> |<span data-ttu-id="a9342-130">velocidad de motor de Hello en qué Hola está impulsando vehículo</span><span class="sxs-lookup"><span data-stu-id="a9342-130">hello engine speed at which hello vehicle is driving</span></span> |<span data-ttu-id="a9342-131">Número generado al azar de 0 a 100</span><span class="sxs-lookup"><span data-stu-id="a9342-131">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="a9342-132">Fuel</span><span class="sxs-lookup"><span data-stu-id="a9342-132">Fuel</span></span> |<span data-ttu-id="a9342-133">nivel de combustible Hola de vehículo Hola</span><span class="sxs-lookup"><span data-stu-id="a9342-133">hello fuel level of hello vehicle</span></span> |<span data-ttu-id="a9342-134">Número generado al azar de 0 a 100 (indica el porcentaje del nivel de combustible)</span><span class="sxs-lookup"><span data-stu-id="a9342-134">Randomly generated number from 0-100 (indicates fuel level percentage)</span></span> |
| <span data-ttu-id="a9342-135">EngineOil</span><span class="sxs-lookup"><span data-stu-id="a9342-135">EngineOil</span></span> |<span data-ttu-id="a9342-136">nivel de petróleo de motor de Hola de vehículo Hola</span><span class="sxs-lookup"><span data-stu-id="a9342-136">hello engine oil level of hello vehicle</span></span> |<span data-ttu-id="a9342-137">Número generado al azar de 0 a 100 (indica el porcentaje del nivel de aceite del motor)</span><span class="sxs-lookup"><span data-stu-id="a9342-137">Randomly generated number from 0-100 (indicates engine oil level percentage)</span></span> |
| <span data-ttu-id="a9342-138">Presión de los neumáticos</span><span class="sxs-lookup"><span data-stu-id="a9342-138">Tire pressure</span></span> |<span data-ttu-id="a9342-139">presión del neumático Hola de vehículo Hola</span><span class="sxs-lookup"><span data-stu-id="a9342-139">hello tire pressure of hello vehicle</span></span> |<span data-ttu-id="a9342-140">Número generado al azar de 0 a 50 (indica el porcentaje del nivel de presión de los neumáticos)</span><span class="sxs-lookup"><span data-stu-id="a9342-140">Randomly generated number from 0-50 (indicates tire pressure level percentage)</span></span> |
| <span data-ttu-id="a9342-141">Odometer</span><span class="sxs-lookup"><span data-stu-id="a9342-141">Odometer</span></span> |<span data-ttu-id="a9342-142">cuentakilómetros Hola de vehículo Hola</span><span class="sxs-lookup"><span data-stu-id="a9342-142">hello odometer reading of hello vehicle</span></span> |<span data-ttu-id="a9342-143">Número generado al azar de 0 a 200000</span><span class="sxs-lookup"><span data-stu-id="a9342-143">Randomly generated number from 0-200000</span></span> |
| <span data-ttu-id="a9342-144">Accelerator_pedal_position</span><span class="sxs-lookup"><span data-stu-id="a9342-144">Accelerator_pedal_position</span></span> |<span data-ttu-id="a9342-145">posición pedales Hola del Acelerador de vehículo Hola</span><span class="sxs-lookup"><span data-stu-id="a9342-145">hello accelerator pedal position of hello vehicle</span></span> |<span data-ttu-id="a9342-146">Número generado al azar de 0 a 100 (indica el porcentaje del nivel del acelerador)</span><span class="sxs-lookup"><span data-stu-id="a9342-146">Randomly generated number from 0-100 (indicates accelerator level percentage)</span></span> |
| <span data-ttu-id="a9342-147">Parking_brake_status</span><span class="sxs-lookup"><span data-stu-id="a9342-147">Parking_brake_status</span></span> |<span data-ttu-id="a9342-148">Indica si está aparcado vehículo de Hola o no</span><span class="sxs-lookup"><span data-stu-id="a9342-148">Indicates whether hello vehicle is parked or not</span></span> |<span data-ttu-id="a9342-149">Verdadero o falso</span><span class="sxs-lookup"><span data-stu-id="a9342-149">True or False</span></span> |
| <span data-ttu-id="a9342-150">Headlamp_status</span><span class="sxs-lookup"><span data-stu-id="a9342-150">Headlamp_status</span></span> |<span data-ttu-id="a9342-151">Indica la ubicación proyector hello en o no</span><span class="sxs-lookup"><span data-stu-id="a9342-151">Indicates where hello headlamp is on or not</span></span> |<span data-ttu-id="a9342-152">Verdadero o falso</span><span class="sxs-lookup"><span data-stu-id="a9342-152">True or False</span></span> |
| <span data-ttu-id="a9342-153">Brake_pedal_status</span><span class="sxs-lookup"><span data-stu-id="a9342-153">Brake_pedal_status</span></span> |<span data-ttu-id="a9342-154">Indica si se presionó pedal frenos de Hola o no</span><span class="sxs-lookup"><span data-stu-id="a9342-154">Indicates whether hello brake pedal is pressed or not</span></span> |<span data-ttu-id="a9342-155">Verdadero o falso</span><span class="sxs-lookup"><span data-stu-id="a9342-155">True or False</span></span> |
| <span data-ttu-id="a9342-156">Transmission_gear_position</span><span class="sxs-lookup"><span data-stu-id="a9342-156">Transmission_gear_position</span></span> |<span data-ttu-id="a9342-157">posición de engranaje de transmisión de Hello del vehículo Hola</span><span class="sxs-lookup"><span data-stu-id="a9342-157">hello transmission gear position of hello vehicle</span></span> |<span data-ttu-id="a9342-158">Estados: primera, segunda, tercera y cuarta, quinta, sexta, séptima, octava</span><span class="sxs-lookup"><span data-stu-id="a9342-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span></span> |
| <span data-ttu-id="a9342-159">Ignition_status</span><span class="sxs-lookup"><span data-stu-id="a9342-159">Ignition_status</span></span> |<span data-ttu-id="a9342-160">Indica si el vehículo de hello está en ejecución o detenido</span><span class="sxs-lookup"><span data-stu-id="a9342-160">Indicates whether hello vehicle is running or stopped</span></span> |<span data-ttu-id="a9342-161">Verdadero o falso</span><span class="sxs-lookup"><span data-stu-id="a9342-161">True or False</span></span> |
| <span data-ttu-id="a9342-162">Windshield_wiper_status</span><span class="sxs-lookup"><span data-stu-id="a9342-162">Windshield_wiper_status</span></span> |<span data-ttu-id="a9342-163">Indica si está activada limpiaparabrisas Hola o no</span><span class="sxs-lookup"><span data-stu-id="a9342-163">Indicates whether hello windshield wiper is turned or not</span></span> |<span data-ttu-id="a9342-164">Verdadero o falso</span><span class="sxs-lookup"><span data-stu-id="a9342-164">True or False</span></span> |
| <span data-ttu-id="a9342-165">ABS</span><span class="sxs-lookup"><span data-stu-id="a9342-165">ABS</span></span> |<span data-ttu-id="a9342-166">Indica si el ABS está activado o no</span><span class="sxs-lookup"><span data-stu-id="a9342-166">Indicates whether ABS is engaged or not</span></span> |<span data-ttu-id="a9342-167">Verdadero o falso</span><span class="sxs-lookup"><span data-stu-id="a9342-167">True or False</span></span> |
| <span data-ttu-id="a9342-168">Timestamp</span><span class="sxs-lookup"><span data-stu-id="a9342-168">Timestamp</span></span> |<span data-ttu-id="a9342-169">Hola de marca de tiempo cuando se crea el punto de datos de Hola</span><span class="sxs-lookup"><span data-stu-id="a9342-169">hello timestamp when hello data point is created</span></span> |<span data-ttu-id="a9342-170">Date</span><span class="sxs-lookup"><span data-stu-id="a9342-170">Date</span></span> |
| <span data-ttu-id="a9342-171">City</span><span class="sxs-lookup"><span data-stu-id="a9342-171">City</span></span> |<span data-ttu-id="a9342-172">ubicación de Hola de vehículo Hola</span><span class="sxs-lookup"><span data-stu-id="a9342-172">hello location of hello vehicle</span></span> |<span data-ttu-id="a9342-173">En esta solución tiene la opción de 4 ciudades: Bellevue, Redmond, Sammamish, Seattle</span><span class="sxs-lookup"><span data-stu-id="a9342-173">4 cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span></span> |

<span data-ttu-id="a9342-174">conjunto de datos de referencia de modelo de Hello vehículo contiene la asignación de modelo de toohello de bastidor.</span><span class="sxs-lookup"><span data-stu-id="a9342-174">hello vehicle model reference dataset contains VIN toohello model mapping.</span></span> 

| <span data-ttu-id="a9342-175">VIN</span><span class="sxs-lookup"><span data-stu-id="a9342-175">VIN</span></span> | <span data-ttu-id="a9342-176">Modelo</span><span class="sxs-lookup"><span data-stu-id="a9342-176">Model</span></span> |
| --- | --- |
| <span data-ttu-id="a9342-177">FHL3O1SA4IEHB4WU1</span><span class="sxs-lookup"><span data-stu-id="a9342-177">FHL3O1SA4IEHB4WU1</span></span> |<span data-ttu-id="a9342-178">Sedán</span><span class="sxs-lookup"><span data-stu-id="a9342-178">Sedan</span></span> |
| <span data-ttu-id="a9342-179">8J0U8XCPRGW4Z3NQE</span><span class="sxs-lookup"><span data-stu-id="a9342-179">8J0U8XCPRGW4Z3NQE</span></span> |<span data-ttu-id="a9342-180">Híbrido</span><span class="sxs-lookup"><span data-stu-id="a9342-180">Hybrid</span></span> |
| <span data-ttu-id="a9342-181">WORG68Z2PLTNZDBI7</span><span class="sxs-lookup"><span data-stu-id="a9342-181">WORG68Z2PLTNZDBI7</span></span> |<span data-ttu-id="a9342-182">Berlina familiar</span><span class="sxs-lookup"><span data-stu-id="a9342-182">Family Saloon</span></span> |
| <span data-ttu-id="a9342-183">JTHMYHQTEPP4WBMRN</span><span class="sxs-lookup"><span data-stu-id="a9342-183">JTHMYHQTEPP4WBMRN</span></span> |<span data-ttu-id="a9342-184">Sedán</span><span class="sxs-lookup"><span data-stu-id="a9342-184">Sedan</span></span> |
| <span data-ttu-id="a9342-185">W9FTHG27LZN1YWO0Y</span><span class="sxs-lookup"><span data-stu-id="a9342-185">W9FTHG27LZN1YWO0Y</span></span> |<span data-ttu-id="a9342-186">Híbrido</span><span class="sxs-lookup"><span data-stu-id="a9342-186">Hybrid</span></span> |
| <span data-ttu-id="a9342-187">MHTP9N792PHK08WJM</span><span class="sxs-lookup"><span data-stu-id="a9342-187">MHTP9N792PHK08WJM</span></span> |<span data-ttu-id="a9342-188">Berlina familiar</span><span class="sxs-lookup"><span data-stu-id="a9342-188">Family Saloon</span></span> |
| <span data-ttu-id="a9342-189">EI4QXI2AXVQQING4I</span><span class="sxs-lookup"><span data-stu-id="a9342-189">EI4QXI2AXVQQING4I</span></span> |<span data-ttu-id="a9342-190">Sedán</span><span class="sxs-lookup"><span data-stu-id="a9342-190">Sedan</span></span> |
| <span data-ttu-id="a9342-191">5KKR2VB4WHQH97PF8</span><span class="sxs-lookup"><span data-stu-id="a9342-191">5KKR2VB4WHQH97PF8</span></span> |<span data-ttu-id="a9342-192">Híbrido</span><span class="sxs-lookup"><span data-stu-id="a9342-192">Hybrid</span></span> |
| <span data-ttu-id="a9342-193">W9NSZ423XZHAONYXB</span><span class="sxs-lookup"><span data-stu-id="a9342-193">W9NSZ423XZHAONYXB</span></span> |<span data-ttu-id="a9342-194">Berlina familiar</span><span class="sxs-lookup"><span data-stu-id="a9342-194">Family Saloon</span></span> |
| <span data-ttu-id="a9342-195">26WJSGHX4MA5ROHNL</span><span class="sxs-lookup"><span data-stu-id="a9342-195">26WJSGHX4MA5ROHNL</span></span> |<span data-ttu-id="a9342-196">Descapotable</span><span class="sxs-lookup"><span data-stu-id="a9342-196">Convertible</span></span> |
| <span data-ttu-id="a9342-197">GHLUB6ONKMOSI7E77</span><span class="sxs-lookup"><span data-stu-id="a9342-197">GHLUB6ONKMOSI7E77</span></span> |<span data-ttu-id="a9342-198">Familiar</span><span class="sxs-lookup"><span data-stu-id="a9342-198">Station Wagon</span></span> |
| <span data-ttu-id="a9342-199">9C2RHVRVLMEJDBXLP</span><span class="sxs-lookup"><span data-stu-id="a9342-199">9C2RHVRVLMEJDBXLP</span></span> |<span data-ttu-id="a9342-200">Compacto</span><span class="sxs-lookup"><span data-stu-id="a9342-200">Compact Car</span></span> |
| <span data-ttu-id="a9342-201">BRNHVMZOUJ6EOCP32</span><span class="sxs-lookup"><span data-stu-id="a9342-201">BRNHVMZOUJ6EOCP32</span></span> |<span data-ttu-id="a9342-202">SUV pequeño</span><span class="sxs-lookup"><span data-stu-id="a9342-202">Small SUV</span></span> |
| <span data-ttu-id="a9342-203">VCYVW0WUZNBTM594J</span><span class="sxs-lookup"><span data-stu-id="a9342-203">VCYVW0WUZNBTM594J</span></span> |<span data-ttu-id="a9342-204">Deportivo</span><span class="sxs-lookup"><span data-stu-id="a9342-204">Sports Car</span></span> |
| <span data-ttu-id="a9342-205">HNVCE6YFZSA5M82NY</span><span class="sxs-lookup"><span data-stu-id="a9342-205">HNVCE6YFZSA5M82NY</span></span> |<span data-ttu-id="a9342-206">SUV mediano</span><span class="sxs-lookup"><span data-stu-id="a9342-206">Medium SUV</span></span> |
| <span data-ttu-id="a9342-207">4R30FOR7NUOBL05GJ</span><span class="sxs-lookup"><span data-stu-id="a9342-207">4R30FOR7NUOBL05GJ</span></span> |<span data-ttu-id="a9342-208">Familiar</span><span class="sxs-lookup"><span data-stu-id="a9342-208">Station Wagon</span></span> |
| <span data-ttu-id="a9342-209">WYNIIY42VKV6OQS1J</span><span class="sxs-lookup"><span data-stu-id="a9342-209">WYNIIY42VKV6OQS1J</span></span> |<span data-ttu-id="a9342-210">SUV grande</span><span class="sxs-lookup"><span data-stu-id="a9342-210">Large SUV</span></span> |
| <span data-ttu-id="a9342-211">8Y5QKG27QET1RBK7I</span><span class="sxs-lookup"><span data-stu-id="a9342-211">8Y5QKG27QET1RBK7I</span></span> |<span data-ttu-id="a9342-212">SUV grande</span><span class="sxs-lookup"><span data-stu-id="a9342-212">Large SUV</span></span> |
| <span data-ttu-id="a9342-213">DF6OX2WSRA6511BVG</span><span class="sxs-lookup"><span data-stu-id="a9342-213">DF6OX2WSRA6511BVG</span></span> |<span data-ttu-id="a9342-214">Cupé</span><span class="sxs-lookup"><span data-stu-id="a9342-214">Coupe</span></span> |
| <span data-ttu-id="a9342-215">Z2EOZWZBXAEW3E60T</span><span class="sxs-lookup"><span data-stu-id="a9342-215">Z2EOZWZBXAEW3E60T</span></span> |<span data-ttu-id="a9342-216">Sedán</span><span class="sxs-lookup"><span data-stu-id="a9342-216">Sedan</span></span> |
| <span data-ttu-id="a9342-217">M4TV6IEALD5QDS3IR</span><span class="sxs-lookup"><span data-stu-id="a9342-217">M4TV6IEALD5QDS3IR</span></span> |<span data-ttu-id="a9342-218">Híbrido</span><span class="sxs-lookup"><span data-stu-id="a9342-218">Hybrid</span></span> |
| <span data-ttu-id="a9342-219">VHRA1Y2TGTA84F00H</span><span class="sxs-lookup"><span data-stu-id="a9342-219">VHRA1Y2TGTA84F00H</span></span> |<span data-ttu-id="a9342-220">Berlina familiar</span><span class="sxs-lookup"><span data-stu-id="a9342-220">Family Saloon</span></span> |
| <span data-ttu-id="a9342-221">R0JAUHT1L1R3BIKI0</span><span class="sxs-lookup"><span data-stu-id="a9342-221">R0JAUHT1L1R3BIKI0</span></span> |<span data-ttu-id="a9342-222">Sedán</span><span class="sxs-lookup"><span data-stu-id="a9342-222">Sedan</span></span> |
| <span data-ttu-id="a9342-223">9230C202Z60XX84AU</span><span class="sxs-lookup"><span data-stu-id="a9342-223">9230C202Z60XX84AU</span></span> |<span data-ttu-id="a9342-224">Híbrido</span><span class="sxs-lookup"><span data-stu-id="a9342-224">Hybrid</span></span> |
| <span data-ttu-id="a9342-225">T8DNDN5UDCWL7M72H</span><span class="sxs-lookup"><span data-stu-id="a9342-225">T8DNDN5UDCWL7M72H</span></span> |<span data-ttu-id="a9342-226">Berlina familiar</span><span class="sxs-lookup"><span data-stu-id="a9342-226">Family Saloon</span></span> |
| <span data-ttu-id="a9342-227">4WPYRUZII5YV7YA42</span><span class="sxs-lookup"><span data-stu-id="a9342-227">4WPYRUZII5YV7YA42</span></span> |<span data-ttu-id="a9342-228">Sedán</span><span class="sxs-lookup"><span data-stu-id="a9342-228">Sedan</span></span> |
| <span data-ttu-id="a9342-229">D1ZVY26UV2BFGHZNO</span><span class="sxs-lookup"><span data-stu-id="a9342-229">D1ZVY26UV2BFGHZNO</span></span> |<span data-ttu-id="a9342-230">Híbrido</span><span class="sxs-lookup"><span data-stu-id="a9342-230">Hybrid</span></span> |
| <span data-ttu-id="a9342-231">XUF99EW9OIQOMV7Q7</span><span class="sxs-lookup"><span data-stu-id="a9342-231">XUF99EW9OIQOMV7Q7</span></span> |<span data-ttu-id="a9342-232">Berlina familiar</span><span class="sxs-lookup"><span data-stu-id="a9342-232">Family Saloon</span></span> |
| <span data-ttu-id="a9342-233">8OMCL3LGI7XNCC21U</span><span class="sxs-lookup"><span data-stu-id="a9342-233">8OMCL3LGI7XNCC21U</span></span> |<span data-ttu-id="a9342-234">Descapotable</span><span class="sxs-lookup"><span data-stu-id="a9342-234">Convertible</span></span> |
| <span data-ttu-id="a9342-235">…….</span><span class="sxs-lookup"><span data-stu-id="a9342-235">…….</span></span> | |

### <a name="references"></a><span data-ttu-id="a9342-236">Referencias</span><span class="sxs-lookup"><span data-stu-id="a9342-236">References</span></span>
[<span data-ttu-id="a9342-237">Solución de simulador telemático de vehículo de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a9342-237">Vehicle Telematics Simulator Visual Studio Solution</span></span>](http://go.microsoft.com/fwlink/?LinkId=717075) 

[<span data-ttu-id="a9342-238">Centro de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="a9342-238">Azure Event Hub</span></span>](https://azure.microsoft.com/services/event-hubs/)

[<span data-ttu-id="a9342-239">Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="a9342-239">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a><span data-ttu-id="a9342-240">Ingesta de datos</span><span class="sxs-lookup"><span data-stu-id="a9342-240">Ingestion</span></span>
<span data-ttu-id="a9342-241">Combinaciones de factoría de datos, análisis de transmisiones y centros de eventos de Azure son tooingest aprovechado Hola vehículo señales, eventos de diagnóstico de hello y en tiempo real y análisis por lotes.</span><span class="sxs-lookup"><span data-stu-id="a9342-241">Combinations of Azure Event Hubs, Stream Analytics, and Data Factory are leveraged tooingest hello vehicle signals, hello diagnostic events, and real-time and batch analytics.</span></span> <span data-ttu-id="a9342-242">Todos estos componentes se crean y configuran como parte de la implementación de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9342-242">All these components are created and configured as part of hello solution deployment.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="a9342-243">Análisis en tiempo real</span><span class="sxs-lookup"><span data-stu-id="a9342-243">Real-time analysis</span></span>
<span data-ttu-id="a9342-244">Hello eventos generados por hello vehículo telemáticas simulador se publican toohello concentrador de eventos mediante Hola SDK de concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="a9342-244">hello events generated by hello Vehicle Telematics Simulator are published toohello Event Hub using hello Event Hub SDK.</span></span> <span data-ttu-id="a9342-245">trabajo de análisis de transmisiones de Hello introduce estos eventos desde Hola centro de eventos y procesos Hola datos en estado de tiempo real tooanalyze Hola vehículo.</span><span class="sxs-lookup"><span data-stu-id="a9342-245">hello Stream Analytics job ingests these events from hello Event Hub and processes hello data in real time tooanalyze hello vehicle health.</span></span> 

![Panel del Centro de eventos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

<span data-ttu-id="a9342-247">*Ilustración 4: Panel del Centro de eventos*</span><span class="sxs-lookup"><span data-stu-id="a9342-247">*Figure 4 - Event Hub dashboard*</span></span>

![Procesamiento de datos del trabajo de Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

<span data-ttu-id="a9342-249">*Ilustración 5: Procesamiento de datos del trabajo de Stream Analytics*</span><span class="sxs-lookup"><span data-stu-id="a9342-249">*Figure 5 - Stream Analytics job processing data*</span></span>

<span data-ttu-id="a9342-250">trabajo de análisis de transmisiones de Hello;</span><span class="sxs-lookup"><span data-stu-id="a9342-250">hello Stream Analytics job;</span></span>

* <span data-ttu-id="a9342-251">recopila datos de hello concentrador de eventos</span><span class="sxs-lookup"><span data-stu-id="a9342-251">ingests data from hello Event Hub</span></span> 
* <span data-ttu-id="a9342-252">realiza una combinación con hello referencia toomap Hola vehículo Niv toohello correspondiente modelo de datos</span><span class="sxs-lookup"><span data-stu-id="a9342-252">performs a join with hello reference data toomap hello vehicle VIN toohello corresponding model</span></span> 
* <span data-ttu-id="a9342-253">los conserva en Azure Blob Storage para unos análisis eficaces por lotes.</span><span class="sxs-lookup"><span data-stu-id="a9342-253">persists them into Azure blob storage for rich batch analytics.</span></span> 

<span data-ttu-id="a9342-254">Después de consulta de análisis de transmisiones de Hello es toopersist usado Hola datos en el almacenamiento de blobs de Azure.</span><span class="sxs-lookup"><span data-stu-id="a9342-254">hello following Stream Analytics query is used toopersist hello data into Azure blob storage.</span></span> 

![Consulta de trabajo de Stream Analytics para la ingesta de datos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

<span data-ttu-id="a9342-256">*Ilustración 6: Consulta de trabajo de Stream Analytics para la ingesta de datos*</span><span class="sxs-lookup"><span data-stu-id="a9342-256">*Figure 6 - Stream Analytics job query for data ingestion*</span></span>

### <a name="batch-analysis"></a><span data-ttu-id="a9342-257">Análisis por lotes</span><span class="sxs-lookup"><span data-stu-id="a9342-257">Batch analysis</span></span>
<span data-ttu-id="a9342-258">También se genera un volumen adicional de las señales y el conjunto de datos de diagnóstico del vehículo simulado para un análisis por lotes más completo.</span><span class="sxs-lookup"><span data-stu-id="a9342-258">We are also generating an additional volume of simulated vehicle signals and diagnostic dataset for richer batch analytics.</span></span> <span data-ttu-id="a9342-259">Esto es necesario tooensure un volumen de datos representativo en buen estado para el procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="a9342-259">This is required tooensure a good representative data volume for batch processing.</span></span> <span data-ttu-id="a9342-260">Para ello, usamos una canalización con el nombre "PrepareSampleDataPipeline" en toogenerate de flujo de trabajo de Data Factory de Azure de hello natural un año de las señales de vehículo simulada y conjunto de datos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="a9342-260">For this purpose, we are using a pipeline named "PrepareSampleDataPipeline" in hello Azure Data Factory workflow toogenerate one year's worth of simulated vehicle signals and diagnostic dataset.</span></span> <span data-ttu-id="a9342-261">Haga clic en [actividad personalizada de factoría de datos](http://go.microsoft.com/fwlink/?LinkId=717077) hello toodownload actividad DotNet personalizada solución de Visual Studio para las personalizaciones de factoría de datos según sus requisitos.</span><span class="sxs-lookup"><span data-stu-id="a9342-261">Click [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) toodownload hello Data Factory custom DotNet activity Visual Studio solution for customizations based on your requirements.</span></span> 

![Preparar los datos de muestra para el flujo de trabajo de procesamiento por lotes](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

<span data-ttu-id="a9342-263">*Ilustración 7: Preparar los datos de muestra para el flujo de trabajo de procesamiento por lotes*</span><span class="sxs-lookup"><span data-stu-id="a9342-263">*Figure 7 - Prepare Sample data for batch processing workflow*</span></span>

<span data-ttu-id="a9342-264">canalización de Hello consta de ADF .net personalizado actividad, aparecen aquí:</span><span class="sxs-lookup"><span data-stu-id="a9342-264">hello pipeline consists of a custom ADF .Net Activity, show here:</span></span>

![Actividad PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

<span data-ttu-id="a9342-266">*Ilustración 8: PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="a9342-266">*Figure 8 - PrepareSampleDataPipeline*</span></span>

<span data-ttu-id="a9342-267">Una vez que la canalización de Hola se ejecuta correctamente y el conjunto de datos de "RawCarEventsTable" está marcado como "Listo", un año que vale la pena de señales de vehículo simulado y de diagnóstico se generan datos.</span><span class="sxs-lookup"><span data-stu-id="a9342-267">Once hello pipeline executes successfully and "RawCarEventsTable" dataset is marked "Ready", one-year worth of simulated vehicle signals and diagnostic data are produced.</span></span> <span data-ttu-id="a9342-268">Ve a continuación Hola carpetas y archivos creados en su cuenta de almacenamiento en el contenedor de "connectedcar" hello:</span><span class="sxs-lookup"><span data-stu-id="a9342-268">You see hello following folder and file created in your storage account under hello "connectedcar" container:</span></span>

![Resultados de PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

<span data-ttu-id="a9342-270">*Ilustración 9: Resultados de PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="a9342-270">*Figure 9 - PrepareSampleDataPipeline Output*</span></span>

### <a name="references"></a><span data-ttu-id="a9342-271">Referencias</span><span class="sxs-lookup"><span data-stu-id="a9342-271">References</span></span>
[<span data-ttu-id="a9342-272">SDK del Centro de eventos de Azure para ingesta de transmisiones</span><span class="sxs-lookup"><span data-stu-id="a9342-272">Azure Event Hub SDK for stream ingestion</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

<span data-ttu-id="a9342-273">[Funcionalidades de movimiento de datos de Data Factory de Azure](../data-factory/data-factory-data-movement-activities.md)
[Actividad DotNet de Data Factory de Azure](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="a9342-273">[Azure Data Factory data movement capabilities](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span></span>

[<span data-ttu-id="a9342-274">Solución de Visual Studio para la actividad DotNet de Factoría de datos de Azure para preparar datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="a9342-274">Azure Data Factory DotNet activity visual studio solution for preparing sample data</span></span>](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-hello-dataset"></a><span data-ttu-id="a9342-275">El conjunto de datos de partición Hola</span><span class="sxs-lookup"><span data-stu-id="a9342-275">Partition hello dataset</span></span>
<span data-ttu-id="a9342-276">las señales de vehículo semiestructurados sin procesar de Hola y conjunto de datos de diagnóstico se crean particiones en el paso de preparación de datos de hello en un formato de mes/año.</span><span class="sxs-lookup"><span data-stu-id="a9342-276">hello raw semi-structured vehicle signals and diagnostic dataset are partitioned in hello data preparation step into a YEAR/MONTH format.</span></span> <span data-ttu-id="a9342-277">Esta subdivisión promociona consulta más eficaz y escalable a largo plazo habilitando a continuación como primera cuenta de hello conmutación de error de un blob cuenta toohello se llena.</span><span class="sxs-lookup"><span data-stu-id="a9342-277">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over from one blob account toohello next as hello first account fills up.</span></span> 

>[!NOTE] 
><span data-ttu-id="a9342-278">Este paso de solución de hello es el procesamiento de toobatch solo es aplicable.</span><span class="sxs-lookup"><span data-stu-id="a9342-278">This step in hello solution is applicable only toobatch processing.</span></span>

<span data-ttu-id="a9342-279">Administración de datos de entrada y salida:</span><span class="sxs-lookup"><span data-stu-id="a9342-279">Input and output data data management:</span></span>

* <span data-ttu-id="a9342-280">Hola **los datos de salida** (con la etiqueta *PartitionedCarEventsTable*) se mantiene toobe durante un largo período de tiempo como formulario de hello atractivos / "rawest" de datos "Data Lake" del cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9342-280">hello **output data** (labeled *PartitionedCarEventsTable*) is toobe kept for a long period of time as hello foundational/"rawest" form of data in hello customer's "Data Lake".</span></span> 
* <span data-ttu-id="a9342-281">Hola **los datos de entrada** toothis canalización normalmente se descartará como datos de salida de hello tienen toohello con plena fidelidad de entrada: solo se almacena (particiones) mejor para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="a9342-281">hello **input data** toothis pipeline would typically be discarded as hello output data has full fidelity toohello input - it's just stored (partitioned) better for subsequent use.</span></span>

![Flujo de trabajo de eventos de automóvil de partición](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

<span data-ttu-id="a9342-283">*Ilustración 10: Flujo de trabajo de eventos de automóvil de partición*</span><span class="sxs-lookup"><span data-stu-id="a9342-283">*Figure 10 – Partition Car Events workflow*</span></span>

<span data-ttu-id="a9342-284">datos sin procesar de Hola se crean particiones en una actividad de HDInsight Hive "PartitionCarEventsPipeline".</span><span class="sxs-lookup"><span data-stu-id="a9342-284">hello raw data is partitioned using a Hive HDInsight activity in "PartitionCarEventsPipeline".</span></span> <span data-ttu-id="a9342-285">datos de ejemplo de Hola generados en el paso 1 para un año se dividen por año/mes.</span><span class="sxs-lookup"><span data-stu-id="a9342-285">hello sample data generated in step 1 for a year is partitioned by YEAR/MONTH.</span></span> <span data-ttu-id="a9342-286">las particiones de Hello son señales de vehículo toogenerate usado y datos de diagnóstico para cada mes (total de 12 particiones) de un año.</span><span class="sxs-lookup"><span data-stu-id="a9342-286">hello partitions are used toogenerate vehicle signals and diagnostic data for each month (total 12 partitions) of a year.</span></span> 

![Actividad PartitionCarEventsPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

<span data-ttu-id="a9342-288">*Figure 11 - PartitionCarEventsPipeline*</span><span class="sxs-lookup"><span data-stu-id="a9342-288">*Figure 11 - PartitionCarEventsPipeline*</span></span>

<span data-ttu-id="a9342-289">***Script de Hive PartitionConnectedCarEvents***</span><span class="sxs-lookup"><span data-stu-id="a9342-289">***PartitionConnectedCarEvents Hive Script***</span></span>

<span data-ttu-id="a9342-290">Hola siguiente script de Hive, denominado "partitioncarevents.hql", se utiliza para crear particiones y se encuentra en hello "\demo\src\connectedcar\scripts" carpeta de descarga de Hola zip.</span><span class="sxs-lookup"><span data-stu-id="a9342-290">hello following Hive script, named "partitioncarevents.hql", is used for partitioning and is located in hello "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 
    
    SET hive.exec.dynamic.partition=true;
    SET hive.exec.dynamic.partition.mode = nonstrict;
    set hive.cli.print.header=true;

    DROP TABLE IF EXISTS RawCarEvents; 
    CREATE EXTERNAL TABLE RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RAWINPUT}'; 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string
    ) partitioned by (YearNo int, MonthNo int) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDOUTPUT}';

    DROP TABLE IF EXISTS Stage_RawCarEvents; 
    CREATE TABLE IF NOT EXISTS Stage_RawCarEvents 
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string,
                YearNo                             int,
                MonthNo                         int) 
    ROW FORMAT delimited fields terminated by ',' LINES TERMINATED BY '10';

    INSERT OVERWRITE TABLE Stage_RawCarEvents
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        Year(gendate),
        Month(gendate)

    FROM RawCarEvents WHERE Year(gendate) = ${hiveconf:Year} AND Month(gendate) = ${hiveconf:Month}; 

    INSERT OVERWRITE TABLE PartitionedCarEvents PARTITION(YearNo, MonthNo) 
    SELECT
        vin,            
        model,
        timestamp,
        outsidetemperature,
        enginetemperature,
        speed,
        fuel,
        engineoil,
        tirepressure,
        odometer,
        city,
        accelerator_pedal_position,
        parking_brake_status,
        headlamp_status,
        brake_pedal_status,
        transmission_gear_position,
        ignition_status,
        windshield_wiper_status,
        abs,
        gendate,
        YearNo,
        MonthNo
    FROM Stage_RawCarEvents WHERE YearNo = ${hiveconf:Year} AND MonthNo = ${hiveconf:Month};

<span data-ttu-id="a9342-291">Una vez que se ejecuta la canalización de hello correctamente, verá Hola después particiones generadas en la cuenta de almacenamiento en el contenedor de "connectedcar" Hola.</span><span class="sxs-lookup"><span data-stu-id="a9342-291">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Salida con particiones](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

<span data-ttu-id="a9342-293">*Ilustración 12: Salida con particiones*</span><span class="sxs-lookup"><span data-stu-id="a9342-293">*Figure 12 - Partitioned Output*</span></span>

<span data-ttu-id="a9342-294">datos de Hola ahora está optimizado, es más fácil de administrar y listo para su posterior procesamiento toogain visión de lote completo.</span><span class="sxs-lookup"><span data-stu-id="a9342-294">hello data is now optimized, is more manageable and ready for further processing toogain rich batch insights.</span></span> 

## <a name="data-analysis"></a><span data-ttu-id="a9342-295">Análisis de datos</span><span class="sxs-lookup"><span data-stu-id="a9342-295">Data Analysis</span></span>
<span data-ttu-id="a9342-296">En esta sección, verá cómo avanzada toocombine análisis de transmisiones de Azure, aprendizaje automático de Azure, Data Factory de Azure y Azure HDInsight para datos completos de transformación de análisis de mantenimiento de vehículo y dirigir.</span><span class="sxs-lookup"><span data-stu-id="a9342-296">In this section, you see how toocombine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory, and Azure HDInsight for rich advanced analytics on vehicle health and driving habits.</span></span> <span data-ttu-id="a9342-297">Hay tres subsecciones aquí:</span><span class="sxs-lookup"><span data-stu-id="a9342-297">There are three subsections here:</span></span>

1. <span data-ttu-id="a9342-298">**Aprendizaje automático**: este apartado incluye información en el experimento de detección de anomalías de Hola que hemos usado en este vehículos toopredict de solución que requiere el servicio de mantenimiento y la necesidad de recuperaciones debido a problemas de toosafety de vehículos.</span><span class="sxs-lookup"><span data-stu-id="a9342-298">**Machine Learning**: This subsection contains information on hello anomaly detection experiment that we have used in this solution toopredict vehicles requiring servicing maintenance and vehicles requiring recalls due toosafety issues.</span></span>
2. <span data-ttu-id="a9342-299">**Análisis en tiempo real**: este apartado incluye información sobre análisis en tiempo real de hello usando el lenguaje de consulta de análisis de transmisiones de Hola y aprendizaje automático de hello en marcha experimentar en tiempo real mediante una aplicación personalizada.</span><span class="sxs-lookup"><span data-stu-id="a9342-299">**Real-time analysis**: This subsection contains information regarding hello real-time analytics using hello Stream Analytics Query Language and operationalizing hello machine learning experiment in real time using a custom application.</span></span>
3. <span data-ttu-id="a9342-300">**Procesar por lotes analysis**: este apartado incluye información relativa a Hola transformar y el procesamiento de datos del lote Hola con HDInsight de Azure y aprendizaje automático de Azure operaciones por factoría de datos de Azure.</span><span class="sxs-lookup"><span data-stu-id="a9342-300">**Batch analysis**: This subsection contains information regarding hello transforming and processing of hello batch data using Azure HDInsight and Azure Machine Learning operationalized by Azure Data Factory.</span></span>

### <a name="machine-learning"></a><span data-ttu-id="a9342-301">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="a9342-301">Machine Learning</span></span>
<span data-ttu-id="a9342-302">Nuestro objetivo es toopredict vehículos de Hola que requieren mantenimiento o recuperación en función de algunas estadísticas de estado.</span><span class="sxs-lookup"><span data-stu-id="a9342-302">Our goal here is toopredict hello vehicles that require maintenance or recall based on certain heath statistics.</span></span> <span data-ttu-id="a9342-303">Hacemos Hola después suposiciones</span><span class="sxs-lookup"><span data-stu-id="a9342-303">We make hello following assumptions</span></span>

* <span data-ttu-id="a9342-304">Si uno de hello tres condiciones siguientes es verdaderas, requieren los vehículos hello **servicio de mantenimiento**:</span><span class="sxs-lookup"><span data-stu-id="a9342-304">If one of hello following three conditions are true, hello vehicles require **servicing maintenance**:</span></span>
  
  * <span data-ttu-id="a9342-305">Presión de los neumáticos es baja</span><span class="sxs-lookup"><span data-stu-id="a9342-305">Tire pressure is low</span></span>
  * <span data-ttu-id="a9342-306">Nivel de aceite del motor es bajo</span><span class="sxs-lookup"><span data-stu-id="a9342-306">Engine oil level is low</span></span>
  * <span data-ttu-id="a9342-307">Temperatura del motor es alta</span><span class="sxs-lookup"><span data-stu-id="a9342-307">Engine temperature is high</span></span>
* <span data-ttu-id="a9342-308">Si uno de hello condiciones siguientes es verdaderas, vehículos Hola pueden tener un **problema de seguridad** y requieren **recuperación**:</span><span class="sxs-lookup"><span data-stu-id="a9342-308">If one of hello following conditions are true, hello vehicles may have a **safety issue** and require **recall**:</span></span>
  
  * <span data-ttu-id="a9342-309">Temperatura del motor es alta, pero la temperatura exterior es baja</span><span class="sxs-lookup"><span data-stu-id="a9342-309">Engine temperature is high but outside temperature is low</span></span>
  * <span data-ttu-id="a9342-310">Temperatura del motor es baja, pero la temperatura exterior es alta</span><span class="sxs-lookup"><span data-stu-id="a9342-310">Engine temperature is low but outside temperature is high</span></span>

<span data-ttu-id="a9342-311">En función de los requisitos anteriores de hello, hemos creado las anomalías toodetect de dos modelos independientes, uno para la detección de mantenimiento del vehículo y otro para la detección de recuperación de vehículo.</span><span class="sxs-lookup"><span data-stu-id="a9342-311">Based on hello previous requirements, we have created two separate models toodetect anomalies, one for vehicle maintenance detection, and one for vehicle recall detection.</span></span> <span data-ttu-id="a9342-312">En estos modelos, el algoritmo de análisis de componentes principales (PCA) integrada de hello sirve para la detección de anomalías.</span><span class="sxs-lookup"><span data-stu-id="a9342-312">In both these models, hello built-in Principal Component Analysis (PCA) algorithm is used for anomaly detection.</span></span> 

<span data-ttu-id="a9342-313">**Modelo de detección de mantenimiento**</span><span class="sxs-lookup"><span data-stu-id="a9342-313">**Maintenance detection model**</span></span>

<span data-ttu-id="a9342-314">Si uno de los tres indicadores tire presión, petróleo motor o temperatura del motor - cumple su condición respectivo, modelo de detección de mantenimiento de hello notifica una anomalía.</span><span class="sxs-lookup"><span data-stu-id="a9342-314">If one of three indicators - tire pressure, engine oil, or engine temperature - satisfies its respective condition, hello maintenance detection model reports an anomaly.</span></span> <span data-ttu-id="a9342-315">Como resultado, únicamente se necesitan tooconsider estos tres variables en la creación de modelos de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9342-315">As a result, we only need tooconsider these three variables in building hello model.</span></span> <span data-ttu-id="a9342-316">En nuestro experimento de aprendizaje automático de Azure, se utiliza en primer lugar un **seleccionar columnas de conjunto de datos** tooextract módulo estos tres variables.</span><span class="sxs-lookup"><span data-stu-id="a9342-316">In our experiment in Azure Machine Learning, we first use a **Select Columns in Dataset** module tooextract these three variables.</span></span> <span data-ttu-id="a9342-317">A continuación utilizamos Hola anomalías basado en PCA módulo toobuild Hola anomalías detección modelo de detección.</span><span class="sxs-lookup"><span data-stu-id="a9342-317">Next we use hello PCA-based anomaly detection module toobuild hello anomaly detection model.</span></span> 

<span data-ttu-id="a9342-318">Análisis de componentes principales (PCA) es una técnica establecida en aprendizaje automático que puede ser la detección de anomalías, clasificación y selección de toofeature aplicado.</span><span class="sxs-lookup"><span data-stu-id="a9342-318">Principal Component Analysis (PCA) is an established technique in machine learning that can be applied toofeature selection, classification, and anomaly detection.</span></span> <span data-ttu-id="a9342-319">PCA convierte un conjunto de casos con variables posiblemente correlacionadas, en un conjunto de valores denominados componentes principales.</span><span class="sxs-lookup"><span data-stu-id="a9342-319">PCA converts a set of case containing possibly correlated variables, into a set of values called principal components.</span></span> <span data-ttu-id="a9342-320">idea clave de Hola de modelado basado en PCA es tooproject datos en un espacio inferior dimensional para que las características y las anomalías se pueden identificar más fácilmente.</span><span class="sxs-lookup"><span data-stu-id="a9342-320">hello key idea of PCA-based modeling is tooproject data onto a lower-dimensional space so that features and anomalies can be more easily identified.</span></span>

<span data-ttu-id="a9342-321">Para cada nueva entrada demasiado hello modelo de detección, detector de anomalías de hello calcula su proyección en vectores propios hello en primer lugar y, a continuación, calcula Hola normalizadas error reconstrucción.</span><span class="sxs-lookup"><span data-stu-id="a9342-321">For each new input too hello detection model, hello anomaly detector first computes its projection on hello eigenvectors, and then computes hello normalized reconstruction error.</span></span> <span data-ttu-id="a9342-322">Este error normalizada es la puntuación de anomalías de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9342-322">This normalized error is hello anomaly score.</span></span> <span data-ttu-id="a9342-323">error Hola Hola superior, hello más anómalos Hola instancia es.</span><span class="sxs-lookup"><span data-stu-id="a9342-323">hello higher hello error, hello more anomalous hello instance is.</span></span> 

<span data-ttu-id="a9342-324">Problema de detección de mantenimiento de hello, cada registro se puede considerar un punto en un espacio de 3 dimensiones definido por la presión tire, petróleo de motor y temperatura del motor coordenadas.</span><span class="sxs-lookup"><span data-stu-id="a9342-324">In hello maintenance detection problem, each record can be considered as a point in a 3-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span></span> <span data-ttu-id="a9342-325">toocapture estas anomalías se puedan Hola original de datos del proyecto en el espacio de 3 dimensiones hello en un espacio de 2 dimensiones con PCA.</span><span class="sxs-lookup"><span data-stu-id="a9342-325">toocapture these anomalies, we can project hello original data in hello 3-dimensional space onto a 2-dimensional space using PCA.</span></span> <span data-ttu-id="a9342-326">Por lo tanto, los estableceremos parámetro hello número de componentes toouse en PCA toobe 2.</span><span class="sxs-lookup"><span data-stu-id="a9342-326">Thus, we set hello parameter Number of components toouse in PCA toobe 2.</span></span> <span data-ttu-id="a9342-327">Este parámetro desempeña un rol importante en la aplicación de la detección de anomalías basada en PCA.</span><span class="sxs-lookup"><span data-stu-id="a9342-327">This parameter plays an important role in applying PCA-based anomaly detection.</span></span> <span data-ttu-id="a9342-328">Después de proyectar datos con PCA, podemos identificar más fácilmente estas anomalías.</span><span class="sxs-lookup"><span data-stu-id="a9342-328">After projecting data using PCA, we can identify these anomalies more easily.</span></span>

<span data-ttu-id="a9342-329">**Modelo de detección de anomalías de recuperación** en el modelo de detección de anomalías de recuperación de hello, usamos Hola seleccionar columnas de conjunto de datos y anomalías basado en PCA módulos de detección de forma similar.</span><span class="sxs-lookup"><span data-stu-id="a9342-329">**Recall anomaly detection model** In hello recall anomaly detection model, we use hello Select Columns in Dataset and PCA-based anomaly detection modules in a similar way.</span></span> <span data-ttu-id="a9342-330">En concreto, se extraen tres variables: temperatura del motor, la temperatura exterior y velocidad - mediante hello **seleccionar columnas de conjunto de datos** módulo.</span><span class="sxs-lookup"><span data-stu-id="a9342-330">Specifically, we first extract three variables - engine temperature, outside temperature, and speed - using hello **Select Columns in Dataset** module.</span></span> <span data-ttu-id="a9342-331">También se incluye velocidad Hola variable, ya que normalmente es la temperatura del motor Hola correlacionado toohello velocidad.</span><span class="sxs-lookup"><span data-stu-id="a9342-331">We also include hello speed variable since hello engine temperature typically is correlated toohello speed.</span></span> <span data-ttu-id="a9342-332">A continuación utilizamos datos de Hola de tooproject del módulo de detección de anomalías basado en PCA de espacio de 3 dimensiones de hello en un espacio tridimensional de 2.</span><span class="sxs-lookup"><span data-stu-id="a9342-332">Next we use PCA-based anomaly detection module tooproject hello data from hello 3-dimensional space onto a 2-dimensional space.</span></span> <span data-ttu-id="a9342-333">se cumplen los criterios de recuperación de Hola y vehículo Hola requiere recuperación cuando la temperatura del motor y la temperatura exterior se correlacionan muy negativamente.</span><span class="sxs-lookup"><span data-stu-id="a9342-333">hello recall criteria are satisfied and so hello vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span></span> <span data-ttu-id="a9342-334">Usa el algoritmo de detección de anomalías basado en PCA, podemos capturar las anomalías de hello después de realizar el PCA.</span><span class="sxs-lookup"><span data-stu-id="a9342-334">Using PCA-based anomaly detection algorithm, we can capture hello anomalies after performing PCA.</span></span> 

<span data-ttu-id="a9342-335">Cualquier modelo de aprendizaje, necesitamos toouse datos normales, que no requieren mantenimiento o recuperación como modelo de detección de anomalías basado en PCA de hello tootrain de datos de entrada de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9342-335">When training either model, we need toouse normal data, which does not require maintenance or recall as hello input data tootrain hello PCA-based anomaly detection model.</span></span> <span data-ttu-id="a9342-336">Hola experimento de puntuación, usamos toodetect de modelo de detección de anomalías de hello entrenado si vehículo Hola requiere mantenimiento o retirada o no.</span><span class="sxs-lookup"><span data-stu-id="a9342-336">In hello scoring experiment, we use hello trained anomaly detection model toodetect whether or not hello vehicle requires maintenance or recall.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="a9342-337">Análisis en tiempo real</span><span class="sxs-lookup"><span data-stu-id="a9342-337">Real-time analysis</span></span>
<span data-ttu-id="a9342-338">Hola después de la consulta de SQL de análisis de secuencia se utiliza Hola de promedio de hello tooget de todos los parámetros del vehículo importante como la velocidad del vehículo, el nivel de combustible, temperatura del motor, cuentakilómetros, tire presión, nivel del motor petróleo y otros.</span><span class="sxs-lookup"><span data-stu-id="a9342-338">hello following Stream Analytics SQL Query is used tooget hello average of all hello important vehicle parameters like vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span></span> <span data-ttu-id="a9342-339">Hello promedios son anomalías toodetect usado, emite alertas y determinar Hola condiciones de estado general de los vehículos utilizados en una región específica y, a continuación, correlacionará toodemographics.</span><span class="sxs-lookup"><span data-stu-id="a9342-339">hello averages are used toodetect anomalies, issue alerts, and determine hello overall health conditions of vehicles operated in specific region and then correlate it toodemographics.</span></span> 

![Consulta de Stream Analytics para el procesamiento en tiempo real](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

<span data-ttu-id="a9342-341">*Ilustración 13: Consulta de Stream Analytics para el procesamiento en tiempo real*</span><span class="sxs-lookup"><span data-stu-id="a9342-341">*Figure 13 – Stream Analytics query for real-time processing*</span></span>

<span data-ttu-id="a9342-342">Todos los promedios de Hola se calculan sobre un TumblingWindow de 3 segundos.</span><span class="sxs-lookup"><span data-stu-id="a9342-342">All hello averages are calculated over a 3-second TumblingWindow.</span></span> <span data-ttu-id="a9342-343">En este caso estamos usando TubmlingWindow puesto que necesitamos que los intervalos de tiempo no se superpongan y sean contiguos.</span><span class="sxs-lookup"><span data-stu-id="a9342-343">We are using TubmlingWindow in this case since we require non-overlapping and contiguous time intervals.</span></span> 

<span data-ttu-id="a9342-344">toolearn más información acerca de todas las funcionalidades de "Ventana" hello en análisis de transmisiones de Azure, haga clic en [basado en ventanas (análisis de transmisiones de Azure)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span><span class="sxs-lookup"><span data-stu-id="a9342-344">toolearn more about all hello "Windowing" capabilities in Azure Stream Analytics, click [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

<span data-ttu-id="a9342-345">**Predicción en tiempo real**</span><span class="sxs-lookup"><span data-stu-id="a9342-345">**Real-time prediction**</span></span>

<span data-ttu-id="a9342-346">Una aplicación se incluye como parte del modelo de aprendizaje automático de solución toooperationalize Hola Hola en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="a9342-346">An application is included as part of hello solution toooperationalize hello machine learning model in real time.</span></span> <span data-ttu-id="a9342-347">Esta aplicación denominada "RealTimeDashboardApp" se crean y configuran como parte de la implementación de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9342-347">This application called “RealTimeDashboardApp” is created and configured as part of hello solution deployment.</span></span> <span data-ttu-id="a9342-348">aplicación Hello realiza siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="a9342-348">hello application performs hello following:</span></span>

1. <span data-ttu-id="a9342-349">Escucha la instancia de concentrador de eventos de tooan donde análisis de transmisiones está publicando continuamente los eventos de hello en un patrón.</span><span class="sxs-lookup"><span data-stu-id="a9342-349">Listens tooan Event Hub instance where Stream Analytics is publishing hello events in a pattern continuously.</span></span> <span data-ttu-id="a9342-350">![Consulta de análisis de secuencia para publicar datos de hello](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *figura 14: consulta de análisis de transmisiones para publicar Hola datos tooan instancia del concentrador de eventos de salida*</span><span class="sxs-lookup"><span data-stu-id="a9342-350">![Stream Analytics query for publishing hello data](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 – Stream Analytics query for publishing hello data tooan output Event Hub instance*</span></span> 
2. <span data-ttu-id="a9342-351">Para cada evento que recibe esta aplicación:</span><span class="sxs-lookup"><span data-stu-id="a9342-351">For every event that this application receives:</span></span> 
   
   * <span data-ttu-id="a9342-352">Datos de Hola de procesos mediante el extremo de puntuación de solicitudes y respuestas de aprendizaje de máquina (RR).</span><span class="sxs-lookup"><span data-stu-id="a9342-352">Processes hello data using Machine Learning Request-Response Scoring (RRS) endpoint.</span></span> <span data-ttu-id="a9342-353">el punto de conexión de Hola RR se publica automáticamente como parte de la implementación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9342-353">hello RRS endpoint is automatically published as part of hello deployment.</span></span>
   * <span data-ttu-id="a9342-354">salida de Hello RR es el conjunto de datos de Power BI de tooa publicado mediante la inserción de hello API.</span><span class="sxs-lookup"><span data-stu-id="a9342-354">hello RRS output is published tooa Power BI dataset using hello push APIs.</span></span>

<span data-ttu-id="a9342-355">Este patrón también es aplicable tooscenarios del que desee toointegrate una aplicación de línea de negocio (LoB) con el flujo de análisis en tiempo real de hello, para escenarios como las alertas, notificaciones y mensajería.</span><span class="sxs-lookup"><span data-stu-id="a9342-355">This pattern is also applicable tooscenarios in which you want toointegrate a Line of Business (LoB) application with hello real-time analytics flow, for scenarios such as alerts, notifications, and messaging.</span></span>

<span data-ttu-id="a9342-356">Haga clic en [RealtimeDashboardApp descarga](http://go.microsoft.com/fwlink/?LinkId=717078) hello toodownload solución RealtimeDashboardApp Visual Studio para las personalizaciones.</span><span class="sxs-lookup"><span data-stu-id="a9342-356">Click [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) toodownload hello RealtimeDashboardApp Visual Studio solution for customizations.</span></span> 

<span data-ttu-id="a9342-357">**Hola tooexecute aplicación de panel en tiempo real**</span><span class="sxs-lookup"><span data-stu-id="a9342-357">**tooexecute hello Real-time Dashboard Application**</span></span>
1. <span data-ttu-id="a9342-358">Extraer y guardar localmente la carpeta ![RealtimeDashboardApp](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Ilustración 16: Carpeta RealtimeDashboardApp*</span><span class="sxs-lookup"><span data-stu-id="a9342-358">Extract and save locally ![RealtimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – RealtimeDashboardApp folder*</span></span>  
2. <span data-ttu-id="a9342-359">Ejecutar la aplicación hello RealtimeDashboardApp.exe</span><span class="sxs-lookup"><span data-stu-id="a9342-359">Execute hello application RealtimeDashboardApp.exe</span></span>
3. <span data-ttu-id="a9342-360">Proporcione credenciales válidas de Power BI, inicie sesión y haga clic en Aceptar</span><span class="sxs-lookup"><span data-stu-id="a9342-360">Provide valid Power BI credentials, sign in and click Accept</span></span> ![Aplicación de inicio de sesión tooPower BI de panel en tiempo real](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Aplicación de panel en tiempo real finalizar el inicio de sesión tooPower BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

<span data-ttu-id="a9342-363">*Figura 17: RealtimeDashboardApp: Inicio de sesión tooPower BI*</span><span class="sxs-lookup"><span data-stu-id="a9342-363">*Figure 17 – RealtimeDashboardApp: Sign-in tooPower BI*</span></span>

>[!NOTE] 
><span data-ttu-id="a9342-364">Si desea que el conjunto de datos de tooflush Hola Power BI, ejecute hello RealtimeDashboardApp con el parámetro "flushdata" hello:</span><span class="sxs-lookup"><span data-stu-id="a9342-364">If you want tooflush hello Power BI dataset, execute hello RealtimeDashboardApp with hello "flushdata" parameter:</span></span> 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a><span data-ttu-id="a9342-365">Análisis por lotes</span><span class="sxs-lookup"><span data-stu-id="a9342-365">Batch analysis</span></span>
<span data-ttu-id="a9342-366">Hola objetivo es tooshow cómo motores Contoso usa hello Azure compute capacidades tooharness grandes cantidades de datos toogain información valiosa en impulsar el patrón, el comportamiento de uso y mantenimiento de vehículo.</span><span class="sxs-lookup"><span data-stu-id="a9342-366">hello goal here is tooshow how Contoso Motors utilizes hello Azure compute capabilities tooharness big data toogain rich insights on driving pattern, usage behavior, and vehicle health.</span></span> <span data-ttu-id="a9342-367">Con esto es posible:</span><span class="sxs-lookup"><span data-stu-id="a9342-367">This makes it possible to:</span></span>

* <span data-ttu-id="a9342-368">Mejorar la experiencia del usuario de Hola y hacerla más barato proporcionando información sobre los hábitos de y los comportamientos de conducción eficaz de combustible que conduce</span><span class="sxs-lookup"><span data-stu-id="a9342-368">Improve hello customer experience and make it cheaper by providing insights on driving habits and fuel efficient driving behaviors</span></span>
* <span data-ttu-id="a9342-369">Obtenga información acerca de forma proactiva acerca de los clientes y sus decisiones de negocios de conducción patrones toogovern y proporcionar Hola mejor en servicios y productos de la clase</span><span class="sxs-lookup"><span data-stu-id="a9342-369">Learn proactively about customers and their driving patters toogovern business decisions and provide hello best in class products & services</span></span>

<span data-ttu-id="a9342-370">En esta solución, que estamos usando como objetivo Hola siguiendo las métricas:</span><span class="sxs-lookup"><span data-stu-id="a9342-370">In this solution, we are targeting hello following metrics:</span></span>

1. <span data-ttu-id="a9342-371">**Dinámico automóvil comportamiento**: identifica la tendencia de Hola de modelos de hello, ubicaciones, condiciones de conducción y tiempo de visión de hello año toogain sobre los patrones de conducción agresivos.</span><span class="sxs-lookup"><span data-stu-id="a9342-371">**Aggressive driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on aggressive driving patterns.</span></span> <span data-ttu-id="a9342-372">Contoso Motors puede usar esta información para campañas de marketing, dando lugar a seguros con nuevas características y prestaciones personalizadas y basados en el uso.</span><span class="sxs-lookup"><span data-stu-id="a9342-372">Contoso Motors can use these insights for marketing campaigns, driving new personalized features and usage-based insurance.</span></span>
2. <span data-ttu-id="a9342-373">**Comportamiento determinante eficaz de combustible**: identifica la tendencia de Hola de modelos de hello, ubicaciones, condiciones de conducción y tiempo de visión de hello año toogain sobre los patrones de conducción eficaz de combustible.</span><span class="sxs-lookup"><span data-stu-id="a9342-373">**Fuel efficient driving behavior**: Identifies hello trend of hello models, locations, driving conditions, and time of hello year toogain insights on fuel efficient driving patterns.</span></span> <span data-ttu-id="a9342-374">Motores de Contoso puede usar estas informaciones para las campañas de marketing imponen nuevas características y automático controladores toohello informes para costo hábitos de conducción descriptivos efectivas y de entorno.</span><span class="sxs-lookup"><span data-stu-id="a9342-374">Contoso Motors can use these insights for marketing campaigns, driving new features and proactive reporting toohello drivers for cost effective and environment friendly driving habits.</span></span> 
3. <span data-ttu-id="a9342-375">**Recuerde modelos**: identifica los modelos que requieren recuperaciones por experimento de aprendizaje automático de detección de anomalías de hello en marcha</span><span class="sxs-lookup"><span data-stu-id="a9342-375">**Recall models**: Identifies models requiring recalls by operationalizing hello anomaly detection machine learning experiment</span></span>

<span data-ttu-id="a9342-376">Echemos un vistazo en los detalles de Hola de cada una de estas métricas,</span><span class="sxs-lookup"><span data-stu-id="a9342-376">Let's look into hello details of each of these metrics,</span></span>

<span data-ttu-id="a9342-377">**Patrón de comportamiento agresivo al volante**</span><span class="sxs-lookup"><span data-stu-id="a9342-377">**Aggressive driving pattern**</span></span>

<span data-ttu-id="a9342-378">Hola particiones señales de vehículo y se procesan los datos de diagnóstico en hello canalización denominado "AggresiveDrivingPatternPipeline" usar modelos de Hive toodetermine hello, la ubicación, vehículo, dando lugar a condiciones y otros parámetros que se comporta agresiva patrón de conducir.</span><span class="sxs-lookup"><span data-stu-id="a9342-378">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "AggresiveDrivingPatternPipeline" using Hive toodetermine hello models, location, vehicle, driving conditions, and other parameters that exhibits aggressive driving pattern.</span></span>

<span data-ttu-id="a9342-379">![Flujo de trabajo de patrón de conducción agresiva](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Ilustración 18: Flujo de trabajo de patrón de conducción agresiva*</span><span class="sxs-lookup"><span data-stu-id="a9342-379">![Aggressive driving pattern workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Aggressive driving pattern workflow*</span></span>


<span data-ttu-id="a9342-380">***Consulta de Hive para el patrón de comportamiento agresivo al volante***</span><span class="sxs-lookup"><span data-stu-id="a9342-380">***Aggressive driving pattern Hive query***</span></span>

<span data-ttu-id="a9342-381">Hola script de Hive denominado "aggresivedriving.hql" que se utiliza para el análisis agresiva patrón determinante de condición se encuentra en "\demo\src\connectedcar\scripts" carpeta de descarga de Hola zip.</span><span class="sxs-lookup"><span data-stu-id="a9342-381">hello Hive script named "aggresivedriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS CarEventsAggresive; 
    CREATE EXTERNAL TABLE CarEventsAggresive
    (
                   vin                         string, 
                model                        string,
                timestamp                    string,
                city                        string,
                speed                          string,
                transmission_gear_position    string,
                brake_pedal_status            string,
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:AGGRESIVEOUTPUT}';



    INSERT OVERWRITE TABLE CarEventsAggresive
    select
    vin,
    model,
    timestamp,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND brake_pedal_status = '1' AND speed >= '50'


<span data-ttu-id="a9342-382">Usa combinación Hola del vehículo posición de engranaje de transmisión, frenos pedales el estado y velocidad toodetect sentido/agresiva automóvil comportamiento basado en frenos patrón a alta velocidad.</span><span class="sxs-lookup"><span data-stu-id="a9342-382">It uses hello combination of vehicle's transmission gear position, brake pedal status, and speed toodetect reckless/aggressive driving behavior based on braking pattern at high speed.</span></span> 

<span data-ttu-id="a9342-383">Una vez que se ejecuta la canalización de hello correctamente, verá Hola después particiones generadas en la cuenta de almacenamiento en el contenedor de "connectedcar" Hola.</span><span class="sxs-lookup"><span data-stu-id="a9342-383">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Resultados de AggressiveDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

<span data-ttu-id="a9342-385">*Ilustración 19: Resultados de AggressiveDrivingPatternPipeline*</span><span class="sxs-lookup"><span data-stu-id="a9342-385">*Figure 19 – AggressiveDrivingPatternPipeline output*</span></span>

<span data-ttu-id="a9342-386">**Patrón de conducción con consumo eficiente de combustible**</span><span class="sxs-lookup"><span data-stu-id="a9342-386">**Fuel efficient driving pattern**</span></span>

<span data-ttu-id="a9342-387">Hola particiones señales de vehículo y datos de diagnóstico se procesan en la canalización de hello denominado "FuelEfficientDrivingPatternPipeline".</span><span class="sxs-lookup"><span data-stu-id="a9342-387">hello partitioned vehicle signals and diagnostic data are processed in hello pipeline named "FuelEfficientDrivingPatternPipeline".</span></span> <span data-ttu-id="a9342-388">Subárbol es toodetermine usado Hola modelos, ubicación, vehículo, determinante condiciones y otras propiedades que exhiben patrón determinante eficaz de combustible.</span><span class="sxs-lookup"><span data-stu-id="a9342-388">Hive is used toodetermine hello models, location, vehicle, driving conditions, and other properties that exhibit fuel efficient driving pattern.</span></span>

![Patrón de conducción con consumo eficiente de combustible](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

<span data-ttu-id="a9342-390">*Ilustración 20: Flujo de trabajo del patrón de conducción con consumo eficiente de combustible*</span><span class="sxs-lookup"><span data-stu-id="a9342-390">*Figure 20 – Fuel-efficient driving pattern workflow*</span></span>

<span data-ttu-id="a9342-391">***Consulta de Hive para el patrón de conducción con consumo eficiente de combustible***</span><span class="sxs-lookup"><span data-stu-id="a9342-391">***Fuel efficient driving pattern Hive query***</span></span>

<span data-ttu-id="a9342-392">Hola script de Hive denominado "fuelefficientdriving.hql" que se utiliza para el análisis agresiva patrón determinante de condición se encuentra en "\demo\src\connectedcar\scripts" carpeta de descarga de Hola zip.</span><span class="sxs-lookup"><span data-stu-id="a9342-392">hello Hive script named "fuelefficientdriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of hello downloaded zip.</span></span> 

    DROP TABLE IF EXISTS PartitionedCarEvents; 
    CREATE EXTERNAL TABLE PartitionedCarEvents
    (
                vin                                string,
                model                            string,
                timestamp                        string,
                outsidetemperature                string,
                enginetemperature                string,
                speed                            string,
                fuel                            string,
                engineoil                        string,
                tirepressure                    string,
                odometer                        string,
                city                            string,
                accelerator_pedal_position        string,
                parking_brake_status            string,
                headlamp_status                    string,
                brake_pedal_status                string,
                transmission_gear_position        string,
                ignition_status                    string,
                windshield_wiper_status            string,
                abs                              string,
                gendate                            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:PARTITIONEDINPUT}';

    DROP TABLE IF EXISTS FuelEfficientDriving; 
    CREATE EXTERNAL TABLE FuelEfficientDriving
    (
                   vin                         string, 
                model                        string,
                   city                        string,
                speed                          string,
                transmission_gear_position    string,                
                brake_pedal_status            string,            
                accelerator_pedal_position    string,                             
                Year                        string,
                Month                        string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:FUELEFFICIENTOUTPUT}';



    INSERT OVERWRITE TABLE FuelEfficientDriving
    select
    vin,
    model,
    city,
    speed,
    transmission_gear_position,
    brake_pedal_status,
    accelerator_pedal_position,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from PartitionedCarEvents
    where transmission_gear_position IN ('fourth', 'fifth', 'sixth', 'seventh', 'eight') AND parking_brake_status = '0' AND brake_pedal_status = '0' AND speed <= '60' AND accelerator_pedal_position >= '50'


<span data-ttu-id="a9342-393">Usa la combinación de Hola de posición de engranaje de transmisión del vehículo, estado pedales frenos, velocidad y combustible de acelerador posición pedales toodetect comportamiento determinante eficaz en función de aceleración, frenos, y acelerar los patrones.</span><span class="sxs-lookup"><span data-stu-id="a9342-393">It uses hello combination of vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position toodetect fuel efficient driving behavior based on acceleration, braking, and speed patterns.</span></span> 

<span data-ttu-id="a9342-394">Una vez que se ejecuta la canalización de hello correctamente, verá Hola después particiones generadas en la cuenta de almacenamiento en el contenedor de "connectedcar" Hola.</span><span class="sxs-lookup"><span data-stu-id="a9342-394">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Resultados de FuelEfficientDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

<span data-ttu-id="a9342-396">*Ilustración 21: Resultados de FuelEfficientDrivingPatternPipeline*</span><span class="sxs-lookup"><span data-stu-id="a9342-396">*Figure 21 – FuelEfficientDrivingPatternPipeline output*</span></span>

<span data-ttu-id="a9342-397">**Predicciones de retirada**</span><span class="sxs-lookup"><span data-stu-id="a9342-397">**Recall Predictions**</span></span>

<span data-ttu-id="a9342-398">experimento de aprendizaje automático de Hola se aprovisionan y se publica como un servicio web como parte de la implementación de la solución de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9342-398">hello machine learning experiment is provisioned and published as a web service as part of hello solution deployment.</span></span> <span data-ttu-id="a9342-399">se utiliza la puntuación punto final de lotes de Hello en este flujo de trabajo, registrado como un servicio vinculado del generador de datos y operaciones con actividad de puntuación de lote de generador de datos.</span><span class="sxs-lookup"><span data-stu-id="a9342-399">hello batch scoring end point is leveraged in this workflow, registered as a data factory linked service and operationalized using data factory batch scoring activity.</span></span>

![Punto de conexión de Machine Learning](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

<span data-ttu-id="a9342-401">*Ilustración 22: Punto de conexión de Machine Learning registrado como un servicio vinculado en Factoría de datos*</span><span class="sxs-lookup"><span data-stu-id="a9342-401">*Figure 22 – Machine learning endpoint registered as a linked service in data factory*</span></span>

<span data-ttu-id="a9342-402">Hola se usa servicio vinculado registrado en hello DetectAnomalyPipeline tooscore Hola datos mediante el modelo de detección de anomalías de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9342-402">hello registered linked service is used in hello DetectAnomalyPipeline tooscore hello data using hello anomaly detection model.</span></span> 

![Actividad de puntuación por lotes de Azure Machine Learning en Factoría de datos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

<span data-ttu-id="a9342-404">*Ilustración 23: Actividad de puntuación por lotes de Azure Machine Learning en Data Factory*</span><span class="sxs-lookup"><span data-stu-id="a9342-404">*Figure 23 – Azure Machine Learning Batch Scoring activity in data factory*</span></span> 

<span data-ttu-id="a9342-405">Hay algunos pasos realizados en esta canalización para la preparación de datos para que se puede operationalized con el servicio web de puntuación de lote de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9342-405">There are few steps performed in this pipeline for data preparation so that it can be operationalized with hello batch scoring web service.</span></span> 

![DetectAnomalyPipeline para predecir la necesidad de retirada de vehículos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

<span data-ttu-id="a9342-407">*Ilustración 24: DetectAnomalyPipeline para predecir la necesidad de retirada de vehículos*</span><span class="sxs-lookup"><span data-stu-id="a9342-407">*Figure 24 – DetectAnomalyPipeline for predicting vehicles requiring recalls*</span></span> 

<span data-ttu-id="a9342-408">***Consulta de Hive de detección de anomalías***</span><span class="sxs-lookup"><span data-stu-id="a9342-408">***Anomaly detection Hive query***</span></span>

<span data-ttu-id="a9342-409">Una vez completada la puntuación de hello, una actividad de HDInsight es tooprocess utilizado y los datos de hello agregado que se clasifican como anomalías por modelo Hola con una puntuación de probabilidad de 0,60 o superior.</span><span class="sxs-lookup"><span data-stu-id="a9342-409">Once hello scoring is completed, an HDInsight activity is used tooprocess and aggregate hello data that are categorized as anomalies by hello model with a probability score of 0.60 or higher.</span></span>

    DROP TABLE IF EXISTS CarEventsAnomaly; 
    CREATE EXTERNAL TABLE CarEventsAnomaly 
    (
                vin                            string,
                model                        string,
                gendate                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                fuel                        string,
                engineoil                    string,
                tirepressure                string,
                odometer                    string,
                city                        string,
                accelerator_pedal_position    string,
                parking_brake_status        string,
                headlamp_status                string,
                brake_pedal_status            string,
                transmission_gear_position    string,
                ignition_status                string,
                windshield_wiper_status        string,
                abs                          string,
                maintenanceLabel            string,
                maintenanceProbability        string,
                RecallLabel                    string,
                RecallProbability            string

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:ANOMALYOUTPUT}';

    DROP TABLE IF EXISTS RecallModel; 
    CREATE EXTERNAL TABLE RecallModel 
    (

                vin                            string,
                model                        string,
                city                        string,
                outsidetemperature            string,
                enginetemperature            string,
                speed                        string,
                Year                        string,
                Month                        string                

    ) ROW FORMAT DELIMITED FIELDS TERMINATED BY ',' LINES TERMINATED BY '10' STORED AS TEXTFILE LOCATION '${hiveconf:RECALLMODELOUTPUT}';

    INSERT OVERWRITE TABLE RecallModel
    select
    vin,
    model,
    city,
    outsidetemperature,
    enginetemperature,
    speed,
    "${hiveconf:Year}" as Year,
    "${hiveconf:Month}" as Month
    from CarEventsAnomaly
    where RecallLabel = '1' AND RecallProbability >= '0.60'


<span data-ttu-id="a9342-410">Una vez que se ejecuta la canalización de hello correctamente, verá Hola después particiones generadas en la cuenta de almacenamiento en el contenedor de "connectedcar" Hola.</span><span class="sxs-lookup"><span data-stu-id="a9342-410">Once hello pipeline is executed successfully, you see hello following partitions generated in your storage account under hello "connectedcar" container.</span></span>

![Resultados de DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

<span data-ttu-id="a9342-412">*Ilustración 25: Resultados de DetectAnomalyPipeline*</span><span class="sxs-lookup"><span data-stu-id="a9342-412">*Figure 25 – DetectAnomalyPipeline output*</span></span>

## <a name="publish"></a><span data-ttu-id="a9342-413">Publicar</span><span class="sxs-lookup"><span data-stu-id="a9342-413">Publish</span></span>

### <a name="real-time-analysis"></a><span data-ttu-id="a9342-414">Análisis en tiempo real</span><span class="sxs-lookup"><span data-stu-id="a9342-414">Real-time analysis</span></span>
<span data-ttu-id="a9342-415">Una de las consultas de hello en el trabajo de análisis de transmisiones de hello publica la salida de tooan de eventos de hello instancia del concentrador de eventos.</span><span class="sxs-lookup"><span data-stu-id="a9342-415">One of hello queries in hello Stream Analytics job publishes hello events tooan output Event Hub instance.</span></span> 

![Trabajo de Stream Analytics publica la salida de tooan instancia del concentrador de eventos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

<span data-ttu-id="a9342-417">*Ilustración 26: análisis de transmisiones publica la salida de tooan instancia del concentrador de eventos*</span><span class="sxs-lookup"><span data-stu-id="a9342-417">*Figure 26 – Stream Analytics job publishes tooan output Event Hub instance*</span></span>

![Instancia de concentrador de eventos de salida de toohello de toopublish de consultas de análisis de transmisiones](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

<span data-ttu-id="a9342-419">*Figura 27: instancia de concentrador de eventos de salida de análisis de transmisiones consulta toopublish toohello*</span><span class="sxs-lookup"><span data-stu-id="a9342-419">*Figure 27 – Stream Analytics query toopublish toohello output Event Hub instance*</span></span>

<span data-ttu-id="a9342-420">Hola que realtimedashboardapp incluido en la solución de hello consume este flujo de eventos.</span><span class="sxs-lookup"><span data-stu-id="a9342-420">This stream of events is consumed by hello RealTimeDashboardApp included in hello solution.</span></span> <span data-ttu-id="a9342-421">Esta aplicación aprovecha el servicio de web de aprendizaje de máquina de solicitud-respuesta de Hola para puntuar en tiempo real y publica Hola de conjunto de datos de Power BI de tooa datos resultantes para su uso.</span><span class="sxs-lookup"><span data-stu-id="a9342-421">This application leverages hello Machine Learning Request-Response web service for real-time scoring and publishes hello resultant data tooa Power BI dataset for consumption.</span></span> 

### <a name="batch-analysis"></a><span data-ttu-id="a9342-422">Análisis por lotes</span><span class="sxs-lookup"><span data-stu-id="a9342-422">Batch analysis</span></span>
<span data-ttu-id="a9342-423">resultados de Hola de lote de Hola y el procesamiento en tiempo real son tablas de base de datos de SQL Azure toohello publicada para su uso.</span><span class="sxs-lookup"><span data-stu-id="a9342-423">hello results of hello batch and real-time processing are published toohello Azure SQL Database tables for consumption.</span></span> <span data-ttu-id="a9342-424">Hello Azure SQL Server, base de datos y tablas de Hola se crean automáticamente como parte del script de instalación de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9342-424">hello Azure SQL Server, Database, and hello tables are created automatically as part of hello setup script.</span></span> 

![Resultados del procesamiento por lotes copiar el flujo de trabajo de toodata mart](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

<span data-ttu-id="a9342-426">*Figura 28: resultados copiar toodata mart flujo de trabajo de procesamiento por lotes*</span><span class="sxs-lookup"><span data-stu-id="a9342-426">*Figure 28 – Batch processing results copy toodata mart workflow*</span></span>

![Trabajo de Stream Analytics publica toodata mart](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

<span data-ttu-id="a9342-428">*Figura 29: análisis de transmisiones publica toodata mart*</span><span class="sxs-lookup"><span data-stu-id="a9342-428">*Figure 29 – Stream Analytics job publishes toodata mart*</span></span>

![Ajuste de puesto de datos en el trabajo de Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

<span data-ttu-id="a9342-430">*Ilustración 30: Ajuste de puesto de datos en el trabajo de Stream Analytics*</span><span class="sxs-lookup"><span data-stu-id="a9342-430">*Figure 30 – Data mart setting in Stream Analytics job*</span></span>

## <a name="consume"></a><span data-ttu-id="a9342-431">Consumo</span><span class="sxs-lookup"><span data-stu-id="a9342-431">Consume</span></span>
<span data-ttu-id="a9342-432">Power BI ofrece a esta solución un panel completo para datos en tiempo real y visualizaciones de análisis predictivo.</span><span class="sxs-lookup"><span data-stu-id="a9342-432">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="a9342-433">Haga clic aquí para obtener instrucciones detalladas sobre cómo configurar informes de Power BI de Hola y el panel de Hola.</span><span class="sxs-lookup"><span data-stu-id="a9342-433">Click here for detailed instructions on setting up hello Power BI reports and hello dashboard.</span></span> <span data-ttu-id="a9342-434">panel de Hello final tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="a9342-434">hello final dashboard looks like this:</span></span>

![Panel de Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

<span data-ttu-id="a9342-436">*Ilustración 31: Panel de Power BI*</span><span class="sxs-lookup"><span data-stu-id="a9342-436">*Figure 31 - Power BI Dashboard*</span></span>

## <a name="summary"></a><span data-ttu-id="a9342-437">Resumen</span><span class="sxs-lookup"><span data-stu-id="a9342-437">Summary</span></span>
<span data-ttu-id="a9342-438">Este documento contiene un desglose detallada de solución de análisis de telemetría de vehículo hello.</span><span class="sxs-lookup"><span data-stu-id="a9342-438">This document contains a detailed drill-down of hello Vehicle Telemetry Analytics Solution.</span></span> <span data-ttu-id="a9342-439">Se presenta un patrón de arquitectura lambda para análisis en tiempo real y de procesamiento por lotes con predicciones y acciones.</span><span class="sxs-lookup"><span data-stu-id="a9342-439">This showcases a lambda architecture pattern for real-time and batch analytics with predictions and actions.</span></span> <span data-ttu-id="a9342-440">Este patrón aplica tooa amplia variedad de casos de uso que requieren la ruta de acceso activa (en tiempo real) y análisis de la ruta de acceso inactivos (lote).</span><span class="sxs-lookup"><span data-stu-id="a9342-440">This pattern applies tooa wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span></span> 

