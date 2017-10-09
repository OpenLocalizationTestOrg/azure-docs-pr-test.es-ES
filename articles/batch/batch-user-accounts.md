---
title: tareas de aaaRun correspondientes a las cuentas de usuario en Azure Batch | Documentos de Microsoft
description: Configure cuentas de usuario para ejecutar tareas en Azure Batch
services: batch
author: tamram
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.openlocfilehash: 13d7d76451d89a3cca090c4ef24ed0ed781bbf09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="45224-103">Ejecución de tareas en cuentas de usuario en Batch</span><span class="sxs-lookup"><span data-stu-id="45224-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="45224-104">En Azure Batch, las tareas siempre se ejecutan en una cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="45224-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="45224-105">De forma predeterminada, las tareas se ejecutan en cuentas de usuario estándar, sin permisos de administrador.</span><span class="sxs-lookup"><span data-stu-id="45224-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="45224-106">Esta configuración de cuenta de usuario predeterminada es normalmente suficiente.</span><span class="sxs-lookup"><span data-stu-id="45224-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="45224-107">Sin embargo, para determinados escenarios, es útil toobe tooconfigure capaz de cuenta de usuario de hello en la que desea que una tarea toorun.</span><span class="sxs-lookup"><span data-stu-id="45224-107">For certain scenarios, however, it's useful toobe able tooconfigure hello user account under which you want a task toorun.</span></span> <span data-ttu-id="45224-108">En este artículo se describe los tipos de Hola de cuentas de usuario y cómo se puede configurar para su escenario.</span><span class="sxs-lookup"><span data-stu-id="45224-108">This article discusses hello types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="45224-109">Tipos de cuentas de usuario</span><span class="sxs-lookup"><span data-stu-id="45224-109">Types of user accounts</span></span>

<span data-ttu-id="45224-110">Azure Batch proporciona dos tipos de cuentas de usuario para ejecutar tareas:</span><span class="sxs-lookup"><span data-stu-id="45224-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="45224-111">**Cuentas de usuario automático.**</span><span class="sxs-lookup"><span data-stu-id="45224-111">**Auto-user accounts.**</span></span> <span data-ttu-id="45224-112">Las cuentas de usuario automática son cuentas de usuario integradas se crean automáticamente por hello servicio por lotes.</span><span class="sxs-lookup"><span data-stu-id="45224-112">Auto-user accounts are built-in user accounts that are created automatically by hello Batch service.</span></span> <span data-ttu-id="45224-113">De forma predeterminada, las tareas se ejecutan en una cuenta de usuario automático.</span><span class="sxs-lookup"><span data-stu-id="45224-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="45224-114">Puede configurar la especificación de usuario automática de Hola para un tooindicate de tarea en qué usuario automática debe ejecutar una tarea de la cuenta.</span><span class="sxs-lookup"><span data-stu-id="45224-114">You can configure hello auto-user specification for a task tooindicate under which auto-user account a task should run.</span></span> <span data-ttu-id="45224-115">especificación de usuario automática de Hello permite toospecify nivel de elevación de Hola y el ámbito de la cuenta de usuario automática de Hola que se ejecutará la tarea hello.</span><span class="sxs-lookup"><span data-stu-id="45224-115">hello auto-user specification allows you toospecify hello elevation level and scope of hello auto-user account that will run hello task.</span></span> 

- <span data-ttu-id="45224-116">**Una cuenta de usuario con nombre.**</span><span class="sxs-lookup"><span data-stu-id="45224-116">**A named user account.**</span></span> <span data-ttu-id="45224-117">Puede especificar una o varias cuentas de usuario con nombre para un grupo al crear el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="45224-117">You can specify one or more named user accounts for a pool when you create hello pool.</span></span> <span data-ttu-id="45224-118">Cada cuenta de usuario se crea en cada nodo del grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="45224-118">Each user account is created on each node of hello pool.</span></span> <span data-ttu-id="45224-119">Además el nombre de la cuenta de toohello, especificar contraseña de cuenta de usuario de hello, elevación nivel y, para grupos de Linux, la clave privada de hello SSH.</span><span class="sxs-lookup"><span data-stu-id="45224-119">In addition toohello account name, you specify hello user account password, elevation level, and, for Linux pools, hello SSH private key.</span></span> <span data-ttu-id="45224-120">Al agregar una tarea, puede especificar Hola con el nombre de cuenta de usuario bajo la que se debe ejecutar esa tarea.</span><span class="sxs-lookup"><span data-stu-id="45224-120">When you add a task, you can specify hello named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="45224-121">versión de servicio de lote de Hello 2017-01-01.4.0 presenta un cambio importante que requiere que actualice su código toocall esa versión.</span><span class="sxs-lookup"><span data-stu-id="45224-121">hello Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code toocall that version.</span></span> <span data-ttu-id="45224-122">Si es migrar código desde una versión anterior del lote, tenga en cuenta que hello **runElevated** propiedad ya no se admite en bibliotecas de cliente de API de REST o proceso por lotes de Hola.</span><span class="sxs-lookup"><span data-stu-id="45224-122">If you are migrating code from an older version of Batch, note that hello **runElevated** property is no longer supported in hello REST API or Batch client libraries.</span></span> <span data-ttu-id="45224-123">Hola de uso nueva **userIdentity** propiedad de un nivel de elevación de toospecify de tarea.</span><span class="sxs-lookup"><span data-stu-id="45224-123">Use hello new **userIdentity** property of a task toospecify elevation level.</span></span> <span data-ttu-id="45224-124">Consulte la sección de hello [actualizar la biblioteca de cliente de lote más reciente de código toohello](#update-your-code-to-the-latest-batch-client-library) para rápido instrucciones detalladas para actualizar el código de proceso por lotes si usa una de las bibliotecas de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="45224-124">See hello section titled [Update your code toohello latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of hello client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="45224-125">las cuentas de usuario de Hello descritas en este artículo no son compatibles con el protocolo de escritorio remoto (RDP) o Shell seguro (SSH), por motivos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="45224-125">hello user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="45224-126">tooconnect tooa nodo ejecución Hola Linux configuración de máquina virtual a través de SSH, consulte [tooa de uso de escritorio remoto VM de Linux en Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="45224-126">tooconnect tooa node running hello Linux virtual machine configuration via SSH, see [Use Remote Desktop tooa Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="45224-127">toonodes tooconnect ejecutan Windows a través de RDP, consulte [conectar tooa VM de Windows Server](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="45224-127">tooconnect toonodes running Windows via RDP, see [Connect tooa Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="45224-128">tooconnect tooa nodo ejecución Hola nube configuración del servicio a través de RDP, consulte [Habilitar conexión a Escritorio remoto para un rol de servicios de nube de Azure](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span><span class="sxs-lookup"><span data-stu-id="45224-128">tooconnect tooa node running hello cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-toofiles-and-directories"></a><span data-ttu-id="45224-129">Directorios y toofiles de acceso de cuenta de usuario</span><span class="sxs-lookup"><span data-stu-id="45224-129">User account access toofiles and directories</span></span>

<span data-ttu-id="45224-130">Una cuenta de usuario automática y una cuenta de usuario con nombre tienen el directorio de trabajo de la tarea del toohello del acceso de lectura/escritura, el directorio compartido y el directorio de tareas de varias instancias.</span><span class="sxs-lookup"><span data-stu-id="45224-130">Both an auto-user account and a named user account have read/write access toohello task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="45224-131">Ambos tipos de cuentas tienen acceso de lectura directorios de toohello inicio y trabajo de preparación.</span><span class="sxs-lookup"><span data-stu-id="45224-131">Both types of accounts have read access toohello startup and job preparation directories.</span></span>

<span data-ttu-id="45224-132">Si una tarea se ejecuta bajo Hola misma cuenta que se usó para ejecutar una tarea de inicio, la tarea hello tiene directorio de tareas de inicio de toohello de acceso de lectura y escritura.</span><span class="sxs-lookup"><span data-stu-id="45224-132">If a task runs under hello same account that was used for running a start task, hello task has read-write access toohello start task directory.</span></span> <span data-ttu-id="45224-133">De forma similar, si una tarea se ejecuta bajo Hola misma cuenta que se usó para ejecutar una tarea de preparación del trabajo, la tarea hello tiene el directorio de trabajo de acceso de lectura y escritura toohello tareas preparación.</span><span class="sxs-lookup"><span data-stu-id="45224-133">Similarly, if a task runs under hello same account that was used for running a job preparation task, hello task has read-write access toohello job preparation task directory.</span></span> <span data-ttu-id="45224-134">Si una tarea se ejecuta bajo una cuenta diferente de la tarea de inicio de Hola o tarea de preparación de trabajos, tarea hello tiene solo las directorio correspondiente de las toohello acceso de lectura.</span><span class="sxs-lookup"><span data-stu-id="45224-134">If a task runs under a different account than hello start task or job preparation task, then hello task has only read access toohello respective directory.</span></span>

<span data-ttu-id="45224-135">Para más información sobre cómo acceder a archivos y directorios desde una tarea, consulte [Desarrollo de soluciones de procesos paralelos a gran escala con Batch](batch-api-basics.md#files-and-directories).</span><span class="sxs-lookup"><span data-stu-id="45224-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="45224-136">Acceso con privilegios elevados para tareas</span><span class="sxs-lookup"><span data-stu-id="45224-136">Elevated access for tasks</span></span> 

<span data-ttu-id="45224-137">nivel de elevación de la cuenta de usuario de Hello indica si una tarea se ejecuta con acceso con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="45224-137">hello user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="45224-138">Tanto las cuentas de usuario automático como las de usuario con nombre se pueden ejecutar con acceso con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="45224-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="45224-139">Hola dos opciones para el nivel de elevación son:</span><span class="sxs-lookup"><span data-stu-id="45224-139">hello two options for elevation level are:</span></span>

- <span data-ttu-id="45224-140">**NonAdmin:** tarea hello se ejecuta como un usuario estándar sin acceso con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="45224-140">**NonAdmin:** hello task runs as a standard user without elevated access.</span></span> <span data-ttu-id="45224-141">nivel de elevación de Hello predeterminado para una cuenta de usuario de lote es siempre **NonAdmin**.</span><span class="sxs-lookup"><span data-stu-id="45224-141">hello default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="45224-142">**Administrador:** tarea hello se ejecuta como un usuario con acceso con privilegios elevados y funciona con permisos de administrador completos.</span><span class="sxs-lookup"><span data-stu-id="45224-142">**Admin:** hello task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="45224-143">Cuentas de usuario automático</span><span class="sxs-lookup"><span data-stu-id="45224-143">Auto-user accounts</span></span>

<span data-ttu-id="45224-144">De forma predeterminada, las tareas se ejecutan en Batch en una cuenta de usuario automático, como usuario estándar sin acceso con privilegios elevados y con el ámbito de la tarea.</span><span class="sxs-lookup"><span data-stu-id="45224-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="45224-145">Cuando se configura la especificación de usuario automática de Hola para el ámbito de la tarea, servicio por lotes de hello crea una cuenta de usuario automática para dicha tarea solo.</span><span class="sxs-lookup"><span data-stu-id="45224-145">When hello auto-user specification is configured for task scope, hello Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="45224-146">ámbito de Hello tootask alternativo es el ámbito de grupo.</span><span class="sxs-lookup"><span data-stu-id="45224-146">hello alternative tootask scope is pool scope.</span></span> <span data-ttu-id="45224-147">Cuando se configura Hola auto-especificación para una tarea para el ámbito de grupo, Hola tarea se ejecuta bajo una cuenta de usuario automático es tarea tooany disponible en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="45224-147">When hello auto-user specification for a task is configured for pool scope, hello task runs under an auto-user account that is available tooany task in hello pool.</span></span> <span data-ttu-id="45224-148">Para obtener más información acerca del ámbito de grupo, consulte sección hello [ejecutar una tarea como Hola auto-usuarios cuyo ámbito de grupo](#run-a-task-as-the-autouser-with-pool-scope).</span><span class="sxs-lookup"><span data-stu-id="45224-148">For more information about pool scope, see hello section titled [Run a task as hello auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="45224-149">ámbito predeterminado de Hello es diferente en los nodos de Windows y Linux:</span><span class="sxs-lookup"><span data-stu-id="45224-149">hello default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="45224-150">En los nodos de Windows, las tareas se ejecutan en el ámbito de la tarea de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="45224-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="45224-151">En los nodos de Linux, se ejecutan siempre en el ámbito de grupo.</span><span class="sxs-lookup"><span data-stu-id="45224-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="45224-152">Hay cuatro configuraciones posibles para la especificación de usuario automática de hello, cada uno de los cuales corresponde tooa única auto-cuenta de usuario:</span><span class="sxs-lookup"><span data-stu-id="45224-152">There are four possible configurations for hello auto-user specification, each of which corresponds tooa unique auto-user account:</span></span>

- <span data-ttu-id="45224-153">Acceso sin privilegios de administrador con ámbito de la tarea (especificación de usuario automática de hello predeterminado)</span><span class="sxs-lookup"><span data-stu-id="45224-153">Non-admin access with task scope (hello default auto-user specification)</span></span>
- <span data-ttu-id="45224-154">Acceso de administrador (elevado) con ámbito de la tarea</span><span class="sxs-lookup"><span data-stu-id="45224-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="45224-155">Acceso sin privilegios de administrador con ámbito de grupo</span><span class="sxs-lookup"><span data-stu-id="45224-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="45224-156">Acceso de administrador con ámbito de grupo</span><span class="sxs-lookup"><span data-stu-id="45224-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="45224-157">Tareas que se ejecutan en el ámbito de la tarea no tiene de hecho acceso tooother tareas en un nodo.</span><span class="sxs-lookup"><span data-stu-id="45224-157">Tasks running under task scope do not have de facto access tooother tasks on a node.</span></span> <span data-ttu-id="45224-158">Sin embargo, un usuario malintencionado con la cuenta de acceso de toohello puede evitar esta limitación mediante el envío de una tarea que se ejecuta con privilegios de administrador y tiene acceso a otros directorios de la tarea.</span><span class="sxs-lookup"><span data-stu-id="45224-158">However, a malicious user with access toohello account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="45224-159">Un usuario malintencionado también podría utilizar el nodo de tooa tooconnect RDP o SSH.</span><span class="sxs-lookup"><span data-stu-id="45224-159">A malicious user could also use RDP or SSH tooconnect tooa node.</span></span> <span data-ttu-id="45224-160">Es importante tooprotect acceso tooyour lote cuenta claves tooprevent este escenario.</span><span class="sxs-lookup"><span data-stu-id="45224-160">It's important tooprotect access tooyour Batch account keys tooprevent such a scenario.</span></span> <span data-ttu-id="45224-161">Si sospecha que se han comprometido su cuenta, ser tooregenerate seguro de las claves.</span><span class="sxs-lookup"><span data-stu-id="45224-161">If you suspect your account may have been compromised, be sure tooregenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="45224-162">Ejecución de una tarea como usuario automático con acceso con privilegios elevados</span><span class="sxs-lookup"><span data-stu-id="45224-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="45224-163">Puede configurar Hola auto-especificación de privilegios de administrador cuando necesite toorun una tarea con acceso con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="45224-163">You can configure hello auto-user specification for administrator privileges when you need toorun a task with elevated access.</span></span> <span data-ttu-id="45224-164">Por ejemplo, una tarea de inicio puede necesitar software para tooinstall el acceso con privilegios elevados en el nodo de Hola.</span><span class="sxs-lookup"><span data-stu-id="45224-164">For example, a start task may need elevated access tooinstall software on hello node.</span></span>

> [!NOTE] 
> <span data-ttu-id="45224-165">En general, es mejor toouse elevados acceso solo cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="45224-165">In general, it's best toouse elevated access only when necessary.</span></span> <span data-ttu-id="45224-166">Es recomendable conceder Hola privilegios mínimos necesarios tooachieve Hola el resultado deseado.</span><span class="sxs-lookup"><span data-stu-id="45224-166">Best practices recommend granting hello minimum privilege necessary tooachieve hello desired outcome.</span></span> <span data-ttu-id="45224-167">Por ejemplo, si una tarea de inicio instala el software para el usuario actual de hello, en lugar de para todos los usuarios, es posible que pueda tooavoid conceder acceso con privilegios elevados tootasks.</span><span class="sxs-lookup"><span data-stu-id="45224-167">For example, if a start task installs software for hello current user, instead of for all users, you may be able tooavoid granting elevated access tootasks.</span></span> <span data-ttu-id="45224-168">Puede configurar la especificación de usuario automática de hello para el acceso de ámbito y sin derechos administrativos de grupo para todas las tareas que necesitan toorun bajo la misma cuenta, incluida la tarea de inicio de hello de Hola.</span><span class="sxs-lookup"><span data-stu-id="45224-168">You can configure hello auto-user specification for pool scope and non-admin access for all tasks that need toorun under hello same account, including hello start task.</span></span> 
>
>

<span data-ttu-id="45224-169">Hola siguientes fragmentos de código muestra cómo tooconfigure Hola especificación de usuario automáticamente.</span><span class="sxs-lookup"><span data-stu-id="45224-169">hello following code snippets show how tooconfigure hello auto-user specification.</span></span> <span data-ttu-id="45224-170">ejemplos de Hello establecen nivel de elevación de hello demasiado`Admin` y Hola ámbito demasiado`Task`.</span><span class="sxs-lookup"><span data-stu-id="45224-170">hello examples set hello elevation level too`Admin` and hello scope too`Task`.</span></span> <span data-ttu-id="45224-171">Ámbito de la tarea es la configuración predeterminada de hello, pero se incluye aquí para simplificar Hola de ejemplo.</span><span class="sxs-lookup"><span data-stu-id="45224-171">Task scope is hello default setting, but is included here for hello sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="45224-172">.NET de Batch</span><span class="sxs-lookup"><span data-stu-id="45224-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="45224-173">Java de Batch</span><span class="sxs-lookup"><span data-stu-id="45224-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="45224-174">Python de Batch</span><span class="sxs-lookup"><span data-stu-id="45224-174">Batch Python</span></span>

```python
user = batchmodels.UserIdentity(
    auto_user=batchmodels.AutoUserSpecification(
        elevation_level=batchmodels.ElevationLevel.admin,
        scope=batchmodels.AutoUserScope.task))
task = batchmodels.TaskAddParameter(
    id='task_1',
    command_line='cmd /c "echo hello world"',
    user_identity=user)
batch_client.task.add(job_id=jobid, task=task)
```

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="45224-175">Ejecución de una tarea como usuario automático con ámbito de grupo</span><span class="sxs-lookup"><span data-stu-id="45224-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="45224-176">Cuando se aprovisiona un nodo, se crean las cuentas de usuario de automática de todo el grupo de dos en cada nodo de grupo de hello, uno con acceso con privilegios elevados y otro sin acceso con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="45224-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in hello pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="45224-177">Establecer ámbito de toopool de ámbito de hello automática del usuario para una tarea determinada, ejecuta la tarea de hello en alguna de estas cuentas de usuario de automática de todo el grupo de dos.</span><span class="sxs-lookup"><span data-stu-id="45224-177">Setting hello auto-user's scope toopool scope for a given task runs hello task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="45224-178">Cuando se especifica el ámbito de grupo de hello auto-usuario, todas las tareas que se ejecutan con acceso de administrador se ejecutan en hello misma cuenta de usuario automática de todo el grupo.</span><span class="sxs-lookup"><span data-stu-id="45224-178">When you specify pool scope for hello auto-user, all tasks that run with administrator access run under hello same pool-wide auto-user account.</span></span> <span data-ttu-id="45224-179">De forma similar, las tareas que se ejecutan sin permisos de administrador también se ejecutan en una sola cuenta de usuario automático para todo el grupo.</span><span class="sxs-lookup"><span data-stu-id="45224-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="45224-180">Hola auto-usuario de todo el grupo de dos cuentas es independientes.</span><span class="sxs-lookup"><span data-stu-id="45224-180">hello two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="45224-181">Tareas que se ejecutan bajo la cuenta administrativa de todo el grupo de hello no pueden compartir datos con tareas que se ejecutan bajo la cuenta estándar de Hola y viceversa.</span><span class="sxs-lookup"><span data-stu-id="45224-181">Tasks running under hello pool-wide administrative account cannot share data with tasks running under hello standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="45224-182">Hola toorunning ventaja en la misma cuenta de usuario automática es que las tareas son tooshare capaz de datos con otras tareas que se ejecutan en Hola de hello mismo nodo.</span><span class="sxs-lookup"><span data-stu-id="45224-182">hello advantage toorunning under hello same auto-user account is that tasks are able tooshare data with other tasks running on hello same node.</span></span>

<span data-ttu-id="45224-183">Uso compartido de información confidencial entre las tareas es un escenario donde la ejecución de tareas en una de las cuentas de usuario automática de todo el grupo de hello dos es útil.</span><span class="sxs-lookup"><span data-stu-id="45224-183">Sharing secrets between tasks is one scenario where running tasks under one of hello two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="45224-184">Por ejemplo, suponga que una tarea de inicio debe tooprovision un secreto en el nodo de Hola que pueden usar otras tareas.</span><span class="sxs-lookup"><span data-stu-id="45224-184">For example, suppose a start task needs tooprovision a secret onto hello node that other tasks can use.</span></span> <span data-ttu-id="45224-185">Podría utilizar la API de protección de datos (DPAPI) de Windows hello, pero requiere privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="45224-185">You could use hello Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="45224-186">En su lugar, puede proteger el secreto de hello en nivel de usuario de Hola.</span><span class="sxs-lookup"><span data-stu-id="45224-186">Instead, you can protect hello secret at hello user level.</span></span> <span data-ttu-id="45224-187">Tareas que se ejecutan bajo puede tener acceso la misma cuenta de usuario de Hola Hola secreto sin acceso con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="45224-187">Tasks running under hello same user account can access hello secret without elevated access.</span></span>

<span data-ttu-id="45224-188">Otro escenario que es conveniente toorun tareas correspondientes a una cuenta de usuario automática con ámbito de grupo es un archivo de interfaz de paso de mensajes (MPI) comparten.</span><span class="sxs-lookup"><span data-stu-id="45224-188">Another scenario where you may want toorun tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="45224-189">Un recurso compartido de archivos MPI es útil cuando los nodos Hola Hola MPI tarea necesidad toowork en Hola mismos datos de archivo.</span><span class="sxs-lookup"><span data-stu-id="45224-189">An MPI file share is useful when hello nodes in hello MPI task need toowork on hello same file data.</span></span> <span data-ttu-id="45224-190">nodo principal Hello crea un recurso compartido de archivos que pueden tener acceso los nodos secundarios Hola si se están ejecutando en hello misma cuenta de usuario automáticamente.</span><span class="sxs-lookup"><span data-stu-id="45224-190">hello head node creates a file share that hello child nodes can access if they are running under hello same auto-user account.</span></span> 

<span data-ttu-id="45224-191">Hola siguiente fragmento de código establece el ámbito de toopool de ámbito de hello automática del usuario para una tarea en .NET de lote.</span><span class="sxs-lookup"><span data-stu-id="45224-191">hello following code snippet sets hello auto-user's scope toopool scope for a task in Batch .NET.</span></span> <span data-ttu-id="45224-192">se omite el nivel de elevación de Hello, por lo que la tarea hello se ejecuta bajo la cuenta de usuario de automática de todo el grupo de estándar de Hola.</span><span class="sxs-lookup"><span data-stu-id="45224-192">hello elevation level is omitted, so hello task runs under hello standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="45224-193">Cuentas de usuario con nombre</span><span class="sxs-lookup"><span data-stu-id="45224-193">Named user accounts</span></span>

<span data-ttu-id="45224-194">Puede definir cuentas de usuario con nombre cuando cree un grupo.</span><span class="sxs-lookup"><span data-stu-id="45224-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="45224-195">Una cuenta de usuario con nombre tiene el nombre y la contraseña que proporcione.</span><span class="sxs-lookup"><span data-stu-id="45224-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="45224-196">Puede especificar el nivel de elevación de Hola para una cuenta de usuario con nombre.</span><span class="sxs-lookup"><span data-stu-id="45224-196">You can specify hello elevation level for a named user account.</span></span> <span data-ttu-id="45224-197">Para los nodos de Linux, también puede proporcionar una clave privada SSH.</span><span class="sxs-lookup"><span data-stu-id="45224-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="45224-198">Existe una cuenta de usuario con nombre en todos los nodos de grupo de Hola y tooall disponibles tareas se está ejecutando en esos nodos.</span><span class="sxs-lookup"><span data-stu-id="45224-198">A named user account exists on all nodes in hello pool and is available tooall tasks running on those nodes.</span></span> <span data-ttu-id="45224-199">Puede definir cualquier número de usuarios con nombre para un grupo.</span><span class="sxs-lookup"><span data-stu-id="45224-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="45224-200">Cuando se agrega una tarea o una colección de tareas, puede especificar que esa tarea Hola se ejecuta bajo una de hello con el nombre de las cuentas de usuario definidas en el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="45224-200">When you add a task or task collection, you can specify that hello task runs under one of hello named user accounts defined on hello pool.</span></span>

<span data-ttu-id="45224-201">Una cuenta de usuario con nombre es útil cuando se desea toorun todas las tareas de un trabajo en Hola la misma cuenta de usuario, pero aislarlas entre tareas que se ejecutan en otros trabajos en hello mismo tiempo.</span><span class="sxs-lookup"><span data-stu-id="45224-201">A named user account is useful when you want toorun all tasks in a job under hello same user account, but isolate them from tasks running in other jobs at hello same time.</span></span> <span data-ttu-id="45224-202">Por ejemplo, puede crear un usuario con nombre para cada trabajo y ejecutar las tareas de cada trabajo en dicha cuenta de usuario con nombre.</span><span class="sxs-lookup"><span data-stu-id="45224-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="45224-203">Entonces, cada trabajo puede compartir un secreto con sus propias tareas, pero no con las que se ejecutan en otros trabajos.</span><span class="sxs-lookup"><span data-stu-id="45224-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="45224-204">También puede utilizar un toorun de cuenta de usuario designado una tarea que establece permisos en recursos externos, como recursos compartidos de archivos.</span><span class="sxs-lookup"><span data-stu-id="45224-204">You can also use a named user account toorun a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="45224-205">Con una cuenta de usuario con nombre es controlan la identidad de usuario de Hola y puede usar los permisos de tooset de identidad de ese usuario.</span><span class="sxs-lookup"><span data-stu-id="45224-205">With a named user account, you control hello user identity and can use that user identity tooset permissions.</span></span>  

<span data-ttu-id="45224-206">Las cuentas de usuario con nombre permiten SSH sin contraseña entre nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="45224-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="45224-207">Puede usar una cuenta de usuario con nombre a los nodos de Linux que necesitan las tareas de varias instancias de toorun.</span><span class="sxs-lookup"><span data-stu-id="45224-207">You can use a named user account with Linux nodes that need toorun multi-instance tasks.</span></span> <span data-ttu-id="45224-208">Cada nodo de grupo de hello puede ejecutar tareas en una cuenta de usuario definida en grupo todo Hola.</span><span class="sxs-lookup"><span data-stu-id="45224-208">Each node in hello pool can run tasks under a user account defined on hello whole pool.</span></span> <span data-ttu-id="45224-209">Para obtener más información acerca de las tareas de varias instancias, consulte [usar múltiples\-instancia las tareas de las aplicaciones de MPI toorun](batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="45224-209">For more information about multi-instance tasks, see [Use multi\-instance tasks toorun MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="45224-210">Creación de cuentas de usuario con nombre</span><span class="sxs-lookup"><span data-stu-id="45224-210">Create named user accounts</span></span>

<span data-ttu-id="45224-211">toocreate con el nombre de las cuentas de usuario en proceso por lotes, agregue una colección de grupo de toohello de cuentas de usuario.</span><span class="sxs-lookup"><span data-stu-id="45224-211">toocreate named user accounts in Batch, add a collection of user accounts toohello pool.</span></span> <span data-ttu-id="45224-212">Hello fragmentos de código siguientes muestran cómo toocreate denominado cuentas de usuario de. NET, Java y Python.</span><span class="sxs-lookup"><span data-stu-id="45224-212">hello following code snippets show how toocreate named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="45224-213">Estos código fragmentos de código muestran cómo toocreate admin y sin derechos administrativos con el nombre de las cuentas en un grupo.</span><span class="sxs-lookup"><span data-stu-id="45224-213">These code snippets show how toocreate both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="45224-214">ejemplos de Hello crean grupos con la configuración del servicio de nube de hello, pero usar Hola mismo enfoque al crear un grupo de Windows o Linux mediante la configuración de máquina virtual de Hola.</span><span class="sxs-lookup"><span data-stu-id="45224-214">hello examples create pools using hello cloud service configuration, but you use hello same approach when creating a Windows or Linux pool using hello virtual machine configuration.</span></span>

#### <a name="batch-net-example-windows"></a><span data-ttu-id="45224-215">Ejemplo de .NET de Batch (Windows)</span><span class="sxs-lookup"><span data-stu-id="45224-215">Batch .NET example (Windows)</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using hello cloud service configuration.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                                         
    virtualMachineSize: "small",                                                
    cloudServiceConfiguration: new CloudServiceConfiguration(osFamily: "5"));   

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount("adminUser", "xyz123", ElevationLevel.Admin),
    new UserAccount("nonAdminUser", "123xyz", ElevationLevel.NonAdmin),
};

// Commit hello pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a><span data-ttu-id="45224-216">Ejemplo de .NET de Batch (Linux)</span><span class="sxs-lookup"><span data-stu-id="45224-216">Batch .NET example (Linux)</span></span>

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello virtual machine configuration toouse toocreate hello pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create hello unbound pool.
pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    targetDedicatedComputeNodes: 3,                                             
    virtualMachineSize: "Standard_A1",                                      
    virtualMachineConfiguration: virtualMachineConfiguration);                  

// Add named user accounts.
pool.UserAccounts = new List<UserAccount>
{
    new UserAccount(
        name: "adminUser",
        password: "xyz123",
        elevationLevel: ElevationLevel.Admin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 12345,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
    new UserAccount(
        name: "nonAdminUser",
        password: "123xyz",
        elevationLevel: ElevationLevel.NonAdmin,
        linuxUserConfiguration: new LinuxUserConfiguration(
            uid: 45678,
            gid: 98765,
            sshPrivateKey: new Guid().ToString()
            )),
};

// Commit hello pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a><span data-ttu-id="45224-217">Ejemplo de Java de Batch</span><span class="sxs-lookup"><span data-stu-id="45224-217">Batch Java example</span></span>

```java
List<UserAccount> userList = new ArrayList<>();
userList.add(new UserAccount().withName(adminUserAccountName).withPassword(adminPassword).withElevationLevel(ElevationLevel.ADMIN));
userList.add(new UserAccount().withName(nonAdminUserAccountName).withPassword(nonAdminPassword).withElevationLevel(ElevationLevel.NONADMIN));
PoolAddParameter addParameter = new PoolAddParameter()
        .withId(poolId)
        .withTargetDedicatedNodes(POOL_VM_COUNT)
        .withVmSize(POOL_VM_SIZE)
        .withCloudServiceConfiguration(configuration)
        .withUserAccounts(userList);
batchClient.poolOperations().createPool(addParameter);
```

#### <a name="batch-python-example"></a><span data-ttu-id="45224-218">Ejemplo de Python de Batch</span><span class="sxs-lookup"><span data-stu-id="45224-218">Batch Python example</span></span>

```python
users = [
    batchmodels.UserAccount(
        name='pool-admin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.admin)
    batchmodels.UserAccount(
        name='pool-nonadmin',
        password='******',
        elevation_level=batchmodels.ElevationLevel.nonadmin)
]
pool = batchmodels.PoolAddParameter(
    id=pool_id,
    user_accounts=users,
    virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
        image_reference=image_ref_to_use,
        node_agent_sku_id=sku_to_use),
    vm_size=vm_size,
    target_dedicated=vm_count)
batch_client.pool.add(pool)
```

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="45224-219">Ejecución de una tarea en una cuenta de usuario con nombre con acceso con privilegios elevados</span><span class="sxs-lookup"><span data-stu-id="45224-219">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="45224-220">toorun una tarea como de un usuario elevado, conjunto de tareas de hello **UserIdentity** tooa de propiedad con el nombre de cuenta de usuario que se creó con su **ElevationLevel** propiedad establecida demasiado`Admin`.</span><span class="sxs-lookup"><span data-stu-id="45224-220">toorun a task as an elevated user, set hello task's **UserIdentity** property tooa named user account that was created with its **ElevationLevel** property set too`Admin`.</span></span>

<span data-ttu-id="45224-221">Este fragmento de código especifica que la tarea hello debe ejecutarse bajo una cuenta de usuario con nombre.</span><span class="sxs-lookup"><span data-stu-id="45224-221">This code snippet specifies that hello task should run under a named user account.</span></span> <span data-ttu-id="45224-222">Esta cuenta de usuario con nombre se definió en el grupo de hello cuando se creó el grupo de Hola.</span><span class="sxs-lookup"><span data-stu-id="45224-222">This named user account was defined on hello pool when hello pool was created.</span></span> <span data-ttu-id="45224-223">En este caso, se creó Hola con el nombre de cuenta de usuario con permisos de administrador:</span><span class="sxs-lookup"><span data-stu-id="45224-223">In this case, hello named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-toohello-latest-batch-client-library"></a><span data-ttu-id="45224-224">Actualizar la biblioteca de cliente de lote más reciente de código toohello</span><span class="sxs-lookup"><span data-stu-id="45224-224">Update your code toohello latest Batch client library</span></span>

<span data-ttu-id="45224-225">versión del servicio de lote de Hello 2017-01-01.4.0 presenta un cambio importante, reemplazando hello **runElevated** propiedad disponible en versiones anteriores con hello **userIdentity** propiedad.</span><span class="sxs-lookup"><span data-stu-id="45224-225">hello Batch service version 2017-01-01.4.0 introduces a breaking change, replacing hello **runElevated** property available in earlier versions with hello **userIdentity** property.</span></span> <span data-ttu-id="45224-226">Hola las tablas siguientes proporciona una simple asignación que puede usar tooupdate su código desde versiones anteriores de las bibliotecas de cliente de Hola.</span><span class="sxs-lookup"><span data-stu-id="45224-226">hello following tables provide a simple mapping that you can use tooupdate your code from earlier versions of hello client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="45224-227">.NET de Batch</span><span class="sxs-lookup"><span data-stu-id="45224-227">Batch .NET</span></span>

| <span data-ttu-id="45224-228">Si el código usa…</span><span class="sxs-lookup"><span data-stu-id="45224-228">If your code uses...</span></span>                  | <span data-ttu-id="45224-229">Actualícelo a…</span><span class="sxs-lookup"><span data-stu-id="45224-229">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="45224-230">`CloudTask.RunElevated` sin especificar</span><span class="sxs-lookup"><span data-stu-id="45224-230">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="45224-231">No se requiere actualización</span><span class="sxs-lookup"><span data-stu-id="45224-231">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="45224-232">Java de Batch</span><span class="sxs-lookup"><span data-stu-id="45224-232">Batch Java</span></span>

| <span data-ttu-id="45224-233">Si el código usa…</span><span class="sxs-lookup"><span data-stu-id="45224-233">If your code uses...</span></span>                      | <span data-ttu-id="45224-234">Actualícelo a…</span><span class="sxs-lookup"><span data-stu-id="45224-234">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="45224-235">`CloudTask.withRunElevated` sin especificar</span><span class="sxs-lookup"><span data-stu-id="45224-235">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="45224-236">No se requiere actualización</span><span class="sxs-lookup"><span data-stu-id="45224-236">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="45224-237">Python de Batch</span><span class="sxs-lookup"><span data-stu-id="45224-237">Batch Python</span></span>

| <span data-ttu-id="45224-238">Si el código usa…</span><span class="sxs-lookup"><span data-stu-id="45224-238">If your code uses...</span></span>                      | <span data-ttu-id="45224-239">Actualícelo a…</span><span class="sxs-lookup"><span data-stu-id="45224-239">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="45224-240">`user_identity=user`, donde</span><span class="sxs-lookup"><span data-stu-id="45224-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="45224-241">`user_identity=user`, donde</span><span class="sxs-lookup"><span data-stu-id="45224-241">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="45224-242">`run_elevated` sin especificar</span><span class="sxs-lookup"><span data-stu-id="45224-242">`run_elevated` not specified</span></span> | <span data-ttu-id="45224-243">No se requiere actualización</span><span class="sxs-lookup"><span data-stu-id="45224-243">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="45224-244">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="45224-244">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="45224-245">Foro de Batch</span><span class="sxs-lookup"><span data-stu-id="45224-245">Batch Forum</span></span>

<span data-ttu-id="45224-246">Hola [foro de lote de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) en MSDN es una gran colocar toodiscuss por lotes y formular preguntas acerca del servicio de Hola.</span><span class="sxs-lookup"><span data-stu-id="45224-246">hello [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="45224-247">Lea los útiles mensajes anclados y envíe sus preguntas a medida que surjan mientras compila sus soluciones del servicio Batch.</span><span class="sxs-lookup"><span data-stu-id="45224-247">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>
