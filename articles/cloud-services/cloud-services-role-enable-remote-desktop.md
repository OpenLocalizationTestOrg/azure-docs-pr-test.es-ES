---
title: aaaEnable escritorio remoto en un servicio de nube de Azure | Documentos de Microsoft
description: "¿Cómo tooconfigure la nube de azure conexiones de escritorio remoto de tooallow de aplicación de servicio"
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: d3110ee8-6526-4585-aba5-d0bc9a713e9b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: adegeo
ms.openlocfilehash: b3c0180bf5ad29cb77e5303ccbd6f9ccc44b7b0a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="enable-remote-desktop-connection-for-a-role-in-azure-cloud-services"></a>Habilitación de la conexión a Escritorio remoto para un rol de Azure Cloud Services

> [!div class="op_single_selector"]
> * [Azure Portal](cloud-services-role-enable-remote-desktop-new-portal.md)
> * [Portal de Azure clásico](cloud-services-role-enable-remote-desktop.md)
> * [PowerShell](cloud-services-role-enable-remote-desktop-powershell.md)
> * [Visual Studio](../vs-azure-tools-remote-desktop-roles.md)

Puede habilitar una conexión a Escritorio remoto en el rol durante el desarrollo mediante la inclusión de módulos de escritorio remoto de hello en la definición de servicio o puede elegir tooenable escritorio remoto a través de hello extensión de escritorio remoto. Hello método preferido es extensión de escritorio remoto de hello toouse tal y como se puede habilitar Escritorio remoto incluso después de que se implementa la aplicación hello sin necesidad de tooredeploy la aplicación.

## <a name="configure-remote-desktop-from-hello-azure-classic-portal"></a>Configurar Escritorio remoto desde el portal de Azure clásico Hola
Hola portal de Azure clásico utiliza el método de extensión de escritorio remoto de Hola por lo que puede habilitar Escritorio remoto incluso después de que se implementa la aplicación hello. Hola **configurar** página de servicio en la nube permite tooenable escritorio remoto, Hola cambiar cuenta de administrador local usa máquinas virtuales de tooconnect toohello, certificado Hola utilizada en la autenticación y establece Hola fecha de expiración.

1. Haga clic en **servicios en la nube**, haga clic en nombre de hello del servicio de nube de hello y, a continuación, haga clic en **configurar**.
2. Haga clic en hello **remoto** situado en la parte inferior de Hola.

    ![Servicios en la nube remotos](./media/cloud-services-role-enable-remote-desktop/CloudServices_Remote.png)

   > [!WARNING]
   > se reiniciarán todas las instancias de rol la primera vez que habilite el Escritorio remoto y haga clic en Aceptar (marca de verificación). tooprevent un reinicio, contraseña de Hola de hello certificado tooencrypt usado debe estar instalado en el rol de Hola. tooprevent un reinicio, [cargar un certificado de servicio en la nube hello](cloud-services-configure-ssl-certificate.md#step-3-upload-a-certificate) y, a continuación, devolver toothis cuadro de diálogo.

3. En **Roles**, seleccione el rol de Hola que desee tooupdate o seleccione **todos los** para todos los roles.
4. Realice uno de hello siguientes cambios:

   * Escritorio remoto, seleccione hello tooenable **habilitar Escritorio remoto** casilla de verificación. toodisable escritorio remoto, Hola desactive casilla de verificación.
   * Crear una cuenta toouse en conexiones de escritorio remoto toohello instancias de rol.
   * Actualice la contraseña de hello cuenta existente de Hola.
   * Seleccione un toouse los certificados cargados para la autenticación (carga Hola certificado mediante **cargar** en hello **certificados** página) o crear un nuevo certificado.
   * Cambiar la fecha de expiración de hello para la configuración de escritorio remoto de Hola.

5. Después terminar las actualizaciones de la configuración, haga clic en **Aceptar** (marca de verificación).

## <a name="remote-into-role-instances"></a>Acceso remoto en instancias de rol
Una vez que Escritorio remoto está habilitado en los roles de hello puede remoto en una instancia de rol a través de varias herramientas.

instancia de rol tooconnect tooa de hello portal de Azure clásico:

1. Haga clic en **instancias** tooopen hello **instancias** página.
2. Seleccione una instancia de rol que tenga el Escritorio remoto configurado.
3. Haga clic en **conectar**y siga el escritorio de hello instrucciones tooopen Hola.
4. Haga clic en **abiertos** y, a continuación, **conectar** toostart Hola conexión a Escritorio remoto.

### <a name="use-visual-studio-tooremote-into-a-role-instance"></a>Usar Visual Studio tooremote en una instancia de rol
En el Explorador de servidores de Visual Studio:

1. Expanda hello **Azure** > **servicios en la nube** > **[nombre de servicio de nube]** nodo.
2. Expanda **Almacenamiento provisional** o **Producción**.
3. Expanda el rol individual Hola.
4. Haga clic en una de las instancias de rol de hello, haga clic en **conectar utilizando Escritorio remoto...** y, a continuación, escriba Hola nombre de usuario y una contraseña.

![Escritorio remoto del Explorador de servidores](./media/cloud-services-role-enable-remote-desktop/ServerExplorer_RemoteDesktop.png)

### <a name="use-powershell-tooget-hello-rdp-file"></a>Usar el archivo RDP de PowerShell tooget Hola
Puede usar hello [Get-AzureRemoteDesktopFile](https://msdn.microsoft.com/library/azure/dn495261.aspx) archivo RDP de cmdlet tooretrieve Hola. A continuación, puede usar archivo RDP de hello con servicio de nube de hello tooaccess de conexión a Escritorio remoto.

### <a name="programmatically-download-hello-rdp-file-through-hello-service-management-rest-api"></a>Descargar mediante programación el archivo RDP de Hola a través de la API de REST de administración de servicios de Hola
Puede usar hello [Descargar archivo RDP](https://msdn.microsoft.com/library/jj157183.aspx) archivo RDP de REST operación toodownload Hola.

## <a name="tooconfigure-remote-desktop-in-hello-service-definition-file"></a>Escritorio remoto en el archivo de definición de servicio de hello tooconfigure
Este método permite tooenable escritorio remoto para la aplicación hello durante el desarrollo. Este enfoque requiere contraseñas cifradas se almacena en la configuración del servicio archivo y cualquier configuración de escritorio remoto de toohello de actualizaciones requeriría una nueva implementación de aplicación hello. Si desea que tooavoid estas desventajas que debe usar la extensión de escritorio remoto de hello enfoque basado en que se ha descrito anteriormente.  

Puede usar Visual Studio demasiado[habilitar una conexión a escritorio remota](../vs-azure-tools-remote-desktop-roles.md) mediante el enfoque de archivo de definición de servicio de Hola.  
Hola pasos siguientes describe Hola cambios necesarios toohello servicio modelo archivos tooenable escritorio remoto. Visual Studio realizará estos cambios automáticamente al publicar.

### <a name="set-up-hello-connection-in-hello-service-model"></a>Configurar conexión de hello en el modelo de servicio de Hola
Hola de uso **importaciones** Hola de elemento tooimport **RemoteAccess** hello y módulo **RemoteForwarder** módulo toohello [ServiceDefinition.csdef](cloud-services-model-and-package.md#csdef) archivo.

Hello archivo de definición de servicio debe ser similar toohello siguiente ejemplo con hello `<Imports>` elemento agregado.

```xml
<ServiceDefinition name="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceDefinition" schemaVersion="2013-03.2.0">
    <WebRole name="WebRole1" vmsize="Small">
        <Sites>
            <Site name="Web">
                <Bindings>
                    <Binding name="Endpoint1" endpointName="Endpoint1" />
                </Bindings>
            </Site>
        </Sites>
        <Endpoints>
            <InputEndpoint name="Endpoint1" protocol="http" port="80" />
        </Endpoints>
        <Imports>
            <Import moduleName="Diagnostics" />
            <Import moduleName="RemoteAccess" />
            <Import moduleName="RemoteForwarder" />
        </Imports>
    </WebRole>
</ServiceDefinition>
```
Hola [ServiceConfiguration.cscfg](cloud-services-model-and-package.md#cscfg) archivo debe ser similar toohello siguiente ejemplo, tenga en cuenta hello `<ConfigurationSettings>` y `<Certificates>` elementos. Hola certificado especificado debe ser [cargado el servicio en la nube toohello](cloud-services-how-to-create-deploy.md#how-to-upload-a-certificate-for-a-cloud-service).

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceConfiguration serviceName="<name-of-cloud-service>" xmlns="http://schemas.microsoft.com/ServiceHosting/2008/10/ServiceConfiguration" osFamily="3" osVersion="*" schemaVersion="2013-03.2.0">
    <Role name="WebRole1">
        <Instances count="2" />
        <ConfigurationSettings>
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.Enabled" value="true" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountUsername" value="[name-of-user-account]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountEncryptedPassword" value="[base-64-encrypted-user-password]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteAccess.AccountExpiration" value="[certificate-expiration]" />
            <Setting name="Microsoft.WindowsAzure.Plugins.RemoteForwarder.Enabled" value="true" />
        </ConfigurationSettings>
        <Certificates>
            <Certificate name="Microsoft.WindowsAzure.Plugins.RemoteAccess.PasswordEncryption" thumbprint="[certificate-thumbprint]" thumbprintAlgorithm="sha1" />
        </Certificates>
    </Role>
</ServiceConfiguration>
```


## <a name="additional-resources"></a>Recursos adicionales
[¿Cómo tooConfigure servicios en la nube](cloud-services-how-to-configure.md)
[preguntas más frecuentes: los servicios de nube escritorio remoto](cloud-services-faq.md)
