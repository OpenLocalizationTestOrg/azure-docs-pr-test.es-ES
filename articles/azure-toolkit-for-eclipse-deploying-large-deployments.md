---
title: aaaDeploying implementaciones a gran escala
description: "Obtenga información acerca de cómo toodeploy grandes implementaciones mediante hello Azure Toolkit for Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 5e18bace-5df0-4af8-ad86-6151ea8bd823
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 6b1d2a7a5e49c78154fc856a221e64ca8dcfbe9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/06/2017
---
# <a name="deploying-large-deployments"></a><span data-ttu-id="b4bea-103">Implementación de implementaciones de gran tamaño</span><span class="sxs-lookup"><span data-stu-id="b4bea-103">Deploying Large Deployments</span></span>
<span data-ttu-id="b4bea-104">Si la implementación es demasiado grande toobe contenido en la carpeta approot de hello predeterminada, puede usar un recurso de almacenamiento local como carpeta raíz de implementación de hello para el JDK y servidor de aplicaciones.</span><span class="sxs-lookup"><span data-stu-id="b4bea-104">If your deployment is too large toobe contained in hello default approot folder, you can use a local storage resource as hello deployment root folder for your JDK and application server.</span></span>

## <a name="toouse-a-local-storage-resource-as-hello-deployment-root-folder-for-large-deployments"></a><span data-ttu-id="b4bea-105">toouse un recurso de almacenamiento local como carpeta de raíz de la implementación de Hola para implementaciones a grandes escala</span><span class="sxs-lookup"><span data-stu-id="b4bea-105">toouse a local storage resource as hello deployment root folder for large deployments</span></span>
1. <span data-ttu-id="b4bea-106">Cree un recurso de almacenamiento local nuevo.</span><span class="sxs-lookup"><span data-stu-id="b4bea-106">Create a new local storage resource.</span></span> <span data-ttu-id="b4bea-107">nombre de Hello del recurso de hello no importa.</span><span class="sxs-lookup"><span data-stu-id="b4bea-107">hello name of hello resource does not matter.</span></span> <span data-ttu-id="b4bea-108">Recursos de almacenamiento se definen en el nivel de rol de Hola.</span><span class="sxs-lookup"><span data-stu-id="b4bea-108">Storage resources are defined at hello role level.</span></span> <span data-ttu-id="b4bea-109">Hello más rápida forma tooaccess Hola almacenamiento local configuración cuadro de diálogo, desde el que puede crear un nuevo recurso de almacenamiento local, es mediante el uso de pasos de hello: menú contextual rol de Hola Hola **el Explorador de proyectos** vista (expanda su Proyecto de Azure nodo si no ve el rol de hello), haga clic en **Azure**y, a continuación, haga clic en **almacenamiento Local**.</span><span class="sxs-lookup"><span data-stu-id="b4bea-109">hello quickest way tooaccess hello local storage configuration dialog, from which you could create a new local storage resource, is by using hello following steps: Right-click hello role in hello **Project Explorer** view (expand your Azure project node if you don't see hello role), click **Azure**, and then click **Local Storage**.</span></span> <span data-ttu-id="b4bea-110">Dentro de hello **almacenamiento Local** cuadro de diálogo, haga clic en **agregar** toocreate un nuevo recurso de almacenamiento local.</span><span class="sxs-lookup"><span data-stu-id="b4bea-110">Within hello **Local Storage** dialog, click **Add** toocreate a new local storage resource.</span></span>

2. <span data-ttu-id="b4bea-111">Hola conjunto deseado tamaño tooat menos 2048 MB (nada menos, podría ocasionar Hola mismos problemas de tamaño de archivo que se encontraría en approot hello).</span><span class="sxs-lookup"><span data-stu-id="b4bea-111">Set hello desired size tooat least 2048 MB (anything less may cause hello same file size problems as you would encounter in hello approot).</span></span>

3. <span data-ttu-id="b4bea-112">Asegúrese de que **limpiar contenido hello cuando se recicla la instancia de rol de hello** está activa; Esto le ayudará a impedir que se ejecute en conflicto con los archivos existentes en el recurso de hello lógica de inicio de la implementación de Hola Hola al rol se recicla la instancia.</span><span class="sxs-lookup"><span data-stu-id="b4bea-112">Ensure that **Clean hello contents when hello role instance is recycled** is checked; this will help prevent hello deployment's startup logic from running into conflicts with pre-existing files in hello resource when hello role instance is recycled.</span></span>

4. <span data-ttu-id="b4bea-113">Asegúrese de que hello **almacenar variables de entorno Hola ruta de acceso del recurso después de la implementación** valor se establece la cadena de toohello **DEPLOYROOT**.</span><span class="sxs-lookup"><span data-stu-id="b4bea-113">Ensure that hello **Environment variable storing hello resource's directory path after deployment** value is set toohello string **DEPLOYROOT**.</span></span> <span data-ttu-id="b4bea-114">El cuadro de diálogo de recursos de almacenamiento local tendrá un aspecto similar a continuación toohello.</span><span class="sxs-lookup"><span data-stu-id="b4bea-114">Your local storage resource dialog will look similar toohello following.</span></span>

   ![][ic667943]

<span data-ttu-id="b4bea-115">O bien, si utiliza **DEPLOYROOT** como hello *nombre* de su recurso local y no cambiar nombre de variable de entorno generados automáticamente de hello (que se establecerá demasiado **DEPLOYROOT_PATH** en ese caso), que podría funcionar para la aplicación.</span><span class="sxs-lookup"><span data-stu-id="b4bea-115">Alternatively, if you use **DEPLOYROOT** as hello *name* of your local resource and you do not change hello automatically-generated environment variable name (which will be set too**DEPLOYROOT_PATH** in that case), that would work for your application as well.</span></span>

<span data-ttu-id="b4bea-116">Encontrará información adicional sobre la creación de un recurso de almacenamiento local en [Propiedades de almacenamiento local][Local storage properties].</span><span class="sxs-lookup"><span data-stu-id="b4bea-116">Additional information about creating a local storage resource can be found at [Local storage properties][Local storage properties].</span></span>

## <a name="see-also"></a><span data-ttu-id="b4bea-117">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="b4bea-117">See Also</span></span>
<span data-ttu-id="b4bea-118">[Kit de herramientas de Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b4bea-118">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="b4bea-119">[Creación de una aplicación Hola a todos para Azure en Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b4bea-119">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="b4bea-120">[Instalar hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="b4bea-120">[Installing hello Azure Toolkit for Eclipse][Installing hello Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="b4bea-121">Para obtener más información acerca del uso de Azure con Java, vea hello [Centro para desarrolladores de Java de Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="b4bea-121">For more information about using Azure with Java, see hello [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Local storage properties]: http://go.microsoft.com/fwlink/?LinkID=699525#local_storage_properties

<!-- IMG List -->

[ic667943]: ./media/azure-toolkit-for-eclipse-deploying-large-deployments/ic667943.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/dn268601.aspx -->
