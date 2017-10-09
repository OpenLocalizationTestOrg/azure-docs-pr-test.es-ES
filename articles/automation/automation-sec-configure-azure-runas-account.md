---
title: aaaConfigure ejecutar como cuentas de Azure | Documentos de Microsoft
description: "Este tutorial le guía a través del uso de creación, las pruebas y ejemplo de Hola de autenticación de la entidad de seguridad en la automatización de Azure."
services: automation
documentationcenter: 
author: mgoedtel
manager: carmonm
editor: 
keywords: "nombre de la entidad de servicio, setspn, autenticación de azure"
ms.assetid: 2f783441-15c7-4ea0-ba27-d7daa39b1dd3
ms.service: automation
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/06/2017
ms.author: magoedte
ROBOTS: NOINDEX
redirect_url: /azure/automation/
redirect_document_id: True
ms.openlocfilehash: 06675d2f6b9d8e7260ffaead4f2b2f61c2b98d13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="authenticate-runbooks-with-an-azure-run-as-account"></a>Autenticación de Runbooks con una cuenta de ejecución de Azure
Este artículo muestra cómo tooconfigure una automatización de Azure cuenta Hola portal de Azure. toodo por lo tanto, se usan Hola ejecutar como cuenta característica tooauthenticate runbooks administrar recursos de Azure Resource Manager o administración de servicios de Azure.

Cuando se crea una cuenta de automatización en hello portal de Azure, se crean automáticamente dos cuentas:

* Una cuenta de ejecución. Esta cuenta crea una entidad de servicio en Azure Active Directory (Azure AD) y un certificado. También asigna control de acceso basado en roles de colaborador de hello (RBAC), que administra los recursos del Administrador de recursos mediante el uso de runbooks.
* Una cuenta de ejecución clásica. Esta cuenta carga un certificado de administración, que es usar toomanage administración de servicios o recursos clásicos mediante runbooks.

Debe crear una automatización cuenta simplifica el proceso de Hola para usted y le ayuda a que empezar rápidamente compilar e implementar runbooks toosupport la automatización.

Con una cuenta de ejecución y una cuenta de ejecución clásica puede:

* Proporcionan una manera normalizada tooauthenticate con Azure para administrar el Administrador de recursos o los recursos de administración de servicios desde los runbooks en hello portal de Azure.
* Automatice el uso de Hola de runbooks globales, que puede configurar en las alertas de Azure.

> [!NOTE]
> Hola [característica de integración de Azure alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md) con la automatización de runbooks global requiere una cuenta de automatización que se configura con una cuenta de ejecución y una cuenta de identificación clásico. Puede seleccionar una cuenta de automatización que ya ha definido las cuentas de ejecución e identificación clásico o puede elegir toocreate una nueva cuenta de automatización.
>  

Este artículo muestra cómo toocreate una cuenta de automatización de hello portal de Azure, actualizar una cuenta de automatización mediante el uso de PowerShell de Azure, administrar la configuración de la cuenta de hello y autenticarse en sus runbooks.

Antes de empezar a crear una cuenta de automatización, es una buena idea toounderstand y tenga en cuenta Hola siguiente:

* Crear una cuenta de automatización no afecta a las cuentas de automatización que se podría haber creado ya en hello clásico o modelo de implementación del Administrador de recursos.
* Hola proceso solo funciona para las cuentas de automatización que se crean en hello portal de Azure. Intentar toocreate una cuenta de hello portal de Azure clásico no replica Hola cuenta configuración de ejecución.
* Si ya dispone de runbooks y activos (por ejemplo, programaciones o variables) en lugar toomanage los recursos clásicos, y desea tooauthenticate runbooks con hello nueva clásico cuenta de ejecución, realice una de las siguientes de hello:

  * toocreate una cuenta de identificación clásico, siga las instrucciones de hello en la sección "Administración de la cuenta de ejecución" de Hola. 
  * la cuenta existente, use Hola PowerShell tooupdate secuencia de comandos en la sección de "Actualizar su cuenta de automatización mediante PowerShell" Hola.
* tooauthenticate mediante Hola nueva cuenta de ejecución y clásico ejecutar como cuenta de automatización de, deberá toomodify Hola de los runbooks existentes con código de ejemplo proporcionado en la sección de hello [ejemplos de código de autenticación](#authentication-code-examples).

    >[!NOTE]
    >Hola cuenta de ejecución es para la autenticación con recursos de administrador de recursos con la entidad de servicio basada en certificados de Hola. Hola clásico cuenta de ejecución es para autenticar con recursos de administración de servicios con un certificado de administración.

## <a name="create-an-automation-account-from-hello-azure-portal"></a>Crear una cuenta de automatización de hello portal de Azure
En esta sección, creará una cuenta de automatización de Azure de hello portal de Azure, que a su vez crea una cuenta de ejecución y una cuenta de identificación clásico.

>[!NOTE]
>toocreate una cuenta de automatización, debe ser miembro del rol de administradores de servicios de Hola o Coadministrador de suscripción de Hola que concede el acceso toohello suscripción. Debe agregarse como instancia de Active Directory de una suscripción de toothat de usuario predeterminada. cuenta de Hello no es necesario toobe asignado un rol con privilegios.
>
>Si no eres un miembro de instancia de Active Directory de la suscripción de hello antes de que se agreguen toohello rol de Coadministrador de suscripción de hello, se agregarán tooActive directorio como invitado. En este caso, recibirá un "no tiene permisos toocreate..." Advertencia de hello **agregar una cuenta de automatización** hoja.
>
>Los usuarios que se agregaron rol de Coadministrador toohello en primer lugar se puede quitar de la instancia de Active Directory de la suscripción de Hola y vuelva a agrega toomake a un usuario en Active Directory completo. tooverify esta situación de hello **Azure Active Directory** panel en el portal de Azure mediante la selección de hello **usuarios y grupos**, seleccione **todos los usuarios** y, después de seleccionar usuario específico de Hello, seleccionar **perfil**. Hola valo hello **tipo de usuario** atributo en el perfil de los usuarios de hello no debería ser igual **invitado**.
>

1. Inicie sesión en el portal de Azure con una cuenta que sea miembro del rol de administradores de suscripción de Hola y Coadministrador de suscripción de hello toohello.

2. Seleccione **Cuentas de Automation**.

3. En hello **cuentas de automatización** hoja, haga clic en **agregar**.
Hola **agregar una cuenta de automatización** abre la hoja.

 ![hoja de "Agregar cuenta de automatización" Hello](media/automation-sec-configure-azure-runas-account/create-automation-account-properties-b.png)

   > [!NOTE]
   > Si la cuenta no es miembro del rol de administradores de suscripción de Hola y Coadministrador de suscripción de hello, Hola después de advertencia se muestra en hello **agregar una cuenta de automatización** hoja:
   >
   >![Advertencia para agregar cuenta de Automation](media/automation-sec-configure-azure-runas-account/create-account-without-perms.png)
   >
   >

4. En hello **agregar una cuenta de automatización** hoja en hello **nombre** , escriba un nombre para la nueva cuenta de automatización.

5. Si tiene más de una suscripción, Hola siguientes:

    a. En **suscripción**, especifique una nueva cuenta de hello.

    b. En **Grupo de recursos**, haga clic en **Create new** (Crear nuevo) o **Use existing** (Usar existente).

    c. En **Ubicación**, especifique un centro de datos de Azure.

6. En **Crear cuenta de ejecución de Azure**, seleccione **Sí** y luego haga clic en **Crear**.

   > [!NOTE]
   > Si decide no toocreate Hola cuenta de ejecución seleccionando **No**, se muestra un mensaje de advertencia hello **agregar una cuenta de automatización** hoja. Aunque se crea la cuenta de hello en hello portal de Azure, no tiene una identidad de autenticación correspondiente en el clásico o el servicio de directorio de suscripción de administrador de recursos. Por lo tanto, la cuenta de hello no tiene ningún tooresources de acceso en su suscripción. Este escenario evita que los runbooks que hacen referencia a esta cuenta puedan autenticarse y realizar tareas con los recursos en dichos modelos de implementación.
   >
   > ![Mensaje de advertencia en la hoja de "Agregar cuenta de automatización" hello](media/automation-sec-configure-azure-runas-account/create-account-decline-create-runas-msg.png)
   >
   > Además, dado que no se crea la entidad de servicio de hello, rol de colaborador de hello no está asignado.
   >

7. Mientras Azure crea la cuenta de automatización de hello, puede seguir el progreso de hello en **notificaciones** en el menú de Hola.

### <a name="resources"></a>Recursos
Cuando se crea correctamente la cuenta de automatización de hello, varios recursos se crean automáticamente para usted. recursos de Hola se resumen en hello las dos tablas siguientes:

#### <a name="run-as-account-resources"></a>Recursos de la cuenta de ejecución

| Recurso | Descripción |
| --- | --- |
| Runbook AzureAutomationTutorial | Runbook gráfico de ejemplo que muestra cómo tooauthenticate mediante el uso de Hola cuenta de ejecución y hace que todos los recursos del Administrador de recursos de Hola. |
| Runbook AzureAutomationTutorialScript | Un runbook de PowerShell de ejemplo que muestra cómo tooauthenticate mediante el uso de Hola cuenta de ejecución y hace que todos los recursos del Administrador de recursos de Hola. |
| AzureRunAsCertificate | activo de certificado de Hola que se crea automáticamente al crear una cuenta de automatización o usar hello siguiente script de PowerShell para una cuenta existente. certificado de Hello le permite tooauthenticate con Azure, por lo que puede administrar los recursos de Azure Resource Manager desde los runbooks. certificado de Hello tiene una duración de un año. |
| AzureRunAsConnection | activo de conexión de Hola que se crea automáticamente al crear una cuenta de automatización o usar el script de PowerShell de Hola para una cuenta existente. |

#### <a name="classic-run-as-account-resources"></a>Recursos de la cuenta de ejecución clásica

| Recurso | Descripción |
| --- | --- |
| Runbook AzureClassicAutomationTutorial | Un runbook gráfico de ejemplo que obtiene todas las máquinas virtuales de Hola que se crean utilizando el modelo de implementación clásica de hello en una suscripción mediante el uso de hello clásico cuenta de ejecución (certificado) y, a continuación, escribe el nombre de la máquina virtual de Hola y el estado. |
| Runbook AzureClassicAutomationTutorial Script | Un runbook de PowerShell de ejemplo que obtiene todos Hola clásicas máquinas virtuales en una suscripción mediante el uso de hello clásico cuenta de ejecución (certificado) y, a continuación, escribe Hola estado y el nombre de la máquina virtual. |
| AzureClassicRunAsCertificate | activo de certificado de Hello creada automáticamente usar tooauthenticate con Azure para que pueda administrar los recursos clásicos Azure desde los runbooks. certificado de Hello tiene una duración de un año. |
| AzureClassicRunAsConnection | activo de conexión creado automáticamente de Hello usar tooauthenticate con Azure para que pueda administrar los recursos clásicos Azure desde los runbooks. |

## <a name="verify-run-as-authentication"></a>Comprobación de la autenticación de ejecución
Realizar una tooconfirm prueba pequeñas que pueda autenticar correctamente mediante el uso de hello nueva cuenta de ejecución.

1. Hola portal de Azure, abra la cuenta de automatización de Hola que creó anteriormente.

2. Haga clic en hello **Runbooks** icono tooopen Hola lista de runbooks.

3. Seleccione hello **AzureAutomationTutorialScript** runbook y, a continuación, haga clic en **iniciar** toostart Hola runbook. se produce Hola siguientes eventos:
 * A [trabajo del runbook](automation-runbook-execution.md) se crea, hello **trabajo** hoja se muestra y se muestra el estado del trabajo de Hola Hola **resumen de trabajos** icono.
 * estado del trabajo Hello, comienza siendo **en cola**, lo que indica que está esperando un runbook worker en hello toobecome de nube disponible.
 * Hola estado pasa a ser **iniciando** cuando un trabajador notificaciones trabajo Hola.
 * Hola estado pasa a ser **ejecuta** cuando Hola runbook comienza a ejecutarse.
 * Cuando el trabajo del runbook Hola ha terminado de ejecutarse, debería ver un estado de **completado**.

       ![Security Principal Runbook Test](media/automation-sec-configure-azure-runas-account/job-summary-automationtutorialscript.png)
4. toosee Hola resultados detallados de hello runbook, haga clic en hello **salida** icono.  
Hola **salida** hoja se muestra, que muestra ese runbook Hola correctamente ha autenticado y devuelve una lista de todos los recursos disponibles en el grupo de recursos de Hola.

5. Hola cerrar **salida** hoja tooreturn toohello **resumen de trabajos** hoja.

6. Hola cerrar **resumen de trabajos** hoja y Hola correspondiente **AzureAutomationTutorialScript** hoja de runbooks.

## <a name="verify-classic-run-as-authentication"></a>Comprobación de la autenticación de ejecución de Azure clásico
Realizar una pequeña similar tooconfirm que pueda autenticar correctamente mediante el uso de hello nueva clásico cuenta de ejecución de pruebas.

1. Hola portal de Azure, abra la cuenta de automatización de Hola que creó anteriormente.

2. Haga clic en hello **Runbooks** icono tooopen Hola lista de runbooks.

3. Seleccione hello **AzureClassicAutomationTutorialScript** runbook y, a continuación, haga clic en **iniciar** demasiado iniciar runbook Hola. se produce Hola siguientes eventos:

 * A [trabajo del runbook](automation-runbook-execution.md) se crea, hello **trabajo** hoja se muestra y se muestra el estado del trabajo de Hola Hola **resumen de trabajos** icono.
 * estado del trabajo Hello, comienza siendo **en cola**, lo que indica que está esperando un runbook worker en hello toobecome de nube disponible.
 * Hola estado pasa a ser **iniciando** cuando un trabajador notificaciones trabajo Hola.
 * Hola estado pasa a ser **ejecuta** cuando Hola runbook comienza a ejecutarse.
 * Cuando el trabajo del runbook Hola ha terminado de ejecutarse, debería ver un estado de **completado**.

    ![Prueba de Runbook de entidad de seguridad](media/automation-sec-configure-azure-runas-account/job-summary-automationclassictutorialscript.png)<br>
4. toosee Hola resultados detallados de hello runbook, haga clic en hello **salida** icono.  
Hola **salida** hoja se muestra, que muestra ese runbook Hola correctamente ha autenticado y devuelve una lista de todas las máquinas virtuales clásicas en la suscripción de Hola.

5. Hola cerrar **salida** hoja tooreturn toohello **resumen de trabajos** hoja.

6. Hola cerrar **resumen de trabajos** hoja y Hola correspondiente **AzureAutomationTutorialScript** hoja de runbooks.

## <a name="managing-your-run-as-account"></a>Administración de la cuenta de ejecución
En algún momento antes de que expire su cuenta de automatización, necesitará toorenew Hola certificado. Si cree que Hola cuenta de ejecución está en peligro, puede eliminar y volver a crearla. Esta sección se describe cómo tooperform estas operaciones.

### <a name="self-signed-certificate-renewal"></a>Renovación de certificado autofirmado
certificado autofirmado de Hola que creó para la cuenta de ejecución de Hola expira un año a partir de la fecha de Hola de creación. Se puede renovar en cualquier momento antes de que expire. Cuando renovarlo, certificado válido de hello actual es retenido tooensure que los runbooks que se ponen en cola hasta o activamente ejecutándose y que autenticarse con hello cuenta de ejecución, no se afecta negativamente. certificado de Hello sigue siendo válido hasta la fecha de expiración.

> [!NOTE]
> Si ha configurado su toouse de cuenta automatización ejecutar como un certificado emitido por la entidad de certificación de empresa y use esta opción, certificado de empresa de Hola se reemplazará por un certificado autofirmado.

Hola toorenew certificados, Hola siguientes:

1. Hola portal de Azure, abrir cuenta de automatización de Hola.

2. En hello **cuenta de automatización** hoja en hello **cuenta propiedades** panel, en **configuración de la cuenta**, seleccione **cuentas de ejecución**.

    ![Panel de propiedades de la cuenta de Automation](media/automation-sec-configure-azure-runas-account/automation-account-properties-pane.png)
3. En hello **cuentas de ejecución** hoja de propiedades, seleccione cualquier Hola ejecutar como cuenta u Hola clásico cuenta de ejecución que desea toorenew Hola certificado.

4. En hello **propiedades** hoja para hello seleccionado cuenta, haga clic en **renovar certificado**.

    ![Renovación del certificado para una cuenta de ejecución](media/automation-sec-configure-azure-runas-account/automation-account-renew-runas-certificate.png)

5. Mientras se que se va a renovar el certificado de hello, puede seguir el progreso de hello en **notificaciones** en el menú de Hola.

### <a name="delete-a-run-as-or-classic-run-as-account"></a>Eliminación de una cuenta de ejecución o de ejecución clásica
Esta sección se describe cómo toodelete y volver a crear una cuenta de ejecución o identificación clásico. Al realizar esta acción, se conserva Hola cuenta de automatización. Después de eliminar una cuenta de ejecución o identificación clásico, puede volver a crearla en hello portal de Azure.

1. Hola portal de Azure, abrir cuenta de automatización de Hola.

2. En hello **cuenta de automatización** hoja, en el panel de propiedades de cuenta hello, seleccione **cuentas de ejecución**.

3. En hello **cuentas de ejecución** hoja de propiedades, seleccione cualquier Hola ejecutar como cuenta de ejecución de o clásico como la cuenta que desea toodelete. A continuación, en hello **propiedades** hoja para hello seleccionado cuenta, haga clic en **eliminar**.

 ![Eliminación de una cuenta de ejecución](media/automation-sec-configure-azure-runas-account/automation-account-delete-runas.png)

4. Mientras se está eliminando la cuenta de hello, puede seguir el progreso de hello en **notificaciones** en el menú de Hola.

5. Después de que se ha eliminado la cuenta de hello, se puede volver a crear en hello **cuentas de ejecución** opción de creación de la hoja de propiedades seleccionando hello **ejecutar como cuenta de Azure**.

 ![Volver a crear Hola automatización de la cuenta de ejecución](media/automation-sec-configure-azure-runas-account/automation-account-create-runas.png)

### <a name="misconfiguration"></a>Error de configuración
Algunos elementos de configuración necesarios para toofunction de cuenta de identificación o identificación clásico Hola correctamente podrían se han eliminado o creó incorrectamente durante la instalación inicial. Hola elementos incluyen:

* Recurso de certificado
* Recurso de conexión
* Se ha quitado la cuenta de ejecución de rol de colaborador de Hola
* Entidad de servicio o aplicación en Azure AD

Hola anterior y otras instancias de una configuración incorrecta, Hola cuenta de automatización detecta Hola cambia y muestra un estado de *incompleta* en hello **cuentas de ejecución** hoja de propiedades para hello cuenta.

![Estado de configuración incompleta de la cuenta de ejecución](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config.png)

Cuando se selecciona la cuenta de identificación de hello, Hola cuenta **propiedades** panel muestra hello mensaje de error siguiente:

![Mensaje de advertencia de configuración incompleta de la cuenta de ejecución](media/automation-sec-configure-azure-runas-account/automation-account-runas-incomplete-config-msg.png).

Rápidamente puede resolver estos problemas de la cuenta ejecutar como eliminar y volver a crear la cuenta de hello.

## <a name="update-your-automation-account-by-using-powershell"></a>Actualización de la cuenta de Automation mediante PowerShell
Puede usar PowerShell tooupdate su cuenta de automatización existente si:

* Crear una cuenta de automatización, pero rechazar toocreate Hola cuenta de ejecución.
* Ya utiliza un administrador de recursos toomanage cuenta recursos de automatización y desea tooupdate Hola cuenta tooinclude Hola cuenta de ejecución para la autenticación de runbook.
* Ya utiliza un recursos clásicos de automatización de la cuenta toomanage y desea tooupdate se toouse Hola clásico cuenta de ejecución en lugar de crear una cuenta nueva y migrar su tooit runbooks y activos.   
* Toocreate que desee ejecutar como y una cuenta de identificación clásico mediante el uso de un certificado emitido por la entidad de certificación (CA) empresarial.

script de Hola tiene Hola siguiendo los requisitos previos:

* script de Hola se puede ejecutar solo en Windows 10 y Windows Server 2016 con módulos de Azure Resource Manager 2.01 y versiones posteriores. No se admite en versiones anteriores de Windows.
* Azure PowerShell 1.0 y versiones superiores. Para obtener información acerca de la versión de Hola PowerShell 1.0, vea [cómo tooinstall y configurar Azure PowerShell](/powershell/azure/overview).
* Una cuenta de automatización, que se hace referencia como valor de Hola de hello *: AutomationAccountName* y *- ApplicationDisplayName* parámetros Hola siguiente script de PowerShell.

Hola tooget los valores de *SubscriptionID*, *ResourceGroup*, y *AutomationAccountName*, que son parámetros necesarios para las secuencias de comandos de hello, Hola siguientes:
1. En el portal de Azure de Hola, seleccione su cuenta de automatización en hello **cuenta de automatización** hoja y, a continuación, seleccione **toda la configuración de**. 
2. En hello **toda la configuración de** hoja, en **configuración de la cuenta**, seleccione **propiedades**. 
3. Tenga en cuenta los valores de hello en hello **propiedades** hoja.

![hoja de "Propiedades" de cuenta de automatización de Hola](media/automation-sec-configure-azure-runas-account/automation-account-properties.png)  

### <a name="create-a-run-as-account-powershell-script"></a>Creación de un script de PowerShell de una cuenta de ejecución
Este script de PowerShell incluye compatibilidad para hello siguiendo configuraciones:

* Creación de una cuenta de ejecución mediante un certificado autofirmado.
* Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado autofirmado.
* Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado de empresa.
* Crear una cuenta de ejecución y una cuenta de identificación clásico mediante un certificado autofirmado en hello en la nube Azure Government.

Dependiendo de la opción de configuración de Hola que seleccione, el script de Hola crea Hola siguientes elementos.

**Para cuentas de ejecución:**

* Crea un Azure AD aplicación toobe exportado con cualquier hello autofirmado o clave pública del certificado de la empresa, crea una cuenta de entidad de servicio para la aplicación hello en Azure AD y asigna Hola rol Colaborador para cuenta de hello en el actual suscripción. Puede cambiar esta configuración tooOwner o cualquier otro rol. Para más información, consulte [Control de acceso basado en rol en Azure Automation](automation-role-based-access-control.md).
* Crea un activo de certificado de automatización denominado *AzureRunAsCertificate* en hello especifica la cuenta de automatización. activo de certificado de Hello contiene la clave privada de hello certificado utilizado por la aplicación hello Azure AD.
* Crea un recurso de conexión de automatización denominado *AzureRunAsConnection* en hello especifica la cuenta de automatización. activo de conexión de Hello contiene applicationId hello, tenantId, Id. de suscripción y la huella digital del certificado.

**Para cuentas de ejecución clásicas:**

* Crea un activo de certificado de automatización denominado *AzureClassicRunAsCertificate* en hello especifica la cuenta de automatización. activo de certificado de Hello contiene la clave privada del certificado Hola utilizado por el certificado de administración de Hola.
* Crea un recurso de conexión de automatización denominado *AzureClassicRunAsConnection* en hello especifica la cuenta de automatización. activo de conexión de Hello contiene el nombre de la suscripción de hello, Id. de suscripción y el nombre del recurso de certificado.

>[!NOTE]
> Si selecciona cualquiera de las opciones para crear una cuenta de identificación clásico, después de ejecuta script de Hola, carga Hola certificado público almacén de administración de toohello (extensión de nombre de archivo .cer) para suscripción Hola esa cuenta de automatización de Hola se creó en.
> 

tooexecute Hola script y cargar el certificado de hello, Hola siguientes:

1. Guardar Hola siguiente secuencia de comandos en el equipo. En este ejemplo, guárdelo con el nombre de archivo de hello *RunAsAccount.ps1 nuevo*.

        #Requires -RunAsAdministrator
         Param (
        [Parameter(Mandatory=$true)]
        [String] $ResourceGroup,

        [Parameter(Mandatory=$true)]
        [String] $AutomationAccountName,

        [Parameter(Mandatory=$true)]
        [String] $ApplicationDisplayName,

        [Parameter(Mandatory=$true)]
        [String] $SubscriptionId,

        [Parameter(Mandatory=$true)]
        [Boolean] $CreateClassicRunAsAccount,

        [Parameter(Mandatory=$true)]
        [String] $SelfSignedCertPlainPassword,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPathForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [String] $EnterpriseCertPlainPasswordForClassicRunAsAccount,

        [Parameter(Mandatory=$false)]
        [ValidateSet("AzureCloud","AzureUSGovernment")]
        [string]$EnvironmentName="AzureCloud",

        [Parameter(Mandatory=$false)]
        [int] $SelfSignedCertNoOfMonthsUntilExpired = 12
        )

        function CreateSelfSignedCertificate([string] $keyVaultName, [string] $certificateName, [string] $selfSignedCertPlainPassword,
                                      [string] $certPath, [string] $certPathCer, [string] $selfSignedCertNoOfMonthsUntilExpired ) {
        $Cert = New-SelfSignedCertificate -DnsName $certificateName -CertStoreLocation cert:\LocalMachine\My `
           -KeyExportPolicy Exportable -Provider "Microsoft Enhanced RSA and AES Cryptographic Provider" `
           -NotAfter (Get-Date).AddMonths($selfSignedCertNoOfMonthsUntilExpired)

        $CertPassword = ConvertTo-SecureString $selfSignedCertPlainPassword -AsPlainText -Force
        Export-PfxCertificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPath -Password $CertPassword -Force | Write-Verbose
        Export-Certificate -Cert ("Cert:\localmachine\my\" + $Cert.Thumbprint) -FilePath $certPathCer -Type CERT | Write-Verbose
        }

        function CreateServicePrincipal([System.Security.Cryptography.X509Certificates.X509Certificate2] $PfxCert, [string] $applicationDisplayName) {  
        $CurrentDate = Get-Date
        $keyValue = [System.Convert]::ToBase64String($PfxCert.GetRawCertData())
        $KeyId = (New-Guid).Guid

        $KeyCredential = New-Object  Microsoft.Azure.Commands.Resources.Models.ActiveDirectory.PSADKeyCredential
        $KeyCredential.StartDate = $CurrentDate
        $KeyCredential.EndDate= [DateTime]$PfxCert.GetExpirationDateString()
        $KeyCredential.EndDate = $KeyCredential.EndDate.AddDays(-1)
        $KeyCredential.KeyId = $KeyId
        $KeyCredential.CertValue  = $keyValue

        # Use key credentials and create an Azure AD application
        $Application = New-AzureRmADApplication -DisplayName $ApplicationDisplayName -HomePage ("http://" + $applicationDisplayName) -IdentifierUris ("http://" + $KeyId) -KeyCredentials $KeyCredential
        $ServicePrincipal = New-AzureRMADServicePrincipal -ApplicationId $Application.ApplicationId
        $GetServicePrincipal = Get-AzureRmADServicePrincipal -ObjectId $ServicePrincipal.Id

        # Sleep here for a few seconds tooallow hello service principal application toobecome active (ordinarily takes a few seconds)
        Sleep -s 15
        $NewRole = New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
        $Retries = 0;
        While ($NewRole -eq $null -and $Retries -le 6)
        {
           Sleep -s 10
           New-AzureRMRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $Application.ApplicationId | Write-Verbose -ErrorAction SilentlyContinue
           $NewRole = Get-AzureRMRoleAssignment -ServicePrincipalName $Application.ApplicationId -ErrorAction SilentlyContinue
           $Retries++;
        }
           return $Application.ApplicationId.ToString();
        }

        function CreateAutomationCertificateAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $certifcateAssetName,[string] $certPath, [string] $certPlainPassword, [Boolean] $Exportable) {
        $CertPassword = ConvertTo-SecureString $certPlainPassword -AsPlainText -Force   
        Remove-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $certifcateAssetName -ErrorAction SilentlyContinue
        New-AzureRmAutomationCertificate -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Path $certPath -Name $certifcateAssetName -Password $CertPassword -Exportable:$Exportable  | write-verbose
        }

        function CreateAutomationConnectionAsset ([string] $resourceGroup, [string] $automationAccountName, [string] $connectionAssetName, [string] $connectionTypeName, [System.Collections.Hashtable] $connectionFieldValues ) {
        Remove-AzureRmAutomationConnection -ResourceGroupName $resourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -Force -ErrorAction SilentlyContinue
        New-AzureRmAutomationConnection -ResourceGroupName $ResourceGroup -AutomationAccountName $automationAccountName -Name $connectionAssetName -ConnectionTypeName $connectionTypeName -ConnectionFieldValues $connectionFieldValues
        }

        Import-Module AzureRM.Profile
        Import-Module AzureRM.Resources

        $AzureRMProfileVersion= (Get-Module AzureRM.Profile).Version
        if (!(($AzureRMProfileVersion.Major -ge 2 -and $AzureRMProfileVersion.Minor -ge 1) -or ($AzureRMProfileVersion.Major -gt 2)))
        {
           Write-Error -Message "Please install hello latest Azure PowerShell and retry. Relevant doc url : https://docs.microsoft.com/powershell/azureps-cmdlets-docs/ "
           return
        }

        Login-AzureRmAccount -EnvironmentName $EnvironmentName
        $Subscription = Select-AzureRmSubscription -SubscriptionId $SubscriptionId

        # Create a Run As account by using a service principal
        $CertifcateAssetName = "AzureRunAsCertificate"
        $ConnectionAssetName = "AzureRunAsConnection"
        $ConnectionTypeName = "AzureServicePrincipal"

        if ($EnterpriseCertPathForRunAsAccount -and $EnterpriseCertPlainPasswordForRunAsAccount) {
        $PfxCertPathForRunAsAccount = $EnterpriseCertPathForRunAsAccount
        $PfxCertPlainPasswordForRunAsAccount = $EnterpriseCertPlainPasswordForRunAsAccount
        } else {
          $CertificateName = $AutomationAccountName+$CertifcateAssetName
          $PfxCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".pfx")
          $PfxCertPlainPasswordForRunAsAccount = $SelfSignedCertPlainPassword
          $CerCertPathForRunAsAccount = Join-Path $env:TEMP ($CertificateName + ".cer")
          CreateSelfSignedCertificate $KeyVaultName $CertificateName $PfxCertPlainPasswordForRunAsAccount $PfxCertPathForRunAsAccount $CerCertPathForRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create a service principal
        $PfxCert = New-Object -TypeName System.Security.Cryptography.X509Certificates.X509Certificate2 -ArgumentList @($PfxCertPathForRunAsAccount, $PfxCertPlainPasswordForRunAsAccount)
        $ApplicationId=CreateServicePrincipal $PfxCert $ApplicationDisplayName

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $CertifcateAssetName $PfxCertPathForRunAsAccount $PfxCertPlainPasswordForRunAsAccount $true

        # Populate hello ConnectionFieldValues
        $SubscriptionInfo = Get-AzureRmSubscription -SubscriptionId $SubscriptionId
        $TenantID = $SubscriptionInfo | Select TenantId -First 1
        $Thumbprint = $PfxCert.Thumbprint
        $ConnectionFieldValues = @{"ApplicationId" = $ApplicationId; "TenantId" = $TenantID.TenantId; "CertificateThumbprint" = $Thumbprint; "SubscriptionId" = $SubscriptionId}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ConnectionAssetName $ConnectionTypeName $ConnectionFieldValues

        if ($CreateClassicRunAsAccount) {
            # Create a Run As account by using a service principal
            $ClassicRunAsAccountCertifcateAssetName = "AzureClassicRunAsCertificate"
            $ClassicRunAsAccountConnectionAssetName = "AzureClassicRunAsConnection"
            $ClassicRunAsAccountConnectionTypeName = "AzureClassicCertificate "
            $UploadMessage = "Please upload hello .cer format of #CERT# toohello Management store by following hello steps below." + [Environment]::NewLine +
                    "Log in toohello Microsoft Azure Management portal (https://manage.windowsazure.com) and select Settings -> Management Certificates." + [Environment]::NewLine +
                    "Then click Upload and upload hello .cer format of #CERT#"

             if ($EnterpriseCertPathForClassicRunAsAccount -and $EnterpriseCertPlainPasswordForClassicRunAsAccount ) {
             $PfxCertPathForClassicRunAsAccount = $EnterpriseCertPathForClassicRunAsAccount
             $PfxCertPlainPasswordForClassicRunAsAccount = $EnterpriseCertPlainPasswordForClassicRunAsAccount
             $UploadMessage = $UploadMessage.Replace("#CERT#", $PfxCertPathForClassicRunAsAccount)
        } else {
             $ClassicRunAsAccountCertificateName = $AutomationAccountName+$ClassicRunAsAccountCertifcateAssetName
             $PfxCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".pfx")
             $PfxCertPlainPasswordForClassicRunAsAccount = $SelfSignedCertPlainPassword
             $CerCertPathForClassicRunAsAccount = Join-Path $env:TEMP ($ClassicRunAsAccountCertificateName + ".cer")
             $UploadMessage = $UploadMessage.Replace("#CERT#", $CerCertPathForClassicRunAsAccount)
             CreateSelfSignedCertificate $KeyVaultName $ClassicRunAsAccountCertificateName $PfxCertPlainPasswordForClassicRunAsAccount $PfxCertPathForClassicRunAsAccount $CerCertPathForClassicRunAsAccount $SelfSignedCertNoOfMonthsUntilExpired
        }

        # Create hello Automation certificate asset
        CreateAutomationCertificateAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountCertifcateAssetName $PfxCertPathForClassicRunAsAccount $PfxCertPlainPasswordForClassicRunAsAccount $false

        # Populate hello ConnectionFieldValues
        $SubscriptionName = $subscription.Subscription.SubscriptionName
        $ClassicRunAsAccountConnectionFieldValues = @{"SubscriptionName" = $SubscriptionName; "SubscriptionId" = $SubscriptionId; "CertificateAssetName" = $ClassicRunAsAccountCertifcateAssetName}

        # Create an Automation connection asset named AzureRunAsConnection in hello Automation account. This connection uses hello service principal.
        CreateAutomationConnectionAsset $ResourceGroup $AutomationAccountName $ClassicRunAsAccountConnectionAssetName $ClassicRunAsAccountConnectionTypeName $ClassicRunAsAccountConnectionFieldValues

        Write-Host -ForegroundColor red $UploadMessage
        }

2. En el equipo, haga clic en **Inicio** y luego inicie **Windows PowerShell** con derechos de usuario elevados.

3. De hello elevado shell de línea de comandos de PowerShell, vaya toohello carpeta que contiene el script de Hola que creó en el paso 1.

4. Ejecutar script de Hola mediante el uso de valores de parámetro de hello para la configuración de Hola que necesite.

    **Creación de una cuenta de ejecución mediante un certificado autofirmado**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $false`

    **Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado autofirmado**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true`

    **Creación de una cuenta de ejecución y una cuenta de ejecución clásica mediante un certificado de empresa**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication>  -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true -EnterpriseCertPathForRunAsAccount <EnterpriseCertPfxPathForRunAsAccount> -EnterpriseCertPlainPasswordForRunAsAccount <StrongPassword> -EnterpriseCertPathForClassicRunAsAccount <EnterpriseCertPfxPathForClassicRunAsAccount> -EnterpriseCertPlainPasswordForClassicRunAsAccount <StrongPassword>`

    **Crear una cuenta de ejecución y una cuenta de identificación clásico mediante un certificado autofirmado en hello en la nube Azure Government**  
    `.\New-RunAsAccount.ps1 -ResourceGroup <ResourceGroupName> -AutomationAccountName <NameofAutomationAccount> -SubscriptionId <SubscriptionId> -ApplicationDisplayName <DisplayNameofAADApplication> -SelfSignedCertPlainPassword <StrongPassword> -CreateClassicRunAsAccount $true  -EnvironmentName AzureUSGovernment`

    > [!NOTE]
    > Una vez ejecutado el script de Hola, será tooauthenticate solicitada con Azure. Inicie sesión con una cuenta que sea miembro del rol de administradores de suscripción de Hola y Coadministrador de suscripción de Hola.
    >
    >

Después de que el script de Hola se ha ejecutado correctamente, observe Hola siguiente:
* Si ha creado una cuenta de identificación clásico con un certificado autofirmado público (archivo .cer), el script de Hola crea y guarda toohello carpeta de archivos temporales en el equipo en el perfil de usuario de hello *%USERPROFILE%\AppData\Local\Temp*, que ya ha utilizado la sesión de PowerShell de tooexecute Hola.
* Si creó una cuenta de identificación clásica con un certificado público de empresa (archivo .cer) , use este certificado. Siga las instrucciones de Hola para [cargar una toohello de certificado de la API de administración portal de Azure clásico](../azure-api-management-certs.md)y, a continuación, validar configuración de credencial de hello con recursos de administración de servicios mediante hello [código de ejemplo tooauthenticate con recursos de administración del servicio](#sample-code-to-authenticate-with-service-management-resources). 
* Si lo hizo *no* crear una cuenta de identificación clásico, autenticar con recursos de administrador de recursos y validar la configuración de credencial de hello mediante hello [código de ejemplo para autenticar con la administración de servicios recursos](#sample-code-to-authenticate-with-resource-manager-resources).

## <a name="sample-code-tooauthenticate-with-resource-manager-resources"></a>Tooauthenticate de código de ejemplo con los recursos del Administrador de recursos
Puede usar los siguientes Hola actualizar código, tomado de Hola de ejemplo *AzureAutomationTutorialScript* runbook de ejemplo, tooauthenticate con hello ejecutar como cuenta toomanage el Administrador de recursos recursos con sus runbooks.

    $connectionName = "AzureRunAsConnection"
    $SubId = Get-AutomationVariable -Name 'SubscriptionId'
    try
    {
       # Get hello connection "AzureRunAsConnection "
       $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

       "Signing in tooAzure..."
       Add-AzureRmAccount `
         -ServicePrincipal `
         -TenantId $servicePrincipalConnection.TenantId `
         -ApplicationId $servicePrincipalConnection.ApplicationId `
         -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
       "Setting context tooa specific subscription"     
       Set-AzureRmContext -SubscriptionId $SubId              
    }
    catch {
        if (!$servicePrincipalConnection)
        {
           $ErrorMessage = "Connection $connectionName not found."
           throw $ErrorMessage
         } else{
            Write-Error -Message $_.Exception
            throw $_.Exception
         }
    }

toohelp tooeasily funcionan entre varias suscripciones, el script de Hola incluye dos líneas adicionales de código que admiten que hacen referencia a un contexto de la suscripción. Un activo de variable denominado *SubscriptionId* contiene Hola identificador de suscripción de Hola. Después de hello `Add-AzureRmAccount` instrucción de cmdlet, hello [ `Set-AzureRmContext` ](/powershell/module/azurerm.profile/set-azurermcontext) cmdlet se ha indicado con el conjunto de parámetros de hello *- Id. de suscripción*. Si el nombre de la variable hello es demasiado genérico, puede revisar tooinclude un prefijo o usar otro toomake de convención de nomenclatura sea más fácil tooidentify. O bien, puede usar el conjunto de parámetros de Hola *- SubscriptionName* en lugar de *- Id. de suscripción* a un activo de variable correspondiente.

Hola cmdlet que utilice para la autenticación en runbook hello, `Add-AzureRmAccount`, usa hello *ServicePrincipalCertificate* conjunto de parámetros. Autentica mediante el certificado de entidad de seguridad de servicio de hello, no las credenciales de usuario de Hola.

## <a name="sample-code-tooauthenticate-with-service-management-resources"></a>Tooauthenticate de código de ejemplo con los recursos de administración de servicios
Puede usar Hola después el código de ejemplo actualizado, que procede de hello *AzureClassicAutomationTutorialScript* runbook de ejemplo, tooauthenticate mediante el uso de hello clásico cuenta de ejecución toomanage recursos clásicos con su runbooks.

    $ConnectionAssetName = "AzureClassicRunAsConnection"
    # Get hello connection
    $connection = Get-AutomationConnection -Name $connectionAssetName        

    # Authenticate tooAzure with certificate
    Write-Verbose "Get connection asset: $ConnectionAssetName" -Verbose
    $Conn = Get-AutomationConnection -Name $ConnectionAssetName
    if ($Conn -eq $null)
    {
       throw "Could not retrieve connection asset: $ConnectionAssetName. Assure that this asset exists in hello Automation account."
    }

    $CertificateAssetName = $Conn.CertificateAssetName
    Write-Verbose "Getting hello certificate: $CertificateAssetName" -Verbose
    $AzureCert = Get-AutomationCertificate -Name $CertificateAssetName
    if ($AzureCert -eq $null)
    {
       throw "Could not retrieve certificate asset: $CertificateAssetName. Assure that this asset exists in hello Automation account."
    }

    Write-Verbose "Authenticating tooAzure with certificate." -Verbose
    Set-AzureSubscription -SubscriptionName $Conn.SubscriptionName -SubscriptionId $Conn.SubscriptionID -Certificate $AzureCert
    Select-AzureSubscription -SubscriptionId $Conn.SubscriptionID

## <a name="next-steps"></a>Pasos siguientes
* [Objetos de aplicación y de entidad de servicio en Azure AD](../active-directory/active-directory-application-objects.md)
* [Control de acceso basado en rol en Azure Automation](automation-role-based-access-control.md)
* [Introducción a los certificados para Azure Cloud Services](../cloud-services/cloud-services-certs-create.md)
