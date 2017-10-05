---
title: "Ejecución de tareas en cuentas de usuario en Azure Batch | Microsoft Docs"
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
ms.openlocfilehash: d408c0565c0ed81fc97cc2b3976a4fc233e31302
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="run-tasks-under-user-accounts-in-batch"></a><span data-ttu-id="2286d-103">Ejecución de tareas en cuentas de usuario en Batch</span><span class="sxs-lookup"><span data-stu-id="2286d-103">Run tasks under user accounts in Batch</span></span>

<span data-ttu-id="2286d-104">En Azure Batch, las tareas siempre se ejecutan en una cuenta de usuario.</span><span class="sxs-lookup"><span data-stu-id="2286d-104">A task in Azure Batch always runs under a user account.</span></span> <span data-ttu-id="2286d-105">De forma predeterminada, las tareas se ejecutan en cuentas de usuario estándar, sin permisos de administrador.</span><span class="sxs-lookup"><span data-stu-id="2286d-105">By default, tasks run under standard user accounts, without administrator permissions.</span></span> <span data-ttu-id="2286d-106">Esta configuración de cuenta de usuario predeterminada es normalmente suficiente.</span><span class="sxs-lookup"><span data-stu-id="2286d-106">These default user account settings are typically sufficient.</span></span> <span data-ttu-id="2286d-107">Sin embargo, para determinados escenarios, resulta útil poder configurar la cuenta de usuario en que desea que se ejecute una tarea.</span><span class="sxs-lookup"><span data-stu-id="2286d-107">For certain scenarios, however, it's useful to be able to configure the user account under which you want a task to run.</span></span> <span data-ttu-id="2286d-108">En este artículo se describen los tipos de cuentas de usuario y cómo puede configurarlos para su escenario.</span><span class="sxs-lookup"><span data-stu-id="2286d-108">This article discusses the types of user accounts and how you can configure them for your scenario.</span></span>

## <a name="types-of-user-accounts"></a><span data-ttu-id="2286d-109">Tipos de cuentas de usuario</span><span class="sxs-lookup"><span data-stu-id="2286d-109">Types of user accounts</span></span>

<span data-ttu-id="2286d-110">Azure Batch proporciona dos tipos de cuentas de usuario para ejecutar tareas:</span><span class="sxs-lookup"><span data-stu-id="2286d-110">Azure Batch provides two types of user accounts for running tasks:</span></span>

- <span data-ttu-id="2286d-111">**Cuentas de usuario automático.**</span><span class="sxs-lookup"><span data-stu-id="2286d-111">**Auto-user accounts.**</span></span> <span data-ttu-id="2286d-112">Las cuentas de usuario automático son cuentas de usuario integradas que el servicio Batch crea automáticamente.</span><span class="sxs-lookup"><span data-stu-id="2286d-112">Auto-user accounts are built-in user accounts that are created automatically by the Batch service.</span></span> <span data-ttu-id="2286d-113">De forma predeterminada, las tareas se ejecutan en una cuenta de usuario automático.</span><span class="sxs-lookup"><span data-stu-id="2286d-113">By default, tasks run under an auto-user account.</span></span> <span data-ttu-id="2286d-114">Puede configurar la especificación de usuario automático de una tarea para indicar en qué cuenta de usuario automático se debería ejecutar esta.</span><span class="sxs-lookup"><span data-stu-id="2286d-114">You can configure the auto-user specification for a task to indicate under which auto-user account a task should run.</span></span> <span data-ttu-id="2286d-115">Además, permite especificar el nivel de elevación y el ámbito de la cuenta de usuario automático que ejecutará la tarea.</span><span class="sxs-lookup"><span data-stu-id="2286d-115">The auto-user specification allows you to specify the elevation level and scope of the auto-user account that will run the task.</span></span> 

- <span data-ttu-id="2286d-116">**Una cuenta de usuario con nombre.**</span><span class="sxs-lookup"><span data-stu-id="2286d-116">**A named user account.**</span></span> <span data-ttu-id="2286d-117">Puede especificar una o varias cuentas de usuario con nombre para un grupo cuando lo crea.</span><span class="sxs-lookup"><span data-stu-id="2286d-117">You can specify one or more named user accounts for a pool when you create the pool.</span></span> <span data-ttu-id="2286d-118">Se crea una cuenta de usuario en cada nodo del grupo.</span><span class="sxs-lookup"><span data-stu-id="2286d-118">Each user account is created on each node of the pool.</span></span> <span data-ttu-id="2286d-119">Además del nombre de la cuenta, especifique la contraseña de la cuenta de usuario, el nivel de elevación y, para grupos de Linux, la clave privada SSH.</span><span class="sxs-lookup"><span data-stu-id="2286d-119">In addition to the account name, you specify the user account password, elevation level, and, for Linux pools, the SSH private key.</span></span> <span data-ttu-id="2286d-120">Cuando agregue una tarea, puede especificar la cuenta de usuario con nombre en que la tarea se debe ejecutar.</span><span class="sxs-lookup"><span data-stu-id="2286d-120">When you add a task, you can specify the named user account under which that task should run.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="2286d-121">La versión 2017-01-01.4.0 del servicio Batch incluye un cambio importante que requiere que se actualice el código para llamar a esa versión.</span><span class="sxs-lookup"><span data-stu-id="2286d-121">The Batch service version 2017-01-01.4.0 introduces a breaking change that requires that you update your code to call that version.</span></span> <span data-ttu-id="2286d-122">Si va a migrar código desde una versión anterior de Batch, tenga en cuenta que la propiedad **runElevated** ya no se admite en las bibliotecas de cliente de la API de REST o Batch.</span><span class="sxs-lookup"><span data-stu-id="2286d-122">If you are migrating code from an older version of Batch, note that the **runElevated** property is no longer supported in the REST API or Batch client libraries.</span></span> <span data-ttu-id="2286d-123">Use la nueva propiedad **userIdentity** de una tarea para especificar el nivel de elevación.</span><span class="sxs-lookup"><span data-stu-id="2286d-123">Use the new **userIdentity** property of a task to specify elevation level.</span></span> <span data-ttu-id="2286d-124">Consulte la sección titulada [Actualización del código a la biblioteca de cliente de Batch más reciente](#update-your-code-to-the-latest-batch-client-library) para ver instrucciones rápidas para actualizar el código de Batch si usa una de las bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="2286d-124">See the section titled [Update your code to the latest Batch client library](#update-your-code-to-the-latest-batch-client-library) for quick guidelines for updating your Batch code if you are using one of the client libraries.</span></span>
>
>

> [!NOTE] 
> <span data-ttu-id="2286d-125">Las cuentas de usuario descritas en este artículo no son compatibles con el Protocolo de escritorio remoto (RDP) ni con Secure Shell (SSH) por seguridad.</span><span class="sxs-lookup"><span data-stu-id="2286d-125">The user accounts discussed in this article do not support Remote Desktop Protocol (RDP) or Secure Shell (SSH), for security reasons.</span></span> 
>
> <span data-ttu-id="2286d-126">Para conectarse a un nodo que ejecuta la configuración de máquina virtual Linux mediante SSH, consulte [Uso del escritorio remoto a una máquina virtual Linux en Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="2286d-126">To connect to a node running the Linux virtual machine configuration via SSH, see [Use Remote Desktop to a Linux VM in Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md).</span></span> <span data-ttu-id="2286d-127">Para conectarse a nodos que ejecutan Windows a través de RDP, consulte [Conexión a una máquina virtual de Windows Server](../virtual-machines/windows/connect-logon.md).</span><span class="sxs-lookup"><span data-stu-id="2286d-127">To connect to nodes running Windows via RDP, see [Connect to a Windows Server VM](../virtual-machines/windows/connect-logon.md).</span></span><br /><br />
> <span data-ttu-id="2286d-128">Para conectarse a un nodo que ejecuta la configuración del servicio en la nube a través de RDP, consulte [Habilitación de la conexión a Escritorio remoto para un rol de Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2286d-128">To connect to a node running the cloud service configuration via RDP, see [Enable Remote Desktop Connection for a Role in Azure Cloud Services](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).</span></span>
>
>

## <a name="user-account-access-to-files-and-directories"></a><span data-ttu-id="2286d-129">Acceso de la cuenta de usuario a archivos y directorios</span><span class="sxs-lookup"><span data-stu-id="2286d-129">User account access to files and directories</span></span>

<span data-ttu-id="2286d-130">Tanto las cuentas de usuario automático como las de usuario con nombre tienen acceso de lectura y escritura al directorio de trabajo, el directorio compartido y el directorio de tareas de instancias múltiples de la tarea.</span><span class="sxs-lookup"><span data-stu-id="2286d-130">Both an auto-user account and a named user account have read/write access to the task’s working directory, shared directory, and multi-instance tasks directory.</span></span> <span data-ttu-id="2286d-131">Ambos tipos de cuenta tienen acceso de lectura a los directorios de inicio y preparación del trabajo.</span><span class="sxs-lookup"><span data-stu-id="2286d-131">Both types of accounts have read access to the startup and job preparation directories.</span></span>

<span data-ttu-id="2286d-132">Si una tarea se ejecuta en la misma cuenta que se usó para ejecutar una tarea de inicio, la tarea tiene acceso de lectura y escritura al directorio de la tarea de inicio.</span><span class="sxs-lookup"><span data-stu-id="2286d-132">If a task runs under the same account that was used for running a start task, the task has read-write access to the start task directory.</span></span> <span data-ttu-id="2286d-133">De forma similar, si una tarea se ejecuta en la misma cuenta que se usó para ejecutar una tarea de preparación del trabajo, la tarea tiene acceso de lectura y escritura al directorio de preparación del trabajo de la tarea.</span><span class="sxs-lookup"><span data-stu-id="2286d-133">Similarly, if a task runs under the same account that was used for running a job preparation task, the task has read-write access to the job preparation task directory.</span></span> <span data-ttu-id="2286d-134">Si una tarea se ejecuta en una cuenta diferente a la de la tarea de inicio o de preparación del trabajo, la tarea solo tiene acceso de lectura al directorio correspondiente.</span><span class="sxs-lookup"><span data-stu-id="2286d-134">If a task runs under a different account than the start task or job preparation task, then the task has only read access to the respective directory.</span></span>

<span data-ttu-id="2286d-135">Para más información sobre cómo acceder a archivos y directorios desde una tarea, consulte [Desarrollo de soluciones de procesos paralelos a gran escala con Batch](batch-api-basics.md#files-and-directories).</span><span class="sxs-lookup"><span data-stu-id="2286d-135">For more information on accessing files and directories from a task, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#files-and-directories).</span></span>

## <a name="elevated-access-for-tasks"></a><span data-ttu-id="2286d-136">Acceso con privilegios elevados para tareas</span><span class="sxs-lookup"><span data-stu-id="2286d-136">Elevated access for tasks</span></span> 

<span data-ttu-id="2286d-137">El nivel de elevación de la cuenta de usuario indica si una tarea se ejecuta con acceso con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="2286d-137">The user account's elevation level indicates whether a task runs with elevated access.</span></span> <span data-ttu-id="2286d-138">Tanto las cuentas de usuario automático como las de usuario con nombre se pueden ejecutar con acceso con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="2286d-138">Both an auto-user account and a named user account can run with elevated access.</span></span> <span data-ttu-id="2286d-139">Las dos opciones para el nivel de elevación son:</span><span class="sxs-lookup"><span data-stu-id="2286d-139">The two options for elevation level are:</span></span>

- <span data-ttu-id="2286d-140">**NonAdmin:** la tarea se ejecuta como usuario estándar sin acceso con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="2286d-140">**NonAdmin:** The task runs as a standard user without elevated access.</span></span> <span data-ttu-id="2286d-141">El nivel de elevación predeterminado para una cuenta de usuario de Batch es siempre **NonAdmin**.</span><span class="sxs-lookup"><span data-stu-id="2286d-141">The default elevation level for a Batch user account is always **NonAdmin**.</span></span>
- <span data-ttu-id="2286d-142">**Admin:** la tarea se ejecuta como usuario con acceso con privilegios elevados y funciona con permisos de administrador completos.</span><span class="sxs-lookup"><span data-stu-id="2286d-142">**Admin:** The task runs as a user with elevated access and operates with full Administrator permissions.</span></span> 

## <a name="auto-user-accounts"></a><span data-ttu-id="2286d-143">Cuentas de usuario automático</span><span class="sxs-lookup"><span data-stu-id="2286d-143">Auto-user accounts</span></span>

<span data-ttu-id="2286d-144">De forma predeterminada, las tareas se ejecutan en Batch en una cuenta de usuario automático, como usuario estándar sin acceso con privilegios elevados y con el ámbito de la tarea.</span><span class="sxs-lookup"><span data-stu-id="2286d-144">By default, tasks run in Batch under an auto-user account, as a standard user without elevated access, and with task scope.</span></span> <span data-ttu-id="2286d-145">Cuando se configura la especificación de usuario automático para el ámbito de la tarea, el servicio Batch crea una cuenta de usuario automático solo para esa tarea.</span><span class="sxs-lookup"><span data-stu-id="2286d-145">When the auto-user specification is configured for task scope, the Batch service creates an auto-user account for that task only.</span></span>

<span data-ttu-id="2286d-146">La alternativa al ámbito de la tarea es el ámbito de grupo.</span><span class="sxs-lookup"><span data-stu-id="2286d-146">The alternative to task scope is pool scope.</span></span> <span data-ttu-id="2286d-147">Cuando se configura la especificación de usuario automático de una tarea para el ámbito de grupo, la tarea se ejecuta en una cuenta de usuario automático que está disponible para cualquier tarea del grupo.</span><span class="sxs-lookup"><span data-stu-id="2286d-147">When the auto-user specification for a task is configured for pool scope, the task runs under an auto-user account that is available to any task in the pool.</span></span> <span data-ttu-id="2286d-148">Para más información acerca del ámbito de grupo, consulte la sección [Ejecución de una tarea como usuario automático con ámbito de grupo](#run-a-task-as-the-autouser-with-pool-scope).</span><span class="sxs-lookup"><span data-stu-id="2286d-148">For more information about pool scope, see the section titled [Run a task as the auto-user with pool scope](#run-a-task-as-the-autouser-with-pool-scope).</span></span>   

<span data-ttu-id="2286d-149">El ámbito predeterminado es diferente en los nodos de Windows y Linux:</span><span class="sxs-lookup"><span data-stu-id="2286d-149">The default scope is different on Windows and Linux nodes:</span></span>

- <span data-ttu-id="2286d-150">En los nodos de Windows, las tareas se ejecutan en el ámbito de la tarea de forma predeterminada.</span><span class="sxs-lookup"><span data-stu-id="2286d-150">On Windows nodes, tasks run under task scope by default.</span></span>
- <span data-ttu-id="2286d-151">En los nodos de Linux, se ejecutan siempre en el ámbito de grupo.</span><span class="sxs-lookup"><span data-stu-id="2286d-151">Linux nodes always run under pool scope.</span></span>

<span data-ttu-id="2286d-152">Existen cuatro configuraciones posibles para la especificación de usuario automático, cada una de las cuales corresponde a una cuenta de usuario automático única:</span><span class="sxs-lookup"><span data-stu-id="2286d-152">There are four possible configurations for the auto-user specification, each of which corresponds to a unique auto-user account:</span></span>

- <span data-ttu-id="2286d-153">Acceso sin privilegios de administrador con ámbito de la tarea (la especificación de usuario automático predeterminada)</span><span class="sxs-lookup"><span data-stu-id="2286d-153">Non-admin access with task scope (the default auto-user specification)</span></span>
- <span data-ttu-id="2286d-154">Acceso de administrador (elevado) con ámbito de la tarea</span><span class="sxs-lookup"><span data-stu-id="2286d-154">Admin (elevated) access with task scope</span></span>
- <span data-ttu-id="2286d-155">Acceso sin privilegios de administrador con ámbito de grupo</span><span class="sxs-lookup"><span data-stu-id="2286d-155">Non-admin access with pool scope</span></span>
- <span data-ttu-id="2286d-156">Acceso de administrador con ámbito de grupo</span><span class="sxs-lookup"><span data-stu-id="2286d-156">Admin access with pool scope</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="2286d-157">Las tareas que se ejecutan en el ámbito de la tarea no tienen acceso de hecho a otras tareas en un nodo.</span><span class="sxs-lookup"><span data-stu-id="2286d-157">Tasks running under task scope do not have de facto access to other tasks on a node.</span></span> <span data-ttu-id="2286d-158">Sin embargo, un usuario malintencionado con acceso a la cuenta podría eludir esta restricción enviando una tarea que se ejecuta con privilegios de administrador y accediendo a los otros directorios de tareas.</span><span class="sxs-lookup"><span data-stu-id="2286d-158">However, a malicious user with access to the account could work around this restriction by submitting a task that runs with administrator privileges and accesses other task directories.</span></span> <span data-ttu-id="2286d-159">Un usuario malintencionado también podría utilizar RDP o SSH para conectarse a un nodo.</span><span class="sxs-lookup"><span data-stu-id="2286d-159">A malicious user could also use RDP or SSH to connect to a node.</span></span> <span data-ttu-id="2286d-160">Es importante proteger el acceso a las claves de la cuenta de Batch para evitar este escenario.</span><span class="sxs-lookup"><span data-stu-id="2286d-160">It's important to protect access to your Batch account keys to prevent such a scenario.</span></span> <span data-ttu-id="2286d-161">Si sospecha que su cuenta está en peligro, asegúrese de volver a generar las claves.</span><span class="sxs-lookup"><span data-stu-id="2286d-161">If you suspect your account may have been compromised, be sure to regenerate your keys.</span></span>
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a><span data-ttu-id="2286d-162">Ejecución de una tarea como usuario automático con acceso con privilegios elevados</span><span class="sxs-lookup"><span data-stu-id="2286d-162">Run a task as an auto-user with elevated access</span></span>

<span data-ttu-id="2286d-163">Puede configurar la especificación de usuario automático con privilegios de administrador cuando necesite ejecutar una tarea con acceso con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="2286d-163">You can configure the auto-user specification for administrator privileges when you need to run a task with elevated access.</span></span> <span data-ttu-id="2286d-164">Por ejemplo, una tarea de inicio puede necesitar acceso con privilegios elevados para instalar software en el nodo.</span><span class="sxs-lookup"><span data-stu-id="2286d-164">For example, a start task may need elevated access to install software on the node.</span></span>

> [!NOTE] 
> <span data-ttu-id="2286d-165">Por lo general, es mejor usar el acceso con privilegios elevados solo cuando sea necesario.</span><span class="sxs-lookup"><span data-stu-id="2286d-165">In general, it's best to use elevated access only when necessary.</span></span> <span data-ttu-id="2286d-166">Según los procedimientos recomendados, es aconsejable conceder los privilegios mínimos necesarios para lograr el resultado deseado.</span><span class="sxs-lookup"><span data-stu-id="2286d-166">Best practices recommend granting the minimum privilege necessary to achieve the desired outcome.</span></span> <span data-ttu-id="2286d-167">Por ejemplo, si una tarea de inicio instala software para el usuario actual, en lugar de para todos los usuarios, es posible que pueda evitar conceder acceso con privilegios elevados a tareas.</span><span class="sxs-lookup"><span data-stu-id="2286d-167">For example, if a start task installs software for the current user, instead of for all users, you may be able to avoid granting elevated access to tasks.</span></span> <span data-ttu-id="2286d-168">Puede configurar la especificación de usuario automático con ámbito de grupo y sin acceso con privilegios elevados para todas las tareas que haya que ejecutar en la misma cuenta, incluida la de inicio.</span><span class="sxs-lookup"><span data-stu-id="2286d-168">You can configure the auto-user specification for pool scope and non-admin access for all tasks that need to run under the same account, including the start task.</span></span> 
>
>

<span data-ttu-id="2286d-169">En los fragmentos de código siguientes, se muestra cómo configurar la especificación de usuario automático.</span><span class="sxs-lookup"><span data-stu-id="2286d-169">The following code snippets show how to configure the auto-user specification.</span></span> <span data-ttu-id="2286d-170">En los ejemplos se establece el nivel de elevación en `Admin` y el ámbito en `Task`.</span><span class="sxs-lookup"><span data-stu-id="2286d-170">The examples set the elevation level to `Admin` and the scope to `Task`.</span></span> <span data-ttu-id="2286d-171">El ámbito de tarea es la configuración predeterminada, pero se incluye aquí a modo informativo.</span><span class="sxs-lookup"><span data-stu-id="2286d-171">Task scope is the default setting, but is included here for the sake of example.</span></span>

#### <a name="batch-net"></a><span data-ttu-id="2286d-172">.NET de Batch</span><span class="sxs-lookup"><span data-stu-id="2286d-172">Batch .NET</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a><span data-ttu-id="2286d-173">Java de Batch</span><span class="sxs-lookup"><span data-stu-id="2286d-173">Batch Java</span></span>

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a><span data-ttu-id="2286d-174">Python de Batch</span><span class="sxs-lookup"><span data-stu-id="2286d-174">Batch Python</span></span>

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

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a><span data-ttu-id="2286d-175">Ejecución de una tarea como usuario automático con ámbito de grupo</span><span class="sxs-lookup"><span data-stu-id="2286d-175">Run a task as an auto-user with pool scope</span></span>

<span data-ttu-id="2286d-176">Cuando se aprovisiona un nodo, se crean dos cuentas de usuario automático para todo el grupo en cada nodo del grupo, una con acceso con privilegios elevados y otra sin él.</span><span class="sxs-lookup"><span data-stu-id="2286d-176">When a node is provisioned, two pool-wide auto-user accounts are created on each node in the pool, one with elevated access, and one without elevated access.</span></span> <span data-ttu-id="2286d-177">Si se establece el ámbito del usuario automático en el ámbito de grupo para una tarea determinada, se ejecuta la tarea en una de estas dos cuentas de usuario automático para todo el grupo.</span><span class="sxs-lookup"><span data-stu-id="2286d-177">Setting the auto-user's scope to pool scope for a given task runs the task under one of these two pool-wide auto-user accounts.</span></span> 

<span data-ttu-id="2286d-178">Cuando se especifica el ámbito de grupo para el usuario automático, todas las tareas que se ejecutan con acceso de administrador se ejecutan en la misma cuenta de usuario automático para todo el grupo.</span><span class="sxs-lookup"><span data-stu-id="2286d-178">When you specify pool scope for the auto-user, all tasks that run with administrator access run under the same pool-wide auto-user account.</span></span> <span data-ttu-id="2286d-179">De forma similar, las tareas que se ejecutan sin permisos de administrador también se ejecutan en una sola cuenta de usuario automático para todo el grupo.</span><span class="sxs-lookup"><span data-stu-id="2286d-179">Similarly, tasks that run without administrator permissions also run under a single pool-wide auto-user account.</span></span> 

> [!NOTE] 
> <span data-ttu-id="2286d-180">Las dos cuentas de usuario automático para todo el grupo son independientes.</span><span class="sxs-lookup"><span data-stu-id="2286d-180">The two pool-wide auto-user accounts are separate accounts.</span></span> <span data-ttu-id="2286d-181">Las tareas que se ejecutan en la cuenta administrativa para todo el grupo no pueden compartir datos con las que se ejecutan en la cuenta estándar y viceversa.</span><span class="sxs-lookup"><span data-stu-id="2286d-181">Tasks running under the pool-wide administrative account cannot share data with tasks running under the standard account, and vice versa.</span></span> 
>
>

<span data-ttu-id="2286d-182">La ventaja de ejecutarlas en la misma cuenta de usuario automático es que las tareas pueden compartir datos con otras tareas que se ejecuten en el mismo nodo.</span><span class="sxs-lookup"><span data-stu-id="2286d-182">The advantage to running under the same auto-user account is that tasks are able to share data with other tasks running on the same node.</span></span>

<span data-ttu-id="2286d-183">Un escenario en que se comparten secretos entre tareas es un ejemplo en el que resulta útil ejecutar tareas en una de las dos cuentas de usuario automático para todo el grupo.</span><span class="sxs-lookup"><span data-stu-id="2286d-183">Sharing secrets between tasks is one scenario where running tasks under one of the two pool-wide auto-user accounts is useful.</span></span> <span data-ttu-id="2286d-184">Por ejemplo, suponga que una tarea de inicio necesita aprovisionar un secreto en el nodo que pueden usar otras tareas.</span><span class="sxs-lookup"><span data-stu-id="2286d-184">For example, suppose a start task needs to provision a secret onto the node that other tasks can use.</span></span> <span data-ttu-id="2286d-185">Podría usar la API de protección de datos de Windows (DPAPI), pero requiere privilegios de administrador.</span><span class="sxs-lookup"><span data-stu-id="2286d-185">You could use the Windows Data Protection API (DPAPI), but it requires administrator privileges.</span></span> <span data-ttu-id="2286d-186">En su lugar, puede proteger el secreto en el nivel de usuario.</span><span class="sxs-lookup"><span data-stu-id="2286d-186">Instead, you can protect the secret at the user level.</span></span> <span data-ttu-id="2286d-187">Las tareas que se ejecutan en la misma cuenta de usuario pueden acceder al secreto sin necesidad del acceso con privilegios elevados.</span><span class="sxs-lookup"><span data-stu-id="2286d-187">Tasks running under the same user account can access the secret without elevated access.</span></span>

<span data-ttu-id="2286d-188">Otro escenario donde podría ejecutar tareas en una cuenta de usuario automático con ámbito de grupo es un recurso compartido de archivos de interfaz de paso de mensajes (MPI).</span><span class="sxs-lookup"><span data-stu-id="2286d-188">Another scenario where you may want to run tasks under an auto-user account with pool scope is a Message Passing Interface (MPI) file share.</span></span> <span data-ttu-id="2286d-189">Un recurso compartido de archivos MPI es útil cuando los nodos de la tarea MPI necesitan trabajar en los mismos datos de archivo.</span><span class="sxs-lookup"><span data-stu-id="2286d-189">An MPI file share is useful when the nodes in the MPI task need to work on the same file data.</span></span> <span data-ttu-id="2286d-190">El nodo principal crea un recurso compartido de archivos al que los nodos secundarios pueden acceder si se ejecutan en la misma cuenta de usuario automático.</span><span class="sxs-lookup"><span data-stu-id="2286d-190">The head node creates a file share that the child nodes can access if they are running under the same auto-user account.</span></span> 

<span data-ttu-id="2286d-191">En el fragmento de código siguiente se establece el ámbito del usuario automático en el ámbito de grupo para una tarea en .NET de Batch.</span><span class="sxs-lookup"><span data-stu-id="2286d-191">The following code snippet sets the auto-user's scope to pool scope for a task in Batch .NET.</span></span> <span data-ttu-id="2286d-192">Se omite el nivel de elevación, de forma que la tarea se ejecuta en la cuenta de usuario automático estándar para todo el grupo.</span><span class="sxs-lookup"><span data-stu-id="2286d-192">The elevation level is omitted, so the task runs under the standard pool-wide auto-user account.</span></span>

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a><span data-ttu-id="2286d-193">Cuentas de usuario con nombre</span><span class="sxs-lookup"><span data-stu-id="2286d-193">Named user accounts</span></span>

<span data-ttu-id="2286d-194">Puede definir cuentas de usuario con nombre cuando cree un grupo.</span><span class="sxs-lookup"><span data-stu-id="2286d-194">You can define named user accounts when you create a pool.</span></span> <span data-ttu-id="2286d-195">Una cuenta de usuario con nombre tiene el nombre y la contraseña que proporcione.</span><span class="sxs-lookup"><span data-stu-id="2286d-195">A named user account has a name and password that you provide.</span></span> <span data-ttu-id="2286d-196">Puede especificar el nivel de elevación para una cuenta de usuario con nombre.</span><span class="sxs-lookup"><span data-stu-id="2286d-196">You can specify the elevation level for a named user account.</span></span> <span data-ttu-id="2286d-197">Para los nodos de Linux, también puede proporcionar una clave privada SSH.</span><span class="sxs-lookup"><span data-stu-id="2286d-197">For Linux nodes, you can also provide an SSH private key.</span></span>

<span data-ttu-id="2286d-198">Existe una cuenta de usuario con nombre en todos los nodos del grupo y está disponible para todas las tareas que se ejecuten en esos nodos.</span><span class="sxs-lookup"><span data-stu-id="2286d-198">A named user account exists on all nodes in the pool and is available to all tasks running on those nodes.</span></span> <span data-ttu-id="2286d-199">Puede definir cualquier número de usuarios con nombre para un grupo.</span><span class="sxs-lookup"><span data-stu-id="2286d-199">You may define any number of named users for a pool.</span></span> <span data-ttu-id="2286d-200">Cuando agregue una tarea o una colección de tareas, puede especificar que la tarea se ejecute en una de las cuentas de usuario con nombre definidas en el grupo.</span><span class="sxs-lookup"><span data-stu-id="2286d-200">When you add a task or task collection, you can specify that the task runs under one of the named user accounts defined on the pool.</span></span>

<span data-ttu-id="2286d-201">Una cuenta de usuario con nombre es útil cuando desea ejecutar todas las tareas de un trabajo en la misma cuenta de usuario, al mismo tiempo que las mantiene aisladas de las tareas que se ejecutan en otros trabajos.</span><span class="sxs-lookup"><span data-stu-id="2286d-201">A named user account is useful when you want to run all tasks in a job under the same user account, but isolate them from tasks running in other jobs at the same time.</span></span> <span data-ttu-id="2286d-202">Por ejemplo, puede crear un usuario con nombre para cada trabajo y ejecutar las tareas de cada trabajo en dicha cuenta de usuario con nombre.</span><span class="sxs-lookup"><span data-stu-id="2286d-202">For example, you can create a named user for each job, and run each job's tasks under that named user account.</span></span> <span data-ttu-id="2286d-203">Entonces, cada trabajo puede compartir un secreto con sus propias tareas, pero no con las que se ejecutan en otros trabajos.</span><span class="sxs-lookup"><span data-stu-id="2286d-203">Each job can then share a secret with its own tasks, but not with tasks running in other jobs.</span></span>

<span data-ttu-id="2286d-204">También puede usar una cuenta de usuario con nombre para ejecutar una tarea que establezca permisos en recursos externos, como recursos compartidos de archivos.</span><span class="sxs-lookup"><span data-stu-id="2286d-204">You can also use a named user account to run a task that sets permissions on external resources such as file shares.</span></span> <span data-ttu-id="2286d-205">Con una cuenta de usuario con nombre, controla la identidad del usuario y puede usarla para establecer permisos.</span><span class="sxs-lookup"><span data-stu-id="2286d-205">With a named user account, you control the user identity and can use that user identity to set permissions.</span></span>  

<span data-ttu-id="2286d-206">Las cuentas de usuario con nombre permiten SSH sin contraseña entre nodos de Linux.</span><span class="sxs-lookup"><span data-stu-id="2286d-206">Named user accounts enable password-less SSH between Linux nodes.</span></span> <span data-ttu-id="2286d-207">Puede usar una cuenta de usuario con nombre con nodos de Linux que necesiten ejecutar tareas de instancias múltiples.</span><span class="sxs-lookup"><span data-stu-id="2286d-207">You can use a named user account with Linux nodes that need to run multi-instance tasks.</span></span> <span data-ttu-id="2286d-208">Cada nodo del grupo puede ejecutar tareas en una cuenta de usuario definida en el grupo completo.</span><span class="sxs-lookup"><span data-stu-id="2286d-208">Each node in the pool can run tasks under a user account defined on the whole pool.</span></span> <span data-ttu-id="2286d-209">Para más información acerca de las tareas de instancias múltiples, consulte [Uso de tareas de instancias múltiples para ejecutar aplicaciones MPI](batch-mpi.md).</span><span class="sxs-lookup"><span data-stu-id="2286d-209">For more information about multi-instance tasks, see [Use multi\-instance tasks to run MPI applications](batch-mpi.md).</span></span>

### <a name="create-named-user-accounts"></a><span data-ttu-id="2286d-210">Creación de cuentas de usuario con nombre</span><span class="sxs-lookup"><span data-stu-id="2286d-210">Create named user accounts</span></span>

<span data-ttu-id="2286d-211">Para crear cuentas de usuario con nombre en Batch, agregue una colección de cuentas de usuario al grupo.</span><span class="sxs-lookup"><span data-stu-id="2286d-211">To create named user accounts in Batch, add a collection of user accounts to the pool.</span></span> <span data-ttu-id="2286d-212">En los fragmentos de código siguientes se muestra cómo crear cuentas de usuario con nombre en .NET, Java y Python.</span><span class="sxs-lookup"><span data-stu-id="2286d-212">The following code snippets show how to create named user accounts in .NET, Java, and Python.</span></span> <span data-ttu-id="2286d-213">En estos fragmentos de código se muestra cómo crear cuentas con nombre con y sin derechos administrativos en un grupo.</span><span class="sxs-lookup"><span data-stu-id="2286d-213">These code snippets show how to create both admin and non-admin named accounts on a pool.</span></span> <span data-ttu-id="2286d-214">En los ejemplos se crean grupos que usan la configuración del servicio en la nube, pero se utiliza el mismo enfoque al crear un grupo de Windows o Linux con la configuración de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="2286d-214">The examples create pools using the cloud service configuration, but you use the same approach when creating a Windows or Linux pool using the virtual machine configuration.</span></span>

#### <a name="batch-net-example-windows"></a><span data-ttu-id="2286d-215">Ejemplo de .NET de Batch (Windows)</span><span class="sxs-lookup"><span data-stu-id="2286d-215">Batch .NET example (Windows)</span></span>

```csharp
CloudPool pool = null;
Console.WriteLine("Creating pool [{0}]...", poolId);

// Create a pool using the cloud service configuration.
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

// Commit the pool.
await pool.CommitAsync();
```

#### <a name="batch-net-example-linux"></a><span data-ttu-id="2286d-216">Ejemplo de .NET de Batch (Linux)</span><span class="sxs-lookup"><span data-stu-id="2286d-216">Batch .NET example (Linux)</span></span>

```csharp
CloudPool pool = null;

// Obtain a collection of all available node agent SKUs.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of the VM image to use.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain the first node agent SKU in the collection that matches
// Ubuntu Server 14.04. 
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create the virtual machine configuration to use to create the pool.
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

Console.WriteLine("Creating pool [{0}]...", poolId);

// Create the unbound pool.
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

// Commit the pool.
await pool.CommitAsync();
```


#### <a name="batch-java-example"></a><span data-ttu-id="2286d-217">Ejemplo de Java de Batch</span><span class="sxs-lookup"><span data-stu-id="2286d-217">Batch Java example</span></span>

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

#### <a name="batch-python-example"></a><span data-ttu-id="2286d-218">Ejemplo de Python de Batch</span><span class="sxs-lookup"><span data-stu-id="2286d-218">Batch Python example</span></span>

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

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a><span data-ttu-id="2286d-219">Ejecución de una tarea en una cuenta de usuario con nombre con acceso con privilegios elevados</span><span class="sxs-lookup"><span data-stu-id="2286d-219">Run a task under a named user account with elevated access</span></span>

<span data-ttu-id="2286d-220">Para ejecutar una tarea como usuario con privilegios elevados, establezca la propiedad **UserIdentity** de la tarea en una cuenta de usuario con nombre que se creó con la propiedad **ElevationLevel** establecida en `Admin`.</span><span class="sxs-lookup"><span data-stu-id="2286d-220">To run a task as an elevated user, set the task's **UserIdentity** property to a named user account that was created with its **ElevationLevel** property set to `Admin`.</span></span>

<span data-ttu-id="2286d-221">En este fragmento de código se especifica que la tarea debe ejecutarse en una cuenta de usuario con nombre.</span><span class="sxs-lookup"><span data-stu-id="2286d-221">This code snippet specifies that the task should run under a named user account.</span></span> <span data-ttu-id="2286d-222">Esta cuenta de usuario con nombre se definió en el grupo cuando este se creó.</span><span class="sxs-lookup"><span data-stu-id="2286d-222">This named user account was defined on the pool when the pool was created.</span></span> <span data-ttu-id="2286d-223">En este caso, la cuenta de usuario con nombre se creó con permisos de administrador:</span><span class="sxs-lookup"><span data-stu-id="2286d-223">In this case, the named user account was created with admin permissions:</span></span>

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-to-the-latest-batch-client-library"></a><span data-ttu-id="2286d-224">Actualización del código a la biblioteca de cliente de Batch más reciente</span><span class="sxs-lookup"><span data-stu-id="2286d-224">Update your code to the latest Batch client library</span></span>

<span data-ttu-id="2286d-225">La versión 2017-01-01.4.0 del servicio Batch incluye un cambio importante: se reemplaza la propiedad **runElevated** disponible en versiones anteriores por la propiedad **userIdentity**.</span><span class="sxs-lookup"><span data-stu-id="2286d-225">The Batch service version 2017-01-01.4.0 introduces a breaking change, replacing the **runElevated** property available in earlier versions with the **userIdentity** property.</span></span> <span data-ttu-id="2286d-226">En las siguientes tablas se proporciona una asignación sencilla que sirve para actualizar el código de versiones anteriores de las bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="2286d-226">The following tables provide a simple mapping that you can use to update your code from earlier versions of the client libraries.</span></span>

### <a name="batch-net"></a><span data-ttu-id="2286d-227">.NET de Batch</span><span class="sxs-lookup"><span data-stu-id="2286d-227">Batch .NET</span></span>

| <span data-ttu-id="2286d-228">Si el código usa…</span><span class="sxs-lookup"><span data-stu-id="2286d-228">If your code uses...</span></span>                  | <span data-ttu-id="2286d-229">Actualícelo a…</span><span class="sxs-lookup"><span data-stu-id="2286d-229">Update it to....</span></span>                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| <span data-ttu-id="2286d-230">`CloudTask.RunElevated` sin especificar</span><span class="sxs-lookup"><span data-stu-id="2286d-230">`CloudTask.RunElevated` not specified</span></span> | <span data-ttu-id="2286d-231">No se requiere actualización</span><span class="sxs-lookup"><span data-stu-id="2286d-231">No update required</span></span>                                                                                               |

### <a name="batch-java"></a><span data-ttu-id="2286d-232">Java de Batch</span><span class="sxs-lookup"><span data-stu-id="2286d-232">Batch Java</span></span>

| <span data-ttu-id="2286d-233">Si el código usa…</span><span class="sxs-lookup"><span data-stu-id="2286d-233">If your code uses...</span></span>                      | <span data-ttu-id="2286d-234">Actualícelo a…</span><span class="sxs-lookup"><span data-stu-id="2286d-234">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| <span data-ttu-id="2286d-235">`CloudTask.withRunElevated` sin especificar</span><span class="sxs-lookup"><span data-stu-id="2286d-235">`CloudTask.withRunElevated` not specified</span></span> | <span data-ttu-id="2286d-236">No se requiere actualización</span><span class="sxs-lookup"><span data-stu-id="2286d-236">No update required</span></span>                                                                                                                     |

### <a name="batch-python"></a><span data-ttu-id="2286d-237">Python de Batch</span><span class="sxs-lookup"><span data-stu-id="2286d-237">Batch Python</span></span>

| <span data-ttu-id="2286d-238">Si el código usa…</span><span class="sxs-lookup"><span data-stu-id="2286d-238">If your code uses...</span></span>                      | <span data-ttu-id="2286d-239">Actualícelo a…</span><span class="sxs-lookup"><span data-stu-id="2286d-239">Update it to....</span></span>                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | <span data-ttu-id="2286d-240">`user_identity=user`, donde</span><span class="sxs-lookup"><span data-stu-id="2286d-240">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | <span data-ttu-id="2286d-241">`user_identity=user`, donde</span><span class="sxs-lookup"><span data-stu-id="2286d-241">`user_identity=user`, where</span></span> <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| <span data-ttu-id="2286d-242">`run_elevated` sin especificar</span><span class="sxs-lookup"><span data-stu-id="2286d-242">`run_elevated` not specified</span></span> | <span data-ttu-id="2286d-243">No se requiere actualización</span><span class="sxs-lookup"><span data-stu-id="2286d-243">No update required</span></span>                                                                                                                                  |


## <a name="next-steps"></a><span data-ttu-id="2286d-244">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="2286d-244">Next steps</span></span>

### <a name="batch-forum"></a><span data-ttu-id="2286d-245">Foro de Batch</span><span class="sxs-lookup"><span data-stu-id="2286d-245">Batch Forum</span></span>

<span data-ttu-id="2286d-246">El [foro de Azure Batch](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) en MSDN es un lugar excelente para debatir y formular preguntas sobre el servicio.</span><span class="sxs-lookup"><span data-stu-id="2286d-246">The [Azure Batch Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) on MSDN is a great place to discuss Batch and ask questions about the service.</span></span> <span data-ttu-id="2286d-247">Lea los útiles mensajes anclados y envíe sus preguntas a medida que surjan mientras compila sus soluciones del servicio Batch.</span><span class="sxs-lookup"><span data-stu-id="2286d-247">Head on over for helpful pinned posts, and post your questions as they arise while you build your Batch solutions.</span></span>