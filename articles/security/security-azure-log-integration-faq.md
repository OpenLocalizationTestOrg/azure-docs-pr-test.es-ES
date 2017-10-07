---
title: "Preguntas más frecuentes sobre la integración de registro aaaAzure | Documentos de Microsoft"
description: "Este artículo responde a las preguntas sobre Azure Log Integration."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: d06d1ac5-5c3b-49de-800e-4d54b3064c64
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload8: na
ms.date: 08/07/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: e886035c9a180d0cd5fcbe9cc02483782df6dbe4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-faq"></a>Preguntas más frecuentes sobre Azure Log Integration
En este artículo se responden algunas preguntas frecuentes sobre Azure Log Integration. 

Integración de registro de Azure es un servicio de sistema operativo de Windows que puede usar los registros de toointegrate sin procesar de los recursos de Azure en los sistemas de administración (SIEM) de eventos e información de seguridad de local. Esta integración proporciona una consola unificada para todos sus activos, local o en la nube de Hola. Puede agregar, correlacionar, analizar y alertar sobre eventos de seguridad asociados con las aplicaciones.

## <a name="is-hello-azure-log-integration-software-free"></a>¿Es un software de integración de Azure registro de hello gratuita?
Sí. No hay ningún cargo por hello software de integración de registro de Azure.

## <a name="where-is-azure-log-integration-available"></a>¿Dónde se encuentra disponible la integración de registro de Azure?

Está actualmente disponible en la versión comercial de Azure y en Azure Government. No se encuentra disponible ni en China ni en Alemania.

## <a name="how-can-i-see-hello-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a>¿Cómo se puede ver las cuentas de almacenamiento de Hola desde el que Azure registro integración extrae los registros de máquina virtual de Azure?
Ejecute el comando de hello **lista de orígenes de azlog**.

## <a name="how-can-i-tell-which-subscription-hello-azure-log-integration-logs-are-from"></a>¿Cómo puedo saber qué Hola suscripción Azure integración de registros son registros de?

En caso de hello de los registros de auditoría que se colocan en hello **AzureResourcemanagerJson** directorios, Id. de suscripción de hello es en nombre de archivo de registro de hello. Esto también es cierto para los registros en hello **AzureSecurityCenterJson** carpeta. Por ejemplo:

20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json

Los registros de auditoría de Azure Active Directory incluyen hello Id. de inquilino como parte del nombre de Hola.

Registros de diagnóstico que se leen desde un centro de eventos no incluyen el Id. de suscripción de hello como parte del nombre de Hola. En cambio, incluyen Nombre_descriptivo hello, especificado como parte de la creación de Hola Hola concentrador del origen de evento. 

## <a name="how-can-i-update-hello-proxy-configuration"></a>¿Cómo puedo actualizar configuración de proxy de hello?
Si el configuración del proxy no permite el acceso de almacenamiento de Azure directamente, abra hello **AZLOG. EXE. CONFIGURACIÓN** en el archivo **c:\Program Files\Microsoft Azure registro integración**. Actualización Hola archivo tooinclude Hola **defaultProxy** sección con la dirección de proxy de Hola de su organización. Después de realiza la actualización de hello, detenga e inicie el servicio de hello mediante comandos de hello **net stop azlog** y **azlog del comando net start**.

    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.net>
        <connectionManagement>
          <add address="*" maxconnection="400" />
        </connectionManagement>
        <defaultProxy>
          <proxy usesystemdefault="true"
          proxyaddress=http://127.0.0.1:8888
          bypassonlocal="true" />
        </defaultProxy>
      </system.net>
      <system.diagnostics>
        <performanceCounters filemappingsize="20971520" />
      </system.diagnostics>   

## <a name="how-can-i-see-hello-subscription-information-in-windows-events"></a>¿Cómo se puede ver la información de suscripción de hello en los eventos de Windows?
Anexar nombre descriptivo del toohello de Id. de hello suscripción al agregar el origen de hello:

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
evento de Hello XML tiene Hola después de metadatos, incluidos el identificador de suscripción de hello:

![XML de eventos][1]

## <a name="error-messages"></a>mensajes de error
### <a name="when-i-run-hello-command-azlog-createazureid-why-do-i-get-hello-following-error"></a>Al ejecutar el comando de Hola **azlog createazureid**, ¿por qué recibo Hola tras error?
Error:

  *No se pudo toocreate aplicación AAD - inquilino 72f988bf-86f1-41af-91ab-2d7cd011db37 - motivo = 'Prohibido' - mensaje = "privilegios suficientes toocomplete hello en la operación."*

Hola **azlog createazureid** toocreate una entidad de servicio en todos los inquilinos de hello Azure AD para las suscripciones de Hola Hola Azure inicio de sesión tiene acceso a los intentos de comando. Si el inicio de sesión de Azure es solo un usuario invitado en ese inquilino de Azure AD, se produce un error en comando hello con "operación de hello toocomplete de privilegios suficientes." Pida inquilino Hola admin tooadd tu cuenta como un usuario de inquilino de Hola.

### <a name="when-i-run-hello-command-azlog-authorize-why-do-i-get-hello-following-error"></a>Al ejecutar el comando de Hola **azlog autorizar**, ¿por qué recibo Hola tras error?
Error:

  *Advertencia de creación de asignación de roles - AuthorizationFailed: cliente hello janedo@microsoft.com' con objeto de identificador 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' no tiene autorización tooperform acción 'Microsoft.Authorization/roleAssignments/write' sobre el ámbito ' / las suscripciones / 70d 95299-d689-4c 97-b971-0d8ff0000000'.*

Hola **azlog autorizar** comando asigna Hola rol de entidad de servicio de lector toohello Azure AD (creado con **azlog createazureid**) toohello proporciona suscripciones. Si hello Azure inicio de sesión no es un administrador o el propietario de la suscripción de hello, se produce un error con un mensaje de error "Error de autorización". Azure Role-Based Access Control (RBAC) del administrador o propietario es necesario toocomplete esta acción.

## <a name="where-can-i-find-hello-definition-of-hello-properties-in-hello-audit-log"></a>¿Dónde puedo encontrar definición Hola de propiedades de hello en el registro de auditoría de hello?
Consulte:

* [Operaciones de auditoría con Azure Resource Manager](../azure-resource-manager/resource-group-audit.md)
* [Lista de los eventos de administración de hello en una suscripción en hello API de REST de Monitor de Azure](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a>¿Dónde puedo encontrar detalles sobre las alertas de Azure Security Center?
Vea [toosecurity responde y administrar las alertas en Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a>¿Cómo puedo modificar la información recopilada mediante el diagnóstico de máquinas virtuales?
Para obtener más información sobre cómo modificar tooget y establecer la configuración de diagnósticos de Azure de hello, consulte [tooenable usar PowerShell diagnósticos de Azure en una máquina virtual ejecuta Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). 

Hola siguiente ejemplo obtiene la configuración de diagnósticos de Azure de hello:

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

Hola de ejemplo siguiente modifica la configuración de diagnósticos de Azure Hola. En esta configuración, se recopilan sólo 4624 de Id. de evento y 4625 de Id. de evento Hola seguridad registro de eventos. Microsoft Antimalware para los eventos de Azure se recopilan de registro de eventos del sistema de Hola. Para obtener detalles sobre el uso de Hola de expresiones XPath, vea [consumir eventos](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

Hello en el ejemplo siguiente se establece la configuración de diagnóstico de Azure hello:

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

Después de realizar cambios, compruebe tooensure de cuenta de almacenamiento de Hola que Hola correcta de los eventos se recopilan.

Si tiene problemas durante la instalación de Hola y configuración, abra una [solicitud de soporte técnico](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request). Seleccione **registro integración** como servicio de hello para el que está solicitando el soporte técnico.

## <a name="can-i-use-azure-log-integration-toointegrate-network-watcher-logs-into-my-siem"></a>¿Puedo usar registros de Monitor de red de integración de Azure Log toointegrate en mi SIEM?

Azure Network Watcher genera grandes cantidades de información de registro. Estos registros no son tooa toobe están hechos enviado SIEM. destino de Hello que solo se admite para los registros de Monitor de red es una cuenta de almacenamiento. Integración de registro de Azure no admite leer estos registros y dejándolos disponible tooa SIEM.

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
