---
title: "aaaUse automático de toodo de la captura de paquetes de red con funciones de Azure y las alertas de supervisión | Documentos de Microsoft"
description: "Este artículo describe cómo toocreate una alerta activa captura de paquetes con Monitor de red de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a>Uso de capturas de paquetes para realizar la supervisión proactiva de la red con alertas y Azure Functions

Captura de paquetes de Monitor de red crea sesiones de captura tráfico tootrack dentro y fuera de las máquinas virtuales. Hello archivo de captura puede tener un filtro que se define tootrack Hola solo el tráfico que desea toomonitor. Estos datos, a continuación, se almacenan en un blob de almacenamiento o localmente en la máquina de invitado de Hola.

Esta funcionalidad se puede iniciar de forma remota desde otros escenarios de automatización, como Azure Functions. Proporciona de captura de paquetes que Hola capturas automático toorun de capacidad, según define anomalías de la red. Otros usos son la recopilación de estadísticas de red, la obtención de información sobre las intrusiones de red y la depuración de las comunicaciones cliente-servidor, entre otros.

Los recursos implementados en Azure se ejecutan las 24 horas, los 7 días de la semana. Usted y su personal no se puede supervisar activamente estado Hola de todos los recursos 24/7. ¿Qué ocurre si un problema se produce a las 2 a. m.?

Al usar Monitor de red, las alertas y funciones desde dentro de hello ecosistema de Azure, puede responder proactivamente con problemas de toosolve de datos y las herramientas de hello en la red.

![Escenario][scenario]

## <a name="prerequisites"></a>Requisitos previos

* versión más reciente de Hola de [Azure PowerShell](/powershell/azure/install-azurerm-ps).
* Una instancia existente de Network Watcher. [Cree una instancia de Network Watcher](network-watcher-create.md) si aún no tiene una.
* Una máquina virtual existente en hello misma región que el Monitor de red con hello [extensión Windows](../virtual-machines/windows/extensions-nwa.md) o [extensión de máquina virtual Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="scenario"></a>Escenario

En este ejemplo, la máquina virtual está enviando los segmentos TCP más de lo habitual y desea toobe una alerta. Los segmentos TCP se usan aquí como ejemplo, pero podría usar cualquier condición de alerta.

Cuando se le indique, desea toounderstand de datos de nivel de paquete tooreceive ¿por qué ha aumentado la comunicación. A continuación, puede tomar medidas comunicación tooregular de tooreturn Hola máquina virtual.

En este escenario se supone que tiene una instancia existente de Network Watcher y un grupo de recursos con una máquina virtual válida.

Hola lista siguiente es una visión general de flujo de trabajo de Hola que tiene lugar:

1. Se desencadena una alerta en la máquina virtual.
1. alerta de Hello llama a la función de Azure a través de un webhook.
1. La función de Azure procesa la alerta de Hola e inicia una sesión de captura de paquetes de Monitor de red.
1. captura de paquetes de saludo se ejecuta en hello VM y recopila tráfico.
1. Hello archivo de captura de paquete se carga tooa cuenta de almacenamiento para su revisión y un diagnóstico más detallado.

tooautomate este proceso, que creamos y conectar una alerta en nuestro tootrigger de máquina virtual cuando se produce el incidente de Hola. También creamos un toocall de función en el Monitor de red.

Este escenario Hola siguientes:

* Creará una función de Azure que inicie una captura de paquetes.
* Crea una regla de alerta en una máquina virtual y configura hello toocall de regla de alerta hello Azure función.

## <a name="create-an-azure-function"></a>Creación de una función de Azure

primer paso de Hello es toocreate una alerta de hello tooprocess función Azure y crear una captura de paquetes.

1. Hola [portal de Azure](https://portal.azure.com), seleccione **New** > **proceso** > **aplicación de la función**.

    ![Creación de una aplicación de función][1-1]

2. En hello **aplicación de la función** hoja, escriba Hola después de valores y, a continuación, seleccione **Aceptar** toocreate Hola aplicación:

    |**Configuración** | **Valor** | **Detalles** |
    |---|---|---|
    |**Nombre de la aplicación**|PacketCaptureExample|nombre de Hola de aplicación de la función de hello.|
    |**Suscripción**|[La suscripción] Hola suscripción para qué aplicación de función de hello toocreate.||
    |**Grupo de recursos**|PacketCaptureRG|Hola recursos grupo toocontain Hola función aplicación.|
    |**Plan de hospedaje**|Plan de consumo| tipo de Hola de plan usa su aplicación de función. Las opciones son Consumo o plan de Azure App Service. |
    |**Ubicación**|Central EE. UU.:| región de Hola de qué aplicación de función de hello toocreate.|
    |**Storage Account**|{autogenerated}| cuenta de almacenamiento de Hola que necesita las funciones de Azure para almacenamiento general.|

3. En hello **PacketCaptureExample función aplicaciones** hoja, seleccione **funciones** > **función personalizada**  >  **+**.

4. Seleccione **HttpTrigger Powershell**y, a continuación, escriba Hola restante información. Por último, toocreate función hello, seleccione **crear**.

    |**Configuración** | **Valor** | **Detalles** |
    |---|---|---|
    |**Escenario**|Experimental|Tipo de escenario|
    |**Asigne un nombre a la función**|AlertPacketCapturePowerShell|Nombre de función hello|
    |**Nivel de autorización**|Función|Nivel de autorización para la función hello|

![Ejemplo de funciones][functions1]

> [!NOTE]
> plantilla de PowerShell de Hello en fase experimental y no tiene compatibilidad completa.

Las personalizaciones son necesarias para este ejemplo y se explican en pasos de Hola.

### <a name="add-modules"></a>Adición de módulos

toouse cmdlets de PowerShell de Monitor de red, cargue la aplicación de hello más reciente PowerShell módulo toohello función.

1. En el equipo local con los módulos de PowerShell de Azure más recientes Hola instalado, ejecute hello siguiente comando de PowerShell:

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    Esto deja de ejemplo Hola ruta de acceso local de los módulos de PowerShell de Azure. Estas carpetas se usan en un paso posterior. los módulos de Hola que se usan en este escenario son:

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

    ![Carpetas de PowerShell][functions5]

1. Seleccione **función de la configuración de la aplicación** > **vaya tooApp Editor servicio**.

    ![Configuración de Function App][functions2]

1. Menú contextual hello **AlertPacketCapturePowershell** carpeta y, a continuación, cree una carpeta denominada **azuremodules**. 

4. Cree una subcarpeta para cada módulo que necesite.

    ![Carpeta y subcarpetas][functions3]

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

1. Menú contextual hello **AzureRM.Network** subcarpeta y, a continuación, seleccione **cargar archivos**. 

6. Vaya tooyour Azure módulos. Hola local **AzureRM.Network** carpeta, seleccione todos los archivos de hello en carpeta de Hola. Después seleccione **Aceptar**. 

7. Repita estos pasos para **AzureRM.Profile** y **AzureRM.Resources**.

    ![Carga de archivos][functions6]

1. Una vez finalizado, cada carpeta debe tener archivos de módulo de PowerShell de Hola desde el equipo local.

    ![Archivos de PowerShell][functions7]

### <a name="authentication"></a>Autenticación

cmdlets de PowerShell de hello toouse, debe autenticarse. Configurar la autenticación en la aplicación de la función de hello. autenticación de tooconfigure, debe configurar las variables de entorno y cargar una aplicación de función de toohello de archivo de clave de cifrado.

> [!NOTE]
> Este escenario proporciona solo un ejemplo de cómo tooimplement la autenticación con las funciones de Azure. Hay otra maneras toodo esto.

#### <a name="encrypted-credentials"></a>Credenciales cifradas

Hola siguiente script de PowerShell crea un archivo de claves denominado **PassEncryptKey.key**. También proporciona una versión cifrada de la contraseña de hello proporcionado. Esta contraseña es hello misma contraseña que se define para la aplicación de Azure Active Directory de Hola que se usa para la autenticación.

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

En el Editor de aplicación de servicio de aplicación de la función de hello hello, cree una carpeta denominada **claves** en **AlertPacketCapturePowerShell**. A continuación, cargar hello **PassEncryptKey.key** archivo que creó en el ejemplo anterior de PowerShell de Hola.

![Clave de funciones][functions8]

### <a name="retrieve-values-for-environment-variables"></a>Recuperación de valores para variables de entorno

requisito final de Hello es tooset las variables de entorno de Hola que son valores de hello tooaccess necesarios para la autenticación. Hello lista siguiente muestra las variables de entorno de Hola que se crean:

* AzureClientID

* AzureTenant

* AzureCredPassword


#### <a name="azureclientid"></a>AzureClientID

Id. de cliente Hello es hello Id. de aplicación de una aplicación en Azure Active Directory.

1. Si aún no tiene un toouse de aplicación, ejecutar Hola después toocreate de ejemplo de una aplicación.

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > contraseña de Hola que usar al crear aplicación hello debe ser Hola misma contraseña que creó anteriormente cuando se guarda el archivo de clave de Hola.

1. Hola portal de Azure, seleccione **suscripciones**. Seleccione toouse de suscripción de hello y, a continuación, seleccione **(de índices IAM) de control de acceso**.

    ![IAM de Functions][functions9]

1. Elija toouse de cuenta de hello y, a continuación, seleccione **propiedades**. Copiar Hola identificador de aplicación.

    ![Id. de aplicación de Functions][functions10]

#### <a name="azuretenant"></a>AzureTenant

Obtener Id. de inquilino de hello ejecutando Hola siguiendo el ejemplo de PowerShell:

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a>AzureCredPassword

valor de Hola de variable de entorno AzureCredPassword hello es valor de Hola que obtendrá ejecutaran Hola siguiendo el ejemplo de PowerShell. En este ejemplo se Hola misma que se muestra en hello anterior **credenciales cifradas** sección. Hola valor requerido es una salida de hello de hello `$Encryptedpassword` variable.  Se trata de hello servicio contraseña de la entidad que se ha cifrado mediante script de PowerShell de Hola.

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a>Almacenar las variables de entorno de Hola

1. Aplicación de la función de toohello vaya. A continuación, seleccione **Configuración de Function App** > **Configurar las opciones de la aplicación**.

    ![Configuración de aplicaciones][functions11]

1. Agregar variables de entorno de Hola y configuración de la aplicación toohello de sus valores y, a continuación, seleccione **guardar**.

    ![Configuración de la aplicación][functions12]

### <a name="add-powershell-toohello-function"></a>Add toohello de PowerShell (función)

Es ahora toomake tiempo llama al Monitor de red desde dentro de hello Azure función. Dependiendo de los requisitos de hello, implementación de Hola de esta función puede variar. Sin embargo, el flujo general de Hola de código de hello es como sigue:

1. Procesar los parámetros de entrada.
2. Paquete existente de la consulta de captura tooverify límites y resolver conflictos de nombre.
3. Crear una captura de paquetes con los parámetros adecuados.
4. Sondear la captura de paquetes periódicamente hasta que finalice.
5. Notificar a usuario Hola que sesión de captura de paquetes de saludo ha finalizado.

Hello en el ejemplo siguiente se es código de PowerShell que puede usarse en función de Hola. Hay valores que necesitan toobe reemplazado para **subscriptionId**, **resourceGroupName**, y **storageAccountName**.

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a>Recuperar la dirección URL de hello (función) 
1. Después de crear la función, configure la dirección URL de Hola de toocall alerta que esté asociada con la función hello. tooget este valor, la función de copiar Hola dirección URL desde la aplicación de la función.

    ![Buscar la dirección URL de hello (función)][functions13]

2. Copiar dirección URL de la función de hello para la aplicación de la función.

    ![Copiar dirección URL de hello (función)][2]

Si necesitas propiedades personalizadas en la carga de Hola de solicitud POST de webhook de hello, consulte demasiado[configurar un webhook en una alerta de métrica Azure](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

## <a name="configure-an-alert-on-a-vm"></a>Configuración de una alerta en una máquina virtual

Las alertas pueden estar configurado toonotify personas cuando una métrica específica supera un umbral que se asigna tooit. En este ejemplo, alerta de hello es en hello segmentos TCP que se envían, pero se puede activar la alerta de Hola para muchas otras métricas. En este ejemplo, una alerta es toocall configurado una función de webhook toocall Hola.

### <a name="create-hello-alert-rule"></a>Crear regla de alerta de Hola

Vaya a máquina virtual existente de tooan y, a continuación, agregar una regla de alerta. Se puede encontrar documentación más detallada sobre la configuración de alertas en [Creación de alertas en Azure Monitor para servicios de Azure (Azure Portal)](../monitoring-and-diagnostics/insights-alerts-portal.md). Escriba Hola después de valores de hello **regla de alerta** hoja y, a continuación, seleccione **Aceptar**.

  |**Configuración** | **Valor** | **Detalles** |
  |---|---|---|
  |**Name**|TCP_Segments_Sent_Exceeded|Nombre de regla de alerta de Hola.|
  |**Descripción**|Los segmentos TCP enviados superaron el umbral|Descripción de Hello para la regla de alerta de Hola.||
  |**Métrica**|Segmentos TCP enviados| alerta de Hello toouse métrica tootrigger Hola. |
  |**Condition**|Mayor que| Hola condición toouse al evaluar la métrica de Hola.|
  |**Umbral**|100| valor de Hola de métrica de Hola que desencadena la alerta de Hola. Este valor debe establecerse tooa valor válido para su entorno.|
  |**Período**|A través de hello últimos cinco minutos| Determina el período de hello en qué toolook para el umbral de hello en métrica Hola.|
  |**Webhook**|[Dirección URL del webhook de la aplicación de función]| URL del webhook Hola de aplicación de función hello que creó en los pasos anteriores de Hola.|

> [!NOTE]
> métrica de segmentos de Hello TCP no está habilitado de forma predeterminada. Más información acerca de cómo tooenable otras métricas visitando [habilitar la supervisión y diagnóstico](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).

## <a name="review-hello-results"></a>Revisar los resultados de Hola

Después de criterios de Hola para desencadenadores de alerta de hello, se crea una captura de paquetes. Vaya tooNetwork monitor y, a continuación, seleccione **captura de paquetes**. En esta página, puede seleccionar Hola paquete captura archivo vínculo toodownload Hola captura de paquetes.

![Visualización de captura de paquetes][functions14]

Si el archivo de captura de Hola se almacena localmente, puede recuperarlo mediante la firma en la máquina virtual de toohello.

Para obtener instrucciones sobre cómo descargar archivos desde cuentas de Azure Storage, consulte [Introducción a Azure Blob Storage mediante .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Otra herramienta que puede usar es el [Explorador de almacenamiento](http://storageexplorer.com/).

Después de que se ha descargado la captura, puede verla con cualquier herramienta que pueda leer un archivo **.cap**. Estos son vínculos tootwo de estas herramientas:

- [Analizador de mensajes de Microsoft](https://technet.microsoft.com/library/jj649776.aspx).
- [WireShark](https://www.wireshark.org/)

## <a name="next-steps"></a>Pasos siguientes

Obtenga información acerca de cómo tooview su paquete captura visitando [análisis de captura de paquetes con Wireshark](network-watcher-deep-packet-inspection.md).


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
