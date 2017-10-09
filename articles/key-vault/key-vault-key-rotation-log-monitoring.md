---
title: "aaaSet el almacén de claves de Azure con la rotación de clave-to-end y auditoría | Documentos de Microsoft"
description: "Utilice este tootoohelp de cómo que obtener configurar con la rotación de claves y supervisión de los registros de almacén de claves."
services: key-vault
documentationcenter: 
author: swgriffith
manager: mbaldwin
tags: 
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: e0c393873077e3b91adc9fa7f39128bc1b6abe26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a>Configuración de Azure Key Vault con la auditoría y la rotación de claves de un extremo a otro
## <a name="introduction"></a>Introducción
Después de crear el almacén de claves, será capaz de toostart con ese almacén toostore sus claves y secretos. Las aplicaciones ya no necesitan toopersist los secretos o claves, pero en su lugar solicitan desde el almacén de claves de hello según sea necesario. Esto le permite tooupdate claves y secretos sin afectar al comportamiento de saludo de la aplicación, lo que abre una amplia gama de posibilidades alrededor de la clave y la administración de secretos.

Este artículo le guía a través de un ejemplo del uso de almacén de claves de Azure toostore un secreto, en este caso, una clave de cuenta de almacenamiento de Azure que se tiene acceso a una aplicación. El artículo también incluye una demostración de la implementación de una rotación programada de dicha clave. Por último, le guía a través de una demostración de cómo toomonitor Hola registros de auditoría de almacén de claves y generar alertas cuando se realizan las solicitudes inesperadas.

> [!NOTE]
> Este tutorial no está previsto tooexplain en detalle Hola inicial el programa de instalación de su almacén de claves. Para obtener información, consulte [Introducción al Almacén de claves de Azure](key-vault-get-started.md). Para obtener instrucciones acerca de la interfaz de la línea de comandos para todas las plataformas, consulte [Administración del almacén de claves mediante CLI](key-vault-manage-with-cli2.md).
>
>

## <a name="set-up-key-vault"></a>Configuración del Almacén de claves
tooenable un tooretrieve un secreto de aplicación desde el almacén de claves, primero debe crear Hola secreto y cargarlo en el almacén de tooyour. Esto puede realizarse a partir de una sesión de PowerShell de Azure y firma en tooyour cuenta de Azure con hello siguiente comando:

```powershell
Login-AzureRmAccount
```

En la ventana emergente del explorador de hello, escriba el nombre de usuario de cuenta de Azure y la contraseña. PowerShell obtendrá todas las suscripciones de Hola que están asociadas a esta cuenta. PowerShell utiliza Hola primera de ellas de forma predeterminada.

Si tiene varias suscripciones, podría tener que toospecify Hola uno que estaba toocreate usa el almacén de claves. Escriba Hola siguiendo las suscripciones de hello toosee para su cuenta:

```powershell
Get-AzureRmSubscription
```

suscripción de hello toospecify que esté asociada con el almacén de claves de hello iniciará la sesión, escriba:

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

Dado que en este artículo se explica cómo se guarda una clave de cuenta de almacenamiento como un secreto, debe obtener dicha clave.

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

Después de recuperar el secreto (en este caso, la clave de cuenta de almacenamiento), debe convertir esa cadena segura tooa y, a continuación, crear un secreto con ese valor en el almacén de claves.

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
A continuación, obtener Hola URI secreto Hola que creó. Cuando se llama a tooretrieve de almacén de claves de Hola la clave secreta se utiliza en un paso posterior. Ejecute el siguiente comando de PowerShell de Hola y tome nota del valor de identificador hello, que es el secreto de hello URI:

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a>Configurar la aplicación hello
Ahora que tiene un secreto almacenado, puede usar código tooretrieve y usarlo. Hay unos pocos pasos a necesario tooachieve esto. Hello paso primero y el más importante es registrando su aplicación con Azure Active Directory y, a continuación, que el almacén de claves se indica en la información de la aplicación para que pueden permitir que las solicitudes de la aplicación.

> [!NOTE]
> La aplicación debe crearse en hello mismo inquilino de Azure Active Directory como su almacén de claves.
>
>

Abra la ficha de hello aplicaciones de Azure Active Directory.

![Abra las aplicaciones de Azure Active Directory](./media/keyvault-keyrotation/AzureAD_Header.png)

Elija **agregar** tooadd una tooyour de aplicación Azure Active Directory.

![Elija AGREGAR](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

Deje el tipo de aplicación Hola como **aplicación WEB Y/O API de WEB** y asigne un nombre a la aplicación.

![Aplicación hello nombre](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

Especifique un valor en **URL DE INICIO DE SESIÓN** y en **URI DE ID DE APLICACIÓN**. En esta demostración, puede especificar los valores que desee y cambiarlos más adelante si es necesario.

![Especifique los identificadores URI necesarios](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

Después de agrega tooAzure Active Directory de la aplicación hello, aparecerá en la página de aplicación Hola. Haga clic en hello **configurar** ficha y, a continuación, busque y copie hello **Id. de cliente** valor. Tome nota del identificador de cliente de hello en pasos posteriores.

A continuación, genere una clave para su aplicación para que pueda interactuar con Azure Active Directory. Puede crear en hello **claves** sección Hola **configuración** ficha. Tome nota de la clave de hello recién generado desde su aplicación de Azure Active Directory para su uso en un paso posterior.

![Claves de aplicaciones de Azure Active Directory](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

Antes de establecer las llamadas desde la aplicación en el almacén de claves de hello, debe indicar el almacén de claves de hello acerca de la aplicación y sus permisos. Hello comando siguiente toma el nombre del almacén de Hola y Hola Id. de cliente de la aplicación de Azure Active Directory y concede **obtener** almacén de claves de tooyour de acceso para la aplicación hello.

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

En este punto, está listo toostart compilar su aplicación llama. En su aplicación, debe instalar paquetes de NuGet hello toointeract necesario con el almacén de claves de Azure y Azure Active Directory. Desde la consola de administrador de paquetes de Visual Studio de hello, escriba Hola siga los comandos. En la escritura de Hola de este artículo, versión actual de hello del paquete de Azure Active Directory hello es 3.10.305231913, por lo que podría desea la versión más reciente de tooconfirm hello y actualizar en consecuencia.

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

En el código de aplicación, cree un método de clase toohold hello para la autenticación de Azure Active Directory. En este ejemplo, la clase se llama **Utils**. Agregue Hola siguiente instrucción using:

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

A continuación, agregue Hola siguiendo el token de JWT de método tooretrieve Hola de Azure Active Directory. Para el mantenimiento, puede que desee valores de cadena codificados de forma rígida de hello toomove en su configuración de aplicación o web.

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

Agregar Hola código necesario toocall el almacén de claves y recuperar su valor secreto. En primer lugar debe agregar la siguiente Hola instrucción using:

```csharp
using Microsoft.Azure.KeyVault;
```

Agregar tooinvoke de llamadas de método hello el almacén de claves y recuperar la clave secreta. En este método, se proporcione el secreto de hello URI que guardó en el paso anterior. Tenga en cuenta use Hola de hello **GetToken** método de hello **Utils** clase creada previamente.

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

Al ejecutar la aplicación, ahora se deben autenticar tooAzure Active Directory y, a continuación, recuperar el valor secreto desde el almacén de claves de Azure.

## <a name="key-rotation-using-azure-automation"></a>Rotación de claves mediante Azure Automation
Existen varias opciones para implementar una estrategia de rotación de los valores que se guardan como secretos del Almacén de claves de Azure. Los secretos pueden rotarse mediante un proceso manual, mediante programación a través de llamadas a API o mediante un script de automatización. Para fines de Hola de este artículo, estará usando Azure PowerShell combinado con automatización de Azure toochange una tecla de acceso de la cuenta de almacenamiento de Azure. A continuación, podrá actualizar un secreto del almacén de claves con esa nueva clave.

tooallow automatización de Azure tooset secretos valores en el almacén de claves, debe obtener Id. de cliente de Hola para conexión de hello denominada AzureRunAsConnection, que se creó cuando se establece la instancia de automatización de Azure. Para encontrar este identificador, seleccione **Recursos** en la instancia de Azure Automation. Desde allí, elija **conexiones** y, a continuación, seleccione hello **AzureRunAsConnection** principal de servicio. Tome nota de hello **identificador de la aplicación**.

![Identificador de cliente de Azure Automation](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

En **Recursos**, elija **Módulos**. De **módulos**, seleccione **galería**y, a continuación, busque y **importación** versiones actualizadas de cada uno de hello siguientes módulos:

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> En la escritura de Hola de este artículo, solo hello toobe módulos se indicó anteriormente que necesita se actualiza para hello siguiente secuencia de comandos. Si se produce algún error en el trabajo de automatización, confirme que ha importado todos los módulos necesarios y sus dependencias.
>
>

Después de recuperar los Id. de aplicación de hello para la conexión de automatización de Azure, debe indicar que el almacén de claves que esta aplicación tiene acceso tooupdate secretos en el almacén. Esto puede realizarse con hello siguiente comando de PowerShell:

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

A continuación, seleccione **Runbooks** en la instancia de Azure Automation y, después, seleccione **Agregar un runbook**. Seleccione **Creación rápida**. Nombre del runbook y seleccione **PowerShell** como tipo de runbook de Hola. Tener Hola opción tooadd una descripción. Por último, haga clic en **Crear**.

![Creación de runbook](./media/keyvault-keyrotation/Create_Runbook.png)

Pegue el siguiente script de PowerShell en el panel del editor de hello para el nuevo runbook de hello:

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get hello connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in tooAzure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set hello following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for hello storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

En el panel del editor de hello, elija **panel prueba** tootest la secuencia de comandos. Una vez que se ejecuta el script de Hola sin errores, puede seleccionar **publicar**, y, a continuación, puede aplicar una programación de runbook de hello en el panel de configuración de runbook de Hola.

## <a name="key-vault-auditing-pipeline"></a>Canalización de auditorías de Key Vault
Al configurar un almacén de claves, puede activar la auditoría de registros toocollect en las solicitudes de acceso realizadas toohello el almacén de claves. Estos registros se guardan en una cuenta de Azure Storage designada y pueden extraerse, supervisarse y analizarse. Hello siguiente escenario utiliza las funciones de Azure, las aplicaciones de Azure lógica y toocreate de registros de auditoría de almacén de claves un toosend canalización un correo electrónico cuando una aplicación que coinciden con el identificador de la aplicación hello de aplicación web de hello recupera los secretos del almacén de Hola.

En primer lugar, debe habilitar los registros en el almacén de claves. Esto puede hacerse a través de hello siga los comandos de PowerShell (se pueden ver detalles completos en [clave de registro de almacén](key-vault-logging.md)):

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

Después de que esta opción está habilitada, los registros de auditoría comenzar a recopilar en hello designado de la cuenta de almacenamiento. Estos registros incluirán eventos acerca de qué usuario, cómo y cuándo ha obtenido acceso a los almacenes de claves.

> [!NOTE]
> Puede tener acceso a la información de registro de 10 minutos tras la operación de almacén de claves de Hola. Normalmente, tardará menos.
>
>

paso siguiente Hello es demasiado[crear una cola de Service Bus de Azure](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md). En ella se insertan los registros de auditoría del almacén de claves. Una vez mensajes de registro de auditoría de hello en cola hello, aplicación de lógica de hello ellos recoge y actúa sobre ellos. Cree un bus de servicio con hello pasos:

1. Crear un espacio de nombres de Bus de servicio (si ya tiene una que desee toouse para ello, omitir tooStep 2).
2. Examinar bus de servicio toohello Hola portal de Azure y espacio de nombres de hello seleccione en que desea toocreate cola de hello.
3. Seleccione **New** y elija **Bus de servicio > cola** y escriba los detalles de hello necesario.
4. Seleccione la información de conexión de Bus de servicio de hello eligiendo el espacio de nombres de Hola y haga clic en **información de conexión**. Necesitará esta información para la sección siguiente Hola.

Después, [crea una función Azure](../azure-functions/functions-create-first-azure-function.md) toopoll registros de almacén de claves en Hola cuenta de almacenamiento y recogida de los nuevos eventos. Esta función se desencadenará en función de una programación.

toocreate una función de Azure, elija **nuevo > aplicación de la función** Hola portal de Azure. Durante el proceso de creación, puede usar un plan de hospedaje existente o crear uno nuevo. También puede utilizar un plan de hospedaje dinámico. Se pueden encontrar más detalles en función de opciones de hospedaje en [cómo tooscale funciones de Azure](../azure-functions/functions-scale.md).

Cuando se crea la función Azure hello, navegar tooit y elegir un temporizador de función y C\#. A continuación, haga clic en **Crear esta función**.

![Hoja de inicio de Azure Functions](./media/keyvault-keyrotation/Azure_Functions_Start.png)

En hello **desarrollar** ficha, reemplace el código de hello run.csx por siguiente hello:

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting toonow.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required tooorder by time as they may not be in hello file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending tooServiceBus, use hello payloadStream and set keeporiginal tootrue
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> Asegúrese de variables de hello tooreplace seguro en hello anterior cuenta de almacenamiento de código toopoint tooyour donde se escriben los registros de almacén de claves de hello, bus de servicio de Hola que creó anteriormente, y Hola registros de almacenamiento de almacén de claves de toohello de ruta de acceso específica.
>
>

función Hello recoge Hola último archivo de registro de cuenta de almacenamiento de Hola donde se escriben los registros de almacén de claves de hello, grabs Hola los eventos más recientes de ese archivo, y los envía tooa cola de Bus de servicio. Dado que un único archivo puede tener varios eventos, debe crear un archivo de sync.txt que función hello también busca en marca de tiempo de hello toodetermine de evento último Hola que ha recogido. Esto garantiza que no insertará Hola mismo evento varias veces. Este archivo sync.txt contiene una marca de tiempo para el último suceso de encontró Hola. registros, cuando carga, Hello tienen toobe ordenado según hello tooensure de marca de tiempo que están ordenados correctamente.

Para esta función, se hacen referencia a un par de bibliotecas adicionales que no están disponibles fuera del cuadro de hello en funciones de Azure. tooinclude estos, necesitamos toopull de funciones de Azure mediante NuGet. Elija hello **ver archivos** opción.

![Opción Ver archivos](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

Y agregue un archivo denominado project.json con el contenido siguiente:

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
Tras **guardar**, funciones de Azure descargará los archivos binarios de hello necesario.

Cambiar toohello **integrar** pestaña y asigne un toouse nombre descriptivo en función de Hola de parámetro de temporizador de Hola. En el anterior código de hello, espera Hola temporizador toobe llama *myTimer*. Especifique un [expresión CRON](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) como sigue: 0 \* \* \* \* \* temporizador Hola que causará Hola función toorun una vez por minuto.

Hola en mismo **integrar** ficha, agregue una entrada de tipo hello **almacenamiento de blobs de Azure**. Esto señala toohello sync.txt archivo que contiene la marca de tiempo de hello del último evento de hello examinado por función hello. Esta opción estará disponible en función de Hola por nombre de parámetro de Hola. En el anterior código de hello, proporcionados por el almacenamiento de blobs de Azure Hola espera toobe de nombre de parámetro de Hola *inputBlob*. Elegir cuenta de almacenamiento de Hola dónde se ubicará el archivo de hello sync.txt (podría ser Hola misma o a una cuenta de almacenamiento diferente). En el campo de ruta de acceso de hello, proporcione la ruta de acceso de Hola donde reside el archivo hello en formato de Hola {container-name}/path/to/sync.txt.

Agregar una salida de tipo hello *almacenamiento de blobs de Azure* salida. Esto señala toohello sync.txt archivo definido en la entrada de Hola. Se utiliza por hello función toowrite Hola marca de tiempo del último evento de hello examinado. código anterior Hello espera este toobe parámetro denominado *outputBlob*.

En este momento, la función hello está listo. Realizar tooswitch seguro atrás toohello **desarrollar** pestaña y guarde el código de hello. Consulte la ventana de salida de hello para los errores de compilación y corríjalos según corresponda. Si se compila el código de hello, código de hello debe ahora puede comprobar los registros de almacén de claves de hello cada minuto y e inserta los nuevos eventos en hello define la cola de Service Bus. Debería ver la información del registro escribir toohello la ventana de registro cada vez que se desencadene la función hello.

### <a name="azure-logic-app"></a>Aplicación lógica de Azure
A continuación debe crear una aplicación de Azure lógica que recoge los eventos de Hola que función hello insertando toohello cola de Bus de servicio, analiza el contenido de Hola y envía un correo electrónico basado en una condición que se buscan coincidencias.

[Crear una aplicación de lógica](../logic-apps/logic-apps-create-a-logic-app.md) yendo demasiado**nuevo > aplicación lógica**.

Una vez que se crea la aplicación de la lógica de hello, navegar tooit y elegir **editar**. Editor de aplicación lógica de hello, elija **cola de Service Bus** y escriba su tooconnect de credenciales de Bus de servicio se toohello cola.

![Bus de servicio de la aplicación lógica de Azure](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

A continuación, elija **Agregar una condición**. En la condición de hello, cambie toohello advanced editor y escriba Hola siguiente código, reemplazando id_aplicación con hello id_aplicación real de la aplicación web:

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

Esta expresión devuelve básicamente **false** si hello *appid* de hello evento de entrada (que es el cuerpo de Hola de mensajes de bienvenida del Bus de servicio) no es Hola *appid* de hello aplicación.

Ahora, cree una acción en la opción **If no, do nothing** (Si no, no hacer nada).

![Elegir una acción en la aplicación lógica de Azure](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

Para la acción de hello, elija **Office 365: enviar correo electrónico**. Rellene Hola campos toocreate un toosend de correo electrónico cuando Hola define la condición devuelve **false**. Si no tiene Office 365, puede mirar alternativas tooachieve Hola los mismos resultados.

En este punto, tiene una canalización de tooend final que comprueba si hay nuevos registros de auditoría de almacén de claves una vez por minuto. Inserta nuevos registros encuentra tooa cola de bus de servicio. aplicación de la lógica de Hola se desencadena cuando se llega a un nuevo mensaje de cola de Hola. Si hello *appid* dentro de hello eventos no coincide con Id. de aplicación Hola de hello llamar a la aplicación, envía un correo electrónico.
