---
title: aaaUsing SQL bases de datos en la pila de Azure | Documentos de Microsoft
description: "Obtenga información acerca de cómo puede implementar las bases de datos SQL como un servicio en la pila de Azure y adaptador de proveedor de recursos de SQL Server de hello pasos rápidos toodeploy Hola"
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
ms.openlocfilehash: 01418ce7cd708ca8f9e302d6bcd2a43ad33df93f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="use-sql-databases-on-microsoft-azure-stack"></a>Uso de bases de datos SQL en Microsoft Azure Stack


Usar Hola SQL Server recursos proveedor adaptador tooexpose bases de datos SQL como un servicio de pila de Azure. Después de instalar el proveedor de recursos de Hola y conéctelo a tooone o más instancias de SQL Server, usted y sus usuarios pueden crear bases de datos para aplicaciones nativas de nube y sitios Web que se basa en SQL, cargas de trabajo que se basan en SQL sin tener que tooprovision un virtual máquina (VM) que hospeda SQL Server cada vez.

proveedor de recursos de Hello no admite todas las capacidades de administración de base de datos de Hola de [base de datos de SQL Azure](https://azure.microsoft.com/services/sql-database/). Por ejemplo, no se admiten grupos elástico de base de datos y rendimiento de base de datos de hello capacidad tooscale. Hola API no es compatible con la base de datos SQL.


## <a name="sql-server-resource-provider-adapter-architecture"></a>Arquitectura del adaptador del proveedor de recursos de SQL Server
proveedor de recursos de Hello no se basa en ni ofrece todas las capacidades de administración de base de datos de Hola de base de datos de SQL Azure. Por ejemplo, grupos de bases de datos elásticas y rendimiento de base de datos de hello capacidad toodial arriba y abajo automáticamente no están disponibles. Sin embargo, Hola recursos proveedor admite similar crear, leer, actualizar y eliminar operaciones (CRUD).

proveedor de recursos de Hola se compone de tres componentes:

- **adaptador de proveedor de recursos de Hello SQL VM**, que es una máquina virtual de Windows ejecuta Servicios de proveedor de Hola.
- **proveedor de recursos de Hello propio**, que procesa las solicitudes de aprovisionamiento y expone recursos de base de datos.
- **Los servidores que hospedan SQL Server**, que proporcionan capacidad para las bases de datos, conocidos como servidores de hospedaje. 

Esta versión ya no crea una instancia de SQL. Debe crear una (o más) o proporcionar acceso a instancias de SQL tooexternal. Hay una serie de opciones tooyou disponibles incluidas las plantillas de hello [Galería de inicio rápido de Azure pila](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/mysql-standalone-server-windows) y elementos del Marketplace. 

>[!NOTE]
Si ha descargado los elementos de Marketplace de SQL, asegúrese de que también descargar Hola extensión de IaaS de SQL o estos no se implementarán.


## <a name="deploy-hello-resource-provider"></a>Implementar el proveedor de recursos de Hola

1. Si no lo ha hecho ya, registrar el kit de desarrollo y descargar la imagen de Windows Server 2016 EVAL Hola descargable a través de administración de Marketplace. También puede utilizar una secuencia de comandos toocreate un [imagen de Windows Server 2016](https://docs.microsoft.com/azure/azure-stack/azure-stack-add-default-image). en tiempo de ejecución de Hello .NET 3.5 ya no es necesario.

2. [Descargar archivo de los archivos binarios de proveedor de recursos SQL de hello](https://aka.ms/azurestacksqlrp) y extraerlo en el host de kit de desarrollo de Hola.

3. Inicie sesión en el host de kit de desarrollo de toohello y extraer Hola directorio temporal del tooa de archivo instalador SQL RP.

4. certificado de raíz de Hello Azure pila se recuperan y se crea un certificado autofirmado como parte de este proceso. 

    __Opcional:__ si necesita tooprovide su propietario, preparar certificados hello y copiar el directorio local de tooa si desea toocustomize certificados hello (script de instalación toohello pasado). Necesita Hola siguientes certificados:

    a. Un certificado comodín para *.dbadapter.\<región\>.\<fqdn externo\>. Este certificado debe ser de confianza, como podría ser emitido por una entidad de certificación (es decir, cadena Hola de confianza debe existir sin necesidad de certificados intermedios). (Un certificado de sitio solo puede utilizarse con nombre VM explícito Hola que proporcionar durante la instalación).

    b. certificado de raíz de Hello utilizado por hello Azure Resource Manager para la instancia de la pila de Azure. Si no se encuentra, se recuperará el certificado de raíz de Hola.


5. Abra un **nueva** elevados de PowerShell de la consola y cambie el directorio de toohello donde extrajo los archivos de Hola. Usar un nuevo tooavoid problemas de ventana que pueden surgir de módulos de PowerShell incorrectos ya están cargados en el sistema de Hola.

6. Si ha instalado cualquier versión de Hola AzureRm o AzureStack PowerShell módulos que no sean 1.2.9 o 1.2.10, es posible que tooremove solicitada ellos u Hola instalación no continuará. Se incluyen las versiones 1.3 o posterior.

7. Ejecute hello DeploySqlProvider.ps1 secuencia de comandos con parámetros de hello enumerada a continuación.

script de Hola realiza estos pasos:

* Si es necesario, descargue una versión compatible de Azure PowerShell.
* Cargar certificados de Hola y otra cuenta de almacenamiento de tooa de artefactos en la pila de Azure.
* Publicar paquetes de la Galería para que pueda implementar bases de datos SQL a través de la Galería de Hola.
* Implementar una máquina virtual mediante la imagen de Windows Server 2016 Hola creado en el paso 1 e instalar el proveedor de recursos de Hola.
* Registrar un registro DNS local que se asigna el proveedor de recursos de tooyour máquina virtual.
* Registre el proveedor de recursos con hello local Azure Resource Manager (inquilino y administrador).

> [!NOTE]
> Si la instalación de hello tiene más de 90 minutos, se puede producir un error y verá un mensaje de error en la pantalla de bienvenida y en el archivo de registro de hello, pero se vuelve a intentar implementación Hola de hello errores paso. Sistemas que no cumplen Hola memoria recomendada y las especificaciones principales pueden no ser capaz de toodeploy Hola SQL RP.
>

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
$vmLocalAdminCreds = New-Object System.Management.Automation.PSCredential ("sqlrpadmin", $vmLocalAdminPass)

$AdminPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force
$AdminCreds = New-Object System.Management.Automation.PSCredential ("admin@mydomain.onmicrosoft.com", $AdminPass)

# change this as appropriate
$PfxPass = ConvertTo-SecureString "P@ssw0rd1" -AsPlainText -Force

# Change directory toohello folder where you extracted hello installation files 
# and adjust hello endpoints
<extracted file directory>\DeploySQLProvider.ps1 -DirectoryTenantID $tenantID -AzCredential $AdminCreds -VMLocalCredential $vmLocalAdminCreds -ResourceGroupName "SqlRPRG" -VmName "SqlVM" -ArmEndpoint "https://adminmanagement.local.azurestack.external" -TenantArmEndpoint "https://management.local.azurestack.external" -DefaultSSLCertificatePassword $PfxPass
 ```

### <a name="deploysqlproviderps1-parameters"></a>Parámetros de DeploySqlProvider.ps1
Puede especificar estos parámetros en la línea de comandos de Hola. Si no lo hace, o se produce un error en cualquier validación de parámetros, se le solicitará tooprovide Hola requiere los.

| Nombre de parámetro | Descripción | Comentario o valor predeterminado |
| --- | --- | --- |
| **DirectoryTenantID** | Hello Azure o el identificador de directorio de AD FS (guid). | _obligatorio_ |
| **AzCredential** | Proporcione las credenciales de Hola para hello cuenta de administrador de servicio de pila de Azure. Debe usar hello mismo las credenciales que usó para la implementación de pila de Azure). | _obligatorio_ |
| **VMLocalCredential** | Definir las credenciales de hello para la cuenta de administrador local de Hola de proveedor de recursos SQL de hello VM. Esta contraseña también se utiliza para hello SQL **sa** cuenta. | _obligatorio_ |
| **ResourceGroupName** | Defina un nombre para un grupo de recursos en el que se almacenarán los elementos creados por este script. Por ejemplo, *SqlRPRG*. |  _requerido_ |
| **VmName** | Definir nombre de Hola de máquina virtual de hello en qué proveedor de recursos de tooinstall Hola. Por ejemplo, *SqlVM*. |  _requerido_ |
| **DependencyFilesLocalPath** | Los archivos de certificados se deben colocar también en este directorio. | _opcional_ |
| **DefaultSSLCertificatePassword** | contraseña de Hello para el archivo de certificado .pfx Hola | _obligatorio_ |
| **MaxRetryCount** | Definir cuántas veces desea tooretry cada operación si se produce un error.| 2 |
| **RetryDuration** | Defina el tiempo de espera de hello entre reintentos, en segundos. | 120 |
| **Desinstalación** | Quitar el proveedor de recursos de Hola y todos los recursos asociados (vea las notas siguientes) | No |
| **DebugMode** | Impide la limpieza automática en caso de error. | No |


## <a name="verify-hello-deployment-using-hello-azure-stack-portal"></a>Comprobar la implementación de hello mediante Hola Portal de la pila de Azure

> [!NOTE]
>  Una vez completado el script de instalación de hello, necesitará hoja de administración de toorefresh hello toosee portal Hola.


1. En el escritorio de máquina virtual de la consola de hello, haga clic en **Portal de Microsoft Azure pila** e inicie sesión en el portal de toohello como administrador de servicios de Hola.

2. Compruebe que la implementación de Hola se realizó correctamente. Haga clic en **grupos de recursos** &gt; haga clic en el grupo de recursos de Hola que usó y, a continuación, asegúrese de que esa parte de essentials Hola de lecturas de hoja (mitad superior) de hello  **_fecha_ (correcto)**.

      ![Comprobar la implementación de hello SQL RP](./media/azure-stack-sql-rp-deploy/sqlrp-verify.png)


## <a name="provide-capacity-by-connecting-tooa-hosting-sql-server"></a>Proporcionar una capacidad mediante la conexión tooa que hospeda SQL server

1. Inicie sesión en toohello portal de administración de la pila de Azure como un administrador de servicios

2. Cree una máquina virtual SQL, a menos que tenga una ya disponible. Marketplace Management ofrece algunas opciones para implementar máquinas virtuales SQL.

3. Haga clic en **Proveedores de recursos** &gt; **SQLAdapter** &gt; **Hosting Servers** (Servidores de hospedaje) &gt; **+Agregar**.

    Hola **servidores de hospedaje de SQL** hoja es donde puede conectar Hola proveedor de recursos de SQL Server tooactual instancias de SQL Server que actúan como Hola back-end del proveedor de recursos.

    ![Servidores de hospedaje](./media/azure-stack-sql-rp-deploy/sqlrp-hostingserver.PNG)

4. Rellenar el formulario de hello con detalles de la conexión de saludo de la instancia de SQL Server.

    ![Nuevo servidor de hospedaje](./media/azure-stack-sql-rp-deploy/sqlrp-newhostingserver.PNG)

    > [!NOTE]
    > Siempre que puede tener acceso a la instancia SQL de Hola por inquilino hello y administración de Azure Resource Manager, se puede colocar bajo el control de proveedor de recursos de Hola. instancia de SQL de Hello __debe__ asignar exclusivamente toohello RP.

5. Cuando agregue servidores, debe asignarlos tooa nuevas o existentes SKU toodifferentiate ofertas de servicio. Por ejemplo, podría tener una instancia de SQL Enterprise proporciona capacidad de la base de datos y copia de seguridad automática, reservar servidores de alto rendimiento para que los departamentos individuales, nombre de SKU de hello etc. debe reflejar propiedades Hola para que los inquilinos pueden colocar sus bases de datos correctamente y deben tener todos los servidores de hospedaje en una SKU hello las mismas capacidades.

    Por ejemplo:

    ![SKU](./media/azure-stack-sql-rp-deploy/sqlrp-newsku.png)

>[!NOTE]
SKU pueden tardar hasta tooan hora toobe visible en el portal de Hola. No se puede crear una base de datos hasta que Hola que SKU se crea.


## <a name="create-your-first-sql-database-tootest-your-deployment"></a>Crear la implementación de su primera tootest de base de datos SQL

1. Inicie sesión en toohello portal de administración de la pila de Azure como administrador del servicio.

2. Haga clic en **+ Nuevo** &gt; **Datos y almacenamiento "** &gt; **SQL Server Datbase (versión preliminar)** &gt; **Agregar**.

3. Rellene el formulario de hello con los detalles de la base de datos, incluidos un **nombre de base de datos**, **tamaño máximo**, y cambio Hola otros parámetros según sea necesario. Es más frecuentes toopick una SKU para la base de datos. Cuando se agregan servidores de hospedaje, que están asignados a una SKU y las bases de datos se crean en ese grupo de servidores que componen Hola SKU de hospedaje.

    ![Nueva base de datos](./media/azure-stack-sql-rp-deploy/newsqldb.png)


4. Rellene Hola configuración de inicio de sesión: **inicio de sesión de base de datos**, y **contraseña**. Se trata de una credencial de autenticación de SQL que se crea para el acceso toothis base de datos únicamente. nombre de usuario de inicio de sesión de Hello debe ser único globalmente. Cree una nueva configuración de inicio de sesión o seleccione una existente. Configuración de inicio de sesión se puede reutilizar para otras bases de datos mediante Hola misma SKU.

    ![Creación de un nuevo inicio de sesión en la base de datos](./media/azure-stack-sql-rp-deploy/create-new-login.png)


5. Enviar el formulario de Hola y espere Hola implementación toocomplete.

    En hoja resultante de hello, observe el campo de "Cadena de conexión" Hola. Puede usar esa cadena en cualquier aplicación que requiera acceso a SQL Server (por ejemplo, una aplicación web) en Azure Stack.

    ![Recuperar la cadena de conexión de Hola](./media/azure-stack-sql-rp-deploy/sql-db-settings.png)

## <a name="add-capacity"></a>Ampliación de capacidad

Agregar más capacidad mediante la adición de hosts SQL adicionales en el portal de Azure pila hello y asociarlos a una SKU adecuado. Si desea que otra instancia de SQL en lugar de hello uno instalado en el proveedor de hello VM toouse, haga clic en **proveedores de recursos** &gt; **SQLAdapter** &gt; **hospedaje de SQL Servidores** &gt; **+ agregar**.

## <a name="making-sql-databases-available-tootenants"></a>Hacer que las bases de datos SQL tootenants disponibles

Crear planes y ofertas toomake bases de datos SQL disponibles para los inquilinos. Debe crear un plan, agregar hello Microsoft.SqlAdapter servicio toohello plan y agregar una cuota existente o cree uno nuevo. Si creas una cuota, puede especificar el inquilino de hello capacidad tooallow Hola.
    ![Crear planes y ofertas tooinclude bases de datos](./media/azure-stack-sql-rp-deploy/sqlrp-newplan.png)

## <a name="tenant-usage-of-hello-resource-provider"></a>Uso de inquilinos de hello proveedor de recursos

Autoservicio de bases de datos se proporcionan a través de la experiencia del portal inquilino Hola.

## <a name="removing-hello-sql-adapter-resource-provider"></a>Quitar Hola proveedor de recursos de adaptador de SQL

En el proveedor de recursos de orden tooremove hello, es fundamental toofirst quitar todas las dependencias.

1. Asegúrese de que haya original paquete de implementación de Hola que has descargado para esta versión de Hola proveedor de recursos.

2. Todas las bases de datos de inquilino deben eliminarse del proveedor de recursos de hello (Esto no eliminará los datos de hello). Esto debe realizarse por parte de inquilinos Hola por sí mismos.

3. Administrador debe eliminar Hola hospedan servidores de hello adaptador de SQL

4. Administrador debe eliminar los planes que hacen referencia a Hola adaptador de SQL.

5. Administrador debe eliminar todos los SKU y cuotas asociadas toohello adaptador de SQL.

6. Vuelva a ejecutar el script de implementación de hello con hello - desinstalar parámetro, los puntos de conexión de Azure Resource Manager, DirectoryTenantID y las credenciales de cuenta de administrador del servicio de Hola.



## <a name="next-steps"></a>Pasos siguientes


Pruebe otros [servicios PaaS](azure-stack-tools-paas-services.md) como hello [proveedor de recursos de MySQL Server](azure-stack-mysql-resource-provider-deploy.md) hello y [proveedor de recursos de servicios de aplicaciones](azure-stack-app-service-overview.md).
