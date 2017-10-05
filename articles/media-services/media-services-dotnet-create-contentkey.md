---
title: "Creación de claves de contenido con .NET"
description: Aprenda a crear claves de contenido que proporcionen un acceso seguro a los recursos.
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 225b05e5-7d30-409c-b5b7-3ef0634310c7
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 3280a6fcde59bae360da7cb9fea4bb649f984e43
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="create-contentkeys-with-net"></a><span data-ttu-id="a9df2-103">Creación de claves de contenido con .NET</span><span class="sxs-lookup"><span data-stu-id="a9df2-103">Create ContentKeys with .NET</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a9df2-104">REST</span><span class="sxs-lookup"><span data-stu-id="a9df2-104">REST</span></span>](media-services-rest-create-contentkey.md)
> * [<span data-ttu-id="a9df2-105">.NET</span><span class="sxs-lookup"><span data-stu-id="a9df2-105">.NET</span></span>](media-services-dotnet-create-contentkey.md)
> 
> 

<span data-ttu-id="a9df2-106">Servicios multimedia permite crear nuevos recursos y entregar recursos cifrados.</span><span class="sxs-lookup"><span data-stu-id="a9df2-106">Media Services enables you to create and deliver encrypted assets.</span></span> <span data-ttu-id="a9df2-107">Una **ContentKey** proporciona acceso seguro a los **recursos**.</span><span class="sxs-lookup"><span data-stu-id="a9df2-107">A **ContentKey** provides secure access to your **Asset**s.</span></span> 

<span data-ttu-id="a9df2-108">Al crear un nuevo recurso (por ejemplo, antes de [cargar archivos](media-services-dotnet-upload-files.md)), puede especificar las siguientes opciones de cifrado: **StorageEncrypted**, **CommonEncryptionProtected** o **EnvelopeEncryptionProtected**.</span><span class="sxs-lookup"><span data-stu-id="a9df2-108">When you create a new asset (for example, before you [upload files](media-services-dotnet-upload-files.md)), you can specify the following encryption options: **StorageEncrypted**, **CommonEncryptionProtected**, or **EnvelopeEncryptionProtected**.</span></span> 

<span data-ttu-id="a9df2-109">Al entregar recursos a los clientes, puede [configurar que los recursos se cifren de forma dinámica](media-services-dotnet-configure-asset-delivery-policy.md) con uno de los dos cifrados siguientes: **DynamicEnvelopeEncryption** o **DynamicCommonEncryption**.</span><span class="sxs-lookup"><span data-stu-id="a9df2-109">When you deliver assets to your clients, you can [configure for assets to be dynamically encrypted](media-services-dotnet-configure-asset-delivery-policy.md) with one of the following two encryptions: **DynamicEnvelopeEncryption** or **DynamicCommonEncryption**.</span></span>

<span data-ttu-id="a9df2-110">Los recursos cifrados tienen que estar asociados con **ContentKey**.</span><span class="sxs-lookup"><span data-stu-id="a9df2-110">Encrypted assets have to be associated with **ContentKey**s.</span></span> <span data-ttu-id="a9df2-111">En este artículo se describe cómo crear una clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="a9df2-111">This article describes how to create a content key.</span></span>

> [!NOTE]
> <span data-ttu-id="a9df2-112">Al crear un nuevo recurso **StorageEncrypted** con el SDK de Media Services para .NET, se crea automáticamente el valor de **ContentKey** y se vincula al recurso.</span><span class="sxs-lookup"><span data-stu-id="a9df2-112">When creating a new **StorageEncrypted** asset using the Media Services .NET SDK , the **ContentKey** is automatically created and linked with the asset.</span></span>
> 
> 

## <a name="contentkeytype"></a><span data-ttu-id="a9df2-113">ContentKeyType</span><span class="sxs-lookup"><span data-stu-id="a9df2-113">ContentKeyType</span></span>
<span data-ttu-id="a9df2-114">Uno de los valores que debe configurar al crear una clave de contenido es el tipo de clave de contenido.</span><span class="sxs-lookup"><span data-stu-id="a9df2-114">One of the values that you must set when create a content key is the content key type.</span></span> <span data-ttu-id="a9df2-115">Elija uno de los valores siguientes.</span><span class="sxs-lookup"><span data-stu-id="a9df2-115">Choose from one of the following values.</span></span> 

    public enum ContentKeyType
    {
        /// <summary>
        /// Specifies a content key for common encryption.
        /// </summary>
        /// <remarks>This is the default value.</remarks>
        CommonEncryption = 0,

        /// <summary>
        /// Specifies a content key for storage encryption.
        /// </summary>
        StorageEncryption = 1,

        /// <summary>
        /// Specifies a content key for configuration encryption.
        /// </summary>
        ConfigurationEncryption = 2,

        /// <summary>
        /// Specifies a content key for Envelope encryption.  Only used internally.
        /// </summary>
        EnvelopeEncryption = 4
    }

## <span data-ttu-id="a9df2-116"><a id="envelope_contentkey"></a>Crear ContentKey de tipo de sobre</span><span class="sxs-lookup"><span data-stu-id="a9df2-116"><a id="envelope_contentkey"></a>Create envelope type ContentKey</span></span>
<span data-ttu-id="a9df2-117">El siguiente fragmento de código crea una clave de contenido del tipo de cifrado de sobre.</span><span class="sxs-lookup"><span data-stu-id="a9df2-117">The following code snippet creates a content key of the envelope encryption type.</span></span> <span data-ttu-id="a9df2-118">A continuación, asocia la clave con el recurso especificado.</span><span class="sxs-lookup"><span data-stu-id="a9df2-118">It then associates the key with the specified asset.</span></span>

    static public IContentKey CreateEnvelopeTypeContentKey(IAsset asset)
    {
        // Create envelope encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.EnvelopeEncryption);

        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int size)
    {
        byte[] randomBytes = new byte[size];
        using (RNGCryptoServiceProvider rng = new RNGCryptoServiceProvider())
        {
            rng.GetBytes(randomBytes);
        }

        return randomBytes;
    }

<span data-ttu-id="a9df2-119">llamada</span><span class="sxs-lookup"><span data-stu-id="a9df2-119">call</span></span>

    IContentKey key = CreateEnvelopeTypeContentKey(encryptedsset);



## <span data-ttu-id="a9df2-120"><a id="common_contentkey"></a>Crear ContentKey de tipo común</span><span class="sxs-lookup"><span data-stu-id="a9df2-120"><a id="common_contentkey"></a>Create common type ContentKey</span></span>
<span data-ttu-id="a9df2-121">El fragmento de código siguiente crea una clave de contenido del tipo de cifrado común.</span><span class="sxs-lookup"><span data-stu-id="a9df2-121">The following code snippet creates a content key of the common encryption type.</span></span> <span data-ttu-id="a9df2-122">A continuación, asocia la clave con el recurso especificado.</span><span class="sxs-lookup"><span data-stu-id="a9df2-122">It then associates the key with the specified asset.</span></span>

    static public IContentKey CreateCommonTypeContentKey(IAsset asset)
    {
        // Create common encryption content key
        Guid keyId = Guid.NewGuid();
        byte[] contentKey = GetRandomBuffer(16);

        IContentKey key = _context.ContentKeys.Create(
                                keyId,
                                contentKey,
                                "ContentKey",
                                ContentKeyType.CommonEncryption);

        // Associate the key with the asset.
        asset.ContentKeys.Add(key);

        return key;
    }

    static private byte[] GetRandomBuffer(int length)
    {
        var returnValue = new byte[length];

        using (var rng =
            new System.Security.Cryptography.RNGCryptoServiceProvider())
        {
            rng.GetBytes(returnValue);
        }

        return returnValue;
    }
<span data-ttu-id="a9df2-123">llamada</span><span class="sxs-lookup"><span data-stu-id="a9df2-123">call</span></span>

    IContentKey key = CreateCommonTypeContentKey(encryptedsset); 


## <a name="media-services-learning-paths"></a><span data-ttu-id="a9df2-124">Rutas de aprendizaje de Servicios multimedia</span><span class="sxs-lookup"><span data-stu-id="a9df2-124">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="a9df2-125">Envío de comentarios</span><span class="sxs-lookup"><span data-stu-id="a9df2-125">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

