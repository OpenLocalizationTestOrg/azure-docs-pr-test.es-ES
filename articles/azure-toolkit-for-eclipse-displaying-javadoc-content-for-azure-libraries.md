---
title: "Visualización del contenido de Javadoc en Eclipse para el paquete de bibliotecas de Azure para Java"
description: "Cómo mostrar el contenido de Javadoc para las bibliotecas de Azure en Eclipse"
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 30f8b6a1-1d76-4d1c-861b-1db478c46e6b
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: b44deb773b2159cba1d5d957455409f10fc49334
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 07/11/2017
---
# <a name="displaying-javadoc-content-in-eclipse-for-the-azure-libraries-package-for-java"></a><span data-ttu-id="0d82c-103">Visualización del contenido de Javadoc en Eclipse para el paquete de bibliotecas de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="0d82c-103">Displaying Javadoc Content in Eclipse for the Azure Libraries Package for Java</span></span>
<span data-ttu-id="0d82c-104">El contenido de Javadoc de las bibliotecas de Azure para Java se puede ver en el entorno de Eclipse asociando el contenido de Javadoc a las bibliotecas de Azure para Java.</span><span class="sxs-lookup"><span data-stu-id="0d82c-104">The Javadoc content for the Azure Libraries for Java can be viewed within your Eclipse environment by associating the Javadoc content to the Azure Libraries for Java.</span></span> <span data-ttu-id="0d82c-105">En los pasos siguientes se muestra cómo usar esta funcionalidad en Eclipse.</span><span class="sxs-lookup"><span data-stu-id="0d82c-105">The following steps show you how to use this functionality within Eclipse.</span></span>

<span data-ttu-id="0d82c-106">Este procedimiento supone que ya ha agregado la biblioteca de Azure para Java a su ruta de acceso de compilación.</span><span class="sxs-lookup"><span data-stu-id="0d82c-106">This procedure assumes you have already added the Azure Library for Java to your build path.</span></span>

## <a name="to-display-javadoc-content-in-eclipse-for-the-azure-libraries-for-java"></a><span data-ttu-id="0d82c-107">Para mostrar el contenido de Javadoc en Eclipse para las bibliotecas de Azure para Java</span><span class="sxs-lookup"><span data-stu-id="0d82c-107">To display Javadoc content in Eclipse for the Azure Libraries for Java</span></span>
* <span data-ttu-id="0d82c-108">En el Explorador de proyectos de Eclipse, en la sección del proyecto **Bibliotecas de referencia** , abra el menú contextual de la biblioteca de Azure para JAR de Java.</span><span class="sxs-lookup"><span data-stu-id="0d82c-108">Within Eclipse's Project Explorer, in the **Referenced Libraries** section of your project, open the context menu for the Azure Library for Java JAR.</span></span> <span data-ttu-id="0d82c-109">Por ejemplo, **microsoft-windowsazure-api-0.1.0.jar** (el número de versión puede ser diferente, en función de la versión que haya instalado).</span><span class="sxs-lookup"><span data-stu-id="0d82c-109">For example, **microsoft-windowsazure-api-0.1.0.jar** (the version number may be different, dependent upon which version you have installed).</span></span>

* <span data-ttu-id="0d82c-110">Haga clic en **Propiedades**.</span><span class="sxs-lookup"><span data-stu-id="0d82c-110">Click **Properties**.</span></span>

* <span data-ttu-id="0d82c-111">En el cuadro de diálogo **Properties** (Propiedades), en el panel izquierdo, haga clic en **Javadoc Location** (Ubicación de Javadoc).</span><span class="sxs-lookup"><span data-stu-id="0d82c-111">Within the **Properties** dialog, in the left-hand pane, click **Javadoc Location**.</span></span> <span data-ttu-id="0d82c-112">Aparecerá el cuadro de diálogo **Ubicación de Javadoc** .</span><span class="sxs-lookup"><span data-stu-id="0d82c-112">The **Javadoc Location** dialog is displayed.</span></span>

* <span data-ttu-id="0d82c-113">Puede especificar una **Javadoc URL** (URL de Javadoc) o un **Javadoc in archive** (Javadoc en archivo).</span><span class="sxs-lookup"><span data-stu-id="0d82c-113">You can specify a **Javadoc URL**, or a **Javadoc in archive**.</span></span>

   * <span data-ttu-id="0d82c-114">Si decide especificar una **URL de Javadoc**, use las direcciones URL como **http://dl.windowsazure.com/javadoc** o **http://dl.windowsazure.com/storage/javadoc**.</span><span class="sxs-lookup"><span data-stu-id="0d82c-114">If you choose to specify a **Javadoc URL**, use the URLs such as **http://dl.windowsazure.com/javadoc** or **http://dl.windowsazure.com/storage/javadoc**.</span></span>

   * <span data-ttu-id="0d82c-115">Si decide usar **Javadoc en archivo**, puede especificar un archivo externo o un archivo de área de trabajo.</span><span class="sxs-lookup"><span data-stu-id="0d82c-115">If you choose to use **Javadoc in archive**, you can specify an external file, or a workspace file.</span></span>

   <span data-ttu-id="0d82c-116">Realice su elección y examine o valide según sea necesario.</span><span class="sxs-lookup"><span data-stu-id="0d82c-116">Make your choice and browse/validate as needed.</span></span> <span data-ttu-id="0d82c-117">En el ejemplo siguiente se asocian las bibliotecas de Azure para Java con el JAR de Javadoc correspondiente que se ha descargado localmente en una carpeta denominada **c:\MyAzureJARs**.</span><span class="sxs-lookup"><span data-stu-id="0d82c-117">The following example associates the Azure Libraries for Java with the corresponding Javadoc JAR that has been downloaded locally to a folder named **c:\MyAzureJARs**.</span></span>

   ![][ic553487]

* <span data-ttu-id="0d82c-118">*Paso opcional*: haga clic en **Validar**.</span><span class="sxs-lookup"><span data-stu-id="0d82c-118">*Optional Step*: Click **Validate**.</span></span> <span data-ttu-id="0d82c-119">Aquí podrían mostrarse posibles problemas con el JAR de Javadoc.</span><span class="sxs-lookup"><span data-stu-id="0d82c-119">Potential issues with the Javadoc JAR could be displayed here.</span></span>

* <span data-ttu-id="0d82c-120">Haga clic en **Aceptar**.</span><span class="sxs-lookup"><span data-stu-id="0d82c-120">Click **OK**.</span></span>

<span data-ttu-id="0d82c-121">Una vez asociado a la biblioteca, el contenido de Javadoc debe mostrarse dentro del IDE de Eclipse.</span><span class="sxs-lookup"><span data-stu-id="0d82c-121">Once associated with the library, the Javadoc content should display within your Eclipse IDE.</span></span> <span data-ttu-id="0d82c-122">Por ejemplo, si `blob` se define del tipo `CloudBlockBlob` dentro de su código, el siguiente es un ejemplo del contenido de Javadoc que aparece cuando escribe `blob.acquireLease` en el código:</span><span class="sxs-lookup"><span data-stu-id="0d82c-122">For example, if `blob` is defined of type `CloudBlockBlob` within your code, the following is an example of Javadoc content that appears when you type `blob.acquireLease` in code:</span></span>

![][ic553488]

## <a name="see-also"></a><span data-ttu-id="0d82c-123">Otras referencias</span><span class="sxs-lookup"><span data-stu-id="0d82c-123">See Also</span></span>
<span data-ttu-id="0d82c-124">[Kit de herramientas de Azure para Eclipse][Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0d82c-124">[Azure Toolkit for Eclipse][Azure Toolkit for Eclipse]</span></span>

<span data-ttu-id="0d82c-125">[Creación de una aplicación Hola a todos para Azure en Eclipse][Creating a Hello World Application for Azure in Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0d82c-125">[Creating a Hello World Application for Azure in Eclipse][Creating a Hello World Application for Azure in Eclipse]</span></span>

<span data-ttu-id="0d82c-126">[Instalación del Kit de herramientas de Azure para Eclipse][Installing the Azure Toolkit for Eclipse]</span><span class="sxs-lookup"><span data-stu-id="0d82c-126">[Installing the Azure Toolkit for Eclipse][Installing the Azure Toolkit for Eclipse]</span></span> 

<span data-ttu-id="0d82c-127">Para obtener más información sobre el uso de Azure con Java, vea el [Centro para desarrolladores de Java de Azure][Azure Java Developer Center].</span><span class="sxs-lookup"><span data-stu-id="0d82c-127">For more information about using Azure with Java, see the [Azure Java Developer Center][Azure Java Developer Center].</span></span>

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Creating a Hello World Application for Azure in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699533
[Installing the Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546

<!-- IMG List -->

[ic553487]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553487.png
[ic553488]: ./media/azure-toolkit-for-eclipse-displaying-javadoc-content-for-azure-libraries/ic553488.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh698319.aspx -->
