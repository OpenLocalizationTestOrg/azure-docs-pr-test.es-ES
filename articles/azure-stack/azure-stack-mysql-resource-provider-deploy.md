---
title: las bases de datos MySQL aaaUse como PaaS en pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo puede implementar el proveedor de recursos MySQL hello y proporcionan bases de datos de MySQL como servicio en la pila de Azure"
services: azure-stack
documentationCenter: 
author: JeffGoldner
manager: bradleyb
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: JeffGo
ms.openlocfilehash: 634e408eae9f3d8257a8610c60def0978ce333c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-mysql-databases-on-microsoft-azure-stack"></a>Usar bases de datos MySQL en Microsoft Azure Stack


Puede implementar un proveedor de recursos MySQL en Azure Stack. Después de implementar el proveedor de recursos de hello, puede crear servidores MySQL Server y bases de datos mediante plantillas de implementación del Administrador de recursos de Azure y proporcionar las bases de datos de MySQL como un servicio. Las bases de datos MySQL, que son comunes en los sitios web, admiten muchas plataformas de sitio web. Por ejemplo, después de implementar el proveedor de recursos de hello, puede crear sitios Web de WordPress de plataforma de aplicaciones Web de Azure Hola como un complemento de servicio (PaaS) para la pila de Azure.

proveedor de MySQL toodeploy hello en un sistema que no tiene acceso a internet, puede copiar el archivo hello [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Download/sConnector-Net/mysql-connector-net-6.9.9.msi) tooa local comparte y proporcionar ese nombre de recurso compartido cuando se le solicite (ver abajo). También debe instalar los módulos de Azure y Azure PowerShell de pila de Hola.


## <a name="mysql-server-resource-provider-adapter-architecture"></a>Arquitectura de adaptador del proveedor de recursos MySQL Server

proveedor de recursos de Hola se compone de tres componentes:

- **adaptador de proveedor de recursos de MySQL de Hello VM**, que es una máquina virtual de Windows ejecuta Servicios de proveedor de Hola.
- **proveedor de recursos de Hello propio**, que procesa las solicitudes de aprovisionamiento y expone recursos de base de datos.
- **Los servidores que hospedan MySQL Server**, que proporcionan capacidad para las bases de datos, conocidos como servidores host. 

Esta versión ya no crea una instancia de MySQL. Debe crearlos y proporcionar acceso a instancias de SQL tooexternal. Puede visitar hello [Galería de inicio rápido de Azure pila](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) para una plantilla de ejemplo que puede crear un servidor de MySQL para usted o descargar e implementar un servidor MySQL de hello Marketplace.

## <a name="deploy-hello-resource-provider"></a>Implementar el proveedor de recursos de Hola

1. Si no lo ha hecho ya, registre el kit de desarrollo y descargue Hola centro de datos de Windows Server 2016 - Eval imagen que se pueden descargar a través de administración de Marketplace. También puede utilizar una secuencia de comandos toocreate un [imagen de Windows Server 2016](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image).

2. [Descargar archivo de los archivos binarios del proveedor de recursos de hello MySQL](https://aka.ms/azurestackmysqlrp) y extraerlo en el host de kit de desarrollo de Hola.

3. Inicie sesión en el host de kit de desarrollo de toohello y extraer Hola directorio temporal del tooa de archivo instalador MySQL RP.

4. certificado de raíz de Hello Azure pila se recuperan y se crea un certificado autofirmado como parte de este proceso. 

    __Opcional:__ si necesita tooprovide su propietario, preparar certificados hello y copiar el directorio local de tooa si desea toocustomize certificados hello (script de instalación toohello pasado). Necesita Hola siguiente:

    a. Un certificado comodín para *.dbadapter.\<región\>.\<fqdn externo\>. Este certificado debe ser de confianza, como podría ser emitido por una entidad de certificación (es decir, cadena Hola de confianza debe existir sin necesidad de certificados intermedios). (Un certificado de sitio solo puede utilizarse con nombre VM explícito Hola que proporcionar durante la instalación).

    b. certificado de raíz de Hello utilizado por hello Azure Resource Manager para la instancia de la pila de Azure. Si no se encuentra, se recuperará el certificado de raíz de Hola.

5. Abra un **nueva** elevados de PowerShell de la consola y cambie el directorio de toohello donde extrajo los archivos de Hola. Usar un nuevo tooavoid problemas de ventana que pueden surgir de módulos de PowerShell incorrectos ya están cargados en el sistema de Hola.

6. Si ha instalado cualquier versión de Hola AzureRm o AzureStack PowerShell módulos que no sean 1.2.9 o 1.2.10, es posible que tooremove solicitada ellos u Hola instalación no continuará. Se incluyen las versiones 1.3 o posterior.

7. Ejecute DeployMySqlProvider.ps1.

Este script sigue estos pasos:

* Si es necesario, descargue una versión compatible de Azure PowerShell.
* Descargue Hola MySQL connector binario (Esto puede proporcionar sin conexión).
* Cargar certificado de Hola y todos los demás tooan artefactos cuenta de almacenamiento de la pila de Azure.
* Publicar paquetes de la Galería para que pueda implementar bases de datos de MySQL a través de la Galería de Hola.
* Implemente una máquina virtual (VM) que hospede al proveedor de recursos.
* Registrar un registro DNS local que se asigna el proveedor de recursos de tooyour máquina virtual.
* Registre el proveedor de recursos con hello Azure Resource Manager local.

Especifique al menos Hola parámetros necesarios en la línea de comandos de hello, o bien, si se ejecuta sin ningún parámetro, son tooenter solicitada ellos. 

Este es un ejemplo que se puede ejecutar desde Hola PowerShell solicite (pero cambiar extremos de información y el portal de la cuenta de hello según sea necesario):


```
# Install hello AzureRM.Bootstrapper module
Install-Module -Name AzureRm.BootStrapper -Force

# Installs and imports hello API Version Profile required by Azure Stack into hello current PowerShell session.
Use-AzureRmProfile -Profile 2017-03-09-profile
Install-Module -Name AzureStack -RequiredVersion 1.2.10 -Force

# Download hello Azure Stack Tools from GitHub and set hello environment
cd c:\
Invoke-Webrequest https://github.com/Azure/AzureStack-Tools/archive/master.zip -OutFile master.zip
Expand-Archive master.zip -DestinationPath . -Force

# This endpoint may be different for your installation
Import-Module C:\AzureStack-Tools-master\Connect\AzureStack.Connect.psm1
Add-AzureRmEnvironment -Name AzureStackAdmin -ArmEndpoint "https://adminmanagement.local.azurestack.external" 

# For AAD, use hello following
$tenantID = Get-AzsDirectoryTenantID -AADTenantName "<your directory name>" -EnvironmentName AzureStackAdmin

# For ADFS, replace hello previous line with
# $tenantID = Get-AzsDirectoryTenantID -ADFS -EnvironmentName AzureStackAdmin

$vmLocalAdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("mysqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory toohello folder where you extracted hello installation files 
# and adjust hello endpoints
<extracted file directory>\DeployMySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "MySqlRG" -VmName "MySQLRP" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass -DependencyFilesLocalPath
 ```

### <a name="deploymysqlproviderps1-parameters"></a>Parámetros de DeployMySqlProvider.ps1

Puede especificar estos parámetros en la línea de comandos de Hola. Si no lo hace, o se produce un error en cualquier validación de parámetros, se le solicitará tooprovide Hola requiere los.

| Nombre de parámetro | Descripción | Comentario o valor predeterminado |
| --- | --- | --- |
| **DirectoryTenantID** | Hola Azure o Id. de directorio de AD FS (guid) | _obligatorio_ |
| **ArmEndpoint** | Hello Azure pila administrativo Administrador de recursos del extremo de Azure | _obligatorio_ |
| **TenantArmEndpoint** | Hello Azure pila Azure Administrador de recursos del extremo del inquilino | _obligatorio_ |
| **AzCredential** | Credencial de la cuenta de administrador de servicios de pila Azure (Hola de uso misma cuenta que usó para la implementación de pila de Azure) | _obligatorio_ |
| **VMLocalCredential** | cuenta de administrador local de Hola de proveedor de recursos de MySQL de hello VM | _obligatorio_ |
| **ResourceGroupName** | Grupo de recursos para los elementos de hello creados por esta secuencia de comandos |  _obligatorio_ |
| **VmName** | Nombre de explotación de VM de hello proveedor de recursos de Hola |  _obligatorio_ |
| **AcceptLicense** | Omite Hola tooaccept prompt Hola licencia de GPL (http://www.gnu.org/licenses/old-licenses/gpl-2.0.html) | |
| **DependencyFilesLocalPath** | Recurso compartido local que contiene de ruta de acceso tooa [mysql-connector-net-6.9.9.msi](https://dev.mysql.com/get/Downloads/Connector-Net/mysql-connector-net-6.9.9.msi). Si proporciona los archivos de certificados, se deben colocar también en este directorio. | _opcional_ |
| **DefaultSSLCertificatePassword** | contraseña de Hello para el archivo de certificado .pfx Hola | _obligatorio_ |
| **MaxRetryCount** | Se vuelve a intentar cada operación si se produce un error. | 2 |
| **RetryDuration** | Tiempo de expiración entre reintentos, en segundos | 120 |
| **Desinstalación** | Quitar proveedor de recursos de Hola | No |
| **DebugMode** | Impide la limpieza automática en caso de error. | No |


Función de velocidades de rendimiento y descarga de sistema de hello, instalación puede tardar tan sólo como 20 minutos o como larga como varias horas. Debe actualizar el portal de administración de hello si hoja de hello MySQLAdapter no está disponible.

> [!NOTE]
> Si la instalación de hello tiene más de 90 minutos, se puede producir un error y verá un mensaje de error en la pantalla de bienvenida y en el archivo de registro de hello. implementación de Hola se reintenta de hello errores paso. Sistemas que no cumplen Hola memoria recomendada y las especificaciones principales pueden no ser capaz de toodeploy Hola MySQL RP.


## <a name="provide-capacity-by-connecting-tooa-mysql-hosting-server"></a>Proporcionar una capacidad mediante la conexión de servidor de hospedaje de MySQL tooa

1. Inicie sesión en toohello portal de la pila de Azure como un administrador del servicio.

2. Haga clic en **Proveedores de recursos** &gt; **MySQLAdapter** &gt; **Hosting Servers** (Servidores host)&gt; **+Agregar**.

    Hola **servidores de hospedaje de MySQL** hoja es donde puede conectar Hola proveedor de recursos de MySQL Server tooactual instancias de MySQL Server que actúan como Hola back-end del proveedor de recursos.

    ![Servidores de hospedaje](./media/azure-stack-mysql-rp-deploy/mysql-add-hosting-server-2.png)

3. Rellenar el formulario de hello con detalles de la conexión de saludo de la instancia del servidor MySQL. Proporcione el nombre de dominio completo (FQDN) de Hola o una dirección IPv4 válida y no Hola VM nombre corto. Esta instalación ya no proporciona una instancia de MySQL predeterminada. Hola tamaño proporciona ayuda a proveedor de recursos de Hola a administrar la capacidad de la base de datos de Hola. Debe ser toohello cerrar la capacidad física del servidor de base de datos de Hola.

    > [!NOTE]
    > Siempre que puede tener acceso a la instancia de MySQL de Hola por inquilino hello y administración de Azure Resource Manager, se puede colocar bajo el control de proveedor de recursos de Hola. instancia de MySQL de Hello __debe__ asignar exclusivamente toohello RP.

4. Cuando agregue servidores, debe asignarlos tooa nueva o existente SKU tooallow diferenciación de ofertas de servicio. Por ejemplo, podría tener una instancia de enterprise proporciona capacidad de la base de datos y copia de seguridad automática, reservar servidores de alto rendimiento para que los departamentos individuales, nombre de SKU de hello etc. debe reflejar propiedades Hola para que los inquilinos pueden colocar sus bases de datos correctamente y deben tener todos los servidores de hospedaje en una SKU hello las mismas capacidades.

    ![Crear una SKU de MySQL](./media/azure-stack-mysql-rp-deploy/mysql-new-sku.png)


>[!NOTE]
SKU pueden tardar hasta tooan hora toobe visible en el portal de Hola. No se puede crear una base de datos hasta que Hola que SKU se crea.


## <a name="create-your-first-mysql-database-tootest-your-deployment"></a>Crear la implementación de su primera tootest de base de datos de MySQL


1. Inicie sesión en toohello portal de la pila de Azure como administrador del servicio.

2. Haga clic en hello **+ nuevo** botón &gt; **datos + almacenamiento** &gt; **(vista previa) de base de datos de MySQL**.

3. Rellene el formulario de hello con detalles de la base de datos de Hola.

    ![Crear una base de datos MySQL de prueba](./media/azure-stack-mysql-rp-deploy/mysql-create-db.png)

4. Seleccione una SKU.

    ![Seleccionar una SKU](./media/azure-stack-mysql-rp-deploy/mysql-select-a-sku.png)

5. Cree una configuración de inicio de sesión. se puede reutilizar la configuración de inicio de sesión de Hola o crea uno nuevo. Esto contiene el nombre de usuario de Hola y la contraseña de la base de datos de Hola.

    ![Creación de un nuevo inicio de sesión en la base de datos](./media/azure-stack-mysql-rp-deploy/create-new-login.png)

    cadena de conexión de Hello incluye el nombre del servidor de base de datos reales de Hola. Copiarlo desde el portal de Hola.

    ![Obtener la cadena de conexión de hello para la base de datos de MySQL Hola](./media/azure-stack-mysql-rp-deploy/mysql-db-created.png)

> [!NOTE]
> longitud de Hola Hola de nombres de usuario no puede superar los 32 caracteres con MySQL 5.7 o en versiones anteriores de 16 caracteres. Se trata de una limitación de las implementaciones de MySQL de Hola.


## <a name="add-capacity"></a>Ampliación de capacidad

Agregar más capacidad al agregar más servidores de MySQL en el portal de Azure pila Hola. Si desea toouse otra instancia de MySQL, haga clic en **proveedores de recursos** &gt; **MySQLAdapter** &gt; **servidores de hospedaje de MySQL** &gt; **+ Agregar**.


## <a name="making-mysql-databases-available-tootenants"></a>Hacer que las bases de datos de MySQL tootenants disponibles
Crear planes y ofertas toomake bases de datos de MySQL disponibles para los inquilinos. Agregar servicio de hello Microsoft.MySqlAdapter, agregue una cuota, etcetera.

![Crear planes y ofertas tooinclude bases de datos](./media/azure-stack-mysql-rp-deploy/mysql-new-plan.png)

## <a name="removing-hello-mysql-adapter-resource-provider"></a>Quitar Hola proveedor de recursos de adaptador de MySQL

proveedor de recursos de tooremove hello, es esencial toofirst quitar todas las dependencias.

1. Asegúrese de que haya original paquete de implementación de Hola que has descargado para esta versión de Hola proveedor de recursos.

2. Todas las bases de datos de inquilino deben eliminarse del proveedor de recursos de hello (Esto no eliminará los datos de hello). Esto debe realizarse por parte de inquilinos Hola por sí mismos.

3. Deben anular el registro de los inquilinos del espacio de nombres de Hola.

4. Administrador debe eliminar Hola servidores de MySQL adaptador Hola de hospedaje

5. Administrador debe eliminar los planes que hacen referencia a Hola adaptador de MySQL.

6. Administrador debe eliminar cualquier toohello asociado el adaptador de MySQL de cuotas.

7. Vuelva a ejecutar el script de implementación de hello con hello - desinstalar parámetro, los puntos de conexión de Azure Resource Manager, DirectoryTenantID y las credenciales de cuenta de administrador del servicio de Hola.




## <a name="next-steps"></a>Pasos siguientes


Pruebe otros [servicios PaaS](azure-stack-tools-paas-services.md) como hello [proveedor de recursos de SQL Server](azure-stack-sql-resource-provider-deploy.md) hello y [proveedor de recursos de servicios de aplicaciones](azure-stack-app-service-overview.md).
