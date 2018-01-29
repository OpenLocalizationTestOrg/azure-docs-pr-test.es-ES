---
title: "Hoja de referencia rápida de XPath de configuración del rol de Cloud Services | Microsoft Docs"
description: "Distintas configuraciones de XPath que puede usar en la configuración del rol de servicio en la nube para exponer la configuración como una variable de entorno."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: c51e4493-0643-4d05-bc44-06c76bcbf7d1
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: adegeo
ms.openlocfilehash: e71adbca34390bda3a7d4067742ffb3a28201449
ms.sourcegitcommit: afc78e4fdef08e4ef75e3456fdfe3709d3c3680b
ms.translationtype: HT
ms.contentlocale: es-ES
ms.lasthandoff: 11/16/2017
---
# <a name="expose-role-configuration-settings-as-an-environment-variable-with-xpath"></a>Exponer los valores de configuración de rol como una variable de entorno con XPath
En el archivo de definición de servicio de un rol web o trabajo en el servicio en la nube, puede exponer los valores de configuración en tiempo de ejecución como variables de entorno. Se admiten los siguientes valores de XPath (que se corresponden con valores de API).

Estos valores de XPath también están disponibles en la biblioteca [Microsoft.WindowsAzure.ServiceRuntime](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.aspx) . 

## <a name="app-running-in-emulator"></a>Aplicación en ejecución en el emulador
Indica que la aplicación se ejecuta en el emulador.

| Tipo | Ejemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/Deployment/@emulated" |
| Código |var x = RoleEnvironment.IsEmulated; |

## <a name="deployment-id"></a>Id. de implementación
Recupera el identificador de implementación de la instancia.

| Tipo | Ejemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/Deployment/@id" |
| Código |var deploymentId = RoleEnvironment.DeploymentId; |

## <a name="role-id"></a>Id. de rol
Recupera el identificador del rol actual de la instancia.

| Tipo | Ejemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@id" |
| Código |var id = RoleEnvironment.CurrentRoleInstance.Id; |

## <a name="update-domain"></a> Actualizar dominio
Recupera el dominio de actualización de la instancia.

| Tipo | Ejemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@updateDomain" |
| Código |var ud = RoleEnvironment.CurrentRoleInstance.UpdateDomain; |

## <a name="fault-domain"></a>Dominio de error
Recupera el dominio de error de la instancia.

| Tipo | Ejemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@faultDomain" |
| Código |var fd = RoleEnvironment.CurrentRoleInstance.FaultDomain; |

## <a name="role-name"></a>Nombre de rol
Recupera el nombre de rol de las instancias.

| Tipo | Ejemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/@roleName" |
| Código |var rname = RoleEnvironment.CurrentRoleInstance.Role.Name; |

## <a name="config-setting"></a>Opción de configuración
Recupera el valor de la opción de configuración especificada.

| Tipo | Ejemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/ConfigurationSettings/ConfigurationSetting[@name='Setting1']/@value" |
| Código |var setting = RoleEnvironment.GetConfigurationSettingValue("Setting1"); |

## <a name="local-storage-path"></a>Ruta de acceso de almacenamiento local
Recupera la ruta de acceso de almacenamiento local de la instancia.

| Tipo | Ejemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@path" |
| Código |var localResourcePath = RoleEnvironment.GetLocalResource("LocalStore1").RootPath; |

## <a name="local-storage-size"></a>Tamaño del almacenamiento local
Recupera el tamaño del almacenamiento local de la instancia.

| Tipo | Ejemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/LocalResources/LocalResource[@name='LocalStore1']/@sizeInMB" |
| Código |var localResourceSizeInMB = RoleEnvironment.GetLocalResource("LocalStore1").MaximumSizeInMegabytes; |

## <a name="endpoint-protocol"></a>Protocolo del punto de conexión
Recupera el protocolo del punto de conexión de la instancia.

| Tipo | Ejemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@protocol" |
| Código |var prot = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].Protocol; |

## <a name="endpoint-ip"></a>IP del punto de conexión
Obtiene la dirección IP del punto de conexión especificado.

| Tipo | Ejemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@address" |
| Código |var address = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Address |

## <a name="endpoint-port"></a>Puerto del punto de conexión
Recupera el puerto del punto de conexión de la instancia.

| Tipo | Ejemplo |
| --- | --- |
| XPath |xpath="/RoleEnvironment/CurrentInstance/Endpoints/Endpoint[@name='Endpoint1']/@port" |
| Código |var port = RoleEnvironment.CurrentRoleInstance.InstanceEndpoints["Endpoint1"].IPEndpoint.Port; |

## <a name="example"></a>Ejemplo
Este es un ejemplo de un rol de trabajo que crea una tarea de inicio con una variable de entorno denominada `TestIsEmulated` establecida en el [@emulated valor xpath](#app-running-in-emulator). 

```xml
<WorkerRole name="Role1">
    <ConfigurationSettings>
      <Setting name="Setting1" />
    </ConfigurationSettings>
    <LocalResources>
      <LocalStorage name="LocalStore1" sizeInMB="1024"/>
    </LocalResources>
    <Endpoints>
      <InternalEndpoint name="Endpoint1" protocol="tcp" />
    </Endpoints>
    <Startup>
      <Task commandLine="example.cmd inputParm">
        <Environment>
          <Variable name="TestConstant" value="Constant"/>
          <Variable name="TestEmptyValue" value=""/>
          <Variable name="TestIsEmulated">
            <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
          </Variable>
          ...
        </Environment>
      </Task>
    </Startup>
    <Runtime>
      <Environment>
        <Variable name="TestConstant" value="Constant"/>
        <Variable name="TestEmptyValue" value=""/>
        <Variable name="TestIsEmulated">
          <RoleInstanceValue xpath="/RoleEnvironment/Deployment/@emulated"/>
        </Variable>
        ...
      </Environment>
    </Runtime>
    ...
</WorkerRole>
```

## <a name="next-steps"></a>Pasos siguientes
Obtenga más información sobre el archivo [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#serviceconfigurationcscfg) .

Cree un paquete [ServicePackage.cspkg](cloud-services-model-and-package.md#servicepackagecspkg) .

Habilite [Escritorio remoto](cloud-services-role-enable-remote-desktop-new-portal.md) para un rol.

