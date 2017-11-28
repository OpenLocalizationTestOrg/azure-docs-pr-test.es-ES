---
title: Conceptos de seguridad de IoT Hub de Azure | Microsoft Docs
description: "Guía del desarrollador: se explica cómo controlar el acceso a IoT Hub para aplicaciones de dispositivo y de back-end. Además, incluye información sobre los tokens de seguridad y la compatibilidad con certificados X.509."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 45631e70-865b-4e06-bb1d-aae1175a52ba
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/08/2017
ms.author: dobett
ms.openlocfilehash: e4fe5400ffcf4446392015aada031dd4dfbf238a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/18/2017
---
# <a name="control-access-to-iot-hub"></a><span data-ttu-id="24dc5-104">Control del acceso a IoT Hub</span><span class="sxs-lookup"><span data-stu-id="24dc5-104">Control access to IoT Hub</span></span>

<span data-ttu-id="24dc5-105">En esta sección se describen las opciones para proteger su instancia de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="24dc5-105">This article describes the options for securing your IoT hub.</span></span> <span data-ttu-id="24dc5-106">IoT Hub usa *permisos* para conceder acceso a cada uno de los puntos de conexión de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="24dc5-106">IoT Hub uses *permissions* to grant access to each IoT hub endpoint.</span></span> <span data-ttu-id="24dc5-107">Los permisos limitan el acceso a un centro de IoT basado en la funcionalidad.</span><span class="sxs-lookup"><span data-stu-id="24dc5-107">Permissions limit the access to an IoT hub based on functionality.</span></span>

<span data-ttu-id="24dc5-108">En este artículo se describe:</span><span class="sxs-lookup"><span data-stu-id="24dc5-108">This article describes:</span></span>

* <span data-ttu-id="24dc5-109">Los distintos permisos que puede conceder a un dispositivo o una aplicación de back-end para acceder a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="24dc5-109">The different permissions that you can grant to a device or back-end app to access your IoT hub.</span></span>
* <span data-ttu-id="24dc5-110">El proceso de autenticación y los tokens que utiliza para comprobar los permisos.</span><span class="sxs-lookup"><span data-stu-id="24dc5-110">The authentication process and the tokens it uses to verify permissions.</span></span>
* <span data-ttu-id="24dc5-111">Cómo definir el ámbito de las credenciales para limitar el acceso a recursos específicos.</span><span class="sxs-lookup"><span data-stu-id="24dc5-111">How to scope credentials to limit access to specific resources.</span></span>
* <span data-ttu-id="24dc5-112">IoT Hub admite los certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="24dc5-112">IoT Hub support for X.509 certificates.</span></span>
* <span data-ttu-id="24dc5-113">Los mecanismos de autenticación de dispositivo personalizado que utilizan los registros de identidad de dispositivo o los esquemas de autenticación.</span><span class="sxs-lookup"><span data-stu-id="24dc5-113">Custom device authentication mechanisms that use existing device identity registries or authentication schemes.</span></span>

### <a name="when-to-use"></a><span data-ttu-id="24dc5-114">Cuándo se deben usar</span><span class="sxs-lookup"><span data-stu-id="24dc5-114">When to use</span></span>

<span data-ttu-id="24dc5-115">Debe tener los permisos adecuados para acceder a cualquiera de los puntos de conexión de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="24dc5-115">You must have appropriate permissions to access any of the IoT Hub endpoints.</span></span> <span data-ttu-id="24dc5-116">Por ejemplo, un dispositivo debe incluir un token que contiene las credenciales de seguridad junto con cada mensaje que se envía a IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="24dc5-116">For example, a device must include a token containing security credentials along with every message it sends to IoT Hub.</span></span>

## <a name="access-control-and-permissions"></a><span data-ttu-id="24dc5-117">Permisos y control del acceso</span><span class="sxs-lookup"><span data-stu-id="24dc5-117">Access control and permissions</span></span>

<span data-ttu-id="24dc5-118">Puede conceder los [permisos](#iot-hub-permissions) de las maneras siguientes:</span><span class="sxs-lookup"><span data-stu-id="24dc5-118">You can grant [permissions](#iot-hub-permissions) in the following ways:</span></span>

* <span data-ttu-id="24dc5-119">**Directivas de acceso compartido de nivel de centro de IoT**.</span><span class="sxs-lookup"><span data-stu-id="24dc5-119">**IoT hub-level shared access policies**.</span></span> <span data-ttu-id="24dc5-120">Las directivas de acceso compartido pueden conceder cualquier combinación de los [permisos](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="24dc5-120">Shared access policies can grant any combination of [permissions](#iot-hub-permissions).</span></span> <span data-ttu-id="24dc5-121">Puede definir las directivas en [Azure Portal][lnk-management-portal] o mediante programación usando las [API de REST del proveedor de recursos de IoT Hub][lnk-resource-provider-apis].</span><span class="sxs-lookup"><span data-stu-id="24dc5-121">You can define policies in the [Azure portal][lnk-management-portal], or programmatically by using the [IoT Hub resource provider REST APIs][lnk-resource-provider-apis].</span></span> <span data-ttu-id="24dc5-122">Un Centro de IoT recién creado tiene las siguientes directivas predeterminadas:</span><span class="sxs-lookup"><span data-stu-id="24dc5-122">A newly created IoT hub has the following default policies:</span></span>

  * <span data-ttu-id="24dc5-123">**iothubowner**: directiva con todos los permisos.</span><span class="sxs-lookup"><span data-stu-id="24dc5-123">**iothubowner**: Policy with all permissions.</span></span>
  * <span data-ttu-id="24dc5-124">**service**: directiva con el permiso **ServiceConnect**.</span><span class="sxs-lookup"><span data-stu-id="24dc5-124">**service**: Policy with **ServiceConnect** permission.</span></span>
  * <span data-ttu-id="24dc5-125">**device**: directiva con el permiso **DeviceConnect**.</span><span class="sxs-lookup"><span data-stu-id="24dc5-125">**device**: Policy with **DeviceConnect** permission.</span></span>
  * <span data-ttu-id="24dc5-126">**registryRead**: directiva con el permiso **RegistryRead**.</span><span class="sxs-lookup"><span data-stu-id="24dc5-126">**registryRead**: Policy with **RegistryRead** permission.</span></span>
  * <span data-ttu-id="24dc5-127">**registryReadWrite**: directiva con los permisos **RegistryRead** y RegistryWrite.</span><span class="sxs-lookup"><span data-stu-id="24dc5-127">**registryReadWrite**: Policy with **RegistryRead** and RegistryWrite permissions.</span></span>
  * <span data-ttu-id="24dc5-128">**Credenciales de seguridad de cada dispositivo**.</span><span class="sxs-lookup"><span data-stu-id="24dc5-128">**Per-device security credentials**.</span></span> <span data-ttu-id="24dc5-129">Cada centro de IoT contiene un [registro de identidades][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="24dc5-129">Each IoT Hub contains an [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="24dc5-130">Para cada dispositivo de este registro de identidades, puede configurar credenciales de seguridad que concedan permisos **DeviceConnect** orientados a los puntos de conexión del dispositivo correspondiente.</span><span class="sxs-lookup"><span data-stu-id="24dc5-130">For each device in this identity registry, you can configure security credentials that grant **DeviceConnect** permissions scoped to the corresponding device endpoints.</span></span>

<span data-ttu-id="24dc5-131">Por ejemplo en una solución típica de IoT:</span><span class="sxs-lookup"><span data-stu-id="24dc5-131">For example, in a typical IoT solution:</span></span>

* <span data-ttu-id="24dc5-132">El componente de administración de dispositivos usa la directiva *registryReadWrite* .</span><span class="sxs-lookup"><span data-stu-id="24dc5-132">The device management component uses the *registryReadWrite* policy.</span></span>
* <span data-ttu-id="24dc5-133">El componente de procesador de eventos usa la directiva *service* .</span><span class="sxs-lookup"><span data-stu-id="24dc5-133">The event processor component uses the *service* policy.</span></span>
* <span data-ttu-id="24dc5-134">El componente de lógica empresarial de dispositivos en tiempo de ejecución usa la directiva *service* .</span><span class="sxs-lookup"><span data-stu-id="24dc5-134">The run-time device business logic component uses the *service* policy.</span></span>
* <span data-ttu-id="24dc5-135">Los dispositivos individuales se conectan usando las credenciales almacenadas en el registro de identidades del centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="24dc5-135">Individual devices connect using credentials stored in the IoT hub's identity registry.</span></span>

> [!NOTE]
> <span data-ttu-id="24dc5-136">Para más detalles, vea [Permisos](#iot-hub-permissions).</span><span class="sxs-lookup"><span data-stu-id="24dc5-136">See [permissions](#iot-hub-permissions) for detailed information.</span></span>

## <a name="authentication"></a><span data-ttu-id="24dc5-137">Autenticación</span><span class="sxs-lookup"><span data-stu-id="24dc5-137">Authentication</span></span>

<span data-ttu-id="24dc5-138">Azure IoT Hub concede acceso a los puntos de conexión mediante la comprobación de un token con las directivas de acceso compartido y las credenciales de seguridad del registro de identidad.</span><span class="sxs-lookup"><span data-stu-id="24dc5-138">Azure IoT Hub grants access to endpoints by verifying a token against the shared access policies and identity registry security credentials.</span></span>

<span data-ttu-id="24dc5-139">Las credenciales de seguridad, como las claves simétricas, nunca se envían en la conexión.</span><span class="sxs-lookup"><span data-stu-id="24dc5-139">Security credentials, such as symmetric keys, are never sent over the wire.</span></span>

> [!NOTE]
> <span data-ttu-id="24dc5-140">El proveedor de recursos de Azure IoT Hub se protege mediante la suscripción de Azure, igual que todos los proveedores en [Azure Resource Manager][lnk-azure-resource-manager].</span><span class="sxs-lookup"><span data-stu-id="24dc5-140">The Azure IoT Hub resource provider is secured through your Azure subscription, as are all providers in the [Azure Resource Manager][lnk-azure-resource-manager].</span></span>

<span data-ttu-id="24dc5-141">Consulte el artículo [Tokens de seguridad][lnk-sas-tokens] para más información sobre cómo crear y utilizar tokens de seguridad.</span><span class="sxs-lookup"><span data-stu-id="24dc5-141">For more information about how to construct and use security tokens, see [IoT Hub security tokens][lnk-sas-tokens].</span></span>

### <a name="protocol-specifics"></a><span data-ttu-id="24dc5-142">Detalles específicos de protocolo</span><span class="sxs-lookup"><span data-stu-id="24dc5-142">Protocol specifics</span></span>

<span data-ttu-id="24dc5-143">Cada protocolo admitido, como MQTT, AMQP y HTTP, transporta tokens de diferentes maneras.</span><span class="sxs-lookup"><span data-stu-id="24dc5-143">Each supported protocol, such as MQTT, AMQP, and HTTP, transports tokens in different ways.</span></span>

<span data-ttu-id="24dc5-144">Al utilizar MQTT, el paquete CONNECT tiene deviceId como ClientId, {iothubhostname}/{deviceId} en el campo Nombre de usuario y un token SAS en el campo Contraseña.</span><span class="sxs-lookup"><span data-stu-id="24dc5-144">When using MQTT, the CONNECT packet has the deviceId as the ClientId, {iothubhostname}/{deviceId} in the Username field, and a SAS token in the Password field.</span></span> <span data-ttu-id="24dc5-145">{iothubhostname} debe ser el CName completo del centro de IoT (por ejemplo, contoso.azure-devices.net).</span><span class="sxs-lookup"><span data-stu-id="24dc5-145">{iothubhostname} should be the full CName of the IoT hub (for example, contoso.azure-devices.net).</span></span>

<span data-ttu-id="24dc5-146">Al usar [AMQP][lnk-amqp], IoT Hub admite [SASL PLAIN][lnk-sasl-plain] y [seguridad basada en notificaciones AMQP][lnk-cbs].</span><span class="sxs-lookup"><span data-stu-id="24dc5-146">When using [AMQP][lnk-amqp], IoT Hub supports [SASL PLAIN][lnk-sasl-plain] and [AMQP Claims-Based-Security][lnk-cbs].</span></span>

<span data-ttu-id="24dc5-147">En el caso de la seguridad basada en notificaciones AMQP, la norma especifica cómo transmitir estos tokens.</span><span class="sxs-lookup"><span data-stu-id="24dc5-147">If you use AMQP claims-based-security, the standard specifies how to transmit these tokens.</span></span>

<span data-ttu-id="24dc5-148">Para SASL PLAIN, el **nombre de usuario** puede ser:</span><span class="sxs-lookup"><span data-stu-id="24dc5-148">For SASL PLAIN, the **username** can be:</span></span>

* <span data-ttu-id="24dc5-149">`{policyName}@sas.root.{iothubName}` si usa tokens de nivel de centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="24dc5-149">`{policyName}@sas.root.{iothubName}` if using IoT hub-level tokens.</span></span>
* <span data-ttu-id="24dc5-150">`{deviceId}@sas.{iothubname}` si usa tokens de ámbito por el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="24dc5-150">`{deviceId}@sas.{iothubname}` if using device-scoped tokens.</span></span>

<span data-ttu-id="24dc5-151">En ambos casos, el campo de contraseña contiene el token, como se describe en el artículo [Tokens de seguridad][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="24dc5-151">In both cases, the password field contains the token, as described in [IoT Hub security tokens][lnk-sas-tokens].</span></span>

<span data-ttu-id="24dc5-152">HTTP implementa la autenticación mediante la inclusión de un token válido en el encabezado de solicitud **Authorization** .</span><span class="sxs-lookup"><span data-stu-id="24dc5-152">HTTP implements authentication by including a valid token in the **Authorization** request header.</span></span>

#### <a name="example"></a><span data-ttu-id="24dc5-153">Ejemplo</span><span class="sxs-lookup"><span data-stu-id="24dc5-153">Example</span></span>

<span data-ttu-id="24dc5-154">Nombre de usuario (DeviceId distingue entre mayúsculas y minúsculas): `iothubname.azure-devices.net/DeviceId`</span><span class="sxs-lookup"><span data-stu-id="24dc5-154">Username (DeviceId is case-sensitive): `iothubname.azure-devices.net/DeviceId`</span></span>

<span data-ttu-id="24dc5-155">Contraseña (Generar token de SAS con el [Explorador de dispositivos][lnk-device-explorer]): `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span><span class="sxs-lookup"><span data-stu-id="24dc5-155">Password (Generate SAS token with the [device explorer][lnk-device-explorer] tool): `SharedAccessSignature sr=iothubname.azure-devices.net%2fdevices%2fDeviceId&sig=kPszxZZZZZZZZZZZZZZZZZAhLT%2bV7o%3d&se=1487709501`</span></span>

> [!NOTE]
> <span data-ttu-id="24dc5-156">Los [SDK IoT de Azure][lnk-sdks] generan tokens automáticamente cuando se conectan al servicio.</span><span class="sxs-lookup"><span data-stu-id="24dc5-156">The [Azure IoT SDKs][lnk-sdks] automatically generate tokens when connecting to the service.</span></span> <span data-ttu-id="24dc5-157">En algunos casos, los SDK IoT de Azure no admiten todos los protocolos o todos los métodos de autenticación.</span><span class="sxs-lookup"><span data-stu-id="24dc5-157">In some cases, the Azure IoT SDKs do not support all the protocols or all the authentication methods.</span></span>

### <a name="special-considerations-for-sasl-plain"></a><span data-ttu-id="24dc5-158">Consideraciones especiales para SASL PLAIN</span><span class="sxs-lookup"><span data-stu-id="24dc5-158">Special considerations for SASL PLAIN</span></span>

<span data-ttu-id="24dc5-159">Cuando se usa SASL PLAIN con AMQP, un cliente que se conecta a una instancia de IoT Hub puede usar un token único para cada conexión TCP.</span><span class="sxs-lookup"><span data-stu-id="24dc5-159">When using SASL PLAIN with AMQP, a client connecting to an IoT hub can use a single token for each TCP connection.</span></span> <span data-ttu-id="24dc5-160">Cuando el token expira, la conexión TCP se desconecta del servicio y desencadena una reconexión.</span><span class="sxs-lookup"><span data-stu-id="24dc5-160">When the token expires, the TCP connection disconnects from the service and triggers a reconnect.</span></span> <span data-ttu-id="24dc5-161">Este comportamiento, aunque no resulta problemático para una aplicación de back-end, es perjudicial para una aplicación de dispositivo por las razones siguientes:</span><span class="sxs-lookup"><span data-stu-id="24dc5-161">This behavior, while not problematic for a back-end app, is damaging for a device app for the following reasons:</span></span>

* <span data-ttu-id="24dc5-162">Las puertas de enlace normalmente se conectan en nombre de muchos dispositivos.</span><span class="sxs-lookup"><span data-stu-id="24dc5-162">Gateways usually connect on behalf of many devices.</span></span> <span data-ttu-id="24dc5-163">Cuando se usa SASL PLAIN, tienen que crear una conexión TCP distintiva para cada dispositivo que se conecta a un centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="24dc5-163">When using SASL PLAIN, they have to create a distinct TCP connection for each device connecting to an IoT hub.</span></span> <span data-ttu-id="24dc5-164">Este escenario aumenta considerablemente el consumo de energía y de recursos de red, y aumenta la latencia de cada conexión de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="24dc5-164">This scenario considerably increases the consumption of power and networking resources, and increases the latency of each device connection.</span></span>
* <span data-ttu-id="24dc5-165">Los dispositivos con recursos restringidos se ven afectados negativamente por el aumento del uso de recursos para volver a conectarse después de cada expiración del token.</span><span class="sxs-lookup"><span data-stu-id="24dc5-165">Resource-constrained devices are adversely affected by the increased use of resources to reconnect after each token expiration.</span></span>

## <a name="scope-iot-hub-level-credentials"></a><span data-ttu-id="24dc5-166">Restricción de las credenciales de nivel de centro de IoT</span><span class="sxs-lookup"><span data-stu-id="24dc5-166">Scope IoT hub-level credentials</span></span>

<span data-ttu-id="24dc5-167">Puede restringir el ámbito de las directivas de seguridad de nivel de centro de IoT mediante la creación de tokens con un URI de recurso restringido.</span><span class="sxs-lookup"><span data-stu-id="24dc5-167">You can scope IoT hub-level security policies by creating tokens with a restricted resource URI.</span></span> <span data-ttu-id="24dc5-168">Por ejemplo, el punto de conexión para enviar mensajes de dispositivo a nube desde un dispositivo es **/devices/{deviceId}/messages/events**.</span><span class="sxs-lookup"><span data-stu-id="24dc5-168">For example, the endpoint to send device-to-cloud messages from a device is **/devices/{deviceId}/messages/events**.</span></span> <span data-ttu-id="24dc5-169">También puede usar una directiva de acceso compartido de nivel de centro de IoT con permisos **DeviceConnect** para firmar un token cuyo resourceURI sea **/devices/{deviceId}**.</span><span class="sxs-lookup"><span data-stu-id="24dc5-169">You can also use an IoT hub-level shared access policy with **DeviceConnect** permissions to sign a token whose resourceURI is **/devices/{deviceId}**.</span></span> <span data-ttu-id="24dc5-170">Este enfoque crea un token que solo se puede usar para enviar mensajes en nombre del **deviceId**del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="24dc5-170">This approach creates a token that is only usable to send messages on behalf of device **deviceId**.</span></span>

<span data-ttu-id="24dc5-171">Se trata de un mecanismo similar a la [directiva de edición de Event Hubs][lnk-event-hubs-publisher-policy], que permite que se implementen métodos de autenticación personalizados.</span><span class="sxs-lookup"><span data-stu-id="24dc5-171">This mechanism is similar to the [Event Hubs publisher policy][lnk-event-hubs-publisher-policy], and enables you to implement custom authentication methods.</span></span>

## <a name="security-tokens"></a><span data-ttu-id="24dc5-172">Tokens de seguridad</span><span class="sxs-lookup"><span data-stu-id="24dc5-172">Security tokens</span></span>

<span data-ttu-id="24dc5-173">IoT Hub usa tokens de seguridad para autenticar dispositivos y servicios para evitar el envío de claves en la conexión.</span><span class="sxs-lookup"><span data-stu-id="24dc5-173">IoT Hub uses security tokens to authenticate devices and services to avoid sending keys on the wire.</span></span> <span data-ttu-id="24dc5-174">Además, los tokens de seguridad están limitados en cuanto al ámbito y el período de validez.</span><span class="sxs-lookup"><span data-stu-id="24dc5-174">Additionally, security tokens are limited in time validity and scope.</span></span> <span data-ttu-id="24dc5-175">Los [SDK IoT de Azure][lnk-sdks] generan automáticamente tokens sin necesidad de ninguna configuración especial.</span><span class="sxs-lookup"><span data-stu-id="24dc5-175">[Azure IoT SDKs][lnk-sdks] automatically generate tokens without requiring any special configuration.</span></span> <span data-ttu-id="24dc5-176">Algunos escenarios, requieren que el usuario genere y utilice directamente los tokens de seguridad.</span><span class="sxs-lookup"><span data-stu-id="24dc5-176">Some scenarios do require you to generate and use security tokens directly.</span></span> <span data-ttu-id="24dc5-177">Entre los escenarios se incluyen los siguientes:</span><span class="sxs-lookup"><span data-stu-id="24dc5-177">Such scenarios include:</span></span>

* <span data-ttu-id="24dc5-178">El uso directo de las superficies MQTT, AMQP o HTTP.</span><span class="sxs-lookup"><span data-stu-id="24dc5-178">The direct use of the MQTT, AMQP, or HTTP surfaces.</span></span>
* <span data-ttu-id="24dc5-179">La implementación del modelo de servicio de tokens, como se explica en [Personalización de la autenticación de dispositivos][lnk-custom-auth].</span><span class="sxs-lookup"><span data-stu-id="24dc5-179">The implementation of the token service pattern, as explained in [Custom device authentication][lnk-custom-auth].</span></span>

<span data-ttu-id="24dc5-180">IoT Hub también permite a los dispositivos autenticarse con esta plataforma utilizando [certificados X.509][lnk-x509].</span><span class="sxs-lookup"><span data-stu-id="24dc5-180">IoT Hub also allows devices to authenticate with IoT Hub using [X.509 certificates][lnk-x509].</span></span>

### <a name="security-token-structure"></a><span data-ttu-id="24dc5-181">Estructura del token de seguridad</span><span class="sxs-lookup"><span data-stu-id="24dc5-181">Security token structure</span></span>

<span data-ttu-id="24dc5-182">Utilice tokens de seguridad para conceder acceso limitado en tiempo a los dispositivos y servicios en la funcionalidad específica de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="24dc5-182">You use security tokens to grant time-bounded access to devices and services to specific functionality in IoT Hub.</span></span> <span data-ttu-id="24dc5-183">Para obtener autorización para conectarse a IoT Hub, los dispositivos y servicios deben enviar tokens de seguridad firmados con un acceso compartido o una clave simétrica.</span><span class="sxs-lookup"><span data-stu-id="24dc5-183">To get authorization to connect to IoT Hub, devices and services must send security tokens signed with either a shared access or symmetric key.</span></span> <span data-ttu-id="24dc5-184">Dichas claves se almacenan con una identidad de dispositivo en el registro de identidad.</span><span class="sxs-lookup"><span data-stu-id="24dc5-184">These keys are stored with a device identity in the identity registry.</span></span>

<span data-ttu-id="24dc5-185">Un token firmado con una clave de acceso compartido concede acceso a toda la funcionalidad asociada con los permisos de la directiva de acceso compartido.</span><span class="sxs-lookup"><span data-stu-id="24dc5-185">A token signed with a shared access key grants access to all the functionality associated with the shared access policy permissions.</span></span> <span data-ttu-id="24dc5-186">Un token firmado con una clave simétrica de identidad del dispositivo solo concede el permiso **DeviceConnect** para la identidad del dispositivo asociado.</span><span class="sxs-lookup"><span data-stu-id="24dc5-186">A token signed with a device identity's symmetric key only grants the **DeviceConnect** permission for the associated device identity.</span></span>

<span data-ttu-id="24dc5-187">El token de seguridad tiene el formato siguiente:</span><span class="sxs-lookup"><span data-stu-id="24dc5-187">The security token has the following format:</span></span>

`SharedAccessSignature sig={signature-string}&se={expiry}&skn={policyName}&sr={URL-encoded-resourceURI}`

<span data-ttu-id="24dc5-188">Estos son los valores esperados:</span><span class="sxs-lookup"><span data-stu-id="24dc5-188">Here are the expected values:</span></span>

| <span data-ttu-id="24dc5-189">Valor</span><span class="sxs-lookup"><span data-stu-id="24dc5-189">Value</span></span> | <span data-ttu-id="24dc5-190">Description</span><span class="sxs-lookup"><span data-stu-id="24dc5-190">Description</span></span> |
| --- | --- |
| <span data-ttu-id="24dc5-191">{signature}</span><span class="sxs-lookup"><span data-stu-id="24dc5-191">{signature}</span></span> |<span data-ttu-id="24dc5-192">Una cadena de firma HMAC-SHA256 con el formato: `{URL-encoded-resourceURI} + "\n" + expiry`.</span><span class="sxs-lookup"><span data-stu-id="24dc5-192">An HMAC-SHA256 signature string of the form: `{URL-encoded-resourceURI} + "\n" + expiry`.</span></span> <span data-ttu-id="24dc5-193">**Importante**: La clave se descodifica en base64 y se utiliza para realizar el cálculo de HMAC-SHA256.</span><span class="sxs-lookup"><span data-stu-id="24dc5-193">**Important**: The key is decoded from base64 and used as key to perform the HMAC-SHA256 computation.</span></span> |
| <span data-ttu-id="24dc5-194">{resourceURI}</span><span class="sxs-lookup"><span data-stu-id="24dc5-194">{resourceURI}</span></span> |<span data-ttu-id="24dc5-195">Prefijo del identificador URI (por segmento) de los puntos de conexión a los que se puede obtener acceso con este token, que comienza por un nombre de host de IoT Hub (sin protocolo)</span><span class="sxs-lookup"><span data-stu-id="24dc5-195">URI prefix (by segment) of the endpoints that can be accessed with this token, starting with host name of the IoT hub (no protocol).</span></span> <span data-ttu-id="24dc5-196">Por ejemplo: `myHub.azure-devices.net/devices/device1`</span><span class="sxs-lookup"><span data-stu-id="24dc5-196">For example, `myHub.azure-devices.net/devices/device1`</span></span> |
| <span data-ttu-id="24dc5-197">{expiry}</span><span class="sxs-lookup"><span data-stu-id="24dc5-197">{expiry}</span></span> |<span data-ttu-id="24dc5-198">Cadenas UTF8 para el número de segundos transcurridos desde el tiempo 00:00:00 UTC el 1 de enero de 1970.</span><span class="sxs-lookup"><span data-stu-id="24dc5-198">UTF8 strings for number of seconds since the epoch 00:00:00 UTC on 1 January 1970.</span></span> |
| <span data-ttu-id="24dc5-199">{URL-encoded-resourceURI}</span><span class="sxs-lookup"><span data-stu-id="24dc5-199">{URL-encoded-resourceURI}</span></span> |<span data-ttu-id="24dc5-200">Codificación de dirección URL en minúsculas del URI del recurso en minúsculas</span><span class="sxs-lookup"><span data-stu-id="24dc5-200">Lower case URL-encoding of the lower case resource URI</span></span> |
| <span data-ttu-id="24dc5-201">{policyName}</span><span class="sxs-lookup"><span data-stu-id="24dc5-201">{policyName}</span></span> |<span data-ttu-id="24dc5-202">El nombre de la directiva de acceso compartido a la que hace referencia este token.</span><span class="sxs-lookup"><span data-stu-id="24dc5-202">The name of the shared access policy to which this token refers.</span></span> <span data-ttu-id="24dc5-203">Ausente en caso de que el token haga referencia a las credenciales del registro de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="24dc5-203">Absent if the token refers to device-registry credentials.</span></span> |

<span data-ttu-id="24dc5-204">**Nota sobre el prefijo**: el prefijo URI se calcula por segmento y no por carácter.</span><span class="sxs-lookup"><span data-stu-id="24dc5-204">**Note on prefix**: The URI prefix is computed by segment and not by character.</span></span> <span data-ttu-id="24dc5-205">Por ejemplo `/a/b` es un prefijo de `/a/b/c` pero `/a/bc`.</span><span class="sxs-lookup"><span data-stu-id="24dc5-205">For example `/a/b` is a prefix for `/a/b/c` but not for `/a/bc`.</span></span>

<span data-ttu-id="24dc5-206">El siguiente fragmento de Node.js muestra una función denominada **generateSasToken** que calcula el token de las entradas `resourceUri, signingKey, policyName, expiresInMins`.</span><span class="sxs-lookup"><span data-stu-id="24dc5-206">The following Node.js snippet shows a function called **generateSasToken** that computes the token from the inputs `resourceUri, signingKey, policyName, expiresInMins`.</span></span> <span data-ttu-id="24dc5-207">Las secciones siguientes detallan cómo inicializar las entradas diferentes para los distintos casos de uso de token.</span><span class="sxs-lookup"><span data-stu-id="24dc5-207">The next sections detail how to initialize the different inputs for the different token use cases.</span></span>

```nodejs
var generateSasToken = function(resourceUri, signingKey, policyName, expiresInMins) {
    resourceUri = encodeURIComponent(resourceUri);

    // Set expiration in seconds
    var expires = (Date.now() / 1000) + expiresInMins * 60;
    expires = Math.ceil(expires);
    var toSign = resourceUri + '\n' + expires;

    // Use crypto
    var hmac = crypto.createHmac('sha256', new Buffer(signingKey, 'base64'));
    hmac.update(toSign);
    var base64UriEncoded = encodeURIComponent(hmac.digest('base64'));

    // Construct autorization string
    var token = "SharedAccessSignature sr=" + resourceUri + "&sig="
    + base64UriEncoded + "&se=" + expires;
    if (policyName) token += "&skn="+policyName;
    return token;
};
```

<span data-ttu-id="24dc5-208">Como comparación, el código de Python equivalente para generar un token de seguridad es:</span><span class="sxs-lookup"><span data-stu-id="24dc5-208">As a comparison, the equivalent Python code to generate a security token is:</span></span>

```python
from base64 import b64encode, b64decode
from hashlib import sha256
from time import time
from urllib import quote_plus, urlencode
from hmac import HMAC

def generate_sas_token(uri, key, policy_name, expiry=3600):
    ttl = time() + expiry
    sign_key = "%s\n%d" % ((quote_plus(uri)), int(ttl))
    print sign_key
    signature = b64encode(HMAC(b64decode(key), sign_key, sha256).digest())

    rawtoken = {
        'sr' :  uri,
        'sig': signature,
        'se' : str(int(ttl))
    }

    if policy_name is not None:
        rawtoken['skn'] = policy_name

    return 'SharedAccessSignature ' + urlencode(rawtoken)
```

> [!NOTE]
> <span data-ttu-id="24dc5-209">Puesto que el período de validez del token se valida en equipos del IoT Hub, el desfase del reloj del equipo que genera el token debe ser mínimo.</span><span class="sxs-lookup"><span data-stu-id="24dc5-209">Since the time validity of the token is validated on IoT Hub machines, the drift on the clock of the machine that generates the token must be minimal.</span></span>

### <a name="use-sas-tokens-in-a-device-app"></a><span data-ttu-id="24dc5-210">Uso de tokens de SAS en una aplicación de dispositivo</span><span class="sxs-lookup"><span data-stu-id="24dc5-210">Use SAS tokens in a device app</span></span>

<span data-ttu-id="24dc5-211">Existen dos maneras de obtener permisos **DeviceConnect** con IoT Hub mediante tokens de seguridad: con una [clave de dispositivo simétrica del registro de identidad](#use-a-symmetric-key-in-the-identity-registry) o una [clave de acceso compartido](#use-a-shared-access-policy).</span><span class="sxs-lookup"><span data-stu-id="24dc5-211">There are two ways to obtain **DeviceConnect** permissions with IoT Hub with security tokens: use a [symmetric device key from the identity registry](#use-a-symmetric-key-in-the-identity-registry), or use a [shared access key](#use-a-shared-access-policy).</span></span>

<span data-ttu-id="24dc5-212">Recuerde que puede acceder a toda la funcionalidad desde los dispositivos expuestos por diseño en los puntos de conexión con el prefijo `/devices/{deviceId}`.</span><span class="sxs-lookup"><span data-stu-id="24dc5-212">Remember that all functionality accessible from devices is exposed by design on endpoints with prefix `/devices/{deviceId}`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="24dc5-213">La única manera de que IoT Hub autentique un dispositivo específico es usando la clave simétrica de identidad de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="24dc5-213">The only way that IoT Hub authenticates a specific device is using the device identity symmetric key.</span></span> <span data-ttu-id="24dc5-214">En los casos en los que se usa una directiva de acceso compartido para tener acceso a la funcionalidad del dispositivo, la solución debe tener en cuenta el componente que emite el token de seguridad como un subcomponente de confianza.</span><span class="sxs-lookup"><span data-stu-id="24dc5-214">In cases when a shared access policy is used to access device functionality, the solution must consider the component issuing the security token as a trusted subcomponent.</span></span>

<span data-ttu-id="24dc5-215">Los puntos de conexión del dispositivo son (con independencia del protocolo):</span><span class="sxs-lookup"><span data-stu-id="24dc5-215">The device-facing endpoints are (irrespective of the protocol):</span></span>

| <span data-ttu-id="24dc5-216">Extremo</span><span class="sxs-lookup"><span data-stu-id="24dc5-216">Endpoint</span></span> | <span data-ttu-id="24dc5-217">Funcionalidad</span><span class="sxs-lookup"><span data-stu-id="24dc5-217">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices/{deviceId}/messages/events` |<span data-ttu-id="24dc5-218">Envío de mensajes de dispositivo a nube.</span><span class="sxs-lookup"><span data-stu-id="24dc5-218">Send device-to-cloud messages.</span></span> |
| `{iot hub host name}/devices/{deviceId}/devicebound` |<span data-ttu-id="24dc5-219">Recepción de mensajes de nube a dispositivo</span><span class="sxs-lookup"><span data-stu-id="24dc5-219">Receive cloud-to-device messages.</span></span> |

### <a name="use-a-symmetric-key-in-the-identity-registry"></a><span data-ttu-id="24dc5-220">Uso de una clave simétrica en el registro de identidades</span><span class="sxs-lookup"><span data-stu-id="24dc5-220">Use a symmetric key in the identity registry</span></span>

<span data-ttu-id="24dc5-221">Cuando se utiliza la clave simétrica de la identidad de un dispositivo para generar un token, el elemento policyName (`skn`) del token se omite.</span><span class="sxs-lookup"><span data-stu-id="24dc5-221">When using a device identity's symmetric key to generate a token, the policyName (`skn`) element of the token is omitted.</span></span>

<span data-ttu-id="24dc5-222">Por ejemplo, un token creado para tener acceso a toda la funcionalidad de dispositivo debe tener los siguientes parámetros:</span><span class="sxs-lookup"><span data-stu-id="24dc5-222">For example, a token created to access all device functionality should have the following parameters:</span></span>

* <span data-ttu-id="24dc5-223">URI de recurso: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="24dc5-223">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="24dc5-224">clave de firma: cualquier clave simétrica de la identidad `{device id}` ,</span><span class="sxs-lookup"><span data-stu-id="24dc5-224">signing key: any symmetric key for the `{device id}` identity,</span></span>
* <span data-ttu-id="24dc5-225">ningún nombre de directiva,</span><span class="sxs-lookup"><span data-stu-id="24dc5-225">no policy name,</span></span>
* <span data-ttu-id="24dc5-226">cualquier fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="24dc5-226">any expiration time.</span></span>

<span data-ttu-id="24dc5-227">Un ejemplo de cómo utilizar la función anterior de Node.js sería:</span><span class="sxs-lookup"><span data-stu-id="24dc5-227">An example using the preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var deviceKey ="...";

var token = generateSasToken(endpoint, deviceKey, null, 60);
```

<span data-ttu-id="24dc5-228">El resultado, que concede acceso a todas las funcionalidades del dispositivo1, sería:</span><span class="sxs-lookup"><span data-stu-id="24dc5-228">The result, which grants access to all functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697`

> [!NOTE]
> <span data-ttu-id="24dc5-229">Se puede generar un token de SAS mediante la herramienta [Explorador de dispositivos][lnk-device-explorer] de .NET o la utilidad de la línea de comandos [iothub-explorer][lnk-iothub-explorer] basada en nodos y varias plataformas.</span><span class="sxs-lookup"><span data-stu-id="24dc5-229">It is possible to generate a SAS token using the .NET [device explorer][lnk-device-explorer] tool or the cross-platform, node-based [iothub-explorer][lnk-iothub-explorer] command-line utility.</span></span>

### <a name="use-a-shared-access-policy"></a><span data-ttu-id="24dc5-230">Uso de una directiva de acceso compartido</span><span class="sxs-lookup"><span data-stu-id="24dc5-230">Use a shared access policy</span></span>

<span data-ttu-id="24dc5-231">Cuando cree un token a partir de una directiva de acceso compartido, establezca el campo `skn` en el nombre de la directiva.</span><span class="sxs-lookup"><span data-stu-id="24dc5-231">When you create a token from a shared access policy, set the `skn` field to the name of the policy.</span></span> <span data-ttu-id="24dc5-232">Esta directiva debe conceder el permiso **DeviceConnect**.</span><span class="sxs-lookup"><span data-stu-id="24dc5-232">This policy must grant the **DeviceConnect** permission.</span></span>

<span data-ttu-id="24dc5-233">Los dos escenarios principales para utilizar directivas de acceso compartido para tener acceso a la funcionalidad del dispositivo son:</span><span class="sxs-lookup"><span data-stu-id="24dc5-233">The two main scenarios for using shared access policies to access device functionality are:</span></span>

* <span data-ttu-id="24dc5-234">[puertas de enlace del protocolo en la nube][lnk-endpoints],</span><span class="sxs-lookup"><span data-stu-id="24dc5-234">[cloud protocol gateways][lnk-endpoints],</span></span>
* <span data-ttu-id="24dc5-235">[servicios de token][lnk-custom-auth] usados para implementar esquemas de autenticación personalizados.</span><span class="sxs-lookup"><span data-stu-id="24dc5-235">[token services][lnk-custom-auth] used to implement custom authentication schemes.</span></span>

<span data-ttu-id="24dc5-236">Dado que la directiva de acceso compartido potencialmente puede conceder acceso para conectarse a cualquier dispositivo, es importante usar el identificador URI de recurso correcto al crear tokens de seguridad.</span><span class="sxs-lookup"><span data-stu-id="24dc5-236">Since the shared access policy can potentially grant access to connect as any device, it is important to use the correct resource URI when creating security tokens.</span></span> <span data-ttu-id="24dc5-237">Esto es especialmente importante para los servicios de token, que tienen que definir el ámbito de token para un dispositivo específico mediante el identificador URI del recurso.</span><span class="sxs-lookup"><span data-stu-id="24dc5-237">This setting is especially important for token services, which have to scope the token to a specific device using the resource URI.</span></span> <span data-ttu-id="24dc5-238">Este punto es menos relevante para puertas de enlace de protocolo, puesto que ya están mediando el tráfico para todos los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="24dc5-238">This point is less relevant for protocol gateways as they are already mediating traffic for all devices.</span></span>

<span data-ttu-id="24dc5-239">Por ejemplo, un servicio de token que usa acceso compartido creado previamente denominado **dispositivo** crearía un token con los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="24dc5-239">As an example, a token service using the pre-created shared access policy called **device** would create a token with the following parameters:</span></span>

* <span data-ttu-id="24dc5-240">URI de recurso: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span><span class="sxs-lookup"><span data-stu-id="24dc5-240">resource URI: `{IoT hub name}.azure-devices.net/devices/{device id}`,</span></span>
* <span data-ttu-id="24dc5-241">clave de firma: una de las claves de la directiva `device` ,</span><span class="sxs-lookup"><span data-stu-id="24dc5-241">signing key: one of the keys of the `device` policy,</span></span>
* <span data-ttu-id="24dc5-242">nombre de la directiva: `device`,</span><span class="sxs-lookup"><span data-stu-id="24dc5-242">policy name: `device`,</span></span>
* <span data-ttu-id="24dc5-243">cualquier fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="24dc5-243">any expiration time.</span></span>

<span data-ttu-id="24dc5-244">Un ejemplo de cómo utilizar la función anterior de Node.js sería:</span><span class="sxs-lookup"><span data-stu-id="24dc5-244">An example using the preceding Node.js function would be:</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices/device1";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="24dc5-245">El resultado, que concede acceso a todas las funcionalidades del dispositivo1, sería:</span><span class="sxs-lookup"><span data-stu-id="24dc5-245">The result, which grants access to all functionality for device1, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices%2fdevice1&sig=13y8ejUk2z7PLmvtwR5RqlGBOVwiq7rQR3WZ5xZX3N4%3D&se=1456971697&skn=device`

<span data-ttu-id="24dc5-246">Una puerta de enlace de protocolo podría utilizar el mismo token para todos los dispositivos que simplemente establecen el URI de recurso en `myhub.azure-devices.net/devices`.</span><span class="sxs-lookup"><span data-stu-id="24dc5-246">A protocol gateway could use the same token for all devices simply setting the resource URI to `myhub.azure-devices.net/devices`.</span></span>

### <a name="use-security-tokens-from-service-components"></a><span data-ttu-id="24dc5-247">Uso de tokens de seguridad de los componentes de servicio</span><span class="sxs-lookup"><span data-stu-id="24dc5-247">Use security tokens from service components</span></span>

<span data-ttu-id="24dc5-248">Los componentes de servicio solo pueden generar tokens de seguridad mediante directivas de acceso compartido que conceden los permisos apropiados, tal y como se explicó anteriormente.</span><span class="sxs-lookup"><span data-stu-id="24dc5-248">Service components can only generate security tokens using shared access policies granting the appropriate permissions as explained previously.</span></span>

<span data-ttu-id="24dc5-249">Estas son las funciones de servicio expuestas en los puntos de conexión:</span><span class="sxs-lookup"><span data-stu-id="24dc5-249">Here is the service functions exposed on the endpoints:</span></span>

| <span data-ttu-id="24dc5-250">Extremo</span><span class="sxs-lookup"><span data-stu-id="24dc5-250">Endpoint</span></span> | <span data-ttu-id="24dc5-251">Funcionalidad</span><span class="sxs-lookup"><span data-stu-id="24dc5-251">Functionality</span></span> |
| --- | --- |
| `{iot hub host name}/devices` |<span data-ttu-id="24dc5-252">Creación, actualización, recuperación y eliminación de las identidades del dispositivo.</span><span class="sxs-lookup"><span data-stu-id="24dc5-252">Create, update, retrieve, and delete device identities.</span></span> |
| `{iot hub host name}/messages/events` |<span data-ttu-id="24dc5-253">Recepción de mensajes de dispositivo a nube.</span><span class="sxs-lookup"><span data-stu-id="24dc5-253">Receive device-to-cloud messages.</span></span> |
| `{iot hub host name}/servicebound/feedback` |<span data-ttu-id="24dc5-254">Recepción de comentarios para los mensajes de nube a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="24dc5-254">Receive feedback for cloud-to-device messages.</span></span> |
| `{iot hub host name}/devicebound` |<span data-ttu-id="24dc5-255">Envío de mensajes de nube a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="24dc5-255">Send cloud-to-device messages.</span></span> |

<span data-ttu-id="24dc5-256">Por ejemplo, un servicio que genera el uso de la directiva de acceso compartido creada previamente denominada **registryRead** crearía un token con los parámetros siguientes:</span><span class="sxs-lookup"><span data-stu-id="24dc5-256">As an example, a service generating using the pre-created shared access policy called **registryRead** would create a token with the following parameters:</span></span>

* <span data-ttu-id="24dc5-257">URI de recurso: `{IoT hub name}.azure-devices.net/devices`,</span><span class="sxs-lookup"><span data-stu-id="24dc5-257">resource URI: `{IoT hub name}.azure-devices.net/devices`,</span></span>
* <span data-ttu-id="24dc5-258">clave de firma: una de las claves de la directiva `registryRead` ,</span><span class="sxs-lookup"><span data-stu-id="24dc5-258">signing key: one of the keys of the `registryRead` policy,</span></span>
* <span data-ttu-id="24dc5-259">nombre de la directiva: `registryRead`,</span><span class="sxs-lookup"><span data-stu-id="24dc5-259">policy name: `registryRead`,</span></span>
* <span data-ttu-id="24dc5-260">cualquier fecha de expiración.</span><span class="sxs-lookup"><span data-stu-id="24dc5-260">any expiration time.</span></span>

```nodejs
var endpoint ="myhub.azure-devices.net/devices";
var policyName = 'device';
var policyKey = '...';

var token = generateSasToken(endpoint, policyKey, policyName, 60);
```

<span data-ttu-id="24dc5-261">El resultado, que concedería acceso para leer todas las identidades del dispositivo, sería:</span><span class="sxs-lookup"><span data-stu-id="24dc5-261">The result, which would grant access to read all device identities, would be:</span></span>

`SharedAccessSignature sr=myhub.azure-devices.net%2fdevices&sig=JdyscqTpXdEJs49elIUCcohw2DlFDR3zfH5KqGJo4r4%3D&se=1456973447&skn=registryRead`

## <a name="supported-x509-certificates"></a><span data-ttu-id="24dc5-262">Certificados X.509 compatibles</span><span class="sxs-lookup"><span data-stu-id="24dc5-262">Supported X.509 certificates</span></span>

<span data-ttu-id="24dc5-263">Puede usar cualquier certificado X.509 para autenticar dispositivos con IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="24dc5-263">You can use any X.509 certificate to authenticate a device with IoT Hub.</span></span> <span data-ttu-id="24dc5-264">Los certificados incluyen:</span><span class="sxs-lookup"><span data-stu-id="24dc5-264">Certificates include:</span></span>

* <span data-ttu-id="24dc5-265">**Un certificado X.509 existente**.</span><span class="sxs-lookup"><span data-stu-id="24dc5-265">**An existing X.509 certificate**.</span></span> <span data-ttu-id="24dc5-266">Puede que un dispositivo ya tenga un certificado X.509 asociado.</span><span class="sxs-lookup"><span data-stu-id="24dc5-266">A device may already have an X.509 certificate associated with it.</span></span> <span data-ttu-id="24dc5-267">El dispositivo puede usar este certificado para autenticarse con IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="24dc5-267">The device can use this certificate to authenticate with IoT Hub.</span></span>
* <span data-ttu-id="24dc5-268">**Un certificado X-509 autofirmado y generado automáticamente**.</span><span class="sxs-lookup"><span data-stu-id="24dc5-268">**A self-generated and self-signed X-509 certificate**.</span></span> <span data-ttu-id="24dc5-269">Un fabricante de dispositivos o implementador interno pueden generar estos certificados y almacenar la clave privada correspondiente (y el certificado) en el dispositivo.</span><span class="sxs-lookup"><span data-stu-id="24dc5-269">A device manufacturer or in-house deployer can generate these certificates and store the corresponding private key (and certificate) on the device.</span></span> <span data-ttu-id="24dc5-270">Puede usar herramientas como [OpenSSL][lnk-openssl] y la utilidad [Windows SelfSignedCertificate][lnk-selfsigned] para este propósito.</span><span class="sxs-lookup"><span data-stu-id="24dc5-270">You can use tools such as [OpenSSL][lnk-openssl] and [Windows SelfSignedCertificate][lnk-selfsigned] utility for this purpose.</span></span>
* <span data-ttu-id="24dc5-271">**Certificado X.509 firmado por una CA**.</span><span class="sxs-lookup"><span data-stu-id="24dc5-271">**CA-signed X.509 certificate**.</span></span> <span data-ttu-id="24dc5-272">Puede utilizar un certificado X.509 generado y firmado por una entidad de certificación (CA) con el objetivo de identificar un dispositivo y autenticarlo con IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="24dc5-272">To identify a device and authenticate it with IoT Hub, you can use an X.509 certificate generated and signed by a Certification Authority (CA).</span></span> <span data-ttu-id="24dc5-273">IoT Hub solo comprueba que la huella digital presentada coincide con la configurada.</span><span class="sxs-lookup"><span data-stu-id="24dc5-273">IoT Hub only verifies that the thumbprint presented matches the configured thumbprint.</span></span> <span data-ttu-id="24dc5-274">IoT Hub no valida la cadena de certificados.</span><span class="sxs-lookup"><span data-stu-id="24dc5-274">IotHub does not validate the certificate chain.</span></span>

<span data-ttu-id="24dc5-275">Un dispositivo puede usar un token de seguridad o un certificado X.509 para realizar la autenticación, pero no ambos.</span><span class="sxs-lookup"><span data-stu-id="24dc5-275">A device may either use an X.509 certificate or a security token for authentication, but not both.</span></span>

### <a name="register-an-x509-certificate-for-a-device"></a><span data-ttu-id="24dc5-276">Registro de certificados X.509 en un dispositivo</span><span class="sxs-lookup"><span data-stu-id="24dc5-276">Register an X.509 certificate for a device</span></span>

<span data-ttu-id="24dc5-277">El [SDK de servicios IoT de Azure para C#][lnk-service-sdk] (versión 1.0.8 o posterior) permite registrar un dispositivo que utilice un certificado X.509 para realizar la autenticación.</span><span class="sxs-lookup"><span data-stu-id="24dc5-277">The [Azure IoT Service SDK for C#][lnk-service-sdk] (version 1.0.8+) supports registering a device that uses an X.509 certificate for authentication.</span></span> <span data-ttu-id="24dc5-278">Otras API como la importación y exportación de dispositivos también admiten este tipo de certificados.</span><span class="sxs-lookup"><span data-stu-id="24dc5-278">Other APIs such as import/export of devices also support X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="24dc5-279">Compatibilidad con C\#</span><span class="sxs-lookup"><span data-stu-id="24dc5-279">C\# Support</span></span>

<span data-ttu-id="24dc5-280">La clase **RegistryManager** permite registrar dispositivos mediante programación.</span><span class="sxs-lookup"><span data-stu-id="24dc5-280">The **RegistryManager** class provides a programmatic way to register a device.</span></span> <span data-ttu-id="24dc5-281">En concreto, los métodos **AddDeviceAsync** y **UpdateDeviceAsync** le permiten registrar y actualizar un dispositivo en el registro de identidad de IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="24dc5-281">In particular, the **AddDeviceAsync** and **UpdateDeviceAsync** methods enable you to register and update a device in the IoT Hub identity registry.</span></span> <span data-ttu-id="24dc5-282">Estos dos métodos toman una instancia **Device** como entrada.</span><span class="sxs-lookup"><span data-stu-id="24dc5-282">These two methods take a **Device** instance as input.</span></span> <span data-ttu-id="24dc5-283">La clase **Device** incluye una propiedad **Authentication** que permite al usuario especificar huellas digitales de certificados X.509 principales y secundarias.</span><span class="sxs-lookup"><span data-stu-id="24dc5-283">The **Device** class includes an **Authentication** property that allows you to specify primary and secondary X.509 certificate thumbprints.</span></span> <span data-ttu-id="24dc5-284">La huella digital representa un hash SHA-1 del certificado X.509 (que se almacena mediante codificación DER binaria).</span><span class="sxs-lookup"><span data-stu-id="24dc5-284">The thumbprint represents a SHA-1 hash of the X.509 certificate (stored using binary DER encoding).</span></span> <span data-ttu-id="24dc5-285">Los usuarios tienen la opción de especificar una huella digital principal o secundaria, o ambas.</span><span class="sxs-lookup"><span data-stu-id="24dc5-285">You have the option of specifying a primary thumbprint or a secondary thumbprint or both.</span></span> <span data-ttu-id="24dc5-286">Las huellas digitales principales y secundarias se admiten para poder controlar los escenarios de sustitución de certificados.</span><span class="sxs-lookup"><span data-stu-id="24dc5-286">Primary and secondary thumbprints are supported to handle certificate rollover scenarios.</span></span>

> [!NOTE]
> <span data-ttu-id="24dc5-287">IoT Hub no necesita el certificado X.509 completo ni tampoco lo almacena, solo requiere la huella digital.</span><span class="sxs-lookup"><span data-stu-id="24dc5-287">IoT Hub does not require or store the entire X.509 certificate, only the thumbprint.</span></span>

<span data-ttu-id="24dc5-288">A continuación, veremos un fragmento de código C\# de ejemplo para registrar un dispositivo mediante un certificado X.509:</span><span class="sxs-lookup"><span data-stu-id="24dc5-288">Here is a sample C\# code snippet to register a device using an X.509 certificate:</span></span>

```csharp
var device = new Device(deviceId)
{
  Authentication = new AuthenticationMechanism()
  {
    X509Thumbprint = new X509Thumbprint()
    {
      PrimaryThumbprint = "921BC9694ADEB8929D4F7FE4B9A3A6DE58B0790B"
    }
  }
};
RegistryManager registryManager = RegistryManager.CreateFromConnectionString(deviceGatewayConnectionString);
await registryManager.AddDeviceAsync(device);
```

### <a name="use-an-x509-certificate-during-run-time-operations"></a><span data-ttu-id="24dc5-289">Uso de certificados X.509 durante las operaciones en entorno de ejecución</span><span class="sxs-lookup"><span data-stu-id="24dc5-289">Use an X.509 certificate during run-time operations</span></span>

<span data-ttu-id="24dc5-290">El [SDK de dispositivos IoT de Azure para .NET][lnk-client-sdk] (versión 1.0.11 o posterior) permite utilizar certificados X.509.</span><span class="sxs-lookup"><span data-stu-id="24dc5-290">The [Azure IoT device SDK for .NET][lnk-client-sdk] (version 1.0.11+) supports the use of X.509 certificates.</span></span>

### <a name="c-support"></a><span data-ttu-id="24dc5-291">Compatibilidad con C\#</span><span class="sxs-lookup"><span data-stu-id="24dc5-291">C\# Support</span></span>

<span data-ttu-id="24dc5-292">La clase **DeviceAuthenticationWithX509Certificate** permite crear instancias **DeviceClient** mediante un certificado X.509.</span><span class="sxs-lookup"><span data-stu-id="24dc5-292">The class **DeviceAuthenticationWithX509Certificate** supports the creation of **DeviceClient** instances using an X.509 certificate.</span></span> <span data-ttu-id="24dc5-293">El certificado X.509 debe tener el formato PFX (también llamado PKCS #12), que incluye la clave privada.</span><span class="sxs-lookup"><span data-stu-id="24dc5-293">The X.509 certificate must be in the PFX (also called PKCS #12) format that includes the private key.</span></span>

<span data-ttu-id="24dc5-294">A continuación, veremos un fragmento de código de ejemplo:</span><span class="sxs-lookup"><span data-stu-id="24dc5-294">Here is a sample code snippet:</span></span>

```csharp
var authMethod = new DeviceAuthenticationWithX509Certificate("<device id>", x509Certificate);

var deviceClient = DeviceClient.Create("<IotHub DNS HostName>", authMethod);
```

## <a name="custom-device-authentication"></a><span data-ttu-id="24dc5-295">Personalización de la autenticación de dispositivos</span><span class="sxs-lookup"><span data-stu-id="24dc5-295">Custom device authentication</span></span>

<span data-ttu-id="24dc5-296">Puede usar el [registro de identidad][lnk-identity-registry] de IoT Hub para configurar las credenciales de seguridad de cada dispositivo y el control de acceso mediante [tokens][lnk-sas-tokens].</span><span class="sxs-lookup"><span data-stu-id="24dc5-296">You can use the IoT Hub [identity registry][lnk-identity-registry] to configure per-device security credentials and access control using [tokens][lnk-sas-tokens].</span></span> <span data-ttu-id="24dc5-297">Si una solución IoT ya tiene un registro de identidad personalizado y un esquema de autenticación, considere la posibilidad de crear un *servicio de token* para integrar esta infraestructura con IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="24dc5-297">If an IoT solution already has a custom identity registry and/or authentication scheme, consider creating a *token service* to integrate this infrastructure with IoT Hub.</span></span> <span data-ttu-id="24dc5-298">De este modo, puede usar otras características de IoT en la solución.</span><span class="sxs-lookup"><span data-stu-id="24dc5-298">In this way, you can use other IoT features in your solution.</span></span>

<span data-ttu-id="24dc5-299">Un servicio de token es un servicio en la nube personalizado.</span><span class="sxs-lookup"><span data-stu-id="24dc5-299">A token service is a custom cloud service.</span></span> <span data-ttu-id="24dc5-300">Usa una *directiva de acceso compartido* de IoT Hub con permisos **DeviceConnect** para crear *tokens centrados en el dispositivo*.</span><span class="sxs-lookup"><span data-stu-id="24dc5-300">It uses an IoT Hub *shared access policy* with **DeviceConnect** permissions to create *device-scoped* tokens.</span></span> <span data-ttu-id="24dc5-301">Estos tokens permiten que un dispositivo se conecte al centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="24dc5-301">These tokens enable a device to connect to your IoT hub.</span></span>

![Pasos del modelo de servicio de tokens][img-tokenservice]

<span data-ttu-id="24dc5-303">Estos son los pasos principales del modelo de servicio de tokens:</span><span class="sxs-lookup"><span data-stu-id="24dc5-303">Here are the main steps of the token service pattern:</span></span>

1. <span data-ttu-id="24dc5-304">Cree una directiva de acceso compartido de IoT Hub con permisos **DeviceConnect** para IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="24dc5-304">Create an IoT Hub shared access policy with **DeviceConnect** permissions for your IoT hub.</span></span> <span data-ttu-id="24dc5-305">Puede crear esta directiva en [Azure Portal][lnk-management-portal] o mediante programación.</span><span class="sxs-lookup"><span data-stu-id="24dc5-305">You can create this policy in the [Azure portal][lnk-management-portal] or programmatically.</span></span> <span data-ttu-id="24dc5-306">El servicio de tokens usará esta directiva para firmar los tokens que crea.</span><span class="sxs-lookup"><span data-stu-id="24dc5-306">The token service uses this policy to sign the tokens it creates.</span></span>
1. <span data-ttu-id="24dc5-307">Cuando un dispositivo necesita tener acceso al centro de IoT, solicita un token firmado al servicio de tokens.</span><span class="sxs-lookup"><span data-stu-id="24dc5-307">When a device needs to access your IoT hub, it requests a signed token from your token service.</span></span> <span data-ttu-id="24dc5-308">El dispositivo se puede autenticar mediante el esquema de autenticación o registro de identidad personalizado para determinar la identidad del dispositivo que el servicio de token usa para crear el token.</span><span class="sxs-lookup"><span data-stu-id="24dc5-308">The device can authenticate with your custom identity registry/authentication scheme to determine the device identity that the token service uses to create the token.</span></span>
1. <span data-ttu-id="24dc5-309">El servicio de token devuelve un token.</span><span class="sxs-lookup"><span data-stu-id="24dc5-309">The token service returns a token.</span></span> <span data-ttu-id="24dc5-310">El token se crea utilizando `/devices/{deviceId}` como `resourceURI`, con `deviceId` como el dispositivo que se autentica.</span><span class="sxs-lookup"><span data-stu-id="24dc5-310">The token is created by using `/devices/{deviceId}` as `resourceURI`, with `deviceId` as the device being authenticated.</span></span> <span data-ttu-id="24dc5-311">El servicio de token usa la directiva de acceso compartido para construir el token.</span><span class="sxs-lookup"><span data-stu-id="24dc5-311">The token service uses the shared access policy to construct the token.</span></span>
1. <span data-ttu-id="24dc5-312">El dispositivo usa el token directamente con el centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="24dc5-312">The device uses the token directly with the IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="24dc5-313">Puede usar la clase .NET [SharedAccessSignatureBuilder][lnk-dotnet-sas] o la clase de Java [IotHubServiceSasToken][lnk-java-sas] para crear un token en el servicio correspondiente.</span><span class="sxs-lookup"><span data-stu-id="24dc5-313">You can use the .NET class [SharedAccessSignatureBuilder][lnk-dotnet-sas] or the Java class [IotHubServiceSasToken][lnk-java-sas] to create a token in your token service.</span></span>

<span data-ttu-id="24dc5-314">El servicio de token puede establecer la caducidad de los tokens como desee.</span><span class="sxs-lookup"><span data-stu-id="24dc5-314">The token service can set the token expiration as desired.</span></span> <span data-ttu-id="24dc5-315">Cuando expira el token, el centro de IoT interrumpe la conexión de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="24dc5-315">When the token expires, the IoT hub severs the device connection.</span></span> <span data-ttu-id="24dc5-316">A continuación, el dispositivo debe solicitar un nuevo token al servicio de token.</span><span class="sxs-lookup"><span data-stu-id="24dc5-316">Then, the device must request a new token from the token service.</span></span> <span data-ttu-id="24dc5-317">Un tiempo de expiración corto aumenta la carga tanto en el dispositivo como en el servicio de token.</span><span class="sxs-lookup"><span data-stu-id="24dc5-317">A short expiry time increases the load on both the device and the token service.</span></span>

<span data-ttu-id="24dc5-318">Para que un dispositivo se conecte al centro, deberá agregarlo al registro de identidades del centro de IoT aunque ya use un token y no una clave de dispositivo para conectarse.</span><span class="sxs-lookup"><span data-stu-id="24dc5-318">For a device to connect to your hub, you must still add it to the IoT Hub identity registry — even though the device is using a token and not a device key to connect.</span></span> <span data-ttu-id="24dc5-319">Por tanto, puede continuar usando el control de acceso por dispositivo habilitando o deshabilitando las identidades del dispositivo en el [registro de identidad][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="24dc5-319">Therefore, you can continue to use per-device access control by enabling or disabling device identities in the [identity registry][lnk-identity-registry].</span></span> <span data-ttu-id="24dc5-320">Esto mitiga los riesgos de usar tokens con tiempos de expiración largos.</span><span class="sxs-lookup"><span data-stu-id="24dc5-320">This approach mitigates the risks of using tokens with long expiry times.</span></span>

### <a name="comparison-with-a-custom-gateway"></a><span data-ttu-id="24dc5-321">Comparación con una puerta de enlace personalizada</span><span class="sxs-lookup"><span data-stu-id="24dc5-321">Comparison with a custom gateway</span></span>

<span data-ttu-id="24dc5-322">El modelo de servicio de token es el método recomendado para implementar un esquema de autenticación o registro de identidades personalizado en IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="24dc5-322">The token service pattern is the recommended way to implement a custom identity registry/authentication scheme with IoT Hub.</span></span> <span data-ttu-id="24dc5-323">Este modelo se recomienda porque IoT Hub sigue controlando la mayoría del tráfico de la solución.</span><span class="sxs-lookup"><span data-stu-id="24dc5-323">This pattern is recommended because IoT Hub continues to handle most of the solution traffic.</span></span> <span data-ttu-id="24dc5-324">Hay casos, sin embargo, en los que el esquema de autenticación personalizado está tan imbricado con el protocolo que se necesita una *puerta de enlace personalizada* que procese todo el tráfico.</span><span class="sxs-lookup"><span data-stu-id="24dc5-324">However, if the custom authentication scheme is so intertwined with the protocol, you may require a *custom gateway* to process all the traffic.</span></span> <span data-ttu-id="24dc5-325">Un ejemplo de escenario de este tipo es la [seguridad de la capa de transporte (TLS) y las claves previamente compartidas (PSK)][lnk-tls-psk].</span><span class="sxs-lookup"><span data-stu-id="24dc5-325">An example of such a scenario is using[Transport Layer Security (TLS) and pre-shared keys (PSKs)][lnk-tls-psk].</span></span> <span data-ttu-id="24dc5-326">Consulte el tema [Puerta de enlace de protocolos][lnk-protocols] para más información.</span><span class="sxs-lookup"><span data-stu-id="24dc5-326">For more information, see the [protocol gateway][lnk-protocols] topic.</span></span>

## <a name="reference-topics"></a><span data-ttu-id="24dc5-327">Temas de referencia:</span><span class="sxs-lookup"><span data-stu-id="24dc5-327">Reference topics:</span></span>

<span data-ttu-id="24dc5-328">Los siguientes temas de referencia proporcionan más información sobre el control de acceso a su IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="24dc5-328">The following reference topics provide you with more information about controlling access to your IoT hub.</span></span>

## <a name="iot-hub-permissions"></a><span data-ttu-id="24dc5-329">Permisos de IoT Hub</span><span class="sxs-lookup"><span data-stu-id="24dc5-329">IoT Hub permissions</span></span>

<span data-ttu-id="24dc5-330">La tabla siguiente enumera los permisos que se puede utilizar para controlar el acceso a su centro de IoT.</span><span class="sxs-lookup"><span data-stu-id="24dc5-330">The following table lists the permissions you can use to control access to your IoT hub.</span></span>

| <span data-ttu-id="24dc5-331">Permiso</span><span class="sxs-lookup"><span data-stu-id="24dc5-331">Permission</span></span> | <span data-ttu-id="24dc5-332">Notas</span><span class="sxs-lookup"><span data-stu-id="24dc5-332">Notes</span></span> |
| --- | --- |
| <span data-ttu-id="24dc5-333">**RegistryRead**.</span><span class="sxs-lookup"><span data-stu-id="24dc5-333">**RegistryRead**</span></span> |<span data-ttu-id="24dc5-334">Concede acceso de lectura al Registro de identidad.</span><span class="sxs-lookup"><span data-stu-id="24dc5-334">Grants read access to the identity registry.</span></span> <span data-ttu-id="24dc5-335">Para más información, consulte [Registro de identidad][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="24dc5-335">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="24dc5-336">Este permiso se usa en servicios de back-end en la nube.</span><span class="sxs-lookup"><span data-stu-id="24dc5-336">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="24dc5-337">**RegistryReadWrite**.</span><span class="sxs-lookup"><span data-stu-id="24dc5-337">**RegistryReadWrite**</span></span> |<span data-ttu-id="24dc5-338">Concede acceso de lectura y escritura al Registro de identidad.</span><span class="sxs-lookup"><span data-stu-id="24dc5-338">Grants read and write access to the identity registry.</span></span> <span data-ttu-id="24dc5-339">Para más información, consulte [Registro de identidad][lnk-identity-registry].</span><span class="sxs-lookup"><span data-stu-id="24dc5-339">For more information, see [Identity registry][lnk-identity-registry].</span></span> <br/><span data-ttu-id="24dc5-340">Este permiso se usa en servicios de back-end en la nube.</span><span class="sxs-lookup"><span data-stu-id="24dc5-340">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="24dc5-341">**ServiceConnect**.</span><span class="sxs-lookup"><span data-stu-id="24dc5-341">**ServiceConnect**</span></span> |<span data-ttu-id="24dc5-342">Concede acceso a los puntos de conexión de comunicación y supervisión accesibles desde el servicio en la nube.</span><span class="sxs-lookup"><span data-stu-id="24dc5-342">Grants access to cloud service-facing communication and monitoring endpoints.</span></span> <br/><span data-ttu-id="24dc5-343">Concede permiso para recibir mensajes de dispositivo a nube, enviar mensajes de nube a dispositivo y recuperar las confirmaciones de entrega correspondientes.</span><span class="sxs-lookup"><span data-stu-id="24dc5-343">Grants permission to receive device-to-cloud messages, send cloud-to-device messages, and retrieve the corresponding delivery acknowledgments.</span></span> <br/><span data-ttu-id="24dc5-344">Concede permiso para recuperar las confirmaciones de entrega para las cargas de archivos.</span><span class="sxs-lookup"><span data-stu-id="24dc5-344">Grants permission to retrieve delivery acknowledgements for file uploads.</span></span> <br/><span data-ttu-id="24dc5-345">Concede permiso para tener acceso a los dispositivos gemelos para actualizar las etiquetas y las propiedades deseadas, recuperar las propiedades notificadas y ejecutar consultas.</span><span class="sxs-lookup"><span data-stu-id="24dc5-345">Grants permission to access device twins to update tags and desired properties, retrieve reported properties, and run queries.</span></span> <br/><span data-ttu-id="24dc5-346">Este permiso se usa en servicios de back-end en la nube.</span><span class="sxs-lookup"><span data-stu-id="24dc5-346">This permission is used by back-end cloud services.</span></span> |
| <span data-ttu-id="24dc5-347">**DeviceConnect**.</span><span class="sxs-lookup"><span data-stu-id="24dc5-347">**DeviceConnect**</span></span> |<span data-ttu-id="24dc5-348">Concede acceso a los puntos de conexión accesibles desde los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="24dc5-348">Grants access to device-facing endpoints.</span></span> <br/><span data-ttu-id="24dc5-349">Concede permiso para enviar mensajes de dispositivo a nube y recibir mensajes de nube a dispositivo.</span><span class="sxs-lookup"><span data-stu-id="24dc5-349">Grants permission to send device-to-cloud messages and receive cloud-to-device messages.</span></span> <br/><span data-ttu-id="24dc5-350">Concede permiso para realizar la carga de archivos desde un dispositivo.</span><span class="sxs-lookup"><span data-stu-id="24dc5-350">Grants permission to perform file upload from a device.</span></span> <br/><span data-ttu-id="24dc5-351">Concede permiso para recibir notificaciones sobre las propiedades de los dispositivos gemelos que desee y actualizar las propiedades notificadas de esos dispositivos gemelos.</span><span class="sxs-lookup"><span data-stu-id="24dc5-351">Grants permission to receive device twin desired property notifications and update device twin reported properties.</span></span> <br/><span data-ttu-id="24dc5-352">Concede permiso para realizar cargas de archivos.</span><span class="sxs-lookup"><span data-stu-id="24dc5-352">Grants permission to perform file uploads.</span></span> <br/><span data-ttu-id="24dc5-353">Este permiso lo usan los dispositivos.</span><span class="sxs-lookup"><span data-stu-id="24dc5-353">This permission is used by devices.</span></span> |

## <a name="additional-reference-material"></a><span data-ttu-id="24dc5-354">Material de referencia adicional</span><span class="sxs-lookup"><span data-stu-id="24dc5-354">Additional reference material</span></span>

<span data-ttu-id="24dc5-355">Otros temas de referencia en la guía del desarrollador de IoT Hub son los siguientes:</span><span class="sxs-lookup"><span data-stu-id="24dc5-355">Other reference topics in the IoT Hub developer guide include:</span></span>

* <span data-ttu-id="24dc5-356">En [Puntos de conexión de IoT Hub][lnk-endpoints], se describen los diferentes puntos de conexión que expone cada centro de IoT Hub para las operaciones en tiempo de ejecución y de administración.</span><span class="sxs-lookup"><span data-stu-id="24dc5-356">[IoT Hub endpoints][lnk-endpoints] describes the various endpoints that each IoT hub exposes for run-time and management operations.</span></span>
* <span data-ttu-id="24dc5-357">En [Cuotas y limitación][lnk-quotas], se describen las cuotas y el comportamiento de limitación que se aplican al servicio IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="24dc5-357">[Throttling and quotas][lnk-quotas] describes the quotas and throttling behaviors that apply to the IoT Hub service.</span></span>
* <span data-ttu-id="24dc5-358">En [SDK de dispositivo y servicio IoT de Azure][lnk-sdks] se muestran los diversos SDK de lenguaje que puede usar para desarrollar aplicaciones para dispositivo y de servicio que interactúen con IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="24dc5-358">[Azure IoT device and service SDKs][lnk-sdks] lists the various language SDKs you can use when you develop both device and service apps that interact with IoT Hub.</span></span>
* <span data-ttu-id="24dc5-359">En [Lenguaje de consulta de IoT Hub][lnk-query], se describe el lenguaje de consulta que se puede usar para recuperar información de IoT Hub sobre los trabajos y dispositivos gemelos.</span><span class="sxs-lookup"><span data-stu-id="24dc5-359">[IoT Hub query language][lnk-query] describes the query language you can use to retrieve information from IoT Hub about your device twins and jobs.</span></span>
* <span data-ttu-id="24dc5-360">En [Compatibilidad con MQTT de IoT Hub][lnk-devguide-mqtt], se proporciona más información sobre la compatibilidad de IoT Hub con el protocolo MQTT.</span><span class="sxs-lookup"><span data-stu-id="24dc5-360">[IoT Hub MQTT support][lnk-devguide-mqtt] provides more information about IoT Hub support for the MQTT protocol.</span></span>

## <a name="next-steps"></a><span data-ttu-id="24dc5-361">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="24dc5-361">Next steps</span></span>

<span data-ttu-id="24dc5-362">Ahora que ha aprendido a controlar el acceso a IoT Hub, puede interesarle los siguientes temas de la Guía del desarrollador de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="24dc5-362">Now you have learned how to control access IoT Hub, you may be interested in the following IoT Hub developer guide topics:</span></span>

* <span data-ttu-id="24dc5-363">[Uso de dispositivos gemelos para sincronizar el estado y las configuraciones][lnk-devguide-device-twins]</span><span class="sxs-lookup"><span data-stu-id="24dc5-363">[Use device twins to synchronize state and configurations][lnk-devguide-device-twins]</span></span>
* <span data-ttu-id="24dc5-364">[Invocación de un método directo en un dispositivo][lnk-devguide-directmethods]</span><span class="sxs-lookup"><span data-stu-id="24dc5-364">[Invoke a direct method on a device][lnk-devguide-directmethods]</span></span>
* <span data-ttu-id="24dc5-365">[Programación de trabajos en varios dispositivos][lnk-devguide-jobs]</span><span class="sxs-lookup"><span data-stu-id="24dc5-365">[Schedule jobs on multiple devices][lnk-devguide-jobs]</span></span>

<span data-ttu-id="24dc5-366">Si desea probar algunos de los conceptos descritos en este artículo, puede interesarle los siguientes tutoriales de IoT Hub:</span><span class="sxs-lookup"><span data-stu-id="24dc5-366">If you would like to try out some of the concepts described in this article, you may be interested in the following IoT Hub tutorials:</span></span>

* <span data-ttu-id="24dc5-367">[Introducción a Azure IoT Hub][lnk-getstarted-tutorial]</span><span class="sxs-lookup"><span data-stu-id="24dc5-367">[Get started with Azure IoT Hub][lnk-getstarted-tutorial]</span></span>
* <span data-ttu-id="24dc5-368">[Cómo enviar mensajes de la nube a un dispositivo con IoT Hub][lnk-c2d-tutorial]</span><span class="sxs-lookup"><span data-stu-id="24dc5-368">[How to send cloud-to-device messages with IoT Hub][lnk-c2d-tutorial]</span></span>
* <span data-ttu-id="24dc5-369">[Procesamiento de mensajes del dispositivo a la nube de IoT Hub][lnk-d2c-tutorial]</span><span class="sxs-lookup"><span data-stu-id="24dc5-369">[How to process IoT Hub device-to-cloud messages][lnk-d2c-tutorial]</span></span>

<!-- links and images -->

[img-tokenservice]: ./media/iot-hub-devguide-security/tokenservice.png
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
[lnk-openssl]: https://www.openssl.org/
[lnk-selfsigned]: https://technet.microsoft.com/library/hh848633

[lnk-resource-provider-apis]: https://docs.microsoft.com/rest/api/iothub/iothubresource
[lnk-sas-tokens]: iot-hub-devguide-security.md#security-tokens
[lnk-amqp]: https://www.amqp.org/
[lnk-azure-resource-manager]: ../azure-resource-manager/resource-group-overview.md
[lnk-cbs]: https://www.oasis-open.org/committees/download.php/50506/amqp-cbs-v1%200-wd02%202013-08-12.doc
[lnk-event-hubs-publisher-policy]: https://code.msdn.microsoft.com/Service-Bus-Event-Hub-99ce67ab
[lnk-management-portal]: https://portal.azure.com
[lnk-sasl-plain]: http://tools.ietf.org/html/rfc4616
[lnk-identity-registry]: iot-hub-devguide-identity-registry.md
[lnk-dotnet-sas]: https://msdn.microsoft.com/library/microsoft.azure.devices.common.security.sharedaccesssignaturebuilder.aspx
[lnk-java-sas]: https://docs.microsoft.com/java/api/com.microsoft.azure.sdk.iot.service.auth._iot_hub_service_sas_token
[lnk-tls-psk]: https://tools.ietf.org/html/rfc4279
[lnk-protocols]: iot-hub-protocol-gateway.md
[lnk-custom-auth]: iot-hub-devguide-security.md#custom-device-authentication
[lnk-x509]: iot-hub-devguide-security.md#supported-x509-certificates
[lnk-devguide-device-twins]: iot-hub-devguide-device-twins.md
[lnk-devguide-directmethods]: iot-hub-devguide-direct-methods.md
[lnk-devguide-jobs]: iot-hub-devguide-jobs.md
[lnk-service-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/service
[lnk-client-sdk]: https://github.com/Azure/azure-iot-sdk-csharp/tree/master/device
[lnk-device-explorer]: https://github.com/Azure/azure-iot-sdk-csharp/blob/master/tools/DeviceExplorer
[lnk-iothub-explorer]: https://github.com/azure/iothub-explorer

[lnk-getstarted-tutorial]: iot-hub-csharp-csharp-getstarted.md
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
