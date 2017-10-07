---
title: aaaWhat es un modelo de servicio en la nube y el paquete | Documentos de Microsoft
description: Describe el modelo de servicio de nube hello (.csdef, .cscfg) y el paquete (.cspkg) en Azure
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 4ce2feb5-0437-496c-98da-1fb6dcb7f59e
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: 5280cdca4810859b6afdbbe1359fc2fabe871894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-hello-cloud-service-model-and-how-do-i-package-it"></a>¿Qué es el modelo de servicio de nube de Hola y cómo puede empaquetar?
Se crea un servicio de nube de tres componentes, definición de servicio de Hola *(.csdef)*, la configuración de servicio de Hola *(.cscfg)*y un paquete de servicios *(.cspkg)*. Ambos hello **ServiceDefinition.csdef** y **ServiceConfig.cscfg** archivos están basados en XML y describir estructura Hola del servicio de nube de Hola y cómo está configurada; denominado modelo Hola. Hola **ServicePackage.cspkg** es un archivo zip que se genera a partir de hello **ServiceDefinition.csdef** y entre otras cosas, contiene todas las dependencias de hello necesario basados en binario. Azure crea un servicio de nube desde ambos hello **ServicePackage.cspkg** hello y **ServiceConfig.cscfg**.

Una vez que se ejecuta el servicio de nube de hello en Azure, puede volver a configurarlo a través de hello **ServiceConfig.cscfg** archivo, pero no se puede modificar la definición de Hola.

## <a name="what-would-you-like-tooknow-more-about"></a>¿Qué desea más información acerca de tooknow?
* Deseo tooknow más información acerca de hello [ServiceDefinition.csdef](#csdef) y [ServiceConfig.cscfg](#cscfg) archivos.
* Eso ya lo sé. Deme [algunos ejemplos](#next-steps) sobre lo que puedo configurar.
* Deseo hello toocreate [ServicePackage.cspkg](#cspkg).
* Estoy usando Visual Studio y quiero...
  * [Crear un servicio en la nube][vs_create]
  * [Volver a configurar un servicio en la nube existente][vs_reconfigure]
  * [Implementar un proyecto de servicio en la nube][vs_deploy]
  * [Escritorio remoto en una instancia de servicio en la nube][remotedesktop]

<a name="csdef"></a>

## <a name="servicedefinitioncsdef"></a>ServiceDefinition.csdef
Hola **ServiceDefinition.csdef** archivo especifica valores de hello que usan Azure tooconfigure un servicio de nube. Hola [esquema de definición de servicio de Azure (archivo de .csdef)](https://msdn.microsoft.com/library/azure/ee758711.aspx) proporciona el formato permitido de Hola para un archivo de definición de servicio. Hello en el ejemplo siguiente se muestra los Hola valores que se pueden definir para hello Web y roles de trabajo:

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceDefinition name="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition">
  <WebRole name="WebRole1" vmsize="Medium">
    <Sites>
      <Site name="Web">
        <Bindings>
          <Binding name="HttpIn" endpointName="HttpIn" />
        </Bindings>
      </Site>
    </Sites>
    <Endpoints>
      <InputEndpoint name="HttpIn" protocol="http" port="80" />
      <InternalEndpoint name="InternalHttpIn" protocol="http" />
    </Endpoints>
    <Certificates>
      <Certificate name="Certificate1" storeLocation="LocalMachine" storeName="My" />
    </Certificates>
    <Imports>
      <Import moduleName="Connect" />
      <Import moduleName="Diagnostics" />
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <LocalResources>
      <LocalStorage name="localStoreOne" sizeInMB="10" />
      <LocalStorage name="localStoreTwo" sizeInMB="10" cleanOnRoleRecycle="false" />
    </LocalResources>
    <Startup>
      <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" />
    </Startup>
  </WebRole>

  <WorkerRole name="WorkerRole1">
    <ConfigurationSettings>
      <Setting name="DiagnosticsConnectionString" />
    </ConfigurationSettings>
    <Imports>
      <Import moduleName="RemoteAccess" />
      <Import moduleName="RemoteForwarder" />
    </Imports>
    <Endpoints>
      <InputEndpoint name="Endpoint1" protocol="tcp" port="10000" />
      <InternalEndpoint name="Endpoint2" protocol="tcp" />
    </Endpoints>
  </WorkerRole>
</ServiceDefinition>
```

Puede hacer referencia a toohello [esquema de definición de servicio](https://msdn.microsoft.com/library/azure/ee758711.aspx) para entender mejor de esquema XML de hello utilizado aquí, sin embargo, aquí es una explicación rápida de algunos de los elementos de hello:

**Sites**  
Contiene definiciones de Hola para aplicaciones web o para sitios Web que se hospedan en IIS7.

**InputEndpoints**  
Contiene definiciones de Hola para puntos de conexión que utiliza el servicio en la nube toocontact Hola.

**InternalEndpoints**  
Contiene definiciones de Hola para los extremos que usan toocommunicate de instancias de rol entre sí.

**ConfigurationSettings**  
Contiene definiciones de configuración de Hola para características de un rol específico.

**Certificados**  
Contiene definiciones de Hola para los certificados que son necesarios para un rol. ejemplo de código anterior Hello muestra un certificado que se usa para la configuración de Hola de Connect de Azure.

**LocalResources**  
Contiene las definiciones de Hola para recursos de almacenamiento local. Un recurso de almacenamiento local es un directorio reservado en sistema de archivos de Hola de máquina virtual de hello en el que está ejecutando una instancia de un rol.

**Imports**  
Contiene las definiciones de Hola para los módulos importados. ejemplo de código anterior Hello muestra los módulos de hello para la conexión a Escritorio remoto y Azure Connect.

**Startup**  
Contiene tareas que se ejecutan cuando se inicia el rol de Hola. Hola tareas se definen en un .cmd o un archivo ejecutable.

<a name="cscfg"></a>

## <a name="serviceconfigurationcscfg"></a>ServiceConfiguration.cscfg
configuración de Hola de hello para el servicio de nube está determinada por los valores de hello en hello **ServiceConfiguration.cscfg** archivo. Especificar número de Hola de instancias que desee toodeploy para cada rol en este archivo. se agregan valores de Hola Hola opciones de configuración que ha definido en el archivo de definición de servicio de hello toohello archivo de configuración de servicio. huellas digitales de Hola para los certificados de administración que están asociados con el servicio de nube de hello también se agregan archivos toohello. Hola [esquema de configuración de servicio de Azure (.cscfg archivo)](https://msdn.microsoft.com/library/azure/ee758710.aspx) proporciona el formato permitido de Hola para un archivo de configuración de servicio.

Hello archivo de configuración de servicio no se empaqueta con la aplicación hello, pero está cargado tooAzure como un archivo independiente y es hello tooconfigure usa el servicio de nube. Puede cargar un nuevo archivo de configuración de servicio sin volver a implementar el servicio en la nube. valores de configuración de Hola para servicio de nube de Hola se pueden cambiar mientras se ejecuta el servicio de nube de Hola. Hello en el ejemplo siguiente se muestra los valores de configuración de Hola que se pueden definir hello Web y roles de trabajo:

```xml
<?xml version="1.0"?>
<ServiceConfiguration serviceName="MyServiceName" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration">
  <Role name="WebRole1">
    <Instances count="2" />
    <ConfigurationSettings>
      <Setting name="SettingName" value="SettingValue" />
    </ConfigurationSettings>

    <Certificates>
      <Certificate name="CertificateName" thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
      <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption"
         thumbprint="CertThumbprint" thumbprintAlgorithm="sha1" />
    </Certificates>
  </Role>
</ServiceConfiguration>
```

Puede hacer referencia a toohello [esquema de configuración de servicio](https://msdn.microsoft.com/library/azure/ee758710.aspx) para una mejor comprensión Hola esquema XML utilizado aquí, sin embargo, aquí es una explicación rápida de elementos de hello:

**Instances**  
Configura el número de Hola de instancias de rol de hello en ejecución. tooprevent la nube de servicio deje de estar disponible durante las actualizaciones, se recomienda implementar más de una instancia de los roles web orientadas. Mediante la implementación de más de una instancia, siguiendo las directrices de toohello Hola [contrato de nivel de proceso de servicio (SLA) de Azure](http://azure.microsoft.com/support/legal/sla/), lo que garantiza una conectividad externa 99,95% para los roles de conexión a Internet cuando dos o más roles se implementan instancias para un servicio.

**ConfigurationSettings**  
Configura opciones de Hola para hello instancias en ejecución para un rol. nombre de Hola de hello `<Setting>` elementos deben coincidir con las definiciones de configuración de hello en el archivo de definición de servicio de Hola.

**Certificados**  
Configura los certificados de Hola que usan el servicio de Hola. ejemplo de código de Hello anterior muestra cómo toodefine Hola certificado para el módulo de RemoteAccess Hola. Hola valo hello *huella digital* atributo debe establecerse la huella digital de toohello de hello certificado toouse.

<p/>

> [!NOTE]
> huella digital de Hello para el certificado de hello puede agregarse toohello archivo de configuración mediante un editor de texto. O bien, se puede agregar valor hello en hello **certificados** ficha de hello **propiedades** página de rol de hello en Visual Studio.
> 
> 

## <a name="defining-ports-for-role-instances"></a>Definición de los puertos de las instancias de rol
Azure permite solo un rol web de tooa de punto de entrada. Esto significa que todo el tráfico se produce a través de una dirección IP. Puede configurar su tooshare un puerto de sitios Web mediante la configuración de hello encabezado toodirect Hola solicitud toohello correcta la ubicación del host. También puede configurar los puertos de las aplicaciones toolisten toowell conocidos en la dirección IP de Hola.

Hello en el ejemplo siguiente muestra hello configuración para un rol web con un sitio Web y una aplicación web. sitio Web de Hello está configurado como ubicación de entrada predeterminada de hello en el puerto 80, y que las aplicaciones web de hello son solicitudes de tooreceive configurado de un encabezado de host alternativo que se llama "mail.mysite.cloudapp.net".

```xml
<WebRole>
  <ConfigurationSettings>
    <Setting name="DiagnosticsConnectionString" />
  </ConfigurationSettings>
  <Endpoints>
    <InputEndpoint name="HttpIn" protocol="http" port="80" />
    <InputEndpoint name="Https" protocol="https" port="443" certificate="SSL"/>
    <InputEndpoint name="NetTcp" protocol="tcp" port="808" certificate="SSL"/>
  </Endpoints>
  <LocalResources>
    <LocalStorage name="Sites" cleanOnRoleRecycle="true" sizeInMB="100" />
  </LocalResources>
  <Site name="Mysite" packageDir="Sites\Mysite">
    <Bindings>
      <Binding name="http" endpointName="HttpIn" />
      <Binding name="https" endpointName="Https" />
      <Binding name="tcp" endpointName="NetTcp" />
    </Bindings>
  </Site>
  <Site name="MailSite" packageDir="MailSite">
    <Bindings>
      <Binding name="mail" endpointName="HttpIn" hostheader="mail.mysite.cloudapp.net" />
    </Bindings>
    <VirtualDirectory name="artifacts" />
    <VirtualApplication name="storageproxy">
      <VirtualDirectory name="packages" packageDir="Sites\storageProxy\packages"/>
    </VirtualApplication>
  </Site>
</WebRole>
```


## <a name="changing-hello-configuration-of-a-role"></a>Cambiar la configuración de Hola de un rol
Puede actualizar configuración de hello del servicio en la nube mientras se ejecuta en Azure, sin necesidad de desconectar el servicio de Hola. información de configuración de toochange, puede cargar un archivo de configuración o modificar el archivo de configuración de hello en colocar y aplicarlo tooyour ejecuta el servicio. Hello siguientes pueden realizarse cambios toohello configuración de un servicio:

* **Cambiar los valores de hello de valores de configuración**  
  Cuando una configuración de cambios, en la configuración una instancia de rol puede elegir tooapply Hola cambio mientras está en línea la instancia de Hola o instancia de hello toorecycle correctamente y aplicar el cambio de hello mientras Hola instancia está sin conexión.
* **Cambiar la topología del servicio Hola de instancias de rol**  
  : los cambios en la topología no afectan a las instancias en ejecución, excepto donde se vaya a eliminar una instancia. Todas las instancias restantes por lo general no es necesario toobe recicle; Sin embargo, puede elegir toorecycle instancias de rol en el cambio de topología de respuesta tooa.
* **Cambio de huella digital del certificado Hola**  
  : solo puede actualizar un certificado cuando una instancia de rol está sin conexión. Si un certificado es agregado, eliminado o cambiado mientras una instancia de rol está en línea, Azure correctamente toma certificado Hola de hello instancia tooupdate sin conexión y volver a iniciarlo en línea una vez completado el cambio de Hola.

### <a name="handling-configuration-changes-with-service-runtime-events"></a>Control de los cambios de configuración con eventos de tiempo de ejecución de servicio
Hola [biblioteca en tiempo de ejecución de Azure](https://msdn.microsoft.com/library/azure/mt419365.aspx) incluye hello [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.aspx) espacio de nombres, que proporciona clases para interactuar con hello entorno de Azure desde un rol. Hola [RoleEnvironment](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) clase define Hola después de eventos que se producen antes y después de un cambio de configuración:

* **[Cambiar](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changing.aspx) evento**  
  Esto se produce antes de cambio de configuración de hello tooa aplicada la instancia especificada de un rol de ofrecerle una tootake oportunidad hacia abajo de instancias de rol de hello si es necesario.
* **[Evento](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleenvironment.changed.aspx) cambiado**  
  Se produce después del cambio de configuración de hello tooa aplicada la instancia especificada de un rol.

> [!NOTE]
> Dado que cambios en el certificado siempre tienen instancias de Hola de un rol sin conexión, no producen eventos RoleEnvironment.Changing o RoleEnvironment.Changed de Hola.
> 
> 

<a name="cspkg"></a>

## <a name="servicepackagecspkg"></a>ServicePackage.cspkg
toodeploy una aplicación como un servicio de nube en Azure, primero debe primera aplicación Hola de paquete en formato adecuado de Hola. Puede usar hello **CSPack** herramienta de línea de comandos (instalado con hello [Azure SDK](https://azure.microsoft.com/downloads/)) archivo de paquete de hello toocreate como una alternativa tooVisual Studio.

**CSPack** usa Hola contenido de hello servicio definición servicios de archivos y configuración toodefine Hola contenido del archivo de paquete de saludo. **CSPack** genera un archivo de paquete de aplicación (.cspkg) que se puede cargar tooAzure mediante hello [portal de Azure](cloud-services-how-to-create-deploy-portal.md#create-and-deploy). De forma predeterminada, se denomina paquete hello `[ServiceDefinitionFileName].cspkg`, pero puede especificar un nombre diferente mediante el uso de hello `/out` opción de **CSPack**.

**CSPack** se encuentra en:  
`C:\Program Files\Microsoft SDKs\Azure\.NET SDK\[sdk-version]\bin\`

> [!NOTE]
> CSPack.exe (en windows) está disponible mediante la ejecución de hello **Microsoft Azure Command Prompt** acceso directo que se instala con hello SDK.  
> 
> Ejecutar programa de hello CSPack.exe toosee documentación sobre todos los conmutadores de hello posibles y los comandos.
> 
> 

<p />

> [!TIP]
> Ejecutar su servicio en la nube localmente en hello **emulador de proceso de Microsoft Azure**, usar hello **/copyonly** opción. Esta opción copia los archivos binarios de hello para el diseño de directorio tooa Hola aplicación desde el que se pueden ejecutar en el emulador de proceso de Hola.
> 
> 

### <a name="example-command-toopackage-a-cloud-service"></a>Comando de ejemplo toopackage un servicio de nube
Hello en el ejemplo siguiente se crea un paquete de aplicación que contiene información de Hola para un rol web. comando Hello especifica toouse de archivo de definición de servicio de hello, directory Hola donde pueden ser archivos binarios encuentra y Hola nombre del archivo de paquete de hello.

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /out:[OutputFileName]
```

Si la aplicación hello contiene un rol web y un rol de trabajo, hello siguiente comando se utiliza:

```cmd
cspack [DirectoryName]\[ServiceDefinition]
       /out:[OutputFileName]
       /role:[RoleName];[RoleBinariesDirectory]
       /sites:[RoleName];[VirtualPath];[PhysicalPath]
       /role:[RoleName];[RoleBinariesDirectory];[RoleAssemblyName]
```

Donde las variables de Hola se definen como sigue:

| Variable | Valor |
| --- | --- |
| \[DirectoryName\] |Hola subdirectorio en hello directorio raíz del proyecto que contiene el archivo de .csdef Hola de hello proyecto de Azure. |
| \[ServiceDefinition\] |nombre de Hola Hola servicio del archivo de definición. De forma predeterminada, este archivo se denomina ServiceDefinition.csdef. |
| \[OutputFileName\] |nombre de Hola para hello genera el archivo de paquete. Normalmente, esto se establece toohello nombre de aplicación hello. Si no se especifica ningún nombre de archivo, el paquete de aplicación Hola se crea como \[ApplicationName\].cspkg. |
| \[RoleName\] |nombre de Hello del rol de hello tal como se define en el archivo de definición de servicio de Hola. |
| \[RoleBinariesDirectory] |ubicación de Hola de archivos binarios de hello para el rol de Hola. |
| \[VirtualPath\] |directorios físicos de Hola para cada ruta de acceso virtual definida en hello sitios sección de definición de servicio de Hola. |
| \[PhysicalPath\] |Hola directorios físicos del contenido de Hola para cada ruta de acceso virtual definidos en el nodo de sitio de Hola de definición de servicio de Hola. |
| \[RoleAssemblyName\] |nombre de Hello del archivo binario de hello para el rol de Hola. |

## <a name="next-steps"></a>Pasos siguientes
Voy a crear un paquete de servicio en la nube y quiero...

* [Configurar Escritorio remoto para una instancia de servicio en la nube][remotedesktop]
* [Implementar un proyecto de servicio en la nube][deploy]

Estoy usando Visual Studio y quiero...

* [Crear un nuevo servicio en la nube][vs_create]
* [Volver a configurar un servicio en la nube existente][vs_reconfigure]
* [Implementar un proyecto de servicio en la nube][vs_deploy]
* [Configurar Escritorio remoto para una instancia de servicio en la nube][vs_remote]

[deploy]: cloud-services-how-to-create-deploy-portal.md
[remotedesktop]: cloud-services-role-enable-remote-desktop.md
[vs_remote]: ../vs-azure-tools-remote-desktop-roles.md
[vs_deploy]: ../vs-azure-tools-cloud-service-publish-set-up-required-services-in-visual-studio.md
[vs_reconfigure]: ../vs-azure-tools-configure-roles-for-cloud-service.md
[vs_create]: ../vs-azure-tools-azure-project-create.md
