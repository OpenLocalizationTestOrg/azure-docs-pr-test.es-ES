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
# <a name="run-tasks-under-user-accounts-in-batch"></a>Ejecución de tareas en cuentas de usuario en Batch

En Azure Batch, las tareas siempre se ejecutan en una cuenta de usuario. De forma predeterminada, las tareas se ejecutan en cuentas de usuario estándar, sin permisos de administrador. Esta configuración de cuenta de usuario predeterminada es normalmente suficiente. Sin embargo, para determinados escenarios, es útil toobe tooconfigure capaz de cuenta de usuario de hello en la que desea que una tarea toorun. En este artículo se describe los tipos de Hola de cuentas de usuario y cómo se puede configurar para su escenario.

## <a name="types-of-user-accounts"></a>Tipos de cuentas de usuario

Azure Batch proporciona dos tipos de cuentas de usuario para ejecutar tareas:

- **Cuentas de usuario automático.** Las cuentas de usuario automática son cuentas de usuario integradas se crean automáticamente por hello servicio por lotes. De forma predeterminada, las tareas se ejecutan en una cuenta de usuario automático. Puede configurar la especificación de usuario automática de Hola para un tooindicate de tarea en qué usuario automática debe ejecutar una tarea de la cuenta. especificación de usuario automática de Hello permite toospecify nivel de elevación de Hola y el ámbito de la cuenta de usuario automática de Hola que se ejecutará la tarea hello. 

- **Una cuenta de usuario con nombre.** Puede especificar una o varias cuentas de usuario con nombre para un grupo al crear el grupo de Hola. Cada cuenta de usuario se crea en cada nodo del grupo de Hola. Además el nombre de la cuenta de toohello, especificar contraseña de cuenta de usuario de hello, elevación nivel y, para grupos de Linux, la clave privada de hello SSH. Al agregar una tarea, puede especificar Hola con el nombre de cuenta de usuario bajo la que se debe ejecutar esa tarea.

> [!IMPORTANT] 
> versión de servicio de lote de Hello 2017-01-01.4.0 presenta un cambio importante que requiere que actualice su código toocall esa versión. Si es migrar código desde una versión anterior del lote, tenga en cuenta que hello **runElevated** propiedad ya no se admite en bibliotecas de cliente de API de REST o proceso por lotes de Hola. Hola de uso nueva **userIdentity** propiedad de un nivel de elevación de toospecify de tarea. Consulte la sección de hello [actualizar la biblioteca de cliente de lote más reciente de código toohello](#update-your-code-to-the-latest-batch-client-library) para rápido instrucciones detalladas para actualizar el código de proceso por lotes si usa una de las bibliotecas de cliente de Hola.
>
>

> [!NOTE] 
> las cuentas de usuario de Hello descritas en este artículo no son compatibles con el protocolo de escritorio remoto (RDP) o Shell seguro (SSH), por motivos de seguridad. 
>
> tooconnect tooa nodo ejecución Hola Linux configuración de máquina virtual a través de SSH, consulte [tooa de uso de escritorio remoto VM de Linux en Azure](../virtual-machines/virtual-machines-linux-use-remote-desktop.md). toonodes tooconnect ejecutan Windows a través de RDP, consulte [conectar tooa VM de Windows Server](../virtual-machines/windows/connect-logon.md).<br /><br />
> tooconnect tooa nodo ejecución Hola nube configuración del servicio a través de RDP, consulte [Habilitar conexión a Escritorio remoto para un rol de servicios de nube de Azure](../cloud-services/cloud-services-role-enable-remote-desktop-new-portal.md).
>
>

## <a name="user-account-access-toofiles-and-directories"></a>Directorios y toofiles de acceso de cuenta de usuario

Una cuenta de usuario automática y una cuenta de usuario con nombre tienen el directorio de trabajo de la tarea del toohello del acceso de lectura/escritura, el directorio compartido y el directorio de tareas de varias instancias. Ambos tipos de cuentas tienen acceso de lectura directorios de toohello inicio y trabajo de preparación.

Si una tarea se ejecuta bajo Hola misma cuenta que se usó para ejecutar una tarea de inicio, la tarea hello tiene directorio de tareas de inicio de toohello de acceso de lectura y escritura. De forma similar, si una tarea se ejecuta bajo Hola misma cuenta que se usó para ejecutar una tarea de preparación del trabajo, la tarea hello tiene el directorio de trabajo de acceso de lectura y escritura toohello tareas preparación. Si una tarea se ejecuta bajo una cuenta diferente de la tarea de inicio de Hola o tarea de preparación de trabajos, tarea hello tiene solo las directorio correspondiente de las toohello acceso de lectura.

Para más información sobre cómo acceder a archivos y directorios desde una tarea, consulte [Desarrollo de soluciones de procesos paralelos a gran escala con Batch](batch-api-basics.md#files-and-directories).

## <a name="elevated-access-for-tasks"></a>Acceso con privilegios elevados para tareas 

nivel de elevación de la cuenta de usuario de Hello indica si una tarea se ejecuta con acceso con privilegios elevados. Tanto las cuentas de usuario automático como las de usuario con nombre se pueden ejecutar con acceso con privilegios elevados. Hola dos opciones para el nivel de elevación son:

- **NonAdmin:** tarea hello se ejecuta como un usuario estándar sin acceso con privilegios elevados. nivel de elevación de Hello predeterminado para una cuenta de usuario de lote es siempre **NonAdmin**.
- **Administrador:** tarea hello se ejecuta como un usuario con acceso con privilegios elevados y funciona con permisos de administrador completos. 

## <a name="auto-user-accounts"></a>Cuentas de usuario automático

De forma predeterminada, las tareas se ejecutan en Batch en una cuenta de usuario automático, como usuario estándar sin acceso con privilegios elevados y con el ámbito de la tarea. Cuando se configura la especificación de usuario automática de Hola para el ámbito de la tarea, servicio por lotes de hello crea una cuenta de usuario automática para dicha tarea solo.

ámbito de Hello tootask alternativo es el ámbito de grupo. Cuando se configura Hola auto-especificación para una tarea para el ámbito de grupo, Hola tarea se ejecuta bajo una cuenta de usuario automático es tarea tooany disponible en el grupo de Hola. Para obtener más información acerca del ámbito de grupo, consulte sección hello [ejecutar una tarea como Hola auto-usuarios cuyo ámbito de grupo](#run-a-task-as-the-autouser-with-pool-scope).   

ámbito predeterminado de Hello es diferente en los nodos de Windows y Linux:

- En los nodos de Windows, las tareas se ejecutan en el ámbito de la tarea de forma predeterminada.
- En los nodos de Linux, se ejecutan siempre en el ámbito de grupo.

Hay cuatro configuraciones posibles para la especificación de usuario automática de hello, cada uno de los cuales corresponde tooa única auto-cuenta de usuario:

- Acceso sin privilegios de administrador con ámbito de la tarea (especificación de usuario automática de hello predeterminado)
- Acceso de administrador (elevado) con ámbito de la tarea
- Acceso sin privilegios de administrador con ámbito de grupo
- Acceso de administrador con ámbito de grupo

> [!IMPORTANT] 
> Tareas que se ejecutan en el ámbito de la tarea no tiene de hecho acceso tooother tareas en un nodo. Sin embargo, un usuario malintencionado con la cuenta de acceso de toohello puede evitar esta limitación mediante el envío de una tarea que se ejecuta con privilegios de administrador y tiene acceso a otros directorios de la tarea. Un usuario malintencionado también podría utilizar el nodo de tooa tooconnect RDP o SSH. Es importante tooprotect acceso tooyour lote cuenta claves tooprevent este escenario. Si sospecha que se han comprometido su cuenta, ser tooregenerate seguro de las claves.
>
>

### <a name="run-a-task-as-an-auto-user-with-elevated-access"></a>Ejecución de una tarea como usuario automático con acceso con privilegios elevados

Puede configurar Hola auto-especificación de privilegios de administrador cuando necesite toorun una tarea con acceso con privilegios elevados. Por ejemplo, una tarea de inicio puede necesitar software para tooinstall el acceso con privilegios elevados en el nodo de Hola.

> [!NOTE] 
> En general, es mejor toouse elevados acceso solo cuando sea necesario. Es recomendable conceder Hola privilegios mínimos necesarios tooachieve Hola el resultado deseado. Por ejemplo, si una tarea de inicio instala el software para el usuario actual de hello, en lugar de para todos los usuarios, es posible que pueda tooavoid conceder acceso con privilegios elevados tootasks. Puede configurar la especificación de usuario automática de hello para el acceso de ámbito y sin derechos administrativos de grupo para todas las tareas que necesitan toorun bajo la misma cuenta, incluida la tarea de inicio de hello de Hola. 
>
>

Hola siguientes fragmentos de código muestra cómo tooconfigure Hola especificación de usuario automáticamente. ejemplos de Hello establecen nivel de elevación de hello demasiado`Admin` y Hola ámbito demasiado`Task`. Ámbito de la tarea es la configuración predeterminada de hello, pero se incluye aquí para simplificar Hola de ejemplo.

#### <a name="batch-net"></a>.NET de Batch

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin, scope: AutoUserScope.Task));
```
#### <a name="batch-java"></a>Java de Batch

```java
taskToAdd.withId(taskId)
        .withUserIdentity(new UserIdentity()
            .withAutoUser(new AutoUserSpecification()
                .withElevationLevel(ElevationLevel.ADMIN))
                .withScope(AutoUserScope.TASK));
        .withCommandLine("cmd /c echo hello");                        
```

#### <a name="batch-python"></a>Python de Batch

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

### <a name="run-a-task-as-an-auto-user-with-pool-scope"></a>Ejecución de una tarea como usuario automático con ámbito de grupo

Cuando se aprovisiona un nodo, se crean las cuentas de usuario de automática de todo el grupo de dos en cada nodo de grupo de hello, uno con acceso con privilegios elevados y otro sin acceso con privilegios elevados. Establecer ámbito de toopool de ámbito de hello automática del usuario para una tarea determinada, ejecuta la tarea de hello en alguna de estas cuentas de usuario de automática de todo el grupo de dos. 

Cuando se especifica el ámbito de grupo de hello auto-usuario, todas las tareas que se ejecutan con acceso de administrador se ejecutan en hello misma cuenta de usuario automática de todo el grupo. De forma similar, las tareas que se ejecutan sin permisos de administrador también se ejecutan en una sola cuenta de usuario automático para todo el grupo. 

> [!NOTE] 
> Hola auto-usuario de todo el grupo de dos cuentas es independientes. Tareas que se ejecutan bajo la cuenta administrativa de todo el grupo de hello no pueden compartir datos con tareas que se ejecutan bajo la cuenta estándar de Hola y viceversa. 
>
>

Hola toorunning ventaja en la misma cuenta de usuario automática es que las tareas son tooshare capaz de datos con otras tareas que se ejecutan en Hola de hello mismo nodo.

Uso compartido de información confidencial entre las tareas es un escenario donde la ejecución de tareas en una de las cuentas de usuario automática de todo el grupo de hello dos es útil. Por ejemplo, suponga que una tarea de inicio debe tooprovision un secreto en el nodo de Hola que pueden usar otras tareas. Podría utilizar la API de protección de datos (DPAPI) de Windows hello, pero requiere privilegios de administrador. En su lugar, puede proteger el secreto de hello en nivel de usuario de Hola. Tareas que se ejecutan bajo puede tener acceso la misma cuenta de usuario de Hola Hola secreto sin acceso con privilegios elevados.

Otro escenario que es conveniente toorun tareas correspondientes a una cuenta de usuario automática con ámbito de grupo es un archivo de interfaz de paso de mensajes (MPI) comparten. Un recurso compartido de archivos MPI es útil cuando los nodos Hola Hola MPI tarea necesidad toowork en Hola mismos datos de archivo. nodo principal Hello crea un recurso compartido de archivos que pueden tener acceso los nodos secundarios Hola si se están ejecutando en hello misma cuenta de usuario automáticamente. 

Hola siguiente fragmento de código establece el ámbito de toopool de ámbito de hello automática del usuario para una tarea en .NET de lote. se omite el nivel de elevación de Hello, por lo que la tarea hello se ejecuta bajo la cuenta de usuario de automática de todo el grupo de estándar de Hola.

```csharp
task.UserIdentity = new UserIdentity(new AutoUserSpecification(scope: AutoUserScope.Pool));
```

## <a name="named-user-accounts"></a>Cuentas de usuario con nombre

Puede definir cuentas de usuario con nombre cuando cree un grupo. Una cuenta de usuario con nombre tiene el nombre y la contraseña que proporcione. Puede especificar el nivel de elevación de Hola para una cuenta de usuario con nombre. Para los nodos de Linux, también puede proporcionar una clave privada SSH.

Existe una cuenta de usuario con nombre en todos los nodos de grupo de Hola y tooall disponibles tareas se está ejecutando en esos nodos. Puede definir cualquier número de usuarios con nombre para un grupo. Cuando se agrega una tarea o una colección de tareas, puede especificar que esa tarea Hola se ejecuta bajo una de hello con el nombre de las cuentas de usuario definidas en el grupo de Hola.

Una cuenta de usuario con nombre es útil cuando se desea toorun todas las tareas de un trabajo en Hola la misma cuenta de usuario, pero aislarlas entre tareas que se ejecutan en otros trabajos en hello mismo tiempo. Por ejemplo, puede crear un usuario con nombre para cada trabajo y ejecutar las tareas de cada trabajo en dicha cuenta de usuario con nombre. Entonces, cada trabajo puede compartir un secreto con sus propias tareas, pero no con las que se ejecutan en otros trabajos.

También puede utilizar un toorun de cuenta de usuario designado una tarea que establece permisos en recursos externos, como recursos compartidos de archivos. Con una cuenta de usuario con nombre es controlan la identidad de usuario de Hola y puede usar los permisos de tooset de identidad de ese usuario.  

Las cuentas de usuario con nombre permiten SSH sin contraseña entre nodos de Linux. Puede usar una cuenta de usuario con nombre a los nodos de Linux que necesitan las tareas de varias instancias de toorun. Cada nodo de grupo de hello puede ejecutar tareas en una cuenta de usuario definida en grupo todo Hola. Para obtener más información acerca de las tareas de varias instancias, consulte [usar múltiples\-instancia las tareas de las aplicaciones de MPI toorun](batch-mpi.md).

### <a name="create-named-user-accounts"></a>Creación de cuentas de usuario con nombre

toocreate con el nombre de las cuentas de usuario en proceso por lotes, agregue una colección de grupo de toohello de cuentas de usuario. Hello fragmentos de código siguientes muestran cómo toocreate denominado cuentas de usuario de. NET, Java y Python. Estos código fragmentos de código muestran cómo toocreate admin y sin derechos administrativos con el nombre de las cuentas en un grupo. ejemplos de Hello crean grupos con la configuración del servicio de nube de hello, pero usar Hola mismo enfoque al crear un grupo de Windows o Linux mediante la configuración de máquina virtual de Hola.

#### <a name="batch-net-example-windows"></a>Ejemplo de .NET de Batch (Windows)

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

#### <a name="batch-net-example-linux"></a>Ejemplo de .NET de Batch (Linux)

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


#### <a name="batch-java-example"></a>Ejemplo de Java de Batch

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

#### <a name="batch-python-example"></a>Ejemplo de Python de Batch

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

### <a name="run-a-task-under-a-named-user-account-with-elevated-access"></a>Ejecución de una tarea en una cuenta de usuario con nombre con acceso con privilegios elevados

toorun una tarea como de un usuario elevado, conjunto de tareas de hello **UserIdentity** tooa de propiedad con el nombre de cuenta de usuario que se creó con su **ElevationLevel** propiedad establecida demasiado`Admin`.

Este fragmento de código especifica que la tarea hello debe ejecutarse bajo una cuenta de usuario con nombre. Esta cuenta de usuario con nombre se definió en el grupo de hello cuando se creó el grupo de Hola. En este caso, se creó Hola con el nombre de cuenta de usuario con permisos de administrador:

```csharp
CloudTask task = new CloudTask("1", "cmd.exe /c echo 1");
task.UserIdentity = new UserIdentity(AdminUserAccountName);
```

## <a name="update-your-code-toohello-latest-batch-client-library"></a>Actualizar la biblioteca de cliente de lote más reciente de código toohello

versión del servicio de lote de Hello 2017-01-01.4.0 presenta un cambio importante, reemplazando hello **runElevated** propiedad disponible en versiones anteriores con hello **userIdentity** propiedad. Hola las tablas siguientes proporciona una simple asignación que puede usar tooupdate su código desde versiones anteriores de las bibliotecas de cliente de Hola.

### <a name="batch-net"></a>.NET de Batch

| Si el código usa…                  | Actualícelo a…                                                                                                 |
|---------------------------------------|------------------------------------------------------------------------------------------------------------------|
| `CloudTask.RunElevated = true;`       | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.Admin));`    |
| `CloudTask.RunElevated = false;`      | `CloudTask.UserIdentity = new UserIdentity(new AutoUserSpecification(elevationLevel: ElevationLevel.NonAdmin));` |
| `CloudTask.RunElevated` sin especificar | No se requiere actualización                                                                                               |

### <a name="batch-java"></a>Java de Batch

| Si el código usa…                      | Actualícelo a…                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `CloudTask.withRunElevated(true);`        | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.ADMIN));`    |
| `CloudTask.withRunElevated(false);`       | `CloudTask.withUserIdentity(new UserIdentity().withAutoUser(new AutoUserSpecification().withElevationLevel(ElevationLevel.NONADMIN));` |
| `CloudTask.withRunElevated` sin especificar | No se requiere actualización                                                                                                                     |

### <a name="batch-python"></a>Python de Batch

| Si el código usa…                      | Actualícelo a…                                                                                                                       |
|-------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------|
| `run_elevated=True`                       | `user_identity=user`, donde <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.admin)) `                |
| `run_elevated=False`                      | `user_identity=user`, donde <br />`user = batchmodels.UserIdentity(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`auto_user=batchmodels.AutoUserSpecification(`<br />&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`elevation_level=batchmodels.ElevationLevel.nonadmin)) `             |
| `run_elevated` sin especificar | No se requiere actualización                                                                                                                                  |


## <a name="next-steps"></a>Pasos siguientes

### <a name="batch-forum"></a>Foro de Batch

Hola [foro de lote de Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch) en MSDN es una gran colocar toodiscuss por lotes y formular preguntas acerca del servicio de Hola. Lea los útiles mensajes anclados y envíe sus preguntas a medida que surjan mientras compila sus soluciones del servicio Batch.
