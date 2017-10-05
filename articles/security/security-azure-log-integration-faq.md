---
title: "Preguntas más frecuentes sobre Azure Log Integration | Microsoft Docs"
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
ms.openlocfilehash: bfdc7154160bb6bb7dc9c46eb2352ce74310c4de
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-log-integration-faq"></a><span data-ttu-id="63667-103">Preguntas más frecuentes sobre Azure Log Integration</span><span class="sxs-lookup"><span data-stu-id="63667-103">Azure Log Integration FAQ</span></span>
<span data-ttu-id="63667-104">En este artículo se responden algunas preguntas frecuentes sobre Azure Log Integration.</span><span class="sxs-lookup"><span data-stu-id="63667-104">This article answers frequently asked questions (FAQ) about Azure Log Integration.</span></span> 

<span data-ttu-id="63667-105">Azure Log Integration es un servicio del sistema operativo Windows que puede usar para integrar los registros sin procesar de los recursos de Azure en los sistemas locales de administración de eventos e información de seguridad (SIEM).</span><span class="sxs-lookup"><span data-stu-id="63667-105">Azure Log Integration is a Windows operating system service that you can use to integrate raw logs from your Azure resources into your on-premises security information and event management (SIEM) systems.</span></span> <span data-ttu-id="63667-106">Esta integración le proporciona un panel unificado de todos los recursos, locales o en la nube.</span><span class="sxs-lookup"><span data-stu-id="63667-106">This integration provides a unified dashboard for all your assets, on-premises or in the cloud.</span></span> <span data-ttu-id="63667-107">Puede agregar, correlacionar, analizar y alertar sobre eventos de seguridad asociados con las aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="63667-107">You can then aggregate, correlate, analyze, and alert for security events associated with your applications.</span></span>

## <a name="is-the-azure-log-integration-software-free"></a><span data-ttu-id="63667-108">¿Es el software Integración de registro de Azure gratuito?</span><span class="sxs-lookup"><span data-stu-id="63667-108">Is the Azure Log Integration software free?</span></span>
<span data-ttu-id="63667-109">Sí.</span><span class="sxs-lookup"><span data-stu-id="63667-109">Yes.</span></span> <span data-ttu-id="63667-110">No hay ningún cargo por el software Integración de registro de Azure.</span><span class="sxs-lookup"><span data-stu-id="63667-110">There is no charge for the Azure Log Integration software.</span></span>

## <a name="where-is-azure-log-integration-available"></a><span data-ttu-id="63667-111">¿Dónde se encuentra disponible la integración de registro de Azure?</span><span class="sxs-lookup"><span data-stu-id="63667-111">Where is Azure Log Integration available?</span></span>

<span data-ttu-id="63667-112">Está actualmente disponible en la versión comercial de Azure y en Azure Government. No se encuentra disponible ni en China ni en Alemania.</span><span class="sxs-lookup"><span data-stu-id="63667-112">It is currently available in Azure Commercial and Azure Government and is not available in China or Germany.</span></span>

## <a name="how-can-i-see-the-storage-accounts-from-which-azure-log-integration-is-pulling-azure-vm-logs"></a><span data-ttu-id="63667-113">¿Cómo puedo ver las cuentas de almacenamiento desde las que el servicio Azure Log Integration extrae los registros de máquinas virtuales de Azure?</span><span class="sxs-lookup"><span data-stu-id="63667-113">How can I see the storage accounts from which Azure Log Integration is pulling Azure VM logs?</span></span>
<span data-ttu-id="63667-114">Ejecute el comando **azlog source list**.</span><span class="sxs-lookup"><span data-stu-id="63667-114">Run the command **azlog source list**.</span></span>

## <a name="how-can-i-tell-which-subscription-the-azure-log-integration-logs-are-from"></a><span data-ttu-id="63667-115">¿Cómo puedo saber de qué suscripción son los registros de integración de Azure?</span><span class="sxs-lookup"><span data-stu-id="63667-115">How can I tell which subscription the Azure Log Integration logs are from?</span></span>

<span data-ttu-id="63667-116">En el caso de los registros de auditoría que se colocan en los directorios **AzureResourcemanagerJson**, el identificador de la suscripción está en el nombre del archivo de registro.</span><span class="sxs-lookup"><span data-stu-id="63667-116">In the case of audit logs that are placed in the **AzureResourcemanagerJson** directories, the subscription ID is in the log file name.</span></span> <span data-ttu-id="63667-117">Esto también se aplica en el caso de los registros de la carpeta **AzureSecurityCenterJson**.</span><span class="sxs-lookup"><span data-stu-id="63667-117">This is also true for logs in the **AzureSecurityCenterJson** folder.</span></span> <span data-ttu-id="63667-118">Por ejemplo:</span><span class="sxs-lookup"><span data-stu-id="63667-118">For example:</span></span>

<span data-ttu-id="63667-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span><span class="sxs-lookup"><span data-stu-id="63667-119">20170407T070805_2768037.0000000023.**1111e5ee-1111-111b-a11e-1e111e1111dc**.json</span></span>

<span data-ttu-id="63667-120">Los registros de auditoría de Azure Active Directory incluyen el identificador del inquilino como parte del nombre.</span><span class="sxs-lookup"><span data-stu-id="63667-120">Azure Active Directory audit logs include the tenant ID as part of the name.</span></span>

<span data-ttu-id="63667-121">Los registros de diagnóstico que se leen desde una instancia de Event Hub no incluyen el identificador de suscripción como parte del nombre.</span><span class="sxs-lookup"><span data-stu-id="63667-121">Diagnostic logs that are read from an event hub do not include the subscription ID as part of the name.</span></span> <span data-ttu-id="63667-122">En su lugar, incluyen el nombre descriptivo especificado como parte de la creación del origen de la instancia de Event Hub.</span><span class="sxs-lookup"><span data-stu-id="63667-122">Instead, they include the friendly name specified as part of the creation of the event hub source.</span></span> 

## <a name="how-can-i-update-the-proxy-configuration"></a><span data-ttu-id="63667-123">¿Cómo se puede actualizar la configuración de proxy?</span><span class="sxs-lookup"><span data-stu-id="63667-123">How can I update the proxy configuration?</span></span>
<span data-ttu-id="63667-124">Si la configuración de proxy no permite el acceso a Azure Storage directamente, abra el archivo **AZLOG.EXE.CONFIG** en **c:\Program Files\Microsoft Azure Log Integration**.</span><span class="sxs-lookup"><span data-stu-id="63667-124">If your proxy setting does not allow Azure storage access directly, open the **AZLOG.EXE.CONFIG** file in **c:\Program Files\Microsoft Azure Log Integration**.</span></span> <span data-ttu-id="63667-125">Actualice el archivo para que incluya la sección **defaultProxy** con la dirección del proxy de su organización.</span><span class="sxs-lookup"><span data-stu-id="63667-125">Update the file to include the **defaultProxy** section with the proxy address of your organization.</span></span> <span data-ttu-id="63667-126">Después realizar la actualización, detenga e inicie el servicio mediante los comandos **net stop azlog** y **net start azlog**.</span><span class="sxs-lookup"><span data-stu-id="63667-126">After the update is done, stop and start the service by using the commands **net stop azlog** and **net start azlog**.</span></span>

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

## <a name="how-can-i-see-the-subscription-information-in-windows-events"></a><span data-ttu-id="63667-127">¿Cómo se puede ver la información de suscripción en los eventos de Windows?</span><span class="sxs-lookup"><span data-stu-id="63667-127">How can I see the subscription information in Windows events?</span></span>
<span data-ttu-id="63667-128">Al agregar el origen, anexe el identificador de suscripción al nombre descriptivo:</span><span class="sxs-lookup"><span data-stu-id="63667-128">Append the subscription ID to the friendly name while adding the source:</span></span>

    Azlog source add <sourcefriendlyname>.<subscription id> <StorageName> <StorageKey>  
<span data-ttu-id="63667-129">El archivo XML de eventos presenta los siguientes metadatos, incluido el identificador de suscripción:</span><span class="sxs-lookup"><span data-stu-id="63667-129">The event XML has the following metadata, including the subscription ID:</span></span>

![XML de eventos][1]

## <a name="error-messages"></a><span data-ttu-id="63667-131">mensajes de error</span><span class="sxs-lookup"><span data-stu-id="63667-131">Error messages</span></span>
### <a name="when-i-run-the-command-azlog-createazureid-why-do-i-get-the-following-error"></a><span data-ttu-id="63667-132">Cuando ejecuto el comando **azlog createazureid**, ¿por qué obtengo el siguiente error?</span><span class="sxs-lookup"><span data-stu-id="63667-132">When I run the command **azlog createazureid**, why do I get the following error?</span></span>
<span data-ttu-id="63667-133">Error:</span><span class="sxs-lookup"><span data-stu-id="63667-133">Error:</span></span>

  <span data-ttu-id="63667-134">*Failed to create AAD Application (Error al crear la aplicación de AAD): Inquilino 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'No tiene privilegios suficientes para completar la operación'.*</span><span class="sxs-lookup"><span data-stu-id="63667-134">*Failed to create AAD Application - Tenant 72f988bf-86f1-41af-91ab-2d7cd011db37 - Reason = 'Forbidden' - Message = 'Insufficient privileges to complete the operation.'*</span></span>

<span data-ttu-id="63667-135">El comando **Azlog createazureid** intenta crear una entidad de servicio en todos los inquilinos de Azure AD de las suscripciones a las que el inicio de sesión de Azure tiene acceso.</span><span class="sxs-lookup"><span data-stu-id="63667-135">The **azlog createazureid** command attempts to create a service principal in all the Azure AD tenants for the subscriptions that the Azure login has access to.</span></span> <span data-ttu-id="63667-136">Si el inicio de sesión de Azure es solo el de un usuario invitado en ese inquilino de Azure AD, el comando generará el error "No tiene privilegios suficientes para completar la operación".</span><span class="sxs-lookup"><span data-stu-id="63667-136">If your Azure login is only a guest user in that Azure AD tenant, the command fails with "Insufficient privileges to complete the operation."</span></span> <span data-ttu-id="63667-137">Solicite al administrador de inquilinos que agregue su cuenta como una cuenta de usuario en el inquilino.</span><span class="sxs-lookup"><span data-stu-id="63667-137">Ask the tenant admin to add your account as a user in the tenant.</span></span>

### <a name="when-i-run-the-command-azlog-authorize-why-do-i-get-the-following-error"></a><span data-ttu-id="63667-138">Cuando ejecuto el comando **azlog authorize**, ¿por qué obtengo el siguiente error?</span><span class="sxs-lookup"><span data-stu-id="63667-138">When I run the command **azlog authorize**, why do I get the following error?</span></span>
<span data-ttu-id="63667-139">Error:</span><span class="sxs-lookup"><span data-stu-id="63667-139">Error:</span></span>

  <span data-ttu-id="63667-140">*Advertencia de creación de la asignación de rol - AuthorizationFailed: el cliente janedo@microsoft.com con objeto de identificador fe9e03e4-4dad-4328-910f-fd24a9660bd2 no tiene autorización para realizar la acción Microsoft.Authorization/roleAssignments/write en el ámbito /subscriptions/70d95299-d689-4c97-b971-0d8ff0000000.*</span><span class="sxs-lookup"><span data-stu-id="63667-140">*Warning creating Role Assignment - AuthorizationFailed: The client janedo@microsoft.com' with object id 'fe9e03e4-4dad-4328-910f-fd24a9660bd2' does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/70d95299-d689-4c97-b971-0d8ff0000000'.*</span></span>

<span data-ttu-id="63667-141">El comando **azlog authorize** asigna el rol Lector a la entidad de servicio de Azure AD (creada con **azlog createazureid**) para las suscripciones proporcionadas.</span><span class="sxs-lookup"><span data-stu-id="63667-141">The **azlog authorize** command assigns the role of reader to the Azure AD service principal (created with **azlog createazureid**) to the provided subscriptions.</span></span> <span data-ttu-id="63667-142">Si el inicio de sesión de Azure no se realiza mediante una cuenta de coadministrador o de propietario de la suscripción, se producirá el error "Error de autorización".</span><span class="sxs-lookup"><span data-stu-id="63667-142">If the Azure login is not a co-administrator or an owner of the subscription, it fails with an "Authorization Failed" error message.</span></span> <span data-ttu-id="63667-143">Se necesita el control de acceso basado en roles de Azure (RBAC) de una cuenta de coadministrador o de propietario para completar esta acción.</span><span class="sxs-lookup"><span data-stu-id="63667-143">Azure Role-Based Access Control (RBAC) of co-administrator or owner is needed to complete this action.</span></span>

## <a name="where-can-i-find-the-definition-of-the-properties-in-the-audit-log"></a><span data-ttu-id="63667-144">¿Dónde puedo encontrar la definición de las propiedades de registro de auditoría?</span><span class="sxs-lookup"><span data-stu-id="63667-144">Where can I find the definition of the properties in the audit log?</span></span>
<span data-ttu-id="63667-145">Consulte:</span><span class="sxs-lookup"><span data-stu-id="63667-145">See:</span></span>

* [<span data-ttu-id="63667-146">Operaciones de auditoría con Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="63667-146">Audit operations with Azure Resource Manager</span></span>](../azure-resource-manager/resource-group-audit.md)
* [<span data-ttu-id="63667-147">Lista de los eventos de administración de una suscripción en la API de REST de Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="63667-147">List the management events in a subscription in the Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931934.aspx)

## <a name="where-can-i-find-details-on-azure-security-center-alerts"></a><span data-ttu-id="63667-148">¿Dónde puedo encontrar detalles sobre las alertas de Azure Security Center?</span><span class="sxs-lookup"><span data-stu-id="63667-148">Where can I find details on Azure Security Center alerts?</span></span>
<span data-ttu-id="63667-149">Consulte [Administración y respuesta a las alertas de seguridad en Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="63667-149">See [Managing and responding to security alerts in Azure Security Center](../security-center/security-center-managing-and-responding-alerts.md).</span></span>

## <a name="how-can-i-modify-what-is-collected-with-vm-diagnostics"></a><span data-ttu-id="63667-150">¿Cómo puedo modificar la información recopilada mediante el diagnóstico de máquinas virtuales?</span><span class="sxs-lookup"><span data-stu-id="63667-150">How can I modify what is collected with VM diagnostics?</span></span>
<span data-ttu-id="63667-151">Consulte [Uso de PowerShell para habilitar Azure Diagnostics en una máquina virtual con Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) para más información acerca de cómo obtener, modificar y configurar Azure Diagnostics en Window.</span><span class="sxs-lookup"><span data-stu-id="63667-151">For details on how to get, modify, and set the Azure Diagnostics configuration, see [Use PowerShell to enable Azure Diagnostics in a virtual machine running Windows](../virtual-machines/windows/ps-extensions-diagnostics.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="63667-152">En el ejemplo siguiente se muestra la configuración de Azure Diagnostics:</span><span class="sxs-lookup"><span data-stu-id="63667-152">The following example gets the Azure Diagnostics configuration:</span></span>

    -AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient
    $publicsettings = (Get-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient).PublicSettings
    $encodedconfig = (ConvertFrom-Json -InputObject $publicsettings).xmlCfg
    $xmlconfig = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($encodedconfig))
    Write-Host $xmlconfig

    $xmlconfig | Out-File -Encoding utf8 -FilePath "d:\WADConfig.xml"

<span data-ttu-id="63667-153">En el ejemplo siguiente se modifica la configuración de Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="63667-153">The following example modifies the Azure Diagnostics configuration.</span></span> <span data-ttu-id="63667-154">En esta configuración, se recopilan solo los eventos ID 4624 e ID 4625 del registro de eventos de seguridad.</span><span class="sxs-lookup"><span data-stu-id="63667-154">In this configuration, only event ID 4624 and event ID 4625 are collected from the security event log.</span></span> <span data-ttu-id="63667-155">Los eventos de Microsoft Antimalware para Azure se recopilan desde el registro de eventos del sistema.</span><span class="sxs-lookup"><span data-stu-id="63667-155">Microsoft Antimalware for Azure events are collected from the system event log.</span></span> <span data-ttu-id="63667-156">Para más información sobre el uso de expresiones XPath, consulte [Consumo de eventos](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span><span class="sxs-lookup"><span data-stu-id="63667-156">For details on the use of XPath expressions, see [Consuming Events](https://msdn.microsoft.com/library/windows/desktop/dd996910(v=vs.85)).</span></span>

    <WindowsEventLog scheduledTransferPeriod="PT1M">
        <DataSource name="Security!*[System[(EventID=4624 or EventID=4625)]]" />
        <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>
    </WindowsEventLog>

<span data-ttu-id="63667-157">En el ejemplo siguiente se establece la configuración de Azure Diagnostics:</span><span class="sxs-lookup"><span data-stu-id="63667-157">The following example sets the Azure Diagnostics configuration:</span></span>

    $diagnosticsconfig_path = "d:\WADConfig.xml"
    Set-AzureRmVMDiagnosticsExtension -ResourceGroupName AzLog-Integration -VMName AzlogClient -DiagnosticsConfigurationPath $diagnosticsconfig_path -StorageAccountName log3121 -StorageAccountKey <storage key>

<span data-ttu-id="63667-158">Después de realizar cambios, compruebe la cuenta de almacenamiento para asegurarse de que se recopilan los eventos correctos.</span><span class="sxs-lookup"><span data-stu-id="63667-158">After you make changes, check the storage account to ensure that the correct events are collected.</span></span>

<span data-ttu-id="63667-159">Si tiene algún problema durante la instalación y configuración, abra una [solicitud de soporte técnico](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span><span class="sxs-lookup"><span data-stu-id="63667-159">If you have any issues during the installation and configuration, please open a [support request](https://docs.microsoft.com/azure/azure-supportability/how-to-create-azure-support-request).</span></span> <span data-ttu-id="63667-160">Seleccione **Azure Log Integration** como el servicio para el que está solicitando el soporte técnico.</span><span class="sxs-lookup"><span data-stu-id="63667-160">Select **Log Integration** as the service for which you are requesting support.</span></span>

## <a name="can-i-use-azure-log-integration-to-integrate-network-watcher-logs-into-my-siem"></a><span data-ttu-id="63667-161">¿Puedo usar Azure Log Integration para integrar los registros de Network Watcher en mi SIEM?</span><span class="sxs-lookup"><span data-stu-id="63667-161">Can I use Azure Log Integration to integrate Network Watcher logs into my SIEM?</span></span>

<span data-ttu-id="63667-162">Azure Network Watcher genera grandes cantidades de información de registro.</span><span class="sxs-lookup"><span data-stu-id="63667-162">Azure Network Watcher generates large quantities of logging information.</span></span> <span data-ttu-id="63667-163">Estos registros no están diseñados para enviarse a un SIEM.</span><span class="sxs-lookup"><span data-stu-id="63667-163">These logs are not meant to be sent to a SIEM.</span></span> <span data-ttu-id="63667-164">El único destino admitido para los registros de Network Watcher es una cuenta de almacenamiento.</span><span class="sxs-lookup"><span data-stu-id="63667-164">The only supported destination for Network Watcher logs is a storage account.</span></span> <span data-ttu-id="63667-165">Azure Log Integration no admite la lectura de estos registros ni su envío a un SIEM.</span><span class="sxs-lookup"><span data-stu-id="63667-165">Azure Log Integration does not support reading these logs and making them available to a SIEM.</span></span>

<!--Image references-->
[1]: ./media/security-azure-log-integration-faq/event-xml.png
