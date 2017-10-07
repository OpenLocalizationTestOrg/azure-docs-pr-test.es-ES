---
title: aaaManaging secretos en aplicaciones de Service Fabric | Documentos de Microsoft
description: "Este artículo describe cómo toosecure secreto valores en una aplicación de Service Fabric."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 94a67e45-7094-4fbd-9c88-51f4fc3c523a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: b8cafcb681d95aaa1b8e9a1afaac78ba5b7f58b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="managing-secrets-in-service-fabric-applications"></a>Administración de secretos en aplicaciones de Service Fabric
Esta guía le guiará por los pasos de saludo de la administración de secretos en una aplicación de Service Fabric. Los secretos pueden ser cualquier información confidencial, como cadenas de conexión de almacenamiento, contraseñas u otros valores que no se deben administrar en texto sin formato.

Esta guía usa secretos y las claves de toomanage del almacén de claves de Azure. Sin embargo, *con* secretos en una aplicación es el clúster implementado tooa toobe de nube independiente de la plataforma tooallow aplicaciones hospedadas desde cualquier lugar. 

## <a name="overview"></a>Información general
Hola valores de configuración del servicio de toomanage de manera recomendada es a través de [paquetes de configuración de servicio][config-package]. Los paquetes de configuración se actualizan mediante actualizaciones acumulativas administradas con validación de estado y reversión automática. Ésta es configuración de tooglobal preferido, ya que reduce las posibilidades de Hola de una interrupción del servicio global. Los secretos cifrados no son ninguna excepción. Service Fabric presenta características integradas para cifrar y descifrar valores en un archivo Settings.xml de paquete de configuración mediante cifrado de certificados.

Hello siguiente diagrama muestra hello flujo básico para administrar el secreto en una aplicación de Service Fabric:

![información general de administración de secretos][overview]

Hay cuatro pasos principales en este flujo:

1. Obtener un certificado de cifrado de datos.
2. Instalar certificado de hello en el clúster.
3. Cifrar valores secretos al implementar una aplicación con el certificado de Hola y se insertan en el archivo de configuración de un servicio Settings.xml.
4. Valores de lectura cifrado fuera Settings.xml mediante el descifrado con Hola mismo certificado de cifrado. 

[Almacén de claves de Azure] [ key-vault-get-started] se utiliza aquí como una ubicación de almacenamiento seguro para los certificados y como una manera tooget certificados instalados en los clústeres de Service Fabric en Azure. Si no va a implementar tooAzure, no es necesario toomanage secretos de almacén de claves de toouse en aplicaciones de Service Fabric.

## <a name="data-encipherment-certificate"></a>Certificado de cifrado de datos
Un certificado de cifrado de datos se utiliza estrictamente para el cifrado y el descifrado de los valores de configuración en un archivo Settings.xml del servicio y no se usa para la autenticación o la forma del texto cifrado. certificado de Hello debe cumplir Hola según los requisitos:

* certificado de Hello debe contener una clave privada.
* certificado de Hello debe crearse para el intercambio de claves, exportable tooa archivo de intercambio de información Personal (.pfx).
* uso de claves de certificado de Hello debe incluir el cifrado de datos (10) y no debe incluir autenticación de servidor o la autenticación de cliente. 
  
  Por ejemplo, al crear un certificado autofirmado mediante PowerShell, Hola `KeyUsage` marca se debe establecer demasiado`DataEncipherment`:
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a>Instalar certificado de hello en el clúster
Este certificado debe instalarse en cada nodo de clúster de Hola. Se utilizará en tiempo de ejecución toodecrypt valores almacenados en Settings.xml de un servicio. Vea [cómo toocreate un clúster mediante el Administrador de recursos de Azure] [ service-fabric-cluster-creation-via-arm] para obtener instrucciones de instalación. 

## <a name="encrypt-application-secrets"></a>Cifrado de los secretos de aplicación
Hola SDK del servicio de Fabric tiene funciones integradas de cifrado y descifrado de secreto. Los valores de secreto se pueden cifrar en el momento de la compilación y luego descifrarse y leerse mediante programación en el código de servicio. 

Hola siguiente comando de PowerShell es tooencrypt usa un secreto. Este comando sólo cifra el valor de hello; lo hace **no** firmar texto de cifrado de Hola. Debe usar hello mismo certificado de cifrado que se instala en el texto de cifrado de tooproduce de clúster para los valores de secreto:

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

Hello cadena base64 resultante contiene texto de cifrado secretas Hola así como información sobre certificados Hola que estaba tooencrypt usado se.  Hello cadena codificada en base 64 se pueden insertar en un parámetro en el archivo de configuración de su servicio Settings.xml con hello `IsEncrypted` atributo establecido demasiado`true`:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a>Inserción de secretos de aplicación en instancias de aplicación
Idealmente, los entornos de implementación toodifferent deberían ser como automatizados como sea posible. Esto puede realizarse mediante la realiza el cifrado de secretos en un entorno de compilación y secretos cifrado de hello como parámetros cuando se crean instancias de la aplicación.

#### <a name="use-overridable-parameters-in-settingsxml"></a>Uso de parámetros reemplazables en Settings.xml
archivo de configuración de Hello Settings.xml permite parámetros reemplazables que se pueden proporcionar en tiempo de creación de la aplicación. Hola de uso `MustOverride` atributo en lugar de proporcionar un valor para un parámetro:

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

valores de toooverride en Settings.xml, declarar un parámetro de invalidación para el servicio de hello en ApplicationManifest.xml:

```xml
<ApplicationManifest ... >
  <Parameters>
    <Parameter Name="MySecret" DefaultValue="" />
  </Parameters>
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="Stateful1Pkg" ServiceManifestVersion="1.0.0" />
    <ConfigOverrides>
      <ConfigOverride Name="Config">
        <Settings>
          <Section Name="MySettings">
            <Parameter Name="MySecret" Value="[MySecret]" IsEncrypted="true" />
          </Section>
        </Settings>
      </ConfigOverride>
    </ConfigOverrides>
  </ServiceManifestImport>
 ```

Ahora se puede especificar el valor de Hola como un *parámetro de la aplicación* al crear una instancia de la aplicación hello. La creación de una instancia de aplicación se puede generar mediante un script con PowerShell, o escribirse en C#, para facilitar la integración en un proceso de compilación.

El uso de PowerShell, parámetro hello es toohello proporcionado `New-ServiceFabricApplication` comando como un [tabla hash](https://technet.microsoft.com/library/ee692803.aspx):

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

Con C#, los parámetros de aplicación se especifican en `ApplicationDescription` como `NameValueCollection`:

```csharp
FabricClient fabricClient = new FabricClient();

NameValueCollection applicationParameters = new NameValueCollection();
applicationParameters["MySecret"] = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=";

ApplicationDescription applicationDescription = new ApplicationDescription(
    applicationName: new Uri("fabric:/MyApp"),
    applicationTypeName: "MyAppType",
    applicationTypeVersion: "1.0.0",
    applicationParameters: applicationParameters)
);

await fabricClient.ApplicationManager.CreateApplicationAsync(applicationDescription);
```

## <a name="decrypt-secrets-from-service-code"></a>Descifrado de secretos desde el código de servicio
Servicios de Service Fabric se ejecutan en el servicio de red de forma predeterminada en Windows y toocertificates de acceso no ha instalado en el nodo de hello sin tener que alguna configuración adicional.

Cuando se utiliza un certificado de cifrado de datos, deberá toomake servicio de red o cualquier servicio de Hola de cuenta de usuario se ejecuta bajo tenga la clave privada del certificado de acceso toohello. Service Fabric controlará conceder acceso para el servicio automáticamente si se configura toodo así. Esta configuración se puede realizar en ApplicationManifest.xml definiendo usuarios y directivas de seguridad para los certificados. En el siguiente ejemplo de Hola, Hola cuenta de servicio de red tiene acceso de lectura tooa certificado definido por su huella digital:

```xml
<ApplicationManifest … >
    <Principals>
        <Users>
            <User Name="Service1" AccountType="NetworkService" />
        </Users>
    </Principals>
  <Policies>
    <SecurityAccessPolicies>
      <SecurityAccessPolicy GrantRights=”Read” PrincipalRef="Service1" ResourceRef="MyCert" ResourceType="Certificate"/>
    </SecurityAccessPolicies>
  </Policies>
  <Certificates>
    <SecretsCertificate Name="MyCert" X509FindType="FindByThumbprint" X509FindValue="[YourCertThumbrint]"/>
  </Certificates>
</ApplicationManifest>
```

> [!NOTE]
> Cuando se copia una huella digital del certificado del certificado de hello almacén complemento en Windows, un carácter invisible se coloca al principio de Hola de cadena de la huella digital de Hola. Este carácter invisible puede producir un error al tratar de toolocate un certificado con huella digital, por lo que debe toodelete seguro este carácter adicional.
> 
> 

### <a name="use-application-secrets-in-service-code"></a>Uso de secretos de aplicación en el código de servicio
Hola API para tener acceso a los valores de configuración de Settings.xml en un paquete de configuración permite descifrar fácil de valores con hello `IsEncrypted` atributo establecido demasiado`true`. Puesto que el texto hello cifra contiene información sobre certificados de hello usado para el cifrado, no necesita toomanually buscar Hola certificado. solo es necesario toobe instalado en el nodo de Hola que se ejecuta el servicio de hello en Hello certificado. Basta con llamar a hello `DecryptValue()` valor secreto original Hola de tooretrieve método:

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a>Pasos siguientes
Más información sobre la [ejecución de aplicaciones con distintos permisos de seguridad](service-fabric-application-runas-security.md)

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
