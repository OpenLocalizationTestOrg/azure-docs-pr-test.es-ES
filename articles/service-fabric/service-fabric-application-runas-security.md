---
title: aaaLearn acerca de las directivas de seguridad de Azure microservicios | Documentos de Microsoft
description: "Información general sobre cómo toorun una aplicación de Service Fabric en sistema y las cuentas de seguridad local, incluido el punto de SetupEntry Hola donde una aplicación necesita tooperform algunas privilegiado acción antes de empezar"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 4242a1eb-a237-459b-afbf-1e06cfa72732
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: mfussell
ms.openlocfilehash: f5afba69e09aa4f3c9efa4d3efc6995c813a1f71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="configure-security-policies-for-your-application"></a>Configuración de directivas de seguridad para la aplicación
Mediante el uso de Azure Service Fabric, puede proteger las aplicaciones que se ejecutan en el clúster de hello en distintas cuentas de usuario. Service Fabric también ayuda a certificados, archivos, directorios y recursos de hello segura que se usan las aplicaciones en tiempo de Hola de implementación con cuentas de usuario de hello, por ejemplo. Esto aumenta la seguridad entre aplicaciones en ejecución, incluso en un entorno hospedado compartido.

De forma predeterminada, aplicaciones de Service Fabric se ejecutan bajo la cuenta de hello hello Fabric.exe proceso se ejecuta bajo. Service Fabric también proporciona capacidad de hello toorun aplicaciones mediante una cuenta de sistema local, que se especifica en el manifiesto de aplicación Hola o cuenta de usuario local. Los tipos de cuenta de sistema local compatibles son **LocalUser**, **NetworkService**, **LocalService** y **LocalSystem**.

 Si estás ejecutando Service Fabric en Windows Server en el centro de datos utilizando el instalador independiente de hello, puede utilizar cuentas de dominio de Active Directory, incluidas las cuentas de servicio administradas de grupo.

Puede definir y crear grupos de usuarios para que se pueden agregar uno o más usuarios tooeach toobe de grupo administrada de manera conjunta. Esto es útil cuando hay varios usuarios para los puntos de entrada de servicio diferente y es necesario toohave ciertos privilegios comunes que están disponibles en el nivel de grupo de Hola.

## <a name="configure-hello-policy-for-a-service-setup-entry-point"></a>Configurar la directiva de Hola para un punto de entrada del programa de instalación de servicio
Como se describe en hello [modelo de aplicación](service-fabric-application-model.md), Hola punto de entrada del programa de instalación, **SetupEntryPoint**, es un punto de entrada con privilegios que se ejecuta con hello mismo credenciales como Service Fabric (normalmente hello *NetworkService* cuenta) antes de cualquier otro punto de entrada. archivo ejecutable de Hello especificado por **EntryPoint** suele ser host de servicio de ejecución prolongada de Hola. Por lo que tiene una entrada de programa de instalación independiente de punto, evita tener toorun host del servicio Hola ejecutable con privilegios altos durante largos períodos de tiempo. Hola ejecutable que **EntryPoint** especifica se ejecuta después de **SetupEntryPoint** se cierra correctamente. Hello proceso resultante se supervisa y se reinicia y vuelve a comenzar con **SetupEntryPoint** si alguna vez finaliza o se bloquea.

Hola aquí te mostramos un ejemplo de manifiesto de servicio simple que muestra Hola SetupEntryPoint y Hola punto de entrada principal para el servicio de Hola.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
        <WorkingFolder>CodePackage</WorkingFolder>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
  </CodePackage>
  <ConfigPackage Name="Config" Version="1.0.0" />
</ServiceManifest>
```

### <a name="configure-hello-policy-by-using-a-local-account"></a>Configurar directiva de hello mediante una cuenta local
Después de configurar Hola servicio toohave un punto de entrada del programa de instalación, puede cambiar los permisos de seguridad de Hola que se ejecuta bajo en el manifiesto de aplicación Hola. Hola de ejemplo siguiente muestra cómo tooconfigure Hola toorun de servicio con privilegios de cuenta de usuario administrador.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupAdminUser" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupAdminUser">
            <MemberOf>
               <SystemGroup Name="Administrators" />
            </MemberOf>
         </User>
      </Users>
   </Principals>
</ApplicationManifest>
```

En primer lugar, cree una sección **Principals** con un nombre de usuario, como SetupAdminUser. Esto indica que ese usuario hello es un miembro del grupo de sistema de los administradores de Hola.

Después, en hello **ServiceManifestImport** sección, configure una directiva tooapply esta entidad de seguridad demasiado**SetupEntryPoint**. Esto indica a Service Fabric que cuando hello **MySetup.bat** archivo se ejecuta, debería ser `RunAs` con privilegios de administrador. Dado que tiene *no* aplicar un punto de entrada principal de toohello de directiva, el código de hello en **MyServiceHost.exe** se ejecuta en el sistema de hello **NetworkService** cuenta. Se trata de cuenta predeterminada de Hola que todos los puntos de entrada de servicio se ejecutan como.

Ahora agreguemos Hola archivo MySetup.bat toohello Visual Studio project tootest Hola privilegios de administrador. En Visual Studio, haga clic en proyecto de servicio de Hola y agregue un nuevo archivo denominado MySetup.bat.

A continuación, asegúrese de que ese archivo de MySetup.bat Hola se incluye en el paquete del servicio de Hola. De forma predeterminada, no lo está. Seleccione el archivo hello, haga clic en el menú contextual de tooget hello y elija **propiedades**. En el cuadro de diálogo de propiedades de hello, asegúrese de que **copiar tooOutput directorio** se establece demasiado**copiar si es posterior**. Vea Hola siguiente captura de pantalla.

![CopyToOutput de Visual Studio para el archivo por lotes de SetupEntryPoint][image1]

Ahora abra hello MySetup.bat archivo y agregue Hola siguientes comandos:

```
REM Set a system environment variable. This requires administrator privilege
setx -m TestVariable "MyValue"
echo System TestVariable set too> out.txt
echo %TestVariable% >> out.txt

REM toodelete this system variable us
REM REG delete "HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Session Manager\Environment" /v TestVariable /f
```

A continuación, compile e implemente el clúster de desarrollo local de hello solución tooa. Después de que se inició el servicio de hello tal como se muestra en el Explorador de tejido de servicio, puede ver que ese archivo de MySetup.bat Hola fue correcto de una de dos maneras. Abra un símbolo del sistema de PowerShell y escriba:

```
PS C:\ [Environment]::GetEnvironmentVariable("TestVariable","Machine")
MyValue
```

Tenga en cuenta, a continuación, nombre de hello del nodo de Hola donde servicio Hola se ha implementado y se inició en el Explorador de Service Fabric: por ejemplo, nodo 2. A continuación, navegue toohello instancia trabajo carpeta toofind hello out.txt archivo de aplicación que muestra el valor de Hola de **TestVariable**. Por ejemplo, si este servicio se ha implementado tooNode 2, a continuación, puede ir hello en la ruta de acceso toothis **MyApplicationType**:

```
C:\SfDevCluster\Data\_App\Node.2\MyApplicationType_App\work\out.txt
```

### <a name="configure-hello-policy-by-using-local-system-accounts"></a>Configurar la directiva de hello mediante cuentas de sistema local
A menudo, es preferible toorun script de inicio de hello usando una cuenta de sistema local en lugar de una cuenta de administrador. Ejecutar la directiva de ejecución de hello como miembro del programa Hola a grupo de administradores normalmente no funciona bien porque máquinas tienen Control de acceso de usuario (UAC) habilitado de forma predeterminada. En tales casos, **recomendación de hello es toorun hello SetupEntryPoint como LocalSystem, en lugar de como un grupo de usuario local agregada tooAdministrators**. Hello en el ejemplo siguiente se muestra configuración hello SetupEntryPoint toorun como LocalSystem:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="SetupLocalSystem" EntryPointType="Setup" />
      </Policies>
   </ServiceManifestImport>
   <Principals>
      <Users>
         <User Name="SetupLocalSystem" AccountType="LocalSystem" />
      </Users>
   </Principals>
</ApplicationManifest>
```

## <a name="start-powershell-commands-from-a-setup-entry-point"></a>Inicio de comandos de PowerShell desde un SetupEntryPoint
toorun PowerShell de hello **SetupEntryPoint** punto, puede ejecutar **PowerShell.exe** en un archivo por lotes que señala tooa PowerShell de archivos. En primer lugar, agregue un proyecto de servicio de PowerShell archivo toohello: por ejemplo, **MySetup.ps1**. Recuerde hello tooset *copiar si es posterior* propiedad para ese archivo hello también se incluye en el paquete del servicio de Hola. Hello en el ejemplo siguiente se muestra un archivo por lotes de ejemplo que se inicia un archivo de PowerShell denominado MySetup.ps1, que establece una variable de entorno de sistema denominada **TestVariable**.

MySetup.bat toostart un archivo de PowerShell:

```
powershell.exe -ExecutionPolicy Bypass -Command ".\MySetup.ps1"
```

En el archivo de PowerShell de hello, agregue Hola después tooset una variable de entorno del sistema:

```
[Environment]::SetEnvironmentVariable("TestVariable", "MyValue", "Machine")
[Environment]::GetEnvironmentVariable("TestVariable","Machine") > out.txt
```

> [!NOTE]
> De forma predeterminada, cuando se ejecuta el archivo por lotes de hello, parece en la carpeta de la aplicación hello llama **trabajar** para los archivos. En este caso, cuando se ejecuta MySetup.bat, queremos este hello toofind MySetup.ps1 en el archivo hello misma carpeta, que es la aplicación hello **el paquete de código** carpeta. toochange esta carpeta, la carpeta de trabajo de Hola de conjunto:
> 
> 

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    </ExeHost>
</SetupEntryPoint>
```

## <a name="use-console-redirection-for-local-debugging"></a>Uso de la redirección de la consola para la depuración local
En ocasiones, resulta útil toosee salida de la consola Hola de ejecución de un script para fines de depuración. toodo esto, puede establecer una directiva de redirección de consola, que escribe el archivo de tooa de salida de hello. Hello archivo de salida se denomina de carpeta de la aplicación escrita toohello **registro** en el nodo de Hola donde se ha implementado y ejecutar aplicación hello. (Consulte dónde toofind esto en el anterior ejemplo de Hola.)

> [!WARNING]
> Nunca use Directiva de redirección de consola de hello en una aplicación que se implementa en producción porque esto puede afectar a la conmutación por error de aplicación de Hola. *Solo* debe usarla con fines de depuración y desarrollo local.  
> 
> 

Hello en el ejemplo siguiente se muestra redirección de la consola de configuración Hola con un valor de FileRetentionCount:

```xml
<SetupEntryPoint>
    <ExeHost>
    <Program>MySetup.bat</Program>
    <WorkingFolder>CodePackage</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="10"/>
    </ExeHost>
</SetupEntryPoint>
```

Si cambia ahora hello MySetup.ps1 archivo toowrite una **Echo** comando, se escribirá toohello el archivo de salida con fines de depuración:

```
Echo "Test console redirection which writes toohello application log folder on hello node that hello application is deployed to"
```

**Después de haber depurado el script, quite inmediatamente esta directiva de redireccionamiento de consola**.

## <a name="configure-a-policy-for-service-code-packages"></a>Configuración de una directiva para los paquetes de código del servicio
En hello pasos anteriores, ha visto cómo tooapply una tooSetupEntryPoint de directiva de ejecución. Echemos un vistazo un poco más en cómo toocreate diferentes entidades de seguridad que se pueden aplicar como directivas de servicio.

### <a name="create-local-user-groups"></a>Creación de grupos de usuarios locales
Puede definir y crear grupos de usuarios que permite que uno o más toobe a los usuarios agrega grupo tooa. Esto es útil si hay varios usuarios para los puntos de entrada de servicio diferente y necesitan toohave ciertos privilegios comunes que están disponibles en el nivel de grupo de Hola. Hello en el ejemplo siguiente se muestra un grupo local denominado **LocalAdminGroup** que tenga privilegios de administrador. Dos usuarios, Customer1 y Customer2, se convierten en miembros de este grupo local.

```xml
<Principals>
 <Groups>
   <Group Name="LocalAdminGroup">
     <Membership>
       <SystemGroup Name="Administrators"/>
     </Membership>
   </Group>
 </Groups>
  <Users>
     <User Name="Customer1">
        <MemberOf>
           <Group NameRef="LocalAdminGroup" />
        </MemberOf>
     </User>
    <User Name="Customer2">
      <MemberOf>
        <Group NameRef="LocalAdminGroup" />
      </MemberOf>
    </User>
  </Users>
</Principals>
```

### <a name="create-local-users"></a>Creación de usuarios locales
Puede crear un usuario local que puede ser utilizado toohelp segura de servicios dentro de la aplicación hello. Cuando un **usuarioLocal** tipo de cuenta se especifica en la sección de entidades de seguridad de Hola Hola del manifiesto de aplicación, Service Fabric crea cuentas de usuario locales en equipos donde se implementa la aplicación hello. De forma predeterminada, estas cuentas no tienen Hola mismos nombres que los especificados en la aplicación hello manifiesto (por ejemplo, Customer3 en el siguiente ejemplo de Hola). En su lugar, se generan dinámicamente y tienen contraseñas aleatorias.

```xml
<Principals>
  <Users>
     <User Name="Customer3" AccountType="LocalUser" />
  </Users>
</Principals>
```

Si una aplicación requiere que ser la misma en todos los equipos (por ejemplo, la autenticación NTLM tooenable) Hola cuentas de usuario y contraseñas, el manifiesto de clúster de Hola debe establecer NTLMAuthenticationEnabled tootrue. Hello manifiesto de clúster debe especificar una NTLMAuthenticationPasswordSecret que se usa toogenerate Hola la misma contraseña en todos los equipos.

```xml
<Section Name="Hosting">
      <Parameter Name="EndpointProviderEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationEnabled" Value="true"/>
      <Parameter Name="NTLMAuthenticationPassworkSecret" Value="******" IsEncrypted="true"/>
 </Section>
```

### <a name="assign-policies-toohello-service-code-packages"></a>Asignar directivas toohello paquetes de código de servicio
Hola **RunAsPolicy** sección un **ServiceManifestImport** especifica la cuenta de hello de sección de entidades de seguridad de Hola que debería ser toorun usa un paquete de código. También asocia código manifiesto de paquetes de servicio de hello con cuentas de usuario en la sección de hello las entidades de seguridad. Esto puede especificarse para el programa de instalación de Hola o puntos de entrada principal, o puede especificar `All` tooapply lo tooboth. Hello en el ejemplo siguiente se muestra distintas directivas que se va a aplicar:

```xml
<Policies>
<RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup"/>
<RunAsPolicy CodePackageRef="Code" UserRef="Customer3" EntryPointType="Main"/>
</Policies>
```

Si **EntryPointType** no se especifica, valor predeterminado de Hola se establece tooEntryPointType = "Main". Especificar **SetupEntryPoint** es especialmente útil cuando desea toorun ciertas operaciones de instalación con privilegios elevados con una cuenta de sistema. código de servicio real de Hello puede ejecutar bajo una cuenta con menos privilegios.

### <a name="apply-a-default-policy-tooall-service-code-packages"></a>Aplicar un paquetes de código predeterminada directiva tooall servicio
Usar hello **DefaultRunAsPolicy** sección toospecify una cuenta de usuario predeterminada para todos los paquetes de código que no tienen un determinado **RunAsPolicy** definido. Si la mayoría de los paquetes de código de hello que se especifican en el manifiesto del servicio Hola utilizado por una aplicación necesita toorun en Hola mismo usuario, hello aplicación solo puede definir una directiva de ejecución predeterminada con esa cuenta de usuario. Hello en el ejemplo siguiente se especifica que, si un paquete de código no tiene un **RunAsPolicy** especificado, debe ejecutar el paquete de código de hello en hello **MyDefaultAccount** especificado en la sección de hello las entidades de seguridad.

```xml
<Policies>
  <DefaultRunAsPolicy UserRef="MyDefaultAccount"/>
</Policies>
```
### <a name="use-an-active-directory-domain-group-or-user"></a>Uso de un usuario o un grupo de dominios de Active Directory
Para una instancia de Service Fabric que se instaló en Windows Server mediante el instalador independiente de hello, puede ejecutar Hola servicio con credenciales de Hola para una cuenta de usuario o grupo de Active Directory. Esto se aplica a Active Directory local dentro del dominio y no a Azure Active Directory (AAD). Mediante el uso de un grupo o usuario de dominio, a continuación, puede tener acceso a otros recursos de dominio de hello (por ejemplo, recursos compartidos de archivos) que se han concedido permisos.

Hello en el ejemplo siguiente se muestra un usuario de Active Directory denominado *Usuarioprueba* con su dominio llamado contraseña cifrada mediante un certificado *MyCert*. Puede usar hello `Invoke-ServiceFabricEncryptText` texto de cifrado secreto de Hola de toocreate de comandos de PowerShell. Vea [Administración de secretos en aplicaciones de Service Fabric](service-fabric-application-secret-management.md) | Microsoft Azure.

Debe implementar la clave privada de hello del equipo local del toohello de contraseña de hello certificado toodecrypt hello mediante el uso de un método fuera de banda (en Azure, esto es a través del Administrador de recursos de Azure). A continuación, cuando Service Fabric implementa la máquina de toohello de paquete de servicio de hello, es capaz de toodecrypt Hola secreto y (junto con el nombre de usuario de Hola) se autentican con Active Directory toorun en esas credenciales.

```xml
<Principals>
  <Users>
    <User Name="TestUser" AccountType="DomainUser" AccountName="Domain\User" Password="[Put encrypted password here using MyCert certificate]" PasswordEncrypted="true" />
  </Users>
</Principals>
<Policies>
  <DefaultRunAsPolicy UserRef="TestUser" />
  <SecurityAccessPolicies>
    <SecurityAccessPolicy ResourceRef="MyCert" PrincipalRef="TestUser" GrantRights="Full" ResourceType="Certificate" />
  </SecurityAccessPolicies>
</Policies>
<Certificates>
```
### <a name="use-a-group-managed-service-account"></a>Use una cuenta de servicio administrada de grupo.
Para una instancia de Service Fabric que se instaló en Windows Server mediante el instalador independiente de hello, puede ejecutar el servicio de Hola como un grupo de cuentas de servicio administradas (gMSA). Tenga en cuenta que esto se aplica a Active Directory local dentro del dominio y no para Azure Active Directory (AAD). Mediante el uso de una gMSA hay ninguna contraseña o la contraseña cifrada que se almacenan en hello `Application Manifest`.

Hello en el ejemplo siguiente se muestra cómo toocreate una cuenta de gMSA llama *svc prueba$*; el modo toodeploy que administran los nodos de clúster de toohello de cuenta de servicio; y cómo tooconfigure Hola principal de usuario.

##### <a name="prerequisites"></a>Requisitos previos.
- dominio de Hello necesita una clave de raíz KDS.
- dominio de Hello debe toobe en un nivel funcional de versiones posteriores o Windows Server 2012.

##### <a name="example"></a>Ejemplo
1. Tiene un administrador de dominio de active directory crear una cuenta de servicio administradas de grupo con hello `New-ADServiceAccount` commandlet y asegúrese de que hello `PrincipalsAllowedToRetrieveManagedPassword` incluye todos Hola service fabric nodos del clúster. Tenga en cuenta que `AccountName`, `DnsHostName` y `ServicePrincipalName` deben ser únicos.
```
New-ADServiceAccount -name svc-Test$ -DnsHostName svc-test.contoso.com  -ServicePrincipalNames http/svc-test.contoso.com -PrincipalsAllowedToRetrieveManagedPassword SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$
```
2. En cada uno de los nodos del clúster de tejido de hello servicio (por ejemplo, `SfNode0$,SfNode1$,SfNode2$,SfNode3$,SfNode4$`), instalar y probar hello gMSA.
```
Add-WindowsFeature RSAT-AD-PowerShell
Install-AdServiceAccount svc-Test$
Test-AdServiceAccount svc-Test$
```
3. Configurar la entidad de seguridad de usuario de Hola y configurar hello RunAsPolicy tooreference Hola usuario.
```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="MyApplicationType" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="MyServiceTypePkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="DomaingMSA"/>
      </Policies>
   </ServiceManifestImport>
  <Principals>
    <Users>
      <User Name="DomaingMSA" AccountType="ManagedServiceAccount" AccountName="domain\svc-Test$"/>
    </Users>
  </Principals>
</ApplicationManifest>
```

## <a name="assign-a-security-access-policy-for-http-and-https-endpoints"></a>Asignación de una directiva de acceso de seguridad a los puntos de conexión HTTP y HTTPS
Si aplica un servicio de tooa de directiva de ejecución y manifiesto de servicio de hello declara los recursos de punto de conexión con protocolo de hello HTTP, debe especificar un **SecurityAccessPolicy** tooensure que los puertos asignan extremos toothese están correctamente control de acceso incluyen hello cuenta de usuario de ejecución que se ejecuta el servicio de Hola. En caso contrario, **http.sys** no tienen acceso toohello servicio y obtener errores con llamadas de cliente de Hola. Hello en el ejemplo siguiente se aplica hello Customer1 cuenta tooan punto de conexión llamado **EndpointName**, que proporciona derechos de acceso completo.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
   <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
</Policies>
```

Para el extremo HTTPS de hello, también tiene tooindicate Hola nombre de hello certificado tooreturn toohello cliente. Puede hacerlo mediante el uso de **EndpointBindingPolicy**, con certificado Hola definida en una sección de certificados en el manifiesto de aplicación Hola.

```xml
<Policies>
   <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
  <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
   <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
  <!--EndpointBindingPolicy is needed if hello EndpointName is secured with https -->
  <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
</Policies
```
## <a name="upgrading-multiple-applications-with-https-endpoints"></a>Actualización de varias aplicaciones con puntos de conexión https
Necesita toobe cuidado de no toouse hello **mismo puerto** para distintas instancias de hello misma aplicación cuando se utiliza http**s**. motivo de Hello es que Service Fabric no sea cert, Hola tooupgrade pueda por una de las instancias de aplicación Hola. Por ejemplo, si desea que la aplicación 1 o de la aplicación 2 ambos tooupgrade su toocert cert 1 2. Cuando se produzca la actualización de hello, Service Fabric que podría limpiado registro de certificado 1 Hola con http.sys aunque hello otra aplicación está seguir utilizándolo. tooprevent, Service Fabric detecta que ya hay otra instancia de la aplicación registrada en el puerto de hello con certificado de Hola (due toohttp.sys) y se produce un error Hola operación.

Por lo tanto, Service Fabric no admite la actualización de dos servicios diferentes mediante **Hola mismo puerto** en instancias de aplicación diferente. En otras palabras, no puede usar Hola mismo certificado en diferentes servicios en hello mismo puerto. Si necesita toohave un certificado en hello mismo puerto, deberá tooensure ese Hola servicios se colocan en distintos equipos con las restricciones de posición. También puede considerar la posibilidad de utilizar puertos dinámicos de Service Fabric para cada servicio en cada instancia de la aplicación. 

Si ve un error de actualización con https, una advertencia de error que dice "hello Windows HTTP Server API no admite varios certificados para las aplicaciones que compartan un puerto."

## <a name="a-complete-application-manifest-example"></a>Ejemplo completo de un manifiesto de aplicación
Hola siguiendo el manifiesto de aplicación muestra muchos de hello valores distintos:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="Application3Type" ApplicationTypeVersion="1.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <Parameters>
      <Parameter Name="Stateless1_InstanceCount" DefaultValue="-1" />
   </Parameters>
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="Stateless1Pkg" ServiceManifestVersion="1.0.0" />
      <ConfigOverrides />
      <Policies>
         <RunAsPolicy CodePackageRef="Code" UserRef="Customer1" />
         <RunAsPolicy CodePackageRef="Code" UserRef="LocalAdmin" EntryPointType="Setup" />
        <!--SecurityAccessPolicy is needed if RunAsPolicy is defined and hello Endpoint is http -->
         <SecurityAccessPolicy ResourceRef="EndpointName" PrincipalRef="Customer1" />
        <!--EndpointBindingPolicy is needed hello EndpointName is secured with https -->
        <EndpointBindingPolicy EndpointRef="EndpointName" CertificateRef="Cert1" />
     </Policies>
   </ServiceManifestImport>
   <DefaultServices>
      <Service Name="Stateless1">
         <StatelessService ServiceTypeName="Stateless1Type" InstanceCount="[Stateless1_InstanceCount]">
            <SingletonPartition />
         </StatelessService>
      </Service>
   </DefaultServices>
   <Principals>
      <Groups>
         <Group Name="LocalAdminGroup">
            <Membership>
               <SystemGroup Name="Administrators" />
            </Membership>
         </Group>
      </Groups>
      <Users>
         <User Name="LocalAdmin">
            <MemberOf>
               <Group NameRef="LocalAdminGroup" />
            </MemberOf>
         </User>
         <!--Customer1 below create a local account that this service runs under -->
         <User Name="Customer1" />
         <User Name="MyDefaultAccount" AccountType="NetworkService" />
      </Users>
   </Principals>
   <Policies>
      <DefaultRunAsPolicy UserRef="LocalAdmin" />
   </Policies>
   <Certificates>
     <EndpointCertificate Name="Cert1" X509FindValue="FF EE E0 TT JJ DD JJ EE EE XX 23 4T 66 "/>
  </Certificates>
</ApplicationManifest>
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a>Pasos siguientes
* [Entender el modelo de aplicación Hola](service-fabric-application-model.md)
* [Especificación de los recursos en un manifiesto de servicio](service-fabric-service-manifest-resources.md)
* [Implementar una aplicación](service-fabric-deploy-remove-applications.md)

[image1]: ./media/service-fabric-application-runas-security/copy-to-output.png
