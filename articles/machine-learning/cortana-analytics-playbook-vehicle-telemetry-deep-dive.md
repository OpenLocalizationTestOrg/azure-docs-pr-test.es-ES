---
title: "Profundización en la predicción del estado de vehículo y los hábitos de conducción - Azure | Microsoft Docs"
description: "Aproveche las posibilidades de Cortana Intelligence para obtener información en tiempo real y predictiva del estado de los vehículos y los hábitos de conducción."
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
ms.openlocfilehash: 0a4dba58445cf0fd9fd8f51d443576bacd92251b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="vehicle-telemetry-analytics-solution-playbook-deep-dive-into-the-solution"></a><span data-ttu-id="2854c-103">Cuaderno de estrategias de soluciones de análisis de telemetría de vehículo: profundización en la solución</span><span class="sxs-lookup"><span data-stu-id="2854c-103">Vehicle telemetry analytics solution playbook: deep dive into the solution</span></span>
<span data-ttu-id="2854c-104">Este **menú** vincula a las secciones de este cuaderno de estrategias.</span><span class="sxs-lookup"><span data-stu-id="2854c-104">This **menu** links to the sections of this playbook:</span></span> 

[!INCLUDE [cap-vehicle-telemetry-playbook-selector](../../includes/cap-vehicle-telemetry-playbook-selector.md)]

<span data-ttu-id="2854c-105">Esta sección profundiza en cada una de las fases que se describen en la sección de arquitectura de la solución, con instrucciones e indicaciones para la personalización.</span><span class="sxs-lookup"><span data-stu-id="2854c-105">This section drills down into each of the stages depicted in the Solution Architecture with instructions and pointers for customization.</span></span> 

## <a name="data-sources"></a><span data-ttu-id="2854c-106">Orígenes de datos</span><span class="sxs-lookup"><span data-stu-id="2854c-106">Data Sources</span></span>
<span data-ttu-id="2854c-107">Esta solución usa dos orígenes de datos diferentes:</span><span class="sxs-lookup"><span data-stu-id="2854c-107">The solution uses two different data sources:</span></span>

* <span data-ttu-id="2854c-108">**conjunto de datos de señales de vehículo y diagnósticos simulados** y</span><span class="sxs-lookup"><span data-stu-id="2854c-108">**simulated vehicle signals and diagnostic dataset** and</span></span> 
* <span data-ttu-id="2854c-109">**catálogo de vehículo**</span><span class="sxs-lookup"><span data-stu-id="2854c-109">**vehicle catalog**</span></span>

<span data-ttu-id="2854c-110">Se incluye un simulador telemático del vehículo como parte de esta solución.</span><span class="sxs-lookup"><span data-stu-id="2854c-110">A vehicle telematics simulator is included as part of this solution.</span></span> <span data-ttu-id="2854c-111">Este simulador emite información de diagnóstico y señales correspondientes al estado del vehículo y al patrón de conducción en un momento dado en el tiempo.</span><span class="sxs-lookup"><span data-stu-id="2854c-111">It emits diagnostic information and signals corresponding to the state of the vehicle and to the driving pattern at a given point in time.</span></span> <span data-ttu-id="2854c-112">Haga clic en el [simulador telemático de vehículo](http://go.microsoft.com/fwlink/?LinkId=717075) para descargar la **solución de simulador telemático de vehículo de Visual Studio** y personalizarla de acuerdo a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="2854c-112">Click [Vehicle Telematics Simulator](http://go.microsoft.com/fwlink/?LinkId=717075) to download the **Vehicle Telematics Simulator Visual Studio Solution** for customizations based on your requirements.</span></span> <span data-ttu-id="2854c-113">El catálogo de vehículo contiene un conjunto de datos de referencia con una asignación de número de identificación VIN a modelo.</span><span class="sxs-lookup"><span data-stu-id="2854c-113">The vehicle catalog contains a reference dataset with a VIN to model mapping.</span></span>

![Simulador telemático de vehículo](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig1-vehicle-telematics-simulator.png)

<span data-ttu-id="2854c-115">*Ilustración 1: Simulador telemático de vehículo*</span><span class="sxs-lookup"><span data-stu-id="2854c-115">*Figure 1 – Vehicle Telematics Simulator*</span></span>

<span data-ttu-id="2854c-116">Se trata de un conjunto de datos con formato JSON que contiene el esquema siguiente.</span><span class="sxs-lookup"><span data-stu-id="2854c-116">This is a JSON-formatted dataset that contains the following schema.</span></span>

| <span data-ttu-id="2854c-117">Columna</span><span class="sxs-lookup"><span data-stu-id="2854c-117">Column</span></span> | <span data-ttu-id="2854c-118">Description</span><span class="sxs-lookup"><span data-stu-id="2854c-118">Description</span></span> | <span data-ttu-id="2854c-119">Valores</span><span class="sxs-lookup"><span data-stu-id="2854c-119">Values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2854c-120">VIN</span><span class="sxs-lookup"><span data-stu-id="2854c-120">VIN</span></span> |<span data-ttu-id="2854c-121">Número de identificación del vehículo generado de forma aleatoria</span><span class="sxs-lookup"><span data-stu-id="2854c-121">Randomly generated Vehicle Identification Number</span></span> |<span data-ttu-id="2854c-122">Se obtiene a partir de una lista maestra de 10.000 números de identificación de vehículo generados de forma aleatoria.</span><span class="sxs-lookup"><span data-stu-id="2854c-122">This is obtained from a master list of 10,000 randomly generated vehicle identification numbers.</span></span> |
| <span data-ttu-id="2854c-123">Outside temperature</span><span class="sxs-lookup"><span data-stu-id="2854c-123">Outside temperature</span></span> |<span data-ttu-id="2854c-124">La temperatura exterior del entorno en el que se está conduciendo el vehículo </span><span class="sxs-lookup"><span data-stu-id="2854c-124">The outside temperature where the vehicle is driving</span></span> |<span data-ttu-id="2854c-125">Número generado al azar de 0 a 100</span><span class="sxs-lookup"><span data-stu-id="2854c-125">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="2854c-126">Engine temperature</span><span class="sxs-lookup"><span data-stu-id="2854c-126">Engine temperature</span></span> |<span data-ttu-id="2854c-127">La temperatura del motor del vehículo</span><span class="sxs-lookup"><span data-stu-id="2854c-127">The engine temperature of the vehicle</span></span> |<span data-ttu-id="2854c-128">Número generado al azar de 0 a 500</span><span class="sxs-lookup"><span data-stu-id="2854c-128">Randomly generated number from 0-500</span></span> |
| <span data-ttu-id="2854c-129">Velocidad</span><span class="sxs-lookup"><span data-stu-id="2854c-129">Speed</span></span> |<span data-ttu-id="2854c-130">La velocidad del motor del vehículo en conducción</span><span class="sxs-lookup"><span data-stu-id="2854c-130">The engine speed at which the vehicle is driving</span></span> |<span data-ttu-id="2854c-131">Número generado al azar de 0 a 100</span><span class="sxs-lookup"><span data-stu-id="2854c-131">Randomly generated number from 0-100</span></span> |
| <span data-ttu-id="2854c-132">Fuel</span><span class="sxs-lookup"><span data-stu-id="2854c-132">Fuel</span></span> |<span data-ttu-id="2854c-133">El nivel de combustible del vehículo</span><span class="sxs-lookup"><span data-stu-id="2854c-133">The fuel level of the vehicle</span></span> |<span data-ttu-id="2854c-134">Número generado al azar de 0 a 100 (indica el porcentaje del nivel de combustible)</span><span class="sxs-lookup"><span data-stu-id="2854c-134">Randomly generated number from 0-100 (indicates fuel level percentage)</span></span> |
| <span data-ttu-id="2854c-135">EngineOil</span><span class="sxs-lookup"><span data-stu-id="2854c-135">EngineOil</span></span> |<span data-ttu-id="2854c-136">El nivel de aceite del motor del vehículo</span><span class="sxs-lookup"><span data-stu-id="2854c-136">The engine oil level of the vehicle</span></span> |<span data-ttu-id="2854c-137">Número generado al azar de 0 a 100 (indica el porcentaje del nivel de aceite del motor)</span><span class="sxs-lookup"><span data-stu-id="2854c-137">Randomly generated number from 0-100 (indicates engine oil level percentage)</span></span> |
| <span data-ttu-id="2854c-138">Presión de los neumáticos</span><span class="sxs-lookup"><span data-stu-id="2854c-138">Tire pressure</span></span> |<span data-ttu-id="2854c-139">La presión de los neumáticos del vehículo</span><span class="sxs-lookup"><span data-stu-id="2854c-139">The tire pressure of the vehicle</span></span> |<span data-ttu-id="2854c-140">Número generado al azar de 0 a 50 (indica el porcentaje del nivel de presión de los neumáticos)</span><span class="sxs-lookup"><span data-stu-id="2854c-140">Randomly generated number from 0-50 (indicates tire pressure level percentage)</span></span> |
| <span data-ttu-id="2854c-141">Odometer</span><span class="sxs-lookup"><span data-stu-id="2854c-141">Odometer</span></span> |<span data-ttu-id="2854c-142">La lectura del cuentakilómetros del vehículo</span><span class="sxs-lookup"><span data-stu-id="2854c-142">The odometer reading of the vehicle</span></span> |<span data-ttu-id="2854c-143">Número generado al azar de 0 a 200000</span><span class="sxs-lookup"><span data-stu-id="2854c-143">Randomly generated number from 0-200000</span></span> |
| <span data-ttu-id="2854c-144">Accelerator_pedal_position</span><span class="sxs-lookup"><span data-stu-id="2854c-144">Accelerator_pedal_position</span></span> |<span data-ttu-id="2854c-145">La posición del pedal del acelerador del vehículo</span><span class="sxs-lookup"><span data-stu-id="2854c-145">The accelerator pedal position of the vehicle</span></span> |<span data-ttu-id="2854c-146">Número generado al azar de 0 a 100 (indica el porcentaje del nivel del acelerador)</span><span class="sxs-lookup"><span data-stu-id="2854c-146">Randomly generated number from 0-100 (indicates accelerator level percentage)</span></span> |
| <span data-ttu-id="2854c-147">Parking_brake_status</span><span class="sxs-lookup"><span data-stu-id="2854c-147">Parking_brake_status</span></span> |<span data-ttu-id="2854c-148">Indica si el vehículo está aparcado o no</span><span class="sxs-lookup"><span data-stu-id="2854c-148">Indicates whether the vehicle is parked or not</span></span> |<span data-ttu-id="2854c-149">Verdadero o falso</span><span class="sxs-lookup"><span data-stu-id="2854c-149">True or False</span></span> |
| <span data-ttu-id="2854c-150">Headlamp_status</span><span class="sxs-lookup"><span data-stu-id="2854c-150">Headlamp_status</span></span> |<span data-ttu-id="2854c-151">Indica si los faros están encendidos o no</span><span class="sxs-lookup"><span data-stu-id="2854c-151">Indicates where the headlamp is on or not</span></span> |<span data-ttu-id="2854c-152">Verdadero o falso</span><span class="sxs-lookup"><span data-stu-id="2854c-152">True or False</span></span> |
| <span data-ttu-id="2854c-153">Brake_pedal_status</span><span class="sxs-lookup"><span data-stu-id="2854c-153">Brake_pedal_status</span></span> |<span data-ttu-id="2854c-154">Indica si el pedal de freno está pisado o no</span><span class="sxs-lookup"><span data-stu-id="2854c-154">Indicates whether the brake pedal is pressed or not</span></span> |<span data-ttu-id="2854c-155">Verdadero o falso</span><span class="sxs-lookup"><span data-stu-id="2854c-155">True or False</span></span> |
| <span data-ttu-id="2854c-156">Transmission_gear_position</span><span class="sxs-lookup"><span data-stu-id="2854c-156">Transmission_gear_position</span></span> |<span data-ttu-id="2854c-157">La posición del cambio de marcha del vehículo</span><span class="sxs-lookup"><span data-stu-id="2854c-157">The transmission gear position of the vehicle</span></span> |<span data-ttu-id="2854c-158">Estados: primera, segunda, tercera y cuarta, quinta, sexta, séptima, octava</span><span class="sxs-lookup"><span data-stu-id="2854c-158">States: first, second, third, fourth, fifth, sixth, seventh, eighth</span></span> |
| <span data-ttu-id="2854c-159">Ignition_status</span><span class="sxs-lookup"><span data-stu-id="2854c-159">Ignition_status</span></span> |<span data-ttu-id="2854c-160">Indica si el vehículo está en marcha o detenido</span><span class="sxs-lookup"><span data-stu-id="2854c-160">Indicates whether the vehicle is running or stopped</span></span> |<span data-ttu-id="2854c-161">Verdadero o falso</span><span class="sxs-lookup"><span data-stu-id="2854c-161">True or False</span></span> |
| <span data-ttu-id="2854c-162">Windshield_wiper_status</span><span class="sxs-lookup"><span data-stu-id="2854c-162">Windshield_wiper_status</span></span> |<span data-ttu-id="2854c-163">Indica si el limpiaparabrisas está activado o no</span><span class="sxs-lookup"><span data-stu-id="2854c-163">Indicates whether the windshield wiper is turned or not</span></span> |<span data-ttu-id="2854c-164">Verdadero o falso</span><span class="sxs-lookup"><span data-stu-id="2854c-164">True or False</span></span> |
| <span data-ttu-id="2854c-165">ABS</span><span class="sxs-lookup"><span data-stu-id="2854c-165">ABS</span></span> |<span data-ttu-id="2854c-166">Indica si el ABS está activado o no</span><span class="sxs-lookup"><span data-stu-id="2854c-166">Indicates whether ABS is engaged or not</span></span> |<span data-ttu-id="2854c-167">Verdadero o falso</span><span class="sxs-lookup"><span data-stu-id="2854c-167">True or False</span></span> |
| <span data-ttu-id="2854c-168">Timestamp</span><span class="sxs-lookup"><span data-stu-id="2854c-168">Timestamp</span></span> |<span data-ttu-id="2854c-169">La marca de tiempo del momento en el que se crea el punto de datos</span><span class="sxs-lookup"><span data-stu-id="2854c-169">The timestamp when the data point is created</span></span> |<span data-ttu-id="2854c-170">Date</span><span class="sxs-lookup"><span data-stu-id="2854c-170">Date</span></span> |
| <span data-ttu-id="2854c-171">City</span><span class="sxs-lookup"><span data-stu-id="2854c-171">City</span></span> |<span data-ttu-id="2854c-172">La ubicación del vehículo</span><span class="sxs-lookup"><span data-stu-id="2854c-172">The location of the vehicle</span></span> |<span data-ttu-id="2854c-173">En esta solución tiene la opción de 4 ciudades: Bellevue, Redmond, Sammamish, Seattle</span><span class="sxs-lookup"><span data-stu-id="2854c-173">4 cities in this solution: Bellevue, Redmond, Sammamish, Seattle</span></span> |

<span data-ttu-id="2854c-174">El conjunto de datos de referencia de modelo del vehículo contiene una asignación de VIN al modelo.</span><span class="sxs-lookup"><span data-stu-id="2854c-174">The vehicle model reference dataset contains VIN to the model mapping.</span></span> 

| <span data-ttu-id="2854c-175">VIN</span><span class="sxs-lookup"><span data-stu-id="2854c-175">VIN</span></span> | <span data-ttu-id="2854c-176">Modelo</span><span class="sxs-lookup"><span data-stu-id="2854c-176">Model</span></span> |
| --- | --- |
| <span data-ttu-id="2854c-177">FHL3O1SA4IEHB4WU1</span><span class="sxs-lookup"><span data-stu-id="2854c-177">FHL3O1SA4IEHB4WU1</span></span> |<span data-ttu-id="2854c-178">Sedán</span><span class="sxs-lookup"><span data-stu-id="2854c-178">Sedan</span></span> |
| <span data-ttu-id="2854c-179">8J0U8XCPRGW4Z3NQE</span><span class="sxs-lookup"><span data-stu-id="2854c-179">8J0U8XCPRGW4Z3NQE</span></span> |<span data-ttu-id="2854c-180">Híbrido</span><span class="sxs-lookup"><span data-stu-id="2854c-180">Hybrid</span></span> |
| <span data-ttu-id="2854c-181">WORG68Z2PLTNZDBI7</span><span class="sxs-lookup"><span data-stu-id="2854c-181">WORG68Z2PLTNZDBI7</span></span> |<span data-ttu-id="2854c-182">Berlina familiar</span><span class="sxs-lookup"><span data-stu-id="2854c-182">Family Saloon</span></span> |
| <span data-ttu-id="2854c-183">JTHMYHQTEPP4WBMRN</span><span class="sxs-lookup"><span data-stu-id="2854c-183">JTHMYHQTEPP4WBMRN</span></span> |<span data-ttu-id="2854c-184">Sedán</span><span class="sxs-lookup"><span data-stu-id="2854c-184">Sedan</span></span> |
| <span data-ttu-id="2854c-185">W9FTHG27LZN1YWO0Y</span><span class="sxs-lookup"><span data-stu-id="2854c-185">W9FTHG27LZN1YWO0Y</span></span> |<span data-ttu-id="2854c-186">Híbrido</span><span class="sxs-lookup"><span data-stu-id="2854c-186">Hybrid</span></span> |
| <span data-ttu-id="2854c-187">MHTP9N792PHK08WJM</span><span class="sxs-lookup"><span data-stu-id="2854c-187">MHTP9N792PHK08WJM</span></span> |<span data-ttu-id="2854c-188">Berlina familiar</span><span class="sxs-lookup"><span data-stu-id="2854c-188">Family Saloon</span></span> |
| <span data-ttu-id="2854c-189">EI4QXI2AXVQQING4I</span><span class="sxs-lookup"><span data-stu-id="2854c-189">EI4QXI2AXVQQING4I</span></span> |<span data-ttu-id="2854c-190">Sedán</span><span class="sxs-lookup"><span data-stu-id="2854c-190">Sedan</span></span> |
| <span data-ttu-id="2854c-191">5KKR2VB4WHQH97PF8</span><span class="sxs-lookup"><span data-stu-id="2854c-191">5KKR2VB4WHQH97PF8</span></span> |<span data-ttu-id="2854c-192">Híbrido</span><span class="sxs-lookup"><span data-stu-id="2854c-192">Hybrid</span></span> |
| <span data-ttu-id="2854c-193">W9NSZ423XZHAONYXB</span><span class="sxs-lookup"><span data-stu-id="2854c-193">W9NSZ423XZHAONYXB</span></span> |<span data-ttu-id="2854c-194">Berlina familiar</span><span class="sxs-lookup"><span data-stu-id="2854c-194">Family Saloon</span></span> |
| <span data-ttu-id="2854c-195">26WJSGHX4MA5ROHNL</span><span class="sxs-lookup"><span data-stu-id="2854c-195">26WJSGHX4MA5ROHNL</span></span> |<span data-ttu-id="2854c-196">Descapotable</span><span class="sxs-lookup"><span data-stu-id="2854c-196">Convertible</span></span> |
| <span data-ttu-id="2854c-197">GHLUB6ONKMOSI7E77</span><span class="sxs-lookup"><span data-stu-id="2854c-197">GHLUB6ONKMOSI7E77</span></span> |<span data-ttu-id="2854c-198">Familiar</span><span class="sxs-lookup"><span data-stu-id="2854c-198">Station Wagon</span></span> |
| <span data-ttu-id="2854c-199">9C2RHVRVLMEJDBXLP</span><span class="sxs-lookup"><span data-stu-id="2854c-199">9C2RHVRVLMEJDBXLP</span></span> |<span data-ttu-id="2854c-200">Compacto</span><span class="sxs-lookup"><span data-stu-id="2854c-200">Compact Car</span></span> |
| <span data-ttu-id="2854c-201">BRNHVMZOUJ6EOCP32</span><span class="sxs-lookup"><span data-stu-id="2854c-201">BRNHVMZOUJ6EOCP32</span></span> |<span data-ttu-id="2854c-202">SUV pequeño</span><span class="sxs-lookup"><span data-stu-id="2854c-202">Small SUV</span></span> |
| <span data-ttu-id="2854c-203">VCYVW0WUZNBTM594J</span><span class="sxs-lookup"><span data-stu-id="2854c-203">VCYVW0WUZNBTM594J</span></span> |<span data-ttu-id="2854c-204">Deportivo</span><span class="sxs-lookup"><span data-stu-id="2854c-204">Sports Car</span></span> |
| <span data-ttu-id="2854c-205">HNVCE6YFZSA5M82NY</span><span class="sxs-lookup"><span data-stu-id="2854c-205">HNVCE6YFZSA5M82NY</span></span> |<span data-ttu-id="2854c-206">SUV mediano</span><span class="sxs-lookup"><span data-stu-id="2854c-206">Medium SUV</span></span> |
| <span data-ttu-id="2854c-207">4R30FOR7NUOBL05GJ</span><span class="sxs-lookup"><span data-stu-id="2854c-207">4R30FOR7NUOBL05GJ</span></span> |<span data-ttu-id="2854c-208">Familiar</span><span class="sxs-lookup"><span data-stu-id="2854c-208">Station Wagon</span></span> |
| <span data-ttu-id="2854c-209">WYNIIY42VKV6OQS1J</span><span class="sxs-lookup"><span data-stu-id="2854c-209">WYNIIY42VKV6OQS1J</span></span> |<span data-ttu-id="2854c-210">SUV grande</span><span class="sxs-lookup"><span data-stu-id="2854c-210">Large SUV</span></span> |
| <span data-ttu-id="2854c-211">8Y5QKG27QET1RBK7I</span><span class="sxs-lookup"><span data-stu-id="2854c-211">8Y5QKG27QET1RBK7I</span></span> |<span data-ttu-id="2854c-212">SUV grande</span><span class="sxs-lookup"><span data-stu-id="2854c-212">Large SUV</span></span> |
| <span data-ttu-id="2854c-213">DF6OX2WSRA6511BVG</span><span class="sxs-lookup"><span data-stu-id="2854c-213">DF6OX2WSRA6511BVG</span></span> |<span data-ttu-id="2854c-214">Cupé</span><span class="sxs-lookup"><span data-stu-id="2854c-214">Coupe</span></span> |
| <span data-ttu-id="2854c-215">Z2EOZWZBXAEW3E60T</span><span class="sxs-lookup"><span data-stu-id="2854c-215">Z2EOZWZBXAEW3E60T</span></span> |<span data-ttu-id="2854c-216">Sedán</span><span class="sxs-lookup"><span data-stu-id="2854c-216">Sedan</span></span> |
| <span data-ttu-id="2854c-217">M4TV6IEALD5QDS3IR</span><span class="sxs-lookup"><span data-stu-id="2854c-217">M4TV6IEALD5QDS3IR</span></span> |<span data-ttu-id="2854c-218">Híbrido</span><span class="sxs-lookup"><span data-stu-id="2854c-218">Hybrid</span></span> |
| <span data-ttu-id="2854c-219">VHRA1Y2TGTA84F00H</span><span class="sxs-lookup"><span data-stu-id="2854c-219">VHRA1Y2TGTA84F00H</span></span> |<span data-ttu-id="2854c-220">Berlina familiar</span><span class="sxs-lookup"><span data-stu-id="2854c-220">Family Saloon</span></span> |
| <span data-ttu-id="2854c-221">R0JAUHT1L1R3BIKI0</span><span class="sxs-lookup"><span data-stu-id="2854c-221">R0JAUHT1L1R3BIKI0</span></span> |<span data-ttu-id="2854c-222">Sedán</span><span class="sxs-lookup"><span data-stu-id="2854c-222">Sedan</span></span> |
| <span data-ttu-id="2854c-223">9230C202Z60XX84AU</span><span class="sxs-lookup"><span data-stu-id="2854c-223">9230C202Z60XX84AU</span></span> |<span data-ttu-id="2854c-224">Híbrido</span><span class="sxs-lookup"><span data-stu-id="2854c-224">Hybrid</span></span> |
| <span data-ttu-id="2854c-225">T8DNDN5UDCWL7M72H</span><span class="sxs-lookup"><span data-stu-id="2854c-225">T8DNDN5UDCWL7M72H</span></span> |<span data-ttu-id="2854c-226">Berlina familiar</span><span class="sxs-lookup"><span data-stu-id="2854c-226">Family Saloon</span></span> |
| <span data-ttu-id="2854c-227">4WPYRUZII5YV7YA42</span><span class="sxs-lookup"><span data-stu-id="2854c-227">4WPYRUZII5YV7YA42</span></span> |<span data-ttu-id="2854c-228">Sedán</span><span class="sxs-lookup"><span data-stu-id="2854c-228">Sedan</span></span> |
| <span data-ttu-id="2854c-229">D1ZVY26UV2BFGHZNO</span><span class="sxs-lookup"><span data-stu-id="2854c-229">D1ZVY26UV2BFGHZNO</span></span> |<span data-ttu-id="2854c-230">Híbrido</span><span class="sxs-lookup"><span data-stu-id="2854c-230">Hybrid</span></span> |
| <span data-ttu-id="2854c-231">XUF99EW9OIQOMV7Q7</span><span class="sxs-lookup"><span data-stu-id="2854c-231">XUF99EW9OIQOMV7Q7</span></span> |<span data-ttu-id="2854c-232">Berlina familiar</span><span class="sxs-lookup"><span data-stu-id="2854c-232">Family Saloon</span></span> |
| <span data-ttu-id="2854c-233">8OMCL3LGI7XNCC21U</span><span class="sxs-lookup"><span data-stu-id="2854c-233">8OMCL3LGI7XNCC21U</span></span> |<span data-ttu-id="2854c-234">Descapotable</span><span class="sxs-lookup"><span data-stu-id="2854c-234">Convertible</span></span> |
| <span data-ttu-id="2854c-235">…….</span><span class="sxs-lookup"><span data-stu-id="2854c-235">…….</span></span> | |

### <a name="references"></a><span data-ttu-id="2854c-236">Referencias</span><span class="sxs-lookup"><span data-stu-id="2854c-236">References</span></span>
[<span data-ttu-id="2854c-237">Solución de simulador telemático de vehículo de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2854c-237">Vehicle Telematics Simulator Visual Studio Solution</span></span>](http://go.microsoft.com/fwlink/?LinkId=717075) 

[<span data-ttu-id="2854c-238">Centro de eventos de Azure</span><span class="sxs-lookup"><span data-stu-id="2854c-238">Azure Event Hub</span></span>](https://azure.microsoft.com/services/event-hubs/)

[<span data-ttu-id="2854c-239">Factoría de datos de Azure</span><span class="sxs-lookup"><span data-stu-id="2854c-239">Azure Data Factory</span></span>](https://azure.microsoft.com/documentation/learning-paths/data-factory/)

## <a name="ingestion"></a><span data-ttu-id="2854c-240">Ingesta de datos</span><span class="sxs-lookup"><span data-stu-id="2854c-240">Ingestion</span></span>
<span data-ttu-id="2854c-241">Se aprovecha una combinación de Azure Event Hubs, Stream Analytics y Data Factory para introducir las señales de vehículo, los eventos de diagnóstico y los análisis en tiempo real y de lotes.</span><span class="sxs-lookup"><span data-stu-id="2854c-241">Combinations of Azure Event Hubs, Stream Analytics, and Data Factory are leveraged to ingest the vehicle signals, the diagnostic events, and real-time and batch analytics.</span></span> <span data-ttu-id="2854c-242">Todos estos componentes se crean y se configuran como parte de la implementación de la solución.</span><span class="sxs-lookup"><span data-stu-id="2854c-242">All these components are created and configured as part of the solution deployment.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="2854c-243">Análisis en tiempo real</span><span class="sxs-lookup"><span data-stu-id="2854c-243">Real-time analysis</span></span>
<span data-ttu-id="2854c-244">Los eventos generados por el simulador telemático de vehículo se publican en el Centro de eventos mediante el SDK del Centro de eventos.</span><span class="sxs-lookup"><span data-stu-id="2854c-244">The events generated by the Vehicle Telematics Simulator are published to the Event Hub using the Event Hub SDK.</span></span> <span data-ttu-id="2854c-245">El trabajo de Stream Analytics recopila estos eventos desde Event Hubs y procesa los datos en tiempo real para analizar el estado del vehículo.</span><span class="sxs-lookup"><span data-stu-id="2854c-245">The Stream Analytics job ingests these events from the Event Hub and processes the data in real time to analyze the vehicle health.</span></span> 

![Panel del Centro de eventos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig4-vehicle-telematics-event-hub-dashboard.png) 

<span data-ttu-id="2854c-247">*Ilustración 4: Panel del Centro de eventos*</span><span class="sxs-lookup"><span data-stu-id="2854c-247">*Figure 4 - Event Hub dashboard*</span></span>

![Procesamiento de datos del trabajo de Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig5-vehicle-telematics-stream-analytics-job-processing-data.png) 

<span data-ttu-id="2854c-249">*Ilustración 5: Procesamiento de datos del trabajo de Stream Analytics*</span><span class="sxs-lookup"><span data-stu-id="2854c-249">*Figure 5 - Stream Analytics job processing data*</span></span>

<span data-ttu-id="2854c-250">Ejecución del trabajo de Stream Analytics;</span><span class="sxs-lookup"><span data-stu-id="2854c-250">The Stream Analytics job;</span></span>

* <span data-ttu-id="2854c-251">recopila datos de Event Hubs</span><span class="sxs-lookup"><span data-stu-id="2854c-251">ingests data from the Event Hub</span></span> 
* <span data-ttu-id="2854c-252">realiza una combinación con los datos de referencia para asignar el VIN del vehículo al modelo correspondiente</span><span class="sxs-lookup"><span data-stu-id="2854c-252">performs a join with the reference data to map the vehicle VIN to the corresponding model</span></span> 
* <span data-ttu-id="2854c-253">los conserva en Azure Blob Storage para unos análisis eficaces por lotes.</span><span class="sxs-lookup"><span data-stu-id="2854c-253">persists them into Azure blob storage for rich batch analytics.</span></span> 

<span data-ttu-id="2854c-254">La siguiente consulta de Stream Analytics se usa para conservar los datos en Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="2854c-254">The following Stream Analytics query is used to persist the data into Azure blob storage.</span></span> 

![Consulta de trabajo de Stream Analytics para la ingesta de datos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig6-vehicle-telematics-stream-analytics-job-query-for-data-ingestion.png) 

<span data-ttu-id="2854c-256">*Ilustración 6: Consulta de trabajo de Stream Analytics para la ingesta de datos*</span><span class="sxs-lookup"><span data-stu-id="2854c-256">*Figure 6 - Stream Analytics job query for data ingestion*</span></span>

### <a name="batch-analysis"></a><span data-ttu-id="2854c-257">Análisis por lotes</span><span class="sxs-lookup"><span data-stu-id="2854c-257">Batch analysis</span></span>
<span data-ttu-id="2854c-258">También se genera un volumen adicional de las señales y el conjunto de datos de diagnóstico del vehículo simulado para un análisis por lotes más completo.</span><span class="sxs-lookup"><span data-stu-id="2854c-258">We are also generating an additional volume of simulated vehicle signals and diagnostic dataset for richer batch analytics.</span></span> <span data-ttu-id="2854c-259">Esto es necesario para garantizar un volumen de datos representativo para el procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="2854c-259">This is required to ensure a good representative data volume for batch processing.</span></span> <span data-ttu-id="2854c-260">Con este propósito, usamos una canalización llamada "PrepareSampleDataPipeline" en el flujo de trabajo de Data Factory de para generar un conjunto de datos de diagnóstico y de señales de vehículo simulado para un año completo.</span><span class="sxs-lookup"><span data-stu-id="2854c-260">For this purpose, we are using a pipeline named "PrepareSampleDataPipeline" in the Azure Data Factory workflow to generate one year's worth of simulated vehicle signals and diagnostic dataset.</span></span> <span data-ttu-id="2854c-261">Haga clic en la [actividad personalizada de la Factoría de datos](http://go.microsoft.com/fwlink/?LinkId=717077) para descargar la solución de Visual Studio de actividad DotNet personalizada de Factoría de datos para realizar personalizaciones que se ajusten a sus necesidades.</span><span class="sxs-lookup"><span data-stu-id="2854c-261">Click [Data Factory custom activity](http://go.microsoft.com/fwlink/?LinkId=717077) to download the Data Factory custom DotNet activity Visual Studio solution for customizations based on your requirements.</span></span> 

![Preparar los datos de muestra para el flujo de trabajo de procesamiento por lotes](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig7-vehicle-telematics-prepare-sample-data-for-batch-processing.png) 

<span data-ttu-id="2854c-263">*Ilustración 7: Preparar los datos de muestra para el flujo de trabajo de procesamiento por lotes*</span><span class="sxs-lookup"><span data-stu-id="2854c-263">*Figure 7 - Prepare Sample data for batch processing workflow*</span></span>

<span data-ttu-id="2854c-264">La canalización consta de una actividad .NET ADF personalizada que se muestra aquí:</span><span class="sxs-lookup"><span data-stu-id="2854c-264">The pipeline consists of a custom ADF .Net Activity, show here:</span></span>

![Actividad PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig8-vehicle-telematics-prepare-sample-data-pipeline.png) 

<span data-ttu-id="2854c-266">*Ilustración 8: PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="2854c-266">*Figure 8 - PrepareSampleDataPipeline*</span></span>

<span data-ttu-id="2854c-267">Una vez que la canalización se ejecute correctamente y se marque el conjunto de datos "RawCarEventsTable" como "Ready", se creará un año entero de datos de señales y diagnóstico de vehículo simulado.</span><span class="sxs-lookup"><span data-stu-id="2854c-267">Once the pipeline executes successfully and "RawCarEventsTable" dataset is marked "Ready", one-year worth of simulated vehicle signals and diagnostic data are produced.</span></span> <span data-ttu-id="2854c-268">Verá la siguiente carpeta y archivo creado en la cuenta de almacenamiento en el contenedor "connectedcar":</span><span class="sxs-lookup"><span data-stu-id="2854c-268">You see the following folder and file created in your storage account under the "connectedcar" container:</span></span>

![Resultados de PrepareSampleDataPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig9-vehicle-telematics-prepare-sample-data-pipeline-output.png) 

<span data-ttu-id="2854c-270">*Ilustración 9: Resultados de PrepareSampleDataPipeline*</span><span class="sxs-lookup"><span data-stu-id="2854c-270">*Figure 9 - PrepareSampleDataPipeline Output*</span></span>

### <a name="references"></a><span data-ttu-id="2854c-271">Referencias</span><span class="sxs-lookup"><span data-stu-id="2854c-271">References</span></span>
[<span data-ttu-id="2854c-272">SDK del Centro de eventos de Azure para ingesta de transmisiones</span><span class="sxs-lookup"><span data-stu-id="2854c-272">Azure Event Hub SDK for stream ingestion</span></span>](../event-hubs/event-hubs-csharp-ephcs-getstarted.md)

<span data-ttu-id="2854c-273">[Funcionalidades de movimiento de datos de Data Factory de Azure](../data-factory/data-factory-data-movement-activities.md)
[Actividad DotNet de Data Factory de Azure](../data-factory/data-factory-use-custom-activities.md)</span><span class="sxs-lookup"><span data-stu-id="2854c-273">[Azure Data Factory data movement capabilities](../data-factory/data-factory-data-movement-activities.md)
[Azure Data Factory DotNet Activity](../data-factory/data-factory-use-custom-activities.md)</span></span>

[<span data-ttu-id="2854c-274">Solución de Visual Studio para la actividad DotNet de Factoría de datos de Azure para preparar datos de ejemplo</span><span class="sxs-lookup"><span data-stu-id="2854c-274">Azure Data Factory DotNet activity visual studio solution for preparing sample data</span></span>](http://go.microsoft.com/fwlink/?LinkId=717077) 

## <a name="partition-the-dataset"></a><span data-ttu-id="2854c-275">Creación de particiones del conjunto de datos</span><span class="sxs-lookup"><span data-stu-id="2854c-275">Partition the dataset</span></span>
<span data-ttu-id="2854c-276">Se crean particiones de las señales semiestructuradas y sin procesar de los vehículos y del conjunto de datos de diagnóstico en el paso de preparación de datos en un formato de año y mes.</span><span class="sxs-lookup"><span data-stu-id="2854c-276">The raw semi-structured vehicle signals and diagnostic dataset are partitioned in the data preparation step into a YEAR/MONTH format.</span></span> <span data-ttu-id="2854c-277">Esta creación de particiones facilita la realización de unas consultas más eficaces y un almacenamiento escalable a largo plazo habilitando el paso de una cuenta de blob a la siguiente cuando la primera cuenta está llena.</span><span class="sxs-lookup"><span data-stu-id="2854c-277">This partitioning promotes more efficient querying and scalable long-term storage by enabling fault-over from one blob account to the next as the first account fills up.</span></span> 

>[!NOTE] 
><span data-ttu-id="2854c-278">Este paso de la solución solo es aplicable al procesamiento por lotes.</span><span class="sxs-lookup"><span data-stu-id="2854c-278">This step in the solution is applicable only to batch processing.</span></span>

<span data-ttu-id="2854c-279">Administración de datos de entrada y salida:</span><span class="sxs-lookup"><span data-stu-id="2854c-279">Input and output data data management:</span></span>

* <span data-ttu-id="2854c-280">Los **datos de salida** (etiquetados *PartitionedCarEventsTable*) se guardarán durante un largo período de tiempo como formulario de datos fundacionales (sin procesamiento alguno) en el "Data Lake" del cliente.</span><span class="sxs-lookup"><span data-stu-id="2854c-280">The **output data** (labeled *PartitionedCarEventsTable*) is to be kept for a long period of time as the foundational/"rawest" form of data in the customer's "Data Lake".</span></span> 
* <span data-ttu-id="2854c-281">Normalmente se podrían descartar los **datos de entrada** para esta canalización, ya que los datos de salida mantienen la máxima fidelidad a la entrada, simplemente se almacenan (se crean particiones) para su uso posterior.</span><span class="sxs-lookup"><span data-stu-id="2854c-281">The **input data** to this pipeline would typically be discarded as the output data has full fidelity to the input - it's just stored (partitioned) better for subsequent use.</span></span>

![Flujo de trabajo de eventos de automóvil de partición](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig10-vehicle-telematics-partition-car-events-workflow.png)

<span data-ttu-id="2854c-283">*Ilustración 10: Flujo de trabajo de eventos de automóvil de partición*</span><span class="sxs-lookup"><span data-stu-id="2854c-283">*Figure 10 – Partition Car Events workflow*</span></span>

<span data-ttu-id="2854c-284">Los datos sin procesar se particionan mediante una actividad de HDInsight Hive en "PartitionCarEventsPipeline".</span><span class="sxs-lookup"><span data-stu-id="2854c-284">The raw data is partitioned using a Hive HDInsight activity in "PartitionCarEventsPipeline".</span></span> <span data-ttu-id="2854c-285">Se crean particiones de los datos de ejemplo generados en el paso 1 durante un año por AÑO y MES.</span><span class="sxs-lookup"><span data-stu-id="2854c-285">The sample data generated in step 1 for a year is partitioned by YEAR/MONTH.</span></span> <span data-ttu-id="2854c-286">Las particiones se utilizan para generar señales de vehículo y datos de diagnóstico para cada mes (un total de 12 particiones) de un año.</span><span class="sxs-lookup"><span data-stu-id="2854c-286">The partitions are used to generate vehicle signals and diagnostic data for each month (total 12 partitions) of a year.</span></span> 

![Actividad PartitionCarEventsPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig11-vehicle-telematics-partition-car-events-pipeline.png)

<span data-ttu-id="2854c-288">*Figure 11 - PartitionCarEventsPipeline*</span><span class="sxs-lookup"><span data-stu-id="2854c-288">*Figure 11 - PartitionCarEventsPipeline*</span></span>

<span data-ttu-id="2854c-289">***Script de Hive PartitionConnectedCarEvents***</span><span class="sxs-lookup"><span data-stu-id="2854c-289">***PartitionConnectedCarEvents Hive Script***</span></span>

<span data-ttu-id="2854c-290">El siguiente script de Hive, llamado "partitioncarevents.hql", se usa para crear particiones y se encuentra en la carpeta "\demo\src\connectedcar\scripts" del archivo zip descargado.</span><span class="sxs-lookup"><span data-stu-id="2854c-290">The following Hive script, named "partitioncarevents.hql", is used for partitioning and is located in the "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 
    
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

<span data-ttu-id="2854c-291">Una vez que se ejecute correctamente la canalización, verá las siguientes particiones generadas en la cuenta de almacenamiento en el contenedor "connectedcar".</span><span class="sxs-lookup"><span data-stu-id="2854c-291">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Salida con particiones](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig12-vehicle-telematics-partitioned-output.png)

<span data-ttu-id="2854c-293">*Ilustración 12: Salida con particiones*</span><span class="sxs-lookup"><span data-stu-id="2854c-293">*Figure 12 - Partitioned Output*</span></span>

<span data-ttu-id="2854c-294">Los datos se han optimizado, ahora son más fáciles de administrar y están listos para su posterior procesamiento con el fin de obtener información de lote completa.</span><span class="sxs-lookup"><span data-stu-id="2854c-294">The data is now optimized, is more manageable and ready for further processing to gain rich batch insights.</span></span> 

## <a name="data-analysis"></a><span data-ttu-id="2854c-295">Análisis de datos</span><span class="sxs-lookup"><span data-stu-id="2854c-295">Data Analysis</span></span>
<span data-ttu-id="2854c-296">En esta sección, verá cómo se combinan Azure Stream Analytics, Azure Machine Learning, Azure Data Factory y Azure HDInsight para realizar un completo análisis avanzado sobre el mantenimiento del vehículo y los hábitos de conducción.</span><span class="sxs-lookup"><span data-stu-id="2854c-296">In this section, you see how to combine Azure Stream Analytics, Azure Machine Learning, Azure Data Factory, and Azure HDInsight for rich advanced analytics on vehicle health and driving habits.</span></span> <span data-ttu-id="2854c-297">Hay tres subsecciones aquí:</span><span class="sxs-lookup"><span data-stu-id="2854c-297">There are three subsections here:</span></span>

1. <span data-ttu-id="2854c-298">**Aprendizaje automático**: esta subsección contiene información sobre el experimento de detección de anomalías que hemos usado en esta solución para predecir los vehículos que requieren mantenimiento y vehículos que precisan una retirada por problemas de seguridad.</span><span class="sxs-lookup"><span data-stu-id="2854c-298">**Machine Learning**: This subsection contains information on the anomaly detection experiment that we have used in this solution to predict vehicles requiring servicing maintenance and vehicles requiring recalls due to safety issues.</span></span>
2. <span data-ttu-id="2854c-299">**Análisis en tiempo real**: esta subsección contiene información relacionada con el análisis en tiempo real a través del lenguaje de consulta de Stream Analytics y poniendo en funcionamiento el experimento de aprendizaje automático en tiempo real usando una aplicación personalizada.</span><span class="sxs-lookup"><span data-stu-id="2854c-299">**Real-time analysis**: This subsection contains information regarding the real-time analytics using the Stream Analytics Query Language and operationalizing the machine learning experiment in real time using a custom application.</span></span>
3. <span data-ttu-id="2854c-300">**Análisis de lotes**: esta subsección contiene información acerca de la transformación y el procesamiento de los datos del lote con Azure HDInsight y Azure Machine Learning aplicado a través de Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="2854c-300">**Batch analysis**: This subsection contains information regarding the transforming and processing of the batch data using Azure HDInsight and Azure Machine Learning operationalized by Azure Data Factory.</span></span>

### <a name="machine-learning"></a><span data-ttu-id="2854c-301">Aprendizaje automático</span><span class="sxs-lookup"><span data-stu-id="2854c-301">Machine Learning</span></span>
<span data-ttu-id="2854c-302">Nuestro objetivo es predecir los vehículos que requieren mantenimiento o retirada según ciertas estadísticas de estado.</span><span class="sxs-lookup"><span data-stu-id="2854c-302">Our goal here is to predict the vehicles that require maintenance or recall based on certain heath statistics.</span></span> <span data-ttu-id="2854c-303">Se realizan las suposiciones siguientes</span><span class="sxs-lookup"><span data-stu-id="2854c-303">We make the following assumptions</span></span>

* <span data-ttu-id="2854c-304">Los vehículos requieren **servicio de mantenimiento**cuando se cumple una de las tres condiciones siguientes:</span><span class="sxs-lookup"><span data-stu-id="2854c-304">If one of the following three conditions are true, the vehicles require **servicing maintenance**:</span></span>
  
  * <span data-ttu-id="2854c-305">Presión de los neumáticos es baja</span><span class="sxs-lookup"><span data-stu-id="2854c-305">Tire pressure is low</span></span>
  * <span data-ttu-id="2854c-306">Nivel de aceite del motor es bajo</span><span class="sxs-lookup"><span data-stu-id="2854c-306">Engine oil level is low</span></span>
  * <span data-ttu-id="2854c-307">Temperatura del motor es alta</span><span class="sxs-lookup"><span data-stu-id="2854c-307">Engine temperature is high</span></span>
* <span data-ttu-id="2854c-308">Los vehículos pueden tener un **problema de seguridad** y requieren **retirada** cuando se cumple una de las siguientes condiciones:</span><span class="sxs-lookup"><span data-stu-id="2854c-308">If one of the following conditions are true, the vehicles may have a **safety issue** and require **recall**:</span></span>
  
  * <span data-ttu-id="2854c-309">Temperatura del motor es alta, pero la temperatura exterior es baja</span><span class="sxs-lookup"><span data-stu-id="2854c-309">Engine temperature is high but outside temperature is low</span></span>
  * <span data-ttu-id="2854c-310">Temperatura del motor es baja, pero la temperatura exterior es alta</span><span class="sxs-lookup"><span data-stu-id="2854c-310">Engine temperature is low but outside temperature is high</span></span>

<span data-ttu-id="2854c-311">En función de los requisitos anteriores, hemos creado dos modelos independientes para detectar anomalías, uno para la detección de mantenimiento del vehículo y otro para la detección de retirada del vehículo.</span><span class="sxs-lookup"><span data-stu-id="2854c-311">Based on the previous requirements, we have created two separate models to detect anomalies, one for vehicle maintenance detection, and one for vehicle recall detection.</span></span> <span data-ttu-id="2854c-312">En ambos modelos, se usa el algoritmo integrado de análisis de componentes principales (PCA) para la detección de anomalías.</span><span class="sxs-lookup"><span data-stu-id="2854c-312">In both these models, the built-in Principal Component Analysis (PCA) algorithm is used for anomaly detection.</span></span> 

<span data-ttu-id="2854c-313">**Modelo de detección de mantenimiento**</span><span class="sxs-lookup"><span data-stu-id="2854c-313">**Maintenance detection model**</span></span>

<span data-ttu-id="2854c-314">Si alguno de los tres indicadores (presión de los neumáticos, aceite del motor o temperatura del motor) cumple su condición respectiva, el modelo de detección de mantenimiento informará sobre una anomalía.</span><span class="sxs-lookup"><span data-stu-id="2854c-314">If one of three indicators - tire pressure, engine oil, or engine temperature - satisfies its respective condition, the maintenance detection model reports an anomaly.</span></span> <span data-ttu-id="2854c-315">Como resultado, solo necesitamos tener en cuenta estas tres variables en la creación del modelo.</span><span class="sxs-lookup"><span data-stu-id="2854c-315">As a result, we only need to consider these three variables in building the model.</span></span> <span data-ttu-id="2854c-316">En nuestro experimento en Azure Machine Learning, primero usamos el módulo **Seleccionar columnas en conjunto de datos** para extraer estas tres variables.</span><span class="sxs-lookup"><span data-stu-id="2854c-316">In our experiment in Azure Machine Learning, we first use a **Select Columns in Dataset** module to extract these three variables.</span></span> <span data-ttu-id="2854c-317">A continuación, usamos el módulo de detección de anomalías basado en PCA para generar el modelo de detección de anomalías.</span><span class="sxs-lookup"><span data-stu-id="2854c-317">Next we use the PCA-based anomaly detection module to build the anomaly detection model.</span></span> 

<span data-ttu-id="2854c-318">El análisis de componentes principales (PCA) es una técnica establecida en aprendizaje automático que se puede aplicar a la selección de características, clasificación y detección de anomalías.</span><span class="sxs-lookup"><span data-stu-id="2854c-318">Principal Component Analysis (PCA) is an established technique in machine learning that can be applied to feature selection, classification, and anomaly detection.</span></span> <span data-ttu-id="2854c-319">PCA convierte un conjunto de casos con variables posiblemente correlacionadas, en un conjunto de valores denominados componentes principales.</span><span class="sxs-lookup"><span data-stu-id="2854c-319">PCA converts a set of case containing possibly correlated variables, into a set of values called principal components.</span></span> <span data-ttu-id="2854c-320">La idea clave de modelado basado en PCA es proyectar los datos en un espacio dimensional inferior, para que las características y las anomalías se puedan identificar más fácilmente.</span><span class="sxs-lookup"><span data-stu-id="2854c-320">The key idea of PCA-based modeling is to project data onto a lower-dimensional space so that features and anomalies can be more easily identified.</span></span>

<span data-ttu-id="2854c-321">Para cada entrada nueva en el modelo de detección, el detector de anomalías calcula su proyección de los vectores propios en primer lugar y, a continuación, calcula el error de reconstrucción normalizado.</span><span class="sxs-lookup"><span data-stu-id="2854c-321">For each new input to  the detection model, the anomaly detector first computes its projection on the eigenvectors, and then computes the normalized reconstruction error.</span></span> <span data-ttu-id="2854c-322">Este error normalizado es la puntuación de anomalías.</span><span class="sxs-lookup"><span data-stu-id="2854c-322">This normalized error is the anomaly score.</span></span> <span data-ttu-id="2854c-323">Cuanto mayor sea el error, más errónea es la instancia.</span><span class="sxs-lookup"><span data-stu-id="2854c-323">The higher the error, the more anomalous the instance is.</span></span> 

<span data-ttu-id="2854c-324">En el problema de detección de mantenimiento, cada registro se puede considerar como un punto en un espacio de 3 dimensiones definido por las coordenadas de presión de los neumáticos, aceite del motor y temperatura del motor.</span><span class="sxs-lookup"><span data-stu-id="2854c-324">In the maintenance detection problem, each record can be considered as a point in a 3-dimensional space defined by tire pressure, engine oil, and engine temperature coordinates.</span></span> <span data-ttu-id="2854c-325">Para capturar estas anomalías, podemos proyectar los datos originales en un espacio de 3 dimensiones o de 2 dimensiones con PCA.</span><span class="sxs-lookup"><span data-stu-id="2854c-325">To capture these anomalies, we can project the original data in the 3-dimensional space onto a 2-dimensional space using PCA.</span></span> <span data-ttu-id="2854c-326">Por lo tanto, establecemos el parámetro Número de componentes para usar en PCA con el valor 2.</span><span class="sxs-lookup"><span data-stu-id="2854c-326">Thus, we set the parameter Number of components to use in PCA to be 2.</span></span> <span data-ttu-id="2854c-327">Este parámetro desempeña un rol importante en la aplicación de la detección de anomalías basada en PCA.</span><span class="sxs-lookup"><span data-stu-id="2854c-327">This parameter plays an important role in applying PCA-based anomaly detection.</span></span> <span data-ttu-id="2854c-328">Después de proyectar datos con PCA, podemos identificar más fácilmente estas anomalías.</span><span class="sxs-lookup"><span data-stu-id="2854c-328">After projecting data using PCA, we can identify these anomalies more easily.</span></span>

<span data-ttu-id="2854c-329">**Modelo de detección de anomalías de retirada** : en el modelo de detección de anomalías de retirada, usamos los módulos Seleccionar columnas en conjunto de datos y de detección de anomalías basado en PCA de forma similar.</span><span class="sxs-lookup"><span data-stu-id="2854c-329">**Recall anomaly detection model** In the recall anomaly detection model, we use the Select Columns in Dataset and PCA-based anomaly detection modules in a similar way.</span></span> <span data-ttu-id="2854c-330">En concreto, en primer lugar extraemos tres variables: temperatura del motor, temperatura exterior y velocidad, usando el módulo **Seleccionar columnas en conjunto de datos** .</span><span class="sxs-lookup"><span data-stu-id="2854c-330">Specifically, we first extract three variables - engine temperature, outside temperature, and speed - using the **Select Columns in Dataset** module.</span></span> <span data-ttu-id="2854c-331">También incluimos la variable de velocidad ya que la temperatura del motor normalmente está correlacionada con la velocidad.</span><span class="sxs-lookup"><span data-stu-id="2854c-331">We also include the speed variable since the engine temperature typically is correlated to the speed.</span></span> <span data-ttu-id="2854c-332">A continuación, usamos el módulo de detección de anomalías basado en PCA para proyectar los datos desde el espacio de 3 dimensiones en un espacio tridimensional de 2.</span><span class="sxs-lookup"><span data-stu-id="2854c-332">Next we use PCA-based anomaly detection module to project the data from the 3-dimensional space onto a 2-dimensional space.</span></span> <span data-ttu-id="2854c-333">Se cumplen los criterios de retirada, por lo que se requiere la retirada del vehículo cuando existe una correlación negativa muy alta entre la temperatura del motor y la temperatura exterior.</span><span class="sxs-lookup"><span data-stu-id="2854c-333">The recall criteria are satisfied and so the vehicle requires recall when engine temperature and outside temperature are highly negatively correlated.</span></span> <span data-ttu-id="2854c-334">A través del algoritmo de detección de anomalías basado en PCA, podemos capturar las anomalías después de realizar el PCA.</span><span class="sxs-lookup"><span data-stu-id="2854c-334">Using PCA-based anomaly detection algorithm, we can capture the anomalies after performing PCA.</span></span> 

<span data-ttu-id="2854c-335">Durante el entrenamiento de ambos modelos, es necesario usar datos normales que no requieran mantenimiento o retirada para los datos de entrada de aprendizaje del modelo de detección de anomalías basado en PCA.</span><span class="sxs-lookup"><span data-stu-id="2854c-335">When training either model, we need to use normal data, which does not require maintenance or recall as the input data to train the PCA-based anomaly detection model.</span></span> <span data-ttu-id="2854c-336">En el experimento de puntuación, usamos el modelo de detección de anomalías entrenado para detectar si el vehículo requiere mantenimiento o retirada.</span><span class="sxs-lookup"><span data-stu-id="2854c-336">In the scoring experiment, we use the trained anomaly detection model to detect whether or not the vehicle requires maintenance or recall.</span></span> 

### <a name="real-time-analysis"></a><span data-ttu-id="2854c-337">Análisis en tiempo real</span><span class="sxs-lookup"><span data-stu-id="2854c-337">Real-time analysis</span></span>
<span data-ttu-id="2854c-338">La siguiente consulta SQL de Stream Analytics se utiliza para obtener el promedio de todos los parámetros importantes del vehículo como la velocidad del vehículo, el nivel de combustible, la temperatura del motor, el kilometraje, la presión de los neumáticos, el nivel de aceite del motor y otros.</span><span class="sxs-lookup"><span data-stu-id="2854c-338">The following Stream Analytics SQL Query is used to get the average of all the important vehicle parameters like vehicle speed, fuel level, engine temperature, odometer reading, tire pressure, engine oil level, and others.</span></span> <span data-ttu-id="2854c-339">Los promedios se utilizan para detectar anomalías, emitir alertas y determinar las condiciones generales de mantenimiento de los vehículos utilizados en una región específica y, luego, se correlacionan con datos demográficos.</span><span class="sxs-lookup"><span data-stu-id="2854c-339">The averages are used to detect anomalies, issue alerts, and determine the overall health conditions of vehicles operated in specific region and then correlate it to demographics.</span></span> 

![Consulta de Stream Analytics para el procesamiento en tiempo real](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig13-vehicle-telematics-stream-analytics-query-for-real-time-processing.png)

<span data-ttu-id="2854c-341">*Ilustración 13: Consulta de Stream Analytics para el procesamiento en tiempo real*</span><span class="sxs-lookup"><span data-stu-id="2854c-341">*Figure 13 – Stream Analytics query for real-time processing*</span></span>

<span data-ttu-id="2854c-342">Todos los promedios se calculan sobre una TumblingWindow de 3 segundos.</span><span class="sxs-lookup"><span data-stu-id="2854c-342">All the averages are calculated over a 3-second TumblingWindow.</span></span> <span data-ttu-id="2854c-343">En este caso estamos usando TubmlingWindow puesto que necesitamos que los intervalos de tiempo no se superpongan y sean contiguos.</span><span class="sxs-lookup"><span data-stu-id="2854c-343">We are using TubmlingWindow in this case since we require non-overlapping and contiguous time intervals.</span></span> 

<span data-ttu-id="2854c-344">Para más información sobre todas las funcionalidades basadas en ventanas de Azure Stream Analytics, haga clic en [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span><span class="sxs-lookup"><span data-stu-id="2854c-344">To learn more about all the "Windowing" capabilities in Azure Stream Analytics, click [Windowing (Azure Stream Analytics)](https://msdn.microsoft.com/library/azure/dn835019.aspx).</span></span>

<span data-ttu-id="2854c-345">**Predicción en tiempo real**</span><span class="sxs-lookup"><span data-stu-id="2854c-345">**Real-time prediction**</span></span>

<span data-ttu-id="2854c-346">Como parte de la solución se incluye una aplicación que ponga en funcionamiento el modelo de aprendizaje automático en tiempo real.</span><span class="sxs-lookup"><span data-stu-id="2854c-346">An application is included as part of the solution to operationalize the machine learning model in real time.</span></span> <span data-ttu-id="2854c-347">Esta aplicación denominada "RealTimeDashboardApp" se crea y configura como parte de la implementación de la solución.</span><span class="sxs-lookup"><span data-stu-id="2854c-347">This application called “RealTimeDashboardApp” is created and configured as part of the solution deployment.</span></span> <span data-ttu-id="2854c-348">Esta aplicación hace lo siguiente:</span><span class="sxs-lookup"><span data-stu-id="2854c-348">The application performs the following:</span></span>

1. <span data-ttu-id="2854c-349">Escucha a una instancia de Event Hubs donde Stream Analytics publica los eventos en un patrón de forma continua.</span><span class="sxs-lookup"><span data-stu-id="2854c-349">Listens to an Event Hub instance where Stream Analytics is publishing the events in a pattern continuously.</span></span> <span data-ttu-id="2854c-350">![Consulta de Stream Analytics para la publicación de datos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figura 14: Consulta de Stream Analytics para publicar los datos en una instancia de Centros de eventos de salida*</span><span class="sxs-lookup"><span data-stu-id="2854c-350">![Stream Analytics query for publishing the data](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig14-vehicle-telematics-stream-analytics-query-for-publishing.png) *Figure 14 – Stream Analytics query for publishing the data to an output Event Hub instance*</span></span> 
2. <span data-ttu-id="2854c-351">Para cada evento que recibe esta aplicación:</span><span class="sxs-lookup"><span data-stu-id="2854c-351">For every event that this application receives:</span></span> 
   
   * <span data-ttu-id="2854c-352">Procesa los datos con el punto de conexión de puntuación de solicitud-respuesta de Aprendizaje automático (RRS).</span><span class="sxs-lookup"><span data-stu-id="2854c-352">Processes the data using Machine Learning Request-Response Scoring (RRS) endpoint.</span></span> <span data-ttu-id="2854c-353">El punto de conexión RRS se publica automáticamente como parte de la implementación.</span><span class="sxs-lookup"><span data-stu-id="2854c-353">The RRS endpoint is automatically published as part of the deployment.</span></span>
   * <span data-ttu-id="2854c-354">La salida RRS se publica en un conjunto de datos de Power BI mediante las API de inserción.</span><span class="sxs-lookup"><span data-stu-id="2854c-354">The RRS output is published to a Power BI dataset using the push APIs.</span></span>

<span data-ttu-id="2854c-355">Este patrón también es aplicable a aquellos escenarios en los que desea integrar una aplicación de línea de negocio con el flujo de análisis en tiempo real para escenarios como alertas, notificaciones, mensajerías, etc.</span><span class="sxs-lookup"><span data-stu-id="2854c-355">This pattern is also applicable to scenarios in which you want to integrate a Line of Business (LoB) application with the real-time analytics flow, for scenarios such as alerts, notifications, and messaging.</span></span>

<span data-ttu-id="2854c-356">Haga clic en la [descarga de RealtimeDashboardApp](http://go.microsoft.com/fwlink/?LinkId=717078) para descargar la solución de Visual Studio de RealtimeDashboardApp para las personalizaciones.</span><span class="sxs-lookup"><span data-stu-id="2854c-356">Click [RealtimeDashboardApp download](http://go.microsoft.com/fwlink/?LinkId=717078) to download the RealtimeDashboardApp Visual Studio solution for customizations.</span></span> 

<span data-ttu-id="2854c-357">**Para ejecutar la aplicación de panel en tiempo real**</span><span class="sxs-lookup"><span data-stu-id="2854c-357">**To execute the Real-time Dashboard Application**</span></span>
1. <span data-ttu-id="2854c-358">Extraer y guardar localmente la carpeta ![RealtimeDashboardApp](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Ilustración 16: Carpeta RealtimeDashboardApp*</span><span class="sxs-lookup"><span data-stu-id="2854c-358">Extract and save locally ![RealtimeDashboardApp folder](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig16-vehicle-telematics-realtimedashboardapp-folder.png) *Figure 16 – RealtimeDashboardApp folder*</span></span>  
2. <span data-ttu-id="2854c-359">Ejecute la aplicación RealtimeDashboardApp.exe.</span><span class="sxs-lookup"><span data-stu-id="2854c-359">Execute the application RealtimeDashboardApp.exe</span></span>
3. <span data-ttu-id="2854c-360">Proporcione credenciales válidas de Power BI, inicie sesión y haga clic en Aceptar</span><span class="sxs-lookup"><span data-stu-id="2854c-360">Provide valid Power BI credentials, sign in and click Accept</span></span> ![Inicio de sesión de la aplicación del panel en tiempo real en Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17a-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) ![Inicio de sesión de finalización de la aplicación del panel en tiempo real en Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig17b-vehicle-telematics-realtimedashboardapp-sign-in-to-powerbi.png) 

<span data-ttu-id="2854c-363">*Ilustración 17: RealtimeDashboardApp: Inicio de sesión en Power BI*</span><span class="sxs-lookup"><span data-stu-id="2854c-363">*Figure 17 – RealtimeDashboardApp: Sign-in to Power BI*</span></span>

>[!NOTE] 
><span data-ttu-id="2854c-364">Si desea vaciar el conjunto de datos de Power BI, ejecute RealtimeDashboardApp con el parámetro "flushdata":</span><span class="sxs-lookup"><span data-stu-id="2854c-364">If you want to flush the Power BI dataset, execute the RealtimeDashboardApp with the "flushdata" parameter:</span></span> 

    RealtimeDashboardApp.exe -flushdata


### <a name="batch-analysis"></a><span data-ttu-id="2854c-365">Análisis por lotes</span><span class="sxs-lookup"><span data-stu-id="2854c-365">Batch analysis</span></span>
<span data-ttu-id="2854c-366">El objetivo aquí es mostrar cómo Contoso Motors usa las funcionalidades de proceso de Azure para aprovechar los macrodatos, con el fin de obtener información valiosa sobre patrones de conducción, comportamientos de uso y estado de los vehículos.</span><span class="sxs-lookup"><span data-stu-id="2854c-366">The goal here is to show how Contoso Motors utilizes the Azure compute capabilities to harness big data to gain rich insights on driving pattern, usage behavior, and vehicle health.</span></span> <span data-ttu-id="2854c-367">Con esto es posible:</span><span class="sxs-lookup"><span data-stu-id="2854c-367">This makes it possible to:</span></span>

* <span data-ttu-id="2854c-368">Mejorar la experiencia del cliente y abaratar los costos de la misma, proporcionando información sobre hábitos de conducción y formas de conducir que hagan un uso más eficiente del combustible</span><span class="sxs-lookup"><span data-stu-id="2854c-368">Improve the customer experience and make it cheaper by providing insights on driving habits and fuel efficient driving behaviors</span></span>
* <span data-ttu-id="2854c-369">Aprender de forma proactiva acerca de los clientes y sus patrones de conducción para encauzar la toma de decisiones empresariales y proporcionar servicios y productos inmejorables</span><span class="sxs-lookup"><span data-stu-id="2854c-369">Learn proactively about customers and their driving patters to govern business decisions and provide the best in class products & services</span></span>

<span data-ttu-id="2854c-370">En esta solución, nuestro destino son las siguientes métricas:</span><span class="sxs-lookup"><span data-stu-id="2854c-370">In this solution, we are targeting the following metrics:</span></span>

1. <span data-ttu-id="2854c-371">**Comportamiento agresivo al volante**: identifica la tendencia de los modelos, ubicaciones, condiciones de circulación y época del año para obtener información sobre un patrón de comportamiento agresivo al volante.</span><span class="sxs-lookup"><span data-stu-id="2854c-371">**Aggressive driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of the year to gain insights on aggressive driving patterns.</span></span> <span data-ttu-id="2854c-372">Contoso Motors puede usar esta información para campañas de marketing, dando lugar a seguros con nuevas características y prestaciones personalizadas y basados en el uso.</span><span class="sxs-lookup"><span data-stu-id="2854c-372">Contoso Motors can use these insights for marketing campaigns, driving new personalized features and usage-based insurance.</span></span>
2. <span data-ttu-id="2854c-373">**Comportamiento de conducción con consumo eficiente de combustible**: identifica la tendencia de los modelos, ubicaciones, condiciones de circulación y época del año para obtener información sobre un patrón de comportamiento de conducción con consumo eficiente de combustible.</span><span class="sxs-lookup"><span data-stu-id="2854c-373">**Fuel efficient driving behavior**: Identifies the trend of the models, locations, driving conditions, and time of the year to gain insights on fuel efficient driving patterns.</span></span> <span data-ttu-id="2854c-374">Contoso Motors puede usar esta información para campañas de marketing, dando lugar a nuevas prestaciones e información proactiva a los conductores sobre hábitos de conducción más económicos y ecológicos.</span><span class="sxs-lookup"><span data-stu-id="2854c-374">Contoso Motors can use these insights for marketing campaigns, driving new features and proactive reporting to the drivers for cost effective and environment friendly driving habits.</span></span> 
3. <span data-ttu-id="2854c-375">**Modelos de retirada**: identifica los modelos que hay que retirar, poniendo en funcionamiento los experimentos de aprendizaje automático de detección de anomalías</span><span class="sxs-lookup"><span data-stu-id="2854c-375">**Recall models**: Identifies models requiring recalls by operationalizing the anomaly detection machine learning experiment</span></span>

<span data-ttu-id="2854c-376">Veamos cada una de estas métricas en detalle.</span><span class="sxs-lookup"><span data-stu-id="2854c-376">Let's look into the details of each of these metrics,</span></span>

<span data-ttu-id="2854c-377">**Patrón de comportamiento agresivo al volante**</span><span class="sxs-lookup"><span data-stu-id="2854c-377">**Aggressive driving pattern**</span></span>

<span data-ttu-id="2854c-378">Los datos de diagnóstico y las señales de vehículo se procesan en la canalización con el nombre "AggresiveDrivingPatternPipeline" mediante Hive para determinar los modelos, ubicación, vehículo, condiciones de conducción y otros parámetros que exhibe el patrón de comportamiento agresivo al volante.</span><span class="sxs-lookup"><span data-stu-id="2854c-378">The partitioned vehicle signals and diagnostic data are processed in the pipeline named "AggresiveDrivingPatternPipeline" using Hive to determine the models, location, vehicle, driving conditions, and other parameters that exhibits aggressive driving pattern.</span></span>

<span data-ttu-id="2854c-379">![Flujo de trabajo de patrón de conducción agresiva](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Ilustración 18: Flujo de trabajo de patrón de conducción agresiva*</span><span class="sxs-lookup"><span data-stu-id="2854c-379">![Aggressive driving pattern workflow](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig18-vehicle-telematics-aggressive-driving-pattern.png) 
*Figure 18 – Aggressive driving pattern workflow*</span></span>


<span data-ttu-id="2854c-380">***Consulta de Hive para el patrón de comportamiento agresivo al volante***</span><span class="sxs-lookup"><span data-stu-id="2854c-380">***Aggressive driving pattern Hive query***</span></span>

<span data-ttu-id="2854c-381">El script de Hive denominado "aggresivedriving.hql" se usa para analizar el patrón de comportamiento agresivo al volante se encuentra en la carpeta "\demo\src\connectedcar\scripts" en el archivo zip descargado.</span><span class="sxs-lookup"><span data-stu-id="2854c-381">The Hive script named "aggresivedriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 

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


<span data-ttu-id="2854c-382">Usa la combinación de la posición del cambio de marcha del vehículo, estado del pedal de freno y la velocidad para detectar comportamientos de conducción temeraria o agresiva basándose en el patrón de frenado a alta velocidad.</span><span class="sxs-lookup"><span data-stu-id="2854c-382">It uses the combination of vehicle's transmission gear position, brake pedal status, and speed to detect reckless/aggressive driving behavior based on braking pattern at high speed.</span></span> 

<span data-ttu-id="2854c-383">Una vez que se ejecute correctamente la canalización, verá las siguientes particiones generadas en la cuenta de almacenamiento en el contenedor "connectedcar".</span><span class="sxs-lookup"><span data-stu-id="2854c-383">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Resultados de AggressiveDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-aggressive-driving-pattern-output.png) 

<span data-ttu-id="2854c-385">*Ilustración 19: Resultados de AggressiveDrivingPatternPipeline*</span><span class="sxs-lookup"><span data-stu-id="2854c-385">*Figure 19 – AggressiveDrivingPatternPipeline output*</span></span>

<span data-ttu-id="2854c-386">**Patrón de conducción con consumo eficiente de combustible**</span><span class="sxs-lookup"><span data-stu-id="2854c-386">**Fuel efficient driving pattern**</span></span>

<span data-ttu-id="2854c-387">Las particiones de las señales del vehículo y los datos de diagnóstico se procesan en la canalización llamada "FuelEfficientDrivingPatternPipeline".</span><span class="sxs-lookup"><span data-stu-id="2854c-387">The partitioned vehicle signals and diagnostic data are processed in the pipeline named "FuelEfficientDrivingPatternPipeline".</span></span> <span data-ttu-id="2854c-388">Hive se usa para determinar los modelos, ubicación, vehículo, condiciones de conducción y otras propiedades que muestren un patrón de conducción con consumo eficiente de combustible.</span><span class="sxs-lookup"><span data-stu-id="2854c-388">Hive is used to determine the models, location, vehicle, driving conditions, and other properties that exhibit fuel efficient driving pattern.</span></span>

![Patrón de conducción con consumo eficiente de combustible](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig19-vehicle-telematics-fuel-efficient-driving-pattern.png) 

<span data-ttu-id="2854c-390">*Ilustración 20: Flujo de trabajo del patrón de conducción con consumo eficiente de combustible*</span><span class="sxs-lookup"><span data-stu-id="2854c-390">*Figure 20 – Fuel-efficient driving pattern workflow*</span></span>

<span data-ttu-id="2854c-391">***Consulta de Hive para el patrón de conducción con consumo eficiente de combustible***</span><span class="sxs-lookup"><span data-stu-id="2854c-391">***Fuel efficient driving pattern Hive query***</span></span>

<span data-ttu-id="2854c-392">El script de Hive denominado "fuelefficientdriving.hql" se usa para analizar el patrón de comportamiento agresivo al volante se encuentra en la carpeta "\demo\src\connectedcar\scripts" en el archivo zip descargado.</span><span class="sxs-lookup"><span data-stu-id="2854c-392">The Hive script named "fuelefficientdriving.hql" used for analyzing aggressive driving condition pattern is located at "\demo\src\connectedcar\scripts" folder of the downloaded zip.</span></span> 

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


<span data-ttu-id="2854c-393">Usa la combinación de la posición del cambio de marcha del vehículo, estado del pedal de freno, velocidad y posición del pedal de acelerador para detectar comportamientos de conducción con consumo eficiente de combustible basándose en patrones de aceleración, frenada y velocidad.</span><span class="sxs-lookup"><span data-stu-id="2854c-393">It uses the combination of vehicle's transmission gear position, brake pedal status, speed, and accelerator pedal position to detect fuel efficient driving behavior based on acceleration, braking, and speed patterns.</span></span> 

<span data-ttu-id="2854c-394">Una vez que se ejecute correctamente la canalización, verá las siguientes particiones generadas en la cuenta de almacenamiento en el contenedor "connectedcar".</span><span class="sxs-lookup"><span data-stu-id="2854c-394">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Resultados de FuelEfficientDrivingPatternPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig20-vehicle-telematics-fuel-efficient-driving-pattern-output.png) 

<span data-ttu-id="2854c-396">*Ilustración 21: Resultados de FuelEfficientDrivingPatternPipeline*</span><span class="sxs-lookup"><span data-stu-id="2854c-396">*Figure 21 – FuelEfficientDrivingPatternPipeline output*</span></span>

<span data-ttu-id="2854c-397">**Predicciones de retirada**</span><span class="sxs-lookup"><span data-stu-id="2854c-397">**Recall Predictions**</span></span>

<span data-ttu-id="2854c-398">El experimento de aprendizaje automático se proporciona y publica como un servicio web como parte de la implementación de la solución.</span><span class="sxs-lookup"><span data-stu-id="2854c-398">The machine learning experiment is provisioned and published as a web service as part of the solution deployment.</span></span> <span data-ttu-id="2854c-399">Se aprovecha el punto de conexión de la puntuación del lote de este flujo de trabajo a través del registro como un servicio vinculado a Factoría de datos, y puesto en funcionamiento a través del uso de la actividad de puntuación de lote de Factoría de datos.</span><span class="sxs-lookup"><span data-stu-id="2854c-399">The batch scoring end point is leveraged in this workflow, registered as a data factory linked service and operationalized using data factory batch scoring activity.</span></span>

![Punto de conexión de Machine Learning](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig21-vehicle-telematics-machine-learning-endpoint.png) 

<span data-ttu-id="2854c-401">*Ilustración 22: Punto de conexión de Machine Learning registrado como un servicio vinculado en Factoría de datos*</span><span class="sxs-lookup"><span data-stu-id="2854c-401">*Figure 22 – Machine learning endpoint registered as a linked service in data factory*</span></span>

<span data-ttu-id="2854c-402">El servicio vinculado registrado se usa en DetectAnomalyPipeline para puntuar los datos usando el modelo de detección de anomalías.</span><span class="sxs-lookup"><span data-stu-id="2854c-402">The registered linked service is used in the DetectAnomalyPipeline to score the data using the anomaly detection model.</span></span> 

![Actividad de puntuación por lotes de Azure Machine Learning en Factoría de datos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig22-vehicle-telematics-aml-batch-scoring.png) 

<span data-ttu-id="2854c-404">*Ilustración 23: Actividad de puntuación por lotes de Azure Machine Learning en Data Factory*</span><span class="sxs-lookup"><span data-stu-id="2854c-404">*Figure 23 – Azure Machine Learning Batch Scoring activity in data factory*</span></span> 

<span data-ttu-id="2854c-405">Hay algunos pasos que se realizan en esta canalización para la preparación de los datos para que puedan usarse con el servicio web de puntuación de lote.</span><span class="sxs-lookup"><span data-stu-id="2854c-405">There are few steps performed in this pipeline for data preparation so that it can be operationalized with the batch scoring web service.</span></span> 

![DetectAnomalyPipeline para predecir la necesidad de retirada de vehículos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig23-vehicle-telematics-pipeline-predicting-recalls.png) 

<span data-ttu-id="2854c-407">*Ilustración 24: DetectAnomalyPipeline para predecir la necesidad de retirada de vehículos*</span><span class="sxs-lookup"><span data-stu-id="2854c-407">*Figure 24 – DetectAnomalyPipeline for predicting vehicles requiring recalls*</span></span> 

<span data-ttu-id="2854c-408">***Consulta de Hive de detección de anomalías***</span><span class="sxs-lookup"><span data-stu-id="2854c-408">***Anomaly detection Hive query***</span></span>

<span data-ttu-id="2854c-409">Una vez completada la puntuación, se usa una actividad de HDInsight para procesar y agregar los datos que están clasificados como anomalías por el modelo con una puntuación de probabilidad de 0,60 o superior.</span><span class="sxs-lookup"><span data-stu-id="2854c-409">Once the scoring is completed, an HDInsight activity is used to process and aggregate the data that are categorized as anomalies by the model with a probability score of 0.60 or higher.</span></span>

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


<span data-ttu-id="2854c-410">Una vez que se ejecute correctamente la canalización, verá las siguientes particiones generadas en la cuenta de almacenamiento en el contenedor "connectedcar".</span><span class="sxs-lookup"><span data-stu-id="2854c-410">Once the pipeline is executed successfully, you see the following partitions generated in your storage account under the "connectedcar" container.</span></span>

![Resultados de DetectAnomalyPipeline](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig24-vehicle-telematics-detect-anamoly-pipeline-output.png) 

<span data-ttu-id="2854c-412">*Ilustración 25: Resultados de DetectAnomalyPipeline*</span><span class="sxs-lookup"><span data-stu-id="2854c-412">*Figure 25 – DetectAnomalyPipeline output*</span></span>

## <a name="publish"></a><span data-ttu-id="2854c-413">Publicar</span><span class="sxs-lookup"><span data-stu-id="2854c-413">Publish</span></span>

### <a name="real-time-analysis"></a><span data-ttu-id="2854c-414">Análisis en tiempo real</span><span class="sxs-lookup"><span data-stu-id="2854c-414">Real-time analysis</span></span>
<span data-ttu-id="2854c-415">Una de las consultas en el trabajo de Stream Analytics publica los eventos en una instancia de Centro de eventos de resultados.</span><span class="sxs-lookup"><span data-stu-id="2854c-415">One of the queries in the Stream Analytics job publishes the events to an output Event Hub instance.</span></span> 

![Trabajo de Stream Analytics publica en una instancia de Centro de eventos de resultados](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig25-vehicle-telematics-stream-analytics-job-publishes-output-event-hub.png)

<span data-ttu-id="2854c-417">*Ilustración 26: Trabajo de Stream Analytics publica en una instancia de Centro de eventos de resultados*</span><span class="sxs-lookup"><span data-stu-id="2854c-417">*Figure 26 – Stream Analytics job publishes to an output Event Hub instance*</span></span>

![Consulta de Stream Analytics para publicar en la instancia de Centro de eventos de resultados](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig26-vehicle-telematics-stream-analytics-query-publish-output-event-hub.png)

<span data-ttu-id="2854c-419">*Ilustración 27: Consulta de Stream Analytics para publicar en la instancia de Centro de eventos de resultados*</span><span class="sxs-lookup"><span data-stu-id="2854c-419">*Figure 27 – Stream Analytics query to publish to the output Event Hub instance*</span></span>

<span data-ttu-id="2854c-420">Esta transmisión de eventos la consume la aplicación RealTimeDashboardApp que se incluye en la solución.</span><span class="sxs-lookup"><span data-stu-id="2854c-420">This stream of events is consumed by the RealTimeDashboardApp included in the solution.</span></span> <span data-ttu-id="2854c-421">Esta aplicación aprovecha el servicio web de solicitud-respuesta de Machine Learning para puntuar en tiempo real y publica los datos resultantes en un conjunto de datos de Power BI para su consumo.</span><span class="sxs-lookup"><span data-stu-id="2854c-421">This application leverages the Machine Learning Request-Response web service for real-time scoring and publishes the resultant data to a Power BI dataset for consumption.</span></span> 

### <a name="batch-analysis"></a><span data-ttu-id="2854c-422">Análisis por lotes</span><span class="sxs-lookup"><span data-stu-id="2854c-422">Batch analysis</span></span>
<span data-ttu-id="2854c-423">Los resultados del procesamiento por lote y en tiempo real se publican en las tablas de Base de datos SQL de Azure para su consumo.</span><span class="sxs-lookup"><span data-stu-id="2854c-423">The results of the batch and real-time processing are published to the Azure SQL Database tables for consumption.</span></span> <span data-ttu-id="2854c-424">El servidor y base de datos de Azure SQL y las tablas se crean automáticamente como parte del script de instalación.</span><span class="sxs-lookup"><span data-stu-id="2854c-424">The Azure SQL Server, Database, and the tables are created automatically as part of the setup script.</span></span> 

![Copia de los resultados de procesamiento por lotes en el flujo de trabajo de puestos de datos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig27-vehicle-telematics-batch-processing-results-copy-to-data-mart.png)

<span data-ttu-id="2854c-426">*Ilustración 28: Copia de los resultados de procesamiento por lotes en el flujo de trabajo de puestos de datos*</span><span class="sxs-lookup"><span data-stu-id="2854c-426">*Figure 28 – Batch processing results copy to data mart workflow*</span></span>

![Trabajo de Stream Analytics se publica en puestos de datos](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig28-vehicle-telematics-stream-analytics-job-publishes-to-data-mart.png)

<span data-ttu-id="2854c-428">*Ilustración 29: Trabajo de Stream Analytics se publica en puestos de datos*</span><span class="sxs-lookup"><span data-stu-id="2854c-428">*Figure 29 – Stream Analytics job publishes to data mart*</span></span>

![Ajuste de puesto de datos en el trabajo de Stream Analytics](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig29-vehicle-telematics-data-mart-setting-in-stream-analytics-job.png)

<span data-ttu-id="2854c-430">*Ilustración 30: Ajuste de puesto de datos en el trabajo de Stream Analytics*</span><span class="sxs-lookup"><span data-stu-id="2854c-430">*Figure 30 – Data mart setting in Stream Analytics job*</span></span>

## <a name="consume"></a><span data-ttu-id="2854c-431">Consumo</span><span class="sxs-lookup"><span data-stu-id="2854c-431">Consume</span></span>
<span data-ttu-id="2854c-432">Power BI ofrece a esta solución un panel completo para datos en tiempo real y visualizaciones de análisis predictivo.</span><span class="sxs-lookup"><span data-stu-id="2854c-432">Power BI gives this solution a rich dashboard for real-time data and predictive analytics visualizations.</span></span> 

<span data-ttu-id="2854c-433">Haga clic aquí para obtener instrucciones detalladas sobre cómo configurar los informes de Power BI y el panel.</span><span class="sxs-lookup"><span data-stu-id="2854c-433">Click here for detailed instructions on setting up the Power BI reports and the dashboard.</span></span> <span data-ttu-id="2854c-434">El panel final tiene este aspecto:</span><span class="sxs-lookup"><span data-stu-id="2854c-434">The final dashboard looks like this:</span></span>

![Panel de Power BI](./media/cortana-analytics-playbook-vehicle-telemetry-deep-dive/fig30-vehicle-telematics-powerbi-dashboard.png)

<span data-ttu-id="2854c-436">*Ilustración 31: Panel de Power BI*</span><span class="sxs-lookup"><span data-stu-id="2854c-436">*Figure 31 - Power BI Dashboard*</span></span>

## <a name="summary"></a><span data-ttu-id="2854c-437">Resumen</span><span class="sxs-lookup"><span data-stu-id="2854c-437">Summary</span></span>
<span data-ttu-id="2854c-438">Este documento contiene un desglose detallado de la solución de análisis de telemetría de vehículos.</span><span class="sxs-lookup"><span data-stu-id="2854c-438">This document contains a detailed drill-down of the Vehicle Telemetry Analytics Solution.</span></span> <span data-ttu-id="2854c-439">Se presenta un patrón de arquitectura lambda para análisis en tiempo real y de procesamiento por lotes con predicciones y acciones.</span><span class="sxs-lookup"><span data-stu-id="2854c-439">This showcases a lambda architecture pattern for real-time and batch analytics with predictions and actions.</span></span> <span data-ttu-id="2854c-440">Este patrón se aplica a una amplia gama de casos de uso que requieren análisis con ruta de acceso activa (en tiempo real) y la ruta de acceso frío (lote).</span><span class="sxs-lookup"><span data-stu-id="2854c-440">This pattern applies to a wide range of use cases that require hot path (real-time) and cold path (batch) analytics.</span></span> 

