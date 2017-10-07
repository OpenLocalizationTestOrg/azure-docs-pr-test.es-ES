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
# <a name="azure-log-integration-faq"></a><span data-ttu-id="9b5d4-103">Preguntas más frecuentes sobre Azure Log Integration</span><span class="sxs-lookup"><span data-stu-id="9b5d4-103">Azure Log Integration FAQ</span></span>
<span data-ttu-id="9b5d4-104">En este artículo se responden algunas preguntas frecuentes sobre Azure Log Integration.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-104">This article answers frequently asked questions (FAQ) about Azure Log Integration.</span></span> 

<span data-ttu-id="9b5d4-105">Integración de registro de Azure es un servicio de sistema operativo de Windows que puede usar los registros de toointegrate sin procesar de los recursos de Azure en los sistemas de administración (SIEM) de eventos e información de seguridad de local.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-105">Azure Log Integration is a Windows operating system service that you can use toointegrate raw logs from your Azure resources into your on-premises security information and event management (SIEM) systems.</span></span> <span data-ttu-id="9b5d4-106">Esta integración proporciona una consola unificada para todos sus activos, local o en la nube de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-106">This integration provides a unified dashboard for all your assets, on-premises or in hello cloud.</span></span> <span data-ttu-id="9b5d4-107">Puede agregar, correlacionar, analizar y alertar sobre eventos de seguridad asociados con las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-107">You can then aggregate, correlate, analyze, and alert for security events associated with your applications.</span></span>

## <a name="is-hello-azure-log-integration-software-free"></a><span data-ttu-id="9b5d4-108">¿Es un software de integración de Azure registro de hello gratuita?</span><span class="sxs-lookup"><span data-stu-id="9b5d4-108">Is hello Azure Log Integration software free?</span></span>
<span data-ttu-id="9b5d4-109">Sí.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-109">Yes.</span></span> <span data-ttu-id="9b5d4-110">No hay ningún cargo por hello software de integración de registro de Azure.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-110">There is no charge for hello Azure Log Integration software.</span></span>

## <a name="where-is-azure-log-integration-available"></a><span data-ttu-id="9b5d4-111">¿Dónde se encuentra disponible la integración de registro de Azure?</span><span class="sxs-lookup"><span data-stu-id="9b5d4-111">Where is Azure Log Integration available?</span></span>

<span data-ttu-id="9b5d4-112">Está actualmente disponible en la versión comercial de Azure y en Azure Government. No se encuentra disponible ni en China ni en Alemania.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-112">It is currently available in Azure Commercial and Azure Government and is not available in China or Germany.</span></span>

## <a name="how-can-i-see-hello-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a><span data-ttu-id="9b5d4-113">¿Cómo se puede ver las cuentas de almacenamiento de Hola desde el que Azure registro integración extrae los registros de máquina virtual de Azure?</span><span class="sxs-lookup"><span data-stu-id="9b5d4-113">How can I see hello storage accounts from which Azure Log Integration is pulling Azure VM logs?</span></span>
<span data-ttu-id="9b5d4-114">Ejecute el comando de hello **lista de orígenes de azlog**.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-114">Run hello command **azlog source list**.</span></span>

## <a name="how-can-i-tell-which-subscription-hello-azure-log-integration-logs-are-from"></a><span data-ttu-id="9b5d4-115">¿Cómo puedo saber qué Hola suscripción Azure integración de registros son registros de?</span><span class="sxs-lookup"><span data-stu-id="9b5d4-115">How can I tell which subscription hello Azure Log Integration logs are from?</span></span>

<span data-ttu-id="9b5d4-116">En caso de hello de los registros de auditoría que se colocan en hello **AzureResourcemanagerJson** directorios, Id. de suscripción de hello es en nombre de archivo de registro de hello.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-116">In hello case of audit logs that are placed in hello **AzureResourcemanagerJson** directories, hello subscription ID is in hello log file name.</span></span> <span data-ttu-id="9b5d4-117">Esto también es cierto para los registros en hello **AzureSecurityCenterJson** carpeta.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-117">This is also true for logs in hello **AzureSecurityCenterJson** folder.</span></span> <span data-ttu-id="9b5d4-118">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="9b5d4-118">For example:</span></span>

<span data-ttu-id="9b5d4-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span><span class="sxs-lookup"><span data-stu-id="9b5d4-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span></span>

<span data-ttu-id="9b5d4-120">Los registros de auditoría de Azure Active Directory incluyen hello Id. de inquilino como parte del nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-120">Azure Active Directory audit logs include hello tenant ID as part of hello name.</span></span>

<span data-ttu-id="9b5d4-121">Registros de diagnóstico que se leen desde un centro de eventos no incluyen el Id. de suscripción de hello como parte del nombre de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-121">Diagnostic logs that are read from an event hub do not include hello subscription ID as part of hello name.</span></span> <span data-ttu-id="9b5d4-122">En cambio, incluyen Nombre_descriptivo hello, especificado como parte de la creación de Hola Hola concentrador del origen de evento.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-122">Instead, they include hello friendly name specified as part of hello creation of hello event hub source.</span></span> 

## <a name="how-can-i-update-hello-proxy-configuration"></a><span data-ttu-id="9b5d4-123">¿Cómo puedo actualizar configuración de proxy de hello?</span><span class="sxs-lookup"><span data-stu-id="9b5d4-123">How can I update hello proxy configuration?</span></span>
<span data-ttu-id="9b5d4-124">Si el configuración del proxy no permite el acceso de almacenamiento de Azure directamente, abra hello **AZLOG. EXE. CONFIGURACIÓN** en el archivo **c:\Program Files\Microsoft Azure registro integración**.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-124">If your proxy setting does not allow Azure storage access directly, open hello **AZLOG.EXE.CONFIG** file in **c:\Program Files\Microsoft Azure Log Integration**.</span></span> <span data-ttu-id="9b5d4-125">Actualización Hola archivo tooinclude Hola **defaultProxy** sección con la dirección de proxy de Hola de su organización.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-125">Update hello file tooinclude hello **defaultProxy** section with hello proxy address of your organization.</span></span> <span data-ttu-id="9b5d4-126">Después de realiza la actualización de hello, detenga e inicie el servicio de hello mediante comandos de hello **net stop azlog** y **azlog del comando net start**.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-126">After hello update is done, stop and start hello service by using hello commands **net stop azlog** and **net start azlog**.</span></span>

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

## <a name="how-can-i-see-hello-subscription-information-in-windows-events"></a><span data-ttu-id="9b5d4-127">¿Cómo se puede ver la información de suscripción de hello en los eventos de Windows?</span><span class="sxs-lookup"><span data-stu-id="9b5d4-127">How can I see hello subscription information in Windows events?</span></span>
<span data-ttu-id="9b5d4-128">Anexar nombre descriptivo del toohello de Id. de hello suscripción al agregar el origen de hello:</span><span class="sxs-lookup"><span data-stu-id="9b5d4-128">Append hello subscription ID toohello friendly name while adding hello source:</span></span>

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
<span data-ttu-id="9b5d4-129">evento de Hello XML tiene Hola después de metadatos, incluidos el identificador de suscripción de hello:</span><span class="sxs-lookup"><span data-stu-id="9b5d4-129">hello event XML has hello following metadata, including hello subscription ID:</span></span>

![XML de eventos][1]

## <a name="error-messages"></a><span data-ttu-id="9b5d4-131">mensajes de error</span><span class="sxs-lookup"><span data-stu-id="9b5d4-131">Error messages</span></span>
### <a name="when-i-run-hello-command-azlog-createazureid-why-do-i-get-hello-following-error"></a><span data-ttu-id="9b5d4-132">Al ejecutar el comando de Hola **azlog createazureid**, ¿por qué recibo Hola tras error?</span><span class="sxs-lookup"><span data-stu-id="9b5d4-132">When I run hello command **azlog createazureid**, why do I get hello following error?</span></span>
<span data-ttu-id="9b5d4-133">Error:</span><span class="sxs-lookup"><span data-stu-id="9b5d4-133">Error:</span></span>

  <span data-ttu-id="9b5d4-134">*No se pudo toocreate aplicación AAD - inquilino 72f988bf-86f1-41af-91ab-2d7cd011db37 - motivo = 'Prohibido' - mensaje = "privilegios suficientes toocomplete hello en la operación."*</span><span class="sxs-lookup"><span data-stu-id="9b5d4-134">*Failed toocreate AAD Application - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'Insufficient privileges toocomplete hello operation.'*</span></span>

<span data-ttu-id="9b5d4-135">Hola **azlog createazureid** toocreate una entidad de servicio en todos los inquilinos de hello Azure AD para las suscripciones de Hola Hola Azure inicio de sesión tiene acceso a los intentos de comando.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-135">hello **azlog createazureid** command attempts toocreate a service principal in all hello Azure AD tenants for hello subscriptions that hello Azure login has access to.</span></span> <span data-ttu-id="9b5d4-136">Si el inicio de sesión de Azure es solo un usuario invitado en ese inquilino de Azure AD, se produce un error en comando hello con "operación de hello toocomplete de privilegios suficientes."</span><span class="sxs-lookup"><span data-stu-id="9b5d4-136">If your Azure login is only a guest user in that Azure AD tenant, hello command fails with "Insufficient privileges toocomplete hello operation."</span></span> <span data-ttu-id="9b5d4-137">Pida inquilino Hola admin tooadd tu cuenta como un usuario de inquilino de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-137">Ask hello tenant admin tooadd your account as a user in hello tenant.</span></span>

### <a name="when-i-run-hello-command-azlog-authorize-why-do-i-get-hello-following-error"></a><span data-ttu-id="9b5d4-138">Al ejecutar el comando de Hola **azlog autorizar**, ¿por qué recibo Hola tras error?</span><span class="sxs-lookup"><span data-stu-id="9b5d4-138">When I run hello command **azlog authorize**, why do I get hello following error?</span></span>
<span data-ttu-id="9b5d4-139">Error:</span><span class="sxs-lookup"><span data-stu-id="9b5d4-139">Error:</span></span>

  <span data-ttu-id="9b5d4-140">*Advertencia de creación de asignación de roles - AuthorizationFailed: cliente hello janedo@microsoft.com' con objeto de identificador 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' no tiene autorización tooperform acción 'Microsoft.Authorization/roleAssignments/write' sobre el ámbito ' / las suscripciones / 70d 95299-d689-4c 97-b971-0d8ff0000000'.*</span><span class="sxs-lookup"><span data-stu-id="9b5d4-140">*Warning creating Role Assignment - AuthorizationFailed: hello client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span></span>

<span data-ttu-id="9b5d4-141">Hola **azlog autorizar** comando asigna Hola rol de entidad de servicio de lector toohello Azure AD (creado con **azlog createazureid**) toohello proporciona suscripciones.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-141">hello **azlog authorize** command assigns hello role of reader toohello Azure AD service principal (created with **azlog createazureid**) toohello provided subscriptions.</span></span> <span data-ttu-id="9b5d4-142">Si hello Azure inicio de sesión no es un administrador o el propietario de la suscripción de hello, se produce un error con un mensaje de error "Error de autorización".</span><span class="sxs-lookup"><span data-stu-id="9b5d4-142">If hello Azure login is not a co-administrator or an owner of hello subscription, it fails with an "Authorization Failed" error message.</span></span> <span data-ttu-id="9b5d4-143">Azure Role-Based Access Control (RBAC) del administrador o propietario es necesario toocomplete esta acción.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-143">Azure Role-Based Access Control (RBAC) of co-administrator or owner is needed toocomplete this action.</span></span>

## <a name="where-can-i-find-hello-definition-of-hello-properties-in-hello-audit-log"></a><span data-ttu-id="9b5d4-144">¿Dónde puedo encontrar definición Hola de propiedades de hello en el registro de auditoría de hello?</span><span class="sxs-lookup"><span data-stu-id="9b5d4-144">Where can I find hello definition of hello properties in hello audit log?</span></span>
<span data-ttu-id="9b5d4-145">Consulte:</span><span class="sxs-lookup"><span data-stu-id="9b5d4-145">See:</span></span>

* [<span data-ttu-id="9b5d4-146">Operaciones de auditoría con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="9b5d4-146">Audit operations with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-audit.md)
* [<span data-ttu-id="9b5d4-147">Lista de los eventos de administración de hello en una suscripción en hello API de REST de Monitor de Azure</span><span class="sxs-lookup"><span data-stu-id="9b5d4-147">List hello management events in a subscription in hello Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a><span data-ttu-id="9b5d4-148">¿Dónde puedo encontrar detalles sobre las alertas de Azure Security Center?</span><span class="sxs-lookup"><span data-stu-id="9b5d4-148">Where can I find details on Azure Security Center alerts?</span></span>
<span data-ttu-id="9b5d4-149">Vea [toosecurity responde y administrar las alertas en Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="9b5d4-149">See [Managing and responding toosecurity alerts in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span></span>

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a><span data-ttu-id="9b5d4-150">¿Cómo puedo modificar la información recopilada mediante el diagnóstico de máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="9b5d4-150">How can I modify what is collected with VM diagnostics?</span></span>
<span data-ttu-id="9b5d4-151">Para obtener más información sobre cómo modificar tooget y establecer la configuración de diagnósticos de Azure de hello, consulte [tooenable usar PowerShell diagnósticos de Azure en una máquina virtual ejecuta Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9b5d4-151">For details on how tooget, modify, and set hello Azure Diagnostics configuration, see [Use PowerShell tooenable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="9b5d4-152">Hola siguiente ejemplo obtiene la configuración de diagnósticos de Azure de hello:</span><span class="sxs-lookup"><span data-stu-id="9b5d4-152">hello following example gets hello Azure Diagnostics configuration:</span></span>

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

<span data-ttu-id="9b5d4-153">Hola de ejemplo siguiente modifica la configuración de diagnósticos de Azure Hola.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-153">hello following example modifies hello Azure Diagnostics configuration.</span></span> <span data-ttu-id="9b5d4-154">En esta configuración, se recopilan sólo 4624 de Id. de evento y 4625 de Id. de evento Hola seguridad registro de eventos.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-154">In this configuration, only event ID 4624 and event ID 4625 are collected from hello security event log.</span></span> <span data-ttu-id="9b5d4-155">Microsoft Antimalware para los eventos de Azure se recopilan de registro de eventos del sistema de Hola.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-155">Microsoft Antimalware for Azure events are collected from hello system event log.</span></span> <span data-ttu-id="9b5d4-156">Para obtener detalles sobre el uso de Hola de expresiones XPath, vea [consumir eventos](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="9b5d4-156">For details on hello use of XPath expressions, see [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span></span>

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

<span data-ttu-id="9b5d4-157">Hello en el ejemplo siguiente se establece la configuración de diagnóstico de Azure hello:</span><span class="sxs-lookup"><span data-stu-id="9b5d4-157">hello following example sets hello Azure Diagnostics configuration:</span></span>

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

<span data-ttu-id="9b5d4-158">Después de realizar cambios, compruebe tooensure de cuenta de almacenamiento de Hola que Hola correcta de los eventos se recopilan.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-158">After you make changes, check hello storage account tooensure that hello correct events are collected.</span></span>

<span data-ttu-id="9b5d4-159">Si tiene problemas durante la instalación de Hola y configuración, abra una [solicitud de soporte técnico](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span><span class="sxs-lookup"><span data-stu-id="9b5d4-159">If you have any issues during hello installation and configuration, please open a [support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span></span> <span data-ttu-id="9b5d4-160">Seleccione **registro integración** como servicio de hello para el que está solicitando el soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-160">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="can-i-use-azure-log-integration-toointegrate-network-watcher-logs-into-my-siem"></a><span data-ttu-id="9b5d4-161">¿Puedo usar registros de Monitor de red de integración de Azure Log toointegrate en mi SIEM?</span><span class="sxs-lookup"><span data-stu-id="9b5d4-161">Can I use Azure Log Integration toointegrate Network Watcher logs into my SIEM?</span></span>

<span data-ttu-id="9b5d4-162">Azure Network Watcher genera grandes cantidades de información de registro.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-162">Azure Network Watcher generates large quantities of logging information.</span></span> <span data-ttu-id="9b5d4-163">Estos registros no son tooa toobe están hechos enviado SIEM.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-163">These logs are not meant toobe sent tooa SIEM.</span></span> <span data-ttu-id="9b5d4-164">destino de Hello que solo se admite para los registros de Monitor de red es una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-164">hello only supported destination for Network Watcher logs is a storage account.</span></span> <span data-ttu-id="9b5d4-165">Integración de registro de Azure no admite leer estos registros y dejándolos disponible tooa SIEM.</span><span class="sxs-lookup"><span data-stu-id="9b5d4-165">Azure Log Integration does not support reading these logs and making them available tooa SIEM.</span></span>

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
