---
title: "aaaFix un error de conexión de SQL, error transitorio | Documentos de Microsoft"
description: "Obtenga información acerca de cómo tootroubleshoot, diagnosticar y evitar un error de conexión de SQL o un error transitorio en la base de datos de SQL Azure. "
keywords: "conexión de sql, cadena de conexión, problemas de conectividad, error transitorio, error de conexión"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: develop apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: d225e610b9e88170ab53ca16d615bd07220603cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a><span data-ttu-id="17c77-104">Acciones para solucionar problemas, diagnosticar y evitar errores de conexión y errores transitorios en Base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="17c77-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span></span>
<span data-ttu-id="17c77-105">Este artículo describe cómo tooprevent, solucionar problemas, diagnosticar y mitigar los errores de conexión y los errores transitorios que se encuentra la aplicación cliente cuando interactúa con la base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="17c77-105">This article describes how tooprevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span></span> <span data-ttu-id="17c77-106">Obtenga información acerca de cómo tooconfigure lógica de reintento, generar la cadena de conexión de Hola y ajuste otros parámetros de conexión.</span><span class="sxs-lookup"><span data-stu-id="17c77-106">Learn how tooconfigure retry logic, build hello connection string, and adjust other connection settings.</span></span>

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a><span data-ttu-id="17c77-107">Errores transitorios</span><span class="sxs-lookup"><span data-stu-id="17c77-107">Transient errors (transient faults)</span></span>
<span data-ttu-id="17c77-108">Un error transitorio es un error que tiene una causa subyacente que pronto se solucionará automáticamente.</span><span class="sxs-lookup"><span data-stu-id="17c77-108">A transient error - also, transient fault - has an underlying cause that will soon resolve itself.</span></span> <span data-ttu-id="17c77-109">Una causa ocasional de los errores transitorios es cuando Hola sistema Azure rápidamente desplaza hardware recursos toobetter equilibrio de carga a diversas cargas de trabajo.</span><span class="sxs-lookup"><span data-stu-id="17c77-109">An occasional cause of transient errors is when hello Azure system quickly shifts hardware resources toobetter load-balance various workloads.</span></span> <span data-ttu-id="17c77-110">La mayoría de estos eventos de reconfiguración a menudo se completan en menos de 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="17c77-110">Most of these reconfiguration events often complete in less than 60 seconds.</span></span> <span data-ttu-id="17c77-111">Durante este intervalo de tiempo de reconfiguración, tendrá conectividad emite tooAzure base de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="17c77-111">During this reconfiguration time span, you may have connectivity issues tooAzure SQL Database.</span></span> <span data-ttu-id="17c77-112">Aplicaciones que se conectan tooAzure debe ser la base de datos de SQL compilada tooexpect estos errores transitorios, identificador de ellos mediante la implementación de lógica en su código en lugar de ponerlos al toousers como errores de aplicación de reintento.</span><span class="sxs-lookup"><span data-stu-id="17c77-112">Applications connecting tooAzure SQL Database should be built tooexpect these transient errors, handle them by implementing retry logic in their code instead of surfacing them toousers as application errors.</span></span>

<span data-ttu-id="17c77-113">Si su programa cliente utiliza ADO.NET, el programa se dijo sobre error transitorio de Hola por throw Hola de un **SqlException**.</span><span class="sxs-lookup"><span data-stu-id="17c77-113">If your client program is using ADO.NET, your program is told about hello transient error by hello throw of an **SqlException**.</span></span> <span data-ttu-id="17c77-114">Hola **número** propiedad se pueden comparar con la lista de Hola de errores transitorios en parte superior de Hola de tema de hello: [códigos de error SQL para las aplicaciones de cliente de base de datos SQL](sql-database-develop-error-messages.md).</span><span class="sxs-lookup"><span data-stu-id="17c77-114">hello **Number** property can be compared against hello list of transient errors near hello top of hello topic: [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="17c77-115">Comparación de conexión y comando</span><span class="sxs-lookup"><span data-stu-id="17c77-115">Connection versus command</span></span>
<span data-ttu-id="17c77-116">Que vuelva a intentar la conexión SQL Hola o establecer de nuevo, según la siguiente hello:</span><span class="sxs-lookup"><span data-stu-id="17c77-116">You'll retry hello SQL connection or establish it again, depending on hello following:</span></span>

* <span data-ttu-id="17c77-117">**Se produce un error transitorio durante un intento de conexión**: se debe reintentar la conexión de hello después retrasar durante unos segundos.</span><span class="sxs-lookup"><span data-stu-id="17c77-117">**A transient error occurs during a connection try**: hello connection should be retried after delaying for several seconds.</span></span>
* <span data-ttu-id="17c77-118">**Se produce un error transitorio durante un comando de consulta SQL**: comando hello no se debe reintentar inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="17c77-118">**A transient error occurs during a SQL query command**: hello command should not be immediately retried.</span></span> <span data-ttu-id="17c77-119">En su lugar, después de un retraso, Hola debe ser recién establecer conexión.</span><span class="sxs-lookup"><span data-stu-id="17c77-119">Instead, after a delay, hello connection should be freshly established.</span></span> <span data-ttu-id="17c77-120">A continuación, se puede recuperar el comando Hola.</span><span class="sxs-lookup"><span data-stu-id="17c77-120">Then hello command can be retried.</span></span>

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a><span data-ttu-id="17c77-121">Lógica de reintento para errores transitorios.</span><span class="sxs-lookup"><span data-stu-id="17c77-121">Retry logic for transient errors</span></span>
<span data-ttu-id="17c77-122">Los programas cliente que encuentran ocasionalmente un error transitorio son más sólidos cuando contienen lógica de reintento.</span><span class="sxs-lookup"><span data-stu-id="17c77-122">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span></span>

<span data-ttu-id="17c77-123">Cuando el programa se comunica con la base de datos de SQL Azure a través de un middleware parte 3ª, consultar con el proveedor de hello si Hola middleware contiene lógica de reintento para errores transitorios.</span><span class="sxs-lookup"><span data-stu-id="17c77-123">When your program communicates with Azure SQL Database through a 3rd party middleware, inquire with hello vendor whether hello middleware contains retry logic for transient errors.</span></span>

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a><span data-ttu-id="17c77-124">Principios de reintento</span><span class="sxs-lookup"><span data-stu-id="17c77-124">Principles for retry</span></span>
* <span data-ttu-id="17c77-125">Debe reintentarse una tooopen de intento de una conexión si Hola error es transitorio.</span><span class="sxs-lookup"><span data-stu-id="17c77-125">An attempt tooopen a connection should be retried if hello error is transient.</span></span>
* <span data-ttu-id="17c77-126">No se debe volver a intentar directamente una instrucción SELECT de SQL que haya fallado con un error transitorio.</span><span class="sxs-lookup"><span data-stu-id="17c77-126">A SQL SELECT statement that fails with a transient error should not be retried directly.</span></span>
  
  * <span data-ttu-id="17c77-127">En su lugar, establecer una conexión nueva y, a continuación, vuelva a intentar Hola seleccione.</span><span class="sxs-lookup"><span data-stu-id="17c77-127">Instead, establish a fresh connection, and then retry hello SELECT.</span></span>
* <span data-ttu-id="17c77-128">Cuando una instrucción SQL UPDATE produce un error transitorio, se debe establecer una conexión nueva antes de Hola que se vuelve a intentar la actualización.</span><span class="sxs-lookup"><span data-stu-id="17c77-128">When a SQL UPDATE statement fails with a transient error, a fresh connection should be established before hello UPDATE is retried.</span></span>
  
  * <span data-ttu-id="17c77-129">lógica de reintento de Hello debe asegurarse de que transacción de base de datos completa de hello completa o esa transacción completa Hola se revierte.</span><span class="sxs-lookup"><span data-stu-id="17c77-129">hello retry logic must ensure that either hello entire database transaction completed, or that hello entire transaction is rolled back.</span></span>

#### <a name="other-considerations-for-retry"></a><span data-ttu-id="17c77-130">Otras consideraciones para el reintento</span><span class="sxs-lookup"><span data-stu-id="17c77-130">Other considerations for retry</span></span>
* <span data-ttu-id="17c77-131">Un programa por lotes que se inicia automáticamente después del horario de trabajo y que se completará antes de mañana, puede permitirse a toovery paciente con largos intervalos de tiempo entre los reintentos.</span><span class="sxs-lookup"><span data-stu-id="17c77-131">A batch program that is automatically started after work hours, and which will complete before morning, can afford toovery patient with long time intervals between its retry attempts.</span></span>
* <span data-ttu-id="17c77-132">Un programa de la interfaz de usuario debe contar con hello tendencia humana toogive seguridad después de una espera demasiado larga.</span><span class="sxs-lookup"><span data-stu-id="17c77-132">A user interface program should account for hello human tendency toogive up after too long a wait.</span></span>
  
  * <span data-ttu-id="17c77-133">Sin embargo, solución de hello no debe ser tooretry cada pocos segundos, porque esa directiva puede saturar el sistema Hola con las solicitudes.</span><span class="sxs-lookup"><span data-stu-id="17c77-133">However, hello solution must not be tooretry every few seconds, because that policy can flood hello system with requests.</span></span>

#### <a name="interval-increase-between-retries"></a><span data-ttu-id="17c77-134">Aumento del intervalo entre reintentos</span><span class="sxs-lookup"><span data-stu-id="17c77-134">Interval increase between retries</span></span>
<span data-ttu-id="17c77-135">Se recomienda un retraso de 5 segundos antes del primer reintento.</span><span class="sxs-lookup"><span data-stu-id="17c77-135">We recommend that you delay for 5 seconds before your first retry.</span></span> <span data-ttu-id="17c77-136">Reintentar después de un retraso inferior a 5 segundos corre el riesgo de servicio en la nube Hola abrumador.</span><span class="sxs-lookup"><span data-stu-id="17c77-136">Retrying after a delay shorter than 5 seconds risks overwhelming hello cloud service.</span></span> <span data-ttu-id="17c77-137">Para cada reintento subsiguientes retraso Hola debe crecer exponencialmente, tooa máximo de 60 segundos.</span><span class="sxs-lookup"><span data-stu-id="17c77-137">For each subsequent retry hello delay should grow exponentially, up tooa maximum of 60 seconds.</span></span>

<span data-ttu-id="17c77-138">Obtener una explicación de hello *período de bloqueo* para los clientes que utilizan ADO.NET está disponible en [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span><span class="sxs-lookup"><span data-stu-id="17c77-138">A discussion of hello *blocking period* for clients that use ADO.NET is available in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span></span>

<span data-ttu-id="17c77-139">Puede que le interese tooset un número máximo de reintentos antes de programa Hola finaliza automáticamente.</span><span class="sxs-lookup"><span data-stu-id="17c77-139">You might also want tooset a maximum number of retries before hello program self-terminates.</span></span>

#### <a name="code-samples-with-retry-logic"></a><span data-ttu-id="17c77-140">Ejemplos de código con lógica de reintento</span><span class="sxs-lookup"><span data-stu-id="17c77-140">Code samples with retry logic</span></span>
<span data-ttu-id="17c77-141">Los ejemplos de código con lógica de reintento, en una variedad de lenguajes de programación, están disponibles en:</span><span class="sxs-lookup"><span data-stu-id="17c77-141">Code samples with retry logic, in a variety of programming languages, are available at:</span></span>

* [<span data-ttu-id="17c77-142">Bibliotecas de conexiones para Base de datos SQL y SQL Server</span><span class="sxs-lookup"><span data-stu-id="17c77-142">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a><span data-ttu-id="17c77-143">Probar su lógica de reintento</span><span class="sxs-lookup"><span data-stu-id="17c77-143">Test your retry logic</span></span>
<span data-ttu-id="17c77-144">tootest la lógica de reintento, se debe simular o producirá un error que puede corregirse mientras el programa se está ejecutando.</span><span class="sxs-lookup"><span data-stu-id="17c77-144">tootest your retry logic, you must simulate or cause an error than can be corrected while your program is still running.</span></span>

##### <a name="test-by-disconnecting-from-hello-network"></a><span data-ttu-id="17c77-145">Probar mediante la desconexión de la red de Hola</span><span class="sxs-lookup"><span data-stu-id="17c77-145">Test by disconnecting from hello network</span></span>
<span data-ttu-id="17c77-146">Una manera que puede probar la lógica de reintento es toodisconnect el equipo cliente desde Hola de red mientras se ejecuta el programa Hola.</span><span class="sxs-lookup"><span data-stu-id="17c77-146">One way you can test your retry logic is toodisconnect your client computer from hello network while hello program is running.</span></span> <span data-ttu-id="17c77-147">error de Hello será:</span><span class="sxs-lookup"><span data-stu-id="17c77-147">hello error will be:</span></span>

* <span data-ttu-id="17c77-148">**SqlException.Number** = 11001</span><span class="sxs-lookup"><span data-stu-id="17c77-148">**SqlException.Number** = 11001</span></span>
* <span data-ttu-id="17c77-149">Mensaje: "Host desconocido"</span><span class="sxs-lookup"><span data-stu-id="17c77-149">Message: "No such host is known"</span></span>

<span data-ttu-id="17c77-150">Como parte del programa Hola primero intente de nuevo intento, el programa puede corregir el error ortográfico hello y, a continuación, intente tooconnect.</span><span class="sxs-lookup"><span data-stu-id="17c77-150">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="17c77-151">toomake este práctico, desconecte el equipo de red de hello antes de iniciar el programa.</span><span class="sxs-lookup"><span data-stu-id="17c77-151">toomake this practical, you unplug your computer from hello network before you start your program.</span></span> <span data-ttu-id="17c77-152">A continuación, el programa reconoce un parámetro de tiempo de ejecución que hace que programa Hola:</span><span class="sxs-lookup"><span data-stu-id="17c77-152">Then your program recognizes a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="17c77-153">Agregue temporalmente 11001 lista tooits de tooconsider de errores como transitorio.</span><span class="sxs-lookup"><span data-stu-id="17c77-153">Temporarily add 11001 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="17c77-154">Intente su primera conexión como de costumbre.</span><span class="sxs-lookup"><span data-stu-id="17c77-154">Attempt its first connection as usual.</span></span>
3. <span data-ttu-id="17c77-155">Después de Hola se captura el error, quite 11001 de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="17c77-155">After hello error is caught, remove 11001 from hello list.</span></span>
4. <span data-ttu-id="17c77-156">Mostrar un mensaje que indica el equipo de hello usuario tooplug hello en red Hola.</span><span class="sxs-lookup"><span data-stu-id="17c77-156">Display a message telling hello user tooplug hello computer into hello network.</span></span>
   * <span data-ttu-id="17c77-157">Detenga la ejecución aún más mediante el uso de cualquier hello **Console.ReadLine** método o un cuadro de diálogo con un botón Aceptar.</span><span class="sxs-lookup"><span data-stu-id="17c77-157">Pause further execution by using either hello **Console.ReadLine** method or a dialog with an OK button.</span></span> <span data-ttu-id="17c77-158">usuario de Hello presiona tecla ENTRAR de hello después de equipo de hello conectado en red de Hola.</span><span class="sxs-lookup"><span data-stu-id="17c77-158">hello user presses hello Enter key after hello computer plugged into hello network.</span></span>
5. <span data-ttu-id="17c77-159">Vuelva a intentar tooconnect, espera correcto.</span><span class="sxs-lookup"><span data-stu-id="17c77-159">Attempt again tooconnect, expecting success.</span></span>

##### <a name="test-by-misspelling-hello-database-name-when-connecting"></a><span data-ttu-id="17c77-160">Las pruebas por nombre de base de datos de error ortográfico Hola al conectarse</span><span class="sxs-lookup"><span data-stu-id="17c77-160">Test by misspelling hello database name when connecting</span></span>
<span data-ttu-id="17c77-161">El programa deliberadamente puede escribió mal el nombre de usuario de hello antes del primer intento de conexión Hola.</span><span class="sxs-lookup"><span data-stu-id="17c77-161">Your program can purposely misspell hello user name before hello first connection attempt.</span></span> <span data-ttu-id="17c77-162">error de Hello será:</span><span class="sxs-lookup"><span data-stu-id="17c77-162">hello error will be:</span></span>

* <span data-ttu-id="17c77-163">**SqlException.Number** = 18456</span><span class="sxs-lookup"><span data-stu-id="17c77-163">**SqlException.Number** = 18456</span></span>
* <span data-ttu-id="17c77-164">Mensaje: "Error de inicio de sesión para el usuario 'WRONG_MyUserName'".</span><span class="sxs-lookup"><span data-stu-id="17c77-164">Message: "Login failed for user 'WRONG_MyUserName'."</span></span>

<span data-ttu-id="17c77-165">Como parte del programa Hola primero intente de nuevo intento, el programa puede corregir el error ortográfico hello y, a continuación, intente tooconnect.</span><span class="sxs-lookup"><span data-stu-id="17c77-165">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="17c77-166">toomake este práctico, su programa pudo reconocer un parámetro de tiempo de ejecución que hace que programa Hola:</span><span class="sxs-lookup"><span data-stu-id="17c77-166">toomake this practical, your program could recognize a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="17c77-167">Agregue temporalmente 18456 lista tooits de tooconsider de errores como transitorio.</span><span class="sxs-lookup"><span data-stu-id="17c77-167">Temporarily add 18456 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="17c77-168">Deliberadamente Agregar nombre de usuario de toohello 'WRONG_'.</span><span class="sxs-lookup"><span data-stu-id="17c77-168">Purposely add 'WRONG_' toohello user name.</span></span>
3. <span data-ttu-id="17c77-169">Después de Hola se captura el error, quite 18456 de lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="17c77-169">After hello error is caught, remove 18456 from hello list.</span></span>
4. <span data-ttu-id="17c77-170">Quite 'WRONG_' nombre de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="17c77-170">Remove 'WRONG_' from hello user name.</span></span>
5. <span data-ttu-id="17c77-171">Vuelva a intentar tooconnect, espera correcto.</span><span class="sxs-lookup"><span data-stu-id="17c77-171">Attempt again tooconnect, expecting success.</span></span>

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a><span data-ttu-id="17c77-172">Parámetros .NET SqlConnection para reintento de conexión</span><span class="sxs-lookup"><span data-stu-id="17c77-172">.NET SqlConnection parameters for connection retry</span></span>
<span data-ttu-id="17c77-173">Si su programa cliente conecta tootooAzure base de datos SQL mediante la clase de .NET Framework de hello **System.Data.SqlClient.SqlConnection**, debe utilizar .NET 4.6.1 o posterior (o .NET Core) lo que permite aprovechar su característica de reintento de conexión.</span><span class="sxs-lookup"><span data-stu-id="17c77-173">If your client program connects tootooAzure SQL Database by using hello .NET Framework class **System.Data.SqlClient.SqlConnection**, you should use .NET 4.6.1 or later (or .NET Core) so you can leverage its connection retry feature.</span></span> <span data-ttu-id="17c77-174">Detalles de la característica de hello [aquí](http://go.microsoft.com/fwlink/?linkid=393996).</span><span class="sxs-lookup"><span data-stu-id="17c77-174">Details of hello feature are [here](http://go.microsoft.com/fwlink/?linkid=393996).</span></span>

<!--
2015-11-30, FwLink 393996 points toodn632678.aspx, which links tooa downloadable .docx related tooSqlClient and SQL Server 2014.
-->


<span data-ttu-id="17c77-175">Al compilar hello [cadena de conexión](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) para su **SqlConnection** de objeto, se deben coordinar valores de hello entre Hola parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="17c77-175">When you build hello [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, you should coordinate hello values among hello following parameters:</span></span>

* <span data-ttu-id="17c77-176">ConnectRetryCount &nbsp;&nbsp;*(El valor predeterminado es 1. El intervalo es de 0 a 255).*</span><span class="sxs-lookup"><span data-stu-id="17c77-176">ConnectRetryCount &nbsp;&nbsp;*(Default is 1. Range is 0 through 255.)*</span></span>
* <span data-ttu-id="17c77-177">ConnectRetryInterval &nbsp;&nbsp;*(El valor predeterminado es 1 segundo. El intervalo es de 1 a 60.)*</span><span class="sxs-lookup"><span data-stu-id="17c77-177">ConnectRetryInterval &nbsp;&nbsp;*(Default is 1 second. Range is 1 through 60.)*</span></span>
* <span data-ttu-id="17c77-178">Connection Timeout &nbsp;&nbsp;*(El valor predeterminado es 15 segundos. El intervalo es de 0 a 2147483647)*</span><span class="sxs-lookup"><span data-stu-id="17c77-178">Connection Timeout &nbsp;&nbsp;*(Default is 15 seconds. Range is 0 through 2147483647)*</span></span>

<span data-ttu-id="17c77-179">En concreto, los valores elegidos deben hacer Hola después de igualdad true:</span><span class="sxs-lookup"><span data-stu-id="17c77-179">Specifically, your chosen values should make hello following equality true:</span></span>

* <span data-ttu-id="17c77-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span><span class="sxs-lookup"><span data-stu-id="17c77-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span></span>

<span data-ttu-id="17c77-181">Por ejemplo, si hello contar = 3 y el intervalo = 10 segundos, un tiempo de espera de solo 29 segundos no bastante proporcionaría sistema Hola tiempo suficiente para su reintento 3er y final al conectar: 29 < 3 * 10.</span><span class="sxs-lookup"><span data-stu-id="17c77-181">For example, if hello count = 3, and interval = 10 seconds, a timeout of only 29 seconds would not quite give hello system enough time for its 3rd and final retry at connecting: 29 < 3 * 10.</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="17c77-182">Comparación de conexión y comando</span><span class="sxs-lookup"><span data-stu-id="17c77-182">Connection versus command</span></span>
<span data-ttu-id="17c77-183">Hola **ConnectRetryCount** y **ConnectRetryInterval** parámetros permiten la **SqlConnection** Hola de objeto vuelva a intentar la operación de conexión sin que se lo indica o molestarle su programa, como devolver el programa de tooyour de control.</span><span class="sxs-lookup"><span data-stu-id="17c77-183">hello **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry hello connect operation without telling or bothering your program, such as returning control tooyour program.</span></span> <span data-ttu-id="17c77-184">reintentos de Hello pueden producirse en hello siguientes situaciones:</span><span class="sxs-lookup"><span data-stu-id="17c77-184">hello retries can occur in hello following situations:</span></span>

* <span data-ttu-id="17c77-185">Llamada del método mySqlConnection.Open</span><span class="sxs-lookup"><span data-stu-id="17c77-185">mySqlConnection.Open method call</span></span>
* <span data-ttu-id="17c77-186">Llamada del método mySqlConnection.Execute</span><span class="sxs-lookup"><span data-stu-id="17c77-186">mySqlConnection.Execute method call</span></span>

<span data-ttu-id="17c77-187">Hay algo muy sutil que tener en cuenta.</span><span class="sxs-lookup"><span data-stu-id="17c77-187">There is a subtlety.</span></span> <span data-ttu-id="17c77-188">Si se produce un error transitorio mientras su *consulta* se está ejecutando, el **SqlConnection** no Hola de reintentar la operación de conexión y por supuesto, no vuelva a intentar la consulta de objeto.</span><span class="sxs-lookup"><span data-stu-id="17c77-188">If a transient error occurs while your *query* is being executed, your **SqlConnection** object does not retry hello connect operation, and it certainly does not retry your query.</span></span> <span data-ttu-id="17c77-189">Sin embargo, **SqlConnection** muy rápidamente comprobaciones Hola conexión antes de enviar la consulta para su ejecución.</span><span class="sxs-lookup"><span data-stu-id="17c77-189">However, **SqlConnection** very quickly checks hello connection before sending your query for execution.</span></span> <span data-ttu-id="17c77-190">Si la comprobación rápida de hello detecta un problema de conexión, **SqlConnection** Hola de reintentos de la operación de conexión.</span><span class="sxs-lookup"><span data-stu-id="17c77-190">If hello quick check detects a connection problem, **SqlConnection** retries hello connect operation.</span></span> <span data-ttu-id="17c77-191">Si se realiza correctamente el reintento de hello, consultar se envía para su ejecución.</span><span class="sxs-lookup"><span data-stu-id="17c77-191">If hello retry succeeds, you query is sent for execution.</span></span>

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a><span data-ttu-id="17c77-192">¿Se debe combinar Connectretrycount con lógica de reintento de la aplicación?</span><span class="sxs-lookup"><span data-stu-id="17c77-192">Should ConnectRetryCount be combined with application retry logic?</span></span>
<span data-ttu-id="17c77-193">Supongamos que su aplicación tiene una lógica de reintento personalizada.</span><span class="sxs-lookup"><span data-stu-id="17c77-193">Suppose your application has robust custom retry logic.</span></span> <span data-ttu-id="17c77-194">Podría Reintentar Hola 4 veces la operación de conexión.</span><span class="sxs-lookup"><span data-stu-id="17c77-194">It might retry hello connect operation 4 times.</span></span> <span data-ttu-id="17c77-195">Si agrega **ConnectRetryInterval** y **ConnectRetryCount** = 3 cadena de conexión de tooyour, aumentará la too4 de recuento de reintentos de Hola * 3 = 12 vuelve a intentar.</span><span class="sxs-lookup"><span data-stu-id="17c77-195">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 tooyour connection string, you will increase hello retry count too4 * 3 = 12 retries.</span></span> <span data-ttu-id="17c77-196">Es posible que no desee un gran número de reintentos.</span><span class="sxs-lookup"><span data-stu-id="17c77-196">You might not intend such a high number of retries.</span></span>

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-tooazure-sql-database"></a><span data-ttu-id="17c77-197">Las conexiones tooAzure base de datos SQL</span><span class="sxs-lookup"><span data-stu-id="17c77-197">Connections tooAzure SQL Database</span></span>
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a><span data-ttu-id="17c77-198">Conexión: cadena de conexión</span><span class="sxs-lookup"><span data-stu-id="17c77-198">Connection: Connection string</span></span>
<span data-ttu-id="17c77-199">cadena de conexión de Hello necesaria para conectar tooAzure base de datos SQL es ligeramente diferente de cadena de Hola para conectar tooMicrosoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="17c77-199">hello connection string necessary for connecting tooAzure SQL Database is slightly different from hello string for connecting tooMicrosoft SQL Server.</span></span> <span data-ttu-id="17c77-200">Puede copiar la cadena de conexión de hello para la base de datos de Hola [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="17c77-200">You can copy hello connection string for your database from hello [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a><span data-ttu-id="17c77-201">Conexión: Dirección IP</span><span class="sxs-lookup"><span data-stu-id="17c77-201">Connection: IP address</span></span>
<span data-ttu-id="17c77-202">Debe configurar Hola base de datos SQL tooaccept comunicación entre el servidor de la dirección IP de hello del equipo de Hola que aloja su programa cliente.</span><span class="sxs-lookup"><span data-stu-id="17c77-202">You must configure hello SQL Database server tooaccept communication from hello IP address of hello computer that hosts your client program.</span></span> <span data-ttu-id="17c77-203">Para ello, editar la configuración de firewall de Hola a través de hello [portal de Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="17c77-203">You do this by editing hello firewall settings through hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="17c77-204">Si ha olvidado la dirección IP de tooconfigure hello, se producirá un error en el programa con un mensaje de error práctica que indica la dirección IP necesario Hola.</span><span class="sxs-lookup"><span data-stu-id="17c77-204">If you forget tooconfigure hello IP address, your program will fail with a handy error message that states hello necessary IP address.</span></span>

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

<span data-ttu-id="17c77-205">Para obtener más información, consulte [Configuración del firewall en Base de datos SQL](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="17c77-205">For more information, see: [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md)</span></span>

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a><span data-ttu-id="17c77-206">Conexión: puertos</span><span class="sxs-lookup"><span data-stu-id="17c77-206">Connection: Ports</span></span>
<span data-ttu-id="17c77-207">Normalmente sólo necesitará tooensure que el puerto 1433 está abierto para la comunicación saliente, en equipo Hola que hospeda programa cliente.</span><span class="sxs-lookup"><span data-stu-id="17c77-207">Typically you only need tooensure that port 1433 is open for outbound communication, on hello computer that hosts you client program.</span></span>

<span data-ttu-id="17c77-208">Por ejemplo, cuando el programa de cliente está alojado en un equipo Windows, Hola Firewall de Windows en el host de hello permite tooopen el puerto 1433:</span><span class="sxs-lookup"><span data-stu-id="17c77-208">For example, when your client program is hosted on a Windows computer, hello Windows Firewall on hello host enables you tooopen port 1433:</span></span>

1. <span data-ttu-id="17c77-209">Abra el Panel de Control de Hola</span><span class="sxs-lookup"><span data-stu-id="17c77-209">Open hello Control Panel</span></span>
2. <span data-ttu-id="17c77-210">&gt; Todos los elementos del Panel de control</span><span class="sxs-lookup"><span data-stu-id="17c77-210">&gt; All Control Panel Items</span></span>
3. <span data-ttu-id="17c77-211">&gt; Firewall de Windows</span><span class="sxs-lookup"><span data-stu-id="17c77-211">&gt; Windows Firewall</span></span>
4. <span data-ttu-id="17c77-212">&gt; Configuración avanzada</span><span class="sxs-lookup"><span data-stu-id="17c77-212">&gt; Advanced Settings</span></span>
5. <span data-ttu-id="17c77-213">&gt; Reglas de salida</span><span class="sxs-lookup"><span data-stu-id="17c77-213">&gt; Outbound Rules</span></span>
6. <span data-ttu-id="17c77-214">&gt; Acciones</span><span class="sxs-lookup"><span data-stu-id="17c77-214">&gt; Actions</span></span>
7. <span data-ttu-id="17c77-215">&gt; Nueva regla</span><span class="sxs-lookup"><span data-stu-id="17c77-215">&gt; New Rule</span></span>

<span data-ttu-id="17c77-216">Si el programa cliente se hospeda en una máquina virtual (VM) de Azure, debe leer:</span><span class="sxs-lookup"><span data-stu-id="17c77-216">If your client program is hosted on an Azure virtual machine (VM), you should read:</span></span><br/><span data-ttu-id="17c77-217">[Puertos más allá del 1433 para ADO.NET 4.5 y SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="17c77-217">[Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

<span data-ttu-id="17c77-218">Para obtener información general acerca de la configuración de puertos y la dirección IP, consulte: [Firewall de Base de datos SQL de Azure](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="17c77-218">For background information about cofiguration of ports and IP address, see: [Azure SQL Database firewall](sql-database-firewall-configure.md)</span></span>

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a><span data-ttu-id="17c77-219">Conexión: ADO.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="17c77-219">Connection: ADO.NET 4.6.1</span></span>
<span data-ttu-id="17c77-220">Si el programa utiliza las clases de ADO.NET como **System.Data.SqlClient.SqlConnection** tooconnect tooAzure base de datos SQL, se recomienda que use .NET Framework versión 4.6.1 o superior.</span><span class="sxs-lookup"><span data-stu-id="17c77-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** tooconnect tooAzure SQL Database, we recommend that you use .NET Framework version 4.6.1 or higher.</span></span>

<span data-ttu-id="17c77-221">ADO.NET 4.6.1:</span><span class="sxs-lookup"><span data-stu-id="17c77-221">ADO.NET 4.6.1:</span></span>

* <span data-ttu-id="17c77-222">Base de datos de SQL Azure, hay mayor confiabilidad cuando se abre una conexión mediante el uso de hello **SqlConnection.Open** método.</span><span class="sxs-lookup"><span data-stu-id="17c77-222">For Azure SQL Database, there is improved reliability when you open a connection by using hello **SqlConnection.Open** method.</span></span> <span data-ttu-id="17c77-223">Hola **abiertos** método incorpora ahora mejor mecanismos de reintento de esfuerzo en errores de respuesta tootransient, para determinados errores en tiempo de espera de conexión de Hola.</span><span class="sxs-lookup"><span data-stu-id="17c77-223">hello **Open** method now incorporates best effort retry mechanisms in response tootransient faults, for certain errors within hello Connection Timeout period.</span></span>
* <span data-ttu-id="17c77-224">Admite la agrupación de conexiones.</span><span class="sxs-lookup"><span data-stu-id="17c77-224">Supports connection pooling.</span></span> <span data-ttu-id="17c77-225">Esto incluye una comprobación eficaz que Hola conexión objeto proporciona el programa está funcionando.</span><span class="sxs-lookup"><span data-stu-id="17c77-225">This includes an efficient verification that hello connection object it gives your program is functioning.</span></span>

<span data-ttu-id="17c77-226">Cuando se utiliza un objeto de conexión desde un grupo de conexiones, se recomienda que el programa temporalmente cerrar conexión hello cuando lo use no inmediatamente.</span><span class="sxs-lookup"><span data-stu-id="17c77-226">When you use a connection object from a connection pool, we recommend that your program temporarily close hello connection when not immediately using it.</span></span> <span data-ttu-id="17c77-227">Volver a abrir una conexión no es caro Hola crear una nueva conexión de forma.</span><span class="sxs-lookup"><span data-stu-id="17c77-227">Re-opening a connection is not expensive hello way creating a new connection is.</span></span>

<span data-ttu-id="17c77-228">Si está usando ADO.NET 4.0 o versiones anteriores, se recomienda que actualice toohello ADO.NET más reciente.</span><span class="sxs-lookup"><span data-stu-id="17c77-228">If you are using ADO.NET 4.0 or earlier, we recommend that you upgrade toohello latest ADO.NET.</span></span>

* <span data-ttu-id="17c77-229">Desde noviembre de 2015 se puede [descargar ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span><span class="sxs-lookup"><span data-stu-id="17c77-229">As of November 2015, you can [download ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span></span>

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a><span data-ttu-id="17c77-230">Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="17c77-230">Diagnostics</span></span>
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a><span data-ttu-id="17c77-231">Diagnóstico: Probar si las utilidades pueden conectarse</span><span class="sxs-lookup"><span data-stu-id="17c77-231">Diagnostics: Test whether utilities can connect</span></span>
<span data-ttu-id="17c77-232">Si el programa presenta tooconnect tooAzure base de datos SQL, una opción de diagnóstico es tootry tooconnect con un programa de utilidad.</span><span class="sxs-lookup"><span data-stu-id="17c77-232">If your program is failing tooconnect tooAzure SQL Database, one diagnostic option is tootry tooconnect with a utility program.</span></span> <span data-ttu-id="17c77-233">Lo ideal es que se conectará la utilidad de hello mediante el uso de Hola la misma biblioteca que usa el programa.</span><span class="sxs-lookup"><span data-stu-id="17c77-233">Ideally hello utility would connect by using hello same library that your program uses.</span></span>

<span data-ttu-id="17c77-234">En cualquier equipo con Windows, puede probar estas utilidades:</span><span class="sxs-lookup"><span data-stu-id="17c77-234">On any Windows computer, you can try these utilities:</span></span>

* <span data-ttu-id="17c77-235">SQL Server Management Studio (ssms.exe), que se conecta mediante ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="17c77-235">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET.</span></span>
* <span data-ttu-id="17c77-236">sqlcmd.exe, que se conecta mediante [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span><span class="sxs-lookup"><span data-stu-id="17c77-236">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span></span>

<span data-ttu-id="17c77-237">Una vez conectado, compruebe que funciona una breve consulta SELECT de SQL.</span><span class="sxs-lookup"><span data-stu-id="17c77-237">Once connected, test whether a short SQL SELECT query works.</span></span>

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-hello-open-ports"></a><span data-ttu-id="17c77-238">Diagnóstico: Puertos abiertos de Hola de comprobación</span><span class="sxs-lookup"><span data-stu-id="17c77-238">Diagnostics: Check hello open ports</span></span>
<span data-ttu-id="17c77-239">Supongamos que se sospecha que se producen errores en los intentos de conexión debido a problemas de tooport.</span><span class="sxs-lookup"><span data-stu-id="17c77-239">Suppose you suspect that connection attempts are failing due tooport issues.</span></span> <span data-ttu-id="17c77-240">En el equipo puede ejecutar una utilidad que informa sobre las configuraciones de puerto de Hola.</span><span class="sxs-lookup"><span data-stu-id="17c77-240">On your computer you can run a utility that reports on hello port configurations.</span></span>

<span data-ttu-id="17c77-241">En Linux Hola utilidades siguientes pueden ser útiles:</span><span class="sxs-lookup"><span data-stu-id="17c77-241">On Linux hello following utilities might be helpful:</span></span>

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * <span data-ttu-id="17c77-242">(Cambiar toobe de valor de ejemplo de Hola su dirección IP).</span><span class="sxs-lookup"><span data-stu-id="17c77-242">(Change hello example value toobe your IP address.)</span></span>

<span data-ttu-id="17c77-243">En Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utilidad puede resultar útil.</span><span class="sxs-lookup"><span data-stu-id="17c77-243">On Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span></span> <span data-ttu-id="17c77-244">Esta es una ejecución de ejemplo que consultar la situación de puerto de hello en un servidor de base de datos de SQL Azure, y que se ejecute en un equipo portátil:</span><span class="sxs-lookup"><span data-stu-id="17c77-244">Here is an example execution that queried hello port situation on an Azure SQL Database server, and which was run on a laptop computer:</span></span>

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting tooresolve name tooIP address...
Name resolved too23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a><span data-ttu-id="17c77-245">Diagnóstico: Registrar los errores</span><span class="sxs-lookup"><span data-stu-id="17c77-245">Diagnostics: Log your errors</span></span>
<span data-ttu-id="17c77-246">A veces un problema intermitente se diagnostica mejor mediante la detección de un patrón general durante varios días o semanas.</span><span class="sxs-lookup"><span data-stu-id="17c77-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span></span>

<span data-ttu-id="17c77-247">El cliente puede ayudar al diagnóstico mediante el registro de todos los errores que encuentra.</span><span class="sxs-lookup"><span data-stu-id="17c77-247">Your client can assist in a diagnosis by logging all errors it encounters.</span></span> <span data-ttu-id="17c77-248">Es posible que pueda toocorrelate entradas del registro de hello con datos de error que inicie una base de datos de SQL Azure propio internamente.</span><span class="sxs-lookup"><span data-stu-id="17c77-248">You might be able toocorrelate hello log entries with error data that Azure SQL Database logs itself internally.</span></span>

<span data-ttu-id="17c77-249">Enterprise Library 6 (EntLib60) ofrece tooassist de clases administradas de .NET con el registro:</span><span class="sxs-lookup"><span data-stu-id="17c77-249">Enterprise Library 6 (EntLib60) offers .NET managed classes tooassist with logging:</span></span>

* [<span data-ttu-id="17c77-250">5 - como fácil como están fuera de un registro de: utilizando Hola bloque de aplicación de registro</span><span class="sxs-lookup"><span data-stu-id="17c77-250">5 - As Easy As Falling Off a Log: Using hello Logging Application Block</span></span>](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a><span data-ttu-id="17c77-251">Diagnóstico: Examinar los registros del sistema en busca de errores</span><span class="sxs-lookup"><span data-stu-id="17c77-251">Diagnostics: Examine system logs for errors</span></span>
<span data-ttu-id="17c77-252">Presentamos algunas instrucciones SELECT de Transact-SQL que consultan los registros de error y otra información.</span><span class="sxs-lookup"><span data-stu-id="17c77-252">Here are some Transact-SQL SELECT statements that query logs of error and other information.</span></span>

| <span data-ttu-id="17c77-253">Consulta de un registro</span><span class="sxs-lookup"><span data-stu-id="17c77-253">Query of log</span></span> | <span data-ttu-id="17c77-254">Descripción</span><span class="sxs-lookup"><span data-stu-id="17c77-254">Description</span></span> |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |<span data-ttu-id="17c77-255">Hola [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) vista proporciona información acerca de los eventos individuales, incluidas algunas que pueden causar errores transitorios o errores de conectividad.</span><span class="sxs-lookup"><span data-stu-id="17c77-255">hello [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, including some that can cause transient errors or connectivity failures.</span></span><br/><br/><span data-ttu-id="17c77-256">Lo ideal es que se puede poner en correlación hello **start_time** o **end_time** valores con información acerca de si su programa cliente tenido problemas.</span><span class="sxs-lookup"><span data-stu-id="17c77-256">Ideally you can correlate hello **start_time** or **end_time** values with information about when your client program experienced problems.</span></span><br/><br/><span data-ttu-id="17c77-257">**Sugerencia:** debe conectarse toohello **principal** la base de datos toorun esto.</span><span class="sxs-lookup"><span data-stu-id="17c77-257">**TIP:** You must connect toohello **master** database toorun this.</span></span> |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |<span data-ttu-id="17c77-258">Hola [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) Vista ofrece recuentos agregados de los tipos de eventos para realizar diagnósticos adicionales.</span><span class="sxs-lookup"><span data-stu-id="17c77-258">hello [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types, for additional diagnostics.</span></span><br/><br/><span data-ttu-id="17c77-259">**Sugerencia:** debe conectarse toohello **principal** la base de datos toorun esto.</span><span class="sxs-lookup"><span data-stu-id="17c77-259">**TIP:** You must connect toohello **master** database toorun this.</span></span> |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-hello-sql-database-log"></a><span data-ttu-id="17c77-260">Diagnóstico: Búsqueda para los eventos de problema de registro de base de datos SQL de Hola</span><span class="sxs-lookup"><span data-stu-id="17c77-260">Diagnostics: Search for problem events in hello SQL Database log</span></span>
<span data-ttu-id="17c77-261">Puede buscar entradas sobre los eventos del problema en el registro de hello de base de datos de SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="17c77-261">You can search for entries about problem events in hello log of Azure SQL Database.</span></span> <span data-ttu-id="17c77-262">Intente Hola después de la instrucción SELECT de Transact-SQL en hello **maestro** base de datos:</span><span class="sxs-lookup"><span data-stu-id="17c77-262">Try hello following Transact-SQL SELECT statement in hello **master** database:</span></span>

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a><span data-ttu-id="17c77-263">Algunas filas devueltas de sys.fn_xe_telemetry_blob_target_read_file</span><span class="sxs-lookup"><span data-stu-id="17c77-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span></span>
<span data-ttu-id="17c77-264">Después se muestra el aspecto de una fila devuelta.</span><span class="sxs-lookup"><span data-stu-id="17c77-264">Next is what a returned row might look like.</span></span> <span data-ttu-id="17c77-265">Hola valores null que se muestra a menudo no son nulos, en otras filas.</span><span class="sxs-lookup"><span data-stu-id="17c77-265">hello null values shown are often not null in other rows.</span></span>

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a><span data-ttu-id="17c77-266">Enterprise Library 6</span><span class="sxs-lookup"><span data-stu-id="17c77-266">Enterprise Library 6</span></span>
<span data-ttu-id="17c77-267">Enterprise Library 6 (EntLib60) es un marco de clases de .NET que ayuda a implementar a los clientes sólidos de servicios en la nube, uno de los cuales es el servicio de base de datos de SQL Azure de Hola.</span><span class="sxs-lookup"><span data-stu-id="17c77-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is hello Azure SQL Database service.</span></span> <span data-ttu-id="17c77-268">Puede encontrar el área de temas tooeach dedicado en el que puede ayudar EntLib60 visitando primera:</span><span class="sxs-lookup"><span data-stu-id="17c77-268">You can locate topics dedicated tooeach area in which EntLib60 can assist by first visiting:</span></span>

* [<span data-ttu-id="17c77-269">Enterprise Library 6: abril de 2013</span><span class="sxs-lookup"><span data-stu-id="17c77-269">Enterprise Library 6 - April 2013</span></span>](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

<span data-ttu-id="17c77-270">La lógica de reintento para controlar los errores transitorios es un área en la que puede ayudar EntLib60:</span><span class="sxs-lookup"><span data-stu-id="17c77-270">Retry logic for handling transient errors is one area in which EntLib60 can assist:</span></span>

* [<span data-ttu-id="17c77-271">4 - su perseverancia, secreto de todos los logros: mediante Hola Transient Fault Handling Application Block</span><span class="sxs-lookup"><span data-stu-id="17c77-271">4 - Perseverance, Secret of All Triumphs: Using hello Transient Fault Handling Application Block</span></span>](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> <span data-ttu-id="17c77-272">Hello código fuente de EntLib60 está disponible para el público [descargar](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span><span class="sxs-lookup"><span data-stu-id="17c77-272">hello source code for EntLib60 is available for public [download](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span></span> <span data-ttu-id="17c77-273">Microsoft no tiene ninguna característica adicional de planes toomake tooEntLib las actualizaciones de mantenimiento o actualizaciones.</span><span class="sxs-lookup"><span data-stu-id="17c77-273">Microsoft has no plans toomake further feature updates or maintenance updates tooEntLib.</span></span>
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a><span data-ttu-id="17c77-274">Clases de EntLib60 para errores transitorios y reintentos</span><span class="sxs-lookup"><span data-stu-id="17c77-274">EntLib60 classes for transient errors and retry</span></span>
<span data-ttu-id="17c77-275">Hola después de las clases de EntLib60 es especialmente útil para la lógica de reintento.</span><span class="sxs-lookup"><span data-stu-id="17c77-275">hello following EntLib60 classes are particularly useful for retry logic.</span></span> <span data-ttu-id="17c77-276">Hola a todos estos son en, o son más bajo, espacio de nombres **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span><span class="sxs-lookup"><span data-stu-id="17c77-276">All these  are in, or are further under, hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span></span>

<span data-ttu-id="17c77-277">*En el espacio de nombres de hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span><span class="sxs-lookup"><span data-stu-id="17c77-277">*In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span></span>

* <span data-ttu-id="17c77-278">**RetryPolicy**</span><span class="sxs-lookup"><span data-stu-id="17c77-278">**RetryPolicy** class</span></span>
  
  * <span data-ttu-id="17c77-279">**ExecuteAction**</span><span class="sxs-lookup"><span data-stu-id="17c77-279">**ExecuteAction** method</span></span>
* <span data-ttu-id="17c77-280">**ExponentialBackoff**</span><span class="sxs-lookup"><span data-stu-id="17c77-280">**ExponentialBackoff** class</span></span>
* <span data-ttu-id="17c77-281">**SqlDatabaseTransientErrorDetectionStrategy**</span><span class="sxs-lookup"><span data-stu-id="17c77-281">**SqlDatabaseTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="17c77-282">**ReliableSqlConnection**</span><span class="sxs-lookup"><span data-stu-id="17c77-282">**ReliableSqlConnection** class</span></span>
  
  * <span data-ttu-id="17c77-283">**ExecuteCommand**</span><span class="sxs-lookup"><span data-stu-id="17c77-283">**ExecuteCommand** method</span></span>

<span data-ttu-id="17c77-284">En el espacio de nombres de hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span><span class="sxs-lookup"><span data-stu-id="17c77-284">In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span></span>

* <span data-ttu-id="17c77-285">**AlwaysTransientErrorDetectionStrategy**</span><span class="sxs-lookup"><span data-stu-id="17c77-285">**AlwaysTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="17c77-286">**NeverTransientErrorDetectionStrategy**</span><span class="sxs-lookup"><span data-stu-id="17c77-286">**NeverTransientErrorDetectionStrategy** class</span></span>

<span data-ttu-id="17c77-287">Estos son vínculos tooinformation sobre EntLib60:</span><span class="sxs-lookup"><span data-stu-id="17c77-287">Here are links tooinformation about EntLib60:</span></span>

* <span data-ttu-id="17c77-288">Libre [Descargar libreta: tooMicrosoft de guía del desarrollador Enterprise Library, 2ª edición](http://www.microsoft.com/download/details.aspx?id=41145)</span><span class="sxs-lookup"><span data-stu-id="17c77-288">Free [Book Download: Developer's Guide tooMicrosoft Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span></span>
* <span data-ttu-id="17c77-289">Procedimientos recomendados: [Orientación general sobre reintentos](../best-practices-retry-general.md) tiene una excelente explicación detallada de la lógica de reintento.</span><span class="sxs-lookup"><span data-stu-id="17c77-289">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span></span>
* <span data-ttu-id="17c77-290">Descarga de NuGet de [Enterprise Library: Bloque de aplicación de control de errores transitorios 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span><span class="sxs-lookup"><span data-stu-id="17c77-290">NuGet download of [Enterprise Library - Transient Fault Handling application block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span></span>

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-hello-logging-block"></a><span data-ttu-id="17c77-291">EntLib60: bloque de registro hello</span><span class="sxs-lookup"><span data-stu-id="17c77-291">EntLib60: hello logging block</span></span>
* <span data-ttu-id="17c77-292">bloque de registro de Hello es una solución altamente configurable y flexible que le permite:</span><span class="sxs-lookup"><span data-stu-id="17c77-292">hello Logging block is a highly flexible and configurable solution that allows you to:</span></span>
  
  * <span data-ttu-id="17c77-293">Crear y almacenar los mensajes de registro en una amplia variedad de ubicaciones.</span><span class="sxs-lookup"><span data-stu-id="17c77-293">Create and store log messages in a wide variety of locations.</span></span>
  * <span data-ttu-id="17c77-294">Clasificar y filtrar los mensajes.</span><span class="sxs-lookup"><span data-stu-id="17c77-294">Categorize and filter messages.</span></span>
  * <span data-ttu-id="17c77-295">Recopilar la información contextual es útil para la depuración y el seguimiento, así como para los requisitos de registro generales y de auditoría.</span><span class="sxs-lookup"><span data-stu-id="17c77-295">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span></span>
* <span data-ttu-id="17c77-296">bloque de registro de Hello abstrae Hola la funcionalidad del registro de destino de registro de hello para que el código de la aplicación hello es coherente, independientemente de la ubicación de Hola y el tipo de almacén de registro de destino de Hola.</span><span class="sxs-lookup"><span data-stu-id="17c77-296">hello Logging block abstracts hello logging functionality from hello log destination so that hello application code is consistent, irrespective of hello location and type of hello target logging store.</span></span>

<span data-ttu-id="17c77-297">Para obtener más información, consulte: [5 - como fácil como están fuera de un registro de: utilizando Hola bloque de aplicación de registro](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="17c77-297">For details see: [5 - As Easy As Falling Off a Log: Using hello Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span></span>

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a><span data-ttu-id="17c77-298">Código fuente del método IsTransient de EntLib60</span><span class="sxs-lookup"><span data-stu-id="17c77-298">EntLib60 IsTransient method source code</span></span>
<span data-ttu-id="17c77-299">Después, desde hello **SqlDatabaseTransientErrorDetectionStrategy** de clases, se muestra código fuente hello C# hello **IsTransient** método.</span><span class="sxs-lookup"><span data-stu-id="17c77-299">Next, from hello **SqlDatabaseTransientErrorDetectionStrategy** class, is hello C# source code for hello **IsTransient** method.</span></span> <span data-ttu-id="17c77-300">código fuente de Hello aclara qué errores se tuvieron en cuenta toobe transitorio y que vuelva a intentar a partir de abril de 2013.</span><span class="sxs-lookup"><span data-stu-id="17c77-300">hello source code clarifies which errors were considered toobe transient and worthy of retry, as of April 2013.</span></span>

<span data-ttu-id="17c77-301">Numerosos **//comment** líneas se han quitado de esta legibilidad tooemphasize de copia.</span><span class="sxs-lookup"><span data-stu-id="17c77-301">Numerous **//comment** lines have been removed from this copy tooemphasize readability.</span></span>

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in hello exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // hello service is currently busy. Retry hello request after 10 seconds.
            // Code: (reason code toobe decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode hello reason code from hello error message to
            // determine hello grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach hello decoded values as additional attributes to
            // hello original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // hello instance of SQL Server you attempted tooconnect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a><span data-ttu-id="17c77-302">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="17c77-302">Next steps</span></span>
* <span data-ttu-id="17c77-303">Para solucionar otros problemas comunes de conexión de base de datos de SQL Azure, visite [tooAzure base de datos SQL de problemas de conexión de la solución de problemas](sql-database-troubleshoot-common-connection-issues.md).</span><span class="sxs-lookup"><span data-stu-id="17c77-303">For troubleshooting other common Azure SQL Database connection issues, visit [Troubleshoot connection issues tooAzure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span></span>
* [<span data-ttu-id="17c77-304">Agrupación de conexiones de SQL Server (ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="17c77-304">SQL Server Connection Pooling (ADO.NET)</span></span>](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [<span data-ttu-id="17c77-305">*Volver a intentar* es una licencia de Apache 2.0 general Reintentando la biblioteca, escrita en **Python**, tarea de hello toosimplify de agregar toojust de comportamiento de reintento sobre cualquier elemento.</span><span class="sxs-lookup"><span data-stu-id="17c77-305">*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in **Python**, toosimplify hello task of adding retry behavior toojust about anything.</span></span>](https://pypi.python.org/pypi/retrying)

