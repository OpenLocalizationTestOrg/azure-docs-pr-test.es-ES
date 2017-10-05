---
title: "Información general de plantillas de licencias de PlayReady de Media Services"
description: "En este tema se ofrece información general sobre la plantilla de licencia de PlayReady que se usó para configurar las licencias de PlayReady."
author: juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: fddce5d0-1278-478f-ae05-9b985c748731
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/29/2017
ms.author: juliako
ms.openlocfilehash: be19f616e36916655390cd05e738e93c08dcdf68
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="media-services-playready-license-template-overview"></a><span data-ttu-id="165fa-103">Información general de plantillas de licencias de PlayReady de Media Services</span><span class="sxs-lookup"><span data-stu-id="165fa-103">Media Services PlayReady license template overview</span></span>
<span data-ttu-id="165fa-104">Servicios multimedia de Azure proporciona un servicio para entregar licencias de Microsoft PlayReady.</span><span class="sxs-lookup"><span data-stu-id="165fa-104">Azure Media Services now provides a service for delivering Microsoft PlayReady licenses.</span></span> <span data-ttu-id="165fa-105">Cuando el reproductor del usuario final (por ejemplo, Silverlight) intenta reproduce el contenido protegido de PlayReady, se envía una solicitud al servicio de entrega de licencias para obtener una licencia.</span><span class="sxs-lookup"><span data-stu-id="165fa-105">When the end user player (for example, Silverlight) tries to play your PlayReady protected content, a request is sent to the license delivery service to obtain a license.</span></span> <span data-ttu-id="165fa-106">Si el servicio de licencia aprueba la solicitud, emite la licencia, la que se envía al cliente y se puede usar para descifrar y reproducir el contenido especificado.</span><span class="sxs-lookup"><span data-stu-id="165fa-106">If the license service approves the request, it issues the license which is sent to the client and can be used to decrypt and play the specified content.</span></span>

<span data-ttu-id="165fa-107">Servicios multimedia también proporciona API que permiten configurar sus licencias de PlayReady.</span><span class="sxs-lookup"><span data-stu-id="165fa-107">Media Services also provides APIs that let you configure your PlayReady licenses.</span></span> <span data-ttu-id="165fa-108">Las licencias contienen los derechos y restricciones que desea para el tiempo de ejecución de DRM de PlayReady con la finalidad de hacer respetar los requisitos cuando un usuario intenta reproducir contenido protegido.</span><span class="sxs-lookup"><span data-stu-id="165fa-108">Licenses contain the rights and restrictions that you want for the PlayReady DRM runtime to enforce when a user is trying to playback protected content.</span></span>
<span data-ttu-id="165fa-109">A continuación se muestran algunos ejemplos de restricciones de licencia de PlayReady que puede especificar:</span><span class="sxs-lookup"><span data-stu-id="165fa-109">Below are some examples of PlayReady license restrictions that you can specify:</span></span>

* <span data-ttu-id="165fa-110">Fecha y hora desde la que la licencia es válida.</span><span class="sxs-lookup"><span data-stu-id="165fa-110">The DateTime from which the license is valid.</span></span>
* <span data-ttu-id="165fa-111">Fecha y hora cuando caduca la licencia.</span><span class="sxs-lookup"><span data-stu-id="165fa-111">The DateTime value when the license expires.</span></span> 
* <span data-ttu-id="165fa-112">Para que la licencia se guarde en un almacenamiento persistente en el cliente.</span><span class="sxs-lookup"><span data-stu-id="165fa-112">For the license to be saved in persistent storage on the client.</span></span> <span data-ttu-id="165fa-113">Las licencias permanentes se usan normalmente para permitir la reproducción sin conexión de contenido.</span><span class="sxs-lookup"><span data-stu-id="165fa-113">Persistent licenses are typically used to allow offline playback of the content.</span></span>
* <span data-ttu-id="165fa-114">El nivel de seguridad mínimo que debe tener un reproductor para reproducir contenido.</span><span class="sxs-lookup"><span data-stu-id="165fa-114">The minimum security level that a player must have to play your content.</span></span> 
* <span data-ttu-id="165fa-115">El nivel de protección de salida de los controles de salida para el contenido de audio y video.</span><span class="sxs-lookup"><span data-stu-id="165fa-115">The output protection level for the output controls for audio\video content.</span></span> 
* <span data-ttu-id="165fa-116">Para obtener más información, consulte la sección Controles de salida (3.5) en el documento [Reglas de cumplimiento normativo de PlayReady](https://www.microsoft.com/playready/licensing/compliance/) .</span><span class="sxs-lookup"><span data-stu-id="165fa-116">For more information, see the Output Controls section (3.5) in the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>

> [!NOTE]
> <span data-ttu-id="165fa-117">Actualmente, solo puede configurar el derecho de reproducción PlayRight de la licencia de PlayReady (este derecho es necesario).</span><span class="sxs-lookup"><span data-stu-id="165fa-117">Currently, you can only configure the PlayRight of the PlayReady license (this right is required).</span></span> <span data-ttu-id="165fa-118">PlayRight da al cliente la capacidad para reproducir el contenido.</span><span class="sxs-lookup"><span data-stu-id="165fa-118">The PlayRight gives the client the ability to playback the content.</span></span> <span data-ttu-id="165fa-119">PlayRight también permite configurar restricciones específicas para la reproducción.</span><span class="sxs-lookup"><span data-stu-id="165fa-119">The PlayRight also allows configuring restrictions specific to playback.</span></span> <span data-ttu-id="165fa-120">Para obtener más información, consulte [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span><span class="sxs-lookup"><span data-stu-id="165fa-120">For more information, see [PlayReadyPlayRight](media-services-playready-license-template-overview.md#PlayReadyPlayRight).</span></span>
> 
> 

<span data-ttu-id="165fa-121">Para configurar licencias de PlayReady con Servicios multimedia, debe configurar la plantilla de licencias de PlayReady de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="165fa-121">To configure PlayReady licenses using Media Services, you must configure the Media Services PlayReady license template.</span></span> <span data-ttu-id="165fa-122">La plantilla se define en XML.</span><span class="sxs-lookup"><span data-stu-id="165fa-122">The template is defined in XML.</span></span>

<span data-ttu-id="165fa-123">En el ejemplo siguiente se muestra la plantilla más sencilla (y común) que configura una licencia básica de streaming.</span><span class="sxs-lookup"><span data-stu-id="165fa-123">The following example shows the simplest (and most common) template that configures a basic streaming license.</span></span> <span data-ttu-id="165fa-124">Con esta licencia, los clientes podrán reproducir contenido protegido con PlayReady.</span><span class="sxs-lookup"><span data-stu-id="165fa-124">With this license, your clients would be able to playback your PlayReady protected content.</span></span>

    <?xml version="1.0" encoding="utf-8"?>
    <PlayReadyLicenseResponseTemplate xmlns:i="http://www.w3.org/2001/XMLSchema-instance" 
                                      xmlns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1">
      <LicenseTemplates>
        <PlayReadyLicenseTemplate>
          <ContentKey i:type="ContentEncryptionKeyFromHeader" />
          <PlayRight />
        </PlayReadyLicenseTemplate>
      </LicenseTemplates>
    </PlayReadyLicenseResponseTemplate>

<span data-ttu-id="165fa-125">El código XML se ajusta al esquema XML de la plantilla de licencias de PlayReady definido en la sección de esquema XML de la plantilla de licencias de PlayReady.</span><span class="sxs-lookup"><span data-stu-id="165fa-125">The XML conforms to the PlayReady license template XML schema defined in the PlayReady license template XML schema section.</span></span>

<span data-ttu-id="165fa-126">Servicios multimedia también define un conjunto de clases de .NET que podría usarse para serializar y deserializar hacia y desde XML.</span><span class="sxs-lookup"><span data-stu-id="165fa-126">Media Services also defines a set of .NET classes that could be used to serialized and deserialized to and from the XML.</span></span> <span data-ttu-id="165fa-127">Para obtener una descripción de las clases principales, vea [Clases .NET de Media Services](media-services-playready-license-template-overview.md#classes).</span><span class="sxs-lookup"><span data-stu-id="165fa-127">For description of main classes, see [Media Services .NET classes](media-services-playready-license-template-overview.md#classes).</span></span> <span data-ttu-id="165fa-128">que se usan para configurar las plantillas de licencia.</span><span class="sxs-lookup"><span data-stu-id="165fa-128">that are used to configure license templates.</span></span>

<span data-ttu-id="165fa-129">Para ver un ejemplo completo que usa clases .NET para configurar la plantilla de licencia de PlayReady, consulte [Uso del cifrado dinámico de PlayReady y servicio de entrega de licencias](media-services-protect-with-drm.md).</span><span class="sxs-lookup"><span data-stu-id="165fa-129">For an end-to-end example that uses .NET classes to configure the PlayReady license template, see [Using PlayReady Dynamic Encryption and License Delivery Service](media-services-protect-with-drm.md).</span></span>

## <span data-ttu-id="165fa-130"><a id="classes"></a>Clases .NET de Servicios multimedia que se usan para configurar las plantillas de licencia</span><span class="sxs-lookup"><span data-stu-id="165fa-130"><a id="classes"></a>Media Services .NET classes that are used to configure license templates</span></span>
<span data-ttu-id="165fa-131">Las siguientes son las clases principales de .NET se usan para configurar las plantillas de licencia de PlayReady de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="165fa-131">The following are the main .NET classes are used to configure Media Services PlayReady license templates.</span></span> <span data-ttu-id="165fa-132">Estas clases se asignan a los tipos definidos en [Esquema XML de plantilla de licencia de PlayReady](media-services-playready-license-template-overview.md#schema).</span><span class="sxs-lookup"><span data-stu-id="165fa-132">These classes map to the types defined in [PlayReady license template XML schema](media-services-playready-license-template-overview.md#schema).</span></span>

<span data-ttu-id="165fa-133">La clase [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) se usa para serializar y deserializar hacia y desde el código XML de la plantilla de licencia de Servicios multimedia.</span><span class="sxs-lookup"><span data-stu-id="165fa-133">The [MediaServicesLicenseTemplateSerializer](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.mediaserviceslicensetemplateserializer.aspx) class is used to serialize and deserialize to and from the Media Services license template XML.</span></span>

### <a name="playreadylicenseresponsetemplate"></a><span data-ttu-id="165fa-134">PlayReadyLicenseResponseTemplate</span><span class="sxs-lookup"><span data-stu-id="165fa-134">PlayReadyLicenseResponseTemplate</span></span>
<span data-ttu-id="165fa-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) : esta clase representa la plantilla para la respuesta que se devuelve al usuario final.</span><span class="sxs-lookup"><span data-stu-id="165fa-135">[PlayReadyLicenseResponseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicenseresponsetemplate.aspx) - This class represents the template for the response sent back to the end user.</span></span> <span data-ttu-id="165fa-136">Contiene un campo para una cadena de datos personalizada entre el servidor de licencias y la aplicación (puede ser útil para la lógica de aplicación personalizada), así como una lista de una o más plantillas de licencia.</span><span class="sxs-lookup"><span data-stu-id="165fa-136">It contains a field for a custom data string between the license server and the application (may be useful for custom app logic) as well as a list of one or more license templates.</span></span>

<span data-ttu-id="165fa-137">Esta es la clase de "nivel superior" en la jerarquía de plantillas.</span><span class="sxs-lookup"><span data-stu-id="165fa-137">This is the “top level” class in the template hierarchy.</span></span> <span data-ttu-id="165fa-138">Lo que significa que la plantilla de respuesta incluye una lista de plantillas de licencia y las plantillas de licencia incluyen (directa o indirectamente) todas las demás clases que conforman los datos de la plantilla que se va a serializar.</span><span class="sxs-lookup"><span data-stu-id="165fa-138">Meaning that the response template includes a list of license templates and the license templates include (directly or indirectly) all of the other classes that make up the template data to be serialized.</span></span>

### <a name="playreadylicensetemplate"></a><span data-ttu-id="165fa-139">PlayReadyLicenseTemplate</span><span class="sxs-lookup"><span data-stu-id="165fa-139">PlayReadyLicenseTemplate</span></span>
<span data-ttu-id="165fa-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) : la clase representa una plantilla de licencia para crear licencias de PlayReady que se devuelven a los usuarios finales.</span><span class="sxs-lookup"><span data-stu-id="165fa-140">[PlayReadyLicenseTemplate](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadylicensetemplate.aspx) - The class represents a license template for creating PlayReady licenses to be returned to the end users.</span></span> <span data-ttu-id="165fa-141">Contiene los datos de la clave de contenido de la licencia y los derechos o restricciones que el tiempo de ejecución DRM de PlayReady debe aplicar cuando use la clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="165fa-141">It contains the data on the content key in the license and any rights or restrictions to be enforced by the PlayReady DRM runtime when using the content key.</span></span>

### <span data-ttu-id="165fa-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span><span class="sxs-lookup"><span data-stu-id="165fa-142"><a id="PlayReadyPlayRight"></a>PlayReadyPlayRight</span></span>
<span data-ttu-id="165fa-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) : esta clase representa el derecho PlayRight de una licencia de PlayReady.</span><span class="sxs-lookup"><span data-stu-id="165fa-143">[PlayReadyPlayRight](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.mediaservices.client.contentkeyauthorization.playreadyplayright.aspx) - This class represents the PlayRight of a PlayReady license.</span></span> <span data-ttu-id="165fa-144">Concede al usuario la capacidad de reproducir contenido sujeto a las restricciones configuradas en la licencia y en el propio derecho PlayRight (para la directiva de reproducción específica).</span><span class="sxs-lookup"><span data-stu-id="165fa-144">It grants the user the ability to playback the content subject to the zero or more restrictions configured in the license and on the PlayRight itself (for playback specific policy).</span></span> <span data-ttu-id="165fa-145">En lo referente a PlayRight, gran parte de la directiva tiene que ver con las restricciones de salida que controlan los tipos de salida sobre los que se puede reproducir el contenido y las restricciones que se deben aplicar cuando se usa una salida determinada.</span><span class="sxs-lookup"><span data-stu-id="165fa-145">Much of the policy on the PlayRight has to do with output restrictions which control the types of outputs that the content can be played over and any restrictions that must be put in place when using a given output.</span></span> <span data-ttu-id="165fa-146">Por ejemplo, si DigitalVideoOnlyContentRestriction está habilitada, el tiempo de ejecución DRM solo permitirá que el vídeo se muestre mostrarse en salidas digitales (las salidas de vídeo analógicas no podrán pasar el contenido).</span><span class="sxs-lookup"><span data-stu-id="165fa-146">For example, if the DigitalVideoOnlyContentRestriction is enabled, then the DRM runtime will only allow the video to be displayed over digital outputs (analog video outputs won’t be allowed to pass the content).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="165fa-147">Estos tipos de restricciones pueden ser muy eficaces, pero también pueden afectar a la experiencia del consumidor.</span><span class="sxs-lookup"><span data-stu-id="165fa-147">These types of restrictions can be very powerful but can also affect the consumer experience.</span></span> <span data-ttu-id="165fa-148">Si las protecciones de salida son demasiado restrictivas, puede que el contenido no se reproduzca en algunos clientes.</span><span class="sxs-lookup"><span data-stu-id="165fa-148">If the output protections are configured too restrictive, the content might be unplayable on some clients.</span></span> <span data-ttu-id="165fa-149">Para más información, consulte el documento [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) .</span><span class="sxs-lookup"><span data-stu-id="165fa-149">For more information, see the [PlayReady Compliance Rules](https://www.microsoft.com/playready/licensing/compliance/) document.</span></span>
> 
> 

<span data-ttu-id="165fa-150">Para ver un ejemplo de los niveles de protección que admite Silverlight, consulte: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span><span class="sxs-lookup"><span data-stu-id="165fa-150">For an example of what protection levels Silverlight supports, see: [Silverlight support for output protections](http://go.microsoft.com/fwlink/?LinkId=617318).</span></span>

## <span data-ttu-id="165fa-151"><a id="schema"></a>Esquema XML de la plantilla de licencia de PlayReady</span><span class="sxs-lookup"><span data-stu-id="165fa-151"><a id="schema"></a>PlayReady license template XML schema</span></span>
    <?xml version="1.0" encoding="utf-8"?>
    <xs:schema xmlns:tns="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:ser="http://schemas.microsoft.com/2003/10/Serialization/" elementFormDefault="qualified" targetNamespace="http://schemas.microsoft.com/Azure/MediaServices/KeyDelivery/PlayReadyTemplate/v1" xmlns:xs="http://www.w3.org/2001/XMLSchema">
      <xs:import namespace="http://schemas.microsoft.com/2003/10/Serialization/" />
      <xs:complexType name="AgcAndColorStripeRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction" />
      <xs:simpleType name="ContentType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Unspecified" />
          <xs:enumeration value="UltravioletDownload" />
          <xs:enumeration value="UltravioletStreaming" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="ContentType" nillable="true" type="tns:ContentType" />
      <xs:complexType name="ExplicitAnalogTelevisionRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="BestEffort" type="xs:boolean" />
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ExplicitAnalogTelevisionRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction" />
      <xs:complexType name="PlayReadyContentKey">
        <xs:sequence />
      </xs:complexType>
      <xs:element name="PlayReadyContentKey" nillable="true" type="tns:PlayReadyContentKey" />
      <xs:complexType name="ContentEncryptionKeyFromHeader">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence />
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromHeader" nillable="true" type="tns:ContentEncryptionKeyFromHeader" />
      <xs:complexType name="ContentEncryptionKeyFromKeyIdentifier">
        <xs:complexContent mixed="false">
          <xs:extension base="tns:PlayReadyContentKey">
            <xs:sequence>
              <xs:element minOccurs="0" name="KeyIdentifier" type="ser:guid" />
            </xs:sequence>
          </xs:extension>
        </xs:complexContent>
      </xs:complexType>
      <xs:element name="ContentEncryptionKeyFromKeyIdentifier" nillable="true" type="tns:ContentEncryptionKeyFromKeyIdentifier" />
      <xs:complexType name="PlayReadyLicenseResponseTemplate">
        <xs:sequence>
          <xs:element name="LicenseTemplates" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
          <xs:element minOccurs="0" name="ResponseCustomData" nillable="true" type="xs:string">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseResponseTemplate" nillable="true" type="tns:PlayReadyLicenseResponseTemplate" />
      <xs:complexType name="ArrayOfPlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" maxOccurs="unbounded" name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ArrayOfPlayReadyLicenseTemplate" nillable="true" type="tns:ArrayOfPlayReadyLicenseTemplate" />
      <xs:complexType name="PlayReadyLicenseTemplate">
        <xs:sequence>
          <xs:element minOccurs="0" name="AllowTestDevices" type="xs:boolean" />
          <xs:element minOccurs="0" name="BeginDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element name="ContentKey" nillable="true" type="tns:PlayReadyContentKey" />
          <xs:element minOccurs="0" name="ContentType" type="tns:ContentType">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExpirationDate" nillable="true" type="xs:dateTime">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="GracePeriod" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="LicenseType" type="tns:PlayReadyLicenseType" />
          <xs:element minOccurs="0" name="PlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyLicenseTemplate" nillable="true" type="tns:PlayReadyLicenseTemplate" />
      <xs:simpleType name="PlayReadyLicenseType">
        <xs:restriction base="xs:string">
          <xs:enumeration value="Nonpersistent" />
          <xs:enumeration value="Persistent" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="PlayReadyLicenseType" nillable="true" type="tns:PlayReadyLicenseType" />
      <xs:complexType name="PlayReadyPlayRight">
        <xs:sequence>
          <xs:element minOccurs="0" name="AgcAndColorStripeRestriction" nillable="true" type="tns:AgcAndColorStripeRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AllowPassingVideoContentToUnknownOutput" type="tns:UnknownOutputPassingOption">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="AnalogVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="CompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="DigitalVideoOnlyContentRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ExplicitAnalogTelevisionOutputRestriction" nillable="true" type="tns:ExplicitAnalogTelevisionRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="FirstPlayExpiration" nillable="true" type="ser:duration">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComponentVideoRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ImageConstraintForAnalogComputerMonitorRestriction" type="xs:boolean">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalAudioOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
          <xs:element minOccurs="0" name="UncompressedDigitalVideoOpl" nillable="true" type="xs:int">
            <xs:annotation>
              <xs:appinfo>
                <DefaultValue EmitDefaultValue="false" xmlns="http://schemas.microsoft.com/2003/10/Serialization/" />
              </xs:appinfo>
            </xs:annotation>
          </xs:element>
        </xs:sequence>
      </xs:complexType>
      <xs:element name="PlayReadyPlayRight" nillable="true" type="tns:PlayReadyPlayRight" />
      <xs:simpleType name="UnknownOutputPassingOption">
        <xs:restriction base="xs:string">
          <xs:enumeration value="NotAllowed" />
          <xs:enumeration value="Allowed" />
          <xs:enumeration value="AllowedWithVideoConstriction" />
        </xs:restriction>
      </xs:simpleType>
      <xs:element name="UnknownOutputPassingOption" nillable="true" type="tns:UnknownOutputPassingOption" />
      <xs:complexType name="ScmsRestriction">
        <xs:sequence>
          <xs:element minOccurs="0" name="ConfigurationData" type="xs:unsignedByte" />
        </xs:sequence>
      </xs:complexType>
      <xs:element name="ScmsRestriction" nillable="true" type="tns:ScmsRestriction" />
    </xs:schema>



## <a name="media-services-learning-paths"></a><span data-ttu-id="165fa-152">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="165fa-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="165fa-153">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="165fa-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

