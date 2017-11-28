---
title: "Introducción a Azure Table Storage | Microsoft Docs"
description: "Almacene datos estructurados en la nube con el Almacenamiento de tablas de Azure, un almacén de datos NoSQL."
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jhubbard
editor: tysonn
ms.assetid: fe46d883-7bed-49dd-980e-5c71df36adb3
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 08/23/2017
ms.author: mimig
ms.openlocfilehash: 9099e90c402185b371495379db943d64fb82cdb8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 08/29/2017
---
# <a name="azure-table-storage-overview"></a><span data-ttu-id="b0307-103">Introducción a Azure Table Storage</span><span class="sxs-lookup"><span data-stu-id="b0307-103">Azure Table storage overview</span></span>

[!INCLUDE [storage-table-cosmos-db-tip-include](../../includes/storage-table-cosmos-db-tip-include.md)]

<span data-ttu-id="b0307-104">Azure Table Storage es un servicio que almacena datos NoSQL estructurados en la nube y proporciona un almacén de claves y atributos con un diseño sin esquema.</span><span class="sxs-lookup"><span data-stu-id="b0307-104">Azure Table storage is a service that stores structured NoSQL data in the cloud, providing a key/attribute store with a schemaless design.</span></span> <span data-ttu-id="b0307-105">Como Almacenamiento de tablas carece de esquema, es fácil adaptar los datos a medida que evolucionan las necesidades de la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b0307-105">Because Table storage is schemaless, it's easy to adapt your data as the needs of your application evolve.</span></span> <span data-ttu-id="b0307-106">El acceso a los datos de Table Storage es rápido y rentable para muchos tipos de aplicaciones y, por lo general, el costo es normalmente menor que con el SQL tradicional para volúmenes parecidos de datos.</span><span class="sxs-lookup"><span data-stu-id="b0307-106">Access to Table storage data is fast and cost-effective for many types of applications, and is typically lower in cost than traditional SQL for similar volumes of data.</span></span>

<span data-ttu-id="b0307-107">Table Storage se puede usar para almacenar conjuntos de datos flexibles, como datos de usuarios para aplicaciones web, libretas de direcciones, información de dispositivos u otros tipos de metadatos que el servicio requiera.</span><span class="sxs-lookup"><span data-stu-id="b0307-107">You can use Table storage to store flexible datasets like user data for web applications, address books, device information, or other types of metadata your service requires.</span></span> <span data-ttu-id="b0307-108">Una tabla puede almacenar un número cualquiera de entidades y una cuenta de almacenamiento puede incluir un número cualquiera de tablas, hasta alcanzar el límite de capacidad de este tipo de cuenta.</span><span class="sxs-lookup"><span data-stu-id="b0307-108">You can store any number of entities in a table, and a storage account may contain any number of tables, up to the capacity limit of the storage account.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

## <a name="next-steps"></a><span data-ttu-id="b0307-109">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="b0307-109">Next steps</span></span>

* <span data-ttu-id="b0307-110">El [Explorador de Microsoft Azure Storage](../vs-azure-tools-storage-manage-with-storage-explorer.md) es una aplicación independiente y gratuita de Microsoft que permite trabajar visualmente con los datos de Azure Storage en Windows, macOS y Linux.</span><span class="sxs-lookup"><span data-stu-id="b0307-110">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>

* [<span data-ttu-id="b0307-111">Introducción a Azure Table Storage mediante .NET</span><span class="sxs-lookup"><span data-stu-id="b0307-111">Getting Started with Azure Table Storage in .NET</span></span>](table-storage-how-to-use-dotnet.md)

* <span data-ttu-id="b0307-112">Consulte la documentación de referencia del servicio de tabla para obtener información detallada acerca de las API disponibles:</span><span class="sxs-lookup"><span data-stu-id="b0307-112">View the Table service reference documentation for complete details about available APIs:</span></span>

    * [<span data-ttu-id="b0307-113">Referencia de la biblioteca de clientes de almacenamiento para .NET</span><span class="sxs-lookup"><span data-stu-id="b0307-113">Storage Client Library for .NET reference</span></span>](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)

    * [<span data-ttu-id="b0307-114">Referencia de API de REST</span><span class="sxs-lookup"><span data-stu-id="b0307-114">REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
