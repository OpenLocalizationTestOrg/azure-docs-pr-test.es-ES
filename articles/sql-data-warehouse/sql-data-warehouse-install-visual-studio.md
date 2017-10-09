---
title: aaaInstall Visual Studio como SSDT para almacenamiento de datos SQL | Documentos de Microsoft
description: "Instalación de herramientas de desarrollo de Visual Studio y SQL Server Data Tools (SSDT) para Almacenamiento de datos SQL de Azure"
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 0ed9b406-9b42-4fe6-b963-fe0a5b48aac1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 03/30/2017
ms.author: anvang;barbkess
ms.openlocfilehash: cf49c13d5cab598ed127f5702c04168b62ede0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="f0a55-103">Instalación de Visual Studio y SSDT para SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f0a55-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="f0a55-104">aplicaciones de toodevelop para almacenamiento de datos de SQL, se recomienda usar versión más reciente de Hola de Visual Studio con la versión más reciente de Hola de SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="f0a55-104">toodevelop applications for SQL Data Warehouse, we recommend using hello most recent version of Visual Studio with hello most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="f0a55-105">También se admite Visual Studio 2013 Update 5 con SSDT por compatibilidad con versiones anteriores.</span><span class="sxs-lookup"><span data-stu-id="f0a55-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="f0a55-106">Con Visual Studio con SSDT, podrá toouse Hola Explorador de objetos de SQL Server toovisually explorar las tablas, vistas, procedimientos almacenados y muchos más objetos en el almacenamiento de datos de SQL, así como ejecutar consultas.</span><span class="sxs-lookup"><span data-stu-id="f0a55-106">Using Visual Studio with SSDT will allow you toouse hello SQL Server Object Explorer toovisually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="f0a55-107">Almacenamiento de datos SQL no es compatible aún con proyectos de base de datos de Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f0a55-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span>  <span data-ttu-id="f0a55-108">Esta característica se agregará en una versión futura.</span><span class="sxs-lookup"><span data-stu-id="f0a55-108">This feature will be added in a future version.</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="f0a55-109">Paso 1: Instalación de Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f0a55-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="f0a55-110">Siga estos toodownload vínculos e instalar Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f0a55-110">Follow these links toodownload and install Visual Studio.</span></span> <span data-ttu-id="f0a55-111">Si ya tiene Visual Studio 2013 o posterior instalado, puede omitir tooStep 2, instale SSDT.</span><span class="sxs-lookup"><span data-stu-id="f0a55-111">If you already have Visual Studio 2013 or later installed, you can skip tooStep 2, install SSDT.</span></span>

1. <span data-ttu-id="f0a55-112">[Descargue Visual Studio][].</span><span class="sxs-lookup"><span data-stu-id="f0a55-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="f0a55-113">Siga hello [instalar Visual Studio] [ Installing Visual Studio] guía en MSDN y elija las configuraciones predeterminadas de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0a55-113">Follow hello [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose hello default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="f0a55-114">Paso 2: Instalación de SSDT</span><span class="sxs-lookup"><span data-stu-id="f0a55-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="f0a55-115">tooinstall SSDT para Visual Studio simplemente busque una actualización SSDT desde dentro de Visual Studio, siga estos pasos.</span><span class="sxs-lookup"><span data-stu-id="f0a55-115">tooinstall SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="f0a55-116">En Visual Studio, haga clic en **Herramientas** / **Extensiones y actualizaciones...**</span><span class="sxs-lookup"><span data-stu-id="f0a55-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="f0a55-117"> / **Actualizaciones**</span><span class="sxs-lookup"><span data-stu-id="f0a55-117"> / **Updates**</span></span>
2. <span data-ttu-id="f0a55-118">Seleccione **Actualizaciones de productos** y busque la actualización **Microsoft SQL Server Update para herramientas de base de datos**.</span><span class="sxs-lookup"><span data-stu-id="f0a55-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="f0a55-119">Si no se encuentra una actualización, debe tener instalado de versión más reciente de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0a55-119">If an update is not found, then you should have hello latest version installed.</span></span>  <span data-ttu-id="f0a55-120">tooconfirm SSDT está instalado, haga clic en **ayuda** / **acerca de Microsoft Visual Studio** y buscar las herramientas de datos de SQL Server en la lista de Hola.</span><span class="sxs-lookup"><span data-stu-id="f0a55-120">tooconfirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in hello list.</span></span>  <span data-ttu-id="f0a55-121">versión más reciente de Hola de SSDT es 14.0.60525.0.</span><span class="sxs-lookup"><span data-stu-id="f0a55-121">hello latest version of SSDT is 14.0.60525.0.</span></span>  <span data-ttu-id="f0a55-122">Si Hola opción tooinstall no está disponible en Visual Studio, o bien, puede visitar hello [de descarga de SSDT] [ SSDT Download] página toodownload e instale SSDT manualmente.</span><span class="sxs-lookup"><span data-stu-id="f0a55-122">If hello option tooinstall is not available from Visual Studio, alternatively you can visit hello [SSDT Download][SSDT Download] page toodownload and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0a55-123">Pasos siguientes</span><span class="sxs-lookup"><span data-stu-id="f0a55-123">Next steps</span></span>
<span data-ttu-id="f0a55-124">Ahora que tiene la versión más reciente de Hola de SSDT, está listo demasiado[conectar] [ connect] tooyour almacenamiento de datos SQL.</span><span class="sxs-lookup"><span data-stu-id="f0a55-124">Now that you have hello latest version of SSDT, you are ready too[connect][connect] tooyour SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Descargue Visual Studio]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
