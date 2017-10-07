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
# <a name="managing-secrets-in-service-fabric-applications"></a><span data-ttu-id="78de3-103">Administración de secretos en aplicaciones de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="78de3-103">Managing secrets in Service Fabric applications</span></span>
<span data-ttu-id="78de3-104">Esta guía le guiará por los pasos de saludo de la administración de secretos en una aplicación de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="78de3-104">This guide walks you through hello steps of managing secrets in a Service Fabric application.</span></span> <span data-ttu-id="78de3-105">Los secretos pueden ser cualquier información confidencial, como cadenas de conexión de almacenamiento, contraseñas u otros valores que no se deben administrar en texto sin formato.</span><span class="sxs-lookup"><span data-stu-id="78de3-105">Secrets can be any sensitive information, such as storage connection strings, passwords, or other values that should not be handled in plain text.</span></span>

<span data-ttu-id="78de3-106">Esta guía usa secretos y las claves de toomanage del almacén de claves de Azure.</span><span class="sxs-lookup"><span data-stu-id="78de3-106">This guide uses Azure Key Vault toomanage keys and secrets.</span></span> <span data-ttu-id="78de3-107">Sin embargo, *con* secretos en una aplicación es el clúster implementado tooa toobe de nube independiente de la plataforma tooallow aplicaciones hospedadas desde cualquier lugar.</span><span class="sxs-lookup"><span data-stu-id="78de3-107">However, *using* secrets in an application is cloud platform-agnostic tooallow applications toobe deployed tooa cluster hosted anywhere.</span></span> 

## <a name="overview"></a><span data-ttu-id="78de3-108">Información general</span><span class="sxs-lookup"><span data-stu-id="78de3-108">Overview</span></span>
<span data-ttu-id="78de3-109">Hola valores de configuración del servicio de toomanage de manera recomendada es a través de [paquetes de configuración de servicio][config-package].</span><span class="sxs-lookup"><span data-stu-id="78de3-109">hello recommended way toomanage service configuration settings is through [service configuration packages][config-package].</span></span> <span data-ttu-id="78de3-110">Los paquetes de configuración se actualizan mediante actualizaciones acumulativas administradas con validación de estado y reversión automática.</span><span class="sxs-lookup"><span data-stu-id="78de3-110">Configuration packages are versioned and updatable through managed rolling upgrades with health-validation and auto rollback.</span></span> <span data-ttu-id="78de3-111">Ésta es configuración de tooglobal preferido, ya que reduce las posibilidades de Hola de una interrupción del servicio global.</span><span class="sxs-lookup"><span data-stu-id="78de3-111">This is preferred tooglobal configuration as it reduces hello chances of a global service outage.</span></span> <span data-ttu-id="78de3-112">Los secretos cifrados no son ninguna excepción.</span><span class="sxs-lookup"><span data-stu-id="78de3-112">Encrypted secrets are no exception.</span></span> <span data-ttu-id="78de3-113">Service Fabric presenta características integradas para cifrar y descifrar valores en un archivo Settings.xml de paquete de configuración mediante cifrado de certificados.</span><span class="sxs-lookup"><span data-stu-id="78de3-113">Service Fabric has built-in features for encrypting and decrypting values in a configuration package Settings.xml file using certificate encryption.</span></span>

<span data-ttu-id="78de3-114">Hello siguiente diagrama muestra hello flujo básico para administrar el secreto en una aplicación de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="78de3-114">hello following diagram illustrates hello basic flow for secret management in a Service Fabric application:</span></span>

![información general de administración de secretos][overview]

<span data-ttu-id="78de3-116">Hay cuatro pasos principales en este flujo:</span><span class="sxs-lookup"><span data-stu-id="78de3-116">There are four main steps in this flow:</span></span>

1. <span data-ttu-id="78de3-117">Obtener un certificado de cifrado de datos.</span><span class="sxs-lookup"><span data-stu-id="78de3-117">Obtain a data encipherment certificate.</span></span>
2. <span data-ttu-id="78de3-118">Instalar certificado de hello en el clúster.</span><span class="sxs-lookup"><span data-stu-id="78de3-118">Install hello certificate in your cluster.</span></span>
3. <span data-ttu-id="78de3-119">Cifrar valores secretos al implementar una aplicación con el certificado de Hola y se insertan en el archivo de configuración de un servicio Settings.xml.</span><span class="sxs-lookup"><span data-stu-id="78de3-119">Encrypt secret values when deploying an application with hello certificate and inject them into a service's Settings.xml configuration file.</span></span>
4. <span data-ttu-id="78de3-120">Valores de lectura cifrado fuera Settings.xml mediante el descifrado con Hola mismo certificado de cifrado.</span><span class="sxs-lookup"><span data-stu-id="78de3-120">Read encrypted values out of Settings.xml by decrypting with hello same encipherment certificate.</span></span> 

<span data-ttu-id="78de3-121">[Almacén de claves de Azure] [ key-vault-get-started] se utiliza aquí como una ubicación de almacenamiento seguro para los certificados y como una manera tooget certificados instalados en los clústeres de Service Fabric en Azure.</span><span class="sxs-lookup"><span data-stu-id="78de3-121">[Azure Key Vault][key-vault-get-started] is used here as a safe storage location for certificates and as a way tooget certificates installed on Service Fabric clusters in Azure.</span></span> <span data-ttu-id="78de3-122">Si no va a implementar tooAzure, no es necesario toomanage secretos de almacén de claves de toouse en aplicaciones de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="78de3-122">If you are not deploying tooAzure, you do not need toouse Key Vault toomanage secrets in Service Fabric applications.</span></span>

## <a name="data-encipherment-certificate"></a><span data-ttu-id="78de3-123">Certificado de cifrado de datos</span><span class="sxs-lookup"><span data-stu-id="78de3-123">Data encipherment certificate</span></span>
<span data-ttu-id="78de3-124">Un certificado de cifrado de datos se utiliza estrictamente para el cifrado y el descifrado de los valores de configuración en un archivo Settings.xml del servicio y no se usa para la autenticación o la forma del texto cifrado.</span><span class="sxs-lookup"><span data-stu-id="78de3-124">A data encipherment certificate is used strictly for encryption and decryption of configuration values in a service's Settings.xml and is not used for authentication or signing of cipher text.</span></span> <span data-ttu-id="78de3-125">certificado de Hello debe cumplir Hola según los requisitos:</span><span class="sxs-lookup"><span data-stu-id="78de3-125">hello certificate must meet hello following requirements:</span></span>

* <span data-ttu-id="78de3-126">certificado de Hello debe contener una clave privada.</span><span class="sxs-lookup"><span data-stu-id="78de3-126">hello certificate must contain a private key.</span></span>
* <span data-ttu-id="78de3-127">certificado de Hello debe crearse para el intercambio de claves, exportable tooa archivo de intercambio de información Personal (.pfx).</span><span class="sxs-lookup"><span data-stu-id="78de3-127">hello certificate must be created for key exchange, exportable tooa Personal Information Exchange (.pfx) file.</span></span>
* <span data-ttu-id="78de3-128">uso de claves de certificado de Hello debe incluir el cifrado de datos (10) y no debe incluir autenticación de servidor o la autenticación de cliente.</span><span class="sxs-lookup"><span data-stu-id="78de3-128">hello certificate key usage must include Data Encipherment (10), and should not include Server Authentication or Client Authentication.</span></span> 
  
  <span data-ttu-id="78de3-129">Por ejemplo, al crear un certificado autofirmado mediante PowerShell, Hola `KeyUsage` marca se debe establecer demasiado`DataEncipherment`:</span><span class="sxs-lookup"><span data-stu-id="78de3-129">For example, when creating a self-signed certificate using PowerShell, hello `KeyUsage` flag must be set too`DataEncipherment`:</span></span>
  
  ```powershell
  New-SelfSignedCertificate -Type DocumentEncryptionCert -KeyUsage DataEncipherment -Subject mydataenciphermentcert -Provider 'Microsoft Enhanced Cryptographic Provider v1.0'
  ```

## <a name="install-hello-certificate-in-your-cluster"></a><span data-ttu-id="78de3-130">Instalar certificado de hello en el clúster</span><span class="sxs-lookup"><span data-stu-id="78de3-130">Install hello certificate in your cluster</span></span>
<span data-ttu-id="78de3-131">Este certificado debe instalarse en cada nodo de clúster de Hola.</span><span class="sxs-lookup"><span data-stu-id="78de3-131">This certificate must be installed on each node in hello cluster.</span></span> <span data-ttu-id="78de3-132">Se utilizará en tiempo de ejecución toodecrypt valores almacenados en Settings.xml de un servicio.</span><span class="sxs-lookup"><span data-stu-id="78de3-132">It will be used at runtime toodecrypt values stored in a service's Settings.xml.</span></span> <span data-ttu-id="78de3-133">Vea [cómo toocreate un clúster mediante el Administrador de recursos de Azure] [ service-fabric-cluster-creation-via-arm] para obtener instrucciones de instalación.</span><span class="sxs-lookup"><span data-stu-id="78de3-133">See [how toocreate a cluster using Azure Resource Manager][service-fabric-cluster-creation-via-arm] for setup instructions.</span></span> 

## <a name="encrypt-application-secrets"></a><span data-ttu-id="78de3-134">Cifrado de los secretos de aplicación</span><span class="sxs-lookup"><span data-stu-id="78de3-134">Encrypt application secrets</span></span>
<span data-ttu-id="78de3-135">Hola SDK del servicio de Fabric tiene funciones integradas de cifrado y descifrado de secreto.</span><span class="sxs-lookup"><span data-stu-id="78de3-135">hello Service Fabric SDK has built-in secret encryption and decryption functions.</span></span> <span data-ttu-id="78de3-136">Los valores de secreto se pueden cifrar en el momento de la compilación y luego descifrarse y leerse mediante programación en el código de servicio.</span><span class="sxs-lookup"><span data-stu-id="78de3-136">Secret values can be encrypted at built-time and then decrypted and read programmatically in service code.</span></span> 

<span data-ttu-id="78de3-137">Hola siguiente comando de PowerShell es tooencrypt usa un secreto.</span><span class="sxs-lookup"><span data-stu-id="78de3-137">hello following PowerShell command is used tooencrypt a secret.</span></span> <span data-ttu-id="78de3-138">Este comando sólo cifra el valor de hello; lo hace **no** firmar texto de cifrado de Hola.</span><span class="sxs-lookup"><span data-stu-id="78de3-138">This command only encrypts hello value; it does **not** sign hello cipher text.</span></span> <span data-ttu-id="78de3-139">Debe usar hello mismo certificado de cifrado que se instala en el texto de cifrado de tooproduce de clúster para los valores de secreto:</span><span class="sxs-lookup"><span data-stu-id="78de3-139">You must use hello same encipherment certificate that is installed in your cluster tooproduce ciphertext for secret values:</span></span>

```powershell
Invoke-ServiceFabricEncryptText -CertStore -CertThumbprint "<thumbprint>" -Text "mysecret" -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="78de3-140">Hello cadena base64 resultante contiene texto de cifrado secretas Hola así como información sobre certificados Hola que estaba tooencrypt usado se.</span><span class="sxs-lookup"><span data-stu-id="78de3-140">hello resulting base-64 string contains both hello secret ciphertext as well as information about hello certificate that was used tooencrypt it.</span></span>  <span data-ttu-id="78de3-141">Hello cadena codificada en base 64 se pueden insertar en un parámetro en el archivo de configuración de su servicio Settings.xml con hello `IsEncrypted` atributo establecido demasiado`true`:</span><span class="sxs-lookup"><span data-stu-id="78de3-141">hello base-64 encoded string can be inserted into a parameter in your service's Settings.xml configuration file with hello `IsEncrypted` attribute set too`true`:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM=" />
  </Section>
</Settings>
```

### <a name="inject-application-secrets-into-application-instances"></a><span data-ttu-id="78de3-142">Inserción de secretos de aplicación en instancias de aplicación</span><span class="sxs-lookup"><span data-stu-id="78de3-142">Inject application secrets into application instances</span></span>
<span data-ttu-id="78de3-143">Idealmente, los entornos de implementación toodifferent deberían ser como automatizados como sea posible.</span><span class="sxs-lookup"><span data-stu-id="78de3-143">Ideally, deployment toodifferent environments should be as automated as possible.</span></span> <span data-ttu-id="78de3-144">Esto puede realizarse mediante la realiza el cifrado de secretos en un entorno de compilación y secretos cifrado de hello como parámetros cuando se crean instancias de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="78de3-144">This can be accomplished by performing secret encryption in a build environment and providing hello encrypted secrets as parameters when creating application instances.</span></span>

#### <a name="use-overridable-parameters-in-settingsxml"></a><span data-ttu-id="78de3-145">Uso de parámetros reemplazables en Settings.xml</span><span class="sxs-lookup"><span data-stu-id="78de3-145">Use overridable parameters in Settings.xml</span></span>
<span data-ttu-id="78de3-146">archivo de configuración de Hello Settings.xml permite parámetros reemplazables que se pueden proporcionar en tiempo de creación de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="78de3-146">hello Settings.xml configuration file allows overridable parameters that can be provided at application creation time.</span></span> <span data-ttu-id="78de3-147">Hola de uso `MustOverride` atributo en lugar de proporcionar un valor para un parámetro:</span><span class="sxs-lookup"><span data-stu-id="78de3-147">Use hello `MustOverride` attribute instead of providing a value for a parameter:</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
  <Section Name="MySettings">
    <Parameter Name="MySecret" IsEncrypted="true" Value="" MustOverride="true" />
  </Section>
</Settings>
```

<span data-ttu-id="78de3-148">valores de toooverride en Settings.xml, declarar un parámetro de invalidación para el servicio de hello en ApplicationManifest.xml:</span><span class="sxs-lookup"><span data-stu-id="78de3-148">toooverride values in Settings.xml, declare an override parameter for hello service in ApplicationManifest.xml:</span></span>

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

<span data-ttu-id="78de3-149">Ahora se puede especificar el valor de Hola como un *parámetro de la aplicación* al crear una instancia de la aplicación hello.</span><span class="sxs-lookup"><span data-stu-id="78de3-149">Now hello value can be specified as an *application parameter* when creating an instance of hello application.</span></span> <span data-ttu-id="78de3-150">La creación de una instancia de aplicación se puede generar mediante un script con PowerShell, o escribirse en C#, para facilitar la integración en un proceso de compilación.</span><span class="sxs-lookup"><span data-stu-id="78de3-150">Creating an application instance can be scripted using PowerShell, or written in C#, for easy integration in a build process.</span></span>

<span data-ttu-id="78de3-151">El uso de PowerShell, parámetro hello es toohello proporcionado `New-ServiceFabricApplication` comando como un [tabla hash](https://technet.microsoft.com/library/ee692803.aspx):</span><span class="sxs-lookup"><span data-stu-id="78de3-151">Using PowerShell, hello parameter is supplied toohello `New-ServiceFabricApplication` command as a [hash table](https://technet.microsoft.com/library/ee692803.aspx):</span></span>

```powershell
PS C:\Users\vturecek> New-ServiceFabricApplication -ApplicationName fabric:/MyApp -ApplicationTypeName MyAppType -ApplicationTypeVersion 1.0.0 -ApplicationParameter @{"MySecret" = "I6jCCAeYCAxgFhBXABFxzAt ... gNBRyeWFXl2VydmjZNwJIM="}
```

<span data-ttu-id="78de3-152">Con C#, los parámetros de aplicación se especifican en `ApplicationDescription` como `NameValueCollection`:</span><span class="sxs-lookup"><span data-stu-id="78de3-152">Using C#, application parameters are specified in an `ApplicationDescription` as a `NameValueCollection`:</span></span>

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

## <a name="decrypt-secrets-from-service-code"></a><span data-ttu-id="78de3-153">Descifrado de secretos desde el código de servicio</span><span class="sxs-lookup"><span data-stu-id="78de3-153">Decrypt secrets from service code</span></span>
<span data-ttu-id="78de3-154">Servicios de Service Fabric se ejecutan en el servicio de red de forma predeterminada en Windows y toocertificates de acceso no ha instalado en el nodo de hello sin tener que alguna configuración adicional.</span><span class="sxs-lookup"><span data-stu-id="78de3-154">Services in Service Fabric run under NETWORK SERVICE by default on Windows and don't have access toocertificates installed on hello node without some extra setup.</span></span>

<span data-ttu-id="78de3-155">Cuando se utiliza un certificado de cifrado de datos, deberá toomake servicio de red o cualquier servicio de Hola de cuenta de usuario se ejecuta bajo tenga la clave privada del certificado de acceso toohello.</span><span class="sxs-lookup"><span data-stu-id="78de3-155">When using a data encipherment certificate, you need toomake sure NETWORK SERVICE or whatever user account hello service is running under has access toohello certificate's private key.</span></span> <span data-ttu-id="78de3-156">Service Fabric controlará conceder acceso para el servicio automáticamente si se configura toodo así.</span><span class="sxs-lookup"><span data-stu-id="78de3-156">Service Fabric will handle granting access for your service automatically if you configure it toodo so.</span></span> <span data-ttu-id="78de3-157">Esta configuración se puede realizar en ApplicationManifest.xml definiendo usuarios y directivas de seguridad para los certificados.</span><span class="sxs-lookup"><span data-stu-id="78de3-157">This configuration can be done in ApplicationManifest.xml by defining users and security policies for certificates.</span></span> <span data-ttu-id="78de3-158">En el siguiente ejemplo de Hola, Hola cuenta de servicio de red tiene acceso de lectura tooa certificado definido por su huella digital:</span><span class="sxs-lookup"><span data-stu-id="78de3-158">In hello following example, hello NETWORK SERVICE account is given read access tooa certificate defined by its thumbprint:</span></span>

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
> <span data-ttu-id="78de3-159">Cuando se copia una huella digital del certificado del certificado de hello almacén complemento en Windows, un carácter invisible se coloca al principio de Hola de cadena de la huella digital de Hola.</span><span class="sxs-lookup"><span data-stu-id="78de3-159">When copying a certificate thumbprint from hello certificate store snap-in on Windows, an invisible character is placed at hello beginning of hello thumbprint string.</span></span> <span data-ttu-id="78de3-160">Este carácter invisible puede producir un error al tratar de toolocate un certificado con huella digital, por lo que debe toodelete seguro este carácter adicional.</span><span class="sxs-lookup"><span data-stu-id="78de3-160">This invisible character can cause an error when trying toolocate a certificate by thumbprint, so be sure toodelete this extra character.</span></span>
> 
> 

### <a name="use-application-secrets-in-service-code"></a><span data-ttu-id="78de3-161">Uso de secretos de aplicación en el código de servicio</span><span class="sxs-lookup"><span data-stu-id="78de3-161">Use application secrets in service code</span></span>
<span data-ttu-id="78de3-162">Hola API para tener acceso a los valores de configuración de Settings.xml en un paquete de configuración permite descifrar fácil de valores con hello `IsEncrypted` atributo establecido demasiado`true`.</span><span class="sxs-lookup"><span data-stu-id="78de3-162">hello API for accessing configuration values from Settings.xml in a configuration package allows for easy decrypting of values that have hello `IsEncrypted` attribute set too`true`.</span></span> <span data-ttu-id="78de3-163">Puesto que el texto hello cifra contiene información sobre certificados de hello usado para el cifrado, no necesita toomanually buscar Hola certificado.</span><span class="sxs-lookup"><span data-stu-id="78de3-163">Since hello encrypted text contains information about hello certificate used for encryption, you do not need toomanually find hello certificate.</span></span> <span data-ttu-id="78de3-164">solo es necesario toobe instalado en el nodo de Hola que se ejecuta el servicio de hello en Hello certificado.</span><span class="sxs-lookup"><span data-stu-id="78de3-164">hello certificate just needs toobe installed on hello node that hello service is running on.</span></span> <span data-ttu-id="78de3-165">Basta con llamar a hello `DecryptValue()` valor secreto original Hola de tooretrieve método:</span><span class="sxs-lookup"><span data-stu-id="78de3-165">Simply call hello `DecryptValue()` method tooretrieve hello original secret value:</span></span>

```csharp
ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");
SecureString mySecretValue = configPackage.Settings.Sections["MySettings"].Parameters["MySecret"].DecryptValue()
```

## <a name="next-steps"></a><span data-ttu-id="78de3-166">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="78de3-166">Next Steps</span></span>
<span data-ttu-id="78de3-167">Más información sobre la [ejecución de aplicaciones con distintos permisos de seguridad](service-fabric-application-runas-security.md)</span><span class="sxs-lookup"><span data-stu-id="78de3-167">Learn more about [running applications with different security permissions](service-fabric-application-runas-security.md)</span></span>

<!-- Links -->
[key-vault-get-started]:../key-vault/key-vault-get-started.md
[config-package]: service-fabric-application-model.md
[service-fabric-cluster-creation-via-arm]: service-fabric-cluster-creation-via-arm.md

<!-- Images -->
[overview]:./media/service-fabric-application-secret-management/overview.png
