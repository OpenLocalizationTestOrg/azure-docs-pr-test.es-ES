---
title: "certificados aaaManage en un clúster de Azure Service Fabric | Documentos de Microsoft"
description: "Describe cómo tooadd nuevos certificados, el certificado de sustitución y quitar certificados tooor desde un clúster de Service Fabric."
services: service-fabric
documentationcenter: .net
author: ChackDan
manager: timlt
editor: 
ms.assetid: 91adc3d3-a4ca-46cf-ac5f-368fb6458d74
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/09/2017
ms.author: chackdan
ms.openlocfilehash: 8e57bd95dbb800ecc04cf6988047e3abdc2fe56a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-certificates-for-a-service-fabric-cluster-in-azure"></a>Agregar o quitar certificados para un clúster de Service Fabric de Azure
Se recomienda que familiarizarse con cómo Service Fabric utiliza los certificados X.509 y estar familiarizado con hello [los escenarios de seguridad de clúster](service-fabric-cluster-security.md). Debe entender qué es un certificado de clúster y para qué se usa antes de seguir avanzando.

Servicio fabric le permite que especificar que dos clústeres certificados, principal y un elemento secundario, al configurar certificados seguridad durante la creación del clúster, en los certificados de tooclient de adición. Consulte demasiado[crear un clúster mediante el portal de azure](service-fabric-cluster-creation-via-portal.md) o [creación de un clúster de azure mediante Azure Resource Manager](service-fabric-cluster-creation-via-arm.md) para obtener más información sobre cómo configurarlas en el momento de su creación. Si especifica solo un certificado de clúster en el momento de creación, a continuación, en el que se usa como certificado principal de Hola. Después de la creación del clúster, puede agregar un nuevo certificado como elemento secundario.

> [!NOTE]
> Para un clúster de seguro, siempre deberá certificado de al menos un clúster (no revocados y no expirados) válidos (principal o secundario) implementado (si no, Hola clúster dejará de funcionar). 90 días antes de que todos los certificados válidos alcancen la expiración, sistema de hello genera un seguimiento de advertencia y también un evento de estado de advertencia en el nodo de Hola. Actualmente, Service Fabric no envía ningún mensaje de correo electrónico ni cualquier otra notificación sobre este tema. 
> 
> 

## <a name="add-a-secondary-cluster-certificate-using-hello-portal"></a>Agregar un certificado de clúster secundario mediante el portal de Hola

No se puede agregar el certificado de clúster secundario a través de hello portal de Azure. Tiene toouse Azure powershell para que. proceso de Hola se describe más adelante en este documento.

## <a name="swap-hello-cluster-certificates-using-hello-portal"></a>Intercambiar los certificados de clúster de hello mediante el portal de Hola

Después de haber implementado correctamente un certificado de clúster secundario, si desea tooswap Hola principal y secundaria, a continuación, navegue toohello hoja de seguridad y la opción hello 'Intercambio con principal' de hello contexto menú tooswap Hola secundaria cert con certificado principal de Hola.

![Intercambiar certificado][Delete_Swap_Cert]

## <a name="remove-a-cluster-certificate-using-hello-portal"></a>Quitar un certificado de clúster mediante el portal de Hola

Para un clúster de seguro, siempre necesitará al menos un válido (no revocado y no expirado) certificado (principal o secundario) implementado en caso contrario, Hola clúster dejará de funcionar.

tooremove certificado secundario se utilice para la seguridad de clúster, Navigate toohello Security blade y opción de 'Delete' hello seleccione del menú contextual de hello en certificado secundario Hola.

Si su intención es certificado de hello tooremove marcado principal y, a continuación, deberá tooswap con Hola secundaria en primer lugar y, a continuación, eliminar Hola secundaria una vez completada la actualización Hola.

## <a name="add-a-secondary-certificate-using-resource-manager-powershell"></a>Incorporación de un certificado secundario mediante Powershell para Resource Manager

Estos pasos se supone que está familiarizado con cómo funciona el Administrador de recursos y ha implementado al menos un clúster de Service Fabric mediante una plantilla de administrador de recursos y tiene plantilla de Hola que usa tooset clúster Hola práctica. También se da por hecho que está familiarizado con el uso de JSON.

> [!NOTE]
> Si desea obtener una plantilla de ejemplo y los parámetros que se puede usar toofollow a lo largo o como punto de partida, descárguelo desde esta [repositorio de git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample). 
> 
> 

### <a name="edit-your-resource-manager-template"></a>Edición de la plantilla de Resource Manager

Para facilitar su siguiente a lo largo, ejemplo 5-VM-1-NodeTypes-Secure_Step2.JSON contiene todas las ediciones de hello que realizaremos. ejemplo de Hola está disponible en [repositorio de git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample).

**Asegúrese de toofollow seguro de todos los pasos de Hola**

**Paso 1:** abra una plantilla de administrador de recursos de hello usa toodeploy del clúster. (Si ha descargado el ejemplo hello de Hola por encima del repositorio, a continuación, utilizar 5-VM-1-NodeTypes-Secure_Step1.JSON toodeploy un clúster segura y, a continuación, abrir dicha plantilla).

**Paso 2:** agregar **dos parámetros nuevos** "secCertificateThumbprint" y "secCertificateUrlValue" de tipo "string" toohello sección de parámetros de la plantilla. Puede copiar Hola siguiente fragmento de código y Agregar plantilla toohello. Según el origen de saludo de la plantilla, ya puede tener estos, caso en ese mover toohello siguiente paso. 
 
```JSON
   "secCertificateThumbprint": {
      "type": "string",
      "metadata": {
        "description": "Certificate Thumbprint"
      }
    },
    "secCertificateUrlValue": {
      "type": "string",
      "metadata": {
        "description": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
      }
    },

```

**Paso 3:** realizar cambios toohello **Microsoft.ServiceFabric/clusters** recurso, busque la definición de recursos "Microsoft.ServiceFabric/clusters" hello en la plantilla. En Propiedades de esa definición, encontrará "Certificado" JSON etiqueta, que debe ser similar Hola siguiente fragmento de JSON:

   
```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

Agregue una nueva etiqueta "thumbprintSecondary" y asígnele un valor "[parameters('secCertificateThumbprint')]".  

Por lo que ahora la definición de recursos de hello debería ser similar Hola siguiente (dependiendo del origen de plantilla de hello, puede que no sea exactamente igual que Hola de fragmento de código siguiente). 

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('certificateThumbprint')]",
          "thumbprintSecondary": "[parameters('secCertificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 

Si desea demasiado**certificado de sustitución hello**, a continuación, especifique el nuevo certificado de hello como principal actual de hello principal y mover como base de datos secundaria. Esto da como resultado en sustitución de Hola de su certificado primario toohello nuevo certificado actual en un paso de implementación.

```JSON
      "properties": {
        "certificate": {
          "thumbprint": "[parameters('secCertificateThumbprint')]",
          "thumbprintSecondary": "[parameters('certificateThumbprint')]",
          "x509StoreName": "[parameters('certificateStoreValue')]"
     }
``` 


**Paso 4:** realizar cambios demasiado**todos los** hello **Microsoft.Compute/virtualMachineScaleSets** las definiciones de recursos - busque hello Microsoft.Compute/virtualMachineScaleSets recurso definición. Desplácese toohello "publisher": "Microsoft.Azure.ServiceFabric" en "virtualMachineProfile".

En configuración del publicador de hello service fabric, debería ver algo parecido a esto.

![Json_Pub_Setting1][Json_Pub_Setting1]

Agregar Hola nuevo certificado entradas tooit

```JSON
               "certificateSecondary": {
                    "thumbprint": "[parameters('secCertificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```

propiedades de Hello deben tener el siguiente aspecto

![Json_Pub_Setting2][Json_Pub_Setting2]

Si desea demasiado**certificado de sustitución hello**, a continuación, especifique el nuevo certificado de hello como principal actual de hello principal y mover como base de datos secundaria. Esto da como resultado en sustitución de Hola de su certificado toohello nuevo certificado actual en un paso de implementación. 


```JSON
               "certificate": {
                   "thumbprint": "[parameters('secCertificateThumbprint')]",
                   "x509StoreName": "[parameters('certificateStoreValue')]"
                     },
               "certificateSecondary": {
                    "thumbprint": "[parameters('certificateThumbprint')]",
                    "x509StoreName": "[parameters('certificateStoreValue')]"
                    }
                  },

```
propiedades de Hello deben tener el siguiente aspecto

![Json_Pub_Setting3][Json_Pub_Setting3]


**Paso 5:** realizar cambios demasiado**todos los** hello **Microsoft.Compute/virtualMachineScaleSets** las definiciones de recursos - busque hello Microsoft.Compute/virtualMachineScaleSets recurso definición. Desplácese toohello "vaultCertificates":, en "OSProfile". Tendrá un aspecto similar al siguiente.


![Json_Pub_Setting4][Json_Pub_Setting4]

Agregar hello secCertificateUrlValue tooit. usar hello siguiente fragmento de código:

```Json
                  {
                    "certificateStore": "[parameters('certificateStoreValue')]",
                    "certificateUrl": "[parameters('secCertificateUrlValue')]"
                  }

```
Ahora Hola resultante Json debe tener un aspecto similar al siguiente.
![Json_Pub_Setting5][Json_Pub_Setting5]


> [!NOTE]
> Asegúrese de que se repite los pasos 4 y 5 para todas las definiciones de recursos de Nodetypes/Microsoft.Compute/virtualMachineScaleSets hello en la plantilla. Si se salta a uno de ellos, no podrá instalarse certificado hello en ese VMSS y tendrá resultados imprevisibles en el clúster, incluidos los clúster Hola dirigiéndose hacia abajo (si se terminará con ningún certificado válido que puede utilizar ese clúster hello para la seguridad. Compruébelo dos veces antes de continuar.
> 
> 


### <a name="edit-your-template-file-tooreflect-hello-new-parameters-you-added-above"></a>Editar los plantilla archivo tooreflect Hola nuevos parámetros que agregó anteriormente
Si usas ejemplo Hola Hola [repositorio de git](https://github.com/ChackDan/Service-Fabric/tree/master/ARM%20Templates/Cert%20Rollover%20Sample) toofollow desde el principio, puede iniciar toomake cambios en el ejemplo hello 5-VM-1-NodeTypes-Secure.paramters_Step2.JSON 

Editar el parámetro de plantilla de administrador de recursos del archivo, agregue dos parámetros nuevos Hola para secCertificateThumbprint y secCertificateUrlValue. 

```JSON
    "secCertificateThumbprint": {
      "value": "thumbprint value"
    },
    "secCertificateUrlValue": {
      "value": "Refers toohello location URL in your key vault where hello certificate was uploaded, it is should be in hello format of https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>"
     },

```

### <a name="deploy-hello-template-tooazure"></a>Implementar Hola plantilla tooAzure

- Se está ahora listo toodeploy su tooAzure de plantilla. Abra un símbolo del sistema de Azure PS versión 1 o superior.
- Inicie sesión en tooyour cuenta de Azure y seleccione la suscripción de azure específica Hola. Se trata de un paso importante para personas que tienen acceso toomore a una suscripción de azure.

```powershell
Login-AzureRmAccount
Select-AzureRmSubscription -SubscriptionId <Subcription ID> 

```

Probar Hola plantilla anterior toodeploying lo. Use Hola mismo grupo de recursos que el clúster está implementado actualmente en.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>

```

Implementar grupo de recursos de hello plantilla tooyour. Use Hola mismo grupo de recursos que el clúster está implementado actualmente en. Ejecute hello AzureRmResourceGroupDeployment nuevo comando. No es necesario el modo de hello toospecify, puesto que es el valor predeterminado de hello **incremental**.

> [!NOTE]
> Si establece el modo tooComplete, puede eliminar accidentalmente los recursos que no están en la plantilla. Por ello no lo utilice en este escenario.
> 
> 

```powershell
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName <Resource Group that your cluster is currently deployed to> -TemplateFile <PathToTemplate>
```

Esta es una forma rellena ejemplo de Hola powershell mismo.

```powershell
$ResouceGroup2 = "chackosecure5"
$TemplateFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure_Step2.json"
$TemplateParmFile = "C:\GitHub\Service-Fabric\ARM Templates\Cert Rollover Sample\5-VM-1-NodeTypes-Secure.parameters_Step2.json"

New-AzureRmResourceGroupDeployment -ResourceGroupName $ResouceGroup2 -TemplateParameterFile $TemplateParmFile -TemplateUri $TemplateFile -clusterName $ResouceGroup2

```

Una vez completada la implementación de hello, conectar tooyour clúster con Hola nuevo certificado y realizar algunas consultas. Si es capaz de toodo. A continuación, puede eliminar los certificados antiguos Hola. 

Si está utilizando un certificado autofirmado, no olvide tooimport en su almacén de certificados local TrustedPeople.

```powershell
######## Set up hello certs on your local box
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My -FilePath c:\Mycertificates\chackdanTestCertificate9.pfx -Password (ConvertTo-SecureString -String abcd123 -AsPlainText -Force)

```
Referencia rápida mostramos clúster segura de hello comando tooconnect tooa 

```powershell
$ClusterName= "chackosecure5.westus.cloudapp.azure.com:19000"
$CertThumbprint= "70EF5E22ADB649799DA3C8B6A6BF7SD1D630F8F3" 

Connect-serviceFabricCluster -ConnectionEndpoint $ClusterName -KeepAliveIntervalInSec 10 `
    -X509Credential `
    -ServerCertThumbprint $CertThumbprint  `
    -FindType FindByThumbprint `
    -FindValue $CertThumbprint `
    -StoreLocation CurrentUser `
    -StoreName My
```
Referencia rápida aquí es el estado de clúster de hello comando tooget

```powershell
Get-ServiceFabricClusterHealth 
```

## <a name="deploying-application-certificates-toohello-cluster"></a>Implementación de clúster de toohello de certificados de aplicación.

Puede usar Hola mismo pasos tal como se describe en los pasos 5 anteriormente toohave Hola certificados implementados a partir de un toohello keyvault nodos. Solo necesita definir y usar parámetros diferentes.


## <a name="adding-or-removing-client-certificates"></a>Incorporación o eliminación de certificados de cliente

En los certificados de clúster de suma toohello, puede agregar operaciones de administración de tooperform de certificados de cliente en un clúster de service fabric.

Puede agregar dos tipos de certificados de cliente: administrador o solo lectura. A continuación, puede tratarse de operaciones de administración de toocontrol usa acceso toohello y operaciones de consulta en el clúster de Hola. De forma predeterminada, los certificados de clúster de Hola se agregan toohello lista de certificados de administración de elementos permitido.

Puede especificar cualquier número de certificados de cliente. Resultados de cada adición o eliminación en un clúster de configuración update toohello service fabric


### <a name="adding-client-certificates---admin-or-read-only-via-portal"></a>Incorporación de certificados de cliente de administrador o solo lectura mediante el portal

1. Desplácese toohello hoja de seguridad y seleccione Hola "+ autenticación" botón encima de la hoja de seguridad de Hola.
2. En la hoja de 'Agregar autenticación' hello, elija hello 'Autenticación de tipo' - 'Solo lectura cliente' o ' Admin'
3. Elegir método de autorización de hello. Esto indica tooService tejido si debe buscar este certificado mediante el nombre del firmante de Hola o huella digital de Hola. En general, no es un método de autorización de seguridad buena práctica toouse Hola de nombre de sujeto. 

![Incorporación de certificados de cliente][Add_Client_Cert]

### <a name="deletion-of-client-certificates---admin-or-read-only-using-hello-portal"></a>Eliminación de certificados de cliente - administrador o solo lectura, utilice Hola portal

tooremove certificado secundario se utilice para la seguridad de clúster, Navigate toohello Security blade y opción de 'Delete' hello seleccione del menú contextual de hello en certificado específico de Hola.



## <a name="next-steps"></a>Pasos siguientes
Lea estos artículos para más información sobre la administración de clúster:

* [Proceso de actualización del clúster de Service Fabric y expectativas del usuario](service-fabric-cluster-upgrade.md)
* [Control de acceso basado en roles para clientes de Service Fabric](service-fabric-cluster-security-roles.md)

<!--Image references-->
[Delete_Swap_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_09.PNG
[Add_Client_Cert]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_13.PNG
[Json_Pub_Setting1]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_14.PNG
[Json_Pub_Setting2]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_15.PNG
[Json_Pub_Setting3]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_16.PNG
[Json_Pub_Setting4]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_17.PNG
[Json_Pub_Setting5]: ./media/service-fabric-cluster-security-update-certs-azure/SecurityConfigurations_18.PNG


