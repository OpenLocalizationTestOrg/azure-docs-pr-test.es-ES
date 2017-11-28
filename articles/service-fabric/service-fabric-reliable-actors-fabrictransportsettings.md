---
title: "Cambio de la configuración de FabricTransport en microservicios de Azure | Microsoft Docs"
description: "Obtenga información sobre cómo configurar las opciones de comunicación de Azure Service Fabric Actor."
services: Service-Fabric
documentationcenter: .net
author: suchiagicha
manager: timlt
editor: 
ms.assetid: dbed72f4-dda5-4287-bd56-da492710cd96
ms.service: Service-Fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/20/2017
ms.author: suchiagicha
ms.openlocfilehash: 75bdd4644f4ccc583271b9169c50a375e2cd6629
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="configure-fabrictransport-settings-for-reliable-actors"></a><span data-ttu-id="22ae8-103">Configuración de FabricTransport de Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="22ae8-103">Configure FabricTransport settings for Reliable Actors</span></span>

<span data-ttu-id="22ae8-104">Estos son los valores que puede configurar:</span><span class="sxs-lookup"><span data-stu-id="22ae8-104">Here are the settings that you can configure:</span></span>
- <span data-ttu-id="22ae8-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="22ae8-105">C#: [FabricTransportRemotingSettings](
https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>
- <span data-ttu-id="22ae8-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span><span class="sxs-lookup"><span data-stu-id="22ae8-106">Java: [FabricTransportRemotingSettings](https://docs.microsoft.com/java/api/microsoft.servicefabric.services.remoting.fabrictransport._fabric_transport_remoting_settings)</span></span>

<span data-ttu-id="22ae8-107">Puede modificar la configuración predeterminada de FabricTransport de las maneras siguientes.</span><span class="sxs-lookup"><span data-stu-id="22ae8-107">You can modify the default configuration of FabricTransport in following ways.</span></span>

## <a name="assembly-attribute"></a><span data-ttu-id="22ae8-108">Atributo de ensamblado</span><span class="sxs-lookup"><span data-stu-id="22ae8-108">Assembly attribute</span></span>

<span data-ttu-id="22ae8-109">El atributo [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) debe aplicarse en los ensamblados del cliente de actor y del servicio de actor.</span><span class="sxs-lookup"><span data-stu-id="22ae8-109">The [FabricTransportActorRemotingProvider](https://docs.microsoft.com/en-us/dotnet/api/microsoft.servicefabric.actors.remoting.fabrictransport.fabrictransportactorremotingproviderattribute?redirectedfrom=MSDN#microsoft_servicefabric_actors_remoting_fabrictransport_fabrictransportactorremotingproviderattribute) attribute needs to be applied on the actor client and actor service assemblies.</span></span>

<span data-ttu-id="22ae8-110">En el ejemplo siguiente se muestra cómo cambiar el valor predeterminado de la configuración de FabricTransport OperationTimeout:</span><span class="sxs-lookup"><span data-stu-id="22ae8-110">The following example shows how to change the default value of FabricTransport OperationTimeout settings:</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600)]
   ```

   <span data-ttu-id="22ae8-111">En el segundo ejemplo se cambian de forma predeterminada los valores de FabricTransport MaxMessageSize y OperationTimeoutInSeconds.</span><span class="sxs-lookup"><span data-stu-id="22ae8-111">Second example changes default Values of FabricTransport MaxMessageSize and OperationTimeoutInSeconds.</span></span>

  ```csharp
    using Microsoft.ServiceFabric.Actors.Remoting.FabricTransport;
    [assembly:FabricTransportActorRemotingProvider(OperationTimeoutInSeconds = 600,MaxMessageSize = 134217728)]
   ```

## <a name="config-package"></a><span data-ttu-id="22ae8-112">Paquete de configuración</span><span class="sxs-lookup"><span data-stu-id="22ae8-112">Config package</span></span>

<span data-ttu-id="22ae8-113">Puede usar un [paquete de configuración](service-fabric-application-model.md) para modificar la configuración predeterminada.</span><span class="sxs-lookup"><span data-stu-id="22ae8-113">You can use a [config package](service-fabric-application-model.md) to modify the default configuration.</span></span>

### <a name="configure-fabrictransport-settings-for-the-actor-service"></a><span data-ttu-id="22ae8-114">Configuración del valor de FabricTransport para el servicio de actor</span><span class="sxs-lookup"><span data-stu-id="22ae8-114">Configure FabricTransport settings for the actor service</span></span>

<span data-ttu-id="22ae8-115">Agregue una sección TransportSettings en el archivo settings.xml.</span><span class="sxs-lookup"><span data-stu-id="22ae8-115">Add a TransportSettings section in the settings.xml file.</span></span>

<span data-ttu-id="22ae8-116">De forma predeterminada, el código de actor busca SectionName como "&lt;ActorName&gt;TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="22ae8-116">By default, actor code looks for SectionName as "&lt;ActorName&gt;TransportSettings".</span></span> <span data-ttu-id="22ae8-117">Si no se encuentra, busca SectionName como "TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="22ae8-117">If that's not found, it checks for SectionName as "TransportSettings".</span></span>

  ```xml
  <Section Name="MyActorServiceTransportSettings">
       <Parameter Name="MaxMessageSize" Value="10000000" />
       <Parameter Name="OperationTimeoutInSeconds" Value="300" />
       <Parameter Name="SecurityCredentialsType" Value="X509" />
       <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
       <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
       <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
       <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
       <Parameter Name="CertificateStoreName" Value="My" />
       <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
       <Parameter Name="CertificateRemoteCommonNames" Value="ServiceFabric-Test-Cert" />
   </Section>
  ```

### <a name="configure-fabrictransport-settings-for-the-actor-client-assembly"></a><span data-ttu-id="22ae8-118">Configuración del valor de FabricTransport para el ensamblado de cliente de actor</span><span class="sxs-lookup"><span data-stu-id="22ae8-118">Configure FabricTransport settings for the actor client assembly</span></span>

<span data-ttu-id="22ae8-119">Si el cliente no se está ejecutando como parte de un servicio, puede crear un archivo "&lt;Nombre del ejecutable del cliente&gt;.settings.xml" en la misma ubicación donde se encuentra el archivo .exe del cliente.</span><span class="sxs-lookup"><span data-stu-id="22ae8-119">If the client is not running as part of a service, you can create a "&lt;Client Exe Name&gt;.settings.xml" file in the same location as the client .exe file.</span></span> <span data-ttu-id="22ae8-120">A continuación, cree una sección TransportSettings en ese archivo.</span><span class="sxs-lookup"><span data-stu-id="22ae8-120">Then add a TransportSettings section in that file.</span></span> <span data-ttu-id="22ae8-121">SectionName debe ser "TransportSettings".</span><span class="sxs-lookup"><span data-stu-id="22ae8-121">SectionName should be "TransportSettings".</span></span>

  ```xml
  <?xml version="1.0" encoding="utf-8"?>
  <Settings xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://schemas.microsoft.com/2011/01/fabric">
    <Section Name="TransportSettings">
      <Parameter Name="SecurityCredentialsType" Value="X509" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
      <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
      <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
      <Parameter Name="OperationTimeoutInSeconds" Value="300" />
      <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
      <Parameter Name="CertificateStoreName" Value="My" />
      <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
      <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    </Section>
  </Settings>
   ```

  * <span data-ttu-id="22ae8-122">Configuración de los ajustes de FabricTransport para cliente/servicio de actor seguros con certificado secundario.</span><span class="sxs-lookup"><span data-stu-id="22ae8-122">Configuring FabricTransport Settings for Secure Actor Service/Client With Secondary Certificate.</span></span>
  <span data-ttu-id="22ae8-123">Puede agregar información de certificado secundario mediante la adición del parámetro CertificateFindValuebySecondary.</span><span class="sxs-lookup"><span data-stu-id="22ae8-123">Secondary certificate information can be added by adding parameter CertificateFindValuebySecondary.</span></span>
  <span data-ttu-id="22ae8-124">A continuación se muestra el ejemplo para TransportSettings del agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="22ae8-124">Below is the example for the Listener TransportSettings.</span></span>

    ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateFindValuebySecondary" Value="h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateRemoteThumbprints" Value="4FEF3950642138446CC364A396E1E881DB76B48C,a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
     <span data-ttu-id="22ae8-125">A continuación se muestra el ejemplo para TransportSettings del cliente.</span><span class="sxs-lookup"><span data-stu-id="22ae8-125">Below is the example for the Client TransportSettings.</span></span>

    ```xml
   <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindByThumbprint" />
    <Parameter Name="CertificateFindValue" Value="4FEF3950642138446CC364A396E1E881DB76B48C" />
    <Parameter Name="CertificateFindValuebySecondary" Value="a9449b018d0f6839a2c5d62b5b6c6ac822b6f667" />
    <Parameter Name="CertificateRemoteThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662,h9449b018d0f6839a2c5d62b5b6c6ac822b6f690" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
    * <span data-ttu-id="22ae8-126">Configuración de los ajustes de FabricTransport para la protección del cliente/servicio de actor con el nombre de sujeto.</span><span class="sxs-lookup"><span data-stu-id="22ae8-126">Configuring FabricTransport  Settings for Securing Actor Service/Client Using Subject Name.</span></span>
    <span data-ttu-id="22ae8-127">El usuario tiene que proporcionar findType como valores FindBySubjectName,add CertificateIssuerThumbprints y CertificateRemoteCommonNames.</span><span class="sxs-lookup"><span data-stu-id="22ae8-127">User needs to provide findType as FindBySubjectName,add CertificateIssuerThumbprints and CertificateRemoteCommonNames values.</span></span>
  <span data-ttu-id="22ae8-128">A continuación se muestra el ejemplo para TransportSettings del agente de escucha.</span><span class="sxs-lookup"><span data-stu-id="22ae8-128">Below is the example for the Listener TransportSettings.</span></span>

     ```xml
    <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateIssuerThumbprints" Value="b3449b018d0f6839a2c5d62b5b6c6ac822b6f662" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
    ```
  <span data-ttu-id="22ae8-129">A continuación se muestra el ejemplo para TransportSettings del cliente.</span><span class="sxs-lookup"><span data-stu-id="22ae8-129">Below is the example for the Client TransportSettings.</span></span>

    ```xml
     <Section Name="TransportSettings">
    <Parameter Name="SecurityCredentialsType" Value="X509" />
    <Parameter Name="CertificateFindType" Value="FindBySubjectName" />
    <Parameter Name="CertificateFindValue" Value="CN = WinFabric-Test-SAN1-Bob" />
    <Parameter Name="CertificateStoreLocation" Value="LocalMachine" />
    <Parameter Name="CertificateStoreName" Value="My" />
    <Parameter Name="CertificateRemoteCommonNames" Value="WinFabric-Test-SAN1-Alice" />
    <Parameter Name="CertificateProtectionLevel" Value="EncryptAndSign" />
    </Section>
     ```
