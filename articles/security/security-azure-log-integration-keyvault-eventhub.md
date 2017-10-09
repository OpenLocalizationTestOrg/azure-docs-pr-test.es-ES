---
title: "registros de aaaIntegrate desde el almacén de claves de Azure mediante el uso de los centros de eventos | Documentos de Microsoft"
description: "Tutorial que proporciona los pasos necesarios de hello toomake almacén de claves de registros disponible tooa SIEM mediante la integración de registro de Azure"
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a>Tutorial de integración de registros de Azure: Procesamiento de eventos de Azure Key Vault mediante Event Hubs

Puede usar eventos de integración de Azure Log tooretrieve iniciado y que estén en el sistema de administración (SIEM) de eventos e información de seguridad de tooyour disponible. Este tutorial muestra un ejemplo de cómo integración de registro de Azure puede ser usado tooprocess registros adquiridos a través de los centros de eventos de Azure.
 
Use este tutorial tooget familiarizará con la integración de registro de Azure y concentradores de eventos trabajo juntos siguiendo Hola ejemplos paso a paso y entender cómo cada paso es compatible con la solución de Hola. A continuación, puede realizarlo que ha aprendido aquí toocreate su propios pasos toosupport requisitos únicos de su empresa.

>[!WARNING]
pasos de Hola y comandos en este tutorial no son toobe previsto copiado y pegado. Tan solo son ejemplos. No use comandos de PowerShell de Hola "tal cual" en el entorno activo. Deben personalizarse en función del entorno específico.


Este tutorial le guiará por el proceso de Hola de tomar concentrador de eventos de almacén de claves de Azure actividad tooan registrado y ponerlo a disposición como sistema JSON archivos tooyour SIEM. A continuación, puede configurar los archivos JSON de SIEM sistema tooprocess Hola.

>[!NOTE]
>La mayoría de los pasos de hello en este tutorial implica la configuración de almacenes de claves, las cuentas de almacenamiento y los centros de eventos. pasos de integración de Azure registro específicos de Hello son final Hola de este tutorial. No realice estos pasos en un entorno de producción, ya que se han diseñado exclusivamente para un entorno de laboratorio. Debe personalizar los pasos de hello antes de usarlos en producción.

Proporciona información a lo largo de la manera de hello le ayuda a que comprender los motivos de hello detrás de cada paso. Artículos de tooother vínculos ofrecen más detalles sobre determinados temas.

Para obtener más información acerca de los servicios de Hola que se mencione en este tutorial, vea: 

- [Azure Key Vault](../key-vault/key-vault-whatis.md)
- [Azure Event Hubs](../event-hubs/event-hubs-what-is-event-hubs.md)
- [Integración de registros de Azure](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a>Configuración inicial

Para poder completar los pasos de hello en este artículo, necesita Hola siguiente:

1. Una suscripción de Azure y una cuenta en esa suscripción con derechos de administrador. Si no tiene una suscripción, puede crear [una cuenta gratuita](https://azure.microsoft.com/free/).
 
2. Un sistema con toohello de acceso a internet que cumpla los requisitos de hello para la instalación de integración de registro de Azure. sistema de Hello puede estar en un servicio de nube u hospedado en local.

3. La [integración de registros de Azure](https://www.microsoft.com/download/details.aspx?id=53324) instalada. tooinstall:

   a. Usar Escritorio remoto tooconnect toohello sistema mencionado en el paso 2.   
   b. Copie el sistema de toohello de instalador de integración de Azure registro de hello. También puede [descargar archivos de instalación de hello](https://www.microsoft.com/download/details.aspx?id=53324).   
   c. Inicie al instalador de Hola y acepte los términos de licencia del Software de Microsoft de Hola.   
   d. Si va a proporcionar información de telemetría, deje activada la casilla de verificación de Hola. Si en su lugar enviaría no tooMicrosoft de información de uso, desactive la casilla de verificación de Hola.
   
   Para obtener más información acerca de la integración de registro de Azure y cómo tooinstall, consulte [integración de registro de Azure con el registro de diagnósticos de Azure y reenvío de eventos de Windows](security-azure-log-integration-get-started.md).

4. versión de PowerShell de Hello más reciente.
 
   Si tiene instalado Windows Server 2016, entonces tiene al menos PowerShell 5.0. Si usa otra versión de Windows Server, es posible que tenga instalada una versión anterior de PowerShell. Puede comprobar la versión de Hola escribiendo ```get-host``` en una ventana de PowerShell. Si no tiene PowerShell 5.0 instalado, puede [descargarlo](https://www.microsoft.com/download/details.aspx?id=50395).

   Una vez haya al menos PowerShell 5.0, puede continuar la versión más reciente de Hola tooinstall:
   
   a. En una ventana de PowerShell, escriba Hola ```Install-Module Azure``` comando. Complete los pasos de instalación de Hola.    
   b. Escriba hello ```Install-Module AzureRM``` comando. Complete los pasos de instalación de Hola.

   Para más información, vea [Instalar Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).


## <a name="create-supporting-infrastructure-elements"></a>Crear los elementos de la infraestructura de soporte

1. Abra una ventana de PowerShell con privilegios elevados y vaya demasiado**C:\Program Files\Microsoft Azure registro integración**.
2. Importar hello AzLog cmdlets al ejecutar el script de Hola LoadAzLogModule.ps1. Escriba hello `.\LoadAzLogModule.ps1` comando. (Hola aviso ". \" en el comando.) Puede ver algo así:</br>

   ![Lista de módulos cargados](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. Escriba hello `Login-AzureRmAccount` comando. En la ventana de inicio de sesión de hello, escriba la información de credenciales de hello para la suscripción de Hola que va a utilizar para este tutorial.

   >[!NOTE]
   >Si se trata de hello primera vez que está iniciando una sesión en tooAzure de este equipo, verá un mensaje que permita que los datos de uso de PowerShell de Microsoft toocollect. Se recomienda que habilite esta recopilación de datos ya que será usado tooimprove PowerShell de Azure.

4. Tras la autenticación correcta, ha iniciado sesión y ver información de Hola Hola siguiente captura de pantalla. Tome nota del nombre de identificador y la suscripción de la suscripción de hello, porque los necesitará más adelante pasos toocomplete.

   ![Ventana de PowerShell](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. Cree variables toostore valores que se usará más adelante. Escriba cada una de hello después de las líneas de PowerShell. Puede que tenga tooadjust Hola valores toomatch su entorno.
    - ```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (El nombre de la suscripción puede ser diferente. Puede ver, como parte del resultado de hello del comando anterior Hola.)
    - ```$location = 'West US'```(Esta variable será la ubicación de Hola de toopass usado donde se deben crear recursos. Puede cambiar esta variable toobe cualquier ubicación de su elección.)
    - ```$random = Get-Random```
    - ``` $name = 'azlogtest' + $random```(nombre de hello puede ser cualquier cosa, pero debe incluir solo letras minúsculas y números).
    - ``` $storageName = $name```(Esta variable se usará para el nombre de cuenta de almacenamiento de Hola.)
    - ```$rgname = $name ```(Esta variable se usará para el nombre de grupo de recursos de Hola.)
    - ``` $eventHubNameSpaceName = $name```(Esto es nombre de Hola de espacio de nombres del concentrador de eventos de hello).
6. Especifique la suscripción de Hola que se va a trabajar con:
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. Cree un grupo de recursos:
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   Si escribe `$rg` en este punto, debería ver la salida de pantalla de toothis similar:

   ![Salida después de la creación de un grupo de recursos](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. Cree una cuenta de almacenamiento que será tookeep usa seguimiento de información de estado:
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. Crear espacio de nombres del concentrador de eventos de Hola. Esto es necesario toocreate un concentrador de eventos.
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. Obtener Id. de función hello que se usará con el proveedor de la visión de hello:
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. Obtenga todas las ubicaciones posibles de Azure y agregue la variable tooa de hello nombres que se puede usar en un paso posterior:
    
    a. ```$locationObjects = Get-AzureRMLocation```    
    b. ```$locations = @('global') + $locationobjects.location```
    
    Si escribe `$locations` en este momento, verá los nombres de ubicación de hello sin información adicional de hello devuelto por Get-AzureRmLocation.
12. Cree un perfil de registro de Azure Resource Manager: 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    Para obtener más información acerca de hello perfil de registros de Azure, consulte [información general de hello Azure Activity Log](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).

> [!NOTE]
> Podría obtener un mensaje de error cuando intente toocreate un perfil de registro. A continuación, puede revisar la documentación de Hola para Get-AzureRmLogProfile y Remove-AzureRmLogProfile. Si ejecuta Get-AzureRmLogProfile, verá información sobre el perfil de registro de hello. Puede eliminar el perfil de registro existente de hello escribiendo hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` comando.
>
>![Error de perfil de Resource Manager](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a>Creación de un Almacén de claves

1. Crear almacén de claves de hello:

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. Configurar el registro de almacén de claves de hello:

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a>Generar actividad de registro

Solicitudes necesitan toobe envía tooKey actividad de registro de toogenerate de almacén. Acciones como la generación de claves, la lectura o el almacenamiento de secretos de Key Vault, crearán entradas del registro.

1. Mostrar claves de almacenamiento actual de hello:
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. Genere una nueva **key2**:
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. Mostrar teclas de Hola de nuevo y lo vea **key2** contiene un valor diferente:
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. Establecer y leer un secreto toogenerate entradas de registro adicionales:
    
   a. ```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` b. ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Secreto devuelto](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a>Configurar la integración de registros de Azure

Ahora que ha configurado el centro de eventos de todos los Hola elementos necesarios toohave registro de almacén de claves tooan, necesita tooconfigure integración de registro de Azure:

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

Ejecute hello AzLog comando para cada concentrador de eventos:

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

Tras un minuto aproximadamente de dos últimos comandos hello en ejecución, debería ver los archivos JSON que se generan. Puede confirmar que mediante la supervisión de directorio de hello **C:\users\AzLog\EventHubJson**.

## <a name="next-steps"></a>Pasos siguientes

- [Preguntas más frecuentes sobre la integración de registro de Azure](security-azure-log-integration-faq.md)
- [Introducción a la integración de registros de Azure](security-azure-log-integration-get-started.md)
- [Integrar registros de recursos de Azure en sistemas SIEM](security-azure-log-integration-overview.md)
