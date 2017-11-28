---
title: "Stream Analytics: Giro de las credenciales de inicio de sesión para entradas y salidas | Microsoft Docs"
description: "Obtenga información acerca de cómo tooupdate hello las credenciales para el análisis de transmisiones entradas y salidas."
keywords: "credenciales de inicio de sesión"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 42ae83e1-cd33-49bb-a455-a39a7c151ea4
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: ac2374c539012b66ab390656c5750024e02f6bdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="rotate-login-credentials-for-inputs-and-outputs-in-stream-analytics-jobs"></a><span data-ttu-id="bbd4c-104">Giro de las credenciales de inicio de sesión para entradas y salidas de los trabajos de Análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="bbd4c-104">Rotate login credentials for inputs and outputs in Stream Analytics Jobs</span></span>
## <a name="abstract"></a><span data-ttu-id="bbd4c-105">Descripción breve</span><span class="sxs-lookup"><span data-stu-id="bbd4c-105">Abstract</span></span>
<span data-ttu-id="bbd4c-106">Análisis de transmisiones de Azure hoy no permite reemplazar las credenciales de hello en una entrada/salida mientras se ejecuta el trabajo de Hola.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-106">Azure Stream Analytics today doesn’t allow replacing hello credentials on an input/output while hello job is running.</span></span>

<span data-ttu-id="bbd4c-107">Mientras que los análisis de transmisiones de Azure admiten reanudar un trabajo desde el último resultado, deseamos tooshare Hola todo el proceso para minimizar el retardo de hello entre Hola detener y a partir del trabajo de Hola y rotación de credenciales de inicio de sesión de Hola.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-107">While Azure Stream Analytics does support resuming a job from last output, we wanted tooshare hello entire process for minimizing hello lag between hello stopping and starting of hello job and rotating hello login credentials.</span></span>

## <a name="part-1---prepare-hello-new-set-of-credentials"></a><span data-ttu-id="bbd4c-108">Parte 1: preparar el nuevo conjunto de credenciales de hello:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-108">Part 1 - Prepare hello new set of credentials:</span></span>
<span data-ttu-id="bbd4c-109">Esta parte es aplicable toohello después de entradas/salidas:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-109">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="bbd4c-110">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="bbd4c-110">Blob Storage</span></span>
* <span data-ttu-id="bbd4c-111">Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="bbd4c-111">Event Hubs</span></span>
* <span data-ttu-id="bbd4c-112">Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="bbd4c-112">SQL Database</span></span>
* <span data-ttu-id="bbd4c-113">Almacenamiento de tablas</span><span class="sxs-lookup"><span data-stu-id="bbd4c-113">Table Storage</span></span>

<span data-ttu-id="bbd4c-114">Para otras entradas/salidas, vaya a la Parte 2.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-114">For other inputs/outputs, proceed with Part 2.</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="bbd4c-115">Almacenamiento de blobs/almacenamiento de tablas</span><span class="sxs-lookup"><span data-stu-id="bbd4c-115">Blob storage/Table storage</span></span>
1. <span data-ttu-id="bbd4c-116">Vaya toohello extensión de almacenamiento en el portal de administración de Azure de hello:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-116">Go toohello Storage extention on hello Azure Management portal:</span></span>  
   ![graphic1][graphic1]
2. <span data-ttu-id="bbd4c-118">Busque utilizada por el trabajo de almacenamiento de Hola y vaya a ella:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-118">Locate hello storage used by your job and go into it:</span></span>  
   ![graphic2][graphic2]
3. <span data-ttu-id="bbd4c-120">Haga clic en el comando de hello administrar claves de acceso:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-120">Click hello Manage Access Keys command:</span></span>  
   ![graphic3][graphic3]
4. <span data-ttu-id="bbd4c-122">Entre la clave de acceso principal de Hola y Hola clave de acceso secundaria, **elegir Hola uno no utilizada por el trabajo**.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-122">Between hello Primary Access Key and hello Secondary Access Key, **pick hello one not used by your job**.</span></span>
5. <span data-ttu-id="bbd4c-123">Presione regenerar: </span><span class="sxs-lookup"><span data-stu-id="bbd4c-123">Hit regenerate:</span></span>  
   ![graphic4][graphic4]
6. <span data-ttu-id="bbd4c-125">Copie la clave de hello recién generado:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-125">Copy hello newly generated key:</span></span>  
   ![graphic5][graphic5]
7. <span data-ttu-id="bbd4c-127">Continuar tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-127">Continue tooPart 2.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="bbd4c-128">Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="bbd4c-128">Event hubs</span></span>
1. <span data-ttu-id="bbd4c-129">Vaya toohello extensión de Bus de servicio en el portal de administración de Azure de hello:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-129">Go toohello Service Bus extension on hello Azure Management portal:</span></span>  
   ![graphic6][graphic6]
2. <span data-ttu-id="bbd4c-131">Busque Hola Namespace de Bus de servicio utilizada por el trabajo y vaya a ella:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-131">Locate hello Service Bus Namespace used by your job and go into it:</span></span>  
   ![graphic7][graphic7]
3. <span data-ttu-id="bbd4c-133">Si el trabajo usa una directiva de acceso compartido en hello Namespace de Bus de servicio, consulte el toostep 6</span><span class="sxs-lookup"><span data-stu-id="bbd4c-133">If your job uses a shared access policy on hello Service Bus Namespace, jump toostep 6</span></span>  
4. <span data-ttu-id="bbd4c-134">Vaya a toohello centros de eventos pestaña:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-134">Go toohello Event Hubs tab:</span></span>  
   ![graphic8][graphic8]
5. <span data-ttu-id="bbd4c-136">Busque Hola concentrador de eventos utilizado por el trabajo y vaya a ella:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-136">Locate hello Event Hub used by your job and go into it:</span></span>  
   ![graphic9][graphic9]
6. <span data-ttu-id="bbd4c-138">Vaya toohello ficha configurar:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-138">Go toohello Configure Tab:</span></span>  
   ![graphic10][graphic10]
7. <span data-ttu-id="bbd4c-140">En hello desplegable Nombre de la directiva, busque la directiva de acceso de hello compartido utilizada por el trabajo:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-140">On hello Policy Name drop-down, locate hello shared access policy used by your job:</span></span>  
   ![graphic11][graphic11]
8. <span data-ttu-id="bbd4c-142">Entre la clave principal de Hola y Hola clave secundaria, **elegir Hola uno no utilizada por el trabajo**.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-142">Between hello Primary Key and hello Secondary Key, **pick hello one not used by your job**.</span></span>  
9. <span data-ttu-id="bbd4c-143">Presione regenerar: </span><span class="sxs-lookup"><span data-stu-id="bbd4c-143">Hit regenerate:</span></span>  
   ![graphic12][graphic12]
10. <span data-ttu-id="bbd4c-145">Copie la clave de hello recién generado:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-145">Copy hello newly generated key:</span></span>  
   ![graphic13][graphic13]
11. <span data-ttu-id="bbd4c-147">Continuar tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-147">Continue tooPart 2.</span></span>  

### <a name="sql-database"></a><span data-ttu-id="bbd4c-148">SQL Database</span><span class="sxs-lookup"><span data-stu-id="bbd4c-148">SQL Database</span></span>
> [!NOTE]
> <span data-ttu-id="bbd4c-149">Nota: deberá tooconnect toohello servicio de base de datos de SQL.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-149">Note: you will need tooconnect toohello SQL Database Service.</span></span> <span data-ttu-id="bbd4c-150">Vamos a tooshow cómo toodo esta mediante Hola experiencia de administración en Hola portal de administración de Azure, pero puede elegir toouse alguna herramienta de cliente como SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-150">We are going tooshow how toodo this using hello management experience on hello Azure Management portal but you may choose toouse some client-side tool such as SQL Server Management Studio as well.</span></span>
>
> 

1. <span data-ttu-id="bbd4c-151">Vaya toohello extensión de bases de datos SQL en el portal de administración de Azure de hello:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-151">Go toohello SQL Databases extension on hello Azure Management portal:</span></span>  
   ![graphic14][graphic14]
2. <span data-ttu-id="bbd4c-153">Busque Hola utilizada por el trabajo de base de datos de SQL y **haga clic en el servidor de hello** vínculo Hola misma línea:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-153">Locate hello SQL Database used by your job and **click on hello server** link on hello same line:</span></span>  
   <span data-ttu-id="bbd4c-154">![graphic15][graphic15]</span><span class="sxs-lookup"><span data-stu-id="bbd4c-154">![graphic15][graphic15]</span></span>
3. <span data-ttu-id="bbd4c-155">Haga clic en el comando de hello administrar:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-155">Click hello Manage command:</span></span>  
   ![graphic16][graphic16]
4. <span data-ttu-id="bbd4c-157">Tipo de base de datos maestra: </span><span class="sxs-lookup"><span data-stu-id="bbd4c-157">Type Database Master:</span></span>  
   ![graphic17][graphic17]
5. <span data-ttu-id="bbd4c-159">Escriba su nombre de usuario y contraseña, y haga clic en Iniciar sesión: </span><span class="sxs-lookup"><span data-stu-id="bbd4c-159">Type in your User Name, Password, and click Log on:</span></span>  
   ![graphic18][graphic18]
6. <span data-ttu-id="bbd4c-161">Haga clic en Nueva consulta: </span><span class="sxs-lookup"><span data-stu-id="bbd4c-161">Click New Query:</span></span>  
   ![graphic19][graphic19]
7. <span data-ttu-id="bbd4c-163">Tipo de hello las siguientes consultas reemplazando < login_name > con el nombre de usuario y reemplazando <enterStrongPasswordHere> con la nueva contraseña:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-163">Type in hello following query replacing <login_name> with your User Name and replacing <enterStrongPasswordHere> with your new password:</span></span>  
   `CREATE LOGIN <login_name> WITH PASSWORD = '<enterStrongPasswordHere>'`
8. <span data-ttu-id="bbd4c-164">Haga clic en Ejecutar: </span><span class="sxs-lookup"><span data-stu-id="bbd4c-164">Click Run:</span></span>  
   ![graphic20][graphic20]
9. <span data-ttu-id="bbd4c-166">Volver atrás toostep 2 y esta vez haga clic en la base de datos de hello:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-166">Go back toostep 2 and this time click hello database:</span></span>  
   ![graphic21][graphic21]
10. <span data-ttu-id="bbd4c-168">Haga clic en el comando de hello administrar:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-168">Click hello Manage command:</span></span>  
   ![graphic22][graphic22]
11. <span data-ttu-id="bbd4c-170">escriba su nombre de usuario y contraseña, y haga clic en Iniciar sesión: </span><span class="sxs-lookup"><span data-stu-id="bbd4c-170">type in your User Name, Password, and click Logon:</span></span>  
   ![graphic23][graphic23]
12. <span data-ttu-id="bbd4c-172">Haga clic en Nueva consulta: </span><span class="sxs-lookup"><span data-stu-id="bbd4c-172">Click New Query:</span></span>  
   ![graphic24][graphic24]
13. <span data-ttu-id="bbd4c-174">Escriba hello las siguientes consultas reemplazando < nombre_usuario > con un nombre por el que quiere tooidentify este inicio de sesión en el contexto de Hola de esta base de datos (puede proporcionar Hola el mismo valor que se le asignó para < login_name >, por ejemplo) y reemplazando < login_name > por el nuevo nombre de usuario:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-174">Type in hello following query replacing <user_name> with a name by which you want tooidentify this login in hello context of this database (you can provide hello same value you gave for <login_name>, for example) and replacing <login_name> with your new user name:</span></span>  
   `CREATE USER <user_name> FROM LOGIN <login_name>`
14. <span data-ttu-id="bbd4c-175">Haga clic en Ejecutar: </span><span class="sxs-lookup"><span data-stu-id="bbd4c-175">Click Run:</span></span>  
   ![graphic25][graphic25]
15. <span data-ttu-id="bbd4c-177">Ahora debe proporcionar el nuevo usuario con hello mismos roles y privilegios que tenía el usuario original.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-177">You should now provide your new user with hello same roles and privileges your original user had.</span></span>
16. <span data-ttu-id="bbd4c-178">Continuar tooPart 2.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-178">Continue tooPart 2.</span></span>

## <a name="part-2-stopping-hello-stream-analytics-job"></a><span data-ttu-id="bbd4c-179">Parte 2: Hola de detención flujo de trabajo de análisis</span><span class="sxs-lookup"><span data-stu-id="bbd4c-179">Part 2: Stopping hello Stream Analytics Job</span></span>
1. <span data-ttu-id="bbd4c-180">Vaya toohello extensión de análisis de transmisiones en el portal de administración de Azure de hello:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-180">Go toohello Stream Analytics extension on hello Azure Management portal:</span></span>  
   ![graphic26][graphic26]
2. <span data-ttu-id="bbd4c-182">Busque su trabajo y vaya a él: </span><span class="sxs-lookup"><span data-stu-id="bbd4c-182">Locate your job and go into it:</span></span>  
   ![graphic27][graphic27]
3. <span data-ttu-id="bbd4c-184">Vaya toohello entradas ficha u Hola salidas en función de si va a rotar las credenciales en una entrada o en una salida de hello.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-184">Go toohello Inputs tab or hello Outputs tab based on whether you are rotating hello credentials on an Input or on an Output.</span></span>  
   ![graphic28][graphic28]
4. <span data-ttu-id="bbd4c-186">Haga clic en el comando de detención de Hola y confirme el trabajo Hola se ha detenido:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-186">Click hello Stop command and confirm hello job has stopped:</span></span>  
   <span data-ttu-id="bbd4c-187">![graphic29][graphic29] espere hello toostop de trabajo.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-187">![graphic29][graphic29] Wait for hello job toostop.</span></span>
5. <span data-ttu-id="bbd4c-188">Busque Hola entrada/salida que desee toorotate credenciales en y vaya a ella:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-188">Locate hello input/output you want toorotate credentials on and go into it:</span></span>  
   ![graphic30][graphic30]
6. <span data-ttu-id="bbd4c-190">Continúe tooPart 3.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-190">Proceed tooPart 3.</span></span>

## <a name="part-3-editing-hello-credentials-on-hello-stream-analytics-job"></a><span data-ttu-id="bbd4c-191">Parte 3: Editar credenciales de hello en hello trabajo de análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="bbd4c-191">Part 3: Editing hello credentials on hello Stream Analytics Job</span></span>
### <a name="blob-storagetable-storage"></a><span data-ttu-id="bbd4c-192">Almacenamiento de blobs/almacenamiento de tablas</span><span class="sxs-lookup"><span data-stu-id="bbd4c-192">Blob storage/Table storage</span></span>
1. <span data-ttu-id="bbd4c-193">Encontrar el campo de clave de la cuenta de almacenamiento de Hola y pegue la clave recién generada:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-193">Find hello Storage Account Key field and paste your newly generated key into it:</span></span>  
   ![graphic31][graphic31]
2. <span data-ttu-id="bbd4c-195">Haga clic en el comando Guardar de Hola y Confirmar guardar los cambios:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-195">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic32][graphic32]
3. <span data-ttu-id="bbd4c-197">Al guardar los cambios se iniciará automáticamente una prueba de conexión ; asegúrese de que haya pasado correctamente.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-197">A connection test will automatically start when you save your changes, make sure that is has successfully passed.</span></span>
4. <span data-ttu-id="bbd4c-198">Continúe tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-198">Proceed tooPart 4.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="bbd4c-199">Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="bbd4c-199">Event hubs</span></span>
1. <span data-ttu-id="bbd4c-200">Encontrar el campo de clave de directiva de centro de eventos de Hola y pegue la clave recién generada:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-200">Find hello Event Hub Policy Key field and paste your newly generated key into it:</span></span>  
   ![graphic33][graphic33]
2. <span data-ttu-id="bbd4c-202">Haga clic en el comando Guardar de Hola y Confirmar guardar los cambios:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-202">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic34][graphic34]
3. <span data-ttu-id="bbd4c-204">Una prueba de conexión se iniciará automáticamente al guardar los cambios; asegúrese de que haya pasado correctamente.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-204">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>
4. <span data-ttu-id="bbd4c-205">Continúe tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-205">Proceed tooPart 4.</span></span>

### <a name="power-bi"></a><span data-ttu-id="bbd4c-206">Power BI</span><span class="sxs-lookup"><span data-stu-id="bbd4c-206">Power BI</span></span>
1. <span data-ttu-id="bbd4c-207">Haga clic en la autorización de renovación de hello:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-207">Click hello Renew authorization:</span></span>  

   ![graphic35][graphic35]
2. <span data-ttu-id="bbd4c-209">Obtendrá Hola después de confirmación:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-209">You will get hello following confirmation:</span></span>  

   ![graphic36][graphic36]
3. <span data-ttu-id="bbd4c-211">Haga clic en el comando Guardar de Hola y Confirmar guardar los cambios:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-211">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic37][graphic37]
4. <span data-ttu-id="bbd4c-213">Al guardar los cambios se iniciará automáticamente una prueba de conexión ; asegúrese de que haya pasado correctamente.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-213">A connection test will automatically start when you save your changes, make sure it has successfully passed.</span></span>
5. <span data-ttu-id="bbd4c-214">Continúe tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-214">Proceed tooPart 4.</span></span>

### <a name="sql-database"></a><span data-ttu-id="bbd4c-215">SQL Database</span><span class="sxs-lookup"><span data-stu-id="bbd4c-215">SQL Database</span></span>
1. <span data-ttu-id="bbd4c-216">Buscar campos de nombre de usuario y contraseña de Hola y pegue el conjunto de credenciales recién creado:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-216">Find hello User Name and Password fields and paste your newly created set of credentials into them:</span></span>  
   ![graphic38][graphic38]
2. <span data-ttu-id="bbd4c-218">Haga clic en el comando Guardar de Hola y Confirmar guardar los cambios:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-218">Click hello Save command and confirm saving your changes:</span></span>  
   ![graphic39][graphic39]
3. <span data-ttu-id="bbd4c-220">Una prueba de conexión se iniciará automáticamente al guardar los cambios; asegúrese de que haya pasado correctamente.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-220">A connection test will automatically start when you save your changes, make sure that it has successfully passed.</span></span>  
4. <span data-ttu-id="bbd4c-221">Continúe tooPart 4.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-221">Proceed tooPart 4.</span></span>

## <a name="part-4-starting-your-job-from-last-stopped-time"></a><span data-ttu-id="bbd4c-222">Parte 4: Inicio del trabajo desde la última vez que se detuvo</span><span class="sxs-lookup"><span data-stu-id="bbd4c-222">Part 4: Starting your job from last stopped time</span></span>
1. <span data-ttu-id="bbd4c-223">Salir de hello entrada/salida:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-223">Navigate away from hello Input/Output:</span></span>  
   ![graphic40][graphic40]
2. <span data-ttu-id="bbd4c-225">Haga clic en el comando de inicio de hello:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-225">Click hello Start command:</span></span>  
   ![graphic41][graphic41]
3. <span data-ttu-id="bbd4c-227">Elija última hora de detención de Hola y haga clic en Aceptar:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-227">Pick hello Last Stopped Time and click OK:</span></span>  
   ![graphic42][graphic42]
4. <span data-ttu-id="bbd4c-229">Continúe tooPart 5.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-229">Proceed tooPart 5.</span></span>  

## <a name="part-5-removing-hello-old-set-of-credentials"></a><span data-ttu-id="bbd4c-230">Parte 5: Quitar Hola anterior conjunto de credenciales</span><span class="sxs-lookup"><span data-stu-id="bbd4c-230">Part 5: Removing hello old set of credentials</span></span>
<span data-ttu-id="bbd4c-231">Esta parte es aplicable toohello después de entradas/salidas:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-231">This part is applicable toohello following inputs/outputs:</span></span>

* <span data-ttu-id="bbd4c-232">Blob Storage</span><span class="sxs-lookup"><span data-stu-id="bbd4c-232">Blob Storage</span></span>
* <span data-ttu-id="bbd4c-233">Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="bbd4c-233">Event Hubs</span></span>
* <span data-ttu-id="bbd4c-234">Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="bbd4c-234">SQL Database</span></span>
* <span data-ttu-id="bbd4c-235">Almacenamiento de tablas</span><span class="sxs-lookup"><span data-stu-id="bbd4c-235">Table Storage</span></span>

### <a name="blob-storagetable-storage"></a><span data-ttu-id="bbd4c-236">Almacenamiento de blobs/almacenamiento de tablas</span><span class="sxs-lookup"><span data-stu-id="bbd4c-236">Blob storage/Table storage</span></span>
<span data-ttu-id="bbd4c-237">Repita parte 1 para la clave de acceso que se había utilizado previamente por el trabajo de Hola toorenew Hola ahora sin usar la clave de acceso.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-237">Repeat Part 1 for hello Access Key that was previously used by your job toorenew hello now unused Access Key.</span></span>

### <a name="event-hubs"></a><span data-ttu-id="bbd4c-238">Centros de eventos</span><span class="sxs-lookup"><span data-stu-id="bbd4c-238">Event hubs</span></span>
<span data-ttu-id="bbd4c-239">Repita parte 1 de hello clave que se había utilizado previamente por el trabajo toorenew Hola clave ahora sin usar.</span><span class="sxs-lookup"><span data-stu-id="bbd4c-239">Repeat Part 1 for hello Key that was previously used by your job toorenew hello now unused Key.</span></span>

### <a name="sql-database"></a><span data-ttu-id="bbd4c-240">SQL Database</span><span class="sxs-lookup"><span data-stu-id="bbd4c-240">SQL Database</span></span>
1. <span data-ttu-id="bbd4c-241">Volver atrás ventana de consulta toohello parte 1 paso 7 y tipo Hola después de consulta, reemplazando < previous_login_name > con el nombre de usuario que se usó previamente por el trabajo de hello:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-241">Go back toohello query window from Part 1 Step 7 and type in hello following query, replacing <previous_login_name> with hello User Name that was previously used by your job:</span></span>  
   `DROP LOGIN <previous_login_name>`  
2. <span data-ttu-id="bbd4c-242">Haga clic en Ejecutar: </span><span class="sxs-lookup"><span data-stu-id="bbd4c-242">Click Run:</span></span>  
   ![graphic43][graphic43]  

<span data-ttu-id="bbd4c-244">Debería obtener Hola después de confirmación:</span><span class="sxs-lookup"><span data-stu-id="bbd4c-244">You should get hello following confirmation:</span></span> 

    Command(s) completed successfully.

## <a name="get-help"></a><span data-ttu-id="bbd4c-245">Obtener ayuda</span><span class="sxs-lookup"><span data-stu-id="bbd4c-245">Get help</span></span>
<span data-ttu-id="bbd4c-246">Para obtener más ayuda, pruebe nuestro [foro de Análisis de transmisiones de Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="bbd4c-246">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbd4c-247">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="bbd4c-247">Next steps</span></span>
* [<span data-ttu-id="bbd4c-248">Introducción tooAzure análisis de transmisiones</span><span class="sxs-lookup"><span data-stu-id="bbd4c-248">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="bbd4c-249">Introducción al uso de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bbd4c-249">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="bbd4c-250">Escalación de trabajos de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="bbd4c-250">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="bbd4c-251">Referencia del lenguaje de consulta de Análisis de transmisiones de Azure</span><span class="sxs-lookup"><span data-stu-id="bbd4c-251">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="bbd4c-252">Referencia de API de REST de administración de Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bbd4c-252">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

[graphic1]: ./media/stream-analytics-login-credentials-inputs-outputs/1-stream-analytics-login-credentials-inputs-outputs.png
[graphic2]: ./media/stream-analytics-login-credentials-inputs-outputs/2-stream-analytics-login-credentials-inputs-outputs.png
[graphic3]: ./media/stream-analytics-login-credentials-inputs-outputs/3-stream-analytics-login-credentials-inputs-outputs.png
[graphic4]: ./media/stream-analytics-login-credentials-inputs-outputs/4-stream-analytics-login-credentials-inputs-outputs.png
[graphic5]: ./media/stream-analytics-login-credentials-inputs-outputs/5-stream-analytics-login-credentials-inputs-outputs.png
[graphic6]: ./media/stream-analytics-login-credentials-inputs-outputs/6-stream-analytics-login-credentials-inputs-outputs.png
[graphic7]: ./media/stream-analytics-login-credentials-inputs-outputs/7-stream-analytics-login-credentials-inputs-outputs.png
[graphic8]: ./media/stream-analytics-login-credentials-inputs-outputs/8-stream-analytics-login-credentials-inputs-outputs.png
[graphic9]: ./media/stream-analytics-login-credentials-inputs-outputs/9-stream-analytics-login-credentials-inputs-outputs.png
[graphic10]: ./media/stream-analytics-login-credentials-inputs-outputs/10-stream-analytics-login-credentials-inputs-outputs.png
[graphic11]: ./media/stream-analytics-login-credentials-inputs-outputs/11-stream-analytics-login-credentials-inputs-outputs.png
[graphic12]: ./media/stream-analytics-login-credentials-inputs-outputs/12-stream-analytics-login-credentials-inputs-outputs.png
[graphic13]: ./media/stream-analytics-login-credentials-inputs-outputs/13-stream-analytics-login-credentials-inputs-outputs.png
[graphic14]: ./media/stream-analytics-login-credentials-inputs-outputs/14-stream-analytics-login-credentials-inputs-outputs.png
[graphic15]: ./media/stream-analytics-login-credentials-inputs-outputs/15-stream-analytics-login-credentials-inputs-outputs.png
[graphic16]: ./media/stream-analytics-login-credentials-inputs-outputs/16-stream-analytics-login-credentials-inputs-outputs.png
[graphic17]: ./media/stream-analytics-login-credentials-inputs-outputs/17-stream-analytics-login-credentials-inputs-outputs.png
[graphic18]: ./media/stream-analytics-login-credentials-inputs-outputs/18-stream-analytics-login-credentials-inputs-outputs.png
[graphic19]: ./media/stream-analytics-login-credentials-inputs-outputs/19-stream-analytics-login-credentials-inputs-outputs.png
[graphic20]: ./media/stream-analytics-login-credentials-inputs-outputs/20-stream-analytics-login-credentials-inputs-outputs.png
[graphic21]: ./media/stream-analytics-login-credentials-inputs-outputs/21-stream-analytics-login-credentials-inputs-outputs.png
[graphic22]: ./media/stream-analytics-login-credentials-inputs-outputs/22-stream-analytics-login-credentials-inputs-outputs.png
[graphic23]: ./media/stream-analytics-login-credentials-inputs-outputs/23-stream-analytics-login-credentials-inputs-outputs.png
[graphic24]: ./media/stream-analytics-login-credentials-inputs-outputs/24-stream-analytics-login-credentials-inputs-outputs.png
[graphic25]: ./media/stream-analytics-login-credentials-inputs-outputs/25-stream-analytics-login-credentials-inputs-outputs.png
[graphic26]: ./media/stream-analytics-login-credentials-inputs-outputs/26-stream-analytics-login-credentials-inputs-outputs.png
[graphic27]: ./media/stream-analytics-login-credentials-inputs-outputs/27-stream-analytics-login-credentials-inputs-outputs.png
[graphic28]: ./media/stream-analytics-login-credentials-inputs-outputs/28-stream-analytics-login-credentials-inputs-outputs.png
[graphic29]: ./media/stream-analytics-login-credentials-inputs-outputs/29-stream-analytics-login-credentials-inputs-outputs.png
[graphic30]: ./media/stream-analytics-login-credentials-inputs-outputs/30-stream-analytics-login-credentials-inputs-outputs.png
[graphic31]: ./media/stream-analytics-login-credentials-inputs-outputs/31-stream-analytics-login-credentials-inputs-outputs.png
[graphic32]: ./media/stream-analytics-login-credentials-inputs-outputs/32-stream-analytics-login-credentials-inputs-outputs.png
[graphic33]: ./media/stream-analytics-login-credentials-inputs-outputs/33-stream-analytics-login-credentials-inputs-outputs.png
[graphic34]: ./media/stream-analytics-login-credentials-inputs-outputs/34-stream-analytics-login-credentials-inputs-outputs.png
[graphic35]: ./media/stream-analytics-login-credentials-inputs-outputs/35-stream-analytics-login-credentials-inputs-outputs.png
[graphic36]: ./media/stream-analytics-login-credentials-inputs-outputs/36-stream-analytics-login-credentials-inputs-outputs.png
[graphic37]: ./media/stream-analytics-login-credentials-inputs-outputs/37-stream-analytics-login-credentials-inputs-outputs.png
[graphic38]: ./media/stream-analytics-login-credentials-inputs-outputs/38-stream-analytics-login-credentials-inputs-outputs.png
[graphic39]: ./media/stream-analytics-login-credentials-inputs-outputs/39-stream-analytics-login-credentials-inputs-outputs.png
[graphic40]: ./media/stream-analytics-login-credentials-inputs-outputs/40-stream-analytics-login-credentials-inputs-outputs.png
[graphic41]: ./media/stream-analytics-login-credentials-inputs-outputs/41-stream-analytics-login-credentials-inputs-outputs.png
[graphic42]: ./media/stream-analytics-login-credentials-inputs-outputs/42-stream-analytics-login-credentials-inputs-outputs.png
[graphic43]: ./media/stream-analytics-login-credentials-inputs-outputs/43-stream-analytics-login-credentials-inputs-outputs.png

