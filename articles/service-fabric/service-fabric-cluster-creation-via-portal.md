---
title: "clúster de Service Fabric aaaCreate en hello portal de Azure | Documentos de Microsoft"
description: "Este artículo describe cómo tooset un clúster de Service Fabric segura en Azure mediante Hola portal de Azure y el almacén de claves de Azure."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a>Crear un clúster de Service Fabric en Azure con hello portal de Azure
> [!div class="op_single_selector"]
> * [Administrador de recursos de Azure](service-fabric-cluster-creation-via-arm.md)
> * [Portal de Azure](service-fabric-cluster-creation-via-portal.md)
> 
> 

Esta es una guía paso a paso que le guiará por los pasos de Hola de configuración de un clúster de Service Fabric seguro en Azure con hello portal de Azure. Esta guía describen Hola pasos:

* Configure el almacén de claves toomanage claves para seguridad de clúster.
* Crear un clúster protegido en Azure a través de hello portal de Azure.
* Autenticación de los administradores mediante certificados.

> [!NOTE]
> Para información sobre opciones de seguridad más avanzadas, como la autenticación de usuarios con Azure Active Directory y la configuración de certificados para la seguridad de las aplicaciones, [cree el clúster mediante Azure Resource Manager][create-cluster-arm].
> 
> 

Un clúster seguro es un clúster que evite las operaciones de toomanagement de acceso no autorizado, que incluye implementar, actualizar y eliminar aplicaciones, servicios y datos de Hola que contienen. Un clúster es un clúster que cualquiera puede conectarse tooat en cualquier momento y realizar operaciones de administración. Aunque es posible toocreate un clúster no seguro, es **recomienda toocreate un clúster segura**. Un clúster no seguro **no se puede proteger en un momento posterior** -se debe crear uno nuevo.

conceptos de Hola se Hola mismo para la creación de clústeres seguros, ya sea clústeres Hola son los clústeres de Linux o clústeres de Windows. Para más información y scripts de aplicaciones auxiliares para crear clústeres seguros de Linux, consulte [Creación de clústeres seguros en Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters). Hello parámetros obtenidos al script de aplicación auxiliar de hello proporcionado se pueden especificar directamente en el portal de hello tal y como se describe en la sección de hello [crear un clúster en el portal de Azure hello](#create-cluster-portal).

## <a name="log-in-tooazure"></a>Inicie sesión en tooAzure
En esta guía se usa [Azure PowerShell][azure-powershell]. Al iniciar una nueva sesión de PowerShell, inicie sesión en tooyour cuenta de Azure y seleccione su suscripción antes de ejecutar comandos de Azure.

Inicie sesión en la cuenta de azure tooyour:

```powershell
Login-AzureRmAccount
```

Seleccione su suscripción:

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a>Configuración del Almacén de claves
Esta parte de la Guía de hello le guía por la creación de un almacén de claves para un clúster de Service Fabric en Azure y para las aplicaciones de Service Fabric. Para obtener una guía completa en el almacén de claves, vea hello [el almacén de claves Guía de introducción][key-vault-get-started].

Service Fabric utiliza certificados X.509 toosecure un clúster. Almacén de claves de Azure es toomanage usa certificados para los clústeres de Service Fabric en Azure. Cuando se implementa un clúster de Azure, proveedor de recursos de Azure de hello responsable de crear clústeres de Service Fabric extrae los certificados de almacén de claves y los instala en clúster de hello las máquinas virtuales.

Hello siguiente diagrama ilustra Hola relación entre el almacén de claves, un clúster de Service Fabric y el proveedor de recursos de Azure de Hola que utiliza certificados almacenados en el almacén de claves cuando crea un clúster:

![Instalación del certificado][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>Creación de un grupo de recursos
Hola primer paso es toocreate un nuevo grupo de recursos específicamente para el almacén de claves. Poner el almacén de claves en su propio grupo de recursos se recomienda para que pueda quitar grupos de recursos de proceso y almacenamiento, como grupo de recursos de Hola que tiene el clúster de Service Fabric - sin perder sus claves y secretos. grupo de recursos de Hola que tiene su almacén de claves debe estar en hello misma región que el clúster de Hola que lo está usando.

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a>Create Key Vault
Crear un almacén de claves en el nuevo grupo de recursos Hola. el almacén de claves de Hello **debe estar habilitada para la implementación** tooallow Hola certificados de tooget de proveedor de recursos de Service Fabric de ella e instalar en nodos de clúster:

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```

Si tiene un Almacén de claves existente, puede habilitarlo para implementación mediante la CLI de Azure:

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a>Agregar tooKey el almacén de certificados
Los certificados se utilizan en toosecure de autenticación y cifrado de Service Fabric tooprovide diversos aspectos de un clúster y sus aplicaciones. Para obtener más información sobre el modo en que se usan los certificados en Service Fabric, consulte los [Escenarios de seguridad de los clústeres de Service Fabric][service-fabric-cluster-security].

### <a name="cluster-and-server-certificate-required"></a>Certificado de clúster y servidor (obligatorio)
Este certificado es necesario toosecure un clúster y evitar tooit de acceso no autorizado. La seguridad adopta dos formas:

* **Autenticación del clúster:** se autentica la comunicación de nodo a nodo para la federación del clúster. Sólo los nodos que se pueden demostrar su identidad con este certificado pueden unirse a clústeres de Hola.
* **Autenticación de servidor:** autentica el cliente de administración de la tooa de los puntos de conexión de administración con hello clúster, por lo que hello administración cliente sabe está hablando clúster real toohello. Este certificado también proporciona SSL para hello API de administración de HTTPS y para el Explorador de Service Fabric a través de HTTPS.

tooserve estos fines, certificado Hola debe cumplir Hola según los requisitos:

* certificado de Hello debe contener una clave privada.
* certificado de Hello debe crearse para el intercambio de claves, exportable tooa archivo de intercambio de información Personal (.pfx).
* Hello nombre de sujeto del certificado debe coincidir con clúster de Service Fabric de hello dominio utilizado tooaccess Hola. Esto es necesario tooprovide SSL de extremos de administración de HTTPS y el Explorador de Service Fabric del clúster de Hola. No se puede obtener un certificado SSL de una entidad de certificación (CA) para hello `.cloudapp.azure.com` dominio. Adquiera un nombre de dominio personalizado para el clúster. Cuando se solicita un certificado del nombre de sujeto del certificado de hello CA debe coincidir con nombre de dominio personalizado de hello utilizado para el clúster.

### <a name="client-authentication-certificates"></a>Certificados de autenticación de cliente
Los certificados de cliente adicionales autentican a los administradores en las tareas de administración del clúster. Service Fabric tiene dos niveles de acceso: **administrador** y **usuario de solo lectura**. Se debe usar como mínimo un certificado para el acceso administrativo. Para accesos de nivel de usuario adicionales, se debe proporcionar un certificado diferente. Para obtener más información sobre los roles de acceso, consulte [Control de acceso basado en roles para clientes de Service Fabric][service-fabric-cluster-security-roles].

No es necesario tooupload cliente autenticación certificados tooKey almacén toowork con Service Fabric. Estos certificados solo necesitan toobe proporcionan toousers que estén autorizados para la administración de clúster. 

> [!NOTE]
> Azure Active Directory es Hola recomienda a clientes de manera tooauthenticate para clúster de las operaciones de administración. toouse Azure Active Directory, debe [crear un clúster mediante el Administrador de recursos de Azure][create-cluster-arm].
> 
> 

### <a name="application-certificates-optional"></a>Certificados de aplicación (opcionales)
Se puede instalar un número cualquiera de certificados adicionales en un clúster para proteger la aplicación. Antes de crear el clúster, considere la posibilidad de escenarios de seguridad de aplicación Hola que requieren un toobe de certificados instalado en nodos de hello, como:

* Cifrado y descifrado de los valores de configuración de aplicación
* Cifrado de datos entre nodos durante la replicación 

No se puede configurar certificados de aplicación al crear un clúster a través de hello portal de Azure. tooconfigure certificados de aplicación en tiempo de instalación de clúster, debe [crear un clúster mediante el Administrador de recursos de Azure][create-cluster-arm]. También puede agregar clúster de toohello certificados de aplicación una vez creada.

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Formato de certificados para el uso del proveedor de recursos de Azure
Los archivos de clave privada (.pfx) se pueden agregar y usar directamente mediante el Almacén de claves. Sin embargo, el proveedor de recursos de Azure Hola requiere toobe de claves que se almacenan en un formato JSON especial que incluye .pfx Hola como un Base64 codificado hello y cadena de contraseña de clave privada. tooaccommodate estos requisitos, las claves deben colocarse en una cadena JSON y, a continuación, se almacenan como *secretos* en el almacén de claves.

toomake facilitar este proceso, un módulo de PowerShell es [disponible en GitHub][service-fabric-rp-helpers]. Siga estos módulo de hello toouse de pasos:

1. Descargar contenido completo de hello del repositorio de hello en un directorio local. 
2. Importar el módulo de hello en la ventana de PowerShell:

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

Hola `Invoke-AddCertToKeyVault` comandos en este módulo de PowerShell da formato a una clave privada del certificado en una cadena JSON y lo carga tooKey almacén automáticamente. Úsela certificado de clúster de hello tooadd y cualquier tooKey de certificados de aplicación adicionales almacén. Repita este paso para todos los certificados adicionales que desee tooinstall en el clúster.

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

Se trata de todos los requisitos previos del almacén de claves de Hola para configurar una plantilla de administrador de recursos de clúster de Service Fabric que se instala certificados para la autenticación de nodo, seguridad del punto de conexión de administración y la autenticación y cualquier seguridad adicional para la aplicación características que usan certificados X.509. En este punto, ahora debería tener Hola después de la instalación de Azure:

* Grupo de recursos del Almacén de claves
  * Almacén de claves
    * Certificado de autenticación de servidor de clúster

</a "create-cluster-portal" ></a>

## <a name="create-cluster-in-hello-azure-portal"></a>Crear clúster en hello portal de Azure
### <a name="search-for-hello-service-fabric-cluster-resource"></a>Busque Hola recurso de clúster de Service Fabric
![Busque la plantilla de clúster de Service Fabric en hello portal de Azure.][SearchforServiceFabricClusterTemplate]

1. Inicie sesión en toohello [portal de Azure][azure-portal].
2. Haga clic en **New** tooadd una nueva plantilla de recursos. Busque la plantilla de servicio de Cluster Server tejido Hola Hola **Marketplace** en **todo**.
3. Seleccione **clúster de Service Fabric** de lista de Hola.
4. Navegue toohello **clúster de Service Fabric** hoja, haga clic en **crear**,
5. Hola **clúster crear Service Fabric** hoja tiene Hola cuatro pasos.

#### <a name="1-basics"></a>1. Aspectos básicos
![Captura de pantalla de la creación de un grupo de recursos.][CreateRG]

En la hoja de conceptos básicos de hello necesita detalles básicos de tooprovide hello para el clúster.

1. Escriba el nombre de hello del clúster.
2. Escriba un **nombre de usuario** y **contraseña** para escritorio remoto para hello las máquinas virtuales.
3. Realizar seguro hello tooselect **suscripción** desea su toobe de clúster implementado, especialmente si tiene varias suscripciones.
4. Cree un **nuevo grupo de recursos**. Es mejor toogive lo Hola mismo nombre que el clúster de hello, ya que ayuda a buscar más adelante, especialmente cuando se está tratando de toomake cambios tooyour implementación o eliminar el clúster.
   
   > [!NOTE]
   > Aunque puede decidir toouse un grupo de recursos existente, es un toocreate recomendable un nuevo grupo de recursos. Esto hace fácil toodelete clústeres que no es necesario.
   > 
   > 
5. Seleccione hello **región** en que desea que el clúster de hello toocreate. Debe usar hello misma región que la clave del almacén está en.

#### <a name="2-cluster-configuration"></a>2. Configuración del clúster
![Creación de un tipo de nodo][CreateNodeType]

Configure los nodos del clúster. Tipos de nodos definen tamaños de máquinas virtuales de hello, Hola número de máquinas virtuales y sus propiedades. El clúster puede tener más de un tipo de nodo pero el tipo de nodo principal de hello (Hola la primera de ellas que define en el portal de hello) debe tener al menos cinco VM, puesto que éste es un tipo de nodo de Hola donde se colocan los servicios del sistema de Service Fabric. No configure **Propiedades de ubicación** porque el sistema agrega automáticamente una propiedad de ubicación predeterminada de "NodeTypeName".

> [!NOTE]
> Un escenario común para varios tipos de nodos es una aplicación que contiene un servicio front-end y un servicio back-end. Desea que el servicio front-end de hello tooput en máquinas virtuales más pequeñas (tamaños de máquina virtual como D2) con puertos abiertos toohello Internet, pero desea tooput servicio de back-end de hello en máquinas virtuales más grandes (con tamaños de máquina virtual como D4, D6, D15 etc.) con ningún puerto de conexión a Internet abierto.
> 
> 

1. Elija un nombre para el tipo de nodo (1 too12 de caracteres que contiene solo letras y números).
2. Hola mínimo **tamaño** de VM para el nodo principal de Hola Hola depende de tipo **durabilidad** nivel que elija para el clúster de Hola. valor predeterminado de Hello para el nivel de durabilidad hello es Bronce. Para obtener más información sobre la durabilidad, consulte [cómo toochoose Hola Service Fabric clúster confiabilidad y durabilidad][service-fabric-cluster-capacity].
3. Seleccione el tamaño de la máquina virtual de Hola y nivel de precios. Las máquinas virtuales de la serie D tienen unidades SSD y son muy recomendables para aplicaciones con estado. No utilice cualquier SKU de máquina virtual que tenga núcleos parciales o menos de 7 GB de capacidad de disco disponible. 
4. Hola mínimo **número** de VM para el nodo principal de Hola Hola depende de tipo **confiabilidad** nivel que elija. valor predeterminado de Hello para el nivel de confiabilidad de hello es plata. Para obtener más información sobre la confiabilidad, consulte [cómo toochoose Hola Service Fabric clúster confiabilidad y durabilidad][service-fabric-cluster-capacity].
5. Elegir Hola número de máquinas virtuales para el tipo de nodo de Hola. Puede escalar hacia arriba o hacia abajo el número de Hola de máquinas virtuales en un tipo de nodo más adelante, pero en el tipo de nodo principal de hello, Hola mínimo está controlada por el nivel de confiabilidad de Hola que ha elegido. Otros tipos de nodo pueden tener un mínimo de 1 máquina virtual.
6. Configure los puntos de conexión personalizados. Este campo le permite tooenter una lista separada por comas de puertos que desea que tooexpose a través de hello equilibrador de carga Azure toohello público de Internet para las aplicaciones. Por ejemplo, si tiene previsto toodeploy un clúster de tooyour de aplicación web, escriba "80" aquí tooallow tráfico en el puerto 80 en el clúster. Para obtener más información sobre los puntos de conexión, consulte la [comunicación con las aplicaciones][service-fabric-connect-and-communicate-with-services].
7. Configure los **diagnósticos**de clúster. De forma predeterminada, se habilitan los diagnósticos en su tooassist de clúster con la solución de problemas. Si desea cambia de diagnóstico toodisable hello **estado** alternar demasiado**desactivar**. **No** se recomienda desactivar los diagnósticos.
8. Seleccione Hola tejido actualizar el modo que desea establecer el clúster. Seleccione **automática**, si desea Hola sistema tooautomatically recogerá Hola última versión disponible e intente tooupgrade su tooit de clúster. Establecer el modo de hello demasiado**Manual**, si desea que toochoose una versión compatible.

> [!NOTE]
> Se admiten solo los clústeres que ejecutan versiones compatibles de Service Fabric. Si selecciona hello **Manual** modo, va a realizar en hello responsabilidad tooupgrade su tooa admitida la versión de clúster. Para obtener más detalles sobre el modo de actualización de Fabric de Hola Hola, consulte [documento de servicio de fabric clúster de actualización.][service-fabric-cluster-upgrade]
> 
> 

#### <a name="3-security"></a>3. Seguridad
![Captura de pantalla de las configuraciones de seguridad del Portal de Azure.][SecurityConfigs]

Hola último paso es clúster tooprovide certificado información toosecure Hola usando Hola el almacén de claves y el certificado información creado anteriormente.

* Rellenar los campos de certificado principal de hello con salida de hello obtenido de cargar hello **certificado de clúster** tooKey almacén con Hola `Invoke-AddCertToKeyVault` comando de PowerShell.

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* Comprobar hello **configurar opciones avanzadas** cuadro tooenter los certificados de cliente para **cliente de administración** y **cliente de solo lectura**. En estos campos, escriba huella digital de Hola de su certificado de cliente de administración y la huella digital de Hola de su certificado de cliente de usuario de solo lectura, si procede. Cuando los administradores intentan tooconnect toohello clúster, se les concede acceso solo si tienen un certificado con una huella digital que coincide con los valores de huella digital de hello introducido aquí.  

#### <a name="4-summary"></a>4. Resumen
![Captura de pantalla de panel de inicio de hello mostrar "Clúster de tejido de servicio de implementación". ][Notifications]

creación de clústeres de hello toocomplete, haga clic en **resumen** Hola a configuraciones de hello toosee que ha proporcionado o descargar plantilla de administrador de recursos de Azure que usan toodeploy el clúster. Después de haber proporcionado parámetros obligatorios hello, Hola **Aceptar** botón se convierte en verde y puede iniciar el proceso de creación de clúster de hello haciendo clic en él.

Puede ver el progreso de la creación de hello en las notificaciones de Hola. (Haga clic en el icono de campana"hello" cerca de la barra de estado de hello en la parte superior de hello derecha de la pantalla). Si hace clic en **Pin tooStartboard** al crear el clúster de hello, verá **implementación de clúster de Service Fabric** anclado toohello **iniciar** panel.

### <a name="view-your-cluster-status"></a>Visualización del estado del clúster
![Captura de pantalla de detalles del clúster en el panel de Hola.][ClusterDashboard]

Una vez creado el clúster, puede inspeccionar el clúster en el portal de hello:

1. Vaya demasiado**examinar** y haga clic en **clústeres del servicio de Fabric**.
2. Busque su clúster y haga clic en él.
3. Ahora puede ver detalles de hello del clúster en panel de hello, incluidos extremo público del clúster de Hola y un explorador de Fabric tooService de vínculo.

Hola **nodo Monitor** sección en la hoja de panel del clúster de hello indica el número de Hola de máquinas virtuales que están activados y no funciona correctamente. Puede encontrar más detalles sobre el estado del clúster de hello en [introducción de modelo de mantenimiento de Service Fabric][service-fabric-health-introduction].

> [!NOTE]
> Clústeres de Service Fabric requieren un cierto número de nodos toobe la disponibilidad de toomaintain siempre y conservan el estado - tooas que se hace referencia "mantenga el quórum". Por tanto, normalmente no es seguro tooshut hacia abajo de todas las máquinas de clúster de Hola a menos que primero ha llevado a cabo una [una copia de seguridad completa del estado del][service-fabric-reliable-services-backup-restore].
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a>Instancia de conjunto de escala de máquinas virtuales de tooa o un nodo de clúster de conexión remota
Cada uno de hello NodeTypes especifica en los resultados de clúster en un conjunto de escala de máquinas virtuales para la obtención de instalación. Vea [remoto conectar la instancia de conjunto de escala de máquinas virtuales de tooa] [ remote-connect-to-a-vm-scale-set] para obtener más información.

## <a name="next-steps"></a>Pasos siguientes
En este punto, tiene un clúster seguro mediante certificados para la autenticación de administración. Después, [conectar clúster tooyour](service-fabric-connect-to-secure-cluster.md) y obtenga información acerca de cómo demasiado[administrar secretos de aplicación](service-fabric-application-secret-management.md).  Más información sobre las [opciones de soporte técnico de Service Fabric](service-fabric-support.md)

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
