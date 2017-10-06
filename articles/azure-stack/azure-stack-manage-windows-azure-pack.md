---
title: "máquinas de virtuales de Windows Azure Pack aaaManage de pila de Azure | Documentos de Microsoft"
description: "Obtenga información acerca de cómo toomanage máquinas virtuales de Windows Azure Pack (WAP) desde el portal de usuarios de hello en la pila de Azure."
services: azure-stack
documentationcenter: 
author: walterov
manager: byronr
editor: 
ms.assetid: 213c2792-d404-4b44-8340-235adf3f8f0b
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: walterov
ms.openlocfilehash: 97dbe34055667a72fddc8507ae389562e885a32e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="manage-windows-azure-pack-virtual-machines-from-azure-stack"></a>Administrar máquinas virtuales de Windows Azure Pack desde Azure Stack
Hola Kit de desarrollo de pila de Azure, puede habilitar el acceso de hello Azure pila usuario tootenant portal máquinas virtuales se ejecutan en Windows Azure Pack. Los inquilinos pueden utilizar hello Azure pila portal toomanage sus máquinas virtuales de IaaS existentes y redes virtuales. Estos recursos están disponibles en el paquete de Windows Azure a través de los componentes subyacentes de Service Provider Foundation (SPF) y Virtual Machine Manager (VMM) Hola. En concreto, los inquilinos pueden:

* Examinar los recursos.
* Examinar los valores de configuración.
* Detener o iniciar una máquina virtual.
* Conectar a máquina virtual de tooa a través del protocolo de escritorio remoto (RDP)
* Crear y administrar puntos de control.
* Eliminar máquinas virtuales y redes virtuales.

Esta funcionalidad se proporciona por hello conector de Windows Azure Pack para la pila de Azure (vista previa). Este artículo muestra cómo tooconfigure Hola connector para un entorno de pila de Azure de nodo único.

Para esta versión preliminar del conector de hello, tenga Hola siguiente:
* Usar hello conector de Windows Azure Pack únicamente en entornos de prueba (de pila de Azure y Windows Azure Pack) y no en las implementaciones de producción.
* Debe tener Windows Azure Pack Update Rollup (UR) 9.1 o una versión posterior, SPF de System Center y VMM UR 9 o posterior.
* System Center 2012 R2 o System Center 2016, pueden ser Hola VMM y los componentes de SPF.
* Debe seguir los pasos de configuración tanto en Azure Stack como en Windows Azure Pack.
* instrucciones de Hello aplican entornos de nube toonon Platform System (CPS).
* tooreview Hola problemas conocidos, consulte [solución de problemas de Microsoft Azure pila](azure-stack-troubleshooting.md).


## <a name="architecture"></a>Arquitectura
Hello siguiente diagrama muestra componentes principales de Hola de hello conector de Windows Azure Pack.

![Hola componentes del conector de Windows Azure Pack](media/azure-stack-manage-wap/image1.png)

Tenga en cuenta Hola detalles siguientes:
* portal de usuarios de Azure pila Hello tiene acceso a información de recursos de Hola de tanto a las nubes (pila de Azure y Windows Azure Pack).
* usuario de Hello debe tener una cuenta que sea válida en ambos entornos.
* portal de usuarios de Hello Azure pila debe tener los componentes de toohello de acceso de red que se ejecutan en Windows Azure Pack.
* Hola **WAP** sección de diagrama de hello, que permite ver Hola nuevo conector de Windows Azure Pack módulos (extensión de WAP y conector) y Hola existente Windows Azure Pack API de inquilinos con componentes de SPF y VMM.


## <a name="identity-management"></a>Administración de identidades
Hola API de inquilino de Windows Azure Pack debe confiar en hello servicio de token de seguridad (STS) de pila de Azure.

Cuando un usuario realiza una acción a través del portal de Azure pila Hola destinado a los recursos de Windows Azure Pack, portal de hello usa Hola API de inquilino de Windows Azure Pack. Por lo tanto, token de autenticación de usuario de hello proporcionado debe proceder de un STS de confianza. Vea Hola siguiente diagrama:

![Diagrama de autenticación del conector de Windows Azure Pack](media/azure-stack-manage-wap/image2.png)

En el entorno de kit de desarrollo de hello, Windows Azure Pack y la pila de Azure tengan proveedores de identidad independiente. Usuarios con acceso a ambos entornos de portal de Azure pila Hola deben tener Hola nombre el mismo nombre principal de usuario (UPN) en ambos proveedores de identidad. Por ejemplo, Hola cuenta  *azurestackadmin@azurestack.local*  también deben existir en hello STS para Windows Azure Pack. Cuando AD FS no se establece toosupport las relaciones de confianza saliente, se establecerá la confianza de hello Windows Azure Pack componentes (API de inquilinos) toohello Azure pila instancia de AD FS.

## <a name="prerequisites"></a>Requisitos previos

### <a name="download-hello-windows-azure-pack-connector"></a>Descargar Hola conector de Windows Azure Pack
En hello [Microsoft Download Center](https://aka.ms/wapconnectorazurestackdlc), descargue el archivo .exe de hello y extráigalo tooyour de equipo local. Una versión posterior, copie Hola contenido tooa, equipo que puede tener acceso a su entorno de Windows Azure Pack.

### <a name="deployment-option-requirement"></a>Requisito de opción de implementación
toointegrate con Windows Azure Pack, puede implementar Azure pila utilizando la opción de AD FS de Hola o hello Azure Active Directory.

### <a name="connectivity-requirements"></a>Requisitos de conectividad
1. Desde el equipo de hello en el que obtener acceso a portal de usuarios de Azure pila hello, asegúrese de que puede tener acceso a portal del inquilino de Windows Azure Pack Hola a través del explorador web de Hola.
2. máquina virtual de Hello AzS WASP01 en pila de Azure debe ser equipo portal del inquilino de Windows Azure Pack toohello tooconnect pueda. Usar la conectividad de red de tooverify Ping.exe. 
3.  Debe tener los certificados válidos para los servicios del conector nuevo Hola. Estos certificados SSL deben emitirlos una entidad de certificación (CA) de confianza. No puede usar certificados autofirmados. certificados SSL de Hello deben ser de confianza por la pila de Azure (específicamente Hola AzS WASP01 VM) y cualquier otro equipo que Hola inquilinos puede usar el portal de usuarios de Azure pila tooaccess Hola.
 
    >[!NOTE]
    Como AzS WASP01 ejecuta Windows Server con la opción de instalación Server Core de hello, puede usar una herramienta de línea de comandos como certificado de Certutil.ext tooimport Hola. Por ejemplo, podría copiar tooc:\temp de archivo .cer de hello en AzS WASP01 y, a continuación, ejecute el comando de hello **certutil - addstore "CA" "c:\temp\certname.cer"**.

4.  tooestablish RDP conectividad tooWindows máquinas virtuales de Azure Pack inquilinos a través del portal de Azure pila hello, entorno de Windows Azure Pack Hola debe permitir que las máquinas virtuales de inquilinos de toohello del tráfico de escritorio remoto.
5.  Para la conectividad entre máquinas virtuales de inquilinos de pila de Azure y máquinas virtuales de inquilinos de Windows Azure Pack, sus direcciones IP externas deben ser enrutables en dos entornos de Hola. Esta conectividad, podría incluir también asociar una nombres de DNS server tooresolve máquina virtual entre entornos de Hola.

### <a name="iis-requirements"></a>Requisitos de IIS
equipo de Hola que hospeda el portal del inquilino de Windows Azure Pack hello (que puede ser un host físico, una máquina virtual o varias máquinas virtuales) debe tener la extensión de IIS de reescritura de dirección URL de hello instalado. Si aún no está instalada, puede descargarla [aquí](https://www.iis.net/downloads/microsoft/url-rewrite). Si varias máquinas virtuales hospedar el portal del inquilino de hello, instale la extensión de hello en cada máquina virtual.

## <a name="configure-azure-stack"></a>Configurar Azure Stack
Antes de configurar Hola conector de Windows Azure Pack, debe habilitar el modo de varias nube en el portal de usuarios de Azure pila Hola. Este modo permite tooselect a los usuarios de los recursos que tooaccess en la nube.

modo de varias nubes tooenable, debe ejecutar hello AzurePackConnector.ps1 agregar script después de la implementación de la pila de Azure. Hello en la tabla siguiente describe los parámetros de script de Hola.


|  Parámetro | Description | Ejemplo |   
| -------- | ------------- | ------- |  
| AzurePackClouds | URI de hello conectores de Windows Azure Pack. Estos URI deberían corresponder toohello portales de inquilinos de Windows Azure Pack. | @{CloudName = "AzurePack1"; CloudEndpoint = "https://waptenantportal1:40005"},@{CloudName = "AzurePack2"; CloudEndpoint = "https://waptenantportal2:40005"}<br><br>  (De forma predeterminada, el valor del puerto de hello es 40005). |  
| AzureStackCloudName | Etiqueta toorepresent Hola local pila de Azure en la nube.| "AzureStack" |
| DisableMultiCloud | Un modo de varias nubes toodisable de conmutador.| N/D |
| | |

Puede ejecutar script de Hola AzurePackConnector.ps1 agregar inmediatamente después de la implementación, o una versión posterior. toorun Hola implementación inmediatamente después de secuencia de comandos, utilice Hola misma sesión de Windows PowerShell donde completa la implementación de la pila de Azure. En caso contrario, puede abrir una nueva sesión de Windows PowerShell como administrador (iniciado sesión como cuenta de hello azurestackadmin).

1. Ejecutar script de Hola AzurePackConnector.ps1 agregar mediante Hola después de comandos (con el entorno de tooyour específico de valores). Tenga en cuenta que script de Hola agregar AzurePackConnector permite tooadd más de un extremo de conector de Windows Azure Pack.
 
 ```powershell
    $cred = New-Object System.Management.Automation.PSCredential("cloudadmin@azurestack.local", `
    (ConvertTo-SecureString -String "<password>" -AsPlainText -Force))
    $session = New-PSSession -ComputerName 'azs-ercs01' `
     -Credential $cred `
     -ConfigurationName PrivilegedEndpoint `
     -Authentication Credssp

    # Enable Multicloud
    Invoke-Command -Session $session -ScriptBlock { Add-AzurePackConnector -AzurePackClouds `
    @{CloudName = "AzurePack_1"; CloudEndpoint = "https://waptenantportal1:40005"},`
    @{CloudName = "AzurePack_2"; CloudEndpoint = "https://waptenantportal2:40005" } `
    -AzureStackCloudName "AzureStack" }

 ```
> [!NOTE]
> En la compilación actual Hola hay un problema donde una vez finalizado el Hola AzurePackConnector Agregar secuencia de comandos, permanece en un bucle de sondeo durante un largo período de tiempo (varios minutos) hasta que termina. Una vez que aparezca el mensaje de bienvenida de **VERBOSE: paso 'Configurar el conector del módulo de Azure' estado: 'Correcto'**, puede detener la secuencia de comandos de Hola o esperar hasta que se detenga por sí mismo. Dado que la configuración de hello ya se ha realizado correctamente no suponer una diferencia.

2. Tome nota de los archivos de salida de hello generados por este script, uno para cada entorno de Windows Azure Pack que especificó. Hello archivos se encuentran en: \\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput. Estos archivos contienen información de Hola que sea necesario tooconfigure Hola destino Windows Azure Pack entornos. Este archivo se pasa como una secuencia de comandos de tooa de parámetro más adelante en estas instrucciones. Este archivo contiene Hola siguiente información:

    * **AzurePackConnectorEndpoint**: contiene el servicio de conector de Windows Azure Pack toohello de hello punto de conexión.
    * **AuthenticationIdentityProviderPartner**: contiene Hola siguiente par de valor:
        * Token de autenticación, firma el certificado que Hola API de inquilino de Windows Azure Pack debe tootrust tooaccept llamadas de hello extensión del portal de pila de Azure.

        * Hola "Territorio" asociado Hola certificado de firma. Por ejemplo: https://adfs.local.azurestack.global.external/adfs/c1d72562-534e-4aa5-92aa-d65df289a107/.

3.  Examinar las carpetas de toohello que contiene los archivos de salida de hello (\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput) y el equipo local de copia Hola archivos tooyour. archivos de Hello tendrá un aspecto similar toothis: AzurePack-06-27-15-50.txt.

4.  Configuración de Hola de prueba.

    a. Abra el explorador e inicie sesión en el portal de usuarios de Azure pila toohello (https://portal.local.azurestack.external/).
    
    b. Después de iniciar sesión como una carga de portal hello e inquilino, verá errores acerca de no ser capaz de toofetch suscripciones o las extensiones de hello nube de Azure Pack. Haga clic en **Aceptar** tooclose estos mensajes. (Estos mensajes de error desaparecerán después de configurar Windows Azure Pack).

    c. Hola aviso **nube** lista desplegable situada en la esquina superior izquierda de hello del portal de Hola.

    ![selector de Hello en la nube en la interfaz de usuario de Azure pila Hola](media/azure-stack-manage-wap/image3.png)

## <a name="configure-windows-azure-pack"></a>Configurar Windows Azure Pack
Solo para esta versión preliminar del conector, Windows Azure Pack se debe configurar manualmente.

>[!IMPORTANT]
En esta versión de vista previa, utilice Hola conector de Windows Azure Pack únicamente en entornos de prueba y no en las implementaciones de producción.

1.  Instalar archivos de MSI de conector en hello Windows Azure Pack portal las máquinas virtuales e instalar certificados. (Si tiene varias máquinas virtuales del portal de inquilinos, debe completar este paso en cada máquina virtual).

    a. En el Explorador de archivos, copie hello **WAPConnector** carpeta (lo que descargó anteriormente) con el nombre de carpeta de tooa **c:\temp** en hello portal las máquinas virtuales.

    b. Abra una consola o RDP conexión toohello inquilino portal máquina virtual.

    c. Cambie los directorios demasiado**c:\temp\wapconnector\setup\scripts**, ejecución hello y **Install-Connector.ps1** tooinstall tres MSI archivos de script. No hay ningún parámetro obligatorio.

     ```powershell
    cd C:\temp\wapconnector\setup\scripts\

    .\Install-Connector.ps1
    ```
     d. Cambie los directorios demasiado**c:\inetpub** y compruebe que se instalan nuevos sitios de tres hello:

       * MgmtSvc-Connector

       * MgmtSvc-ConnectorExtension

       * MgmtSvc-ConnectorController

    e. De Hola mismo **c:\temp\wapconnector\setup\scripts** carpeta, ejecute hello **Certificates.ps1 configurar** tooinstall certificados de secuencias de comandos. De forma predeterminada, usará Hola mismo certificado que está disponible para el sitio del Portal del inquilino de hello en Windows Azure Pack. Asegúrese de que se trata de un certificado válido (de confianza por máquina virtual de Azure de pila AzS WASP01 de Hola y todos los equipos cliente que tiene acceso a portal de Azure pila hello). En caso contrario, no funcionará la comunicación. (Como alternativa, puede pasar explícitamente una huella digital del certificado como un parámetro mediante el uso de Hola - parámetro de huella digital.)

     ```powershell
        cd C:\temp\wapconnector\setup\scripts\

        .\Configure-Certificates.ps1
    ```

    f. configuración de hello toofinish de estos tres servicios, ejecute hello **WapConnector.ps1 configurar** tooupdate Hola Web.config archivo parámetros de script.

    |  Parámetro | Description | Ejemplo |   
    | -------- | ------------- | ------- |  
    | TenantPortalFQDN | portal del inquilino Windows Azure Pack Hola FQDN. | tenant.contoso.com | 
    | TenantAPIFQDN | Hola FQDN de API de inquilino de Windows Azure Pack. | tenantapi.contoso.com  |
    | AzureStackPortalFQDN | portal de usuarios de Azure pila de Hello FQDN. | portal.local.azurestack.external |
    | | |
    
     ```powershell
    .\Configure-WapConnector.ps1 -TenantPortalFQDN "tenant.contoso.com" `
         -TenantAPIFQDN "tenantapi.contoso.com" `
         -AzureStackPortalFQDN "portal.local.azurestack.external"
    ```
    g. Si tiene varias máquinas virtuales del portal de inquilinos, repita el paso 1 para cada una de ellas.

2. Instalación Hola nuevo MSI de API de inquilinos en cada máquina virtual de API de inquilino de Windows Azure Pack.

    a. Si está usando un equilibrador de carga, puede que desee toomark Hola virtual machine como sin conexión.

    b. En el Explorador de archivos, copie hello **WAPConnector** tooa carpeta denominado **c:\temp** en cada equipo de la API de inquilinos.

    c. Archivo de copia hello AzurePackConnectorOutput.txt que guardó anteriormente, demasiado**c:\temp\WAPConnector**.

    d. Abra una conexión RDP o consola toohello VM de API de inquilinos ha copiado los archivos de Hola a.
    
    e. Cambie los directorios demasiado**c:\temp\wapconnector\setup\scripts**y ejecute **TenantAPI.ps1 actualización**. Esta nueva versión de API de inquilinos de WAP hello contiene un tooenable de cambio de una relación de confianza no sólo con STS actual de hello, sino también con la instancia de Hola de AD FS en la pila de Azure.

     ```powershell
    cd C:\temp\wapconnector\setup\packages\

    .\Update-TenantAPI.ps1
    ```

    f.  Repita el paso 2 en cualquier otra máquina virtual ejecuta Hola API de inquilinos.
3. De **sola** de hello máquinas virtuales de API de inquilino, ejecutar hello TrustAzureStack.ps1 Configurar secuencia de comandos tooadd una relación de confianza entre Hola API de inquilinos y la instancia de hello AD FS en la pila de Azure. Debe usar una cuenta con la base de datos Microsoft.MgmtSvc.Store toohello de acceso de administrador del sistema. Esta secuencia de comandos tiene Hola parámetros siguientes:

    | Parámetro | Description | Ejemplo |
    | --------- | ------------| ------- |
   | SqlServer | nombre de Hola de SQL Server que contiene la base de datos de hello Microsoft.MgmtSvc.Store Hola. Este parámetro es obligatorio. | SQLServer | 
   | DataFile | archivo de salida de Hello que se generó durante la configuración de hello del modo de hello Azure pila varias nube anteriormente. Este parámetro es obligatorio. | AzurePack-06-27-15-50.txt | 
   | PromptForSqlCredential | Indica que el script de Hola debe solicitarle interactivamente un toouse de credencial de autenticación de SQL cuando se conecta la instancia de SQL Server toohello. Hola proporcionado credenciales debe tener suficientes permisos toouninstall bases de datos, esquemas y eliminar los inicios de sesión de usuario. Si no se proporciona ninguno, el script de Hola asume que ese contexto de usuario actual tiene acceso. | No se necesita ningún valor. |
   |  |  |

    Si no sabe hello toouse de SQL Server, puede detectarlo. Conectar el equipo de API de inquilinos toohello, usar Hola Unprotect-MgmtSvc comando toounprotect Hola Web.config de la API de inquilino archivo y busque el nombre del servidor hello en la cadena de conexión de Hola. Recuerde toorun MgmtSvc proteger nuevo archivo Web.config de la API de inquilino de tooprotect hello.

  ```powershell
  cd C:\temp\wapconnector\setup\scripts\

 .\Configure-TrustAzureStack.ps1 -SqlServer "SQLServer" `
       -DataFile "C:\temp\wapconnector\AzurePackConnectorOutput.txt"
  ```

## <a name="example"></a>Ejemplo
Hello en el ejemplo siguiente se muestra una implementación completa de conector de Windows Azure Pack en una configuración de la pila de Azure de nodo único y dos instalaciones de Windows Azure Pack Express. (Cada instalación de Express se encuentra en un único equipo, con los nombres de ejemplo de Hola *wapcomputer1* y*wapcomputer2*.)

```powershell
# Run hello following script on hello Azure Stack host
$cred = New-Object System.Management.Automation.PSCredential("cloudadmin@azurestack.local",`
     (ConvertTo-SecureString -String "p@ssw0rd" -AsPlainText -Force))
$session = New-PSSession -ComputerName 'azs-ercs01' -Credential $cred `
     -ConfigurationName PrivilegedEndpoint -Authentication Credssp
 
# Enable Multicloud
invoke-command -Session $session -ScriptBlock { Add-AzurePackConnector -AzurePackClouds `
     @{CloudName = "AzurePack_1"; CloudEndpoint = "https://wapcomputer1.contoso.com:40005"},`
     @{CloudName = "AzurePack_2"; CloudEndpoint = "https://wapcomputer2.contoso.com:40005"}`
     -AzureStackCloudName "AzureStack" }  

```
Descargar el archivo .exe de hello de hello [Microsoft Download Center](https://aka.ms/wapconnectorazurestackdlc), extráigalo y copie hello WAPConnector carpeta tooa **c:\temp** carpeta en el equipo de Windows Azure Pack Hola. Copie los archivos de Hola que se generaron como resultado en la secuencia de comandos anterior hello (ubicado en \\\su1fileserver\SU1_Infrastructure_1\AzurePackConnectorOutput) toohello **c:\temp\WAPConnector** carpeta. (archivos Hola se parece similar toothis: AzurePack-06-27-15-50.txt.) A continuación, ejecute hello siguiente secuencia de comandos, una vez por instancia de Windows Azure Pack:

 ```powershell
# Install Connector components
cd C:\temp\WAPConnector\Setup\Scripts
.\Install-Connector.ps1

# Configure Certificates for hello new Connector services
.\Configure-Certificates.ps1

# Configure hello Connector services
.\Configure-WapConnector.ps1 -TenantPortalFQDN "wapcomputer1.contoso.com" `
     -TenantAPIFQDN "wapcomputer1.contoso.com" `
     -AzureStackPortalFQDN "portal.local.azurestack.external"

# Install hello updated TenantAPI
.\Update-TenantAPI.ps1

# Establish trust with hello Azure Stack AD FS
.\Configure-TrustAzureStack.ps1 -SqlServer "wapcomputer1" `
     -DataFile "C:\temp\wapconnector\AzurePack-06-27-15-50.txt" 

```
## <a name="troubleshooting-tips"></a>Sugerencias de solución de problemas
1.  Asegúrese de que haya conectividad de red entre Azure Stack y Windows Azure Pack. Esta conectividad debe estar entre cualquier equipo de inquilino que tiene acceso a portal de Azure pila Hola y Hola Windows Azure Pack portal las máquinas virtuales donde se ejecutan los servicios del conector nuevo Hola.
2.  Asegúrese de que todos los FQDN especificados sean correctos.
3.  Asegúrese de que son de confianza certificados SSL de Hola se usan en los servicios del conector nuevo hello en pila de Azure (específicamente Hola AzS WASP01 VM) y otro inquilino de Hola de equipo puede usar el portal de usuarios de Azure pila tooaccess Hola.
4. Para revisar los problemas conocidos, vea [Microsoft Azure Stack troubleshooting](azure-stack-troubleshooting.md) (Solución de problemas de Microsoft Azure Stack).


## <a name="next-steps"></a>Pasos siguientes
[Uso de portales de administrador y usuario de hello en la pila de Azure](azure-stack-manage-portals.md)
